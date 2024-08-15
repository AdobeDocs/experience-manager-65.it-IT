---
title: Aggiunta di ContextHub alle pagine e accesso agli store
description: Aggiungi ContextHub alle pagine per abilitare le funzioni di ContextHub e per collegare le librerie JavaScript di ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Aggiunta di ContextHub alle pagine e accesso agli store {#adding-contexthub-to-pages-and-accessing-stores}

Aggiungi ContextHub alle pagine per abilitare le funzioni di ContextHub e per collegare le librerie JavaScript di ContextHub.

L’API JavaScript di ContextHub consente di accedere ai dati contestuali gestiti da ContextHub. Questa pagina descrive brevemente le funzioni principali dell’API per accedere e manipolare i dati contestuali. Per informazioni dettagliate ed esempi di codice, segui i collegamenti alla documentazione di riferimento delle API.

## Aggiunta di ContextHub a un componente pagina {#adding-contexthub-to-a-page-component}

Per abilitare le funzionalità di ContextHub e collegare le librerie JavaScript di ContextHub, includi il componente `contexthub` nella sezione `head` della pagina. Il codice HTL del componente page deve essere simile al seguente esempio:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Inoltre, devi configurare se la barra degli strumenti di ContextHub viene visualizzata in modalità Anteprima. Vedi [Visualizzazione e nascondere l&#39;interfaccia utente di ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Informazioni sugli store ContextHub {#about-contexthub-stores}

Utilizza gli archivi ContextHub per rendere persistenti i dati contestuali. ContextHub fornisce i seguenti tipi di store che costituiscono la base di tutti i tipi di store:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tutti i tipi di archivio sono estensioni della classe [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core). Per informazioni sulla creazione di un tipo di archivio, vedere [Creazione di archivi personalizzati](ch-extend.md#creating-custom-store-candidates). Per informazioni sui tipi di archivio campioni, vedi [Candidati archivio ContextHub campione](ch-samplestores.md).

### Modalità di persistenza {#persistence-modes}

Gli archivi Context Hub utilizzano una delle seguenti modalità di persistenza:

* **Locale:** utilizza HTML5 localStorage per salvare i dati in modo permanente. L’archiviazione locale viene mantenuta nel browser per tutte le sessioni.
* **Sessione:** utilizza HTML5 sessionStorage per salvare i dati in modo permanente. L’archiviazione della sessione viene mantenuta per tutta la durata della sessione del browser ed è disponibile per tutte le finestre del browser.
* **Cookie:** utilizza il supporto nativo dei cookie del browser per l&#39;archiviazione dei dati. I dati dei cookie vengono inviati al e dal server nelle richieste HTTP.
* **Window.name:** Utilizza la proprietà window.name per rendere persistenti i dati.
* **Memoria:** utilizza un oggetto JavaScript per salvare i dati in modo permanente.

Per impostazione predefinita, Context Hub utilizza la modalità di persistenza locale. Se il browser non supporta o consente HTML5 localStorage, viene utilizzata la persistenza della sessione. Se il browser non supporta o consente HTML5 sessionStorage, viene utilizzata la persistenza Window.name.

### Dati store {#store-data}

Internamente, i dati vengono memorizzati in una struttura ad albero, consentendo l&#39;aggiunta di valori come tipi primari o oggetti complessi. Quando si aggiungono oggetti complessi agli archivi, le proprietà dell&#39;oggetto formano rami nella struttura dati. Ad esempio, il seguente oggetto complesso viene aggiunto a un archivio vuoto denominato location:

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

La struttura ad albero dei dati dell’archivio può essere concettualizzata come segue:

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

La struttura ad albero definisce gli elementi dati nell’archivio come coppie chiave/valore. Nell&#39;esempio precedente, la chiave `/number` corrisponde al valore `321` e la chiave `/data/country` corrisponde al valore `Switzerland`.

### Manipolazione di oggetti {#manipulating-objects}

ContextHub fornisce la classe [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) per la manipolazione degli oggetti JavaScript. Utilizzare le funzioni di questa classe per manipolare gli oggetti JavaScript prima di aggiungerli a un archivio o dopo averli ottenuti da un archivio.

Inoltre, la classe [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) fornisce funzioni per serializzare gli oggetti alle stringhe e deserializzare le stringhe agli oggetti. Utilizzare questa classe per la gestione dei dati JSON per supportare browser che non includono in modo nativo le funzioni `JSON.parse` e `JSON.stringify`.

## Interazione con gli store ContextHub {#interacting-with-contexthub-stores}

Utilizzare l&#39;oggetto JavaScript [`ContextHub`](contexthub-api.md#ui-event-constants) per ottenere un archivio come oggetto JavaScript. Una volta ottenuto l&#39;oggetto store, è possibile manipolare i dati in esso contenuti. Utilizzare la funzione [`getAllStores`](contexthub-api.md#getallstores) o [`getStore`](contexthub-api.md#getstore-name) per ottenere l&#39;archivio.

### Accesso ai dati store {#accessing-store-data}

La classe JavaScript [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) definisce diverse funzioni per l&#39;interazione con i dati dell&#39;archivio. Le funzioni seguenti memorizzano e recuperano più elementi di dati contenuti negli oggetti:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

I singoli elementi di dati sono memorizzati come un insieme di coppie chiave/valore. Per memorizzare e recuperare i valori, specifica la chiave corrispondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Tieni presente che i candidati all’archivio personalizzato possono definire funzioni aggiuntive per consentire l’accesso ai dati dell’archivio.

>[!NOTE]
>
>ContextHub non è a conoscenza, per impostazione predefinita, dell’accesso attualmente utilizzato sui server di pubblicazione e tali utenti sono considerati da ContextHub come &quot;Anonimi&quot;.
>
>Puoi rendere ContextHub consapevole degli utenti connessi caricando l’archivio profili. Fai riferimento al [codice di esempio su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Evento ContextHub {#contexthub-eventing}

ContextHub include un framework di eventi che ti consente di reagire automaticamente per archiviare gli eventi. Ogni oggetto archivio contiene un oggetto [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) disponibile come proprietà [`eventing`](contexthub-api.md#eventing) dell&#39;archivio. Utilizzare la funzione [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) per associare una funzione JavaScript a un evento store.

## Utilizzo di Context Hub per manipolare i cookie {#using-context-hub-to-manipulate-cookies}

L’API JavaScript di Context Hub fornisce supporto tra browser diversi per la gestione dei cookie del browser. Lo spazio dei nomi [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) definisce diverse funzioni per la creazione, la manipolazione e l&#39;eliminazione dei cookie.

## Determinazione dei segmenti ContextHub risolti {#determining-resolved-contexthub-segments}

Il motore di segmenti ContextHub consente di determinare quali dei segmenti registrati vengono risolti nel contesto corrente. Utilizzare la funzione getResolvedSegments della classe [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) per recuperare i segmenti risolti. Utilizzare quindi la funzione `getName` o `getPath` della classe [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) per verificare la presenza di un segmento.

### Segmenti ContextHub {#contexthub-segments}

I segmenti ContextHub sono installati sotto il nodo `/conf/<site>/settings/wcm/segments`.

I seguenti segmenti sono installati con il [sito WKND tutorial.](getting-started.md)

* estate
* inverno

Le regole utilizzate per risolvere questi segmenti sono riepilogate come segue:

* Innanzitutto, viene utilizzato l&#39;archivio [geolocation](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) per determinare la latitudine dell&#39;utente.
* Quindi l&#39;elemento dati del mese dell&#39;[archivio surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina la stagione in cui si trova tale latitudine.

>[!WARNING]
>
>I segmenti installati vengono forniti come configurazioni di riferimento per aiutarti a creare la tua configurazione dedicata per il progetto. Non utilizzarle direttamente.

## Debug di ContextHub {#debugging-contexthub}

Sono disponibili diverse opzioni per il debug di ContextHub, inclusa la generazione di registri. Per ulteriori informazioni, vedere [Configurazione di ContextHub.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Panoramica del framework ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fornisce una [pagina di diagnostica](ch-diagnostics.md) in cui è possibile visualizzare una panoramica del framework ContextHub.
