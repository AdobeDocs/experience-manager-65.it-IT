---
title: Aggiunta di ContextHub alle pagine e accesso ai negozi
description: Aggiungi ContextHub alle tue pagine per abilitare le funzionalità di ContextHub e per effettuare il collegamento alle librerie Javascript di ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Aggiunta di ContextHub alle pagine e accesso ai negozi {#adding-contexthub-to-pages-and-accessing-stores}

Aggiungi ContextHub alle tue pagine per abilitare le funzionalità di ContextHub e per effettuare il collegamento alle librerie Javascript di ContextHub.

L’API Javascript di ContextHub fornisce l’accesso ai dati contestuali gestiti da ContextHub. Questa pagina descrive brevemente le funzioni principali dell’API per l’accesso ai dati contestuali e la loro manipolazione. Segui i collegamenti alla documentazione di riferimento API per visualizzare informazioni dettagliate ed esempi di codice.

## Aggiunta di ContextHub a un componente pagina {#adding-contexthub-to-a-page-component}

Per abilitare le funzioni ContextHub e per effettuare il collegamento alle librerie Javascript di ContextHub, includi le `contexthub` nel `head` della pagina. Il codice HTL per il componente pagina deve essere simile al seguente esempio:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

È inoltre necessario configurare se la barra degli strumenti di ContextHub viene visualizzata in modalità Anteprima. Vedi [Mostrare e nascondere l’interfaccia utente di ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Informazioni sugli archivi ContextHub {#about-contexthub-stores}

Utilizza gli archivi ContextHub per mantenere i dati contestuali. ContextHub fornisce i seguenti tipi di archivi che costituiscono la base di tutti i tipi di store:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tutti i tipi di archivio sono estensioni del [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe. Per informazioni sulla creazione di un nuovo tipo di archivio, consulta [Creazione di store personalizzati](ch-extend.md#creating-custom-store-candidates). Per informazioni sui tipi di archivio di esempio, consulta [Candidati allo store ContextHub di esempio](ch-samplestores.md).

### Modalità di persistenza {#persistence-modes}

Gli archivi di Context Hub utilizzano una delle seguenti modalità di persistenza:

* **Locale:** Utilizza HTML5 localStorage per mantenere i dati. L&#39;archiviazione locale viene mantenuta sul browser in più sessioni.
* **Sessione:** Utilizza HTML5 sessionStorage per mantenere i dati. L’archiviazione della sessione viene mantenuta per tutta la durata della sessione del browser ed è disponibile per tutte le finestre del browser.
* **Cookie:** Utilizza il supporto nativo dei cookie del browser per l&#39;archiviazione dei dati. I dati dei cookie vengono inviati a e dal server nelle richieste HTTP.
* **Window.name:** Utilizza la proprietà window.name per mantenere i dati.
* **Memoria:** Utilizza un oggetto Javascript per mantenere i dati.

Per impostazione predefinita, Context Hub utilizza la modalità di persistenza locale. Se il browser non supporta o consente HTML5 localStorage, viene utilizzata la persistenza della sessione. Se il browser non supporta o consente HTML5 sessionStorage, viene utilizzata la persistenza Window.name.

### Dati store {#store-data}

All’interno, archiviare i dati forma una struttura ad albero, consentendo l’aggiunta di valori come tipi principali o oggetti complessi. Quando si aggiungono oggetti complessi agli archivi, le proprietà dell&#39;oggetto vengono aggiunte ai rami della struttura dati. Ad esempio, il seguente oggetto complesso viene aggiunto a un archivio vuoto denominato location:

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

La struttura ad albero dei dati archiviati può essere concettualizzata come segue:

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

### Manipolazione degli oggetti {#manipulating-objects}

ContextHub fornisce [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) Classe per la manipolazione di oggetti JavaScript. Utilizzare le funzioni di questa classe per manipolare gli oggetti Javascript prima di aggiungerli a uno store o dopo averli ottenuti da uno store.

Inoltre, la [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) Questa classe fornisce funzioni per la serializzazione degli oggetti alle punture e la deserializzazione delle stringhe agli oggetti. Usa questa classe per gestire i dati JSON per supportare i browser che non includono in modo nativo i `JSON.parse` e `JSON.stringify` funzioni.

## Interazione con gli archivi ContextHub {#interacting-with-contexthub-stores}

Utilizza la [`ContextHub`](contexthub-api.md#ui-event-constants) Oggetto JavaScript per ottenere un archivio come oggetto Javascript. Una volta ottenuto l&#39;oggetto Store è possibile manipolare i dati contenuti. Utilizza la [`getAllStores`](contexthub-api.md#getallstores) o [`getStore`](contexthub-api.md#getstore-name) per ottenere lo store.

### Accesso ai dati dell’archivio {#accessing-store-data}

La [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) La classe JavaScript definisce diverse funzioni per l&#39;interazione con i dati dell&#39;archivio. Le seguenti funzioni memorizzano e recuperano più elementi dati contenuti negli oggetti:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

I singoli elementi dati sono memorizzati come un insieme di coppie chiave/valore. Per memorizzare e recuperare i valori si specifica la chiave corrispondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

I candidati all’archivio personalizzati possono definire funzioni aggiuntive che consentono l’accesso ai dati archiviati.

>[!NOTE]
>
>ContextHub non è per impostazione predefinita a conoscenza dell&#39;accesso attualmente utilizzato sui server di pubblicazione e tali utenti sono considerati da ContextHub come &quot;Anonymous&quot;.
>
>Puoi rendere ContextHub consapevole degli utenti connessi caricando l’archivio dei profili. Fai riferimento a [codice di esempio su GitHub qui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Evento ContextHub {#contexthub-eventing}

ContextHub include un framework di eventi che consente di reagire automaticamente agli eventi archiviati. Ogni oggetto store contiene un [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) oggetto disponibile come [`eventing`](contexthub-api.md#eventing) proprietà. Utilizza la [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) per associare una funzione Javascript a un evento store.

## Utilizzo di Context Hub per manipolare i cookie {#using-context-hub-to-manipulate-cookies}

L’API Javascript di Context Hub fornisce supporto cross-browser per la gestione dei cookie del browser. La [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) Lo spazio dei nomi definisce diverse funzioni per la creazione, la manipolazione e l’eliminazione dei cookie.

## Determinazione dei segmenti ContextHub risolti {#determining-resolved-contexthub-segments}

Il motore di segmenti ContextHub ti consente di determinare quali dei segmenti registrati vengono risolti nel contesto corrente. Utilizzare la funzione getResolvedSegments del [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) per recuperare i segmenti risolti. Quindi, utilizza il `getName` o `getPath` funzione [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) da sottoporre a test per un segmento.

### Segmenti ContextHub {#contexthub-segments}

I segmenti ContextHub sono installati sotto la `/conf/<site>/settings/wcm/segments` nodo.

I seguenti segmenti sono installati con [Sito tutorial WKND.](getting-started.md)

* estate
* inverno

Le regole utilizzate per risolvere questi segmenti sono riepilogate come segue:

* Prima la [geolocalizzazione](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) viene utilizzato per determinare la latitudine dell&#39;utente.
* Quindi la voce dati del mese del [negozio surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina quale stagione è in quella latitudine.

>[!WARNING]
>
>I segmenti installati vengono forniti come configurazioni di riferimento per facilitare la creazione di una configurazione dedicata per il progetto e non devono quindi essere utilizzati direttamente.

## Debug di ContextHub {#debugging-contexthub}

Esistono diverse opzioni per il debug di ContextHub, inclusa la generazione di registri. Vedi [Configurazione di ContextHub per ulteriori informazioni.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Vedi una panoramica del framework ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fornisce un [pagina di diagnostica](ch-diagnostics.md) dove puoi visualizzare una panoramica del framework ContextHub.
