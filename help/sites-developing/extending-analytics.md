---
title: Estensione del tracciamento degli eventi
seo-title: Estensione del tracciamento degli eventi
description: AEM Analytics consente di monitorare l’interazione degli utenti sul sito Web
seo-description: AEM Analytics consente di monitorare l’interazione degli utenti sul sito Web
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Estensione del tracciamento degli eventi{#extending-event-tracking}

AEM Analytics consente di monitorare l’interazione degli utenti sul sito Web. In qualità di sviluppatore potrebbe essere necessario:

* Monitora il modo in cui i visitatori interagiscono con i tuoi componenti. Questo può essere fatto con [Eventi personalizzati.](#custom-events)
* [Accedere ai valori in ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Aggiungi callback](#adding-record-callbacks) di record.

>[!NOTE]
>
>Queste informazioni sono fondamentalmente generiche, ma utilizzano [ Adobe Analytics](/help/sites-administering/adobeanalytics.md) per esempi specifici.
>
>Per informazioni generali sullo sviluppo di componenti e finestre di dialogo, vedere [Sviluppo di componenti](/help/sites-developing/components.md).

## Eventi personalizzati {#custom-events}

Gli eventi personalizzati tengono traccia di qualsiasi cosa dipenda dalla disponibilità di un componente specifico sulla pagina. Questo include anche eventi specifici per i modelli, in quanto il componente pagina viene trattato come un altro componente.

### Tracciamento degli eventi personalizzati al caricamento della pagina {#tracking-custom-events-on-page-load}

Questo può essere fatto utilizzando lo pseudo-attributo `data-tracking` (l&#39;attributo record precedente è ancora supportato per la compatibilità con le versioni precedenti). Potete aggiungere questo tag a qualsiasi tag HTML.

La sintassi per `data-tracking` è

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Potete passare un numero qualsiasi di coppie chiave-valore come secondo parametro, che è chiamato payload.

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

Al caricamento della pagina, tutti gli attributi `data-tracking` verranno raccolti e aggiunti all&#39;archivio eventi di ContextHub, dove possono essere mappati  eventi Adobe Analytics. Gli eventi non mappati non verranno tracciati da  Adobe Analytics. Per ulteriori informazioni sulla mappatura degli eventi, vedere [Connessione a  Adobe Analytics](/help/sites-administering/adobeanalytics.md).

### Tracciamento eventi personalizzati dopo il caricamento della pagina {#tracking-custom-events-after-page-load}

Per tenere traccia degli eventi che si verificano dopo il caricamento di una pagina (ad esempio, le interazioni con l&#39;utente), utilizzare la funzione JavaScript `CQ_Analytics.record`:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Dove

* `events` è una stringa o un array di stringhe (per più eventi).

* `values` contiene tutti i valori da monitorare
* `collect` è facoltativo e restituisce un array contenente l&#39;evento e l&#39;oggetto dati.
* `options` è facoltativo e contiene opzioni di tracciamento dei collegamenti come elementi HTML  `obj` e  ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` è un attributo necessario ed è consigliabile impostarlo su  `<%=resource.getResourceType()%>`

Ad esempio, con la definizione seguente, se un utente fa clic sul collegamento **Passa all&#39;inizio**, vengono attivati i due eventi `jumptop` e `headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Accesso ai valori in ContextHub {#accessing-values-in-the-contexthub}

L&#39;API JavaScript ContextHub dispone di una funzione `getStore(name)` che restituisce lo store specificato, se disponibile. Lo store ha una funzione `getItem(key)` che restituisce il valore della chiave specificata, se disponibile. Utilizzando la funzione `getKeys()` è possibile recuperare un array di chiavi definite per lo store specifico.

È possibile notificare le modifiche di valore in uno store eseguendo il binding di una funzione utilizzando la funzione `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

Il modo migliore per ricevere una notifica della disponibilità iniziale di ContextHub è utilizzare la funzione `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventi aggiuntivi per ContextHub:**

Tutti i negozi pronti:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Specifico per lo store:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Vedi anche [Riferimento API ContextHub completo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Aggiunta di callback di record {#adding-record-callbacks}

Prima e dopo che le callback vengono registrate utilizzando le funzioni `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Entrambe le funzioni assumono una funzione come primo argomento e un rango come secondo argomento, che stabilisce l&#39;ordine in cui vengono eseguite le callback.

Se il callback restituisce false, le callback seguenti nella catena di esecuzione non verranno eseguite.
