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
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 5%

---

# Componenti per frammenti di contenuto{#components-for-content-fragments}

## Componenti per l’authoring dei frammenti {#components-for-fragment-authoring}

>[!CAUTION]
>
>Si sconsiglia di estendere o modificare i componenti effettivi utilizzati nell’Editor frammento, in quanto sono ancora soggetti a modifiche.

Consulta la [API di gestione dei frammenti di contenuto - Lato client](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

>[!CAUTION]
>
>Il [Componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en) è ora consigliato. Consulta [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it) per ulteriori dettagli.
>
>Questa sezione descrive il componente originale distribuito per essere utilizzato con i frammenti di contenuto (**Frammento di contenuto** nel **Generale** gruppo).

>[!NOTE]
>
>Vedi anche [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/sites-developing/content-fragments-config-components-rendering.md) per ulteriori informazioni.

I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici. [Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto](/help/sites-authoring/content-fragments.md). Puoi anche utilizzare una risorsa per frammenti di contenuto esistente tramite [trascinarlo dal browser risorse alla pagina](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) (come per altri componenti basati su risorse, ad esempio l’immagine del componente di base). Il componente per frammenti di contenuto predefinito ne visualizza solo uno [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) del frammento di contenuto di riferimento. Utilizzando la finestra di dialogo del componente è possibile definire [elemento, variante e intervallo di paragrafi di frammenti](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) che desideri visualizzare sulla pagina.

>[!NOTE]
>
>Questo componente Frammento di contenuto è stato introdotto in AEM 6.2 come versione migliorata del componente Articolo, che ora è diventato obsoleto.

>[!NOTE]
>
>I frammenti di contenuto non sono supportati nell’interfaccia classica.

### Definizione {#definition}

Il **Frammento di contenuto** il componente viene utilizzato per contenere un riferimento a una risorsa di un frammento di contenuto (risorse di testo effettivamente migliorate). Il tipo di risorsa per il frammento di contenuto è:

`dam/cfm/components/contentfragment/contentfragment`

Il riferimento è definito nella proprietà:

`fileReference`

Solo l’editor dell’interfaccia touch supporta completamente i componenti per frammenti di contenuto, che includono la libreria client:

`cq.authoring.editor.plugin.cfm`

Questa libreria aggiunge all’editor funzioni specifiche dei frammenti di contenuto. È ad esempio disponibile il supporto per la possibilità di aggiungere e configurare frammenti di contenuto sulla pagina, per cercare le risorse dei frammenti di contenuto nel browser delle risorse e per il contenuto associato nel pannello laterale.

### Contenuto intermedio {#in-between-content}

Il **Frammento di contenuto** t consente di rilasciare componenti aggiuntivi tra i diversi paragrafi del [elemento](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). In pratica, l’elemento visualizzato è composto da paragrafi diversi (ogni paragrafo è contrassegnato da un ritorno a capo). Tra ciascuno di questi paragrafi, è possibile inserire contenuto utilizzando altri componenti.

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
* Riutilizza il nodo del frammento di contenuto: `cq:editConfig`

   * Il `afterinsert`/ `afteredit`/ `afterdelete` I listener vengono utilizzati per attivare gli eventi JS. Questi eventi vengono gestiti nel `cq.authoring.editor.plugin.cfm` libreria client per visualizzare il contenuto associato nel pannello laterale.
   * Il `cq:dropTargets` sono configurate per supportare il trascinamento delle risorse dei frammenti di contenuto.
   * `cq:inplaceEditing` è configurato per supportare l’authoring di un frammento di contenuto nell’editor pagina. L’editor locale del frammento è definito nel `cq.authoring.editor.plugin.cfm` e consente di aprire la libreria corrente tramite un collegamento rapido [elemento/variante](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) nel [editor frammenti](/help/assets/content-fragments/content-fragments-variations.md).

### Riscrittura delle risorse prima del rendering {#asset-rewriting-before-rendering}

La gestione dei frammenti di contenuto utilizza un processo di rendering interno per generare l’output HTML finale per una pagina. Viene utilizzato internamente dal componente Frammento di contenuto, ma anche dal processo in background che aggiorna i frammenti di riferimento nelle pagine di riferimento.

Internamente, per tale rendering viene utilizzato il rewriter di Sling. La rispettiva configurazione si trova in `/libs/dam/config/rewriter/cfm` e possono essere regolati, se necessario. Consulta la [Rewriter Apache Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) per ulteriori informazioni.

>[!CAUTION]
>
>Se regoli/sovrapponi la configurazione del rewriter:
>
>* `/libs/dam/config/rewriter/cfm`
>
>Quindi il `serializerType` **deve** è aggiornato a:
>
>* `serializerType="html5-serializer"`

La configurazione preconfigurata utilizza i seguenti trasformatori:

* `transformer-cfm-payloadfilter` - per recuperare `body` parte ( `<body>...</body>`) solo del HTML del frammento

* `transformer-cfm-parfilter` : filtra i paragrafi indesiderati se è specificato un intervallo di paragrafi (come può essere fatto con il componente Frammento di contenuto)
* `transformer-cfm-assetprocessor` : viene utilizzato internamente per recuperare un elenco delle risorse incorporate nel frammento

Il processo di rendering viene esposto tramite [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) e possono essere utilizzati (ad esempio) da componenti personalizzati, se necessario.
