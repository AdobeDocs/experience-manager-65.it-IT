---
title: Contributo a AEM
seo-title: Contributo a AEM
description: AEM è sviluppato seguendo metodologie collaudate comunemente utilizzate in progetti open source di grandi dimensioni
seo-description: AEM è sviluppato seguendo metodologie collaudate comunemente utilizzate in progetti open source di grandi dimensioni
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2726'
ht-degree: 1%

---


# Contributo a AEM{#contributing-to-aem}

## Metodologia di sviluppo {#development-methodology}

AEM è sviluppato seguendo metodologie collaudate comunemente utilizzate nei grandi progetti open source. Molti elementi chiave nello stack AEM tecnologia sono infatti mantenuti come progetti open source attivi, come Sling e Jackrabbit, che sono stati contribuiti alla Apache Software Foundation. Un aspetto importante di questo spirito presente in AEM è che si è incoraggiati a utilizzare le mailing list e i forum online disponibili per interazioni dirette con il team di sviluppo.

Se contribuisci a componenti di AEM, devi acquisire familiarità con AEM come faresti quando contribuisci a un progetto open source, e comunicare con il team di base esistente come faresti quando intendi contribuire a tale progetto.

## Esperienza richiesta {#required-experience}

Il protocollo HyperText Transfer Protocol (HTTP) è fondamentale per tutte le operazioni. Pertanto, prima di contribuire a AEM, è necessario avere una conoscenza approfondita di HTTP, idealmente nella misura in cui si sarebbe in grado di scrivere la propria implementazione Java di un server HTTP multithread con thread-pooling. È inoltre necessario avere una conoscenza approfondita del comportamento di conservazione HTTP/1.1 e delle interazioni server/client con JavaScript, in particolare dello stile asincrono di interazione rappresentato da AJAX.

Poiché il dinamismo della pagina e il contenuto interattivo sono fondamentali per l&#39;esperienza WM, è essenziale avere una conoscenza abbastanza approfondita del modello di oggetto documento e del suo potenziale di manipolazione programmatica in risposta agli eventi. Dovreste avere alcune conoscenze, ad esempio, della modifica DOM in tempo reale e del comportamento di trascinamento della selezione su più documenti del browser (ad esempio, utilizzando iframe).

Al livello più alto, quindi, dovreste avere una solida comprensione di:

* il protocollo [HTTP/1.1](https://www.ietf.org/rfc/rfc2616.txt)
* HTML (preferibilmente [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* Cascading Style Sheets
* Extensible Markup Language (XML)
* Pattern di progettazione JavaScript e XML (AJAX) asincroni
* JavaScript Object Notation (JSON)
* il modello di oggetto documento
* Interazioni statiche e senza stato
* [Identificatori risorsa uniformi](https://www.ietf.org/rfc/rfc2396.txt)
* Cookie browser
* e altri moderni concetti di sviluppo web

Lo stack tecnologico di Adobe Experience Manager si basa sul contenitore [Apache Felix](https://felix.apache.org/) OSGI con il framework Web Apache Sling](https://sling.apache.org/site/index.html) e incorpora un repository di contenuti Java ([JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)) basato su [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). [ È necessario acquisire familiarità con questi singoli progetti, nonché con qualsiasi altro componente open source (ad esempio, Apache Lucene) utilizzato nell&#39;area in cui si intende contribuire.

## Conoscenza tribale {#tribal-knowledge}

Alcuni concetti e principi guida sono profondamente radicati nella cultura della prima giornata. Questa sezione elenca alcuni dei problemi &quot;profondamente DNA-incorporati&quot; di cui dovreste essere a conoscenza.

### Tutto è contenuto {#everything-is-content}

Il contenuto include non solo tutti i dati che l&#39;applicazione Web persiste. Il codice del programma, le librerie, gli script, i modelli, HTML, CSS, le immagini e gli artefatti di tutti i tipi, qualsiasi cosa e qualsiasi cosa, vengono memorizzati nell&#39;archivio dei contenuti e importati/esportati sotto forma di pacchetti tramite Gestione pacchetti e Condivisione pacchetti.

### Modello di David {#david-s-model}

Il modo in cui il contenuto deve essere modellato in un archivio di contenuti Java richiede un modo di pensare completamente diverso da quello che è prassi comune nel settore del software per la modellazione dei dati nel mondo relazionale. La lettura essenziale per qualsiasi nuovo arrivato alla gestione dei contenuti, il modo JCR è [modello David: Guida alla modellazione del contenuto](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTfulness {#restfulness}

L&#39;approccio REST è profondamente radicato in ciò che facciamo. Ciò significa, tra l&#39;altro, evitare interazioni statiche e tenere presente che gli URI sono indirizzi definitivi per i contenuti e i servizi.

REST (REpresentational State Transfer) si riferisce allo stile architettonico del software su cui si basa il World Wide Web. Descrive gli elementi chiave che fanno funzionare il Web, e quindi fornisce un insieme di principi per come dovrebbe essere progettato il software basato su Web. Quando si progetta un&#39;API da utilizzare sul Web, ha pertanto senso aderire a queste &quot;best practice&quot;.

Poiché il REST fornisce la filosofia guida dietro a così tanto di ciò che facciamo, dovreste considerare essenziale diventare esperti nei principi del design RESTful. Un buon punto di partenza è con [la tesi di Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Risoluzione richiesta Sling {#sling-request-resolution}

Un aspetto chiave da comprendere AEM è il modo in cui le richieste in arrivo si relazionano al contenuto e al comportamento delle applicazioni, come il contenuto è strutturato nell&#39;archivio dei contenuti e dove AEM cercare la logica dell&#39;applicazione per gestire la richiesta. Scoprite come decomporre l&#39;URL Apache [Sling](https://sling.apache.org/site/url-decomposition.html) e come applicare lo stile architettonico REST e i relativi vincoli di sistema stateless, cacheable e a più livelli.

Gli aspetti chiave per comprendere la risoluzione delle richieste di Apache Sling sono il modo in cui le richieste vengono associate principalmente a una risorsa specifica nell&#39;archivio dei contenuti, il modo in cui le proprietà aggiuntive della richiesta, insieme alle proprietà di questi oggetti contenuto, determinano quale codice dell&#39;applicazione verrà richiamato per eseguire il rendering del contenuto e come il codice in /apps sostituisce il codice in /libs.

### Avvio rapido {#quickstart}

No step tre: Per installare ed eseguire, è sufficiente scaricare e fare doppio clic sul file JAR di Quickstart. Non c&#39;è un terzo passo. Qualsiasi funzionalità opzionale aggiuntiva non deve richiedere altro che l&#39;installazione del pacchetto appropriato da Package Share.

Piccola dimensione di Avvio rapido: Mantenete al minimo le dimensioni del file JAR di Quickstart. Utilizzo intelligente e ottimizzato delle librerie, spostamento delle funzionalità facoltative per la condivisione del pacchetto.

Tempo di avvio più rapido: Quando apportate una modifica che potrebbe influire sul tempo di avvio, accertatevi che sia più breve, non più lungo.

### Lineare e Media {#lean-and-mean}

Favoriamo codici e progetti leggeri, piccoli, veloci ed eleganti. &quot;Abbastanza buono&quot; non è abbastanza buono.

Riuso del codice: La nostra architettura di prodotto basata su OSGi e la filosofia &quot;tutto è contenuto&quot; significa che abbiamo insolitamente buone opportunità per riutilizzare codice e artefatti. Cerchiamo di approfittare di questo fatto quando possibile per mantenere le caratteristiche magre e medie.

Attacco in sospensione: Favoriamo interazioni a stretto contatto con le persone a dipendenze strette e &quot;indesiderata intimità&quot;. Il raccordo a scomparsa permette inoltre un maggiore riutilizzo del codice.

### Non interrompere la demo {#don-t-break-the-demo}

Acquisisci familiarità con gli script dimostrativi e le funzionalità dei prodotti che vengono visualizzate più spesso nelle demo. Comprendere che, almeno, nulla di ciò che si fa dovrebbe mai interrompere una funzione &quot;demo script&quot;. Il prodotto di base deve essere sempre demo-ready, anche durante lo sviluppo.

### Progettazione per affidabilità {#design-for-reliability}

Ci sforziamo di progettare e codificare le funzionalità in modo semplice, in modo che (ad esempio) un problema con un singolo elemento DOM non impedisca il rendering di un&#39;intera pagina. In altre parole: Fare cose che dovrebbero essere fatali, fatali. Rendi tutto il resto sopravvissuto. Fare il prodotto &quot;perdonare&quot;.

### Anomalo è il nuovo normale {#abnormal-is-the-new-normal}

Non dipendere dai ganci di arresto, assicurati che l&#39;avvio sia pulito. Terminazione anomala è una normale terminazione.

`shutdown == kill -9 == power outage`

### Prepararsi per il clustering elastico {#be-ready-for-elastic-clustering}

Sempre pronto per il clustering elastico, sempre supporre che ci sia il clustering. Come regola generale, il rispetto di tutto ciò che si trova nell&#39;archivio dei contenuti comporta il supporto del clustering integrato.

### Progettazione per compatibilità con versioni precedenti {#design-for-backward-compatibility}

Niente di quello che fai dovrebbe interrompere il vecchio codice di un cliente. Considerare solo `/libs` per contenere il codice prodotto che può essere aggiornato durante un aggiornamento. La sezione `/apps` dell&#39;archivio è codice progetto e la sezione `/etc` contiene configurazioni personalizzate che devono essere mantenute. In genere, non sovrascrivere nulla in `/apps`, `/content` e `/home`. Dopo un aggiornamento, il codice, le configurazioni e il contenuto del progetto precedente devono continuare a funzionare come prima dell&#39;aggiornamento.

La progettazione della compatibilità con le versioni precedenti garantisce inoltre che l&#39;esperienza di aggiornamento corrisponda alla semplicità dell&#39;installazione iniziale. È sufficiente arrestare AEM, sostituire il file JAR di Quickstart e riavviare AEM. Con una base di installazione in rapida crescita, l&#39;efficienza dell&#39;aggiornamento sarà un vantaggio sempre più importante.

Anche se le API esistenti possono e devono essere contrassegnate come obsolete quando sono più recenti, una funzionalità migliore le sostituisce, tutte le API rese pubbliche in una versione precedente della versione 5.x devono rimanere funzionanti, poiché potrebbero essere utilizzate nel codice dell&#39;applicazione personalizzato. Tali API non devono essere rimosse.

La compatibilità con le versioni precedenti dovrebbe essere tenuta presente anche per quanto riguarda la coerenza generale della struttura dei contenuti e l&#39;esperienza dell&#39;utente.

## Concetti di base {#core-concepts}

**Istanza**  autore: in genere, per motivi di sicurezza, governance e per altri motivi, un sito di produzione suddivide le istanze di AEM in istanze Autore e Pubblica. Per ulteriori informazioni sull&#39;architettura di distribuzione (comprese le istanze Author/Publish), consultate la documentazione sulle istanze AEM.

**Caching, friggere e cuocere**  - Tradizionalmente, i concetti di cuocere e friggere sono una distinzione importante tra i diversi sistemi di gestione dei contenuti Web. In linguaggio CMS, per &quot;cottura&quot; si intende il concetto di invio di dati a file statici in fase di pubblicazione, mentre per &quot;frittura&quot; si intende il concetto di elaborazione di dati per la presentazione finale in fase di richiesta (cioè, solo in tempo).

**Clustering e bilanciamento**  del carico: per aumentare la disponibilità e migliorare le prestazioni di un ambiente di produzione, è comune combinare più istanze Author e/o Publish (in cluster), rendendole disponibili a diversi gruppi di utenti o bilanciandole in base al carico all&#39;interno di una configurazione Dispatcher.

È inoltre possibile combinare più istanze dell&#39;archivio dei contenuti per creare una soluzione *JCR ad alta disponibilità*, che può quindi essere integrata con la soluzione AEM per massimizzare la protezione contro i guasti hardware e software. Per ulteriori informazioni, vedere [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter).

**Componente**  - In AEM, un componente è un tipo di oggetto, le cui istanze possono in genere essere create trascinandole dalla barra laterale, ad esempio. Ad esempio, i componenti forniti con AEM includono i componenti Testo, Titolo, Tag Cloud, Carosello, Immagine ed Elenco, tutti disponibili nella barra laterale in fase di esecuzione.

**Content Finder**  - In modalità di authoring, Content Finder è un pannello speciale (fotogramma) a sinistra della pagina che, a seconda della scheda selezionata in alto, visualizza gli elenchi di immagini, documenti, risorse di Flash, pagine, paragrafi o risorse di repository che è possibile trascinare da Content Finder alla pagina su cui si sta lavorando (a destra).

**Risorse**  digitali - In AEM, le risorse digitali sono (generalmente) immagini e file multimediali. Per ulteriori informazioni, consulta Utilizzo delle risorse digitali in DAM.

**Dispatcher** : il dispatcher è sia uno strumento di caching che di bilanciamento del carico, oltre a fornire alcune garanzie di sicurezza.

**widget**  ExtJS - La maggior parte degli elementi dell&#39;interfaccia utente in AEM utilizzano ExtJS, una libreria di widget di terze parti scritta in JavaScript. ExtJS offre widget dell’interfaccia utente personalizzabili e prestazioni elevate e un modello di componenti estensibile.

**JCR, Java Content Repository**  - La specifica Java Content Repository (JSR-283) fornisce sia un modello dati astratto che un&#39;interfaccia di programmazione applicazioni per realizzare un archivio dati NoSQL scalabile che combina le funzionalità di un file system e di un database oggetti. Sebbene non sia necessario comprendere il JSR-283 nei dettagli completi, è necessario prendere tempo per acquisire familiarità con le funzionalità di base del JCR e con il modello di dati sottostante, perché JCR è ciò che rende possibile la filosofia di AEM &quot;tutto è contenuto&quot;.

In sostanza, JCR è un sistema di nodi e proprietà, in cui i nodi possono ereditare da altri nodi e tutto il contenuto è memorizzato come proprietà *values*. Si noti che, oltre all&#39;ereditarietà ordinaria, JCR consente un concetto di nodi &quot;mixin&quot;, che consente la modellazione di più ereditarietà.

JCR ha una serie di tipi di nodi e di proprietà predefiniti, ma in generale il sistema di digitazione è abbastanza flessibile, e (in effetti) uno dei punti di forza di JCR è che consente di memorizzare e gestire con la stessa facilità contenuti strutturati e non strutturati. In altre parole, JCR può contenere dati altamente strutturati, ma può anche contenere strutture di dati dinamici arbitrarie senza vincoli di schema.

JavaDoc per l&#39;API Java di JCR è [qui](http://jackrabbit.apache.org/jcr/jcr-api.html).

Prima di provare a leggere la specifica JavaDoc o JCR stessa, potresti voler consultare [questa spiegazione di alto livello](/help/sites-developing/the-basics.md#java-content-repository) di JCR, come implementato da Adobe Experience Services.

**Multi-Site Manager (MSM)**  - La funzione MSM di AEM aiuta i clienti a gestire contenuti multilingue e multinazionali, consentendo loro di bilanciare il branding centralizzato con contenuti localizzati.

**OSGi** - OSGi è la tecnologia runtime basata sui servizi che fornisce la base per lo sviluppo Java modularizzato in AEM. Si tratta di un framework che fornisce non solo un ambiente di caricamento ed esecuzione altamente dinamico (e sicuro) per le risorse di codice (note come pacchetti), ma anche il pieno controllo sulla visibilità e sul ciclo di vita dei vari servizi esposti dai bundle. Un registro dei servizi fornisce un modello di cooperazione per i bundle che tiene conto delle dinamiche del ciclo di vita (e dei requisiti di versione). OSGi risolve molti dei problemi che i server applicativi intendevano risolvere, ma lo fa in modo leggero e altamente dinamico, rendendo possibile, ad esempio, la distribuzione a caldo dei servizi (rendendo il nuovo codice immediatamente disponibile senza riavviare il server).

**Parsys, Sistema**  paragrafi - Il sistema paragrafo (parsys) è un componente composto che consente agli autori di aggiungere a una pagina componenti di tipi diversi e contiene altri componenti paragrafo. Ciascun tipo di paragrafo è rappresentato da un componente. Anche il sistema paragrafo stesso è un componente, che contiene gli altri componenti paragrafo.

**Microkernel** : ogni area di lavoro del repository può essere configurata separatamente per memorizzare i dati attraverso un microkernel specifico (una classe che gestisce la lettura e la scrittura dei dati). Analogamente, l&#39;archivio delle versioni dell&#39;archivio può essere configurato in modo indipendente per l&#39;utilizzo di un particolare microkernel. Sono disponibili diversi microkernel, in grado di memorizzare i dati in diversi formati di file o database relazionali. (Ad esempio, esistono persistence manager per MongoDB, DB2 o  Oracle) Il microkernel predefinito per AEM è TarMK (vedere di seguito).

**Istanza**  di pubblicazione - Per motivi di sicurezza, governance e per altri motivi, un sito di produzione dividerà in genere le istanze di AEM in istanze di Autore e Pubblicazione. Per ulteriori informazioni sull&#39;architettura di distribuzione (comprese le istanze Author/Publish), consultate la documentazione sulle istanze AEM.

**Quickstart** - A differenza di molti altri programmi, si installa AEM utilizzando un singolo &quot;Quickstart&quot; auto-estraente file JAR. Quando si fa doppio clic sul file JAR per la prima volta, tutto ciò che serve viene installato automaticamente. Il JAR di avvio rapido include tutti i file richiesti per l&#39;archivio CRX (comprese le strutture amministrative), i servizi dell&#39;archivio virtuale, i servizi di indice e di ricerca, i servizi del flusso di lavoro, la protezione e un server Web, oltre al CQ Servlet Engine (CQSE) e a tutti i servizi AEM. Non ci sono altri file da installare: il Quickstart è autonomo.

La prima volta che si avvia Quickstart, viene creato in background un intero repository compatibile con JCR, che può richiedere alcuni minuti. Dopo l&#39;avvio iniziale, le avvii successivi sono molto più veloci in quanto l&#39;infrastruttura del repository è già stata impostata.

Molte opzioni di avvio (ad esempio, il numero della porta attiva e se l&#39;istanza AEM in questione deve essere un&#39;istanza Pubblica rispetto a un&#39;istanza Author; e molto altro) può essere controllato rinominando in modo appropriato il file Quickstart. Per visualizzare un elenco delle opzioni, eseguire la JAR con &quot;-help&quot; sulla riga di comando:

```shell
java -jar <quickstartfilename>.jar -help
```

**agenti**  di replica: gli agenti di replica sono fondamentali per AEM come meccanismo utilizzato per pubblicare (attivare) il contenuto da un autore a un ambiente di pubblicazione; cancellare il contenuto dalla cache del dispatcher; restituite all’ambiente Authoring il contenuto generato dall’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione.

**Scaffolding** - Con la funzione di scaffolding è possibile creare un modulo (una pagina di scaffolding) con campi che riflettono la struttura desiderata per le pagine e quindi utilizzare questo modulo per creare facilmente pagine basate su questa struttura.

**Segmentazione** : i visitatori del sito hanno interessi e obiettivi diversi quando arrivano a un sito. Comprendere gli obiettivi dei visitatori e soddisfare le loro aspettative è un importante prerequisito per il successo del marketing online. La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i dettagli di un visitatore.

**Barra laterale** - La barra laterale è una finestra mobile simile a una palette visualizzata sulla pagina modificabile, dalla quale è possibile trascinare nuovi componenti e eseguire le azioni applicabili alla pagina.

**Site Catalyst** - Il SiteCatalyst offre agli esperti di marketing un&#39;unica posizione per misurare, analizzare e ottimizzare i dati integrati da tutte le iniziative online attraverso più canali di marketing. Potete utilizzare  Adobe SiteCatalyst per analizzare i dati da AEM siti Web.

**Tar Storage (TarMK)** - TarMK è il sistema di persistenza predefinito in AEM. Anche se AEM può essere configurato per utilizzare un sistema di persistenza diverso (come MongoDB), TarMK ha alcuni vantaggi in quanto è ottimizzato per le prestazioni per i casi di utilizzo JCR tipici (quindi è molto veloce), utilizza un formato di dati standard di settore e può essere eseguito rapidamente e facilmente il backup.

**Modello**  - In AEM, un Modello specifica un particolare tipo di pagina. Definisce la struttura di una pagina (in genere specifica una miniatura e varie proprietà). Ad esempio, potete utilizzare modelli distinti per le pagine di prodotti, le mappe dei siti e le informazioni di contatto.

**Flusso di lavoro** : il sistema AEM Workflow consente la creazione di processi automatizzati che coinvolgono pagine o risorse.
