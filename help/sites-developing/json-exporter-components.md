---
title: Abilitazione dell’esportazione JSON per un componente
seo-title: Enabling JSON Export for a Component
description: I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modeling.
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 9%

---

# Abilitazione dell’esportazione JSON per un componente{#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modeling.

## Panoramica {#overview}

L’esportazione JSON è basata su [Modelli Sling](https://sling.apache.org/documentation/bundles/models.html)e [Esportatore di modelli Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) quadro (su cui si basa [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, dovrai seguire questi due passaggi per abilitare l’esportazione JSON su qualsiasi componente.

* [Definire un modello Sling per il componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotare l’interfaccia del modello Sling](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Innanzitutto, per il componente deve essere definito un modello Sling.

>[!NOTE]
>
>Per un esempio di utilizzo dei modelli Sling, consulta l’articolo [Sviluppo di esportatori di modelli Sling in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

La classe di implementazione del modello Sling deve essere annotata con quanto segue:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo, il componente può essere esportato autonomamente, utilizzando `.model` selettore e `.json` estensione.

Inoltre, questo specifica che la classe Sling Model può essere adattata nel `ComponentExporter` interfaccia.

>[!NOTE]
>
>Le annotazioni Jackson non vengono solitamente specificate a livello di classe Sling Model, ma a livello di interfaccia Model. In questo modo, l’esportazione JSON viene considerata come parte dell’API del componente.

>[!NOTE]
>
>La `ExporterConstants` e `ComponentExporter` le lezioni vengono da `com.adobe.cq.export.json` pacchetto.

### Utilizzo di più selettori {#multiple-selectors}

Sebbene non sia un caso d’uso standard, è possibile configurare più selettori in aggiunta al `model` selettore.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Tuttavia, in tal caso, `model` Il selettore deve essere il primo selettore e l&#39;estensione deve essere `.json`.

## Annotare l’interfaccia del modello Sling {#annotate-the-sling-model-interface}

Per essere presi in considerazione dal framework JSON Exporter, l&#39;interfaccia Model dovrebbe implementare il `ComponentExporter` o `ContainerExporter`, nel caso di un componente contenitore).

L&#39;interfaccia del modello Sling corrispondente ( `MyComponent`) viene quindi annotata utilizzando [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come esportare (serializzato).

Per definire quali metodi devono essere serializzati, è necessario annotare correttamente l’interfaccia Model. Per impostazione predefinita, tutti i metodi che rispettano la convenzione di denominazione usuale per i getter verranno serializzati e deriveranno naturalmente i loro nomi di proprietà JSON dai nomi dei getter. Questo può essere impedito o sostituito con `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

I componenti core supportano l’esportazione JSON a partire dalla versione [1.1.0 dei componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) e può essere utilizzato come riferimento.

Per un esempio, vedi l’implementazione del modello Sling del componente di base immagine e la relativa interfaccia annotata.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-core-wcm-components su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli vedi:

* La [Argomento Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Esportatore JSON per Content Services](/help/sites-developing/json-exporter.md)
* [Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) e [Componente Frammento di contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
