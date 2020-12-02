---
title: 'Best practice  '
seo-title: 'Best practice  '
description: Segui questa pagina per apprendere le best practice e le linee guida utili per gli sviluppatori esperti AEM siti che desiderano creare modelli e componenti per app mobili.
seo-description: Segui questa pagina per apprendere le best practice e le linee guida utili per gli sviluppatori esperti AEM siti che desiderano creare modelli e componenti per app mobili.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Best practice   {#best-practices}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La creazione di un&#39;app AEM Mobile On-demand Services  è diversa dalla creazione di un&#39;app che viene eseguita direttamente nella shell Cordova (o PhoneGap). Gli sviluppatori dovrebbero avere familiarità con:

* Plug-in supportati oltre ai plug-in specifici di AEM Mobile .

>[!NOTE]
>
>Per informazioni dettagliate sui plug-in, consultate le risorse seguenti:
>
>* [Utilizzo dei plug-in Cordova in  AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilizzo  plug-in abilitati a Cordova specifici di AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* I modelli che utilizzano la funzionalità plug-in devono essere scritti in modo tale che siano ancora modificabili nel browser, senza che sia presente il ponte del plugin.

   * Ad esempio, attendere la funzione *deviceready* prima di tentare di accedere all&#39;API di un plug-in.

## Linee guida per AEM sviluppatori {#guidelines-for-aem-developers}

Le seguenti linee guida aiuteranno AEM sviluppatori esperti per i siti che desiderano creare modelli e componenti per app mobili:

**Struttura AEM modelli di siti per incoraggiare il riutilizzo e l&#39;estensibilità**

* Preferisci più file di script componenti su un singolo file monolitico

   * Sono disponibili diversi punti di estensione vuoti, ad esempio *customheaderlibs.html* e *customfooterlibs.html*, che consentono allo sviluppatore di modificare il modello di pagina mentre duplica il minor numero possibile di codice di base
   * I modelli possono quindi essere estesi e personalizzati tramite il meccanismo Sling *sling:resourceSuperType*

* Preferisci Sightly/HTL su JSP come linguaggio modulare

   * Questo favorisce la separazione del codice dalla marcatura, offre protezione XSS integrata e ha una sintassi più familiare

**Ottimizzazione per prestazioni su dispositivo**

* Lo script specifico per l&#39;articolo e i fogli di stile devono essere inclusi nel payload dell&#39;articolo, utilizzando il modello di sincronizzazione dei contenuti dps-article
* Gli script e i fogli di stile condivisi da più articoli devono essere inclusi nelle risorse condivise, tramite il modello di sincronizzazione dei contenuti dps-HTMLResources
* Non fare riferimento ad alcuno script esterno che bloccano il rendering

>[!NOTE]
>
>Per ulteriori informazioni sugli script esterni [qui](https://developers.google.com/speed/docs/insights/BlockingJS) per il blocco del rendering, consultate &lt;a0/>.

**Preferisci librerie JS e CSS lato client specifiche dell&#39;app a librerie specifiche per il Web**

* Per evitare problemi di sovraccarico nelle librerie come jQuery Mobile per gestire una vasta gamma di dispositivi e browser
* Quando un modello è in esecuzione nella visualizzazione Web di un&#39;app, potete controllare le piattaforme e le versioni che l&#39;app supporterà, nonché la consapevolezza che sarà presente il supporto JavaScript. Ad esempio, preferisci Ionic (forse solo il CSS) rispetto all&#39;interfaccia utente jQuery Mobile e Onsen rispetto all&#39;Bootstrap.

>[!NOTE]
>
>Per ulteriori informazioni su jQuery Mobile, fare clic [qui](https://jquerymobile.com/browser-support/1.4/).

**Preferisci le microlibrerie su uno stack completo**

* Il tempo necessario per inserire i contenuti nel vetro del dispositivo verrà rallentato da ogni libreria da cui dipendono gli articoli. Questo rallentamento è aggravato quando viene utilizzata una nuova visualizzazione Web per eseguire il rendering di ogni articolo, in modo che ogni libreria debba essere inizializzata nuovamente da zero
* Se gli articoli non sono creati come SPA (app a pagina singola), probabilmente non è necessario includere una libreria di stack completa come Angular
* Preferite librerie singole più piccole per aggiungere l&#39;interattività richiesta dalla pagina, ad esempio [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Ridurre al minimo le dimensioni del payload dell&#39;articolo**

* Utilizzate le risorse più piccole possibili in grado di coprire efficacemente il più grande viewport che si desidera supportare, a una risoluzione ragionevole
* Utilizzate uno strumento come *ImageOptim* sulle immagini per rimuovere eventuali metadati in eccesso

## Introduzione {#getting-ahead}

Per ulteriori informazioni sugli altri due ruoli e responsabilità, consulta le risorse seguenti:

* [Administrator](/help/mobile/aem-mobile.md)
* [Authoring](/help/mobile/aem-mobile-on-demand.md)
