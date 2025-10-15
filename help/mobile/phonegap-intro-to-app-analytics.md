---
title: Tracciare le prestazioni dell’app con Adobe Mobile Analytics
description: Con Adobe Mobile Services, puoi ottenere informazioni su come gli utenti utilizzano le tue app mobili monitorando l’utilizzo, gli arresti anomali dell’app, i dettagli del dispositivo e molte altre metriche critiche per le tue app mobili. Per ulteriori informazioni, segui questa pagina.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# Tracciare le prestazioni dell’app con Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

{{ue-over-mobile}}

Desideri promuovere conversioni più elevate dei clienti e fidelizzazione.

Desideri offrire ai tuoi clienti esperienze rilevanti e coinvolgenti.

Che cosa fa la tua app AEM Mobile per le campagne di marketing?

Come mettere a punto le applicazioni mobili per fornire la migliore esperienza agli utenti?

Con Adobe Mobile Services, puoi ottenere informazioni su come gli utenti utilizzano le tue app mobili monitorando l’utilizzo, gli arresti anomali dell’app, i dettagli del dispositivo e molte altre metriche critiche per le tue app mobili.

Adobe Experience Manager Mobili fornisce un’occhiata ai dettagli della tua analisi mobile direttamente dal dashboard dell’applicazione AEM Mobile. Il riquadro **Metriche mobile** nel dashboard fornisce Real-Time Analytics per la tua app mobile, consentendo a sviluppatori, autori e amministratori di ottenere un rapido sguardo sullo stato della tua app mobile. Sotto le copertine, il motore dell&#39;analisi è il SDK [Adobe Mobile Analytics](https://business.adobe.com/it/products/analytics/mobile-marketing.html). Il SDK Adobe Mobile Analytics può essere collegato alle applicazioni in modo nativo o tramite un plug-in PhoneGap Bridge per le visualizzazioni Web. Le metriche vengono raccolte e memorizzate nella cache del dispositivo fino a quando il dispositivo non è connesso, e i dati vengono inviati al cloud di Adobe Mobile Services a scopo di reporting e analisi.

Adobe Mobile Analytics SDK fornisce quanto segue:

1. **Raccolta dati per i canali mobili** - Raccolta di dati completi per i siti Web e le app mobili in tutti i principali sistemi operativi.
1. **Analisi del coinvolgimento mobile** - Comprendi il coinvolgimento degli utenti nell&#39;app mobile, nel sito Web o nel video, compresa la frequenza con cui i consumatori avviano il canale, se effettuano acquisti da esso e altro ancora.
1. **Dashboard e rapporti per app mobili** - Ottieni rapporti sull&#39;utilizzo che includono metriche del ciclo di vita per le tue app e metriche per app store. Vedi le tendenze per utenti, avvii, durata media della sessione, durata di conservazione e arresti anomali.
1. **Analisi campagna mobile** - Quantifica l&#39;efficacia di campagne specifiche per dispositivi mobili come SMS, annunci di ricerca mobile, annunci di visualizzazione mobile e codici QR.
1. **Analisi della geolocalizzazione** - Trova il punto in cui gli utenti dell&#39;app avviano e interagiscono con le tue esperienze mobili in base alla posizione GPS o ai punti di interesse.
1. **Analisi dei percorsi**: scopri come gli utenti si spostano nell&#39;app per determinare quali schermate ed elementi dell&#39;interfaccia utente coinvolgono gli utenti e quali causano l&#39;abbandono.

In questa sezione viene descritto come [gli sviluppatori di AEM](#developers) possono imparare a dotare le app AEM Mobile di funzionalità di tracciamento di Analytics.

Infine, [Amministratori AEM](#administrators) imparano a:

* creazione di un servizio cloud in Adobe Mobile Services
* creare una configurazione per servizio mobile e associare una suite di rapporti
* associare la configurazione del servizio mobile a un’app mobile
* visualizzare le metriche tramite il Centro di comando delle app AEM
* assegnare la configurazione SDK di AMS all’app mobile

## Per sviluppatori: integra Analytics nell’app {#for-developers-integrate-analytics-into-your-app}

**Prerequisito:** gli amministratori AEM devono configurare la configurazione cloud di Adobe Mobile Services, [come descritto di seguito](#amscloudserviceconfig).

Gli sviluppatori sono responsabili dell&#39;[aggiunta di analisi a un&#39;app AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) per tenere traccia dei contenuti dell&#39;app mobile, generare report e capire in che modo gli utenti interagiscono con essi e per misurare le metriche chiave del ciclo di vita, ad esempio avvii, durata dell&#39;app e frequenza di arresti anomali.

## Per gli amministratori: configurare il Cloud Service Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Per sfruttare i vantaggi di Adobe Mobile Services, devi configurare il Cloud Service AEM Adobe Mobile Services con le informazioni del tuo account Adobe Analytics. Il Centro comandi app fornisce un riquadro **Analizza metriche** in cui è possibile creare e associare il servizio cloud all&#39;app mobile.

Per configurare il servizio cloud nella tua app mobile, fai clic sull’icona a forma di ingranaggio nella sezione Analizza metriche.

![chlimage_1-125](assets/chlimage_1-125.png)

Fai clic sull’icona a forma di ingranaggio nel riquadro Analizza metriche per aprire la finestra di dialogo modale &quot;Configura analisi Mobile Services&quot;. Seleziona la configurazione dal menu a discesa Seleziona una configurazione del servizio mobile. Se è necessario creare una configurazione, fare clic sul pulsante chiave inglese.

Per creare un servizio cloud Adobe Mobile Service sono necessari due passaggi: stabilire la connessione al servizio e selezionare la suite di rapporti da assegnare alla configurazione.

Per iniziare, fai clic sul pulsante &#39;+&#39; nella sezione Gestisci Cloud Service del dashboard.

![chlimage_1-126](assets/chlimage_1-126.png)

Dopo aver fatto clic sul pulsante &#39;**+**&#39;, verrà visualizzata la procedura guidata **Aggiungi Cloud Service**.

![chlimage_1-127](assets/chlimage_1-127.png)

Seleziona o crea una configurazione per servizio mobile compilando i campi obbligatori come mostrato di seguito. Il tuo amministratore AEM richiede queste informazioni per creare correttamente la connessione ad Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Dopo aver completato le impostazioni dell’account Mobile Services, ti viene richiesto di selezionare un’app. In questo modo si collega il reporting di Adobe Mobile Services Analytics a tale applicazione.

Seleziona il servizio mobile desiderato, quindi fai clic su Aggiorna per assegnare la configurazione del servizio mobile e chiudere la finestra di dialogo.

Ora che hai associato la configurazione del servizio mobile all’app AEM Mobile, il riquadro inizia a recuperare i dati delle metriche e inizia a generare i rapporti.

![chlimage_1-129](assets/chlimage_1-129.png)

### File di configurazione SDK di Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

A questo punto, l’app mobile è associata a un servizio cloud, ma non sa ancora come comunicare ad Adobe Analytics le metriche mobile raccolte. Per collegare l’app mobile ad Adobe Analytics, è necessario aggiungere a Adobe Experience Manager il file di configurazione SDK di Adobe Mobile Services.

Dal riquadro Analizza metriche, fai clic sull’icona a forma di freccia per esporre le voci del menu Scarica/Carica configurazione SDK di AMS.

![chlimage_1-130](assets/chlimage_1-130.png)

Il primo passaggio consiste nell’ottenere la configurazione SDK da Adobe Mobile Services. Fai clic su Scarica configurazione SDK AMS per essere reindirizzato al sito web di Adobe Mobile Services da cui puoi scaricare il file di configurazione. Dopo aver ottenuto il file ADBMobileConfig.json, fai clic su &quot;Carica configurazione SDK AMS&quot; per caricare il file di configurazione nell’AEM.

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
