---
title: Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets
seo-title: Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets
description: Informazioni sul supporto per i frammenti di contenuto in  API HTTP AEM Assets.
seo-description: Informazioni sul supporto per i frammenti di contenuto in  API HTTP AEM Assets.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 3%

---


# Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets{#content-fragments-support-in-aem-assets-http-api}

## Panoramica {#overview}

>[!NOTE]
>
>L’API [HTTP](/help/assets/mac-api-assets.md) Assets include:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto

>
>
L&#39;implementazione corrente di  API HTTP AEM Assets è REST.

L’API [REST di Adobe Experience Manager (AEM)](/help/assets/mac-api-assets.md) Assets consente agli sviluppatori di accedere al contenuto (memorizzato in AEM) direttamente tramite l’API HTTP, tramite operazioni CRUD (Crea, Leggi, Aggiorna, Elimina).

L&#39;API consente di utilizzare AEM come CMS headless (Content Management System) fornendo Content Services a un&#39;applicazione front-end JavaScript. Oppure qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire le risposte JSON.

Ad esempio, le applicazioni SPA (Single Page Applications), basate su framework o personalizzate, richiedono il contenuto fornito tramite l&#39;API HTTP, spesso in formato JSON.

I componenti core AEM forniscono un&#39;API molto completa, flessibile e personalizzabile che può servire le operazioni di lettura necessarie a questo scopo, e il cui output JSON può essere personalizzato, ma richiedono AEM know-how WCM (Web Content Management) per l&#39;implementazione, in quanto devono essere ospitati in pagine (API) basate su modelli AEM dedicati. Non tutte le organizzazioni di sviluppo SPA hanno accesso a tali risorse.

Questo è il momento in cui è possibile utilizzare l&#39;API REST di Risorse. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio, immagini e frammenti di contenuto), senza dover prima incorporarle in una pagina e distribuire i contenuti in formato JSON serializzato. (Non è possibile personalizzare l&#39;output JSON dall&#39;API REST di Assets). L’API REST di Risorse consente inoltre agli sviluppatori di modificare il contenuto, creando nuove risorse, aggiornando o eliminando risorse esistenti, frammenti di contenuto e cartelle.

API REST di Risorse:

* segue il principio [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa il formato [SIREN](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione out-of-the-box di una versione AEM recente.

## Concetti fondamentali {#key-concepts}

L’API REST di Risorse offre l’accesso [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)alle risorse memorizzate in un’istanza AEM. Utilizza l’ `/api/assets` endpoint e richiede il percorso della risorsa per accedervi (senza l’interlinea `/content/dam`).

Il metodo HTTP determina l’operazione da eseguire:

* **GET** - per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** - per creare nuove risorse o cartelle
* **PUT** - per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE** - per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, specificate che una cartella o una risorsa debba essere creata da una richiesta di **POST** .

Il formato esatto delle richieste supportate è definito nella documentazione [API Reference](/help/assets/assets-api-content-fragments.md#api-reference) .

### Comportamento Transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che le richieste successive (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST AEM (Risorse) e componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Aspetto</td>
   <td>API REST di Assets<br /> </td>
   <td>Componente<br /> AEM (componenti che utilizzano i modelli Sling)</td>
  </tr>
  <tr>
   <td>Casi d’uso supportati</td>
   <td>Scopo generale.</td>
   <td><p>Ottimizzato per il consumo in un'applicazione a pagina singola (SPA) o in qualsiasi altro contesto (che utilizza contenuti).</p> <p>Può anche contenere informazioni sul layout.</p> </td>
  </tr>
  <tr>
   <td>Operazioni supportate</td>
   <td><p>Crea, Leggi, Aggiorna, Elimina.</p> <p>Con operazioni aggiuntive in base al tipo di entità.</p> </td>
   <td>Sola lettura.</td>
  </tr>
  <tr>
   <td>Accesso</td>
   <td><p>È accessibile direttamente.</p> <p>Utilizza l’ <code>/api/assets </code>endpoint mappato su <code>/content/dam</code> (nella directory archivio).</p> <p>Ad esempio, per accedere a:<code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br /> richiesta:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>È necessario fare riferimento a un componente AEM in una pagina AEM.</p> <p>Utilizza il <code>.model</code> selettore per creare la rappresentazione JSON.</p> <p>Esempio di URL:<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>Sicurezza</td>
   <td><p>Sono possibili più opzioni.</p> <p>Si propone l'OAuth; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza AEM configurazione standard.</td>
  </tr>
  <tr>
   <td>Osservazioni architettoniche</td>
   <td><p>In genere, l'accesso in scrittura viene indirizzato a un'istanza di creazione.</p> <p>La lettura può essere diretta anche a un’istanza di pubblicazione.</p> </td>
   <td>Poiché questo approccio è di sola lettura, in genere viene utilizzato per le istanze di pubblicazione.</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Uscita SIREN basata su JSON: verboso, ma potente. Consente di spostarsi all'interno del contenuto.</td>
   <td>output proprietario basato su JSON; configurabile tramite Sling Models. Navigare nella struttura del contenuto è difficile da implementare (ma non necessariamente impossibile).</td>
  </tr>
 </tbody>
</table>

### Sicurezza {#security}

Se l&#39;API REST di Assets è utilizzata in un ambiente senza requisiti di autenticazione specifici, AEM filtro CORS deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [CORS/AEM spiegato](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Video - Sviluppo per CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



Negli ambienti con requisiti di autenticazione specifici, è consigliabile OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa. Consultate [Utilizzo dei frammenti](/help/assets/content-fragments/content-fragments.md)di contenuto.

Per ulteriori informazioni sulle funzioni disponibili tramite l&#39;API, vedete:

* [Funzionalità](/help/assets/mac-api-assets.md#assets) disponibili dell’API REST di Assets
* [Tipi di entità](/help/assets/assets-api-content-fragments.md#entity-types)

### Pagine {#paging}

L’API REST di Assets supporta il paging (per richieste di GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta conterrà informazioni di paging come parte della `properties` sezione dell&#39;output SIREN. Questa `srn:paging` proprietà contiene il numero totale di entità (figlio) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>Le pagine vengono in genere applicate alle entità contenitore (ovvero alle cartelle o alle risorse con rappresentazioni), in quanto si riferiscono agli elementi secondari dell&#39;entità richiesta.

#### Esempio: Pagine {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
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

Le cartelle fungono da contenitori per risorse e altre cartelle. che riflettono la struttura dell&#39;archivio dei contenuti AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella; ad esempio nome, titolo, ecc. Le risorse sono esposte come entità figlie di cartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa, l&#39;elenco di entità figlio potrebbe già contenere l&#39;intero set di proprietà che definisce la rispettiva entità figlio. In alternativa, solo una serie ridotta di proprietà può essere esposta per un&#39;entità in questo elenco di entità figlio.

### Assets {#assets}

Se viene richiesta una risorsa, la risposta restituirà i relativi metadati; come titolo, nome e altre informazioni, come definite dallo schema delle risorse corrispondenti.

I dati binari di una risorsa sono esposti come collegamento SIREN di tipo `content` (noto anche come `rel attribute`).

Le risorse possono avere più rappresentazioni. In genere sono esposte come entità figlie, con una sola eccezione rappresentata dalla rappresentazione in miniatura, che viene esposta come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

Un frammento [di](/help/assets/content-fragments/content-fragments.md) contenuto è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, come testi, numeri, date, ecc.

Poiché le risorse *standard* sono diverse (ad esempio immagini o audio), per gestirle è necessario applicare alcune regole aggiuntive.

#### Rappresentanza {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono completamente contenuti nell&#39;output JSON (all&#39;interno della `properties` proprietà).

* Sono anche considerati atomici, ovvero gli elementi e le variazioni sono esposti come parte delle proprietà del frammento rispetto a come collegamenti o entità figlio. Questo consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un&#39;API HTTP. Pertanto, il *consumatore* deve conoscere il modello di un frammento (almeno un minimo), anche se la maggior parte delle informazioni può essere ricavata dal payload; come tipi di dati, ecc. fanno parte della definizione.

Per creare un nuovo frammento di contenuto, è necessario fornire il percorso (archivio interno).

#### Contenuto associato {#associated-content}

Il contenuto associato al momento non è esposto.

## Utilizzando {#using}

L’utilizzo può variare a seconda se usate un ambiente di authoring o pubblicazione AEM e se usate un caso d’uso specifico.

* La creazione è strettamente legata a un&#39;istanza di creazione ([e al momento non esiste alcun modo per replicare un frammento da pubblicare utilizzando questa API](/help/assets/assets-api-content-fragments.md#limitations)).
* La consegna è possibile da entrambi, in quanto AEM il contenuto richiesto solo in formato JSON.

   * L’archiviazione e la distribuzione da un’istanza di creazione AEM dovrebbero essere sufficienti per le applicazioni libreria multimediale protette dal firewall.
   * Per la distribuzione Web dal vivo, è consigliabile un&#39;istanza di pubblicazione AEM.

>[!CAUTION]
>
>La configurazione del dispatcher AEM istanze cloud potrebbe bloccare l&#39;accesso a `/api`.

>[!NOTE]
>
>Per ulteriori dettagli, consultate [API Reference](/help/assets/assets-api-content-fragments.md#api-reference)(Riferimento API). In particolare, API [Adobe Experience Manager Assets - Frammenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)di contenuto.

### Lettura/Consegna {#read-delivery}

Utilizzo tramite:

`GET /{cfParentPath}/{cfName}.json`

Esempio:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

La risposta è JSON serializzata con il contenuto strutturato come nel frammento di contenuto. I riferimenti vengono forniti come URL di riferimento.

Sono possibili due tipi di operazioni di lettura:

* Leggendo un frammento di contenuto specifico per percorso, viene restituita la rappresentazione JSON del frammento di contenuto.
* Lettura di una cartella di frammenti di contenuto in base al percorso: restituisce le rappresentazioni JSON di tutti i frammenti di contenuto all’interno della cartella.

### Crea {#create}

Utilizzo tramite:

`POST /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON del frammento di contenuto da creare, incluso qualsiasi contenuto iniziale da impostare sugli elementi del frammento di contenuto. È obbligatorio impostare la `cq:model` proprietà e puntare a un modello di frammento di contenuto valido. In caso contrario si verificherà un errore. È inoltre necessario aggiungere un&#39;intestazione `Content-Type` impostata su `application/json`.

### Aggiorna {#update}

Utilizzo tramite

`PUT /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON di ciò che deve essere aggiornato per il frammento di contenuto specificato.

Può trattarsi semplicemente del titolo o della descrizione di un frammento di contenuto, di un singolo elemento o di tutti i valori e/o metadati dell&#39;elemento. È inoltre obbligatorio fornire una `cq:model` proprietà valida per gli aggiornamenti.

### Elimina {#delete}

Utilizzo tramite:

`DELETE /{cfParentPath}/{cfName}`

## Limitazioni  {#limitations}

Esistono alcuni limiti:

* **Le varianti non possono essere scritte e aggiornate.** Se tali varianti vengono aggiunte a un payload (ad es. per gli aggiornamenti), verranno ignorate. Tuttavia, la variazione sarà servita tramite consegna ( `GET`).

* **I modelli di frammento di contenuto non sono attualmente supportati**: non possono essere letti o creati. Per poter creare un nuovo frammento di contenuto o aggiornarne uno esistente, gli sviluppatori devono conoscere il percorso corretto del modello di frammento di contenuto. Attualmente l’unico metodo per ottenere una panoramica di questi metodi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non è disponibile alcun controllo per verificare se a un frammento di contenuto esistente viene fatto riferimento. Pertanto, ad esempio, l&#39;eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina che contiene un riferimento.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visti nelle circostanze pertinenti:

* **200 (OK)**

   Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`

   * aggiornamento di un frammento di contenuto tramite `PUT`

* **201 (Creato)**

   Restituito quando:

   * creazione di un frammento di contenuto tramite `POST`

* **404 (non trovato)**

   Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500 (errore interno del server)**

   >[!NOTE]
   >
   >Questo errore viene restituito:
   >
   >
   >
   >    * quando si è verificato un errore che non può essere identificato con un codice specifico
   >    * quando il payload specificato non era valido


   Di seguito sono elencati gli scenari più comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (spaziatura fissa) generato:

   * La cartella principale non esiste (durante la creazione di un frammento di contenuto tramite `POST`)
   * Non viene fornito alcun modello di frammento di contenuto (valore null), la risorsa è null (potenziale problema di autorizzazione) o la risorsa non è un modello di frammento valido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * Impossibile creare il frammento di contenuto (potenziale problema di autorizzazione):

      * `Could not create content fragment`
   * Impossibile aggiornare il titolo e la descrizione:

      * `Could not set value on content fragment`
   * Impossibile impostare i metadati:

      * `Could not set metadata on content fragment`
   * Impossibile trovare l&#39;elemento di contenuto o aggiornarlo

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

## API Reference {#api-reference}

Consultate qui per riferimenti API dettagliati:

* [API Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP di Assets](/help/assets/mac-api-assets.md)

   * [Funzioni disponibili](/help/assets/mac-api-assets.md#assets)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta:

* [Documentazione API HTTP Assets](/help/assets/mac-api-assets.md)
* [Sessione AEM Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)

