---
title: Risoluzione dei problemi relativi a query lente
seo-title: Risoluzione dei problemi relativi a query lente
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 6d8680bcfb03197ac33bc7efb0e40796e38fef20
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 0%

---


# Risoluzione dei problemi relativi a query lente{#troubleshooting-slow-queries}

## Classificazioni query lente {#slow-query-classifications}

Sono disponibili 3 principali classificazioni di query lente in AEM, elencate per gravità:

1. **Query senza indice**

   * Query che **non** si risolvono in un indice e attraversano il contenuto del JCR per raccogliere i risultati

1. **Query limitate (o con ambito) scadenti**

   * Query che si risolvono in un indice, ma che devono scorrere tutte le voci di indice per raccogliere i risultati

1. **Query set di risultati di grandi dimensioni**

   * Query che restituiscono un numero molto elevato di risultati

Le prime 2 classificazioni di query (senza indice e con restrizioni limitate) sono lente, perché forzano il motore di query Oak a ispezionare ogni risultato **potenziale** (nodo di contenuto o voce di indice) per identificare quale appartiene al set di risultati **effettivo** .

L&#39;ispezione di ogni potenziale risultato è ciò che viene chiamato Traversing.

Poiché ogni potenziale risultato deve essere analizzato, il costo per determinare il set di risultati effettivo cresce in modo lineare con il numero di potenziali risultati.

L&#39;aggiunta di restrizioni di query e indici di ottimizzazione consente di memorizzare i dati di indice in un formato ottimizzato che consenta un rapido recupero dei risultati e riduce o elimina la necessità di un controllo lineare dei set di risultati potenziali.

In AEM 6.3, per impostazione predefinita, quando viene raggiunto un attraversamento di 100.000, la query ha esito negativo e genera un&#39;eccezione. Questo limite non esiste per impostazione predefinita nelle versioni AEM precedenti alla AEM 6.3, ma può essere impostato tramite la configurazione OSGi delle impostazioni del motore di query Apache Jackrabbit e il fagiolo JMX QueryEngineSettings (proprietà LimitReads).

### Rilevamento di query senza indice {#detecting-index-less-queries}

#### Durante lo sviluppo {#during-development}

Spiegare **tutte** le **query e assicurarsi che i relativi piani di query non contengano il/&amp;ast; traversa** la spiegazione. Esempio di piano query di navigazione:

* **PIANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Post-distribuzione {#post-deployment}

* Monitorate le query `error.log` trasversali senza indice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Questo messaggio viene registrato solo se non è disponibile alcun indice e se la query attraversa potenzialmente molti nodi. I messaggi non vengono registrati se è disponibile un indice, ma la quantità da scorrere è piccola e quindi veloce.

* Visitate la console delle operazioni [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) AEM e [spiegate](/help/sites-administering/operations-dashboard.md#explain-query) le query lente alla ricerca di spiegazioni incrociate o senza query indice.

### Rilevamento Di Query Limitate {#detecting-poorly-restricted-queries}

#### Durante lo sviluppo {#during-development-1}

Spiegare tutte le query e assicurarsi che vengano risolte in un indice sintonizzato in modo che corrispondano alle restrizioni di proprietà della query.

* La copertura del piano query ideale include tutte le restrizioni `indexRules` di proprietà e almeno le restrizioni di proprietà più restrittive nella query.
* Le query che ordinano i risultati devono essere risolte in un indice delle proprietà Lucene con regole di indice per le proprietà ordinate per quelle impostate `orderable=true.`

#### Ad esempio, l&#39;impostazione predefinita `cqPageLucene` non dispone di una regola di indice per `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Prima di aggiungere la regola di indice cq:tags

* **cq:tags, regola di indice**

   * Non esiste fuori dalla casella

* **Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Piano query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Questa query corrisponde all&#39; `cqPageLucene` indice, ma poiché non esiste alcuna regola di indice delle proprietà per `jcr:content` o `cq:tags`, quando viene valutata questa restrizione, ogni record nell&#39; `cqPageLucene` indice viene controllato per determinare una corrispondenza. Ciò significa che se l&#39;indice contiene 1 milione di `cq:Page` nodi, vengono controllati 1 milione di record per determinare il set di risultati.

Dopo l&#39;aggiunta della regola di indice cq:tags

* **cq:tags, regola di indice**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **Piano query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

L&#39;aggiunta di indexRule per `jcr:content/cq:tags` nell&#39; `cqPageLucene` indice consente di memorizzare `cq:tags` i dati in modo ottimizzato.

Quando viene eseguita una query con la `jcr:content/cq:tags` restrizione, l&#39;indice può cercare i risultati per valore. Ciò significa che se 100 `cq:Page` nodi hanno `myTagNamespace:myTag` come valore, vengono restituiti solo quei 100 risultati, e gli altri 999.000 sono esclusi dai controlli di restrizione, migliorando le prestazioni di un fattore di 10.000.

Naturalmente, ulteriori limitazioni delle query riducono i set di risultati idonei e ottimizzano ulteriormente l&#39;ottimizzazione delle query.

Allo stesso modo, senza una regola di indice aggiuntiva per la `cq:tags` proprietà, anche una query full-text con una restrizione su `cq:tags` non avrebbe funzionato correttamente, in quanto i risultati dell&#39;indice restituirebbero tutte le corrispondenze full-text. La restrizione relativa ai tag cq:tags viene filtrata dopo di essa.

Un&#39;altra causa del filtraggio post-indice è l&#39;Access Control Lists, che spesso viene persa durante lo sviluppo. Assicurarsi che la query non restituisca percorsi che potrebbero essere inaccessibili all&#39;utente. Questa operazione può essere eseguita in genere mediante una migliore struttura del contenuto e l&#39;indicazione di limitazioni rilevanti del percorso della query.

Un modo utile per identificare se l&#39;indice di Lucene sta restituendo molti risultati per restituire un sottoinsieme molto piccolo come risultato della query è quello di abilitare i registri DEBUG per `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` e vedere quanti documenti vengono caricati dall&#39;indice. Il numero di risultati finali rispetto al numero di documenti caricati non dovrebbe essere sproporzionato. For more information, see [Logging](/help/sites-deploying/configure-logging.md).

#### Post-distribuzione {#post-deployment-1}

* Monitorare le query `error.log` di attraversamento:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visitate la console delle operazioni AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) e [Spiegate](/help/sites-administering/operations-dashboard.md#explain-query) le query lente alla ricerca di piani di query che non risolvono le restrizioni delle proprietà query alle regole delle proprietà di indice.

### Rilevamento di query con set di risultati di grandi dimensioni {#detecting-large-result-set-queries}

#### Durante lo sviluppo {#during-development-2}

Impostare soglie basse per oak.queryLimitInMemory (ad esempio 10000) e oak.queryLimitReads (ad esempio 5000) e ottimizzare la query costosa quando si tocca un UnsupportedOperationException che dice &quot;La query ha letto più di x nodi...&quot;

In questo modo si evitano le query che richiedono molte risorse (ad es. non sostenuto da alcun indice o sostenuto da un indice di copertura inferiore). Ad esempio, una query che legge nodi 1M porterebbe a molti IO e avrebbe un impatto negativo sulle prestazioni complessive dell&#39;applicazione. Pertanto, qualsiasi query che non riesce a causa di limiti superiori deve essere analizzata e ottimizzata.

#### Post-distribuzione {#post-deployment-2}

* Monitorare i registri per le query che attivano il consumo di memoria heap di grandi nodi: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizzare la query per ridurre il numero di nodi attraversati

* Monitorare i registri per le query che attivano un grande consumo di memoria heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizzare la query per ridurre il consumo di memoria heap

Per le versioni AEM 6.0 - 6.2, è possibile ottimizzare la soglia per l&#39;attraversamento dei nodi tramite i parametri JVM nello script di avvio AEM per evitare che le query di grandi dimensioni sovraccarichino l&#39;ambiente. I valori consigliati sono:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri di cui sopra sono preconfigurati per impostazione predefinita e possono essere modificati tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ottimizzazione delle prestazioni delle query {#query-performance-tuning}

Il motto dell&#39;ottimizzazione delle prestazioni della query in AEM è:

**&quot;Più restrizioni, meglio è.&quot;**

Di seguito sono riportati gli adeguamenti consigliati per garantire le prestazioni della query. Innanzitutto, sintonizzate la query, un&#39;attività meno intrusiva e, se necessario, regolate le definizioni di indice.

### Adeguamento dell&#39;istruzione Query {#adjusting-the-query-statement}

AEM supporta le seguenti lingue di query:

* Query Builder
* JCR-SQL2
* XPath

Nell&#39;esempio seguente viene utilizzato Query Builder in quanto è il linguaggio di query più comune utilizzato dagli sviluppatori AEM, tuttavia gli stessi principi sono applicabili a JCR-SQL2 e XPath.

1. Aggiungete una restrizione relativa al tipo di nodo in modo che la query corrisponda a un indice esistente della proprietà Lucene.

* **Query non ottimizzata**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query ottimizzata**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   Query prive di una forza di restrizione del tipo di nodo AEM assumere il `nt:base` tipo di nodo, di cui ogni nodo in AEM è un sottotipo, che di fatto non determina alcuna limitazione del tipo di nodo.

   L&#39;impostazione `type=cq:Page` limita questa query ai soli `cq:Page` nodi e risolve la query a AEM cqPageLucene, limitando i risultati a un sottoinsieme di nodi (solo `cq:Page` nodi) in AEM.

1. Regolare la limitazione del tipo di nodo della query in modo che la query corrisponda a un indice esistente della proprietà Lucene.

* **Query non ottimizzata**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query ottimizzata**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` è il tipo di nodo padre di `cq:Page`, e supponendo `jcr:content/contentType=article-page` sia applicato solo ai `cq:Page` nodi tramite la nostra applicazione personalizzata, questa query restituirà solo `cq:Page` nodi dove `jcr:content/contentType=article-page`. Questa è una restrizione non ottimale, però, perché:

   * Un altro nodo eredita da `nt:hierarchyNode` (ad esempio `dam:Asset`) aggiunta non necessaria al set di risultati potenziali.
   * Non esiste un indice AEM fornito per `nt:hierarchyNode`, tuttavia, in quanto esiste un indice fornito per `cq:Page`.
   L&#39;impostazione `type=cq:Page` limita questa query ai soli `cq:Page` nodi e risolve la query a AEM cqPageLucene, limitando i risultati a un sottoinsieme di nodi (solo nodi cq:Page) in AEM.

1. In alternativa, regolate le restrizioni delle proprietà in modo che la query corrisponda a un indice delle proprietà esistente.

* **Query non ottimizzata**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query ottimizzata**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   Modificando la restrizione delle proprietà da `jcr:content/contentType` (un valore personalizzato) a una proprietà nota, la query `sling:resourceType` consente di risolvere l&#39;indice delle proprietà `slingResourceType` che indicizza tutto il contenuto per `sling:resourceType`.

   Gli indici delle proprietà (a differenza degli indici delle proprietà Lucene) vengono utilizzati al meglio quando la query non viene visualizzata per tipo di nodo e una singola limitazione di proprietà domina il set di risultati.

1. Aggiungete alla query il limite più restrittivo possibile per il percorso. Ad esempio, preferisci `/content/my-site/us/en` over `/content/my-site`, o `/content/dam` over `/`.

* **Query non ottimizzata**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query ottimizzata**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   L&#39;ambito della limitazione del percorso `path=/content`per `path=/content/my-site/us/en` consentire agli indici di ridurre il numero di voci indice da ispezionare. Quando la query può limitare il percorso molto bene, oltre solo `/content` o `/content/dam`, assicurarsi che l&#39;indice sia `evaluatePathRestrictions=true`.

   Nota: l&#39;utilizzo `evaluatePathRestrictions` aumenta la dimensione dell&#39;indice.

1. Quando possibile, evitare funzioni/operazioni di query quali: `LIKE` e `fn:XXXX` come i loro costi si adattano al numero di risultati basati sulle restrizioni.

* **Query non ottimizzata**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **Query ottimizzata**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   La condizione LIKE è lenta da valutare perché non è possibile utilizzare alcun indice se il testo inizia con un carattere jolly (&quot;%...&quot;). La condizione jcr:contains consente l&#39;uso di un indice full-text, ed è pertanto preferita. Ciò richiede che l&#39;indice delle proprietà Lucene risolto disponga di indexRule per `jcr:content/contentType` con `analayzed=true`.

   L&#39;utilizzo di funzioni di query come `fn:lowercase(..)` può essere più difficile da ottimizzare in quanto non esistono equivalenti più veloci (al di fuori di configurazioni di analizzatore indice più complesse e obtrusive). È consigliabile identificare altre limitazioni di ambito per migliorare le prestazioni complessive della query, richiedendo che le funzioni operino sulla più piccola serie di risultati potenziali possibili.

1. ***Questa regolazione è specifica di Query Builder e non si applica a JCR-SQL2 o XPath.***

   Utilizzate [Query Builder&#39;Total](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) quando l&#39;intero set di risultati **non** è immediatamente necessario.

   * **Query non ottimizzata**

      ```js
      type=cq:Page
      path=/content
      ```

   * **Query ottimizzata**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   Per i casi in cui l&#39;esecuzione delle query è rapida ma il numero di risultati è elevato, p. `guessTotal` è un&#39;ottimizzazione critica per le query di Query Builder.

   `p.guessTotal=100` comunica a Query Builder di raccogliere solo i primi 100 risultati e imposta un flag booleano che indica se esistono almeno un altro risultato (ma non quanti altri risultati, in quanto contando questo numero si verificherebbe un rallentamento). Questa ottimizzazione è eccezionale per l’impaginazione o per infiniti casi di utilizzo del caricamento, in cui solo un sottoinsieme di risultati viene visualizzato in modo incrementale.

## Sintonizzazione indice esistente {#existing-index-tuning}

1. Se la query ottimale viene risolta in un Indice proprietà, non rimane nulla da fare in quanto gli indici delle proprietà sono minimamente sintonizzabili.
1. In caso contrario, la query deve essere risolta in un indice delle proprietà Lucene. Se non è possibile risolvere alcun indice, passare a Creazione di un nuovo indice.
1. Se necessario, convertire la query in XPath o JCR-SQL2.

   * **Query Builder**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath generato dalla query Query Builder**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. Fornire l&#39;XPath (o JCR-SQL2) al generatore [di definizione dell&#39;indice](https://oakutils.appspot.com/generate/index) Oak per generare la definizione ottimizzata dell&#39;indice di proprietà Lucene.

   **Definizione indice proprietà Lucene generata**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. Unisci manualmente la definizione generata nell&#39;indice esistente delle proprietà Lucene in modo additivo. Prestate attenzione a non rimuovere le configurazioni esistenti in quanto potrebbero essere utilizzate per soddisfare altre query.

   1. Individuate l&#39;indice delle proprietà Lucene esistente che copre cq:Page (utilizzando la funzione di gestione dell&#39;indice). In questo caso, `/oak:index/cqPageLucene`.
   1. Identificare il delta di configurazione tra la definizione dell&#39;indice ottimizzata (Passaggio 4) e l&#39;indice esistente (/oak:index/cqPageLucene), quindi aggiungere le configurazioni mancanti dall&#39;indice ottimizzato alla definizione dell&#39;indice esistente.
   1. Per AEM Best practice di reindicizzazione, è possibile aggiornare o reindicizzare in ordine, in base al fatto che il contenuto esistente verrà influenzato da questa modifica alla configurazione dell&#39;indice.

## Crea nuovo indice {#create-a-new-index}

1. Verificare che la query non venga risolta in un indice delle proprietà Lucene esistente. In caso contrario, vedere la sezione precedente sull&#39;ottimizzazione e l&#39;indice esistente.
1. Se necessario, convertire la query in XPath o JCR-SQL2.

   * **Query Builder**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath generato dalla query Query Builder**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Fornire l&#39;XPath (o JCR-SQL2) al generatore [di definizione dell&#39;indice](https://oakutils.appspot.com/generate/index) Oak per generare la definizione ottimizzata dell&#39;indice di proprietà Lucene.

   **Definizione indice proprietà Lucene generata**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. Distribuisci la definizione dell&#39;indice delle proprietà Lucene generato.

   Aggiungete la definizione XML fornita da Oak Index Definition Generator per il nuovo indice al progetto AEM che gestisce le definizioni dell&#39;indice Oak (ricordate, considera le definizioni dell&#39;indice Oak come codice, dal momento che il codice dipende da esse).

   Distribuire e testare il nuovo indice seguendo il normale ciclo di vita AEM sviluppo software e verificare che la query sia risolta nell&#39;indice e che la query sia performante.

   Dopo la distribuzione iniziale di questo indice, AEM comporrà l&#39;indice con i dati richiesti.

## Quando sono OK le query senza indice e traversal? {#when-index-less-and-traversal-queries-are-ok}

A causa AEM architettura flessibile dei contenuti, è difficile prevedere e garantire che l&#39;attraversamento delle strutture dei contenuti non evolva nel tempo fino a raggiungere dimensioni inaccettabili.

Pertanto, assicurarsi che gli indici soddisfino le query, a meno che la combinazione di restrizione percorso e restrizione nodetype garantisca che **meno di 20 nodi vengano mai attraversati.**

## Strumenti di sviluppo query {#query-development-tools}

###  Adobe supportato {#adobe-supported}

* **Debugger Query Builder**

   * Interfaccia Web per l&#39;esecuzione di query Query Builder e per generare l&#39;XPath di supporto (da utilizzare in Generatore di definizione di query o indice Oak).
   * AEM all&#39;indirizzo [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Strumento Query**

   * Interfaccia Web per l&#39;esecuzione di query XPath e JCR-SQL2.
   * AEM in [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Strumenti > Query...

* **[Spiega query](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Pannello Operazioni AEM che fornisce una spiegazione dettagliata (piano query, tempo query e numero di risultati) per qualsiasi query XPATH o JCR-SQL2 specificata.

* **[Query lente/popolari](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Una dashboard delle operazioni AEM che elenca le query lente e popolari recenti eseguite su AEM.

* **[Gestione indice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM Operations WebUI che visualizza gli indici sull&#39;istanza AEM; facilita la comprensione degli indici già esistenti, che possono essere mirati o incrementati.

* **[Registrazione](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registrazione di Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registrazione esecuzione query Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configurazione OSGi delle impostazioni del motore di query Apache Jackrabbit**

   * Configurazione OSGi che configura il comportamento di errore per l’attraversamento delle query.
   * Situato su AEM in [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX**

   * MBean JMX utilizzato per stimare il numero di nodi nelle strutture ad albero del contenuto in AEM.
   * Posizionato su AEM in [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Community supportata {#community-supported}

* **[Generatore definizione indice Oak](https://oakutils.appspot.com/generate/index)**

   * Generare un indice di proprietà di Lucence ottimale dalle istruzioni di query XPath o JCR-SQL2.

* **[Plug-in AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Estensione del browser Web Google Chrome che espone i dati di registro per ogni richiesta, incluse le query eseguite e i relativi piani di query, nella console degli strumenti di sviluppo del browser.
   * Richiede [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) per essere installato e attivato su AEM.
