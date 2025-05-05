---
title: Abilitazione dell’esportazione JSON per un componente
description: I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 6%

---

# Abilitazione dell’esportazione JSON per un componente{#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.

## Panoramica {#overview}

L&#39;esportazione JSON è basata su [modelli Sling](https://sling.apache.org/documentation/bundles/models.html) e sul framework [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che a sua volta si basa su [annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, segui questi due passaggi per abilitare l’esportazione JSON su qualsiasi componente.

* [Definire un modello Sling per il componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotare l’interfaccia del modello Sling](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Innanzitutto, è necessario definire un modello Sling per il componente.

>[!NOTE]
>
>Per un esempio di utilizzo dei modelli Sling, vedere [Sviluppo di Sling Model Exporters in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=it).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo è possibile esportare il componente da solo, utilizzando il selettore `.model` e l&#39;estensione `.json`.

Inoltre, questo specifica che la classe del modello Sling può essere adattata nell&#39;interfaccia `ComponentExporter`.

>[!NOTE]
>
>Le annotazioni Jackson non vengono specificate a livello di classe del modello Sling, ma piuttosto a livello di interfaccia del modello. In questo modo, l’esportazione JSON deve essere considerata parte dell’API del componente.

>[!NOTE]
>
>Le classi `ExporterConstants` e `ComponentExporter` provengono dal bundle `com.adobe.cq.export.json`.

### Utilizzo di più selettori {#multiple-selectors}

Anche se non è un caso d&#39;uso standard, è possibile configurare più selettori oltre al selettore `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

In questo caso, tuttavia, il selettore `model` deve essere il primo e l&#39;estensione deve essere `.json`.

## Annotare l’interfaccia del modello Sling {#annotate-the-sling-model-interface}

Affinché il framework di esportazione JSON possa tenerne conto, l&#39;interfaccia del modello deve implementare l&#39;interfaccia `ComponentExporter` (o `ContainerExporter`, se è presente un componente contenitore).

L&#39;interfaccia del modello Sling corrispondente ( `MyComponent`) verrà quindi annotata utilizzando [annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come deve essere esportata (serializzata).

L&#39;interfaccia del modello deve essere annotata correttamente per definire quali metodi devono essere serializzati. Per impostazione predefinita, tutti i metodi che rispettano la consueta convenzione di denominazione per i getter vengono serializzati e derivano i loro nomi di proprietà JSON naturalmente dai nomi dei getter. Questa operazione può essere impedita o ignorata utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

I Componenti core hanno supportato l&#39;esportazione JSON dalla versione [1.1.0 dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e possono essere utilizzati come riferimento.

Ad esempio, consulta l’implementazione del modello Sling del componente core Immagine e la relativa interfaccia con annotazioni.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-core-wcm-components su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentazione correlata {#related-documentation}

Per ulteriori dettagli, vedi:

* L&#39;argomento [Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/it/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Esportatore JSON per Content Services](/help/sites-developing/json-exporter.md)
* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente frammento di contenuto](https://helpx.adobe.com/it/experience-manager/core-components/using/content-fragment-component.html)
