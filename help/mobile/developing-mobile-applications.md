---
title: Sviluppo di applicazioni mobili in AEM
seo-title: Sviluppo di applicazioni mobili in AEM
description: Seguite questa pagina per iniziare a sviluppare applicazioni mobili in AEM utilizzando  Adobe PhoneGap Enterprise.
seo-description: Seguite questa pagina per iniziare a sviluppare applicazioni mobili in AEM utilizzando  Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

AEM utilizza  soluzioni di pubblicazione di Adobe di Adobe PhoneGap e , consentendo di creare e gestire applicazioni mobili multipiattaforma basate su piattaforme e ricche di contenuti e basate su utility:

* Gestisci tutte le tue app mobili aziendali in un&#39;unica posizione.
* Rivedete le app in ambienti di sviluppo e di pre-produzione senza la complessità dei profili di provisioning e senza dover creare e caricare l&#39;app per la condivisione.
* Utilizzate l&#39;ambiente di authoring AEM per creare e gestire contenuti avanzati per le vostre app.
* Utilizzate HTML5 con  Adobe PhoneGap per creare esperienze avanzate con funzionalità native per dispositivi.
* Visualizzazioni Web HTML5 per applicazioni **native** nuove o preesistenti tramite Cordova WebViews.
* Crea, cura e condividi contenuti multimediali avanzati su tutti i canali di distribuzione, inclusi web, mobile-web, app e stampa.

AEM si integra con il Adobe  **[PhoneGap Build servizio](https://build.phonegap.com/)** per semplificare il processo di creazione e implementazione dell&#39;applicazione.

**Adobe** ContentSyncconsente agli utenti di scaricare facilmente gli aggiornamenti di pagina e contenuto Over-the-Air (OTA) sui loro dispositivi senza dover reinstallare l&#39;applicazione o scaricarla dall&#39;appStore, Google Play o da altre origini di app.

**Adobe** Analytics completamente integrato nelle app AEM e consente il tracciamento dettagliato di distribuzione, geolocalizzazione, sistemi operativi, dispositivi, flussi di clic, tracciamento iBeacon e altro ancora.

## Creazione di app {#creating-apps}

Gli sviluppatori possono utilizzare il [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) con risorse aggiuntive reperibili in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) per avviare AEM app con PhoneGap, inclusa un&#39;app nativa di riferimento che esegue Cordova Webviews.

Il file Leggimi per l&#39;archivio di Starter Kit Git include un&#39;esercitazione per l&#39;utilizzo del kit di avvio:

* Personalizzare il marchio
* Esempi di destinazione di creazione e distribuzione
* Configurazione archivio del controllo del codice sorgente
* Installare e distribuire in istanze AEM locali o remote
* Disinstallazione da AEM

>[!NOTE]
>
>Un&#39;ulteriore fonte di implementazione di riferimento, compresi i laboratori, è reperibile su GitHub [qui](https://github.com/adobe-marketing-cloud-apps) e, la sorgente &quot;cucina-lavello&quot; [qui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Sviluppo per host IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Gli sviluppatori IOS devono essere a conoscenza di un problema aperto con le app Cordova in esecuzione su iOS 9. Questo problema impedisce che vengano effettuate richieste a host non sicuri (ad esempio *http://localhost:4502*). Questo problema verrà risolto con una prossima release di cordova-ios (utilizzata dalla CLI Cordova), ma nel frattempo sono disponibili due soluzioni:

1. Come soluzione immediata, potete comunque utilizzare senza problemi uno qualsiasi dei simulatori iOS 8.
1. Se devi usare iOS 9, il file app -Info.plist (trovato dopo l&#39;esecuzione di `cordova platform add ios` in &quot;&lt;app root>/platform/ios/&lt;nome app>/&lt;nome app>/&lt;nome app>-Info.plist&quot;) può essere modificato manualmente per includere la seguente proprietà:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Per ulteriori informazioni su &quot;App Transport Security&quot;, consultate la sezione seguente della [prerelease docs](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) di Apple iOS9 e questa [discussione Stack Overflow](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem-1}

* [Avvio AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md)
* [Struttura di un&#39;app](/help/mobile/phonegap-structure-an-app.md)
* [Creazione e modifica di app tramite la console App](/help/mobile/phonegap-apps-console.md)
* [Applicazioni a pagina singola](/help/mobile/phonegap-single-page-applications.md)
* [Sviluppo di app con PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)
* [Accesso alle funzioni del dispositivo](/help/mobile/phonegap-access-device-features.md)
* [Tracciare le prestazioni delle app con  Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Aggiungere  Adobe Analytics all&#39;applicazione mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifiche push](/help/mobile/phonegap-push-notifications.md)
* [Personalizzazione  dei contenuti AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L&#39;anatomia di un&#39;app](/help/mobile/phonegap-apps-arch.md)
* [La tua app ibrida è pronta per  AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per  Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
