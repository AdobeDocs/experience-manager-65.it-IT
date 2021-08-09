---
title: Distribuzione di immagini ottimizzate per un sito reattivo
description: Come utilizzare la funzione di codice reattivo per fornire immagini ottimizzate
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
feature: Gestione risorse
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 10%

---

# Fornire immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizza la funzione Codice reattivo quando desideri condividere il codice per il servizio reattivo con il tuo sviluppatore web. Puoi copiare il codice reattivo (**[!UICONTROL RESS]**) negli appunti per condividerlo con lo sviluppatore web.

Questa funzione ha senso utilizzare se il sito web si trova su un sito web WCM di terze parti. Tuttavia, se il sito web si trova in Adobe Experience Manager, un server di immagini offsite esegue il rendering dell&#39;immagine e la fornisce alla pagina web.

Vedere anche [Incorporare il visualizzatore video in una pagina Web](embed-code.md).

Consulta anche [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

**Per fornire immagini ottimizzate per un sito reattivo:**

1. Passa all’immagine per la quale desideri fornire codice reattivo e, nel menu a discesa, seleziona **[!UICONTROL Rendering]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >Dynamic Media - La modalità ibrida richiede la pubblicazione di predefiniti per immagini; Dynamic Media - La modalità Scene7 pubblica automaticamente i predefiniti per immagini.

1. Selezionare **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Nella finestra di dialogo **[!UICONTROL Incorpora immagine reattiva]** , seleziona e copia il testo del codice reattivo e incollalo nel sito Web per accedere alla risorsa reattiva.
1. Modifica i punti di interruzione predefiniti nel codice di incorporamento in modo che corrispondano ai punti di interruzione del sito web reattivo, direttamente nel codice. Inoltre, prova le diverse risoluzioni immagine fornite in diversi punti di interruzione della pagina.

## Utilizzo di HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media è supportata tramite HTTP/2, che fornisce tempi di risposta e caricamento migliori.

Per informazioni dettagliate su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media, consulta [Distribuzione di contenuti HTTP2](http2.md) .
