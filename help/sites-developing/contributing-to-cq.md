---
title: Contribuire a AEM
seo-title: Contributing to AEM
description: AEM viene sviluppato seguendo metodologie collaudate comunemente utilizzate in progetti open source di grandi dimensioni
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 1%

---

# Contribuire a AEM{#contributing-to-aem}

## Metodologia di sviluppo {#development-methodology}

AEM viene sviluppato seguendo metodologie collaudate comunemente utilizzate in grandi progetti open source. Molti elementi di base nello stack di tecnologia AEM sono infatti mantenuti come progetti open source attivi, come Sling e Jackrabbit, che sono stati contribuire ad Apache Software Foundation. Un aspetto importante di questo spirito presente in AEM è che si è incoraggiati a utilizzare le mailing list e i forum online disponibili per interazioni dirette con il team di sviluppo.

Se stai contribuendo a componenti di AEM, devi acquisire familiarità con AEM come faresti quando contribuisci a un progetto open source e comunicare con il team di base esistente come faresti quando vuoi contribuire a tale progetto.

## Esperienza richiesta {#required-experience}

Il protocollo HTTP (HyperText Transfer Protocol) è fondamentale per tutto ciò che facciamo. Pertanto, prima di contribuire a AEM, dovresti avere una conoscenza approfondita di HTTP, idealmente nella misura in cui saresti in grado di scrivere la tua implementazione Java di un server HTTP multithread con thread-pooling. È inoltre necessario avere una conoscenza approfondita del comportamento &quot;keep-alive&quot; di HTTP/1.1 e delle interazioni lato server/client con JavaScript, in particolare dello stile asincrono di interazione rappresentato da AJAX.

Poiché il dinamismo delle pagine e il contenuto interattivo sono elementi chiave dell’esperienza WM, è essenziale avere una comprensione abbastanza approfondita del modello di oggetto documento e del suo potenziale di manipolazione programmatica in risposta agli eventi. Devi conoscere, ad esempio, il comportamento di manipolazione DOM in tempo reale e di trascinamento della selezione su più documenti del browser (ad esempio, utilizzando gli iframe).

Al livello più alto, quindi, dovresti avere una solida comprensione di:

* la [Protocollo HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferibilmente [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Fogli di stile a cascata
* XML (Extensible Markup Language)
* Pattern di progettazione JavaScript e XML (AJAX) asincroni
* Notazione oggetto JavaScript (JSON)
* Modello a oggetti documento
* Interazioni statiche e senza stato
* [Identificatori di risorse uniformi](https://www.ietf.org/rfc/rfc2396.txt)
* Browser cookie
* e altri moderni concetti di sviluppo web

Lo stack tecnologico di Adobe Experience Manager si basa sui [Apache Felix](https://felix.apache.org/) Contenitore OSGI con [Sling Apache](https://sling.apache.org/site/index.html) framework web e incorpora un Java Content Repository ([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)) in base a [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). Devi acquisire familiarità con questi singoli progetti, nonché con tutti gli altri componenti open source (ad esempio, Apache Lucene) utilizzati nell’area in cui intendi contribuire.

## Conoscenza tribale {#tribal-knowledge}

Alcuni concetti e principi guida sono profondamente radicati nella cultura dell&#39;ex giorno. Questa sezione elenca alcuni dei problemi &quot;profondamente incorporati nel DNA&quot; di cui dovresti essere a conoscenza.

### Tutto è contenuto {#everything-is-content}

Il contenuto include non solo tutti i dati che l&#39;applicazione Web persiste. Il codice del programma, le librerie, gli script, i modelli, HTML, CSS, le immagini e gli artefatti di tutti i tipi, qualsiasi cosa e tutto viene mantenuto nell’archivio dei contenuti e importato/esportato sotto forma di pacchetti tramite Gestione pacchetti e Condivisione pacchetti.

### Modello di David {#david-s-model}

Il modo in cui il contenuto deve essere modellato in un archivio di contenuti Java richiede un modo di pensare completamente diverso da quello che è una pratica comune nel settore del software per la modellazione dei dati nel mondo relazionale. Lettura essenziale per qualsiasi nuovo arrivato alla gestione dei contenuti il modo JCR è [Modello di David: Guida alla modellazione dei contenuti](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

L&#39;approccio REST è profondamente radicato in ciò che facciamo. Ciò significa, tra l’altro, evitare interazioni statiche e tenere presente che gli URI sono indirizzi definitivi per i contenuti e i servizi.

REST (REpresentational State Transfer) si riferisce allo stile architettonico del software su cui si basa il World Wide Web. Descrive gli elementi chiave che fanno funzionare il Web e fornisce quindi un insieme di principi per la progettazione del software basato sul web. Quando si progetta un’API da utilizzare sul web, ha pertanto senso attenersi a queste &quot;best practice&quot;.

Poiché il REST fornisce la filosofia guida dietro così tanto di quello che facciamo, dovreste considerare essenziale diventare esperti nei principi del design RESTful. Un buon punto di partenza è con [La tesi di Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Risoluzione della richiesta Sling {#sling-request-resolution}

Un aspetto chiave da comprendere sulle AEM è il modo in cui le richieste in arrivo si riferiscono al contenuto e al comportamento dell’applicazione, il modo in cui il contenuto è strutturato nell’archivio dei contenuti e dove AEM cercare la logica dell’applicazione per gestire la richiesta. Informazioni su Apache [Sling URL decomposizione](https://sling.apache.org/site/url-decomposition.html) e il modo in cui applica lo stile architettonico REST e i suoi vincoli di sistema senza stato, memorizzabili nella cache e su più livelli.

Gli aspetti chiave per comprendere la risoluzione delle richieste di Apache Sling sono il modo in cui le richieste si mappano principalmente a una risorsa specifica nell&#39;archivio dei contenuti, il modo in cui le proprietà aggiuntive della richiesta, insieme alle proprietà di questi oggetti di contenuto, determinano quale codice dell&#39;applicazione verrà richiamato per eseguire il rendering del contenuto e come il codice in /apps sostituisce il codice in /libs.

### Quickstart {#quickstart}

Nessun passaggio tre: Per installare ed eseguire, è sufficiente scaricare e fare doppio clic sul file JAR Quickstart. Non c&#39;è nessun passaggio numero tre. Qualsiasi funzionalità opzionale aggiuntiva non dovrebbe richiedere altro che l&#39;installazione del pacchetto appropriato da Package Share.

Piccola dimensione Quickstart: Mantieni al minimo le dimensioni del file JAR Quickstart. Utilizza le librerie in modo intelligente e ottimizzato, spostando le funzionalità facoltative nella condivisione dei pacchetti.

Tempo di avvio più rapido: Quando apporti una modifica che potrebbe influire sul tempo di avvio, assicurati che sia più breve, non più lungo.

### Lean e Mean {#lean-and-mean}

Favoriamo codici e progetti leggeri, piccoli, veloci ed eleganti. &quot;Abbastanza buono&quot; non è abbastanza buono.

Riutilizzo del codice: La nostra architettura di prodotto basata su OSGi e la filosofia &quot;tutto è contenuto&quot; significa che abbiamo insolitamente buone opportunità per riutilizzare il codice e gli artefatti. Cerchiamo di approfittare di questo fatto quando possibile per mantenere le caratteristiche magre e medie.

Attacco a vuoto: Favoriamo interazioni distanziate su dipendenze strette e &quot;indesiderate intimità&quot;. L&#39;accoppiamento a scomparsa consente inoltre un maggiore riutilizzo del codice.

### Non interrompere la demo {#don-t-break-the-demo}

Acquisisci familiarità con gli script demo e le funzionalità di prodotto più spesso mostrate nelle demo. Comprendere che, almeno, nulla deve mai interrompere una funzione &quot;demo script&quot;. Il prodotto di base deve essere sempre demo-ready, anche durante lo sviluppo.

### Design per affidabilità {#design-for-reliability}

Ci sforziamo di progettare e codificare le funzionalità in modo da evitare errori, in modo che (ad esempio) un problema con un singolo elemento DOM non causi il rendering di un’intera pagina. In altre parole: Fate cose che dovrebbero essere fatali, fatali. Rendi sopravvissuto tutto il resto. Rendi il prodotto &quot;perdonante&quot;.

### L&#39;anomalia è la nuova normale {#abnormal-is-the-new-normal}

Non dipendere dagli hook di spegnimento, assicurati la pulizia all&#39;avvio. Terminazione anormale è terminazione normale.

`shutdown == kill -9 == power outage`

### Prepararsi per il clustering elastico {#be-ready-for-elastic-clustering}

Sempre pronto per il clustering elastico, sempre supporre che ci sia clustering. Come regola generale, rispettare tutto ciò che si trova nell’archivio dei contenuti significa integrare il supporto del clustering.

### Progettazione per compatibilità con le versioni precedenti {#design-for-backward-compatibility}

Niente di ciò che si deve fare dovrebbe interrompere il vecchio codice di un cliente. Solo `/libs` per contenere il codice prodotto che può essere aggiornato durante un aggiornamento. La `/apps` la sezione dell’archivio è il codice del progetto e la `/etc` contiene configurazioni personalizzate che devono essere mantenute. In genere, non sovrascrivere nulla in `/apps`, `/content` e `/home`. Dopo un aggiornamento, il codice, le configurazioni e il contenuto del progetto precedente devono continuare a funzionare come prima dell’aggiornamento.

La progettazione della compatibilità con le versioni precedenti garantisce inoltre che l’esperienza di aggiornamento corrisponda alla semplicità dell’installazione iniziale. È sufficiente interrompere AEM, sostituire il file JAR Quickstart e riavviare AEM. Con una base di installazione in rapida crescita, l&#39;efficienza dell&#39;aggiornamento sarà un vantaggio sempre più significativo.

Anche se le API esistenti possono e devono essere contrassegnate come obsolete quando sono più recenti, con funzioni migliori vengono sostituite, tutte le API rese pubbliche in una versione precedente della versione 5.x devono rimanere funzionanti, poiché potrebbero essere utilizzate nel codice dell’applicazione personalizzato. Non è necessario rimuovere tali API.

La compatibilità con le versioni precedenti dovrebbe essere tenuta presente anche per quanto riguarda la coerenza generale della struttura dei contenuti e dell’esperienza utente.

## Concetti di base {#core-concepts}

**Istanza autore** - In genere, per motivi di sicurezza, governance e altri, un sito di produzione divide le istanze di AEM in istanze di authoring e pubblicazione. Per ulteriori informazioni sull’architettura di distribuzione (incluse le istanze Author/Publish), consulta la documentazione sulle istanze AEM.

**Memorizzazione in cache, frittura e cottura** - Tradizionalmente, i concetti di cottura e frittura sono una distinzione importante tra i diversi sistemi di gestione dei contenuti web. In gergo CMS, &quot;baking&quot; si riferisce al concetto di impegno di dati a file statici in fase di pubblicazione, mentre &quot;friggere&quot; si riferisce al concetto di elaborazione di dati per la presentazione finale in fase di richiesta (cioè, solo in tempo).

**Clustering e bilanciamento del carico** - Per aumentare la disponibilità e migliorare le prestazioni di un ambiente di produzione, è comune combinare più istanze di authoring e/o pubblicazione (in cluster), rendendole disponibili a diversi gruppi di utenti o bilanciandole in base al carico dietro una configurazione di Dispatcher.

È inoltre possibile combinare più istanze dell’archivio dei contenuti per creare un *disponibilità elevata* Soluzione JCR, che può poi essere integrata con la soluzione AEM per massimizzare la protezione da guasti hardware e software. Vedi [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) per ulteriori informazioni.

**Componente** - In AEM, un componente è un tipo di oggetto, le cui istanze possono generalmente essere create trascinandole dalla barra laterale, ad esempio. Ad esempio, i componenti predefiniti forniti con AEM includono i componenti Testo, Titolo, Tag Cloud, Carosello, Immagine ed Elenco , tutti disponibili nella barra laterale in fase di esecuzione.

**Content Finder** - In modalità di authoring, Content Finder è un pannello speciale (frame) sul lato sinistro della pagina che, a seconda della scheda selezionata in alto, visualizza elenchi di immagini, documenti, risorse di Flash, pagine, paragrafi o risorse di archivio che puoi trascinare dal Content Finder alla pagina su cui stai lavorando (a destra).

**Risorse digitali** - In AEM, le risorse digitali sono (in genere) immagini e file rich media. Per ulteriori informazioni, consulta Utilizzo di risorse digitali in DAM.

**Dispatcher** - Dispatcher è sia uno strumento di caching che di bilanciamento del carico, nonché una garanzia di sicurezza specifica.

**Widget ExtJS** - La maggior parte degli elementi dell&#39;interfaccia utente in AEM utilizza ExtJS, una libreria di widget di terze parti scritta in JavaScript. ExtJS dispone di widget di interfaccia utente personalizzabili e ad alte prestazioni e di un modello a componenti ben progettato ed estensibile.

**JCR, Java Content Repository** - La specifica Java Content Repository (JSR-283) fornisce sia un modello dati astratto che un&#39;interfaccia di programmazione applicazioni per la realizzazione di un archivio dati NoSQL scalabile massicciamente che combina le funzionalità di un file system e di un database oggetti. Sebbene non sia necessario comprendere il JSR-283 in modo dettagliato, è necessario prendere tempo per acquisire familiarità con le funzionalità di base del JCR e con il modello dati che lo sottende, perché JCR è ciò che rende possibile la filosofia di AEM &quot;tutto è contenuto&quot;.

In sostanza, JCR è un sistema di nodi e proprietà, in cui i nodi possono ereditare da altri nodi e tutto il contenuto viene memorizzato come proprietà *values*. Nota che oltre all&#39;ereditarietà ordinaria, JCR consente un concetto di nodi &quot;mixin&quot;, che consente di modellare più ereditarietà.

JCR ha una serie di tipi di nodo predefiniti e tipi di proprietà, ma in generale il sistema di digitazione è abbastanza flessibile e (in effetti) uno dei punti di forza di JCR è che consente di memorizzare e gestire contenuti strutturati e non strutturati con la stessa facilità. In altre parole, JCR può contenere dati altamente strutturati, ma può anche contenere strutture di dati dinamici arbitrarie senza vincoli di schema.

JavaDoc per l&#39;API Java di JCR è [qui](http://jackrabbit.apache.org/jcr/jcr-api.html).

Prima di provare a leggere la specifica JavaDoc o JCR stessa, potresti voler guardare [questa spiegazione di alto livello](/help/sites-developing/the-basics.md#java-content-repository) di JCR come implementato da Adobe Experience Services.

**Multi-Site Manager (MSM)** - La funzione MSM di AEM aiuta i clienti a gestire contenuti multilingue e multinazionali, consentendo loro di bilanciare il branding centralizzato con contenuti localizzati.

**OSGi** - OSGi è la tecnologia runtime basata sui servizi che fornisce la base per lo sviluppo Java modularizzato in AEM. Si tratta di un framework che fornisce non solo un ambiente di classificazione ed esecuzione altamente dinamico (e sicuro) per le risorse di codice (noti come bundle), ma anche un controllo completo sulla visibilità e sul ciclo di vita dei vari servizi esposti dai bundle. Un registro di servizio fornisce un modello di cooperazione per i bundle che prende in considerazione le dinamiche del ciclo di vita (e i requisiti di versione). OSGi risolve molti dei problemi che i server applicativi intendevano risolvere, ma lo fa in modo leggero e altamente dinamico, consentendo, ad esempio, la distribuzione a caldo dei servizi (rendendo il nuovo codice immediatamente disponibile senza riavviare il server).

**Parsys, Sistema Paragrafo** - Il sistema paragrafo (parsys) è un componente composto che consente agli autori di aggiungere a una pagina componenti di tipi diversi e contiene altri componenti paragrafo. Ciascun tipo di paragrafo è rappresentato da un componente. Anche il sistema paragrafo stesso è un componente, che contiene gli altri componenti paragrafo.

**Microkernel** - Ogni area di lavoro nel repository può essere configurata separatamente per memorizzare i propri dati attraverso un microkernel specifico (una classe che gestisce la lettura e la scrittura dei dati). Analogamente, l&#39;archivio delle versioni a livello di archivio può anche essere configurato in modo indipendente per utilizzare un particolare microkernel. Sono disponibili diversi microkernel, in grado di memorizzare i dati in diversi formati di file o database relazionali. (Ad esempio, esistono gestori di persistenza per MongoDB, DB2 o Oracle) Il microkernel predefinito per AEM è TarMK (vedi più avanti).

**Pubblica istanza** - Per motivi di sicurezza, governance e altri motivi, un sito di produzione divide in genere le istanze di AEM in istanze di authoring e pubblicazione. Per ulteriori informazioni sull’architettura di distribuzione (incluse le istanze Author/Publish), consulta la documentazione sulle istanze AEM.

**Quickstart** - A differenza di molti altri programmi, si installa AEM utilizzando un singolo file JAR autoestraente &quot;Quickstart&quot;. Quando fai doppio clic sul file JAR per la prima volta, tutto ciò di cui hai bisogno viene installato automaticamente. Il JAR quickstart include tutti i file necessari per l&#39;archivio CRX (incluse le strutture amministrative), i servizi dell&#39;archivio virtuale, i servizi di indice e ricerca, i servizi del flusso di lavoro, la sicurezza e un server Web, oltre al CQ Servlet Engine (CQSE) e tutti i servizi AEM. Nessun altro file da installare: Quickstart è autonomo.

Al primo avvio di Quickstart, viene creato un intero archivio compatibile con JCR in background, che può richiedere diversi minuti. Dopo l&#39;avvio iniziale, le successive startup sono molto più rapide in quanto l&#39;infrastruttura del repository è già stata definita.

Molte opzioni di avvio (come il numero di porta attivo e se l&#39;istanza AEM in questione deve essere un&#39;istanza Publish rispetto a un&#39;istanza Author; e molto altro) può essere controllato rinominando in modo appropriato il file Quickstart . Per visualizzare un elenco delle opzioni a questo proposito, esegui il JAR con &quot;-help&quot; sulla riga di comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**Agenti di replica** - Gli agenti di replica sono fondamentali per AEM come meccanismo utilizzato per pubblicare (attivare) contenuti da un autore a un ambiente di pubblicazione; scarica contenuto dalla cache del Dispatcher; dall’ambiente Publish all’ambiente Author vengono restituiti i contenuti generati dall’utente (ad esempio, l’input del modulo).

**Scaffolding** - Con la funzione di scaffolding è possibile creare un modulo (scaffolding) con campi che riflettono la struttura desiderata per le pagine e quindi utilizzare il modulo per creare facilmente pagine basate su questa struttura.

**Segmentazione** - I visitatori del sito hanno interessi e obiettivi diversi quando arrivano a un sito. Comprendere gli obiettivi dei visitatori e soddisfare le loro aspettative è un importante prerequisito per il successo per il marketing online. La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i dettagli di un visitatore.

**Barra laterale** - La barra laterale è una finestra mobile simile a una palette visualizzata sulla pagina modificabile, dalla quale è possibile trascinare nuovi componenti ed eseguire le azioni applicabili alla pagina.

**Site Catalyst** - Il SiteCatalyst offre agli esperti di marketing un’unica posizione per misurare, analizzare e ottimizzare i dati integrati da tutte le iniziative online su più canali di marketing. Puoi utilizzare Adobe SiteCatalyst per analizzare i dati da AEM siti web.

**Archiviazione Tar (TarMK)** - TarMK è il sistema di persistenza predefinito in AEM. Anche se AEM può essere configurato per utilizzare un sistema di persistenza diverso (come MongoDB), TarMK ha alcuni vantaggi in quanto è ottimizzato per le prestazioni per i casi d’uso tipici JCR (quindi molto veloce), utilizza un formato dati standard del settore e può essere eseguito in modo rapido e semplice il backup.

**Modello** - In AEM, un modello specifica un particolare tipo di pagina. Definisce la struttura di una pagina (in genere specifica anche una miniatura e varie proprietà). Ad esempio, potete utilizzare modelli distinti per le pagine di prodotti, le mappe dei siti e le informazioni di contatto.

**Flusso di lavoro** - Il sistema AEM Workflow consente la creazione di processi automatizzati che coinvolgono pagine o risorse.
