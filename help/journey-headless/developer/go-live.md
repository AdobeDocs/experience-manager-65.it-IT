---
title: Come pubblicare con la tua applicazione headless
description: In questa parte del Percorso di sviluppo headless AEM, scopri come distribuire in tempo reale un’applicazione headless.
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 49%

---

# Come pubblicare con la tua applicazione headless {#go-live}

In questa parte del [AEM Percorso di sviluppatori headless](overview.md), scopri come distribuire un’applicazione headless in tempo reale.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come aggiornare i contenuti tramite le API di AEM Assets](update-your-content.md) hai imparato ad aggiornare il contenuto headless esistente in AEM tramite API e ora dovresti:

* Comprendere l’API HTTP di AEM Assets.

Questo articolo si basa sulle nozioni di base che ti faranno capire come preparare il progetto AEM headless da pubblicare.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la pipeline di pubblicazione headless AEM e le considerazioni sulle prestazioni di cui devi tener conto prima di pubblicare l’applicazione.

* Scopri l’SDK per AEM e gli strumenti di sviluppo necessari
* Imposta un runtime di sviluppo locale per simulare il contenuto prima di iniziare a vivere
* Informazioni di base sulla replica dei contenuti AEM e sulla memorizzazione nella cache
* Proteggi e ridimensiona l’applicazione prima del lancio
* Monitoraggio dei problemi di prestazioni e debug

## L’SDK di AEM {#the-aem-sdk}

L’SDK di AEM viene utilizzato per generare e distribuire il codice personalizzato. È lo strumento principale che è necessario sviluppare e testare l&#39;applicazione headless prima di andare in diretta. Contiene i seguenti artefatti:

* Il file jar Quickstart: un file jar eseguibile che può essere utilizzato per impostare sia un’istanza di authoring che di pubblicazione
* Strumenti Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX
* Jar API Java™ - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per lo sviluppo rispetto ad AEM
* Jar Javadoc: i javadoc per il jar API Java™

## Strumenti di sviluppo aggiuntivi {#additional-development-tools}

Oltre all’SDK di AEM, sono necessari strumenti aggiuntivi per lo sviluppo e il test locale del codice e del contenuto:

* Java™
* Git
* Apache Maven
* La libreria Node.js
* L’IDE che preferisci

Poiché AEM è un&#39;applicazione Java™, devi installare Java™ e Java™ SDK per supportare lo sviluppo di AEM as a Cloud Service.

Git è ciò che utilizzerai per gestire il controllo del codice sorgente e per tenere traccia delle modifiche a Cloud Manager e, quindi, distribuirle su un’istanza di produzione.

AEM utilizza Apache Maven per creare progetti generati dall’archetipo del progetto Maven di AEM. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente di runtime JavaScript utilizzato per lavorare con le risorse front-end di un progetto AEM `ui.frontend` sottoprogetto. Node.js è distribuito con npm, che è di fatto Node.js Package Manager, utilizzato per gestire le dipendenze JavaScript.

## Panoramica dei componenti di un sistema AEM {#components-of-an-aem-system-at-a-glance}

Ora, osserviamo le parti costitutive di un ambiente AEM.

Un ambiente AEM completo è costituito da authoring, pubblicazione e Dispatcher. Questi stessi componenti sono resi disponibili nel runtime di sviluppo locale per semplificare l’anteprima del codice e del contenuto prima di iniziare a usare il programma.

* Il **servizio di authoring** è il luogo in cui gli utenti interni creano, gestiscono e visualizzano in anteprima i contenuti.

* **Servizio di pubblicazione** è considerato l’ambiente &quot;live&quot; ed è tipicamente ciò con cui gli utenti finali interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio Author, vengono distribuiti (replicati) nel servizio Publish. Il modello di implementazione più comune per le applicazioni headless AEM consiste nella connessione della versione di produzione dell’applicazione a un servizio di pubblicazione AEM.

* **Il Dispatcher** è un server web statico potenziato con il modulo Dispatcher di AEM. Memorizza nella cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti di codice o contenuto acquisiti dall&#39;applicazione headless, distribuisci gli aggiornamenti al runtime AEM locale. tra cui istanze locali dei servizi di authoring e pubblicazione AEM.

Assicurati di prendere nota delle distinzioni tra ogni componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più. Ad esempio, prova gli aggiornamenti del contenuto sull’authoring o testa il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un Dispatcher e un server http Apache saranno sempre posti davanti a un’istanza di pubblicazione AEM. Fornisce servizi di caching e sicurezza per il sistema AEM, pertanto è fondamentale testare il codice e gli aggiornamenti di contenuto anche in Dispatcher.

## Anteprima del codice e del contenuto localmente con l’ambiente di sviluppo locale {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Per preparare il progetto senza testa AEM per il lancio, assicurati che tutte le parti costitutive del progetto funzionino bene.

Per farlo, devi mettere tutto insieme: codice, contenuto e configurazione, e testalo in un ambiente di sviluppo locale per essere pronto al funzionamento.

L&#39;ambiente di sviluppo locale si compone di tre aree principali:

1. Progetto AEM - contiene tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori AEM lavoreranno
1. Local AEM Runtime: versioni locali dei servizi di authoring e pubblicazione AEM utilizzati per distribuire il codice dal progetto AEM
1. Esecuzione del Dispatcher locale: una versione locale del server Web Apache httpd che include il modulo Dispatcher

Una volta configurato l’ambiente di sviluppo locale, puoi simulare il servizio dei contenuti all’app React distribuendo localmente un server Node statico.

Per maggiori informazioni sulla configurazione di un ambiente di sviluppo locale e di tutte le dipendenze necessarie per l’anteprima dei contenuti, vedi [Documentazione sulla distribuzione di produzione](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=en).

## Prepara la tua applicazione AEM headless per GoLive {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Ora è il momento di preparare l&#39;applicazione senza testa AEM per il lancio, seguendo le best practice descritte di seguito.

### Proteggere l&#39;applicazione headless prima di Launch {#secure-and-scale-before-launch}

1. Preparare [Autenticazione](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) per le richieste GraphQL

### Struttura del modello e output GraphQL {#structure-vs-output}

* Evita di creare query con output superiore a 15 KB di JSON (gzip compresso). I file JSON lunghi richiedono un uso intensivo delle risorse per l’analisi da parte dell’applicazione client.
* Evita più di cinque livelli nidificati di gerarchie di frammenti. Livelli aggiuntivi rendono difficile per gli autori dei contenuti valutare l’impatto delle loro modifiche.
* Utilizza query con più oggetti invece di modellare query con gerarchie di dipendenza all’interno dei modelli. In questo modo si ottiene una flessibilità a lungo termine per ristrutturare l’output JSON senza dover apportare molte modifiche al contenuto.

### Massimizza il rapporto Hit-cache CDN {#maximize-cdn}

* Non utilizzare query GraphQL dirette, a meno che stia richiedendo contenuto in tempo reale dalla superficie.
   * Utilizza le query persistenti quando possibile.
   * Fornisci TTL CDN oltre 600 secondi in modo che la CDN possa memorizzarli nella cache.
   * AEM può calcolare l’impatto di una modifica del modello sulle query esistenti.
* Dividi i file JSON/le query GraphQL tra una velocità di modifica bassa e alta del contenuto per ridurre il traffico client a CDN e assegnare un valore TTL più alto. In questo modo si riduce al minimo la validità del CDN con il server di origine.
* Per annullare attivamente la validità del contenuto dalla rete CDN, utilizza l’eliminazione morbida. In questo modo la rete CDN può scaricare nuovamente il contenuto senza causare una perdita di cache.

>[!NOTE]
>
>Vedi [Risorse aggiuntive](#additional-resources) per ulteriori informazioni su CDN e memorizzazione in cache.

### Migliora il tempo di download dei contenuti headless {#improve-download-time}

* Assicurati che i client HTTP utilizzino HTTP/2.
* Assicurati che i client HTTP accettino la richiesta di intestazioni per gzip.
* Riduci al minimo il numero di domini utilizzati per ospitare JSON e gli artefatti di riferimento.
* Utilizzo `Last-modified-since` per aggiornare le risorse.
* Utilizza l’output `_reference` nel file JSON per iniziare a scaricare risorse senza dover analizzare file JSON completi.

<!-- End of CDN Review -->

## Distribuzione alla produzione {#deploy-to-production}

La distribuzione in Produzione può dipendere dal fatto che sia presente un *tradizionale* AEM’istanza che viene implementata utilizzando Maven o in Adobe Managed Services (AMS) e quindi utilizzando Cloud Manager.

## Distribuzione in produzione tramite Maven {#deploy-to-production-maven}

Per *tradizionale* implementazione (non AMS) tramite Maven, vedi la [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) per una panoramica.

## Distribuzione in produzione tramite Cloud Manager {#deploy-to-production-cloud-manager}

Se sei un cliente AMS che utilizza Cloud Manager, puoi inviare gli aggiornamenti di codice a un [archivio Git centralizzato in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html).

Dopo aver caricato gli aggiornamenti su Cloud Manager, implementali in AEM utilizzando [pipeline CI/CD di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Monitoraggio delle prestazioni {#performance-monitoring}

Per garantire agli utenti la migliore esperienza possibile quando utilizzano l’applicazione AEM headless, è importante monitorare le metriche delle prestazioni chiave, come illustrato di seguito:

* Convalida delle versioni di anteprima e di produzione dell’app
* Verifica delle pagine di stato di AEM per lo stato di disponibilità del servizio corrente
* Accesso ai rapporti sulle prestazioni
   * Prestazioni della distribuzione
      * Server di origine - numero di chiamate, tassi di errore, carichi della CPU, traffico del payload
   * Prestazioni dell’authoring
      * Verifica il numero di utenti, richieste e caricamento
* Accedere ai rapporti sulle prestazioni specifici per app e spazio
   * Una volta che il server è attivo, controllare se le metriche generali sono verde/arancione/rosso, quindi identificare problemi specifici dell’app
   * Aprire gli stessi rapporti sopra filtrati di app o spazio (ad esempio desktop Photoshop, paywall)
   * Utilizzare le API del registro Splunk per accedere alle prestazioni del servizio e dell’applicazione
   * Contattare l’Assistenza clienti in caso di altri problemi.

## Risoluzione dei problemi {#troubleshooting}

### Debugging {#debugging}

Segui queste best practice come approccio generale al debug:

* Convalida funzionalità e prestazioni con la versione di anteprima dell’applicazione
* Convalida funzionalità e prestazioni con la versione di produzione dell’applicazione
* Convalida con JSON l’anteprima dell’Editor di frammento di contenuto
* Per verificare la presenza di applicazioni client o problemi di consegna, controlla il JSON nell’applicazione client
* Per verificare la presenza di problemi relativi al contenuto o AEM nella cache, controlla il JSON utilizzando GraphQL

### Registrazione di un bug con Support {#logging-a-bug-with-support}

Per segnalare in modo efficiente un bug con il supporto, se hai bisogno di ulteriore assistenza, completa i seguenti passaggi:

* Se necessario, acquisisci le schermate del problema
* Documenta un modo per riprodurre il problema
* Documenta il contenuto con cui il problema si ripresenta
* Segnala un problema tramite il portale di supporto AEM con la priorità appropriata

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il Percorso per sviluppatori AEM headless! Ora dovresti avere imparato:

* La differenza tra distribuzione headless e headful dei contenuti.
* Le funzionalità headless di AEM.
* Come organizzare un progetto AEM headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come pubblicare con un progetto AEM headless.
* Cosa fare dopo il completamento del go-live.

Hai già lanciato il tuo primo progetto AEM Headless o ora hai tutte le conoscenze per farlo. Ottimo lavoro!

### Esplora le applicazioni a pagina singola {#explore-spa}

Non c&#39;è bisogno di fermare i negozi senza testa in AEM, però. In [Introduzione al percorso](getting-started.md#integration-levels), ha discusso come AEM supporta non solo la consegna headless e i modelli tradizionali full-stack, ma supporta anche modelli ibridi che combinano i vantaggi di entrambi.

Se questo tipo di flessibilità è necessario per il progetto, continua con la parte facoltativa e aggiuntiva del percorso, [Come creare applicazioni a pagina singola (SPA) con AEM.](create-spa.md)

## Risorse aggiuntive {#additional-resources}

* [Guida allo sviluppo AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [Cloud Manager per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=en)

* Cache CDN

   * [Controllo di una cache CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Configurazione della [Rewriter CDN](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*cerca il rewriter CDN*)
