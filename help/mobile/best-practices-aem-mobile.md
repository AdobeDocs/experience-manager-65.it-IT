---
title: Best practice per AEM Mobile On-demand Services
description: Scopri le best practice e le linee guida per gli sviluppatori di Adobe Experience Manager (AEM) competenti per i siti che desiderano creare modelli e componenti per app mobili.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Best practice {#best-practices}

{{ue-over-mobile}}

La creazione di un’app AEM Mobile On-demand Services è diversa dalla creazione di un’app che viene eseguita direttamente nella shell Cordova (o PhoneGap). Gli sviluppatori devono avere familiarità con:

* Plug-in supportati come plug-in predefiniti e plug-in specifici per dispositivi mobili Adobe Experience Manager (AEM).

>[!NOTE]
>
>Per informazioni approfondite sui plug-in, consulta le risorse seguenti:
>
>* [Utilizzo dei plug-in Cordova in AEM Mobile](https://helpx.adobe.com/it/digital-publishing-solution/help/cordova-api.html)
>* [Utilizzo di plug-in abilitati per Cordova specifici per AEM Mobile](https://helpx.adobe.com/it/digital-publishing-solution/help/app-runtime-api.html)
>

* I modelli che utilizzano la funzionalità del plug-in devono essere scritti in modo tale da poter essere creati nel browser senza che sia presente il bridge di plug-in.

   * Ad esempio, assicurati di attendere la funzione *deviceready* prima di tentare di accedere all&#39;API di un plug-in.

## Linee guida per gli sviluppatori AEM {#guidelines-for-aem-developers}

Le seguenti linee guida aiutano gli sviluppatori AEM competenti per i siti che desiderano creare modelli e componenti per app mobili:

**Strutturare i modelli di siti AEM per incoraggiare il riutilizzo e l&#39;estensibilità**

* Preferisci più file script di componenti rispetto a un singolo file monolitico

   * Sono forniti diversi punti di estensione vuoti, ad esempio *customheaderlibs.html* e *customfooterlibs.html*, che consentono allo sviluppatore di modificare il modello della pagina duplicando il minor numero possibile di codici di base
   * I modelli possono quindi essere estesi e personalizzati tramite il meccanismo *sling:resourceSuperType* di Sling

* Preferisci Sightly/HTL a JSP come linguaggio di modelli

   * L’utilizzo di questa opzione favorisce la separazione del codice dal markup, offre una protezione XSS integrata e una sintassi più familiare

**Ottimizza per prestazioni su dispositivo**

* I fogli di stile e gli script specifici dell’articolo devono essere inclusi nel payload dell’articolo, utilizzando il modello dps-article contentsync
* Gli script e i fogli di stile condivisi da più articoli devono essere inclusi nelle risorse condivise tramite il modello di sincronizzazione dei contenuti dps-HTMLResources
* Non fare riferimento a script esterni che bloccano il rendering

>[!NOTE]
>
>Ulteriori informazioni sugli script esterni che bloccano il rendering [sono disponibili qui](https://developers.google.com/speed/docs/insights/BlockingJS).

**Preferisci le librerie JS e CSS lato client specifiche per l&#39;app rispetto a quelle specifiche per il Web**

* Per evitare il sovraccarico in librerie come jQuery Mobile per gestire un&#39;ampia gamma di dispositivi e browser
* Quando un modello viene eseguito nella visualizzazione web di un’app, puoi controllare le piattaforme e le versioni che l’app supporterà e sapere che sarà presente il supporto JavaScript. Ad esempio, preferisci Ionic (solo CSS) rispetto a jQuery Mobile e Onsen UI rispetto a Bootstrap.

>[!NOTE]
>
>Per ulteriori informazioni su jQuery mobile, fai clic [qui](https://jquerymobile.com/browser-support/1.4/).

**Preferisci le microlibrerie a quelle full stack**

* Il tempo necessario per inserire i contenuti nel vetro del dispositivo viene rallentato da ogni libreria da cui dipendono gli articoli. Questo rallentamento si aggrava quando si utilizza una nuova visualizzazione web per eseguire il rendering di ogni articolo, pertanto ogni libreria deve essere inizializzata di nuovo da zero
* Se i tuoi articoli non sono generati come SPA (app a pagina singola), probabilmente non devi includere una libreria full stack come Angular
* Preferisci librerie singole più piccole che consentono di aggiungere l&#39;interattività richiesta dalla pagina, ad esempio [Fastclick](https://github.com/ftlabs/fastclick) o [Velocity.js](https://velocityjs.org)

**Riduci al minimo le dimensioni del payload dell&#39;articolo**

* Utilizzare le risorse più piccole possibili in grado di coprire efficacemente il riquadro di visualizzazione più ampio supportato, a una risoluzione ragionevole
* Utilizza uno strumento come *ImageOptim* nelle immagini per rimuovere eventuali metadati in eccesso

## Come procedere {#getting-ahead}

Per ulteriori informazioni sugli altri due ruoli e responsabilità, consulta le risorse seguenti:

* [Amministratore](/help/mobile/aem-mobile.md)
* [Autore](/help/mobile/aem-mobile-on-demand.md)
