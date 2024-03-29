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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Admin Console{#admin-consoles}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica tramite le console di amministrazione è disabilitata. Di conseguenza, le icone a comparsa visualizzate quando si muovono sopra determinate icone della console, consentendo l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell’interfaccia classica in `/libs/cq/core/content/nav` possono essere riattivate singolarmente in modo che **Interfaccia classica** L’opzione viene visualizzata di nuovo sopra l’icona della console quando viene spostata.

In questo esempio, stai riattivando l’interfaccia classica per la console Sites.

1. Utilizzando CRXDE Liti, individua il nodo corrispondente all’Admin Console per il quale desideri riabilitare l’interfaccia classica. Si trovano in:

   `/libs/cq/core/content/nav`

   Per esempio

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleziona il nodo corrispondente alla console per la quale desideri riabilitare l’interfaccia classica. Per questo esempio, stai riattivando l’interfaccia utente classica per la console Sites.

   `/libs/cq/core/content/nav/sites`

1. Creare una sovrapposizione utilizzando **Sovrapponi nodo** opzione; ad esempio:

   * **Percorso**: `/apps/cq/core/content/nav/sites`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (seleziona la casella di controllo)

1. Aggiungi la seguente proprietà booleana al nodo sovrapposto:

   `enableDesktopOnly = {Boolean}true`

1. Il **Interfaccia classica** L’opzione è nuovamente disponibile come opzione a comparsa nell’Admin Console.

   ![opzione popover dell’interfaccia classica](assets/syui-01-2019-02-27-15-16-55.png)

Ripeti questi passaggi per ogni console per la quale desideri riabilitare l’accesso alla versione dell’interfaccia classica.
