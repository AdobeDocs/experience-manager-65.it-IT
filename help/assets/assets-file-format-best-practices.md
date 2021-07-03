---
title: Best practice per l’elaborazione dei formati di file supportati
description: Best practice per elaborare i vari tipi di file supportati utilizzando [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Gestione delle risorse, Strumenti per sviluppatori
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Best practice per i formati di file delle risorse {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] supporta numerose librerie di formati di file proprietari e di terze parti per soddisfare diversi requisiti di supporto dei file da parte degli utenti. Le librerie di Adobi supportate includono [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Inoltre, [!DNL Experience Manager Assets] supporta librerie di terze parti, inclusi [!DNL ImageMagick], [!DNL TwelveMonkeys] e così via.

Per i formati di file supportati, consulta [Formati supportati da Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Se utilizzi [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l’Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Rivolgiti al rappresentante dell’Assistenza clienti Adobe per implementare queste best practice per la distribuzione AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbero non essere in grado di elaborare file PSB ad alta risoluzione con più di 3000 x 23000 pixel.

## [!DNL Adobe Camera Raw] libreria {#adobe-camera-raw-library}

Per prestazioni ottimali, Adobe consiglia di utilizzare la libreria [!DNL Adobe Camera Raw] per i file RAW e DNG.

[!DNL Adobe Camera Raw] La libreria supporta il profilo colore CMYK come input. Tuttavia, genera l&#39;output nello spazio colore RGB e supporta l&#39;output solo in formato JPEG. Non mantiene lo spazio colore del file di origine (ad esempio CMYK) nelle miniature.

Per ulteriori informazioni, consulta [Supporto Camera Raw](/help/assets/camera-raw.md).

## Libreria Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Per risultati migliori, Adobe consiglia di utilizzare la libreria Adobe PDF Rasterizer per i seguenti file:

* File PDF pesanti e ad uso intensivo di contenuti
* File AI con miniature non generate come predefiniti
* Per i file AI con colori SPOT (PMS)

Miniature e anteprime generate con PDF Rasterizer sono di qualità migliore rispetto all’output raster preconfigurato. La libreria Adobe PDF Rasterizer non supporta alcuna conversione del colore. Indipendentemente dallo spazio colore del file PDF di origine, Adobe PDF Rasterizer genera solo output RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe consiglia di utilizzare [!DNL Adobe InDesign Server] per estrarre rappresentazioni specifiche di [!DNL Adobe InDesign], ad esempio IDML e HTML. Per ulteriori informazioni, consulta [Aggiunta di risorse di Experience Manager come riferimenti in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera e distribuisce più varianti di contenuti avanzati in tempo reale attraverso la rete globale, scalabile e ottimizzata per le prestazioni. Fornisce esperienze di visualizzazione interattive e semplifica il processo di gestione delle campagne digitali. Per informazioni dettagliate sull&#39;abilitazione di [!DNL Dynamic Media], consulta [Configurazione di Dynamic Media](/help/assets/config-dynamic.md).

Attualmente, [!DNL Dynamic Media] può supportare video fino a 15 GB di contenuto per file.

## Libreria ImageMagick {#imagemagick-library}

Adobe consiglia di utilizzare la libreria ImageMagick nei seguenti scenari:

* Per generare rappresentazioni di miniature per i file EPS.
* Per conservare le informazioni sul profilo immagine.
* Per preservare la trasparenza.
* Per elaborare i file PSD e PSB.

Per informazioni su come impostare la libreria [!DNL ImageMagick] in [!DNL Experience Manager], consulta [Utilizzo di ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Per un utilizzo ottimale, consulta [Best practice per la configurazione di ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Libreria di transcodifica delle immagini {#image-transcoding-library}

La libreria di transcodifica delle immagini di Adobe è una soluzione di elaborazione delle immagini che esegue funzioni di base per la gestione delle immagini, tra cui codifica, transcodifica, ricampionamento, ridimensionamento e così via.

La libreria di transcodifica delle immagini supporta i seguenti tipi MIME:

* JPG/JPEG
* PNG (8 bit e 16 bit)
* GIF
* BMP
* TIFF/TIFF compresso (a parte i TIFF a 32 bit e i PTiff).
* ICO
* ICN

Per informazioni dettagliate, consulta [Imaging Transcoding Library](/help/assets/imaging-transcoding-library.md).
