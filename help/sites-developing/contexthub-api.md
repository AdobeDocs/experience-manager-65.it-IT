---
title: Riferimento API ContextHub Javascript
seo-title: Riferimento API ContextHub Javascript
description: L'API ContextHub Javascript è disponibile per gli script quando il componente ContextHub è stato aggiunto alla pagina
seo-description: L'API ContextHub Javascript è disponibile per gli script quando il componente ContextHub è stato aggiunto alla pagina
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '5029'
ht-degree: 2%

---


# Riferimento API ContextHub Javascript{#contexthub-javascript-api-reference}

L&#39;API ContextHub Javascript è disponibile per gli script quando il componente [ContextHub è stato aggiunto alla pagina](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Costanti ContextHub {#contexthub-constants}

Valori costanti definiti dall&#39;API ContextHub Javascript.

### Costanti evento {#event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per gli store ContextHub. Vedere anche [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Costante | Descrizione | Valore |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | Spazio dei nomi evento di ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indica che tutti gli store richiesti sono registrati, inizializzati e pronti per essere consumati | all-stores-ready |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indica che non tutti gli store sono stati inizializzati entro un determinato timeout | magazzini parzialmente pronti |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Generato quando un negozio è registrato | registrato nel negozio |
| ContextHub.Constants.EVENT_STORE_READY | Indica che i negozi sono pronti per funzionare. Viene attivato immediatamente dopo la registrazione, ad eccezione degli store JSONP, dove viene attivato quando vengono estratti i dati. | pronto per il negozio |
| ContextHub.Constants.EVENT_STORE_UPDATED | Generato quando uno store aggiorna la sua persistenza | aggiornamento store |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nome contenitore persistenza | ContextHubPersistenza |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Memorizza il nome della chiave di persistenza specifica in cui è memorizzato il risultato JSON non elaborato | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Memorizza la marca temporale specifica che indica quando sono stati estratti i dati JSON | /_/tempo di risposta |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Memorizza l’URL specifico del servizio JSON utilizzato durante l’ultima chiamata | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indica se l&#39;interfaccia utente di ContextHub è espansa | /_/container-espanso |

### Costanti evento interfaccia utente {#ui-event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per l’interfaccia utente ContextHub.

| **Costante** | **Descrizione** | **Valore** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Generato quando una modalità viene registrata | in modalità automatica |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Generato quando una modalità non è registrata | ui-mode non registrato |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Generato quando viene registrato un renderer di modalità | modalità automatica, con rendering registrato |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Generato quando un renderer di modalità non è registrato | renderer in modalità automatica non registrato |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Generato quando viene aggiunta una nuova modalità | in modalità automatica |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Generato quando una modalità viene rimossa | rimosso in modalità automatica |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Generato quando l’utente seleziona una modalità | modalità di selezione automatica |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Generato quando viene registrato un nuovo modulo | modulo-utente registrato |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Generato quando un modulo non è registrato | modulo-ui non registrato |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Generato quando viene registrato un renderer di moduli | modulo-modulo-renderer registrato |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Generato quando un renderer di modulo non è registrato | Modulo-ui-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Generato quando viene aggiunto un nuovo modulo | modulo-aggiunto |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Generato quando un modulo viene rimosso | rimosso da un modulo |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Generato quando il contenitore dell’interfaccia utente viene aggiunto alla pagina | contenitore-aggiunto |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Generato all’apertura dell’interfaccia utente ContextHub | contenitore-ui aperto |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Generato quando l’interfaccia utente ContextHub viene compressa | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Generato quando una proprietà viene modificata | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | Generato ogni volta che viene eseguito il rendering dell’interfaccia utente ContextHub (ad esempio dopo una modifica di proprietà) | con riproduzione automatica |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Generato quando il contenitore dell&#39;interfaccia utente viene inizializzato | inizializzato dall&#39;utente |
| ContextHub.Constants.ACTIVE_UI_MODE | Indica la modalità interfaccia attiva | /_/active-ui-mode |

## Riferimento API ContextHub Javascript {#contexthub-javascript-api-reference-2}

L&#39;oggetto ContextHub consente l&#39;accesso a tutti gli store.

### Funzioni (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Restituisce tutti gli store ContextHub registrati.

Questa funzione non ha parametri.

**Valore restituito**

Un oggetto che contiene tutti gli store ContextHub. Ogni store è un oggetto che utilizza lo stesso nome dello store.

**Esempio**

L&#39;esempio seguente recupera tutti gli store e recupera lo store di geolocalizzazione:

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera uno store come oggetto Javascript.

**Parametri**

* **name:** Nome con cui è stato registrato lo store.

**Valore restituito**

Un oggetto che rappresenta lo store.

**Esempio**

L&#39;esempio seguente recupera l&#39;archivio di geolocalizzazione:

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Rappresenta un segmento ContextHub. Utilizzate ContextHub.SegmentEngine.SegmentManager per ottenere i segmenti.

### Funzioni (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Restituisce il nome del segmento come valore String.

#### getPath() {#getpath}

Restituisce il percorso di repository della definizione del segmento come valore String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornisce l&#39;accesso ai segmenti ContextHub.

### Funzioni (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Restituisce i segmenti risolti nel contesto corrente. Questa funzione non ha parametri.

**Valore restituito**

Un array di oggetti ContextHub.SegmentEngine.Segment.

## ContextHub.Store.Core {#contexthub-store-core}

La classe base per gli store ContextHub.

### Proprietà (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un oggetto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) . Utilizzare questo oggetto per eseguire il binding delle funzioni per memorizzare gli eventi. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

Il nome dello store.

#### persistenza {#persistence}

Un oggetto ContextHub.Utils.Persistenza. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedete `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Funzioni (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(struttura ad albero, opzioni) {#addallitems-tree-options}

Unisce un oggetto dati o una matrice ai dati dello store. Ogni coppia chiave/valore nell&#39;oggetto o nella matrice viene aggiunta allo store (tramite la `setItem` funzione):

* **Oggetto:** Le chiavi sono i nomi delle proprietà.
* **Array:** Le chiavi sono gli indici degli array.

I valori possono essere oggetti.

**Parametri**

* **struttura:** (Oggetto o array) I dati da aggiungere allo store.
* **opzioni:** (Oggetto) Un oggetto facoltativo di opzioni passato alla funzione setItem. Per informazioni, vedi il `options` parametro di [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Valore restituito**

Un `boolean` valore:

* Il valore di `true` indica che l&#39;oggetto dati è stato memorizzato.
* Il valore di `false` indica che l&#39;archivio dati è invariato.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Crea un riferimento da una chiave a un&#39;altra chiave. Una chiave non può fare riferimento a se stessa.

**Parametri**

* **key:** La chiave a cui fa riferimento `anotherKey`.

* **altra chiave:** Chiave a cui fa riferimento `key`.

**Valore restituito**

Un `boolean` valore:

* Un valore di `true` indica che il riferimento è stato aggiunto.
* Un valore di `false` indica che non è stato aggiunto alcun riferimento.

#### announceReadiness() {#announcereadiness}

Attiva l’ `ready` evento per lo store. Questa funzione non ha parametri e non restituisce alcun valore.

#### clean() {#clean}

Rimuove tutti i dati dallo store. La funzione non ha parametri e non restituisce valori.

#### getItem(key) {#getitem-key}

Restituisce il valore associato a una chiave.

**Parametri**

* **key:** (String) La chiave per la quale restituire il valore.

**Valore restituito**

Un oggetto che rappresenta il valore della chiave.

#### getKeys(includeInternali) {#getkeys-includeinternals}

Recupera le chiavi dallo store. Facoltativamente potete recuperare le chiavi utilizzate internamente dal framework ContextHub.

**Parametri**

* **includeInternali:** Un valore di `true` include le chiavi utilizzate internamente nei risultati. Queste chiavi iniziano con il carattere di sottolineatura (&quot;_&quot;). Il valore predefinito è `false`.

**Valore restituito**

Un array di nomi chiave ( `string` valori).

#### getReferences() {#getreferences}

Recupera i riferimenti dallo store.

**Valore restituito**

Un array che utilizza chiavi di riferimento come indici per le chiavi di riferimento:

* Le chiavi di riferimento corrispondono al `key` parametro della `addReference` funzione.

* Le chiavi di riferimento corrispondono al `anotherKey` parametro della `addReference` funzione.

#### getTree(includeInterni) {#gettree-includeinternals}

Recupera la struttura dati dallo store. Facoltativamente potete includere le coppie chiave/valore utilizzate internamente dal framework ContextHub.

**Parametri**

* `includeInternals:` Un valore di `true` include nei risultati coppie chiave/valore utilizzate internamente. Le chiavi di questi dati iniziano con il carattere di sottolineatura (&quot;_&quot;). Il valore predefinito è `false`.

**Valore restituito**

Un oggetto che rappresenta la struttura dei dati. Le chiavi sono i nomi delle proprietà dell&#39;oggetto.

#### init(name, config) {#init-name-config}

Inizializza lo store.

* Imposta i dati dello store su un oggetto vuoto.
* Imposta i riferimenti dell&#39;archivio su un oggetto vuoto.
* eventChannel è data:*name*, dove *name* è il nome dell&#39;archivio.

* StoreDataKey è /store/*name*, dove *name* è il nome dello store.

**Parametri**

* **name:** Il nome dello store.
* **config:** Un oggetto che contiene le proprietà di configurazione:

   * eventDeferring: Il valore predefinito è 32.
   * evento: L&#39;oggetto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) per questo store. Il valore predefinito è l&#39;oggetto ContextHub.eventing utilizzato.
   * persistenza: L&#39;oggetto ContextHub.Utils.Persistenza per lo store. Il valore predefinito è l&#39;oggetto ContextHub.persistence.

#### isEventingPaused() {#iseventingpaused}

Determina se l&#39;evento viene messo in pausa per lo store.

**Valore restituito**

Un valore booleano:

* `true`: Eventing viene messo in pausa in modo che non venga attivato alcun evento per lo store.
* `false`: Eventing non viene messo in pausa in modo che gli eventi vengano attivati per lo store.

#### pauseEventing() {#pauseeventing}

Sospende l&#39;evento per lo store in modo da non attivare eventi. Questa funzione non richiede parametri e non restituisce alcun valore.

#### removeItem(key, options) {#removeitem-key-options}

Rimuove una coppia chiave/valore dallo store.

Quando una chiave viene rimossa, la funzione attiva l&#39; `data` evento. I dati dell&#39;evento includono il nome dell&#39;archivio, il nome della chiave che è stata rimossa, il valore rimosso, il nuovo valore per la chiave (null) e il tipo di azione &quot;remove&quot;.

Facoltativamente, potete impedire l&#39;attivazione dell&#39; `data` evento.

**Parametri**

* **key:** (Stringa) Il nome della chiave da rimuovere.
* **opzioni:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:

   * silenzioso: Un valore di `true` impedisce l&#39;attivazione dell&#39; `data` evento. Il valore predefinito è `false`.

**Valore restituito**

Un `boolean` valore:

* Un valore di `true` indica che la coppia chiave/valore è stata rimossa.
* Il valore di `false` indica che l&#39;archivio dati è invariato perché la chiave non è stata trovata nello store.

#### removeReference(key) {#removereference-key}

Rimuove un riferimento dallo store.

**Parametri**

* **key:** Il riferimento chiave da rimuovere. Questo parametro corrisponde al `key` parametro della `addReference` funzione.

**Valore restituito**

Un `boolean` valore:

* Un valore di `true` indica che il riferimento è stato rimosso.
* Il valore di `false` indica che la chiave non era valida e che lo store non è cambiato.

#### reset(keepRemainData) {#reset-keepremainingdata}

Ripristina i valori iniziali dei dati persistenti dello store. Facoltativamente, puoi rimuovere tutti gli altri dati dallo store. L&#39;evento viene messo in pausa per lo store mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare l&#39;istanza dell&#39;oggetto store.

**Parametri**

* **keepRestainData:** (Booleano) Un valore true causa la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

Ripristina i valori iniziali dei dati persistenti dello store. Facoltativamente, puoi rimuovere tutti gli altri dati dallo store. L&#39;evento viene messo in pausa per lo store mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare l&#39;istanza dell&#39;oggetto store.

**Parametri**

* keepRestainData: (Booleano) Un valore true causa la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveReference(key, try) {#resolvereference-key-retry}

Recupera una chiave di riferimento. Facoltativamente, è possibile specificare il numero di iterazioni da utilizzare per risolvere la corrispondenza migliore.

**Parametri**

* **key:** (String) La chiave per la quale risolvere il riferimento. Questo `key` parametro corrisponde al `key` parametro della `addReference` funzione.

* **try:** (Numero) Il numero di iterazioni da utilizzare.

**Valore restituito**

Un `string` valore che rappresenta la chiave di riferimento. Se non viene risolto alcun riferimento, viene restituito il valore del `key` parametro.

#### curriculumEventing() {#resumeeventing}

Riprende l&#39;evento per lo store in modo da attivare gli eventi. Questa funzione non definisce alcun parametro e non restituisce alcun valore.

#### setItem(key, value, options) {#setitem-key-value-options}

Aggiunge una coppia chiave/valore allo store.

Attiva l&#39; `data` evento solo se il valore della chiave è diverso dal valore attualmente memorizzato per la chiave. Facoltativamente, potete impedire l&#39;attivazione dell&#39; `data` evento.

I dati dell&#39;evento includono il nome dello store, la chiave, il valore precedente, il nuovo valore e il tipo di azione di `set`.

**Parametri**

* **key:** (String) Il nome della chiave.
* **opzioni:** (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:

   * silenzioso: Un valore di `true` impedisce l&#39;attivazione dell&#39; `data` evento. Il valore predefinito è `false`.

* **value:** (Oggetto) Il valore da associare alla chiave.

**Valore restituito**

Un `boolean` valore:

* Il valore di `true` indica che l&#39;oggetto dati è stato memorizzato.
* Il valore di `false` indica che l&#39;archivio dati è invariato.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Uno store che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno o, facoltativamente, da un servizio che restituisce dati JSON. Specificate i dettagli del servizio utilizzando la [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) funzione al momento della creazione di un&#39;istanza di questa classe.

Lo store utilizza la persistenza in memoria (variabile Javascript). I dati dello store sono disponibili solo per tutta la durata della pagina.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) ed eredita le funzioni di tale classe.

### Funzioni (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura i dettagli per la connessione al servizio JSONP utilizzato da questo oggetto. Potete aggiornare o sostituire la configurazione esistente. La funzione non restituisce alcun valore.

**Parametri**

* **serviceConfig:** Un oggetto che contiene le proprietà seguenti:

   * host: (String) Il nome del server o l&#39;indirizzo IP.
   * jsonp: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {callback: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.
   * params: (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
   * percorso: (String) Il percorso del servizio.
   * porta: (Numero) Il numero di porta del servizio.
   * secure: (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:

      * auto: //
      * true: https://
      * false: https://

* **override:** (Boolean). Un valore di `true` determina la sostituzione della configurazione del servizio esistente con le proprietà di `serviceConfig`. Un valore di `false` determina l&#39;unione delle proprietà di configurazione del servizio esistenti con quelle di `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Restituisce la risposta non elaborata memorizzata nella cache dall&#39;ultima chiamata al servizio JSONP. La funzione non richiede parametri.

**Valore restituito**

Un oggetto che rappresenta la risposta non elaborata.

#### getServiceDetails() {#getservicedetails}

Recupera l&#39;oggetto del servizio per questo oggetto ContextHub.Store.JSONPStore. L&#39;oggetto service contiene tutte le informazioni necessarie per creare l&#39;URL del servizio.

**Valore restituito**

Un oggetto con le seguenti proprietà:

* **host:** (String) Il nome del server o l&#39;indirizzo IP.
* **jsonp:** (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {callback: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.

* **params:** (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
* **percorso:** (String) Il percorso del servizio.
* **porta:** (Numero) Il numero di porta del servizio.
* **secure:** (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:

   * auto: //
   * true: https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera l&#39;URL del servizio JSONP.

**Parametri**

* **resolve:** (Booleano) Determina se includere nell&#39;URL i parametri risolti. Un valore di `true` risolve i parametri e `false` non lo è.

**Valore restituito**

Un `string` valore che rappresenta l&#39;URL del servizio.

#### init(name, config) {#init-name-config-1}

inizializza l&#39;oggetto ContextHub.Store.JSONPStore.

**Parametri**

* **name:** (String) Il nome dello store.
* **config:** (Oggetto) Un oggetto che contiene la proprietà service. L&#39;oggetto JSONPStore utilizza le proprietà dell&#39; `service` oggetto per creare l&#39;URL del servizio JSONP:

   * eventDeferring: 32.
   * evento: L&#39;oggetto ContextHub.Utils.Eventing per lo store. Il valore predefinito è l&#39; `ContextHub.eventing` oggetto.
   * persistenza: L&#39;oggetto ContextHub.Utils.Persistenza per lo store. Per impostazione predefinita, viene utilizzata la persistenza della memoria (oggetto Javascript).
   * service: (Oggetto)

      * host: (String) Il nome del server o l&#39;indirizzo IP.
      * jsonp: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Quando è true, l&#39; `{callback: "ContextHub.Callbacks.*Object.name*}`oggetto viene aggiunto a `service.params`.
      * params: (Oggetto) Parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi e i valori dei parametri sono rispettivamente i nomi e i valori delle proprietà dell&#39;oggetto.
      * percorso: (String) Il percorso del servizio.
      * porta: (Numero) Il numero di porta del servizio.
      * secure: (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:

         * auto: //
         * true: https://
         * false: https://
      * timeout: (Numero) Il tempo di attesa che il servizio JSONP risponda prima del timeout, in millisecondi.
      * ttl: Il tempo minimo in millisecondi che trascorre tra le chiamate al servizio JSONP. (Vedere la funzione [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) ).


#### queryService(reload) {#queryservice-reload}

Interrompe il servizio JSONP remoto e memorizza nella cache la risposta. Se il tempo trascorso dalla precedente chiamata a questa funzione è inferiore al valore di `config.service.ttl`, il servizio non viene chiamato e la risposta nella cache non viene modificata. Facoltativamente, puoi forzare la chiamata al servizio. La `config.service.ttl`proprietà viene impostata quando si chiama la funzione [init](/help/sites-developing/contexthub-api.md#init-name-config) per inizializzare lo store.

Attiva l’evento ready al termine della query. Se l&#39;URL del servizio JSONP non è impostato, la funzione non esegue alcuna operazione.

**Parametri**

* **ricaricare:** (Booleano) Il valore true rimuove la risposta memorizzata nella cache e forza la chiamata al servizio JSONP.

#### reset {#reset}

Ripristina i valori iniziali dei dati persistenti dello store e chiama il servizio JSONP. Facoltativamente, puoi rimuovere tutti gli altri dati dallo store. L&#39;evento viene messo in pausa per lo store mentre i valori iniziali vengono reimpostati. Questa funzione non restituisce alcun valore.

I valori iniziali sono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare l&#39;istanza dell&#39;oggetto store.

**Parametri**

* **keepRestainData:** (Booleano) Un valore true causa la persistenza dei dati non iniziali. Se si imposta il valore false, tutti i dati vengono rimossi, ad eccezione dei valori iniziali.

#### resolveParameter(f) {#resolveparameter-f}

Risolve il parametro specificato.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore estende [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) in modo da ereditare tutte le funzioni di tale classe. Tuttavia, i dati recuperati dal servizio JSONP vengono memorizzati in base alla configurazione della persistenza ContextHub. (Vedere Modalità [di persistenza](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) in modo da ereditare tutte le funzioni di tale classe. I dati in questo archivio sono persistenti in base alla configurazione della persistenza ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) in modo da ereditare tutte le funzioni di tale classe. I dati in questo archivio sono persistenti utilizzando la persistenza in memoria (oggetto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestisce i moduli dell’interfaccia utente e i renderer dei moduli dell’interfaccia utente.

### Funzioni (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, DontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un renderer di moduli dell&#39;interfaccia utente con ContextHub. Dopo la registrazione del renderer, può essere utilizzato per [creare moduli](/help/sites-administering/contexthub-config.md#adding-a-ui-module)di interfaccia utente. Utilizzate questa funzione quando [estendete ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) per creare un renderer di moduli interfaccia utente personalizzato.

**Parametri**

* **moduleType:** (String) Identificatore per il renderer del modulo dell&#39;interfaccia utente. Se un renderer è già registrato utilizzando il valore specificato, il renderer esistente non viene registrato prima della registrazione del renderer.
* **renderer:** (String) Il nome della classe che esegue il rendering del modulo dell&#39;interfaccia utente.
* **dontRender:** (Booleano) Impostato `true` per impedire il rendering dell&#39;interfaccia utente ContextHub dopo la registrazione del renderer. Il valore predefinito è `false`.

**Esempio**

Nell&#39;esempio seguente, un renderer viene registrato come tipo di modulo contestexthub.browserinfo.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Una classe di utilità per l&#39;interazione con i cookie.

### Funzioni (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se esiste un cookie.

**Parametri**

* **key:** Un elemento `String` che contiene la chiave del cookie per il quale si sta eseguendo il test.

**Valore restituito**

Il `boolean` valore true indica che il cookie esiste.

**Esempio**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Restituisce tutti i cookie con chiavi che corrispondono a un filtro.

**Parametri**

* (Facoltativo) **filtro:** Criteri per la corrispondenza delle chiavi dei cookie. Per restituire tutti i cookie, non specificate alcun valore. Sono supportati i tipi seguenti:

   * Stringa: La stringa viene confrontata con il cookie key.
   * Array: Ogni elemento dell&#39;array è un filtro.
   * Un oggetto RegExp: La funzione test dell&#39;oggetto viene utilizzata per far corrispondere i tasti cookie.
   * Una funzione: Una funzione che verifica la presenza di un cookie key per una corrispondenza. La funzione deve prendere il cookie key come parametro e restituire true se il test conferma una corrispondenza.

**Valore restituito**

Un oggetto di cookie. Le proprietà dell&#39;oggetto sono cookie key e i valori chiave sono cookie values.

**Esempio**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Restituisce un valore di cookie.

**Parametri**

* **key:** Chiave del cookie per il quale si desidera ottenere il valore.

**Valore restituito**

Il valore del cookie, o `null` se non è stato trovato alcun cookie per la chiave.

**Esempio**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Restituisce un array delle chiavi dei cookie esistenti che corrispondono a un filtro.

**Parametri**

* **filter:** Criteri per la corrispondenza delle chiavi dei cookie. Sono supportati i tipi seguenti:

   * Stringa: La stringa viene confrontata con il cookie key.
   * Array: Ogni elemento dell&#39;array è un filtro.
   * Un oggetto RegExp: La funzione test dell&#39;oggetto viene utilizzata per far corrispondere i tasti cookie.
   * Una funzione: Una funzione che verifica la presenza di un cookie key per una corrispondenza. La funzione deve prendere il cookie key come parametro e restituire `true` se il test conferma una corrispondenza.

**Valore restituito**

Un array di stringhe in cui ogni stringa è la chiave di un cookie che corrisponde al filtro.

**Esempio**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Rimuove un cookie. Per rimuovere il cookie, il valore è impostato su una stringa vuota e la data di scadenza è impostata sul giorno prima della data corrente.

**Parametri**

* **key:** Un `String` valore che rappresenta la chiave del cookie da rimuovere.

* **opzioni:** Un oggetto che contiene i valori delle proprietà per la configurazione degli attributi del cookie. Vedere la ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` funzione per ulteriori informazioni. La `expires` proprietà non ha effetto.

**Valore restituito**

Questa funzione non restituisce un valore.

**Esempio**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea un cookie della chiave e del valore specificati e aggiunge il cookie al documento corrente. Facoltativamente, potete specificare opzioni che configurano gli attributi del cookie.

**Parametri**

* **key:** Una stringa che contiene la chiave del cookie.
* **value:** Una stringa che contiene il valore del cookie.
* **opzioni:** (Facoltativo) Un oggetto che contiene una delle seguenti proprietà che configurano gli attributi del cookie:

   * expires: Un valore `date` o `number` che specifica quando scade il cookie. Un valore data specifica l&#39;ora assoluta di scadenza. Un numero (in giorni) imposta l&#39;ora di scadenza sull&#39;ora corrente più il numero. Il valore predefinito è `undefined`.
   * secure: Un `boolean` valore che specifica l&#39; `Secure` attributo del cookie. Il valore predefinito è `false`.
   * percorso: Un `String` valore da utilizzare come `Path` attributo del cookie. Il valore predefinito è `undefined`.

**Valore restituito**

Il cookie con il valore impostato.

**Esempio**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Rimuove tutti i cookie che corrispondono a un determinato filtro. I cookie vengono associati utilizzando la funzione getKeys e rimossi utilizzando la funzione removeItem.

**Parametri**

* **filter:** L&#39; `filter` argomento da utilizzare nella chiamata alla `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` funzione.

* **opzioni:** L&#39; `options` argomento da utilizzare nella chiamata alla `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` funzione.

**Valore restituito**

Questa funzione non restituisce un valore.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Consente di eseguire il binding e la disassociazione delle funzioni agli eventi dell&#39;archivio ContextHub. Accedere agli oggetti ContextHub.Utils.Eventing per uno store utilizzando la proprietà [eventing](/help/sites-developing/contexthub-api.md#eventing) dello store.

### Funzioni (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Separa una funzione da un evento.

**Parametri**

* **name:** Il [nome dell&#39;evento](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) per il quale si desidera annullare il binding della funzione.

* **selettore:** Selettore che identifica il binding. (Vedere il `selector` parametro per le funzioni [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) e [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) ).

**Valore restituito**

Questa funzione non restituisce alcun valore.

#### on(nome, gestore, selettore, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Collega una funzione a un evento. La funzione viene chiamata ogni volta che si verifica l&#39;evento. Facoltativamente, è possibile chiamare la funzione per gli eventi che si sono verificati in passato, prima che venga stabilito il binding.

**Parametri**

* **name:** (Stringa) Il [nome dell&#39;evento](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) a cui si sta effettuando il binding della funzione.

* **handler:** (Funzione) La funzione da associare all&#39;evento.
* **selettore:** (String) Un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la `off` funzione per rimuovere il binding.

* **triggerForPastEvents:** (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore che `false` richiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

**Valore restituito**

Quando l&#39; `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e il gestore verrà chiamato.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

**Esempio**

Nell&#39;esempio seguente viene associata una funzione all&#39;evento data dell&#39;archivio di geolocalizzazione. La funzione compila un elemento sulla pagina con il valore per l&#39;elemento di dati di latitudine dallo store.

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(nome, gestore, selettore, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Collega una funzione a un evento. La funzione viene chiamata una sola volta, per la prima occorrenza dell&#39;evento. Facoltativamente, è possibile chiamare la funzione per l&#39;evento che si è verificato in passato, prima che venga stabilito il binding.

**Parametri**

* **name:** (Stringa) Il [nome dell&#39;evento](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) a cui si sta effettuando il binding della funzione.

* **handler:** (Funzione) La funzione da associare all&#39;evento.
* **selettore:** (String) Un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la `off` funzione per rimuovere il binding.

* **triggerForPastEvents:** (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore che `false` richiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

**Valore restituito**

Quando l&#39; `triggerForPastEvents` argomento è `true`, questa funzione restituisce un `boolean` valore che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e il gestore verrà chiamato.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Una classe di utilità che consente a un oggetto di ereditare le proprietà e i metodi di un altro oggetto.

### Funzioni (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Fa sì che un oggetto erediti le proprietà e i metodi di un altro oggetto.

**Parametri**

* **bambino:** (Oggetto) L&#39;oggetto che eredita.
* **parent:** (Oggetto) L&#39;oggetto che definisce le proprietà e i metodi ereditati.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornisce funzioni per la serializzazione di oggetti in formato JSON e la deserializzazione di stringhe JSON in oggetti.

### Funzioni (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analizza un valore di stringa come JSON e lo converte in un oggetto javascript.

**Parametri**

* **data:** Un valore stringa in formato JSON.

**Valore restituito**

Un oggetto Javascript.

**Esempio**

Il codice `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` restituisce il seguente oggetto:

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializza i valori e gli oggetti JavaScript in valori stringa del formato JSON.

**Parametri**

* **data:** Il valore o l&#39;oggetto da serializzare. Questa funzione supporta valori booleani, array, numero, stringa e data.

**Valore restituito**

Il valore di stringa serializzato. Quando `data` `egExp` è un valore R, questa funzione restituisce un oggetto vuoto. Quando `data` è una funzione, restituisce `undefined`.

**Esempio**

Il codice seguente restituisce `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Questa classe semplifica la manipolazione degli oggetti dati da memorizzare o da recuperare dagli store ContextHub.

### Funzioni (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia di un oggetto dati e vi aggiunge la struttura dati da un secondo oggetto. La funzione restituisce la copia e non modifica nessuno degli oggetti originali. Quando le strutture ad albero dati dei due oggetti contengono chiavi identiche, il valore del secondo oggetto sovrascrive il valore del primo oggetto.

**Parametri**

* **struttura:** L&#39;oggetto copiato.
* **SecondTree:** L&#39;oggetto unito alla copia dell&#39; `tree` oggetto.

**Valore restituito**

Un oggetto che contiene i dati uniti.

#### cleanup() {#cleanup}

Crea una copia di un oggetto, trova e rimuove elementi nella struttura dati che non contengono valori, valori null o valori non definiti e restituisce la copia.

**Parametri**

* **struttura:** L&#39;oggetto da pulire.

**Valore restituito**

Una copia della struttura ad albero che viene pulita.

#### getItem() {#getitem}

Recupera il valore da un oggetto per la chiave.

**Parametri**

* **struttura:** L&#39;oggetto data.
* **key:** Chiave per il valore da recuperare.

**Valore restituito**

Il valore corrispondente alla chiave. Quando la chiave dispone di chiavi figlio, questa funzione restituisce un oggetto complesso. Quando il tipo del valore della chiave è `undefined`, `null` viene restituito.

**Esempio**

Considerare il seguente oggetto Javascript:

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

Il seguente codice di esempio restituisce il valore `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

Il codice di esempio seguente recupera il valore per una chiave con chiavi figlio:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La funzione restituisce l&#39;oggetto seguente:

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera tutte le chiavi dalla struttura dati di un oggetto. Facoltativamente, è possibile recuperare solo le chiavi degli elementi secondari di una chiave specifica. Facoltativamente, potete anche specificare un ordinamento delle chiavi recuperate.

**Parametri**

* **struttura:** L&#39;oggetto da cui recuperare le chiavi della struttura dati.
* **parent:** (Facoltativo) Chiave di un elemento nella struttura dei dati per la quale si desidera recuperare le chiavi degli elementi secondari.
* **ordine:** (Facoltativo) Funzione che determina l&#39;ordine delle chiavi restituite. (Vedere [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) in Mozilla Developer Network.)

**Valore restituito**

Un array di chiavi.

**Esempio**

Considerare il seguente oggetto:

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

Lo `ContextHub.Utils.JSON.tree.getKeys(myObject);` script restituisce la seguente matrice:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia di un dato oggetto, rimuove il ramo specificato dalla struttura dei dati e restituisce la copia modificata.

**Parametri**

* struttura: Un oggetto dati.
* key: La chiave da rimuovere.

**Valore restituito**

Una copia dell&#39;oggetto dati originale con la chiave rimossa.

**Esempio**

Considerare il seguente oggetto:

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

Lo script di esempio seguente rimuove il ramo /uno/due/tre/quattro dalla struttura dei dati:

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La funzione restituisce l&#39;oggetto seguente:

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanizeKey(key) {#sanitizekey-key}

Rimuove i valori stringa per renderli utilizzabili come chiavi. Per eliminare una stringa, questa funzione esegue le azioni seguenti:

* Riduce più barre consecutive a una singola barra.
* Rimuove gli spazi bianchi dall&#39;inizio e dalla fine della stringa.
* Divide il risultato in un array di stringhe delimitate da barre.

Utilizzare l&#39;array risultante per creare una chiave utilizzabile.  **Parametri**

* **key:** La `string` pulizia.

**Valore restituito**

Un array di `string` valori in cui ogni stringa è la porzione di `key` cui sono state delimitate le barre. rappresenta la chiave sanizzata. Se la matrice sanizzata ha una lunghezza pari a zero, questa funzione restituisce `null`.

**Esempio**

Il codice seguente rimuove una stringa per generare l&#39;array `["this", "is", "a", "path"]`e genera quindi la chiave `"/this/is/a/path"` dall&#39;array:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Aggiunge una coppia chiave/valore alla struttura dati di una copia di un oggetto. Per informazioni sulle strutture ad albero dei dati, vedere [Persistenza](/help/sites-developing/contexthub.md#persistence).

**Parametri**

* struttura: Un oggetto dati.
* key: Chiave da associare al valore che si sta aggiungendo. La chiave è il percorso dell&#39;elemento nella struttura dei dati. Questa funzione richiede `ContextHub.Utils.JSON.tree.sanitize` di rimuovere completamente la chiave prima di aggiungerla.
* value: Valore da aggiungere alla struttura dati.

**Valore restituito**

Una copia dell&#39; `tree` oggetto che include la coppia `key`/ `value` .

**Esempio**

Considerate il seguente codice JavaScript:

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

L&#39;oggetto myObject ha il valore seguente:

## ContextHub.Utils.storeCandidate {#contexthub-utils-storecandidates}

Consente di registrare i candidati allo store e di ottenere i candidati allo store registrati.

### Funzioni (ContextHub.Utils.storeCandidate) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandiates(storeType) {#getregisteredcandidates-storetype}

Restituisce i tipi di store registrati come candidati store. Recuperare i candicati registrati di un tipo di archivio specifico o di tutti i tipi di store.

**Parametri**

* **storeType:** (String) Il nome del tipo di store. Vedere il `storeType` parametro della [ funzione `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) .

**Valore restituito**

Un oggetto di tipi di store. Le proprietà dell&#39;oggetto sono i nomi dei tipi di archivio e i valori delle proprietà sono un array di candidati store registrati.

#### getStoreFromCandidate(storeType) {#getstorefromcandidates-storetype}

Restituisce un tipo di archivio dai candidati registrati. Se viene registrato più di un tipo di store con lo stesso nome, la funzione restituisce il tipo di store con la priorità più alta.

**Parametri**

* storeType: (String) Il nome del candidato dello store. Vedere il `storeType` parametro della [ funzione `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) .

**Valore restituito**

Un oggetto che rappresenta il candidato dello store registrato. Se il tipo di archivio richiesto non è registrato, viene generato un errore.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Restituisce i nomi dei tipi di store registrati come candidati store. Questa funzione non richiede parametri.

**Valore restituito**

Un array di valori stringa, in cui ogni stringa è il tipo di storetype con cui è stato registrato un candidato all&#39;archiviazione. Vedere il `storeType` parametro della [ funzione `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) .

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra un oggetto store come candidato allo store utilizzando un nome e una priorità.

La priorità è un numero che indica l&#39;importanza degli store con lo stesso nome. Quando un candidato del negozio viene registrato con lo stesso nome di un candidato del negozio già registrato, viene utilizzato il candidato con la priorità più alta. Quando si registra un candidato per un negozio, lo store viene registrato solo se la priorità è superiore ai candidati dello store registrato dello stesso nome.

**Parametri**

* **store:** (Oggetto) L&#39;oggetto store da registrare come candidato store.
* **storeType:** (String) Il nome del candidato dello store. Questo valore è richiesto quando si crea un&#39;istanza del candidato store.
* **priorità:** (Numero) La priorità del candidato del negozio.
* **si applica:** (Funzione) La funzione da richiamare che valuta l&#39;applicabilità dello store nell&#39;ambiente corrente. La funzione deve restituire `true` se lo store è applicabile e `false` in caso contrario. Il valore predefinito è una funzione che restituisce true: `function() {return true;}`

**Esempio**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

