---
title: Best practice per query e indicizzazione
seo-title: Best practice per query e indicizzazione
description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
seo-description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Best practice per query e indicizzazione{#best-practices-for-queries-and-indexing}

Oltre alla transizione a Oak in AEM 6, sono state apportate alcune modifiche importanti alla gestione di query e indici. In Jackrabbit 2, tutto il contenuto era indicizzato per impostazione predefinita e poteva essere interrogato liberamente. In Oak, gli indici devono essere creati manualmente sotto il `oak:index` nodo. Una query può essere eseguita senza un indice, ma per i set di dati di grandi dimensioni sarà eseguita molto lentamente o persino in modo interrotto.

Questo articolo descriverà quando creare indici e quando non sono necessari, trucchi per evitare di utilizzare query quando non sono necessari e suggerimenti per ottimizzare indici e query in modo da ottenere le migliori prestazioni possibili.

Inoltre, leggere la documentazione [Oak per scrivere query e indici](/help/sites-deploying/queries-and-indexing.md). Oltre a considerare gli indici come un nuovo concetto in AEM 6, durante la migrazione del codice da una precedente installazione di AEM è necessario tenere conto delle differenze di sintassi nelle query Oak.

## Quando utilizzare le query {#when-to-use-queries}

### Struttura del repository e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un repository, occorre tenere conto di diversi fattori. Tra questi, controlli di accesso, localizzazione, ereditarietà di componenti e proprietà di pagina.

Durante la progettazione di una tassonomia che risponda a questi problemi, è importante considerare anche la &quot;traversabilità&quot; del design di indicizzazione. In questo contesto, la traversabilità è la capacità di una tassonomia che consente l&#39;accesso prevedibile al contenuto in base al suo percorso. Questo renderà un sistema più performante che è più facile da mantenere di uno che richiederà molte query da eseguire.

Inoltre, durante la progettazione di una tassonomia, è importante considerare se l&#39;ordine è importante. Nei casi in cui l&#39;ordine esplicito non è richiesto e si prevedono numerosi nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è necessario ordinare `nt:unstructured` e `sling:OrderedFolder` sarebbe più appropriato.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni di imposizione più eseguite su un sistema AEM, è consigliabile evitarle nei componenti. L&#39;esecuzione di diverse query ogni volta che viene eseguito il rendering di una pagina può spesso compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare di eseguire query durante il rendering dei componenti: **attraversare i nodi** e **preacquisire i risultati**.

#### Navigazione dei nodi {#traversing-nodes}

Se il repository è progettato in modo tale da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera questi dati dai percorsi necessari può essere distribuito senza dover eseguire query per trovarli.

Un esempio potrebbe essere rappresentato dal rendering del contenuto che rientra in una determinata categoria. Un approccio consiste nell’organizzare il contenuto con una proprietà category che può essere richiesta per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nel strutturare il contenuto in una tassonomia per categoria in modo che possa essere recuperato manualmente.

Ad esempio, se il contenuto è memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

il `/content/myUnstructuredContent/parentCategory/childCategory` nodo può essere semplicemente recuperato, i relativi elementi secondari possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, può essere più veloce attraversare la directory archivio e raccogliere i nodi richiesti, anziché creare una query per restituire lo stesso set di risultati. In linea generale, occorre evitare le interrogazioni laddove possibile.

#### Preacquisizione dei risultati {#prefetching-results}

A volte il contenuto o i requisiti intorno al componente non consentiranno l&#39;uso del passaggio dei nodi come metodo per recuperare i dati richiesti. In questi casi, le query necessarie devono essere eseguite prima del rendering del componente in modo da garantire prestazioni ottimali all’utente finale.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non è previsto che il contenuto venga modificato, la query può essere eseguita quando l’autore applica le impostazioni nella finestra di dialogo.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita su una programmazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Quindi, i risultati possono essere scritti in una posizione condivisa nella directory archivio. Tutti i componenti che necessitano di questi dati possono quindi estrarre i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

## Ottimizzazione query {#query-optimization}

Durante l&#39;esecuzione di una query che non utilizza un indice, gli avvisi vengono registrati per quanto riguarda l&#39;attraversamento dei nodi. Se si tratta di una query che verrà eseguita spesso, è necessario creare un indice. Per determinare l&#39;indice utilizzato da una determinata query, si consiglia di utilizzare lo strumento [](/help/sites-administering/operations-dashboard.md#explain-query) Query Spiega. Per ulteriori informazioni, la registrazione DEBUG può essere abilitata per le API di ricerca pertinenti.

>[!NOTE]
>
>Dopo aver modificato una definizione di indice, è necessario rigenerare l&#39;indice (reindicizzato). A seconda della dimensione dell’indice, il completamento dell’operazione potrebbe richiedere del tempo.

Quando si eseguono query complesse, possono verificarsi casi in cui la suddivisione della query in più query più piccole e l&#39;unione dei dati attraverso il codice dopo che il fatto è più performante. La raccomandazione per questi casi è di confrontare le prestazioni dei due approcci per determinare quale opzione sarebbe migliore per il caso d&#39;uso in questione.

AEM consente di scrivere query in tre modi:

* Tramite le API [QueryBuilder](/help/sites-developing/querybuilder-api.md) (consigliato)
* Utilizzo di XPath (consigliato)
* Utilizzo di SQL2

Mentre tutte le query vengono convertite in SQL2 prima di essere eseguite, il sovraccarico della conversione delle query è minimo e, quindi, la maggiore preoccupazione nella scelta di un linguaggio di query sarà la leggibilità e il livello di comfort dal team di sviluppo.

>[!NOTE]
>
>Quando si utilizza QueryBuilder, per impostazione predefinita viene determinato il conteggio dei risultati, che risulta più lento in Oak rispetto alle versioni precedenti di Jackrabbit. Per compensare questo, è possibile utilizzare il parametro [](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)approssimativoTotale.

### Lo strumento Spiega query {#the-explain-query-tool}

Come per qualsiasi lingua di query, il primo passo per ottimizzare una query è capire come verrà eseguita. Per abilitare questa attività, potete utilizzare lo strumento [](/help/sites-administering/operations-dashboard.md#explain-query) Spiega query presente nel Pannello operazioni. Con questo strumento, è possibile collegare e spiegare una query. Viene visualizzato un avviso se la query causerà problemi con un archivio di grandi dimensioni, oltre al tempo di esecuzione e agli indici utilizzati. Lo strumento può anche caricare un elenco di query lente e popolari che possono essere spiegate e ottimizzate.

### Registrazione DEBUG per le query {#debug-logging-for-queries}

Per ottenere ulteriori informazioni sulla scelta dell&#39;indice da utilizzare da parte di Oak e sulla modalità in cui il motore di query esegue effettivamente una query, è possibile aggiungere una configurazione di registrazione **DEBUG** per i pacchetti seguenti:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Assicuratevi di rimuovere questo logger quando avete finito di debugging della query in quanto produrrà un sacco di attività e può eventualmente riempire il disco con i file di registro.

Per ulteriori informazioni su come eseguire questa operazione, consulta la documentazione [](/help/sites-deploying/configure-logging.md)Registrazione.

### Statistiche indice {#index-statistics}

Lucene registra un file JMX che fornisce informazioni dettagliate sui contenuti indicizzati, incluse le dimensioni e il numero di documenti presenti in ciascuno degli indici.

Puoi raggiungerlo accedendo alla console JMX all&#39;indirizzo `https://server:port/system/console/jmx`

Una volta effettuato l’accesso alla console JMX, eseguite una ricerca per **Lucene Index Statistics** per individuarla. Altre statistiche di indice sono disponibili in **IndexStats** MBean.

Per le statistiche delle query, consultate l&#39;MBean denominato **Oak Query Statistics**.

Se desiderate approfondire gli indici con uno strumento come [Luke](https://code.google.com/p/luke/), dovrete utilizzare la console Oak per scaricare l&#39;indice dalla directory `NodeStore` a una directory del file system. Per istruzioni su come eseguire questa operazione, leggere la documentazione [di](https://jackrabbit.apache.org/oak/docs/query/lucene.html)Lucene.

Potete anche estrarre gli indici nel sistema in formato JSON. A tal fine, è necessario accedere a `https://server:port/oak:index.tidy.-1.json`

### Limiti per le query {#query-limits}

**Durante lo sviluppo**

Impostare soglie basse per `oak.queryLimitInMemory` (ad esempio 10000) e quercia. `queryLimitReads` (ad esempio 5000) e ottimizzare la query costosa quando si tocca un UnsupportedOperationException che dice &quot;La query ha letto più di x nodi...&quot;

In questo modo si evitano le query che richiedono molte risorse (ad esempio non sostenuto da alcun indice o sostenuto da un indice di copertura inferiore). Ad esempio, una query che legge 1 milione di nodi comporterebbe un aumento dell&#39;I/O e avrebbe un impatto negativo sulle prestazioni complessive dell&#39;applicazione. Qualsiasi query che non riesce a causa di limiti superiori deve essere analizzata e ottimizzata.

#### **Post-distribuzione**{#post-deployment}

* Monitorare i registri per le query che attivano il consumo di memoria heap di grandi nodi: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizzare la query per ridurre il numero di nodi attraversati

* Monitorare i registri per le query che attivano un grande consumo di memoria heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizzare la query per ridurre il consumo di memoria heap

Per le versioni di AEM 6.0 - 6.2, puoi regolare la soglia per l’attraversamento dei nodi tramite i parametri JVM nello script di avvio di AEM per evitare che query di grandi dimensioni sovraccarichino l’ambiente.

I valori consigliati sono:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri indicati sopra sono OOTB preconfigurati e possono essere memorizzati tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Suggerimenti per la creazione di indici efficienti {#tips-for-creating-efficient-indexes}

### Devo creare un indice? {#should-i-create-an-index}

La prima domanda da porre al momento della creazione o dell’ottimizzazione degli indici è se questi siano effettivamente necessari per una determinata situazione. Se si desidera eseguire la query in questione solo una volta o solo occasionalmente e in un momento di picco per il sistema attraverso un processo batch, potrebbe essere meglio non creare alcun indice.

Dopo aver creato un indice, ogni volta che i dati indicizzati vengono aggiornati, è necessario aggiornare anche l&#39;indice. Poiché questo comporta implicazioni in termini di prestazioni per il sistema, gli indici dovrebbero essere creati solo quando sono effettivamente richiesti.

Inoltre, gli indici sono utili solo se i dati contenuti all&#39;interno dell&#39;indice sono abbastanza univoci da giustificarlo. Considerate un indice in un libro e gli argomenti trattati. Quando si indicizza un insieme di argomenti in un testo, in genere sono presenti centinaia o migliaia di voci, il che consente di passare rapidamente a un sottoinsieme di pagine per trovare rapidamente le informazioni che si stanno cercando. Se l&#39;indice contenesse solo due o tre voci, ognuna delle quali indicava diverse centinaia di pagine, l&#39;indice non sarebbe molto utile. Lo stesso concetto si applica agli indici di database. Se ci sono solo due valori univoci, l&#39;indice non sarà molto utile. Detto questo, un indice può anche diventare troppo grande per essere utile. Per consultare le statistiche sugli indici, consulta [Statistiche](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) di indice sopra.

### Lucene o indici di proprietà? {#lucene-or-property-indexes}

Gli indici Lucene sono stati introdotti in Oak 1.0.9 e offrono alcune potenti ottimizzazioni sugli indici delle proprietà introdotti nel primo avvio di AEM 6. Nel decidere se utilizzare gli indici Lucene o gli indici di proprietà, tenere presente quanto segue:

* Gli indici di Lucene offrono molte più funzionalità degli indici di proprietà. Ad esempio, un indice di proprietà può indicizzare solo una singola proprietà, mentre un indice Lucene può includere molti. Per ulteriori informazioni su tutte le funzioni disponibili negli indici Lucene, consulta la [documentazione](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Gli indici di Lucene sono asincrono. Questo offre un notevole miglioramento delle prestazioni, ma può anche causare un ritardo tra il momento in cui i dati vengono scritti nell&#39;archivio e il momento in cui l&#39;indice viene aggiornato. Se è fondamentale che le query restituiscano risultati accurati al 100%, è necessario un indice di proprietà.
* In quanto asincrone, gli indici Lucene non possono applicare vincoli di univocità. Se necessario, sarà necessario creare un indice di proprietà.

In generale, si consiglia di utilizzare indici Lucene a meno che non vi sia un&#39;urgente necessità di utilizzare indici di proprietà in modo da poter ottenere i vantaggi di prestazioni e flessibilità più elevate.

### Indicizzazione Solr {#solr-indexing}

AEM supporta anche l’indicizzazione Solr per impostazione predefinita. Questa funzione è principalmente utilizzata per supportare la ricerca full text, ma può essere utilizzata anche per supportare qualsiasi tipo di query JCR. Solr deve essere considerato quando le istanze di AEM non dispongono della capacità CPU per gestire il numero di query necessarie nelle distribuzioni che richiedono molta ricerca, come i siti Web basati sulla ricerca con un numero elevato di utenti simultanei. In alternativa, Solr può essere implementato in un approccio basato su crawler per sfruttare alcune delle caratteristiche più avanzate della piattaforma.

Gli indici solr possono essere configurati per l&#39;esecuzione incorporati nel server AEM per gli ambienti di sviluppo oppure per essere scaricati in un&#39;istanza remota per migliorare la scalabilità della ricerca negli ambienti di produzione e di staging. Mentre l&#39;offload della ricerca migliorerà la scalabilità, introdurrà latenza e per questo motivo, non è consigliato a meno che non richiesto. Per ulteriori informazioni su come configurare l’integrazione con Solr e come creare indici Solr, consulta la documentazione [Query](/help/sites-deploying/queries-and-indexing.md#the-solr-index)Oak e Indicizzazione.

>[!NOTE]
>
>L&#39;approccio integrato di ricerca Solr consente di scaricare l&#39;indicizzazione su un server Solr. Se le funzioni più avanzate del server Solr vengono utilizzate con un approccio basato su crawler, sarà necessario un ulteriore lavoro di configurazione. Headwire ha creato un connettore [](https://www.aemsolrsearch.com/#/) open source per accelerare questi tipi di implementazioni.

Il lato negativo di questo approccio è che, mentre per impostazione predefinita, le query AEM rispettano gli ACL e quindi nascondono i risultati a cui un utente non ha accesso, esternalizzando la ricerca a un server Solr non sarà in grado di supportare questa funzionalità. Se la ricerca deve essere esternalizzata in questo modo, occorre prestare maggiore attenzione al fatto che gli utenti non ricevano risultati che non dovrebbero vedere.

I casi d’uso potenziali in cui questo approccio può essere appropriato sono i casi in cui i dati di ricerca provenienti da più fonti possono dover essere aggregati. Ad esempio, un sito potrebbe essere ospitato su AEM e un secondo sito potrebbe essere ospitato su una piattaforma di terze parti. È possibile configurare Solr per eseguire una ricerca per indicizzazione del contenuto di entrambi i siti e memorizzarlo in un indice aggregato. Ciò consentirebbe ricerche tra siti.

### Design Considerations {#design-considerations}

La documentazione Oak per gli indici Lucene elenca diverse considerazioni da fare durante la progettazione degli indici:

* Se la query utilizza restrizioni di percorso diverse, utilizzare `evaluatePathRestrictions`. In questo modo la query restituirà il sottoinsieme di risultati nel percorso specificato e li filtrerà in base alla query. In caso contrario, la query cercherà tutti i risultati che corrispondono ai parametri della query nell&#39;archivio e li filtrerà in base al percorso.
* Se la query utilizza l&#39;ordinamento, è necessario avere una definizione esplicita della proprietà ordinata e impostare `ordered` per essa `true` . Ciò consentirà di ordinare i risultati come tali nell&#39;indice e di risparmiare sulle operazioni di ordinamento costose al momento dell&#39;esecuzione della query.

* Inserire solo ciò che è necessario nell&#39;indice. L&#39;aggiunta di funzioni o proprietà non necessarie causerà un aumento e una riduzione delle prestazioni dell&#39;indice.
* In un indice di proprietà, avere un nome di proprietà univoco contribuirebbe a ridurre le dimensioni di un indice, ma per gli indici di Lucene, utilizzare `nodeTypes` e `mixins` dovrebbe essere fatto per ottenere indici di coesione. La query su uno specifico `nodeType` o `mixin` sarà più efficace della query `nt:base`. Quando si utilizza questo approccio, definire `indexRules` per l&#39;oggetto `nodeTypes` in questione.

* Se le query vengono eseguite solo in determinati percorsi, creare tali indici sotto tali percorsi. Gli indici non sono necessari per vivere nella directory principale del repository.
* Si consiglia di utilizzare un indice singolo quando tutte le proprietà da indicizzare sono correlate per consentire a Lucene di valutare il maggior numero possibile di restrizioni di proprietà in modo nativo. Inoltre, una query utilizzerà un solo indice, anche quando si esegue un join.

### CopyOnRead {#copyonread}

Nei casi in cui `NodeStore` viene memorizzato in remoto, `CopyOnRead` è possibile abilitare un&#39;opzione denominata. L&#39;opzione causerà la scrittura dell&#39;indice remoto nel file system locale durante la lettura. Ciò può contribuire a migliorare le prestazioni delle query che vengono spesso eseguite in base a questi indici remoti.

Questo può essere configurato nella console OSGi sotto il servizio **LuceneIndexProvider** ed è attivato per impostazione predefinita a partire da Oak 1.0.13.

### Rimozione degli indici {#removing-indexes}

Quando si rimuove un indice, si consiglia sempre di disattivare temporaneamente l&#39;indice impostando la `type` proprietà su `disabled` ed eseguendo delle verifiche per verificare che l&#39;applicazione funzioni correttamente prima di eliminarla. Tenete presente che un indice non viene aggiornato mentre è disabilitato, pertanto potrebbe non avere il contenuto corretto se viene riabilitato e potrebbe essere necessario reindicizzarlo.

Dopo aver rimosso un indice di proprietà in un&#39;istanza TarMK, sarà necessario eseguire compaction per recuperare lo spazio su disco in uso. Per gli indici Lucene, il contenuto effettivo dell&#39;indice risiede in BlobStore, pertanto sarebbe necessario un processo di raccolta dei rifiuti per l&#39;archivio dati.

Quando si rimuove un indice in un&#39;istanza MongoDB, il costo dell&#39;eliminazione è proporzionale al numero di nodi nell&#39;indice. Poiché l’eliminazione di un indice di grandi dimensioni può causare problemi, si consiglia di disattivare l’indice ed eliminarlo solo durante una finestra di manutenzione, utilizzando uno strumento come **quercia-mongo.js**. Nota: questo approccio non deve essere utilizzato per il contenuto dei nodi regolari, in quanto può introdurre incoerenze nei dati.

>[!NOTE]
>
>Per ulteriori informazioni su oak-mongo.js, consulta la sezione [Strumenti della riga di](https://jackrabbit.apache.org/oak/docs/command_line.html) comando della documentazione Oak.

## Reindicizzazione {#re-indexing}

In questa sezione vengono illustrati gli **unici** motivi validi per reindicizzare gli indici Oak.

Al di fuori dei motivi indicati di seguito, l’avvio di nuovi indici Oak **non** modificherà il comportamento né risolverà i problemi, e aumenterà inutilmente il carico su AEM.

È opportuno evitare di reindicizzare gli indici Oak se non per motivi esposti nelle tabelle di seguito.

>[!NOTE]
>
>Prima di consultare le tabelle riportate di seguito per determinare la reindicizzazione è utile,** sempre **verify:
>
>* la query è corretta
>* la query viene risolta nell&#39;indice previsto (utilizzando [Query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)Spiega)
>* processo di indicizzazione completato
>



### Modifiche alla configurazione dell&#39;indice Oak {#oak-index-configuration-changes}

L’unica condizione accettabile di non-erring per reindicizzare gli indici Oak è se la configurazione di un indice Oak è cambiata.

*Il reindicizzazione deve essere sempre affrontata con la dovuta considerazione per l&#39;impatto sulle prestazioni complessive di AEM ed eseguita durante i periodi di attività o finestre di manutenzione ridotte.*

I seguenti dettagli possono essere presentati insieme alle risoluzioni:

* [Modifica definizione indice proprietà](#property-index-definition-change)
* [Modifica definizione indice Lucene](#lucene-index-definition-change)

#### Modifica definizione indice proprietà {#property-index-definition-change}

* Si applica per/if:

   * Tutte le versioni di Oak
   * Solo indici di [proprietà](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomi:

   * Nodi esistenti prima dell&#39;aggiornamento della definizione dell&#39;indice delle proprietà mancanti dai risultati

* Come verificare:

   * Determinare se i nodi mancanti sono stati creati/modificati prima della distribuzione della definizione di indice aggiornata.
   * Verificare le `jcr:created` proprietà o `jcr:lastModified` le proprietà di eventuali nodi mancanti rispetto all&#39;ora di modifica dell&#39;indice

* Come risolvere:

   * [Reindicizzare](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) l&#39;indice di lucene
   * In alternativa, toccate (eseguite un&#39;operazione di scrittura positiva) i nodi mancanti

      * Richiede tocco manuale o codice personalizzato
      * Richiede la conoscenza del set di nodi mancanti
      * Richiede la modifica di qualsiasi proprietà sul nodo

#### Modifica definizione indice Lucene {#lucene-index-definition-change}

* Si applica per/if:

   * Tutte le versioni di Oak
   * Solo indici [lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice di Lucene non contiene i risultati previsti
   * I risultati della query non riflettono il comportamento previsto della definizione di indice
   * Il piano di query non riporta l&#39;output previsto in base alla definizione dell&#39;indice

* Come verificare:

   * Verificare che la definizione dell&#39;indice sia stata modificata utilizzando il metodo JMX Mbay (LuceneIndex) delle statistiche dell&#39;indice Lucene `diffStoredIndexDefinition`.

* Come risolvere:

   * Versioni di quercia precedenti alla 1.6:

      * [Reindicizzare](#how-to-re-index) l&#39;indice di lucene
   * Oak versione 1.6+

      * Se il contenuto esistente non viene influenzato dalle modifiche, è necessario solo aggiornare

         * [Aggiornare](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) l&#39;indice di lucene impostando [oak:queryIndexDefinition]@refresh=true
      * In caso contrario, [reindicizzare](#how-to-re-index) l&#39;indice di lucene

         * Nota: Lo stato dell&#39;indice dall&#39;ultimo corretto reindicizzazione (o indicizzazione iniziale) viene utilizzato fino all&#39;attivazione di un nuovo reindicizzazione



### Errori e situazioni eccezionali {#erring-and-exceptional-situations}

Nella tabella seguente sono illustrate le uniche situazioni di errore ed eccezione accettabili in cui la reindicizzazione degli indici Oak risolverà il problema.

Se si verifica un problema in AEM che non soddisfa i criteri indicati di seguito, **non** reindicizzare gli indici, in quanto non risolverà il problema.

I seguenti dettagli possono essere presentati insieme alle risoluzioni:

* [Valore binario dell&#39;indice Lucene mancante](#lucene-index-binary-is-missing)
* [Il binario dell&#39;indice di Lucene è danneggiato](#lucene-index-binary-is-corrupt)

#### Valore binario dell&#39;indice Lucene mancante {#lucene-index-binary-is-missing}

* Si applica per/if:

   * Tutte le versioni di Oak
   * Solo indici [lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice di Lucene non contiene i risultati previsti

* Come verificare:

   * Il file di registro degli errori contiene un&#39;eccezione che indica la mancanza di un binario dell&#39;indice Lucene

* Come risolvere:

   * eseguire un controllo del repository di attraversamento; ad esempio:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      l&#39;attraversamento del repository determina se mancano altri file binari (oltre ai file lucene)

   * Se mancano file binari diversi dagli indici di lucene, eseguire il ripristino dal backup
   * In caso contrario, [reindirizzare](#how-to-re-index) *tutti* gli indici di lucene
   * Nota:

      Questa condizione è indicativa di un datastore configurato in modo errato che potrebbe generare QUALSIASI binario (ad esempio asset (file binari) da perdere.

      In questo caso, ripristinare l&#39;ultima versione buona nota del repository per recuperare tutti i binari mancanti.

#### Il binario dell&#39;indice di Lucene è danneggiato {#lucene-index-binary-is-corrupt}

* Si applica per/if:

   * Tutte le versioni di Oak
   * Solo indici [lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice di Lucene non contiene i risultati previsti

* Come verificare:

   * Il `AsyncIndexUpdate` (ogni 5s) errore con un’eccezione nel log error.log:

      `...a Lucene index file is corrupt...`

* Come risolvere:

   * Rimuovere la copia locale dell&#39;indice lucene

      1. Arresta AEM
      1. Elimina la copia locale dell&#39;indice di lucene in `crx-quickstart/repository/index`
      1. Riavvia AEM
   * Se questo non risolve il problema, e le `AsyncIndexUpdate` eccezioni persistono:

      1. [Reindicizzare](#how-to-re-index) l&#39;indice di errore
      1. È inoltre possibile archiviare un ticket di supporto [](https://helpx.adobe.com/support.html) Adobe


### Come reindicizzare {#how-to-re-index}

>[!NOTE]
>
>In AEM 6.5, [oak-run.jar è il metodo](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) SOLO supportato per la reindicizzazione nei repository MongoMK o RDBMK.

#### Indice delle proprietà di reindicizzazione {#re-indexing-property-indexes}

* Utilizzare [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) per reindicizzare l&#39;indice delle proprietà
* Impostare la proprietà asincrona-reindex su true nell&#39;indice delle proprietà

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindicizzare l’indice delle proprietà in modo asincrono utilizzando la console Web tramite **PropertyIndexAsyncReindex** MBean;

   ad esempio,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Riindicizzazione indici delle proprietà Lucene {#re-indexing-lucene-property-indexes}

* Utilizzate [oak-run.jar per reindicizzare](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) l&#39;indice delle proprietà Lucene.
* Impostate la proprietà asincrona-reindex su true nell&#39;indice delle proprietà lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sezione precedente riassume e inquadra le linee guida per il reindicizzazione Oak contenute nella documentazione [](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) Apache Oak nel contesto di AEM.

### Pre-estrazione del testo dei binari {#text-pre-extraction-of-binaries}

La preestrazione del testo è il processo di estrazione ed elaborazione del testo dai file binari, direttamente dall&#39;archivio dati attraverso un processo isolato, e di esposizione diretta del testo estratto ai successivi re/indici degli indici Oak.

* La preestrazione del testo Oak è consigliata per reindicizzare gli indici Lucene nei repository con grandi volumi di file (file binari) contenenti testo estraibile (ad esempio PDF, documenti Word, PPT, TXT ecc.) idonei alla ricerca full-text tramite indici Oak distribuiti; ad esempio `/oak:index/damAssetLucene`.
* La preestrazione del testo avvantaggia solo la reindicizzazione degli indici Lucene e degli indici delle proprietà NOT Oak, poiché gli indici delle proprietà non estraggono testo dai binari.
* La preestrazione del testo ha un impatto positivo elevato quando l’indicizzazione full-text dei file binari con testo pesante (PDF, Doc, TXT, ecc.), dove come archivio di immagini non avrà le stesse efficienze, poiché le immagini non contengono testo estraibile.
* La preestrazione del testo esegue l’estrazione del testo di ricerca full-text in modo estremamente efficiente e lo espone al processo di re/indicizzazione Oak in modo estremamente efficiente.

#### Quando è possibile utilizzare la preestrazione del testo? {#when-can-text-pre-extraction-be-used}

Reindicizzazione di un indice lucene **esistente** con l&#39;opzione di estrazione binaria abilitata

* reindicizzazione dell&#39;elaborazione di **tutto** il contenuto candidato nell&#39;archivio; quando i file binari da cui estrarre il testo completo sono numerosi o complessi, su AEM viene imposto un maggiore carico di calcolo per l’esecuzione dell’estrazione full-text. La preestrazione del testo sposta il &quot;lavoro computazionale&quot; dell’estrazione del testo in un processo isolato che accede direttamente all’Archivio dati di AEM, evitando sovraccarichi e controversie sulle risorse in AEM.

Supporto della distribuzione di un **nuovo** indice lucene in AEM con l’estrazione binaria abilitata

* Quando in AEM viene distribuito un nuovo indice (con l’estrazione binaria abilitata), Oak indicizza automaticamente tutto il contenuto candidato alla successiva esecuzione asincrona dell’indice full-text. Per gli stessi motivi descritti in precedenza nella reindicizzazione, questo potrebbe causare un carico eccessivo su AEM.

#### Quando è possibile utilizzare la preestrazione del testo NOT? {#when-can-text-pre-extraction-not-be-used}

La preestrazione del testo non può essere utilizzata per i nuovi contenuti aggiunti alla directory archivio, né per quelli necessari.

Il nuovo contenuto viene aggiunto alla directory archivio in modo naturale e incrementale mediante il processo di indicizzazione full-text asincrono (per impostazione predefinita, ogni 5 secondi).

Con il normale funzionamento di AEM, ad esempio il caricamento di risorse tramite l’interfaccia utente Web o l’assimilazione programmatica di risorse, AEM indicherà automaticamente e in modo incrementale il nuovo contenuto binario con l’indice full-text. Poiché la quantità di dati è incrementale e relativamente bassa (circa la quantità di dati che possono essere memorizzati nell’archivio in 5 secondi), AEM può eseguire l’estrazione full-text dai binari durante l’indicizzazione senza compromettere le prestazioni complessive del sistema.

#### Prerequisiti per l’utilizzo della preestrazione del testo {#prerequisites-to-using-text-pre-extraction}

* Verrà reindicizzato un indice di lucene che esegue l&#39;estrazione binaria full-text o distribuisce un nuovo indice che eseguirà i binari di indice full-text del contenuto esistente
* Il contenuto (file binari) da cui estrarre prima il testo deve trovarsi nella directory archivio
* Una finestra di manutenzione per generare il file CSV E per eseguire la reindicizzazione finale
* Versione quercia: 1.0.18+, 1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* Una cartella/condivisione del file system per memorizzare il testo estratto accessibile dalle istanze AEM di indicizzazione

   * La configurazione OSGi di preestrazione del testo richiede un percorso del file system per i file di testo estratti, per cui devono essere accessibili direttamente dall’istanza AEM (unità locale o condivisione file)

#### Come eseguire la preestrazione del testo {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***I comandi oak-run.jar descritti di seguito sono completamente enumerati in[https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>Il diagramma e i passaggi descritti qui di seguito spiegano e completano i passaggi tecnici di preestrazione del testo descritti nella documentazione Apache Oak.

![Flusso del processo di preestrazione del testo](assets/chlimage_1-139.png)

**Genera elenco di contenuti da pre-estrarre**

*Eseguire il passaggio 1(a-b) durante una finestra di manutenzione/un periodo di utilizzo basso, durante il quale il Node Store viene attraversato durante l&#39;operazione, che può comportare un carico significativo sul sistema.*

1 bis. Esegui `oak-run.jar --generate` per creare un elenco di nodi con testo preestratto.

1 ter. L’elenco dei nodi (1a) è memorizzato nel file system come file CSV

Tenete presente che l’intero archivio nodi viene attraversato (come specificato dai percorsi nel comando di esecuzione della query) ogni volta `--generate` che viene eseguito e viene creato un **nuovo** file CSV. Il file CSV **non** viene riutilizzato tra le esecuzioni discrete del processo di preestrazione del testo (passaggi 1 - 2).

**Pre-estrazione del testo nel file system**

*Il passaggio 2(a-c) può essere eseguito durante il normale funzionamento di AEM se interagisce solo con l’Archivio dati.*

2 bis. Esegui `oak-run.jar --tika` per preestrarre il testo per i nodi binari enumerati nel file CSV generato in (1b)

2 ter. Il processo avviato in (2a) accede direttamente ai nodi binari definiti nel CSV in Data Store ed estrae il testo.

2 quater.  Il testo estratto viene memorizzato nel file system in un formato assimilabile dal processo di reindicizzazione Oak (3a)

Il testo preestratto è identificato nel CSV dall’impronta digitale binaria. Se il file binario è lo stesso, lo stesso testo preestratto può essere utilizzato nelle istanze di AEM. Poiché AEM Publish è in genere un sottoinsieme di AEM Author, il testo preestratto da AEM Author può spesso essere utilizzato anche per reindirizzare AEM Publish (sempre che AEM Publish disponga dell&#39;accesso del file system ai file di testo estratti).

Il testo preestratto può essere aggiunto in modo incrementale nel tempo. La preestrazione del testo salta l&#39;estrazione per i binari precedentemente estratti, quindi è consigliabile mantenere il testo preestratto nel caso in cui la reindicizzazione debba ripetersi in futuro (supponendo che il contenuto estratto non sia troppo grande). In caso affermativo, valutate la compressione dei contenuti nel frattempo, poiché il testo viene compresso correttamente).

**Reindicizzare gli indici Oak, ottenendo il testo completo dai file di testo estratti**

*Eseguire nuovamente il reindicizzazione (passaggi 3a-b) durante un periodo di manutenzione/basso utilizzo durante l&#39;attraversamento del Node Store durante l&#39;operazione, che potrebbe causare un carico significativo sul sistema.*

3 bis. [Il nuovo indice](#how-to-re-index) degli indici Lucene viene richiamato in AEM

3 ter. La configurazione OSGi Apache Jackrabbit Oak DataStore PreExtedTextProvider Oak (configurata per puntare al testo estratto tramite un percorso del file system) istruisce Oak al testo full-text originato dai file estratti ed evita di colpire e elaborare direttamente i dati memorizzati nella directory archivio.

