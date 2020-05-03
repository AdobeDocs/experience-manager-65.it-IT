---
title: Gestisci i metadati delle risorse digitali in [!DNL Adobe Experience Manager].
description: Scopri i tipi di metadati e come [!DNL Risorse Adobe Experience Manager] consente di gestire i metadati per le risorse per facilitarne la categorizzazione e l’organizzazione. [!DNL Experience Manager] consente di organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c32e64d4921d7239d07f57ab9e12c744758faa0a

---


# Gestione dei metadati delle risorse digitali {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] mantiene i metadati per ogni risorsa. Consente una classificazione e un’organizzazione più semplici delle risorse e aiuta le persone che cercano una risorsa specifica. Grazie alla possibilità di estrarre i metadati dai file caricati in [!DNL Experience Manager Assets], la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di conservare e gestire i metadati insieme alle risorse, potete organizzare ed elaborare automaticamente le risorse in base ai metadati.

* [Metadati XMP](xmp.md).
* [Come modificare o aggiungere metadati](meta-edit.md).
* [Riferimento](meta-ref.md)per gli schemi di metadati.

## Perché abbiamo bisogno di metadati {#why-we-need-metadata}

Metadati significa dati sui dati. A questo proposito, i dati si riferiscono alla risorsa digitale, ad esempio un&#39;immagine. I metadati sono fondamentali per una gestione efficiente delle risorse.

I metadati sono la raccolta di tutti i dati disponibili per una risorsa, ma non necessariamente contenuti in tale immagine. Alcuni esempi di metadati sono:

* Nome della risorsa.
* Ora e data dell’ultima modifica.
* Dimensione della risorsa così come è stata memorizzata nella directory archivio.
* Nome della cartella in cui è contenuta.
* Risorse correlate o tag applicati.

Queste proprietà sono le proprietà di metadati di base che Experience Manager può gestire per le risorse, consentendo agli utenti di visualizzare tutte le risorse. Ad esempio, ordinare le risorse per data dell’ultima modifica è utile quando si tenta di individuare le risorse aggiunte di recente.

Puoi aggiungere più dati di alto livello alle risorse digitali, ad esempio:

* Tipo di risorsa (è un’immagine, un video, una clip audio o un documento?).
* Proprietario della risorsa.
* Titolo della risorsa.
* Descrizione della risorsa.
* Tag assegnati a una risorsa.

Più metadati consentono di classificare ulteriormente le risorse ed è utile man mano che cresce la quantità di informazioni digitali. È possibile gestire poche centinaia di file in base solo ai nomi dei file. Tuttavia, questo approccio non è scalabile. Non è sufficiente che il numero di persone coinvolte e il numero di attività gestite aumentino.

Con l’aggiunta di metadati, il valore di una risorsa digitale aumenta, poiché la risorsa diventa,

* Più accessibile - i sistemi e gli utenti possono trovarlo facilmente.
* Gestione più semplice: puoi trovare più facilmente le risorse con lo stesso set di proprietà e apportare loro le modifiche necessarie.
* Completa: la risorsa contiene ulteriori informazioni e contesto con più metadati.

Per questi motivi, [!DNL Assets] offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Tipi di metadati {#types-of-metadata}

I due tipi di metadati di base sono i metadati tecnici e i metadati descrittivi.

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere mantenuti manualmente. [!DNL Experience Manager Assets] e altri software determinano automaticamente i metadati tecnici e i metadati potrebbero essere modificati al momento della modifica della risorsa. I metadati tecnici disponibili per una risorsa dipendono in larga misura dal tipo di file della risorsa. Alcuni esempi di metadati tecnici sono:

* Dimensione di un file.
* Dimensioni (altezza e larghezza) di un’immagine.
* Bitrate di un file audio o video.
* Risoluzione (livello di dettaglio) di un’immagine.

I metadati descrittivi sono metadati relativi al dominio applicazione, ad esempio l’azienda da cui proviene una risorsa. I metadati descrittivi non possono essere determinati automaticamente. Viene creato manualmente o semi-automaticamente. Ad esempio, una fotocamera GPS può tracciare automaticamente latitudine e longitudine e aggiungere il geotag all&#39;immagine.

Il costo per la creazione manuale di informazioni di metadati descrittivi è elevato. Pertanto, vengono stabiliti degli standard per facilitare lo scambio di metadati tra i sistemi software e le organizzazioni. [!DNL Experience Manager Assets] supporta tutti gli standard pertinenti per la gestione dei metadati.

## Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. Sono supportati alcuni standard di codifica:

* XMP: utilizzato per [!DNL Assets] archiviare i metadati estratti nella directory archivio.
* ID3: per i file audio e video.
* Exif: per i file di immagine.
* Altro/Legacy: da [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e così via.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) è uno standard aperto utilizzato da [!DNL Experience Manager Assets] per la gestione di tutti i metadati. Lo standard offre una codifica universale dei metadati che può essere incorporata in tutti i formati di file. Adobe e altre società supportano lo standard XMP in quanto fornisce un modello di contenuto avanzato. Gli utenti dello standard XMP e di [!DNL Experience Manager Assets] hanno una piattaforma potente su cui costruire. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Ulteriori informazioni sui formati:

* I tag ID3 funzionano nei file MP3 e mp3PRO.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l&#39;implementazione open-source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di tag proprietario.

### Exif {#exif}

Exchangeable image file format (Exif) è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in molti formati di file, come JPEG, TIFF, RIFF e WAV. Exif memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Le coppie nome-valore dei metadati sono anche denominate tag, da non confondere con i tag in [!DNL Experience Manager].  Le moderne fotocamere digitali creano i metadata Exif e il software di grafica moderna lo supportano. Il formato Exif è il denominatore più basso per la gestione dei metadati, in particolare per le immagini.

Un importante limite di Exif è dato dal fatto che alcuni formati di file immagine popolari come BMP, GIF o PNG non lo supportano.

I campi di metadati definiti da Exif sono generalmente di natura tecnica e sono di utilizzo limitato per la gestione dei metadati descrittivi. Per questo motivo, [!DNL Experience Manager Assets] offre la mappatura delle proprietà Exif negli schemi [di metadati](metadata-schemas.md) comuni e in [XMP](xmp-writeback.md).

### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file sono Microsoft Word, PowerPoint, Excel e così via.

## Schemi metadati {#metadata-schemata}

Gli schemi di metadati sono set predefiniti di definizioni di proprietà di metadati utilizzabili in varie applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che le proprietà sono &#39;about&#39; della risorsa.

Potete anche progettare i vostri schemi di metadati, se non ne esiste uno che soddisfi le vostre esigenze. Non duplicare le informazioni esistenti. La separazione degli schemi all&#39;interno di un&#39;organizzazione semplifica la condivisione dei metadati. [!DNL Experience Manager] fornisce un elenco predefinito degli schemi di metadati più comuni. L’elenco consente di iniziare nuovamente la strategia dei metadati e di scegliere rapidamente le proprietà di metadati necessarie.

Gli schemi di metadati supportati sono elencati di seguito.

### Metadati standard {#standard-metadata}

* DC - [!DNL Dublin Core] è un set importante e ampiamente utilizzato di metadati.
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` e `iptc4xmpExt` - International Press Communications Standard contiene molti metadata specifici per oggetto.
* RDF - Framework Descrizione risorsa - per metadati Web semantici generici.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Ticketing di base.

### Metadati specifici per l’applicazione {#application-specific-metadata}

I metadati specifici dell&#39;applicazione includono metadati tecnici e descrittivi. Se utilizzate tali metadati, altre applicazioni potrebbero non essere in grado di utilizzarli. Ad esempio, un’altra applicazione di rendering delle immagini potrebbe non essere in grado di accedere ai [!DNL Adobe Photoshop] metadati. Potete creare un passaggio del flusso di lavoro che modifica una proprietà specifica di un’applicazione in una proprietà standard.

* ACDSee - Metadati gestiti dal [!DNL ACDSee] programma. Consultate [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Usato da [!DNL Experience Manager Assets].
* DAM - Usato da [!DNL Experience Manager Assets].
* DEX - [Optima SC Descrizione Explorer](http://www.optimasc.com/products/dex/index.html) è una raccolta di strumenti per la gestione di metadati e file per i sistemi operativi Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadati Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - Requisiti [di pubblicazione per metadati](https://www.idealliance.org/prism-metadata)standard di settore.
* PRL - PRISM Rights Language.
* PUR - Diritti di utilizzo PRISM.
* `xmpPlus` - Integrazione di PLUS con XMP.

### Metadati specifici per la fotografia {#photography-specific-metadata}

* Exif - Informazioni tecniche della telecamera, inclusa la posizione GPS.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadati immagine (non solo per le immagini TIFF).

### Metadati specifici per la stampa {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e applicazioni di terze parti.
* PRISM - Requisiti [di pubblicazione per metadati](https://www.prismstandard.org)standard di settore.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadati XMP per il testo di pagina.

### Metadati multimediali specifici {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestione dei supporti.

## Flussi di lavoro basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l&#39;efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro ed esegue quindi alcune azioni predefinite. Ad esempio, potete usare alcuni dei flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha o meno un titolo. In caso contrario, il sistema notifica l’aggiunta di un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente o meno la distribuzione. Pertanto, il sistema invia la risorsa a un server o all’altro.
* Un flusso di lavoro può verificare la presenza di risorse senza metadati obbligatori predefiniti o risorse con metadati *non validi* .
