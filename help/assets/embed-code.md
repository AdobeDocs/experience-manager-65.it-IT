---
title: Incorporazione di un visualizzatore video o immagine per contenuti multimediali dinamici in una pagina Web
description: Scopri come incorporare video o immagini Dynamic Media in una pagina Web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 572b856fbdd1ef916f8f897ba86ddefafee324fc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 21%

---


# Incorporazione di video per file multimediali dinamici, visualizzatori immagini o visualizzatori dimensionali in una pagina Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Potete incorporare gli URL solo se _non_ utilizzate AEM come WCM. Se utilizzate AEM come WCM, [potete aggiungere le risorse direttamente sulla pagina.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>Il codice da incorporare è disponibile per la copia solo dopo aver pubblicato la risorsa selezionata. Dovete inoltre pubblicare il predefinito per visualizzatori o per immagini.
>
>Consultate [Pubblicazione delle risorse](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

**Per incorporare il visualizzatore per video o immagini dinamici in una pagina Web**

1. Andate alla risorsa video o immagine *pubblicata* di cui desiderate copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consultate [Pubblicazione delle risorse.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, selezionate il menu a discesa e toccate **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, toccate il nome di un predefinito per visualizzatori. Il predefinito per visualizzatori viene applicato alla risorsa.
1. Toccate **[!UICONTROL Incorpora]**.
1. Nella finestra di dialogo **[!UICONTROL Incorpora codice]** , copiate l’intero codice negli Appunti, quindi toccate **[!UICONTROL Chiudi]**.
1. Incollate il codice da incorporare nelle pagine Web.

## Utilizzo di HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, migliorando la risposta e i tempi di caricamento.

Per informazioni dettagliate sull’utilizzo di HTTP/2 con l’account per contenuti multimediali dinamici, consultate Consegna di contenuti [](http2.md) HTTP2.
