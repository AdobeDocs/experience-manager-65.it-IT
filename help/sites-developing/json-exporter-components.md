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
source-git-commit: 10072609bc371b5f2dce425e90e583f14f96e371
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---


# Abilitazione dell&#39;esportazione JSON per un componente{#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.

## Panoramica {#overview}

JSON Export si basa su modelli [](https://sling.apache.org/documentation/bundles/models.html)Sling e sul framework [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che a sua volta si basa sulle annotazioni [Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, per abilitare l’esportazione JSON su qualsiasi componente dovrete seguire questi due passaggi.

* [Definire un modello Sling per il componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotazione dell&#39;interfaccia Sling Model](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Per il componente deve essere definito innanzitutto un modello Sling.

>[!NOTE]
>
>Per un esempio di utilizzo di Sling Models, consultate l’articolo [Sviluppo di Sling Model Exporter in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo il componente può essere esportato in modo indipendente, utilizzando il `.model` selettore e l’ `.json` estensione.

Inoltre, questo specifica che la classe Sling Model può essere adattata all&#39; `ComponentExporter` interfaccia.

>[!NOTE]
>
>Le annotazioni Jackson non vengono in genere specificate a livello di classe Sling Model, ma a livello di interfaccia Model. In questo modo, assicuratevi che l’esportazione JSON sia considerata parte dell’API del componente.

>[!NOTE]
>
>Le `ExporterConstants` e `ComponentExporter` le classi provengono dal `com.adobe.cq.export.json` bundle.

### Utilizzo di più selettori {#multiple-selectors}

Sebbene non sia un caso d’uso standard, è possibile configurare più selettori oltre al `model` selettore.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

In tal caso, tuttavia, il `model` selettore deve essere il primo e l&#39;estensione deve essere `.json`.

## Annotazione dell&#39;interfaccia del modello Sling {#annotate-the-sling-model-interface}

Per essere presa in considerazione dal framework JSON Exporter, l&#39;interfaccia Model dovrebbe implementare l&#39; `ComponentExporter` interfaccia (o `ContainerExporter`, nel caso di un componente contenitore).

La corrispondente interfaccia Sling Model ( `MyComponent`) viene quindi annotata utilizzando le annotazioni [Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come deve essere esportata (serializzata).

L&#39;interfaccia Model deve essere annotata correttamente per definire i metodi da serializzare. Per impostazione predefinita, tutti i metodi che rispettano le consuete convenzioni di denominazione per i getter saranno serializzati e deriveranno naturalmente i nomi delle loro proprietà JSON dai nomi dei getter. Questo può essere impedito o ignorato utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

I componenti core hanno supportato l’esportazione JSON dalla release [1.1.0 dei componenti](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) core e possono essere utilizzati come riferimento.

Per un esempio, consultate Implementazione del modello Sling del componente Image Core e la relativa interfaccia annotata.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Open aem-core-wcm-components project on GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Related Documentation {#related-documentation}

Per maggiori dettagli, consulta:

* Argomento Frammenti di [contenuto nella guida utente delle risorse](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Esportatore JSON per Content Services](/help/sites-developing/json-exporter.md)
* [Componenti](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) di base e componente Frammento di [contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

