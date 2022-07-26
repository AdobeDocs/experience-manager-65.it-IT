---
title: API Query Builder
seo-title: Query Builder API
description: La funzionalità di Asset Share Query Builder è esposta tramite un’API Java e un’API REST.
seo-description: The functionality of the Asset Share Query Builder is exposed through a Java API and a REST API.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
source-git-commit: 49a74d8c14c79e72f9df1e2ec41652ebc6fe76b6
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 0%

---

# API Query Builder{#query-builder-api}

La funzionalità del [Query Builder per condivisione risorse](/help/assets/assets-finder-editor.md) è esposto tramite un’API Java e un’API REST. Questa sezione descrive queste API.

Generatore di query lato server ( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegue una query XPath, filtra facoltativamente il set di risultati e, se necessario, estrae anche i facet.

La descrizione della query è semplicemente un insieme di predicati ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Gli esempi includono un predicato full-text che corrisponde al `jcr:contains()` in XPath.

Per ogni tipo di predicato, esiste un componente valutatore ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) che sa come gestire quel predicato specifico per XPath, filtraggio ed estrazione del facet. È molto facile creare valutatori personalizzati, che sono collegati tramite il runtime del componente OSGi.

L’API REST consente di accedere esattamente alle stesse funzioni tramite HTTP e le risposte vengono inviate in JSON.

>[!NOTE]
>
>L’API QueryBuilder viene creata utilizzando l’API JCR. Puoi anche eseguire query su Adobe Experience Manager JCR utilizzando l&#39;API JCR da un bundle OSGi. Per informazioni, consulta [Query dei dati di Adobe Experience Manager tramite l’API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessione Gem {#gem-session}

[AEM gemme](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/overview.html) è una serie di approfondimenti tecnici su Adobe Experience Manager forniti da esperti di Adobe. Questa sessione dedicata al generatore di query è molto utile per una panoramica e l&#39;utilizzo dello strumento.

>[!NOTE]
>
>Guarda la sessione AEM Gem [Moduli di ricerca semplificati con il querybuilder AEM](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html) per una panoramica dettagliata del generatore di query.

## Query di esempio {#sample-queries}

Questi esempi sono forniti nella notazione dello stile delle proprietà Java. Per utilizzarli con l’API Java, utilizza un `HashMap` come nell’esempio di API che segue.

Per `QueryBuilder` Servlet JSON, ogni esempio include un collegamento all’installazione locale di CQ (nel percorso predefinito, `http://localhost:4502`). Tieni presente che devi accedere alla tua istanza CQ prima di usare questi collegamenti.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet json del generatore di query visualizza un massimo di 10 hit.
>
>L’aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>**`p.limit=-1`**

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, potresti voler usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query **restituisce dieci risultati** (o per essere precisi un massimo di dieci), ma informarti **Numero di hit:** che sono effettivamente disponibili:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) **restituisce tutti i risultati** (potrebbe essere un numero elevato a seconda dell’istanza):

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilizzo di p.guessTotal per restituire i risultati {#using-p-guesstotal-to-return-the-results}

Lo scopo del `p.guessTotal` restituisce il numero appropriato di risultati che possono essere mostrati combinando i valori p.offset e p.limit minimi. Il vantaggio di utilizzare questo parametro è il miglioramento delle prestazioni con grandi set di risultati. In questo modo si evita di calcolare l&#39;intero totale (ad esempio chiamando result.getSize()) e di leggere l&#39;intero set di risultati, ottimizzato fino al motore OAK &amp; index. Questa può essere una differenza significativa quando ci sono 100 migliaia di risultati, sia in termini di tempo di esecuzione che di utilizzo della memoria.

Lo svantaggio del parametro è che gli utenti non vedono il totale esatto. Ma è possibile impostare un numero minimo come p.guessTotal=1000 in modo che possa sempre leggere fino a 1000, in modo da ottenere i totali esatti per set di risultati più piccoli, ma se è più di questo, è possibile solo mostrare &quot;e più&quot;.

Aggiungi `p.guessTotal=true` alla query seguente per vedere come funziona:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

La query restituirà la variabile `p.limit` predefinito `10` risultati con un `0` offset:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

A partire da AEM 6.0 SP2, è anche possibile utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizza la stessa query di cui sopra, ma modifica il valore di `p.guessTotal` a `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Restituisce un numero con lo stesso limite predefinito di 10 risultati con un offset 0, ma visualizza solo un massimo di 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione della paginazione {#implementing-pagination}

Per impostazione predefinita, il Generatore di query fornisce anche il numero di hit. A seconda della dimensione del risultato, questo potrebbe richiedere molto tempo, in quanto la determinazione del conteggio accurato comporta il controllo di ogni risultato per il controllo degli accessi. Per lo più, il totale viene utilizzato per implementare l’impaginazione per l’interfaccia utente finale. Poiché la determinazione del conteggio esatto può essere lenta, si consiglia di utilizzare la funzione guessTotal per implementare l’impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottieni e visualizza il conteggio accurato del numero di hit totali ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) o totale nella risposta querybuilder.json) sono inferiori o uguali a 100;
* Imposta `guessTotal` a 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`, `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati nella prima pagina e fornire l’impaginazione per le tre pagine successive. Puoi anche utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 risultati trovati&quot;**.
   * `total=100`, `more=true` - Indica che il numero totale di hit è maggiore di 100 e che il conteggio esatto non è noto. L’interfaccia utente può visualizzare fino a dieci pagine come parte della prima pagina e fornire impaginazione per le dieci pagine successive. È inoltre possibile utilizzare questa opzione per visualizzare un testo come **&quot;più di 100 risultati trovati&quot;**. Man mano che l’utente passa alle successive chiamate effettuate al Generatore di query, il limite di `guessTotal` e anche del `offset` e `limit` Parametri.

`guessTotal` Deve essere utilizzato anche nei casi in cui l’interfaccia utente deve utilizzare lo scorrimento infinito, per evitare che Query Builder determini l’esatto numero di hit.

### Trova i file jar e ordinali, prima più recenti {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Trova tutte le pagine e ordinale per ultima modifica {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Trova tutte le pagine e ordinale per ultima modifica, ma decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Ricerca full-text, ordinata per punteggio {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Cercare pagine con tag specifici {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Utilizza la `tagid` predicare come nell&#39;esempio se conosci l&#39;ID tag esplicito.

Utilizza la `tag` predicato per il percorso del titolo del tag (senza spazi).

Perché, nell’esempio precedente, stai cercando le pagine ( `cq:Page` nodi), è necessario utilizzare il percorso relativo da quel nodo per `tagid.property` predicato, ovvero `jcr:content/cq:tags`. Per impostazione predefinita, la `tagid.property` semplicemente `cq:tags`.

### Cerca in più percorsi (utilizzando i gruppi) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Questa query utilizza un *gruppo* (denominato &quot; `group`&quot;), che agisce per delimitare le sottoespressioni all’interno di una query, come fanno le parentesi nelle notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

All’interno del gruppo nell’esempio, il `path` Il predicato viene utilizzato più volte. Per differenziare e ordinare le due istanze del predicato (l’ordinamento è necessario per alcuni predicati), è necessario preimpostare i predicati con *N* `_ where`*N* è l&#39;indice di ordinamento. Nell’esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

La `p` in `p.or` è un delimitatore speciale che indica quanto segue (in questo caso un `or`) è un *parameter* del gruppo, invece di un subpredicato del gruppo, come `1_path`.

Se no `p.or` viene dato allora tutti i predicati sono ANDed insieme, cioè, ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per predicati diversi.

### Cerca proprietà {#search-for-properties}

Qui stai cercando tutte le pagine di un dato modello, utilizzando `cq:template` proprietà:

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

Questo ha lo svantaggio che il `jcr:content` vengono restituiti i nodi delle pagine, non le pagine stesse. Per risolvere questo problema, è possibile eseguire ricerche per percorso relativo:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Ricerca di più proprietà {#search-for-multiple-properties}

Quando si utilizza il predicato proprietà più volte, è necessario aggiungere di nuovo i prefissi numerici:

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Ricerca di più valori di proprietà {#search-for-multiple-property-values}

Per evitare grandi gruppi quando si desidera cercare più valori di una proprietà ( `"A" or "B" or "C"`), è possibile fornire più valori al `property` predicato:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

Per le proprietà con più valori, puoi anche richiedere che più valori corrispondano ( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Ottimizzazione dei risultati {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON di QueryBuilder restituisce un set predefinito di proprietà per ciascun nodo nel risultato della ricerca (ad esempio percorso, nome, titolo, ecc.). Per ottenere il controllo sulle proprietà restituite, è possibile effettuare una delle seguenti operazioni:

Specifica

```
p.hits=full
```

in tal caso tutte le proprietà verranno incluse per ogni nodo:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Utilizzare

```
p.hits=selective
```

e specifica le proprietà che desideri inserire

```
p.properties
```

separati da uno spazio:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selettivo&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

Un&#39;altra cosa che è possibile fare è includere nodi figlio nella risposta di QueryBuilder. Per eseguire questa operazione è necessario specificare

```
p.nodedepth=n
```

dove `n` è il numero di livelli che la query deve restituire. Tieni presente che, affinché un nodo figlio possa essere restituito, deve essere specificato dal selettore delle proprietà

```
p.hits=full
```

Esempio:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## Predicati aggiuntivi {#morepredicates}

Per ulteriori predicati, consulta la sezione [Pagina di riferimento del predicato di Query Builder](/help/sites-developing/querybuilder-predicate-reference.md).

Puoi anche controllare la [Javadoc per `PredicateEvaluator` classi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc per queste classi contiene l&#39;elenco delle proprietà che è possibile utilizzare.

Prefisso del nome della classe (ad esempio, &quot; `similar`&quot; [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è *proprietà principale* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in minuscolo).

Per tali proprietà principali, è possibile accorciare la query e utilizzare &quot; `similar=/content/en`&quot; invece della variante completa &quot; `similar.similar=/content/en`&quot;. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

## Esempio di utilizzo dell’API di Query Builder {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>Per informazioni su come creare un bundle OSGi che utilizza l&#39;API QueryBuilder e utilizza tale bundle OSGi all&#39;interno di un&#39;applicazione Adobe Experience Manager, vedi [Creazione di bundle OSGi Adobe CQ che utilizzano l&#39;API di Query Builder](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I.

La stessa query eseguita su HTTP utilizzando il servlet Query Builder (JSON):

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento delle query {#storing-and-loading-queries}

Le query possono essere archiviate nell’archivio in modo da poterle utilizzare in un secondo momento. La `QueryBuilder` fornisce il `storeQuery` metodo con la firma seguente:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando utilizzi [ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) il metodo `Query` viene memorizzato nell&#39;archivio come file o come proprietà in base al `createFile` valore dell&#39;argomento. L’esempio seguente mostra come salvare un `Query` al percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Qualsiasi query precedentemente archiviata può essere caricata dal repository utilizzando [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) metodo:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` memorizzato nel percorso `/mypath/getfiles` può essere caricato dal seguente snippet:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per riprodurre e eseguire il debug delle query querybuilder, è possibile utilizzare la console di debug di QueryBuilder in

`http://localhost:4502/libs/cq/search/content/querydebug.html`

o in alternativa il servlet json querybuilder a

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` è solo un esempio).

### Debug generale di Recommendations {#general-debugging-recommendations}

### Ottieni XPath spiegabile tramite registrazione {#obtain-explain-able-xpath-via-logging}

Spiegare **tutto** le query durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

* Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile

   * Vai su https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Crea un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` a **DEBUG**.

* Una volta abilitato DEBUG per la classe di cui sopra, i registri visualizzeranno l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incolla la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per oscurare il piano di query

### Ottieni XPath spiegabile tramite il debugger di Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Utilizza il debugger QueryBuilder AEM per generare una query XPath spiegabile:

Spiegare **tutto** le query durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

**Ottieni XPath spiegabile tramite registrazione**

* Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile

   * Vai su https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Crea un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` a **DEBUG**.

* Una volta abilitato DEBUG per la classe di cui sopra, i registri visualizzeranno l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incolla la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per ottenere il piano di query

**Ottieni XPath spiegabile tramite il debugger di Query Builder**

* Utilizza il debugger QueryBuilder AEM per generare una query XPath spiegabile:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Fornire la query Query Builder nel debugger di Query Builder
1. Esegui la ricerca
1. Ottieni l&#39;XPath generato
1. Incolla la query XPath in Explain Query as XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non-querybuilder (XPath, JCR-SQL2) possono essere fornite direttamente a Explain Query.

Per un elenco a discesa su come eseguire il debug delle query con QueryBuilder, guarda il video seguente.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Debug delle query con la registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nella sezione [Creazione di propri logger e scrittori](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

L&#39;output di log (livello INFO) dell&#39;implementazione del generatore di query durante l&#39;esecuzione della query descritta in Testing and Debugging:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Se disponi di una query che utilizza valutatori predicati che filtrano o utilizzano un ordine personalizzato per comparatore, questa operazione verrà rilevata anche nella query:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Collegamenti Javadoc {#javadoc-links}

| **Javadoc** | **Descrizione** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | API QueryBuilder e query di base |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bukets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Punti (contenuti nei facet) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Valutatori del predicato |
| [com.day.cq.search.facets.extractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori di sfaccettature (per valutatori) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Scrittore di risultati JSON per il servlet Querybuilder (/bin/querybuilder.json) |
