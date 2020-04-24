---
title: Formati supportati per le risorse
description: Elenco dei formati di file supportati da AEM Assets e da Dynamic Media e delle funzioni supportate per ciascun formato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5304d956161ee7edce2ad5c058eec3ac7e200abf

---


# Formati di risorse supportati {#assets-supported-formats}

Risorse AEM supporta un&#39;ampia gamma di formati di file e ogni funzionalità supporta vari tipi MIME.

Per integrare AEM Assets con altre soluzioni DAM (Digital Asset Management) e software desktop conformi agli standard, utilizza l’Extensible Metadata Platform (XMP) di Adobe.

Utilizzate la legenda per comprendere il livello di supporto.

| Livello di supporto | Descrizione |
|:---:|---|
| ✓ | Supportato |
| * | Supportato con le funzioni del componente aggiuntivo |
| − | Non applicabile |

## Formati di immagini raster supportati in AEM Assets {#supported-raster-image-formats}

| Formato | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione delle miniature | Modifica interattiva | Write-back metadati | Approfondimenti |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PFM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

† L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere l’immagine effettiva o meno.

## Formati di immagini raster supportati in Contenuti multimediali dinamici (#supported-raster-image-format-dynamic-media)

| Formato | Carica<br> (formato di input) | Creare<br> un predefinito<br> per immagini<br> (formato di output) | Anteprima<br> rappresentazione dinamica<br> | Distribuzione<br> di rappresentazioni dinamiche<br> | Download<br> della rappresentazione dinamica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **†** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**†** L&#39;immagine unita viene estratta dal file PSD. Si tratta di un&#39;immagine generata da Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l’immagine unita potrebbe essere l’immagine effettiva o meno.

Oltre alle informazioni di cui sopra, considerate quanto segue:

* Il supporto per i file EPS si applica solo alle immagini raster. Ad esempio, la generazione di miniature per le immagini vettoriali EPS non è supportata per impostazione predefinita. Per aggiungere supporto, [configurare ImageMagick](best-practices-for-imagemagick.md). Per integrare strumenti di terze parti per abilitare funzionalità aggiuntive, consulta Gestore [multimediale basato su riga di](media-handlers.md#command-line-based-media-handler)comando.

* La funzione di reimpostazione dei metadati funziona per il formato di file PSB quando viene aggiunta al `NComm` gestore.

* Per utilizzare gli elementi multimediali dinamici per visualizzare in anteprima e generare rappresentazioni dinamiche per i file EPS, consultate Formati di file [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per i file EPS, la funzione di writeback dei metadati è supportata in PostScript Document Structuring Convention (PS-Adobe) versione 3.0 o successiva.

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

## Libreria PDF Rasterizer supportata {#supported-pdf-rasterizer-library}

La libreria Adobe PDF Rasterizer genera miniature e anteprime di alta qualità per file Adobe Illustrator e PDF di grandi dimensioni e ricchi di contenuti. Adobe consiglia di utilizzare la libreria PDF Rasterizer per le seguenti operazioni:

* I file AI/PDF ad alta intensità di contenuto che richiedono molte risorse per l&#39;elaborazione.
* File AI/PDF, per i quali le miniature non vengono generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## Libreria di transcodifica immagini supportata {#supported-image-transcoding-library}

La libreria Adobe Imaging Transcoding è una soluzione di elaborazione delle immagini che esegue funzioni fondamentali per la gestione delle immagini, come la codifica, la transcodifica, il ricampionamento e il ridimensionamento.

La libreria di transcodifica delle immagini supporta i tipi JPG/JPEG, PNG (8 bit e 16 bit), GIF, BMP, TIFF/Compresso TIFF (a parte file TIFF a 32 bit e PTIFF), ICO e ICN MIME.

Consultate Libreria [transcodifica](imaging-transcoding-library.md)Imaging.

## Camera Raw supportata {#supported-camera-raw}

La libreria Adobe Camera Raw consente a Risorse AEM di acquisire immagini crude. See [Camera Raw support](camera-raw.md).

## Formati di documenti di Risorse supportati {#supported-document-formats}

I formati dei documenti supportati per le funzioni di gestione delle risorse sono i seguenti:

<!--
DO NOT PUBLISH THIS TABLE -- Removing it as it got malformed during GitHub migration.

| Format | Storage | Metadata<br> management | Metadata<br> extraction | Thumbnail<br> generation | Interactive<br> editing | Metadata<br> writeback | [Insights](touch-ui-asset-insights.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | &#10003; | &#10003; | | &#10003; | &#10003; | &#10003; | &#10003; | |
| DOC | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| DOCX | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| ODT | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| HTML | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| RTF | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| TXT | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| XLS | &#10003; | &#10003; | &#10003; | | | | | &#10003; |
| XLSX | &#10003; | &#10003; | &#10003; | &#10003; | | | | &#10003; |
| ODS | &#10003; | &#10003; | &#10003; | | | | | |
| PPT | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | | &#10003; |
| PPTX | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | | &#10003; |
| ODP | &#10003; | &#10003; | &#10003; | | | | | |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | &#10003; | &#10003; | | &#10003; | &#10003; | &#10003; | &#10003; | |
| PS | &#10003; | &#10003; | | | | | | |
| QXP | &#10003; | &#10003; | | | | | | |
| EPUB | &#10003; | &#10003; | | &#10003; | &#10003; | | | |
-->

| Formato | Archiviazione | [Gestione dei metadati](metadata.md) | Estrazione full-text<br> | [Estrazione di metadati](metadata.md) | Generazione delle miniature<br> | [Estrazione di risorse secondarie](managing-linked-subassets.md) | [Write-back metadati](xmp-writeback.md) | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## Formati di documento supportati in Contenuti multimediali dinamici (#supported-document-format-dynamic-media)

| Formato | Carica<br> (formato di input) | Creare<br> un predefinito<br> per immagini<br> (formato di output) | Anteprima<br> rappresentazione dinamica<br> | Distribuzione<br> di rappresentazioni dinamiche<br> | Download<br> della rappresentazione dinamica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

Oltre alla funzionalità di cui sopra, tenete presente quanto segue:

* Per utilizzare gli elementi multimediali dinamici per generare rappresentazioni dinamiche per i file PDF, consultate Formati di file [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare gli elementi multimediali dinamici per visualizzare in anteprima e generare rappresentazioni dinamiche per i file AI, consultate Formati di file [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare gli elementi multimediali dinamici per generare rappresentazioni dinamiche per i file INDD, consultate Formato [di file](../assets/managing-image-presets.md#indesign-indd-file-format)InDesign (INDD).

## Formati multimediali supportati {#supported-multimedia-formats}

|  | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione delle miniature | Transcodifica FFMPEG |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | * |
| MIDI | ✓ | ✓ |  | − | * |
| 3GP | ✓ | ✓ |  | − | * |
| MP3 | ✓ | ✓ | ✓ | − | * |
| MPG | ✓ | ✓ |  | − | * |
| OGA | ✓ | ✓ |  | − | * |
| OGG | ✓ | ✓ |  | − | * |
| RA | ✓ | ✓ |  | − | * |
| WAV | ✓ | ✓ |  | − | * |
| WMA | ✓ | ✓ |  | − | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Formati video di input supportati in Contenuti multimediali dinamici per la transcodifica {#supported-input-video-formats-for-dynamic-media-transcoding}

| Estensione dei file video | Contenitore | Codec video consigliati | Codec video non supportati |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (tutti i profili) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animazione Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Interferenza A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Video Raw rosso | MJPEG 2000 |  |
| RAM, RM | RealVideo | Non supportato | Real G2 (RV 20), Real 8 (RV 30), Real 10 (RV 40) |
| FLAC | Flac nativo | Codec audio senza perdita di dati |  |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 |  |

## Formati di archivio supportati {#supported-archive-formats}

I formati di archivio supportati e l&#39;applicabilità dei flussi di lavoro DAM comuni sono descritti nella tabella seguente.

| Formati | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna di contenuti multimediali dinamici |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Altri formati supportati {#other-supported-formats}

L&#39;applicabilità dei flussi di lavoro DAM comuni ad alcuni altri formati di file è descritta nella tabella seguente. Per tutti i file è supportata la consueta funzionalità DAM come archiviazione, controllo delle versioni, ACL, flusso di lavoro, pubblicazione e gestione dei metadati, ad eccezione di Distribuzione di contenuti multimediali dinamici.

| Formati | Archiviazione | Gestione versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna di contenuti multimediali dinamici |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (se configurato con un proprio dominio di consegna) |  |  |  |  |  | ✓ |

## Supported MIME types {#supported-mime-types}

Per impostazione predefinita, AEM rileva il tipo di file utilizzando l’estensione file. AEM è in grado di rilevarlo dal contenuto dei file. In quest’ultimo caso, selezionate l’opzione [!UICONTROL Rileva MIME dal contenuto] in Servizio  Day CQ DAM Mime Type nella console Web di AEM.

Un elenco dei tipi MIME supportati è disponibile in CRXDE Lite all&#39;indirizzo `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Estensione file | Tipo MIME/ Tipo di supporto Internet | Valore jobParam predefinito | Valore jobParam consentito |
|---|---|---|---|
| Immagine | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | Il valore predefinito jobParam viene applicato a tutte le risorse di tipo mime immagine.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Supporto](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)dei parametri di caricamento di risorse/Scene7 basati su tipi MIME.
>* [Configurare il supporto](config-dynamic.md)dei parametri di processo di caricamento in base al tipo MIME.

