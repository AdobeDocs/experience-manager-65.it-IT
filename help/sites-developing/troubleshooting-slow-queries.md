---
title: Risoluzione dei problemi relativi alle query lente
seo-title: Troubleshooting Slow Queries
description: Risoluzione dei problemi relativi alle query lente
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 0%

---

# Risoluzione dei problemi relativi alle query lente{#troubleshooting-slow-queries}

## Classificazioni query lente {#slow-query-classifications}

Ci sono tre classificazioni principali di query lente in AEM, elencate per gravità:

1. **Query senza indice**

   * Query che eseguono **not** risolvi in un indice e attraversa il contenuto del JCR per raccogliere i risultati

1. **Query con restrizioni (o con ambito) scadenti**

   * Query che si risolvono in un indice, ma devono attraversare tutte le voci di indice per raccogliere i risultati

1. **Query set di risultati di grandi dimensioni**

   * Query che restituiscono un numero elevato di risultati

Le prime due classificazioni di query (senza indice e con restrizioni limitate) sono lente. Sono lenti perché forzano il motore di query Oak a ispezionare ogni **potenziale** risultato (nodo di contenuto o voce di indice) per identificare quali appartengono nel **effettivo** set di risultati.

L&#39;atto di ispezionare ogni potenziale risultato è quello che viene chiamato Traversing.

Poiché ogni risultato potenziale deve essere esaminato, il costo per determinare il set di risultati effettivo cresce in modo lineare con il numero di risultati potenziali.

L’aggiunta di restrizioni alle query e indici di ottimizzazione consente di memorizzare i dati di indice in un formato ottimizzato che consenta un rapido recupero dei risultati e riduce o elimina la necessità di un’ispezione lineare dei potenziali set di risultati.

In AEM 6.3, per impostazione predefinita, quando viene raggiunto un attraversamento di 100.000, la query non riesce e genera un&#39;eccezione. Questo limite non esiste per impostazione predefinita nelle versioni AEM precedenti AEM 6.3, ma può essere impostato tramite la configurazione OSGi delle impostazioni del motore di query Apache Jackrabbit e il fagiolo JMX QueryEngineSettings (proprietà LimitReads).

### Rilevamento di query senza indice {#detecting-index-less-queries}

#### Durante lo sviluppo {#during-development}

Spiegare **tutto** invia query e assicurati che i relativi piani di query non contengano **/&amp;ast; traverse** spiegazione in loro. Esempio di attraversamento del piano di query:

* **PIANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Post-distribuzione {#post-deployment}

* Monitorare `error.log` per le query traversal senza indice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Questo messaggio viene registrato solo se non è disponibile alcun indice e se la query attraversa potenzialmente molti nodi. I messaggi non vengono registrati se è disponibile un indice, ma la quantità da attraversare è piccola e quindi veloce.

* Visita il AEM [Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance) console operativa e [Spiegare](/help/sites-administering/operations-dashboard.md#explain-query) query lente alla ricerca di spiegazioni di query traversal o senza indicizzazione.

### Rilevamento di query con restrizioni errate {#detecting-poorly-restricted-queries}

#### Durante lo sviluppo {#during-development-1}

Spiega tutte le query e assicurati che vengano risolte in un indice sintonizzato in modo da corrispondere alle restrizioni di proprietà della query.

* Copertura del piano di query ideale `indexRules` per tutte le restrizioni di proprietà e almeno per le restrizioni di proprietà più restrittive nella query.
* Le query che ordinano i risultati devono essere risolte in un indice di proprietà Lucene con regole di indice per le proprietà ordinate per che sono impostate `orderable=true.`

#### Ad esempio, il valore predefinito `cqPageLucene` non dispone di una regola di indice per `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Prima di aggiungere la regola di indice cq:tags

* **cq:tags Regola indice**

   * Non esiste

* **Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Piano query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Questa query viene risolta nella `cqPageLucene` indice, ma perché non esiste alcuna regola dell&#39;indice di proprietà per `jcr:content` o `cq:tags`, quando viene valutata questa restrizione, ogni record nel `cqPageLucene` viene controllato per determinare una corrispondenza. Di conseguenza, se l&#39;indice contiene 1 milione `cq:Page` poi vengono controllati 1 milione di record per determinare il set di risultati.

Dopo aver aggiunto la regola di indice cq:tags

* **cq:tags Regola indice**

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

L&#39;aggiunta di indexRule per `jcr:content/cq:tags` in `cqPageLucene` index `cq:tags` dati da memorizzare in modo ottimizzato.

Quando una query contiene `jcr:content/cq:tags` restrizione viene eseguita, l&#39;indice può cercare i risultati per valore. Ciò significa che se 100 `cq:Page` i nodi `myTagNamespace:myTag` come valore, vengono restituiti solo i 100 risultati e gli altri 999.000 sono esclusi dai controlli di restrizione, migliorando le prestazioni di un fattore di 10.000.

Ulteriori restrizioni alle query riducono i set di risultati idonei e ottimizzano ulteriormente l’ottimizzazione delle query.

Allo stesso modo, senza una regola di indice aggiuntiva per `cq:tags` proprietà , anche una query full-text con una limitazione su `cq:tags` avrebbe prestazioni sbagliate in quanto i risultati dell&#39;indice restituirebbero tutte le corrispondenze a testo intero. La restrizione su cq:tags verrebbe filtrata dopo di essa.

Un&#39;altra causa del filtraggio post-indice è l&#39;accesso agli elenchi di controllo che spesso viene mancato durante lo sviluppo. Assicurati che la query non restituisca percorsi che potrebbero essere inaccessibili all’utente. A tal fine è possibile migliorare la struttura del contenuto e fornire pertinenti limitazioni del percorso nella query.

Un modo utile per identificare se l&#39;indice Lucene sta restituendo molti risultati per restituire un piccolo sottoinsieme come risultato della query, è quello di abilitare i log DEBUG per `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. In questo modo è possibile vedere quanti documenti vengono caricati dall&#39;indice. Il numero di risultati finali rispetto al numero di documenti caricati non dovrebbe essere sproporzionato. Per ulteriori informazioni, consulta [Registrazione](/help/sites-deploying/configure-logging.md).

#### Post-distribuzione {#post-deployment-1}

* Monitorare `error.log` per le query traversal:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visita il AEM [Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance) console operativa e [Spiegare](/help/sites-administering/operations-dashboard.md#explain-query) query lente alla ricerca di piani di query che non risolvono le restrizioni di proprietà query alle regole di proprietà dell&#39;indice.

### Rilevamento di query con set di risultati di grandi dimensioni {#detecting-large-result-set-queries}

#### Durante lo sviluppo {#during-development-2}

Imposta soglie basse per oak.queryLimitInMemory (ad esempio, 10000) e oak.queryLimitReads (ad esempio, 5000) e ottimizza la query costosa quando raggiungi un UnsupportedOperationException dicendo &quot;La query legge più di x nodi..&quot;.

L&#39;impostazione di soglie basse aiuta a evitare le query ad alta intensità di risorse (ovvero, non supportate da alcun indice o supportate da un indice di copertura inferiore). Ad esempio, una query che legge un milione di nodi porterebbe a un sacco di IO e avrebbe un impatto negativo sulle prestazioni complessive dell&#39;applicazione. Quindi qualsiasi query che non riesce a causa dei limiti sopra indicati deve essere analizzata e ottimizzata.

#### Post-distribuzione {#post-deployment-2}

* Monitora i log per le query che attivano il consumo di memoria heap di grandi nodi o traversal di grandi dimensioni : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizza la query in modo da ridurre il numero di nodi attraversati.

* Monitora i registri per le query che attivano un grande consumo di memoria heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizza la query in modo da ridurre il consumo di memoria heap.

Per le versioni AEM 6.0 - 6.2, è possibile ottimizzare la soglia per l&#39;attraversamento dei nodi tramite i parametri JVM nello script di avvio AEM per evitare che le query di grandi dimensioni sovraccarichino l&#39;ambiente. I valori consigliati sono :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri di cui sopra sono preconfigurati per impostazione predefinita e possono essere modificati tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ottimizzazione delle prestazioni delle query {#query-performance-tuning}

Il motto dell’ottimizzazione delle prestazioni delle query in AEM è:

**&quot;Più restrizioni, meglio è.&quot;**

Di seguito sono riportati gli adeguamenti consigliati per garantire le prestazioni della query. Prima regola la query, un&#39;attività meno invasiva e poi, se necessario, regola le definizioni degli indici.

### Adeguamento dell’istruzione query {#adjusting-the-query-statement}

AEM supporta i seguenti linguaggi di query:

* Query Builder
* JCR-SQL2
* XPath

Nell&#39;esempio seguente viene utilizzato Query Builder in quanto è il linguaggio di query più comune utilizzato dagli sviluppatori AEM, tuttavia gli stessi principi sono applicabili a JCR-SQL2 e XPath.

1. Aggiungi una restrizione del tipo di nodo in modo che la query venga risolta in un indice della proprietà Lucene esistente.

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

   Query prive di una forza di restrizione di tipo nodetype AEM per assumere la `nt:base` nodetype, di cui ogni nodo in AEM è un sottotipo, con conseguente assenza di restrizioni relative al nodetype.

   Impostazione `type=cq:Page` limita questa query a `cq:Page` e risolve la query in AEM cqPageLucene, limitando i risultati a un sottoinsieme di nodi (solo `cq:Page` nodi) in AEM.

1. Regola la restrizione del tipo di nodo della query in modo che la query venga risolta in un indice di proprietà Lucene esistente.

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

   `nt:hierarchyNode` è il tipo di nodo padre di `cq:Page`. Supponendo `jcr:content/contentType=article-page` viene applicato solo a `cq:Page` nodi tramite l&#39;applicazione personalizzata di Adobe, questa query restituisce solo `cq:Page` nodi in cui `jcr:content/contentType=article-page`. Questo flusso è comunque una restrizione non ottimale, perché:

   * Altri nodi ereditano da `nt:hierarchyNode` (ad esempio, `dam:Asset`) aggiungendo inutilmente al set di potenziali risultati.
   * Nessun indice fornito AEM esiste per `nt:hierarchyNode`, tuttavia, in quanto esiste un indice fornito per `cq:Page`.
   Impostazione `type=cq:Page` limita questa query a `cq:Page` e risolve la query in AEM cqPageLucene, limitando i risultati in un sottoinsieme di nodi (solo nodi cq:Page) in AEM.

1. In alternativa, regola le restrizioni di proprietà in modo che la query venga risolta in un indice di proprietà esistente.

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

   Modifica della restrizione della proprietà da `jcr:content/contentType` (un valore personalizzato) per la proprietà nota `sling:resourceType` consente la risoluzione della query sull&#39;indice delle proprietà `slingResourceType` che indicizza tutto il contenuto per `sling:resourceType`.

   Gli indici delle proprietà (a differenza degli indici delle proprietà Lucene) vengono utilizzati al meglio quando la query non viene rilevata per tipo di nodo e una singola restrizione delle proprietà domina il set di risultati.

1. Aggiungi alla query la restrizione più restrittiva possibile al percorso. Ad esempio, preferisci `/content/my-site/us/en` over `/content/my-site`oppure `/content/dam` over `/`.

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

   Applicazione dell’ambito alla restrizione del percorso `path=/content`a `path=/content/my-site/us/en` consente agli indici di ridurre il numero di voci di indice che devono essere ispezionate. Quando la query può limitare bene il percorso, oltre `/content` o `/content/dam`, assicurati che l&#39;indice `evaluatePathRestrictions=true`.

   Nota che utilizza `evaluatePathRestrictions` aumenta la dimensione dell&#39;indice.

1. Se possibile, evita funzioni di query e operazioni di query quali: `LIKE` e `fn:XXXX` poiché i loro costi variano in base al numero di risultati basati sulle restrizioni.

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

   La condizione LIKE è lenta da valutare perché non è possibile utilizzare alcun indice se il testo inizia con un carattere jolly (&quot;%...&quot;). La condizione jcr:contains consente di utilizzare un indice fulltext ed è pertanto preferita. Richiede che l&#39;indice di proprietà Lucene risolto abbia indexRule per `jcr:content/contentType` con `analayzed=true`.

   Utilizzo di funzioni di query come `fn:lowercase(..)` può essere più difficile da ottimizzare in quanto non ci sono equivalenti più veloci (al di fuori delle configurazioni più complesse e intrusive dell&#39;analizzatore dell&#39;indice). È consigliabile identificare altre restrizioni dell&#39;ambito per migliorare le prestazioni complessive della query, richiedendo alle funzioni di funzionare sul set più piccolo possibile di risultati potenziali.

1. ***Questa regolazione è specifica di Query Builder e non si applica a JCR-SQL2 o XPath.***

   Utilizzo [Parametro guessTotal di Query Builder](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) quando l&#39;insieme completo dei risultati è **not** immediatamente necessario.

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
   Per i casi in cui l’esecuzione della query è veloce ma il numero di risultati è elevato, p. `guessTotal` è un’ottimizzazione critica per le query di Query Builder.

   `p.guessTotal=100` comunica a Query Builder di raccogliere solo i primi 100 risultati. Inoltre, per impostare un flag booleano che indica se esiste almeno un altro risultato (ma non il numero, in quanto il conteggio di questo numero comporta una lentezza). Questa ottimizzazione eccelle per l’impaginazione o i casi d’uso di caricamento infiniti, in cui viene visualizzato solo un sottoinsieme di risultati in modo incrementale.

## Sintonizzazione indice esistente {#existing-index-tuning}

1. Se la query ottimale viene risolta in un indice di proprietà, allora non c&#39;è più niente da fare perché gli indici di proprietà sono minimamente sintonizzabili.
1. In caso contrario, la query deve essere risolta in un indice di proprietà Lucene. Se non è possibile risolvere alcun indice, passa a Creazione di un nuovo indice.
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

1. Fornisci XPath (o JCR-SQL2) al generatore di definizione dell&#39;indice Oak in `https://oakutils.appspot.com/generate/index` in modo da poter generare la definizione dell&#39;indice di proprietà Lucene ottimizzato. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definizione dell&#39;indice della proprietà Lucene generato**

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

1. Unisci manualmente la definizione generata nell&#39;Indice proprietà Lucene esistente in modo additivo. Presta attenzione a non rimuovere le configurazioni esistenti in quanto possono essere utilizzate per soddisfare altre query.

   1. Individua l&#39;indice della proprietà Lucene esistente che copre cq:Page (utilizzando Index Manager). In questo caso, `/oak:index/cqPageLucene`.
   1. Identifica il delta di configurazione tra la definizione dell&#39;indice ottimizzato (Passaggio n. 4) e l&#39;indice esistente (/oak:index/cqPageLucene) e aggiungi le configurazioni mancanti dall&#39;Indice ottimizzato alla definizione dell&#39;indice esistente.
   1. In base alle best practice per la reindicizzazione di AEM, è in ordine un aggiornamento o una reindicizzazione, in base a se il contenuto esistente potrebbe essere interessato da questa modifica della configurazione dell&#39;indice.

## Crea un nuovo indice {#create-a-new-index}

1. Verifica che la query non venga risolta in un indice di proprietà Lucene esistente. In caso affermativo, vedere la sezione precedente sull&#39;ottimizzazione e l&#39;indice esistente.
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

1. Fornisci XPath (o JCR-SQL2) al generatore di definizione dell&#39;indice Oak in `https://oakutils.appspot.com/generate/index` in modo da poter generare la definizione dell&#39;indice di proprietà Lucene ottimizzato. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definizione dell&#39;indice della proprietà Lucene generato**

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

1. Distribuisci la definizione dell&#39;indice di proprietà Lucene generato.

   Aggiungi la definizione XML fornita da Oak Index Definition Generator per il nuovo indice al progetto AEM che gestisce le definizioni degli indici Oak (ricorda, tratta le definizioni degli indici Oak come codice, dal momento che il codice dipende da loro).

   Distribuisci e verifica il nuovo indice seguendo il consueto ciclo di vita di sviluppo del software AEM e verifica che la query si risolva nell&#39;indice e che la query sia performante.

   Nella distribuzione iniziale di questo indice, AEM popolato l&#39;indice con i dati richiesti.

## Quando sono OK le query senza indice e traversal? {#when-index-less-and-traversal-queries-are-ok}

A causa AEM’architettura dei contenuti flessibile, è difficile prevedere e garantire che l’attraversamento delle strutture di contenuto non evolva nel tempo per diventare eccessivamente grande.

Pertanto, assicurati che gli indici soddisfino le query, a meno che la combinazione di restrizione del percorso e restrizione del tipo di nodo garantisca che **meno di 20 nodi vengono mai attraversati.**

## Strumenti di sviluppo delle query {#query-development-tools}

### Adobe supportato {#adobe-supported}

* **Debugger di Query Builder**

   * Interfaccia Web per l’esecuzione di query Query Builder e la generazione del supporto XPath (da utilizzare in Explain Query o in Oak Index Definition Generator).
   * Il AEM a [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Strumento Query**

   * Interfaccia Web per l&#39;esecuzione di query XPath e JCR-SQL2.
   * Il AEM a [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Strumenti > Query..

* **[Spiega query](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Dashboard delle operazioni di AEM che fornisce una spiegazione dettagliata (piano query, tempo query e numero di risultati) per qualsiasi query XPATH o JCR-SQL2 specificata.

* **[Query lente/popolari](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Una dashboard delle operazioni di AEM elenca le query lente e popolari recenti eseguite su AEM.

* **[Gestione indice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Un&#39;interfaccia Web AEM Operations che visualizza gli indici sull&#39;istanza AEM; facilita la comprensione degli indici esistenti; può essere mirato o aumentato.

* **[Registrazione](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registrazione Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registrazione esecuzione query Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configurazione OSGi delle impostazioni del motore di query Apache Jackrabbit**

   * Configurazione OSGi che configura il comportamento di errore per l’attraversamento delle query.
   * Il AEM a [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **Mbean JMX NodeCounter**

   * MBean JMX utilizzato per stimare il numero di nodi nelle strutture di contenuto in AEM.
   * Il AEM a [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Community supportata {#community-supported}

* **Generatore di definizione dell&#39;indice Oak in`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Genera un indice di proprietà Lucence ottimale dalle istruzioni di query XPath o JCR-SQL2.

* **[Plug-in di AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Estensione del browser web Google Chrome che espone i dati di log per richiesta, incluse le query eseguite e i relativi piani di query, nella console degli strumenti di sviluppo del browser.
   * Richiede [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) da installare e attivare in AEM.
