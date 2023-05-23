---
title: Abilitazione dell’esportazione JSON per un componente
seo-title: Enabling JSON Export for a Component
description: I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---

# Abilitazione dell’esportazione JSON per un componente{#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.

## Panoramica {#overview}

L’esportazione JSON si basa su [Modelli Sling](https://sling.apache.org/documentation/bundles/models.html), e sul [Esportatore modello Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che si basa su [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling per esportare JSON. Pertanto, dovrai seguire questi due passaggi per abilitare l’esportazione JSON su qualsiasi componente.

* [Definire un modello Sling per il componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Annotare l’interfaccia del modello Sling](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Innanzitutto, è necessario definire un modello Sling per il componente.

>[!NOTE]
>
>Per un esempio di utilizzo dei modelli Sling, consulta l’articolo [Sviluppo di esportatori di modelli Sling nell’AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo il componente può essere esportato da solo utilizzando `.model` e il `.json` estensione.

Inoltre, questo specifica che la classe del modello Sling può essere adattata in `ComponentExporter` di rete.

>[!NOTE]
>
>Le annotazioni Jackson di solito non sono specificate a livello di classe di modello Sling, ma piuttosto a livello di interfaccia di modello. In questo modo, l’esportazione JSON deve essere considerata parte dell’API del componente.

>[!NOTE]
>
>Il `ExporterConstants` e `ComponentExporter` le classi provengono da `com.adobe.cq.export.json` pacchetto.

### Utilizzo di più selettori {#multiple-selectors}

Anche se non è un caso di utilizzo standard, è possibile configurare più selettori oltre al `model` selettore.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Tuttavia, in tal caso, `model` il selettore deve essere il primo selettore e l’estensione deve essere `.json`.

## Annotare l’interfaccia del modello Sling {#annotate-the-sling-model-interface}

Affinché il framework di esportazione JSON possa tenere conto di, l’interfaccia modello deve implementare `ComponentExporter` interfaccia (o `ContainerExporter`, nel caso di un componente contenitore).

Interfaccia corrispondente del modello Sling ( `MyComponent`) verrebbe quindi annotato utilizzando [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire la modalità di esportazione (serializzata).

L’interfaccia del modello deve essere annotata correttamente per definire quali metodi serializzare. Per impostazione predefinita, tutti i metodi che rispettano la consueta convenzione di denominazione per i getter vengono serializzati e derivano i nomi delle proprietà JSON naturalmente dai nomi dei getter. Questo può essere impedito o sovrascritto utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

I Componenti core hanno supportato l’esportazione JSON dalla versione [1.1.0 dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e possono essere utilizzati come riferimento.

Ad esempio, consulta l’implementazione del modello Sling del componente core Immagine e la relativa interfaccia con annotazioni.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-core-wcm-components su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, cfr.:

* Il [Argomento Frammenti di contenuto nella guida utente di Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-authoring/content-fragments.md)
* [Esportatore JSON per Content Services](/help/sites-developing/json-exporter.md)
* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente Frammento di contenuto](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
