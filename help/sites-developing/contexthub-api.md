---
title: Riferimento API di ContextHub Javascript
seo-title: Riferimento API di ContextHub Javascript
description: L’API Javascript di ContextHub è disponibile per i tuoi script quando il componente ContextHub è stato aggiunto alla pagina
seo-description: L’API Javascript di ContextHub è disponibile per i tuoi script quando il componente ContextHub è stato aggiunto alla pagina
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5031'
ht-degree: 3%

---


# Riferimento API ContextHub Javascript{#contexthub-javascript-api-reference}

L’API Javascript di ContextHub è disponibile per i tuoi script quando il componente [ContextHub è stato aggiunto alla pagina](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Costanti ContextHub {#contexthub-constants}

Valori costanti definiti dall’API Javascript di ContextHub.

### Costanti evento {#event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per gli archivi ContextHub. Vedi anche [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Costante | Descrizione | Valore |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | Spazio dei nomi evento di ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indica che tutti gli archivi richiesti sono registrati, inizializzati e pronti per essere consumati | pronto all&#39;uso |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indica che non tutti gli archivi sono stati inizializzati entro un determinato timeout | stores-parzialmente-ready |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Generato quando un negozio è registrato | registrato nel negozio |
| ContextHub.Constants.EVENT_STORE_READY | Indica che gli archivi sono pronti per funzionare. Viene attivato immediatamente dopo la registrazione, ad eccezione degli archivi JSONP, dove viene attivato quando i dati vengono recuperati). | pronto all&#39;uso |
| ContextHub.Constants.EVENT_STORE_UPDATED | Generato quando un archivio aggiorna la sua persistenza | aggiornato |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nome del contenitore di persistenza | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Memorizza il nome della chiave di persistenza specifica in cui è memorizzato il risultato JSON non elaborato | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Memorizza una marca temporale specifica che indica quando sono stati recuperati i dati JSON | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Memorizza l’url specifico del servizio JSON utilizzato durante l’ultima chiamata | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indica se l’interfaccia utente di ContextHub è espansa | /_/container-espanso |

### Costanti evento interfaccia utente {#ui-event-constants}

Nella tabella seguente sono elencati i nomi degli eventi che si verificano per l’interfaccia utente di ContextHub.

| **Costante** | **Descrizione** | **Valore** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Attivazione quando viene registrata una modalità | in modalità ui-registrato |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Attivato quando una modalità non è registrata | modalità interfaccia utente non registrata |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Generato quando viene registrato un renderer di modalità | registrati in modalità ui-renderer |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Generato quando un renderer di modalità non è registrato | in modalità ui-renderer-unregistrato |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Attivazione quando viene aggiunta una nuova modalità | aggiunto in modalità ui |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Attivato quando viene rimossa una modalità | modalità-ui-remove |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Attivazione quando l’utente seleziona una modalità | in modalità utente selezionata |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Generato quando viene registrato un nuovo modulo | registrato nell&#39;interfaccia utente |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Generato quando un modulo non viene registrato | modulo-ui non registrato |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Generato quando un modulo di rendering è registrato | utente-module-renderer-registrato |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Generato quando un modulo di rendering non viene registrato | modulo-ui-renderer-unregistrato |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Generato quando viene aggiunto un nuovo modulo | aggiunto al modulo |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Generato quando un modulo viene rimosso | rimosso dall&#39;interfaccia utente |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Generato quando il contenitore dell’interfaccia utente viene aggiunto alla pagina | aggiunto all’interfaccia utente |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Attivazione all’apertura dell’interfaccia utente di ContextHub | contenitore-aperto |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Attivazione quando l’interfaccia utente di ContextHub viene compressa | chiuso-contenitore-ui |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Generato quando una proprietà viene modificata | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | Viene attivata ogni volta che viene eseguito il rendering dell’interfaccia utente di ContextHub (ad esempio dopo una modifica della proprietà) | renderizzato dall&#39;interfaccia utente |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Generato quando il contenitore dell’interfaccia utente viene inizializzato | inizializzato dall&#39;interfaccia utente |
| ContextHub.Constants.ACTIVE_UI_MODE | Indica la modalità di interfaccia attiva | /_/active-ui-mode |

## Riferimento API ContextHub Javascript {#contexthub-javascript-api-reference-2}

L&#39;oggetto ContextHub fornisce l&#39;accesso a tutti gli archivi.

### Funzioni (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Restituisce tutti gli archivi ContextHub registrati.

Questa funzione non dispone di parametri.

**Valore restituito**

Un oggetto che contiene tutti gli archivi ContextHub. Ogni archivio è un oggetto che utilizza lo stesso nome dell&#39;archivio.

**Esempio**

L&#39;esempio seguente recupera tutti gli archivi e quindi recupera l&#39;archivio di geolocalizzazione:

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera un archivio come oggetto Javascript.

**Parametri**

* **name:** il nome con cui è stato registrato lo store.

**Valore restituito**

Oggetto che rappresenta l&#39;archivio.

**Esempio**

L&#39;esempio seguente recupera l&#39;archivio di geolocalizzazione:

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Rappresenta un segmento ContextHub. Utilizza ContextHub.SegmentEngine.SegmentManager per ottenere i segmenti.

### Funzioni (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Restituisce il nome del segmento come valore String.

#### getPath() {#getpath}

Restituisce il percorso di archivio della definizione del segmento come valore String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Consente l’accesso ai segmenti ContextHub.

### Funzioni (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Restituisce i segmenti risolti nel contesto corrente. Questa funzione non dispone di parametri.

**Valore restituito**

Matrice di oggetti ContextHub.SegmentEngine.Segment.

## ContextHub.Store.Core {#contexthub-store-core}

La classe di base per gli archivi ContextHub.

### Proprietà (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un oggetto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing). Utilizzare questo oggetto per eseguire il binding delle funzioni per memorizzare gli eventi. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

Nome del negozio.

#### persistenza {#persistence}

Un oggetto ContextHub.Utils.Persistence. Per informazioni sul valore predefinito e sull&#39;inizializzazione, vedere `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Funzioni (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Unisce un oggetto dati o una matrice ai dati archiviati. Ogni coppia chiave/valore nell&#39;oggetto o nella matrice viene aggiunta all&#39;archivio (tramite la funzione `setItem`):

* **Oggetto:** Le chiavi sono i nomi delle proprietà.
* **Array:** Le chiavi sono gli indici della matrice.

I valori possono essere oggetti.

**Parametri**

* **struttura:**  (oggetto o matrice) i dati da aggiungere all&#39;archivio.
* **options:** (Object) Un oggetto facoltativo di opzioni passato alla funzione setItem. Per informazioni, vedere il parametro `options` di [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Valore restituito**

Valore `boolean`:

* Il valore `true` indica che l’oggetto dati è stato memorizzato.
* Un valore di `false` indica che l’archivio dati è invariato.

#### addReference(key, otherKey) {#addreference-key-anotherkey}

Crea un riferimento da una chiave a un&#39;altra chiave. Una chiave non può fare riferimento a se stessa.

**Parametri**

* **key:** la chiave a cui fa riferimento  `anotherKey`.

* **altra chiave:** chiave a cui fa riferimento  `key`.

**Valore restituito**

Valore `boolean`:

* Un valore di `true` indica che il riferimento è stato aggiunto.
* Il valore `false` indica che non è stato aggiunto alcun riferimento.

#### annunciaReadiness() {#announcereadiness}

Attiva l&#39;evento `ready` per questo archivio. Questa funzione non ha parametri e non restituisce alcun valore.

#### clean() {#clean}

Rimuove tutti i dati dall’archivio. La funzione non dispone di parametri e di valori restituiti.

#### getItem(key) {#getitem-key}

Restituisce il valore associato a una chiave.

**Parametri**

* **key:**  (stringa) la chiave per la quale restituire il valore.

**Valore restituito**

Oggetto che rappresenta il valore della chiave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera le chiavi dall&#39;archivio. Facoltativamente, puoi recuperare le chiavi utilizzate internamente dal framework ContextHub.

**Parametri**

* **includeInternali:** un valore di  `true` include nei risultati le chiavi utilizzate internamente. Queste chiavi iniziano con il carattere di sottolineatura (&quot;_&quot;). Il valore predefinito è `false`.

**Valore restituito**

Matrice di nomi chiave ( `string` valori).

#### getReferences() {#getreferences}

Recupera i riferimenti dall&#39;archivio.

**Valore restituito**

Matrice che utilizza le chiavi di riferimento come indici per le chiavi di riferimento:

* Le chiavi di riferimento corrispondono al parametro `key` della funzione `addReference`.

* Le chiavi di riferimento corrispondono al parametro `anotherKey` della funzione `addReference`.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera la struttura dati dall&#39;archivio. Facoltativamente, puoi includere le coppie chiave/valore utilizzate internamente dal framework ContextHub.

**Parametri**

* `includeInternals:` Un valore di  `true` include nei risultati coppie chiave/valore utilizzate internamente. Le chiavi di questi dati iniziano con il carattere di sottolineatura (&quot;_&quot;). Il valore predefinito è `false`.

**Valore restituito**

Oggetto che rappresenta la struttura dati. Le chiavi sono i nomi delle proprietà dell&#39;oggetto.

#### init(name, config) {#init-name-config}

Inizializza l&#39;archivio.

* Imposta i dati dell&#39;archivio su un oggetto vuoto.
* Imposta i riferimenti dell&#39;archivio su un oggetto vuoto.
* L&#39;eventoChannel è data:*name*, dove *name* è il nome dell&#39;archivio.

* Il valore storeDataKey è /store/*name*, dove *name* è il nome dell&#39;archivio.

**Parametri**

* **name:** il nome dello store.
* **config:** un oggetto che contiene le proprietà di configurazione:

   * eventDeferring: Il valore predefinito è 32.
   * evento: L&#39;oggetto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) per questo archivio. Il valore predefinito è utilizzato dall&#39;oggetto ContextHub.eventing.
   * persistenza: L&#39;oggetto ContextHub.Utils.Persistence per questo archivio. Il valore predefinito è l&#39;oggetto ContextHub.persistence.

#### isEventingPaused() {#iseventingpaused}

Determina se l&#39;evento viene messo in pausa per questo archivio.

**Valore restituito**

Un valore booleano:

* `true`: L&#39;evento viene messo in pausa in modo che non vengano attivati eventi per questo archivio.
* `false`: L&#39;evento non viene messo in pausa in modo che gli eventi vengano attivati per questo archivio.

#### pauseEventing() {#pauseeventing}

Sospende l&#39;evento per l&#39;archivio in modo che non vengano attivati eventi. Questa funzione non richiede parametri e non restituisce alcun valore.

#### removeItem(key, options) {#removeitem-key-options}

Rimuove una coppia chiave/valore dall’archivio.

Quando una chiave viene rimossa, la funzione attiva l&#39;evento `data` . I dati dell&#39;evento includono il nome dell&#39;archivio, il nome della chiave rimossa, il valore rimosso, il nuovo valore per la chiave (null) e il tipo di azione &quot;remove&quot;.

Facoltativamente, puoi impedire l’attivazione dell’evento `data` .

**Parametri**

* **key:**  (stringa) il nome della chiave da rimuovere.
* **options:**  (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:

   * silenzioso: Un valore di `true` impedisce l&#39;attivazione dell&#39;evento `data` . Il valore predefinito è `false`.

**Valore restituito**

Valore `boolean`:

* Un valore di `true` indica che la coppia chiave/valore è stata rimossa.
* Un valore di `false` indica che l&#39;archivio dati è invariato perché la chiave non è stata trovata nell&#39;archivio.

#### removeReference(key) {#removereference-key}

Rimuove un riferimento dall&#39;archivio.

**Parametri**

* **key:** il riferimento chiave da rimuovere. Questo parametro corrisponde al parametro `key` della funzione `addReference`.

**Valore restituito**

Valore `boolean`:

* Un valore di `true` indica che il riferimento è stato rimosso.
* Un valore di `false` indica che la chiave non era valida e che l&#39;archivio è invariato.

#### reset(keepRemainData) {#reset-keepremainingdata}

Ripristina i valori iniziali dei dati persistenti dell&#39;archivio. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo negozio mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali vengono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

**Parametri**

* **keepRemainData:**  (booleano) Se si imposta il valore true, i dati non iniziali verranno mantenuti. Il valore false causa la rimozione di tutti i dati, ad eccezione dei valori iniziali.

Ripristina i valori iniziali dei dati persistenti dell&#39;archivio. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo negozio mentre lo store viene reimpostato. Questa funzione non restituisce alcun valore.

I valori iniziali vengono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

**Parametri**

* keepRemainData: (Booleano) Un valore true causa la persistenza dei dati non iniziali. Il valore false causa la rimozione di tutti i dati, ad eccezione dei valori iniziali.

#### resolveReference(key, try) {#resolvereference-key-retry}

Recupera una chiave di riferimento. Facoltativamente, puoi specificare il numero di iterazioni da utilizzare per risolvere la corrispondenza migliore.

**Parametri**

* **key:**  (stringa) la chiave per la quale risolvere il riferimento. Questo parametro `key` corrisponde al parametro `key` della funzione `addReference`.

* **riprova:**  (numero) Il numero di iterazioni da utilizzare.

**Valore restituito**

Valore `string` che rappresenta la chiave di riferimento. Se non viene risolto alcun riferimento, viene restituito il valore del parametro `key` .

#### curriculumEventing() {#resumeeventing}

Riprende gli eventi per questo archivio in modo che gli eventi vengano attivati. Questa funzione non definisce alcun parametro e non restituisce alcun valore.

#### setItem(key, value, options) {#setitem-key-value-options}

Aggiunge una coppia chiave/valore all’archivio.

Attiva l&#39;evento `data` solo se il valore della chiave è diverso dal valore attualmente memorizzato per la chiave. Facoltativamente, puoi impedire l’attivazione dell’evento `data` .

I dati dell’evento includono il nome dell’archivio, la chiave, il valore precedente, il nuovo valore e il tipo di azione `set`.

**Parametri**

* **key:** (String) Il nome della chiave.
* **options:**  (Oggetto) Un oggetto di opzioni. Le seguenti proprietà dell&#39;oggetto sono valide:

   * silenzioso: Un valore di `true` impedisce l&#39;attivazione dell&#39;evento `data` . Il valore predefinito è `false`.

* **value:** (Object) il valore da associare alla chiave.

**Valore restituito**

Valore `boolean`:

* Il valore `true` indica che l’oggetto dati è stato memorizzato.
* Un valore di `false` indica che l’archivio dati è invariato.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Un archivio che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno o facoltativamente da un servizio che restituisce dati JSON. Specifica i dettagli del servizio utilizzando la funzione [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) quando crei un&#39;istanza di questa classe.

L&#39;archivio utilizza la persistenza in memoria (variabile Javascript). I dati dell’archivio sono disponibili solo per tutta la durata della pagina.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) e eredita le funzioni di tale classe.

### Funzioni (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura i dettagli della connessione al servizio JSONP utilizzato da questo oggetto. È possibile aggiornare o sostituire la configurazione esistente. La funzione non restituisce alcun valore.

**Parametri**

* **serviceConfig:** oggetto che contiene le seguenti proprietà:

   * host: (Stringa) Il nome del server o l&#39;indirizzo IP.
   * jsonp: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {è: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.
   * parametri: (Oggetto) Parametri URL rappresentati come proprietà dell’oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
   * percorso: (Stringa) Il percorso del servizio.
   * porta: (Numero) Il numero di porta del servizio.
   * sicuro: (Stringa o booleana) Determina il protocollo da utilizzare per l&#39;URL del servizio:

      * auto: //
      * true: https://
      * false: https://

* **override:**  (booleano). Un valore di `true` fa sì che la configurazione del servizio esistente venga sostituita dalle proprietà di `serviceConfig`. Un valore di `false` fa sì che le proprietà di configurazione del servizio esistenti vengano unite alle proprietà di `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Restituisce la risposta non elaborata memorizzata nella cache dall&#39;ultima chiamata al servizio JSONP. La funzione non richiede parametri.

**Valore restituito**

Oggetto che rappresenta la risposta non elaborata.

#### getServiceDetails() {#getservicedetails}

Recupera l&#39;oggetto del servizio per questo oggetto ContextHub.Store.JSONPStore. L&#39;oggetto service contiene tutte le informazioni necessarie per creare l&#39;URL del servizio.

**Valore restituito**

Un oggetto con le seguenti proprietà:

* **host:**  (stringa) il nome del server o l&#39;indirizzo IP.
* **jsonp:**  (booleano) un valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, il callback {è: &quot;ContextHub.Callback.*L&#39;oggetto Object.name*} viene aggiunto all&#39;oggetto service.params.

* **parametri:**  (oggetto) parametri URL rappresentati come proprietà dell&#39;oggetto. I nomi dei parametri sono nomi di proprietà e i valori dei parametri sono valori di proprietà.
* **path:** (String) Il percorso del servizio.
* **porta:**  (numero) Il numero di porta del servizio.
* **secure:**  (String o Boolean) Determina il protocollo da utilizzare per l&#39;URL del servizio:

   * auto: //
   * true: https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera l&#39;URL del servizio JSONP.

**Parametri**

* **resolve:**  (booleano) Determina se includere nell&#39;URL i parametri risolti. Un valore di `true` risolve i parametri e `false` no.

**Valore restituito**

Valore `string` che rappresenta l&#39;URL del servizio.

#### init(name, config) {#init-name-config-1}

inizializza l&#39;oggetto ContextHub.Store.JSONPStore.

**Parametri**

* **name:** (String) Il nome dell&#39;archivio.
* **config:** (Object) Un oggetto che contiene la proprietà del servizio. L&#39;oggetto JSONPStore utilizza le proprietà dell&#39;oggetto `service` per costruire l&#39;URL del servizio JSONP:

   * eventDeferring: 32.
   * evento: L&#39;oggetto ContextHub.Utils.Eventing per questo archivio. Il valore predefinito è l&#39;oggetto `ContextHub.eventing` .
   * persistenza: L&#39;oggetto ContextHub.Utils.Persistence per questo archivio. Per impostazione predefinita, viene utilizzata la persistenza della memoria (oggetto Javascript).
   * servizio: (Oggetto)

      * host: (Stringa) Il nome del server o l&#39;indirizzo IP.
      * jsonp: (Booleano) Il valore true indica che il servizio è un servizio JSONP, false in caso contrario. Se true, l&#39;oggetto `{callback: "ContextHub.Callbacks.*Object.name*}`viene aggiunto a `service.params`.
      * parametri: (Oggetto) Parametri URL rappresentati come proprietà dell’oggetto. I nomi e i valori dei parametri sono rispettivamente i nomi e i valori delle proprietà dell&#39;oggetto.
      * percorso: (Stringa) Il percorso del servizio.
      * porta: (Numero) Il numero di porta del servizio.
      * sicuro: (Stringa o booleana) Determina il protocollo da utilizzare per l&#39;URL del servizio:

         * auto: //
         * true: https://
         * false: https://
      * timeout: (Numero) Il tempo di attesa della risposta del servizio JSONP prima del timeout, in millisecondi.
      * ttl: La quantità minima di tempo in millisecondi che trascorre tra le chiamate al servizio JSONP. (Vedere la funzione [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) ).


#### queryService(reload) {#queryservice-reload}

Esegue una query sul servizio JSONP remoto e memorizza nella cache la risposta. Se il tempo trascorso dalla precedente chiamata a questa funzione è inferiore al valore di `config.service.ttl`, il servizio non viene chiamato e la risposta nella cache non viene modificata. Facoltativamente, puoi forzare la chiamata del servizio. La proprietà `config.service.ttl`viene impostata quando si chiama la funzione [init](/help/sites-developing/contexthub-api.md#init-name-config) per inizializzare l&#39;archivio.

Attiva l&#39;evento ready al termine della query. Se l’URL del servizio JSONP non è impostato, la funzione non esegue alcuna operazione.

**Parametri**

* **reload:**  (booleano) Il valore true rimuove la risposta nella cache e forza la chiamata del servizio JSONP.

#### reset {#reset}

Reimposta i valori iniziali dei dati persistenti dell&#39;archivio e quindi chiama il servizio JSONP. Facoltativamente, puoi rimuovere tutti gli altri dati dall’archivio. L&#39;evento viene messo in pausa per questo archivio mentre i valori iniziali vengono reimpostati. Questa funzione non restituisce alcun valore.

I valori iniziali vengono forniti nella proprietà initialValues dell&#39;oggetto config utilizzato per creare un&#39;istanza dell&#39;oggetto store.

**Parametri**

* **keepRemainData:**  (booleano) Se si imposta il valore true, i dati non iniziali verranno mantenuti. Il valore false causa la rimozione di tutti i dati, ad eccezione dei valori iniziali.

#### resolveParameter(f) {#resolveparameter-f}

Risolve il parametro specificato.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore estende [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) in modo da ereditare tutte le funzioni di quella classe. Tuttavia, i dati recuperati dal servizio JSONP vengono mantenuti in base alla configurazione della persistenza ContextHub. (Vedere [Modalità di persistenza](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) in modo che erediti tutte le funzioni di quella classe. I dati in questo archivio vengono mantenuti in base alla configurazione della persistenza ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) in modo che erediti tutte le funzioni di quella classe. I dati in questo archivio vengono mantenuti utilizzando la persistenza in memoria (oggetto Javascript).

## ContextHub.UI {#contexthub-ui}

Gestisce i moduli di interfaccia utente e i moduli di rendering dell’interfaccia utente.

### Funzioni (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un modulo di rendering dell&#39;interfaccia utente con ContextHub. Dopo la registrazione del renderer, può essere utilizzato per [creare moduli di interfaccia utente](ch-configuring.md#adding-a-ui-module). Utilizza questa funzione quando [estendi ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) per creare un modulo di rendering personalizzato dell’interfaccia utente.

**Parametri**

* **moduleType:**  (String) l’identificatore del modulo di rendering dell’interfaccia utente. Se un renderer è già registrato utilizzando il valore specificato, il renderer esistente viene annullato prima della registrazione del renderer.
* **renderer:**  (stringa) il nome della classe che esegue il rendering del modulo dell’interfaccia utente.
* **dontRender:**  (booleano) imposta su  `true` per impedire il rendering dell&#39;interfaccia utente di ContextHub dopo la registrazione del renderer. Il valore predefinito è `false`.

**Esempio**

L’esempio seguente registra un renderer come tipo di modulo contexthub.browserinfo.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Classe di utilità per l&#39;interazione con i cookie.

### Funzioni (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se esiste un cookie.

**Parametri**

* **key:** un  `String` che contiene la chiave del cookie di cui stai eseguendo il test.

**Valore restituito**

Un valore `boolean` di true indica che il cookie esiste.

**Esempio**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Restituisce tutti i cookie con chiavi che corrispondono a un filtro.

**Parametri**

* (Facoltativo) **filtro:** Criteri per le chiavi dei cookie corrispondenti. Per restituire tutti i cookie, non specificare alcun valore. Sono supportati i seguenti tipi:

   * Stringa: La stringa viene confrontata con la chiave cookie.
   * Matrice: Ogni elemento della matrice è un filtro.
   * Un oggetto RegExp: La funzione di test dell&#39;oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Funzione: Funzione che verifica una chiave cookie per una corrispondenza. La funzione deve prendere la chiave cookie come parametro e restituire true se il test conferma una corrispondenza.

**Valore restituito**

Un oggetto di cookie. Le proprietà dell’oggetto sono chiavi cookie e i valori chiave sono valori cookie.

**Esempio**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Restituisce un valore cookie.

**Parametri**

* **key:** la chiave del cookie di cui desideri il valore.

**Valore restituito**

Il valore del cookie o `null` se non è stato trovato alcun cookie per la chiave.

**Esempio**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Restituisce una matrice delle chiavi dei cookie esistenti che corrispondono a un filtro.

**Parametri**

* **filter:** Criteri per la corrispondenza delle chiavi dei cookie. Sono supportati i seguenti tipi:

   * Stringa: La stringa viene confrontata con la chiave cookie.
   * Matrice: Ogni elemento della matrice è un filtro.
   * Un oggetto RegExp: La funzione di test dell&#39;oggetto viene utilizzata per far corrispondere le chiavi dei cookie.
   * Funzione: Funzione che verifica una chiave cookie per una corrispondenza. La funzione deve prendere la chiave cookie come parametro e restituire `true` se il test conferma una corrispondenza.

**Valore restituito**

Array di stringhe in cui ogni stringa è la chiave di un cookie che corrisponde al filtro.

**Esempio**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Rimuove un cookie. Per rimuovere il cookie, il valore è impostato su una stringa vuota e la data di scadenza è impostata sul giorno precedente la data corrente.

**Parametri**

* **key:** un  `String` valore che rappresenta la chiave del cookie da rimuovere.

* **options:** oggetto che contiene i valori delle proprietà per la configurazione degli attributi cookie. Per informazioni, consulta la funzione ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` . La proprietà `expires` non ha alcun effetto.

**Valore restituito**

Questa funzione non restituisce un valore.

**Esempio**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crea un cookie della chiave e del valore specificati e aggiunge il cookie al documento corrente. Facoltativamente, puoi specificare le opzioni che configurano gli attributi del cookie.

**Parametri**

* **key:** String che contiene la chiave del cookie.
* **value:** un valore String che contiene il valore del cookie.
* **options:**  (Facoltativo) un oggetto che contiene una delle seguenti proprietà che configurano gli attributi del cookie:

   * scade: Un valore `date` o `number` che specifica quando scade il cookie. Un valore di data specifica l&#39;ora assoluta di scadenza. Un numero (in giorni) imposta l&#39;ora di scadenza all&#39;ora corrente più il numero. Il valore predefinito è `undefined`.
   * sicuro: Un valore `boolean` che specifica l&#39;attributo `Secure` del cookie. Il valore predefinito è `false`.
   * percorso: Un valore `String` da utilizzare come attributo `Path` del cookie. Il valore predefinito è `undefined`.

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

Rimuove tutti i cookie che corrispondono a un determinato filtro. I cookie vengono associati utilizzando la funzione getKeys e rimossi utilizzando la funzione removeItem .

**Parametri**

* **filter:** l&#39; `filter` argomento da utilizzare nella chiamata alla  `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` funzione.

* **options:** l&#39; `options` argomento da utilizzare nella chiamata alla  `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` funzione.

**Valore restituito**

Questa funzione non restituisce un valore.

## ContextHub.Utils.Event {#contexthub-utils-eventing}

Consente di eseguire il binding e il binding delle funzioni agli eventi dell’archivio ContextHub. Accedi agli oggetti ContextHub.Utils.Eventing per un archivio utilizzando la proprietà [eventing](/help/sites-developing/contexthub-api.md#eventing) dell&#39;archivio.

### Funzioni (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Separa una funzione da un evento.

**Parametri**

* **name:** il  [nome dell’](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento per il quale si sta eseguendo il binding della funzione.

* **selettore:** il selettore che identifica il binding. (Vedere il parametro `selector` per le funzioni [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) e [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) ).

**Valore restituito**

Questa funzione non restituisce alcun valore.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Associa una funzione a un evento. La funzione viene chiamata ogni volta che si verifica l&#39;evento. Facoltativamente, è possibile chiamare la funzione per gli eventi che si sono verificati in passato, prima che venga stabilito il binding.

**Parametri**

* **name:** (String) Il  [nome dell&#39;](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento a cui si sta eseguendo il binding della funzione.

* **handler:**  (Funzione) La funzione da associare all&#39;evento.
* **selettore:**  (stringa) un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la funzione `off` per rimuovere il binding.

* **triggerForPastEvents:**  (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

**Valore restituito**

Quando l&#39;argomento `triggerForPastEvents` è `true`, questa funzione restituisce un valore `boolean` che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e verrà chiamato il gestore.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

**Esempio**

Nell&#39;esempio seguente viene associata una funzione all&#39;evento dati dell&#39;archivio di geolocalizzazione. La funzione popola un elemento della pagina con il valore dell&#39;elemento dati di latitudine dall&#39;archivio.

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

Associa una funzione a un evento. La funzione viene chiamata una sola volta, per la prima occorrenza dell&#39;evento. Facoltativamente, è possibile chiamare la funzione per l&#39;evento che si è verificato in passato, prima che il binding sia stabilito.

**Parametri**

* **name:** (String) Il  [nome dell&#39;](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento a cui si sta eseguendo il binding della funzione.

* **handler:**  (Funzione) La funzione da associare all&#39;evento.
* **selettore:**  (stringa) un identificatore univoco per il binding. È necessario che il selettore identifichi il binding se si desidera utilizzare la funzione `off` per rimuovere il binding.

* **triggerForPastEvents:**  (Boolean) Indica se il gestore deve essere eseguito per gli eventi che si sono verificati in passato. Un valore di `true` chiama il gestore per gli eventi passati. Un valore di `false` chiama il gestore per gli eventi futuri. Il valore predefinito è `true`.

**Valore restituito**

Quando l&#39;argomento `triggerForPastEvents` è `true`, questa funzione restituisce un valore `boolean` che indica se l&#39;evento si è verificato in passato:

* `true`: L&#39;evento si è verificato in passato e verrà chiamato il gestore.
* `false`: L&#39;evento non si è verificato in passato.

Se `triggerForPastEvents` è `false`, questa funzione non restituisce alcun valore.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Classe di utilità che consente a un oggetto di ereditare le proprietà e i metodi di un altro oggetto.

### Funzioni (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Fa sì che un oggetto erediti le proprietà e i metodi di un altro oggetto.

**Parametri**

* **secondario:**  (oggetto) l’oggetto che eredita.
* **parent:**  (Object) l&#39;oggetto che definisce le proprietà e i metodi ereditati.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornisce funzioni per serializzare gli oggetti in formato JSON e deserializzare le stringhe JSON negli oggetti.

### Funzioni (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analizza un valore stringa come JSON e lo converte in un oggetto javascript.

**Parametri**

* **data:** un valore stringa in formato JSON.

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

Serializza i valori e gli oggetti Javascript in valori stringa in formato JSON.

**Parametri**

* **data:** il valore o l’oggetto da serializzare. Questa funzione supporta valori booleani, array, numero, stringa e data.

**Valore restituito**

Il valore della stringa serializzata. Quando `data` è un valore R `egExp`, questa funzione restituisce un oggetto vuoto. Quando `data` è una funzione, restituisce `undefined`.

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

Questa classe facilita la manipolazione degli oggetti dati da memorizzare o recuperare dagli archivi ContextHub.

### Funzioni (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia di un oggetto dati e gli aggiunge la struttura dati da un secondo oggetto. La funzione restituisce la copia e non modifica nessuno degli oggetti originali. Quando le strutture ad albero dati dei due oggetti contengono chiavi identiche, il valore del secondo oggetto sovrascrive il valore del primo oggetto.

**Parametri**

* **tree:** l&#39;oggetto copiato.
* **secondoTree:** l&#39;oggetto unito alla copia dell&#39; `tree` oggetto.

**Valore restituito**

Oggetto contenente i dati uniti.

#### cleanup() {#cleanup}

Crea una copia di un oggetto, trova e rimuove gli elementi nella struttura dati che non contengono valori, valori nulli o valori non definiti e restituisce la copia.

**Parametri**

* **tree:** l’oggetto da pulire.

**Valore restituito**

Una copia dell&#39;albero che viene pulita.

#### getItem() {#getitem}

Recupera il valore da un oggetto per la chiave a.

**Parametri**

* **tree:** l&#39;oggetto dati.
* **key:** la chiave per il valore da recuperare.

**Valore restituito**

Il valore corrispondente alla chiave. Quando la chiave dispone di chiavi secondarie, questa funzione restituisce un oggetto complesso. Quando il tipo del valore della chiave è `undefined`, viene restituito `null`.

**Esempio**

Considera il seguente oggetto Javascript:

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

Il codice di esempio seguente restituisce il valore `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

Il codice di esempio seguente recupera il valore di una chiave con chiavi figlio:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La funzione restituisce il seguente oggetto:

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

Recupera tutte le chiavi dalla struttura dati di un oggetto. Facoltativamente, puoi recuperare solo le chiavi degli elementi secondari di una chiave specifica. Facoltativamente, puoi anche specificare un ordinamento delle chiavi recuperate.

**Parametri**

* **tree:** l’oggetto da cui recuperare le chiavi della struttura dati.
* **parent:**  (facoltativo) la chiave di un elemento nella struttura dati per la quale si desidera recuperare le chiavi degli elementi figlio.
* **order:**  (facoltativo) funzione che determina l’ordinamento delle chiavi restituite. (Consultare [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) in Mozilla Developer Network.)

**Valore restituito**

Un array di chiavi.

**Esempio**

Considera il seguente oggetto:

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

Lo script `ContextHub.Utils.JSON.tree.getKeys(myObject);` restituisce la seguente matrice:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia di un oggetto specificato, rimuove il ramo specificato dalla struttura dati e restituisce la copia modificata.

**Parametri**

* albero: Un oggetto dati.
* chiave: Chiave da rimuovere.

**Valore restituito**

Copia dell&#39;oggetto dati originale con la chiave rimossa.

**Esempio**

Considera il seguente oggetto:

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

Lo script di esempio seguente rimuove il ramo /uno/due/tre/quattro dalla struttura dati:

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La funzione restituisce il seguente oggetto:

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### cleanizeKey(key) {#sanitizekey-key}

Rimuove i valori stringa per renderli utilizzabili come chiavi. Per bonificare una stringa, questa funzione esegue le azioni seguenti:

* Riduce più barre consecutive a una singola barra.
* Rimuove gli spazi bianchi dall’inizio e dalla fine della stringa.
* Divide il risultato in una matrice di stringhe delimitate da barre.

Utilizzare la matrice risultante per creare una chiave utilizzabile.  **Parametri**

* **key:** L&#39; `string` da bonificare.

**Valore restituito**

Matrice di valori `string` in cui ogni stringa rappresenta la parte di `key` delimitata dalle barre. rappresenta la chiave sanizzata. Se la matrice bonificata ha una lunghezza pari a zero, questa funzione restituisce `null`.

**Esempio**

Il codice seguente rimuove una stringa per produrre l&#39;array `["this", "is", "a", "path"]`, quindi genera la chiave `"/this/is/a/path"` dall&#39;array:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Aggiunge una coppia chiave/valore alla struttura dati di una copia di un oggetto. Per informazioni sulle strutture ad albero dei dati, vedere [Persistence](/help/sites-developing/contexthub.md#persistence).

**Parametri**

* albero: Un oggetto dati.
* chiave: Chiave da associare al valore aggiunto. La chiave è il percorso dell’elemento nella struttura dati. Questa funzione chiama `ContextHub.Utils.JSON.tree.sanitize` per igienizzare la chiave prima di aggiungerla.
* valore: Valore da aggiungere alla struttura dati.

**Valore restituito**

Una copia dell&#39;oggetto `tree` che include la coppia `key`/ `value`.

**Esempio**

Prendi in considerazione il seguente codice JavaScript:

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

L&#39;oggetto myObject ha il seguente valore:

## ContextHub.Utils.storeCandidate {#contexthub-utils-storecandidates}

Consente di registrare i candidati allo store e ottenere i candidati allo store registrati.

### Funzioni (ContextHub.Utils.storeCandidate) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidate(storeType) {#getregisteredcandidates-storetype}

Restituisce i tipi di archivio registrati come candidati allo store. Recupera i candicati registrati di un tipo di archivio specifico o di tutti i tipi di archivio.

**Parametri**

* **storeType:** (String) Il nome del tipo di archivio. Vedere il parametro `storeType` della funzione [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) .

**Valore restituito**

Un oggetto di tipi di archivio. Le proprietà dell&#39;oggetto sono i nomi dei tipi di archivio e i valori delle proprietà sono una matrice di candidati store registrati.

#### getStoreFromCandidate(storeType) {#getstorefromcandidates-storetype}

Restituisce un tipo di archivio dai candidati registrati. Se vengono registrati più di un tipo di archivio con lo stesso nome, la funzione restituisce il tipo di archivio con la priorità più elevata.

**Parametri**

* storeType: (Stringa) Il nome del candidato dello store. Vedere il parametro `storeType` della funzione [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) .

**Valore restituito**

Oggetto che rappresenta il candidato all&#39;archiviazione registrato. Se il tipo di archivio richiesto non è registrato, viene generato un errore.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Restituisce i nomi dei tipi di archivio registrati come candidati allo store. Questa funzione non richiede parametri.

**Valore restituito**

Matrice di valori stringa, in cui ogni stringa è il tipo di archivio con cui è stato registrato un candidato all&#39;archiviazione. Vedere il parametro `storeType` della funzione [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) .

#### registerStoreCandidate(store, storeType, priority, applica) {#registerstorecandidate-store-storetype-priority-applies}

Registra un oggetto store come candidato all&#39;archiviazione utilizzando un nome e una priorità.

La priorità è un numero che indica l’importanza degli archivi con lo stesso nome. Quando un candidato del negozio viene registrato con lo stesso nome di un candidato del negozio già registrato, viene utilizzato il candidato con la priorità più alta. Quando si registra un candidato al negozio, il negozio viene registrato solo se la priorità è superiore ai candidati registrati dello stesso nome.

**Parametri**

* **store:**  (Oggetto) L&#39;oggetto store da registrare come candidato store.
* **storeType:** (String) Il nome del candidato dello store. Questo valore è necessario quando si crea un&#39;istanza del candidato store.
* **priorità:**  (numero) La priorità del candidato del negozio.
* **applica:**  (Funzione) La funzione da richiamare che valuta l&#39;applicabilità dell&#39;archivio nell&#39;ambiente corrente. La funzione deve restituire `true` se lo store è applicabile e `false` in caso contrario. Il valore predefinito è una funzione che restituisce true: `function() {return true;}`

**Esempio**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

