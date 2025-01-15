---
title: Configurazione del Cloud Service Adobe Target
description: Segui questa pagina per scoprire come ottenere il set corretto di autorizzazioni per utenti e gruppi, creare servizi cloud, configurare l’applicazione per l’attività e infine generare il contenuto.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Configurazione del Cloud Service Adobe Target {#configuring-adobe-target-cloud-service}

{{ue-over-mobile}}

>[!NOTE]
>
>Questo documento fa parte della [Guida introduttiva a Adobe Experience Manager (AEM) Mobile](/help/mobile/getting-started-aem-mobile.md), un punto di partenza consigliato per AEM Mobile.

Ci sono diversi passaggi che devono essere messi insieme prima che gli autori dei contenuti possano iniziare a generare contenuti mirati per le app mobili: è possibile ottenere il set giusto di autorizzazioni per utenti e gruppi, creare servizi cloud, configurare l’applicazione per l’attività e infine generare il contenuto.

Si presume che l&#39;applicazione di riferimento ibrida [AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) sia stata distribuita e accessibile tramite il dashboard di AEM Mobile.

## Autorizzazioni {#permissions}

Gli utenti che devono accedere alla console di personalizzazione devono far parte del gruppo `target-activity-authors`. Nell’ambito della configurazione di utenti e gruppi, si consiglia di aggiungere il gruppo target-attività-group al gruppo apps-admins. L&#39;aggiunta del gruppo target-activity-authors consente agli utenti di visualizzare la voce del menu di navigazione di Personalization.

Se si dimentica di aggiungere gli utenti o i gruppi ai quali si desidera concedere l’accesso all’Admin Console di personalizzazione, il gruppo target-activity-authors non sarà in grado di visualizzare la console di personalizzazione.

## Servizi cloud {#cloud-services}

Per ottenere contenuti mirati che funzionano per le app mobili, è necessario configurare due servizi: il servizio Adobe Target e il servizio Adobe Mobile Services. Il servizio Adobe Target fornisce il motore per elaborare le richieste dei client e restituire il contenuto personalizzato. Il servizio Adobe Mobile Services fornisce la connessione tra i servizi Adobe e l’app mobile tramite il file ADBMobileConfig.json, utilizzato dal plug-in Cordova di AMS. Dal dashboard di AEM Mobile, puoi configurare l’applicazione aggiungendo i due servizi.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

Dal dashboard di AEM Mobile, individua il Cloud Service Gestisci e fai clic sul pulsante +.

![chlimage_1-8](assets/chlimage_1-8.png)

Dalla procedura guidata Aggiungi Cloud Service, seleziona la scheda del servizio cloud &quot;Adobe Target&quot; e fai clic su Avanti.

![chlimage_1-9](assets/chlimage_1-9.png)

Dal menu a discesa Seleziona una configurazione, puoi creare una configurazione o selezionarne una esistente. Per creare una configurazione, seleziona &quot;Crea configurazione&quot; dal menu a discesa. Immetti un titolo per la configurazione Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori per questi campi, contatta il supporto Adobe Target. Fai clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fai clic sul pulsante Invia per creare il servizio cloud.

Il servizio cloud creato viene associato automaticamente all’app mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo apps. Per l’esempio di app ibrida, viene impostato su /content/mobileapps/hybrid-reference-app/jcr:content con il valore che punta al nodo del framework generato automaticamente in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Il nodo del framework ha due proprietà impostate per impostazione predefinita: genere ed età. Il framework viene utilizzato solo dall’anteprima AEM e non ha alcun impatto sul dispositivo.

Dopo il completamento della procedura guidata, il riquadro Gestisci Cloud Service contiene il servizio cloud di Target, ma contiene un avviso relativo a un account di Adobe Mobile Services mancante.

![chlimage_1-10](assets/chlimage_1-10.png)

## Servizio mobile di Adobe {#adobe-mobile-service}

È necessario collegare un account di Adobe Mobile Services (AMS) anche all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un&#39;associazione con l&#39;account AMS, l&#39;account AMS deve essere modificato da un utente che dispone di autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS, visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l&#39;app mobile e fai clic sulle impostazioni. Individua il campo Opzioni di SDK Target, inserisci il codice client nel campo e fai clic su Salva.

![chlimage_1-11](assets/chlimage_1-11.png)

Ora che il codice client è stato associato all’app mobile, quando il servizio cloud AMS è configurato tramite il dashboard di Adobe Mobile, le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json.

### Servizio di Adobe Mobile {#adobe-mobile-service-could-service}

Ora che AMS è configurato, è necessario associare l’applicazione mobile alla dashboard di Adobe Mobile. Dal dashboard di AEM Mobile, individua il Cloud Service Gestisci e fai clic sul pulsante +.

![chlimage_1-12](assets/chlimage_1-12.png)

Seleziona la scheda di Adobe Mobile Services e fai clic su Avanti.

![chlimage_1-13](assets/chlimage_1-13.png)

Dal passaggio della procedura guidata Crea o seleziona, seleziona il menu a discesa Mobile Service, quindi seleziona la voce Create Configuration (Crea configurazione). Fornisci titolo, società, nome utente, password e seleziona il centro dati appropriato. Se non conosci questi valori, contatta l’amministratore di Adobe Mobile Services per ottenerli. Dopo aver compilato tutti i campi, fare clic su **Verifica**. Il processo di verifica passa a AMS, verifica le credenziali per l’account e, al termine della convalida, viene compilato un elenco di applicazioni mobili in cui si seleziona l’applicazione mobile associata dal menu a discesa. Fare clic sul pulsante Invia per completare la procedura guidata. Il processo può richiedere un po’ di tempo per ottenere i dati di configurazione ed eventuali analisi associate all’applicazione. Al termine del processo, fai clic su **Fine** dal modale per tornare alla dashboard di Adobe Mobile.

Tornando al dashboard di Mobile, la sezione Gestione Cloud Service contiene il servizio cloud AMS. Inoltre, il riquadro Analizza metriche è compilato con i rapporti sul ciclo di vita.

![chlimage_1-14](assets/chlimage_1-14.png)

## Gestori di sincronizzazione contenuti di Target {#target-content-sync-handlers}

Per distribuire contenuti al dispositivo dell’utente, il contenuto viene generato eseguendo il rendering delle offerte create dagli autori di contenuti AEM. Per gestire il rendering delle offerte target, è disponibile un nuovo gestore di sincronizzazione dei contenuti che elabora le offerte. Utilizzando l&#39;applicazione di riferimento ibrida come esempio, il pacchetto di contenuti en (inglese) contiene ContentSyncConfig con un gestore [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). Il passaggio successivo è fondamentale per il rendering delle offerte al dispositivo. Il gestore mobileapffers dispone di una proprietà path che identifica il percorso dell&#39;attività di personalizzazione utilizzata per l&#39;applicazione.

Ad esempio, se è presente un&#39;attività in */content/campaigns/hybridref*, copia questo percorso e incollalo come valore nella proprietà *path* del gestore mobileappoffers.

Per l’applicazione di riferimento ibrida, sono disponibili due gestori di offerte mobili, uno per lo sviluppo e uno per le produzioni.

Dopo aver impostato il percorso delle attività nella proprietà path del gestore mobileapffers, salva il gestore. Il gestore è ora pronto per iniziare a eseguire il rendering delle offerte per dispositivi mobili.

### Modalità rendering {#render-mode}

Il gestore mobileapffers è configurato in modo diverso per le impostazioni di pubblicazione e sviluppo. Per le impostazioni di pubblicazione esiste una proprietà denominata *renderMode* con un valore di *publish* impostato sul nodo cq:ContentSyncConfig. Il gestore mobileapffers fa riferimento al renderMode e, se impostato su publish, modifica l’ID mbox creato. Per impostazione predefinita, alle mbox create dall’AEM viene aggiunto un valore —author all’ID mbox. Questo identifica che l’attività non è stata pubblicata e deve utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene gestito tramite la dashboard di Adobe Mobile, il contenuto gestito viene considerato pronto per la produzione e ne viene eseguito il rendering tramite la configurazione di sincronizzazione contenuti non di sviluppo. Il rendering in questo modo fa sì che —author venga rimosso da tutti gli ID mbox e preveda che un’attività pubblicata sia disponibile sul server di Target. Prima di testare il contenuto con staging, assicurati che l’attività sia pubblicata.

## Creazione di contenuti {#creating-content}

Ora che i servizi cloud sono stati creati e il gestore mobileapffers è stato configurato, gli autori di contenuti possono iniziare a generare esperienze mirate.
