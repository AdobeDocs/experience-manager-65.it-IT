---
title: Admin Console
seo-title: Admin Consoles
description: Scopri come utilizzare gli Admin Console disponibili nell’AEM.
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: 729e5eb99b0c14f3d2fd8c3f4ec636f7fb52124f
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# Admin Console{#admin-consoles}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica tramite le console di amministrazione è stata disattivata. Di conseguenza, le icone a comparsa visualizzate quando si muovono sopra determinate icone della console, consentendo l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell’interfaccia classica in `/libs/cq/core/content/nav` possono essere riattivate singolarmente in modo che **Interfaccia classica** L’opzione viene visualizzata di nuovo sopra l’icona della console quando viene spostata.

In questo esempio viene riattivata l’interfaccia classica per la console Sites.

1. Utilizzando CRXDE Lite, trova il nodo corrispondente all’Admin Console per il quale desideri riabilitare l’interfaccia classica. Si trovano in:

   `/libs/cq/core/content/nav`

   Per esempio

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleziona il nodo corrispondente alla console per la quale desideri riabilitare l’interfaccia classica. Nel nostro esempio, riattiveremo l’interfaccia utente classica per la console Sites.

   `/libs/cq/core/content/nav/sites`

1. Creare una sovrapposizione utilizzando **Sovrapponi nodo** opzione; ad esempio:

   * **Percorso**: `/apps/cq/core/content/nav/sites`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (seleziona la casella di controllo)

1. Aggiungi la seguente proprietà booleana al nodo sovrapposto:

   `enableDesktopOnly = {Boolean}true`

1. Il **Interfaccia classica** l’opzione è nuovamente disponibile come opzione a comparsa in admin console.

   ![opzione popover dell’interfaccia classica](assets/syui-01-2019-02-27-15-16-55.png)

Ripeti questi passaggi per ogni console per la quale desideri riabilitare l’accesso alla versione dell’interfaccia classica.
