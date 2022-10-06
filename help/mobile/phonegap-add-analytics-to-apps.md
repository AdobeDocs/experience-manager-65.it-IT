---
title: Aggiungere Adobe Analytics all’applicazione mobile
seo-title: Add Adobe Analytics to your Mobile Application
description: Segui questa pagina per scoprire come utilizzare Mobile App Analytics nelle app AEM integrando con Adobe Mobile Services.
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Aggiungere Adobe Analytics all’applicazione mobile{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Vuoi creare esperienze coinvolgenti e rilevanti per gli utenti delle tue app mobili? Se non utilizzi l’SDK di Adobe Mobile Services per monitorare e misurare il ciclo di vita e l’utilizzo delle applicazioni, in base a cosa si basano le tue decisioni. Dove sono i tuoi clienti più fedeli? Come puoi garantire che le conversioni siano sempre rilevanti e ottimizzate?

Gli utenti accedono a tutti i contenuti? Stanno abbandonando l’app e, in caso affermativo, dove? Con quale frequenza rimangono nell’app e con quale frequenza tornano a utilizzarla? Quali modifiche è possibile introdurre e quindi misurare tale aumento della fidelizzazione? E per quanto riguarda le percentuali di arresto anomalo, l&#39;app si blocca per i tuoi utenti?

Approfitta di [Analisi delle app mobili](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) nelle app AEM integrando con [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Strumento le app AEM per tenere traccia, generare rapporti e comprendere in che modo gli utenti interagiscono con la tua app mobile e i contenuti e per misurare le metriche chiave del ciclo di vita, come gli avvii, il tempo nell’app e la frequenza degli arresti anomali.

Questa sezione descrive come AEM *Sviluppatori* può:

* Integrare Mobile Analytics nella tua app mobile
* Verifica il tracciamento delle analisi con Bloodhound

## Prerequisiti {#prerequisties}

AEM Mobile richiede un account Adobe Analytics per raccogliere e segnalare i dati di tracciamento nell&#39;app. Come parte della configurazione del AEM *Amministratore* :

* Imposta un account Adobe Analytics e crea una suite di rapporti per la tua applicazione in Mobile Services.
* Configura un Cloud Service AMS in Adobe Experience Manager (AEM).

## Per sviluppatori: integrare Mobile Analytics nella tua app {#for-developers-integrate-mobile-analytics-into-your-app}

### Configura ContentSync per estrarre il file di configurazione {#configure-contentsync-to-pull-in-configuration-file}

Una volta configurato l’account Analytics, dovrai creare una configurazione di sincronizzazione dei contenuti per inserire il contenuto nell’applicazione mobile.

Per ulteriori informazioni, consulta Configurazione del contenuto di sincronizzazione dei contenuti . La configurazione dovrà istruire Content Sync per inserire ADBMobileConfig nella directory /www. Ad esempio, nell’app Geometrixx Outdoors la configurazione Content Sync si trova in: */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. Esiste anche una configurazione per lo sviluppo; tuttavia, è identica alla configurazione non di sviluppo nel caso dei Geometrixx Outdoors.

Per ulteriori informazioni su come scaricare ADBMobileConfig dal dashboard App AEM Mobile, consulta File di configurazione SDK di Analytics - Mobile Services - Adobe Mobile Services .

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Ogni piattaforma richiede che ADBMobileConfig venga copiato in una posizione specifica.

Se si crea con PhoneGap CLI, è possibile farlo con uno script gancio di compilazione cordova. Questo è visibile nell’app Geometrixx Outdoors in:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Per iOS il file dovrà essere copiato nel progetto XCode **Risorse** directory (es. &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se l&#39;app è destinata ad Android, il percorso in cui copiare la pagina è &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Per ulteriori dettagli sull’utilizzo degli hook durante la build CLI di PhoneGap, consulta [Tre ganci necessari per il progetto Cordova/PhoneGap](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### Aggiungere il plug-in AMS nell’app {#add-the-ams-plugin-in-the-app}

Affinché l’app raccolga i dati, il plug-in Adobe Mobile Services (AMS) deve essere incluso come parte dell’app. Inserendo il plug-in come funzione nel config.xml dell&#39;app, è possibile utilizzare un altro gancio Cordova per aggiungere automaticamente il plug-in durante il processo di creazione di PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Il file config.xml dell&#39;app dei Geometrixx Outdoors si trova in */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’esempio precedente richiede una versione specifica del plug-in da utilizzare aggiungendo un &#39;#&#39; e quindi un valore di tag dopo l’URL del plug-in. Questa è una buona pratica da seguire per evitare che vengano visualizzati problemi imprevisti a causa dell’aggiunta di plug-in non testati durante una build.

Dopo aver eseguito questi passaggi, l&#39;app verrà abilitata per segnalare tutte le metriche del ciclo di vita fornite da Adobe Analytics. Sono inclusi dati come avvii, arresti anomali e installazioni. Se sono gli unici dati a cui tenete allora avete finito. Se desideri raccogliere dati personalizzati, dovrai dotarti del codice.

### Strumento il codice per il tracciamento completo delle app {#instrument-your-code-for-full-app-tracking}

Sono disponibili diverse API di tracciamento fornite nel [API Plug-in Phonegap AMS.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Questi ti consentono di tenere traccia degli stati e delle azioni, ad esempio le pagine a cui gli utenti si spostano nell’app, quali controlli vengono utilizzati di più. Il modo più semplice per abilitare il tracciamento dell’app è quello di utilizzare le API di Analytics fornite dal plug-in AMS.

* ADB.trackState()
* ADB.trackAction()

Per riferimento, puoi dare un&#39;occhiata al codice nell&#39;app Geometrixx Outdoors. Nell’app Geometrixx Outdoors vengono tracciate tutte le navigazioni di pagina utilizzando il metodo ADB.trackState() . Per ulteriori dettagli, consulta il codice sorgente /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

La strumentazione del codice sorgente con queste chiamate di metodo consente di raccogliere metriche complete sull&#39;applicazione.

#### Proprietà per la connessione ad AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l espone le seguenti proprietà per la connessione ad AMS:

| **Etichetta** | **Descrizione** | **Predefiniti** |
|---|---|---|
| Endpoint API | URL di base delle API HTTP di Adobe Mobile Services | https://api.omniture.com |
| Endpoint di configurazione | URL utilizzato per recuperare la configurazione ADB Mobile per l&#39;ID suite di rapporti specificato | /ams/1.0/app/config/ |
| App di Mobile Services | Ottenere un elenco di app all&#39;interno dell&#39;azienda degli utenti | /ams/1.0/apps |
