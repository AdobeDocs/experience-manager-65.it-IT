---
title: Configurare AEM Assets con Brand Portal
seo-title: Configurare AEM Assets con Brand Portal
description: Scoprite come configurare AEM Assets con Brand Portal per la pubblicazione di risorse e raccolte in Brand Portal.
seo-description: Scoprite come configurare AEM Assets con Brand Portal per la pubblicazione di risorse e raccolte in Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 15%

---


# Configurare AEM Assets con Brand Portal {#configure-integration-65}

 risorse di Adobe Experience Manager (AEM) è configurato con Brand Portal tramite Adobe Developer Console, che fornisce un token IMS per l’autorizzazione del tenant del Brand Portal.

>[!NOTE]
>
>La configurazione di AEM Assets con Brand Portal tramite Adobe Developer Console è supportata in AEM 6.5.4.0 e versioni successive.
>
>Precedentemente, Brand Portal era stato configurato nell’interfaccia classica tramite il gateway OAuth legacy, che utilizza lo scambio di token JWT per ottenere un token di accesso IMS per l’autorizzazione.
>
>La configurazione tramite OAuth legacy non è più supportata dal 6 aprile 2020 e viene modificata in configurazione tramite Adobe Developer Console.


>[!TIP]
>
>***Solo per i clienti esistenti***
>
>Si consiglia di continuare a utilizzare la configurazione gateway OAuth esistente. Se si verificano problemi con la configurazione del gateway OAuth precedente, eliminate la configurazione esistente e create una nuova configurazione tramite Adobe Developer Console.



Questa guida descrive i due casi d’uso seguenti:
* [Nuova configurazione](#configure-new-integration-65): Se siete un nuovo utente del Brand Portal e desiderate configurare l’istanza di creazione degli AEM Assets con Brand Portal, potete creare una nuova configurazione in Adobe Developer Console.
* [Configurazione](#upgrade-integration-65)aggiornamento: Se siete un utente esistente di Brand Portal con l’istanza di creazione AEM Assets configurata con Brand Portal su OAuth Gateway legacy, si consiglia di eliminare le configurazioni esistenti e creare una nuova configurazione in Adobe Developer Console.

Le informazioni fornite si basano sul presupposto che chiunque legga la presente Guida abbia familiarità con le seguenti tecnologie:

* Installazione, configurazione e amministrazione di pacchetti  Adobe Experience Manager e AEM.

* Utilizzo di sistemi operativi Linux e Microsoft Windows.

## Prerequisiti {#prerequisites}

Per configurare AEM Assets con Brand Portal, è necessario quanto segue:

* Un&#39;istanza di creazione AEM Assets con Service Pack più recente.
* URL del tenant di Brand Portal.
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant di Brand Portal.


[Scaricare e installare AEM 6.5](#aemquickstart)

[Scarica e installa la versione più recente di AEM Service Pack](#servicepack)

### Scaricare e installare AEM 6.5 {#aemquickstart}

È consigliabile disporre di AEM 6.5 per configurare un’istanza di creazione AEM. Se AEM non è già operativo, scaricatelo dai seguenti percorsi:

* Se siete già clienti AEM, scaricate AEM 6.5 dal sito Web [delle licenze](http://licensing.adobe.com)Adobe.

* Se sei un partner Adobe, utilizza [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) per richiedere AEM 6.5.

Dopo aver scaricato AEM, per istruzioni su come impostare un’istanza di creazione AEM, consultate [Implementazione e manutenzione](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### Download e installazione dell&#39;ultimo Service Pack di AEM {#servicepack}

Per istruzioni dettagliate, vedete

* [Note sulla versione di AEM 6.5 Service Pack](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Contatta l’Assistenza** clienti se non riesci a trovare il pacchetto AEM o il Service Pack più recente.

## Creare la configurazione {#configure-new-integration-65}

La configurazione di AEM Assets con Brand Portal richiede configurazioni sia nell’istanza di creazione AEM Assets, sia in Adobe Developer Console.

1. Nell’istanza di creazione AEM Assets, create un account IMS e generate un certificato pubblico (chiave pubblica).

1. In Adobe Developer Console, crea un progetto per il tenant del Brand Portal (organizzazione).

1. Nel progetto, configura un&#39;API utilizzando la chiave pubblica per creare una connessione a un account di servizio (JWT).

1. Ottenete le credenziali dell&#39;account del servizio e le informazioni sul payload JWT.

1. Nell’istanza di creazione AEM Assets, configurate l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.

1. Nell’istanza di creazione di AEM Assets, configurate il servizio cloud Brand Portal tramite l’account IMS e l’endpoint del Brand Portal (URL organizzazione).

1. Verificate la configurazione pubblicando una risorsa dall’istanza di creazione di AEM Assets in Brand Portal.


>[!NOTE]
>
>Un tenant di Brand Portal può essere configurato solo con un’istanza di autore di AEM Assets.
>
>Non configurate un tenant di Brand Portal con più istanze di creazione di AEM Assets.



Se state configurando AEM Assets con Brand Portal per la prima volta, eseguite i seguenti passaggi nella sequenza elencata:
1. [Recuperare il certificato pubblico](#public-certificate)
1. [Creare una connessione account di servizio (JWT)](#createnewintegration)
1. [Configurare l&#39;account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)
1. [Verificare la configurazione](#test-integration)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica il tenant di Brand Portal con l’istanza di authoring di AEM Assets.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l&#39;account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

Il certificato pubblico consente di autenticare il profilo in Adobe Developer Console.

1. Accedete all’istanza di creazione AEM Assets. L’URL predefinito è
   `http:// localhost:4502/aem/start.html`
1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Interfaccia utente di configurazione dell’account Adobe IMS](assets/ims-config1.png)

1. Nella pagina Configurazioni Adobe IMS, fate clic su **[!UICONTROL Crea]**.

1. Viene nuovamente visualizzata la pagina Configurazione **[!UICONTROL account tecnico di]** Adobe IMS. By default, the **Certificate** tab opens.

   Selezionate la soluzione cloud **[!UICONTROL Adobe Brand Portal]**.

1. Seleziona la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per il certificato. L’alias funge da nome della finestra di dialogo.

1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fate clic su **[!UICONTROL OK]** nella finestra di dialogo per generare il certificato pubblico.

   ![Crea certificato](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   Il file del certificato verrà utilizzato nei passaggi successivi per configurare l&#39;API per il tenant del Brand Portal e generare le credenziali dell&#39;account del servizio in Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** , potete creare l&#39;account Adobe IMS, ma per questo dovrete disporre delle credenziali dell&#39;account di servizio generate in Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Aprite una nuova scheda e [create una connessione account di servizio (JWT) in Adobe Developer Console](#createnewintegration) per ottenere le credenziali e il payload JWT per configurare l&#39;account IMS.

### Creare una connessione account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, i progetti e le API sono configurati a livello di organizzazione (tenant Brand Portal). La configurazione di un&#39;API crea una connessione a un account di servizio (JWT) in Adobe Developer Console. Esistono due metodi per configurare l&#39;API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare l’istanza di creazione di AEM Assets con Brand Portal, dovete generare un certificato pubblico (chiave pubblica) nell’istanza di creazione di AEM Assets e creare le credenziali in Adobe Developer Console caricando la chiave pubblica. Questa chiave pubblica viene utilizzata per configurare l&#39;API per l&#39;organizzazione Brand Portal selezionata e genera le credenziali e il payload JWT per l&#39;account del servizio. Tali credenziali vengono ulteriormente utilizzate per configurare l&#39;account IMS nell&#39;istanza di creazione AEM Assets. Una volta configurato l’account IMS, potete configurare il servizio cloud Brand Portal nell’istanza di creazione AEM Assets.

Effettuate le seguenti operazioni per generare le credenziali dell&#39;account del servizio e il payload JWT:

1. Accedete ad Adobe Developer Console con privilegi di amministratore di sistema nell’organizzazione IMS (tenant Brand Portal). L’URL predefinito è

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >Accertatevi di aver selezionato l&#39;organizzazione IMS corretta (tenant Brand Portal) dal menu a discesa (elenco organizzazioni) situato nell&#39;angolo superiore destro.

1. Click **[!UICONTROL Create new project]**. Viene creato un progetto vuoto per la vostra organizzazione.

   Fate clic su **[!UICONTROL Modifica progetto]** per aggiornare il Titolo **[!UICONTROL e la]** Descrizione **[!UICONTROL del]** progetto, quindi fate clic su **[!UICONTROL Salva]**.

   ![Crea progetto](assets/service-account1.png)

1. Nella scheda Panoramica progetto, fate clic su **[!UICONTROL Aggiungi API]**.

   ![Aggiungi API](assets/service-account2.png)

1. Nella finestra Aggiungi un API, selezionate **[!UICONTROL AEM Brand Portal]** e fate clic su **[!UICONTROL Avanti]**.

   Assicuratevi di avere accesso al servizio AEM Brand Portal.

1. Nella finestra Configura API, fate clic su **[!UICONTROL Carica la chiave]** pubblica. Quindi, fate clic su **[!UICONTROL Seleziona un file]** e caricate il certificato pubblico (file .crt) scaricato nella sezione [Ottieni certificato](#public-certificate) pubblico.

   Fai clic su **[!UICONTROL Avanti]**.

   ![Carica chiave pubblica](assets/service-account3.png)

1. Verifica il certificato pubblico e fai clic su **[!UICONTROL Avanti]**.

1. Selezionate il profilo di prodotto predefinito **[!UICONTROL Assets Brand Portal]** e fate clic su **[!UICONTROL Salva configurazione]**.

   ![Seleziona profilo di prodotto](assets/service-account4.png)

1. Con l&#39;API configurata, verrete reindirizzati alla panoramica dell&#39;API. Nel menu di navigazione a sinistra, in **[!UICONTROL Credenziali]**, fate clic su Account **[!UICONTROL servizio (JWT)]**.

   >[!NOTE]
   >
   >Potete visualizzare le credenziali ed eseguire altre azioni (generare token JWT, copiare i dettagli delle credenziali, recuperare il segreto client e così via) in base alle esigenze.

1. Dalla scheda Credenziali **** client, copiate l&#39;ID **** client.

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Credenziali account di servizio](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

Ora potete utilizzare l&#39;ID client (chiave API), il segreto client e il payload JWT per [configurare l&#39;account](#create-ims-account-configuration) IMS nell&#39;istanza cloud AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### Creare la configurazione dell’account IMS {#create-ims-account-configuration}

Verifica di aver eseguito i seguenti passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Creare una connessione account di servizio (JWT)](#createnewintegration)

Effettuate le seguenti operazioni per configurare l&#39;account IMS creato per [ottenere il certificato](#public-certificate)pubblico.

1. Aprite IMS Configuration (Configurazione IMS) e passate alla scheda **[!UICONTROL Account]** . La pagina è rimasta aperta durante il [recupero del certificato](#public-certificate)pubblico.

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   In **[!UICONTROL Server autorizzazioni]**, immetti l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Incollate l&#39;ID client nella chiave API, nel segreto client e nel payload JWT che avete copiato durante la [creazione della connessione](#createnewintegration)dell&#39;account del servizio (JWT).

   Fai clic su **[!UICONTROL Crea]**.

   L&#39;account IMS è configurato.

   ![Configurazione dell’account IMS](assets/create-new-integration6.png)


1. Seleziona la configurazione IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Se la configurazione è stata completata, viene visualizzato un messaggio che informa che il *token è stato recuperato* correttamente.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Puoi disporre di una sola configurazione IMS. Non creare più configurazioni IMS.
>
>Verifica che la configurazione IMS superi il controllo di integrità. Se la configurazione non supera questa verifica, non è valida. Dovrai quindi eliminarla e creare una nuova configurazione valida.



### Configurare il servizio cloud {#configure-the-cloud-service}

Per creare il servizio cloud Brand Portal, effettuate le seguenti operazioni:

1. Accedete all’istanza di creazione AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fate clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Selezionate la configurazione IMS creata durante la [configurazione dell&#39;account](#create-ims-account-configuration)IMS.

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization) URL.

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud. L’istanza di creazione AEM Assets ora è configurata con il tenant del Brand Portal.

### Verificare la configurazione {#test-integration}

Effettuate le seguenti operazioni per convalidare la configurazione:

1. Accedi all’istanza cloud AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. Nella pagina Replica, fate clic su **[!UICONTROL Agenti sull’autore]**.

   ![](assets/test-integration2.png)

1. Per ciascun tenant vengono creati quattro agenti di replica.

   Individuate gli agenti di replica del tenant del Brand Portal.

   Fate clic sull&#39;URL dell&#39;agente di replica.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Gli agenti di replica lavorano in parallelo e condividono la distribuzione dei processi in modo uniforme, aumentando così la velocità di pubblicazione di quattro volte la velocità originale. Una volta configurato il servizio cloud, non è richiesta ulteriore configurazione per abilitare gli agenti di replica attivati per impostazione predefinita per abilitare la pubblicazione parallela di più risorse.


1. Per verificare la connessione tra AEM Assets e Brand Portal, fai clic su **[!UICONTROL Prova connessione]**.

   ![](assets/test-integration4.png)

   Nella parte inferiore della pagina viene visualizzato un messaggio che informa che il pacchetto di test è stato consegnato correttamente.

   ![](assets/test-integration5.png)

1. Verificate i risultati del test su tutti e quattro gli agenti di replica uno per uno.


   >[!NOTE]
   >
   >Evitate di disattivare qualsiasi agente di replica. Potrebbe causare il fallimento della replica di alcune delle risorse.

L’istanza di creazione AEM Assets è stata configurata correttamente con Brand Portal. È ora possibile:

* [Pubblicare risorse da AEM Assets su Brand Portal](../assets/brand-portal-publish-assets.md)
* [Pubblicare cartelle da AEM Assets su Brand Portal](../assets/brand-portal-publish-folder.md)
* [Pubblicare raccolte da AEM Assets su Brand Portal](../assets/brand-portal-publish-collection.md)
* [Configurare l’origine](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) delle risorse per consentire agli utenti del Brand Portal di contribuire e pubblicare le risorse per i AEM Assets.

## Aggiornamento della configurazione {#upgrade-integration-65}

Per aggiornare le configurazioni esistenti, eseguite i seguenti passaggi nella sequenza elencata:
1. [Verificare i processi in esecuzione](#verify-jobs)
1. [Elimina configurazioni esistenti](#delete-existing-configuration)
1. [Creare la configurazione](#configure-new-integration-65)

### Verificare i processi in esecuzione {#verify-jobs}

Prima di apportare eventuali modifiche, verificate che nell’istanza di creazione AEM Assets non sia in esecuzione alcun processo di pubblicazione. A tal fine, è possibile verificare tutti e quattro gli agenti di replica e assicurarsi che le code siano vuote.

1. Accedete all’istanza di creazione AEM Assets.

1. Dal pannello **Strumenti** ![Strumenti](assets/do-not-localize/tools.png) , accedi a **[!UICONTROL Distribuzione]** > Replica **** distribuzione.

1. Nella pagina Replica, fate clic su **[!UICONTROL Agenti sull’autore]**.

   ![](assets/test-integration2.png)

1. Individuate gli agenti di replica del tenant del Brand Portal.

   Verificate che la **coda sia inattiva** per tutti gli agenti di replica. Nessun processo di pubblicazione attivo.

   ![](assets/test-integration3.png)

### Elimina configurazioni esistenti {#delete-existing-configuration}

È necessario eseguire il seguente elenco di controllo durante l&#39;eliminazione delle configurazioni esistenti.
* Elimina tutti e quattro gli agenti di replica
* Elimina servizio cloud
* Elimina utente MAC

1. Accedete all’istanza di creazione dei AEM Assets e aprite CRX Lite come amministratore. L’URL predefinito è

   `http:// localhost:4502/crx/de/index.jsp`

1. Individuate `/etc/replications/agents.author` ed eliminate tutti e quattro gli agenti di replica del tenant del Brand Portal in uso.

   ![](assets/delete-replication-agent.png)

1. Individuate `/etc/cloudservices/mediaportal` ed eliminate la configurazione **** Cloud Service.

   ![](assets/delete-cloud-service.png)

1. Individuate `/home/users/mac` ed eliminate l&#39;utente **** MAC del tenant di Brand Portal.

   ![](assets/delete-mac-user.png)


È ora possibile [creare la configurazione](#configure-new-integration-65) tramite Adobe Developer Console nell&#39;istanza di creazione di AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


