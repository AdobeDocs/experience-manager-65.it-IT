---
title: Abilitazione dell'esportazione JSON per un componente
seo-title: Abilitazione dell'esportazione JSON per un componente
description: I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.
seo-description: I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 4%

---


# Abilitazione dell&#39;esportazione JSON per un componente{#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.

## Panoramica {#overview}

L&#39;esportazione JSON si basa su [Sling Models](https://sling.apache.org/documentation/bundles/models.html) e sul framework [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che si basa su [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, per abilitare l’esportazione JSON su qualsiasi componente dovrete seguire questi due passaggi.

* [Definire un modello Sling per il componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotazione dell&#39;interfaccia Sling Model](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Per il componente deve essere definito innanzitutto un modello Sling.

>[!NOTE]
>
>Per un esempio di utilizzo di Sling Models, vedere l&#39;articolo [Developing Sling Model Exporter in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Questo garantisce che il componente possa essere esportato autonomamente, utilizzando il selettore `.model` e l&#39;estensione `.json`.

Inoltre, questo specifica che la classe Sling Model può essere adattata all&#39;interfaccia `ComponentExporter`.

>[!NOTE]
>
>Le annotazioni Jackson non vengono in genere specificate a livello di classe Sling Model, ma a livello di interfaccia Model. In questo modo, assicuratevi che l’esportazione JSON sia considerata parte dell’API del componente.

>[!NOTE]
>
>Le classi `ExporterConstants` e `ComponentExporter` provengono dal pacchetto `com.adobe.cq.export.json`.

### Utilizzo di più selettori {#multiple-selectors}

Sebbene non sia un caso d&#39;uso standard, è possibile configurare più selettori oltre al selettore `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

In tal caso, tuttavia, il selettore `model` deve essere il primo selettore e l&#39;estensione deve essere `.json`.

## Annota dell&#39;interfaccia del modello Sling {#annotate-the-sling-model-interface}

Per essere presa in considerazione dal framework JSON Exporter, l&#39;interfaccia Model deve implementare l&#39;interfaccia `ComponentExporter` (o `ContainerExporter`, nel caso di un componente contenitore).

L&#39;interfaccia del modello Sling corrispondente ( `MyComponent`) verrà quindi annotata utilizzando le annotazioni di [Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come esportare (serializzato).

L&#39;interfaccia Model deve essere annotata correttamente per definire i metodi da serializzare. Per impostazione predefinita, tutti i metodi che rispettano le consuete convenzioni di denominazione per i getter saranno serializzati e deriveranno naturalmente i nomi delle loro proprietà JSON dai nomi dei getter. Questo può essere impedito o sostituito utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

I componenti core supportano l&#39;esportazione JSON dalla versione [1.1.0 dei componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) e possono essere utilizzati come riferimento.

Per un esempio, consultate Implementazione del modello Sling del componente Image Core e la relativa interfaccia annotata.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Open aem-core-wcm-components project on GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, consulta:

* Argomento [Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Esportatore JSON per Content Services](/help/sites-developing/json-exporter.md)
* [Componenti ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) di base e componente Frammento di  [contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

