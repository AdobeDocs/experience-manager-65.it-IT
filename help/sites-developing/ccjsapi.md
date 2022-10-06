---
title: API JavaScript per il contesto client
seo-title: Client Context Javascript API
description: API JavaScript per il contesto client
seo-description: The Javascript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3153'
ht-degree: 4%

---

# API JavaScript per il contesto client{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

L&#39;oggetto CQ_Analytics.ClientContextMgr è un singleton che contiene un set di archivi di sessione registrati automaticamente e fornisce metodi per la registrazione, la persistenza e la gestione degli archivi di sessione.

Estende CQ_Analytics.PersistedSessionStore.

### Metodi {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Restituisce un archivio di sessione con un nome specificato. Vedi anche [Accesso a un archivio sessioni](/help/sites-developing/client-context.md#accessing-session-stores).

**Parametri**

* nome: Stringa. Nome dell&#39;archivio sessioni.

**Valore restituito**

Un oggetto CQ_Analytics.SessionStore che rappresenta l&#39;archivio delle sessioni del nome specificato. Restituisce `null` quando non esiste un archivio del nome specificato.

#### register(sessionstore) {#register-sessionstore}

Registra un archivio sessioni con ClientContext. Attiva gli eventi di registrazione e aggiornamento dello storage al termine del processo.

**Parametri**

* sessionstore: CQ_Analytics.SessionStore. Oggetto dell&#39;archivio sessioni da registrare.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornisce metodi per ascoltare l&#39;attivazione e la registrazione dell&#39;archivio sessioni. Vedi anche [Controllo della definizione e dell&#39;inizializzazione di un archivio sessioni](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Metodi {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Registra una funzione di callback chiamata quando viene inizializzato un archivio di sessione. Per gli archivi inizializzati più volte, specifica un ritardo di callback in modo che la funzione di callback venga chiamata una sola volta:

* Quando l&#39;archivio viene inizializzato durante il periodo di ritardo di un&#39;inizializzazione precedente, la chiamata della funzione precedente viene annullata e la funzione viene richiamata nuovamente per l&#39;inizializzazione corrente.
* Se il periodo di ritardo scade prima di un&#39;inizializzazione successiva, la funzione di callback viene eseguita due volte.

Ad esempio, un archivio sessioni si basa su un oggetto JSON e viene recuperato tramite una richiesta JSON. Sono possibili i seguenti scenari di inizializzazione:

* La richiesta viene completata, i dati recuperati e caricati nell&#39;archivio. In questo caso, l&#39;inizializzazione viene eseguita una volta.
* La richiesta non riesce (timeout). In questo caso l&#39;inizializzazione non viene eseguita e non sono presenti dati nell&#39;archivio.
* L’archivio è precompilato con valori predefiniti (proprietà init), ma la richiesta non riesce (timeout). Esiste una sola inizializzazione con valori predefiniti.
* Lo store è prepopolato.

Quando il ritardo è impostato su `true` Per un numero di millisecondi, il metodo attende prima di richiamare il metodo di callback. Se un altro evento di inizializzazione viene attivato prima del passaggio del ritardo, attenderà che venga superato il tempo di ritardo senza alcun evento di inizializzazione. Questo consente di attendere l&#39;attivazione di un secondo evento di inizializzazione e chiama la funzione di callback nel caso più ottimale.

**Parametri**

* storeName: Stringa. Nome dell&#39;archivio sessioni da aggiungere al listener.
* callback: Funzione. La funzione da chiamare all&#39;inizializzazione dello store.
* ritardo: Valore booleano o numerico. Il tempo in millisecondi impiegato per ritardare la chiamata alla funzione di callback. Un valore booleano di `true` utilizza il ritardo predefinito di `200 ms`. Un valore booleano di `false` o un numero negativo non causa alcun ritardo.

**Valore restituito**

Nessun valore restituito.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Registra una funzione di callback chiamata quando viene registrato un archivio di sessione. L&#39;evento di registrazione si verifica quando un negozio viene registrato in [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parametri**

* storeName: Stringa. Nome dell&#39;archivio sessioni da aggiungere al listener.
* callback: Funzione. La funzione da chiamare all&#39;inizializzazione dello store.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Archivio di sessione non persistente contenente dati JSON. I dati vengono recuperati da un servizio JSONP esterno. Utilizza la `getInstance` o `getRegisteredInstance` per creare un&#39;istanza di questa classe.

Estende CQ_Analytics.JSONStore.

### Proprietà {#properties}

Per le proprietà ereditate, consulta CQ_Analytics.JSONStore e CQ_Analytics.SessonStore .

### Metodi {#methods-2}

Consulta anche CQ_Analytics.JSONStore e CQ_Analytics.SessonStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crea un oggetto CQ_Analytics.JSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: Stringa. URL del servizio JSONP
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* deferLoading: (Facoltativo) Booleano. Il valore true impedisce la chiamata del servizio JSONP alla creazione di oggetti. Se si imposta il valore false, viene richiamato il servizio JSONP.
* loadingCallback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Il nuovo oggetto CQ_Analytics.JSONPStore o null se storeName è null.

#### getServiceURL() {#getserviceurl}

Recupera l’URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Valore restituito**

Stringa che rappresenta l&#39;URL del servizio o null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Chiama il servizio JSONP. L&#39;URL JSONP è l&#39;URL del servizio con suffisso con un nome della funzione di callback di ritorno.

**Parametri**

* serviceURL: (Facoltativo) Stringa. Il servizio JSONP da chiamare. Se si imposta il valore null, verrà utilizzato l&#39;URL di servizio già configurato. Un valore non nullo imposta il servizio JSONP da utilizzare per questo oggetto. (Vedi setServiceURL.)
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crea un oggetto CQ_Analytics.JSONPStore e registra l&#39;archivio con Client Context.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: (Facoltativo) Stringa. URL del servizio JSONP.
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Imposta l’URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: Stringa. URL del servizio JSONP che fornisce dati JSON

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Un contenitore per un oggetto JSON. Crea un&#39;istanza di questa classe per creare un archivio di sessione non persistente che contiene dati JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Puoi definire un set di dati che popola l&#39;archivio al momento dell&#39;inizializzazione.

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-1}

#### STOREKEY {#storekey}

Chiave che identifica lo store. Utilizza la `getInstance` per recuperare questo valore.

#### STORENAME {#storename}

Nome del negozio. Utilizza la `getInstance` per recuperare questo valore.

### Metodi {#methods-3}

Consulta anche CQ_Analytics.SessionStore per i metodi ereditati.

#### cancella() {#clear}

Rimuove i dati dell’archivio sessioni e rimuove tutte le proprietà di inizializzazione.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON ).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Oggetto. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera i dati della sessione archiviata in formato JSON.

**Parametri**

Nessuno.

**Valore restituito**

Un oggetto che rappresenta i dati archiviati in formato JSON.

#### init() {#init}

Cancella l&#39;archivio delle sessioni e lo inizializza con la proprietà di inizializzazione. Imposta il flag di inizializzazione su `true` e poi attiva il pulsante `initialize` e `update` eventi.

**Parametri**

Nessuno.

**Valore restituito**

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

Per questo esempio, nell&#39;archivio vengono create le seguenti proprietà:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: Un oggetto JSON contenente i dati da memorizzare.
* doNotClear: Il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall&#39;oggetto JSON.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crea un oggetto CQ_Analytics.JSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON ). Il nuovo oggetto viene registrato automaticamente con Clickstream Cloud Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Oggetto. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Attiva eventi e consente ad altri oggetti di ascoltare questi eventi e reagire. Le classi che estendono questa classe possono attivare eventi che causano la chiamata di listener.

### Metodi {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra un listener per un evento. Vedi anche [Creazione di un listener per reagire a un aggiornamento dell&#39;archivio sessioni](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parametri**

* evento: Stringa. Nome dell&#39;evento da ascoltare.
* fct: Funzione. La funzione che viene chiamata quando si verifica l&#39;evento.
* ambito di applicazione: (Facoltativo) Oggetto. Ambito in cui eseguire la funzione del gestore. Il contesto &quot;this&quot; della funzione di gestione.

**Valore restituito**

Nessun valore restituito.

#### removeListener(event, fct) {#removelistener-event-fct}

Rimuove il gestore eventi specificato per un evento.

**Parametri**

* evento: Stringa. Nome dell&#39;evento.
* fct: Funzione. Il gestore eventi.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Contenitore persistente di un oggetto JSON recuperato da un servizio JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Metodi {#methods-5}

Consulta anche CQ_Analytics.PersistedJSONStore per i metodi ereditati.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: Stringa. URL del servizio JSONP
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* deferLoading: (Facoltativo) Booleano. Il valore true impedisce la chiamata del servizio JSONP alla creazione di oggetti. Se si imposta il valore false, viene richiamato il servizio JSONP.
* loadingCallback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Il nuovo oggetto CQ_Analytics.PersistedJSONPStore o null se storeName è null.

#### getServiceURL() {#getserviceurl-1}

Recupera l’URL del servizio JSONP utilizzato da questo oggetto per recuperare i dati JSON.

**Parametri**

Nessuno.

**Valore restituito**

Stringa che rappresenta l&#39;URL del servizio o null se non è stato configurato alcun URL del servizio.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Chiama il servizio JSONP. L&#39;URL JSONP è l&#39;URL del servizio con suffisso con un nome della funzione di callback di ritorno.

**Parametri**

* serviceURL: (Facoltativo) Stringa. Il servizio JSONP da chiamare. Se si imposta il valore null, verrà utilizzato l&#39;URL di servizio già configurato. Un valore non nullo imposta il servizio JSONP da utilizzare per questo oggetto. (Vedi setServiceURL.)
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crea un oggetto CQ_Analytics.PersistedJSONPStore e registra l&#39;archivio con Client Context.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli. Se non viene fornito alcun valore storeName, il metodo restituisce null.
* serviceURL: (Facoltativo) Stringa. URL del servizio JSONP.
* dynamicData: (Facoltativo) Oggetto. Dati JSON da aggiungere ai dati di inizializzazione dell&#39;archivio prima della chiamata della funzione di callback.
* callback: (Facoltativo) Stringa. Nome della funzione da chiamare per l&#39;elaborazione dell&#39;oggetto JSONP restituito dal servizio JSONP. La funzione di callback deve definire un singolo parametro che è un oggetto CQ_Analytics.JSONPStore.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONPStore registrato.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Imposta l’URL del servizio JSONP da utilizzare per il recupero dei dati JSON.

**Parametri**

* serviceURL: Stringa. URL del servizio JSONP che fornisce dati JSON

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Contenitore persistente di un oggetto JSON.

Estensioni `CQ_Analytics.PersistedSessionStore`.

### Proprietà {#properties-2}

#### STOREKEY {#storekey-1}

Chiave che identifica lo store. Utilizza la `getInstance` per recuperare questo valore.

#### STORENAME {#storename-1}

Nome del negozio. Utilizza la `getInstance` per recuperare questo valore.

### Metodi {#methods-6}

Consulta anche CQ_Analytics.PersistedSessionStore per i metodi ereditati.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON ).

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Oggetto. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera i dati della sessione archiviata in formato JSON.

**Parametri**

Nessuno.

**Valore restituito**

Un oggetto che rappresenta i dati archiviati in formato JSON.

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

Per questo esempio, nell&#39;archivio vengono create le seguenti proprietà:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parametri**

* jsonData: Un oggetto JSON contenente i dati da memorizzare.
* doNotClear: Il valore true mantiene le proprietà di inizializzazione esistenti e aggiunge quelle derivate dall&#39;oggetto JSON. Il valore false rimuove le proprietà di inizializzazione esistenti prima di aggiungere quelle derivate dall&#39;oggetto JSON.

**Valore restituito**

Nessun valore restituito.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crea un oggetto CQ_Analytics.PersistedJSONStore con un nome specificato e inizializzato con i dati JSON specificati (chiama il metodo initJSON ). Il nuovo oggetto viene registrato automaticamente con Client Context Manager.

**Parametri**

* storeName: Stringa. Nome da utilizzare come proprietà STORENAME. Il valore della proprietà STOREKEY è impostato su storeName con tutti i caratteri maiuscoli.
* jsonData: Oggetto. Un oggetto che contiene dati JSON.

**Valore restituito**

L&#39;oggetto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Contenitore di proprietà e valori. I dati vengono memorizzati utilizzando CQ_Analytics.SessionPersistence. Crea un&#39;istanza di questa classe per creare un archivio di sessione persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Proprietà {#properties-3}

#### STOREKEY {#storekey-2}

Il valore predefinito è `key`.

### Metodi {#methods-7}

Per i metodi ereditati, consulta CQ_Analytics.SessionStore .

Quando i metodi ereditati `clear`, `setProperty`, `setProperties`, `removeProperty` vengono utilizzate per modificare i dati dell&#39;archivio, le modifiche vengono mantenute automaticamente, a meno che le proprietà modificate non siano contrassegnate come nonPersisted.

#### getStoreKey() {#getstorekey}

Recupera la `STOREKEY` proprietà.

**Parametri**

Nessuno

**Valore restituito**

Il valore del `STOREKEY` proprietà.

#### isPersisted(name) {#ispersisted-name}

Determina se una proprietà dati è persistente.

**Parametri**

* nome: Stringa. Nome della proprietà.

**Valore restituito**

Un valore booleano di `true` se la proprietà è persistente e un valore di `false` se il valore non è una proprietà persistente.

#### persist() {#persist}

Persiste l&#39;archivio delle sessioni. La modalità di persistenza predefinita utilizza il browser `localStorage` utilizzo `ClientSidePersistence` come nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage non è disponibile o scrivibile, l&#39;archivio viene mantenuto come proprietà della finestra.

Attiva la `persist` evento al termine.

**Parametri**

Nessuno

**Valore restituito**

Nessun valore restituito.

#### reset(deferEvent) {#reset-deferevent}

Rimuove tutte le proprietà dei dati dall’archivio e persiste l’archivio. Facoltativamente non attiva il `udpate` evento al termine.

**Parametri**

* deferEvent: Il valore true impedisce la `update` dell&#39;attivazione. Un valore di `false` causa l&#39;attivazione dell&#39;evento di aggiornamento.

**Valore restituito**

Nessun valore restituito.

#### setNonPersisted(name) {#setnonpersisted-name}

Contrassegna una proprietà dati come non persistente.

**Parametri**

* nome: Stringa. Nome della proprietà che non deve essere persistente.

**Valore restituito**

Nessun valore restituito.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore rappresenta un archivio di sessioni. Crea un&#39;istanza di questa classe per creare un archivio sessioni:

`mystore = new CQ_Analytics.SessionStore`

Estende CQ_Analytics.Observable.

### Proprietà {#properties-4}

#### STORENAME {#storename-2}

Nome dell&#39;archivio sessioni. Utilizzare getName per recuperare il valore di questa proprietà.

### Metodi {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Aggiunge una proprietà e un valore ai dati di inizializzazione dell&#39;archivio sessioni.

Utilizza loadInitProperties per popolare i dati dell&#39;archivio sessioni con i valori di inizializzazione.

**Parametri**

* nome: Stringa. Nome della proprietà da aggiungere.
* valore: Stringa. Il valore della proprietà da aggiungere.

**Valore restituito**

Nessun valore restituito.

#### cancella() {#clear-1}

Rimuove tutte le proprietà dei dati dall’archivio.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### getData(excluded) {#getdata-excluded}

Restituisce i dati dell&#39;archivio. Facoltativamente, esclude le proprietà del nome dai dati. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

esclusi: (Facoltativo) Matrice di nomi di proprietà da escludere dai dati restituiti.

**Valore restituito**

Oggetto di proprietà e relativi valori.

#### getInitProperty(name) {#getinitproperty-name}

Recupera il valore di una proprietà dati.

**Parametri**

* nome: Stringa. Nome della proprietà dati da recuperare.

**Valore restituito**

Il valore della proprietà data. Restituzioni `null` se l&#39;archivio sessioni non contiene proprietà del nome specificato.

#### getName() {#getname}

Restituisce il nome dell&#39;archivio sessioni.

**Parametri**

Nessuno.

**Valore restituito**

Valore String che rappresenta il nome dell&#39;archivio.

#### getProperty(name, raw) {#getproperty-name-raw}

Restituisce il valore di una proprietà. Il valore viene restituito come proprietà non elaborata o come valore filtrato XSS. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* nome: Stringa. Nome della proprietà dati da recuperare.
* grezzo: Booleano. Se il valore è true, viene restituito il valore della proprietà non elaborata. Se si imposta il valore false, il valore restituito verrà filtrato tramite XSS.

**Valore restituito**

Il valore della proprietà data.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Restituisce i nomi delle proprietà contenute nell&#39;archivio sessioni. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

esclusi: (Facoltativo) Matrice di nomi di proprietà da omettere dai risultati.

**Valore restituito**

Matrice di valori String che rappresenta i nomi delle proprietà di sessione.

#### getSessionStore() {#getsessionstore}

Restituisce l&#39;archivio sessioni associato all&#39;oggetto corrente.

**Parametri**

Nessuno.

**Valore restituito**

this

#### init() {#init-1}

Segna l&#39;archivio come inizializzato e attiva il `initialize` evento.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### isInitialized() {#isinitialized}

Indica se l&#39;archivio delle sessioni è inizializzato.

**Parametri**

Nessuno.

**Valore restituito**

Un valore di `true` se l&#39;archivio è inizializzato e un valore di `false` se l&#39;archivio non è inizializzato.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Aggiunge le proprietà di un oggetto specificato ai dati di inizializzazione dell&#39;archivio sessioni. Facoltativamente, i dati dell’oggetto vengono aggiunti anche ai dati dell’archivio.

**Parametri**

* obj: Oggetto che contiene proprietà enumerabili.
* setValues: Se true, le proprietà obj vengono aggiunte ai dati dell&#39;archivio sessioni se i dati dell&#39;archivio non includono già una proprietà con lo stesso nome. Se false, non vengono aggiunti dati ai dati dell&#39;archivio sessioni.

**Valore restituito**

Nessun valore restituito.

#### removeProperty(name) {#removeproperty-name}

Rimuove una proprietà dall’archivio sessioni. Attiva la `update` evento al termine. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* nome: Stringa. Nome della proprietà da rimuovere.

**Valore restituito**

Nessun valore restituito.

#### reset() {#reset}

Ripristina i valori iniziali dell’archivio dati. L’implementazione predefinita rimuove semplicemente tutti i dati. Attiva la `update` evento al termine.

**Parametri**

Nessuno.

**Valore restituito**

Nessun valore restituito.

#### setProperties(properties) {#setproperties-properties}

Imposta i valori di più proprietà. Attiva la `update` evento al termine. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* Proprietà: Oggetto. Un oggetto che contiene proprietà enumerabili. Ogni nome e valore della proprietà viene aggiunto all&#39;archivio.

**Valore restituito**

Nessun valore restituito.

#### setProperty(name, value) {#setproperty-name-value}

Imposta il valore di una proprietà. Attiva la `update` evento al termine. Chiama `init` se la proprietà data dell&#39;archivio non esiste.

**Parametri**

* nome: Stringa. Nome della proprietà.
* valore: Stringa. Valore proprietà.

**Valore restituito**

Nessun valore restituito.
