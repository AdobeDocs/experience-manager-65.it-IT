---
title: Admin Console
description: Scopri come utilizzare gli Admin Console disponibili in Adobe Experience Manager.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Admin Console{#admin-consoles}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica tramite le console di amministrazione è disabilitata. Di conseguenza, le icone a comparsa visualizzate quando si muovono sopra determinate icone della console, consentendo l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell&#39;interfaccia classica in `/libs/cq/core/content/nav` può essere riattivata singolarmente in modo che l&#39;opzione **Interfaccia classica** venga nuovamente visualizzata sull&#39;icona della console quando viene spostata.

In questo esempio, stai riattivando l’interfaccia classica per la console Sites.

1. Utilizzando CRXDE Lite, individua il nodo corrispondente all’Admin Console per il quale desideri riabilitare l’interfaccia classica. Si trovano in:

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

1. L&#39;opzione **Interfaccia classica** è nuovamente disponibile come opzione a comparsa nell&#39;Admin Console.

   ![opzione popover classica dell&#39;interfaccia utente](assets/syui-01-2019-02-27-15-16-55.png)

Ripeti questi passaggi per ogni console per la quale desideri riabilitare l’accesso alla versione dell’interfaccia classica.
