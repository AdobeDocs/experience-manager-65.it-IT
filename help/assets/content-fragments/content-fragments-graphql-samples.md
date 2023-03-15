---
title: 'Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query'
description: Scopri come utilizzare GraphQL con AEM per distribuire contenuti headless esplorando contenuti e query di esempio.
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
source-git-commit: bb5d39277db10fd8d3b436c8d1f40d9d2010adee
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 93%

---

# Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Scopri come utilizzare GraphQL con AEM per distribuire contenuti headless esplorando contenuti e query di esempio.

>[!NOTE]
>
>Questa pagina deve essere letta insieme a:
>
>* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
>* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
>* [API GraphQL AEM per l’utilizzo con Frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)


Come introduzione alle query GraphQL e per scoprire come funzionano con i Frammenti di contenuto AEM è utile visualizzare alcuni esempi pratici.

Per assistenza, consulta:

* Un [esempio di struttura dei Frammenti di contenuto](#content-fragment-structure-graphql)

* E alcuni [esempi di query GraphQL](#graphql-sample-queries), in base alla struttura del frammento di contenuto di esempio (modelli di Frammento di contenuto e frammenti di contenuto correlati).


## GraphQL: query di esempio con l’utilizzo della struttura dei frammenti di contenuto di esempio {#graphql-sample-queries-sample-content-fragment-structure}

Approfondisci queste query di esempio per le illustrazioni di creazione query, insieme ai risultati di esempio.

>[!NOTE]
>
>A seconda dell’istanza, è possibile accedere direttamente all’[Interfaccia GraphiQL inclusa con API GraphQL AEM](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) per l’invio e la verifica delle query.
>
>Esempio: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>Le query di esempio si basano sulla [struttura dei frammenti di contenuto di esempio da utilizzare con GraphQL](#content-fragment-structure-graphql)

### Query di esempio: tutti gli schemi e i tipi di dati disponibili {#sample-all-schemes-datatypes}

Il risultato comprende tutti i `types` di tutti gli schemi disponibili.

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

### Query di esempio: tutte le informazioni su tutte le città {#sample-all-information-all-cities}

Per recuperare tutte le informazioni su tutte le città, puoi utilizzare la query di base:
**Query di esempio**

```xml
{
  cityList {
    items
  }
}
```

Una volta eseguita, il sistema la espanderà automaticamente per includere tutti i campi:

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

### Query di esempio: nomi di tutte le città {#sample-names-all-cities}

Questa è una query semplice che restituisce `name` tutte le voci dello `city` schema.

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

### Query di esempio: un singolo frammento di città specifico {#sample-single-specific-city-fragment}

Si tratta di una query che restituisce i dettagli di una singola voce di frammento in una posizione specifica nell’archivio.

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

### Query di esempio: tutte le città con una variante denominata {#sample-cities-named-variation}

Se crei una nuova variante, denominata “Berlino centro” (`berlin_centre`), relativa alla `city` Berlino, puoi utilizzare una query per restituire i dettagli della variante.

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

### Query di esempio: nomi di tutte le città Contrassegnati come interruzioni città {#sample-names-all-cities-tagged-city-breaks}

Se:

* creare una varietà di tag, denominati `Tourism` : `Business`, `City Break`, `Holiday`
* e assegnarle alla variante principale di varie `City` istanze

Puoi quindi utilizzare una query per restituire i dettagli del `name` e `tags`di tutte le voci con tag di City Breaks nel `city`schema.

**Query di esempio**

```xml
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
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
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        }
      ]
    }
  }
}
```

### Query di esempio: dettagli completi del CEO e dei dipendenti di un’azienda {#sample-full-details-company-ceos-employees}

Utilizzando la struttura dei frammenti nidificati, questa query restituisce tutti i dettagli del CEO e di tutti i dipendenti di una società.

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

### Query di esempio: tutte le persone con nome “Jobs” o “Smith” {#sample-all-persons-jobs-smith}

Questo filtra tutte le `persons` che hanno il nome `Jobs` o `Smith`.

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

### Query di esempio: tutte le persone che non hanno nome “Jobs” {#sample-all-persons-not-jobs}

Questo filtra tutte le `persons` che hanno il nome `Jobs` o `Smith`.

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

### Query di esempio: tutte le avventure il cui `_path` inizia con un prefisso specifico {#sample-wknd-all-adventures-cycling-path-filter}

Tutte le `adventures` il cui `_path` inizia con un prefisso specifico (`/content/dam/wknd/en/adventures/cycling`).

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

### Query di esempio: tutte le città situate in Germania o Svizzera con una popolazione compresa tra 400000 e 999999 {#sample-all-cities-d-ch-population}

In questo caso il filtro è impostato su una combinazione di campi. Viene utilizzato un `AND` (implicito) per selezionare l’intervallo di `population`, mentre un `OR` (esplicito) viene utilizzato per selezionare le città richieste.

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

### Query di esempio: tutte le città con SAN nel nome, indipendentemente dalla maiuscola {#sample-all-cities-san-ignore-case}

Questa query interroga tutte le città che hanno `SAN` nel nome, indipendentemente dalla maiuscola.

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

### Query di esempio: filtro su un array con un elemento che deve verificarsi almeno una volta {#sample-array-item-occur-at-least-once}

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

### Query di esempio: filtro su un valore di array esatto {#sample-array-exact-value}

Questa query filtra un determinato valore di array.

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

### Query di esempio per frammenti di contenuto nidificato: tutte le società con almeno un dipendente che ha nome “Smith” {#sample-companies-employee-smith}

Questa query illustra il filtro per qualsiasi `person` di `name` “Smith” e restituisce informazioni da due frammenti nidificati, `company` e `employee`.

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

### Query di esempio per frammenti di contenuto nidificato: tutte le aziende in cui tutti i dipendenti hanno vinto il premio “Gamestar” {#sample-all-companies-employee-gamestar-award}

Questa query illustra il filtraggio su tre frammenti nidificati: `company`, `employee` e `award`.

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

### Esempio di query per metadati: elenco dei metadati per i riconoscimenti denominati GB {#sample-metadata-awards-gb}

Questa query illustra il filtraggio su tre frammenti nidificati: `company`, `employee` e `award`.

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

Queste query di esempio si basano sul progetto WKND. Caratteristiche:

* Modelli di Frammento di contenuto disponibili in:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Frammenti di contenuto (e altro contenuto) disponibili in:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Poiché i risultati possono essere estesi, non vengono riprodotti qui.

### Query di esempio per tutti i Frammenti di contenuto di un determinato modello con le proprietà specificate {#sample-wknd-all-model-properties}

Questa query di esempio rappresenta un’interrogazione per ottenere:

* per tutti i Frammenti di contenuto di tipo `article`
* con proprietà `path` e `author`.

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

Questa query rappresenta un’interrogazione per ottenere:

* per tutti i frammenti di contenuto di tipo `adventure`
* metadati

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

### Query di esempio per un singolo Frammento di contenuto di un modello specificato {#sample-wknd-single-content-fragment-of-given-model}

Questa query di esempio rappresenta un’interrogazione per ottenere:

* per un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all’interno del quale, sono presenti tutti i formati di contenuto:
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

### Query di esempio per un modello per frammenti di contenuto derivante da un modello {#sample-wknd-content-fragment-model-from-model}

Questa query di esempio rappresenta un’interrogazione per ottenere:

* un singolo frammento di contenuto
   * dettagli del modello per frammenti di contenuto sottostante

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

### Query di esempio per un frammento di contenuto nidificato: tipo di modello singolo {#sample-wknd-nested-fragment-single-model}

Questa query rappresenta un’interrogazione per ottenere:

* un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all’interno del quale, è presente il percorso e l’autore del frammento (nidificato) a cui si fa riferimento

>[!NOTE]
>
>Il campo `referencearticle` include il tipo di dati `fragment-reference`.

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

### Query di esempio per un frammento di contenuto nidificato: più tipi di modello {#sample-wknd-nested-fragment-multiple-model}

Questa query rappresenta un’interrogazione per ottenere:

* più frammenti di contenuto di tipo `bookmark`
   * con riferimenti ai frammenti per altri frammenti di tipi di modello specifici `article` e `adventure`

>[!NOTE]
>
>Il campo `fragments` include il tipo di dati `fragment-reference`, con i modelli `Article`, `Adventure` selezionati.

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

### Query di esempio per un frammento di contenuto di un modello specifico con riferimenti ai contenuti {#sample-wknd-fragment-specific-model-content-reference}

Sono disponibili due tipi di questa query:

1. Per restituire tutti i riferimenti ai contenuti.
1. Per restituire riferimenti a contenuti specifici di tipo `attachments`.

Tali query rappresentano interrogazioni per ottenere:

* più frammenti di contenuto di tipo `bookmark`
   * con riferimenti ai contenuti per altri frammenti

#### Query di esempio per più frammenti di contenuto con riferimenti di prelettura {#sample-wknd-multiple-fragments-prefetched-references}

La query seguente restituisce tutti i riferimenti di contenuto utilizzando `_references`:

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

La query seguente restituisce tutti gli `attachments`: un campo specifico (gruppo secondario) di tipo `content-reference`:

>[!NOTE]
>
>Il campo `attachments` include il tipo di dati `content-reference`, con diversi moduli selezionati.

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

### Query di esempio per un singolo frammento di contenuto con riferimento dell’editor Rich Text in linea {#sample-wknd-single-fragment-rte-inline-reference}

Questa query rappresenta un’interrogazione per ottenere:

* un singolo frammento di contenuto di tipo `bookmark` in un percorso specifico
   * all’interno del quale, sono presenti riferimenti dell’editor Rich Text in linea

>[!NOTE]
>
>I riferimenti dell’editor Rich Text in linea vengono popolati in `_references`.

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

### Query di esempio per una singola variante di frammento di contenuto di un determinato modello {#sample-wknd-single-fragment-given-model}

Questa query rappresenta un’interrogazione per ottenere:

* un singolo frammento di contenuto di tipo `article` in un percorso specifico
   * all&#39;interno del quale, sono presenti dati relativi alla variante: `variation1`

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

### Query di esempio per una variante denominata di più frammenti di contenuto di un determinato modello {#sample-wknd-variation-multiple-fragment-given-model}

Questa query rappresenta un’interrogazione per ottenere:

* frammenti di contenuto di tipo `article` con una variante specifica: `variation1`

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

### Query di esempio per più frammenti di contenuto e relative varianti di un modello specifico {#sample-wknd-multiple-fragment-variations-given-model}

Questa query rappresenta un’interrogazione:

* per frammenti di contenuto di tipo `article` e tutte le varianti

**Query di esempio**

```xml
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Query di esempio per le varianti di frammento di contenuto di un modello specifico a cui è associato un tag specifico{#sample-wknd-fragment-variations-given-model-specific-tag}

Questa query rappresenta un’interrogazione:

* per frammenti di contenuto di tipo `article` con una o più varianti con il tag `WKND : Activity / Hiking`

**Query di esempio**

```xml
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Query di esempio per più frammenti di contenuto di una determinata lingua {#sample-wknd-multiple-fragments-given-locale}

Questa query rappresenta un’interrogazione per ottenere:

* frammenti di contenuto di tipo `article` all’interno della lingua `fr`

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

## Struttura di esempio dei frammenti di contenuto (utilizzata con GraphQL) {#content-fragment-structure-graphql}

Le query di esempio si basano sulla seguente struttura, che utilizza:

* Uno o più [modelli per frammenti di contenuto di esempio](#sample-content-fragment-models-schemas): costituisce la base per gli schemi GraphQL

* [Frammenti di contenuto di esempio](#sample-content-fragments) basati sui modelli di cui sopra

### Modelli per frammenti di contenuto di esempio (schemi) {#sample-content-fragment-models-schemas}

Per le query di esempio, verranno utilizzati i seguenti modelli di contenuto e le relative interrelazioni (riferimenti ->):

* [Azienda](#model-company)
-> [Utente](#model-person)
-> [Riconoscimento](#model-award)

* [Città](#model-city)

#### Azienda {#model-company}

I campi di base che definiscono l’azienda sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome dell’azienda | Testo su riga singola |  |
| CEO | Riferimento frammento (singolo) | [Persona](#model-person) |
| Dipendenti | Riferimento frammento (con più campi) | [Persona](#model-person) |

#### Persona {#model-person}

I campi che definiscono un’utente, che può anche essere un dipendente:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Nome | Testo su riga singola |  |
| Nome | Testo su riga singola |  |
| Premi | Riferimento frammento (con più campi) | [Riconoscimento](#model-award) |

#### Riconoscimento {#model-award}

I campi che definiscono un riconoscimento sono:

| Nome campo | Tipo di dati | Riferimento |
|--- |--- |--- |
| Scelta rapida/ID | Testo su riga singola |  |
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

| Nome dell’azienda | CEO | Dipendenti |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nome | Nome | Premi |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Slade |  Cutter |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Croft |  Lara | Gamestar |
| Caulfield |  Max |  Gameblitz |
|  Jobs |  Steve |   |

#### Riconoscimento {#fragment-award}

| Scelta rapida/ID | Titolo |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Città {#fragment-city}

| Nome | Paese | Popolazione | Categorie |
|--- |--- |--- |--- |
| Basilea | Svizzera | 172258 | city:emea |
| Berlino | Germania | 3669491 | city:capital<br>city:emea |
| Bucarest | Romania | 1821000 |  city:capital<br>city:emea |
| San Francisco |  USA |  883306 |  city:beach<br>city:na |
| San Jose |  USA |  102635 |  city:na |
| Stoccarda |  Germania |  634830 |  city:emea |
|  Zurigo |  Svizzera |  415367 |  city:capital<br>city:emea |
