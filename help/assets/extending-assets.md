---
title: Personalizza ed estendi [!DNL Adobe Experience Manager Assets].
description: Scoprite come personalizzare ed estendere l’Editor risorse e condivisione di risorse, che offre agli utenti un’interfaccia e un set di funzionalità specifici.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Personalizzare ed estendere [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor è il principale punto di accesso che gli utenti di un sito Web Enterprise Manager  utilizzeranno per trovare, visualizzare e manipolare le risorse digitali presenti nell’archivio.

In qualità di [!DNL Experience Manager] sviluppatore, potete personalizzare ed estendere l’Editor risorse in diversi modi, presentando agli utenti un’interfaccia e un set di funzionalità specifici.

È possibile personalizzare o migliorare i seguenti aspetti della funzionalità:

* [Estendi editor risorse](asseteditorx.md)
* [Estendi ricerca risorse](searchx.md)
* [Elabora risorse tramite gestori e flussi di lavoro](media-handlers.md)
* [Integrare le risorse con il flusso di attività](extending-activity-stream.md)
* [Sviluppo proxy delle risorse](proxy.md)
* [Procedure ottimali per la configurazione di ImageMagick](best-practices-for-imagemagick.md)

## Personalizzare l’aspetto {#customizing-the-look-and-feel}

È possibile personalizzare i seguenti aspetti dell’aspetto e del comportamento dell’Editor risorse:

* Logo: È possibile aggiungere il logo aziendale all&#39;interfaccia.
* Colori e font: È possibile modificare i colori e i font utilizzati nell&#39;interfaccia.
* Codice HTML: Per una personalizzazione più completa, potete modificare il codice HTML sottostante che definisce le interfacce.

## Personalizzare le rappresentazioni {#customizing-renditions}

Nella [!DNL Experience Manager Assets] terminologia una rappresentazione è il modulo in cui viene presentata una risorsa. In generale, una particolare risorsa può avere più rappresentazioni. Ad esempio, l’immagine a colori interi può avere una rappresentazione nelle dimensioni originali, un’altra in una dimensione ridotta e un’altra in scala di grigio.

Le rappresentazioni in cui è disponibile una particolare risorsa possono essere personalizzate e create nuove rappresentazioni.
