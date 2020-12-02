---
title: Componenti per frammenti di contenuto
seo-title: Componenti per frammenti di contenuto
description: AEM frammenti di contenuto vengono creati e gestiti come risorse indipendenti dalla pagina
seo-description: AEM frammenti di contenuto vengono creati e gestiti come risorse indipendenti dalla pagina
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 4%

---


# Componenti per frammenti di contenuto{#components-for-content-fragments}

## Componenti per l&#39;authoring dei frammenti {#components-for-fragment-authoring}

>[!CAUTION]
>
>Non è consigliabile estendere o modificare i componenti effettivi utilizzati nell&#39;Editor frammento in quanto sono ancora soggetti a modifiche.

Consultate l&#39;API [Content Fragment Management API - Client-Side](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

>[!CAUTION]
>
>È ora consigliabile [Componente di base frammento di contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html). Per ulteriori informazioni, vedere [Sviluppo di componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
>
>In questa sezione viene illustrato il componente originale distribuito per l&#39;utilizzo con frammenti di contenuto (**Frammento di contenuto** nel gruppo **Generale**).

>[!NOTE]
>
>Per ulteriori informazioni, vedere anche [Frammenti di contenuto Configurazione dei componenti per il rendering](/help/sites-developing/content-fragments-config-components-rendering.md).

I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti versatili utilizzabili in qualsiasi canale, con possibili varianti per canali specifici. [Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto](/help/sites-authoring/content-fragments.md). Per usare una risorsa di frammento di contenuto esistente, puoi anche [trascinarla dal browser delle risorse alla pagina](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (come per altri componenti basati su risorse, come ad esempio Immagine componente base). Il componente per frammenti di contenuto fornito visualizza un solo elemento [](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del frammento di contenuto a cui viene fatto riferimento. Utilizzando la finestra di dialogo del componente è possibile definire l&#39; [elemento, la variante e l&#39;intervallo di paragrafi del frammento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) che si desidera visualizzare sulla pagina.

>[!NOTE]
>
>Questo componente Frammento di contenuto è stato introdotto in AEM 6.2 come versione avanzata del componente Articolo, obsoleto.

>[!NOTE]
>
>I frammenti di contenuto non sono supportati nell’interfaccia classica.

### Definizione {#definition}

Il componente **Frammento di contenuto** viene utilizzato per contenere un riferimento a una risorsa di frammento di contenuto (risorse di testo migliorate). Il tipo di risorsa per il frammento di contenuto è:

`dam/cfm/components/contentfragment/contentfragment`

Il riferimento è definito nella proprietà:

`fileReference`

Solo l’editor dell’interfaccia touch supporta completamente i componenti dei frammenti di contenuto, che includono la libreria client:

`cq.authoring.editor.plugin.cfm`

Questa libreria aggiunge all’editor funzioni specifiche per i frammenti di contenuto. Ad esempio, sono disponibili il supporto per la possibilità di aggiungere e configurare frammenti di contenuto nella pagina, la possibilità di cercare risorse per frammenti di contenuto nel browser Risorse e per il contenuto associato nel pannello laterale.

### Contenuto intermedio {#in-between-content}

Il componente **Frammenti di contenuto** t consente di inserire componenti aggiuntivi tra i diversi paragrafi dell&#39;elemento [visualizzato ](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). In sostanza, l’elemento visualizzato è composto da paragrafi diversi (ogni paragrafo è contrassegnato da un ritorno a capo). Tra questi paragrafi, è possibile inserire il contenuto utilizzando altri componenti.

Da un punto di vista tecnico, ogni paragrafo dell&#39;elemento visualizzato* *vive in parsys propri, e ogni componente aggiunto tra i paragrafi sarà (sotto il cofano) inserito nel parsys.

In altre parole, se l’istanza del componente frammento di contenuto è composta da tre paragrafi, il componente conterrà tre diversi parsys nella directory archivio. Tutto il contenuto intermedio aggiunto al frammento di contenuto si trova effettivamente all&#39;interno di questi parsys.

Nel repository, il contenuto intermedio viene memorizzato rispetto alla posizione all’interno della struttura di paragrafi, ovvero non è collegato al contenuto effettivo del paragrafo.

A questo proposito, consideriamo che:

* Un&#39;istanza di un frammento di contenuto composto da tre paragrafi
* E che alcuni contenuti sono già stati inseriti dopo il secondo paragrafo

   * Ciò significa che il contenuto verrà memorizzato nel secondo parsys.

In sostanza, se la struttura del paragrafo di questa istanza viene modificata (modificando la variante, l’elemento o l’intervallo di paragrafi visualizzati), potrebbe influenzare il contenuto intermedio visualizzato quando il contenuto del frammento di contenuto:

* Viene modificato e viene aggiunto un altro paragrafo prima del secondo paragrafo:

   * Il contenuto intermedio verrà visualizzato dopo il paragrafo appena creato (il secondo parsys ora contiene il paragrafo appena creato).

* Viene modificato e il secondo paragrafo viene rimosso:

   * Il contenuto intermedio viene visualizzato dopo il paragrafo precedente (il secondo paragrafo parsys ora contiene il terzo precedente).

* È configurato in modo che venga visualizzato solo il primo paragrafo:

   * Il contenuto intermedio non verrà visualizzato (il secondo parsys non viene più visualizzato a causa della nuova configurazione).

### Personalizzazione del componente frammento di contenuto {#customizing-the-content-fragment-component}

Per utilizzare il componente per frammenti di contenuto out-of-the-box come modello per l’estensione, è necessario rispettare il contratto seguente:

* Riutilizzate lo script di rendering HTL e i relativi POJO associati per vedere in che modo la funzione di contenuto intermedio è implementata.
* Riutilizzare il nodo del frammento di contenuto: `cq:editConfig`

   * I `afterinsert`/ `afteredit`/ `afterdelete` listener vengono utilizzati per attivare gli eventi JS. Questi eventi saranno gestiti nella `cq.authoring.editor.plugin.cfm` libreria client per visualizzare il contenuto associato nel pannello laterale.
   * Le `cq:dropTargets` sono configurate per supportare il trascinamento di risorse di frammenti di contenuto.
   * `cq:inplaceEditing` è configurato per supportare la creazione di un frammento di contenuto nell’editor pagina. L&#39;editor locale del frammento è definito nella libreria client `cq.authoring.editor.plugin.cfm` e consente un collegamento rapido per aprire l&#39;elemento [element/variation](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) corrente nell&#39;editor [frammenti](/help/assets/content-fragments/content-fragments-variations.md).

### Riscrittura risorsa prima del rendering {#asset-rewriting-before-rendering}

Content Fragment Management utilizza un processo di rendering interno per generare l&#39;output HTML finale per una pagina. Questo viene utilizzato internamente dal componente Frammento di contenuto, ma anche dal processo in background che aggiorna i frammenti di riferimento sulle pagine di riferimento.

Internamente, Sling Rewriter viene utilizzato per tale rendering. La configurazione corrispondente si trova in `/libs/dam/config/rewriter/cfm` e può essere regolata se necessario. Per ulteriori informazioni, vedere [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html).

La configurazione out-of-the-box utilizza i seguenti trasformatori:

* `transformer-cfm-payloadfilter` - per il recupero della  `body` parte (  `<body>...</body>`) del solo codice HTML del frammento

* `transformer-cfm-parfilter` - Rimuove i paragrafi indesiderati se è specificato un intervallo di paragrafi (come può essere fatto con il componente Frammento di contenuto)
* `transformer-cfm-assetprocessor` - viene utilizzato internamente per recuperare un elenco delle risorse incorporate nel frammento

Il processo di rendering è esposto tramite [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e può essere sfruttato (ad esempio) da componenti personalizzati, se necessario.
