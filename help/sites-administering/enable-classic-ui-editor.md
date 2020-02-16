---
title: Editor
seo-title: Editor
description: Scoprite come tornare all’editor dell’interfaccia classica.
seo-description: Scoprite come tornare all’editor dell’interfaccia classica.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# Editor{#editor}

Per impostazione predefinita, è stata disattivata la possibilità di passare all’interfaccia classica dall’editor.

Per riattivare l’opzione **Apri nell’interfaccia** classica nel menu Informazioni **** pagina, attenetevi alla seguente procedura.

1. Utilizzando CRXDE Lite, individuare il seguente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Esempio

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Create una sovrapposizione utilizzando l’opzione **Overlay Node** (Nodo sovrapposizione); ad esempio:

   * **Percorso**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi** di nodo: active (seleziona la casella di controllo)

1. Aggiungete la seguente proprietà di testo con più valori al nodo sovrapposto:

   `sling:hideProperties = ["granite:hidden"]`

1. L’opzione **Apri nell’interfaccia** classica è nuovamente disponibile nel menu Informazioni **** pagina durante la modifica delle pagine.

   ![](assets/syui-03-2019-02-27-15-19-48.png)