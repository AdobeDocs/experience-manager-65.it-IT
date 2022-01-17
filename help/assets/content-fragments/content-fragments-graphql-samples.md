---
title: Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query
description: Scopri come utilizzare GraphQL con AEM per distribuire contenuti headless esplorando contenuti e query di esempio.
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
source-git-commit: 1a3d5a6b3b4f7af67d6a62cdaab484daa536cb63
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 6%

---

# Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Scopri come utilizzare GraphQL con AEM per distribuire contenuti headless esplorando contenuti e query di esempio.

>[!NOTE]
>
>Questa pagina deve essere letta insieme a:
>
>* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
>* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM API GraphQL per l’utilizzo con frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)


Per iniziare a utilizzare le query GraphQL e come funzionano con i frammenti di contenuto AEM è utile visualizzare alcuni esempi pratici.

Per assistenza, consulta:

* A [struttura dei frammenti di contenuto di esempio](#content-fragment-structure-graphql)

* E alcuni [query GraphQL di esempio](#graphql-sample-queries), in base alla struttura del frammento di contenuto di esempio (Modelli di frammento di contenuto e frammenti di contenuto correlati).


## GraphQL - Query di esempio utilizzando la struttura dei frammenti di contenuto di esempio {#graphql-sample-queries-sample-content-fragment-structure}

Vedi queste query di esempio per le illustrazioni di creazione query, insieme ai risultati di esempio.

>[!NOTE]
>
>A seconda dell’istanza, è possibile accedere direttamente al [Interfaccia GraphiQL inclusa con API GraphQL AEM](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) per l’invio e la verifica delle query.
>
>Esempio: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>Le query di esempio si basano sul [Struttura dei frammenti di contenuto di esempio da utilizzare con GraphQL](#content-fragment-structure-graphql)

### Query di esempio - Tutti gli schemi e i tipi di dati disponibili {#sample-all-schemes-datatypes}

Verrà restituito tutto `types` per tutti gli schemi disponibili.

**Query di esempio**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Risultato di esempio**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le informazioni su tutte le città {#sample-all-information-all-cities}

Per recuperare tutte le informazioni su tutte le città, è possibile utilizzare la query di base:
**Query di esempio**

```xml
{
  cityList {
    items
  }
}
```

Una volta eseguita, il sistema espanderà automaticamente la query per includere tutti i campi:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Query di esempio - Nomi di tutte le città {#sample-names-all-cities}

Questa è una query semplice per restituire il `name`di tutte le voci `city`schema.

**Query di esempio**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Query Di Esempio - Un Singolo Frammento Di Città Specifico {#sample-single-specific-city-fragment}

Si tratta di una query per restituire i dettagli di una singola voce di frammento in una posizione specifica nell’archivio.

**Query di esempio**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Query di esempio - Tutte le città con una variante denominata {#sample-cities-named-variation}

Se crei una nuova variante, denominata &quot;Centro Berlino&quot; (`berlin_centre`), per `city` A Berlino è quindi possibile utilizzare una query per restituire i dettagli della variante.

**Query di esempio**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Dettagli completi dell&#39;amministratore delegato e dei dipendenti di un&#39;azienda {#sample-full-details-company-ceos-employees}

Utilizzando la struttura dei frammenti nidificati, questa query restituisce tutti i dettagli dell&#39;amministratore delegato di una società e di tutti i relativi dipendenti.

**Query di esempio**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le persone con un nome &quot;Jobs&quot; o &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Questo filtra tutto `persons` per tutti quelli che hanno il nome `Jobs`o `Smith`.

**Query di esempio**

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le persone che non hanno un nome &quot;Jobs&quot; {#sample-all-persons-not-jobs}

Questo filtra tutto `persons` per tutti quelli che hanno il nome `Jobs`o `Smith`.

**Query di esempio**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le avventure di cui `_path` sta iniziando con un prefisso specifico {#sample-wknd-all-adventures-cycling-path-filter}

Tutto `adventures` dove `_path` inizia con un prefisso specifico (`/content/dam/wknd/en/adventures/cycling`).

**Query di esempio**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le città situate in Germania o Svizzera con una popolazione compresa tra 400000 e 999999 {#sample-all-cities-d-ch-population}

In questo caso viene filtrata una combinazione di campi. Un `AND` (implicito) viene utilizzato per selezionare il `population`intervallo, mentre `OR` (esplicito) viene utilizzato per selezionare le città richieste.

**Query di esempio**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Query di esempio - Tutte le città con SAN nel nome, indipendentemente dal caso {#sample-all-cities-san-ignore-case}

Questa query interroga tutte le città che hanno `SAN` nel nome, indipendentemente dal caso.

**Query di esempio**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Query di esempio - Filtro su una matrice con un elemento che deve verificarsi almeno una volta {#sample-array-item-occur-at-least-once}

Questa query filtra un array con un elemento (`city:na`) che deve verificarsi almeno una volta.

**Query di esempio**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio - Filtro su un valore di array esatto {#sample-array-exact-value}

Questa query filtra un valore di matrice esatto.

**Query di esempio**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio per frammenti di contenuto nidificato - Tutte le società con almeno un dipendente con un nome &quot;Smith&quot; {#sample-companies-employee-smith}

Questa query illustra il filtro per qualsiasi `person` di `name` &quot;Smith&quot;, che restituisce informazioni da due frammenti nidificati - `company` e `employee`.

**Query di esempio**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Query di esempio per frammenti di contenuto nidificato - Tutte le aziende in cui tutti i dipendenti hanno vinto il premio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Questa query illustra il filtraggio su tre frammenti nidificati - `company`, `employee`e `award`.

**Query di esempio**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Esempio di query per metadati - Elenco dei metadati per i riconoscimenti denominati GB {#sample-metadata-awards-gb}

Questa query illustra il filtraggio su tre frammenti nidificati - `company`, `employee`e `award`.

**Query di esempio**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Risultati di esempio**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Query di esempio con il progetto WKND {#sample-queries-using-wknd-project}

Queste query di esempio si basano sul progetto WKND. Ciò comporta:

* Modelli per frammenti di contenuto disponibili in:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Frammenti di contenuto (e altro contenuto) disponibili in:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Poiché i risultati possono essere estesi, non vengono riprodotti qui.

### Query di esempio per tutti i frammenti di contenuto di un determinato modello con le proprietà specificate {#sample-wknd-all-model-properties}

Questa query di esempio interroga:

* per tutti i frammenti di contenuto di tipo `article`
* con `path`e `author` proprietà.

**Query di esempio**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Query di esempio per metadati {#sample-wknd-metadata}

Questa query interroga:

* per tutti i frammenti di contenuto di tipo `adventure`
* Metadati

**Query di esempio**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Query di esempio per un singolo frammento di contenuto di un modello specificato {#sample-wknd-single-content-fragment-of-given-model}

Questa query di esempio interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno di tale, tutti i formati di contenuto:
      * HTML
      * Markdown
      * Testo normale
      * JSON

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Query di esempio per un modello di frammento di contenuto da un modello {#sample-wknd-content-fragment-model-from-model}

Questa query di esempio interroga:

* per un singolo frammento di contenuto
   * dettagli del modello di frammento di contenuto sottostante

**Query di esempio**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Query di esempio per un frammento di contenuto nidificato - Tipo di modello singolo{#sample-wknd-nested-fragment-single-model}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all’interno di esso, il percorso e l’autore del frammento a cui si fa riferimento (nidificato)

>[!NOTE]
>
>Il campo `referencearticle` ha il tipo di dati `fragment-reference`.

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Query di esempio per un frammento di contenuto nidificato - Tipo di modello multiplo{#sample-wknd-nested-fragment-multiple-model}

Questa query interroga:

* per più frammenti di contenuto di tipo `bookmark`
   * con i riferimenti ai frammenti ad altri frammenti di tipi di modelli specifici `article` e `adventure`

>[!NOTE]
>
>Il campo `fragments` ha il tipo di dati `fragment-reference`, con i modelli `Article`, `Adventure` selezionato.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Query di esempio per un frammento di contenuto di un modello specifico con riferimenti di contenuto{#sample-wknd-fragment-specific-model-content-reference}

Questa query contiene due informazioni:

1. Per restituire tutti i riferimenti al contenuto.
1. Per restituire riferimenti di contenuto specifici di tipo `attachments`.

Queste domande interrogano:

* per più frammenti di contenuto di tipo `bookmark`
   * con riferimenti a contenuti ad altri frammenti

#### Query di esempio per più frammenti di contenuto con riferimenti prerecuperati {#sample-wknd-multiple-fragments-prefetched-references}

La seguente query restituisce tutti i riferimenti di contenuto utilizzando `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Query di esempio per più frammenti di contenuto con allegati {#sample-wknd-multiple-fragments-attachments}

La seguente query restituisce tutti `attachments` - un campo specifico (sottogruppo) di tipo `content-reference`:

>[!NOTE]
>
>Il campo `attachments` ha il tipo di dati `content-reference`, con diversi moduli selezionati.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Query di esempio per un singolo frammento di contenuto con riferimento in linea RTE {#sample-wknd-single-fragment-rte-inline-reference}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `bookmark` in un percorso specifico
   * all’interno di questo, riferimenti in linea dell’editor Rich Text

>[!NOTE]
>
>I riferimenti in linea dell’editor Rich Text sono idratati in `_references`.

**Query di esempio**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Query di esempio per una singola variante di frammento di contenuto di un modello specificato {#sample-wknd-single-fragment-given-model}

Questa query interroga:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno di tale, i dati relativi alla variazione: `variation1`

**Query di esempio**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query di esempio per una variante denominata di più frammenti di contenuto di un modello specificato {#sample-wknd-variation-multiple-fragment-given-model}

Questa query interroga:

* per frammenti di contenuto di tipo `article` con una variazione specifica: `variation1`

**Query di esempio**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query di esempio per più frammenti di contenuto di una determinata impostazione internazionale {#sample-wknd-multiple-fragments-given-locale}

Questa query interroga:

* per frammenti di contenuto di tipo `article` all&#39;interno del `fr` locale

**Query di esempio**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## Struttura dei frammenti di contenuto di esempio (utilizzata con GraphQL) {#content-fragment-structure-graphql}

Le query di esempio si basano sulla seguente struttura, che utilizza:

* Uno o più [Modelli per frammenti di contenuto di esempio](#sample-content-fragment-models-schemas) - costituisce la base per gli schemi GraphQL

* [Frammenti di contenuto di esempio](#sample-content-fragments) in base ai modelli di cui sopra

### Modelli per frammenti di contenuto di esempio (schemi) {#sample-content-fragment-models-schemas}

Per le query di esempio, utilizzeremo i seguenti Modelli di contenuto e le loro interrelazioni (riferimenti ->):

* [Azienda](#model-company)
-> [Persona](#model-person)
    -> [Premio](#model-award)

* [Città](#model-city)

#### Azienda {#model-company}

I campi di base che definiscono la società sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome dell&#39;azienda | Testo su riga singola |  |
| Amministratore delegato | Riferimento frammento (singolo) | [Person](#model-person) |
| Dipendenti | Riferimento frammento (campo multiplo) | [Persona](#model-person) |

#### Person {#model-person}

I campi che definiscono una persona, che può anche essere un dipendente:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome | Testo su riga singola |  |
| Nome | Testo su riga singola |  |
| Premi | Riferimento frammento (campo multiplo) | [Premio](#model-award) |

#### Premio {#model-award}

I campi che definiscono un premio sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Collegamento/ID | Testo su riga singola |  |
| Titolo | Testo su riga singola |  |

#### Città {#model-city}

I campi per la definizione di una città sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome | Testo su riga singola |  |
| Paese | Testo su riga singola |  |
| Popolazione | Numero |  |
| Categorie | Tag |  |

### Frammenti di contenuto di esempio {#sample-content-fragments}

I frammenti seguenti vengono utilizzati per il modello appropriato.

#### Azienda {#fragment-company}

| Nome dell&#39;azienda | Amministratore delegato | Dipendenti |
|--- |--- |--- |
| Apple | Steve Jobs | Duca Marsh<br>Max campo |
|  Little Pony Inc. | Adam Smith | Lara croft<br>Sfera di taglio |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nome | Nome | Premi |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Slave |  Cagliare |  Gameblitz<br>Gamestar |
| Palude |  Duca |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Processi |  Steve |   |

#### Premio {#fragment-award}

| Collegamento/ID | Titolo |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Città {#fragment-city}

| Nome | Paese | Popolazione | Categorie |
|--- |--- |--- |--- |
| Basilea | Svizzera | 172258 | città:emea |
| Berlino | Germania | 3669491 | città:capitale<br>città:emea |
| Bucarest | Romania | 1821000 |  città:capitale<br>città:emea |
| San Francisco |  USA |  883306 |  città:spiaggia<br>città:na |
| San Jose |  USA |  102635 |  città:na |
| Stoccarda |  Germania |  634830 |  città:emea |
|  Zurigo |  Svizzera |  415367 |  città:capitale<br>città:emea |
