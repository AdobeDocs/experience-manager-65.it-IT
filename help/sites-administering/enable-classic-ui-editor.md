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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '110'
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
