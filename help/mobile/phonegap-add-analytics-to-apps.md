---
title: Aggiungere Adobe Analytics alla tua applicazione mobile
description: Segui questa pagina per scoprire come utilizzare l’analisi delle app mobili nelle app Adobe Experience Manager tramite l’integrazione con Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Aggiungere Adobe Analytics alla tua applicazione mobile{#add-adobe-analytics-to-your-mobile-application}

{{ue-over-mobile}}

Vuoi creare esperienze coinvolgenti e rilevanti per gli utenti delle tue app mobili? Se non utilizzi Adobe Mobile Services SDK per monitorare e misurare il ciclo di vita e l’utilizzo delle applicazioni, su quali basi stai prendendo le tue decisioni? Dove sono i tuoi clienti più fedeli? Come puoi garantirti di essere rilevante e di ottimizzare le conversioni?

Gli utenti accedono a tutti i contenuti? Stanno abbandonando l&#39;app e, in caso affermativo, dove? Quanto spesso rimangono nell’app e quanto spesso tornano per utilizzarla? Quali modifiche è possibile introdurre e quindi misurare l&#39;aumento della conservazione? E le percentuali di arresti anomali, l’app si arresta in modo anomalo per i tuoi utenti?

Approfitta di [Mobile App Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html) nelle tue app Adobe Experience Manager (AEM) tramite l&#39;integrazione con [Adobe Mobile Services](https://business.adobe.com/products/campaign/mobile-marketing.html).

Utilizza le tue app AEM per monitorare, segnalare e capire in che modo gli utenti interagiscono con la tua app mobile e i tuoi contenuti e per misurare le metriche chiave del ciclo di vita, come avvii, tempo nell’app e frequenza di arresti anomali.

In questa sezione viene descritto come gli sviluppatori *AEM* possono:

* Integrare Mobile Analytics nell’app mobile
* Test del tracciamento delle analisi con Bloodhound

## Prerequisiti {#prerequisties}

AEM Mobile richiede un account Adobe Analytics per raccogliere e segnalare i dati di tracciamento nell’app. Come parte della configurazione, l&#39;amministratore *AEM* deve prima:

* Configura un account Adobe Analytics e crea una suite di rapporti per la tua applicazione in Mobile Services.
* Configurare un Cloud Service AMS in Adobe Experience Manager (AEM).

## Per sviluppatori: integra Mobile Analytics nell’app. {#for-developers-integrate-mobile-analytics-into-your-app}

### Configura ContentSync per richiamare il file di configurazione {#configure-contentsync-to-pull-in-configuration-file}

Dopo aver configurato l’account Analytics, crea una configurazione di Sincronizzazione contenuti per richiamare il contenuto nell’applicazione mobile.

Per ulteriori dettagli, consulta Configurazione del contenuto di sincronizzazione contenuti. La configurazione deve indicare a Content Sync di inserire ADBMobileConfig nella directory /www. Nell&#39;app Geometrixx Outdoors, ad esempio, la configurazione di Sincronizzazione contenuti è: */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. Esiste anche una configurazione per lo sviluppo. Tuttavia, è identica alla configurazione non di sviluppo se sono presenti Geometrixx Outdoors.

Per ulteriori dettagli su come scaricare ADBMobileConfig dal dashboard delle app AEM per applicazioni mobili, vedi File di configurazione SDK di Analytics - Mobile Services - Adobe Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Ogni piattaforma richiede che ADBMobileConfig sia copiato in una posizione specifica.

Se si crea con PhoneGap CLI, è possibile farlo con script di hook di build cordova. Questo può essere visto nell&#39;app Geometrixx Outdoors all&#39;indirizzo:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Per iOS il file deve essere copiato nella directory **Resources** del progetto Xcode (ad esempio, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Se l’app è destinata a Android™, il percorso da copiare è &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Per ulteriori dettagli sull&#39;utilizzo degli hook durante la compilazione CLI di PhoneGap, vedi [Tre hook necessari per il progetto Cordova/PhoneGap](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

Affinché l&#39;app possa raccogliere i dati, è necessario includere nell&#39;app il plug-in Adobe Mobile Services (AMS). Includendo il plug-in come funzione nel file config.xml dell’app, è possibile utilizzare un altro hook Cordova per aggiungere automaticamente il plug-in durante il processo di PhoneGap build.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Il file config.xml dell&#39;app Geometrixx Outdoors si trova in */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’esempio precedente richiede una versione specifica del plug-in da utilizzare aggiungendo un &quot;#&quot; e quindi un valore tag dopo l’URL del plug-in. È buona prassi evitare problemi imprevisti dovuti all’aggiunta di plug-in non testati durante una generazione.

Dopo aver eseguito questi passaggi, l’app sarà abilitata per segnalare tutte le metriche del ciclo di vita fornite da Adobe Analytics. Ciò include dati quali avvii, arresti anomali e installazioni. Se questi sono gli unici dati che ti interessano, allora hai finito. Se desideri raccogliere dati personalizzati, devi instrumentare il codice.

### Strumentazione del codice per il tracciamento completo delle app {#instrument-your-code-for-full-app-tracking}

Sono disponibili diverse API di tracciamento fornite nell&#39;API del plug-in PhoneGap [AMS.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

Questi consentono di tenere traccia degli stati e delle azioni, ad esempio delle pagine a cui gli utenti accedono nell’app, i controlli più utilizzati. Il modo più semplice per dotare l’app di tracciamento è utilizzare le API di Analytics fornite dal plug-in AMS.

* ADB.trackState()
* ADB.trackAction()

Per riferimento, osserva il codice nell’app Geometrixx Outdoors. Nell’app Geometrixx Outdoors, tutta la navigazione nelle pagine viene tracciata utilizzando il metodo ADB.trackState(). Per maggiori dettagli, vedi il codice sorgente per /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Strumentando il codice sorgente con le chiamate di questo metodo, puoi raccogliere metriche complete rispetto all’applicazione.

#### Proprietà per la connessione ad AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l espone le seguenti proprietà per la connessione ad AMS:

| **Etichetta** | **Descrizione** | **Predefinito** |
|---|---|---|
| Endpoint API | URL di base delle API HTTP di Adobe Mobile Services | https://api.omniture.com |
| Endpoint di configurazione | URL utilizzato per recuperare la configurazione ADB Mobile per l’ID suite di rapporti specificato | /ams/1.0/app/config/ |
| App Mobile Services | Ottieni un elenco di app all’interno dell’azienda degli utenti | /ams/1.0/apps |
