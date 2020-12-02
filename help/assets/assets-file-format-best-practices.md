---
title: Procedure ottimali per l'elaborazione dei formati di file supportati
description: Procedure ottimali per l'elaborazione dei vari tipi di file supportati utilizzando [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Best practice per il formato dei file delle risorse {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] supporta numerose librerie di formati di file proprietari e di terze parti per soddisfare diversi requisiti di supporto dei file da parte degli utenti. Le librerie di Adobi  supportate includono [!DNL Adobe Camera Raw], Gibson,  Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Inoltre, [!DNL Experience Manager Assets] supporta librerie di terze parti, inclusi [!DNL ImageMagick], [!DNL TwelveMonkeys] e così via.

Per i formati di file supportati, consultate [Formati supportati di risorse](/help/assets/assets-formats.md).

>[!TIP]
>
>Se utilizzi [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l&#39;Assistenza clienti  Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Consultate  rappresentante dell&#39;Assistenza clienti di Adobe per implementare queste best practice per l&#39;implementazione di AMS e scegliere i migliori strumenti e modelli possibili per  formati proprietari  Adobe. [!DNL Experience Manager] potrebbero non essere in grado di elaborare file PSB ad alta risoluzione con oltre 30000 x 23000 pixel.

## [!DNL Adobe Camera Raw] library  {#adobe-camera-raw-library}

Per ottenere prestazioni ottimali,  Adobe consiglia di utilizzare la libreria [!DNL Adobe Camera Raw] per i file RAW e DNG.

[!DNL Adobe Camera Raw] la libreria supporta il profilo colore CMYK come input. Tuttavia, genera l’output in spazio colore RGB e supporta solo l’output in formato JPEG. Non mantiene lo spazio colore del file di origine (ad esempio CMYK) nelle miniature.

Per ulteriori informazioni, vedere [Supporto Camera Raw](/help/assets/camera-raw.md).

##  libreria Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Per risultati ottimali,  Adobe consiglia di utilizzare la libreria  Adobe PDF Rasterizer per i file seguenti:

* File PDF pesanti e ricchi di contenuti
* File AI con miniature non generate
* Per i file AI con colori SPOT (PMS)

Le miniature e le anteprime generate con PDF Rasterizer sono di qualità migliore rispetto all’output raster fornito con Scene7. La libreria  Adobe PDF Rasterizer non supporta la conversione del colorspace. A prescindere dallo spazio colore del file PDF di origine,  Adobe PDF Rasterizer genera solo l’output RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

 Adobe consiglia di utilizzare [!DNL Adobe InDesign Server] per estrarre rappresentazioni specifiche di [!DNL Adobe InDesign], come IDML e HTML. Per ulteriori informazioni, consultate [Aggiunta  risorse di Experience Manager come riferimenti in  Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera e offre diverse varianti di contenuti avanzati in tempo reale attraverso la rete globale, scalabile e ottimizzata per le prestazioni. Offre esperienze di visualizzazione interattive e semplifica il processo di gestione delle campagne digitali. Per informazioni dettagliate sull&#39;abilitazione di [!DNL Dynamic Media], vedere [Configurazione di contenuti multimediali dinamici](/help/assets/config-dynamic.md).

Attualmente, [!DNL Dynamic Media] supporta i video fino a 15 GB di contenuto per file.

## Libreria ImageMagick {#imagemagick-library}

 Adobe consiglia di utilizzare la libreria ImageMagick nei seguenti scenari:

* Per generare rappresentazioni delle miniature per i file EPS.
* Per mantenere le informazioni sul profilo immagine.
* Per mantenere la trasparenza.
* Per elaborare i file PSD e PSB.

Per informazioni su come impostare la libreria [!DNL ImageMagick] in [!DNL Experience Manager], vedere [Utilizzo di ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Per un utilizzo ottimale, consultate [Best practice per la configurazione di ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Libreria di transcodifica delle immagini {#image-transcoding-library}

La libreria  Adobe Imaging Transcoding è una soluzione per l’elaborazione delle immagini che esegue le funzioni di base per la gestione delle immagini, tra cui la codifica delle immagini, la transcodifica, il ricampionamento, il ridimensionamento e così via.

La libreria di transcodifica per immagini supporta i seguenti tipi MIME:

* JPG/JPEG
* PNG (8 bit e 16 bit)
* GIF
* BMP
* TIFF/TIFF compresso (a parte i formati a 32 bit e PTiff).
* ICO
* ICN

Per informazioni dettagliate, consultate [Libreria di transcodifica delle immagini](/help/assets/imaging-transcoding-library.md).
