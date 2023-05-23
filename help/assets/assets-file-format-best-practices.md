---
title: Best practice per l’elaborazione dei formati di file supportati
description: Best practice per elaborare i vari tipi di file supportati tramite [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 3%

---

# Best practice per il formato dei file delle risorse {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] supporta numerose librerie di formati di file proprietarie e di terze parti per soddisfare i diversi requisiti di supporto dei file degli utenti. Le librerie di Adobi supportate includono: [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Inoltre, [!DNL Experience Manager Assets] supporta librerie di terze parti, tra cui [!DNL ImageMagick], [!DNL TwelveMonkeys]e così via.

Per i formati di file supportati, vedi [Formati di risorse supportati](/help/assets/assets-formats.md).

>[!TIP]
>
>Se sta usando [!DNL Experience Manager] in Adobe Managed Services (AMS), contatta l’Assistenza clienti di Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Collabora con il rappresentante dell’Assistenza clienti di Adobe per implementare queste best practice per la tua implementazione di AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbe non elaborare file PSB ad altissima risoluzione con una risoluzione superiore a 30000x23000 pixel.

## [!DNL Adobe Camera Raw] libreria {#adobe-camera-raw-library}

Per prestazioni ottimali, l’Adobe consiglia di utilizzare [!DNL Adobe Camera Raw] libreria per file RAW e DNG.

[!DNL Adobe Camera Raw] La libreria supporta il profilo colore CMYK come input. Tuttavia, genera l&#39;output in RGB colorspace e supporta l&#39;output solo in formato JPEG. Non mantiene lo spazio colore del file di origine (ad esempio CMYK) nelle miniature.

Per ulteriori informazioni, consulta [Supporto Camera Raw](/help/assets/camera-raw.md).

## Libreria Rasterizer di Adobe PDF {#adobe-pdf-rasterizer-library}

Per ottenere risultati ottimali, l’Adobe consiglia di utilizzare la libreria Rasterizer di Adobe PDF per i seguenti file:

* File PDF pesanti e ad alta intensità di contenuti
* File AI con miniature non generati come tali
* Per i file AI con colori SPOT (PMS)

Le miniature e le anteprime generate con PDF Rasterizer offrono una qualità migliore rispetto all&#39;output raster predefinito. La libreria di Adobe PDF Rasterizer non supporta alcuna conversione di spazio colore. Indipendentemente dallo spazio colore del file PDF di origine, Adobe PDF Rasterizer genera solo output RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

L’Adobe consiglia di utilizzare [!DNL Adobe InDesign Server] per estrarre [!DNL Adobe InDesign]rappresentazioni specifiche di, ad esempio IDML e HTML. Per ulteriori informazioni, consulta [Aggiunta di risorse Experience Manager come riferimenti in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] consente di generare e distribuire in tempo reale più varianti di rich content attraverso una rete globale, scalabile e ottimizzata per le prestazioni. Offre esperienze di visualizzazione interattive e semplifica il processo di gestione delle campagne digitali. Per informazioni dettagliate sull’abilitazione di [!DNL Dynamic Media], vedi [Configurazione di Dynamic Media](/help/assets/config-dynamic.md).

Attualmente, [!DNL Dynamic Media] può supportare video fino a 15 GB di contenuto per file.

## Libreria ImageMagick {#imagemagick-library}

L&#39;Adobe consiglia di utilizzare la libreria ImageMagick nei seguenti scenari:

* Per generare copie trasformate di miniature per i file EPS.
* Per conservare le informazioni del profilo immagine.
* Per mantenere la trasparenza.
* Per elaborare file PSD e PSB.

Per sapere come impostare [!DNL ImageMagick] libreria in [!DNL Experience Manager], vedi [Utilizzo di ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Per un utilizzo ottimale, consulta [Best practice per la configurazione di ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Libreria trascodifica immagini {#image-transcoding-library}

Adobe Imaging Transcoding Library è una soluzione di elaborazione delle immagini che esegue funzioni di base per la gestione delle immagini, tra cui codifica, transcodifica, ricampionamento, ridimensionamento e così via.

La libreria di trascodifica immagini supporta i seguenti tipi MIME:

* JPG/JPEG
* PNG (8 bit e 16 bit)
* GIF
* BMP
* TIFF/Compressed TIFF (a parte Tiff e PTiiff a 32 bit).
* ICO
* ICN

Per ulteriori informazioni, consulta [Libreria trascodifica immagini](/help/assets/imaging-transcoding-library.md).
