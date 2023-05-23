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
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte del [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guida di, punto di partenza consigliato per AEM Mobile.

Esistono diversi passaggi da completare prima che gli autori dei contenuti possano iniziare a generare contenuti mirati per le app per dispositivi mobili: è necessario ottenere il set giusto di autorizzazioni per utenti e gruppi, creare servizi cloud, configurare l’applicazione per l’attività e infine generare i contenuti.

L&#39;ipotesi è che il [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) è stato distribuito correttamente e accessibile tramite la dashboard di AEM Mobile.

## Autorizzazioni {#permissions}

Gli utenti che hanno bisogno di accedere alla console di personalizzazione devono far parte del gruppo `target-activity-authors` gruppo. Nell’ambito della configurazione di utenti e gruppi, si consiglia di aggiungere il gruppo target-attività-group al gruppo apps-admins. Aggiungendo il gruppo target-activity-authors, gli utenti potranno visualizzare la voce del menu di navigazione Personalizzazione.

Se si dimentica di aggiungere al gruppo target-activity-authors gli utenti o i gruppi a cui si desidera avere accesso all’Admin Console di personalizzazione, gli utenti non potranno visualizzare la console di personalizzazione.

## Servizi cloud {#cloud-services}

Per ottenere contenuti mirati che funzionano per le app mobili, è necessario configurare due servizi: il servizio Adobe Target e il servizio Adobe Mobile Services. Il servizio Adobe Target fornisce il motore per elaborare le richieste dei client e restituire il contenuto personalizzato. Il servizio Adobe Mobile Services fornisce la connessione tra i servizi Adobe e l’app mobile tramite il file ADBMobileConfig.json, utilizzato dal plug-in Cordova di AMS. Dal dashboard di AEM Mobile puoi configurare l’applicazione aggiungendo i due servizi.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

Dal dashboard di AEM Mobile, individua il Cloud Services Gestisci e fai clic sul pulsante +.

![chlimage_1-8](assets/chlimage_1-8.png)

Dalla procedura guidata Aggiungi Cloud Service, seleziona la scheda del servizio cloud &quot;Adobe Target&quot; e fai clic su Avanti.

![chlimage_1-9](assets/chlimage_1-9.png)

Dal menu a discesa Seleziona una configurazione puoi creare una nuova configurazione o selezionarne una esistente. Per creare una nuova configurazione, seleziona &quot;Crea configurazione&quot; dal menu a discesa. Immetti un titolo per la configurazione Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori per questi campi, contatta il supporto Adobe Target. Fai clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fai clic sul pulsante Invia per creare il servizio cloud.

Il servizio cloud creato viene associato automaticamente all’app mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo apps. Per l’esempio di app ibrida, viene impostato su /content/mobileapps/hybrid-reference-app/jcr:content con il valore che punta al nodo del framework generato automaticamente che si trova in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Il nodo del framework ha due proprietà impostate per impostazione predefinita: genere ed età. Il framework viene utilizzato solo dall’anteprima AEM e non ha alcun impatto sul dispositivo.

Dopo il completamento della procedura guidata, il riquadro Gestisci Cloud Service conterrà il servizio cloud di Target, ma contiene un avviso relativo a un account Adobe Mobile Service mancante.

![chlimage_1-10](assets/chlimage_1-10.png)

## Servizio mobile Adobe {#adobe-mobile-service}

È necessario collegare un account Adobe Mobile Services (AMS) anche all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un&#39;associazione con l&#39;account AMS, l&#39;account AMS deve essere modificato da un utente che dispone di autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS, visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l’app mobile e fai clic sulle impostazioni. Individua il campo Opzioni SDK Target, inserisci il codice client nel campo e fai clic su Salva.

![chlimage_1-11](assets/chlimage_1-11.png)

Ora che il codice client è stato associato all’app mobile, quando il servizio cloud AMS è configurato tramite l’Adobe Dashboard per dispositivi mobili, le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json.

### Servizio mobile Adobe: servizio possibile {#adobe-mobile-service-could-service}

Ora che AMS è stato configurato, è il momento di associare l’app mobile all’Adobe Dashboard mobile. Dal dashboard di AEM Mobile, individua il Cloud Services Gestisci e fai clic sul pulsante +.

![chlimage_1-12](assets/chlimage_1-12.png)

Seleziona la scheda Adobe Mobile Services e fai clic su Avanti.

![chlimage_1-13](assets/chlimage_1-13.png)

Dal passaggio della procedura guidata Crea o seleziona, seleziona il menu a discesa Mobile Service e seleziona la voce Create Configuration (Crea configurazione). Fornisci titolo, società, nome utente, password e seleziona il centro dati appropriato. Se non conosci questi valori, contatta l’amministratore di Adobe Mobile Services per ottenerli. Una volta compilati tutti i campi, fai clic sul pulsante Verifica. Il processo di verifica passa a AMS, verifica le credenziali per l’account e, una volta completata la convalida, viene compilato un elenco di applicazioni mobili in cui si seleziona l’applicazione mobile associata dal menu a discesa. Fare clic sul pulsante Invia per completare la procedura guidata. Il processo può richiedere un po’ di tempo per ottenere i dati di configurazione ed eventuali analisi associate all’applicazione. Una volta completata la procedura, fai clic sul pulsante Fine dal modale per tornare alla dashboard di Adobe Mobile.

Tornando alla dashboard di Mobile, la sezione Gestione Cloud Services conterrà il servizio cloud AMS. Noterai inoltre che la sezione Analizza metriche verrà compilata con i rapporti sul ciclo di vita.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestori di sincronizzazione contenuti di Target {#target-content-sync-handlers}

Per distribuire contenuti al dispositivo dell’utente, il contenuto viene generato eseguendo il rendering delle offerte create dagli autori di contenuti AEM. Per gestire il rendering delle offerte target è disponibile un nuovo gestore di sincronizzazione dei contenuti che elaborerà le offerte. Utilizzando l’applicazione di riferimento ibrida come esempio, il pacchetto di contenuti en (inglese) contiene ContentSyncConfig con un [mobileapffffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) handler. Il passaggio successivo è fondamentale per il rendering delle offerte al dispositivo. Il gestore mobileapffers dispone di una proprietà path che identifica il percorso dell&#39;attività di personalizzazione da utilizzare per l&#39;applicazione.

Ad esempio, in presenza di un’attività situata in */content/campaigns/hybridref* copia questo percorso e incollalo come valore in *percorso* proprietà del gestore mobileapffers.

Per l’applicazione di riferimento ibrida sono disponibili due gestori di offerte mobili, uno per lo sviluppo e uno per le produzioni.

Una volta impostato il percorso delle attività nella proprietà path del gestore mobileapffers, salva il gestore. Il gestore sarà ora pronto per iniziare a eseguire il rendering delle offerte per i nostri dispositivi mobili.

### Modalità rendering {#render-mode}

Il gestore mobileapffers è configurato in modo diverso per le impostazioni di pubblicazione e sviluppo. Per le impostazioni di pubblicazione è disponibile una proprietà denominata *renderMode* con un valore di *pubblicare* impostata sul nodo cq:ContentSyncConfig. Il gestore mobileapffers fa riferimento al renderMode e, se impostato su publish, modifica l’ID mbox creato. Per impostazione predefinita, alle mbox create dall’AEM viene aggiunto un valore —author all’ID mbox. Questo identifica che l’attività non è stata pubblicata e deve utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene gestito tramite l’Adobe Mobile Dashboard, il contenuto gestito viene considerato pronto per la produzione e ne viene eseguito il rendering tramite la configurazione di sincronizzazione contenuti non di sviluppo. Se si esegue il rendering in questo modo, l’autore —author verrà rimosso da tutti gli ID mbox e si prevede che un’attività pubblicata sia disponibile sul server Target. Prima di testare il contenuto in staging, assicurati che l’attività sia stata pubblicata.

## Creazione del contenuto {#creating-content}

Ora che i servizi cloud sono stati creati e il gestore mobileapffers è stato configurato, gli autori di contenuti possono iniziare a generare esperienze mirate.
