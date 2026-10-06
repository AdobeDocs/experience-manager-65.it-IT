---
title: Incorpora il visualizzatore Dynamic Media Video, Immagine o Dimensionale in una pagina web
description: Scopri come incorporare video Dynamic Media, immagini o immagini 3D in una pagina web
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 20%
---
# Incorpora il visualizzatore Dynamic Media Video, Immagine o Dimensionale in una pagina web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilizza la funzione **[!UICONTROL Codice da incorporare]** per riprodurre il video o visualizzare una risorsa incorporata in una pagina web. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Codice da incorporare]**.

Gli URL vengono incorporati solo se *non* utilizza Adobe Experience Manager come WCM. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente nella pagina](adding-dynamic-media-assets-to-pages.md).

Consulta [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consulta [Distribuire immagini ottimizzate per un sito reattivo](responsive-site.md).

>[!NOTE]
>
>Il codice da incorporare è disponibile per la copia solo dopo la pubblicazione della risorsa selezionata. Inoltre, devi pubblicare anche il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).
>
>Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

**Per incorporare il video Dynamic Media, il visualizzatore di immagini o il visualizzatore dimensionale in una pagina Web:**

1. Passa alla risorsa video o immagine *pubblicata* di cui desideri copiare il codice da incorporare.

   Il codice da incorporare è disponibile per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito per immagini.

   Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

   Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. Nella barra a sinistra, seleziona il menu a discesa e seleziona **[!UICONTROL Visualizzatori]**.
1. Nella barra a sinistra, seleziona un nome per il predefinito visualizzatore. Il predefinito visualizzatore viene applicato alla risorsa.
1. Seleziona **[!UICONTROL Incorpora]**.
1. Nella finestra di dialogo **[!UICONTROL Incorpora codice]**, copiare l&#39;intero codice negli Appunti, quindi selezionare **[!UICONTROL Chiudi]**.
1. Incolla il codice da incorporare nelle pagine web.

## Utilizzo di HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, il che offre tempi di risposta e caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con l&#39;account Dynamic Media.
