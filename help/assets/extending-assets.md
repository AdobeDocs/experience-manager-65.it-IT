---
title: Personalizzare ed estendere [!DNL Assets]
description: Scopri come personalizzare ed estendere Condivisione risorse e Editor risorse, con un’interfaccia e un set di funzionalità specifiche per gli utenti.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Personalizzare ed estendere [!DNL Assets] {#customizing-and-extending-assets}

L’Editor risorse è il punto di accesso principale che gli utenti di un Adobe di sito Web Enterprise Manager utilizzeranno per trovare, visualizzare e manipolare le risorse digitali nell’archivio.

Come un [!DNL Experience Manager] sviluppatore, puoi personalizzare ed estendere Asset Editor in diversi modi, presentando agli utenti un’interfaccia e un set di funzionalità specifiche.

È possibile personalizzare o migliorare i seguenti aspetti della funzionalità:

* [Estendi editor risorse](asseteditorx.md)
* [Estendi ricerca risorse](searchx.md)
* [Elaborare risorse utilizzando gestori di file multimediali e flussi di lavoro](media-handlers.md)
* [Integrare le risorse con il flusso di attività](extending-activity-stream.md)
* [Sviluppo proxy delle risorse](proxy.md)
* [Best practice per configurare ImageMagick](best-practices-for-imagemagick.md)

## Personalizzare l&#39;aspetto {#customizing-the-look-and-feel}

Sono personalizzabili i seguenti aspetti dell’Editor risorse:

* Logo: puoi aggiungere il logo della tua organizzazione all’interfaccia.
* Colori e font: è possibile modificare i colori e i font utilizzati nell’interfaccia.
* Codice HTML: per una personalizzazione più dettagliata è possibile modificare il codice HTML sottostante che definisce le interfacce.

## Personalizzare le rappresentazioni {#customizing-renditions}

In entrata [!DNL Experience Manager Assets] terminologia per rappresentazione si intende la forma in cui viene presentata una risorsa. In generale, una particolare risorsa può avere più rappresentazioni. Ad esempio, un’immagine a colori può avere una rappresentazione nelle dimensioni originali, un’altra con dimensioni ridotte e un’altra con dimensioni ridotte e convertita in scala di grigio.

È possibile personalizzare le rappresentazioni in cui è disponibile una particolare risorsa e crearne di nuove.
