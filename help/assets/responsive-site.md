---
title: Fornire immagini ottimizzate per un sito reattivo
description: Come utilizzare la funzione del codice reattivo per fornire immagini ottimizzate
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 13%

---

# Distribuzione di immagini ottimizzate per un sito reattivo {#delivering-optimized-images-for-a-responsive-site}

Utilizza la funzione Codice reattivo per condividere il codice per il servizio reattivo con il tuo sviluppatore web. Copia il responsive (**[!UICONTROL RESS]**) negli Appunti, in modo da poterlo condividere con lo sviluppatore web.

Questa funzione è utile se il sito web si trova su un WCM di terze parti. Tuttavia, se il tuo sito web si trova su Adobe Experience Manager, un server di immagini fuori sede esegue il rendering dell’immagine e la fornisce alla pagina web.

Vedi anche [Incorporare il Visualizzatore video in una pagina Web](embed-code.md).

Vedi anche [Collegare gli URL all’applicazione web](linking-urls-to-yourwebapplication.md).

**Per fornire immagini ottimizzate per un sito reattivo:**

1. Passa all’immagine per la quale desideri fornire il codice reattivo e, nel menu a discesa, seleziona **[!UICONTROL Rappresentazioni]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleziona un predefinito per immagini reattive. Vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >Per poter rendere disponibili i pulsanti **[!UICONTROL URL]** o **[!UICONTROL RESS]**, la risorsa selezionata *e* il predefinito immagine o il predefinito visualizzatore devono essere pubblicati.
   >
   >Dynamic Medie - La modalità ibrida richiede di pubblicare predefiniti per immagini; Dynamic Medie - la modalità Scene7 pubblica automaticamente i predefiniti per immagini.

1. Seleziona **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. In **[!UICONTROL Incorpora immagine reattiva]** , seleziona e copia il testo del codice reattivo e incollalo nel sito web per accedere alla risorsa reattiva.
1. Modifica i punti di interruzione predefiniti nel codice di incorporamento in modo che corrispondano ai punti di interruzione del sito web dinamico, direttamente nel codice. Inoltre, verifica le diverse risoluzioni dell’immagine distribuite in diversi punti di interruzione della pagina.

## Utilizza HTTP/2 per distribuire le risorse Dynamic Medie {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Medie è supportata tramite HTTP/2, che fornisce tempi di risposta e caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Medie.
