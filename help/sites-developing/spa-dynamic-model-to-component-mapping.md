---
title: Mappatura da modello dinamico a componente per SPA
seo-title: Mappatura da modello dinamico a componente per SPA
description: In questo articolo viene descritto in che modo si verifica la mappatura del modello dinamico al componente nell’SDK SPA JavaScript per AEM.
seo-description: In questo articolo viene descritto in che modo si verifica la mappatura del modello dinamico al componente nell’SDK SPA JavaScript per AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Mappatura da modello dinamico a componente per SPA{#dynamic-model-to-component-mapping-for-spas}

In questo documento viene descritto in che modo si verifica la mappatura del modello dinamico al componente nell’SDK Javascript SPA per AEM.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Modulo di mappatura dei componenti {#componentmapping-module}

Il modulo `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. memorizza i componenti front-end e consente all’applicazione a pagina singola di mappare i componenti front-end sui tipi di risorse AEM. Questo consente una risoluzione dinamica dei componenti durante l&#39;analisi del modello JSON dell&#39;applicazione.

Ogni elemento presente nel modello contiene un campo `:type` che espone un tipo di risorsa AEM. Quando è montato, il componente front-end può eseguire il rendering utilizzando il frammento del modello ricevuto dalle librerie sottostanti.

Per ulteriori informazioni sull&#39;analisi dei modelli e sull&#39;accesso al modello dei componenti front-end, fare riferimento al documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md).

Vedete anche il pacchetto npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Applicazione a pagina singola basata su modello {#model-driven-single-page-application}

Le applicazioni a pagina singola che utilizzano l’SDK SPA JavaScript per AEM sono basate su modelli:

1. I componenti front-end si registrano nel [archivio mappatura componenti](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Quindi il [Contenitore](/help/sites-developing/spa-blueprint.md#container), una volta fornito con un modello dal [Provider di modelli](/help/sites-developing/spa-blueprint.md#the-model-provider), esegue un&#39;iterazione sul contenuto del modello ( `:items`).

1. Nel caso di una pagina, i relativi elementi secondari ( `:children`) ottengono prima una classe di componenti dalla [mappatura dei componenti](/help/sites-developing/spa-blueprint.md#componentmapping) e quindi la creano in un&#39;istanza.

## Inizializzazione app {#app-initialization}

Ogni componente viene esteso con le funzionalità di [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). L&#39;inizializzazione assume pertanto la seguente forma generale:

1. Ogni provider di modelli si inizializza e ascolta le modifiche apportate al pezzo di modello che corrisponde al suo componente interno.
1. Il [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) deve essere inizializzato come rappresentato dal [flusso di inizializzazione](/help/sites-developing/spa-blueprint.md).

1. Una volta memorizzato, il gestore modelli pagina restituisce il modello completo dell&#39;app.
1. Questo modello viene quindi passato al componente principale front-end [Container](/help/sites-developing/spa-blueprint.md#container) dell&#39;applicazione.
1. I pezzi del modello vengono infine propagati a ogni singolo componente secondario.

![app_model_initialize](assets/app_model_initialization.png)

