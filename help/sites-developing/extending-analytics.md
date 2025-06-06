---
title: Estensione del tracciamento degli eventi
description: AEM Analytics consente di monitorare l’interazione dell’utente sul sito web
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Estensione del tracciamento degli eventi{#extending-event-tracking}

AEM Analytics consente di monitorare l’interazione dell’utente sul sito web. In qualità di sviluppatore, potresti dover:

* Monitora il modo in cui i visitatori interagiscono con i componenti. Questa operazione può essere eseguita con [eventi personalizzati.](#custom-events)
* [Accedere ai valori in ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Aggiungi callback di record](#adding-record-callbacks).

>[!NOTE]
>
>Queste informazioni sono essenzialmente generiche, ma per esempi specifici viene utilizzato [Adobe Analytics](/help/sites-administering/adobeanalytics.md).
>
>Per informazioni generali sullo sviluppo di componenti e finestre di dialogo, vedere [Sviluppo di componenti](/help/sites-developing/components.md).

## Eventi personalizzati {#custom-events}

Gli eventi personalizzati tengono traccia di tutto ciò che dipende dalla disponibilità di un componente specifico sulla pagina. Sono inclusi anche gli eventi specifici del modello, in quanto il componente pagina viene trattato come un altro componente.

### Tracciamento Degli Eventi Personalizzati Al Caricamento Della Pagina {#tracking-custom-events-on-page-load}

Questa operazione può essere eseguita utilizzando lo pseudo-attributo `data-tracking` (l&#39;attributo di record precedente è ancora supportato per la compatibilità con le versioni precedenti). Puoi aggiungerlo a qualsiasi tag HTML.

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

Al caricamento della pagina, tutti gli attributi `data-tracking` verranno raccolti e aggiunti all&#39;archivio eventi di ContextHub, dove possono essere mappati agli eventi di Adobe Analytics. Gli eventi non mappati non verranno tracciati da Adobe Analytics. Vedi [Connessione ad Adobe Analytics](/help/sites-administering/adobeanalytics.md) per ulteriori dettagli sugli eventi di mappatura.

### Tracciamento Degli Eventi Personalizzati Dopo Il Caricamento Della Pagina {#tracking-custom-events-after-page-load}

Per tenere traccia degli eventi che si verificano dopo il caricamento di una pagina, ad esempio le interazioni dell&#39;utente, utilizzare la funzione JavaScript `CQ_Analytics.record`:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Dove

* `events` è una stringa o una matrice di stringhe (per più eventi).

* `values` contiene tutti i valori da tracciare
* `collect` è facoltativo e restituirà un array contenente l&#39;evento e l&#39;oggetto dati.
* `options` è facoltativo e contiene opzioni di tracciamento dei collegamenti come l&#39;elemento HTML `obj` e ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` è un attributo necessario e si consiglia di impostarlo su `<%=resource.getResourceType()%>`

Ad esempio, con la seguente definizione, un utente che fa clic sul collegamento **Passa all&#39;inizio** causerà l&#39;attivazione dei due eventi `jumptop` e `headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Accesso ai valori in ContextHub {#accessing-values-in-the-contexthub}

L&#39;API JavaScript ContextHub ha una funzione `getStore(name)` che restituisce l&#39;archivio specificato, se disponibile. L&#39;archivio dispone di una funzione `getItem(key)` che restituisce il valore della chiave specificata, se disponibile. Utilizzando la funzione `getKeys()` è possibile recuperare un array di chiavi definite per l&#39;archivio specifico.

È possibile ricevere notifiche sulle modifiche dei valori in un archivio associando una funzione utilizzando la funzione `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

Il modo migliore per ricevere una notifica della disponibilità iniziale di ContextHub è utilizzare la funzione `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventi aggiuntivi per ContextHub:**

Tutti i negozi sono pronti:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Specifico per store:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Vedi anche il riferimento API [ContextHub completo](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Aggiunta di callback di record {#adding-record-callbacks}

I callback prima e dopo sono registrati utilizzando le funzioni `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Entrambe le funzioni assumono una funzione come primo argomento e una classificazione come secondo argomento, che determina l&#39;ordine di esecuzione dei callback.

Se il callback restituisce false, i callback che seguono nella catena di esecuzione non verranno eseguiti.
