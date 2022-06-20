---
title: Supporto dei frammenti di contenuto Adobe Experience Manager nell’API HTTP delle risorse
description: Scopri il supporto per i frammenti di contenuto nell’API HTTP di Assets, una funzione importante AEM consegna headless.
feature: Content Fragments,Assets HTTP API
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 2%

---

# Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets {#content-fragments-support-in-aem-assets-http-api}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=en) |
| AEM 6.5 | Questo articolo |


## Panoramica {#overview}

Scopri il supporto per i frammenti di contenuto nell’API HTTP di Assets, una funzione importante AEM consegna headless.

>[!NOTE]
>
>La [API HTTP di Assets](/help/assets/mac-api-assets.md) comprende:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto
>
>L’implementazione corrente dell’API HTTP Assets si basa sul [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) stile architettonico.

La [API REST di Assets](/help/assets/mac-api-assets.md) consente agli sviluppatori di Adobe Experience Manager di accedere ai contenuti (memorizzati in AEM) direttamente tramite l’API HTTP tramite operazioni CRUD (Crea, Leggi, Aggiorna, Elimina).

L’API ti consente di utilizzare Adobe Experience Manager come CMS headless (Content Management System) fornendo servizi per contenuti a un’applicazione front-end JavaScript. O qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio, le applicazioni a pagina singola (SPA), basate su framework o personalizzate, richiedono il contenuto fornito tramite l’API HTTP, spesso in formato JSON.

Quando [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) fornisce un’API molto completa, flessibile e personalizzabile che può servire le operazioni di lettura necessarie a questo scopo e il cui output JSON può essere personalizzato, richiedono AEM know-how WCM (Web Content Management) per l’implementazione, in quanto devono essere ospitati in pagine basate su modelli AEM dedicati. Non tutte le SPA organizzazioni di sviluppo hanno accesso diretto a tali conoscenze.

Questo è il momento in cui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio, immagini e frammenti di contenuto) senza dover prima incorporarle in una pagina e consegnare il contenuto in formato JSON serializzato.

>[!NOTE]
>
>Non è possibile personalizzare l’output JSON dall’API REST di Assets.

L’API REST di Assets consente inoltre agli sviluppatori di modificare il contenuto creando nuove risorse, aggiornando o eliminando risorse esistenti, frammenti di contenuto e cartelle.

API REST di Assets:

* segue [Principio delle HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa [Formato SIREN](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione di AEM recente.

## Concetti fondamentali {#key-concepts}

Le offerte API REST di Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)Accesso in stile -style alle risorse memorizzate all’interno di un’istanza AEM.

Utilizza il `/api/assets` e richiede il percorso della risorsa per accedervi (senza l’iniziale `/content/dam`).

* Ciò significa che per accedere alla risorsa in:
   * `/content/dam/path/to/asset`
* È necessario richiedere:
   * `/api/assets/path/to/asset`

Ad esempio, per accedere a `/content/dam/wknd/en/adventures/cycling-tuscany`, richiesta `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Accedere a:
>
>* `/api/assets` **non** l&#39;uso `.model` selettore.
>* `/content/path/to/page` **does** richiedere l&#39;uso `.model` selettore.


Il metodo HTTP determina l&#39;operazione da eseguire:

* **GET** - per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** - per creare nuove risorse o cartelle
* **PUT** - per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE** - per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debba essere creata da un **POST** richiesta.

Il formato esatto delle richieste supportate è definito nella [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference) documentazione.

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che il successivo (`write`Le richieste ) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST AEM (Assets) e componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspetto</td>
   <td>API REST di Assets<br/> </td>
   <td>Componente AEM<br/> (componenti che utilizzano modelli Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casi d’uso supportati</td>
   <td>Scopo generale.</td>
   <td><p>Ottimizzato per il consumo in applicazioni a pagina singola (SPA) o in qualsiasi altro contesto (che consuma contenuti).</p> <p>Può anche contenere informazioni sul layout.</p> </td>
  </tr>
  <tr>
   <td>Operazioni supportate</td>
   <td><p>Crea, Leggi, Aggiorna, Elimina.</p> <p>Con operazioni aggiuntive a seconda del tipo di entità.</p> </td>
   <td>Sola lettura.</td>
  </tr>
  <tr>
   <td>Accesso</td>
   <td><p>È accessibile direttamente.</p> <p>Utilizza il <code>/api/assets </code>endpoint, mappato su <code>/content/dam</code> (nel repository).</p> 
   <p>Un esempio di percorso potrebbe essere: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Deve essere fatto riferimento tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il <code>.model</code> selettore per creare la rappresentazione JSON.</p> <p>Un esempio di percorso potrebbe essere:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Sicurezza</td>
   <td><p>Sono possibili più opzioni.</p> <p>è proposta l’OAuth; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza AEM configurazione standard.</td>
  </tr>
  <tr>
   <td>Osservazioni architettoniche</td>
   <td><p>L'accesso in scrittura si rivolge in genere a un'istanza dell'autore.</p> <p>La lettura può anche essere diretta a un'istanza di pubblicazione.</p> </td>
   <td>Poiché questo approccio è di sola lettura, in genere viene utilizzato per le istanze di pubblicazione.</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Output SIREN basato su JSON: verboso, ma potente. Consente di spostarsi all’interno del contenuto.</td>
   <td>output proprietario basato su JSON; configurabile tramite modelli Sling. La navigazione nella struttura dei contenuti è difficile da implementare (ma non necessariamente impossibile).</td>
  </tr>
 </tbody>
</table>

### Sicurezza {#security}

Se l’API REST di Assets viene utilizzata in un ambiente senza requisiti di autenticazione specifici, AEM filtro CORS deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Spiegazione di CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Video: sviluppo per CORS con AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>


In ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa, consulta [Utilizzo dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per ulteriori informazioni sulle funzioni disponibili tramite API, consulta:

* La [API REST di Assets](/help/assets/mac-api-assets.md)
* [Tipi di entità](/help/assets/assets-api-content-fragments.md#entity-types), dove vengono illustrate le funzioni specifiche di ciascun tipo supportato (in base ai frammenti di contenuto)

### Paging {#paging}

L’API REST di Assets supporta il paging (per richieste GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta conterrà informazioni di paging come parte del `properties` sezione dell&#39;uscita SIREN. Questo `srn:paging` contiene il numero totale di entità (secondarie) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>La paging viene in genere applicata alle entità contenitore (ovvero cartelle o risorse con rendering), in quanto si riferisce agli elementi secondari dell’entità richiesta.

#### Esempio: Paging {#example-paging}

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

Le cartelle fungono da contenitori per risorse e altre cartelle. Essi riflettono la struttura dell’archivio dei contenuti AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella; ad esempio nome, titolo, ecc. Le risorse vengono esposte come entità secondarie di cartelle e sottocartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa delle risorse e delle cartelle secondarie, l’elenco delle entità figlio può già contenere l’intero set di proprietà che definisce la rispettiva entità figlio. In alternativa, solo un set ridotto di proprietà può essere esposto per un’entità in questo elenco di entità figlio.

### Assets {#assets}

Se viene richiesta una risorsa, la risposta restituirà i relativi metadati; quali titolo, nome e altre informazioni definite dal rispettivo schema di risorse.

I dati binari di una risorsa sono esposti come collegamento SIREN di tipo `content`.

Le risorse possono avere più rappresentazioni. Questi sono generalmente esposti come entità secondarie, una delle quali è un rendering di miniature, che è esposto come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

A [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, quali testi, numeri, date, ecc.

Poiché esistono diverse differenze tra *standard* risorse (come immagini o audio), sono applicabili alcune regole aggiuntive per gestirle.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono completamente contenuti nell’output JSON (all’interno di `properties` proprietà).

* Sono anche considerate atomiche, ovvero gli elementi e le varianti sono esposti come parte delle proprietà del frammento rispetto a come collegamenti o entità secondarie. Ciò consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto, *consumer* deve conoscere il modello di un frammento (almeno un minimo), anche se la maggior parte delle informazioni può essere dedotta dal payload; come tipi di dati, ecc. fanno parte della definizione.

Per creare un nuovo frammento di contenuto, è necessario fornire il percorso (archivio interno) del modello.

#### Contenuto associato {#associated-content}

Il contenuto associato non è attualmente esposto.

## Utilizzando {#using}

L’utilizzo può variare a seconda che utilizzi un ambiente di authoring o pubblicazione AEM e del tuo caso d’uso specifico.

* Si consiglia vivamente di associare la creazione a un’istanza di authoring ([e al momento non esiste alcun modo per replicare un frammento da pubblicare utilizzando questa API](/help/assets/assets-api-content-fragments.md#limitations)).
* La consegna è possibile da entrambi, in quanto AEM il contenuto richiesto solo in formato JSON.

   * L&#39;archiviazione e la consegna da un&#39;istanza di authoring AEM dovrebbero essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.

   * Per la distribuzione web live, si consiglia un’istanza di pubblicazione AEM.

>[!CAUTION]
>
>La configurazione del dispatcher su AEM istanze potrebbe bloccare l’accesso a `/api`.

>[!NOTE]
>
>Per ulteriori dettagli, consulta la sezione [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference). In particolare, [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

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

Il corpo deve contenere una rappresentazione JSON del frammento di contenuto da creare, incluso qualsiasi contenuto iniziale da impostare sugli elementi del frammento di contenuto. È obbligatorio impostare il `cq:model` e deve puntare a un modello di frammento di contenuto valido. In caso contrario si verifica un errore. È inoltre necessario aggiungere un’intestazione `Content-Type` che è impostato su `application/json`.

### Aggiorna {#update}

Utilizzo tramite

`PUT /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON di ciò che deve essere aggiornato per il frammento di contenuto specificato.

Può trattarsi semplicemente del titolo o della descrizione di un frammento di contenuto, di un singolo elemento o di tutti i valori e/o metadati degli elementi.

### Elimina {#delete}

L’utilizzo avviene tramite:

`DELETE /{cfParentPath}/{cfName}`

## Limitazioni  {#limitations}

Ci sono alcune limitazioni:

* **I modelli di frammento di contenuto non sono attualmente supportati**: non possono essere letti o creati. Per poter creare un nuovo frammento di contenuto o aggiornarne uno esistente, gli sviluppatori devono conoscere il percorso corretto per il modello di frammento di contenuto. Attualmente l’unico metodo per ottenere una panoramica di questi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non è disponibile alcun controllo per stabilire se viene fatto riferimento a un frammento di contenuto esistente. Pertanto, ad esempio, l’eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina che contiene un riferimento al frammento di contenuto eliminato.
* **Tipo di dati JSON** L’output API REST di *Tipo di dati JSON* è attualmente *output basato su stringhe*.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visti nelle circostanze pertinenti:

* **200** (OK) Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`
   * aggiornamento di un frammento di contenuto tramite `PUT`

* **201** (Creato) Restituito quando:

   * creazione corretta di un frammento di contenuto tramite `POST`

* **404** (Non trovato) Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500** (Errore interno del server)

   >[!NOTE]
   >
   >Questo errore viene restituito:
   >
   >* quando si è verificato un errore che non può essere identificato con un codice specifico
   >* quando il payload specificato non era valido


   Di seguito sono elencati gli scenari comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (monospazio) generato:

   * La cartella principale non esiste (durante la creazione di un frammento di contenuto tramite `POST`)
   * Non viene fornito alcun modello di frammento di contenuto (cq:model mancante), non può essere letto (a causa di un percorso non valido o di un problema di autorizzazione) o non è disponibile un modello di frammento valido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * Impossibile creare il frammento di contenuto (potenzialmente un problema di autorizzazione):

      * `Could not create content fragment`
   * Impossibile aggiornare il titolo e la descrizione:

      * `Could not set value on content fragment`
   * Impossibile impostare i metadati:

      * `Could not set metadata on content fragment`
   * Impossibile trovare l&#39;elemento contenuto o aggiornarlo

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

Vedi qui per riferimenti API dettagliati:

* [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [API HTTP di Assets](/help/assets/mac-api-assets.md)

   * [Funzioni disponibili](/help/assets/mac-api-assets.md#assets)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta:

* [Documentazione API HTTP di Assets](/help/assets/mac-api-assets.md)
* [Sessione Gem AEM: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
