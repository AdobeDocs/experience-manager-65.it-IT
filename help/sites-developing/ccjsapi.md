---
title: API JavaScript ClientContext
seo-title: Client Context JavaScript API
description: Scopri l’API JavaScript per ClientContext in Adobe Experience Manager.
seo-description: The JavaScript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3157'
ht-degree: 2%

---

# API JavaScript ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

L&#39;oggetto CQ_Analytics.ClientContextMgr è un singleton che contiene un set di archivi di sessioni autoregistrati e fornisce metodi per la registrazione, la persistenza e la gestione degli archivi di sessioni.

Estende CQ_Analytics.PersistedSessionStore.

### Metodi {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Restituisce un archivio di sessione con il nome specificato. Vedi anche [Accesso a un archivio sessioni](/help/sites-developing/client-context.md#accessing-session-stores).

**Parametri**

* name: String. Nome dell&#39;archivio sessione.

**Restituisce**

Oggetto CQ_Analytics.SessionStore che rappresenta l&#39;archivio di sessione del nome specificato. Restituisce `null` quando non esiste alcun archivio con il nome specificato.

#### register(sessionstore) {#register-sessionstore}

Registra un archivio di sessione con ClientContext. Attiva gli eventi storeregister e storeupdate al completamento.

**Parametri**

* sessionstore: CQ_Analytics.SessionStore. Oggetto archivio sessione da registrare.

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornisce metodi per l&#39;ascolto dell&#39;attivazione e della registrazione dell&#39;archivio di sessione. Vedi anche [Controllo della definizione e dell&#39;inizializzazione di un archivio sessioni](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Metodi {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una funzione di callback chiamata quando viene inizializzato un archivio di sessione. Per gli archivi inizializzati più volte, specificare un ritardo di callback in modo che la funzione di callback venga chiamata una sola volta:

* Quando l’archivio viene inizializzato durante il periodo di ritardo di un’inizializzazione precedente, la chiamata di funzione precedente viene annullata e la funzione viene richiamata di nuovo per l’inizializzazione corrente.
* Se il periodo di ritardo scade prima che si verifichi una successiva inizializzazione, la funzione di callback viene eseguita due volte.

Ad esempio, un archivio di sessione è basato su un oggetto JSON e viene recuperato tramite una richiesta JSON. Sono possibili i seguenti scenari di inizializzazione:

* La richiesta è stata completata, i dati sono stati recuperati e caricati nell’archivio. In questo caso, l&#39;inizializzazione viene eseguita una volta.
* La richiesta non riesce (timeout). In questo caso l’inizializzazione non viene eseguita e non sono presenti dati nell’archivio.
* L’archivio è precompilato con i valori predefiniti (proprietà iniziali), ma la richiesta non riesce (timeout). Esiste una sola inizializzazione con i valori predefiniti.
* Il negozio è prepopolato.

Quando il ritardo è impostato su `true` oppure diversi millisecondi prima di richiamare il metodo callback. Se prima del superamento del ritardo viene attivato un altro evento di inizializzazione, questo attenderà il superamento del tempo di ritardo senza alcun evento di inizializzazione. Questo consente di attendere l’attivazione di un secondo evento di inizializzazione e chiama la funzione di callback nel caso più ottimale.

**Parametri**

* storeName: Stringa. Nome dell&#39;archivio sessione per aggiungere il listener.
* callback: funzione. Funzione da chiamare all’inizializzazione dell’archivio.
* delay: booleano o numero. Quantità di tempo per il ritardo della chiamata alla funzione di callback, in millisecondi. Valore booleano di `true` utilizza il ritardo predefinito di `200 ms`. Valore booleano di `false` o un numero negativo non fa sì che venga utilizzato alcun ritardo.

**Restituisce**

Nessun valore restituito.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una funzione di callback chiamata quando viene registrato un archivio di sessione. L&#39;evento di registrazione si verifica quando un archivio è registrato in [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parametri**

* storeName: Stringa. Nome dell&#39;archivio sessione per aggiungere il listener.
* callback: funzione. Funzione da chiamare all’inizializzazione dell’archivio.

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Archivio di sessione non persistente contenente dati JSON. I dati vengono recuperati da un servizio JSONP esterno. Utilizza il `getInstance` o `getRegisteredInstance` per creare un&#39;istanza di questa classe.

Estende l&#39;archivio CQ_Analytics.JSONS.

### Proprietà {#properties}

Consulta CQ_Analytics.JSONStore e CQ_Analytics.SessionStore per le proprietà ereditate.

### Metodi {#methods-2}

Vedi anche CQ_Analytics.JSONStore e CQ_Analytics.SessionStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un oggetto CQ_Analytics.JSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun storeName, il metodo restituisce null.
* serviceURL: String. URL del servizio JSONP
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* deferLoading: (facoltativo) booleano. Il valore true impedisce che il servizio JSONP venga richiamato durante la creazione dell&#39;oggetto. Se si imposta il valore false, viene chiamato il servizio JSONP.
* loadingCallback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

Il nuovo oggetto CQ_Analytics.JSONPStore o null se storeName è null.

#### getServiceURL() {#getserviceurl}

Recupera l&#39;URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Restituisce**

Stringa che rappresenta l&#39;URL del servizio oppure null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Chiama il servizio JSONP. L’URL JSONP è l’URL del servizio a cui viene aggiunto un nome di funzione di callback.

**Parametri**

* serviceURL: (facoltativo) stringa. Il servizio JSONP da chiamare. Se il valore è null, verrà utilizzato l&#39;URL del servizio già configurato. Un valore non Null imposta il servizio JSONP da utilizzare per questo oggetto. Consulta setServiceURL.
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* callback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un oggetto CQ_Analytics.JSONPStore e registra l&#39;archivio in ClientContext.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun storeName, il metodo restituisce null.
* serviceURL: (facoltativo) stringa. URL del servizio JSONP.
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* callback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

Oggetto CQ_Analytics.JSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Imposta l&#39;URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: String. URL del servizio JSONP che fornisce dati JSON

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Contenitore per un oggetto JSON. Crea un’istanza di questa classe per creare un archivio di sessioni non persistente contenente dati JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Puoi definire un set di dati che popola l’archivio al momento dell’inizializzazione.

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-1}

#### STOREKEY {#storekey}

Chiave che identifica l&#39;archivio. Utilizza il `getInstance` per recuperare questo valore.

#### STORENAME {#storename}

Nome dell’archivio. Utilizza il `getInstance` per recuperare questo valore.

### Metodi {#methods-3}

Vedi anche CQ_Analytics.SessionStore per i metodi ereditati.

#### cancella() {#clear}

Rimuove i dati dell&#39;archivio di sessione e tutte le proprietà di inizializzazione.

**Parametri**

Nessuno.

**Restituisce**

Nessun valore restituito.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: oggetto. Oggetto che contiene dati JSON.

**Restituisce**

Oggetto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera i dati dell’archivio sessione in formato JSON.

**Parametri**

Nessuno.

**Restituisce**

Oggetto che rappresenta i dati dell’archivio in formato JSON.

#### init() {#init}

Cancella l&#39;archivio di sessione e lo inizializza con la proprietà di inizializzazione. Imposta il flag di inizializzazione su `true` e quindi attiva il `initialize` e `update` eventi.

**Parametri**

Nessuno.

**Restituisce**

Nessun dato restituito.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crea proprietà di inizializzazione dai dati in un oggetto JSON. Facoltativamente, puoi rimuovere tutte le proprietà di inizializzazione esistenti.

I nomi delle proprietà sono derivati dalla gerarchia dei dati nell’oggetto JSON. Il codice di esempio seguente rappresenta un oggetto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

In questo esempio vengono create le seguenti proprietà nell&#39;archivio:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: un oggetto JSON che contiene i dati da archiviare.
* doNotClear: il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall’oggetto JSON.

**Restituisce**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON). Il nuovo oggetto viene registrato automaticamente con Clickstream Cloud Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: oggetto. Oggetto che contiene dati JSON.

**Restituisce**

Oggetto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Attiva gli eventi e consente ad altri oggetti di ascoltarli e reagire. Le classi che estendono questa classe possono generare eventi che causano la chiamata dei listener.

### Metodi {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra un listener per un evento. Vedi anche [Creazione di un listener per reagire a un aggiornamento dell’archivio sessioni](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parametri**

* event: String. Nome dell’evento da ascoltare.
* fct: Funzione. Funzione chiamata quando si verifica l’evento.
* ambito: oggetto (facoltativo). Ambito in cui eseguire la funzione del gestore. Contesto &quot;this&quot; della funzione di gestione.

**Restituisce**

Nessun valore restituito.

#### removeListener(event, fct) {#removelistener-event-fct}

Rimuove il gestore eventi specificato per un evento.

**Parametri**

* event: String. Nome dell’evento.
* fct: Funzione. Gestore eventi.

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Contenitore persistente di un oggetto JSON recuperato da un servizio JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Metodi {#methods-5}

Vedi anche CQ_Analytics.PersistedJSONStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun storeName, il metodo restituisce null.
* serviceURL: String. URL del servizio JSONP
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* deferLoading: (facoltativo) booleano. Il valore true impedisce che il servizio JSONP venga richiamato durante la creazione dell&#39;oggetto. Se si imposta il valore false, viene chiamato il servizio JSONP.
* loadingCallback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

Il nuovo oggetto CQ_Analytics.PersistedJSONPStore o null se storeName è null.

#### getServiceURL() {#getserviceurl-1}

Recupera l&#39;URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Restituisce**

Stringa che rappresenta l&#39;URL del servizio oppure null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Chiama il servizio JSONP. L’URL JSONP è l’URL del servizio a cui viene aggiunto un nome di funzione di callback.

**Parametri**

* serviceURL: (facoltativo) stringa. Il servizio JSONP da chiamare. Se il valore è null, verrà utilizzato l&#39;URL del servizio già configurato. Un valore non Null imposta il servizio JSONP da utilizzare per questo oggetto. Consulta setServiceURL.
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* callback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore e registra l&#39;archivio in ClientContext.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun storeName, il metodo restituisce null.
* serviceURL: (facoltativo) stringa. URL del servizio JSONP.
* dynamicData: oggetto (facoltativo). Dati JSON da aggiungere ai dati di inizializzazione dell’archivio prima che venga chiamata la funzione di callback.
* callback: (facoltativo) stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Restituisce**

L&#39;oggetto CQ_Analytics.PersistedJSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Imposta l&#39;URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: String. URL del servizio JSONP che fornisce dati JSON

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Contenitore persistente di un oggetto JSON.

Estende `CQ_Analytics.PersistedSessionStore`.

### Proprietà {#properties-2}

#### STOREKEY {#storekey-1}

Chiave che identifica l&#39;archivio. Utilizza il `getInstance` per recuperare questo valore.

#### STORENAME {#storename-1}

Nome dell’archivio. Utilizza il `getInstance` per recuperare questo valore.

### Metodi {#methods-6}

Vedi anche CQ_Analytics.PersistedSessionStore per i metodi ereditati.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: oggetto. Oggetto che contiene dati JSON.

**Restituisce**

Oggetto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera i dati dell’archivio sessione in formato JSON.

**Parametri**

Nessuno.

**Restituisce**

Oggetto che rappresenta i dati dell’archivio in formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crea proprietà di inizializzazione dai dati in un oggetto JSON. Facoltativamente, puoi rimuovere tutte le proprietà di inizializzazione esistenti.

I nomi delle proprietà sono derivati dalla gerarchia dei dati nell’oggetto JSON. Il codice di esempio seguente rappresenta un oggetto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

In questo esempio vengono create le seguenti proprietà nell&#39;archivio:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: un oggetto JSON che contiene i dati da archiviare.
* doNotClear: il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall’oggetto JSON.

**Restituisce**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON). Il nuovo oggetto viene registrato automaticamente con ClientContext Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY viene impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: oggetto. Oggetto che contiene dati JSON.

**Restituisce**

Oggetto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Contenitore di proprietà e valori. I dati vengono memorizzati utilizzando CQ_Analytics.SessionPersistence. Creare un&#39;istanza di questa classe per creare un archivio di sessioni persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-3}

#### STOREKEY {#storekey-2}

Il valore predefinito è `key`.

### Metodi {#methods-7}

Consulta CQ_Analytics.SessionStore per i metodi ereditati.

Quando i metodi ereditati `clear`, `setProperty`, `setProperties`, `removeProperty` vengono utilizzate per modificare i dati dell’archivio, le modifiche vengono rese automaticamente persistenti, a meno che le proprietà modificate non vengano contrassegnate come notPersisted.

#### getStoreKey() {#getstorekey}

Recupera il `STOREKEY` proprietà.

**Parametri**

Nessuno

**Restituisce**

Il valore della proprietà `STOREKEY` proprietà.

#### isPersisted(name) {#ispersisted-name}

Determina se una proprietà di dati è persistente.

**Parametri**

* name: String. Nome della proprietà.

**Restituisce**

Un valore booleano di `true` se la proprietà è persistente e un valore di `false` se il valore non è una proprietà persistente.

#### persist() {#persist}

Persiste nell&#39;archivio della sessione. La modalità di persistenza predefinita utilizza il browser `localStorage` utilizzo `ClientSidePersistence` come nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage non è disponibile o scrivibile, l&#39;archivio viene mantenuto come proprietà della finestra.

Attiva il `persist` al completamento.

**Parametri**

Nessuno

**Restituisce**

Nessun valore restituito.

#### reset(deferEvent) {#reset-deferevent}

Rimuove tutte le proprietà dei dati dall&#39;archivio e lo salva in modo permanente. Facoltativamente, non attiva il `udpate` al completamento.

**Parametri**

* deferEvent: un valore true impedisce che `update` dall&#39;attivazione dell&#39;evento. Un valore di `false` attiva l&#39;evento di aggiornamento.

**Restituisce**

Nessun valore restituito.

#### setNonPersisted(name) {#setnonpersisted-name}

Segnala una proprietà di dati come non persistente.

**Parametri**

* name: String. Nome della proprietà che non deve essere resa persistente.

**Restituisce**

Nessun valore restituito.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore rappresenta un archivio di sessione. Creare un&#39;istanza di questa classe per creare un archivio di sessione:

`mystore = new CQ_Analytics.SessionStore`

Estende CQ_Analytics.Observable.

### Proprietà {#properties-4}

#### STORENAME {#storename-2}

Nome dell&#39;archivio sessione. Utilizzare getName per recuperare il valore di questa proprietà.

### Metodi {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Aggiunge una proprietà e un valore ai dati di inizializzazione dell&#39;archivio sessioni.

Utilizzare loadInitProperties per popolare i dati dell&#39;archivio sessione con i valori di inizializzazione.

**Parametri**

* name: String. Nome della proprietà da aggiungere.
* value: String. Valore della proprietà da aggiungere.

**Restituisce**

Nessun valore restituito.

#### cancella() {#clear-1}

Rimuove tutte le proprietà dei dati dall&#39;archivio.

**Parametri**

Nessuno.

**Restituisce**

Nessun valore restituito.

#### getData(excluded) {#getdata-excluded}

Restituisce i dati dell&#39;archivio. Facoltativamente, esclude le proprietà del nome dai dati. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

excluded: (facoltativo) array di nomi di proprietà da escludere dai dati restituiti.

**Restituisce**

Oggetto di proprietà e relativi valori.

#### getInitProperty(name) {#getinitproperty-name}

Recupera il valore di una proprietà dati.

**Parametri**

* name: String. Nome della proprietà dati da recuperare.

**Restituisce**

Valore della proprietà dati. Ritorni `null` se l’archivio di sessione non contiene alcuna proprietà con il nome specificato.

#### getName() {#getname}

Restituisce il nome dell&#39;archivio sessione.

**Parametri**

Nessuno.

**Restituisce**

Valore String che rappresenta il nome dell&#39;archivio.

#### getProperty(name, raw) {#getproperty-name-raw}

Restituisce il valore di una proprietà. Il valore viene restituito come proprietà non elaborata o come valore filtrato da XSS. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: String. Nome della proprietà dati da recuperare.
* raw: booleano. Se si imposta il valore true, viene restituito il valore della proprietà raw. Se si imposta il valore false, il valore restituito viene filtrato in base al valore XSS.

**Restituisce**

Valore della proprietà dati.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Restituisce i nomi delle proprietà contenute nell&#39;archivio delle sessioni. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

excluded: (facoltativo) array di nomi di proprietà da omettere dai risultati.

**Restituisce**

Matrice di valori String che rappresentano i nomi delle proprietà di sessione.

#### getSessionStore() {#getsessionstore}

Restituisce l&#39;archivio di sessione associato all&#39;oggetto corrente.

**Parametri**

Nessuno.

**Restituisce**

questo

#### init() {#init-1}

Contrassegna l&#39;archivio come inizializzato e attiva `initialize` evento.

**Parametri**

Nessuno.

**Restituisce**

Nessun valore restituito.

#### isInitialized() {#isinitialized}

Indica se l&#39;archivio sessioni è inizializzato.

**Parametri**

Nessuno.

**Restituisce**

Un valore di `true` se l’archivio è inizializzato e un valore di `false` se l’archivio non è inizializzato.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Aggiunge le proprietà di un determinato oggetto ai dati di inizializzazione dell&#39;archivio sessione. Facoltativamente, i dati oggetto vengono aggiunti anche ai dati dell&#39;archivio.

**Parametri**

* obj: oggetto contenente proprietà enumerabili.
* setValues: se è true, le proprietà obj vengono aggiunte ai dati dell&#39;archivio di sessione se i dati dell&#39;archivio non includono già una proprietà con lo stesso nome. Se è false, nessun dato viene aggiunto ai dati dell’archivio sessione.

**Restituisce**

Nessun valore restituito.

#### removeProperty(name) {#removeproperty-name}

Rimuove una proprietà dall&#39;archivio della sessione. Attiva il `update` al completamento. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: String. Nome della proprietà da rimuovere.

**Restituisce**

Nessun valore restituito.

#### ripristina() {#reset}

Ripristina i valori iniziali dell&#39;archivio dati. L’implementazione predefinita rimuove semplicemente tutti i dati. Attiva il `update` al completamento.

**Parametri**

Nessuno.

**Restituisce**

Nessun valore restituito.

#### setProperties(properties) {#setproperties-properties}

Imposta i valori di più proprietà. Attiva il `update` al completamento. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* Proprietà: oggetto. Oggetto contenente proprietà enumerabili. Ogni nome e valore di proprietà viene aggiunto all’archivio.

**Restituisce**

Nessun valore restituito.

#### setProperty(name, value) {#setproperty-name-value}

Imposta il valore di una proprietà. Attiva il `update` al completamento. Chiama il `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: String. Nome della proprietà.
* value: String. Valore proprietà.

**Restituisce**

Nessun valore restituito.
