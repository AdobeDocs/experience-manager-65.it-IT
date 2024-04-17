---
title: Aggiunta di ContextHub alle pagine e accesso agli store
description: Aggiungi ContextHub alle pagine per abilitare le funzioni di ContextHub e per collegare le librerie JavaScript di ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Aggiunta di ContextHub alle pagine e accesso agli store {#adding-contexthub-to-pages-and-accessing-stores}

Aggiungi ContextHub alle pagine per abilitare le funzioni di ContextHub e per collegare le librerie JavaScript di ContextHub.

L’API JavaScript ContextHub fornisce accesso ai dati contestuali gestiti da ContextHub. Questa pagina descrive brevemente le funzioni principali dell’API per accedere e manipolare i dati contestuali. Per informazioni dettagliate ed esempi di codice, segui i collegamenti alla documentazione di riferimento delle API.

## Aggiunta di ContextHub a un componente pagina {#adding-contexthub-to-a-page-component}

Per abilitare le funzioni di ContextHub e collegare le librerie JavaScript di ContextHub, includi `contexthub` componente in `head` della pagina. Il codice HTL del componente page deve essere simile al seguente esempio:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Inoltre, devi configurare se la barra degli strumenti di ContextHub viene visualizzata in modalità Anteprima. Consulta [Visualizzazione e nascondere l’interfaccia utente di ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Informazioni sugli store ContextHub {#about-contexthub-stores}

Utilizza gli archivi ContextHub per rendere persistenti i dati contestuali. ContextHub fornisce i seguenti tipi di store che costituiscono la base di tutti i tipi di store:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tutti i tipi di store sono estensioni del [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe. Per informazioni sulla creazione di un tipo di archivio, consulta [Creazione di store personalizzati](ch-extend.md#creating-custom-store-candidates). Per informazioni sui tipi di archivio di esempio, vedi [Candidati archivio ContextHub di esempio](ch-samplestores.md).

### Modalità di persistenza {#persistence-modes}

Gli archivi Context Hub utilizzano una delle seguenti modalità di persistenza:

* **Locale:** Utilizza HTML5 localStorage per salvare i dati in modo permanente. L’archiviazione locale viene mantenuta nel browser per tutte le sessioni.
* **Sessione:** Utilizza HTML5 sessionStorage per rendere persistenti i dati. L’archiviazione della sessione viene mantenuta per tutta la durata della sessione del browser ed è disponibile per tutte le finestre del browser.
* **Cookie:** Utilizza il supporto nativo dei cookie del browser per l’archiviazione dei dati. I dati dei cookie vengono inviati al e dal server nelle richieste HTTP.
* **Window.name:** Utilizza la proprietà window.name per mantenere i dati.
* **Memoria:** Utilizza un oggetto JavaScript per mantenere i dati in modo permanente.

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

La struttura ad albero definisce gli elementi dati nell’archivio come coppie chiave/valore. Nell’esempio precedente, la chiave `/number` corrisponde al valore `321`e la chiave `/data/country` corrisponde al valore `Switzerland`.

### Manipolazione di oggetti {#manipulating-objects}

ContextHub fornisce [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) classe per la manipolazione di oggetti JavaScript. Utilizzare le funzioni di questa classe per manipolare gli oggetti JavaScript prima di aggiungerli a un archivio o dopo averli ottenuti da un archivio.

Inoltre, il [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) La classe fornisce funzioni per serializzare gli oggetti alle stringhe e deserializzare le stringhe agli oggetti. Utilizza questa classe per gestire i dati JSON e supportare i browser che non includono in modo nativo il `JSON.parse` e `JSON.stringify` funzioni.

## Interazione con gli store ContextHub {#interacting-with-contexthub-stores}

Utilizza il [`ContextHub`](contexthub-api.md#ui-event-constants) Oggetto JavaScript per ottenere un archivio come oggetto JavaScript. Una volta ottenuto l&#39;oggetto store, è possibile manipolare i dati in esso contenuti. Utilizza il [`getAllStores`](contexthub-api.md#getallstores) o [`getStore`](contexthub-api.md#getstore-name) per ottenere il punto vendita.

### Accesso ai dati store {#accessing-store-data}

Il [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) La classe JavaScript definisce diverse funzioni per interagire con i dati dell’archivio. Le funzioni seguenti memorizzano e recuperano più elementi di dati contenuti negli oggetti:

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
>Puoi rendere ContextHub consapevole degli utenti connessi caricando l’archivio profili. Fai riferimento a [codice di esempio su GitHub qui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Evento ContextHub {#contexthub-eventing}

ContextHub include un framework di eventi che ti consente di reagire automaticamente per archiviare gli eventi. Ogni oggetto store contiene un [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) oggetto disponibile come [`eventing`](contexthub-api.md#eventing) proprietà. Utilizza il [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) funzione per associare una funzione JavaScript a un evento store.

## Utilizzo di Context Hub per manipolare i cookie {#using-context-hub-to-manipulate-cookies}

L’API JavaScript di Context Hub fornisce supporto cross-browser per la gestione dei cookie del browser. Il [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace definisce diverse funzioni per creare, manipolare ed eliminare i cookie.

## Determinazione dei segmenti ContextHub risolti {#determining-resolved-contexthub-segments}

Il motore di segmenti ContextHub consente di determinare quali dei segmenti registrati vengono risolti nel contesto corrente. Utilizzare la funzione getResolvedSegments di [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) classe per recuperare i segmenti risolti. Quindi, utilizza `getName` o `getPath` funzione del [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) classe per testare un segmento.

### Segmenti ContextHub {#contexthub-segments}

I segmenti ContextHub vengono installati sotto il `/conf/<site>/settings/wcm/segments` nodo.

I seguenti segmenti vengono installati con [Sito tutorial WKND.](getting-started.md)

* estate
* inverno

Le regole utilizzate per risolvere questi segmenti sono riepilogate come segue:

* Prima il [geolocalizzazione](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) store viene utilizzato per determinare la latitudine dell’utente.
* Quindi l&#39;elemento dati del mese del [store surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina la stagione in quella latitudine.

>[!WARNING]
>
>I segmenti installati vengono forniti come configurazioni di riferimento per aiutarti a creare la tua configurazione dedicata per il progetto. Non utilizzarle direttamente.

## Debug di ContextHub {#debugging-contexthub}

Sono disponibili diverse opzioni per il debug di ContextHub, inclusa la generazione di registri. Consulta [Configurazione di ContextHub per ulteriori informazioni.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Panoramica del framework ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fornisce un [pagina diagnostica](ch-diagnostics.md) dove puoi vedere una panoramica del framework ContextHub.
