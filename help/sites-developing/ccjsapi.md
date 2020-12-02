---
title: API JavaScript ClientContext
seo-title: API JavaScript ClientContext
description: API Javascript per ClientContext
seo-description: API Javascript per ClientContext
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 4%

---


# API JavaScript ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

L&#39;oggetto CQ_Analytics.ClientContextMgr è un singleton che contiene un set di store di sessioni autoregistrati e fornisce metodi per la registrazione, la persistenza e la gestione degli store di sessioni.

Estende CQ_Analytics.PersistedSessionStore.

### Metodi {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Restituisce un archivio di sessione con un nome specificato. Vedere anche [Accesso a uno store di sessione](/help/sites-developing/client-context.md#accessing-session-stores).

**Parametri**

* name: Stringa. Nome dello store di sessioni.

**Valore restituito**

Un oggetto CQ_Analytics.SessionStore che rappresenta lo store di sessioni del nome specificato. Restituisce `null` se non esiste alcun archivio del nome specificato.

#### register(sessionstore) {#register-sessionstore}

Registra uno store di sessione con ClientContext. Attiva gli eventi storeregister e storeupdate al termine.

**Parametri**

* sessionstore: CQ_Analytics.SessionStore. L&#39;oggetto session store da registrare.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornisce metodi per ascoltare l&#39;attivazione e la registrazione dell&#39;archivio sessioni. Vedere anche [Controllo della definizione e inizializzazione di uno store di sessioni](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Metodi {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una funzione di callback che viene chiamata quando viene inizializzato uno store di sessioni. Per gli store che sono inizializzati più volte, specificate un ritardo di callback in modo che la funzione di callback venga chiamata una sola volta:

* Quando lo store viene inizializzato durante il periodo di ritardo di un&#39;inizializzazione precedente, la chiamata della funzione precedente viene annullata e la funzione viene richiamata di nuovo per l&#39;inizializzazione corrente.
* Se il periodo di ritardo scade prima di una successiva inizializzazione, la funzione di callback viene eseguita due volte.

Ad esempio, uno store di sessione si basa su un oggetto JSON e viene recuperato tramite una richiesta JSON. Sono possibili i seguenti scenari di inizializzazione:

* La richiesta è completata, i dati recuperati e caricati nello store. In questo caso, l&#39;inizializzazione viene eseguita una volta.
* La richiesta non riesce (timeout). In questo caso l&#39;inizializzazione non viene eseguita e non sono presenti dati nello store.
* Lo store è precompilato con valori predefiniti (proprietà init), ma la richiesta non riesce (timeout). Esiste una sola inizializzazione con valori predefiniti.
* Il negozio è precompilato.

Quando il ritardo è impostato su `true` o su un numero di millisecondi, il metodo attende prima di richiamare il metodo di callback. Se viene attivato un altro evento di inizializzazione prima del superamento del ritardo, quest&#39;ultimo aspetterà che venga superato il tempo di ritardo senza che si verifichi alcun evento di inizializzazione. Questo consente di attivare un secondo evento di inizializzazione e richiama la funzione di callback nel caso più ottimale.

**Parametri**

* storeName: Stringa. Il nome dell&#39;archivio delle sessioni da cui aggiungere il listener.
* callback: Funzione. La funzione da invocare all&#39;inizializzazione dello store.
* ritardo: Booleano o Numero. Tempo in millisecondi per il ritardo della chiamata alla funzione di callback. Un valore booleano di `true` utilizza il ritardo predefinito di `200 ms`. Un valore booleano di `false` o un numero negativo non causa alcun ritardo.

**Valore restituito**

Nessun valore restituito.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una funzione di callback che viene chiamata quando viene registrato uno store di sessioni. L&#39;evento di registro si verifica quando uno store viene registrato in [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parametri**

* storeName: Stringa. Il nome dell&#39;archivio delle sessioni da cui aggiungere il listener.
* callback: Funzione. La funzione da invocare all&#39;inizializzazione dello store.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Un archivio di sessioni non persistente che contiene dati JSON. I dati vengono recuperati da un servizio JSONP esterno. Utilizzare il metodo `getInstance` o `getRegisteredInstance` per creare un&#39;istanza di questa classe.

Estende CQ_Analytics.JSONStore.

### Proprietà {#properties}

Per informazioni sulle proprietà ereditate, consultate CQ_Analytics.JSONStore e CQ_Analytics.SessonStore.

### Metodi {#methods-2}

Consulta anche CQ_Analytics.JSONStore e CQ_Analytics.SessonStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, afterLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un oggetto CQ_Analytics.JSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: Stringa. URL del servizio JSONP
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* deferLoading: (Facoltativo) Valore Boolean. Il valore true impedisce il richiamo del servizio JSONP alla creazione di oggetti. Se si imposta il valore false, viene chiamato il servizio JSONP.
* loadingCallback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Il nuovo oggetto CQ_Analytics.JSONPStore o null se storeName è nullo.

#### getServiceURL() {#getserviceurl}

Recupera l&#39;URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Valore restituito**

Stringa che rappresenta l&#39;URL del servizio, oppure null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Chiama il servizio JSONP. L’URL JSONP è l’URL del servizio con suffisso con il nome della funzione di callback di ritorno.

**Parametri**

* serviceURL: (Facoltativo) Stringa. Il servizio JSONP da chiamare. Se si imposta il valore null, verrà utilizzato l&#39;URL del servizio già configurato. Un valore non nullo imposta il servizio JSONP da utilizzare per questo oggetto. Consultate setServiceURL.
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un oggetto CQ_Analytics.JSONPStore e registra lo store con ClientContext.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: (Facoltativo) Stringa. URL del servizio JSONP.
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Imposta l&#39;URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: Stringa. L&#39;URL del servizio JSONP che fornisce dati JSON

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Contenitore per un oggetto JSON. Create un&#39;istanza di questa classe per creare un archivio di sessioni non persistente che contenga dati JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

È possibile definire un set di dati che compili lo store al momento dell&#39;inizializzazione.

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-1}

#### STOREKEY {#storekey}

Chiave che identifica lo store. Utilizzare il metodo `getInstance` per recuperare questo valore.

#### STORENAME {#storename}

Il nome dello store. Utilizzare il metodo `getInstance` per recuperare questo valore.

### Metodi {#methods-3}

Consulta anche CQ_Analytics.SessionStore per i metodi ereditati.

#### cancella() {#clear}

Rimuove i dati dell&#39;archivio sessioni e rimuove tutte le proprietà di inizializzazione.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e viene inizializzato con i dati JSON specificati (chiama il metodo initJSON).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Object. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera i dati dell&#39;archivio delle sessioni in formato JSON.

**Parametri**

Nessuno.

**Valore restituito**

Un oggetto che rappresenta i dati dell&#39;archivio in formato JSON.

#### init() {#init}

Cancella l&#39;archivio delle sessioni e lo inizializza con la proprietà di inizializzazione. Imposta il flag di inizializzazione su `true`, quindi attiva gli eventi `initialize` e `update`.

**Parametri**

Nessuno.

**Valore restituito**

Nessun dato restituito.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crea proprietà di inizializzazione dai dati in un oggetto JSON. Facoltativamente, potete rimuovere tutte le proprietà di inizializzazione esistenti.

I nomi delle proprietà sono derivati dalla gerarchia dei dati nell&#39;oggetto JSON. Il seguente codice di esempio rappresenta un oggetto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Per questo esempio, nello store vengono create le seguenti proprietà:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: Un oggetto JSON che contiene i dati da memorizzare.
* doNotClear: Il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall&#39;oggetto JSON.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e viene inizializzato con i dati JSON specificati (chiama il metodo initJSON). Il nuovo oggetto viene registrato automaticamente con Clickstream Cloud Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Object. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONStore.

## CQ_Analytics.Osservabile {#cq-analytics-observable}

Attiva eventi e consente ad altri oggetti di ascoltare tali eventi e reagire. Le classi che estendono questa classe possono attivare eventi che causano la chiamata dei listener.

### Metodi {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra un listener per un evento. Vedere anche [Creazione di un listener per reagire a un aggiornamento dello store di sessioni](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parametri**

* event: Stringa. Il nome dell’evento da ascoltare.
* fct: Funzione. La funzione che viene chiamata quando si verifica l&#39;evento.
* ambito: (Facoltativo) Object. Ambito in cui eseguire la funzione del gestore. Contesto &quot;this&quot; della funzione gestore.

**Valore restituito**

Nessun valore restituito.

#### removeListener(event, fct) {#removelistener-event-fct}

Rimuove il gestore eventi specificato per un evento.

**Parametri**

* event: Stringa. Il nome dell’evento.
* fct: Funzione. Il gestore eventi.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Contenitore persistente di un oggetto JSON recuperato da un servizio JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Metodi {#methods-5}

Consulta anche CQ_Analytics.PersistedJSONStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, afterLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: Stringa. URL del servizio JSONP
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* deferLoading: (Facoltativo) Valore Boolean. Il valore true impedisce il richiamo del servizio JSONP alla creazione di oggetti. Se si imposta il valore false, viene chiamato il servizio JSONP.
* loadingCallback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Il nuovo oggetto CQ_Analytics.PersistedJSONPStore o null se storeName è null.

#### getServiceURL() {#getserviceurl-1}

Recupera l&#39;URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Valore restituito**

Stringa che rappresenta l&#39;URL del servizio, oppure null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Chiama il servizio JSONP. L’URL JSONP è l’URL del servizio con suffisso con il nome della funzione di callback di ritorno.

**Parametri**

* serviceURL: (Facoltativo) Stringa. Il servizio JSONP da chiamare. Se si imposta il valore null, verrà utilizzato l&#39;URL del servizio già configurato. Un valore non nullo imposta il servizio JSONP da utilizzare per questo oggetto. Consultate setServiceURL.
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore e registra lo store con ClientContext.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: (Facoltativo) Stringa. URL del servizio JSONP.
* dynamicData: (Facoltativo) Object. I dati JSON da aggiungere ai dati di inizializzazione dello store prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Il nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che sia un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Imposta l&#39;URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: Stringa. L&#39;URL del servizio JSONP che fornisce dati JSON

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Contenitore persistente di un oggetto JSON.

Estende `CQ_Analytics.PersistedSessionStore`.

### Proprietà {#properties-2}

#### STOREKEY {#storekey-1}

Chiave che identifica lo store. Utilizzare il metodo `getInstance` per recuperare questo valore.

#### STORENAME {#storename-1}

Il nome dello store. Utilizzare il metodo `getInstance` per recuperare questo valore.

### Metodi {#methods-6}

Consulta anche CQ_Analytics.PersistedSessionStore per i metodi ereditati.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e viene inizializzato con i dati JSON specificati (chiama il metodo initJSON).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Object. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera i dati dell&#39;archivio delle sessioni in formato JSON.

**Parametri**

Nessuno.

**Valore restituito**

Un oggetto che rappresenta i dati dell&#39;archivio in formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crea proprietà di inizializzazione dai dati in un oggetto JSON. Facoltativamente, potete rimuovere tutte le proprietà di inizializzazione esistenti.

I nomi delle proprietà sono derivati dalla gerarchia dei dati nell&#39;oggetto JSON. Il seguente codice di esempio rappresenta un oggetto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Per questo esempio, nello store vengono create le seguenti proprietà:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: Un oggetto JSON che contiene i dati da memorizzare.
* doNotClear: Il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall&#39;oggetto JSON.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e viene inizializzato con i dati JSON specificati (chiama il metodo initJSON). Il nuovo oggetto viene registrato automaticamente con Client Context Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Object. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Contenitore di proprietà e valori. I dati vengono memorizzati utilizzando CQ_Analytics.SessionPersistenza. Create un&#39;istanza di questa classe per creare uno store di sessioni persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-3}

#### STOREKEY {#storekey-2}

Il valore predefinito è `key`.

### Metodi {#methods-7}

Consulta CQ_Analytics.SessionStore per i metodi ereditati.

Quando i metodi ereditati `clear`, `setProperty`, `setProperties`, `removeProperty` vengono utilizzati per modificare i dati dello store, le modifiche vengono mantenute automaticamente, a meno che le proprietà modificate non siano contrassegnate come non persistenti.

#### getStoreKey() {#getstorekey}

Recupera la proprietà `STOREKEY`.

**Parametri**

Nessuno

**Valore restituito**

Il valore della proprietà `STOREKEY`.

#### isPersisted(name) {#ispersisted-name}

Determina se una proprietà dati è persistente.

**Parametri**

* name: Stringa. Nome della proprietà.

**Valore restituito**

Un valore booleano di `true` se la proprietà è persistente e un valore di `false` se il valore non è una proprietà persistente.

#### persist() {#persist}

Persiste lo store sessione. La modalità di persistenza predefinita utilizza il browser `localStorage` utilizzando `ClientSidePersistence` come nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage non è disponibile o scrivibile, lo store viene mantenuto come proprietà della finestra.

Attiva l&#39;evento `persist` al termine.

**Parametri**

Nessuno

**Valore restituito**

Nessun valore restituito.

#### reset(deferEvent) {#reset-deferevent}

Rimuove tutte le proprietà dei dati dall&#39;archivio e persiste nell&#39;archivio. Facoltativamente, non attiva l&#39;evento `udpate` al termine.

**Parametri**

* deferEvent: Il valore true impedisce l&#39;attivazione dell&#39;evento `update`. Un valore di `false` attiva l&#39;evento update.

**Valore restituito**

Nessun valore restituito.

#### setNonPersisted(name) {#setnonpersisted-name}

Contrassegna una proprietà dati come non persistente.

**Parametri**

* name: Stringa. Il nome della proprietà che non deve essere persistente.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore rappresenta uno store di sessioni. Create un&#39;istanza di questa classe per creare uno store di sessioni:

`mystore = new CQ_Analytics.SessionStore`

Estende CQ_Analytics.Observable.

### Proprietà {#properties-4}

#### STORENAME {#storename-2}

Nome dello store di sessioni. Utilizzare getName per recuperare il valore di questa proprietà.

### Metodi {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Aggiunge una proprietà e un valore ai dati di inizializzazione dell&#39;archivio di sessione.

Utilizzare loadInitProperties per compilare i dati dell&#39;archivio di sessione con i valori di inizializzazione.

**Parametri**

* name: Stringa. Nome della proprietà da aggiungere.
* value: Stringa. Il valore della proprietà da aggiungere.

**Valore restituito**

Nessun valore restituito.

#### cancella() {#clear-1}

Rimuove tutte le proprietà dei dati dall&#39;archivio.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### getData(escluso) {#getdata-excluded}

Restituisce i dati dell&#39;archivio. Facoltativamente, esclude le proprietà del nome dai dati. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

escluso: (Facoltativo) Un array di nomi di proprietà da escludere dai dati restituiti.

**Valore restituito**

Un oggetto di proprietà e relativi valori.

#### getInitProperty(name) {#getinitproperty-name}

Recupera il valore di una proprietà data.

**Parametri**

* name: Stringa. Nome della proprietà data da recuperare.

**Valore restituito**

Il valore della proprietà data. Restituisce `null` se l&#39;archivio delle sessioni non contiene alcuna proprietà del nome specificato.

#### getName() {#getname}

Restituisce il nome dell’archivio delle sessioni.

**Parametri**

Nessuno.

**Valore restituito**

Un valore String che rappresenta il nome dell&#39;archivio.

#### getProperty(name, raw) {#getproperty-name-raw}

Restituisce il valore di una proprietà. Il valore viene restituito come proprietà raw o come valore filtrato XSS. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: Stringa. Nome della proprietà data da recuperare.
* raw: Boolean. Se si imposta il valore true, viene restituito il valore della proprietà raw. Se si imposta false, il valore restituito verrà filtrato in XSS.

**Valore restituito**

Il valore della proprietà data.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Restituisce i nomi delle proprietà contenute nell&#39;archivio delle sessioni. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

escluso: (Facoltativo) Un array di nomi di proprietà da omettere dai risultati.

**Valore restituito**

Un array di valori String che rappresentano i nomi delle proprietà session.

#### getSessionStore() {#getsessionstore}

Restituisce lo store sessione associato all&#39;oggetto corrente.

**Parametri**

Nessuno.

**Valore restituito**

this

#### init() {#init-1}

Contrassegna lo store come inizializzato e attiva l&#39;evento `initialize`.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### isInitialized() {#isinitialized}

Indica se l&#39;archivio delle sessioni è inizializzato.

**Parametri**

Nessuno.

**Valore restituito**

Un valore di `true` se lo store viene inizializzato e un valore di `false` se lo store non è inizializzato.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Aggiunge le proprietà di un dato oggetto ai dati di inizializzazione dell&#39;archivio delle sessioni. Facoltativamente, i dati dell&#39;oggetto vengono aggiunti anche ai dati dello store.

**Parametri**

* obj: Un oggetto che contiene proprietà enumerabili.
* setValues: Se true, le proprietà obj vengono aggiunte ai dati dell&#39;archivio sessioni se i dati dell&#39;archivio non includono già una proprietà con lo stesso nome. Se è false, non vengono aggiunti dati all&#39;archivio delle sessioni.

**Valore restituito**

Nessun valore restituito.

#### removeProperty(name) {#removeproperty-name}

Rimuove una proprietà dall&#39;archivio delle sessioni. Attiva l&#39;evento `update` al termine. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: Stringa. Nome della proprietà da rimuovere.

**Valore restituito**

Nessun valore restituito.

#### reset() {#reset}

Ripristina i valori iniziali dell&#39;archivio dati. L’implementazione predefinita rimuove semplicemente tutti i dati. Attiva l&#39;evento `update` al termine.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### setProperties(properties) {#setproperties-properties}

Imposta i valori di più proprietà. Attiva l&#39;evento `update` al termine. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* Proprietà: Object. Un oggetto che contiene proprietà enumerabili. Ogni nome e valore di proprietà viene aggiunto allo store.

**Valore restituito**

Nessun valore restituito.

#### setProperty(name, value) {#setproperty-name-value}

Imposta il valore di una proprietà. Attiva l&#39;evento `update` al termine. Chiama il metodo `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* name: Stringa. Nome della proprietà.
* value: Stringa. Valore proprietà.

**Valore restituito**

Nessun valore restituito.
