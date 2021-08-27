---
title: Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL
description: Scopri come utilizzare AEM frammenti di contenuto con GraphQL per la distribuzione di contenuti headless.
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con Adobe Experience Manager (AEM), puoi utilizzare Frammenti di contenuto, insieme all’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard), per distribuire in modo headless contenuti strutturati da utilizzare nelle applicazioni. La possibilità di personalizzare un’unica query API ti consente di recuperare e fornire il contenuto specifico di cui desideri eseguire il rendering (come risposta alla singola query API).

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM):
>
>* [AEM Commerce consuma dati da una piattaforma commerce tramite GraphQL](/help/commerce/cif/integrating/magento.md).
>* [AEM Frammenti di contenuto collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/assets/content-fragments/graphql-api-content-fragments.md).


## CMS headless {#headless-cms}

Un sistema di gestione dei contenuti headless (CMS) è:

* &quot;*Un sistema di gestione dei contenuti headless, o CMS headless, è un sistema di gestione dei contenuti (CMS) back-end basato su un archivio di contenuti che rende i contenuti accessibili tramite un&#39;API per la visualizzazione su qualsiasi dispositivo.*

   Vedere [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

In termini di authoring di frammenti di contenuto in AEM ciò significa che:

* È possibile utilizzare Frammenti di contenuto per creare contenuti che non sono destinati principalmente alla pubblicazione diretta (1:1) su pagine formattate.

* Il contenuto dei frammenti di contenuto sarà strutturato in modo predeterminato in base ai modelli di frammento di contenuto . Questo semplifica l&#39;accesso alle applicazioni, che elaboreranno ulteriormente i contenuti.

## GraphQL - Panoramica {#graphql-overview}

GraphQL è:

* &quot;*..un linguaggio di query per le API e un runtime per l&#39;esecuzione di tali query con i dati esistenti.*&quot;.

   Consulta [GraphQL.org](https://graphql.org)

L’ [AEM API GraphQL](#aem-graphql-api) consente di eseguire query (complesse) sui [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md); con ogni query in base a un tipo di modello specifico. Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

## AEM API GraphQL {#aem-graphql-api}

Per Adobe Experience è stata sviluppata un’implementazione personalizzata dell’API GraphQL standard. Per informazioni dettagliate, consulta [AEM API GraphQL per l’utilizzo con Frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md) .

L&#39;implementazione AEM dell&#39;API GraphQL si basa sulle [librerie Java GraphQL](https://graphql.org/code/#java).

## Frammenti di contenuto da utilizzare con l’API GraphQL AEM {#content-fragments-use-with-aem-graphql-api}

[I ](#content-fragments) frammenti di contenuto possono essere utilizzati come base per GraphQL per query AEM come:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* I [Modelli di frammento di contenuto](#content-fragments-models) forniscono la struttura richiesta tramite tipi di dati definiti.
* Il [Riferimento frammento](#fragment-references), disponibile durante la definizione di un modello, può essere utilizzato per definire livelli aggiuntivi di struttura.

![Frammenti di contenuto da utilizzare con i frammenti ](assets/cfm-nested-01.png "GraphQLContent per GraphQL")

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contenere contenuti strutturati.

* Si basano su un [modello di frammento di contenuto](#content-fragments-models) che predefinisce la struttura per il frammento risultante.

### Modelli per frammenti di contenuto {#content-fragments-models}

Questi [Modelli di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md):

* Vengono utilizzati per generare gli [Schemi](https://graphql.org/learn/schema/) una volta **Abilitati**.

* Fornisci i tipi di dati e i campi richiesti per GraphQL. Assicurano che la tua applicazione richieda solo ciò che è possibile e riceva ciò che è previsto.

* Il tipo di dati **[Riferimenti frammento](#fragment-references)** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre livelli aggiuntivi di struttura.

### Riferimenti ai frammenti {#fragment-references}

Il **[Riferimento al frammento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato durante la definizione di un modello di frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di un modello di frammento di contenuto specifico.

* Consente di recuperare dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a più frammenti secondari (recuperati) dal frammento principale.

### Anteprima JSON {#json-preview}

Per semplificare la progettazione e lo sviluppo dei modelli di frammenti di contenuto, puoi visualizzare in anteprima l’ [output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Per un&#39;introduzione all&#39;utilizzo dell&#39;API GraphQL AEM, consulta [Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query](/help/assets/content-fragments/content-fragments-graphql-samples.md) .

## Tutorial: guida introduttiva a AEM Headless e GraphQL

Stai cercando un tutorial pratico? Consulta la [Guida introduttiva AEM Headless e l’esercitazione end-to-end GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) che illustra come creare ed esporre contenuti utilizzando le API GraphQL di AEM e utilizzati da un’app esterna, in uno scenario CMS headless.
