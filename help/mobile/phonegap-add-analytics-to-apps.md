---
title: Aggiungere  Adobe Analytics all'applicazione mobile
seo-title: Aggiungere  Adobe Analytics all'applicazione mobile
description: Segui questa pagina per scoprire come utilizzare Mobile App Analytics nelle AEM App integrando con  Adobe Mobile Services.
seo-description: Segui questa pagina per scoprire come utilizzare Mobile App Analytics nelle AEM App integrando con  Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Aggiungi  Adobe Analytics all&#39;applicazione mobile{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Vuoi creare esperienze coinvolgenti e pertinenti per gli utenti delle tue applicazioni mobili? Se non utilizzi l&#39;SDK di Mobile Services  Adobe per monitorare e misurare il ciclo di vita e l&#39;utilizzo dell&#39;applicazione, in base a cosa stai prendendo le tue decisioni? Dove sono i tuoi clienti più fedeli? Come puoi garantire che le conversioni siano sempre rilevanti e ottimizzate?

Gli utenti accedono a tutti i contenuti? Stanno abbandonando l&#39;app e, in caso affermativo, dove? Con quale frequenza restano nell&#39;app e con quale frequenza tornano per utilizzare l&#39;app? Quali modifiche è possibile introdurre e quindi misurare tale aumento di mantenimento? Che dire delle percentuali di arresto anomalo, l&#39;app si blocca per i tuoi utenti?

Sfrutta [Mobile App Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) nelle app AEM integrando con [ Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Strumenti le tue app AEM per tenere traccia, segnalare e comprendere in che modo gli utenti interagiscono con la tua app mobile e il contenuto e per misurare le metriche del ciclo di vita chiave, come avvii, tempo nell&#39;app e tasso di arresto anomalo.

Questa sezione descrive come AEM *sviluppatori* possono:

* Integrare Mobile Analytics nell’applicazione mobile
* Test del tracciamento delle analisi con Bloodhound

## Prerequisiti {#prerequisties}

 AEM Mobile richiede un account Adobe Analytics  per raccogliere e segnalare i dati di tracciamento nell&#39;app. Come parte della configurazione, il AEM *Amministratore* dovrà prima:

* Imposta un account Adobe Analytics  e crea una suite di rapporti per la tua applicazione in Mobile Services.
* Configurare un Cloud Service AMS in Adobe Experience Manager (AEM).

## Per sviluppatori - Integrare Mobile Analytics nella tua app {#for-developers-integrate-mobile-analytics-into-your-app}

### Configurare ContentSync per il pulling del file di configurazione {#configure-contentsync-to-pull-in-configuration-file}

Una volta configurato l&#39;account Analytics, dovrete creare una configurazione di sincronizzazione dei contenuti per inserire il contenuto nell&#39;applicazione mobile.

Per ulteriori dettagli, consultate Configurazione del contenuto di sincronizzazione dei contenuti. Per inserire ADBMobileConfig nella directory /www, è necessario configurare Content Sync. Ad esempio, nell&#39;app Geometrixx Outdoors la configurazione Content Sync (Sincronizzazione contenuto) si trova in: */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Esiste anche una configurazione per lo sviluppo; tuttavia, è identica alla configurazione non di sviluppo nel caso dei Geometrixx Outdoors.

Per ulteriori dettagli su come scaricare ADBMobileConfig dal dashboard App AEM applicazione mobile, consultare Analytics - Mobile Services -  file di configurazione SDK di Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Ciascuna piattaforma richiede che ADBMobileConfig venga copiato in un percorso specifico.

Se si crea con l&#39;interfaccia CLI di PhoneGap, ciò può essere fatto con uno script gancio di compilazione cordova. Questo può essere visualizzato nell’app Geometrixx Outdoors all’indirizzo:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Per iOS, il file dovrà essere copiato nella directory **Resources** del progetto XCode (ad esempio &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se l&#39;app è destinata ad Android, il percorso in cui copiarla è &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Per ulteriori dettagli sull&#39;utilizzo degli ganci durante la build CLI di PhoneGap, fare riferimento a [Tre ganci necessari per il progetto Cordova/PhoneGap](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

### Aggiungete il plug-in AMS nell&#39;app {#add-the-ams-plugin-in-the-app}

Affinché l&#39;app raccolga i dati, il plug-in  Adobe Mobile Services (AMS) deve essere incluso come parte dell&#39;app. Inserendo il plug-in come funzionalità nel file config.xml dell&#39;app, è possibile utilizzare un altro gancio Cordova per aggiungere automaticamente il plug-in durante il processo di creazione di PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Il file config.xml Geometrixx Outdoors App si trova in */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L&#39;esempio precedente richiede l&#39;utilizzo di una versione specifica del plug-in aggiungendo un &#39;#&#39; e quindi un valore di tag dopo l&#39;URL del plug-in. Si tratta di una buona pratica da seguire per garantire che i problemi imprevisti non vengano visualizzati a causa di plug-in non testati aggiunti durante una build.

Dopo aver eseguito questi passaggi, l&#39;app sarà abilitata a segnalare tutte le metriche del ciclo di vita fornite da  Adobe Analytics. Sono inclusi dati quali avvii, arresti anomali e installazioni. Se questi sono gli unici dati che ti interessano allora hai finito. Se si desidera raccogliere dati personalizzati, sarà necessario dotare il codice.

### Strumento del codice per il tracciamento completo delle app {#instrument-your-code-for-full-app-tracking}

Nell&#39;API plug-in Phonegap di [AMS sono disponibili diverse API di tracciamento.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Questi consentono di tenere traccia degli stati e delle azioni, ad esempio dove si trovano le pagine a cui gli utenti si spostano all&#39;interno dell&#39;app, quali controlli vengono utilizzati di più. Il modo più semplice per strumentalizzare l&#39;app per il tracciamento è utilizzare le API di Analytics fornite dal plug-in AMS.

* ADB.trackState()
* ADB.trackAction()

Per riferimento, potete dare un&#39;occhiata al codice nell&#39;app Geometrixx Outdoors. Nell&#39;app Geometrixx Outdoors, tutte le operazioni di navigazione delle pagine vengono tracciate utilizzando il metodo ADB.trackState(). Per ulteriori dettagli, consultate il codice sorgente /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Tramite la strumentazione del codice sorgente con queste chiamate di metodo è possibile raccogliere metriche complete rispetto all’applicazione.

#### Proprietà per la connessione ad AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl espone le seguenti proprietà per la connessione ad AMS:

| **Etichetta** | **Descrizione** | **Impostazione predefinita** |
|---|---|---|
| Endpoint API | URL di base delle API HTTP di Mobile Services di  Adobe | https://api.omniture.com |
| Endpoint di configurazione | L&#39;URL utilizzato per recuperare il file di configurazione ADB Mobile per l&#39;ID suite di rapporti specificato | /ams/1.0/app/config/ |
| App Mobile Services | Ottenere un elenco di app all&#39;interno della società degli utenti | /ams/1.0/apps |

