---
title: Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL
description: Scopri come utilizzare Frammenti di contenuto AEM con GraphQL per la distribuzione di contenuti headless.
feature: Content Fragments
role: User
exl-id: 2debd678-2d73-41f2-b33c-c29d661f6a6b
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 74%

---

# Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con Adobe Experience Manager (AEM), puoi utilizzare Frammenti di contenuto e l’API GraphQL AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni. La possibilità di personalizzare una singola query API consente di recuperare e fornire il contenuto specifico che desideri riprodurre (come risposta alla singola query API).

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>GraphQL è attualmente utilizzato in due scenari (separati) in Adobe Experience Manager (AEM):
>
>* [AEM Commerce sfrutta i dati da una piattaforma commerce tramite GraphQL](/help/commerce/cif/integrating/magento.md).
>* [I Frammenti di contenuto AEM collaborano con l’API GraphQL di AEM (un’implementazione personalizzata, basata su GraphQL standard) per fornire contenuti strutturati da utilizzare nelle applicazioni](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

## CMS headless {#headless-cms}

Un sistema per la gestione dei contenuti (CMS) headless è:

* &quot;*Un sistema di gestione dei contenuti headless, o CMS headless, è un sistema di gestione dei contenuti (CMS) di back-end progettato come archivio di contenuti che li rende accessibili tramite un’API per la visualizzazione su qualsiasi dispositivo.*

  Vedi [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

In termini di authoring di frammenti di contenuto in AEM, questo significa che:

* È possibile utilizzare i frammenti di contenuto per l’authoring contenuti che non sono destinati principalmente alla pubblicazione diretta (1:1) su pagine formattate.

* Il contenuto dei frammenti sarà strutturato in modo predeterminato in base ai modelli per frammenti di contenuto. Questo ne semplifica l’accesso da parte delle applicazioni che poi elaboreranno ulteriormente i contenuti.

## GraphQL: panoramica {#graphql-overview}

GraphQL è:

* “*...un linguaggio di query per le API e un runtime per l’esecuzione di tali query con i dati esistenti.*”

  Vedi [GraphQL.org](https://graphql.org)

Il [API GRAPHQL AEM](#aem-graphql-api) consente di eseguire query (complesse) sul [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md); ogni query è basata su un tipo di modello specifico. Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

## API GraphQL di AEM {#aem-graphql-api}

Ad Adobe, è stata sviluppata un’implementazione personalizzata dell’API GraphQL standard. Per informazioni, consulta [API GraphQL AEM per l’utilizzo con Frammenti di contenuto](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

L’implementazione dell’API GraphQL per AEM si basa sulle [librerie Java GraphQL](https://graphql.org/code/#java).

## Frammenti di contenuto da utilizzare con l’API GraphQL di AEM {#content-fragments-use-with-aem-graphql-api}

I [frammenti di contenuto](#content-fragments) possono essere utilizzati come base per GraphQL per query AEM per i seguenti motivi:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* I [Modelli per frammenti di contenuto](#content-fragments-models) forniscono la struttura richiesta per mezzo di tipi di dati definiti.
* Il [Riferimento frammento](#fragment-references), disponibile quando si definisce un modello, può essere utilizzato per definire livelli di struttura aggiuntivi.

![Frammenti di contenuto da utilizzare con GraphQL](assets/cfm-nested-01.png "Frammenti di contenuto da utilizzare con GraphQL")

### Frammenti di contenuto {#content-fragments}

Frammenti di contenuto:

* Contengono contenuti strutturati.

* Sono basati su un [Modello per frammenti di contenuto](#content-fragments-models) che predefinisce la struttura del frammento risultante.

### Modelli per frammenti di contenuto {#content-fragments-models}

I [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md):

* Sono utilizzati per generare gli [Schemi](https://graphql.org/learn/schema/), una volta **Abilitati**.

* Forniscono i tipi di dati e i campi richiesti per GraphQL. Assicurano che l’applicazione trasmetta solo richieste ammesse e riceva solo i contenuti previsti.

* Il tipo di dati **[Riferimenti frammento](#fragment-references)** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre ulteriori livelli di struttura.

### Riferimenti frammento {#fragment-references}

Il **[Riferimento frammento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato durante la definizione di un modello per frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di un modello per frammento di contenuto specifico.

* Consente di recuperare i dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a (recuperare) più frammenti secondari dal frammento principale.

### Anteprima JSON {#json-preview}

Per semplificare la progettazione e lo sviluppo dei modelli per frammenti di contenuto, puoi visualizzare in anteprima l’[output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query {#learn-graphql-with-aem-sample-content-queries}

Per un’introduzione all’utilizzo dell’API GraphQL di AEM, consulta [Imparare a utilizzare GraphQL con AEM: contenuto di esempio e query](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md).

## Tutorial: guida introduttiva ad AEM headless e GraphQL

Cerchi un pratico tutorial? Dai un&#39;occhiata al tutorial [Guida introduttiva di headless AEM e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it) che illustra come creare ed esporre contenuti, utilizzati da un’app esterna, mediante le API GraphQL di AEM in uno scenario CMS headless.
