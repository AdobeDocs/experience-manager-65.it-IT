---
title: Query e indicizzazione Oak
seo-title: Query e indicizzazione Oak
description: Scopri come configurare gli indici in AEM.
seo-description: Scopri come configurare gli indici in AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: b01f6d3726fd6aa06ffedaf10dfde9526479a2a3
workflow-type: tm+mt
source-wordcount: '2880'
ht-degree: 1%

---


# Query Oak e indicizzazione{#oak-queries-and-indexing}

>[!NOTE]
>
>Questo articolo riguarda la configurazione degli indici nel AEM 6. Per le best practice sull&#39;ottimizzazione delle prestazioni di query e indicizzazione, vedere [Best practice for Query and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md) (Tecniche consigliate per query e indicizzazione).

## Introduzione {#introduction}

A differenza di Jackrabbit 2, Oak non indicizza il contenuto per impostazione predefinita. Se necessario, è necessario creare indici personalizzati, come avviene per i database relazionali tradizionali. Se non esiste un indice per una query specifica, è possibile che molti nodi vengano attraversati. La query può funzionare ma probabilmente è molto lenta.

Se Oak rileva una query senza indice, viene stampato un messaggio di registro di livello WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Lingue di query supportate {#supported-query-languages}

Il motore di query Oak supporta le seguenti lingue:

* XPath (consigliato)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipi di indicizzatore e calcolo dei costi {#indexer-types-and-cost-calculation}

Il backend basato su Apache Oak consente di collegare diversi indicizzatori al repository.

Un indicizzatore è l&#39; **Indice proprietà**, per il quale la definizione dell&#39;indice è memorizzata nell&#39;archivio stesso.

Per impostazione predefinita sono disponibili anche le implementazioni per **Apache Lucene** e **Solr**, che supportano entrambe l&#39;indicizzazione full-text.

Se non è disponibile alcun altro indicizzatore, viene utilizzato l&#39; **Indice trasversale**. Ciò significa che il contenuto non è indicizzato e che i nodi di contenuto vengono attraversati per trovare corrispondenze alla query.

Se per una query sono disponibili più indicizzatori, ogni indicizzatore disponibile stima il costo dell&#39;esecuzione della query. Oak sceglie quindi l&#39;indicizzatore con il costo stimato più basso.

![chlimage_1-148](assets/chlimage_1-148.png)

Il diagramma precedente è una rappresentazione ad alto livello del meccanismo di esecuzione delle query di Apache Oak.

Innanzitutto, la query viene analizzata in una struttura ad albero della sintassi astratta. Quindi, la query viene controllata e trasformata in SQL-2 che è la lingua nativa per le query Oak.

Successivamente, ciascun indice viene consultato per stimare il costo della query. Una volta completato, i risultati dell&#39;indice più economico vengono recuperati. Infine, i risultati vengono filtrati, sia per garantire che l&#39;utente corrente abbia accesso in lettura al risultato che il risultato corrisponda alla query completa.

## Configurazione degli indici {#configuring-the-indexes}

>[!NOTE]
>
>Per un repository di grandi dimensioni, la creazione di un indice richiede molto tempo. Ciò vale sia per la creazione iniziale di un indice, sia per la reindicizzazione (ricreazione di un indice dopo la modifica della definizione). Vedere anche [Risoluzione dei problemi di indici di rovere](/help/sites-deploying/troubleshooting-oak-indexes.md) e [Prevenzione di reindicizzazione lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Se la reindicizzazione è necessaria in archivi di grandi dimensioni, specialmente quando si utilizza MongoDB e per indici full-text, prendere in considerazione la preestrazione del testo e utilizzare l&#39;esecuzione della quercia per creare l&#39;indice iniziale e reindicizzarlo.

Gli indici sono configurati come nodi nell&#39;archivio sotto il nodo **quercia:index**.

Il tipo del nodo di indice deve essere **oak:QueryIndexDefinition.** Sono disponibili diverse opzioni di configurazione per ciascun indicizzatore come proprietà del nodo. Per ulteriori informazioni, vedere i dettagli di configurazione per ciascun tipo di indicizzatore riportato di seguito.

### Indice proprietà {#the-property-index}

L&#39;indice delle proprietà è generalmente utile per le query con vincoli di proprietà ma non con testo completo. Può essere configurato seguendo la procedura seguente:

1. Aprire CRXDE andando su `http://localhost:4502/crx/de/index.jsp`
1. Crea un nuovo nodo sotto **quercia:index**
1. Denominate il nodo **PropertyIndex** e impostate il tipo di nodo su **oak:QueryIndexDefinition**
1. Imposta le seguenti proprietà per il nuovo nodo:

   * **type:**  `property` (di tipo String)
   * **propertyNames:**  `jcr:uuid` (di tipo Name)

   In questo esempio viene indicizzata la proprietà `jcr:uuid`, il cui lavoro consiste nell&#39;esporre l&#39;identificatore universale univoco (UUID) del nodo a cui è associato.

1. Salva le modifiche.

L&#39;indice delle proprietà presenta le seguenti opzioni di configurazione:

* La proprietà **type** specifica il tipo di indice e in questo caso deve essere impostata su **property**

* La proprietà **propertyNames** indica l&#39;elenco delle proprietà che verranno memorizzate nell&#39;indice. Se manca, il nome del nodo verrà utilizzato come valore di riferimento del nome della proprietà. In questo esempio, la proprietà **jcr:uuid** il cui lavoro consiste nell&#39;esporre l&#39;identificatore univoco (UUID) del nodo corrispondente viene aggiunta all&#39;indice.

* Il flag **univoco** che, se impostato su **true** aggiunge un vincolo di univocità all&#39;indice delle proprietà.

* La proprietà **dichiararingNodeTypes** consente di specificare un determinato tipo di nodo a cui l&#39;indice si applica solo.
* Il flag **reindex** che, se impostato su **true**, attiverà un reindice completo del contenuto.

### Indice ordinato {#the-ordered-index}

L&#39;indice ordinato è un&#39;estensione dell&#39;indice Property. Tuttavia, è stato dichiarato obsoleto. Gli indici di questo tipo devono essere sostituiti con [Indice proprietà Lucene](#the-lucene-property-index).

### Indice Lucene full text {#the-lucene-full-text-index}

Un indicizzatore full text basato su Apache Lucene è disponibile in AEM 6.

Se è configurato un indice full-text, tutte le query con una condizione full-text utilizzano l&#39;indice full-text, indipendentemente dal fatto che siano presenti altre condizioni indicizzate e indipendentemente dall&#39;eventuale limitazione del percorso.

Se non è configurato alcun indice full-text, le query con condizioni full-text non funzioneranno come previsto.

Poiché l&#39;indice viene aggiornato tramite un thread in background asincrono, alcune ricerche full-text non saranno disponibili per una piccola finestra di tempo fino al completamento dei processi in background.

Puoi configurare un indice full-text di Lucene seguendo la procedura seguente:

1. Aprite CRXDE e create un nuovo nodo sotto **quercia:index**.
1. Denominate il nodo **LuceneIndex** e impostate il tipo di nodo su **quercia:QueryIndexDefinition**
1. Aggiungi le seguenti proprietà al nodo:

   * **type:**  `lucene` (di tipo String)
   * **asincrono:**  `async` (di tipo String)

1. Salva le modifiche.

L&#39;indice Lucene presenta le seguenti opzioni di configurazione:

* La proprietà **type** che specifica il tipo di indice deve essere impostata su **lucene**
* La proprietà **asincrona** che deve essere impostata su **asincrona**. Questo invierà il processo di aggiornamento dell&#39;indice a un thread in background.
* La proprietà **includePropertyTypes**, che definirà quale sottoinsieme di tipi di proprietà verrà incluso nell&#39;indice.
* La proprietà **excludePropertyNames** che definirà un elenco di nomi di proprietà - proprietà da escludere dall&#39;indice.
* Il flag **reindex** che, se impostato su **true**, attiva un reindicizzatore completo del contenuto.

### Indice proprietà Lucene {#the-lucene-property-index}

A partire da **Oak 1.0.8**, Lucene può essere utilizzato per creare indici che includono vincoli di proprietà non full-text.

Per ottenere un indice delle proprietà Lucene, la proprietà **fulltextEnabled** deve sempre essere impostata su false.

Effettuate la seguente query di esempio:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Per definire un indice delle proprietà Lucene per la query di cui sopra, potete aggiungere la seguente definizione creando un nuovo nodo in **oak:index:**

* **Nome:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una volta creato il nodo, aggiungere le seguenti proprietà:

* **tipo:**

   ```
   lucene (of type String)
   ```

* **asincrono:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>Rispetto al normale indice delle proprietà, l&#39;indice delle proprietà Lucene è sempre configurato in modalità asincrona. Pertanto, i risultati restituiti dall&#39;indice potrebbero non riflettere sempre lo stato più aggiornato del repository.

>[!NOTE]
>
>Per informazioni più specifiche sull&#39;indice delle proprietà Lucene, consultate la [pagina della documentazione Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene Analyzers {#lucene-analyzers}

Dalla versione 1.2.0, Oak supporta gli analizzatori Lucene.

Gli analizzatori vengono utilizzati sia quando un documento viene indicizzato, sia durante la query. Un analizzatore esamina il testo dei campi e genera un flusso di token. Gli analizzatori Lucene sono composti da una serie di classi di token e filtri.

Gli analizzatori possono essere configurati tramite il nodo `analyzers` (di tipo `nt:unstructured`) all&#39;interno della definizione `oak:index`.

L&#39;analizzatore predefinito per un indice è configurato nel nodo secondario `default` del nodo analizzatore.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Per un elenco degli analizzatori disponibili, consultate la documentazione API della versione Lucene in uso.

#### Specifica della classe analizzatore direttamente {#specifying-the-analyzer-class-directly}

Se desiderate utilizzare un analizzatore out-of-the-box, potete configurarlo seguendo la procedura seguente:

1. Individuare l&#39;indice con cui si desidera utilizzare l&#39;analizzatore sotto il nodo `oak:index`.

1. Sotto l&#39;indice, creare un nodo secondario denominato `default` di tipo `nt:unstructured`.

1. Aggiungere una proprietà al nodo predefinito con le seguenti proprietà:

   * **Nome:** `class`
   * **Tipo:** `String`
   * **Valore:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   Il valore è il nome della classe analizzatore che si desidera utilizzare.

   È inoltre possibile impostare l&#39;analizzatore da utilizzare con una versione lucene specifica utilizzando la proprietà di stringa opzionale `luceneMatchVersion`. Un sintax valido per utilizzarlo con Lucene 4.7 sarebbe:

   * **Nome:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valore:** `LUCENE_47`

   Se `luceneMatchVersion` non viene fornito, Oak utilizzerà la versione di Lucene con cui viene spedito.

1. Se si desidera aggiungere un file di stop words alle configurazioni dell&#39;analizzatore, è possibile creare un nuovo nodo sotto `default` uno con le seguenti proprietà:

   * **Nome:** `stopwords`
   * **Tipo:** `nt:file`

#### Creazione di analisi tramite composizione {#creating-analyzers-via-composition}

È inoltre possibile comporre gli analizzatori in base a `Tokenizers`, `TokenFilters` e `CharFilters`. A questo scopo, specificate un analizzatore e create nodi secondari dei relativi token e filtri facoltativi che verranno applicati nell&#39;ordine elencato. Vedere anche [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Considerate questa struttura di nodi come esempio:

* **Nome:** `analyzers`

   * **Nome:** `default`

      * **Nome:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `HTMLStrip`
         * **Nome:** `Mapping`
      * **Nome:** `tokenizer`

         * **Nome proprietà:** `name`

            * **Tipo:** `String`
            * **Valore:** `Standard`
      * **Nome:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `LowerCase`
         * **Nome:** `Stop`

            * **Nome proprietà:** `words`

               * **Tipo:** `String`
               * **Valore:** `stop1.txt, stop2.txt`
            * **Nome:** `stop1.txt`

               * **Tipo:** `nt:file`
            * **Nome:** `stop2.txt`

               * **Tipo:** `nt:file`





Il nome dei filtri, charFilters e token viene creato rimuovendo i suffissi di fabbrica. Pertanto:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` diventa  `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` diventa  `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` diventa  `Stop`

Qualsiasi parametro di configurazione richiesto per la fabbrica è specificato come proprietà del codice in questione.

Per casi come il caricamento di parole di arresto in cui è necessario caricare contenuto da file esterni, il contenuto può essere fornito creando un nodo figlio di tipo `nt:file` per il file in questione.

### Indice Solr {#the-solr-index}

Lo scopo dell&#39;indice Solr è principalmente la ricerca full-text, ma può anche essere utilizzato per indicizzare la ricerca per percorso, limitazioni delle proprietà e restrizioni del tipo primario. Ciò significa che l&#39;indice Solr in Oak può essere utilizzato per qualsiasi tipo di query JCR.

L&#39;integrazione in AEM avviene a livello di repository, in modo che Solr è uno dei possibili indici che possono essere utilizzati in Oak, la nuova implementazione del repository fornito con AEM.

Può essere configurato per funzionare come server incorporato con l&#39;istanza AEM o come server remoto.

### Configurazione di AEM con un server Solr incorporato {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>Non utilizzate un server Solr incorporato in un ambiente di produzione. Deve essere utilizzato solo in un ambiente di sviluppo.

AEM può essere utilizzato con un server Solr incorporato che può essere configurato tramite la console Web. In questo caso, il server Solr verrà eseguito nella stessa JVM dell&#39;istanza AEM a cui è incorporato.

È possibile configurare il server Solr incorporato tramite:

1. Passate alla console Web all&#39;indirizzo `https://serveraddress:4502/system/console/configMgr`
1. Cercare &quot;**Oak Solr server provider**&quot;.
1. Premere il pulsante di modifica e nella finestra seguente impostare il tipo di server su **Embedded Solr** nell&#39;elenco a discesa.

1. Quindi, modificare &quot;**Configurazione del server incorporato Oak Solr**&quot; e creare una configurazione. Per ulteriori informazioni sulle opzioni di configurazione, visitare il [sito Web Apache Solr](https://lucene.apache.org/solr/documentation.html).

   >[!NOTE]
   >
   >La configurazione della directory principale Solr (solr.home.path) cercherà una cartella con lo stesso nome nella cartella di installazione AEM.

1. Apri CRXDE e accedi come amministratore.
1. Aggiungete un nodo denominato **solrlndex** di tipo **quercia:QueryIndexDefinition** in **quercia:index** con le seguenti proprietà:

   * **type:** `solr`(di tipo String)
   * **asincrono:** `async`(di tipo String)
   * **reindex:** `true`(di tipo Boolean)

1. Salva le modifiche.

### Configurazione di AEM con un singolo server Solr remoto {#configuring-aem-with-a-single-remote-solr-server}

AEM anche essere configurato per l&#39;utilizzo con un&#39;istanza del server Solr remoto:

1. Scarica ed estrai la versione più recente di Solr. Per ulteriori informazioni su come eseguire questa operazione, consultare la [documentazione di installazione Apache Solr](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. Ora, create due truffe Solr. A tale scopo, potete creare delle cartelle per ogni condivisione nella cartella in cui è stato eseguito il upacked del file Solr:

   * Per la prima condivisione, create la cartella:

   `<solrunpackdirectory>\aemsolr1\node1`

   * Per la seconda condivisione, create la cartella:

   `<solrunpackdirectory>\aemsolr2\node2`

1. Individuate l&#39;istanza di esempio nel pacchetto Solr. In genere si trova in una cartella denominata &quot; `example`&quot; nella radice del pacchetto.
1. Copiate le cartelle seguenti dall&#39;istanza di esempio alle due cartelle condivise ( `aemsolr1\node1` e `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Create una nuova cartella denominata &quot; `cfg`&quot; in ciascuna delle due cartelle condivise.
1. Inserite i file di configurazione Solr e Zookeeper nelle cartelle appena create `cfg`.

   >[!NOTE]
   >
   >Per ulteriori informazioni sulla configurazione Solr e ZooKeeper, consultare la [documentazione di configurazione Solr](https://wiki.apache.org/solr/ConfiguringSolr) e la [Guida introduttiva di ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Avviare la prima condivisione con il supporto di ZooKeeper andando a `aemsolr1\node1` ed eseguendo il comando seguente:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Avviare la seconda condivisione andando in `aemsolr2\node2` ed eseguendo il comando seguente:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Dopo l&#39;avvio di entrambe le condivisioni, verificare che tutto sia pronto e funzionante collegandosi all&#39;interfaccia Solr in `http://localhost:8983/solr/#/`
1. Avviare AEM e passare alla console Web all&#39;indirizzo `http://localhost:4502/system/console/configMgr`
1. Impostate la seguente configurazione in **Configurazione del server remoto Oak Solr**:

   * URL HTTP solr: `http://localhost:8983/solr/`

1. Scegliere **Remote Solr** nell&#39;elenco a discesa in **Oak Solr** server provider.

1. Vai a CRXDE e accedi come amministratore.
1. Create un nuovo nodo denominato **solrIndex** in **quercia:index** e impostate le seguenti proprietà:

   * **type:** solr (di tipo String)
   * **asincrono:** asincrono (di tipo String)
   * **reindex:** true (di tipo Boolean)

1. Salva le modifiche.

#### Configurazione consigliata per Solr {#recommended-configuration-for-solr}

Di seguito è riportato un esempio di configurazione di base che può essere utilizzata con tutte e tre le distribuzioni Solr descritte in questo articolo. Contiene gli indici delle proprietà dedicate già presenti in AEM e non devono essere utilizzati con altre applicazioni.

Per utilizzarlo correttamente, è necessario inserire il contenuto dell&#39;archivio direttamente nella directory principale Solr. Nel caso di distribuzioni con più nodi, dovrebbe trovarsi direttamente nella cartella principale di ciascun nodo.

File di configurazione Solr consigliati

[Ottieni file](assets/recommended-conf.zip)

### Strumenti di indicizzazione AEM {#aem-indexing-tools}

AEM 6.1 integra inoltre due strumenti di indicizzazione presenti in AEM 6.0 come parte del set di strumenti  Adobe Consulting Services Commons:

1. **Spiega query**, uno strumento progettato per aiutare gli amministratori a capire come vengono eseguite le query;
1. **Oak Index Manager**, un&#39;interfaccia utente Web per mantenere gli indici esistenti.

È ora possibile raggiungerli andando a **Strumenti - Operazioni - Dashboard - Diagnosi** dalla schermata di benvenuto AEM.

Per ulteriori informazioni su come utilizzarle, consultare la [documentazione del dashboard operativo](/help/sites-administering/operations-dashboard.md).

#### Creazione di indici di proprietà tramite OSGi {#creating-property-indexes-via-osgi}

Il pacchetto ACS Commons espone anche le configurazioni OSGi che possono essere utilizzate per creare indici di proprietà.

È possibile accedervi dalla console Web cercando &quot;**Assicurarsi che l&#39;indice delle proprietà Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Risoluzione dei problemi di indicizzazione {#troubleshooting-indexing-issues}

Le situazioni possono verificarsi quando l&#39;esecuzione delle query richiede molto tempo e il tempo generale di risposta del sistema è lento.

Questa sezione presenta una serie di raccomandazioni sulle azioni da intraprendere per individuare la causa di tali problemi e consigli su come risolverli.

#### Preparazione delle informazioni di debug per l&#39;analisi {#preparing-debugging-info-for-analysis}

Il modo più semplice per ottenere le informazioni necessarie per la query da eseguire è tramite lo strumento [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query). Questo consente di raccogliere le informazioni precise necessarie per eseguire il debug di una query lenta senza dover consultare le informazioni relative al livello di registro. Questa operazione è consigliabile se si conosce la query di cui si sta eseguendo il debug.

Se questo non è possibile per qualsiasi motivo, è possibile raccogliere i registri di indicizzazione in un unico file e utilizzarli per risolvere il problema specifico.

#### Abilita registrazione {#enable-logging}

Per abilitare la registrazione, è necessario abilitare i registri di livello **DEBUG** per le categorie relative all&#39;indicizzazione e alle query Oak. Queste categorie sono:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La categoria **com.day.cq.search** è applicabile solo se si utilizza l&#39;utility QueryBuilder AEM fornita.

>[!NOTE]
>
>È importante che i file di registro siano impostati su DEBUG solo per la durata dell’esecuzione della query di cui si desidera eseguire la risoluzione dei problemi. In caso contrario, nel corso del tempo verrà generata una grande quantità di eventi nei registri. Per questo motivo, una volta raccolti i registri richiesti, tornate alla registrazione di livello INFO per le categorie sopra menzionate.

È possibile attivare la registrazione seguendo questa procedura:

1. Posizionate il browser su `https://serveraddress:port/system/console/slinglog`
1. Fare clic sul pulsante **Aggiungi nuovo logger** nella parte inferiore della console.
1. Nella riga appena creata, aggiungete le categorie sopra indicate. È possibile utilizzare il simbolo **+** per aggiungere più categorie a un singolo logger.
1. Scegliere **DEBUG** dall&#39;elenco a discesa **Livello di registro**.
1. Impostate il file di output su `logs/queryDebug.log`. Questo metterà in correlazione tutti gli eventi DEBUG in un unico file di registro.
1. Eseguire la query o eseguire il rendering della pagina che utilizza la query di cui si desidera eseguire il debug.
1. Dopo aver eseguito la query, tornate alla console di registrazione e modificate il livello di registro del nuovo logger in **INFO**.

#### Configurazione indice {#index-configuration}

La modalità di valutazione della query dipende in larga misura dalla configurazione dell&#39;indice. È importante ottenere la configurazione dell&#39;indice per poter essere analizzata o inviata al supporto. Potete ottenere la configurazione come pacchetto di contenuti o una rappresentazione JSON.

Poiché nella maggior parte dei casi, la configurazione di indicizzazione è memorizzata nel nodo `/oak:index` in CRXDE, è possibile ottenere la versione JSON in:

`https://serveraddress:port/oak:index.tidy.-1.json`

Se l&#39;indice è configurato in una posizione diversa, modificare il percorso di conseguenza.

#### Uscita MBean {#mbean-output}

In alcuni casi è utile fornire l&#39;output di MBeans relativi all&#39;indice per il debug. È possibile eseguire questa operazione tramite:

1. Passate alla console JMX in:
   `https://serveraddress:port/system/console/jmx`

1. Cercate i seguenti MBeans:

   * Statistiche indice Lucene
   * Statistiche di supporto di CopyOnRead
   * Statistiche query Oak
   * IndexStats

1. Fare clic su ciascuno dei MBeans per ottenere le statistiche sulle prestazioni. Create uno screenshot o prendete nota di questi elementi qualora sia necessario inviarli per il supporto.

Puoi anche ottenere la variante JSON di queste statistiche ai seguenti URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

È inoltre possibile fornire un output JMX consolidato tramite `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Questo includerebbe tutti i dettagli MBean correlati a Oak nel formato JSON.

#### Altri dettagli {#other-details}

Potete raccogliere ulteriori dettagli per facilitare la risoluzione del problema, ad esempio:

1. La versione Oak su cui l&#39;istanza è in esecuzione. Per visualizzarlo, aprite CRXDE e guardate la versione nell&#39;angolo inferiore destro della pagina di benvenuto, oppure verificate la versione del bundle `org.apache.jackrabbit.oak-core`.
1. L&#39;output del debugger di QueryBuilder della query del problema. È possibile accedere al debugger all&#39;indirizzo: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

