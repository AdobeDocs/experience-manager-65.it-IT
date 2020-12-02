---
title: Incorporamento di un visualizzatore video o immagine per contenuti multimediali dinamici in una pagina Web
description: Scopri come incorporare video o immagini Dynamic Media in una pagina Web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 21%

---


# Incorporazione di video per file multimediali dinamici, visualizzatore immagini o visualizzatore dimensionale in una pagina Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Gli URL vengono incorporati solo se _non_ vengono utilizzati AEM come WCM. Se utilizzi AEM come WCM, [aggiungi le risorse direttamente sulla pagina.](adding-dynamic-media-assets-to-pages.md)

Vedere [Collegamento di URL all&#39;applicazione Web.](linking-urls-to-yourwebapplication.md)

Vedere [Distribuzione di immagini ottimizzate per un sito reattivo.](responsive-site.md)

>[!NOTE]
>
>Il codice da incorporare è disponibile per la copia solo dopo aver pubblicato la risorsa selezionata. Dovete inoltre pubblicare il predefinito per visualizzatori o per immagini.
>
>Consultate [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).
>
>Consultate [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consultate [Pubblicazione di predefiniti per immagini](managing-image-presets.md#publishing-image-presets).

**Per incorporare il visualizzatore per video o immagini dinamici in una pagina Web**

1. Andate alla risorsa video o immagine *pubblicata* di cui desiderate copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Vedere [Pubblicazione delle risorse.](publishing-dynamicmedia-assets.md)

   Consultate [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).

   Consultate [Pubblicazione di predefiniti per immagini](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, selezionate il menu a discesa e toccate **[!UICONTROL Visualizzatori.]**
1. Nella barra a sinistra, toccate il nome di un predefinito per visualizzatori. Il predefinito per visualizzatori viene applicato alla risorsa.
1. Toccare **[!UICONTROL Incorpora.]**
1. Nella finestra di dialogo **[!UICONTROL Incorpora codice]**, copiare l&#39;intero codice negli Appunti, quindi toccare **[!UICONTROL Chiudi.]**
1. Incollate il codice da incorporare nelle pagine Web.

## Utilizzo di HTTP/2 per distribuire le risorse multimediali dinamiche {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, migliorando la risposta e i tempi di caricamento.

Per informazioni dettagliate sull&#39;utilizzo di HTTP/2 con l&#39;account Dynamic Media, consultate [HTTP2 Delivery of Content](http2.md) (Distribuzione di contenuti HTTP2&lt;a1/>).
