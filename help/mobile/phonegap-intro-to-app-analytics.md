---
title: Tracciare le prestazioni dell’app con Adobe Mobile Analytics
description: Con Mobile Services di Adobe, puoi ottenere informazioni su come gli utenti utilizzano le tue app mobili monitorando l’utilizzo, gli arresti anomali dell’app, i dettagli del dispositivo e molte altre metriche critiche per le tue app mobili. Per ulteriori informazioni, segui questa pagina.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Tracciare le prestazioni dell’app con Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Desideri promuovere conversioni più elevate dei clienti e fidelizzazione.

Desideri offrire ai tuoi clienti esperienze rilevanti e coinvolgenti.

Che cosa fa la tua app AEM Mobile per le campagne di marketing?

Come mettere a punto le applicazioni mobili per fornire la migliore esperienza agli utenti?

Con Mobile Services di Adobe, puoi ottenere informazioni su come gli utenti utilizzano le tue app mobili monitorando l’utilizzo, gli arresti anomali dell’app, i dettagli del dispositivo e molte altre metriche critiche per le tue app mobili.

Adobe Experience Manager Mobili fornisce un’occhiata ai dettagli della tua analisi mobile direttamente dal dashboard dell’applicazione AEM Mobile. Il **Sezione metriche di Mobile** nel dashboard di fornisce Real-Time Analytics per la tua app mobile, consentendo a sviluppatori, autori e amministratori di dare una rapida occhiata allo stato della tua app mobile. Sotto le copertine, l&#39;elemento chiave dell&#39;analisi è il [Adobe di analisi per dispositivi mobili](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK L’SDK di Analytics per dispositivi mobili di Adobe può essere collegato alle applicazioni in modo nativo o tramite un plug-in PhoneGap Bridge per le visualizzazioni Web. Le metriche vengono raccolte e memorizzate nella cache del dispositivo fino a quando il dispositivo non è connesso, e i dati vengono inviati al cloud Adobe Mobile Services per scopi di reporting e analisi.

L’SDK di Adobe Mobile Analytics fornisce quanto segue:

1. **Raccolta di dati per i canali mobili** : raccogli dati completi per i tuoi siti web e app mobili su tutti i principali sistemi operativi.
1. **Analisi del coinvolgimento mobile** - Comprendi il coinvolgimento degli utenti nell’app mobile, nel sito web o nel video, compresa la frequenza con cui i consumatori avviano il canale, se effettuano acquisti da esso e altro ancora.
1. **Dashboard e rapporti dell’app mobile** : ottieni rapporti sull’utilizzo che includono le metriche del ciclo di vita per le app e le metriche dell’app store. Consulta le tendenze per utenti, avvii, durata media della sessione, durata di conservazione e arresti anomali.
1. **Analisi di una campagna mobile** - Quantificare l’efficacia delle campagne specifiche per dispositivi mobili come SMS, annunci di ricerca per dispositivi mobili, annunci di visualizzazione su dispositivi mobili e codici QR.
1. **Analisi della geolocalizzazione** : scopri dove gli utenti dell’app avviano e interagiscono con le tue esperienze mobili tramite la posizione GPS o i punti di interesse.
1. **Analisi dei percorsi** : scopri come gli utenti si spostano nell’app per determinare quali schermate ed elementi dell’interfaccia utente coinvolgono gli utenti e quali causano l’abbandono.

Questa sezione descrive come [Sviluppatori AEM](#developers) scopri quindi come dotare le app AEM Mobile di tracciamento analytics.

Infine, [Amministratori AEM](#administrators) scopri:

* creazione di un servizio cloud per Adobe Mobile Services
* creare una configurazione per servizio mobile e associare una suite di rapporti
* associare la configurazione del servizio mobile a un’app mobile
* visualizzare le metriche tramite il Centro di comando delle app AEM
* assegnare la configurazione SDK di AMS all’app mobile

## Per sviluppatori: integra Analytics nell’app {#for-developers-integrate-analytics-into-your-app}

**Prerequisito:** Gli amministratori AEM devono configurare la configurazione cloud di Adobe Mobile Services, [come discusso di seguito](#amscloudserviceconfig).

Gli sviluppatori sono responsabili di [aggiunta di analytics a un’app AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) se necessario, per tenere traccia di come gli utenti interagiscono con i contenuti dell’app mobile, generare rapporti e capire in che modo misurano le metriche chiave del ciclo di vita, ad esempio avvii, tempo in app e frequenza di arresti anomali.

## Per gli amministratori: configurare il Cloud Service Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Per sfruttare i vantaggi di Adobe Mobile Services, devi configurare il Cloud Service AEM Adobe Mobile Services con le informazioni del tuo account Adobe Analytics. Il Centro comandi app fornisce un **Analizzare le metriche** riquadro in cui è possibile creare e associare cloud service alla tua app mobile.

Per configurare il servizio cloud nella tua app mobile, fai clic sull’icona a forma di ingranaggio nella sezione Analizza metriche.

![chlimage_1-125](assets/chlimage_1-125.png)

Fai clic sull’icona a forma di ingranaggio nel riquadro Analizza metriche per aprire la finestra di dialogo modale &quot;Configura analisi Mobile Services&quot;. Seleziona la configurazione dal menu a discesa Seleziona una configurazione del servizio mobile. Se è necessario creare una configurazione, fare clic sul pulsante chiave inglese.

Per creare un Adobe di servizio cloud Mobile Services sono necessari due passaggi: la connessione al servizio e la selezione della suite di rapporti da assegnare alla configurazione.

Per iniziare, fai clic sul pulsante &#39;+&#39; nella sezione Gestisci Cloud Service del dashboard.

![chlimage_1-126](assets/chlimage_1-126.png)

Dopo aver fatto clic su &quot;&quot;**+**&#39;, il pulsante **Aggiungi Cloud Service** viene visualizzata la procedura guidata.

![chlimage_1-127](assets/chlimage_1-127.png)

Seleziona o crea una configurazione per servizio mobile compilando i campi obbligatori come mostrato di seguito. Il tuo amministratore AEM richiede queste informazioni per creare correttamente la connessione ad Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Dopo aver completato le impostazioni dell’account Mobile Services, ti viene richiesto di selezionare un’app. In questo modo si collega il reporting analitico di Adobe Mobile Services a tale applicazione.

Seleziona il servizio mobile desiderato, quindi fai clic su Aggiorna per assegnare la configurazione del servizio mobile e chiudere la finestra di dialogo.

Ora che hai associato la configurazione del servizio mobile all’app AEM Mobile, il riquadro inizia a recuperare i dati delle metriche e inizia a generare i rapporti.

![chlimage_1-129](assets/chlimage_1-129.png)

### File di configurazione SDK di Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

A questo punto, l’app mobile è associata a un servizio cloud, ma non sa ancora come comunicare ad Adobe Analytics le metriche mobile raccolte. Per collegare l’app mobile ad Adobe Analytics, è necessario aggiungere a Adobe Experience Manager il file di configurazione SDK di Adobe Mobile Services.

Dal riquadro Analizza metriche, fai clic sull&#39;icona a forma di freccia per esporre le voci del menu Scarica/Carica configurazione SDK di AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

Il primo passaggio consiste nell’ottenere la configurazione SDK da Adobe Mobile Services. Fai clic su Scarica configurazione SDK di AMS per essere reindirizzato al sito web di Adobe Mobile Services da cui puoi scaricare il file di configurazione. Dopo aver ottenuto il file ADBMobileConfig.json, fai clic su &quot;Carica configurazione SDK di AMS&quot; per caricare il file di configurazione in AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Fai clic sul pulsante Carica configurazione applicazione Adobe Mobile Services e individua il file ADBMobileConfig.json, quindi fai clic su Carica.

Ora che l’app mobile ha accesso al file ADBMobileConfig.json, dispone delle conoscenze necessarie per comunicare con Adobe Analytics e iniziare a generare rapporti sul valore delle metriche importanti che contribuiscono al successo delle app.

## Quali sono le prossime novità? {#what-s-next}

1. [Avvia la mia esperienza con l’app AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gestire il contenuto dell’app](/help/mobile/phonegap-manage-app-content.md)
1. [Genera la mia applicazione](/help/mobile/building-app-mobile-phonegap.md)
1. [Monitora le prestazioni dell’app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Distribuire un’esperienza app personalizzata con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Invia messaggi importanti agli utenti](/help/mobile/phonegap-push-notifications.md)
