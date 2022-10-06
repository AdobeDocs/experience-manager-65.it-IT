---
title: Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web
description: Scopri come incorporare video, immagini o immagini 3D di Dynamic Media in una pagina web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 21%

---

# Incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Incorpora codice]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora codice]**.

Incorpora gli URL solo se lo sei *not* utilizzo di Adobe Experience Manager come WCM. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente sulla pagina](adding-dynamic-media-assets-to-pages.md).

Vedi [Collegare gli URL all’applicazione Web](linking-urls-to-yourwebapplication.md).

Vedi [Fornire immagini ottimizzate per un sito reattivo](responsive-site.md).

>[!NOTE]
>
>Il codice di incorporamento non è disponibile per la copia finché non avrai pubblicato la risorsa selezionata. Inoltre, devi pubblicare il predefinito visualizzatore o il predefinito immagine.
>
>Vedi [Pubblicare le risorse](publishing-dynamicmedia-assets.md).
>
>Vedi [Pubblicare i predefiniti per visualizzatori](managing-viewer-presets.md#publishing-viewer-presets).
>
>Vedi [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

**Per incorporare un visualizzatore video, immagine o dimensionale di Dynamic Media in una pagina web:**

1. Passa a *pubblicato* risorsa video o immagine di cui desideri copiare il codice da incorporare.

   Il codice è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Vedi [Pubblicare le risorse](publishing-dynamicmedia-assets.md).

   Vedi [Pubblicare i predefiniti per visualizzatori](managing-viewer-presets.md#publishing-viewer-presets).

   Vedi [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, seleziona il menu a discesa e seleziona **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, seleziona un nome di predefinito visualizzatore. Il predefinito visualizzatore viene applicato alla risorsa.
1. Seleziona **[!UICONTROL Incorpora]**.
1. In **[!UICONTROL Codice di incorporamento]** copia l&#39;intero codice negli Appunti, quindi seleziona **[!UICONTROL Chiudi]**.
1. Incolla il codice di incorporamento nelle pagine web.

## Utilizzo di HTTP/2 per fornire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media può ora avvenire tramite HTTP/2, garantendo tempi di risposta e caricamento migliori.

Vedi [Distribuzione di contenuti HTTP2](http2.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media.
