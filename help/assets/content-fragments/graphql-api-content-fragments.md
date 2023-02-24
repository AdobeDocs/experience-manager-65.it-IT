---
title: API GraphQL AEM per l’utilizzo con Frammenti di contenuto
description: Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) con l’API GraphQL AEM per la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 42ef4694a3301ae1cd34766ce4c19f4b0e2f2c38
workflow-type: tm+mt
source-wordcount: '3695'
ht-degree: 87%

---

# API GraphQL AEM per l’utilizzo con Frammenti di contenuto {#graphql-api-for-use-with-content-fragments}

Scopri come utilizzare Frammenti di contenuto in Adobe Experience Manager (AEM) con l’API GraphQL AEM per la distribuzione di contenuti headless.

L’API GraphQL AEM utilizzata con i Frammenti di contenuto è pesantemente basata sull’API GraphQL standard open source.

L’utilizzo dell’API GraphQL in AEM consente la consegna efficiente di Frammenti di contenuto ai client JavaScript in implementazioni CMS headless:

* evita richieste API iterative come con REST,
* garantisce che la consegna sia limitata ai requisiti specifici,
* consente la consegna in massa di ciò che è esattamente necessario per il rendering come risposta a una singola query API.

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM):
>
>* [AEM Commerce sfrutta i dati da una piattaforma Commerce tramite GraphQL](/help/commerce/cif/integrating/magento.md).
>* I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni.


## API GraphQL {#graphql-api}

GraphQL è:

* “*...un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti. GraphQL fornisce una descrizione completa e comprensibile dei dati nell’API, offre ai clienti la possibilità di chiedere esattamente ciò di cui hanno bisogno e niente di più, semplifica l’evoluzione delle API nel tempo e abilita potenti strumenti per gli sviluppatori.*”.

   Vedi [GraphQL.org](https://graphql.org)

* “*...una specifica aperta per un livello API flessibile. Posiziona GraphQL sui backend esistenti per costruire prodotti più rapidamente che mai....*”.

   Vedi [Esplorare GraphQL](https://www.graphql.com).

* *“..un linguaggio e una specifica di query di dati sviluppati internamente da Facebook nel 2012 prima di essere resi open source nel 2015. Offre un’alternativa alle architetture basate su REST allo scopo di aumentare la produttività degli sviluppatori e ridurre al minimo le quantità di dati trasferiti. GraphQL viene utilizzato in produzione da centinaia di organizzazioni di tutte le dimensioni...”*

   Vedi [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Per ulteriori informazioni sull’API GraphQL, consulta le sezioni seguenti (tra molte altre risorse):

* In [graphql.org](https://graphql.org):

   * [Introduzione a GraphQL](https://graphql.org/learn)

   * [Specifiche GraphQL](https://spec.graphql.org/)

* In [graphql.com](https://graphql.com):

   * [Guide](https://www.graphql.com/guides/)

   * [Esercitazioni](https://www.graphql.com/tutorials/)

   * [Casi di studio](https://www.graphql.com/case-studies/)

L’implementazione di GraphQL per AEM si basa sulla libreria Java GraphQL standard. Consulta:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [Java GraphQL su GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL utilizza quanto segue:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemi e tipi](https://graphql.org/learn/schema/)**:

   * Gli schemi vengono generati da AEM in base ai modelli di Frammenti di contenuto.
   * Utilizzando i tuoi schemi, GraphQL presenta i tipi e le operazioni consentiti per l’implementazione GraphQL per AEM.

* **[Campi](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * Il percorso in AEM che risponde alle query GraphQL e fornisce accesso agli schemi GraphQL.

   * Consulta [Abilitazione dell’endpoint GraphQL](#enabling-graphql-endpoint) per ulteriori dettagli.

Consulta[(GraphQL.org) Introduzione a GraphQL](https://graphql.org/learn/) per informazioni complete, che comprendono le [Best practice](https://graphql.org/learn/best-practices/).

### Tipi di query GraphQL {#graphql-query-types}

Con GraphQL è possibile eseguire query per ottenere:

* Un **ingresso singolo**

* Un **[elenco delle voci](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM fornisce funzionalità per convertire le query (entrambi i tipi) in [Query persistenti](/help/assets/content-fragments/persisted-queries.md), che può essere memorizzato nella cache da Dispatcher e CDN.

### Tecniche consigliate per le query GraphQL (Dispatcher e CDN) {#graphql-query-best-practices}

La [Query persistenti](/help/assets/content-fragments/persisted-queries.md) sono il metodo consigliato da utilizzare nelle istanze di pubblicazione come:

* vengono memorizzate nella cache;
* sono gestite centralmente da AEM

>[!NOTE]
>
>Di solito non esiste un dispatcher/CDN sull’autore, quindi non c’è alcun guadagno nell’utilizzo di query persistenti lì; oltre a testarli.

Le query GraphQL che utilizzano richieste POST non sono consigliate in quanto non sono memorizzate nella cache, pertanto in un’istanza predefinita Dispatcher è configurato per bloccare tali query.

Anche se GraphQL supporta anche le richieste GET, possono raggiungere i limiti (ad esempio la lunghezza dell’URL) che possono essere evitati utilizzando le query persistenti.

>[!NOTE]
>
>In futuro, la capacità di eseguire query dirette potrebbe diventare obsoleta.

## GraphQL per AEM endpoint {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere allo schema GraphQL;
* inviare le query GraphQL;
* ricevere le risposte (alle query GraphQL).

Esistono due tipi di endpoint in AEM:

* Globale
   * Disponibile per tutti i siti.
   * Questo endpoint può utilizzare tutti i modelli per frammenti di contenuto di tutte le configurazioni di Sites (definite nella sezione [Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Se esistono modelli per frammenti di contenuto che devono essere condivisi tra le configurazioni di Sites, questi devono essere creati nelle configurazioni globali di Sites.
* Configurazioni di Sites:
   * Corrisponde a una configurazione Sites, come definita nella sezione [Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Sono specifiche per un determinato sito o progetto.
   * Un endpoint specifico per la configurazione di Sites utilizzerà i modelli di frammento di contenuto di quella specifica configurazione di Sites insieme a quelli della configurazione globale di Sites.

>[!CAUTION]
>
>L’Editor frammento di contenuto può consentire a un frammento di contenuto di una configurazione Sites di fare riferimento a un frammento di contenuto di un’altra configurazione Sites (tramite criteri).
>
>In questo caso non tutti i contenuti saranno recuperabili utilizzando un endpoint specifico per la configurazione Sites.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile inserire modelli per frammenti di contenuto condivisi nella configurazione globale di Sites.

Il percorso dell’archivio di GraphQL per l’endpoint globale di AEM è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare un endpoint per GraphQL per AEM è necessario:

* [Abilitare l’endpoint GraphQL](#enabling-graphql-endpoint)
* [Pubblicare l’endpoint GraphQL](#publishing-graphql-endpoint)

### Abilitazione dell’endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata. Vedi la sezione [Frammenti di contenuto - Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se l’[utilizzo di modelli per frammenti di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l’opzione **Crea** non sarà disponibile.

Per abilitare l’endpoint corrispondente:

1. Passa a **Strumenti**, **Risorse**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Si aprirà la finestra di dialogo **Crea nuovo endpoint GraphQL**. Qui potrai definire:
   * **Nome**: nome dell’endpoint; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: dal menu a discesa, seleziona il sito o il progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato la seguente avvertenza:
   >
   >* *Se non vengono gestiti correttamente, gli endpoint GraphQL possono causare problemi di prestazioni e sicurezza dei dati. Dopo aver creato un endpoint, assicurati di impostare le autorizzazioni appropriate.*


1. Per confermare, fai clic su **Crea**.
1. La finestra di dialogo **Passaggi successivi** fornisce un collegamento diretto alla console Sicurezza per verificare che l’endpoint appena creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare sull’endpoint eventuali ACL appropriate al tuo caso d’uso.

### Pubblicazione dell’endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e scegli **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Devi configurare sull’endpoint le ACL appropriate al tuo caso d’uso.

## Interfaccia GraphiQL {#graphiql-interface}

Attuazione dello standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) L’interfaccia è disponibile per l’utilizzo con AEM GraphQL.

>[!NOTE]
>
>GraphiQL è incluso in tutti gli ambienti di AEM (ma sarà accessibile/visibile solo quando configuri gli endpoint).
>
>Nelle versioni precedenti, era necessario un pacchetto per installare l’IDE GraphiQL. Se installato, ora è possibile rimuoverlo.

Questa interfaccia ti consente di inserire e testare direttamente le query.

Ad esempio:

* `http://localhost:4502/content/graphiql.html`

Offre funzioni quali evidenziazione della sintassi, completamento automatico, suggerimenti automatici, nonché una cronologia e una documentazione online:

![Interfaccia di GraphiQL](assets/cfm-graphiql-interface.png "Interfaccia di GraphiQL")

>[!NOTE]
>
>Per maggiori dettagli vedi [Utilizzo dell&#39;IDE GraphiQL](/help/assets/content-fragments/graphiql-ide.md).

## Casi di utilizzo per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi di utilizzo possono dipendere dal tipo di ambiente AEM:

* ambiente di pubblicazione; utilizzato per:
   * effettuare query sui dati per l’applicazione JS (caso di utilizzo standard)

* ambiente di authoring; utilizzato per:
   * effettuare query sui dati a “scopo di gestione dei contenuti”:
      * GraphQL in AEM è attualmente un’API di sola lettura.
      * L’API REST può essere utilizzata per le operazioni CR(u)D.

## Autorizzazioni {#permission}

Le autorizzazioni sono quelle necessarie per accedere ad Assets.

Le query GraphQL vengono eseguite con l&#39;autorizzazione dell&#39;utente AEM della richiesta sottostante. Se l’utente non dispone dell’accesso in lettura ad alcuni frammenti (memorizzati come risorse), non farà parte del set di risultati.

Inoltre, l’utente deve avere accesso a un endpoint GraphQL per poter eseguire query GraphQL.

## Generazione schema {#schema-generation}

GraphQL è un’API fortemente tipizzata, il che significa che i dati devono essere chiaramente strutturati e organizzati per tipo.

La specifica GraphQL fornisce una serie di linee guida su come creare una solida API per l’interrogazione dei dati su una determinata istanza. A questo scopo, un client deve recuperare lo [Schema](#schema-generation), che contiene tutti i tipi necessari per una query.

Per quanto riguarda i Frammenti di contenuto, gli schemi GraphQL (struttura e tipi) sono basati su [modelli di Frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) **abilitati** e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di Frammenti di contenuto che sono stati **abilitati**) sono leggibili attraverso l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, che in questo modo potrebbero trapelare; ad esempio, informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello di Frammento di contenuto denominato `Article`, AEM genera l’oggetto `article` di un tipo `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Modello di Frammento di contenuto:

   ![Modello di Frammento di contenuto da utilizzare con GraphQL](assets/cfm-graphqlapi-01.png "Modello di Frammento di contenuto da utilizzare con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su modello di Frammento di contenuto](assets/cfm-graphqlapi-02.png "Schema GraphQL basato su modello di Frammento di contenuto")

   Questo mostra che il tipo `ArticleModel` generato contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato Frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Tali [campi di supporto](#helper-fields) sono contrassegnati con un `_` per distinguere tra ciò che è stato definito dall’utente e ciò che è stato generato automaticamente.

1. Un Frammento di contenuto basato sul modello di articolo creato da un utente può essere interrogato tramite GraphQL. Per esempi, consulta la sezione [Query di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (basata su una [struttura di Frammento di contenuto di esempio da utilizzare con GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di Frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si rivede un modello di Frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di Frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e garantisce stabilità.

Ad esempio, se:

1. installi un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. vengono generati dei tipi GraphQL per `Model-1` e `Model-2`.

1. Poi modifica `Content-Fragment-Model-2`:

   1. verrà aggiornato solo il tipo GraphQL `Model-2`.

   1. Mentre `Model-1` rimarrà lo stesso.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di Frammento di contenuto tramite l’API REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, dove il client gestisce il fatto che lo schema viene chiamato con l’estensione `GQLschema`. Ad esempio, l’esecuzione di una semplice richiesta `GET` di `/content/cq:graphql/global/endpoint.GQLschema` si tradurrà nell’output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

### Generazione schema: modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che venga pubblicato un modello di Frammento di contenuto principale, ma non il modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera uno schema *incompleto* per il modello di Frammento di contenuto principale. Ciò significa che il Riferimento al frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## Campi {#fields}

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati dall’utente.

   Per creare campi in base alla modalità di configurazione del modello di frammento di contenuto, viene utilizzata una selezione di [Tipi di campo](#field-types). I nomi dei campi vengono ricavati dal campo **Nome proprietà** del **Tipo di dato**.

   * C&#39;è da prendere in considerazione anche la proprietà **Rendering come**, perché gli utenti possono configurare determinati tipi di dati; ad esempio, come testo a riga singola o come campo multiplo.

* GraphQL per AEM genera anche una serie di [campi di supporto](#helper-fields).

   Questi vengono utilizzati per identificare un Frammento di contenuto o per ottenere ulteriori informazioni su di esso.

### Tipi di campi {#field-types}

GraphQL per AEM supporta un elenco di tipi. Vengono rappresentati tutti i tipi di dati dei modelli di Frammento di contenuto supportati e i corrispondenti tipi GraphQL:

| Modello di Frammento di contenuto: tipo di dati | Tipo GraphQL | Descrizione |
|--- |--- |--- |
| Testo su riga singola | Stringa, [Stringa] |  Utilizzato per stringhe semplici come nomi di autore, nomi di posizione, ecc. |
| Testo su più righe | Stringa |  Utilizzato per l’output di testo, ad esempio il corpo di un articolo |
| Numero |  Mobile, [Mobile] | Utilizzato per visualizzare il numero a virgola mobile e i numeri regolari |
| Booleano |  Booleano |  Utilizzato per visualizzare le caselle di controllo → semplici istruzioni true/false |
| Data e ora | Calendario |  Utilizzato per visualizzare la data e l’ora in formato ISO 8086. A seconda del tipo selezionato, sono disponibili tre versioni da utilizzare in AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumerazione |  Stringa |  Utilizzato per visualizzare un’opzione da un elenco di opzioni definito durante la creazione del modello |
|  Tag |  [Stringa] |  Utilizzato per visualizzare un elenco di stringhe che rappresentano tag utilizzati in AEM |
| Riferimento contenuto |  Stringa |  Utilizzato per visualizzare il percorso per un’altra risorsa in AEM |
| Riferimento frammento |  *Un tipo di modello* |  Utilizzato per fare riferimento ad altri frammenti di contenuto di un determinato tipo di modello, definito al momento della creazione del modello |

### Campi di supporto {#helper-fields}

Oltre ai tipi di dati per i campi generati dall’utente, GraphQL for AEM genera anche una serie di campi *di supporto* per consentire l’identificazione di un frammento di contenuto o per fornire informazioni aggiuntive su un frammento di contenuto.

#### Percorso {#path}

In GraphQL, il campo Percorso viene utilizzato come identificatore. Rappresenta il percorso della risorsa Frammenti di contenuto all’interno dell’archivio AEM. Questo è l’identificatore di un frammento di contenuto in quanto:

* è univoco all’interno di AEM,
* può essere facilmente recuperato.

Il seguente codice visualizza i percorsi di tutti i frammenti di contenuto creati in base al modello per frammenti di contenuto `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Inoltre, per recuperare un singolo frammento di contenuto di un tipo specifico, è necessario determinarne prima il percorso. Esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Vedi [Query di esempio: un singolo frammento di città specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadati {#metadata}

Tramite GraphQL, AEM espone inoltre i metadati di un frammento di contenuto. I metadati sono informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso della miniatura, la descrizione di un frammento di contenuto, la data di creazione, e così via.

Poiché i metadati vengono generati tramite l’Editor schemi e, pertanto, non dispongono di una struttura specifica, il tipo di `TypedMetaData` GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate per i seguenti tipi scalari:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Ogni tipo scalare rappresenta una coppia nome-valore singola o un array di coppie nome-valore, in cui il valore di tale coppia è del tipo all&#39;interno del quale è stato raggruppato.

Ad esempio, se vuoi recuperare il titolo di un frammento di contenuto, si tratta di una proprietà stringa, pertanto è necessario eseguire una query per tutti i metadati stringa:

Per eseguire una query per i metadati:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Puoi visualizzare tutti i tipi di metadati GraphQL se visualizzi lo schema GraphQL generato. Tutti i tipi di modello hanno lo stesso `TypedMetaData`.

>[!NOTE]
>
>**Differenza tra metadati normali e quelli di array**
>Nota: `StringMetadata` e `StringArrayMetadata` si riferiscono a ciò che è memorizzato nell’archivio, non alla modalità di recupero.
>
>Ad esempio, effettuando una chiamata del campo `stringMetadata`, può essere restituito un array di tutti i metadati memorizzati nell’archivio come una `String`; se si effettua una chiamata dell’`stringArrayMetadata` può essere restituito un array di tutti i metadati memorizzati nell’archivio come `String[]`.

Vedi [Query di esempio per metadati: elenca i metadati per riconoscimenti con titolo GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Varianti {#variations}

Il campo `_variations` è stato implementato per semplificare l’esecuzione delle query sulle varianti di un frammento di contenuto. Esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Vedi [Query di esempio: tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

>[!NOTE]
>
>Se per un frammento di contenuto non esiste la variante determinata, la variante principale verrà restituita come impostazione predefinita (fallback).

<!--
## Security Considerations {#security-considerations}
-->

## Variabili GraphQL {#graphql-variables}

GraphQL consente di inserire variabili nella query. Per ulteriori informazioni, consulta la [documentazione di GraphQL per variabili](https://graphql.org/learn/queries/#variables).

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Article` che hanno una variante specifica, puoi specificare la variabile `variation` in GraphiQL.

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Direttive GraphQL {#graphql-directives}

In GraphQL è possibile modificare le query basate su variabili, denominate Direttive GraphQL.

Ad esempio, puoi includere il campo `adventurePrice` in una query per tutti i `AdventureModels` basati su una variabile `includePrice`.

![Direttive GraphQL](assets/cfm-graphqlapi-04.png "Direttive GraphQL")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtro {#filtering}

Puoi inoltre utilizzare il filtro nelle query GraphQL per restituire dati specifici.

Il filtro utilizza una sintassi basata su operatori ed espressioni di tipo logico.

Ad esempio, la query (di base) seguente filtra tutti gli utenti denominati `Jobs` o `Smith`:

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

Per altri esempi, consulta:

* informazioni dettagliate di [GraphQL per estensioni AEM](#graphql-extensions)

* [Query di esempio che utilizzano il contenuto e la struttura di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * e il [contenuto e la struttura di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) predisposta per l’utilizzo in query di esempio

* [Query di esempio basate sul progetto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL per AEM: riepilogo delle estensioni {#graphql-extensions}

Le operazioni di base delle query con GraphQL per AEM sono conformi alle specifiche standard di GraphQL. Per le query GraphQL con AEM sono disponibili alcune estensioni:

* Se necessiti di un singolo risultato:
   * utilizza il nome del modello; ad es. città

* Se prevedi un elenco di risultati:
   * aggiungi `List` al nome del modello; ad esempio, `cityList`
   * Vedi [Query di esempio: informazioni su tutte le città](#sample-all-information-all-cities)

* Il filtro `includeVariations` è incluso nel `List` tipo di query.  Per recuperare le varianti dei frammenti di contenuto nei risultati della query, quindi la `includeVariations` il filtro deve essere impostato su `true`.

   >[!CAUTION]
   >Il filtro `includeVariations` non può essere utilizzato insieme al campo generato dal sistema `_variation`.

* Se vuoi utilizzare un operatore OR logico:
   * utilizza ` _logOp: OR`
   * Vedi [Query di esempio: tutti gli utenti denominati “Jobs” o “Smith”](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* Esiste anche l’operatore AND logico, ma è (spesso) implicito

* Puoi eseguire query sui nomi dei campi corrispondenti ai campi all’interno del modello per frammenti di contenuto
   * Vedi [Query di esempio: informazioni complete sull’amministratore delegato e sui dipendenti di un’azienda](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono disponibili alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale`: per visualizzare la lingua; basato su Language Manager
         * Vedi [Query di esempio per più frammenti di contenuto di una specifica impostazione locale](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata`: per visualizzare i metadati del frammento
         * Vedi [Query di esempio per metadati: elenca i metadati per riconoscimenti con titolo GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
      * `_model`: consente di eseguire query per un modello per frammenti di contenuto (percorso e titolo)
         * Vedi [Query di esempio per un modello per frammenti di contenuto da un modello](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)
      * `_path`: il percorso del frammento di contenuto all’interno dell’archivio
         * Vedi [Query di esempio: un singolo frammento di città specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
      * `_reference`: per visualizzare riferimenti; inclusi riferimenti in linea nell’Editor testo RTF
         * Vedi [Query di esempio per più frammenti di contenuto con riferimenti di prelettura](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation`: per visualizzare varianti specifiche all’interno del frammento di contenuto

         >[!NOTE]
         >
         >Se per un frammento di contenuto non esiste la variante determinata, la variante principale verrà restituita come impostazione predefinita (fallback).

         >[!CAUTION]
         >Campo generato dal sistema `_variation` non può essere utilizzato insieme al filtro `includeVariations`.

         * Vedi [Query di esempio: tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
      * `_tags` : rivelare gli ID di frammenti di contenuto o varianti che contengono tag; è un array di `cq:tags` identificatori.

         * Vedi [Query di esempio - Nomi di tutte le città con tag come interruzioni di città](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * Vedi [Query di esempio per le varianti di frammento di contenuto di un modello specifico a cui è associato un tag specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

         >[!NOTE]
         >
         >È inoltre possibile eseguire una query sui tag elencando i metadati di un frammento di contenuto.
   * E operazioni:

      * `_operator`: applica operatori specifici; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Vedi [Query di esempio: tutti gli utenti non denominati “Jobs”](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * Vedi [Query di esempio: tutte le avventure in cui `_path` inizia con un prefisso specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`: applica condizioni specifiche; ad esempio, `AT_LEAST_ONCE`
         * Vedi [Query di esempio: applica filtro su un array con un elemento che deve verificarsi almeno una volta](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase`: per ignorare il caso durante la query
         * Vedi [Query di esempio: tutte le città che contengono SAN nel nome, indipendentemente da maiuscole/minuscole](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)











* I tipi di unione GraphQL sono supportati:

   * utilizza `... on`
      * Vedi [Query di esempio per un frammento di contenuto di un modello specifico con un riferimento ai contenuti](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* Fallback durante la query dei frammenti nidificati:

   * Se la variante richiesta non esiste in un frammento nidificato, la variabile **Master** viene restituita la variante .

<!--
## Persisted Queries (Caching) {#persisted-queries-caching}

After preparing a query with a POST request, it can be executed with a GET request that can be cached by HTTP caches or a CDN.

This is required as POST queries are usually not cached, and if using GET with the query as a parameter there is a significant risk of the parameter becoming too large for HTTP services and intermediates.

Persisted queries must always use the endpoint related to the [appropriate Sites configuration](#graphql-aem-endpoint); so they can use either, or both:

* The Global configuration and endpoint
  The query has access to all Content Fragment Models.
* Specific Sites configuration(s) and endpoint(s)
  Creating a persisted query for a specific Sites configuration requires a corresponding Sites-configuration-specific endpoint (to provide access to the related Content Fragment Models). 
  For example, to create a persisted query specifically for the WKND Sites configuration, a corresponding WKND-specific Sites configuration, and a WKND-specific endpoint must be created in advance.

>[!NOTE]
>
>See [Enable Content Fragment Functionality in Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) for more details.
>
>The **GraphQL Persistence Queries** need to be enabled, for the appropriate Sites configuration. 

For example, if there is a particular query called `my-query`, which uses a model `my-model` from the Sites configuration `my-conf`:

* You can create a query using the `my-conf` specific endpoint, and then the query will be saved as following: 
`/conf/my-conf/settings/graphql/persistentQueries/my-query`
* You can create the same query using `global` endpoint, but then the query will be saved as following:
`/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>These are two different queries - saved under different paths. 
>
>They just happen to use the same model - but via different endpoints.


Here are the steps required to persist a given query:

1. Prepare the query by PUTing it to the new endpoint URL `/graphql/persist.json/<config>/<persisted-label>`.

   For example, create a persisted query:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. At this point, check the response.

   For example, check for success:

     ```xml
     {
       "action": "create",
       "configurationName": "wknd",
       "name": "plain-article-query",
       "shortPath": "/wknd/plain-article-query",
       "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
     }
     ```

1. You can then replay the persisted query by GETing the URL `/graphql/execute.json/<shortPath>`.

   For example, use the persisted query:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Update a persisted query by POSTing to an already existing query path.

   For example, use the persisted query:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Create a wrapped plain query.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Create a wrapped plain query with cache control.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Create a persisted query with parameters:

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Executing a query with parameters.

   For example:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"

   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. To execute the query on publish, the related persist tree need to replicated

   * Using a POST for replication:

     ```xml
     $curl -X POST   http://localhost:4502/bin/replicate.json \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
       -F cmd=activate
     ```

   * Using a package:
     1. Create a new package definition.
     1. Include the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).
     1. Build the package.
     1. Replicate the package.

   * Using replication/distribution tool.
     1. Go to the Distribution tool.
     1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

   * Using a workflow (via workflow launcher configuration):
     1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).

1. Once the query configuration is on publish, the same principles apply, just using the publish endpoint.

   >[!NOTE]
   >
   >For anonymous access the system assumes that the ACL allows "everyone" to have access to the query configuration.
   >
   >If that is not the case it will not be able to execute.

   >[!NOTE]
   >
   >Any semicolons (";") in the URLs need to be encoded.
   >
   >For example, as in the request to Execute a persisted query:
   >
   >```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Querying the GraphQL endpoint from an External Website {#query-graphql-endpoint-from-external-website}

To access the GraphQL endpoint from an external website you need to configure the:

* [CORS Filter](#cors-filter)
* [Referrer Filter](#referrer-filter)
-->

### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Per una panoramica dettagliata della politica di condivisione delle risorse CORS in AEM vedi [Comprendere la condivisione CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=it#understand-cross-origin-resource-sharing-(cors)).

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS nell’archivio Git del cliente. Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati. 

Questa configurazione deve specificare un&#39;origine sito Web attendibile `alloworigin` o `alloworiginregexp` per i quali deve essere concesso l&#39;accesso.

Ad esempio, per consentire l’accesso all’endpoint GraphQL  e all’endpoint con query persistenti per `https://my.domain` puoi utilizzare:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se hai configurato un percorso personalizzato per l’endpoint, puoi utilizzarlo in `allowedpaths`.

### Filtro referrer {#referrer-filter}

Oltre alla configurazione CORS, è necessario configurare un filtro Referrer per consentire l’accesso da host di terze parti.

A questo scopo, aggiungi un file di configurazione OSGi Referrer Filter appropriato che:

* specifica un nome host fidato del sito web; `allow.hosts` oppure `allow.hosts.regexp`,
* concede l’accesso per questo nome host.

Ad esempio, per concedere l’accesso alle richieste con il Referrer `my.domain` puoi:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Spetta al cliente:
>
>* concedere l’accesso solo ai domini attendibili;
>* assicurarsi che non siano esposte informazioni sensibili;
>* non utilizzare una sintassi con carattere jolly [*]; questa infatti comporterebbe la disattivazione dell’accesso autenticato all’endpoint GraphQL, rendendolo accessibile a chiunque.


>[!CAUTION]
>
>Tutti gli [schemi](#schema-generation) GraphQL (derivati dai modelli per frammenti di contenuto che sono stati **abilitati**) sono leggibili attraverso l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, che in questo modo potrebbero trapelare; ad esempio, informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

## Autenticazione {#authentication}

Vedi [Autenticazione per query GraphQL AEM remote su frammenti di contenuto](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Domande frequenti {#faqs}

Domande poste:

1. **D**: “*quali sono le differenze tra l’API di GraphQL per AEM e l’API di Query Builder?*”

   * **R**: 
“*l’API di GraphQL per AEM offre il controllo totale dell’output JSON ed è uno standard di settore per l’esecuzione di query sui contenuti.
In futuro, AEM prevede di investire nell’API di GraphQL per AEM.*”

## Tutorial: guida introduttiva ad AEM headless e GraphQL {#tutorial}

Cerchi un pratico tutorial? Dai un&#39;occhiata al tutorial [Guida introduttiva di headless AEM e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) che illustra come creare ed esporre contenuti, utilizzati da un’app esterna, mediante le API GraphQL di AEM in uno scenario CMS headless.
