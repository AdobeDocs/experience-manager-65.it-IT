---
title: Tecniche consigliate per query e indicizzazione
seo-title: Best Practices for Queries and Indexing
description: Questo articolo fornisce linee guida su come ottimizzare indici e query.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4679'
ht-degree: 9%

---

# Tecniche consigliate per query e indicizzazione{#best-practices-for-queries-and-indexing}

Insieme alla transizione a Oak nel AEM 6, sono state apportate alcune modifiche importanti al modo in cui vengono gestite le query e gli indici. In Jackrabbit 2, tutto il contenuto era indicizzato per impostazione predefinita e poteva essere interrogato liberamente. In Oak, gli indici devono essere creati manualmente sotto il `oak:index` nodo. Una query può essere eseguita senza un indice, ma per i set di dati di grandi dimensioni, viene eseguita molto lentamente o persino in arresto.

Questo articolo illustra quando creare indici e quando non sono necessari, trucchi per evitare di utilizzare query quando non sono necessari e suggerimenti per ottimizzare indici e query in modo da ottenere le migliori prestazioni possibili.

Inoltre, assicurati di leggere il [Documentazione Oak sulla scrittura di query e indici](/help/sites-deploying/queries-and-indexing.md). Oltre a considerare gli indici come un nuovo concetto nel AEM 6, vi sono differenze sintattiche nelle query Oak che devono essere prese in considerazione durante la migrazione del codice da una precedente installazione AEM.

## Quando utilizzare le query {#when-to-use-queries}

### Struttura dell’archivio e della tassonomia {#repository-and-taxonomy-design}

Durante la progettazione della tassonomia di un archivio, occorre tenere conto di diversi fattori, tra cui controlli di accesso, localizzazione, ereditarietà di componenti e proprietà di pagina.

Durante la progettazione di una tassonomia che tenga conto di questi problemi, è importante anche considerare la “fruibilità” del design di indicizzazione. In questo contesto, l’attraversabilità è la capacità di una tassonomia che consente un accesso prevedibile ai contenuti in base al relativo percorso. Questo renderà più performante un sistema più semplice da mantenere rispetto a uno che richiederà l&#39;esecuzione di molte query.

Inoltre, durante la progettazione di una tassonomia, è importante considerare l’importanza dell’ordinamento. Nei casi in cui non è richiesto un ordinamento esplicito e si prevede un numero elevato di nodi di pari livello, è preferibile utilizzare un tipo di nodo non ordinato come `sling:Folder` o `oak:Unstructured`. Nei casi in cui è richiesto l’ordinamento, `nt:unstructured` e `sling:OrderedFolder` potrebbero essere più adatti.

### Query nei componenti {#queries-in-components}

Poiché le query possono essere una delle operazioni più gravose su un sistema AEM, è consigliabile evitarle nei componenti. Spesso, l’esecuzione di più query ogni volta che viene eseguito il rendering di una pagina può compromettere le prestazioni del sistema. Esistono due strategie che possono essere utilizzate per evitare l’esecuzione di query durante il rendering dei componenti: **navigazione dei nodi** e **preacquisizione dei risultati**.

#### Navigazione dei nodi {#traversing-nodes}

Se l’archivio è progettato in modo tale da consentire una conoscenza preventiva della posizione dei dati richiesti, il codice che recupera tali dati dai percorsi necessari può essere utilizzato senza dover eseguire query per trovarli.

Un esempio potrebbe essere il rendering di contenuti che rientrano a una determinata categoria. Un approccio consiste nell’organizzare i contenuti con una proprietà di categoria su cui è possibile eseguire una query per compilare un componente che mostra gli elementi in una categoria.

Un approccio migliore consisterebbe nello strutturare i contenuti in una tassonomia per categoria, in modo da poterli recuperare manualmente.

Ad esempio, se il contenuto viene memorizzato in una tassonomia simile a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

il `/content/myUnstructuredContent/parentCategory/childCategory` nodo può essere semplicemente recuperato, i relativi nodi secondari possono essere analizzati e utilizzati per eseguire il rendering del componente.

Inoltre, quando si tratta di un set di risultati piccolo o omogeneo, navigare l’archivio e raccogliere i nodi richiesti può essere una soluzione più veloce rispetto alla creazione di una query per restituire lo stesso set di risultati. In generale, occorre evitare le query laddove possibile.

#### Preacquisizione dei risultati {#prefetching-results}

A volte il contenuto o i requisiti intorno al componente non consentono l’uso di node traversal come metodo per recuperare i dati richiesti. In questi casi, è necessario eseguire le query necessarie prima di eseguire il rendering del componente in modo da garantire prestazioni ottimali per l’utente finale.

Se i risultati richiesti per il componente possono essere calcolati al momento della creazione e non c’è alcuna aspettativa che il contenuto venga modificato, la query può essere eseguita quando l’autore applica le impostazioni nella finestra di dialogo.

Se i dati o il contenuto vengono modificati regolarmente, la query può essere eseguita secondo una pianificazione o tramite un listener per gli aggiornamenti dei dati sottostanti. Dopodiché, i risultati possono essere scritti in una posizione condivisa nell’archivio. Tutti i componenti che necessitano di questi dati possono quindi richiamare i valori da questo singolo nodo senza dover eseguire una query in fase di esecuzione.

## Ottimizzazione delle query {#query-optimization}

Quando si esegue una query che non utilizza un indice, verranno registrati avvisi relativi all&#39;attraversamento dei nodi. Se si tratta di una query che verrà eseguita spesso, è necessario creare un indice. Per determinare l&#39;indice utilizzato da una determinata query, il [Strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) è consigliato. Per ulteriori informazioni, la registrazione DEBUG può essere abilitata per le API di ricerca pertinenti.

>[!NOTE]
>
>Dopo aver modificato la definizione di un indice, quest&#39;ultimo deve essere ricostruito (reindicizzato). A seconda delle dimensioni dell’indice, il completamento dell’operazione potrebbe richiedere del tempo.

Quando si eseguono query complesse, possono verificarsi casi in cui la suddivisione della query in più query più piccole e l&#39;unione dei dati tramite codice dopo che il fatto è più performante. Per questi casi si consiglia di confrontare le prestazioni dei due approcci per determinare quale opzione sarebbe migliore per il caso d’uso in questione.

AEM consente di scrivere query in uno dei tre modi seguenti:

* Tramite il [API di QueryBuilder](/help/sites-developing/querybuilder-api.md) (consigliato)
* Utilizzo di XPath (consigliato)
* Utilizzo di SQL2

Mentre tutte le query vengono convertite in SQL2 prima dell&#39;esecuzione, il sovraccarico della conversione delle query è minimo e quindi, la maggiore preoccupazione nella scelta di un linguaggio di query sarà la leggibilità e il livello di comfort dal team di sviluppo.

>[!NOTE]
>
>Quando si utilizza QueryBuilder, per impostazione predefinita verrà determinato il conteggio dei risultati, che è più lento in Oak rispetto alle versioni precedenti di Jackrabbit. Per compensare questo, è possibile utilizzare il [Parametro guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Strumento Spiega query {#the-explain-query-tool}

Come per qualsiasi linguaggio di query, il primo passo per ottimizzare una query è capire come verrà eseguita. Per abilitare questa attività, puoi utilizzare la funzione [Strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) fa parte del dashboard delle operazioni. Con questo strumento, è possibile collegare e spiegare una query. Viene visualizzato un avviso se la query causerà problemi con un archivio di grandi dimensioni, nonché il tempo di esecuzione e gli indici che verranno utilizzati. Lo strumento può anche caricare un elenco di query lente e popolari che possono poi essere spiegate e ottimizzate.

### Registrazione DEBUG per le query {#debug-logging-for-queries}

Per ottenere alcune informazioni aggiuntive su come Oak sta scegliendo l&#39;indice da utilizzare e come il motore di query sta eseguendo effettivamente una query, un **DEBUG** la configurazione della registrazione può essere aggiunta per i seguenti pacchetti:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Assicurati di rimuovere questo logger quando hai finito di eseguire il debug della query in quanto produrrà un sacco di attività e può alla fine riempire il disco con i file di log.

Per ulteriori informazioni su come eseguire questa operazione, consulta la [Documentazione sulla registrazione](/help/sites-deploying/configure-logging.md).

### Statistiche indice {#index-statistics}

Lucene registra un fagiolo JMX che fornirà dettagli sul contenuto indicizzato, tra cui la dimensione e il numero di documenti presenti in ciascuno degli indici.

Puoi raggiungerlo accedendo alla console JMX all’indirizzo `https://server:port/system/console/jmx`

Una volta effettuato l’accesso alla console JMX, esegui una ricerca per **Statistiche dell&#39;indice Lucene** per trovarla. Altre statistiche sull&#39;indice si trovano nella **IndexStats** MBean.

Per le statistiche delle query, controlla l’MBean denominato **Statistiche query Oak**.

Se desideri approfondire gli indici utilizzando uno strumento come [Luca](https://code.google.com/p/luke/), sarà necessario utilizzare la console Oak per scaricare l’indice dal `NodeStore` in una directory filesystem. Per istruzioni su come eseguire questa operazione, leggere il [Documentazione di Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Puoi anche estrarre gli indici nel tuo sistema in formato JSON. Per farlo, devi accedere a `https://server:port/oak:index.tidy.-1.json`

### Limiti per le query {#query-limits}

**Durante lo sviluppo**

Imposta soglie basse per `oak.queryLimitInMemory` (es. 10000) e quercia. `queryLimitReads` (es. 5000) e ottimizza la query costosa quando si preme un UnsupportedOperationException dicendo &quot;La query legge più di x nodi...&quot;

Questo consente di evitare query ad alta intensità di risorse (ad es. non supportato da alcun indice o sostenuto da un indice di copertura inferiore). Ad esempio, una query che legge 1 milione di nodi comporterebbe un aumento dell’I/O e avrebbe un impatto negativo sulle prestazioni complessive dell’applicazione. Qualsiasi query che non riesce a causa dei limiti sopra indicati deve essere analizzata e ottimizzata.

#### **Post-distribuzione** {#post-deployment}

* Monitora i log per le query che attivano il consumo di memoria heap di grandi nodi o traversal di grandi dimensioni : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizza la query per ridurre il numero di nodi attraversati

* Monitora i registri per le query che attivano un grande consumo di memoria heap :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizza la query per ridurre il consumo di memoria heap

Per le versioni AEM 6.0 - 6.2, è possibile ottimizzare la soglia per l&#39;attraversamento dei nodi tramite i parametri JVM nello script di avvio AEM per evitare che le query di grandi dimensioni sovraccarichino l&#39;ambiente.

I valori consigliati sono :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri di cui sopra sono preconfigurati OOTB e possono essere mantenuti tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Suggerimenti per la creazione di indici efficienti {#tips-for-creating-efficient-indexes}

### È necessario creare un indice? {#should-i-create-an-index}

La prima domanda da porsi quando si creano o si ottimizzano gli indici è se sono realmente necessari per una determinata situazione. Se esegui la query in questione solo una volta o solo occasionalmente e a un&#39;ora di picco per il sistema attraverso un processo batch, potrebbe essere meglio non creare alcun indice.

Dopo aver creato un indice, ogni volta che i dati indicizzati vengono aggiornati, l&#39;indice deve essere aggiornato. Poiché questo comporta implicazioni in termini di prestazioni per il sistema, gli indici dovrebbero essere creati solo quando sono effettivamente necessari.

Inoltre, gli indici sono utili solo se i dati contenuti all’interno dell’indice sono abbastanza univoci da garantirne l’attendibilità. Considera un indice in un libro e gli argomenti che tratta. Quando si indicizza un insieme di argomenti in un testo, di solito ci saranno centinaia o migliaia di voci, che ti consente di passare rapidamente a un sottoinsieme di pagine per trovare rapidamente le informazioni che stai cercando. Se quell&#39;indice contenesse solo due o tre voci, ognuna delle quali indicava diverse centinaia di pagine, l&#39;indice non sarebbe molto utile. Lo stesso concetto si applica agli indici di database. Se ci sono solo due valori univoci, l&#39;indice non sarà molto utile. Detto questo, un indice può anche diventare troppo grande per essere utile. Per le statistiche degli indici, vedi [Statistiche indice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) sopra.

### Indici di proprietà o Lucene? {#lucene-or-property-indexes}

Gli indici Lucene sono stati introdotti in Oak 1.0.9 e offrono alcune potenti ottimizzazioni sugli indici delle proprietà che sono stati introdotti nel lancio iniziale di AEM 6. Nel decidere se utilizzare gli indici Lucene o gli indici di proprietà, considera quanto segue:

* Gli indici Lucene offrono molte più funzionalità degli indici delle proprietà. Ad esempio, un indice di proprietà può indicizzare solo una singola proprietà, mentre un indice Lucene può includerne molte. Per ulteriori informazioni su tutte le funzioni disponibili negli indici Lucene, consulta la [documentazione](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Gli indici Lucene sono asincroni. Anche se questo offre un notevole incremento delle prestazioni, può anche causare un ritardo tra il momento in cui i dati vengono scritti nell’archivio e il momento in cui l’indice viene aggiornato. Se è fondamentale che le query restituiscano risultati precisi al 100%, sarà necessario un indice di proprietà.
* In virtù del fatto che è asincrono, gli indici Lucene non possono applicare vincoli di unicità. Se questo è necessario, allora sarà necessario creare un indice di proprietà.

In generale, si consiglia di utilizzare gli indici Lucene a meno che non vi sia una necessità irresistibile di utilizzare gli indici delle proprietà in modo da poter ottenere i vantaggi di prestazioni e flessibilità più elevate.

### Indicizzazione solare {#solr-indexing}

AEM fornisce inoltre il supporto per l&#39;indicizzazione Solr per impostazione predefinita. Questa funzione viene utilizzata principalmente per supportare la ricerca full text, ma può anche essere utilizzata per supportare qualsiasi tipo di query JCR. Solr dovrebbe essere considerato quando le istanze AEM non hanno la capacità della CPU per gestire il numero di query necessarie in implementazioni intensive di ricerca come siti web basati su ricerca con un numero elevato di utenti simultanei. In alternativa, Solr può essere implementato in un approccio basato su crawler per sfruttare alcune delle funzioni più avanzate della piattaforma.

Gli indici Solr possono essere configurati per l&#39;esecuzione di dati incorporati nel server AEM per gli ambienti di sviluppo oppure possono essere scaricati in un&#39;istanza remota per migliorare la scalabilità di ricerca negli ambienti di produzione e di staging. Mentre lo scaricamento della ricerca migliorerà la scalabilità, introdurrà latenza e per questo motivo, è sconsigliato se non richiesto. Per ulteriori informazioni su come configurare l’integrazione Solr e come creare indici Solr, consulta la sezione [Documentazione su query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Se si adotta l&#39;approccio integrato di ricerca Solr, si può scaricare l&#39;indicizzazione su un server Solr. Se le funzioni più avanzate del server Solr vengono utilizzate tramite un approccio basato su crawler, sarà necessario un ulteriore lavoro di configurazione. La cuffia ha creato un [connettore open source](https://www.aemsolrsearch.com/#/) accelerare questi tipi di implementazioni.

Il lato negativo di questo approccio è che, mentre per impostazione predefinita, le query AEM rispetteranno le ACL e quindi nascondono i risultati a cui un utente non ha accesso, esternalizzare la ricerca a un server Solr non supporterà questa funzione. Se la ricerca deve essere esternalizzata in questo modo, occorre prestare maggiore attenzione affinché gli utenti non ricevano risultati che non dovrebbero vedere.

I casi d’uso potenziali in cui questo approccio può essere appropriato sono i casi in cui i dati di ricerca provenienti da più fonti possono dover essere aggregati. Ad esempio, potresti avere un sito ospitato su AEM e un secondo sito ospitato su una piattaforma di terze parti. È possibile configurare Solr per eseguire la ricerca per indicizzazione del contenuto di entrambi i siti e archiviarli in un indice aggregato. Ciò consentirebbe ricerche tra siti diversi.

### Considerazioni sulla progettazione {#design-considerations}

La documentazione Oak per gli indici Lucene elenca diverse considerazioni da fare durante la progettazione degli indici:

* Se la query utilizza restrizioni di percorso diverse, utilizza `evaluatePathRestrictions`. Questo consentirà alla query di restituire il sottoinsieme di risultati sotto il percorso specificato e quindi di filtrarli in base alla query. In caso contrario, la query cercherà tutti i risultati che corrispondono ai parametri di query nel repository e quindi li filtrerà in base al percorso.
* Se la query utilizza l&#39;ordinamento, disporre di una definizione esplicita della proprietà ordinata e impostare `ordered` a `true` per questo. Ciò consentirà di ordinare i risultati come tali nell’indice e di risparmiare sulle costose operazioni di ordinamento al momento dell’esecuzione della query.

* Mettete solo ciò che è necessario nell&#39;indice. L&#39;aggiunta di funzionalità o proprietà non necessarie causerà l&#39;aumento e il rallentamento delle prestazioni dell&#39;indice.
* In un indice di proprietà, avere un nome di proprietà univoco contribuirebbe a ridurre la dimensione su un indice, ma per gli indici Lucene, l&#39;uso di `nodeTypes` e `mixins` per ottenere indici coerenti. Query di uno specifico `nodeType` o `mixin` sarà più performante che fare query `nt:base`. Quando utilizzi questo approccio, definisci `indexRules` per `nodeTypes` in questione.

* Se le query vengono eseguite solo in determinati percorsi, crea tali indici sotto tali percorsi. Gli indici non sono necessari per vivere nella directory principale dell&#39;archivio.
* Si consiglia di utilizzare un singolo indice quando tutte le proprietà indicizzate sono correlate per consentire a Lucene di valutare il maggior numero possibile di restrizioni di proprietà in modo nativo. Inoltre, una query utilizzerà un solo indice, anche quando si esegue un join.

### CopyOnRead {#copyonread}

Nei casi in cui `NodeStore` viene memorizzato in remoto, un&#39;opzione denominata `CopyOnRead` può essere attivato. L&#39;opzione fa sì che l&#39;indice remoto venga scritto nel file system locale quando viene letto. Questo può aiutare a migliorare le prestazioni per le query che vengono spesso eseguite con questi indici remoti.

Questa può essere configurata nella console OSGi sotto la **LuceneIndexProvider** e è abilitato per impostazione predefinita a partire da Oak 1.0.13.

### Rimozione degli indici {#removing-indexes}

Quando si rimuove un indice, si consiglia sempre di disattivare temporaneamente l&#39;indice impostando il `type` proprietà di `disabled` e eseguire test per garantire che l&#39;applicazione funzioni correttamente prima di eliminarla. Tieni presente che un indice non viene aggiornato mentre è disabilitato, pertanto potrebbe non avere il contenuto corretto se viene riabilitato e potrebbe essere necessario reindicizzarlo.

Dopo aver rimosso un indice di proprietà su un&#39;istanza TarMK, sarà necessario eseguire la compattazione per recuperare lo spazio su disco in uso. Per gli indici Lucene, l&#39;effettivo contenuto dell&#39;indice vive nel BlobStore, quindi sarebbe necessario un archivio dati per la raccolta degli oggetti inattivi.

Quando si rimuove un indice su un&#39;istanza MongoDB, il costo di eliminazione è proporzionale al numero di nodi nell&#39;indice. Poiché l&#39;eliminazione di un indice di grandi dimensioni può causare problemi, l&#39;approccio consigliato è quello di disabilitare l&#39;indice ed eliminarlo solo durante una finestra di manutenzione, utilizzando uno strumento come **oak-mongo.js**. Tieni presente che questo approccio non deve essere utilizzato per il contenuto normale dei nodi in quanto può introdurre incongruenze nei dati.

>[!NOTE]
>
>Per ulteriori informazioni su oak-mongo.js, consulta la sezione [Sezione Strumenti riga di comando](https://jackrabbit.apache.org/oak/docs/command_line.html) della documentazione Oak.

### Foglio di calcolo della query JCR {#jcrquerycheatsheet}

Per supportare la creazione di query JCR e le definizioni degli indici efficienti, la [Scheda di riferimento rapido per le query JCR](assets/JCR_query_cheatsheet-v1.1.pdf) è disponibile per il download e l’utilizzo come riferimento durante lo sviluppo. Contiene query di esempio per QueryBuilder, XPath e SQL-2, che coprono scenari multipli che si comportano in modo diverso in termini di prestazioni delle query. Fornisce inoltre consigli su come creare o personalizzare gli indici Oak. Il contenuto di questo Cheat Sheet si applica a AEM 6.5 e AEM as a Cloud Service.

## Reindicizzazione {#re-indexing}

Questa sezione delinea la **only** motivi accettabili per reindicizzare gli indici Oak.

Al di fuori dei motivi descritti di seguito, l&#39;avvio di reindici di Oak **not** modificare il comportamento o risolvere i problemi e aumentare inutilmente il carico su AEM.

Occorre evitare la reindicizzazione degli indici Oak, a meno che non sia coperta da una motivazione nelle tabelle seguenti.

>[!NOTE]
>
>Prima di consultare le tabelle seguenti per determinare la reindicizzazione è utile, **sempre** verifica:
>
>* la query è corretta
>* la query viene risolta nell&#39;indice previsto (utilizzando [Spiega query](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* il processo di indicizzazione è stato completato
>


### Modifiche alla configurazione dell&#39;indice Oak {#oak-index-configuration-changes}

L&#39;unica condizione accettabile di non-erring per la reindicizzazione degli indici Oak è se la configurazione di un indice Oak è cambiata.

*La reindicizzazione deve sempre essere affrontata con la dovuta considerazione per il suo impatto sulle prestazioni complessive AEM ed eseguita durante i periodi di bassa attività o di intervallo di manutenzione.*

I seguenti dettagli possono essere presentati insieme alle risoluzioni:

* [Modifica della definizione dell&#39;indice di proprietà](#property-index-definition-change)
* [Modifica della definizione dell&#39;indice Lucene](#lucene-index-definition-change)

#### Modifica della definizione dell&#39;indice di proprietà {#property-index-definition-change}

* Si applica a/se:

   * Tutte le versioni Oak
   * Solo [indici delle proprietà](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomi:

   * Nodi esistenti prima dell&#39;aggiornamento della definizione dell&#39;indice delle proprietà mancanti dai risultati

* Come verificare:

   * Determina se i nodi mancanti sono stati creati/modificati prima della distribuzione della definizione di indice aggiornata.
   * Verifica la `jcr:created` o `jcr:lastModified` proprietà di eventuali nodi mancanti rispetto al tempo modificato dell&#39;indice

* Come risolvere:

   * [Reindicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) l&#39;indice lucene
   * In alternativa, puoi toccare (eseguire un&#39;operazione di scrittura benigna) i nodi mancanti

      * Richiede tocco manuale o codice personalizzato
      * Richiede che il set di nodi mancanti sia noto
      * Richiede la modifica di qualsiasi proprietà sul nodo

#### Modifica della definizione dell&#39;indice Lucene {#lucene-index-definition-change}

* Si applica a/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice Lucene non contiene i risultati previsti
   * I risultati della query non riflettono il comportamento previsto nella definizione dell&#39;indice
   * Il piano di query non riporta l&#39;output previsto in base alla definizione dell&#39;indice

* Come verificare:

   * Verifica che la definizione dell&#39;indice sia stata modificata utilizzando il metodo Lucene Index statistics JMX Mbean (LuceneIndex) `diffStoredIndexDefinition`.

* Come risolvere:

   * Versioni di Oak precedenti alla 1.6:

      * [Reindicizzazione](#how-to-re-index) l&#39;indice lucene
   * Oak versioni 1.6+

      * Se le modifiche non apportano contenuto esistente, è necessario solo un aggiornamento

         * [Aggiorna](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) l&#39;indice lucene impostando [oak:queryIndexDefinition]@refresh=true
      * Else, [reindicizzazione](#how-to-re-index) l&#39;indice lucene

         * Nota: Lo stato dell’indice dall’ultima reindicizzazione corretta (o indicizzazione iniziale) verrà utilizzato fino a quando non viene attivata una nuova reindicizzazione.



### Situazioni di errore ed eccezionali {#erring-and-exceptional-situations}

La tabella seguente descrive le uniche situazioni di errore accettabili ed eccezionali in cui la reindicizzazione degli indici Oak risolverà il problema.

Se si verifica un problema su AEM che non corrisponde ai criteri descritti di seguito, fai **not** reindicizza eventuali indici, in quanto non risolverà il problema.

I seguenti dettagli possono essere presentati insieme alle risoluzioni:

* [Il binario dell&#39;indice Lucene è mancante](#lucene-index-binary-is-missing)
* [Il binario dell&#39;indice Lucene è corrotto](#lucene-index-binary-is-corrupt)

#### Il binario dell&#39;indice Lucene è mancante {#lucene-index-binary-is-missing}

* Si applica a/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice Lucene non contiene i risultati previsti

* Come verificare:

   * Il file di log degli errori contiene un&#39;eccezione che indica che manca un binario dell&#39;indice Lucene

* Come risolvere:

   * Eseguire un controllo del repository di traversata; ad esempio:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      l&#39;attraversamento dell&#39;archivio determina se mancano altri file binari (oltre ai file lucene)

   * Se mancano i binari diversi dagli indici lucene, eseguire il ripristino dal backup
   * In caso contrario, [reindicizzazione](#how-to-re-index) *tutto* indici lucene
   * Nota:

      Questa condizione è indicativa di un datastore configurato in modo errato che può comportare QUALSIASI binario (ad esempio asset binari) da perdere.

      In questo caso, ripristina l&#39;ultima versione valida nota dell&#39;archivio per recuperare tutti i binari mancanti.

#### Il binario dell&#39;indice Lucene è corrotto {#lucene-index-binary-is-corrupt}

* Si applica a/se:

   * Tutte le versioni Oak
   * Solo [indici lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomi:

   * L&#39;indice Lucene non contiene i risultati previsti

* Come verificare:

   * La `AsyncIndexUpdate` (ogni 5s) fallirà con un&#39;eccezione nel log degli errori:

      `...a Lucene index file is corrupt...`

* Come risolvere:

   * Rimuovi la copia locale dell&#39;indice lucene

      1. Interrompi AEM
      1. Elimina la copia locale dell&#39;indice lucene in `crx-quickstart/repository/index`
      1. Riavvia AEM
   * Se questo non risolve il problema, e il `AsyncIndexUpdate` persistono le eccezioni:

      1. [Reindicizzazione](#how-to-re-index) l&#39;indice di errore
      1. Anche un file [Supporto Adobe](https://helpx.adobe.com/support.html) biglietto


### Come reindicizzare {#how-to-re-index}

>[!NOTE]
>
>AEM 6.5, [oak-run.jar è il metodo ONLY supportato](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) per la reindicizzazione su archivi MongoMK o RDBMK.

#### Indice delle proprietà di reindicizzazione {#re-indexing-property-indexes}

* Utilizzo [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) per reindicizzare l&#39;indice delle proprietà
* Imposta la proprietà async-reindex su true sull&#39;indice delle proprietà

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindicizza l&#39;indice delle proprietà in modo asincrono utilizzando la Console web tramite la **PropertyIndexAsyncReindex** MBean;

   Esempio,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Re-indicizzazione indici delle proprietà Lucene {#re-indexing-lucene-property-indexes}

* Utilizzo [oak-run.jar per reindicizzare](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) l&#39;indice della proprietà Lucene.
* Imposta la proprietà async-reindex su true sull&#39;indice delle proprietà lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La sezione precedente riassume e incornicia le indicazioni di reindicizzazione Oak dal [Documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) nel contesto di AEM.

### Pre-estrazione del testo dei binari {#text-pre-extraction-of-binaries}

La preestrazione del testo è il processo di estrazione ed elaborazione del testo dai binari, direttamente dall’archivio dati tramite un processo isolato, ed espone direttamente il testo estratto ai successivi re/indici degli indici Oak.

* La preestrazione del testo Oak è consigliata per la re/indicizzazione degli indici Lucene sugli archivi con grandi volumi di file (binari) che contengono testo estraibile (ad esempio PDF, documenti di Word, PPT, TXT, ecc.) idonei alla ricerca full-text tramite indici Oak distribuiti; per esempio `/oak:index/damAssetLucene`.
* La preestrazione del testo beneficerà solo della reindicizzazione degli indici Lucene e degli indici delle proprietà NOT Oak, in quanto gli indici delle proprietà non estraggono testo dai binari.
* La preestrazione del testo ha un impatto positivo elevato quando la reindicizzazione full-text di file binari pesanti (PDF, Doc, TXT, ecc.), in cui come archivio di immagini non godrà delle stesse efficienze in quanto le immagini non contengono testo estraibile.
* La preestrazione del testo esegue l’estrazione del testo relativo alla ricerca full-text in modo extra-efficiente e lo espone al processo di re/indicizzazione Oak in modo da risultare estremamente efficiente da utilizzare.

#### Quando è possibile utilizzare la preestrazione del testo? {#when-can-text-pre-extraction-be-used}

Re-indicizzazione di un **esistente** indice lucene con estrazione binaria abilitata

* Elaborazione della reindicizzazione **tutto** contenuto candidato nell&#39;archivio; quando i binari da cui estrarre il testo completo sono numerosi o complessi, un maggiore carico di calcolo per eseguire l’estrazione full-text viene posizionato su AEM. La preestrazione del testo sposta il &quot;lavoro computazionale&quot; dell’estrazione del testo in un processo isolato che accede direttamente AEM Data Store, evitando costi comuni e contese delle risorse in AEM.

Sostenere la diffusione di un **nuovo** lucene index to AEM con estrazione binaria abilitata

* Quando un nuovo indice (con l’estrazione binaria abilitata) viene distribuito in AEM, Oak indicizza automaticamente tutti i contenuti candidati nella successiva esecuzione asincrona dell’indice di testo completo. Per gli stessi motivi descritti nella reindicizzazione di cui sopra, ciò può comportare un carico eccessivo su AEM.

#### Quando è possibile utilizzare la preestrazione del testo NOT? {#when-can-text-pre-extraction-not-be-used}

La preestrazione del testo non può essere utilizzata per i nuovi contenuti aggiunti all’archivio, né è necessaria.

Il nuovo contenuto viene aggiunto all’archivio verrà naturalmente e gradualmente indicizzato dal processo di indicizzazione full-text asincrono (per impostazione predefinita, ogni 5 secondi).

In condizioni normali di AEM, ad esempio durante il caricamento di risorse tramite l’interfaccia utente web o l’acquisizione programmatica di risorse, AEM indicizza automaticamente e in modo incrementale il nuovo contenuto binario. Poiché la quantità di dati è incrementale e relativamente piccola (circa la quantità di dati che possono essere memorizzati nell’archivio in 5 secondi), AEM può eseguire l’estrazione full-text dai binari durante l’indicizzazione senza influire sulle prestazioni complessive del sistema.

#### Prerequisiti per l’utilizzo della preestrazione del testo {#prerequisites-to-using-text-pre-extraction}

* Reindicizzerai un indice lucene che esegue l’estrazione binaria full-text o distribuirai un nuovo indice che eseguirà i binari di indice full-text del contenuto esistente
* Il contenuto (file binari) da cui estrarre il testo deve trovarsi nell’archivio
* Una finestra di manutenzione per generare il file CSV E per eseguire la reindicizzazione finale
* Versione Oak: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versione 1.7.4+
* Cartella/condivisione file system per memorizzare il testo estratto accessibile dalle istanze di indicizzazione AEM

   * La configurazione OSGi di pre-estrazione del testo richiede un percorso del file system ai file di testo estratti, in modo che siano accessibili direttamente dall&#39;istanza AEM (unità locale o file share mount)

#### Come eseguire la preestrazione del testo {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***I comandi oak-run.jar descritti di seguito sono completamente enumerati in [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>Il diagramma e i passaggi descritti di seguito spiegano e completano i passaggi tecnici di preestrazione del testo descritti nella documentazione Apache Oak.

![Flusso del processo di preestrazione del testo](assets/chlimage_1-139.png)

**Genera elenco di contenuti da pre-estrarre**

*Esegui il passaggio 1(a-b) durante una finestra di manutenzione/un periodo di utilizzo ridotto, mentre il Node Store viene attraversato durante questa operazione, che può comportare un carico significativo sul sistema.*

1 bis. Esegui `oak-run.jar --generate` per creare un elenco di nodi in cui il loro testo verrà pre-estratto.

1 ter. L’elenco dei nodi (1a) è memorizzato nel file system come file CSV

Tieni presente che l’intero Node Store viene attraversato ogni volta (come specificato dai percorsi nel comando oak-run) `--generate` viene eseguito e viene eseguito un **nuovo** Viene creato un file CSV. Il file CSV è **not** riutilizzato tra esecuzioni discrete del processo di preestrazione del testo (passaggi 1 - 2).

**Preestrarre testo nel file system**

*Il passaggio 2 (a-c) può essere eseguito durante il normale funzionamento di AEM se interagisce solo con l&#39;archivio dati.*

2 bis. Esegui `oak-run.jar --tika` per preestrarre il testo per i nodi binari enumerati nel file CSV generato in (1b)

2 ter. Il processo avviato in (2a) accede direttamente ai nodi binari definiti nel CSV nel Data Store ed estrae il testo.

2 quater.  Il testo estratto viene memorizzato nel file system in un formato assimilabile dal processo di reindicizzazione Oak (3a)

Il testo pre-estratto è identificato nel CSV dall’impronta digitale binaria. Se il file binario è lo stesso, lo stesso testo pre-estratto può essere utilizzato in AEM istanze. Poiché AEM Publish è solitamente un sottoinsieme di AEM Author, il testo pre-estratto da AEM Author può spesso essere utilizzato anche per reindicizzare AEM Publish (partendo dal presupposto che AEM Publish abbia accesso al file di testo estratto).

Il testo pre-estratto può essere aggiunto in modo incrementale nel tempo. La preestrazione del testo salterà l’estrazione per i binari precedentemente estratti, quindi è consigliabile mantenere il testo pre-estratto nel caso in cui la reindicizzazione debba ripetersi in futuro (supponendo che il contenuto estratto non sia eccessivamente grande). Se lo è, valuta la compressione dei contenuti nel frattempo, dal momento che il testo si comprime bene).

**Reindicizza gli indici Oak, ottenendo il testo completo dai file di testo estratti**

*Esegui la reindicizzazione (passaggi 3a-b) durante un periodo di manutenzione/basso utilizzo mentre il Node Store viene attraversato durante questa operazione, che può comportare un carico significativo sul sistema.*

3 bis. [Reindicizzazione](#how-to-re-index) di indici Lucene viene richiamato in AEM

3 ter. La configurazione OSGi Apache Jackrabbit Oak DataStore PreExtraitTextProvider OSGi (configurata per puntare al testo estratto tramite un percorso del file system) istruisce Oak al testo full-text ottenuto dai file estratti ed evita di colpire ed elaborare direttamente i dati memorizzati nell&#39;archivio.
