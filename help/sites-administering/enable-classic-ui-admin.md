---
title: Admin Console
description: Scopri come utilizzare le Admin Console disponibili in Adobe Experience Manager.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
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
source-wordcount: '238'
ht-degree: 2%
---

# Admin Console{#admin-consoles}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica tramite le console di amministrazione è disabilitata. Di conseguenza, le icone a comparsa visualizzate quando si muovono sopra determinate icone della console, consentendo l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell&#39;interfaccia classica in `/libs/cq/core/content/nav` può essere riattivata singolarmente in modo che l&#39;opzione **Interfaccia classica** venga nuovamente visualizzata sull&#39;icona della console quando viene spostata.

In questo esempio, stai riattivando l’interfaccia classica per la console Sites.

1. Utilizzando CRXDE Lite, trova il nodo corrispondente all’Admin Console per il quale desideri riabilitare l’interfaccia classica. Si trovano in:

   `/libs/cq/core/content/nav`

   Ad esempio

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleziona il nodo corrispondente alla console per la quale desideri riabilitare l’interfaccia classica. Per questo esempio, stai riattivando l’interfaccia utente classica per la console Sites.

   `/libs/cq/core/content/nav/sites`

1. Crea una sovrapposizione utilizzando l&#39;opzione **Sovrapponi nodo**, ad esempio:

   * **Percorso**: `/apps/cq/core/content/nav/sites`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (selezionare la casella di controllo)

1. Aggiungi la seguente proprietà booleana al nodo sovrapposto:

   `enableDesktopOnly = {Boolean}true`

1. L&#39;opzione **Interfaccia classica** è nuovamente disponibile come opzione a comparsa in Admin Console.

   ![opzione popover classica dell&#39;interfaccia utente](assets/syui-01-2019-02-27-15-16-55.png)

Ripeti questi passaggi per ogni console per la quale desideri riabilitare l’accesso alla versione dell’interfaccia classica.
