---
title: Ottimizzazione delle query GraphQL
description: Scopri come ottimizzare le query GraphQL per filtrare, impaginare e ordinare i frammenti di contenuto in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# Ottimizzazione delle query GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Prima di applicare queste raccomandazioni di ottimizzazione, considera [Aggiornamento dei frammenti di contenuto per il paging e l’ordinamento nel filtro GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) per prestazioni ottimali.

In un’istanza AEM con un numero elevato di frammenti di contenuto condivisi dallo stesso modello, le query di elenco GraphQL possono diventare costose (in termini di risorse).

Il motivo è perché *tutto* i frammenti che condividono un modello utilizzato all’interno della query GraphQL devono essere caricati in memoria. Questa operazione richiede tempo e memoria. Il filtro, che può ridurre il numero di elementi nel set di risultati (finale), può essere applicato solo **dopo** il caricamento dell’intero set di risultati in memoria.

Questo processo può portare all’impressione che anche piccoli set di risultati (possono) portare a prestazioni errate. Tuttavia, in realtà, la lentezza è causata dalle dimensioni del set di risultati iniziale, in quanto deve essere gestito internamente prima di poter applicare il filtro.

Per ridurre i problemi di prestazioni e memoria, il set di risultati iniziale deve essere ridotto il più possibile.

AEM consente due approcci per ottimizzare le query GraphQL:

* [Filtro ibrido](#hybrid-filtering)
* [Paging](#paging) (o impaginazione)

   * [Ordinamento](#sorting) non è direttamente correlato all’ottimizzazione, ma è correlato al paging

Ogni approccio ha i propri casi d’uso e limitazioni. Questo documento fornisce informazioni su Filtro ibrido e Paging, con alcune [best practice](#best-practices) per ottimizzare le query GraphQL.

## Filtro ibrido {#hybrid-filtering}

Il filtro ibrido combina il filtro JCR con il filtro AEM.

Un filtro JCR viene applicato (sotto forma di vincolo di query) prima di caricare il set di risultati in memoria per il filtro AEM. Questo processo riduce il set di risultati caricato in memoria, in quanto il filtro JCR rimuove prima i risultati superflui.

>[!NOTE]
>
>Per motivi tecnici (ad esempio, flessibilità, nidificazione di frammenti), l’AEM non può delegare l’intero filtro al JCR.

Questa tecnica mantiene la flessibilità fornita dai filtri GraphQL, delegando la maggior parte del filtro possibile a JCR.

## Paging {#paging}

GraphQL nell’AEM supporta due tipi di impaginazione:

* [paginazione basata su limite/scostamento](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Questo tipo di impaginazione viene utilizzato per le query elenco; queste query terminano con 
`List`; per esempio, `articleList`.
Per utilizzarlo, devi fornire la posizione del primo elemento da restituire (il `offset`) e il numero di elementi da restituire (il `limit`, o dimensioni della pagina).

* [paginazione basata su cursore](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (rappresentante: `first`e `after`) Questo tipo di impaginazione fornisce un ID univoco per ogni elemento, noto anche come cursore.
Nella query, si specifica il cursore dell’ultimo elemento della pagina precedente, più le dimensioni della pagina (il numero massimo di elementi da restituire).

   Poiché l’impaginazione basata su cursore non si adatta alle strutture di dati delle query basate su elenco, AEM ha introdotto il tipo di query `Paginated`; ad esempio, `articlePaginated`. Le strutture di dati e i parametri utilizzati seguono i [Specifica di connessione cursore GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM attualmente supporta il paging in avanti (utilizzando i parametri `after`/`first`).
   >
   >Il paging all’indietro (utilizzando `before`/`last`) non è supportato.

## Ordinamento {#sorting}

L’ordinamento può essere efficiente solo se tutti i criteri di ordinamento sono correlati ai frammenti di primo livello.

Se l’ordinamento include uno o più campi presenti in un frammento nidificato, tutti i frammenti che condividono il modello di livello principale devono essere caricati in memoria. Questo flusso causa un impatto negativo sulle prestazioni.

>[!NOTE]
>
>L’ordinamento sui campi di livello superiore ha anche un impatto sulle prestazioni, seppure ridotto.

## Best practice {#best-practices}

L’obiettivo principale di tutte le ottimizzazioni è ridurre il set di risultati iniziale. Le best practice elencate di seguito indicano come farlo. Possono (e devono) essere combinate.

### Filtrare solo le proprietà di livello superiore {#filter-top-level-properties-only}

Attualmente, il filtro a livello JCR funziona solo per i frammenti di livello superiore.

Se un filtro comprende i campi di un frammento nidificato, AEM deve ricorrere al caricamento (nella memoria) di tutti i frammenti che condividono il modello sottostante.

Puoi comunque ottimizzare tali query GraphQL combinando espressioni filtro su campi di frammenti di primo livello e su campi di frammenti nidificati con [Operatore AND](#logical-operations-in-filter-expressions).

### Utilizzare la struttura del contenuto {#use-content-structure}

Nell’AEM, si ritiene buona prassi utilizzare la struttura dell’archivio per limitare l’ambito dei contenuti da elaborare.

Applica questo approccio alle query GraphQL applicando un filtro sulla `_path` campo del frammento di livello principale:

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

Se filtri o esegui l’ordinamento in base a frammenti nidificati, le query impaginate possono risultare ancora lente in quanto l’AEM deve ancora caricare in memoria quantità maggiori di frammenti. Pertanto, se combini filtri e paging, tieni in considerazione le regole per il filtraggio (come indicato sopra).

Per il paging, l’ordinamento è ugualmente importante, in quanto i risultati impaginati vengono sempre ordinati in modo esplicito o implicito.

Se sei principalmente interessato a recuperare solo le prime pagine, non vi è alcuna differenza significativa tra l’utilizzo le query `...List` o `...Paginated`. Tuttavia, se l’applicazione è interessata a leggere più di una o due pagine, è necessario considerare la query `...Paginated` , poiché offre prestazioni notevolmente migliori con le pagine successive.

### Operazioni logiche nelle espressioni di filtro {#logical-operations-in-filter-expressions}

Se esegui il filtro su frammenti nidificati, puoi comunque applicare il filtro JCR fornendo un filtro correlato su un campo di livello principale combinato utilizzando `AND` operatore.

Un caso d’uso tipico consiste nel limitare l’ambito della query utilizzando un filtro sulla `_path` del frammento di livello principale. Quindi, filtra altri campi che potrebbero trovarsi al livello superiore o su un frammento nidificato.

In questo caso, le diverse espressioni di filtro vengono combinate con `AND`. Pertanto, il filtro su `_path` può limitare efficacemente il set di risultati iniziale. Tutti gli altri filtri sui campi di livello superiore possono aiutare a ridurre il set di risultati iniziale, purché siano combinati con `AND`.

Le espressioni di filtro combinate con `OR` non possono essere ottimizzate se sono interessati dei frammenti nidificati. Tali `OR` le espressioni possono essere ottimizzate solo se *no* sono coinvolti frammenti nidificati.

### Evitare di filtrare i campi di testo su più righe {#avoid-filtering-multiline-textfields}

I campi di un campo di testo multiriga (html, markdown, testo normale, json) non possono essere filtrati tramite una query JCR, in quanto il contenuto di tali campi deve essere calcolato al volo.

Se è ancora necessario filtrare in base a un campo di testo multiriga, è consigliabile limitare la dimensione del set di risultati iniziale aggiungendo ulteriori espressioni di filtro e combinarle con `AND`. Limitare l’ambito filtrando sul campo `_path` è un altro buon approccio.

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

* Filtrare le espressioni su una `Calendar`, `Date`, o `Time` valore che utilizza il `NOT_AT` operatore.
