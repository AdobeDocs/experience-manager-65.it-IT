---
title: Componente pagina SPA
seo-title: Componente pagina SPA
description: In un SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti secondari, ma lo delega al framework SPA. Questo documento spiega come questo rende univoco il componente pagina di un SPA.
seo-description: In un SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti secondari, ma lo delega al framework SPA. Questo documento spiega come questo rende univoco il componente pagina di un SPA.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---


# SPA componente pagina{#spa-page-component}

In un SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti secondari, ma lo delega al framework SPA. Questo documento spiega come questo rende univoco il componente pagina di un SPA.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Introduzione {#introduction}

Il componente della pagina per un SPA non fornisce gli elementi HTML dei suoi componenti secondari tramite un file JSP o HTL e oggetti risorsa. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti secondari viene recuperata come struttura dati JSON (ovvero come modello). I componenti SPA vengono quindi aggiunti alla pagina in base al modello JSON fornito. La composizione iniziale del corpo del componente della pagina è pertanto diversa dalle controparti HTML sottoposte a pre rendering.

## Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina è delegata a un modulo [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) fornito. Il SPA deve interagire con il modulo `PageModelManager` quando si inizializza per recuperare il modello di pagina iniziale e registrarsi per gli aggiornamenti del modello, prodotto principalmente quando l&#39;autore sta modificando la pagina tramite Editor pagina. Il `PageModelManager` è accessibile SPA progetto come pacchetto npm. Essendo un interprete tra AEM e il SPA, il `PageModelManager` deve accompagnare il SPA.

Per consentire la creazione della pagina, è necessario aggiungere una libreria client denominata `cq.authoring.pagemodel.messaging` per fornire un canale di comunicazione tra il SPA e l&#39;editor pagina. Se il componente della pagina SPA eredita dal componente wcm/core della pagina, sono disponibili le seguenti opzioni per rendere disponibile la categoria della libreria client `cq.authoring.pagemodel.messaging`:

* Se il modello è modificabile, aggiungete la categoria della libreria client al criterio pagina.
* Aggiungete la categoria della libreria client utilizzando `customfooterlibs.html` del componente pagina.

Non dimenticare di limitare l&#39;inclusione della categoria `cq.authoring.pagemodel.messaging` al contesto dell&#39;editor di pagina.

## Tipo di dati di comunicazione {#communication-data-type}

Il tipo di dati di comunicazione è impostato come elemento HTML all&#39;interno del componente Pagina AEM utilizzando l&#39;attributo `data-cq-datatype`. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste di GET hanno raggiunto gli endpoint del modello Sling di un componente. Quando si verifica un aggiornamento nell’editor di pagina, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina avvisa quindi il SPA degli aggiornamenti.

**Componente pagina SPA -`body.html`**

```
<div id="page"></div>
```

Oltre ad essere una buona prassi per non ritardare la generazione del DOM, il framework SPA richiede che gli script vengano aggiunti alla fine del corpo.

**Componente pagina SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Proprietà delle risorse meta che descrivono il contenuto SPA:

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
>Il selettore predefinito del modello è impostato in modo statico quando si richiede la rappresentazione del modello Sling di un componente.

## Metaproprietà {#meta-properties}

* `cq:wcmmode`: Modalità WCM degli editor (ad esempio pagina, modello)
* `cq:pagemodel_root_url`: URL del modello principale dell&#39;app. È fondamentale quando si accede direttamente a una pagina figlia, dal momento che il modello di pagina figlia è un frammento del modello radice dell&#39;app. Il ` [PageModelManager](/help/sites-developing/spa-page-component.md)` quindi ricompone sistematicamente il modello iniziale dell&#39;applicazione quando entra nell&#39;applicazione dal punto di ingresso principale.

* `cq:pagemodel_router`: Attivare o disattivare la  ` [ModelRouter](/help/sites-developing/spa-routing.md)` libreria  `PageModelManager` 

* `cq:pagemodel_route_filters`: Elenco separato da virgole o espressioni regolari per fornire percorsi che  ` [ModelRouter](/help/sites-developing/spa-routing.md)` devono essere ignorati.

>[!CAUTION]
>
>Questo documento utilizza l&#39;app We.Retail Journal solo a scopo dimostrativo. Non deve essere utilizzato per nessun progetto.
>
>Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l&#39;SDK SPA. Tutti SPA progetti su AEM devono essere basati sul tipo di archivio di Maven per SPA Starter Kit.

## Sincronizzazione sovrapposizione Editor pagina {#page-editor-overlay-synchronization}

La sincronizzazione delle sovrapposizioni è garantita dallo stesso Mutation Observer fornito dalla categoria `cq.authoring.page`.

## Configurazione struttura esportata JSON modello Sling {#sling-model-json-exported-structure-configuration}

Quando le funzionalità di routing sono abilitate, il presupposto è che l&#39;esportazione JSON del SPA contenga i diversi percorsi dell&#39;applicazione grazie all&#39;esportazione JSON del componente di navigazione AEM. L&#39;output JSON del componente di navigazione AEM può essere configurato nel criterio di contenuto SPA pagina principale tramite le due seguenti proprietà:

* `structureDepth`: Numero corrispondente alla profondità della struttura esportata
* `structurePatterns`: Regex di array di regessi corrispondenti alla pagina da esportare

Questo può essere mostrato nel contenuto SPA campione in `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
