---
title: Configurare l’editor Rich Text per più editor locali.
description: Crea più editor locali in Adobe Experience Manager configurando l’Editor Rich Text.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Configurare più editor locali {#configure-multiple-in-place-editors}

È possibile configurare l’Editor Rich Text in Adobe Experience Manager in modo che disponga di più editor locali. Una volta configurata, puoi selezionare il contenuto appropriato e aprire l’editor appropriato.

![Un editor locale specifico](assets/rte-inplace-editor.png)

## Configurare più editor {#configure-multiple-editors}

Per abilitare più editor locali, la struttura di un `cq:InplaceEditingConfig` il tipo di nodo è stato migliorato con la definizione di `cq:ChildEditorConfig` tipo di nodo.

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

Per configurare più editor, eseguire la procedura seguente:

1. Sul nodo `cq:inplaceEditing` (di tipo `cq:InplaceEditingConfig`) definisci le seguenti proprietà:

   * Nome:`editorType`
   * Tipo: `String`
   * Valore: `hybrid`

1. Crea un nodo sotto questo nodo:

   * Nome: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. Sotto `cq:childEditors` , crea un nodo per ciascun editor locale:

   * Nome: il nome di ciascun nodo è il nome della proprietà che rappresenta, come nel caso delle destinazioni di rilascio. Ad esempio: `image` e `text`.
   * Tipo: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Esiste una correlazione tra le destinazioni di rilascio definite e gli editor secondari. Il nome del `cq:ChildEditorConfig` viene considerato come ID della destinazione di rilascio, da utilizzare come parametro per l’editor secondario selezionato. Se la sottoarea modificabile non ha una destinazione di rilascio, ad esempio, in un componente di testo, il nome dell’editor figlio viene comunque considerato un ID per identificare l’area modificabile corrispondente.

1. Su ciascuno di questi nodi (`cq:ChildEditorConfig`) definisci le proprietà:

   * Nome: `type`.
   * Valore: nome dell’editor locale registrato; ad esempio, `image` e `text`.

   * Nome: `title`.
   * Valore: il titolo visualizzato nell’elenco di selezione dei componenti degli editor disponibili. Ad esempio: `Image` e `Text`.

### Configurazione aggiuntiva per gli editor Rich Text {#additional-configuration-for-rich-text-editors}

La configurazione di più editor Rich Text è leggermente diversa, in quanto è possibile configurare separatamente ogni singola istanza di RTE. Per ulteriori informazioni, consulta [configurare l’editor Rich Text](/help/sites-administering/rich-text-editor.md). Per disporre di più editor Rich Text, creare una configurazione per ogni editor Rich Text locale. L’Adobe consiglia di creare il nuovo nodo di configurazione in `cq:InplaceEditingConfig` in quanto ogni singolo editor Rich Text può avere una configurazione diversa. Nel nuovo nodo creare ogni singola configurazione dell’editor Rich Text.

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
>Tuttavia, per l’editor Rich Text, `configPath` questa proprietà è supportata quando nel componente è presente una sola istanza dell’editor di testo (sottoarea modificabile). Questo utilizzo di `configPath` viene fornito per supportare la compatibilità con le versioni precedenti delle finestre di dialogo dell’interfaccia utente del componente.

>[!CAUTION]
>
>Non denominare il nodo di configurazione dell’editor Rich Text come `config`. In caso contrario, le configurazioni dell’editor Rich Text sono disponibili solo per gli amministratori e non per gli utenti del gruppo `content-author`.

## Esempi di codice {#code-samples}

Puoi trovare il codice di questa pagina su [progetto aem-authoring-hybrideditors su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Puoi scaricare il progetto completo come [un archivio ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Aggiungere un editor locale {#add-an-in-place-editor}

Per informazioni generali sull’aggiunta di un editor locale, consulta il documento [personalizzare l’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configurare l’editor Rich Text in Experience Manager](/help/sites-administering/rich-text-editor.md).
