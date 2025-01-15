---
title: Sviluppo di applicazioni mobili in AEM
description: Segui questa pagina per iniziare a sviluppare app mobili in AEM utilizzando Adobe PhoneGap Enterprise.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# Sviluppo di applicazioni mobili in AEM {#developing-mobile-applications-in-aem}

{{ue-over-mobile}}

L’AEM utilizza Adobe PhoneGap e le soluzioni Adobe Publishing per creare e gestire applicazioni mobili multipiattaforma ricche di contenuti e basate su utility:

* Gestisci tutte le app mobili aziendali in un’unica posizione.
* Esamina le app negli ambienti di sviluppo e staging senza la complessità dei profili di provisioning e l’impegno aggiuntivo per generare e caricare l’app per la condivisione.
* Utilizza l’ambiente di authoring AEM per creare e gestire contenuti avanzati per le tue app.
* Utilizza HTML5 con Adobe PhoneGap per creare esperienze avanzate con funzionalità native per i dispositivi.
* Introduzione delle visualizzazioni Web di HTML5 alle applicazioni **native** nuove o preesistenti tramite Cordova WebViews.
* Creazione, cura e condivisione di contenuti multimediali avanzati su tutti i canali di distribuzione, tra cui web, mobile-web, mobile-app e stampa.

AEM si integra con il servizio Adobe PhoneGap Build (`https://build.phonegap.com/`) per semplificare il processo di compilazione e distribuzione dell&#39;applicazione.

**Adobe ContentSync** consente agli utenti di scaricare facilmente gli aggiornamenti di pagina e contenuto Over-the-Air (OTA) sui propri dispositivi senza dover reinstallare l&#39;applicazione o scaricare da appStore, Google Play o altre origini dell&#39;app.

**Adobe Analytics** è completamente integrato nelle app AEM e consente il tracciamento dettagliato di distribuzione, geolocalizzazione, sistemi operativi, dispositivi, click-stream, tracciamento iBeacon e altro ancora.

## Creazione di app {#creating-apps}

Gli sviluppatori possono utilizzare il [PhoneGap Starter Kit per AEM](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) insieme alle risorse aggiuntive disponibili in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) per avviare le app AEM con PhoneGap, inclusa un&#39;app nativa di riferimento che esegue Cordova Webviews.

Il file readme per l’archivio Git di Starter Kit include un’esercitazione per l’utilizzo del kit di avvio:

* Personalizzare il branding
* Esempi di destinazioni di build e distribuzione Maven
* Configurazione dell’archivio di controllo Source
* Installazione e distribuzione in istanze AEM locali o remote
* Disinstalla da AEM

>[!NOTE]
>
>Un&#39;ulteriore origine di implementazione di riferimento, inclusi i laboratori, è disponibile su GitHub [qui](https://github.com/adobe-marketing-cloud-apps) e, l&#39;origine &quot;Kitchen-sink&quot; [qui](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Sviluppo per host IOS 9 e HTTP {#developing-for-ios-and-http-hosts}

Gli sviluppatori di IOS devono essere a conoscenza di un problema aperto relativo alle app Cordova in esecuzione su iOS 9. Questo problema impedisce l&#39;esecuzione di richieste a host non sicuri (ad esempio *http://localhost:4502*). Questo problema verrà risolto con una prossima versione di cordova-ios (utilizzata da Cordova CLI), ma nel frattempo sono disponibili due soluzioni alternative:

1. Come soluzione alternativa immediata, puoi comunque utilizzare senza problemi uno qualsiasi dei simulatori iOS 8.
1. Se devi utilizzare iOS 9, il file apps -Info.plist (trovato dopo l&#39;esecuzione di `cordova platform add ios` in &quot;&lt;app root>/platform/ios/&lt;app name>/&lt;app name>-Info.plist&quot;) può essere modificato manualmente per includere la seguente proprietà:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Per ulteriori dettagli su &quot;App Transport Security&quot;, consulta la seguente sezione della [documentazione prerelease iOS9 di Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) e questa [discussione sull&#39;overflow dello stack](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

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
