---
title: Sviluppo di applicazioni mobili in AEM
seo-title: Sviluppo di applicazioni mobili in AEM
description: Segui questa pagina per iniziare a sviluppare applicazioni mobili in AEM tramite Adobe PhoneGap Enterprise.
seo-description: Segui questa pagina per iniziare a sviluppare applicazioni mobili in AEM tramite Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

AEM sfrutta Adobe PhoneGap e le soluzioni Adobe Publishing, consentendo di creare e gestire applicazioni mobili multipiattaforma basate sia sui contenuti che sulle utility:

* Gestisci tutte le tue app mobili aziendali in un&#39;unica posizione.
* Rivedete le app in ambienti di sviluppo e di pre-produzione senza la complessità dei profili di provisioning e senza dover creare e caricare l&#39;app per la condivisione.
* Utilizzate l&#39;ambiente di authoring di AEM per creare e gestire contenuto avanzato per le vostre app.
* Utilizzate HTML5 con Adobe PhoneGap per creare esperienze avanzate con funzionalità native per dispositivi.
* Potete introdurre le visualizzazioni Web HTML5 nelle applicazioni **native** nuove o preesistenti tramite Cordova WebViews.
* Crea, cura e condividi contenuti multimediali avanzati su tutti i canali di distribuzione, inclusi web, mobile-web, app e stampa.

AEM si integra con il servizio **[Adobe](https://build.phonegap.com/)**PhoneGap Build per semplificare il processo di creazione e implementazione delle applicazioni.

**Adobe ContentSync** consente agli utenti di scaricare facilmente gli aggiornamenti di pagina e contenuto Over-the-Air (OTA) sui propri dispositivi senza dover reinstallare l&#39;applicazione o scaricarla da appStore, Google Play o altre fonti di app.

**Adobe Analytics** è completamente integrato nelle app AEM e consente il tracciamento dettagliato di distribuzione, geolocalizzazione, sistemi operativi, dispositivi, flussi di clic, tracciamento iBeacon e altro ancora.

## Creazione di app {#creating-apps}

Gli sviluppatori possono utilizzare [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) con risorse aggiuntive reperibili in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) per avviare le app AEM con PhoneGap, inclusa un&#39;app nativa di riferimento che esegue Cordova Webviews.

Il file Leggimi per il repository Starter Kit Git include un&#39;esercitazione per l&#39;utilizzo del kit di avvio:

* Personalizzare il marchio
* Esempi di destinazione di creazione e distribuzione
* Configurazione archivio del controllo del codice sorgente
* Installazione e implementazione in istanze AEM locali o remote
* Disinstallazione da AEM

>[!NOTE]
>
>Ulteriori fonti di implementazione di riferimento, compresi i laboratori, si trovano su GitHub [qui](https://github.com/adobe-marketing-cloud-apps) e, la fonte &quot;cucina-lavello&quot; [qui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Sviluppo per gli host IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Gli sviluppatori IOS devono essere a conoscenza di un problema aperto con le app Cordova in esecuzione su iOS 9. Questo problema impedisce che vengano effettuate richieste a host non sicuri (ad esempio *http://localhost:4502*). Questo problema verrà risolto con una prossima release di cordova-ios (utilizzata dalla CLI Cordova), ma nel frattempo sono disponibili due soluzioni:

1. Come soluzione immediata, potete comunque utilizzare senza problemi uno qualsiasi dei simulatori iOS 8.
1. Se devi usare iOS 9, il file app -Info.plist (trovato dopo l&#39;esecuzione `cordova platform add ios` in &quot;&lt;app root>/platform/ios/&lt;nome app>/&lt;nome app>-Info.plist&quot;) può essere modificato manualmente per includere la seguente proprietà:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Per ulteriori informazioni su &quot;App Transport Security&quot;, consultate la sezione seguente dei documenti prerelease di [Apple iOS9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e questa discussione [sull&#39;](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)overflow dello stack.

## Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem-1}

* [Avvio di AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md)
* [Struttura di un&#39;app](/help/mobile/phonegap-structure-an-app.md)
* [Creazione e modifica di app tramite la console App](/help/mobile/phonegap-apps-console.md)
* [Applicazioni a pagina singola](/help/mobile/phonegap-single-page-applications.md)
* [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)
* [Accesso alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Tracciare le prestazioni delle app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Aggiungere Adobe Analytics alla tua applicazione mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifiche push](/help/mobile/phonegap-push-notifications.md)
* [Personalizzazione del contenuto AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L&#39;anatomia di un&#39;app](/help/mobile/phonegap-apps-arch.md)
* [L&#39;app ibrida è pronta per AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Additional Resources {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
