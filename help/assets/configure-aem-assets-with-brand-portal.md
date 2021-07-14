---
title: Configurare AEM Assets con Brand Portal
seo-title: Configurare AEM Assets con Brand Portal
description: Scopri come configurare AEM Assets con Brand Portal per la pubblicazione di risorse e raccolte su Brand Portal.
seo-description: Scopri come configurare AEM Assets con Brand Portal per la pubblicazione di risorse e raccolte su Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
source-git-commit: aed6e28d7ff228ecbaeaf0d468d1d9bcb4373f90
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 10%

---

# Configurare AEM Assets con Brand Portal {#configure-integration-65}

Adobe Experience Manager Assets Brand Portal consente di pubblicare risorse di marchio approvate da Adobe Experience Manager Assets in Brand Portal e di distribuirle agli utenti Brand Portal.

AEM Assets è configurato con Brand Portal tramite Adobe Developer Console, che fornisce un token account Adobe Identity Management Services (IMS) per l’autorizzazione del tenant Brand Portal.

>[!NOTE]
>
>La configurazione di AEM Assets con Brand Portal tramite Adobe Developer Console è supportata in AEM 6.5.4.0 e versioni successive.
>
>In precedenza, Brand Portal era configurato tramite il gateway OAuth legacy, che utilizza lo scambio JSON Web Token (JWT) per ottenere un token di accesso IMS per l’autorizzazione.
>
>La configurazione tramite il gateway OAuth legacy non è più supportata dal 6 aprile 2020 e viene modificata in Adobe Developer Console.

>[!TIP]
>
>***Solo per i clienti esistenti***
>
>Si consiglia di continuare a utilizzare la configurazione del gateway OAuth esistente. Nel caso in cui si verifichino problemi con la configurazione del gateway OAuth legacy, elimina la configurazione esistente e crea una nuova configurazione tramite Adobe Developer Console.

Questa guida descrive i due casi d’uso seguenti:

* [Nuova configurazione](#configure-new-integration-65): Se sei un nuovo utente Brand Portal e desideri configurare la tua istanza di authoring AEM Assets con Brand Portal, puoi creare la configurazione tramite Adobe Developer Console.
* [Aggiorna la configurazione](#upgrade-integration-65): Se sei un utente Brand Portal esistente con configurazione su gateway OAuth legacy, elimina la configurazione esistente e crea una nuova configurazione tramite Adobe Developer Console.

Le informazioni fornite si basano sul presupposto che chiunque legga questa Guida abbia familiarità con le seguenti tecnologie:

* Installazione, configurazione e amministrazione dei pacchetti Adobe Experience Manager e AEM.

* Utilizzo di sistemi operativi Linux e Microsoft Windows.

## Prerequisiti {#prerequisites}

Per configurare AEM Assets con Brand Portal, è necessario quanto segue:

* Un’istanza di authoring AEM Assets in esecuzione con l’ultimo Service Pack
* URL tenant Brand Portal
* Un utente con privilegi di amministratore di sistema nell’organizzazione IMS del tenant di Brand Portal

[Scarica e installa AEM 6.5](#aemquickstart)

[Scarica e installa l&#39;ultimo Service Pack AEM](#servicepack)

### Scarica e installa AEM 6.5 {#aemquickstart}

Si consiglia di avere AEM 6.5 per impostare un&#39;istanza di authoring AEM. Se non hai AEM in esecuzione, scaricalo dalle seguenti posizioni:

* Se sei un cliente AEM esistente, scarica AEM 6.5 dal [sito web Adobe Licensing](http://licensing.adobe.com).

* Se sei un partner di Adobe, utilizza [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) per richiedere AEM 6.5.

Dopo aver scaricato AEM, per istruzioni su come impostare un&#39;istanza AEM dell&#39;autore, consulta [distribuzione e manutenzione](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#default-local-install).

### Scarica e installa AEM Service Pack più recente {#servicepack}

Per istruzioni dettagliate, vedi

* [Note sulla versione di AEM 6.5 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=it)

**Se non riesci a trovare l&#39;ultimo pacchetto AEM o Service Pack, contatta** il supporto.

## Creare la configurazione {#configure-new-integration-65}

La configurazione di AEM Assets con Brand Portal richiede configurazioni sia nell’istanza di authoring di AEM Assets che in Adobe Developer Console.

1. In AEM Assets, crea un account IMS e genera un certificato pubblico (chiave pubblica).
1. In Adobe Developer Console, crea un progetto per il tenant Brand Portal (organizzazione).
1. Nel progetto, configura un’API utilizzando la chiave pubblica per creare una connessione a un account di servizio (JWT).
1. Ottieni le credenziali dell&#39;account del servizio e le informazioni sul payload JWT.
1. In AEM Assets, configura l’account IMS utilizzando le credenziali dell’account del servizio e il payload JWT.
1. In AEM Assets, configura il servizio cloud Brand Portal utilizzando l’account IMS e l’endpoint Brand Portal (URL organizzazione).
1. Verifica la configurazione pubblicando una risorsa da AEM Assets a Brand Portal.

>[!NOTE]
>
>Un’istanza di authoring di AEM Assets può essere configurata con un solo tenant Brand Portal.

Esegui i seguenti passaggi nella sequenza elencata se stai configurando AEM Assets con Brand Portal per la prima volta:
1. [Recuperare il certificato pubblico](#public-certificate)
1. [Crea connessione account di servizio (JWT)](#createnewintegration)
1. [Configurare l’account IMS](#create-ims-account-configuration)
1. [Configurare il servizio cloud](#configure-the-cloud-service)
1. [Verificare la configurazione](#test-integration)

### Creare la configurazione IMS {#create-ims-configuration}

La configurazione IMS autentica l’istanza di authoring di AEM Assets con il tenant Brand Portal.

La configurazione IMS prevede due passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Configurare l’account IMS](#create-ims-account-configuration)

### Recuperare il certificato pubblico {#public-certificate}

La chiave pubblica (certificato) autentica il tuo profilo in Adobe Developer Console.

1. Accedi alla tua istanza di authoring di AEM Assets. L’URL predefinito è `http://localhost:4502/aem/start.html`.

1. Dal pannello **Strumenti** ![Strumenti](assets/do-not-localize/tools.png), passa a **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni IMS di Adobe]**.

1. Nella pagina Configurazioni IMS di Adobe, fai clic su **[!UICONTROL Crea]**. Reindirizzerà alla pagina **[!UICONTROL Adobe IMS Technical Account Configuration]** . Per impostazione predefinita, viene visualizzata la scheda **Certificato** .

1. Seleziona **[!UICONTROL Adobe Brand Portal]** nell&#39;elenco a discesa **[!UICONTROL Soluzione cloud]** .

1. Seleziona la casella di controllo **[!UICONTROL Crea nuovo certificato]** e specifica un **alias** per la chiave pubblica. L&#39;alias funge da nome della chiave pubblica.

1. Fai clic su **[!UICONTROL Crea certificato]**. Quindi, fai clic su **[!UICONTROL OK]** per generare la chiave pubblica.

   ![Crea certificato](assets/ims-config2.png)

1. Fai clic sull&#39;icona **[!UICONTROL Scarica chiave pubblica]** e salva il file della chiave pubblica (.crt) sul computer.

   La chiave pubblica verrà utilizzata in seguito per configurare l’API per il tenant Brand Portal e generare le credenziali dell’account del servizio in Adobe Developer Console.

   ![Scarica certificato](assets/ims-config3.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Nella scheda **Account** viene creato l’account Adobe IMS che richiede le credenziali dell’account del servizio generate in Adobe Developer Console. Per il momento tieni aperta questa pagina.

   Apri una nuova scheda e [crea una connessione a un account di servizio (JWT) in Adobe Developer Console](#createnewintegration) per ottenere le credenziali e il payload JWT per la configurazione dell’account IMS.

### Crea connessione account di servizio (JWT) {#createnewintegration}

In Adobe Developer Console, i progetti e le API sono configurati a livello di tenant Brand Portal (organizzazione). La configurazione di un’API crea una connessione a un account di servizio (JWT). Esistono due metodi per configurare l’API, generando una coppia di chiavi (chiavi private e pubbliche) o caricando una chiave pubblica. Per configurare AEM Assets con Brand Portal, devi generare una chiave pubblica (certificato) in AEM Assets e creare credenziali in Adobe Developer Console caricando la chiave pubblica. Queste credenziali sono necessarie per configurare l’account IMS in AEM Assets. Una volta configurato l’account IMS, puoi configurare il servizio cloud Brand Portal in AEM Assets.

Esegui i seguenti passaggi per generare le credenziali dell’account del servizio e il payload JWT:

1. Accedi ad Adobe Developer Console con privilegi di amministratore di sistema nell’organizzazione IMS (tenant Brand Portal). L&#39;URL predefinito è [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Accertati di aver selezionato l’organizzazione IMS corretta (tenant Brand Portal) dall’elenco a discesa (organizzazione) che si trova nell’angolo in alto a destra.

1. Fai clic su **[!UICONTROL Crea nuovo progetto]**. Per la tua organizzazione viene creato un progetto vuoto con un nome generato dal sistema.

   Fai clic su **[!UICONTROL Modifica progetto]** per aggiornare il **[!UICONTROL Titolo progetto]** e **[!UICONTROL Descrizione]**, quindi fai clic su **[!UICONTROL Salva]**.

1. Nella scheda **[!UICONTROL Panoramica progetto]** , fai clic su **[!UICONTROL Aggiungi API]**.

1. In **[!UICONTROL Aggiungi una finestra API]**, seleziona **[!UICONTROL AEM Brand Portal]** e fai clic su **[!UICONTROL Avanti]**.

   Assicurati di avere accesso al servizio AEM Brand Portal.

1. Nella finestra **[!UICONTROL Configura API]**, fai clic su **[!UICONTROL Carica la chiave pubblica]**. Quindi, fai clic su **[!UICONTROL Seleziona un file]** e carica la chiave pubblica (.crt file) che hai scaricato nella sezione [Ottieni certificato pubblico](#public-certificate) .

   Fai clic su **[!UICONTROL Avanti]**.

   ![Carica chiave pubblica](assets/service-account3.png)

1. Verifica la chiave pubblica e fai clic su **[!UICONTROL Avanti]**.

1. Seleziona **[!UICONTROL Assets Brand Portal]** come profilo di prodotto predefinito e fai clic su **[!UICONTROL Salva API configurata]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleziona profilo prodotto](assets/service-account4.png)

1. Una volta configurata l’API, vieni reindirizzato alla pagina di panoramica dell’API. Nella navigazione a sinistra sotto **[!UICONTROL Credenziali]**, fai clic sull&#39;opzione **[!UICONTROL Account di servizio (JWT)]**.

   >[!NOTE]
   >
   >Puoi visualizzare le credenziali ed eseguire azioni quali generare token JWT, copiare i dettagli delle credenziali, recuperare il segreto client e così via.

1. Dalla scheda **[!UICONTROL Credenziali client]**, copia l&#39; **[!UICONTROL ID client]**.

   Fai clic su **[!UICONTROL Recupera segreto client]** e copia il **[!UICONTROL segreto client]**.

   ![Credenziali account di servizio](assets/service-account5.png)

1. Passa alla scheda **[!UICONTROL Genera JWT]** e copia le informazioni **[!UICONTROL Payload JWT]** .

Ora puoi utilizzare l’ID client (chiave API), il segreto client e il payload JWT su [configurare l’account IMS](#create-ims-account-configuration) in AEM Assets.

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

### Configurare l’account IMS {#create-ims-account-configuration}

Verifica di aver eseguito i seguenti passaggi:

* [Recuperare il certificato pubblico](#public-certificate)
* [Crea connessione account di servizio (JWT)](#createnewintegration)

Esegui i seguenti passaggi per configurare l’account IMS.

1. Apri la configurazione IMS e passa alla scheda **[!UICONTROL Account]** . Hai tenuto aperta la pagina durante [il recupero del certificato pubblico](#public-certificate).

1. Specifica un **[!UICONTROL titolo]** per l’account IMS.

   Nel campo **[!UICONTROL Server autorizzazioni]** , specifica l’URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Specifica l&#39;ID client nel campo **[!UICONTROL Chiave API]**, **[!UICONTROL Segreto client]** e **[!UICONTROL Payload]** (Payload JWT) che hai copiato durante la creazione della connessione dell&#39;account del servizio (JWT)](#createnewintegration).[

   Fai clic su **[!UICONTROL Crea]**.

   L’account IMS è configurato.

   ![Configurazione dell’account IMS](assets/create-new-integration6.png)

1. Seleziona la configurazione dell’account IMS e fai clic su **[!UICONTROL Verifica stato]**.

   Fare clic su **[!UICONTROL Controlla]** nella finestra di dialogo. Una volta completata la configurazione, viene visualizzato un messaggio che informa che il *Token viene recuperato correttamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Puoi disporre di una sola configurazione IMS.
>
>Verifica che la configurazione IMS superi il controllo di integrità. Se la configurazione non supera questa verifica, non è valida. Dovrai quindi eliminarla e creare una nuova configurazione valida.

### Configurare il servizio cloud {#configure-the-cloud-service}

Esegui i seguenti passaggi per configurare il servizio cloud Brand Portal:

1. Accedi alla tua istanza di authoring di AEM Assets.

1. Dal pannello **Strumenti** ![Strumenti](assets/do-not-localize/tools.png), passa a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Nella pagina Configurazioni Brand Portal, fai clic su **[!UICONTROL Crea]**.

1. Specifica un **[!UICONTROL titolo]** per la configurazione.

   Seleziona la configurazione IMS creata durante la [configurazione dell’account IMS](#create-ims-account-configuration).

   Nel campo **[!UICONTROL URL servizio]** , specifica l’URL del tenant Brand Portal (organizzazione).

   ![](assets/create-cloud-service.png)

1. Fai clic su **[!UICONTROL Salva e chiudi]**. Viene creata la configurazione cloud.

   L’istanza di authoring di AEM Assets è ora configurata con il tenant Brand Portal.

### Verificare la configurazione {#test-integration}

Esegui i seguenti passaggi per convalidare la configurazione:

1. Accedi alla tua istanza cloud di AEM Assets.

1. Dal pannello **Strumenti** ![Strumenti](assets/do-not-localize/tools.png), passa a **[!UICONTROL Implementazione]** > **[!UICONTROL Replica]**.

   ![](assets/test-integration1.png)

1. Nella pagina Replica, fai clic su **[!UICONTROL Agenti sull&#39;autore]**.

   ![](assets/test-integration2.png)

   Puoi visualizzare i quattro agenti di replica creati per il tenant Brand Portal.

   Individua gli agenti di replica del tenant Brand Portal e fai clic sull’URL dell’agente di replica.

   ![](assets/test-integration3.png)

   >[!NOTE]
   >
   >Gli agenti di replica lavorano in parallelo e condividono la distribuzione del lavoro in modo uniforme, aumentando così la velocità di pubblicazione di quattro volte la velocità originale. Una volta configurato il servizio cloud, non è necessaria alcuna configurazione aggiuntiva per abilitare gli agenti di replica attivati per impostazione predefinita per abilitare la pubblicazione parallela di più risorse.

1. Per verificare la connessione tra AEM Assets e Brand Portal, fai clic sull&#39;icona **[!UICONTROL Prova connessione]** .

   ![](assets/test-integration4.png)

   Viene visualizzato un messaggio che informa che il pacchetto di test *è stato consegnato correttamente*.

   ![](assets/test-integration5.png)

1. Verifica i risultati del test su tutti e quattro gli agenti di replica.


   >[!NOTE]
   >
   >Evita di disabilitare uno qualsiasi degli agenti di replica, in quanto può causare il mancato funzionamento della replica delle risorse (in esecuzione nella coda).
   >
   >Assicurati che tutti e quattro gli agenti di replica siano configurati per evitare errori di timeout. Consulta [risoluzione dei problemi relativi alla pubblicazione parallela in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html?lang=en#connection-timeout).

Ora puoi:

* [Pubblicare risorse da AEM Assets su Brand Portal](../assets/brand-portal-publish-assets.md)
* [Pubblicare risorse da Brand Portal ad AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)  - Asset Sourcing in Brand Portal
* [Pubblicare cartelle da AEM Assets su Brand Portal](../assets/brand-portal-publish-folder.md)
* [Pubblicare raccolte da AEM Assets su Brand Portal](../assets/brand-portal-publish-collection.md)
* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Pubblicare tag in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Per ulteriori informazioni, consulta la [documentazione Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) .


## Configurazione dell&#39;aggiornamento {#upgrade-integration-65}

Esegui i seguenti passaggi nella sequenza elencata per aggiornare le configurazioni esistenti ad Adobe Developer Console:
1. [Verificare i processi in esecuzione](#verify-jobs)
1. [Elimina configurazioni esistenti](#delete-existing-configuration)
1. [Creare la configurazione](#configure-new-integration-65)

### Verificare i processi in esecuzione {#verify-jobs}

Assicurati che nessun processo di pubblicazione sia in esecuzione nell’istanza di authoring di AEM Assets prima di apportare eventuali modifiche. A questo scopo, puoi verificare lo stato dei processi attivi su tutti e quattro gli agenti di replica e verificare che le code siano inattive.

1. Accedi alla tua istanza di authoring di AEM Assets.

1. Dal pannello **Strumenti** ![Strumenti](assets/do-not-localize/tools.png), passa a **[!UICONTROL Implementazione]** > **[!UICONTROL Replica distribuzione]**.

1. Nella pagina Replica, fai clic su **[!UICONTROL Agenti sull&#39;autore]**.

   ![](assets/test-integration2.png)

1. Individua gli agenti di replica del tenant Brand Portal.

   Assicurati che la **coda sia inattiva** per tutti gli agenti di replica, nessun processo di pubblicazione è attivo.

   ![](assets/test-integration3.png)

### Elimina configurazioni esistenti {#delete-existing-configuration}

È necessario eseguire la seguente lista di controllo durante l&#39;eliminazione delle configurazioni esistenti:
* Elimina tutti e quattro gli agenti di replica
* Elimina servizio cloud Brand Portal
* Elimina utente MAC

1. Accedi alla tua istanza di authoring di AEM Assets e apri CRX Lite come amministratore. L’URL predefinito è `http://localhost:4502/crx/de/index.jsp`.

1. Passa a `/etc/replications/agents.author` ed elimina tutti e quattro gli agenti di replica del tenant Brand Portal.

   ![](assets/delete-replication-agent.png)

1. Passa a `/etc/cloudservices/mediaportal` ed elimina la configurazione del servizio cloud Brand Portal.

   ![](assets/delete-cloud-service.png)

1. Passa a `/home/users/mac` ed elimina l’ **utente MAC** del tenant Brand Portal.

   ![](assets/delete-mac-user.png)


È ora possibile [creare la configurazione](#configure-new-integration-65) tramite Adobe Developer Console nell’istanza di authoring AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
