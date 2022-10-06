---
title: Admin Console
seo-title: Admin Consoles
description: Scopri come utilizzare gli Admin Console disponibili in AEM.
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# Admin Console{#admin-consoles}

Per impostazione predefinita, è stata disabilitata la possibilità di passare all’interfaccia classica tramite le console di amministrazione. Pertanto, le icone a comparsa visualizzate quando si passa il mouse su alcune icone della console e si consente l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell’interfaccia classica in `/libs/cq/core/content/nav` può essere riattivato singolarmente in modo che il **Interfaccia classica** torna nuovamente a essere visualizzata sull’icona della console quando viene spostata.

In questo esempio, riattiveremo l’interfaccia classica per la console Sites .

1. Utilizzando CRXDE Lite, trova il nodo corrispondente alla console di amministrazione per cui desideri riabilitare l’interfaccia classica. Si trovano in:

   `/libs/cq/core/content/nav`

   Esempio

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Seleziona il nodo corrispondente alla console per la quale desideri riattivare l’interfaccia classica. Ad esempio, riattiveremo l’interfaccia classica per la console Sites .

   `/libs/cq/core/content/nav/sites`

1. Crea una sovrapposizione utilizzando il **Nodo di sovrapposizione** opzione; ad esempio:

   * **Percorso**: `/apps/cq/core/content/nav/sites`
   * **Posizione sovrapposizione**: `/apps/`
   * **Tipi di nodo corrispondenti**: attivo (seleziona la casella di controllo)

1. Aggiungi la seguente proprietà booleana al nodo sovrapposto:

   `enableDesktopOnly = {Boolean}true`

1. La **Interfaccia classica** è nuovamente disponibile come opzione di pover in admin console.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Ripeti questi passaggi per ogni console per la quale desideri riabilitare l’accesso alla versione dell’interfaccia classica.
