---
title: Configurazione di più editor interni
seo-title: Configurazione di più editor interni
description: È possibile configurare il componente in modo che abbia più editor locali
seo-description: È possibile configurare il componente in modo che abbia più editor locali
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Configurazione di più editor interni{#configuring-multiple-in-place-editors}

È possibile configurare il componente in modo che disponga di più editor interni nell’interfaccia touch.

Una volta configurato, potete selezionare il contenuto appropriato e aprire l&#39;editor appropriato. Esempio:

![chlimage_1-8](assets/chlimage_1-8a.png)

## Configurazione di più editor {#configuring-multiple-editors}

Per abilitare più editor interni, la struttura di un tipo di `cq:InplaceEditingConfig` nodo è stata migliorata con la definizione del tipo di `cq:ChildEditorConfig` nodo.

Esempio:

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Per configurare più editor:

1. Sul nodo `cq:inplaceEditing` (di tipo `cq:InplaceEditingConfig`) definire la proprietà:

   * Nome:`editorType`
   * Tipo: `String`
   * Valore: `hybrid`

1. Sotto questo nodo creare un nuovo nodo:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. Sotto il `cq:childEditors` nodo create un nuovo nodo per ciascun editor locale:

   * Nome: il nome di ciascun nodo deve essere il nome della proprietà che rappresenta (come con le destinazioni di rilascio). Esempio, `image`, `text`.
   * Tipo: cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >Esiste una correlazione tra le destinazioni di rilascio definite e gli editor secondari. Il nome del `cq:ChildEditorConfig` nodo verrà considerato come ID destinazione di rilascio, da utilizzare come parametro per l&#39;editor secondario selezionato. Se l’area secondaria modificabile non ha una destinazione di rilascio (ad esempio, come con un componente di testo), il nome dell’editor secondario viene comunque considerato come un ID per identificare l’area modificabile corrispondente.

1. In ciascuno di questi nodi ( `cq:ChildEditorConfig`) definire le proprietà:

   * Nome: `type`
   * Valore: nome dell’editor locale registrato; ad esempio `image`, `text`

   * Nome: `title`
   * Valore: il titolo che si desidera visualizzare nell’elenco di selezione dei componenti (degli editor disponibili); ad esempio `Image`, `Text`

### Configurazione aggiuntiva per gli editor Rich Text {#additional-configuration-for-rich-text-editors}

La configurazione per più editor Rich Text è leggermente diversa, in quanto potete configurare ogni singola istanza RTE separatamente.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Configurazione dell’editor](/help/sites-administering/rich-text-editor.md)Rich Text.

Per avere più editor Rich Text è necessaria una configurazione per ogni editor Rich Text in-place:

* In `cq:InplaceEditingConfig` Definisci un `config` nodo.

   * Sotto il `config` nodo definire ogni singola configurazione RTE.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Si consiglia di definire il `config` nodo sotto `cq:InplaceEditingConfig` in quanto ogni singolo editor Rich Text può avere una configurazione diversa.
>
>Tuttavia, per l’editor Rich Text, la `configPath` proprietà è supportata quando nel componente è presente una sola istanza dell’editor di testo (area secondaria modificabile). Questo utilizzo `configPath` viene fornito per supportare la compatibilità con le precedenti finestre di dialogo dell’interfaccia utente del componente.

## Esempi di codice {#code-samples}

**CODICE SU GITHUB**

Puoi trovare il codice di questa pagina su GitHub

* [Open aem authoring-hybridedit project on GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## Aggiunta di un editor locale {#adding-an-in-place-editor}

Per informazioni generali sull’aggiunta di un editor locale, consultate il documento [Personalizzazione dell’authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)delle pagine.
