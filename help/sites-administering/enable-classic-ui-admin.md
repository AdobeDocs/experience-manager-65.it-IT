---
title: 'Admin Console '
seo-title: 'Admin Console '
description: Scoprite come utilizzare gli Admin Console  disponibili in AEM.
seo-description: Scoprite come utilizzare gli Admin Console  disponibili in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---


# Admin Console {#admin-consoles}

Per impostazione predefinita, è stata disattivata la possibilità di passare all’interfaccia classica tramite le console di amministrazione. Pertanto, le icone a comparsa visualizzate quando si passa il mouse su determinate icone della console e si consente l’accesso all’interfaccia classica, non vengono più visualizzate.

Ogni console con una versione dell&#39;interfaccia classica in `/libs/cq/core/content/nav` può essere riattivata singolarmente, in modo che l&#39;opzione **Interfaccia classica** venga nuovamente visualizzata sopra l&#39;icona della console quando viene spostata.

In questo esempio viene riattivata l’interfaccia classica per la console Siti.

1. Utilizzando CRXDE Lite, trovate il nodo corrispondente alla console di amministrazione per il quale desiderate riabilitare l’interfaccia classica. Sono disponibili in:

   `/libs/cq/core/content/nav`

   Esempio

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Selezionate il nodo corrispondente alla console per la quale desiderate riattivare l’interfaccia classica. Ad esempio, riattiveremo l’interfaccia classica per la console Siti.

   `/libs/cq/core/content/nav/sites`

1. Create una sovrapposizione utilizzando l&#39;opzione **Overlay Node**; ad esempio:

   * **Percorso**: `/apps/cq/core/content/nav/sites`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi** di nodo: active (seleziona la casella di controllo)

1. Aggiungete la seguente proprietà booleana al nodo sovrapposto:

   `enableDesktopOnly = {Boolean}true`

1. L&#39;opzione **Interfaccia classica** è nuovamente disponibile come opzione del puntatore nella console di amministrazione.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Ripetete questi passaggi per ogni console per la quale desiderate riattivare l’accesso alla versione dell’interfaccia classica.