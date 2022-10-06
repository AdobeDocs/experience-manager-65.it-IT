---
title: Personalizza ed estendi [!DNL Assets]
description: Scopri come personalizzare ed estendere Asset Share e Asset Editor, che offre agli utenti un’interfaccia e un set di funzionalità personalizzati.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Personalizza ed estendi [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor è il punto di accesso principale che gli utenti di un sito web Adobe Enterprise Manager utilizzeranno per trovare, visualizzare e manipolare le risorse digitali nell’archivio.

Come [!DNL Experience Manager] per sviluppatori, puoi personalizzare ed estendere Asset Editor in diversi modi, presentando agli utenti un’interfaccia e un set di funzionalità specifici.

È possibile personalizzare o migliorare i seguenti aspetti della funzionalità:

* [Estendi editor risorse](asseteditorx.md)
* [Estendi ricerca risorse](searchx.md)
* [Elabora risorse utilizzando gestori di contenuti multimediali e flussi di lavoro](media-handlers.md)
* [Integrare le risorse con il flusso di attività](extending-activity-stream.md)
* [Sviluppo proxy risorse](proxy.md)
* [Best practice per configurare ImageMagick](best-practices-for-imagemagick.md)

## Personalizzare l’aspetto {#customizing-the-look-and-feel}

Sono personalizzabili i seguenti aspetti dell’aspetto e del comportamento di Asset Editor:

* Logo: Puoi aggiungere all’interfaccia il logo della tua organizzazione.
* Colori e caratteri: È possibile modificare i colori e i font utilizzati nell’interfaccia.
* Codice HTML: Per una personalizzazione più completa è possibile modificare il codice HTML sottostante che definisce le interfacce.

## Personalizzare le rappresentazioni {#customizing-renditions}

In [!DNL Experience Manager Assets] la terminologia di un rendering è il modulo in cui viene presentata una risorsa. In generale, una particolare risorsa può avere più rappresentazioni. Ad esempio, l’immagine a colori completi può avere un rendering nelle dimensioni originali, un altro in una dimensione ridotta e un altro in scala di grigi.

Le rappresentazioni disponibili in una particolare risorsa possono essere personalizzate e possono essere create nuove rappresentazioni.
