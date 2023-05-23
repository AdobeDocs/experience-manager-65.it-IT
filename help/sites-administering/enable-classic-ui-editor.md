---
title: Editor
seo-title: Editor
description: Scopri come tornare all’Editor dell’interfaccia classica.
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 7%

---

# Editor{#editor}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica dall’editor è stata disattivata.

Per riattivare l’opzione **Apri nell’interfaccia classica** nel **Informazioni pagina** , eseguire la procedura seguente.

1. Utilizzando CRXDE Lite, individua il seguente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Per esempio

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Creare una sovrapposizione utilizzando **Sovrapponi nodo** opzione; ad esempio:

   * **Percorso**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (seleziona la casella di controllo)

1. Aggiungi la seguente proprietà di testo con più valori al nodo sovrapposto:

   `sling:hideProperties = ["granite:hidden"]`

1. Il **Apri nell’interfaccia classica** è nuovamente disponibile nella **Informazioni pagina** durante la modifica delle pagine.

   ![](assets/syui-03-2019-02-27-15-19-48.png)
