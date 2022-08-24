---
title: Configurazione di Microsoft Dynamics OData
seo-title: Microsoft Dynamics ODtata configuration
description: Utilizza, integra e lavora con i servizi Microsoft Dynamics online e on-premise tramite il modello dati del modulo.
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Configurazione di Microsoft Dynamics OData{#microsoft-dynamics-odata-configuration}

![integrazione dei dati](assets/data-integeration.png)

Microsoft Dynamics è un software di gestione delle relazioni con i clienti (CRM) e Enterprise Resource Planning (ERP) che fornisce soluzioni aziendali per la creazione e la gestione di account cliente, contatti, lead, opportunità e casi. [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md) fornisce una configurazione del servizio cloud OData per integrare Forms con il server Microsoft Dynamics online e on-premise. Consente di creare un modello dati modulo basato su entità, attributi e servizi definiti nel servizio Microsoft Dynamics. Il modello dati del modulo può essere utilizzato per creare moduli adattivi che interagiscono con il server Microsoft Dynamics per abilitare i flussi di lavoro aziendali. Esempio:

* Query del server Microsoft Dynamics per dati e precompilazione dei moduli adattivi
* Inserire dati in Microsoft Dynamics per l’invio di moduli adattivi
* Scrivere dati in Microsoft Dynamics tramite entità personalizzate definite nel modello dati del modulo e viceversa

Il pacchetto aggiuntivo di AEM Forms include anche la configurazione di riferimento di OData che puoi sfruttare per integrare rapidamente Microsoft Dynamics con AEM Forms.

Quando il pacchetto è installato, le seguenti entità e servizi sono disponibili nella tua istanza AEM Forms:

* Cloud Service MS Dynamics OData (servizio OData)
* Modello dati per moduli con entità e servizi Microsoft Dynamics preconfigurati.

Le entità e i servizi Microsoft Dynamics preconfigurati in un modello dati modulo sono disponibili nell’istanza AEM Forms solo se la modalità di esecuzione per l’istanza AEM è impostata come `samplecontent` (predefinito). Il Cloud Service MS Dynamics OData (OData Service) è disponibile anche con altre modalità di esecuzione. Per ulteriori informazioni sulla configurazione delle modalità di esecuzione per un&#39;istanza AEM, vedi [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md).

## Prerequisiti {#prerequisites}

Prima di iniziare a configurare e configurare Microsoft Dynamics, assicurati di disporre di:

* Installato il [Pacchetto aggiuntivo di AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Microsoft Dynamics 365 configurato online o installato un’istanza di una delle seguenti versioni di Microsoft Dynamics:

   * Microsoft Dynamics 365 on-premise
   * Microsoft Dynamics 2016 on-premise

* [Registrazione dell&#39;applicazione per il servizio online Microsoft Dynamics con Microsoft Azure Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Prendi nota dei valori dell’ID client (noto anche come ID applicazione) e del segreto client per il servizio registrato. Questi valori vengono utilizzati mentre [configurazione del servizio cloud per il servizio Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Imposta URL di risposta per l’applicazione Microsoft Dynamics registrata {#set-reply-url-for-registered-microsoft-dynamics-application}

Per impostare l’URL di risposta per l’applicazione Microsoft Dynamics registrata, procedi come segue:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l’integrazione di AEM Forms con il server online Microsoft Dynamics.

1. Vai all’account Microsoft Azure Active Directory e aggiungi l’URL di configurazione del servizio cloud seguente in **URL di risposta** impostazioni per l&#39;applicazione registrata:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Directory di Azure](assets/azure_directory_new.png)

1. Salva la configurazione.

## Configurazione di Microsoft Dynamics per IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics utilizza l’autenticazione basata sulle attestazioni per fornire l’accesso ai dati sul server Microsoft Dynamics CRM a utenti esterni. Per abilitare questa opzione, procedi come segue per configurare Microsoft Dynamics per la distribuzione su Internet (IFD) e configurare le impostazioni di attestazione.

>[!NOTE]
>
>Utilizzare questa procedura solo durante l’integrazione di AEM Forms con il server Microsoft Dynamics locale.

1. Configura l’istanza on-premise di Microsoft Dynamics per IFD come descritto in [Configurare IFD per Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Esegui i seguenti comandi utilizzando Windows PowerShell per configurare le impostazioni delle attestazioni su Microsoft Dynamics abilitato per IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Vedi [Registrazione app per CRM on-premise (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) per i dettagli.

## Configurare il client OAuth sul computer AD FS {#configure-oauth-client-on-ad-fs-machine}

Per registrare un client OAuth nel computer Active Directory Federation Services (AD FS) e concedere l&#39;accesso al computer AD FS, procedere come segue:

>[!NOTE]
>
>Utilizzare questa procedura solo durante l’integrazione di AEM Forms con il server Microsoft Dynamics locale.

1. Esegui il comando seguente:

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Dove:

   * `Client-ID` è un ID client che è possibile generare utilizzando qualsiasi generatore GUID.
   * `redirect-uri` è l’URL del servizio cloud Microsoft Dynamics OData su AEM Forms. Il servizio cloud predefinito installato con il pacchetto AEM Forms viene distribuito al seguente URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Esegui il seguente comando per concedere l&#39;accesso al computer AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Dove:

   * `resource` è l’URL dell’organizzazione di Microsoft Dynamics.

1. Microsoft Dynamics utilizza il protocollo HTTPS. Per richiamare endpoint AD FS dal server Forms, installa il certificato del sito Microsoft Dynamics nell’archivio certificati Java utilizzando `keytool` sul computer che esegue AEM Forms.

## Configurare il servizio cloud per il servizio Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

La **Cloud Service MS Dynamics OData (servizio OData)** la configurazione viene fornita con la configurazione OData predefinita. Per configurarlo per la connessione al servizio Microsoft Dynamics, procedi come segue.

1. Passa a **[!UICONTROL Strumenti > Cloud Services > Origini dati]** e tocca `global` cartella di configurazione.
1. Seleziona **Cloud Service MS Dynamics OData (servizio OData)** configurazione e tocca **[!UICONTROL Proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà di configurazione del servizio cloud.

   In **Impostazioni di autenticazione** scheda:

   1. Immetti il valore per la **Directory principale servizio** campo . Vai all’istanza di Dynamics e passa a **Riferimenti per sviluppatori** per visualizzare il valore del campo Directory principale del servizio. Ad esempio, https://&lt;tenant-name>/api/data/v9.1/

   1. Sostituisci i valori predefiniti nella **ID client**(di cui anche **ID applicazione**), **Segreto client**, **URL OAuth**, **Aggiorna URL token**, **URL token di accesso** e **Risorsa** campi con valori della configurazione del servizio Microsoft Dynamics. È obbligatorio specificare l’URL dell’istanza di dinamica nel **Risorsa** per configurare Microsoft Dynamics con un modello dati modulo. Utilizza l’URL principale del servizio per derivare l’URL dell’istanza dinamica. Ad esempio: [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Specifica **openid** in **Ambito di autorizzazione** campo per il processo di autorizzazione in Microsoft Dynamics.

   ![Impostazioni di autenticazione](assets/dynamics_authentication_settings_new.png)

1. Fai clic su **[!UICONTROL Connettiti a OAuth]**. Verrai reindirizzato alla pagina di accesso di Microsoft Dynamics.
1. Accedi con le tue credenziali di Microsoft Dynamics e accetta per consentire la configurazione del servizio cloud di connettersi al servizio Microsoft Dynamics. È un’attività una tantum stabilire una connessione tra il servizio cloud e il servizio.

   Viene quindi reindirizzato alla pagina di configurazione del servizio cloud, che visualizza un messaggio che informa che la configurazione OData è stata salvata correttamente.

Il servizio cloud Cloud Service OData di MS Dynamics (OData Service) è configurato e connesso con il servizio Dynamics.

## Crea modello dati modulo {#create-form-data-model}

Quando si installa il pacchetto AEM Forms, un modello dati del modulo,**Microsoft Dynamics FDM**, viene distribuito sull’istanza AEM. Per impostazione predefinita, il modello dati del modulo utilizza il servizio Microsoft Dynamics configurato nel Cloud Service OData di MS Dynamics (OData Service) come origine dati.

All’apertura del modello dati del modulo per la prima volta, si connette al servizio Microsoft Dynamics configurato e recupera le entità dall’istanza di Microsoft Dynamics. Le entità &quot;contatto&quot; e &quot;lead&quot; di Microsoft Dynamics sono già state aggiunte nel modello dati del modulo.

Per rivedere il modello dati del modulo, passare a **[!UICONTROL Forms > Integrazioni dati]**. Seleziona **Microsoft Dynamics FDM** e fai clic su **Modifica** per aprire il modello dati del modulo in modalità di modifica. In alternativa, è possibile aprire il modello dati modulo direttamente dal seguente URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Successivamente, è possibile creare un modulo adattivo basato sul modello di dati del modulo e utilizzarlo in vari casi di utilizzo di moduli adattivi, ad esempio:

* Precompilare il modulo adattivo eseguendo query sulle informazioni provenienti da entità e servizi di Microsoft Dynamics
* Richiamare le operazioni del server Microsoft Dynamics definite in un modello di dati modulo utilizzando regole del modulo adattive
* Scrittura dei dati del modulo inviati alle entità Microsoft Dynamics

Si consiglia di creare una copia del modello dati del modulo fornito con il pacchetto AEM Forms e di configurare modelli e servizi dati in base alle proprie esigenze. In questo modo gli eventuali aggiornamenti futuri del pacchetto non sovrascriveranno il modello dati del modulo.

Per ulteriori informazioni sulla creazione e l’utilizzo del modello dati modulo nei flussi di lavoro aziendali, consulta [Integrazione dei dati](../../forms/using/data-integration.md).
