---
title: Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets
seo-title: Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets
description: Scopri il supporto per i frammenti di contenuto nell’API HTTP di AEM Assets.
seo-description: Scopri il supporto per i frammenti di contenuto nell’API HTTP di AEM Assets.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 3%

---


# Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets{#content-fragments-support-in-aem-assets-http-api}

## Panoramica {#overview}

>[!NOTE]
>
>L’ [API HTTP Assets](/help/assets/mac-api-assets.md) include:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto

>
>
L’implementazione corrente dell’API HTTP AEM Assets è REST.

Adobe Experience Manager (AEM) [API REST di Assets](/help/assets/mac-api-assets.md) consente agli sviluppatori di accedere ai contenuti (memorizzati in AEM) direttamente tramite l’API HTTP, tramite operazioni CRUD (Crea, Leggi, Aggiorna, Elimina).

L’API ti consente di utilizzare AEM come CMS headless (Content Management System) fornendo Content Services a un’applicazione front-end JavaScript. O qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio, le applicazioni a pagina singola (SPA), basate su framework o personalizzate, richiedono il contenuto fornito tramite l’API HTTP, spesso in formato JSON.

Anche se AEM componenti core forniscono un’API molto completa, flessibile e personalizzabile che può servire le operazioni di lettura necessarie a questo scopo e il cui output JSON può essere personalizzato, richiedono AEM know-how WCM (Web Content Management) per l’implementazione, in quanto devono essere ospitati in pagine (API) basate su modelli AEM dedicati. Non tutte le SPA organizzazioni di sviluppo hanno accesso a tali risorse.

Questo è il momento in cui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio, immagini e frammenti di contenuto) senza prima doverle incorporare in una pagina e di consegnare il contenuto in formato JSON serializzato. (Non è possibile personalizzare l’output JSON dall’API REST di Assets). L’API REST di Assets consente inoltre agli sviluppatori di modificare il contenuto creando nuove risorse, aggiornando o eliminando risorse esistenti, frammenti di contenuto e cartelle.

API REST di Assets:

* segue il principio [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa il [formato SIREN](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione di AEM recente.

## Concetti fondamentali {#key-concepts}

L’API REST di Assets offre accesso in stile [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) alle risorse memorizzate in un’istanza AEM. Utilizza l’ `/api/assets` endpoint e richiede il percorso della risorsa per accedervi (senza l’ `/content/dam` iniziale).

Il metodo HTTP determina l&#39;operazione da eseguire:

* **GET** : per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** : per creare nuove risorse o cartelle
* **PUT** : per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE** : per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debba essere creata da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nella documentazione [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference) .

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che le richieste successive (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST AEM (Assets) rispetto ai componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Aspetto</td>
   <td>API REST delle risorse<br /> </td>
   <td>AEM Componente<br /> (componenti che utilizzano modelli Sling)</td>
  </tr>
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
   <td><p>È accessibile direttamente.</p> <p>Utilizza l'endpoint <code>/api/assets </code>mappato a <code>/content/dam</code> (nel repository).</p> <p>Ad esempio, per accedere alla richiesta:<code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br />:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>Deve essere fatto riferimento tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il selettore <code>.model</code> per creare la rappresentazione JSON.</p> <p>Un esempio di URL potrebbe essere:<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
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
>* [Spiegazione di CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Video: sviluppo per CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



In ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa. Consulta [Uso dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per ulteriori informazioni sulle funzioni disponibili tramite API, consulta:

* [Funzioni disponibili ](/help/assets/mac-api-assets.md#assets) dell’API REST di Assets
* [Tipi di entità](/help/assets/assets-api-content-fragments.md#entity-types)

### Paging {#paging}

L’API REST di Assets supporta il paging (per richieste GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta conterrà informazioni di paging come parte della sezione `properties` dell&#39;output SIREN. Questa proprietà `srn:paging` contiene il numero totale di entità (secondarie) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>La paging viene in genere applicata alle entità contenitore (ovvero cartelle o risorse con rendering), in quanto si riferisce agli elementi secondari dell’entità richiesta.

#### Esempio: Paging {#example-paging}

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

Le cartelle fungono da contenitori per risorse e altre cartelle. Essi riflettono la struttura dell’archivio dei contenuti AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella; ad esempio nome, titolo, ecc. Le risorse vengono esposte come entità secondarie di cartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa, l’elenco delle entità figlio può già contenere l’intero set di proprietà che definisce la rispettiva entità figlio. In alternativa, solo un set ridotto di proprietà può essere esposto per un’entità in questo elenco di entità figlio.

### Assets {#assets}

Se viene richiesta una risorsa, la risposta restituirà i relativi metadati; quali titolo, nome e altre informazioni definite dallo schema delle risorse rispettive.

I dati binari di una risorsa sono esposti come collegamento SIREN di tipo `content` (noto anche come `rel attribute`).

Le risorse possono avere più rappresentazioni. Questi vengono generalmente esposti come entità secondarie, con un’eccezione rappresentata dal rendering delle miniature, che viene esposto come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, quali testi, numeri, date, ecc.

Poiché esistono diverse differenze tra le risorse *standard* (come immagini o audio), per gestirle è necessario applicare alcune regole aggiuntive.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono completamente contenute nell’output JSON (all’interno della proprietà `properties` ).

* Sono anche considerate atomiche, ovvero gli elementi e le varianti sono esposti come parte delle proprietà del frammento rispetto a come collegamenti o entità secondarie. Ciò consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto il *consumatore* deve conoscere il modello di un frammento (almeno un minimo), anche se la maggior parte delle informazioni può essere dedotta dal payload; come tipi di dati, ecc. fanno parte della definizione.

Per creare un nuovo frammento di contenuto, è necessario fornire il percorso (archivio interno).

#### Contenuto associato {#associated-content}

Il contenuto associato non è attualmente esposto.

## Utilizzando {#using}

L’utilizzo può variare a seconda che utilizzi un ambiente di authoring o pubblicazione AEM e del tuo caso d’uso specifico.

* La creazione è strettamente legata a un&#39;istanza dell&#39;autore ([e al momento non c&#39;è modo di replicare un frammento da pubblicare utilizzando questa API](/help/assets/assets-api-content-fragments.md#limitations)).
* La consegna è possibile da entrambi, in quanto AEM il contenuto richiesto solo in formato JSON.

   * L&#39;archiviazione e la consegna da un&#39;istanza di authoring AEM dovrebbero essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.
   * Per la distribuzione web live, si consiglia un’istanza di pubblicazione AEM.

>[!CAUTION]
>
>La configurazione del dispatcher su AEM istanze cloud potrebbe bloccare l’accesso a `/api`.

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Riferimento API](/help/assets/assets-api-content-fragments.md#api-reference). In particolare, [API Adobe Experience Manager Assets - Frammenti di contenuto](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### Lettura/consegna {#read-delivery}

L’utilizzo avviene tramite:

`GET /{cfParentPath}/{cfName}.json`

Esempio:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

La risposta viene serializzata JSON con il contenuto strutturato come nel frammento di contenuto. I riferimenti vengono consegnati come URL di riferimento.

Sono possibili due tipi di operazioni di lettura:

* Quando si legge un frammento di contenuto specifico in base al percorso, viene restituita la rappresentazione JSON del frammento di contenuto.
* Lettura di una cartella di frammenti di contenuto in base al percorso: restituisce le rappresentazioni JSON di tutti i frammenti di contenuto all’interno della cartella.

### Crea {#create}

L’utilizzo avviene tramite:

`POST /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON del frammento di contenuto da creare, incluso qualsiasi contenuto iniziale da impostare sugli elementi del frammento di contenuto. È obbligatorio impostare la proprietà `cq:model` e deve puntare a un modello di frammento di contenuto valido. In caso contrario si verifica un errore. È inoltre necessario aggiungere un&#39;intestazione `Content-Type` impostata su `application/json`.

### Aggiorna {#update}

Utilizzo tramite

`PUT /{cfParentPath}/{cfName}`

Il corpo deve contenere una rappresentazione JSON di ciò che deve essere aggiornato per il frammento di contenuto specificato.

Può trattarsi semplicemente del titolo o della descrizione di un frammento di contenuto, di un singolo elemento o di tutti i valori e/o metadati degli elementi. È inoltre obbligatorio fornire una proprietà `cq:model` valida per gli aggiornamenti.

### Elimina {#delete}

L’utilizzo avviene tramite:

`DELETE /{cfParentPath}/{cfName}`

## Limitazioni  {#limitations}

Ci sono alcune limitazioni:

* **Le varianti non possono essere scritte e aggiornate.** Se tali varianti vengono aggiunte a un payload (ad esempio, per aggiornamenti), verranno ignorate. Tuttavia, la variante verrà servita tramite consegna ( `GET`).

* **I modelli di frammento di contenuto non sono attualmente supportati**: non possono essere letti o creati. Per poter creare un nuovo frammento di contenuto o aggiornarne uno esistente, gli sviluppatori devono conoscere il percorso corretto per il modello di frammento di contenuto. Attualmente l’unico metodo per ottenere una panoramica di questi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non è disponibile alcun controllo per stabilire se viene fatto riferimento a un frammento di contenuto esistente. Pertanto, ad esempio, l’eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina contenente un riferimento.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visti nelle circostanze pertinenti:

* **200 (OK)**

   Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`

   * aggiornamento completato di un frammento di contenuto tramite `PUT`

* **201 (Creato)**

   Restituito quando:

   * creazione corretta di un frammento di contenuto tramite `POST`

* **404 (non trovato)**

   Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500 (errore server interno)**

   >[!NOTE]
   >
   >Questo errore viene restituito:
   >
   >
   >
   >    * quando si è verificato un errore che non può essere identificato con un codice specifico
   >    * quando il payload specificato non era valido


   Di seguito sono elencati gli scenari comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (monospazio) generato:

   * La cartella principale non esiste (durante la creazione di un frammento di contenuto tramite `POST`)
   * Non viene fornito alcun modello di frammento di contenuto (valore nullo), la risorsa è null (potenzialmente un problema di autorizzazione) o la risorsa non è un modello di frammento valido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
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

