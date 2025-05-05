---
title: Risoluzione dei problemi relativi a query lente
description: Scopri come risolvere i problemi relativi alle query lente in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---

# Risoluzione dei problemi relativi a query lente{#troubleshooting-slow-queries}

## Classificazioni query lente {#slow-query-classifications}

Esistono tre classificazioni principali delle query lente nell’AEM, elencate per gravità:

1. **Query senza indice**

   * Le query che **non** risolvono in un indice e attraversano il contenuto di JCR per raccogliere i risultati

1. **Query con restrizioni (o con ambito) insufficiente**

   * Query che si risolvono in un indice, ma devono attraversare tutte le voci dell&#39;indice per raccogliere i risultati

1. **Query con set di risultati di grandi dimensioni**

   * Query che restituiscono un numero elevato di risultati

Le prime due classificazioni di query (senza indice e con restrizioni insufficienti) sono lente. Sono lenti perché forzano il motore di query di Oak a ispezionare ogni **risultato potenziale** (nodo di contenuto o voce di indice) per identificare quale appartiene al set di risultati **effettivo**.

L&#39;atto di ispezionare ogni potenziale risultato è quello che è chiamato Traversing.

Poiché ogni risultato potenziale deve essere ispezionato, il costo per determinare il set di risultati effettivo aumenta in modo lineare con il numero di risultati potenziali.

L’aggiunta di restrizioni alle query e di indici di tuning consente di memorizzare i dati dell’indice in un formato ottimizzato che consente un rapido recupero dei risultati e, riduce o elimina la necessità di un’ispezione lineare dei potenziali set di risultati.

In AEM 6.3, per impostazione predefinita, quando viene raggiunto un attraversamento di 100.000, la query non riesce e viene generata un’eccezione. Questo limite non esiste per impostazione predefinita nelle versioni AEM precedenti alla AEM 6.3, ma può essere impostato tramite la configurazione OSGi Apache Jackrabbit Query Engine Settings e il bean JMX QueryEngineSettings (proprietà LimitReads).

### Rilevamento delle query senza indice {#detecting-index-less-queries}

#### Durante lo sviluppo {#during-development}

Spiega **tutte** le query e assicurati che i relativi piani di query non contengano la spiegazione **/&ast; traverse**. Esempio di piano di query di attraversamento:

* **PIANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Post-Distribuzione {#post-deployment}

* Monitorare `error.log` per le query di attraversamento senza indice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Questo messaggio viene registrato solo se non è disponibile alcun indice e se la query attraversa potenzialmente molti nodi. I messaggi non vengono registrati se è disponibile un indice, ma la quantità di navigazione è ridotta e quindi veloce.

* Visita la console delle operazioni [Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance) dell&#39;AEM e [Spiega](/help/sites-administering/operations-dashboard.md#explain-query) le query lente in cerca di spiegazioni di query trasversali o senza spiegazioni di query di indice.

### Rilevamento di query con restrizioni insufficienti {#detecting-poorly-restricted-queries}

#### Durante lo sviluppo {#during-development-1}

Spiega tutte le query e assicurati che vengano risolte in un indice sottoposto a tuning in modo che corrisponda alle restrizioni di proprietà della query.

* La copertura del piano di query ideale ha `indexRules` per tutte le restrizioni di proprietà e almeno per le restrizioni di proprietà più severe nella query.
* Le query che ordinano i risultati devono essere risolte in un indice delle proprietà Lucene con regole di indice per le proprietà che impostano `orderable=true.`

#### Ad esempio, `cqPageLucene` predefinito non ha una regola indice per `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Prima di aggiungere la regola di indice cq:tags

* **cq:tags, regola indice**

   * Non esiste come impostazione predefinita

* **Query di Query Builder**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **Piano query**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Questa query viene risolta nell&#39;indice `cqPageLucene`, ma poiché non esiste alcuna regola dell&#39;indice delle proprietà per `jcr:content` o `cq:tags`, quando questa restrizione viene valutata, ogni record nell&#39;indice `cqPageLucene` viene controllato per determinare una corrispondenza. Di conseguenza, se l&#39;indice contiene 1 milione di nodi `cq:Page`, vengono controllati 1 milione di record per determinare il set di risultati.

Dopo l’aggiunta della regola di indice cq:tags

* **cq:tags, regola indice**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Query di Query Builder**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **Piano query**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

L&#39;aggiunta di indexRule per `jcr:content/cq:tags` nell&#39;indice `cqPageLucene` consente l&#39;archiviazione ottimizzata dei dati di `cq:tags`.

Quando viene eseguita una query con la restrizione `jcr:content/cq:tags`, l&#39;indice può cercare i risultati per valore. Ciò significa che se 100 nodi `cq:Page` hanno `myTagNamespace:myTag` come valore, vengono restituiti solo questi 100 risultati e gli altri 999.000 vengono esclusi dai controlli di restrizione, migliorando le prestazioni di un fattore di 10.000.

Più restrizioni alle query riducono i set di risultati idonei e ottimizzano ulteriormente l’ottimizzazione delle query.

Analogamente, senza una regola di indice aggiuntiva per la proprietà `cq:tags`, anche una query full-text con una restrizione su `cq:tags` avrebbe prestazioni insoddisfacenti in quanto i risultati dell&#39;indice restituirebbero tutte le corrispondenze full-text. La restrizione su cq:tags verrebbe filtrata dopo di essa.

Un’altra causa del filtraggio post-indice è rappresentata dagli elenchi di controllo di accesso, che spesso vengono saltati durante lo sviluppo. Verificare che la query non restituisca percorsi che potrebbero essere inaccessibili all&#39;utente. Ciò può essere fatto migliorando la struttura del contenuto e fornendo restrizioni rilevanti sul percorso della query.

Un modo utile per identificare se l&#39;indice Lucene restituisce molti risultati per restituire un piccolo sottoinsieme come risultato della query consiste nell&#39;abilitare i registri DEBUG per `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. In questo modo è possibile visualizzare il numero di documenti caricati dall&#39;indice. Il numero di risultati finali rispetto al numero di documenti caricati non dovrebbe essere sproporzionato. Per ulteriori informazioni, vedere [Registrazione](/help/sites-deploying/configure-logging.md).

#### Post-Distribuzione {#post-deployment-1}

* Monitorare `error.log` per le query di attraversamento:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visita la console delle operazioni [Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance) dell&#39;AEM e [Spiega](/help/sites-administering/operations-dashboard.md#explain-query) le query lente che cercano piani di query che non risolvono le restrizioni delle proprietà di query alle regole di proprietà di indice.

### Rilevamento di query di set di risultati di grandi dimensioni {#detecting-large-result-set-queries}

#### Durante lo sviluppo {#during-development-2}

Imposta soglie basse per oak.queryLimitInMemory (ad esempio, 10000) e oak.queryLimitReads (ad esempio, 5000) e ottimizza la query costosa quando si preme un UnsupportedOperationException che indica &quot;La query legge più di x nodi...&quot;

L’impostazione di soglie basse consente di evitare query che richiedono un uso intensivo delle risorse (non supportate da alcun indice o supportate da un indice di copertura inferiore). Ad esempio, una query che legge un milione di nodi produrrebbe un numero elevato di operazioni di I/O e influirebbe negativamente sulle prestazioni complessive dell&#39;applicazione. Pertanto, qualsiasi query che non riesca a causa di limiti superiori deve essere analizzata e ottimizzata.

#### Post-Distribuzione {#post-deployment-2}

* Monitora i registri per le query che attivano l’attraversamento di nodi di grandi dimensioni o il consumo di memoria heap di grandi dimensioni: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Ottimizza la query in modo da ridurre il numero di nodi attraversati.

* Monitora i registri per le query che attivano un consumo elevato di memoria heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Ottimizza la query in modo da ridurre il consumo di memoria heap.

Per le versioni da AEM 6.0 a 6.2, è possibile regolare la soglia per l’attraversamento dei nodi tramite i parametri JVM nello script di avvio dell’AEM per evitare che le query di grandi dimensioni sovraccarichi l’ambiente. I valori consigliati sono:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

In AEM 6.3, i due parametri precedenti sono preconfigurati per impostazione predefinita e possono essere modificati tramite OSGi QueryEngineSettings.

Ulteriori informazioni disponibili in: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ottimizzazione delle prestazioni delle query {#query-performance-tuning}

Il motto dell’ottimizzazione delle prestazioni delle query in AEM è:

**&quot;Maggiori sono le restrizioni, meglio è.&quot;**

Di seguito sono riportati gli adeguamenti consigliati per garantire le prestazioni delle query. Ottimizza innanzitutto la query, un’attività meno invasiva, quindi, se necessario, ottimizza le definizioni dell’indice.

### Adeguamento dell&#39;istruzione di query {#adjusting-the-query-statement}

L’AEM supporta i seguenti linguaggi di query:

* Query Builder
* JCR-SQL2
* XPath

L’esempio seguente utilizza Query Builder perché è il linguaggio di query più comune utilizzato dagli sviluppatori AEM, tuttavia gli stessi principi sono applicabili a JCR-SQL2 e XPath.

1. Aggiungi una restrizione di tipo nodo in modo che la query venga risolta in un indice delle proprietà Lucene esistente.

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

  Le query prive di una restrizione del tipo di nodo forzano l&#39;AEM ad assumere il tipo di nodo `nt:base`, che ogni nodo nell&#39;AEM è un sottotipo di, determinando di fatto nessuna restrizione del tipo di nodo.

  L&#39;impostazione di `type=cq:Page` limita questa query a soli `cq:Page` nodi e risolve la query in cqPageLucene dell&#39;AEM, limitando i risultati a un sottoinsieme di nodi (solo `cq:Page` nodi) nell&#39;AEM.

1. Regola la restrizione del tipo di nodo della query in modo che la query venga risolta in un indice delle proprietà Lucene esistente.

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

  `nt:hierarchyNode` è il tipo di nodo padre di `cq:Page`. Supponendo che `jcr:content/contentType=article-page` sia applicato solo a `cq:Page` nodi tramite l&#39;applicazione personalizzata di Adobe, questa query restituisce solo `cq:Page` nodi in cui `jcr:content/contentType=article-page`. Tuttavia, questo flusso rappresenta una restrizione subottimale, perché:

   * Altri nodi ereditano da `nt:hierarchyNode` (ad esempio, `dam:Asset`) aggiungendo inutilmente al set di risultati potenziali.
   * Nessun indice fornito da AEM per `nt:hierarchyNode`, tuttavia è presente un indice fornito per `cq:Page`.

  L&#39;impostazione di `type=cq:Page` limita questa query a soli `cq:Page` nodi e risolve la query in cqPageLucene dell&#39;AEM, limitando i risultati a un sottoinsieme di nodi (solo nodi cq:Page) nell&#39;AEM.

1. In alternativa, modificare le restrizioni di proprietà in modo che la query venga risolta in un Indice di proprietà esistente.

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

  La modifica della restrizione della proprietà da `jcr:content/contentType` (un valore personalizzato) alla proprietà nota `sling:resourceType` consente alla query di risolvere l&#39;indice della proprietà `slingResourceType` che indicizza tutto il contenuto di `sling:resourceType`.

  Gli indici di proprietà (a differenza degli indici di proprietà Lucene) vengono utilizzati in modo ottimale quando la query non rileva per tipo di nodo e una singola restrizione di proprietà domina il set di risultati.

1. Aggiungi alla query la restrizione di percorso più restrittiva possibile. Ad esempio, preferisci `/content/my-site/us/en` rispetto a `/content/my-site` o `/content/dam` rispetto a `/`.

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

  L&#39;ambito della restrizione del percorso da `path=/content` a `path=/content/my-site/us/en` consente agli indici di ridurre il numero di voci di indice da esaminare. Quando la query è in grado di limitare il percorso in modo adeguato, oltre a `/content` o `/content/dam`, verificare che l&#39;indice contenga `evaluatePathRestrictions=true`.

  L&#39;utilizzo di `evaluatePathRestrictions` aumenta le dimensioni dell&#39;indice.

1. Se possibile, evitare funzioni di query e operazioni di query quali `LIKE` e `fn:XXXX`, poiché i relativi costi vengono scalati in base al numero di risultati basati su restrizioni.

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

  La condizione LIKE è lenta da valutare perché non è possibile utilizzare alcun indice se il testo inizia con un carattere jolly (&quot;%...&quot;). La condizione jcr:contains consente l’utilizzo di un indice full-text ed è pertanto da preferirsi. L&#39;indice della proprietà Lucene risolto deve avere indexRule per `jcr:content/contentType` con `analayzed=true`.

  L&#39;utilizzo di funzioni di query come `fn:lowercase(..)` potrebbe essere più difficile da ottimizzare in quanto non sono disponibili equivalenti più veloci (al di fuori di configurazioni più complesse e intrusive di Index Analyzer). È meglio identificare altre restrizioni di ambito per migliorare le prestazioni complessive delle query, richiedendo che le funzioni funzionino sul minor numero possibile di risultati potenziali.

1. ***Questa regolazione è specifica di Query Builder e non si applica a JCR-SQL2 o XPath.***

   Utilizza [guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) di Query Builder&#39; quando il set completo di risultati è **non** immediatamente necessario.

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

   Nei casi in cui l&#39;esecuzione delle query è veloce ma il numero di risultati è elevato, p. `guessTotal` rappresenta un&#39;ottimizzazione critica per le query di Query Builder.

   `p.guessTotal=100` comunica a Query Builder di raccogliere solo i primi 100 risultati. E, per impostare un flag booleano che indica se esiste almeno un altro risultato (ma non quanti altri, poiché contando questo numero si ottiene una lentezza). Questa ottimizzazione è eccezionale per i casi di utilizzo di impaginazione o caricamento infinito, in cui viene visualizzato in modo incrementale solo un sottoinsieme di risultati.

## Ottimizzazione indice esistente {#existing-index-tuning}

1. Se la query ottimale viene risolta in un indice delle proprietà, non rimane nulla da fare poiché gli indici delle proprietà sono minimamente ottimizzabili.
1. In caso contrario, la query deve essere risolta in un indice della proprietà Lucene. Se non è possibile risolvere alcun indice, passa a Creazione di un indice.
1. Se necessario, convertire la query in XPath o JCR-SQL2.

   * **Query di Query Builder**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **XPath generato dalla query di Query Builder**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. Fornire XPath (o JCR-SQL2) al generatore di definizioni dell&#39;indice Oak in `https://oakutils.appspot.com/generate/index` in modo da poter generare la definizione ottimizzata dell&#39;indice delle proprietà Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

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

1. Unisci manualmente la definizione generata nell’indice della proprietà Lucene esistente in modo additivo. Fai attenzione a non rimuovere le configurazioni esistenti, in quanto potrebbero essere utilizzate per soddisfare altre query.

   1. Individua l’indice esistente della proprietà Lucene relativo a cq:Page (utilizzando Gestione indice ). In questo caso, `/oak:index/cqPageLucene`.
   1. Identifica il delta di configurazione tra la definizione dell’indice ottimizzato (passaggio #4) e l’indice esistente (/oak:index/cqPageLucene) e aggiungi le configurazioni mancanti dall’indice ottimizzato alla definizione dell’indice esistente.
   1. In base alle best practice per la reindicizzazione dell’AEM, è necessario aggiornare o reindicizzare il contenuto in base al caso in cui questa modifica della configurazione dell’indice possa influire sul contenuto esistente.

## Crea un nuovo indice {#create-a-new-index}

1. Verificare che la query non venga risolta in un indice delle proprietà Lucene esistente. In caso affermativo, vedere la sezione precedente sull&#39;ottimizzazione e l&#39;indice esistente.
1. Se necessario, convertire la query in XPath o JCR-SQL2.

   * **Query di Query Builder**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **XPath generato dalla query di Query Builder**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. Fornire XPath (o JCR-SQL2) al generatore di definizioni dell&#39;indice Oak in `https://oakutils.appspot.com/generate/index` in modo da poter generare la definizione ottimizzata dell&#39;indice delle proprietà Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

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

1. Distribuisci la definizione dell’indice delle proprietà Lucene generato.

   Aggiungi la definizione XML fornita da Oak Index Definition Generator per il nuovo indice al progetto AEM che gestisce le definizioni dell’indice Oak (ricorda che considera le definizioni dell’indice Oak come codice, poiché il codice dipende da esse).

   Distribuisci e verifica il nuovo indice seguendo il consueto ciclo di sviluppo del software AEM e verifica che la query si risolva nell’indice e che sia performante.

   Al momento della distribuzione iniziale di questo indice, l’AEM lo popola con i dati necessari.

## Quando le query senza indice e trasversali sono corrette? {#when-index-less-and-traversal-queries-are-ok}

A causa della flessibilità dell’architettura dei contenuti dell’AEM, è difficile prevedere e garantire che gli attraversamenti delle strutture dei contenuti non si evolvano nel tempo fino a raggiungere dimensioni inaccettabili.

Assicurati pertanto che gli indici soddisfino le query, tranne nel caso in cui la combinazione di limitazione del percorso e di limitazione del tipo di nodo garantisca che **meno di 20 nodi siano mai attraversati.**

## Strumenti di sviluppo delle query {#query-development-tools}

### Adobe supportato {#adobe-supported}

* **Debugger di Query Builder**

   * Interfaccia Web per l&#39;esecuzione di query di Query Builder e la generazione dell&#39;XPath di supporto (da utilizzare in Explain Query o Oak Index Definition Generator).
   * Su AEM in [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Liti - Strumento Query**

   * Interfaccia Web per l&#39;esecuzione di query XPath e JCR-SQL2.
   * Su AEM in [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Strumenti > Query...

* **[Spiega query](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Un dashboard Operazioni AEM che fornisce una spiegazione dettagliata (piano query, tempo query e numero di risultati) per una determinata query XPATH o JCR-SQL2.

* **[Query lente/popolari](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Una dashboard delle operazioni dell’AEM che elenca le recenti query lente e popolari eseguite sull’AEM.

* **[Gestione indice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Un’interfaccia web per le operazioni dell’AEM che visualizza gli indici nell’istanza dell’AEM; facilita la comprensione degli indici esistenti; può essere mirata o incrementata.

* **[Registrazione](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registrazione di Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Registrazione esecuzione query Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Configurazione OSGi impostazioni motore di query Apache Jackrabbit**

   * Configurazione OSGi che configura il comportamento di errore per l’attraversamento delle query.
   * Su AEM in [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **JMX Mbean di NodeCounter**

   * MBean JMX utilizzato per stimare il numero di nodi nelle strutture dei contenuti nell’AEM.
   * Su AEM in [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Community supportata {#community-supported}

* **Generatore definizione indice Oak in`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Genera l’indice ottimale della proprietà Lucence dalle istruzioni di query XPath o JCR-SQL2.

* **_Plug-in Chrome AEM_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * Il plug-in di Chrome _AEM_ è un&#39;estensione del browser Web Google Chrome che espone i dati di registro per richiesta, incluse le query di esecuzione e i relativi piani di query, nella console degli strumenti di sviluppo del browser.
   * Richiede l&#39;installazione e l&#39;abilitazione di [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) su AEM.
