---
title: Mappatura di un modello dinamico a un componente per SPA
description: Scopri come avviene la mappatura del modello dinamico ai componenti nell’SDK SPA di JavaScript per Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Mappatura di un modello dinamico a un componente per SPA{#dynamic-model-to-component-mapping-for-spas}

Questo documento descrive come avviene la mappatura del modello dinamico ai componenti nell’SDK SPA di JavaScript per Adobe Experience Manager (AEM).

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono il rendering lato client basato sul framework SPA (ad esempio, React o Angular).

## Modulo ComponentMapping {#componentmapping-module}

Il modulo `ComponentMapping` viene fornito come pacchetto NPM al progetto front-end. Memorizza i componenti front-end e consente all’applicazione a pagina singola di mappare i componenti front-end ai tipi di risorse AEM. Ciò abilita una risoluzione dinamica dei componenti durante l’analisi del modello JSON dell’applicazione.

Ogni elemento presente nel modello contiene un campo `:type` che espone un tipo di risorsa AEM. Una volta montato, il componente front-end può eseguire il rendering utilizzando il frammento di modello ricevuto dalle librerie sottostanti.

Per ulteriori informazioni sull&#39;analisi del modello e sull&#39;accesso al componente front-end del modello, vedere [Blueprint per SPA](/help/sites-developing/spa-blueprint.md).

Vedi anche il pacchetto npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Applicazione a pagina singola basata su modello {#model-driven-single-page-application}

Le applicazioni a pagina singola che utilizzano JavaScript SPA SDK per AEM sono basate su modelli:

1. I componenti front-end si registrano nell&#39;[archivio mappature componenti](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Il contenitore [Contenitore](/help/sites-developing/spa-blueprint.md#container), una volta fornito con un modello da [Provider di modelli](/help/sites-developing/spa-blueprint.md#the-model-provider), scorre il contenuto del modello ( `:items`).

1. Se è presente una pagina, i relativi elementi secondari ( `:children`) ottengono prima una classe di componente da [Mappatura componente](/help/sites-developing/spa-blueprint.md#componentmapping) e quindi creano un&#39;istanza.

## Inizializzazione app {#app-initialization}

Ogni componente viene esteso con le funzionalità di [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). L&#39;inizializzazione assume pertanto la seguente forma generale:

1. Ogni provider di modelli si inizializza e ascolta le modifiche apportate al pezzo di modello che corrisponde al relativo componente interno.
1. [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) deve essere inizializzato come rappresentato dal [flusso di inizializzazione](/help/sites-developing/spa-blueprint.md).

1. Una volta memorizzata, il gestore modelli della pagina restituisce il modello completo dell’app.
1. Questo modello viene quindi passato al componente principale front-end [Container](/help/sites-developing/spa-blueprint.md#container) dell&#39;applicazione.
1. I pezzi del modello vengono infine propagati a ogni singolo componente figlio.

![app_model_initialization](assets/app_model_initialization.png)
