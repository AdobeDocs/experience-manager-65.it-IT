---
title: Componenti per frammenti di contenuto
seo-title: Components for Content Fragments
description: I frammenti di contenuto AEM vengono creati e gestiti come risorse indipendenti dalla pagina
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 5%

---

# Componenti per frammenti di contenuto{#components-for-content-fragments}

## Componenti per l’authoring dei frammenti {#components-for-fragment-authoring}

>[!CAUTION]
>
>Non è consigliabile estendere o modificare i componenti effettivi utilizzati nell’Editor frammento in quanto sono ancora soggetti a modifiche.

Consulta la sezione [API di gestione dei frammenti di contenuto - Lato client](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

>[!CAUTION]
>
>La [Componente core frammento di contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) è ora consigliato. Vedi [Sviluppo di componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) per ulteriori dettagli.
>
>Questa sezione descrive il componente originale consegnato per l’uso con i frammenti di contenuto (**Frammento di contenuto** in **Generale** gruppo).

>[!NOTE]
>
>Vedi anche [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/sites-developing/content-fragments-config-components-rendering.md) per ulteriori informazioni.

I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti versatili utilizzabili in qualsiasi canale, con possibili varianti per canali specifici. [Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto](/help/sites-authoring/content-fragments.md). Puoi inoltre utilizzare una risorsa frammento di contenuto esistente per [trascinarlo dal browser delle risorse alla pagina](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (come per altri componenti basati su risorse, ad esempio il componente di base Immagine). Il componente per frammenti di contenuto pronto all’uso visualizza un solo componente [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del frammento di contenuto a cui si fa riferimento. Nella finestra di dialogo del componente puoi definire la [elemento, variante e intervallo di paragrafi del frammento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) che si desidera visualizzare sulla pagina.

>[!NOTE]
>
>Questo componente Frammento di contenuto è stato introdotto in AEM 6.2 come versione avanzata del componente Articolo , che è stato dichiarato obsoleto.

>[!NOTE]
>
>I frammenti di contenuto non sono supportati nell’interfaccia classica.

### Definizione {#definition}

La **Frammento di contenuto** viene utilizzato per contenere un riferimento a una risorsa di frammento di contenuto (con miglioramenti effettivi delle risorse di testo). Il tipo di risorsa per il frammento di contenuto è:

`dam/cfm/components/contentfragment/contentfragment`

Il riferimento è definito nella proprietà :

`fileReference`

Solo l’editor dell’interfaccia touch supporta completamente i componenti dei frammenti di contenuto, che includono la libreria client:

`cq.authoring.editor.plugin.cfm`

Questa libreria aggiunge all’editor funzioni specifiche dei frammenti di contenuto. Ad esempio, sono disponibili il supporto per la possibilità di aggiungere e configurare frammenti di contenuto nella pagina, la possibilità di cercare risorse per frammenti di contenuto nel browser Risorse e per il contenuto associato nel pannello laterale.

### Contenuto intermedio {#in-between-content}

La **Frammenti di contenuto** Il componente permette di rilasciare ulteriori componenti tra i diversi paragrafi della [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). In sostanza, l’elemento visualizzato è composto da paragrafi diversi (ogni paragrafo è contrassegnato da un ritorno a capo). Tra ciascuno di questi paragrafi, puoi inserire il contenuto utilizzando altri componenti.

Da un punto di vista tecnico, ogni paragrafo dell’elemento visualizzato* *vive nel proprio parsys e ogni componente che aggiungi tra i paragrafi sarà inserito (sotto il cofano) nel parsys.

In altre parole, se l’istanza del componente frammento di contenuto è composta da tre paragrafi, il componente avrà tre parsys diversi nell’archivio. Tutto il contenuto intermedio aggiunto al frammento di contenuto si trova effettivamente all’interno di questi parsys.

Nell’archivio il contenuto intermedio viene memorizzato rispetto alla sua posizione all’interno della struttura del paragrafo generale, ovvero non è collegato al contenuto effettivo del paragrafo.

A questo proposito, consideriamo che:

* Un’istanza di un frammento di contenuto composto da tre paragrafi
* E che alcuni contenuti sono già stati inseriti dopo il secondo paragrafo

   * Ciò significa che il contenuto verrà memorizzato nel secondo parsys.

In sostanza, se la struttura del paragrafo di questa istanza cambia (modificando la variante, l’elemento o l’intervallo di paragrafi visualizzati), potrebbe influenzare il contenuto intermedio visualizzato quando il contenuto del frammento di contenuto:

* Viene modificato e viene aggiunto un altro paragrafo prima del secondo paragrafo:

   * Il contenuto intermedio verrà visualizzato dopo il nuovo paragrafo creato (il secondo parsys ora contiene il paragrafo appena creato).

* Viene modificato e il secondo paragrafo viene rimosso:

   * Il contenuto intermedio viene visualizzato dopo il paragrafo precedente (il secondo parsys ora contiene il terzo paragrafo precedente).

* È configurato in modo che venga visualizzato solo il primo paragrafo:

   * Il contenuto intermedio non verrà visualizzato (il secondo parsys non viene più visualizzato a causa della nuova configurazione).

### Personalizzazione del componente Frammento di contenuto {#customizing-the-content-fragment-component}

Per utilizzare il componente frammento di contenuto predefinito come blueprint per l’estensione, è necessario rispettare il contratto seguente:

* Riutilizza lo script di rendering HTL e il relativo POJO associato per vedere come viene implementata la funzione di contenuto intermedio.
* Riutilizzare il nodo del frammento di contenuto: `cq:editConfig`

   * La `afterinsert`/ `afteredit`/ `afterdelete` i listener vengono utilizzati per attivare gli eventi JS. Questi eventi verranno gestiti nel `cq.authoring.editor.plugin.cfm` libreria client per visualizzare il contenuto associato nel pannello laterale.
   * La `cq:dropTargets` sono configurati per supportare il trascinamento delle risorse dei frammenti di contenuto.
   * `cq:inplaceEditing` è configurato per supportare la creazione di un frammento di contenuto nell’editor pagina. L’editor locale del frammento è definito nella sezione `cq.authoring.editor.plugin.cfm` libreria client e consente un collegamento rapido per aprire la [elemento/variante](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) in [editor frammenti](/help/assets/content-fragments/content-fragments-variations.md).

### Riscrittura delle risorse prima del rendering {#asset-rewriting-before-rendering}

La gestione dei frammenti di contenuto utilizza un processo di rendering interno per generare l’output finale di HTML per una pagina. Viene utilizzato internamente dal componente Frammento di contenuto, ma anche dal processo in background che aggiorna i frammenti di riferimento sulle pagine di riferimento.

Internamente, lo sling Rewriter viene utilizzato per quel rendering. La configurazione corrispondente si trova in `/libs/dam/config/rewriter/cfm` e può essere regolato se necessario. Consulta la sezione [Rewriter Sling Apache](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) per ulteriori informazioni.

>[!CAUTION]
>
>Se regoli/sovrapponi la configurazione del rewriter:
>
>* `/libs/dam/config/rewriter/cfm`
>
>quindi il `serializerType` **deve** vengono aggiornati a:
>
>* `serializerType="html5-serializer"`


La configurazione predefinita utilizza i seguenti trasformatori:

* `transformer-cfm-payloadfilter` - per il recupero del `body` parte ( `<body>...</body>`) solo del HTML del frammento

* `transformer-cfm-parfilter` - filtra i paragrafi indesiderati se è specificato un intervallo di paragrafi (come è possibile fare con il componente Frammento di contenuto)
* `transformer-cfm-assetprocessor` - viene utilizzato internamente per recuperare un elenco delle risorse incorporate nel frammento

Il processo di rendering viene esposto attraverso [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e può essere utilizzato (ad esempio) dai componenti personalizzati, se necessario.
