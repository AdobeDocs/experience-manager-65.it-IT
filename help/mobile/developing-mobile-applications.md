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
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

AEM sfrutta le soluzioni Adobe PhoneGap e Adobe Publishing, consentendo di creare e gestire applicazioni mobili multipiattaforma basate su contenuti e utility:

* Gestisci tutte le tue app mobili aziendali in un&#39;unica posizione.
* Esamina le app negli ambienti di sviluppo e di staging senza la complessità dei profili di provisioning e con l’impegno aggiuntivo per creare e caricare l’app per la condivisione.
* Utilizza l’ambiente di authoring AEM per creare e gestire contenuti avanzati per le tue app.
* Utilizza HTML5 con Adobe PhoneGap per creare esperienze avanzate con funzionalità native per dispositivi.
* Presenta le visualizzazioni web di HTML5 a nuove o preesistenti **nativo** applicazioni tramite Cordova WebViews.
* Crea, cura e condividi contenuti multimediali avanzati su tutti i canali di distribuzione, compresi web, web mobile, app mobile e stampa.

AEM si integra con l’Adobe **[servizio PhoneGap Build](https://build.phonegap.com/)** per semplificare il processo di creazione e distribuzione delle applicazioni.

**Adobe ContentSync** consente agli utenti di scaricare facilmente gli aggiornamenti di pagina e contenuto Over-the-Air (OTA) sui propri dispositivi senza dover reinstallare l&#39;applicazione o scaricare dall&#39;appStore, Google Play o altre sorgenti dell&#39;app.

**Adobe Analytics** è completamente integrato nelle app AEM e consente il tracciamento dettagliato di distribuzione, geolocalizzazione, sistemi operativi, dispositivi, flussi di clic, tracciamento iBeacon e altro ancora.

## Creazione di app {#creating-apps}

Gli sviluppatori possono utilizzare [Kit AEM PhoneGap Starter](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) insieme alle risorse aggiuntive disponibili in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) per avviare app AEM con PhoneGap, inclusa un’app nativa di riferimento che esegue Cordova Webviews.

Il file readme per l’archivio Git di Starter Kit include un tutorial per l’utilizzo del kit di avvio:

* Personalizzare il marchio
* Obiettivi di generazione e distribuzione di esempio Maven
* Configurazione dell’archivio di controllo del codice sorgente
* Installare e distribuire in istanze AEM locali o remote
* Disinstalla da AEM

>[!NOTE]
>
>Puoi trovare un’altra origine di implementazione di riferimento, compresi i laboratori, su GitHub [qui](https://github.com/adobe-marketing-cloud-apps) e la sorgente del &quot;lavello da cucina&quot; [qui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Sviluppo per gli host IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Gli sviluppatori IOS devono essere a conoscenza di un problema aperto con le app Cordova in esecuzione su iOS 9. Questo problema impedisce che le richieste vengano effettuate a host non sicuri (come *http://localhost:4502*). Questo problema verrà risolto con una prossima versione di cordova-ios (consumata da Cordova CLI), ma nel frattempo sono disponibili due soluzioni alternative:

1. Come soluzione immediata, puoi comunque utilizzare uno qualsiasi dei simulatori iOS 8 senza alcun problema.
1. Se devi utilizzare iOS 9, le tue app -Info.plist (trovate dopo l&#39;esecuzione `cordova platform add ios` in &quot;&lt;app root=&quot;&quot;>/platform/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>Il file -Info.plist&quot;) può essere modificato manualmente per includere la seguente proprietà:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Per maggiori dettagli su &quot;App Transport Security&quot;, vedi la seguente sezione di [Documentazione pre-rilascio di Apple iOS9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e questo [Discussione sull&#39;overflow dello stack](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem-1}

* [Avvio AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md)
* [Struttura di un&#39;app](/help/mobile/phonegap-structure-an-app.md)
* [Creazione e modifica di app tramite la console App](/help/mobile/phonegap-apps-console.md)
* [Applicazioni a pagina singola](/help/mobile/phonegap-single-page-applications.md)
* [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)
* [Accesso alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Tracciare le prestazioni dell’app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Aggiungere Adobe Analytics all’applicazione mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifiche push](/help/mobile/phonegap-push-notifications.md)
* [Personalizzazione dei contenuti AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L&#39;anatomia di un&#39;app](/help/mobile/phonegap-apps-arch.md)
* [La tua app ibrida è pronta per AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e le responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
