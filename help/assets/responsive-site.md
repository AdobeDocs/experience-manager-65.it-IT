---
title: Distribuzione di immagini ottimizzate per un sito reattivo
description: Come utilizzare la funzione di codice reattivo per fornire immagini ottimizzate
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 12%

---


# Distribuzione di immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizzate la funzione di codice reattivo quando desiderate condividere il codice per il servizio reattivo con il vostro sviluppatore Web. Copiate negli Appunti il codice reattivo (**[!UICONTROL RESS]**) in modo da poterlo condividere con lo sviluppatore Web.

Questa funzione è utile se il sito Web si trova su un sito Web WCM di terze parti. Tuttavia, se il sito Web è AEM, un server immagini esterno esegue il rendering dell’immagine e la trasmette alla pagina Web.

Consultate anche [Incorporamento del visualizzatore video in una pagina Web.](embed-code.md)

Vedere anche [Collegamento di URL all&#39;applicazione Web.](linking-urls-to-yourwebapplication.md)

**Per fornire immagini ottimizzate per un sito** reattivo:

1. Andate all&#39;immagine per la quale desiderate fornire il codice reattivo e, nel menu a discesa, toccate **[!UICONTROL Renditions]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >Contenuti multimediali dinamici - La modalità ibrida richiede la pubblicazione di predefiniti per immagini; Contenuti multimediali dinamici - La modalità Scene7 pubblica automaticamente i predefiniti per immagini.

1. Toccare **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Nella finestra di dialogo **[!UICONTROL Incorpora immagine reattiva]**, selezionate e copiate il testo del codice reattivo, quindi incollatelo nel sito Web per accedere alla risorsa reattiva.
1. Modificate i punti di interruzione predefiniti nel codice da incorporare in modo che corrispondano a quelli del sito Web reattivo direttamente nel codice. Inoltre, provate le diverse risoluzioni immagine trasmesse in punti di interruzione di pagina diversi.

## Utilizzo di HTTP/2 per distribuire le risorse multimediali dinamiche {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media è supportata mediante HTTP/2, che fornisce una risposta e tempi di caricamento migliori.

Per informazioni dettagliate sull&#39;utilizzo di HTTP/2 con l&#39;account Dynamic Media, consultate [HTTP2 Delivery of Content](http2.md) (Distribuzione di contenuti HTTP2&lt;a1/>).
