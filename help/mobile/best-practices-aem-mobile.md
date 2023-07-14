---
title: Best practice per AEM Mobile On-demand Services
description: Scopri le best practice e le linee guida per gli sviluppatori AEM esperti per i siti che desiderano creare modelli e componenti per app mobili.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# Best practice {#best-practices}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

La creazione di un’app AEM Mobile On-demand Services è diversa dalla creazione di un’app che viene eseguita direttamente nella shell Cordova (o PhoneGap). Gli sviluppatori devono avere familiarità con:

* Plug-in supportati e plug-in specifici per AEM Mobile.

>[!NOTE]
>
>Per informazioni approfondite sui plug-in, consulta le risorse seguenti:
>
>* [Utilizzo dei plug-in Cordova in AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Utilizzo di plug-in abilitati per Cordova specifici per AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* I modelli che utilizzano la funzionalità del plug-in devono essere scritti in modo tale da poter essere creati nel browser senza che sia presente il bridge di plug-in.

   * Ad esempio, assicurati di attendere che *pronto all&#39;uso* prima di tentare di accedere all’API di un plug-in.

## Linee guida per gli sviluppatori AEM {#guidelines-for-aem-developers}

Le seguenti linee guida aiutano gli sviluppatori esperti di AEM per i siti, che desiderano creare modelli e componenti per app mobili:

**Strutturare modelli di siti AEM per incoraggiare il riutilizzo e l’estensibilità**

* Preferisci più file script di componenti rispetto a un singolo file monolitico

   * Vengono forniti diversi punti di estensione vuoti, ad esempio *customheaderlibs.html* e *customfooterlibs.html*, che consentono allo sviluppatore di modificare il modello della pagina duplicando il minor numero possibile di codice di base
   * I modelli possono quindi essere estesi e personalizzati tramite Sling’s *sling:resourceSuperType* meccanismo

* Preferisci Sightly/HTL a JSP come linguaggio di modelli

   * L’utilizzo di questa opzione favorisce la separazione del codice dal markup, offre una protezione XSS incorporata e una sintassi più familiare

**Ottimizza per prestazioni su dispositivo**

* I fogli di stile e gli script specifici dell’articolo devono essere inclusi nel payload dell’articolo, utilizzando il modello dps-article contentsync
* Gli script e i fogli di stile condivisi da più articoli devono essere inclusi nelle risorse condivise tramite il modello di sincronizzazione dei contenuti dps-HTMLResources
* Non fare riferimento a script esterni che bloccano il rendering

>[!NOTE]
>
>Ulteriori informazioni sugli script esterni che bloccano il rendering [qui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferisci librerie JS e CSS lato client specifiche per l’app rispetto a quelle specifiche per il web**

* Per evitare il sovraccarico in librerie come jQuery Mobile per gestire un&#39;ampia gamma di dispositivi e browser
* Quando un modello viene eseguito nella visualizzazione web di un’app, puoi controllare le piattaforme e le versioni che l’app supporterà e sapere che sarà presente il supporto JavaScript. Ad esempio, preferisci Ionic (forse solo CSS) rispetto a jQuery Mobile e Onsen UI rispetto a Bootstrap.

>[!NOTE]
>
>Per ulteriori informazioni su jQuery mobile, fai clic su [qui](https://jquerymobile.com/browser-support/1.4/).

**Preferisci le micro librerie a quelle full stack**

* Il tempo necessario per inserire i contenuti nel vetro del dispositivo verrà rallentato da ogni libreria da cui dipendono gli articoli. Questo rallentamento si aggrava quando si utilizza una nuova visualizzazione web per eseguire il rendering di ogni articolo, pertanto ogni libreria deve essere inizializzata di nuovo da zero
* Se i tuoi articoli non sono generati come SPA (app a pagina singola), probabilmente non devi includere una libreria full stack come Angular
* Preferisci librerie di dimensioni ridotte e monouso per aggiungere l’interattività necessaria per la pagina, ad esempio [Clic rapido](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Riduci al minimo le dimensioni del payload dell’articolo**

* Utilizzare le risorse più piccole possibili in grado di coprire efficacemente il riquadro di visualizzazione più ampio supportato, a una risoluzione ragionevole
* Utilizza uno strumento come *ImageOptim* sulle immagini per rimuovere eventuali metadati in eccesso

## Come procedere {#getting-ahead}

Per ulteriori informazioni sugli altri due ruoli e responsabilità, consulta le risorse seguenti:

* [Amministratore](/help/mobile/aem-mobile.md)
* [Autore](/help/mobile/aem-mobile-on-demand.md)
