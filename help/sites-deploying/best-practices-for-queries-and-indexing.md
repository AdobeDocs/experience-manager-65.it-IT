---
title: Best practice per query e indicizzazione
description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '4598'
ht-degree: 7%

---

# Best practice per query e indicizzazione{#best-practices-for-queries-and-indexing}

Oltre alla transizione a Oak nell’AEM 6, sono state apportate alcune modifiche importanti al modo in cui vengono gestite le query e gli indici. Sotto Jackrabbit 2, tutto il contenuto era indicizzato per impostazione predefinita e poteva essere interrogato liberamente. In Oak, gli indici devono essere creati manualmente sotto `oak:index` nodo. Una query può essere eseguita senza un indice, ma per i set di dati di grandi dimensioni verrà eseguita lentamente o verrà interrotta.

Questo articolo illustra quando creare indici e quando non sono necessari, trucchi per evitare di utilizzare le query quando non sono necessarie e suggerimenti per ottimizzare indici e query per ottenere le migliori prestazioni possibili.

Inoltre, leggi le [Documentazione Oak sulla scrittura di query e indici](/help/sites-deploying/queries-and-indexing.md). Oltre al fatto che gli indici sono un nuovo concetto nell’AEM 6, esistono differenze sintattiche nelle query Oak che devono essere prese in considerazione durante la migrazione del codice da una precedente installazione dell’AEM.

## Quando utilizzare le query {#when-to-use-queries}

### Struttura dell’archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, occorre tenere conto di diversi fattori, Ad esempio, controlli di accesso, localizzazione, componente ed ereditarietà delle proprietà di pagina.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la “fruibilità” del design di indicizzazione. In questo contesto, la navigabilità è la capacità di una tassonomia che consente l’accesso prevedibile al contenuto in base al suo percorso. In questo modo si otterrà un sistema più efficiente e più semplice da gestire rispetto a un sistema che richiede l&#39;esecuzione di più query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l’importanza dell’ordinamento. Nei casi in cui non è richiesto un ordinamento esplicito e sono previsti molti nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesto l’ordinamento, `nt:unstructured`, e `sling:OrderedFolder` sono più appropriati.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni più gravose su un sistema AEM, è consigliabile evitarle nei componenti. Spesso, l’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l’esecuzione di query durante il rendering dei componenti: **navigazione dei nodi** e **preacquisizione dei risultati**.

#### Navigazione dei nodi {#traversing-nodes}

Se l’archivio è progettato in modo tale da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera tali dati dai percorsi necessari può essere distribuito senza dover eseguire query per trovarli.

Un esempio potrebbe essere il rendering di contenuti che rientrano a una determinata categoria. Un approccio consiste nell’organizzare i contenuti con una proprietà di categoria su cui è possibile eseguire una query per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nello strutturare i contenuti in una tassonomia per categoria, in modo da poterli recuperare manualmente.

Ad esempio, se il contenuto viene memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

Il `/content/myUnstructuredContent/parentCategory/childCategory` Il nodo può essere semplicemente recuperato, i relativi nodi secondari possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, può essere più rapido attraversare l’archivio e raccogliere i nodi richiesti, anziché creare una query per restituire lo stesso set di risultati. In generale, occorre evitare le query laddove possibile.

#### Preacquisizione dei risultati {#prefetching-results}

A volte il contenuto o i requisiti relativi al componente non consentono l’utilizzo della navigazione dei nodi come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query richieste prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali per l’utente finale.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto cambi, la query può essere eseguita quando l’autore applica le impostazioni nella finestra di dialogo.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita secondo una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Dopodiché, i risultati possono essere scritti in una posizione condivisa nell’archivio. Tutti i componenti che necessitano di questi dati possono quindi richiamare i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

## Ottimizzazione query {#query-optimization}

Quando si esegue una query che non utilizza un indice, vengono registrati avvisi relativi all’attraversamento dei nodi. Se si tratta di una query che verrà eseguita spesso, crea un indice. Per determinare quale indice viene utilizzato da una determinata query, [Strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) è consigliato. Per ulteriori informazioni, la registrazione DEBUG può essere abilitata per le API di ricerca pertinenti.

>[!NOTE]
>
>Dopo aver modificato la definizione di un indice, è necessario ricrearlo (reindicizzarlo). A seconda delle dimensioni dell&#39;indice, il completamento dell&#39;operazione potrebbe richiedere del tempo.

Durante l’esecuzione di query complesse, possono verificarsi casi in cui la query viene suddivisa in più query più piccole e i dati vengono uniti tramite il codice dopo che il fatto è più performante. Per questi casi si raccomanda di confrontare le prestazioni dei due approcci per determinare quale opzione sarebbe migliore per il caso d’uso in questione.

L’AEM consente di scrivere le query in uno dei tre modi seguenti:

* Attraverso il [API QueryBuilder](/help/sites-developing/querybuilder-api.md) (consigliato)
* Utilizzo di XPath (consigliato)
* Utilizzo di SQL2

Anche se tutte le query vengono convertite in SQL2 prima di essere eseguite, il sovraccarico della conversione delle query è minimo e, di conseguenza, la principale preoccupazione quando si sceglie un linguaggio di query sarà la leggibilità e il livello di comfort dal team di sviluppo.

>[!NOTE]
>
>Quando si utilizza QueryBuilder, per impostazione predefinita viene determinato il conteggio dei risultati, più lento in Oak rispetto alle versioni precedenti di Jackrabbit. Per compensare questo, puoi utilizzare [parametro guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Strumento Spiega query {#the-explain-query-tool}

Come per qualsiasi linguaggio di query, il primo passaggio per ottimizzare una query consiste nel comprenderne la modalità di esecuzione. Per abilitare questa attività, puoi utilizzare [Strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) che fa parte del dashboard operazioni. Con questo strumento, è possibile collegare e spiegare una query. Viene visualizzato un avviso se la query causa problemi con un archivio di grandi dimensioni e con il runtime e gli indici utilizzati. Lo strumento può anche caricare un elenco di query lente e popolari che possono quindi essere spiegate e ottimizzate.

### Registrazione DEBUG per query {#debug-logging-for-queries}

Per ottenere ulteriori informazioni sulla scelta dell’indice da utilizzare da parte di Oak e sul modo in cui il motore di query esegue effettivamente una query, si consiglia di: **DEBUG** è possibile aggiungere la configurazione di registrazione per i seguenti pacchetti:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Assicurati di rimuovere questo logger al termine del debug della query. Tende a generare una grande quantità di attività e può eventualmente riempire il disco con i file di registro.

Per ulteriori informazioni, vedere [Documentazione sulla registrazione](/help/sites-deploying/configure-logging.md).

### Statistiche indice {#index-statistics}

Lucene registra un bean JMX che fornirà dettagli sul contenuto indicizzato, incluse le dimensioni e il numero di documenti presenti in ciascuno degli indici.

Puoi raggiungerlo accedendo alla console JMX all’indirizzo `https://server:port/system/console/jmx`

Dopo aver effettuato l’accesso alla console JMX, cerca **Statistiche indice Lucene** per trovarlo. Altre statistiche di indice sono disponibili nella sezione **IndexStats** MBean.

Per le statistiche delle query, osserva il codice MBean denominato **Statistiche query Oak**.

Se desideri esplorare gli indici utilizzando uno strumento come [Luke](https://code.google.com/archive/p/luke/), è necessario utilizzare la console Oak per scaricare l’indice dal `NodeStore` in una directory del file system. Per istruzioni su come eseguire questa operazione, leggere [Documentazione di Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Puoi anche estrarre gli indici nel sistema in formato JSON. A questo scopo, devi accedere `https://server:port/oak:index.tidy.-1.json`

### Limiti per le query {#query-limits}

**Durante lo sviluppo**

Imposta soglie basse per `oak.queryLimitInMemory` (ad esempio, 10000) e Oak. `queryLimitReads` (ad esempio, 5000) e ottimizzare la costosa query quando si preme un UnsupportedOperationException che indica &quot;La query legge più di x nodi...&quot;

Questo consente di evitare le query che richiedono molte risorse, ovvero che non sono supportate da alcun indice o da un indice a copertura ridotta. Ad esempio, una query che legge 1 milione di nodi porterebbe a un aumento dell’I/O e avrebbe un impatto negativo sulle prestazioni complessive dell’applicazione. Qualsiasi query che non riesce a causa di limiti superiori deve essere analizzata e ottimizzata.

#### **Post-distribuzione** {#post-deployment}

* Monitora i registri per le query che attivano l’attraversamento di nodi di grandi dimensioni o il consumo di memoria heap di grandi dimensioni: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizza la query per ridurre il numero di nodi attraversati

* Monitora i registri per le query che attivano un consumo elevato di memoria heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizza la query per ridurre il consumo di memoria heap

Per le versioni da AEM 6.0 a 6.2, è possibile regolare la soglia per l’attraversamento dei nodi tramite i parametri JVM nello script di avvio dell’AEM per evitare che le query di grandi dimensioni sovraccarichi l’ambiente.

I valori consigliati sono:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri precedenti sono OOTB preconfigurati e possono essere mantenuti tramite OSGi QueryEngineSettings.

Ulteriori informazioni sono disponibili su: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Suggerimenti per la creazione di indici efficienti {#tips-for-creating-efficient-indexes}

### È necessario creare un indice? {#should-i-create-an-index}

La prima domanda da porsi durante la creazione o l’ottimizzazione degli indici è se sono necessari per una determinata situazione. Se la query in questione verrà eseguita una sola volta o solo occasionalmente e in un momento non di picco per il sistema tramite un processo batch, potrebbe essere preferibile non creare alcun indice.

Dopo aver creato un indice, ogni volta che i dati indicizzati vengono aggiornati, anche l’indice deve essere aggiornato. Poiché questo comporta implicazioni in termini di prestazioni per il sistema, gli indici devono essere creati solo quando sono necessari.

Inoltre, gli indici sono utili solo se i dati contenuti all’interno dell’indice sono sufficientemente univoci da giustificarlo. Considera un indice in un libro e gli argomenti trattati. Quando si indicizza un set di argomenti in un testo, in genere sono presenti centinaia o migliaia di voci, che consentono di passare rapidamente a un sottoinsieme di pagine per trovare rapidamente le informazioni desiderate. Se tale indice avesse solo due o tre voci, ognuna delle quali indica diverse centinaia di pagine, l’indice non sarebbe utile. Lo stesso concetto si applica agli indici di database. Se sono presenti solo due valori univoci, l’indice non sarà utile. Detto questo, un indice può anche diventare troppo grande per essere utile. Per esaminare le statistiche dell’indice, vedi [Statistiche indice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) sopra.

### Indici Lucene o di proprietà? {#lucene-or-property-indexes}

Gli indici Lucene sono stati introdotti in Oak 1.0.9 e offrono alcune potenti ottimizzazioni rispetto agli indici di proprietà introdotti nel lancio iniziale dell’AEM 6. Quando decidi se utilizzare gli indici Lucene o gli indici di proprietà, prendi in considerazione quanto segue:

* Gli indici Lucene offrono molte più funzioni degli indici di proprietà. Ad esempio, un indice delle proprietà può indicizzare solo una singola proprietà, mentre un indice Lucene può includere molte. Per ulteriori informazioni su tutte le funzioni disponibili negli indici Lucene, consulta la [documentazione](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Gli indici Lucene sono asincroni. Questo offre un notevole miglioramento delle prestazioni, ma può anche indurre un ritardo tra la scrittura dei dati nell’archivio e l’aggiornamento dell’indice. Se è fondamentale che le query restituiscano risultati accurati al 100%, è necessario un indice delle proprietà.
* Poiché sono asincroni, gli indici Lucene non possono applicare vincoli di univocità. Se necessario, è necessario implementare un indice delle proprietà.

In generale, si consiglia di utilizzare gli indici Lucene a meno che non vi sia la necessità urgente di utilizzare gli indici di proprietà in modo da poter beneficiare di prestazioni e flessibilità più elevate.

### Indicizzazione Solr {#solr-indexing}

Per impostazione predefinita, l’AEM supporta anche l’indicizzazione Solr. Viene utilizzato per supportare la ricerca full-text, ma può anche essere utilizzato per supportare qualsiasi tipo di query JCR. Solr deve essere preso in considerazione quando le istanze AEM non hanno la capacità della CPU per gestire il numero di query necessarie in implementazioni che richiedono un uso intensivo della ricerca, come i siti web basati sulla ricerca con un numero elevato di utenti simultanei. In alternativa, Solr può essere implementato in un approccio basato su crawler per utilizzare alcune delle funzioni più avanzate della piattaforma.

Gli indici Solr possono essere configurati per l’esecuzione incorporata sul server AEM per gli ambienti di sviluppo oppure possono essere scaricati su un’istanza remota per migliorare la scalabilità della ricerca negli ambienti di produzione e di staging. L&#39;offload della ricerca migliora la scalabilità, ma introduce una latenza e per questo motivo non è consigliato a meno che non sia necessario. Per ulteriori informazioni su come configurare l&#39;integrazione Solr e creare indici Solr, vedere [Documentazione su query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Con l&#39;approccio di ricerca Solr integrata è possibile scaricare l&#39;indicizzazione su un server Solr. Se le funzioni più avanzate del server Solr vengono utilizzate tramite un approccio basato su crawler, è necessario un ulteriore lavoro di configurazione.

L’inconveniente di questo approccio è che, anche se per impostazione predefinita le query AEM rispettano gli ACL e quindi nascondono i risultati a cui un utente non ha accesso, l’esternalizzazione della ricerca a un server Solr non supporterà questa funzione. Se la ricerca deve essere esternalizzata in questo modo, è necessario prestare particolare attenzione affinché agli utenti non vengano presentati risultati che non dovrebbero vedere.

Potenziali casi d’uso in cui questo approccio può essere appropriato sono i casi in cui può essere necessario aggregare i dati di ricerca provenienti da più fonti. Ad esempio, puoi avere un sito ospitato sull’AEM e un secondo sito ospitato su una piattaforma di terze parti. Solr può essere configurato per eseguire la ricerca per indicizzazione del contenuto di entrambi i siti e memorizzarli in un indice aggregato. Questo consentirebbe ricerche intersito.

### Considerazioni sulla progettazione {#design-considerations}

Nella documentazione Oak per gli indici Lucene sono elencate diverse considerazioni da tenere in considerazione durante la progettazione degli indici:

* Se la query utilizza restrizioni di percorso diverse, utilizza `evaluatePathRestrictions`. Questo consente alla query di restituire il sottoinsieme di risultati nel percorso specificato e quindi di filtrarli in base alla query. In caso contrario, la query cerca tutti i risultati che corrispondono ai parametri di query nell’archivio e quindi li filtra in base al percorso.
* Se la query utilizza l&#39;ordinamento, impostare una definizione di proprietà esplicita per la proprietà ordinata e `ordered` a `true` per quello. Ciò consente di ordinare i risultati come tali nell’indice e di risparmiare su costose operazioni di ordinamento al momento dell’esecuzione della query.

* Inserisci solo il necessario nell’indice. L’aggiunta di funzioni o proprietà non necessarie causa la crescita dell’indice e rallenta le prestazioni.
* In un indice delle proprietà, l’utilizzo di un nome di proprietà univoco aiuterebbe a ridurre le dimensioni di un indice, ma per gli indici Lucene l’utilizzo di `nodeTypes` e `mixins` Per ottenere indici coesivi. Query di uno specifico `nodeType` o `mixin` sarà più performante rispetto alla query `nt:base`. Quando si utilizza questo approccio, definire `indexRules` per `nodeTypes` in questione.

* Se le query vengono eseguite solo in determinati percorsi, crea tali indici in tali percorsi. Non è necessario che gli indici risiedano nella directory principale dell’archivio.
* Utilizza un singolo indice quando tutte le proprietà in fase di indicizzazione sono correlate per consentire a Lucene di valutare il maggior numero possibile di restrizioni di proprietà in modo nativo. Inoltre, una query utilizzerà un solo indice, anche quando si esegue un join.

### CopyOnRead {#copyonread}

Nei casi in cui `NodeStore` è memorizzato in remoto, un&#39;opzione denominata `CopyOnRead` possono essere abilitati. L&#39;opzione consente di scrivere l&#39;indice remoto nel file system locale quando viene letto. Questo può aiutare a migliorare le prestazioni per le query che vengono spesso eseguite su questi indici remoti.

Questo può essere configurato nella console OSGi in **LuceneIndexProvider** ed è abilitato per impostazione predefinita a partire da Oak 1.0.13.

### Rimozione degli indici {#removing-indexes}

Quando si rimuove un indice, si consiglia sempre di disattivarlo temporaneamente impostando il `type` proprietà a `disabled` ed esegui dei test per garantire il corretto funzionamento dell’applicazione prima di eliminarla effettivamente. Un indice non viene aggiornato se disabilitato, pertanto potrebbe non avere il contenuto corretto se viene riabilitato e potrebbe essere necessario reindicizzarlo.

Dopo aver rimosso un indice di proprietà in un&#39;istanza TarMK, è necessario eseguire la compattazione per recuperare lo spazio su disco in uso. Per gli indici Lucene, il contenuto effettivo dell’indice si trova nel BlobStore, pertanto sarebbe necessaria una raccolta di oggetti inattivi dell’archivio dati.

Quando si rimuove un indice in un’istanza MongoDB, il costo dell’eliminazione è proporzionale al numero di nodi nell’indice. Poiché l’eliminazione di un indice di grandi dimensioni può causare problemi, l’approccio consigliato consiste nel disattivare l’indice e eliminarlo solo durante una finestra di manutenzione, utilizzando uno strumento come **oak-mongo.js**. Tieni presente che questo approccio non deve essere utilizzato per il contenuto dei nodi regolari, in quanto può introdurre incoerenze nei dati.

>[!NOTE]
>
>Per ulteriori informazioni su oak-mongo.js, consulta la sezione [Sezione Strumenti della riga di comando](https://jackrabbit.apache.org/oak/docs/command_line.html) della documentazione di Oak.

### Scheda di riferimento rapido per le query JCR {#jcrquerycheatsheet}

Per supportare la creazione di query JCR e le definizioni degli indici efficienti, la [Scheda di riferimento rapido per le query JCR](assets/JCR_query_cheatsheet-v1.1.pdf) è disponibile per il download e l’utilizzo come riferimento durante lo sviluppo. Contiene query di esempio per QueryBuilder, XPath e SQL-2 comprendendo scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre consigli su come creare o personalizzare gli indici Oak. Il contenuto di questa Scheda di riferimento rapido si applica a AEM 6.5 e AEM as a Cloud Service.

## Reindicizzazione {#re-indexing}

Questa sezione illustra **solo** motivi accettabili per reindicizzare gli indici Oak.

Al di fuori dei motivi descritti di seguito, l’avvio delle reindici degli indici Oak non **non** modificare il comportamento o risolvere i problemi e aumentare inutilmente i carichi per l’AEM.

La reindicizzazione degli indici Oak deve essere evitata a meno che non sia spiegata da un motivo nelle tabelle seguenti.

>[!NOTE]
>
>Prima di consultare le tabelle seguenti per determinare se la reindicizzazione è utile, **sempre** verifica:
>
>* la query è corretta
>* la query viene risolta nell’indice previsto (utilizzando [Spiega query](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* processo di indicizzazione completato
>

### Modifiche alla configurazione dell’indice Oak {#oak-index-configuration-changes}

Le uniche condizioni non errate accettabili per la reindicizzazione degli indici Oak sono se la configurazione di un indice Oak è cambiata.

*La reindicizzazione deve sempre essere affrontata tenendo in debita considerazione il suo impatto sulle prestazioni complessive dell’AEM ed eseguita durante i periodi di bassa attività o di finestre di manutenzione.*

Di seguito sono riportati i possibili problemi relativi alle risoluzioni:

* [Modifica definizione indice proprietà](#property-index-definition-change)
* [Modifica definizione indice Lucene](#lucene-index-definition-change)

#### Modifica definizione indice proprietà {#property-index-definition-change}

* Si applica per/se:

   * Tutte le versioni Oak
   * Solo [indici di proprietà](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomi:

   * Nodi esistenti prima dell’aggiornamento della definizione dell’indice delle proprietà mancanti nei risultati

* Come verificare:

   * Determina se i nodi mancanti sono stati creati/modificati prima della distribuzione della definizione di indice aggiornata.
   * Verificare la `jcr:created` o `jcr:lastModified` proprietà di eventuali nodi mancanti rispetto all’ora di modifica dell’indice

* Come risolvere:

   * [Reindicizza](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) l’indice di lucene
   * In alternativa, toccare (eseguire un’operazione di scrittura benigna) i nodi mancanti

      * Richiede contatti manuali o codice personalizzato
      * Richiede che il set di nodi mancanti sia noto
      * Richiede la modifica di qualsiasi proprietà sul nodo

#### Modifica definizione indice Lucene {#lucene-index-definition-change}

* Si applica per/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti
   * I risultati della query non riflettono il comportamento previsto della definizione dell’indice
   * Il piano di query non segnala l’output previsto in base alla definizione dell’indice

* Come verificare:

   * Verificare che la definizione dell&#39;indice sia stata modificata utilizzando il metodo JMX Mbean (LuceneIndex) delle statistiche dell&#39;indice di Lucene `diffStoredIndexDefinition`.

* Come risolvere:

   * Versioni Oak precedenti alla versione 1.6:

      * [Reindicizza](#how-to-re-index) l’indice di lucene

   * Oak versioni 1.6+

      * Se il contenuto esistente non è interessato dalle modifiche, è necessario solo un aggiornamento

         * [Aggiorna](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) l&#39;indice lucene impostando [oak:queryIndexDefinition]@refresh=true

      * Altrimenti, [reindicizzare](#how-to-re-index) l’indice di lucene

         * Nota: lo stato dell’indice dall’ultima reindicizzazione valida (o indicizzazione iniziale) viene utilizzato fino a quando non viene attivata una nuova reindicizzazione

### Errori e situazioni eccezionali {#erring-and-exceptional-situations}

La tabella seguente descrive l’unico errore accettabile e le situazioni eccezionali in cui la reindicizzazione degli indici Oak risolve il problema.

Se si verifica un problema relativo all’AEM che non soddisfa i criteri descritti di seguito, **non** reindicizza eventuali indici, in quanto non risolverà il problema.

Di seguito sono riportati i possibili problemi relativi alle risoluzioni:

* [Manca il binario dell&#39;indice Lucene](#lucene-index-binary-is-missing)
* [Il file binario dell&#39;indice di Lucene è danneggiato](#lucene-index-binary-is-corrupt)

#### Manca il binario dell&#39;indice Lucene {#lucene-index-binary-is-missing}

* Si applica per/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti

* Come verificare:

   * Il file di log degli errori contiene un&#39;eccezione che indica che manca un binario dell&#39;indice Lucene

* Come risolvere:

   * Eseguire una verifica dell’archivio di attraversamento, ad esempio:

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     l’attraversamento dell’archivio determina se mancano altri file binari (oltre ai file lucene)

   * Se mancano dati binari diversi dagli indici Lucene, eseguire il ripristino dal backup
   * Altrimenti, [reindicizzare](#how-to-re-index) *tutto* indici lucene
   * Nota:

     Questa condizione è indicativa di un archivio dati configurato in modo errato che potrebbe causare la perdita di dati binari ANY (ad esempio, binari di risorse).

     In questo caso, ripristina l’ultima versione valida nota dell’archivio per recuperare tutti i file binari mancanti.

#### Il file binario dell&#39;indice di Lucene è danneggiato {#lucene-index-binary-is-corrupt}

* Si applica per/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti

* Come verificare:

   * Il `AsyncIndexUpdate` (ogni cinque secondi) avrà esito negativo con un’eccezione nel registro degli errori:

     `...a Lucene index file is corrupt...`

* Come risolvere:

   * Rimuovi la copia locale dell’indice Lucene

      1. Interrompere l’AEM
      1. Elimina la copia locale dell’indice Lucene in `crx-quickstart/repository/index`
      1. Riavvia AEM

   * Se questo non risolve il problema, e `AsyncIndexUpdate` le eccezioni persistono:

      1. [Reindicizza](#how-to-re-index) l&#39;indice di errore
      1. File anche [Supporto Adobe](https://helpx.adobe.com/support.html) ticket

### Reindicizzare {#how-to-re-index}

>[!NOTE]
>
>AEM 6.5, [oak-run.jar è l’UNICO metodo supportato](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) per la reindicizzazione su archivi MongoMK o RDBMK.

#### Reindicizzazione degli indici delle proprietà {#re-indexing-property-indexes}

* Utilizzare [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) per reindicizzare l&#39;indice delle proprietà
* Impostare la proprietà async-reindex su true nell&#39;indice della proprietà

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindicizzare l’indice delle proprietà in modo asincrono utilizzando la console web tramite **PropertyIndexAsyncReindex** MBean;

  ad esempio,

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindicizzazione degli indici della proprietà Lucene {#re-indexing-lucene-property-indexes}

* Utilizzare [oak-run.jar per reindicizzare](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) l&#39;indice della proprietà Lucene.
* Impostare la proprietà async-reindex su true nell&#39;indice della proprietà Lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sezione precedente riepiloga e inquadra la guida alla reindicizzazione Oak dalla [Documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) nell&#39;ambito dell&#39;AEM.

### Pre-estrazione del testo dei dati binari {#text-pre-extraction-of-binaries}

La pre-estrazione del testo è il processo di estrazione ed elaborazione del testo dai dati binari, direttamente dall’archivio dati tramite un processo isolato ed esponendo direttamente il testo estratto a successive re/indicizzazioni degli indici Oak.

* La pre-estrazione del testo Oak è consigliata per la re/indicizzazione degli indici Lucene in archivi con grandi volumi di file (binari) contenenti testo estraibile (ad esempio, PDF, documenti Word, PPT, TXT e così via) idonei per la ricerca full-text tramite indici Oak distribuiti; ad esempio, `/oak:index/damAssetLucene`.
* La pre-estrazione del testo offre vantaggi solo per la re/indicizzazione degli indici Lucene e NOT Oak, in quanto gli indici di proprietà non estraggono il testo dai binari.
* La pre-estrazione del testo ha un forte impatto positivo quando la reindicizzazione full-text di file binari contenenti testo (PDF, Doc, TXT e così via), mentre un archivio di immagini non presenta le stesse efficienze poiché le immagini non contengono testo estraibile.
* La pre-estrazione del testo esegue l’estrazione di testo completo relativo alla ricerca in modo molto efficiente e lo espone al processo di re/indicizzazione Oak in modo molto efficiente.

#### Quando può essere utilizzata la pre-estrazione del testo? {#when-can-text-pre-extraction-be-used}

Reindicizzazione di un **esistente** indice lucene con estrazione binaria abilitata

* Reindicizzazione dell’elaborazione **tutto** contenuto candidato nell’archivio; quando i dati binari da cui estrarre il testo completo sono numerosi o complessi, l’AEM è soggetto a un onere di calcolo maggiore per eseguire l’estrazione del testo completo. La pre-estrazione del testo sposta il &quot;lavoro computazionalmente costoso&quot; dell’estrazione del testo in un processo isolato che accede direttamente all’archivio dati dell’AEM, evitando il sovraccarico e il conflitto di risorse nell’AEM.

Sostenere l&#39;implementazione di un **nuovo** indice Lucene per AEM con estrazione binaria abilitata

* Quando un nuovo indice (con estrazione binaria abilitata) viene distribuito in AEM, Oak indicizza automaticamente tutto il contenuto candidato alla successiva esecuzione dell’indice full-text asincrono. Per le stesse ragioni descritte nella reindicizzazione di cui sopra, ciò può comportare un carico eccessivo sull’AEM.

#### Quando NON è possibile utilizzare la pre-estrazione del testo? {#when-can-text-pre-extraction-not-be-used}

La pre-estrazione del testo non può essere utilizzata per i nuovi contenuti aggiunti all’archivio, né è necessaria.

Il nuovo contenuto aggiunto all’archivio viene indicizzato naturalmente e in modo incrementale dal processo di indicizzazione full-text asincrono (per impostazione predefinita, ogni 5 secondi).

In condizioni di normale funzionamento dell’AEM, ad esempio in caso di caricamento di risorse tramite l’interfaccia web o di inserimento programmatico di risorse, l’AEM indicizzerà in modo automatico e incrementale il nuovo contenuto binario. Poiché la quantità di dati è incrementale e relativamente piccola (approssimativamente la quantità di dati che può essere mantenuta nell’archivio in 5 secondi), l’AEM può eseguire l’estrazione full-text dai dati binari durante l’indicizzazione senza influire sulle prestazioni complessive del sistema.

#### Prerequisiti per l’utilizzo della pre-estrazione del testo {#prerequisites-to-using-text-pre-extraction}

* Reindicizzazione di un indice Lucene che esegue l&#39;estrazione binaria full-text o distribuzione di un nuovo indice che indicizzerà i file binari full-text del contenuto esistente
* Il contenuto (binari) da cui estrarre il testo in anteprima deve trovarsi nell’archivio
* Una finestra di manutenzione per generare il file CSV E per eseguire la reindicizzazione finale
* Oak versione: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versione 1.7.4+
* Una cartella/condivisione del file system per memorizzare il testo estratto accessibile dalle istanze AEM di indicizzazione

   * La configurazione OSGi di pre-estrazione del testo richiede un percorso del file system per i file di testo estratti, quindi devono essere accessibili direttamente dall’istanza AEM (unità locale o montaggio con condivisione file)

#### Come eseguire la pre-estrazione del testo {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***I comandi oak-run.jar descritti di seguito sono completamente enumerati in [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>Il diagramma precedente e i passaggi riportati di seguito spiegano e integrano i passaggi tecnici del testo pre-estrazione descritti nella documentazione di Apache Oak.

![Flusso processo di pre-estrazione testo](assets/chlimage_1-139.png)

**Genera elenco di contenuti da pre-estrarre**

*Eseguire il passaggio 1(a-b) durante un intervallo di manutenzione/periodo di utilizzo ridotto durante lo spostamento dell&#39;archivio nodi durante questa operazione, che può causare un carico significativo sul sistema.*

1a. Esegui `oak-run.jar --generate` per creare un elenco di nodi in cui verrà preestratto il testo.

1b. L&#39;elenco dei nodi (1a) viene archiviato nel file system come file CSV

L’intero archivio nodi viene attraversato ogni volta (come specificato dai percorsi nel comando oak-run ) `--generate` viene eseguito, e **nuovo** Viene creato il file CSV. Il file CSV è **non** riutilizzato tra esecuzioni discrete del processo di pre-estrazione del testo (passaggi 1-2).

**Pre-estrarre il testo nel file system**

*La fase 2(a-c) può essere eseguita durante il normale funzionamento dell’AEM se interagisce solo con l’archivio dati.*

2a. Esegui `oak-run.jar --tika` per preestrarre il testo per i nodi binari enumerati nel file CSV generato in (1b)

2b. Il processo avviato in (2a) accede direttamente ai nodi binari definiti nel file CSV in Data Store ed estrae il testo.

2 quater. Il testo estratto viene memorizzato nel file system in un formato che può essere acquisito dal processo di reindicizzazione Oak (3a)

Il testo pre-estratto viene identificato nel file CSV dall’impronta digitale binaria. Se il file binario è lo stesso, è possibile utilizzare lo stesso testo pre-estratto in tutte le istanze AEM. Poiché la pubblicazione AEM è in genere un sottoinsieme di creazione AEM, il testo pre-estratto dall’autore AEM può spesso essere utilizzato anche per reindicizzare la pubblicazione AEM (supponendo che la pubblicazione AEM abbia accesso al file di testo estratto dal file system).

Il testo pre-estratto può essere aggiunto in modo incrementale a nel tempo. La pre-estrazione del testo salta l’estrazione per i file binari estratti in precedenza, pertanto è consigliabile mantenere il testo pre-estratto nel caso in cui la reindicizzazione debba verificarsi nuovamente in futuro (supponendo che il contenuto estratto non sia eccessivamente grande. In caso affermativo, valutare la compressione del contenuto nel frattempo, poiché il testo viene compresso correttamente.

**Reindicizza indici Oak, ricerca full-text da file di testo estratto**

*Eseguire la reindicizzazione (passaggi 3a-b) durante un periodo di manutenzione/basso utilizzo mentre l’archivio nodi viene attraversato durante questa operazione, che può comportare un carico significativo sul sistema.*

3a. [Reindicizza](#how-to-re-index) degli indici Lucene viene richiamato nell’AEM.

3b. La configurazione OSGi di Apache Jackrabbit Oak DataStore PreExtractedTextProvider (configurata per puntare al testo estratto tramite un percorso del file system) indica a Oak il testo full-text di origine dai file estratti ed evita di colpire ed elaborare direttamente i dati memorizzati nell’archivio.
