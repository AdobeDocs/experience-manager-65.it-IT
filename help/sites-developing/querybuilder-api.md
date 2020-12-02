---
title: API Query Builder
seo-title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un'API Java e un'API REST.
seo-description: La funzionalità di Asset Share Query Builder è esposta tramite un'API Java e un'API REST.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: a491d4e9bd9ffc68c4ba7cac3149f48cf7576ee8
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 0%

---


# API Query Builder{#query-builder-api}

La funzionalità di [Asset Share Query Builder](/help/assets/assets-finder-editor.md) è esposta tramite un&#39;API Java e un&#39;API REST. Questa sezione descrive queste API.

Il generatore di query lato server ( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegue una query XPath, eventualmente applica un filtro al set di risultati e, se necessario, estrae anche i facet.

La descrizione della query è semplicemente un insieme di predicati ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Alcuni esempi includono un predicato full-text, che corrisponde alla funzione `jcr:contains()` in XPath.

Per ciascun tipo di predicato, è presente un componente valutatore ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) in grado di gestire tale predicato specifico per XPath, filtraggio ed estrazione dei facet. È molto facile creare valutatori personalizzati, che vengono collegati tramite il runtime dei componenti OSGi.

L&#39;API REST fornisce l&#39;accesso esattamente alle stesse funzionalità tramite HTTP, con le risposte inviate in JSON.

>[!NOTE]
>
>L&#39;API QueryBuilder viene creata utilizzando l&#39;API JCR. Potete anche eseguire una query su Adobe Experience Manager JCR utilizzando l&#39;API JCR da un bundle OSGi. Per informazioni, vedere [Query dei dati Adobe Experience Manager tramite l&#39;API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessione Gem {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis una serie di approfondimenti tecnici in Adobe Experience Manager forniti da  esperti Adobe. Questa sessione dedicata al generatore di query è molto utile per una panoramica e l&#39;utilizzo dello strumento.

>[!NOTE]
>
>Per una panoramica dettagliata del generatore di query, vedere la sessione AEM Gem [Facilitare la ricerca di moduli con il querybuilder](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) AEM.

## Query di esempio {#sample-queries}

Questi esempi sono riportati nella notazione dello stile delle proprietà Java. Per utilizzarli con l&#39;API Java, utilizzate Java `HashMap` come nell&#39;esempio di API che segue.

Per il Servlet `QueryBuilder` JSON, ogni esempio include un collegamento all&#39;installazione locale di CQ (nel percorso predefinito, `http://localhost:4502`). Prima di usare questi collegamenti, è necessario accedere all’istanza CQ.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet json del generatore di query visualizza un massimo di 10 hit.
>
>L&#39;aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>**`p.limit=-1`**

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, potresti voler usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query restituisce **dieci risultati** (o per essere precisi, un massimo di dieci), ma vi informa del **Numero di hit:** effettivamente disponibili:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) restituirà tutti i risultati **(a seconda dell&#39;istanza potrebbe essere un numero elevato):**

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilizzo di p.impressionTotal per restituire i risultati {#using-p-guesstotal-to-return-the-results}

Lo scopo del parametro `p.guessTotal` è di restituire il numero appropriato di risultati che possono essere mostrati combinando i valori p.offset e p.limit minimi. Il vantaggio di utilizzare questo parametro è rappresentato da prestazioni migliori con set di risultati di grandi dimensioni. In questo modo si evita di calcolare il totale totale (ad esempio, chiamando result.getSize()) e di leggere l’intero set di risultati, ottimizzato fino al motore e indice OAK. Ciò può rappresentare una differenza significativa in presenza di 100 migliaia di risultati, sia in termini di tempo di esecuzione che di utilizzo della memoria.

Lo svantaggio per il parametro è che gli utenti non vedono il totale esatto. Ma potete impostare un numero minimo come p.indovinoTotale=1000 in modo che sia sempre letto fino a 1000, quindi ottenete i totali esatti per i set di risultati più piccoli, ma se è più di questo, potete solo mostrare &quot;e più&quot;.

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

La query restituirà il valore predefinito `p.limit` di `10` risultati con un offset `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

A partire da AEM 6.0 SP2, è anche possibile utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizzate la stessa query di cui sopra, ma modificate il valore di `p.guessTotal` in `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Verrà restituito un numero con lo stesso limite predefinito di 10 risultati con un offset pari a 0, ma verranno visualizzati solo 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione impaginazione {#implementing-pagination}

Per impostazione predefinita, Query Builder fornisce anche il numero di hit. A seconda della dimensione del risultato, questo potrebbe richiedere molto tempo, poiché per determinare il conteggio accurato è necessario controllare ogni risultato per il controllo dell&#39;accesso. La maggior parte del totale viene utilizzata per implementare l&#39;impaginazione per l&#39;interfaccia utente finale. Poiché determinare il conteggio esatto può essere lento, si consiglia di utilizzare la funzione approssimativaTotale per implementare l&#39;impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottenere e visualizzare il conteggio accurato del numero totale di hit ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) o totale nella risposta querybuilder.json) è minore o uguale a 100;
* Impostate `guessTotal` su 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`,  `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati nella prima pagina e fornire impaginazione per le tre pagine successive. Potete inoltre utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 Results found&quot;**.
   * `total=100`,  `more=true` - Indica che il numero totale di hit è maggiore di 100 e che il conteggio esatto non è noto. L’interfaccia utente può essere visualizzata fino a dieci nella prima pagina e fornire impaginazione per le dieci pagine successive. È inoltre possibile utilizzare questa opzione per visualizzare un testo come **&quot;oltre 100 risultati trovati&quot;**. Man mano che l&#39;utente passa alle pagine successive, le chiamate effettuate al Generatore di query aumentano il limite di `guessTotal` e anche dei parametri `offset` e `limit`.

`guessTotal` dovrebbe essere utilizzato anche nei casi in cui l&#39;interfaccia utente deve utilizzare lo scorrimento infinito, per evitare che il Generatore di query determini l&#39;esatto numero di hit.

### Trovare i file JAR e ordinarli, prima {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Trovare tutte le pagine e ordinarle in base all&#39;ultima modifica {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Trovare tutte le pagine e ordinarle per ultima modifica, ma decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

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

### Ricerca di pagine con tag specifici {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags&#39;

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Utilizzate il predicato `tagid` come nell&#39;esempio, se conoscete l&#39;ID di tag esplicito.

Utilizzate il predicato `tag` per il percorso del titolo del tag (senza spazi).

Poiché, nell&#39;esempio precedente, si stanno cercando pagine ( `cq:Page` nodi), è necessario utilizzare il percorso relativo da tale nodo per il predicato `tagid.property`, che è `jcr:content/cq:tags`. Per impostazione predefinita, il `tagid.property` è semplicemente `cq:tags`.

### Cerca in più percorsi (tramite gruppi) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Questa query utilizza un *gruppo* (denominato &quot; `group`&quot;) che agisce per delimitare le sottoespressioni all&#39;interno di una query, come accade per le parentesi in notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

All&#39;interno del gruppo nell&#39;esempio, il predicato `path` viene utilizzato più volte. Per distinguere e ordinare le due istanze del predicato (l&#39;ordine è richiesto per alcuni predicati), è necessario preimpostare i predicati con *N* `_ where`*N* come indice di ordinamento. Nell&#39;esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

`p` in `p.or` è un delimitatore speciale che indica che ciò che segue (in questo caso un `or`) è un *parametro* del gruppo, a differenza di un subpredicato del gruppo, come `1_path`.

Se non viene fornito alcun valore `p.or`, tutti i predicati vengono inseriti insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per diversi predicati.

### Cerca proprietà {#search-for-properties}

Qui state cercando tutte le pagine di un dato modello, utilizzando la proprietà `cq:template`:

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

Questo ha lo svantaggio di restituire i nodi `jcr:content` delle pagine, non le pagine stesse. Per risolvere questo problema, potete eseguire una ricerca in base al percorso relativo:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Ricerca di più proprietà {#search-for-multiple-properties}

Quando si utilizza più volte il predicato delle proprietà, è necessario aggiungere di nuovo i prefissi numerici:

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Cerca più valori di proprietà {#search-for-multiple-property-values}

Per evitare gruppi di grandi dimensioni quando si desidera cercare più valori di una proprietà ( `"A" or "B" or "C"`), è possibile fornire più valori al predicato `property`:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

Per le proprietà multivalore, potete anche richiedere che più valori corrispondano ( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Ottimizzazione dei risultati restituiti {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON QueryBuilder restituirà un set predefinito di proprietà per ciascun nodo nel risultato della ricerca (ad esempio percorso, nome, titolo, ecc.). Per controllare quali proprietà vengono restituite, è possibile effettuare una delle seguenti operazioni:

Specifica

```
p.hits=full
```

in tal caso tutte le proprietà saranno incluse per ciascun nodo:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Utilizzo

```
p.hits=selective
```

e specificare le proprietà in cui si desidera accedere

```
p.properties
```

separati da uno spazio:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=Selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3article&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

È inoltre possibile includere nodi secondari nella risposta di QueryBuilder. A tal fine è necessario specificare

```
p.nodedepth=n
```

dove `n` è il numero di livelli che si desidera che venga restituito dalla query. Per restituire un nodo figlio, è necessario specificarlo dal selettore delle proprietà

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

## Altri predicati {#morepredicates}

Per ulteriori predicati, consultate la pagina [Riferimento predicato Generatore di query](/help/sites-developing/querybuilder-predicate-reference.md).

È inoltre possibile controllare il codice [Javadoc per le classi `PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Javadoc per queste classi contiene l&#39;elenco delle proprietà utilizzabili.

Il prefisso del nome della classe (ad esempio, &quot; `similar`&quot; in [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è la *proprietà principal* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in lettere minuscole).

Per tali proprietà principali, è possibile ridurre la query e utilizzare &quot; `similar=/content/en`&quot; invece della variante completa &quot; `similar.similar=/content/en`&quot;. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

## Esempio di utilizzo dell&#39;API Query Builder {#example-query-builder-api-usage}

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
>Per informazioni su come creare un bundle OSGi che utilizza l&#39;API QueryBuilder e utilizzare il bundle OSGi all&#39;interno di un&#39;applicazione Adobe Experience Manager, vedere [Creazione  bundle Adobe CQ OSGi che utilizzano l&#39;API di Query Builder](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I.

La stessa query eseguita su HTTP tramite il servlet Query Builder (JSON):

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento delle query {#storing-and-loading-queries}

Le query possono essere memorizzate nella directory archivio in modo da poterle utilizzare in un secondo momento. `QueryBuilder` fornisce il metodo &quot;`storeQuery` con la seguente firma:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza il metodo [ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession), l&#39;elemento `Query` specificato viene memorizzato nell&#39;archivio come file o come proprietà in base al valore dell&#39;argomento `createFile`. L&#39;esempio seguente mostra come salvare un `Query` nel percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Eventuali query precedentemente archiviate possono essere caricate dall&#39;archivio utilizzando il metodo [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` memorizzato nel percorso `/mypath/getfiles` può essere caricato dal frammento seguente:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per riprodurre e debuggare query querybuilder, è possibile utilizzare la console QueryBuilder Debugger in

`http://localhost:4502/libs/cq/search/content/querydebug.html`

oppure, in alternativa, il servlet json querybuilder su

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` è solo un esempio).

### Debug generale Recommendations {#general-debugging-recommendations}

### Ottenete XPath spiegabile tramite la registrazione {#obtain-explain-able-xpath-via-logging}

Spiegare le query **all** durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

* Abilitare i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante spiegabile

   * Andate a https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Create un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.

* Una volta attivato DEBUG per la classe sopra riportata, i registri visualizzeranno l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incolla la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per oscurare il piano di query

### Ottenete XPath spiegabile tramite il debugger di Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Utilizzate il debugger AEM QueryBuilder per generare una query XPath spiegabile:

Spiegare le query **all** durante il ciclo di sviluppo rispetto all&#39;indice di destinazione impostato.

**Ottenete XPath spiegabile tramite la registrazione**

* Abilitare i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante spiegabile

   * Andate a https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Create un nuovo logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.

* Una volta attivato DEBUG per la classe sopra riportata, i registri visualizzeranno l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incollare la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per ottenere il piano di query

**Ottenete XPath spiegabile tramite il debugger di Query Builder**

* Utilizzate il debugger AEM QueryBuilder per generare una query XPath spiegabile:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Fornisce la query Query Builder nel debugger di Query Builder
1. Eseguire la ricerca
1. Ottenete l&#39;XPath generato
1. Incollare la query XPath in Explain Query come XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non-querybuilder (XPath, JCR-SQL2) possono essere fornite direttamente a Explain Query.

Per un elenco a discesa su come eseguire il debug delle query con QueryBuilder, vedete il video seguente.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Debug di query con registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nella sezione [Creazione di propri logger e scrittori](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

L&#39;output di registro (livello INFO) dell&#39;implementazione del generatore di query durante l&#39;esecuzione della query descritta in Testing and Debugging:

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

Se si dispone di una query utilizzando i valutatori predicati che filtrano o utilizzano un ordine personalizzato per confronto, anche questo verrà notato nella query:

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
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | QueryBuilder di base e API Query |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bukets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Punti (contenuti nei facet) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Predicate Valutatori |
| [com.day.cq.search.facets.extrattori](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori di sfaccettature (per valutatori) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Scrittore di risultati JSON per il servlet Querybuilder (/bin/querybuilder.json) |

