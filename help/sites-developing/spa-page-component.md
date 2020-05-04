---
title: Componente pagina SPA
seo-title: Componente pagina SPA
description: In un’area SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. In questo documento viene illustrato come questo rende univoco il componente di pagina di un’area speciale.
seo-description: In un’area SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. In questo documento viene illustrato come questo rende univoco il componente di pagina di un’area speciale.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579

---


# Componente pagina SPA{#spa-page-component}

In un’area SPA, il componente pagina non fornisce gli elementi HTML dei suoi componenti figlio, ma lo delega al framework SPA. In questo documento viene illustrato come questo rende univoco il componente di pagina di un’area speciale.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su SPA (ad esempio React o Angular).

## Introduzione {#introduction}

Il componente di pagina per un&#39;app SPA non fornisce gli elementi HTML dei suoi componenti secondari tramite un file JSP o HTL e oggetti risorsa. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti secondari viene recuperata come struttura dati JSON (ovvero come modello). I componenti SPA vengono quindi aggiunti alla pagina in base al modello JSON fornito. La composizione iniziale del corpo del componente della pagina è pertanto diversa dalle controparti HTML sottoposte a pre rendering.

## Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina è delegata a un [ modulo specificato `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) . L&#39;SPA deve interagire con il `PageModelManager` modulo quando si inizializza per recuperare il modello di pagina iniziale e registrarsi per gli aggiornamenti del modello, prodotto principalmente quando l&#39;autore sta modificando la pagina tramite Editor pagina. Il progetto SPA `PageModelManager` è accessibile come pacchetto npm. Essendo un interprete tra AEM e l’SPA, il `PageModelManager` progetto è inteso ad accompagnare l’SPA.

Per consentire la creazione della pagina, `cq.authoring.pagemodel.messaging` è necessario aggiungere una libreria client denominata per fornire un canale di comunicazione tra l’API e l’editor pagina. Se il componente della pagina SPA eredita dal componente wcm/core della pagina, sono disponibili le seguenti opzioni per rendere disponibile la categoria della libreria `cq.authoring.pagemodel.messaging` client:

* Se il modello è modificabile, aggiungete la categoria della libreria client al criterio pagina.
* Aggiungete la categoria della libreria client utilizzando il componente `customfooterlibs.html` della pagina.

Non dimenticare di limitare l’inclusione della `cq.authoring.pagemodel.messaging` categoria al contesto dell’editor di pagina.

## Tipo di dati di comunicazione {#communication-data-type}

Il tipo di dati di comunicazione è impostato con l’ `data-cq-datatype` attributo un elemento HTML all’interno del componente Pagina AEM. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste GET hanno raggiunto gli endpoint del modello Sling di un componente. Quando si verifica un aggiornamento nell’editor di pagina, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina invia quindi un avviso all’area SPA degli aggiornamenti.

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
* `cq:pagemodel_root_url`: URL del modello principale dell&#39;app. È fondamentale quando si accede direttamente a una pagina figlia, dal momento che il modello di pagina figlia è un frammento del modello radice dell&#39;app. Il modello iniziale dell&#39;applicazione viene ` [PageModelManager](/help/sites-developing/spa-page-component.md)` quindi sistematicamente ricomposto quando entra nell&#39;applicazione dal punto di ingresso principale.

* `cq:pagemodel_router`: Attivare o disattivare la ` [ModelRouter](/help/sites-developing/spa-routing.md)` libreria `PageModelManager`

* `cq:pagemodel_route_filters`: Elenco separato da virgole o espressioni regolari per fornire percorsi che ` [ModelRouter](/help/sites-developing/spa-routing.md)` devono essere ignorati.

>[!CAUTION]
>
>Questo documento utilizza l&#39;app We.Retail Journal solo a scopo dimostrativo. Non deve essere utilizzato per nessun progetto.
>
>Qualsiasi progetto AEM deve sfruttare il Project Archetype [di](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html)AEM, che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK SPA.Tutti i progetti SPA su AEM devono essere basati sul tipo di archivio di Maven per SPA Starter Kit.

## Sincronizzazione sovrapposizione Editor pagina {#page-editor-overlay-synchronization}

La sincronizzazione delle sovrapposizioni è garantita dallo stesso Mutation Observer fornito dalla `cq.authoring.page` categoria.

## Configurazione struttura esportata JSON modello Sling {#sling-model-json-exported-structure-configuration}

Quando le funzionalità di routing sono abilitate, si presuppone che l’esportazione JSON dell’app SPA contenga i diversi percorsi dell’applicazione grazie all’esportazione JSON del componente di navigazione AEM. L&#39;output JSON del componente di navigazione AEM può essere configurato nei criteri di contenuto della pagina principale dell&#39;app tramite le due seguenti proprietà:

* `structureDepth`: Numero corrispondente alla profondità della struttura esportata
* `structurePatterns`: Regex di array di regessi corrispondenti alla pagina da esportare

Questo può essere mostrato nel contenuto di esempio SPA in `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
