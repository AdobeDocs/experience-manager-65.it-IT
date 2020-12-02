---
title: Formati di file supportati e tipi MIME
description: Formati di file e tipi MIME supportati da [!DNL Assets] and [!DNL Dynamic Media] e funzionalità supportate per ciascun formato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: eaff176bf3ffc197607b8eb39b15c1e945927f8e
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 10%

---


# Formati supportati in [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] supporta un&#39;ampia gamma di formati di file e ogni funzionalità supporta vari tipi MIME. Per integrare [!DNL Assets] con altre soluzioni di gestione delle risorse digitali (DAM) conformi agli standard e con il software desktop, utilizzate   [!DNL Extensible Metadata Platform] (XMP).

Utilizzate la legenda per comprendere il livello di supporto.

| Livello di supporto | Descrizione |
| :-----------: | ------------------------------ |
| AND | Supportato |
| * | Supportato con le funzioni del componente aggiuntivo |
| - | Non applicabile |

## Formati immagine raster supportati in [!DNL Experience Manager] {#supported-raster-image-formats}

I formati di immagine raster supportati in [!DNL Assets] sono:

| Formato | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione delle miniature | Modifica | Write-back metadati | Approfondimenti |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | AND | AND | AND | AND | AND | AND | AND |
| GIF | AND | AND | AND | AND | AND | - | AND |
| TIFF | AND | AND | AND | AND | - | AND | AND |
| JPEG | AND | AND | AND | AND | AND | AND | AND |
| BMP | AND | AND | AND | AND | AND | - | AND |
| PNM | AND | AND | - | - | - | - | AND |
| PGM | AND | AND | - | - | - | - | AND |
| PBM | AND | AND | - | - | - | - | AND |
| PPM | AND | AND | - | - | - | - | AND |
| PSD | AND | AND | AND | AND | - | - | AND |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | AND | AND | AND | - | AND | - |
| PICT | - | - | - | - | - | - | AND |
| PSB | AND | AND | AND | AND | - | - | - |

† L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da  Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere l’immagine effettiva o meno.

I formati di immagine raster supportati in [!DNL Dynamic Media] sono:

| Formato | Upload<br> (formato di ingresso) | Crea<br> immagine<br> predefinito<br> (formato di output) | Rendering di Preview<br> dynamic<br> | Distribuzione di rappresentazioni dinamiche<br><br> | Download della rappresentazione<br> dinamica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | AND | AND | AND | AND | AND |
| GIF | AND | AND | AND | AND | AND |
| TIFF | AND | AND | AND | AND | AND |
| JPEG | AND | AND | AND | AND | AND |
| BMP | AND | - | - | - | - |
| PSD | AND | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | AND | AND | AND | AND |
| PICT | AND | - | - | - | - |

† L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da  Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere l’immagine effettiva o meno.

Oltre alle informazioni di cui sopra, considerate quanto segue:

* Il supporto per i file EPS si applica solo alle immagini raster. Ad esempio, la generazione di miniature per le immagini vettoriali EPS non è supportata per impostazione predefinita. Per aggiungere supporto, [configurare ImageMagick](best-practices-for-imagemagick.md). Per integrare strumenti di terze parti per abilitare funzionalità aggiuntive, vedere [Gestore multimediale basato su riga di comando](media-handlers.md#command-line-based-media-handler).

* La funzione di reimpostazione dei metadati funziona per il formato di file PSB quando viene aggiunta al gestore `NComm`.

* Per utilizzare [!DNL Dynamic Media] per visualizzare l&#39;anteprima e generare rappresentazioni dinamiche per i file EPS, vedere [ formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per i file EPS, la funzione di writeback dei metadati è supportata in PostScript Document Structuring Convention (Adobe PS-) versione 3.0 o successiva.

## Formati 3D supportati {#support-3d-formats}

È supportato il seguente elenco di formati 3D.

Consultate anche [Utilizzo delle risorse 3D negli elementi multimediali dinamici.](/help/assets/assets-3d.md)

| Formato | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo di accesso | Anteprima miniature | Anteprima 3D | Distribuzione di contenuti multimediali dinamici |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | AND | AND | AND |  | AND | AND | - | - |
| gLB | AND | AND | AND | AND | AND | - | AND | AND |
| gLTF | AND | AND | AND |  | AND | - | AND | - |
| OBJ | AND | AND | AND | AND | AND | - | AND | AND |
| STL | AND | AND | AND | AND | AND | - | AND | AND |
| USDz | AND | AND | AND | AND | AND | - | - | AND |

## Formati immagine raster non supportati in Contenuti multimediali dinamici {#unsupported-image-formats-dynamic-media}

Nell&#39;elenco seguente sono descritti i sottotipi di formati di file immagine raster *non* supportati negli elementi multimediali dinamici.

Vedere anche [Rilevamento di formati di file non supportati per gli elementi multimediali dinamici](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* File PNG con dimensioni blocco IDAT superiori a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Scala di grigio o Bitmap non sono supportati. Gli spazi colore DuoTone, Lab e Indexed non sono supportati.
* File PSD con una profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* file TIFF con spazio colore Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEF file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Libreria Rasterizer PDF supportata {#supported-pdf-rasterizer-library}

La libreria  Adobe PDF Rasterizer genera miniature e anteprime di alta qualità per file [!DNL Adobe Illustrator] e PDF di grandi dimensioni e ricchi di contenuti.  Adobe consiglia di utilizzare la libreria PDF Rasterizer per le seguenti operazioni:

* I file AI/PDF ad alta intensità di contenuto che richiedono molte risorse per l&#39;elaborazione.
* File AI/PDF, per i quali le miniature non vengono generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Vedere [Utilizzo di PDF Rasterizer](aem-pdf-rasterizer.md).

## Libreria di transcodifica immagini supportata {#supported-image-transcoding-library}

La libreria  Adobe Imaging Transcoding è una soluzione di elaborazione delle immagini che esegue funzioni fondamentali per la gestione delle immagini, come la codifica, la transcodifica, il ricampionamento e il ridimensionamento.

La libreria di transcodifica delle immagini supporta i tipi JPG/JPEG, PNG (8 bit e 16 bit), GIF, BMP, TIFF/Compresso TIFF (a parte file TIFF a 32 bit e PTIFF), ICO e ICN MIME.

Vedere [Libreria di transcodifica delle immagini](imaging-transcoding-library.md).

## Camera raw supportata {#supported-camera-raw}

La libreria [!DNL Adobe Camera Raw] consente a [!DNL Assets] di acquisire immagini non elaborate. Vedere [Supporto Camera Raw](camera-raw.md).

## Formati di documento [!DNL Assets] supportati {#supported-document-formats}

I formati dei documenti supportati per le funzioni di gestione delle risorse sono i seguenti:

| Formato | Archiviazione | [Gestione dei metadati](metadata.md) | Estrazione full-text<br> | [Estrazione di metadati](metadata.md) | Generazione di miniature<br> | [Estrazione di risorse secondarie](managing-linked-subassets.md) | [Write-back metadati](xmp-writeback.md) | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | AND | - | AND | AND | AND | AND | - |
| DOC | AND | AND | AND | AND | - | - | - | AND |
| DOCX | AND | AND | AND | AND | - | - | - | AND |
| ODT | AND | AND | AND | - | - | - | - | AND |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | AND | AND | AND | AND | AND | AND | AND |
| HTML | AND | AND | AND | - | - | - | - | AND |
| RTF | AND | AND | AND | - | - | - | - | AND |
| TXT | AND | AND | AND | - | - | - | - | AND |
| XLS | AND | AND | AND | - | - | - | - | AND |
| XLSX | AND | AND | AND | AND | - | - | - | AND |
| ODS | AND | AND | AND | - | - | - | - | - |
| PPT | AND | AND | AND | AND | AND | AND | - | AND |
| PPTX | AND | AND | AND | AND | AND | AND | - | AND |
| ODP | AND | AND | AND | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | AND | AND | - | AND | AND | AND | AND | - |
| PS | AND | AND | - | - | - | - | - | - |
| QXP | AND | AND | - | - | - | - | - | - |
| EPUB | AND | AND | - | AND | AND | - | - | - |

## Formati di documento supportati in Contenuti multimediali dinamici {#supported-document-formats-dynamic-media}

| Formato | Upload<br> (formato di ingresso) | Crea<br> immagine<br> predefinito<br> (formato di output) | Rendering di Preview<br> dynamic<br> | Distribuzione di rappresentazioni dinamiche<br><br> | Download della rappresentazione<br> dinamica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | AND | AND | AND | AND | AND |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | AND | - | - | - | - |

Oltre alla funzionalità di cui sopra, tenete presente quanto segue:

* Per utilizzare gli elementi multimediali dinamici per generare rappresentazioni dinamiche per i file PDF, vedere [ formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare gli elementi multimediali dinamici per visualizzare in anteprima e generare rappresentazioni dinamiche per i file AI, consultate [ formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare gli elementi multimediali dinamici per generare rappresentazioni dinamiche per i file INDD, consultate [ InDesign (INDD) file format](../assets/managing-image-presets.md#indesign-indd-file-format).

## Formati multimediali supportati {#supported-multimedia-formats}

|  | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione delle miniature | Transcodifica FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | AND | AND | - | - | * |
| MIDI | AND | AND | - | - | * |
| 3GP | AND | AND | - | - | * |
| MP3 | AND | AND | AND | - | * |
| MPG | AND | AND | - | - | * |
| OGA | AND | AND | - | - | * |
| OGG | AND | AND | - | - | * |
| RA | AND | AND | - | - | * |
| WAV | AND | AND | - | - | * |
| WMA | AND | AND | - | - | * |
| DVI | AND | AND | - | * | * |
| FLV | AND | AND | - | * | * |
| M4V | AND | AND | - | * | * |
| MPEG | AND | AND | - | * | * |
| OGV | AND | AND | - | * | * |
| MOV | AND | AND | - | * | * |
| WMV | AND | AND | - | * | * |
| SWF | AND | AND | - | - | - |

## Formati video di input supportati in Contenuti multimediali dinamici per la transcodifica {#supported-input-video-formats-for-dynamic-media-transcoding}

| Estensione dei file video | Contenitore | Codec video consigliati | Codec video non supportati |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (tutti i profili) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animazione Apple |
| FLV, F4V | Flash Adobe  | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | Interferenza A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Video Raw rosso | MJPEG 2000 | - |
| RAM, RM | RealVideo | Non supportato | Real G2 (RV 20), Real 8 (RV 30), Real 10 (RV 40) |
| FLAC | Flac nativo | Codec audio senza perdita di dati | - |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 | - |

## Formati di archivio supportati {#supported-archive-formats}

I formati di archivio supportati e l&#39;applicabilità dei flussi di lavoro DAM comuni sono descritti nella tabella seguente.

| Formati | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna di contenuti multimediali dinamici |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | AND | AND | AND | AND | AND | - |
| JAR | AND | AND | AND | AND | AND | - |
| RAR | AND | AND | AND | AND | AND | - |
| TAR | AND | AND | AND | AND | AND | - |
| ZIP | AND | AND | AND | AND | AND | AND |

## Altri formati supportati {#other-supported-formats}

Di seguito viene descritta l’applicabilità delle consuete funzionalità DAM per alcuni formati di file specifici.

| Formati | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna di contenuti multimediali dinamici |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | AND | AND | AND | AND | AND | - |
| CSS | AND | AND | AND | AND | AND | AND |
| VTT | AND | AND | AND | AND | AND | AND |
| XML | AND | AND | AND | AND | AND | AND |
| JavaScript (se configurato con un proprio dominio di consegna) | - | - | - | - | - | AND |

>[!NOTE]
>
>Il caricamento e la distribuzione di file JavaScript potrebbe non essere sicuro. Se necessario, le sovrapposizioni possono essere utilizzate per impedire agli utenti di caricare file JS.

## Tipi MIME supportati {#supported-mime-types}

Per impostazione predefinita, [!DNL Experience Manager] rileva il tipo di file utilizzando l&#39;estensione del file. [!DNL Experience Manager] è in grado di rilevarla dal contenuto dei file. Per quest&#39;ultima, selezionare l&#39;opzione [!UICONTROL Rileva MIME dal contenuto] in [!UICONTROL Day CQ DAM Mime Type Service] nella [!DNL Experience Manager] console Web.

Un elenco dei tipi MIME supportati è disponibile in CRXDE Lite in `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Estensione file | Tipo MIME/ Tipo di supporto Internet | Valore jobParam predefinito | Valore jobParam consentito |
|---|---|---|---|
| Immagine | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | Il jobParam predefinito si applica a tutte le risorse di tipo MIME immagine.<ul><li>[knockoutBackgroundOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| TTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shock-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Abilita il supporto](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support) dei parametri di caricamento per le risorse basate su tipo MIME e per i file multimediali dinamici classici.
>* [Configurare il supporto](config-dynamic.md) dei parametri di processo di caricamento in base al tipo MIME.

