---
title: Query GraphQL persistenti
description: Scopri come rendere persistenti le query GraphQL in Adobe Experience Manager per ottimizzare le prestazioni. Le query persistenti possono essere richieste dalle applicazioni client tramite il metodo HTTP GET e la risposta può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni delle applicazioni client.
source-git-commit: 9369f7cb9c507bbd7d7761440ceef907552aeb7d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 100%

---

# Query GraphQL persistenti {#persisted-queries-caching}

Le query persistenti sono query GraphQL create e memorizzate sul server di Adobe Experience Manager (AEM) as a Cloud Service. Possono essere richiamate tramite una richiesta GET da parte delle applicazioni client. La risposta di una richiesta GET può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni dell’applicazione client richiedente. In questo sono diverse dalle query GraphQL standard, che vengono eseguite utilizzando richieste POST in cui la risposta non può essere facilmente memorizzata nella cache.

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

La [IDE GraphiQL](/help/assets/content-fragments/graphiql-ide.md) è disponibile in AEM per sviluppare, testare e mantenere le query GraphQL, prima del [trasferimento all’ambiente di produzione](#transfer-persisted-query-production). Per i casi che richiedono personalizzazione (come la [personalizzazione della cache](/help/assets/content-fragments/graphiql-ide.md#caching-persisted-queries)) puoi utilizzare l’API; vedi l’esempio curl fornito in [Persistenza di una query GraphQL](#how-to-persist-query).

## Query ed endpoint persistenti {#persisted-queries-and-endpoints}

Le query persistenti devono sempre utilizzare l’endpoint correlato alla [configurazione Sites adeguata](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint) in modo che possano utilizzare una delle due opzioni seguenti, oppure entrambe:

* Configurazione globale ed endpoint
La query ha accesso a tutti i modelli per frammenti di contenuto.
* Configurazione/i di Sites ed endpoint specifici 
La creazione di una query persistente per una configurazione di Sites specifica richiede un endpoint specifico per la configurazione di Sites corrispondente (in modo da fornire accesso ai relativi modelli per frammenti di contenuto).
Ad esempio, per creare una query persistente per la configurazione di Sites WKND, è necessario aver già creato una configurazione di Sites specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Per ulteriori dettagli, vedi [Abilitare la funzionalità Frammenti di contenuto nel browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
>
>Per la configurazione di Sites appropriata, è necessario abilitare **query GraphQL persistenti**.

Ad esempio, se vi è una particolare query denominata `my-query`, che utilizza un modello `my-model` della configurazione Sites `my-conf`:

* Puoi creare una query utilizzando l’endpoint `my-conf` specifico. La query viene salvata come segue:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puoi creare la stessa query utilizzando l’endpoint `global`, ma in questo caso la query viene salvata come segue:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Si tratta di due query diverse, salvate in percorsi diversi.
>
>Utilizzano lo stesso modello, ma tramite endpoint diversi.

## Rendere persistente una query GraphQL {#how-to-persist-query}

Si consiglia di creare le query persistenti in un ambiente di authoring AEM per poi [trasferire la query](#transfer-persisted-query-production) nell’ambiente di pubblicazione AEM di produzione, per l’utilizzo da parte delle applicazioni.

Esistono diversi metodi per le query persistenti, tra cui:

* IDE GraphiQL: vedi [Salvataggio delle query persistenti](/help/assets/content-fragments/graphiql-ide.md#saving-persisted-queries) (metodo preferito)
* curl: vedi l’esempio seguente
* Altri strumenti, tra cui [Postman](https://www.postman.com/)

L’IDE GraphiQL è il metodo **preferito** per le query persistenti. Per rendere persistente una determinata query utilizzando lo strumento per riga di comando **cURL**:

1. Prepara la query inserendola mediante il metodo PUT nel nuovo URL dell’endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Ad esempio, crea una query persistente:

   ```shell
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

1. A questo punto, verifica la risposta.

   Ad esempio, verifica se l’operazione è riuscita:

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Puoi quindi richiedere la query persistente utilizzando il metodo GET per l’URL `/graphql/execute.json/<shortPath>`.

   Ad esempio, utilizza la query persistente:

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Per aggiorna una query persistente, utilizza il metodo POST per un percorso di query già esistente.

   Ad esempio, utilizza la query persistente:

   ```shell
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

1. Crea una query normale racchiusa.

   Esempio:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crea una query normale racchiusa con il controllo della cache.

   Esempio:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crea una query persistente con parametri:

   Esempio:

   ```shell
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


## Come eseguire una query persistente {#execute-persisted-query}

Per eseguire una query persistente, un’applicazione client invia una richiesta GET utilizzando la seguente sintassi:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

dove `PERSISTENT_PATH` è un percorso abbreviato in cui viene salvata la query persistente.

1. Ad esempio `wknd` è il nome della configurazione e `plain-article-query` è il nome della query persistente. Per eseguire la query:

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Esegui una query con parametri.

   >[!NOTE]
   >
   > Le variabili e i valori della query devono essere correttamente [codificati](#encoding-query-url) durante l’esecuzione di una query persistente.

   Esempio:

   ```xml
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Per ulteriori dettagli, consulta la sezione sulle [variabili di query](#query-variables).

## Utilizzo delle variabili di query {#query-variables}

Le variabili di query possono essere utilizzate con le query persistenti. Le variabili di query aggiunte alla richiesta devono essere precedute da un punto e virgola (`;`) e devono utilizzare il nome e il valore della variabile. Se si utilizzano più variabili, queste devono essere separate da un punto e virgola.

Il pattern si presenta come segue:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Ad esempio, la seguente query contiene una variabile `activity` per filtrare un elenco in base a un valore di attività:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Questa query può essere resa persistente in un percorso `wknd/adventures-by-activity`. Per chiamare la query persistente dove `activity=Camping`, la richiesta sarà simile alla seguente:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Tieni presente che `%3B` è la codifica UTF-8 per `;` e `%3D` è la codifica per `=`. Affinché la query persistente possa essere eseguita, le variabili della query ed eventuali caratteri speciali devono essere [codificati correttamente](#encoding-query-url).

<!--
## Caching your persisted queries {#caching-persisted-queries}

Persisted queries are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application.

By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL). 

This value is set to:

* 7200 seconds is the default TTL for the Dispatcher and CDN; also known as *shared caches*
  * default: s-maxage=7200
* 60 is the default TTL for the client (for example, a browser)
  * default: maxage=60

If you want to change the TTL for your GraphLQ query, then the query must be either:

* persisted after managing the [HTTP Cache headers - from the GraphQL IDE](#http-cache-headers)
* persisted using the [API method](#cache-api). 

### Managing HTTP Cache Headers in GraphQL  {#http-cache-headers-graphql}

The GraphiQL IDE - see [Saving Persisted Queries](/help/assets/content-fragments/graphiql-ide.md#managing-cache)

### Managing Cache from the API {#cache-api}

This involves posting the query to AEM using CURL in your command line interface. 

For an example:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

The `cache-control` can be set at the creation time (PUT) or later on (for example, via a POST request for instance). The cache-control is optional when creating the persisted query, as AEM can provide the default value. See [How to persist a GraphQL query](#how-to-persist-query), for an example of persisting a query using curl.
-->

## Codifica dell’URL della query per l’utilizzo da parte di un’app {#encoding-query-url}

Per poter essere utilizzati da un’applicazione, eventuali caratteri speciali utilizzati per creare variabili di query (come punto e virgola (`;`), segno di uguale (`=`), barra `/`) deve essere convertito nella codifica UTF-8 corrispondente.

Esempio:

```xml
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

L’URL può essere suddiviso nelle seguenti parti:

| Parte URL | Descrizione |
|----------| -------------|
| `/graphql/execute.json` | Endpoint di query persistente |
| `/wknd/adventure-by-path` | Percorso query persistente |
| `%3B` | Codice per `;` |
| `adventurePath` | Variabile query |
| `%3D` | Codice per `=` |
| `%2F` | Codice per `/` |
| `%2Fcontent%2Fdam...` | Percorso codificato del frammento di contenuto |

Come testo normale, l’URI della richiesta si presenta così:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Per utilizzare una query persistente in un’app client, è necessario utilizzare l’SDK client AEM headless per [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) oppure [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). L’SDK client headless codificherà automaticamente tutte le variabili di query in modo appropriato nella richiesta.

## Trasferimento di una query persistente all’ambiente di produzione  {#transfer-persisted-query-production}

Le query persistenti devono sempre essere create su un servizio AEM Author e quindi pubblicate (replicate) in un servizio AEM Publish. Spesso, le query persistenti vengono create e testate in ambienti inferiori, come ambienti locali o di sviluppo. È quindi necessario promuovere le query persistenti in ambienti di livello superiore, rendendole infine disponibili in un ambiente AEM Publish di produzione affinché possano essere utilizzate da parte delle applicazioni client.

### Query persistenti nei pacchetti

È possibile integrare le query persistenti in [pacchetti AEM](/help/sites-administering/package-manager.md). I pacchetti AEM possono quindi essere scaricati e installati in ambienti diversi. I pacchetti AEM possono essere replicati anche da un ambiente AEM Author ad ambienti AEM Publish.

Per creare un pacchetto:

1. Passa a **Strumenti** > **Implementazione** > **Pacchetti**.
1. Per creare un nuovo pacchetto, tocca **Crea pacchetto**. Viene visualizzata una finestra di dialogo per la definizione del pacchetto.
1. Nella finestra di dialogo Definizione pacchetto, nella sezione **Generale** inserisci un **Nome**, ad esempio “wknd-persistent-queries”.
1. Immetti un numero di versione, ad esempio a “1.0”.
1. Nella sezione **Filtri**, aggiungi un nuovo **Filtro**. Utilizza Trova percorso per selezionare la cartella `persistentQueries` sotto la configurazione. Ad esempio, per la configurazione `wknd` il percorso completo sarà `/conf/wknd/settings/graphql/persistentQueries`.
1. Tocca **Salva** per salvare la definizione del nuovo pacchetto e chiudere la finestra di dialogo.
1. Tocca **Genera** nella definizione del pacchetto appena creata.

Dopo aver generato il pacchetto puoi:

* **Scaricare** il pacchetto e ricaricalo in un altro ambiente.
* **Replicare** il pacchetto toccando **Altro** > **Replica**. Il pacchetto verrà replicato nell’ambiente AEM Publish collegato.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
