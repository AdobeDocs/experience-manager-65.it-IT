---
title: Come aggiornare il contenuto utilizzando le API di AEM Assets.
description: In questa parte del Percorso per sviluppatori Headless di AEM, scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto.
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 87%

---

# Come aggiornare il contenuto utilizzando le API di AEM Assets. {#update-your-content}

In questa parte del [Percorso per sviluppatori headless di AEM,](overview.md) scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso headless di AEM, [Come accedere ai contenuti utilizzando API di distribuzione di AEM](access-your-content.md) hai imparato ad accedere ai contenuti headless in AEM utilizzando l’API GraphQL AEM e ora dovresti:

* Conoscere GraphQL ad alto livello.
* Sapere come funziona l’API GraphQL di AEM.
* Comprendere alcune query pratiche di esempio.

Questo articolo si basa su questi elementi fondamentali per comprendere come aggiornare il contenuto headless esistente in AEM utilizzando l’API REST.

## Obiettivo {#objective}

* **Pubblico**: avanzato
* **Obiettivo**: scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto:
   * introduzione all’API HTTP di AEM Assets.
   * Introduzione e discussione sul supporto per i frammenti di contenuto nell’API.
   * Illustrazione dei dettagli dell’API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Perché è necessaria l’API HTTP delle risorse per i frammenti di contenuto {#why-http-api}

Nella fase precedente del Percorso Headless, hai imparato a usare l’API GraphQL di AEM per recuperare il contenuto utilizzando le query.

Allora perché è necessaria un&#39;altra API?

L’API HTTP di Assets consente di: **Letto** contenuti, ma consente anche di: **Crea**, **Aggiorna** e **Elimina** content: azioni che non sono possibili con l’API di GraphQL.

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione di Adobe Experience Manager recente.

## API HTTP di Assets {#assets-http-api}

L’API HTTP di Assets include:

* API REST di Assets
* incluso il supporto per i frammenti di contenuto

L’implementazione corrente dell’API HTTP di Assets si basa sullo stile architettonico **REST** e consente di accedere ai contenuti (memorizzati in AEM) utilizzando operazioni **CRUD** (Create (Crea), Read (Leggi), Update (Aggiorna) e Delete (Elimina)).

Con queste operazioni l’API consente di utilizzare Adobe Experience Manager come CMS (Content Management System) headless fornendo Content Services a un’applicazione front-end JavaScript. O qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON. Ad esempio, le applicazioni a pagina singola (SPA), basate su framework o personalizzate, richiedono il contenuto fornito tramite un’API, spesso in formato JSON.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## API HTTP di Assets e frammenti di contenuto {#assets-http-api-content-fragments}

I frammenti di contenuto vengono utilizzati per la distribuzione headless e un frammento di contenuto è un tipo speciale di risorsa. Vengono utilizzati per accedere a dati strutturati, tra cui testi, numeri, date.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Utilizzo dell’API REST di Assets {#using-aem-assets-rest-api}

### Accesso {#access}

L’API REST di Assets utilizza l’`/api/assets` endpoint e richiede il percorso della risorsa per accedervi (senza l’iniziale `/content/dam`).

* Ciò significa che per accedere alla risorsa in:
   * `/content/dam/path/to/asset`
* è necessario richiedere:
   * `/api/assets/path/to/asset`

Ad esempio, per accedere a `/content/dam/wknd/en/adventures/cycling-tuscany`, richiedi `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>l’accesso a:
>
>* `/api/assets` **non è** necessario l’uso del selettore `.model`.
>* `/content/path/to/page` **richiede** l’uso del selettore `.model`.

### Operazione {#operation}

Il metodo HTTP determina l’operazione da eseguire:

* **GET**: per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST**: per creare nuove risorse o cartelle
* **PUT**: per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE**: per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debbano essere create da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nella documentazione di riferimento API.

L’utilizzo può variare a seconda che utilizzi un ambiente di authoring o pubblicazione di AEM, insieme al tuo caso d’uso specifico.

* Si consiglia vivamente di associare la creazione a un’istanza di authoring (e al momento non esiste alcun modo per replicare un frammento da pubblicare utilizzando questa API).
* La distribuzione è possibile da entrambi, in quanto AEM fornisce il contenuto richiesto solo in formato JSON.

   * L’archiviazione e la consegna da un’istanza di authoring AEM dovrebbero essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.

   * Per la distribuzione web live, si consiglia un’istanza di pubblicazione AEM.

>[!CAUTION]
>
>La configurazione del dispatcher su istanze AEM potrebbe bloccare l’accesso a `/api`.

>[!NOTE]
>
>Per ulteriori dettagli, consulta la Guida di riferimento API. In particolare, [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### Lettura/consegna {#read-delivery}

L’utilizzo avviene tramite:

`GET /{cfParentPath}/{cfName}.json`

Esempio:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

La risposta viene serializzata JSON con il contenuto strutturato come nel frammento di contenuto. I riferimenti vengono consegnati come URL di riferimento.

Sono possibili due tipi di operazioni di lettura:

* Quando si legge un frammento di contenuto specifico in base al percorso, viene restituita la rappresentazione JSON del frammento di contenuto.
* Lettura di una cartella di frammenti di contenuto in base al percorso: restituisce le rappresentazioni JSON di tutti i frammenti di contenuto all’interno della cartella.

### Creare {#create}

L’utilizzo avviene tramite:

`POST /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON del frammento di contenuto da creare, incluso qualsiasi contenuto iniziale da impostare sugli elementi del frammento di contenuto. È obbligatorio impostare la proprietà `cq:model` e deve puntare a un modello di frammento di contenuto valido. In caso contrario si verifica un errore. È inoltre necessario aggiungere un’intestazione `Content-Type` che è impostata su `application/json`.

### Aggiornare {#update}

L’utilizzo avviene tramite:

`PUT /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON di ciò che deve essere aggiornato per il frammento di contenuto specificato.

Può trattarsi semplicemente del titolo o della descrizione di un frammento di contenuto, di un singolo elemento o di tutti i valori e/o metadati degli elementi.

### Eliminare {#delete}

L’utilizzo avviene tramite:

`DELETE /{cfParentPath}/{cfName}`

Per ulteriori dettagli sull’utilizzo dell’API REST di AEM Assets, puoi fare riferimento a:

* API HTTP di Adobe Experience Manager Assets (risorse aggiuntive)
* Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets (risorse aggiuntive)

## Passaggio successivo {#whats-next}

Ora che hai completato questa parte del percorso per sviluppatori headless di AEM, dovresti:

* Scopri le nozioni di base dell’API HTTP di AEM Assets.
* Scopri in che modo i frammenti di contenuto sono supportati in questa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Dovresti continuare il tuo percorso headless AEM rivedendo il documento successivamente [Come utilizzare l&#39;applicazione headless](go-live.md) dove puoi portare in diretta il tuo progetto AEM Headless!

## Risorse aggiuntive {#additional-resources}

* [API HTTP di Assets](/help/assets/mac-api-assets.md)
* [API REST per frammenti di contenuto](/help/assets/assets-api-content-fragments.md)
   * [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference)
* [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
* [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
* [Spiegazione di CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=it)
* [Video: sviluppo per CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=it)
* Un [Introduzione all’AEM come CMS headless](/help/sites-developing/headless/introduction.md)
* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorials per headless nell&#39;AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
