---
title: Configurare l’editor Rich Text per più editor locali.
description: Potete creare più editor interni nel  Adobe Experience Manager configurando Editor Rich Text.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---


# Configurare più editor interni {#configure-multiple-in-place-editors}

Potete configurare l’editor Rich Text in  Adobe Experience Manager in modo che contenga più editor interni. Una volta configurato, potete selezionare il contenuto appropriato e aprire l&#39;editor appropriato.

![Un editor locale specifico](assets/rte-inplace-editor.png)

## Configurare più editor {#configure-multiple-editors}

Per abilitare più editor interni, la struttura di un tipo di `cq:InplaceEditingConfig` nodo è stata migliorata con la definizione del tipo di `cq:ChildEditorConfig` nodo.

Ad esempio:

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Per configurare più editor, effettuate le seguenti operazioni:

1. Sul nodo `cq:inplaceEditing` (di tipo `cq:InplaceEditingConfig`) definire le seguenti proprietà:

   * Nome:`editorType`
   * Tipo: `String`
   * Valore: `hybrid`

1. Sotto questo nodo, crea un nodo:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. Sotto `cq:childEditors` il nodo, crea un nodo per ciascun editor locale:

   * Nome: Il nome di ciascun nodo è il nome della proprietà che rappresenta, come nel caso delle destinazioni di rilascio. Ad esempio `image` e `text`.
   * Tipo: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Esiste una correlazione tra le destinazioni di rilascio definite e gli editor secondari. Il nome del `cq:ChildEditorConfig` nodo viene considerato come ID destinazione di rilascio, da utilizzare come parametro per l&#39;editor secondario selezionato. Se la sottoarea modificabile non ha una destinazione di rilascio, ad esempio, in un componente di testo, il nome dell’editor secondario viene comunque considerato come un ID per identificare l’area modificabile corrispondente.

1. In ciascuno di questi nodi (`cq:ChildEditorConfig`) definire le proprietà:

   * Nome: `type`.
   * Valore: il nome dell’editor locale registrato; ad esempio `image` e `text`.

   * Nome: `title`.
   * Valore: Titolo visualizzato nell’elenco di selezione dei componenti degli editor disponibili. Ad esempio `Image` e `Text`.

### Configurazione aggiuntiva per gli editor Rich Text {#additional-configuration-for-rich-text-editors}

La configurazione per più editor Rich Text è leggermente diversa, in quanto potete configurare ogni singola istanza RTE separatamente. Per informazioni dettagliate, consultate [configurare l&#39;Editor](/help/sites-administering/rich-text-editor.md)Rich Text. Per fare in modo che più editor Rich Text creino una configurazione per ogni editor Rich Text in loco. Adobe consiglia di creare il nuovo nodo di configurazione in `cq:InplaceEditingConfig` quanto ogni singolo editor Rich Text può avere una configurazione diversa. Sotto il nuovo nodo creare ogni singola configurazione RTE.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Tuttavia, per l’editor Rich Text, la `configPath` proprietà è supportata quando nel componente è presente una sola istanza dell’editor di testo (area secondaria modificabile). Questo utilizzo di `configPath` è fornito per supportare la compatibilità con le precedenti finestre di dialogo dell’interfaccia utente del componente.

>[!CAUTION]
>
>Non assegnare al nodo di configurazione RTE il nome `config`. In caso contrario, le configurazioni dell’editor Rich Text sono disponibili solo per gli amministratori e non per gli utenti del gruppo `content-author`.

## Code samples {#code-samples}

Il codice di questa pagina è disponibile nel progetto [aem-authoring-hybridedit su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Potete scaricare l&#39;intero progetto come [archivio](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)ZIP.

## Aggiunta di un editor locale {#add-an-in-place-editor}

Per informazioni generali sull’aggiunta di un editor locale, consultate il documento [sulla personalizzazione dell’authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)delle pagine.

>[!MORELIKETHIS]
>
>* [Configurare l’editor Rich Text in  Experience Manager](/help/sites-administering/rich-text-editor.md).

