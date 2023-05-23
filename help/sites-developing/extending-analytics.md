---
title: Estensione del tracciamento degli eventi
seo-title: Extending Event Tracking
description: AEM Analytics consente di tenere traccia dell’interazione dell’utente sul sito web
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Estensione del tracciamento degli eventi{#extending-event-tracking}

AEM Analytics consente di tenere traccia dell’interazione dell’utente sul sito web. In qualità di sviluppatore, potresti dover:

* Monitora il modo in cui i visitatori interagiscono con i componenti. Questa operazione può essere eseguita con [Eventi personalizzati.](#custom-events)
* [Accedere ai valori in ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Aggiungi callback di record](#adding-record-callbacks).

>[!NOTE]
>
>Queste informazioni sono fondamentalmente generiche, ma utilizzano [Adobe Analytics](/help/sites-administering/adobeanalytics.md) per esempi specifici.
>
>Per informazioni generali sullo sviluppo di componenti e finestre di dialogo, consultate [Sviluppo di componenti](/help/sites-developing/components.md).

## Eventi personalizzati {#custom-events}

Gli eventi personalizzati tengono traccia di tutto ciò che dipende dalla disponibilità di un componente specifico sulla pagina. Sono inclusi anche gli eventi specifici del modello, in quanto il componente pagina viene trattato come un altro componente.

### Tracciamento Degli Eventi Personalizzati Al Caricamento Della Pagina {#tracking-custom-events-on-page-load}

Questa operazione può essere eseguita utilizzando lo pseudo-attributo `data-tracking` l&#39;attributo di record precedente è ancora supportato per la compatibilità con le versioni precedenti. Puoi aggiungerlo a qualsiasi tag HTML.

La sintassi per `data-tracking` è

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

È possibile passare un numero qualsiasi di coppie chiave-valore come secondo parametro, denominato payload.

Un esempio potrebbe essere:

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

Al caricamento della pagina, tutte `data-tracking` Gli attributi verranno raccolti e aggiunti all’archivio eventi di ContextHub, dove possono essere mappati agli eventi di Adobe Analytics. Gli eventi non mappati non verranno tracciati da Adobe Analytics. Consulta [Connessione ad Adobe Analytics](/help/sites-administering/adobeanalytics.md) per ulteriori dettagli sulla mappatura degli eventi.

### Tracciamento Degli Eventi Personalizzati Dopo Il Caricamento Della Pagina {#tracking-custom-events-after-page-load}

Per tenere traccia degli eventi che si verificano dopo il caricamento di una pagina (come le interazioni dell’utente), utilizza `CQ_Analytics.record` Funzione JavaScript:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Dove

* `events` è una stringa o una matrice di stringhe (per più eventi).

* `values` contiene tutti i valori da tracciare
* `collect` è facoltativo e restituirà un array contenente l’evento e l’oggetto dati.
* `options` è facoltativo e contiene opzioni di tracciamento dei collegamenti come l’elemento HTML `obj` e ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` è un attributo necessario e si consiglia di impostarlo su `<%=resource.getResourceType()%>`

Ad esempio, con la seguente definizione, un utente fa clic su **Passa all&#39;inizio** causerà i due eventi, `jumptop` e `headlineclick`, da licenziare:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Accesso ai valori in ContextHub {#accessing-values-in-the-contexthub}

L’API JavaScript di ContextHub dispone di un `getStore(name)` funzione che restituisce l&#39;archivio specificato, se disponibile. Il negozio ha `getItem(key)` funzione che restituisce il valore della chiave specificata, se disponibile. Utilizzo di `getKeys()` funzione è possibile recuperare un array di chiavi definite per l’archivio specifico.

Puoi ricevere notifiche sulle modifiche di valore su un archivio associando una funzione utilizzando `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` funzione.

Il modo migliore per ricevere notifiche sulla disponibilità iniziale di ContextHub è utilizzare `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` funzione.

**Eventi aggiuntivi per ContextHub:**

Tutti i negozi sono pronti:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Specifico per store:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Vedi anche il [Riferimento API di ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Aggiunta di callback di record {#adding-record-callbacks}

Prima e dopo la registrazione dei callback tramite le funzioni `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Entrambe le funzioni assumono una funzione come primo argomento e una classificazione come secondo argomento, che determina l&#39;ordine di esecuzione dei callback.

Se il callback restituisce false, i callback che seguono nella catena di esecuzione non verranno eseguiti.
