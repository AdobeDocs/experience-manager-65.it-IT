---
title: Editor
description: Scopri come tornare all’Editor dell’interfaccia classica.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Editor{#editor}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica dall’editor è stata disattivata.

Per riattivare l’opzione **Apri nell’interfaccia classica** nel **Informazioni pagina** , eseguire la procedura seguente.

1. Utilizzando CRXDE Liti, individua il seguente nodo:

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

   ![apri nell’interfaccia classica, opzione da informazioni pagina](assets/syui-03-2019-02-27-15-19-48.png)
