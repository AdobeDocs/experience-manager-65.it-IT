---
title: Componenti per frammenti di contenuto
description: I frammenti di contenuto di Adobe Experience Manager (AEM) vengono creati e gestiti come risorse indipendenti dalla pagina
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Componenti per frammenti di contenuto{#components-for-content-fragments}

## Componenti per l’authoring dei frammenti {#components-for-fragment-authoring}

>[!CAUTION]
>
>Si sconsiglia di estendere o modificare i componenti effettivi utilizzati nell’Editor frammento, in quanto sono ancora soggetti a modifiche.

Consulta [API di gestione dei frammenti di contenuto - Lato client](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

>[!CAUTION]
>
>Il [componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=it) è ora consigliato. Per ulteriori dettagli, vedere [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html).
>
>Questa sezione descrive il componente originale distribuito per l&#39;utilizzo con frammenti di contenuto (**Frammento di contenuto** nel gruppo **Generale**).

>[!NOTE]
>
>Per ulteriori informazioni, vedere anche [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/sites-developing/content-fragments-config-components-rendering.md).

I frammenti di contenuto di Adobe Experience Manager (AEM) sono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici. [È quindi possibile utilizzare questi frammenti e le relative varianti durante la creazione delle pagine di contenuto](/help/sites-authoring/content-fragments.md). Puoi anche utilizzare una risorsa frammento di contenuto esistente trascinandola dal browser risorse alla pagina ](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (come per altri componenti basati su risorse, come l&#39;immagine del componente di base). [ Il componente predefinito per frammenti di contenuto visualizza solo un [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del frammento di contenuto di riferimento. La finestra di dialogo del componente consente di definire l&#39;elemento [, la variante e l&#39;intervallo di paragrafi del frammento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) che si desidera visualizzare nella pagina.

>[!NOTE]
>
>Questo componente Frammento di contenuto è stato introdotto in AEM 6.2 come versione migliorata del componente Articolo, che ora è diventato obsoleto.

>[!NOTE]
>
>I frammenti di contenuto non sono supportati nell’interfaccia classica.

### Definizione {#definition}

Il componente **Frammento di contenuto** viene utilizzato per contenere un riferimento a una risorsa frammento di contenuto (risorse di testo effettivamente migliorate). Il tipo di risorsa per il frammento di contenuto è:

`dam/cfm/components/contentfragment/contentfragment`

Il riferimento è definito nella proprietà:

`fileReference`

Solo l’editor dell’interfaccia touch supporta completamente i componenti per frammenti di contenuto, che includono la libreria client:

`cq.authoring.editor.plugin.cfm`

Questa libreria aggiunge all’editor funzioni specifiche dei frammenti di contenuto. È ad esempio disponibile il supporto per la possibilità di aggiungere e configurare frammenti di contenuto sulla pagina, per cercare le risorse dei frammenti di contenuto nel browser delle risorse e per il contenuto associato nel pannello laterale.

### Contenuto intermedio {#in-between-content}

Il componente **Frammento di contenuto** t consente di rilasciare componenti aggiuntivi tra i diversi paragrafi dell&#39;[elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) visualizzato. In pratica, l’elemento visualizzato è composto da paragrafi diversi (ogni paragrafo è contrassegnato da un ritorno a capo). Tra ciascuno di questi paragrafi, è possibile inserire contenuto utilizzando altri componenti.

Da un punto di vista tecnico, ogni paragrafo dell&#39;elemento visualizzato si trova in un proprio parsys, e ogni componente che aggiungi tra i paragrafi viene (sotto il cofano) inserito nel parsys.

In altre parole, se l’istanza del componente Frammento di contenuto è composta da tre paragrafi, il componente avrà tre diversi parsys nell’archivio. Tutto il contenuto intermedio aggiunto al frammento di contenuto si trova effettivamente all’interno di questi parsys.

Nell’archivio, il contenuto intermedio viene memorizzato rispetto alla sua posizione all’interno della struttura generale dei paragrafi, ovvero non viene associato al contenuto effettivo dei paragrafi.

Per illustrare questo aspetto, tieni presente quanto segue:

* Un’istanza di un frammento di contenuto composta da tre paragrafi
* E che parte del contenuto è già stata inserita dopo il secondo paragrafo

   * Ciò significa che il contenuto viene memorizzato nel secondo parsys.

Fondamentalmente, se la struttura paragrafo di questa istanza cambia (modificando la variante, l’elemento o l’intervallo di paragrafi visualizzati), ciò potrebbe influire sul contenuto intermedio visualizzato quando il contenuto del frammento di contenuto:

* Viene modificato e viene aggiunto un altro paragrafo prima del secondo paragrafo:

   * Il contenuto intermedio viene visualizzato dopo il paragrafo appena creato (il secondo parsys contiene ora il paragrafo appena creato).

* Viene modificato e il secondo paragrafo viene rimosso:

   * Il contenuto intermedio viene visualizzato dopo il paragrafo che in precedenza era il terzo (il secondo parsys ora contiene il precedente terzo paragrafo).

* È configurato in modo da visualizzare solo il primo paragrafo:

   * Il contenuto intermedio non viene visualizzato (il secondo parsys non viene più renderizzato a causa della nuova configurazione).

### Personalizzazione del componente Frammento di contenuto {#customizing-the-content-fragment-component}

Per utilizzare il componente predefinito frammento di contenuto come blueprint per l’estensione, è necessario rispettare il seguente contratto:

* Riutilizza lo script di rendering HTL e il relativo POJO associato per vedere come viene implementata la funzione di contenuto intermedio.
* Riutilizzare il nodo del frammento di contenuto: `cq:editConfig`

   * I listener `afterinsert`/ `afteredit`/ `afterdelete` vengono utilizzati per attivare gli eventi JS. Questi eventi vengono gestiti nella libreria client `cq.authoring.editor.plugin.cfm` per visualizzare il contenuto associato nel pannello laterale.
   * `cq:dropTargets` sono configurati per supportare il trascinamento delle risorse dei frammenti di contenuto.
   * `cq:inplaceEditing` è configurato per supportare l&#39;authoring di un frammento di contenuto nell&#39;editor pagina. L&#39;editor locale del frammento è definito nella libreria client `cq.authoring.editor.plugin.cfm` e consente l&#39;apertura di un collegamento rapido per l&#39;[elemento/variante](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) corrente nell&#39;[editor frammento](/help/assets/content-fragments/content-fragments-variations.md).

### Riscrittura delle risorse prima del rendering {#asset-rewriting-before-rendering}

La gestione dei frammenti di contenuto utilizza un processo di rendering interno per generare l’output HTML finale per una pagina. Viene utilizzato internamente dal componente Frammento di contenuto, ma anche dal processo in background che aggiorna i frammenti di riferimento nelle pagine di riferimento.

Internamente, per tale rendering viene utilizzato il rewriter di Sling. La rispettiva configurazione si trova in `/libs/dam/config/rewriter/cfm` e può essere regolata, se necessario. Per ulteriori informazioni, vedi [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html).

>[!CAUTION]
>
>Se regoli/sovrapponi la configurazione del rewriter:
>
>* `/libs/dam/config/rewriter/cfm`
>
>Quindi `serializerType` **must** deve essere aggiornato a:
>
>* `serializerType="html5-serializer"`

La configurazione preconfigurata utilizza i seguenti trasformatori:

* `transformer-cfm-payloadfilter` - solo per il recupero della parte `body` ( `<body>...</body>`) del HTML del frammento

* `transformer-cfm-parfilter` - esclude i paragrafi indesiderati se è specificato un intervallo di paragrafi (come può essere fatto con il componente Frammento di contenuto)
* `transformer-cfm-assetprocessor` - viene utilizzato internamente per recuperare un elenco delle risorse incorporate nel frammento

Il processo di rendering è esposto tramite [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e può essere utilizzato (ad esempio) da componenti personalizzati, se necessario.
