---
title: Componente pagina SPA
seo-title: SPA Page Component
description: In un SPA il componente pagina non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. Questo documento spiega come questo rende univoco il componente della pagina di un SPA.
seo-description: In an SPA the page component doesn't provide the HTML elements of its child components, but instead delegates this to the SPA framework. This document explains how this makes the page component of an SPA unique.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 17c198c744111753ffffcc0758f98859524c964e
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 3%

---

# Componente pagina SPA{#spa-page-component}

In un SPA il componente pagina non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. Questo documento spiega come questo rende univoco il componente della pagina di un SPA.

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

Il componente page per un SPA non fornisce gli elementi HTML dei suoi componenti figlio tramite un file JSP o HTL e oggetti risorsa. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti figlio viene recuperata come struttura dati JSON (ovvero come modello). I componenti SPA vengono quindi aggiunti alla pagina in base al modello JSON fornito. La composizione del corpo iniziale del componente pagina è quindi diversa dalle controparti HTML pre-renderizzate.

## Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a un [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) modulo . Il SPA deve interagire con il `PageModelManager` modulo quando si inizializza per recuperare il modello di pagina iniziale e registrarsi per gli aggiornamenti del modello, prodotto principalmente quando l’autore sta modificando la pagina tramite l’Editor pagina. La `PageModelManager` è accessibile SPA progetto come pacchetto npm. Essendo un interprete tra AEM e SPA, il `PageModelManager` è destinato ad accompagnare il SPA.

Per consentire la creazione della pagina, crea una libreria client denominata `cq.authoring.pagemodel.messaging` deve essere aggiunto per fornire un canale di comunicazione tra il SPA e l’editor di pagine. Se il componente pagina SPA eredita dal componente wcm/core della pagina, sono disponibili le seguenti opzioni per rendere il `cq.authoring.pagemodel.messaging` categoria libreria client disponibile:

* Se il modello è modificabile, aggiungi la categoria della libreria client al criterio della pagina.
* Aggiungi la categoria della libreria client utilizzando `customfooterlibs.html` del componente page.

Non dimenticare di limitare l’inclusione del `cq.authoring.pagemodel.messaging` al contesto dell’editor di pagine.

## Tipo di dati di comunicazione {#communication-data-type}

Il tipo di dati di comunicazione è impostato un elemento HTML all’interno del componente Pagina AEM utilizzando `data-cq-datatype` attributo. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste GET hanno raggiunto gli endpoint del modello Sling di un componente. Dopo che si verifica un aggiornamento nell’editor di pagine, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina avvisa quindi il SPA degli aggiornamenti.

**Componente pagina SPA -`body.html`**

```
<div id="page"></div>
```

Oltre a essere una buona pratica per non ritardare la generazione del DOM, il framework SPA richiede che gli script vengano aggiunti alla fine del corpo.

**Componente pagina SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Proprietà della risorsa meta che descrivono il contenuto SPA:

**Componente pagina SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Il selettore del modello predefinito viene impostato statisticamente quando si richiede la rappresentazione del modello Sling di un componente.

## Metaproprietà {#meta-properties}

* `cq:wcmmode`: Modalità WCM degli editor (ad esempio pagina, modello)
* `cq:pagemodel_root_url`: URL del modello principale dell’app. Importante quando si accede direttamente a una pagina figlio, poiché il modello di pagina figlio è un frammento del modello principale dell’app. La ` [PageModelManager](/help/sites-developing/spa-page-component.md)` quindi ricompone sistematicamente il modello iniziale dell&#39;applicazione quando entra nell&#39;applicazione dal suo punto di ingresso principale.

* `cq:pagemodel_router`: Attiva o disattiva la ` [ModelRouter](/help/sites-developing/spa-routing.md)` del `PageModelManager` libreria

* `cq:pagemodel_route_filters`: Elenco o espressioni regolari separati da virgole per fornire i percorsi ` [ModelRouter](/help/sites-developing/spa-routing.md)` devono ignorare.

>[!CAUTION]
>
>Questo documento utilizza l&#39;app We.Retail Journal solo a scopo dimostrativo. Non deve essere utilizzato per alcun lavoro di progetto.
>
>Qualsiasi progetto AEM deve sfruttare [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta SPA progetti utilizzando React o Angular e sfrutta l’SDK SPA. Tutti i progetti SPA su AEM devono essere basati su Maven Archetype for SPA Starter Kit.

## Sincronizzazione sovrapposizione Editor pagina {#page-editor-overlay-synchronization}

La sincronizzazione delle sovrapposizioni è garantita dallo stesso Mutation Observer fornito dal `cq.authoring.page` categoria.

## Configurazione della struttura esportata JSON del modello Sling {#sling-model-json-exported-structure-configuration}

Quando le funzionalità di routing sono abilitate, si presume che l’esportazione JSON del SPA contenga i diversi percorsi dell’applicazione grazie all’esportazione JSON del componente di navigazione AEM. L’output JSON del componente di navigazione AEM può essere configurato nel criterio del contenuto della pagina principale SPA tramite le due proprietà seguenti:

* `structureDepth`: Numero corrispondente alla profondità dell&#39;albero esportato
* `structurePatterns`: Regex della matrice di regex corrispondente alla pagina da esportare

Può essere mostrato nel contenuto SPA di esempio in `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
