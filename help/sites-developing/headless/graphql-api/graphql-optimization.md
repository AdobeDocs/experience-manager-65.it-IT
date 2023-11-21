---
title: Ottimizzazione delle query GraphQL
description: Scopri come ottimizzare le query GraphQL per filtrare, impaginare e ordinare i frammenti di contenuto in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 58%

---

# Ottimizzazione delle query GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Prima di applicare queste raccomandazioni di ottimizzazione, considera [Aggiornamento dei frammenti di contenuto per il paging e l’ordinamento nel filtro GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) per prestazioni ottimali.

Queste linee guida servono a prevenire problemi di prestazioni con le query GraphQL.

## Elenco di controllo GraphQL {#graphql-checklist}

Il seguente elenco di controllo ha lo scopo di aiutarti a ottimizzare la configurazione e l’utilizzo di GraphQL in Adobe Experience Manager (AEM) as a Cloud Service.

### Primi Principi {#first-principles}

#### Utilizzare query GraphQL persistenti {#use-persisted-graphql-queries}

**Consiglio**

Si consiglia vivamente l’utilizzo di query GraphQL persistenti.

Le query GraphQL persistenti consentono di ridurre le prestazioni di esecuzione delle query utilizzando la rete CDN (Content Delivery Network). Le applicazioni client richiedono query persistenti con richieste GET per un’esecuzione rapida abilitata per Edge.

**Ulteriori riferimenti**

Consulta:

* [Query GraphQL persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### Installare il pacchetto dell’indice di GraphQL {#install-graphql-index-package}

**Consiglio**

Clienti che utilizzano GraphQL *deve* installa il pacchetto Experience Manager Frammento di contenuto con indice GraphQL. In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate. Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

Consulta le Note sulla versione per la versione appropriata per il tuo Service Pack. Ad esempio, per il Service Pack più recente, vedi [Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

**Ulteriori riferimenti**
Consulta:

* [Installare il pacchetto di indice GraphQL per frammenti di contenuto Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### Strategia cache {#cache-strategy}

Per l’ottimizzazione si possono utilizzare anche vari metodi di caching.

#### Abilita caching del Dispatcher AEM {#enable-aem-dispatcher-caching}

**Consiglio**

[Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) è la cache di primo livello all’interno del servizio AEM, prima della cache CDN.

**Ulteriori riferimenti**

Consulta:

* [Query persistenti GraphQL: abilitazione della memorizzazione nella cache in Dispatcher](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### Utilizzare una rete per la distribuzione dei contenuti (CDN) {#use-cdn}

**Consiglio**

Le query GraphQL e le relative risposte JSON possono essere memorizzate nella cache se impostate come `GET` richieste quando si utilizza una rete CDN. Al contrario, le richieste non memorizzate nella cache possono essere molto (risorse) costose e lente da elaborare, con il potenziale di ulteriori effetti negativi sulle risorse dell’origine.

**Ulteriori riferimenti**

Consulta:

* [Utilizzo della CDN nell’AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it#using-dispatcher-with-a-cdn)

#### Impostare le intestazioni di controllo cache HTTP {#set-http-cache-control-headers}

**Consiglio**

Quando si utilizzano query GraphQL persistenti con una rete CDN, si consiglia di impostare intestazioni di controllo della cache HTTP appropriate.

Ogni query persistente può avere un proprio set specifico di intestazioni di controllo cache. Le intestazioni possono essere impostate su [API GRAPHQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

Possono essere impostati anche utilizzando **cURL** strumento da riga di comando. Ad esempio, utilizzando un’ `PUT` richiesta di creare una query normale racchiusa con controllo cache.

```shell
$ curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**Ulteriori riferimenti**

Consulta:

* [Memorizzazione in cache delle query persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [Rendere persistente una query GraphQL](/help/sites-developing/headless/graphql-api/persisted-queries.md#how-to-persist-query)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### Ottimizzazione query GraphQL {#graphql-query-optimization}

In un’istanza AEM con un numero elevato di frammenti di contenuto che condividono lo stesso modello, le query di elenco GraphQL possono diventare costose (in termini di risorse).

Questo perché devono essere caricati in memoria *tutti* i frammenti che condividono un modello utilizzato all’interno della query GraphQL. Ciò richiede tempo e memoria. Il filtro, che può ridurre il numero di elementi nel set di risultati (finale), può essere applicato solo **dopo** il caricamento dell’intero set di risultati in memoria.

Questo può dare l’impressione che anche piccoli set di risultati portino a cattive prestazioni. Tuttavia, in realtà la lentezza è causata dalle dimensioni del set di risultati iniziale, in quanto deve essere gestito internamente prima di poter applicare il filtro.

Per ridurre i problemi di prestazioni e memoria, il set di risultati iniziale deve essere ridotto il più possibile.

AEM consente due approcci per ottimizzare le query GraphQL:

* [Filtro ibrido](#use-aem-graphql-hybrid-filtering)
* [Paging](#use-aem-graphql-pagination) (o impaginazione)

   * [Ordinamento](#use-graphql-sorting) non è direttamente correlato all’ottimizzazione, ma è correlato al paging

Ogni approccio ha i propri casi d’uso e limitazioni. Questa sezione fornisce informazioni su Filtro e paging ibridi, insieme ad alcuni [best practice](#best-practices) da utilizzare nell’ottimizzazione delle query GraphQL.

#### Utilizzare il filtro ibrido AEM GraphQL {#use-aem-graphql-hybrid-filtering}

**Consiglio**

Il filtro ibrido combina il filtro JCR con il filtro AEM.

Un filtro JCR viene applicato (sotto forma di vincolo di query) prima di caricare il set di risultati in memoria per il filtro AEM. In questo modo si riduce il set di risultati caricato in memoria, dato che il filtro JCR rimuove i risultati superflui precedenti.

>[!NOTE]
>
>Per motivi tecnici (ad esempio flessibilità o nidificazione di frammenti), AEM non può delegare l’intera operazione di filtro a JCR.

Questa tecnica mantiene la flessibilità fornita dai filtri GraphQL, delegando la maggior parte del filtro possibile a JCR.

>[!NOTE]
>
>Il filtro ibrido AEM richiede l’aggiornamento dei frammenti di contenuto esistenti

**Ulteriori riferimenti**

Consulta:

* [Aggiornamento dei frammenti di contenuto per il paging e l’ordinamento nel filtro GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [Query di esempio con filtro per ID _tags e varianti escluse](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### Usa paginazione GraphQL {#use-aem-graphql-pagination}

**Consiglio**

Il tempo di risposta di query complesse, con set di risultati di grandi dimensioni, può essere migliorato segmentando le risposte in blocchi utilizzando l’impaginazione, uno standard di GraphQL.

GraphQL nell’AEM supporta due tipi di impaginazione:

* [paginazione basata su limite/scostamento](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Viene utilizzato per le query elenco; queste terminano con `List`ad esempio, `articleList`.
Per utilizzarlo, devi fornire la posizione del primo elemento da restituire (il `offset`) e il numero di elementi da restituire (il `limit`, o dimensioni della pagina).

* [paginazione basata su cursore](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (rappresentato da `first` e `after`)
Fornisce un ID univoco per ciascun elemento, noto anche come cursore.
Nella query, si specifica il cursore dell’ultimo elemento della pagina precedente, più le dimensioni della pagina (il numero massimo di elementi da restituire).

  Poiché l’impaginazione basata su cursore non si adatta alle strutture di dati delle query basate su elenco, AEM ha introdotto il tipo di query `Paginated`; ad esempio, `articlePaginated`. Le strutture di dati e i parametri utilizzati seguono i [Specifica di connessione cursore GraphQL](https://relay.dev/graphql/connections.htm).

  >[!NOTE]
  >
  >AEM attualmente supporta il paging in avanti (utilizzando i parametri `after`/`first`).
  >
  >Il paging all’indietro (utilizzando `before`/`last`) non è supportato.

**Ulteriori riferimenti**

Consulta:

* [Query di impaginazione di esempio utilizzando prima e dopo](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### Usa ordinamento GraphQL {#use-graphql-sorting}

**Consiglio**

Inoltre, uno standard GraphQL, l’ordinamento consente ai client di ricevere contenuti JSON in ordine ordinato. Questo può ridurre la necessità di ulteriori elaborazioni sul client.

L’ordinamento può essere efficiente solo se tutti i criteri di ordinamento sono correlati ai frammenti di primo livello.

Se l’ordinamento include uno o più campi che si trovano su un frammento nidificato, tutti i frammenti che condividono il modello di livello principale devono essere caricati in memoria. Questo causa un impatto negativo sulle prestazioni.

>[!NOTE]
>
>L’ordinamento sui campi di livello superiore ha anche un impatto sulle prestazioni, seppure ridotto.

**Ulteriori riferimenti**

Consulta:

* [Query di esempio con filtro per ID _tags ed varianti escluse e ordinamento per nome](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## Best practice {#best-practices}

L’obiettivo principale di tutte le raccomandazioni di ottimizzazione è ridurre il set di risultati iniziale. Le best practice elencate di seguito indicano come farlo. Possono (e devono) essere combinate.

### Filtrare solo le proprietà di livello superiore {#filter-top-level-properties-only}

Attualmente, il filtro a livello JCR funziona solo per i frammenti di livello superiore.

Se un filtro comprende i campi di un frammento nidificato, AEM deve ricorrere al caricamento (nella memoria) di tutti i frammenti che condividono il modello sottostante.

Puoi comunque ottimizzare tali query GraphQL combinando espressioni filtro su campi di frammenti di primo livello e su campi di frammenti nidificati con l’[operatore AND](#logical-operations-in-filter-expressions).

### Utilizzare la struttura del contenuto {#use-content-structure}

In AEM, si ritiene generalmente buona prassi utilizzare la struttura dell’archivio per restringere l’ambito dei contenuti da elaborare.

Questo approccio deve essere applicato anche alle query GraphQL.

A questo scopo, puoi applicare un filtro sul campo `_path` del frammento di livello principale:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>Il finale `/` su `value` è necessario per ottenere le migliori prestazioni.

### Usare il paging {#use-paging}

È inoltre possibile utilizzare il paging per ridurre il set di risultati iniziale, in particolare se le richieste non utilizzano alcun filtro e ordinamento.

Se si filtra o si ordina in base a frammenti nidificati, le query impaginate possono ancora risultare lente, in quanto l’AEM potrebbe dover ancora caricare in memoria grandi quantità di frammenti. Pertanto, se combini filtri e paging, tieni in considerazione le regole per il filtraggio (come indicato sopra).

Per il paging, l’ordinamento è ugualmente importante, in quanto i risultati impaginati vengono sempre ordinati in modo esplicito o implicito.

Se sei principalmente interessato a recuperare solo le prime pagine, non vi è alcuna differenza significativa tra l’utilizzo le query `...List` o `...Paginated`. Tuttavia, se l’applicazione è interessata a leggere più di una o due pagine, è necessario considerare la query `...Paginated` , poiché offre prestazioni notevolmente migliori con le pagine successive.

### Operazioni logiche nelle espressioni di filtro {#logical-operations-in-filter-expressions}

Se esegui il filtro su frammenti nidificati, puoi comunque applicare il filtro JCR fornendone uno correlato su un campo di livello principale combinato utilizzando l’operatore `AND`.

Un caso d’uso tipico è quello di limitare l’ambito della query utilizzando un filtro sul campo `_path` del frammento di livello principale, per poi applicare un filtro ai campi aggiuntivi che potrebbero trovarsi nel livello principale o in un frammento nidificato.

In questo caso, le diverse espressioni di filtro vengono combinate con `AND`. Pertanto, il filtro su `_path` può limitare efficacemente il set di risultati iniziale. Tutti gli altri filtri sui campi di livello superiore possono aiutare a ridurre il set di risultati iniziale, purché siano combinati con `AND`.

Le espressioni di filtro combinate con `OR` non possono essere ottimizzate se sono interessati dei frammenti nidificati. Le espressioni `OR` possono essere ottimizzate solo se *nessun* frammento nidificato è coinvolto.

### Evitare di filtrare i campi di testo su più righe {#avoid-filtering-multiline-textfields}

I campi di un campo di testo multiriga (html, markdown, testo semplice, JSON) non possono essere filtrati tramite una query JCR, in quanto il contenuto di tali campi deve essere calcolato al volo.

Se devi ancora filtrare un campo di testo multiriga, prova a limitare la dimensione del set di risultati iniziale aggiungendo ulteriori espressioni di filtro e combinale con `AND`. Limitare l’ambito filtrando sul campo `_path` è un altro buon approccio.

### Evitare di filtrare i campi virtuali {#avoid-filtering-virtual-fields}

I campi virtuali (la maggior parte dei campi inizia con `_`) vengono calcolati durante l’esecuzione di una query GraphQL e non rientrano pertanto nell’ambito del filtro basato su JCR.

Un’eccezione importante è il campo `_path`, che può essere utilizzato in modo efficace per ridurre le dimensioni del set di risultati iniziale, se il contenuto è strutturato di conseguenza (vedi [Utilizzare la struttura del contenuto](#use-content-structure)).

### Filtro: esclusioni {#filtering-exclusions}

Ci sono molte altre situazioni in cui un’espressione di filtro non può essere valutata a livello JCR (e quindi deve essere evitata per ottenere le migliori prestazioni):

* Espressioni di filtro su un valore `Float` che utilizzano l’opzione filtro `_sensitiveness` e dove `_sensitiveness` è impostato su un valore diverso da `0.0`.

* Espressioni di filtro sul valore `String` che utilizzano l’opzione filtro `_ignoreCase`.

* Filtro sui valori `null`.

* Filtri su array con `_apply: ALL_OR_EMPTY`.

* Filtri su array con `_apply: INSTANCES`, `_instances: 0`.

* Espressioni di filtro che utilizzano l’operatore `CONTAINS_NOT`.

* Espressioni di filtro su un valore `Calendar`, `Date` o `Time` che utilizza l’operatore `NOT_AT`.

### Riduci a icona la nidificazione dei frammenti di contenuto {#minimize-content-fragment-nesting}

La nidificazione dei frammenti di contenuto è un ottimo modo per modellare strutture di contenuto personalizzate. Puoi anche avere un frammento con un frammento nidificato con un frammento nidificato, con... e così via.

Tuttavia, la creazione di una struttura con troppi livelli può aumentare i tempi di elaborazione di una query GraphQL, in quanto GraphQL deve attraversare l’intera gerarchia di tutti i frammenti di contenuto nidificati.

Una nidificazione approfondita può anche avere effetti negativi sulla governance dei contenuti. In generale, si consiglia di limitare la nidificazione dei frammenti di contenuto a meno di cinque o sei livelli.

### Non generare tutti i formati (elementi di testo su più righe) {#do-not-output-all-formats}

AEM GraphQL può restituire il testo, creato nel **[Testo su più righe](/help/assets/content-fragments/content-fragments-models.md#data-types)** tipo di dati, in più formati: Rich Text, Simple Text e Markdown.

L’output di tutti e tre i formati aumenta la dimensione dell’output di testo in JSON di un fattore di tre. Questo, combinato con set di risultati generalmente grandi da query molto ampie, può produrre risposte JSON molto grandi che richiedono quindi molto tempo per il calcolo. È meglio limitare l’output solo ai formati di testo necessari per il rendering del contenuto.

### Modifica dei frammenti di contenuto {#modifying-content-fragments}

Modifica solo i frammenti di contenuto e le relative risorse, utilizzando l’interfaccia utente o le API dell’AEM. Non apportare modifiche direttamente in JCR.

### Verificare le query {#test-your-queries}

L’elaborazione delle query GraphQL è simile all’elaborazione delle query di ricerca ed è notevolmente più complessa delle semplici richieste API per tutti i contenuti di GET.

Pianificare, testare e ottimizzare accuratamente le query in un ambiente controllato non di produzione è fondamentale per il successo successivo quando viene utilizzato in produzione.
