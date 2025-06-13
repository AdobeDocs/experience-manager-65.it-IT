---
title: Formati di file supportati e tipi MIME
description: Formati di file e tipi MIME supportati da [!DNL Assets] e [!DNL Dynamic Media] e funzionalità supportate per ciascun formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 12%

---

# Formati supportati in [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] supporta un&#39;ampia gamma di formati di file e ogni funzionalità supporta diversi tipi MIME. Per integrare [!DNL Assets] con altre soluzioni DAM (Digital Asset Management) e software desktop conformi agli standard, utilizzare Adobe [!DNL Extensible Metadata Platform] (XMP).

La legenda seguente indica i diversi livelli di supporto.

| Livello di supporto | Descrizione |
| :-----------: | ------------------------------ |
| ✓ | Funzione supportata |
| &#42; | Supportato con funzioni aggiuntive |
| − | Non applicabile |

## Formati immagine raster supportati in [!DNL Experience Manager] {#supported-raster-image-formats}

I formati supportati per l&#39;immagine raster in [!DNL Assets] sono:

| Formato | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione miniature | Modifica | Writeback di metadati | Approfondimenti |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| ‡ PSD | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡ L&#39;immagine unita viene estratta dal file PSD. Si tratta di un’immagine generata da Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l&#39;immagine unita potrebbe essere o meno l&#39;immagine effettiva.

Oltre alle informazioni di cui sopra, considera quanto segue:

* Il supporto per i file EPS si applica solo alle immagini raster. Ad esempio, la generazione di miniature per le immagini vettoriali EPS non è supportata per impostazione predefinita. Per aggiungere supporto, [configura ImageMagick](best-practices-for-imagemagick.md). Per integrare strumenti di terze parti per abilitare funzionalità aggiuntive, vedere [Gestore di supporti basato su riga di comando](media-handlers.md#command-line-based-media-handler).

* Il writeback dei metadati funziona per il formato di file PSB quando viene aggiunto al gestore `NComm`.

* Per i file EPS, il writeback dei metadati è supportato in PostScript Document Structuring Convention (PS-Adobe) versione 3.0 o successiva.

## Formati 3D supportati {#support-3d-formats}

È supportato il seguente elenco di formati 3D.

Vedi anche [Utilizzo di risorse 3D in Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Archiviazione | Controllo delle versioni | Flusso di lavoro | Pubblicazione | Controllo degli accessi | Anteprima miniatura | Anteprima 3D | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## Libreria PDF Rasterizer supportata {#supported-pdf-rasterizer-library}

La libreria Rasterizer di Adobe PDF genera anteprime e miniature di alta qualità per file [!DNL Adobe Illustrator] e PDF di grandi dimensioni e ad uso intensivo di contenuti. Adobe consiglia di utilizzare la libreria Rasterizer di PDF per i seguenti elementi:

* File AI/PDF ad uso intensivo di contenuti che richiedono molte risorse per essere elaborati.
* File AI/PDF, per i quali le miniature non vengono generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Vedere [Utilizzo di PDF Rasterizer](aem-pdf-rasterizer.md).

## Libreria di trascodifica delle immagini supportata {#supported-image-transcoding-library}

La libreria Adobe Imaging Transcoding è una soluzione di elaborazione delle immagini che esegue funzioni di base per la gestione delle immagini, quali codifica, transcodifica, ricampionamento e ridimensionamento.

La libreria Imaging Transcoding supporta JPG/JPEG, PNG (8 bit e 16 bit), GIF, BMP, TIFF/Compressed TIFF (a parte i file TIFF a 32 bit e i file PTIFF), ICO e i tipi ICN MIME.

Vedi [Libreria trascodifica immagini](imaging-transcoding-library.md).

## Camera Raw supportato {#supported-camera-raw}

La libreria [!DNL Adobe Camera Raw] consente a [!DNL Assets] di acquisire immagini non elaborate. Consulta [Supporto Camera Raw](camera-raw.md).

## Formati di documenti [!DNL Assets] supportati {#supported-document-formats}

I formati di documento supportati per le funzioni di gestione delle risorse sono i seguenti:

| Formato | Archiviazione | [Gestione metadati](metadata.md) | Estrazione full-text<br> | [Estrazione metadati](metadata.md) | Generazione miniature<br> | [Estrazione risorsa secondaria](managing-linked-subassets.md) | [Writeback metadati](xmp-writeback.md) | [Risorse collegate](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| EPUB | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## Formati multimediali supportati {#supported-multimedia-formats}

| | Archiviazione | Gestione dei metadati | Estrazione di metadati | Generazione miniature | Transcodifica FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## Formati di archiviazione supportati {#supported-archive-formats}

I formati di archivio supportati e l’applicabilità dei flussi di lavoro DAM comuni sono descritti nella tabella seguente.

| Formati | Archiviazione | Controllo delle versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Altri formati supportati {#other-supported-formats}

Di seguito è descritta l’applicabilità delle usuali funzionalità DAM per alcuni formati di file specifici.

| Formati | Archiviazione | Controllo delle versioni | Flusso di lavoro | Pubblicazione | Controllo accesso | Consegna Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (se configurato con un proprio dominio di consegna) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>Il caricamento e la distribuzione di file JavaScript possono essere sicuri o meno. Se necessario, puoi utilizzare le sovrapposizioni per impedire agli utenti di caricare file JS.

## Tipi MIME supportati {#supported-mime-types}

Per impostazione predefinita, [!DNL Experience Manager] rileva il tipo di file utilizzando l&#39;estensione. [!DNL Experience Manager] può rilevarla dal contenuto dei file. Per quest&#39;ultimo, selezionare [!UICONTROL Rileva MIME dal contenuto] opzione in [!UICONTROL Day CQ DAM Mime Type Service] nella console Web [!DNL Experience Manager].

Un elenco dei tipi MIME supportati è disponibile in CRXDE Lite in `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Estensione file | Tipo MIME/tipo di file multimediale Internet | Valore jobParam predefinito | Valore jobParam consentito |
|---|---|---|---|
| Immagine | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | Il valore predefinito jobParam si applica a tutte le risorse di tipo MIME per immagini.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options)</li><li>[manualCropOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html?lang=it)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options)</li><li>[emailSetting](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings)</li><li>[xmpKeywords](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options)</li></ul> |
| 3G2 | video/3gpp2 | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| 3GP | video/3gpp | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[opzioniPostScript](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options)</li><li> [illustratorOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| BMP | image/bmp | | |
| CSS | text/css | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| M4V | video/x-m4v | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MOV | video/quicktime | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MPEG | video/mpeg | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MPG | video/mpeg | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| OTF | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [opzioniPDF](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[opzioniPostScript](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options)</li><li>[illustratorOptions]&#x200B;(https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF/TIFF | image/tiff | | |
| TTC | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | video/dvd | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [EscludiVideoMasterDaAVS](https://experienceleague.adobe.com/it/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media: formati video di ingresso supportati per la transcodifica {#supported-input-video-formats-for-dynamic-media-transcoding}

| Estensione file video | Contenitore | Codec video consigliati | Codec video non supportati |
|---|---|---|---|
| AVI | Interfoliazione A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (file di animazione vettoriale) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, animazione Apple |
| MP4 | MPEG-4 | H264/AVC (tutti i profili) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| ‡ MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Schermo Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

‡ Questo formato video non è ancora supportato per l’utilizzo con video interattivi in Dynamic Media o con Annotation in Experience Manager Assets.

## Dynamic Media - Formati di documenti supportati {#supported-document-formats-dynamic-media}

| Formato | Carica<br> (formato di input) | Crea <br> immagine<br> predefinito<br> (formato di output) | Anteprima <br> rappresentazione dinamica<br> | Consegna <br> rappresentazione dinamica<br> | Scarica <br> rappresentazione dinamica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (vedere la nota seguente) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Per i PDF protetti, è supportato solo il caricamento.

Oltre alle funzionalità di cui sopra, considera quanto segue:

* Per utilizzare Dynamic Media per generare rappresentazioni dinamiche per i file PDF, vedere [Formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare Dynamic Media per visualizzare in anteprima e generare rappresentazioni dinamiche per i file AI, vedere [Formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per utilizzare Dynamic Media per generare rappresentazioni dinamiche per i file INDD, vedere [Formato file InDesign (INDD)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - Formati supportati per le immagini raster {#supported-raster-image-formats-dynamic-media}

| Formato | Carica (formato di input) | Crea predefinito immagine (formato di output) | Anteprima rappresentazione dinamica | Distribuzione di una rappresentazione dinamica | Scarica rappresentazione dinamica | Imposta i tipi che supportano questo formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Immagine](/help/assets/image-sets.md), [File multimediali diversi](/help/assets/mixed-media-sets.md) e [Rotazione](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/image-sets.md), [File multimediali diversi](/help/assets/mixed-media-sets.md) e [Rotazione](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/image-sets.md), [File multimediali diversi](/help/assets/mixed-media-sets.md) e [Rotazione](/help/assets/spin-sets.md) |
| ‡ PSD | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Immagine](/help/assets/image-sets.md), [File multimediali diversi](/help/assets/mixed-media-sets.md) e [Rotazione](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ L&#39;immagine unita viene estratta dal file PSD. Si tratta di un’immagine generata da Adobe Photoshop e inclusa nel file PSD. A seconda delle impostazioni, l&#39;immagine unita potrebbe essere o meno l&#39;immagine effettiva.

* Il supporto per i file EPS si applica solo alle immagini raster. Ad esempio, la generazione di miniature per le immagini vettoriali EPS non è supportata per impostazione predefinita. Per aggiungere supporto, [configura ImageMagick](best-practices-for-imagemagick.md). Per integrare strumenti di terze parti per abilitare funzionalità aggiuntive, vedere [Gestore di supporti basato su riga di comando](media-handlers.md#command-line-based-media-handler).

* Per utilizzare [!DNL Dynamic Media] per visualizzare in anteprima e generare rappresentazioni dinamiche per i file EPS, vedere [Formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Per i file EPS, il writeback dei metadati è supportato in PostScript Document Structuring Convention (PS-Adobe) versione 3.0 o successiva.

## Dynamic Media - Formati immagine raster non supportati {#unsupported-image-formats-dynamic-media}

Nell&#39;elenco seguente vengono descritti i sottotipi di formati di file immagine raster *non* supportati in Dynamic Media.

* File PNG con dimensioni del blocco IDAT superiori a 100 MB.
* File PSB.
* I file PSD con uno spazio colore diverso da CMYK, RGB, Gradazioni di grigio o Bitmap non sono supportati. DuoTone, Lab e gli spazi colore indicizzati non sono supportati.
* File PSD con profondità di bit maggiore di 16.
* File TIFF con dati a virgola mobile.
* File TIFF con spazio colore Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media - Formati 3D supportati {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati 3D.

Vedi anche [Utilizzo di risorse 3D in Dynamic Media](/help/assets/assets-3d.md).

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary | Include i materiali e le texture come un&#39;unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivio zip | model/vnd.usdz+zip | *Supporto solo per l&#39;acquisizione. Nessuna visualizzazione o interazione disponibile.* USDZ è un formato 3D proprietario che può essere visualizzato in modalità nativa dai dispositivi Safari e iOS. |

>[!MORELIKETHIS]
>
>* [Abilita il supporto dei parametri dei processi di caricamento Assets e Dynamic Media Classic basati sul tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configura MIME basato sul tipo per il supporto dei parametri del processo di caricamento](config-dynamic.md).
