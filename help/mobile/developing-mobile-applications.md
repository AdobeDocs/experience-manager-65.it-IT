---
title: Sviluppo di applicazioni mobili in AEM
seo-title: Developing Mobile Applications in AEM
description: Segui questa pagina per iniziare a sviluppare app mobili in AEM utilizzando Adobe PhoneGap Enterprise.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

L’AEM sfrutta Adobe PhoneGap e Adobe Publishing Solutions per creare e gestire applicazioni mobili multipiattaforma ricche di contenuti e basate su utility:

* Gestisci tutte le app mobili aziendali in un’unica posizione.
* Esamina le app negli ambienti di sviluppo e staging senza la complessità dei profili di provisioning e l’impegno aggiuntivo per generare e caricare l’app per la condivisione.
* Utilizza l’ambiente di authoring AEM per creare e gestire contenuti avanzati per le tue app.
* Utilizza HTML5 con Adobe PhoneGap per creare esperienze avanzate con funzionalità native per i dispositivi.
* Introduzione delle visualizzazioni Web di HTML5 a nuove o preesistenti **nativo** applicazioni tramite Cordova WebViews.
* Creazione, cura e condivisione di contenuti multimediali avanzati su tutti i canali di distribuzione, tra cui web, mobile-web, mobile-app e stampa.

L&#39;AEM si integra con il servizio Adobe PhoneGap Build (`https://build.phonegap.com/`) per semplificare la creazione e la distribuzione delle applicazioni.

**Adobe ContentSync** consente agli utenti di scaricare facilmente gli aggiornamenti di pagine e contenuti Over-the-Air (OTA) sui propri dispositivi senza dover reinstallare l’applicazione o scaricare da appStore, Google Play o altre origini dell’app.

**Adobe Analytics** è completamente integrato nelle app AEM e consente il tracciamento dettagliato di distribuzione, geolocalizzazione, sistemi operativi, dispositivi, click-stream, tracciamento iBeacon e altro ancora.

## Creazione di app {#creating-apps}

Gli sviluppatori possono utilizzare [Kit di avvio PhoneGap per AEM](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) insieme alle risorse aggiuntive trovate in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) per avviare le app AEM con PhoneGap, inclusa un&#39;app nativa di riferimento che esegue Cordova Webviews.

Il file readme per l’archivio Git di Starter Kit include un’esercitazione per l’utilizzo del kit di avvio:

* Personalizzare il branding
* Esempi di destinazioni di build e distribuzione Maven
* Configurazione archivio controllo del codice sorgente
* Installazione e distribuzione in istanze AEM locali o remote
* Disinstalla da AEM

>[!NOTE]
>
>Un’ulteriore origine di implementazione di riferimento, inclusi i laboratori, è disponibile su GitHub [qui](https://github.com/adobe-marketing-cloud-apps) e, la fonte &quot;cucina-lavello&quot; [qui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Sviluppo per host IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Gli sviluppatori di IOS devono essere a conoscenza di un problema aperto relativo alle app Cordova in esecuzione su iOS 9. Questo problema impedisce l’esecuzione di richieste a host non sicuri (ad esempio *http://localhost:4502*). Questo problema verrà risolto con una prossima versione di cordova-ios (utilizzata da Cordova CLI), ma nel frattempo sono disponibili due soluzioni alternative:

1. Come soluzione alternativa immediata, puoi comunque utilizzare senza problemi uno qualsiasi dei simulatori iOS 8.
1. Se devi utilizzare iOS 9, le tue app - Info.plist (trovate dopo l&#39;esecuzione `cordova platform add ios` in &quot;&lt;app root=&quot;&quot;>/platform/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;) può essere modificato manualmente per includere la seguente proprietà:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Per maggiori dettagli su &quot;App Transport Security&quot;, consulta la seguente sezione di [Documentazione prerelease iOS9 di Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e questo [Discussione sull&#39;overflow dello stack](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem-1}

* [Avvio di PhoneGap AEM](/help/mobile/starting-aem-phonegap-app.md)
* [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md)
* [Strutturare un’app](/help/mobile/phonegap-structure-an-app.md)
* [Creazione e modifica di app tramite la console App](/help/mobile/phonegap-apps-console.md)
* [Applicazioni a pagina singola](/help/mobile/phonegap-single-page-applications.md)
* [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)
* [Accedere alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Tracciare le prestazioni dell’app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Aggiungere Adobe Analytics alla tua applicazione mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifiche push](/help/mobile/phonegap-push-notifications.md)
* [Personalizzazione dei contenuti AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [Anatomia di un’app](/help/mobile/phonegap-apps-arch.md)
* [La tua app ibrida è pronta per AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di uno sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
