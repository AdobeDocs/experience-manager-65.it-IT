---
title: Contribuire all’AEM
description: L’AEM è sviluppato seguendo metodologie comprovate comunemente utilizzate in grandi progetti open source
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2642'
ht-degree: 0%

---

# Contribuire all’AEM{#contributing-to-aem}

## Metodologia di sviluppo {#development-methodology}

L’AEM è sviluppato seguendo metodologie comprovate comunemente utilizzate in grandi progetti open source. Molti elementi core nello stack tecnologico dell’AEM sono infatti mantenuti come progetti open source attivi, come Sling e Jackrabbit, che hanno contribuito alla Apache Software Foundation. Un aspetto importante di questo spirito che è presente in AEM è che si è incoraggiati a utilizzare le mailing list disponibili e i forum online per interazioni dirette con il team di sviluppo.

Se contribuisci ai componenti dell’AEM, impara a conoscere l’AEM come faresti quando contribuisci a un progetto open-source e comunica con il team di base esistente come faresti quando hai intenzione di contribuire a tale progetto.

## Esperienza richiesta {#required-experience}

Il protocollo HTTP (HyperText Transfer Protocol) è fondamentale per tutte le attività svolte. Pertanto, prima di contribuire all’AEM, è necessario avere una conoscenza approfondita di HTTP, idealmente nella misura in cui è possibile scrivere una propria implementazione Java™ di un server HTTP multithread con thread-pooling. È inoltre necessario conoscere il comportamento keep-alive di HTTP/1.1 e le interazioni lato server/client con JavaScript, in particolare lo stile di interazione asincrona rappresentato dall&#39;AJAX.

Poiché il dinamismo delle pagine e i contenuti interattivi sono fondamentali per l&#39;esperienza WM, è essenziale avere una conoscenza approfondita del modello a oggetti documento e del suo potenziale di manipolazione programmatica in risposta agli eventi. È necessario avere una certa conoscenza, ad esempio, della manipolazione DOM in tempo reale e del comportamento di trascinamento su più documenti del browser (ad esempio, utilizzando gli iframe).

Al livello più alto, dovresti avere una solida conoscenza di:

* il protocollo [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferibilmente [HTML5](https://html.spec.whatwg.org/))
* Cascading Style Sheets
* XML (Extensible Markup Language)
* Modelli di progettazione JavaScript e XML (AJAX) asincroni
* Notazione oggetto JavaScript (JSON)
* Modello a oggetti documento
* Interazioni con stato e senza stato
* [Identificatori risorse uniformi](https://www.ietf.org/rfc/rfc2396.txt)
* Cookie del browser
* e altri concetti moderni di sviluppo web

Lo stack tecnologico di Adobe Experience Manager si basa sul contenitore OSGI [Apache Felix](https://felix.apache.org/documentation/index.html) con il framework web [Apache Sling](https://sling.apache.org/index.html) e incorpora un archivio di contenuti Java™ ([JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)) basato su [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/jcr-api.html). Acquisisci familiarità con questi singoli progetti e con qualsiasi altro componente open-source (ad esempio, Apache Lucene) utilizzato nell’area in cui intendi contribuire.

## Conoscenza tribale {#tribal-knowledge}

Alcuni concetti e principi guida sono profondamente radicati nella cultura antica. Questa sezione elenca alcuni dei problemi &quot;profondamente legati al DNA&quot; che dovresti conoscere.

### Tutto è contenuto {#everything-is-content}

Il contenuto include non solo tutti i dati persistenti dell’applicazione web. Il codice del programma, le librerie, gli script, i modelli, i HTML, i CSS, le immagini e gli artefatti di tutti i tipi, qualsiasi cosa e tutto viene mantenuto nell’archivio dei contenuti e importato/esportato sotto forma di pacchetti tramite Gestione pacchetti e Condivisione pacchetti.

### Modello di David {#david-s-model}

Il modo in cui il contenuto deve essere modellato in un Java™ Content Repository richiede un modo di pensare completamente diverso rispetto a quello che è pratica comune nel settore del software per la modellazione dei dati nel mondo relazionale. Lettura essenziale per qualsiasi nuovo arrivato alla gestione dei contenuti la modalità JCR è [Modello di David: una guida per la modellazione dei contenuti](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

L&#39;approccio REST è profondamente radicato in ciò che facciamo. Ciò significa, tra l’altro, evitare interazioni con informazioni di stato e tenere presente che gli URI sono indirizzi definitivi per contenuti e servizi.

REST (REpresentational State Transfer) si riferisce allo stile architettonico del software su cui si basa il World Wide Web. Descrive gli elementi chiave che fanno funzionare il Web e fornisce quindi un insieme di principi per la progettazione del software basato sul Web. Durante la progettazione di un’API da utilizzare sul web, ha quindi senso aderire a queste &quot;best practice&quot;.

Poiché REST fornisce la filosofia che guida gran parte di ciò che facciamo, dovresti considerare essenziale diventare esperti nei principi del design RESTful. Un buon punto di partenza è la dissertazione di [Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Risoluzione richiesta Sling {#sling-request-resolution}

Un aspetto chiave per comprendere l’AEM è il modo in cui le richieste in entrata si relazionano al contenuto e al comportamento dell’applicazione, il modo in cui il contenuto è strutturato nell’archivio dei contenuti e il punto in cui l’AEM cerca la logica dell’applicazione per gestire la richiesta. Scopri la decomposizione dell’URL Apache [Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html) e il modo in cui applica lo stile dell’architettura REST e i vincoli di sistema senza stato, memorizzabili in cache e su più livelli.

Gli aspetti chiave per comprendere la risoluzione delle richieste di Apache Sling sono il modo in cui le richieste vengono principalmente mappate a una risorsa specifica nel Content Repository, il modo in cui le proprietà aggiuntive della richiesta, insieme alle proprietà di questi oggetti di contenuto, determinano quale codice dell’applicazione viene richiamato per riprodurre il contenuto e il modo in cui il codice in /apps sostituisce il codice in /libs.

### Quickstart {#quickstart}

Nessun passaggio tre: per installare ed eseguire, è sufficiente scaricare e fare doppio clic sul file JAR Quickstart. Non c&#39;è nessun passaggio tre. Per qualsiasi funzionalità opzionale aggiuntiva è sufficiente installare il pacchetto appropriato da Condivisione pacchetti.

Dimensioni ridotte di Quickstart: mantenere al minimo le dimensioni del file JAR Quickstart. Utilizza in modo intelligente e ottimizzato le librerie, spostando le funzionalità facoltative in Condivisione pacchetti.

Tempi di avvio più rapidi: quando si apporta una modifica che potrebbe influire sul tempo di avvio, assicurarsi che sia più breve, non più lungo.

### Snella e media {#lean-and-mean}

Preferiamo il codice e i progetti leggeri, piccoli, veloci ed eleganti. &quot;Abbastanza buono&quot; non basta.

Riutilizzo del codice: la nostra architettura di prodotto basata su OSGi e la filosofia &quot;Everything is content&quot; (tutto è contenuto) ci offrono opportunità insolitamente buone per il riutilizzo del codice e degli artefatti. Cerchiamo di sfruttare questo fatto ogni volta possibile per mantenere le funzioni snelle e mediocri.

Accoppiamento libero: favoriamo le interazioni liberamente accoppiate rispetto a dipendenze strette e &quot;intimità indesiderata&quot;. L&#39;accoppiamento flessibile consente inoltre un maggior riutilizzo del codice.

### Non interrompere la demo {#don-t-break-the-demo}

Acquisisci familiarità con gli script demo e le funzionalità dei prodotti che vengono mostrati più spesso nelle demo. Devi capire che niente di ciò che fai deve mai interrompere una funzione di &quot;script dimostrativo&quot;. Il prodotto di base deve essere sempre pronto per la dimostrazione, anche durante lo sviluppo.

### Design affidabile {#design-for-reliability}

Ci impegniamo a progettare e codificare le funzioni in modo fallsoft, in modo che (ad esempio) un problema con un singolo elemento DOM non faccia in modo che un’intera pagina non venga riprodotta. In altre parole: fare cose che dovrebbero essere fatali, fatali. Rendi tutto il resto superabile. Rendi il prodotto &quot;perdonante&quot;.

### Anormale è il nuovo normale {#abnormal-is-the-new-normal}

Non dipendere dagli hook di arresto, assicurati che la pulizia venga eseguita all&#39;avvio. La terminazione anomala è la terminazione normale.

`shutdown == kill -9 == power outage`

### Essere pronti per il clustering elastico {#be-ready-for-elastic-clustering}

Essere sempre pronti per il clustering elastico; presupporre sempre che sia presente il clustering. In genere, rispettare tutto ciò che si trova nell’archivio dei contenuti significa supportare il clustering integrato.

### Progettazione per compatibilità con le versioni precedenti {#design-for-backward-compatibility}

Non devi fare nulla per violare il vecchio codice di un cliente. Considera solo `/libs` per contenere codice prodotto che può essere aggiornato durante un aggiornamento. La sezione `/apps` dell&#39;archivio è il codice del progetto e la sezione `/etc` contiene configurazioni personalizzate che devono essere mantenute. In genere, non sovrascrivere nulla in `/apps`, `/content` e `/home`. Dopo un aggiornamento, il vecchio codice di progetto, le configurazioni e il contenuto dovrebbero continuare a funzionare come prima dell’aggiornamento.

La progettazione per la compatibilità con le versioni precedenti assicura inoltre che l’esperienza di aggiornamento corrisponda alla semplicità dell’installazione iniziale. È sufficiente arrestare l’AEM, sostituire il file JAR di Quickstart e riavviare l’AEM. Con una base di installazione in rapida crescita, l&#39;efficienza dell&#39;aggiornamento è un vantaggio sempre più significativo.

Anche se le API esistenti possono e devono essere contrassegnate come obsolete quando sono più recenti, una migliore funzionalità le sostituisce, tutte le API che sono state rese pubbliche in una precedente versione 5.x devono rimanere funzionali, in quanto potrebbero essere utilizzate nel codice personalizzato dell’applicazione. Nessuna API di questo tipo deve essere rimossa.

È inoltre necessario tenere presente la compatibilità con le versioni precedenti per quanto riguarda la coerenza generale della struttura dei contenuti e l’esperienza utente.

## Concetti di base {#core-concepts}

**Istanza Autore** - In genere, per motivi di sicurezza, governance e altro, un sito di produzione divide le istanze di AEM in istanze Autore e Publish. Per ulteriori informazioni sull’architettura di distribuzione (incluse le istanze Author/Publish), consulta la documentazione sulle istanze AEM.

**Caching, frittura e cottura** - In genere, i concetti di cottura e frittura rappresentano una distinzione importante tra i diversi sistemi di gestione dei contenuti web. In gergo CMS, &quot;baking&quot; si riferisce al concetto di commit dei dati in file statici al momento della pubblicazione, mentre &quot;fying&quot; si riferisce al concetto di elaborazione dei dati per la presentazione finale al momento della richiesta (ovvero, appena nel tempo).

**Clustering e bilanciamento del carico** - Per aumentare la disponibilità e migliorare le prestazioni di un ambiente di produzione, è comune combinare più istanze di Author e/o Publish (in cluster), rendendole disponibili a gruppi diversi di utenti o bilanciandole con il carico dietro una configurazione di Dispatcher.

È inoltre possibile combinare più istanze dell&#39;archivio dei contenuti per creare una soluzione JCR *ad alta disponibilità*, che può essere integrata con la soluzione AEM per massimizzare la protezione da guasti hardware e software. Per ulteriori informazioni, vedere [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter).

**Componente** - In AEM, un componente è un tipo di oggetto, le cui istanze possono generalmente essere create trascinandole e rilasciandole, ad esempio, dal Sidekick. Ad esempio, i componenti predefiniti forniti con AEM includono i componenti Testo, Titolo, Tag Cloud, Carosello, Immagine ed Elenco, tutti disponibili dal Sidekick in fase di esecuzione.

**Content Finder** - In modalità di authoring, Content Finder è un pannello speciale (cornice) sul lato sinistro della pagina che, a seconda della scheda selezionata nella parte superiore, visualizza elenchi di immagini, documenti, risorse di Flash, pagine, paragrafi o risorse del repository che è possibile trascinare e rilasciare dal Content Finder alla pagina su cui si sta lavorando (sulla destra).

**Risorse digitali** - In AEM, Digital Assets è (in genere) costituito da immagini e file rich media. Per ulteriori informazioni, consulta Utilizzo di Digital Assets in DAM.

**Dispatcher** - Dispatcher è uno strumento di caching e bilanciamento del carico e fornisce alcune protezioni di sicurezza.

**Widget ExtJS** - La maggior parte degli elementi dell&#39;interfaccia utente dell&#39;AEM utilizza ExtJS, una libreria di widget di terze parti scritta in JavaScript. ExtJS dispone di widget per l&#39;interfaccia utente personalizzabili a elevate prestazioni e di un modello di componente ben progettato ed estensibile.

**JCR, Java™ Content Repository** - La specifica Java™ Content Repository (JSR-283) fornisce sia un modello di dati astratto che un&#39;interfaccia di programmazione dell&#39;applicazione per la realizzazione di un repository di dati NoSQL ampiamente scalabile che combina le caratteristiche di un file system e di un database di oggetti. Anche se non è necessario comprendere JSR-283 in modo esaustivo, è necessario prendere tempo per acquisire familiarità con le funzionalità di base di JCR e il modello dati sottostante, perché JCR è ciò che rende possibile la filosofia &quot;tutto è contenuto&quot; dell’AEM.

In sostanza, JCR è un sistema di nodi e proprietà, in cui i nodi possono ereditare da altri nodi e tutto il contenuto viene archiviato come proprietà *values*. Oltre all’ereditarietà ordinaria, JCR consente il concetto di nodi &quot;mixin&quot;, che consente la modellazione di più ereditarietà.

JCR dispone di diversi tipi di nodo e tipi di proprietà predefiniti, ma in generale il sistema di digitazione è flessibile e uno dei punti di forza di JCR è che consente di memorizzare e gestire contenuti strutturati e non strutturati con la stessa facilità. In altre parole, JCR può gestire dati altamente strutturati, ma può anche ospitare strutture di dati dinamici arbitrari senza vincoli di schema.

JavaDoc per l&#39;API Java™ di JCR è disponibile da [Apache Software Foundation - JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html).

Prima di tentare di leggere JavaDoc o la specifica JCR stessa, è possibile esaminare [questa spiegazione di alto livello](/help/sites-developing/the-basics.md#java-content-repository) di JCR implementata da Adobe Experience Services.

**Multi-Site Manager (MSM)** - La funzione MSM di AEM consente ai clienti di gestire contenuti multilingue e multinazionali, consentendo loro di bilanciare il branding centralizzato con i contenuti localizzati.

**OSGi** - OSGi è la tecnologia di runtime basata sui servizi che fornisce la base per lo sviluppo Java™ modularizzato in AEM. Si tratta di un framework che fornisce non solo un ambiente di caricamento ed esecuzione altamente dinamico (e sicuro) per le risorse di codice (noti come bundle), ma anche un controllo completo sulla visibilità e sul ciclo di vita dei vari servizi esposti dai bundle. Un registro di servizio fornisce un modello di cooperazione per i bundle che tiene conto delle dinamiche del ciclo di vita (e dei requisiti di versione). OSGi risolve molti dei problemi che gli application server erano destinati a risolvere, ma lo fa in modo leggero e altamente dinamico, rendendo possibile, ad esempio, l’implementazione a caldo dei servizi (rendendo il nuovo codice immediatamente disponibile senza riavviare il server).

**Parsys, Sistema paragrafi** - Il sistema paragrafi (parsys) è un componente composto che consente agli autori di aggiungere componenti di tipi diversi a una pagina e contiene altri componenti paragrafo. Ogni tipo di paragrafo è rappresentato come componente. Anche il sistema paragrafo è un componente che contiene gli altri componenti paragrafo.

**Microkernel** - Ogni area di lavoro nell&#39;archivio può essere configurata separatamente per archiviare i dati tramite un microkernel specifico, ovvero una classe che gestisce la lettura e la scrittura dei dati. Analogamente, l’archivio delle versioni a livello di repository può anche essere configurato in modo indipendente per utilizzare un particolare microkernel. Sono disponibili diversi microkernel, in grado di memorizzare dati in vari formati di file o database relazionali. (Ad esempio, esistono gestori di persistenza per MongoDB, DB2® o Oracle) Il microkernel predefinito per l’AEM è TarMK (vedi di seguito ulteriori informazioni).

**Istanza di Publish** - Per motivi di sicurezza, governance e altro, un sito di produzione divide in genere le istanze dell&#39;AEM in istanze di authoring e Publish. Per ulteriori informazioni sull’architettura di distribuzione (incluse le istanze Author/Publish), consulta la documentazione sulle istanze AEM.

**Quickstart** - A differenza di molti altri programmi, puoi installare AEM utilizzando un singolo file JAR autoestraente &quot;Quickstart&quot;. Quando fai doppio clic sul file JAR per la prima volta, tutto ciò che ti serve viene installato automaticamente. Il file JAR quickstart include tutti i file necessari per l&#39;archivio CRX (incluse le strutture amministrative), i servizi dell&#39;archivio virtuale, i servizi di indicizzazione e ricerca, i servizi del flusso di lavoro, la sicurezza e un server Web, oltre al motore CQ Servlet Engine (CQSE) e a tutti i servizi AEM. Nessun altro file da installare: Quickstart è autonomo.

La prima volta che avvii Quickstart, crea in background un intero archivio compatibile con JCR, il che può richiedere alcuni minuti. Dopo questo avvio iniziale, le avviazioni successive sono molto più rapide in quanto l’infrastruttura dell’archivio è già stata impostata.

Molte opzioni di avvio (come il numero di porta attivo e se l’istanza AEM in questione deve essere un’istanza di Publish rispetto a un’istanza di authoring e molto altro) possono essere controllate rinominando in modo appropriato il file Quickstart. Per visualizzare un elenco di opzioni a questo proposito, esegui il file JAR con &quot;-help&quot; sulla riga di comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agenti di replica** - Gli agenti di replica sono centrali per l&#39;AEM in quanto meccanismo utilizzato per attivare il contenuto di Publish da un ambiente di authoring a uno di pubblicazione; svuotare il contenuto dalla cache di Dispatcher; restituire il contenuto generato dall&#39;utente (ad esempio, l&#39;input del modulo) dall&#39;ambiente di Publish all&#39;ambiente di authoring.

**Scaffolding** - Con lo scaffolding è possibile creare un modulo (uno scaffolding) con campi che riflettono la struttura desiderata per le pagine e quindi utilizzare questo modulo per creare facilmente pagine basate su questa struttura.

**Segmentazione** - I visitatori del sito hanno interessi e obiettivi diversi quando accedono al sito. Comprendere gli obiettivi dei visitatori e soddisfare le loro aspettative è un importante prerequisito di successo per il marketing online. La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i dettagli di un visitatore.

**Sidekick** - Il Sidekick è una finestra mobile simile a una tavolozza visualizzata nella pagina modificabile, dalla quale è possibile trascinare nuovi componenti e eseguire le azioni applicabili alla pagina.

**Site Catalyst** - Il SiteCatalyst offre agli addetti al marketing un&#39;unica posizione per misurare, analizzare e ottimizzare i dati integrati di tutte le iniziative online su più canali di marketing. Puoi utilizzare Adobe SiteCatalyst per analizzare i dati dai siti web dell’AEM.

**Archiviazione Tar (TarMK)** - TarMK è il sistema di persistenza predefinito in AEM. Anche se l’AEM può essere configurato per utilizzare un sistema di persistenza diverso (come MongoDB), TarMK ha alcuni vantaggi in quanto è ottimizzato per le prestazioni per i tipici casi d’uso JCR (quindi è veloce), utilizza un formato dati standard di settore e può essere sottoposto a backup in modo rapido e semplice.

**Modello** - In AEM, un Modello specifica un particolare tipo di pagina. Definisce la struttura di una pagina (specificando anche in genere un’immagine di miniatura e varie proprietà). Ad esempio, puoi avere modelli separati per pagine di prodotti, sitemap e informazioni di contatto.

**Flusso di lavoro** - Il sistema Flusso di lavoro AEM consente la creazione di processi automatizzati che coinvolgono pagine o risorse.
