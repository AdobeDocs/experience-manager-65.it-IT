---
title: Personalizza ed estendi [!DNL Assets]
description: Scopri come personalizzare ed estendere Asset Share e Asset Editor, che offre agli utenti un’interfaccia e un set di funzionalità personalizzati.
contentOwner: AG
role: Developer
feature: Developer Tools
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---


# Personalizza ed estendi [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor è il punto di accesso principale che gli utenti di un sito web Adobe Enterprise Manager utilizzeranno per trovare, visualizzare e manipolare le risorse digitali nell’archivio.

In qualità di sviluppatore [!DNL Experience Manager], puoi personalizzare ed estendere Asset Editor in diversi modi, presentando agli utenti un’interfaccia e un set di funzionalità specifici.

È possibile personalizzare o migliorare i seguenti aspetti della funzionalità:

* [Estendi editor risorse](asseteditorx.md)
* [Estendi ricerca risorse](searchx.md)
* [Elabora risorse utilizzando gestori di contenuti multimediali e flussi di lavoro](media-handlers.md)
* [Integrare le risorse con il flusso di attività](extending-activity-stream.md)
* [Sviluppo proxy risorse](proxy.md)
* [Best practice per configurare ImageMagick](best-practices-for-imagemagick.md)

## Personalizza l&#39;aspetto {#customizing-the-look-and-feel}

Sono personalizzabili i seguenti aspetti dell’aspetto e del comportamento di Asset Editor:

* Logo: Puoi aggiungere all’interfaccia il logo della tua organizzazione.
* Colori e caratteri: È possibile modificare i colori e i font utilizzati nell’interfaccia.
* Codice HTML: Per una personalizzazione più completa è possibile modificare il codice HTML sottostante che definisce le interfacce.

## Personalizzare le rappresentazioni {#customizing-renditions}

Nella terminologia [!DNL Experience Manager Assets] un rendering è il modulo in cui viene presentata una risorsa. In generale, una particolare risorsa può avere più rappresentazioni. Ad esempio, l’immagine a colori completi può avere un rendering nelle dimensioni originali, un altro in una dimensione ridotta e un altro in scala di grigi.

Le rappresentazioni disponibili in una particolare risorsa possono essere personalizzate e possono essere create nuove rappresentazioni.
