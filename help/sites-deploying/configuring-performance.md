---
title: Ottimizzazione delle prestazioni
seo-title: Ottimizzazione delle prestazioni
description: Scoprite come configurare alcuni aspetti di AEM per ottimizzare le prestazioni.
seo-description: Scoprite come configurare alcuni aspetti di AEM per ottimizzare le prestazioni.
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '6722'
ht-degree: 2%

---


# Ottimizzazione delle prestazioni{#performance-optimization}

>[!NOTE]
>
>Per linee guida generali sulle prestazioni, consultare la pagina [Performance Guidelines](/help/sites-deploying/performance-guidelines.md) (Linee guida sulle prestazioni).
>
>Per ulteriori informazioni sulla risoluzione dei problemi di prestazioni, vedere anche la [Struttura delle prestazioni](/help/sites-deploying/performance-tree.md).
>
>Inoltre, è possibile esaminare un articolo della Knowlege Base su [Suggerimenti per l&#39;ottimizzazione delle prestazioni.](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

Un problema chiave è rappresentato dal tempo impiegato dal sito Web per rispondere alle richieste dei visitatori. Anche se questo valore varia per ogni richiesta, è possibile definire un valore target medio. Una volta dimostrato che questo valore è sia raggiungibile che gestibile, può essere utilizzato per monitorare le prestazioni del sito Web e indicare lo sviluppo di potenziali problemi.

I tempi di risposta desiderati saranno diversi negli ambienti di creazione e pubblicazione, in base alle diverse caratteristiche del pubblico di destinazione:

## Ambiente di authoring {#author-environment}

Questo ambiente viene utilizzato dagli autori che immettono e aggiornano i contenuti. Deve essere adatto a un numero limitato di utenti che generano un numero elevato di richieste ad alte prestazioni durante l&#39;aggiornamento delle pagine di contenuto e dei singoli elementi di tali pagine.

## Ambiente di pubblicazione {#publish-environment}

Questo ambiente contiene il contenuto che potete rendere disponibile agli utenti. In questo caso il numero di richieste è ancora maggiore e la velocità è altrettanto vitale, ma dato che la natura delle richieste è meno dinamica, si possono applicare ulteriori meccanismi di miglioramento delle prestazioni; come la memorizzazione nella cache del contenuto o il bilanciamento del carico.

>[!NOTE]
>
>* Dopo aver configurato per l&#39;ottimizzazione delle prestazioni, seguire le procedure riportate in [Giorno duro](/help/sites-developing/tough-day.md) per verificare l&#39;ambiente con un carico elevato.
>* Vedere anche [Suggerimenti per l&#39;ottimizzazione delle prestazioni](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

>



## Metodologia di ottimizzazione delle prestazioni {#performance-optimization-methodology}

Una metodologia di ottimizzazione delle prestazioni per i progetti CQ può essere riassunta in cinque semplici regole che possono essere seguite per evitare problemi di prestazioni fin dall’inizio:

1. [Pianificazione per l&#39;ottimizzazione](#planning-for-optimization)
1. [Simula realtà](#simulate-reality)
1. [Definizione di obiettivi solidi](#establish-solid-goals)
1. [Rimani pertinente](#stay-relevant)
1. [Cicli Di Iterazione Agile](#agile-iteration-cycles)

Queste regole, in larga misura, si applicano ai progetti Web in generale, e sono pertinenti per i project manager e gli amministratori di sistema per garantire che i loro progetti non si scontrino con problemi di prestazioni al momento dell&#39;avvio.

### Pianificazione per l&#39;ottimizzazione {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

Circa il 10% dello sforzo di progetto dovrebbe essere pianificato per la fase di ottimizzazione delle prestazioni. Naturalmente, i requisiti effettivi di ottimizzazione delle prestazioni dipenderanno dal livello di complessità di un progetto e dall&#39;esperienza del team di sviluppo. Anche se il progetto potrebbe (in ultima analisi) non richiedere tutto il tempo allocato, è buona norma pianificare sempre l&#39;ottimizzazione delle prestazioni nell&#39;area suggerita.

Quando possibile, un progetto dovrebbe essere avviato in modo flessibile a un pubblico limitato per raccogliere esperienze reali ed eseguire ulteriori ottimizzazioni, senza la pressione aggiuntiva che segue un annuncio completo.

Una volta &quot;live&quot;, l&#39;ottimizzazione delle prestazioni non è finita. Questo è il momento in cui si verifica il carico &quot;reale&quot; sul sistema. È importante pianificare ulteriori adeguamenti dopo l’avvio.

Poiché il carico del sistema cambia e i profili di prestazione del sistema si modificano nel tempo, è necessario pianificare una &quot;messa a punto&quot; o un &quot;controllo dello stato&quot; delle prestazioni a intervalli di 6-12 mesi.

### Simula realtà {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

Se andate in diretta con un sito Web e scoprite dopo il lancio che avete incontrato problemi di prestazioni, vi è un solo motivo: I test di carico e di prestazioni non hanno simulato la realtà abbastanza da vicino.

Simulare la realtà è difficile e quanto sforzo si può ragionevolmente voler investire per ottenere &quot;reale&quot; dipende dalla natura del progetto. &quot;Reale&quot; significa non solo &quot;codice reale&quot; e &quot;traffico reale&quot;, ma anche &quot;contenuto reale&quot;, soprattutto per quanto riguarda la dimensione e la struttura dei contenuti. I modelli possono comportarsi in modo completamente diverso a seconda delle dimensioni e della struttura dell’archivio.

### Definizione di obiettivi solidi {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

Non va sottovalutata l&#39;importanza di realizzare adeguatamente gli obiettivi prestazionali. Spesso, una volta che le persone si focalizzano su obiettivi di performance specifici, è molto difficile cambiare questi obiettivi in seguito, anche se sono basati su ipotesi selvagge.

Stabilire buoni e solidi obiettivi prestazionali è in realtà una delle aree più difficili. Spesso è meglio raccogliere registri e benchmark reali da un sito Web comparabile (ad esempio il predecessore del nuovo sito).

### Rimani pertinente {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

È importante ottimizzare un collo di bottiglia alla volta. Se provate a fare cose in parallelo senza convalidare l&#39;impatto dell&#39;ottimizzazione unica, perderete la traccia di quale misura di ottimizzazione effettivamente ha aiutato.

### Cicli di iterazione degli assi {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

Il perfezionamento delle prestazioni è un processo iterativo che richiede, misurare, analizzare, ottimizzare e convalidare fino al raggiungimento dell&#39;obiettivo. Per tenere debitamente conto di questo aspetto, implementate un processo di convalida agile nella fase di ottimizzazione, anziché un processo di test più pesante dopo ogni iterazione.

Ciò significa in gran parte che lo sviluppatore che implementa l&#39;ottimizzazione deve avere un modo rapido per sapere se l&#39;ottimizzazione ha già raggiunto l&#39;obiettivo. Si tratta di informazioni preziose, perché quando si raggiunge l&#39;obiettivo, l&#39;ottimizzazione è finita.

## Linee guida sulle prestazioni di base {#basic-performance-guidelines}

In genere, mantenete le richieste HTML non memorizzate nella cache fino a meno di 100 ms. Più specificamente, possono essere utilizzati come orientamento:

* Il 70% delle richieste di pagine deve essere risposto in meno di 100 ms.
* Il 25% delle richieste di pagine deve ricevere una risposta entro 100-300 ms.
* Il 4% delle richieste di pagine deve ricevere una risposta entro 300ms-500ms.
* L&#39;1% delle richieste di pagine deve ricevere una risposta entro 500 ms-1000 ms.
* Nessuna pagina deve rispondere più lentamente di 1 secondo.

I numeri sopra riportati si basano sulle seguenti condizioni:

* misurati al momento della pubblicazione (nessun overhead correlato a un ambiente di authoring)
* misurati sul server (nessun sovraccarico di rete)
* non memorizzato nella cache (nessuna cache di output CQ, nessuna cache del dispatcher)
* solo per elementi complessi con molte dipendenze (HTML, JS, PDF, ...)
* nessun altro carico sul sistema

Ci sono alcuni problemi che spesso contribuiscono a problemi di prestazioni. Questi ruotano principalmente intorno a:

* inefficienza della cache dello dispatcher
* l&#39;utilizzo di query in normali modelli di visualizzazione.

La sintonizzazione a livello di JVM e del sistema operativo in genere non comporta grandi balzi nelle prestazioni e dovrebbe pertanto essere eseguita alla fine del ciclo di ottimizzazione.

Anche la struttura di un archivio dei contenuti può avere un impatto sulle prestazioni. Per ottenere prestazioni ottimali, il numero di nodi secondari associati a singoli nodi in un archivio di contenuti non deve superare 1.000 (come regola generale).

I migliori amici durante un normale esercizio di ottimizzazione delle prestazioni sono:

* `request.log`
* temporizzazione basata su componenti
* ultimo, ma non meno importante, profiler Java.

### Prestazioni durante il caricamento e la modifica di risorse digitali {#performance-when-loading-and-editing-digital-assets}

A causa dell’elevato volume di dati coinvolti nel caricamento e nella modifica delle risorse digitali, le prestazioni possono diventare un problema.

Due fattori influiscono sulle prestazioni:

* CPU: più core consentono un lavoro più fluido durante la transcodifica
* Disco rigido - dischi RAID paralleli raggiungono lo stesso

Per migliorare le prestazioni è possibile considerare quanto segue:

* Quante risorse verranno caricate al giorno? Una buona stima può basarsi su:

![chlimage_1-77](assets/chlimage_1-77.png)

* Il periodo di tempo in cui verranno apportate le modifiche (in genere la durata della giornata lavorativa, più per le operazioni internazionali).
* La dimensione media delle immagini caricate (e la dimensione delle rappresentazioni generate per immagine) in megabyte.
* Determinare la velocità dati media:

![chlimage_1-78](assets/chlimage_1-78.png)

* L&#39;80% di tutte le modifiche verranno effettuate nel 20% del tempo, quindi nel tempo di picco si avrà 4 volte la velocità dati media. Questo è il vostro obiettivo di prestazioni.

## Monitoraggio delle prestazioni {#performance-monitoring}

Le prestazioni (o l&#39;assenza) sono una delle prime cose che gli utenti notano, così come con qualsiasi applicazione con un&#39;interfaccia utente, le prestazioni sono di importanza fondamentale. Per ottimizzare le prestazioni dell’installazione di CQ è necessario monitorare i vari attributi dell’istanza e il relativo comportamento.

Per informazioni su come eseguire il monitoraggio delle prestazioni, vedere [Monitoraggio delle prestazioni](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

I problemi che causano problemi di prestazioni sono spesso difficili da individuare, anche quando i loro effetti sono facili da vedere.

Un punto di partenza di base è una buona conoscenza del sistema quando funziona normalmente. A meno che non si sappia come l&#39;ambiente &quot;appare&quot; e &quot;si comporta&quot; quando viene eseguito correttamente, può essere difficile individuare il problema quando le prestazioni peggiorano. Ciò significa che è necessario dedicare un po&#39; di tempo alle indagini sul sistema quando viene eseguito senza problemi e assicurarsi che la raccolta delle informazioni sulle prestazioni sia un&#39;attività continua. Questo vi fornirà una base per il confronto qualora le prestazioni ne risentano.

Il diagramma seguente illustra il percorso che una richiesta di contenuti CQ può seguire, e quindi il numero di elementi diversi che possono influire sulle prestazioni.

![chlimage_1-79](assets/chlimage_1-79.png)

Le prestazioni sono anche un equilibrio tra Volume e Capacità:

**** Volume: l&#39;ammontare dell&#39;output elaborato e consegnato dal sistema.

**** Capacità: capacità del sistema di fornire il volume.

Questo può essere illustrato in diverse aree della catena Web.

![chlimage_1-80](assets/chlimage_1-80.png)

Esistono diverse aree funzionali che spesso hanno un impatto sulle prestazioni:

* Caching
* Codice applicazione (progetto)
* Funzionalità di ricerca

### Regole di base sulle prestazioni {#basic-rules-regarding-performance}

Quando si ottimizzano le prestazioni, si dovrebbero tenere presenti alcune regole:

* Il tuning delle prestazioni *deve essere* incluso in ogni progetto.
* Non eseguire l&#39;ottimizzazione all&#39;inizio del ciclo di sviluppo.
* Le prestazioni sono buone solo quanto il collegamento più debole.
* Pensate sempre alla capacità rispetto al volume.
* Prima di tutto, ottimizzate le cose importanti.
* Non eseguire mai l&#39;ottimizzazione senza *obiettivi realistici*.

>[!NOTE]
>
>Tenete presente che il meccanismo utilizzato per misurare le prestazioni spesso influisce esattamente su ciò che state cercando di misurare. Si dovrebbe sempre cercare di rendere conto di queste discrepanze, eliminando il più possibile i loro effetti; in particolare, i plug-in del browser dovrebbero essere disattivati ogniqualvolta possibile.

## Configurazione per prestazioni {#configuring-for-performance}

Alcuni aspetti di CQ (e/o CRX sottostante) possono essere configurati per ottimizzare le prestazioni. Di seguito sono riportati alcuni suggerimenti e opzioni che consentono di verificare se e come utilizzare la funzionalità in questione prima di apportare modifiche.

>[!NOTE]
>
>Per ulteriori informazioni, vedere l&#39;articolo [KB](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

### Indicizzazione ricerca {#search-indexing}

A partire da AEM 6.0, Adobe Experience Manager utilizza un&#39;architettura repository basata su Oak.

Per informazioni aggiornate sull’indicizzazione, consultate:

* [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Query e indicizzazione](/help/sites-deploying/queries-and-indexing.md)

### Elaborazione flusso di lavoro simultanea {#concurrent-workflow-processing}

Limitare il numero di processi di workflow in esecuzione simultanea per migliorare le prestazioni. Per impostazione predefinita, il motore del flusso di lavoro elabora in parallelo tutti i flussi di lavoro disponibili per la macchina virtuale Java. Quando i passaggi del flusso di lavoro richiedono grandi quantità di risorse di elaborazione (RAM o CPU), l&#39;esecuzione parallela di diversi di questi flussi di lavoro può richiedere molto alle risorse server disponibili.

Ad esempio, quando si caricano immagini (o risorse DAM in generale), i flussi di lavoro importano automaticamente le immagini in DAM. Le immagini sono spesso ad alta risoluzione e possono facilmente consumare centinaia di MB di heap per l&#39;elaborazione. La gestione parallela di queste immagini colloca un carico elevato sul sottosistema di memoria e sul Garbage Collector.

Il motore del flusso di lavoro utilizza le code di processo Apache Sling per gestire e pianificare l’elaborazione degli elementi di lavoro. Per impostazione predefinita, dal factory del servizio di configurazione della coda di processo Apache Sling sono stati creati i seguenti servizi per l&#39;elaborazione dei processi del flusso di lavoro:

* Coda flusso di lavoro Granite: La maggior parte dei passaggi del flusso di lavoro, ad esempio quelli che elaborano le risorse DAM, utilizza il servizio Coda flussi di lavoro Granite.
* Coda processo esterno flusso di lavoro Granite: Questo servizio è utilizzato per i passaggi di flusso di lavoro estremi speciali, solitamente utilizzati per contattare un sistema esterno e per eseguire il polling dei risultati. Ad esempio, il passaggio  InDesign Media Extraction Process è implementato come processo esterno. Il motore del flusso di lavoro utilizza la coda esterna per elaborare il polling. (Vedere [com.day.cq.workflow.exec.WorkflowExternalProcess](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

Configurate questi servizi per limitare il numero massimo di processi di flusso di lavoro in esecuzione simultanea.

**Nota:** la configurazione di queste code di processi interessa tutti i flussi di lavoro a meno che non sia stata creata una coda di lavoro per un modello di flusso di lavoro specifico (consultate  [Configurare la coda per un ](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) modello di flusso di lavoro specifico riportato di seguito).

**Configurazione nell&#39;archivio**

Se state configurando i servizi [utilizzando un nodo sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository), è necessario trovare il PID dei servizi esistenti, ad esempio: org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705. È possibile individuare il PID utilizzando la console Web.

È necessario configurare la proprietà denominata queue.maxparallela.

**Configurazione nella console Web**

Per configurare questi servizi [utilizzando la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), individuare gli elementi di configurazione esistenti sotto il service factory di configurazione della coda di lavoro Apache Sling.

È necessario configurare la proprietà denominata Massimo processi paralleli.

### Configurare la coda per un flusso di lavoro specifico {#configure-the-queue-for-a-specific-workflow}

Create una coda di processo per un modello di flusso di lavoro specifico in modo da poter configurare la gestione del processo per tale modello di flusso di lavoro. In questo modo, le configurazioni influiscono sull&#39;elaborazione per un flusso di lavoro specifico, mentre la configurazione della coda di flusso di lavoro Granite predefinita controlla l&#39;elaborazione di altri flussi di lavoro.

Quando vengono eseguiti, i modelli di workflow creano processi Sling per un argomento specifico. Per impostazione predefinita, l’argomento corrisponde agli argomenti configurati per la coda generale del flusso di lavoro Granite o per la coda del processo esterno del flusso di lavoro Granite:

* com/adobe/granite/workflow/job&amp;ast;
* com/adobe/granite/workflow/external/job&amp;ast;

Gli argomenti di processo effettivi generati dai modelli di flusso di lavoro includono il suffisso specifico per il modello. Ad esempio, il modello di flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] genera processi con il seguente argomento:

com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model

Pertanto, potete creare una coda di processo per l’argomento che corrisponde agli argomenti di processo del modello di workflow. La configurazione delle proprietà relative alle prestazioni della coda ha effetto solo sul modello di flusso di lavoro che genera i processi che corrispondono all&#39;argomento della coda.

La procedura seguente crea una coda di processo per un flusso di lavoro, utilizzando come esempio il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].

1. Eseguite il modello di flusso di lavoro per il quale desiderate creare la coda dei processi, in modo da generare le statistiche degli argomenti. Ad esempio, aggiungi un&#39;immagine alle risorse per eseguire il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].
1. Aprite la console Processi Sling. ([http://localhost:4502/system/console/slingevent](http://localhost:4502/system/console/slingevent))
1. Scopri gli argomenti relativi al flusso di lavoro nella console. Per DAM Update Asset, sono disponibili i seguenti argomenti:

   * com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model
   * com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model

1. Crea una coda di processi per ciascuno di questi argomenti. Per creare una coda di processi, create una configurazione di fabbrica per il servizio factory Apache Sling Job Queue.

   Le configurazioni di fabbrica sono simili alla coda del flusso di lavoro Granite descritta in [Elaborazione del flusso di lavoro simultanea](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing), tranne per il fatto che la proprietà Topics corrisponde all&#39;argomento dei processi del flusso di lavoro.

### Servizio di sincronizzazione risorse CQ5 DAM {#cq-dam-asset-synchronization-service}

`AssetSynchronizationService` viene utilizzato per sincronizzare le risorse dai repository montati (tra cui LiveLink, Documentum, tra gli altri). Per impostazione predefinita, questo esegue un controllo regolare ogni 300 secondi (5 minuti), quindi se non si utilizzano i repository montati, è possibile disattivare questo servizio.

A tal fine, [è possibile configurare il servizio OSGi](/help/sites-deploying/configuring-osgi.md) **CQ DAM Asset Synchronization Service** per impostare il **periodo di sincronizzazione** ( `scheduler.period`) su (almeno) 1 anno (definito in secondi).

### Più istanze DAM {#multiple-dam-instances}

La distribuzione di più istanze DAM può essere utile per migliorare le prestazioni, ad esempio:

* il carico è elevato a causa del caricamento regolare di un gran numero di risorse per l’ambiente di authoring; in questo caso, un&#39;istanza DAM separata può essere dedicata all&#39;autore del servizio.
* disponete di più team in sedi mondiali (ad esempio USA, Europa, Asia).

Ulteriori considerazioni sono:

* separazione tra &quot;lavoro in corso&quot; sull’autore e &quot;finale&quot; sulla pubblicazione
* separazione degli utenti interni per l’autore da visitatori/utenti esterni al momento della pubblicazione (ad esempio, agenti, rappresentanti della stampa, clienti, studenti, ecc.).

## Best practice per la garanzia della qualità {#best-practices-for-quality-assurance}

Le prestazioni sono di importanza fondamentale per l’ambiente di pubblicazione. Pertanto, durante l’implementazione del progetto dovete pianificare e analizzare attentamente i test di prestazioni che effettuerete per l’ambiente di pubblicazione.

Questa sezione offre una panoramica standardizzata dei problemi relativi alla definizione di un concetto di test specifico per i test delle prestazioni nell&#39;ambiente *publish*. Ciò è particolarmente interessante per ingegneri di QA, project manager e amministratori di sistema.

Di seguito viene illustrato un approccio standardizzato ai test di prestazioni per un&#39;applicazione CQ nell&#39;ambiente *Publish*. Sono previste cinque fasi:

* [Verifica della conoscenza](#verification-of-knowledge)
* [Definizione di ambito di applicazione](#scope-definition)
* [Metodologie Di Prova](#test-methodologies)
* [Definizione degli obiettivi prestazionali](#defining-the-performance-goals)
* [Ottimizzazione](#optimization)

Il controllo è un processo aggiuntivo e completo, necessario ma non limitato ai test.

### Verifica della conoscenza {#verification-of-knowledge}

Un primo passaggio consiste nel documentare le informazioni di base che è necessario conoscere prima di poter iniziare il test:

* l&#39;architettura dell&#39;ambiente di test
* una mappa dell&#39;applicazione che specifica gli elementi interni che dovranno essere testati (sia in isolamento che in combinazione)

#### Architettura di test {#test-architecture}

È necessario documentare chiaramente l&#39;architettura dell&#39;ambiente di test utilizzato per il test delle prestazioni.

Sarà necessaria una riproduzione dell&#39;ambiente di produzione Publish pianificato, insieme a Dispatcher e Load Balancer.

#### Mappa applicazione {#application-map}

Per ottenere una panoramica chiara, potete creare una mappa dell’intera applicazione (questa potrebbe essere disponibile anche dai test sull’ambiente Authoring).

una rappresentazione diagramma degli elementi interni dell&#39;applicazione, che possa fornire una panoramica dei requisiti di prova; con la codifica dei colori può anche fungere da base per la creazione di report.

### Definizione ambito {#scope-definition}

Un&#39;applicazione avrà in genere una selezione di casi di utilizzo. Alcuni saranno molto importanti, altri meno.

Per focalizzare l&#39;ambito del test delle prestazioni sulla pubblicazione, si consiglia di definire i seguenti parametri:

* casi di utilizzo aziendale più importanti
* casi di utilizzo tecnico più critici

Il numero di casi d’uso dipende dall’utente, ma deve essere limitato a un numero facilmente gestibile (ad esempio tra 5 e 10).

Una volta selezionati i casi d’uso chiave, gli indicatori prestazioni chiave (KPI) e gli strumenti utilizzati per misurarli possono essere definiti per ogni caso. Esempi di KPI comuni:

* Tempo di risposta finale
* Tempo di risposta del servlet
* Tempo di risposta per un singolo componente
* Tempo di risposta per i servizi
* Numero di thread inattivi nel pool di thread
* Numero di connessioni gratuite
* Risorse di sistema come CPU e accesso I/O

### Metodologie di prova {#test-methodologies}

Questo concetto include 4 scenari utilizzati per definire e testare gli obiettivi prestazionali:

* Test per singoli componenti
* Test combinati dei componenti
* *Vai* Livescenario
* Scenari di errore

In base ai seguenti principi.

**Punti di interruzione componente**

* Ogni componente ha un punto di interruzione specifico in relazione alle prestazioni. Ciò significa che un componente può mostrare buone prestazioni fino al raggiungimento di un punto specifico, dopodiché le prestazioni peggioreranno rapidamente.
* Per ottenere una panoramica completa dell’applicazione, è innanzitutto necessario verificare i componenti per determinare quando viene raggiunto il punto di interruzione di ciascuna applicazione.
* Per trovare il punto di interruzione è possibile eseguire un test di carico in cui, in un periodo di tempo, si aumenta il numero di utenti per creare un carico crescente. Monitorando questo carico e la risposta dei componenti, si verificherà un comportamento di prestazioni specifico quando viene raggiunto il punto di interruzione del componente. Il punto può essere definito dal numero di transazioni simultanee al secondo, insieme al numero di utenti simultanei (se il componente è sensibile a questo indicatore KPI).
* Tali informazioni possono quindi fungere da punto di riferimento per i miglioramenti, indicare l&#39;efficienza delle misure utilizzate e contribuire a definire gli scenari di test.

**Transazioni**

* Il termine transazione è utilizzato per rappresentare la richiesta di una pagina Web completa, inclusa la pagina stessa e tutte le chiamate successive; ad esempio, la richiesta di pagina, le chiamate AJAX, le immagini e altri oggetti.**Richiesta Drill Down**
* Per analizzare completamente ogni richiesta potete rappresentare ogni elemento dello stack di chiamate, quindi calcolare il tempo medio di elaborazione per ogni elemento.

### Definizione degli obiettivi di prestazioni {#defining-the-performance-goals}

Una volta definiti l’ambito e i relativi KPI, è possibile impostare gli obiettivi di prestazioni specifici. Ciò comporta l&#39;elaborazione di scenari di test, insieme ai valori target.

Sarà necessario testare le prestazioni sia in condizioni medie che di picco. Inoltre, avrete bisogno di Andare Live scenario test per garantire che si possa soddisfare per aumentare l&#39;interesse nel sito Web quando viene reso disponibile per la prima volta.

Qualsiasi esperienza, o statistiche che potreste aver raccolto da un sito Web esistente, può essere utile anche per determinare gli obiettivi futuri; ad esempio il traffico principale dal sito Web live.

#### Test per singolo componente {#single-component-tests}

I componenti critici dovranno essere testati, sia in condizioni medie che di picco.

In entrambi i casi, è possibile definire il numero previsto di transazioni al secondo quando un numero predefinito di utenti utilizza il sistema.

| Componente | Tipo di test | #Utenti | Tx/sec (previsto) | Tx/sec (testato) | Descrizione |
|---|---|---|---|---|---|
| Homepage Utente Singolo | Media | 1 | 1 |  |  |
|  | Picco | 3 | 3 |  |  |
| Homepage 100 utenti | Media | 100 | 3 |  |  |
|  | Picco | 100 | 1 |  |

#### Test combinati dei componenti {#combined-component-tests}

La verifica dei componenti in combinazione offre una migliore riflessione sul comportamento delle applicazioni. Anche in questo caso è necessario testare le condizioni medie e di picco.

| Scenario | Componente | #Utenti | Tx/sec (previsto) | Tx/sec (testato) | Descrizione |
|---|---|---|---|---|---|
| Media mista | Home page | 10 | 1 |  |  |
|  | Ricerca | 10 | 3 |  |  |
|  | Notizie | 10 | 2 |  |  |
|  | Eventi | 10 | 1 |  |  |
|  | Activations | 10 | 3 |  | Simulazione del comportamento dell’autore. |
| Picco misto | Home page | 100 | 5 |  |  |
|  | Ricerca | 50 | 5 |  |  |
|  | Notizie | 100 | 10 |  |  |
|  | Eventi | 100 | 10 |  |  |
|  | Activations | 20 | 20 |  | Simulazione del comportamento dell’autore. |

#### Esecuzione di test live {#going-live-tests}

Nei primi giorni successivi alla disponibilità del sito Web, è possibile che si verifichi un aumento del livello di interesse. Questo sarà probabilmente anche maggiore dei valori di picco per i quali avete eseguito il test. È vivamente consigliato testare scenari Go Live per garantire che il sistema possa soddisfare questa situazione.

| Scenario | Tipo di test | #Utenti | Tx/sec (previsto) | Tx/sec (testato) | Descrizione |
|---|---|---|---|---|---|
| Vai al picco live | Home page | 200 | 20 |  |  |
|  | Ricerca | 100 | 10 |  |  |
|  | Notizie | 200 | 20 |  |  |
|  | Eventi | 200 | 20 |  |  |
|  | Activations | 20 | 20 |  | Simulazione del comportamento dell’autore. |

#### Test scenario errore {#error-scenario-tests}

È inoltre necessario testare gli scenari di errore per garantire che il sistema reagisca correttamente e correttamente. Non solo per come viene gestito l&#39;errore, ma anche per l&#39;impatto che potrebbe avere sulle prestazioni. Esempio:

* cosa accade quando l&#39;utente tenta di inserire un termine di ricerca non valido nella casella di ricerca
* cosa accade quando il termine di ricerca è così generale che restituisce un numero eccessivo di risultati

Nel concepire questi test si dovrebbe ricordare che non tutti gli scenari si verificano regolarmente. Tuttavia, il loro impatto sull&#39;intero sistema è importante.

| Scenario di errore | Tipo errore | #Utenti | Tx/sec (previsto) | Tx/sec (testato) | Descrizione |
|---|---|---|---|---|---|
| Sovraccarico del componente di ricerca | Cerca nei caratteri jolly globali (asterisco) | 10 | 1 |  | Solo &amp;ast;&amp;ast;&amp;ast; vengono cercate. |
|  | Interrompi parola | 20 | 2 |  | Ricerca di una parola di arresto. |
|  | Stringa vuota | 10 | 1 |  | Ricerca di una stringa vuota. |
|  | Caratteri speciali | 10 | 1 |  | Ricerca di caratteri speciali. |

#### Test di resistenza {#endurance-tests}

Alcuni problemi si verificheranno solo dopo che il sistema è stato in funzione per un periodo di tempo continuo; sia ore o anche giorni. Una prova di resistenza è utilizzata per testare un carico medio costante in un periodo di tempo richiesto. È quindi possibile analizzare qualsiasi degradazione delle prestazioni.

| Scenario | Tipo di test | #Utenti | Tx/sec (previsto) | Tx/sec (testato) | Descrizione |
|---|---|---|---|---|---|
| Prova di resistenza (72 ore) | Home page | 10 | 3 |  |  |
|  | Ricerca | 10 | 3 |  |  |
|  | Notizie | 20 | 2 |  |  |
|  | Eventi | 10 | 3 |  |  |
|  | Activations | 1 | 1 |  | Simulazione del comportamento dell’autore. |

### Ottimizzazione {#optimization}

Nelle fasi successive dell&#39;implementazione sarà necessario ottimizzare l&#39;applicazione per raggiungere / massimizzare gli obiettivi di prestazioni.

Eventuali ottimizzazioni effettuate devono essere verificate in modo da garantire che:

* senza influire sulla funzionalità
* è stato verificato con le prove di carico prima del rilascio

È disponibile una serie di strumenti per aiutarti con la generazione del carico, il monitoraggio delle prestazioni e/o l&#39;analisi dei risultati:

* [JMeter](https://jakarta.apache.org/jmeter/)
* [Load Runner](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)
* [](https://www.determyne.com/) DeterminareInsideApps
* [InfraRED](https://www.infraredsoftware.com/)
* [Profilo interattivo Java](https://jiprof.sourceforge.net/)
* molti altri...

Dopo l&#39;ottimizzazione, sarà necessario eseguire nuovamente il test per confermare l&#39;impatto.

### Generazione rapporti {#reporting}

Sarà necessaria una relazione permanente per informare tutti sullo stato; come accennato in precedenza con la codifica a colori, la mappa di architettura può essere utilizzata per questo.

Una volta completati tutti i test, sarà necessario eseguire un rapporto su:

* eventuali errori critici riscontrati
* questioni non critiche che necessitano di ulteriori indagini
* eventuali ipotesi effettuate durante la prova
* eventuali raccomandazioni derivanti dalla verifica

## Ottimizzazione delle prestazioni quando si utilizza il dispatcher {#optimizing-performance-when-using-the-dispatcher}

Il [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) è  strumento  caching e/o bilanciamento del carico. Quando si utilizza il dispatcher è consigliabile ottimizzare il sito Web per le prestazioni della cache.

>[!NOTE]
>
>Le versioni del dispatcher sono indipendenti da AEM, tuttavia la documentazione del dispatcher è incorporata nella documentazione AEM. Usa sempre la documentazione del dispatcher incorporata nella documentazione per la versione più recente di AEM.
>
>Potresti essere stato reindirizzato a questa pagina se hai seguito un collegamento alla documentazione di Dispatcher incorporato nella documentazione di una versione precedente di AEM.

Il Dispatcher offre una serie di meccanismi incorporati che è possibile utilizzare per ottimizzare le prestazioni se il sito Web ne usufruisce. In questa sezione viene illustrato come progettare il sito Web per massimizzare i vantaggi della memorizzazione nella cache.

>[!NOTE]
>
>Potrebbe essere utile ricordare che il Dispatcher memorizza la cache su un server Web standard. Ciò significa che:
>
>* è possibile memorizzare nella cache tutto ciò che è possibile memorizzare come pagina e richiederlo utilizzando un URL
>* non è possibile memorizzare altri elementi, quali cookie, dati di sessione e dati del modulo.

>
>
In generale, molte strategie di caching richiedono la selezione di buoni URL e non affidarsi a questi dati aggiuntivi.
>
>Con la versione 4.1.11 del dispatcher è inoltre possibile memorizzare nella cache le intestazioni delle risposte. Vedere [Memorizzazione delle intestazioni delle risposte HTTP nella cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache).


### Calcolo del rapporto cache del dispatcher {#calculating-the-dispatcher-cache-ratio}

La formula del rapporto cache stima la percentuale di richieste gestite dalla cache rispetto al numero totale di richieste che arrivano nel sistema. Per calcolare il rapporto della cache è necessario disporre dei seguenti elementi:

* Numero totale di richieste. Queste informazioni sono disponibili in Apache `access.log`. Per ulteriori dettagli, vedere la [documentazione ufficiale di Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* Numero di richieste servite dall&#39;istanza Pubblica. Queste informazioni sono disponibili in `request.log` dell&#39;istanza. Per ulteriori dettagli, vedere [Interpretazione della richiesta.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) e [Ricerca dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

La formula per calcolare il rapporto della cache è la seguente:

* (Il numero totale di richieste **meno** il numero di richieste in Pubblica) **divise** per il numero totale di richieste.

Ad esempio, se il numero totale di richieste è 129491 e il numero di richieste servite dall’istanza Pubblica è 58959, il rapporto della cache è: **(129491 - 58959)/129491= 54,5%**.

Se non si dispone di un&#39;associazione uno-uno editore/dispatcher, sarà necessario aggiungere insieme le richieste di tutti i dispatcher e gli editori per ottenere una misurazione accurata. Vedere anche [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Per ottenere prestazioni ottimali,  Adobe consiglia un rapporto cache compreso tra 90% e 95%.

#### Utilizzo della codifica di pagina coerente {#using-consistent-page-encoding}

Con la versione 4.1.11 del dispatcher è possibile memorizzare nella cache le intestazioni delle risposte. Se non si memorizzano nella cache le intestazioni di risposta sul dispatcher, possono verificarsi problemi se si memorizzano le informazioni di codifica della pagina nell&#39;intestazione. In questa situazione, quando Dispatcher invia una pagina dalla cache, per la pagina viene utilizzata la codifica predefinita del server Web. Esistono due modi per evitare questo problema:

* Se utilizzate una sola codifica, accertatevi che la codifica utilizzata sul server Web sia la stessa della codifica predefinita del sito Web AEM.
* Utilizzate un tag `<META>` nella sezione HTML `head` per impostare la codifica, come nell&#39;esempio seguente:

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### Evitare i parametri URL {#avoid-url-parameters}

Se possibile, evitate i parametri URL per le pagine che desiderate memorizzare nella cache. Ad esempio, se disponete di una raccolta immagini, l&#39;URL seguente non viene mai memorizzato nella cache (a meno che Dispatcher non sia [configurato di conseguenza](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache)):

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

Tuttavia, potete inserire questi parametri nell’URL della pagina, come segue:

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>Questo URL richiama la stessa pagina e lo stesso modello di galleria.html. Nella definizione del modello, è possibile specificare quale script esegue il rendering della pagina oppure utilizzare lo stesso script per tutte le pagine.

#### Personalizza per URL {#customize-by-url}

Se consentite agli utenti di modificare la dimensione del font (o qualsiasi altra personalizzazione del layout), accertatevi che le diverse personalizzazioni siano riportate nell’URL.

Ad esempio, i cookie non sono memorizzati nella cache, pertanto se si memorizzano le dimensioni del font in un cookie (o in un meccanismo simile), la dimensione del font non viene mantenuta per la pagina memorizzata nella cache. Di conseguenza, il dispatcher restituisce i documenti di qualsiasi dimensione di font a caso.

L&#39;inclusione della dimensione del font nell&#39;URL come selettore evita questo problema:

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>Per la maggior parte degli aspetti del layout, è anche possibile utilizzare fogli di stile e/o script sul lato client. Questi di solito funzionano molto bene con la cache.
>
>Questa funzione è utile anche per una versione di stampa in cui potete usare un URL come: &quot;
>
>`www.myCompany.com/news/main.print.html`
>
>Utilizzando la combinazione di script della definizione del modello, potete specificare uno script separato che esegue il rendering delle pagine di stampa.

#### Annullamento della convalida dei file immagine utilizzati come titoli {#invalidating-image-files-used-as-titles}

Se eseguite il rendering dei titoli di pagina o di altro testo come immagini, si consiglia di memorizzare i file in modo che vengano eliminati in seguito a un aggiornamento del contenuto sulla pagina:

1. Inserite il file immagine nella stessa cartella della pagina.
1. Usate il seguente formato di denominazione per il file immagine:

   `<page file name>.<image file name>`

Ad esempio, è possibile memorizzare il titolo della pagina myPage.html nel file myPage.title.gif. Questo file viene eliminato automaticamente se la pagina viene aggiornata, pertanto qualsiasi modifica al titolo della pagina viene automaticamente riflessa nella cache.

>[!NOTE]
>
>Il file immagine non esiste necessariamente fisicamente nell&#39;istanza AEM. È possibile utilizzare uno script che crea in modo dinamico il file immagine. Il dispatcher memorizza quindi il file sul server Web.

#### Annullamento della convalida dei file immagine utilizzati per la navigazione {#invalidating-image-files-used-for-navigation}

Se si utilizzano le immagini per le voci di navigazione, il metodo è sostanzialmente lo stesso che con i titoli, leggermente più complessi. Archiviate tutte le immagini di navigazione con le pagine di destinazione. Se si utilizzano due immagini per la modalità normale e attiva, è possibile utilizzare i seguenti script:

* Uno script che visualizza la pagina come normale.
* Uno script che elabora richieste &quot;.normal&quot; e restituisce l&#39;immagine normale.
* Uno script che elabora &quot;.active&quot; richiede e restituisce l&#39;immagine attivata.

È importante creare queste immagini con lo stesso handle di denominazione della pagina, per fare in modo che un aggiornamento del contenuto elimini sia queste immagini che la pagina.

Per le pagine che non vengono modificate, le immagini rimangono nella cache, anche se le pagine stesse vengono in genere invalidate automaticamente.

#### Personalizzazione {#personalization}

Il Dispatcher non è in grado di memorizzare nella cache i dati personalizzati, pertanto si consiglia di limitare la personalizzazione a dove necessario. Per illustrare i motivi:

* Se utilizzate una pagina iniziale liberamente personalizzabile, tale pagina deve essere composta ogni volta che un utente la richiede.
* Se, invece, si offre una scelta di 10 pagine iniziali diverse, è possibile memorizzare nella cache ciascuna di esse, migliorando così le prestazioni.

>[!NOTE]
>
>Se personalizzate ciascuna pagina (ad esempio inserendo il nome dell’utente nella barra del titolo) non potete memorizzarla nella cache, il che può avere un impatto maggiore sulle prestazioni.
>
>Tuttavia, se dovete eseguire questa operazione, potete:
>
>* utilizzate iFrame per dividere la pagina in una parte identica per tutti gli utenti e in una parte identica per tutte le pagine dell&#39;utente. Potete quindi memorizzare nella cache entrambe le parti.
>* utilizzate JavaScript lato client per visualizzare informazioni personalizzate. Tuttavia, è necessario verificare che la pagina venga visualizzata correttamente anche se l&#39;utente disattiva JavaScript.

>



#### Connessioni permanenti {#sticky-connections}

[Connessione ](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#the-benefits-of-load-balancing) fissa, assicurarsi che i documenti per un utente siano tutti composti sullo stesso server. Se un utente lascia la cartella e successivamente vi ritorna, la connessione rimane fissa. Definite una cartella per contenere tutti i documenti che richiedono connessioni permanenti per il sito Web. Cercate di non inserire altri documenti. Questo influisce sul bilanciamento del carico se utilizzate pagine personalizzate e dati di sessione.

#### Tipi MIME {#mime-types}

Esistono due modi in cui un browser può determinare il tipo di file:

1. Per estensione (ad esempio .html, .gif, .jpg, ecc.)
1. Per tipo MIME inviato dal server con il file.

Per la maggior parte dei file, il tipo MIME è implicito nell&#39;estensione del file. i.e.:

1. Per estensione (ad esempio .html, .gif, .jpg, ecc.)
1. Per tipo MIME inviato dal server con il file.

Se il nome del file non ha estensione, viene visualizzato come testo normale.

Con la versione 4.1.11 del dispatcher è possibile memorizzare nella cache le intestazioni delle risposte. Se non si memorizzano nella cache le intestazioni di risposta del dispatcher, tenere presente che il tipo MIME fa parte dell&#39;intestazione HTTP. Di conseguenza, se l&#39;applicazione AEM restituisce file che non hanno una fine riconosciuta e si basano invece sul tipo MIME, questi file potrebbero essere visualizzati in modo non corretto.

Per essere certi che i file siano memorizzati nella cache in modo corretto, attenetevi alle seguenti linee guida:

* Accertatevi che i file abbiano sempre l&#39;estensione corretta.
* Evitate gli script di server di file generici, con URL quali download.jsp?file=2214. riscrivere lo script per utilizzare gli URL contenenti la specifica del file; nell’esempio precedente, questo sarà download.2214.pdf.

## Prestazioni di backup {#backup-performance}

Questa sezione presenta una serie di benchmark utilizzati per valutare le prestazioni dei backup CQ e gli effetti dell&#39;attività di backup sulle prestazioni dell&#39;applicazione. Il backup CQ presenta un carico significativo sul sistema mentre viene eseguito, e misuriamo questo, così come gli effetti delle impostazioni di ritardo del backup che tentano di modulare questi effetti. L&#39;obiettivo è quello di fornire alcuni dati di riferimento sulle prestazioni previste dei backup in configurazioni realistiche e sulle quantità di dati di produzione, e di fornire indicazioni su come stimare i tempi di backup per i sistemi pianificati.

### Ambiente di riferimento {#reference-environment}

#### Sistema fisico {#physical-system}

I risultati riportati in questo documento sono stati ottenuti da benchmark eseguiti in un ambiente di riferimento con la seguente configurazione. Questa configurazione è simile a un ambiente di produzione tipico di un data center:

* H-P ProLiant DL380 G6, 8 CPU x 2,533 GHz
* Unità SCSI Serial Attached 300 GB 10.000 RPM
* Controller RAID hardware; 8 unità in un array RAID0+5
* CPU immagine VMware x 2 Intel Xeon E5540 a 2,53 GHz
* RedHat Linux 2.6.18-194.el5; Java 1.6.0_29
* Single Author instance con CQ 5.5 GM.

Il sottosistema del disco su questo server è abbastanza veloce, rappresentativo di una configurazione RAID ad alte prestazioni che potrebbe essere utilizzata in un server di produzione. Le prestazioni di backup possono essere sensibili alle prestazioni del disco e i risultati in questo ambiente riflettono le prestazioni su una configurazione RAID molto veloce. L&#39;immagine VMWare è configurata per avere un singolo grande volume di disco che risiede fisicamente nello storage locale su disco, sull&#39;array RAID.

La configurazione CQ posiziona il repository e il datastore sullo stesso volume logico, insieme a tutto il sistema operativo e il software CQ. La directory di destinazione per i backup risiede anche in questo file system logico.

#### Volumi di dati {#data-volumes}

Nella tabella seguente sono illustrate le dimensioni dei volumi di dati utilizzati nei benchmark di backup. Il contenuto della linea di base iniziale viene installato per primo, quindi vengono aggiunte ulteriori quantità note di dati per aumentare le dimensioni del contenuto di cui viene eseguito il backup. I backup verranno creati con incrementi specifici per rappresentare un aumento significativo del contenuto e di ciò che può essere prodotto in un giorno. La distribuzione dei contenuti (pagine, immagini, tag) si baserà approssimativamente sulla composizione realistica delle risorse di produzione. Pagine, immagini e tag possono essere limitati a un massimo di 800 pagine figlie. Ogni pagina includerà i componenti titolo, Flash, testo/immagine, video, presentazione, modulo, tabella, cloud e carosello. Le immagini verranno caricate da un pool di 400 file unici, di dimensioni comprese tra 37 kB e 594 kB.

<table>
 <tbody>
  <tr>
   <td><strong>Contenuto</strong></td>
   <td><strong>Nodi</strong></td>
   <td><strong>Pagine</strong></td>
   <td><strong>Immagini</strong></td>
   <td><strong>Tag</strong></td>
  </tr>
  <tr>
   <td>Installazione di base</td>
   <td>69.610</td>
   <td>562</td>
   <td>256</td>
   <td>237</td>
  </tr>
  <tr>
   <td>Piccoli contenuti per il backup incrementale</td>
   <td><br type="_moz" /> </td>
   <td>+100</td>
   <td>+2</td>
   <td>+2</td>
  </tr>
  <tr>
   <td>Contenuti di grandi dimensioni per il backup completo</td>
   <td><br type="_moz" /> </td>
   <td>+10.000</td>
   <td>+100</td>
   <td>+100</td>
  </tr>
 </tbody>
</table>

Il benchmark di backup viene ripetuto con i set di contenuti aggiuntivi aggiunti a ogni ripetizione.

#### Scenari di riferimento {#benchmark-scenarios}

I benchmark di backup coprono due scenari principali: backup quando il sistema è sottoposto a un carico significativo dell&#39;applicazione e backup quando il sistema è inattivo. Sebbene la raccomandazione generale sia di eseguire i backup quando il sistema CQ è il più inattivo possibile, in alcune situazioni è necessario eseguire il backup quando il sistema è sotto carico.

**I** backup Idle StateBackup vengono eseguiti senza alcuna altra attività in CQ.

**In** LoadBackups vengono eseguiti mentre il sistema è sotto l&#39;80% di carico dai processi online. Il ritardo del backup è stato modificato per vedere l&#39;impatto sul caricamento.

I tempi di backup e le dimensioni del backup risultante vengono ricavati dai registri del server CQ. In genere si consiglia di pianificare i backup per i tempi di inattività di CQ, ad esempio nel cuore della notte. Questo scenario è rappresentativo dell&#39;approccio raccomandato.

Il caricamento sarà composto da creazione/eliminazione di pagine, traversate e query con la maggior parte del carico proveniente da attraversamenti di pagina e query. L’aggiunta e la rimozione di troppe pagine aumenta continuamente la dimensione dell’area di lavoro e impedisce il completamento dei backup. La distribuzione del carico che lo script utilizzerà è il 75% di traversate di pagina, il 24% di query e l&#39;1% di creazioni di pagina (livello singolo senza sottopagine nidificata). Il picco di transazioni medie al secondo su un sistema inattivo viene raggiunto con 4 thread simultanei, che è ciò che verrà utilizzato per testare i backup sotto carico.

L&#39;impatto del carico sulle prestazioni di backup può essere stimato dalla differenza tra le prestazioni con e senza questo carico dell&#39;applicazione. L&#39;impatto del backup sul throughput dell&#39;applicazione si trova confrontando il throughput dello scenario in transazioni all&#39;ora con e senza un backup simultaneo in corso, e con i backup che funzionano con diverse impostazioni di &quot;ritardo del backup&quot;.

**Impostazione** ritardataPer diversi scenari abbiamo anche modificato l&#39;impostazione del ritardo di backup, utilizzando valori di 10 ms (predefinito), 1 ms e 0 ms, per scoprire in che modo questa impostazione influiva sulle prestazioni dei backup.

**Backup** typeTutti i backup erano backup esterni del repository effettuati in una directory di backup senza creare un file ZIP, tranne in un caso unico per il confronto dove il comando tar è stato utilizzato direttamente. Poiché i backup incrementali non possono essere creati su un file zip, o quando il backup completo precedente è un file zip, il metodo di directory di backup è il più utilizzato nelle situazioni di produzione.

### Riepilogo dei risultati {#summary-of-results}

#### Tempo di backup e Troughput {#backup-time-and-troughput}

Il risultato principale di questi benchmark è di mostrare come i tempi di backup variano in funzione del tipo di backup e della quantità complessiva di dati. Il grafico seguente mostra il tempo di backup ottenuto utilizzando la configurazione di backup predefinita, in funzione del numero totale di pagine.

![chlimage_1-81](assets/chlimage_1-81.png)

I tempi di backup su un’istanza inattiva sono abbastanza coerenti, con una media di 0,608 MB/s indipendentemente dai backup completi o incrementali (vedere il grafico di seguito). Il tempo di backup è semplicemente una funzione della quantità di dati di cui viene eseguito il backup. Il tempo necessario per completare un backup completo aumenta nettamente con il numero totale di pagine. Il tempo necessario per completare un backup incrementale aumenta anche con il numero totale di pagine, ma con una frequenza molto inferiore. Il tempo necessario per completare il backup incrementale è molto più breve a causa della quantità relativamente ridotta di dati sottoposti a backup.

La dimensione del backup prodotto è il principale fattore determinante del tempo necessario per completare un backup. Il grafico seguente mostra il tempo impiegato in funzione della dimensione finale del backup.

![chlimage_1-82](assets/chlimage_1-82.png)

Questo grafico mostra che sia i backup incrementali che quelli completi seguono un semplice pattern di dimensioni rispetto al tempo che possiamo misurare come throughput. I tempi di backup su un&#39;istanza inattiva sono abbastanza coerenti, con una media di 0,61 MB/sec, indipendentemente dai backup completi o incrementali nell&#39;ambiente di riferimento.

#### Ritardo backup {#backup-delay}

Il parametro di ritardo del backup viene fornito per limitare la possibilità di backup che interferiscano con i carichi di lavoro di produzione. Il parametro specifica un tempo di attesa, in millisecondi, che viene incluso nell&#39;operazione di backup file per file. L’effetto complessivo dipende in parte dalla dimensione dei file interessati. La misurazione delle prestazioni di backup in MB/sec offre un modo ragionevole per confrontare gli effetti del ritardo sul backup.

* L&#39;esecuzione contemporanea di un backup con il normale caricamento dell&#39;applicazione avrà un impatto negativo sul throughput del caricamento regolare.
* L&#39;impatto può essere leggero, fino al 5%, o potrebbe essere molto significativo, causando fino al 75% di riduzione del throughput, e questo probabilmente dipende dall&#39;applicazione più di ogni altra cosa.
* Il backup non è un carico pesante sulla CPU, quindi i carichi di lavoro di produzione che richiedono molta CPU potrebbero risentire meno del backup rispetto a quelli che richiedono un uso intensivo di I/O.

![chlimage_1-83](assets/chlimage_1-83.png)

Per confrontare il throughput ottenuto utilizzando un backup del file system (utilizzando &#39;tar&#39;) per il backup degli stessi file del repository. Le prestazioni del catrame sono paragonabili, ma leggermente superiori al backup con ritardo impostato a zero. L&#39;impostazione di un ritardo minimo riduce notevolmente il throughput di backup e il ritardo predefinito di 10 ms riduce notevolmente il throughput. Nelle situazioni in cui i backup possono essere pianificati quando l&#39;utilizzo complessivo dell&#39;applicazione è molto basso o l&#39;applicazione può essere completamente inattiva, è probabilmente consigliabile ridurre il ritardo al di sotto del valore predefinito, in modo da consentire il backup più rapido.

L&#39;impatto effettivo del throughput dell&#39;applicazione di un backup in corso dipende dai dettagli dell&#39;applicazione e dell&#39;infrastruttura. La scelta del valore di ritardo dovrebbe essere fatta attraverso un&#39;analisi empirica dell&#39;applicazione, ma dovrebbe essere scelta il più piccola possibile, in modo da completare i backup il più rapidamente possibile. Poiché esiste solo una correlazione debole tra la scelta del valore di ritardo e l&#39;impatto sul throughput dell&#39;applicazione, la scelta del ritardo dovrebbe favorire tempi di backup complessivi più brevi, al fine di ridurre al minimo l&#39;impatto complessivo dei backup. Un backup che richiede 8 ore per essere completato, ma che influisce sul throughput del -20% potrebbe avere un impatto complessivo maggiore di uno che richiede 2 ore per completare, ma influenza il throughput del -30%.

### Riferimenti {#references}

* [Amministrazione - Backup e ripristino](/help/sites-administering/backup-and-restore.md)
* [Gestione - Capacità e volume](/help/managing/best-practices-further-reference.md#capacity-and-volume)

