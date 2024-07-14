---
title: Editor
description: Scopri come tornare all’Editor dell’interfaccia classica.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Editor{#editor}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica dall’editor è stata disattivata.

Per riattivare l&#39;opzione **Apri nell&#39;interfaccia classica** nel menu **Informazioni pagina**, eseguire la procedura seguente.

1. Utilizzando CRXDE Lite, individua il seguente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Ad esempio

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Crea una sovrapposizione utilizzando l&#39;opzione **Sovrapponi nodo**, ad esempio:

   * **Percorso**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (selezionare la casella di controllo)

1. Aggiungi la seguente proprietà di testo con più valori al nodo sovrapposto:

   `sling:hideProperties = ["granite:hidden"]`

1. L&#39;opzione **Apri nell&#39;interfaccia classica** è nuovamente disponibile nel menu **Informazioni pagina** durante la modifica delle pagine.

   ![apri nell&#39;interfaccia classica, opzione da informazioni pagina](assets/syui-03-2019-02-27-15-19-48.png)
