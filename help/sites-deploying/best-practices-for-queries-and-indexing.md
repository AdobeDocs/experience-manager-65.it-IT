---
title: Best practice per query e indicizzazione
description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '4520'
ht-degree: 5%

---

# Best practice per query e indicizzazione{#best-practices-for-queries-and-indexing}

Oltre alla transizione ad Oak nell’AEM 6, sono state apportate alcune modifiche importanti al modo in cui vengono gestite le query e gli indici. Sotto Jackrabbit 2, tutto il contenuto era indicizzato per impostazione predefinita e poteva essere interrogato liberamente. In Oak, gli indici devono essere creati manualmente sotto il nodo `oak:index`. Una query può essere eseguita senza un indice, ma per i set di dati di grandi dimensioni verrà eseguita lentamente o verrà interrotta.

Questo articolo illustra quando creare indici e quando non sono necessari, trucchi per evitare di utilizzare le query quando non sono necessarie e suggerimenti per ottimizzare indici e query per ottenere le migliori prestazioni possibili.

Inoltre, assicurati di leggere la [documentazione di Oak sulla scrittura di query e indici](/help/sites-deploying/queries-and-indexing.md). Oltre al fatto che gli indici sono un nuovo concetto nell’AEM 6, esistono differenze sintattiche nelle query Oak che devono essere prese in considerazione durante la migrazione del codice da una precedente installazione AEM.

## Quando utilizzare le query {#when-to-use-queries}

### Struttura dell’archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, occorre tenere conto di diversi fattori, Ad esempio, controlli di accesso, localizzazione, componente ed ereditarietà delle proprietà di pagina.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la “fruibilità” del design di indicizzazione. In questo contesto, la navigabilità è la capacità di una tassonomia che consente l’accesso prevedibile al contenuto in base al suo percorso. In questo modo si otterrà un sistema più efficiente e più semplice da gestire rispetto a un sistema che richiede l&#39;esecuzione di più query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l’importanza dell’ordinamento. Nei casi in cui non è richiesto un ordinamento esplicito e sono previsti molti nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesto l&#39;ordinamento, `nt:unstructured` e `sling:OrderedFolder` sono più appropriati.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni più gravose su un sistema AEM, è consigliabile evitarle nei componenti. Spesso, l’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l&#39;esecuzione di query durante il rendering dei componenti: **navigazione dei nodi** e **preacquisizione dei risultati**.

#### Navigazione dei nodi {#traversing-nodes}

Se l’archivio è progettato in modo tale da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera tali dati dai percorsi necessari può essere distribuito senza dover eseguire query per trovarli.

Un esempio potrebbe essere il rendering di contenuti che rientrano a una determinata categoria. Un approccio consiste nell’organizzare i contenuti con una proprietà di categoria su cui è possibile eseguire una query per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nello strutturare i contenuti in una tassonomia per categoria, in modo da poterli recuperare manualmente.

Ad esempio, se il contenuto viene memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

Il nodo `/content/myUnstructuredContent/parentCategory/childCategory` può essere semplicemente recuperato, i relativi nodi secondari possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, può essere più rapido attraversare l’archivio e raccogliere i nodi richiesti, anziché creare una query per restituire lo stesso set di risultati. In generale, occorre evitare le query laddove possibile.

#### Preacquisizione dei risultati {#prefetching-results}

A volte il contenuto o i requisiti relativi al componente non consentono l’utilizzo della navigazione dei nodi come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query richieste prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali per l’utente finale.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto cambi, la query può essere eseguita quando l’autore applica le impostazioni nella finestra di dialogo.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita secondo una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Dopodiché, i risultati possono essere scritti in una posizione condivisa nell’archivio. Tutti i componenti che necessitano di questi dati possono quindi richiamare i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

## Ottimizzazione query {#query-optimization}

Quando si esegue una query che non utilizza un indice, vengono registrati avvisi relativi all’attraversamento dei nodi. Se si tratta di una query che verrà eseguita spesso, crea un indice. Per determinare quale indice utilizza una determinata query, si consiglia lo strumento [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query). Per ulteriori informazioni, la registrazione DEBUG può essere abilitata per le API di ricerca pertinenti.

>[!NOTE]
>
>Dopo aver modificato la definizione di un indice, è necessario ricrearlo (reindicizzarlo). A seconda delle dimensioni dell&#39;indice, il completamento dell&#39;operazione potrebbe richiedere del tempo.

Durante l’esecuzione di query complesse, possono verificarsi casi in cui la query viene suddivisa in più query più piccole e i dati vengono uniti tramite il codice dopo che il fatto è più performante. Per questi casi si raccomanda di confrontare le prestazioni dei due approcci per determinare quale opzione sarebbe migliore per il caso d’uso in questione.

L’AEM consente di scrivere le query in uno dei tre modi seguenti:

* Tramite le [API QueryBuilder](/help/sites-developing/querybuilder-api.md) (consigliato)
* Utilizzo di XPath (consigliato)
* Utilizzo di SQL2

Anche se tutte le query vengono convertite in SQL2 prima di essere eseguite, il sovraccarico della conversione delle query è minimo e, di conseguenza, la principale preoccupazione quando si sceglie un linguaggio di query sarà la leggibilità e il livello di comfort dal team di sviluppo.

>[!NOTE]
>
>Quando si utilizza QueryBuilder, per impostazione predefinita viene determinato il conteggio dei risultati, più lento in Oak rispetto alle versioni precedenti di Jackrabbit. Per compensare questa situazione, è possibile utilizzare il parametro [guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Strumento Spiega query {#the-explain-query-tool}

Come per qualsiasi linguaggio di query, il primo passaggio per ottimizzare una query consiste nel comprenderne la modalità di esecuzione. Per abilitare questa attività, è possibile utilizzare lo strumento [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) che fa parte del dashboard operazioni. Con questo strumento, è possibile collegare e spiegare una query. Viene visualizzato un avviso se la query causa problemi con un archivio di grandi dimensioni e con il runtime e gli indici utilizzati. Lo strumento può anche caricare un elenco di query lente e popolari che possono quindi essere spiegate e ottimizzate.

### Registrazione DEBUG per query {#debug-logging-for-queries}

Per ulteriori informazioni sulla scelta dell&#39;indice da utilizzare da parte di Oak e sull&#39;esecuzione effettiva di una query da parte del motore di query, è possibile aggiungere una configurazione di registrazione **DEBUG** per i pacchetti seguenti:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Assicurati di rimuovere questo logger al termine del debug della query. Tende a generare una grande quantità di attività e può eventualmente riempire il disco con i file di registro.

Per ulteriori informazioni su come eseguire questa operazione, consulta la [documentazione sulla registrazione](/help/sites-deploying/configure-logging.md).

### Statistiche indice {#index-statistics}

Lucene registra un bean JMX che fornirà dettagli sul contenuto indicizzato, incluse le dimensioni e il numero di documenti presenti in ciascuno degli indici.

È possibile raggiungerlo accedendo alla console JMX all&#39;indirizzo `https://server:port/system/console/jmx`

Dopo aver effettuato l&#39;accesso alla console JMX, eseguire una ricerca per **Statistiche indice di Lucene** per individuarlo. Altre statistiche di indice sono disponibili in **IndexStats** MBean.

Per le statistiche sulle query, controllare il codice MBean denominato **Statistiche query Oak**.

Se desideri esplorare gli indici utilizzando uno strumento come [Luca](https://code.google.com/archive/p/luke/), devi utilizzare la console Oak per scaricare l&#39;indice da `NodeStore` in una directory del file system. Per istruzioni su come eseguire questa operazione, consulta la [documentazione Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Puoi anche estrarre gli indici nel sistema in formato JSON. A questo scopo, devi accedere a `https://server:port/oak:index.tidy.-1.json`

### Limiti per le query {#query-limits}

**Durante lo sviluppo**

Impostare soglie basse per `oak.queryLimitInMemory` (ad esempio, 10000) e Oak. `queryLimitReads` (ad esempio, 5000) e ottimizza la costosa query quando si preme un UnsupportedOperationException che indica &quot;La query ha letto più di x nodi...&quot;

Questo consente di evitare le query che richiedono molte risorse, ovvero che non sono supportate da alcun indice o da un indice a copertura ridotta. Ad esempio, una query che legge 1 milione di nodi porterebbe a un aumento dell’I/O e avrebbe un impatto negativo sulle prestazioni complessive dell’applicazione. Qualsiasi query che non riesce a causa di limiti superiori deve essere analizzata e ottimizzata.

#### **Distribuzione-Post** {#post-deployment}

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

In AEM 6.3, i due parametri precedenti sono preconfigurati e possono essere mantenuti tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Suggerimenti per la creazione di indici efficienti {#tips-for-creating-efficient-indexes}

### È necessario creare un indice? {#should-i-create-an-index}

La prima domanda da porsi durante la creazione o l’ottimizzazione degli indici è se sono necessari per una determinata situazione. Se la query in questione verrà eseguita una sola volta o solo occasionalmente e in un momento non di picco per il sistema tramite un processo batch, potrebbe essere preferibile non creare alcun indice.

Dopo aver creato un indice, ogni volta che i dati indicizzati vengono aggiornati, anche l’indice deve essere aggiornato. Poiché questo comporta implicazioni in termini di prestazioni per il sistema, gli indici devono essere creati solo quando sono necessari.

Inoltre, gli indici sono utili solo se i dati contenuti all’interno dell’indice sono sufficientemente univoci da giustificarlo. Considera un indice in un libro e gli argomenti trattati. Quando si indicizza un set di argomenti in un testo, in genere sono presenti centinaia o migliaia di voci, che consentono di passare rapidamente a un sottoinsieme di pagine per trovare rapidamente le informazioni desiderate. Se tale indice avesse solo due o tre voci, ognuna delle quali indica diverse centinaia di pagine, l’indice non sarebbe utile. Lo stesso concetto si applica agli indici di database. Se sono presenti solo due valori univoci, l’indice non sarà utile. Detto questo, un indice può anche diventare troppo grande per essere utile. Per esaminare le statistiche dell&#39;indice, vedere [Statistiche indice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics).

### Indici Lucene o di proprietà? {#lucene-or-property-indexes}

Gli indici Lucene sono stati introdotti in Oak 1.0.9 e offrono alcune potenti ottimizzazioni rispetto agli indici delle proprietà introdotti nel lancio iniziale dell’AEM 6. Quando decidi se utilizzare gli indici Lucene o gli indici di proprietà, prendi in considerazione quanto segue:

* Gli indici Lucene offrono molte più funzioni degli indici di proprietà. Ad esempio, un indice delle proprietà può indicizzare solo una singola proprietà, mentre un indice Lucene può includere molte. Per ulteriori informazioni su tutte le funzionalità disponibili negli indici Lucene, consulta la [documentazione](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Gli indici Lucene sono asincroni. Questo offre un notevole miglioramento delle prestazioni, ma può anche indurre un ritardo tra la scrittura dei dati nell’archivio e l’aggiornamento dell’indice. Se è fondamentale che le query restituiscano risultati accurati al 100%, è necessario un indice delle proprietà.
* Poiché sono asincroni, gli indici Lucene non possono applicare vincoli di univocità. Se necessario, è necessario implementare un indice delle proprietà.

In generale, si consiglia di utilizzare gli indici Lucene a meno che non vi sia la necessità urgente di utilizzare gli indici di proprietà in modo da poter beneficiare di prestazioni e flessibilità più elevate.

### Indicizzazione Solr {#solr-indexing}

Per impostazione predefinita, l’AEM supporta anche l’indicizzazione Solr. Viene utilizzato per supportare la ricerca full-text, ma può anche essere utilizzato per supportare qualsiasi tipo di query JCR. Solr deve essere preso in considerazione quando le istanze AEM non hanno la capacità della CPU per gestire il numero di query necessarie in implementazioni che richiedono un uso intensivo della ricerca, come i siti web basati sulla ricerca con un numero elevato di utenti simultanei. In alternativa, Solr può essere implementato in un approccio basato su crawler per utilizzare alcune delle funzioni più avanzate della piattaforma.

Gli indici Solr possono essere configurati per l’esecuzione incorporata sul server AEM per gli ambienti di sviluppo oppure possono essere scaricati su un’istanza remota per migliorare la scalabilità della ricerca negli ambienti di produzione e di staging. L&#39;offload della ricerca migliora la scalabilità, ma introduce una latenza e per questo motivo non è consigliato a meno che non sia necessario. Per ulteriori informazioni su come configurare l&#39;integrazione Solr e creare indici Solr, vedere la [documentazione relativa alle query e all&#39;indicizzazione di Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Con l&#39;approccio di ricerca Solr integrata è possibile scaricare l&#39;indicizzazione su un server Solr. Se le funzioni più avanzate del server Solr vengono utilizzate tramite un approccio basato su crawler, è necessario un ulteriore lavoro di configurazione.

L’inconveniente di questo approccio è che, anche se per impostazione predefinita le query AEM rispettano gli ACL e quindi nascondono i risultati a cui un utente non ha accesso, l’esternalizzazione della ricerca a un server Solr non supporterà questa funzione. Se la ricerca deve essere esternalizzata in questo modo, è necessario prestare particolare attenzione affinché agli utenti non vengano presentati risultati che non dovrebbero vedere.

Potenziali casi d’uso in cui questo approccio può essere appropriato sono i casi in cui può essere necessario aggregare i dati di ricerca provenienti da più fonti. Ad esempio, puoi avere un sito ospitato sull’AEM e un secondo sito ospitato su una piattaforma di terze parti. Solr può essere configurato per eseguire la ricerca per indicizzazione del contenuto di entrambi i siti e memorizzarli in un indice aggregato. Questo consentirebbe ricerche intersito.

### Considerazioni sulla progettazione {#design-considerations}

Nella documentazione di Oak per gli indici Lucene sono elencate diverse considerazioni da tenere in considerazione durante la progettazione degli indici:

* Se la query utilizza restrizioni di percorso diverse, utilizzare `evaluatePathRestrictions`. Questo consente alla query di restituire il sottoinsieme di risultati nel percorso specificato e quindi di filtrarli in base alla query. In caso contrario, la query cerca tutti i risultati che corrispondono ai parametri di query nell’archivio e quindi li filtra in base al percorso.
* Se la query utilizza l&#39;ordinamento, impostare una definizione di proprietà esplicita per la proprietà ordinata e impostare `ordered` su `true`. Ciò consente di ordinare i risultati come tali nell’indice e di risparmiare su costose operazioni di ordinamento al momento dell’esecuzione della query.

* Inserisci solo il necessario nell’indice. L’aggiunta di funzioni o proprietà non necessarie causa la crescita dell’indice e rallenta le prestazioni.
* In un indice di proprietà, l&#39;utilizzo di un nome di proprietà univoco contribuirebbe a ridurre la dimensione di un indice, ma per gli indici Lucene è necessario utilizzare `nodeTypes` e `mixins` per ottenere indici coesivi. L&#39;esecuzione di query su un `nodeType` o un `mixin` specifico sarà più efficiente dell&#39;esecuzione di query su `nt:base`. Quando si utilizza questo approccio, definire `indexRules` per `nodeTypes` in questione.

* Se le query vengono eseguite solo in determinati percorsi, crea tali indici in tali percorsi. Non è necessario che gli indici risiedano nella directory principale dell’archivio.
* Utilizza un singolo indice quando tutte le proprietà in fase di indicizzazione sono correlate per consentire a Lucene di valutare il maggior numero possibile di restrizioni di proprietà in modo nativo. Inoltre, una query utilizzerà un solo indice, anche quando si esegue un join.

### CopyOnRead {#copyonread}

Nei casi in cui `NodeStore` è archiviato in remoto, è possibile abilitare un&#39;opzione denominata `CopyOnRead`. L&#39;opzione consente di scrivere l&#39;indice remoto nel file system locale quando viene letto. Questo può aiutare a migliorare le prestazioni per le query che vengono spesso eseguite su questi indici remoti.

Può essere configurato nella console OSGi nel servizio **LuceneIndexProvider** ed è abilitato per impostazione predefinita a partire da Oak 1.0.13.

### Rimozione degli indici {#removing-indexes}

Durante la rimozione di un indice, è sempre consigliabile disattivare temporaneamente l&#39;indice impostando la proprietà `type` su `disabled` ed eseguire test per verificare che l&#39;applicazione funzioni correttamente prima di eliminarlo. Un indice non viene aggiornato se disabilitato, pertanto potrebbe non avere il contenuto corretto se viene riabilitato e potrebbe essere necessario reindicizzarlo.

Dopo aver rimosso un indice di proprietà in un&#39;istanza TarMK, è necessario eseguire la compattazione per recuperare lo spazio su disco in uso. Per gli indici Lucene, il contenuto effettivo dell’indice si trova nel BlobStore, pertanto sarebbe necessaria una raccolta di oggetti inattivi dell’archivio dati.

Quando si rimuove un indice in un’istanza MongoDB, il costo dell’eliminazione è proporzionale al numero di nodi nell’indice. Poiché l&#39;eliminazione di un indice di grandi dimensioni può causare problemi, si consiglia di disabilitare l&#39;indice ed eliminarlo solo durante una finestra di manutenzione, utilizzando uno strumento come **oak-mongo.js**. Tieni presente che questo approccio non deve essere utilizzato per il contenuto dei nodi regolari, in quanto può introdurre incoerenze nei dati.

>[!NOTE]
>
>Per ulteriori informazioni su oak-mongo.js, consulta la [sezione Strumenti da riga di comando](https://jackrabbit.apache.org/oak/docs/command_line.html) della documentazione di Oak.

### Scheda di riferimento rapido per le query JCR {#jcrquerycheatsheet}

Per supportare la creazione di query JCR e le definizioni degli indici efficienti, la [Scheda di riferimento rapido per le query JCR](assets/JCR_query_cheatsheet-v1.1.pdf) è disponibile per il download e l&#39;utilizzo come riferimento durante lo sviluppo. Contiene query di esempio per QueryBuilder, XPath e SQL-2 comprendendo scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre consigli su come creare o personalizzare gli indici Oak. Il contenuto di questa Scheda di riferimento rapido si applica a AEM 6.5 e AEM as a Cloud Service.

## Reindicizzazione {#re-indexing}

Questa sezione descrive i **soli** motivi accettabili per reindicizzare gli indici Oak.

Al di fuori dei motivi descritti di seguito, l&#39;avvio delle reindicizzazioni degli indici Oak **non** modifica il comportamento o risolve i problemi e aumenta inutilmente i carichi sull&#39;AEM.

La reindicizzazione degli indici Oak deve essere evitata a meno che non sia coperta da un motivo nelle tabelle seguenti.

>[!NOTE]
>
>Prima di consultare le tabelle seguenti per determinare se la reindicizzazione è utile, **verifica sempre**:
>
>* la query è corretta
>* la query viene risolta nell&#39;indice previsto (utilizzando [Spiega query](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* processo di indicizzazione completato
>

### Modifiche alla configurazione dell’indice Oak {#oak-index-configuration-changes}

Le uniche condizioni non errate accettabili per la reindicizzazione degli indici Oak sono se la configurazione di un indice Oak è cambiata.

*La reindicizzazione deve sempre essere affrontata tenendo in debita considerazione il suo impatto sulle prestazioni complessive dell&#39;AEM ed eseguita durante periodi di bassa attività o finestre di manutenzione.*

Di seguito sono riportati i possibili problemi relativi alle risoluzioni:

* [Modifica definizione indice proprietà](#property-index-definition-change)
* [Modifica definizione indice Lucene](#lucene-index-definition-change)

#### Modifica definizione indice proprietà {#property-index-definition-change}

* Si applica per/se:

   * Tutte le versioni di Oak
   * Solo [indici di proprietà](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomi:

   * Nodi esistenti prima dell’aggiornamento della definizione dell’indice delle proprietà mancanti nei risultati

* Come verificare:

   * Determina se i nodi mancanti sono stati creati/modificati prima della distribuzione della definizione di indice aggiornata.
   * Verificare le proprietà `jcr:created` o `jcr:lastModified` di eventuali nodi mancanti in base all&#39;ora di modifica dell&#39;indice

* Come risolvere:

   * [Reindicizza](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) l&#39;indice Lucene
   * In alternativa, toccare (eseguire un’operazione di scrittura benigna) i nodi mancanti

      * Richiede contatti manuali o codice personalizzato
      * Richiede che il set di nodi mancanti sia noto
      * Richiede la modifica di qualsiasi proprietà sul nodo

#### Modifica definizione indice Lucene {#lucene-index-definition-change}

* Si applica per/se:

   * Tutte le versioni di Oak
   * Solo [indici Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti
   * I risultati della query non riflettono il comportamento previsto della definizione dell’indice
   * Il piano di query non segnala l’output previsto in base alla definizione dell’indice

* Come verificare:

   * Verificare che la definizione dell&#39;indice sia stata modificata utilizzando le statistiche dell&#39;indice di Lucene JMX Mbean (LuceneIndex), metodo `diffStoredIndexDefinition`.

* Come risolvere:

   * Versioni di Oak precedenti alla 1.6:

      * [Reindicizza](#how-to-re-index) l&#39;indice Lucene

   * Oak versioni 1.6+

      * Se il contenuto esistente non è interessato dalle modifiche, è necessario solo un aggiornamento

         * [Aggiorna](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) l&#39;indice Lucene impostando [oak:queryIndexDefinition]@refresh=true

      * Altrimenti [reindicizza](#how-to-re-index) l&#39;indice Lucene

         * Nota: lo stato dell’indice dall’ultima reindicizzazione valida (o indicizzazione iniziale) viene utilizzato fino a quando non viene attivata una nuova reindicizzazione

### Errori e situazioni eccezionali {#erring-and-exceptional-situations}

La tabella seguente descrive l’unico errore accettabile e le situazioni eccezionali in cui la reindicizzazione degli indici Oak risolve il problema.

Se si verifica un problema in AEM che non corrisponde ai criteri descritti di seguito, **non** reindicizzare gli indici, in quanto il problema non verrà risolto.

Di seguito sono riportati i possibili problemi relativi alle risoluzioni:

* [Manca il binario dell&#39;indice Lucene](#lucene-index-binary-is-missing)
* [Il file binario dell&#39;indice di Lucene è danneggiato](#lucene-index-binary-is-corrupt)

#### Manca il binario dell&#39;indice Lucene {#lucene-index-binary-is-missing}

* Si applica per/se:

   * Tutte le versioni di Oak
   * Solo [indici Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti

* Come verificare:

   * Il file di log degli errori contiene un&#39;eccezione che indica che manca un binario dell&#39;indice Lucene

* Come risolvere:

   * Eseguire una verifica dell’archivio di attraversamento, ad esempio:

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     l’attraversamento dell’archivio determina se mancano altri file binari (oltre ai file lucene)

   * Se mancano dati binari diversi dagli indici Lucene, eseguire il ripristino dal backup
   * In caso contrario, [reindicizza](#how-to-re-index) *tutti* gli indici Lucene
   * Nota:

     Questa condizione è indicativa di un archivio dati configurato in modo errato che potrebbe causare la perdita di dati binari ANY (ad esempio, binari di risorse).

     In questo caso, ripristina l’ultima versione valida nota dell’archivio per recuperare tutti i file binari mancanti.

#### Il file binario dell&#39;indice di Lucene è danneggiato {#lucene-index-binary-is-corrupt}

* Si applica per/se:

   * Tutte le versioni di Oak
   * Solo [indici Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L’indice Lucene non contiene i risultati previsti

* Come verificare:

   * `AsyncIndexUpdate` (ogni cinque secondi) avrà esito negativo con un&#39;eccezione nel log degli errori:

     `...a Lucene index file is corrupt...`

* Come risolvere:

   * Rimuovi la copia locale dell’indice Lucene

      1. Interrompere l’AEM
      1. Elimina la copia locale dell&#39;indice Lucene in `crx-quickstart/repository/index`
      1. Riavvia AEM

   * Se il problema non viene risolto e le eccezioni `AsyncIndexUpdate` persistono:

      1. [Reindicizza](#how-to-re-index) l&#39;indice erring
      1. Archivia anche un ticket di [supporto Adobe](https://helpx.adobe.com/support.html)

### Reindicizzare {#how-to-re-index}

>[!NOTE]
>
>In AEM 6.5, [oak-run.jar è l&#39;UNICO metodo supportato](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) per la reindicizzazione negli archivi MongoMK o RDBMK.

#### Reindicizzazione degli indici delle proprietà {#re-indexing-property-indexes}

* Utilizza [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) per reindicizzare l&#39;indice delle proprietà
* Impostare la proprietà async-reindex su true nell&#39;indice della proprietà

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindicizzare l&#39;indice delle proprietà in modo asincrono utilizzando la console Web tramite **PropertyIndexAsyncReindex** MBean;

  ad esempio:

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindicizzazione degli indici della proprietà Lucene {#re-indexing-lucene-property-indexes}

* Utilizza [oak-run.jar per reindicizzare](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) l&#39;indice della proprietà Lucene.
* Impostare la proprietà async-reindex su true nell&#39;indice della proprietà Lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sezione precedente riepiloga e inquadra le linee guida per la reindicizzazione di Oak tratte dalla [documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) nel contesto dell&#39;AEM.

### Pre-estrazione del testo dei dati binari {#text-pre-extraction-of-binaries}

La pre-estrazione del testo è il processo di estrazione ed elaborazione del testo dai dati binari, direttamente dall’archivio dati tramite un processo isolato, ed esposizione diretta del testo estratto a successive re/indicizzazioni degli indici Oak.

* La pre-estrazione del testo Oak è consigliata per la reindicizzazione degli indici Lucene in archivi con grandi volumi di file (file binari) contenenti testo estraibile (ad esempio PDF, documenti Word, PPT, TXT e così via) idonei per la ricerca full-text tramite indici Oak distribuiti, ad esempio `/oak:index/damAssetLucene`.
* La pre-estrazione del testo offre vantaggi solo per la re/indicizzazione degli indici Lucene e NON per gli indici delle proprietà Oak, poiché gli indici delle proprietà non estraggono il testo dai dati binari.
* La pre-estrazione del testo ha un forte impatto positivo quando la reindicizzazione full-text di file binari contenenti testo (PDF, Doc, TXT e così via), mentre un archivio di immagini non presenta le stesse efficienze poiché le immagini non contengono testo estraibile.
* La pre-estrazione del testo esegue l’estrazione di testo completo relativo alla ricerca in modo molto efficiente e lo espone al processo di reindicizzazione Oak in modo molto efficiente.

#### Quando può essere utilizzata la pre-estrazione del testo? {#when-can-text-pre-extraction-be-used}

Reindicizzazione di un indice Lucene **esistente** con estrazione binaria abilitata

* Reindicizzazione dell&#39;elaborazione di **tutti** i contenuti candidati nell&#39;archivio; quando i file binari da cui estrarre il testo completo sono numerosi o complessi, l&#39;AEM deve sostenere un carico di elaborazione maggiore per eseguire l&#39;estrazione del testo completo. La pre-estrazione del testo sposta il &quot;lavoro computazionalmente costoso&quot; dell&#39;estrazione del testo in un processo isolato che accede direttamente all&#39;Archivio dati dell&#39;AEM, evitando il sovraccarico e il conflitto di risorse nell&#39;AEM.

Supporto della distribuzione di un indice Lucene **new** all&#39;AEM con estrazione binaria abilitata

* Quando un nuovo indice (con estrazione binaria abilitata) viene distribuito in AEM, Oak indicizza automaticamente tutto il contenuto candidato alla successiva esecuzione dell’indice full-text asincrono. Per le stesse ragioni descritte nella reindicizzazione di cui sopra, ciò può comportare un carico eccessivo sull’AEM.

#### Quando NON è possibile utilizzare la pre-estrazione del testo? {#when-can-text-pre-extraction-not-be-used}

La pre-estrazione del testo non può essere utilizzata per i nuovi contenuti aggiunti all’archivio, né è necessaria.

Il nuovo contenuto aggiunto all’archivio viene indicizzato naturalmente e in modo incrementale dal processo di indicizzazione full-text asincrono (per impostazione predefinita, ogni 5 secondi).

In condizioni di normale funzionamento dell’AEM, ad esempio in caso di caricamento di Assets tramite l’interfaccia web o di acquisizione programmatica di Assets, l’AEM indicizzerà in modo automatico e incrementale il nuovo contenuto binario. Poiché la quantità di dati è incrementale e relativamente piccola (approssimativamente la quantità di dati che può essere mantenuta nell’archivio in 5 secondi), l’AEM può eseguire l’estrazione full-text dai dati binari durante l’indicizzazione senza influire sulle prestazioni complessive del sistema.

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

![Flusso del processo di pre-estrazione del testo](assets/chlimage_1-139.png)

**Genera elenco di contenuti da pre-estrarre**

*Eseguire il passaggio 1(a-b) durante un intervallo di manutenzione o un periodo di utilizzo ridotto durante l&#39;attraversamento dell&#39;archivio nodi durante questa operazione, che può comportare un carico significativo sul sistema.*

1 bis. Eseguire `oak-run.jar --generate` per creare un elenco di nodi per i quali verrà preestratto il testo.

1 ter. L&#39;elenco dei nodi (1a) viene archiviato nel file system come file CSV

L&#39;intero archivio nodi viene attraversato (come specificato dai percorsi nel comando oak-run) ogni volta che `--generate` viene eseguito e viene creato un file CSV **nuovo**. Il file CSV è **not** riutilizzato tra esecuzioni discrete del processo di pre-estrazione del testo (passaggi 1 - 2).

**Estrarre il testo nel file system**

*Il passaggio 2(a-c) può essere eseguito durante il normale funzionamento dell&#39;AEM se interagisce solo con l&#39;archivio dati.*

2 bis. Esegui `oak-run.jar --tika` per preestrarre il testo per i nodi binari enumerati nel file CSV generato in (1b)

2 ter. Il processo avviato in (2a) accede direttamente ai nodi binari definiti nel file CSV in Data Store ed estrae il testo.

2 quater. Il testo estratto viene memorizzato nel file system in un formato che può essere acquisito dal processo di reindicizzazione Oak (3a)

Il testo pre-estratto viene identificato nel file CSV dall’impronta digitale binaria. Se il file binario è lo stesso, è possibile utilizzare lo stesso testo pre-estratto in tutte le istanze AEM. Poiché AEM Publish è solitamente un sottoinsieme di AEM Author, il testo pre-estratto da AEM Author può spesso essere utilizzato anche per reindicizzare AEM Publish (supponendo che AEM Publish abbia accesso al file system ai file di testo estratti).

Il testo pre-estratto può essere aggiunto in modo incrementale a nel tempo. La pre-estrazione del testo salta l’estrazione per i file binari estratti in precedenza, pertanto è consigliabile mantenere il testo pre-estratto nel caso in cui la reindicizzazione debba verificarsi nuovamente in futuro (supponendo che il contenuto estratto non sia eccessivamente grande. In caso affermativo, valutare la compressione del contenuto nel frattempo, poiché il testo viene compresso correttamente.

**Reindicizza indici Oak, ricerca full-text da file di testo estratto**

*Eseguire la reindicizzazione (passaggi 3a-b) durante un periodo di manutenzione/basso utilizzo mentre l&#39;archivio nodi viene attraversato durante questa operazione, che può comportare un carico significativo sul sistema.*

3 bis. [Reindicizzazione](#how-to-re-index) degli indici Lucene richiamati in AEM.

3 ter. La configurazione OSGi di Apache Jackrabbit Oak DataStore PreExtractedTextProvider (configurata per puntare al testo estratto tramite un percorso del file system) indica ad Oak di ottenere il testo full-text dai file estratti ed evita di raggiungere ed elaborare direttamente i dati memorizzati nell’archivio.
