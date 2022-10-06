---
title: Configurazione del Cloud Service Adobe Target
seo-title: Configuring Adobe Target Cloud Service
description: Segui questa pagina per scoprire come ottenere il set corretto di autorizzazioni per utenti e gruppi, creare servizi cloud, configurare l’applicazione per l’attività e infine generare il contenuto.
seo-description: Follow this page to understand how to get right set of permissions for users and groups, creating cloud services, configuring the application for the activity, and finally generating the content.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 1%

---

# Configurazione del Cloud Service Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte del [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guida, un punto di partenza consigliato per riferimento AEM Mobile.

È necessario procedere in diversi modi per collaborare prima che gli autori dei contenuti possano iniziare a generare contenuti mirati per le app per dispositivi mobili: Ottieni il set di autorizzazioni corretto per utenti e gruppi, creazione di servizi cloud, configurazione dell’applicazione per l’attività e infine generazione del contenuto.

Il presupposto che si prospetta è che la [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) è stato implementato e accessibile tramite la dashboard di AEM Mobile.

## Autorizzazioni {#permissions}

Gli utenti che devono accedere alla console di personalizzazione devono far parte del gruppo `target-activity-authors` gruppo. È consigliabile che, come parte della configurazione degli utenti e del gruppo, il gruppo target-activity venga aggiunto al gruppo apps-admins . Aggiungendo il gruppo target-activity-authors , gli utenti potranno vedere la voce di menu di navigazione Personalizzazione.

Se dimentichi di aggiungere al gruppo target-activity-authors gli utenti o i gruppi a cui desideri accedere da admin console di personalizzazione, gli utenti non potranno più visualizzare la console di personalizzazione.

## Cloud Services {#cloud-services}

Per il funzionamento del contenuto di destinazione per le applicazioni mobili sono necessari due servizi: Adobe Target Service e Adobe Mobile Services. Il servizio Adobe Target fornisce il motore per l’elaborazione delle richieste dei clienti e la restituzione del contenuto personalizzato. Il servizio Adobe Mobile Services fornisce la connessione tra Adobe Services e l’app mobile tramite il file ADBMobileConfig.json, utilizzato dal plug-in AMS Cordova. Dalla dashboard di AEM Mobile è possibile configurare l&#39;applicazione aggiungendo i due servizi.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

Dalla dashboard di AEM Mobile individua i Cloud Services di gestione e fai clic sul pulsante + .

![chlimage_1-8](assets/chlimage_1-8.png)

Dalla procedura guidata Aggiungi Cloud Service selezionare la scheda del servizio cloud &quot;Adobe Target&quot; e fare clic su Avanti.

![chlimage_1-9](assets/chlimage_1-9.png)

Dal menu a discesa Seleziona una configurazione puoi creare una nuova configurazione o selezionarla da una esistente. Per creare una nuova configurazione, seleziona &quot;Crea configurazione&quot; dal menu a discesa. Immetti un titolo per la configurazione di Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori per questi campi, contatta il supporto Adobe Target. Fai clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fai clic sul pulsante Invia per creare il servizio cloud.

Il servizio cloud che viene creato viene associato automaticamente all’app mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo di app. Per l&#39;esempio di app ibrida viene impostato su /content/mobileapps/ibrido-reference-app/jcr:content con il valore che punta al nodo del framework generato automaticamente, che si trova in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Il nodo del framework ha due proprietà impostate per impostazione predefinita, genere ed età. Il framework viene utilizzato solo AEM visualizzazione in anteprima e non ha alcun impatto sul dispositivo.

Dopo il completamento della procedura guidata, il riquadro Gestione Cloud Service conterrà il servizio cloud di Target, tuttavia contiene un avviso relativo a un account Adobe Mobile Service mancante.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

È necessario collegare un account Adobe Mobile Services (AMS) anche all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un’associazione con l’account AMS, l’account AMS deve essere modificato da un utente che dispone delle autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l’app mobile e fai clic sulle impostazioni . Individua il campo Opzioni SDK Target e inserisci il codice client nel campo , quindi fai clic su Salva.

![chlimage_1-11](assets/chlimage_1-11.png)

Ora che il codice client è stato associato all’app mobile, quando il servizio cloud AMS è configurato tramite la dashboard di Adobe Mobile, le impostazioni per le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json .

### Servizio Adobe Mobile Potrebbe {#adobe-mobile-service-could-service}

Ora che AMS è stato configurato, è il momento di associare l’app mobile nel dashboard di Adobe Mobile. Dalla dashboard di AEM Mobile individua i Cloud Services di gestione e fai clic sul pulsante + .

![chlimage_1-12](assets/chlimage_1-12.png)

Seleziona la scheda Adobe Mobile Services e fai clic su Avanti.

![chlimage_1-13](assets/chlimage_1-13.png)

Dal passaggio Crea o Seleziona procedura guidata , seleziona il menu a discesa Mobile Services e seleziona la voce Crea configurazione . Fornisci un titolo, una società, un nome utente e una password e seleziona il centro dati appropriato. Se non conosci questi valori, contatta l’amministratore di Adobe Mobile Services per ottenerli. Dopo aver compilato tutti i campi, fai clic sul pulsante Verifica . Il processo di verifica va ad AMS e verifica le credenziali per l’account. Una volta eseguita la convalida, un elenco di applicazioni mobili verrà compilato nel punto in cui si seleziona l’applicazione mobile associata dal menu a discesa. Fare clic sul pulsante Invia per completare la procedura guidata. Il processo potrebbe richiedere un po&#39; di tempo per ottenere i dati di configurazione e qualsiasi analisi associata all&#39;applicazione. Una volta completato il processo, fai clic sul pulsante Fine dal modale per tornare alla dashboard mobile di Adobe.

Tornando alla Dashboard mobile, la sezione Gestione Cloud Services conterrà il servizio cloud AMS. Noterai inoltre che la sezione Analizza metriche sarà compilata con rapporti sul ciclo di vita.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestori di sincronizzazione dei contenuti di Target {#target-content-sync-handlers}

Per distribuire contenuti al contenuto del dispositivo dell’utente, viene generato il rendering delle offerte create dagli autori AEM contenuti. Per gestire il rendering delle offerte target, è disponibile un nuovo gestore di sincronizzazione dei contenuti che elabora le offerte. Utilizzando come esempio l’applicazione di riferimento ibrida, il pacchetto di contenuto en (inglese) contiene la configurazione ContentSyncConfig con un [telefonatori](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) handler. Il passaggio successivo è fondamentale per il rendering delle offerte sul dispositivo. Il gestore mobileappoffer ha una proprietà path che identifica il percorso dell&#39;attività di personalizzazione da utilizzare per l&#39;applicazione.

Ad esempio, se esiste un’attività che si trova in */content/campagne/hybridref* copia questo percorso e incollalo come valore nel *path* proprietà del gestore mobileappoffers.

Per l&#39;applicazione di riferimento ibrida sono disponibili due gestori di dispositivi mobili, uno per lo sviluppo e uno per le produzioni.

Una volta impostato il percorso delle attività nella proprietà del percorso del gestore mobileappoffer, salva il gestore. Il gestore sarà ora pronto per avviare il rendering delle offerte per i nostri dispositivi mobili.

### Modalità rendering {#render-mode}

Il gestore mobileappoffer è configurato in modo diverso per le impostazioni di pubblicazione e di sviluppo. Per le impostazioni di pubblicazione è presente una proprietà denominata *renderMode* con un valore di *pubblicare* impostato sul nodo cq:ContentSyncConfig . Il gestore mobileappoffers fa riferimento a renderMode e, se impostato su publish, modificherà l&#39;id mbox che viene creato. Per impostazione predefinita, alle mbox create da AEM è stato aggiunto un valore —author all&#39;id mbox. Questo identifica che l’attività non è stata pubblicata e dovrebbe utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene messo in staging tramite la dashboard di Adobe Mobile, il contenuto in staging viene considerato contenuto pronto per la produzione e sottoposto a rendering tramite la configurazione di sincronizzazione dei contenuti non per sviluppo. Il rendering in questo modo causerà la rimozione dell’autore —da tutti gli ID mbox e prevede che un’attività pubblicata sia disponibile sul server Target. Prima di testare il contenuto in staging, accertati che l’attività sia stata pubblicata.

## Creazione del contenuto {#creating-content}

Dopo la creazione dei servizi cloud e la configurazione del gestore di dispositivi mobili, gli autori dei contenuti possono iniziare a generare esperienze mirate.
