---
title: Supporto dei frammenti di contenuto di Adobe Experience Manager nell’API Assets HTTP
description: Scopri il supporto per i frammenti di contenuto nell’API Assets HTTP di, un’importante componente della funzione di distribuzione headless dell’AEM.
feature: Content Fragments,Assets HTTP API
role: Developer
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 25%

---

# Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets {#content-fragments-support-in-aem-assets-http-api}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=it) |
| AEM 6.5 | Questo articolo |


## Panoramica {#overview}

Scopri il supporto per i frammenti di contenuto nell’API Assets HTTP di, un’importante componente della funzione di distribuzione headless dell’AEM.

>[!NOTE]
>
>Il [API HTTP di Assets](/help/assets/mac-api-assets.md) comprende:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto
>
>L’implementazione corrente dell’API Assets HTTP si basa sulla [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) stile architettonico.

Il [API REST di Assets](/help/assets/mac-api-assets.md) consente agli sviluppatori di Adobe Experience Manager di accedere ai contenuti (memorizzati nell’AEM) direttamente tramite l’API HTTP, mediante operazioni CRUD (Create, Read, Update, Delete).

L’API consente di utilizzare Adobe Experience Manager come CMS (Content Management System) headless fornendo Content Services a un’applicazione front-end JavaScript. O qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio, le applicazioni a pagina singola (SPA), basate su framework o personalizzate, richiedono contenuti forniti tramite l’API HTTP, spesso in formato JSON.

Mentre [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) fornisce un’API molto completa, flessibile e personalizzabile che può servire alle operazioni di lettura necessarie a questo scopo e il cui output JSON può essere personalizzato richiede il know-how WCM (Web Content Management) dell’AEM per l’implementazione in quanto deve essere ospitato in pagine basate su modelli AEM dedicati. Non tutte le organizzazioni per lo sviluppo dell&#39;SPA hanno accesso diretto a tali conoscenze.

Qui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio immagini e frammenti di contenuto), senza doverle incorporare in una pagina, e di distribuire il contenuto in formato JSON serializzato.

>[!NOTE]
>
>Non è possibile personalizzare l’output JSON dall’API REST di Assets.

L’API REST di Assets consente inoltre agli sviluppatori di modificare i contenuti creando, aggiornando o eliminando risorse, frammenti di contenuto e cartelle esistenti.

API REST di Assets:

* segue la [Principio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa [Formato Sirena](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile su ogni installazione standard di una versione recente dell’AEM.

## Concetti fondamentali {#key-concepts}

Le offerte API REST di Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)accesso in stile alle risorse memorizzate all’interno di un’istanza AEM.

Utilizza il `/api/assets` e richiede il percorso della risorsa per accedervi (senza l&#39;opzione `/content/dam`).

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

Il metodo HTTP determina l’operazione da eseguire:

* **GET**: per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST**: per creare nuove risorse o cartelle
* **PUT**: per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE**: per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debbano essere create da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nel [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference) documentazione.

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che il successivo (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST di AEM (Assets) e componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Formato</td>
   <td>API REST di Assets<br/> </td>
   <td>Componente AEM<br/> (componenti che utilizzano modelli Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casi d’uso supportati</td>
   <td>Obiettivo generale.</td>
   <td><p>Ottimizzato per l’utilizzo in un contesto di applicazione a pagina singola (SPA) o in qualsiasi altro contesto (che consuma contenuti).</p> <p>Può contenere anche informazioni sul layout.</p> </td>
  </tr>
  <tr>
   <td>Operazioni supportate</td>
   <td><p>Crea, Leggi, Aggiorna, Elimina.</p> <p>Con operazioni aggiuntive a seconda del tipo di entità.</p> </td>
   <td>Sola lettura.</td>
  </tr>
  <tr>
   <td>Accesso</td>
   <td><p>È accessibile direttamente.</p> <p>Utilizza il <code>/api/assets </code>endpoint, mappato a <code>/content/dam</code> (nell’archivio).</p> 
   <p>Un esempio di percorso sarà simile al seguente: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Deve essere referenziato tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il <code>.model</code> per creare la rappresentazione JSON.</p> <p>Un esempio di percorso sarà simile al seguente:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Sicurezza</td>
   <td><p>Sono possibili più opzioni.</p> <p>OAuth è proposto; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza la configurazione standard dell’AEM.</td>
  </tr>
  <tr>
   <td>Osservazioni di architettura</td>
   <td><p>L'accesso in scrittura in genere si rivolge a un'istanza di authoring.</p> <p>La lettura può anche essere indirizzata a un’istanza Publish.</p> </td>
   <td>Poiché questo approccio è di sola lettura, in genere viene utilizzato per le istanze di pubblicazione.</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Output SIREN basato su JSON: dettagliato, ma potente. Consente di spostarsi all’interno del contenuto.</td>
   <td>Output proprietario basato su JSON; configurabile tramite modelli Sling. Navigare nella struttura del contenuto è difficile da implementare (ma non necessariamente impossibile).</td>
  </tr>
 </tbody>
</table>

### Sicurezza {#security}

Se l’API REST di Assets viene utilizzata in un ambiente senza requisiti di autenticazione specifici, il filtro AEM CORS deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Spiegazione di CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Video: sviluppo per CORS con AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

Negli ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa, vedi [Utilizzo dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per ulteriori informazioni sulle funzioni disponibili tramite l’API, consulta:

* Il [API REST di Assets](/help/assets/mac-api-assets.md)
* [Tipi di entità](/help/assets/assets-api-content-fragments.md#entity-types), in cui sono spiegate le funzioni specifiche di ciascun tipo supportato (come pertinenti ai frammenti di contenuto)

### Paging {#paging}

L’API REST di Assets supporta il paging (per le richieste GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta conterrà informazioni di paging come parte del `properties` sezione dell&#39;output SIREN. Questo `srn:paging` contiene il numero totale di entità (figlio) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>Il paging viene in genere applicato alle entità contenitore (ad esempio cartelle o risorse con rappresentazioni), in quanto si riferisce agli elementi figlio dell’entità richiesta.

#### Esempio: paging {#example-paging}

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

## Tipi di entità {#entity-types}

### Cartelle {#folders}

Le cartelle fungono da contenitori per risorse e altre cartelle. Riflettono la struttura dell’archivio dei contenuti dell’AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella, ad esempio il nome, il titolo e così via. Le risorse vengono esposte come entità secondarie di cartelle e sottocartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa delle risorse e cartelle figlio, l’elenco delle entità figlio può già contenere l’intero set di proprietà che definisce la rispettiva entità figlio. In alternativa, è possibile esporre solo un set ridotto di proprietà per un&#39;entità in questo elenco di entità figlio.

### Risorse {#assets}

Se viene richiesta una risorsa, la risposta ne restituirà i metadati, ad esempio titolo, nome e altre informazioni come definito dal rispettivo schema della risorsa.

I dati binari di una risorsa vengono esposti come collegamento SIREN di tipo `content`.

Le risorse possono avere più rappresentazioni. In genere vengono esposte come entità secondarie, ad eccezione della rappresentazione di una miniatura esposta come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

A [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri, date.

Poiché esistono diverse differenze *standard* risorse (come immagini o audio), si applicano alcune regole aggiuntive per la loro gestione.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono completamente contenuti nell’output JSON (all’interno del `properties` proprietà ).

* Sono anche considerati atomici, ovvero gli elementi e le varianti vengono esposti come parte delle proprietà del frammento e non come collegamenti o entità secondarie. Questo consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto, il *consumer* deve conoscere (come minimo) il modello di un frammento, anche se la maggior parte delle informazioni può essere dedotta dal payload, come tipi di dati e così via. fanno parte della definizione.

Per creare un frammento di contenuto, è necessario fornire il percorso (archivio interno) del modello.

#### Contenuto associato {#associated-content}

Il contenuto associato non è attualmente esposto.

## Utilizzando {#using}

L’utilizzo può variare a seconda che utilizzi un ambiente di authoring o pubblicazione di AEM, insieme al tuo caso d’uso specifico.

* Si consiglia vivamente di associare la creazione a un&#39;istanza di authoring ([e attualmente non è possibile replicare un frammento da pubblicare utilizzando questa API](/help/assets/assets-api-content-fragments.md#limitations)).
* La distribuzione è possibile da entrambi, in quanto AEM fornisce il contenuto richiesto solo in formato JSON.

   * L’archiviazione e la consegna da un’istanza di authoring AEM dovrebbero essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.

   * Per la distribuzione web live, si consiglia un’istanza di pubblicazione AEM.

>[!CAUTION]
>
>La configurazione del dispatcher su istanze AEM potrebbe bloccare l’accesso a `/api`.

>[!NOTE]
>
>Per maggiori dettagli, vedi [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference). In particolare, [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

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

## Limitazioni {#limitations}

Esistono alcune limitazioni:

* **I modelli per frammenti di contenuto non sono attualmente supportati**: non possono essere letti o creati. Per poter creare un frammento di contenuto o aggiornarne uno esistente, gli sviluppatori devono conoscere il percorso corretto del modello per frammenti di contenuto. Attualmente, l’unico metodo per ottenere una panoramica di questi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non sono presenti controlli per verificare se viene fatto riferimento a un frammento di contenuto esistente. Pertanto, ad esempio, l’eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina che contiene un riferimento al frammento di contenuto eliminato.
* **Tipo di dati JSON** L’output REST API di *Tipo di dati JSON* è attualmente *output basato su stringhe*.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visualizzati nelle circostanze pertinenti:

* **200** (OK) Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`
   * aggiornamento di un frammento di contenuto tramite `PUT`

* **201** (Creato) Restituito quando:

   * creazione di un frammento di contenuto tramite `POST`

* **404** (Non trovato) Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500** (Errore interno del server)

  >[!NOTE]
  >
  >Questo errore viene restituito:
  >
  >* si è verificato un errore che non può essere identificato con un codice specifico
  >* quando il payload specificato non era valido

  Di seguito sono elencati gli scenari comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (monospazio) generato:

   * La cartella principale non esiste (quando si crea un frammento di contenuto tramite `POST`)
   * Non è stato fornito alcun modello per frammenti di contenuto (cq:model è mancante), non può essere letto (a causa di un percorso non valido o di un problema di autorizzazione) o non è disponibile alcun modello per frammenti valido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * Impossibile creare il frammento di contenuto (potrebbe trattarsi di un problema di autorizzazione):

      * `Could not create content fragment`

   * Impossibile aggiornare il titolo e/o la descrizione:

      * `Could not set value on content fragment`

   * Impossibile impostare i metadati:

      * `Could not set metadata on content fragment`

   * Impossibile trovare o aggiornare l’elemento di contenuto

      * `Could not update content element`
      * `Could not update fragment data of element`

  I messaggi di errore dettagliati vengono in genere restituiti nel modo seguente:

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## Riferimento API {#api-reference}

Consulta qui per riferimenti API dettagliati:

* [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP di Assets](/help/assets/mac-api-assets.md)

   * [Funzioni disponibili](/help/assets/mac-api-assets.md#assets)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta:

* [Documentazione API HTTP di Assets](/help/assets/mac-api-assets.md)
* [Sessione AEM Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
