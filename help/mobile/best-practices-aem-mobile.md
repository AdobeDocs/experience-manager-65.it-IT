---
title: Best practice
seo-title: Best Practices
description: Segui questa pagina per scoprire le best practice e linee guida utili per gli sviluppatori esperti AEM per i siti che desiderano creare modelli e componenti per app mobili.
seo-description: Follow this page to  learn best practices and guidelines that will help experienced AEM developers for sites, who want to build mobile app templates and components.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Best practice   {#best-practices}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La creazione di un’app AEM Mobile On-demand Services è diversa dalla creazione di un’app che viene eseguita direttamente nella shell Cordova (o PhoneGap). Gli sviluppatori devono avere familiarità con:

* Plug-in supportati out-of-the-box e plug-in specifici di AEM Mobile.

>[!NOTE]
>
>Per ulteriori informazioni sui plug-in, consulta le risorse seguenti:
>
>* [Utilizzo dei plug-in Cordova in AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilizzo di plug-in abilitati per Cordova specifici per AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* I modelli che utilizzano la funzionalità dei plug-in devono essere scritti in modo tale che siano ancora modificabili nel browser, senza che il bridge del plugin sia presente.

   * Ad esempio, assicurati di aspettare il *deviceready* prima di tentare di accedere all’API di un plug-in.

## Linee guida per gli sviluppatori AEM {#guidelines-for-aem-developers}

Le seguenti linee guida aiuteranno gli sviluppatori esperti AEM per i siti che desiderano creare modelli e componenti per app mobili:

**Struttura AEM modelli di siti per incoraggiare il riutilizzo e l’estensibilità**

* Preferisce più file di script componenti su un singolo file monolitico

   * Vengono forniti diversi punti di estensione vuoti, ad esempio *customheaderlibs.html* e *customfooterlibs.html*, che consente allo sviluppatore di modificare il modello di pagina mentre duplica il minor numero possibile di codice di base
   * I modelli possono quindi essere estesi e personalizzati tramite Sling&#39;s *sling:resourceSuperType* meccanismo

* Preferisci Sightly/HTL su JSP come linguaggio template

   * L&#39;utilizzo di questo incoraggia una separazione del codice dal markup, offre una protezione XSS integrata e ha una sintassi più familiare

**Ottimizzare le prestazioni su dispositivi**

* Lo script specifico per l&#39;articolo e i fogli di stile devono essere inclusi nel payload dell&#39;articolo, utilizzando il modello di sincronizzazione dei contenuti dps-article
* Gli script e i fogli di stile condivisi da più di un articolo devono essere inclusi nelle risorse condivise tramite il modello contentsync dps-HTMLResource
* Non fare riferimento a script esterni che bloccano il rendering

>[!NOTE]
>
>Ulteriori informazioni sugli script esterni per il blocco del rendering [qui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferisci librerie JS e CSS lato client specifiche per l’app rispetto a librerie specifiche per il web**

* Per evitare sovraccarichi in librerie come jQuery Mobile per gestire un’enorme quantità di dispositivi e browser
* Quando un modello è in esecuzione nella visualizzazione web di un&#39;app, hai il controllo sulle piattaforme e sulle versioni che l&#39;app supporterà, nonché sulla conoscenza che sarà presente il supporto JavaScript. Ad esempio, preferisci Ionic (forse solo il CSS) rispetto all’interfaccia utente jQuery Mobile e Onsen rispetto alla Bootstrap.

>[!NOTE]
>
>Per ulteriori informazioni su jQuery mobile, fai clic su [qui](https://jquerymobile.com/browser-support/1.4/).

**Preferisci le microlibrerie a tutto stack**

* Il tempo necessario per inserire i contenuti nel vetro del dispositivo verrà rallentato da ogni libreria da cui dipendono gli articoli. Questo rallentamento viene aggravato quando si utilizza una nuova visualizzazione Web per il rendering di ogni articolo, in modo che ogni libreria debba essere inizializzata di nuovo da zero
* Se gli articoli non sono generati come SPA (app a pagina singola), probabilmente non è necessario includere una libreria di stack completa come ad Angular
* Preferisci librerie a scopo singolo più piccole per aggiungere l’interattività necessaria per la pagina, ad esempio [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Ridurre al minimo le dimensioni del payload dell’articolo**

* Utilizzare le risorse più piccole possibili che possono coprire efficacemente il più grande riquadro di visualizzazione che si sta supportando, a una risoluzione ragionevole
* Usa uno strumento come *ImmagineOptim* sulle immagini per rimuovere eventuali metadati in eccesso

## Come procedere {#getting-ahead}

Per ulteriori informazioni sugli altri due ruoli e responsabilità, consulta le risorse seguenti:

* [Amministratore](/help/mobile/aem-mobile.md)
* [Autore](/help/mobile/aem-mobile-on-demand.md)
