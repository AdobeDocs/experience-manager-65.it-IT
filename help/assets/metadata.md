---
title: Gestione dei metadati per le risorse digitali
description: Scopri i tipi di metadati e come Risorse AEM consente di gestire i metadati per le risorse per facilitarne la categorizzazione e l’organizzazione.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Manage metadata for digital assets {#managing-metadata-for-digital-assets}

Risorse Adobe Experience Manager (AEM) conserva i metadati per ogni risorsa. Questo semplifica la categorizzazione e l’organizzazione delle risorse e aiuta le persone che cercano una risorsa specifica. Grazie alla possibilità di estrarre i metadati dai file caricati in Risorse AEM, la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di gestire e mantenere con le risorse metadati arbitrari, Risorse AEM consente di organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.

* [Metadati XMP](xmp.md)
* [Come modificare o aggiungere metadati](meta-edit.md)
* [Riferimento schema metadati](meta-ref.md)

## Perché abbiamo bisogno di metadati {#why-we-need-metadata}

Metadati significa dati sui dati. A questo proposito, i dati si riferiscono alla risorsa con cui hai a che fare, ad esempio un’immagine. I metadati sono importanti perché consentono agli utenti di gestire le risorse in modo più efficiente.

I metadati sono la raccolta di tutti i dati disponibili per questa immagine, ma non necessariamente contenuti in tale immagine, ad esempio:

* il nome della risorsa
* l&#39;ora e la data dell&#39;ultima modifica
* le dimensioni dell’immagine così come è stata memorizzata nella directory archivio
* il nome della cartella in cui si trova

Queste sono le proprietà di metadati di base che AEM può gestire per le risorse, che consentono agli utenti di visualizzare tutte le risorse, ad esempio, ordinate in base alla data dell’ultima modifica, utile quando cercano di scoprire quali risorse sono state aggiunte di recente alla directory archivio.

Puoi aggiungere più dati di alto livello alle risorse digitali, ad esempio:

* il tipo di risorsa (è un&#39;immagine, un video, una clip audio o un documento?)
* proprietario della risorsa
* titolo della risorsa
* la descrizione del bene
* i tag assegnati a una risorsa

Più metadati consentono di classificare ulteriormente le risorse ed è utile man mano che cresce la quantità di informazioni digitali. Anche se è possibile per una singola persona gestire un elenco di poche centinaia di file semplicemente in base ai loro nomi di file, questo approccio è inferiore quando il numero di persone coinvolte e il numero di risorse gestite aumenta.

Man mano che i metadati vengono aggiunti alle risorse, il valore della risorsa aumenta, perché la risorsa diventa

* più accessibile - la gente può trovare molto più facile
* gestione più semplice: è possibile trovare risorse con lo stesso set di proprietà in modo più semplice e apportare modifiche
* più complesso: più metadati sono stati aggiunti a una risorsa, più importante sarà la gestione dei metadati

Per questi motivi, Risorse AEM offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Nozioni di base sui metadati {#metadata-basics}

I metadati vengono estratti dalle risorse al momento dell’importazione (assimilazione). Inoltre, l’aggiunta di metadati facilita ulteriormente la classificazione delle risorse.

Questa sezione descrive i tipi di metadati e gli standard di codifica.

### Tipi di metadati {#types-of-metadata}

Esistono due tipi di metadati di base:

* metadata
* metadati descrittivi

#### Metadati tecnici {#technical-metadata}

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere mantenuti manualmente. I metadati tecnici possono essere determinati automaticamente da Risorse AEM e altri software e possono essere modificati al momento della modifica della risorsa. I metadati tecnici disponibili per una risorsa dipendono in larga misura dal tipo di file della risorsa. Di seguito sono riportati alcuni esempi di metadati tecnici:

* le dimensioni di un file
* le dimensioni (altezza e larghezza) di un’immagine
* bitrate di un file audio o video
* la risoluzione (livello di dettaglio) di un&#39;immagine

#### Metadati descrittivi {#descriptive-metadata}

I metadati descrittivi sono metadati relativi al dominio applicazione, ad esempio l’azienda da cui proviene una risorsa. I metadati descrittivi non possono essere determinati automaticamente. Deve essere creato manualmente o semi-automaticamente. Ad esempio, una videocamera GPS può tracciare automaticamente latitudine e longitudine dell&#39;immagine e aggiungere queste informazioni ai metadati dell&#39;immagine.

A causa dell&#39;alto costo del lavoro manuale necessario per creare informazioni descrittive sui metadati, sono stati definiti standard per facilitare lo scambio di metadati tra i sistemi software e le organizzazioni.

AEM Assets supporta tutti gli standard pertinenti per la gestione dei metadati.

Data l&#39;importanza dei metadata e l&#39;elevato coinvolgimento manuale necessario per creare i metadata, sono stati definiti standard che semplificano lo scambio.

### Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. Sono supportati alcuni standard di codifica:

* XMP: utilizzato da Risorse AEM per archiviare i metadati estratti nella directory archivio.
* ID3: per i file audio e video.
* EXIF: per i file di immagine.
* Altro/Legacy: da Microsoft Word, PowerPoint, Excel e così via.

#### XMP {#xmp}

XMP è la piattaforma di metadati estensibile e lo standard di metadati utilizzato da AEM Assets per la gestione di tutti i metadati. Oltre a offrire una codifica di metadati universale che può essere incorporata in tutti i formati di file, XMP fornisce un modello di contenuto avanzato ed è supportato da Adobe e da altre aziende, in modo che gli utenti di XMP in combinazione con Risorse AEM possano sfruttare una piattaforma potente.

#### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Ulteriori informazioni sui formati:

* I tag ID3 funzionano nei file MP3 e MP3pro.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l&#39;implementazione open source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di tag proprietario.

#### EXIF {#exif}

EXIF significa formato di file di immagine sostituibile ed è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in diversi formati di file, come JPEG, TIFF, RIFF e WAV.

Una limitazione importante di EXIF è che non è supportato da altri formati di file immagine popolari come BMP, GIF o PNG.

EXIF memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Queste coppie nome-valore di metadati sono anche denominate tag, da non confondere con i tag in AEM.

Poiché l&#39;EXIF viene creata automaticamente dalle moderne telecamere digitali e supportata dai moderni software grafici, può essere considerata il denominatore più basso per la gestione dei metadata.

La maggior parte dei campi di metadati definiti da EXIF sono di natura altamente tecnica e di utilizzo limitato per la gestione dei metadati descrittivi. Per questo motivo, AEM Assets offre la mappatura delle proprietà EXIF negli schemi [di metadati](metadata-schemas.md) comuni e in [XMP](xmp-writeback.md), il potente formato di metadati utilizzato da Risorse AEM per la gestione dei metadati.

#### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file sono Microsoft Word, PowerPoint, Excel e così via.

## Schemata metadati {#metadata-schemata}

Gli schemi di metadati sono insiemi predefiniti di definizioni di proprietà di metadati che possono essere utilizzati in un’ampia gamma di applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che le proprietà riguardano la risorsa.

Potete anche progettare i vostri schemi di metadati personali se non ne esistono alcuno che soddisfi le vostre esigenze (prestate attenzione, tuttavia, a non duplicare elementi già esistenti). La separazione degli schemi all&#39;interno di un&#39;organizzazione semplifica la condivisione dei metadati tra le organizzazioni.

AEM fornisce un elenco completo degli schemi di metadati più comuni, che consente di avviare rapidamente la strategia per i metadati e di scegliere le proprietà di metadati necessarie da uno schema già definito.

Gli schemi di metadati supportati sono elencati nella sezione seguente.

### Metadati standard {#standard-metadata}

* dc - Dublin Core - il set di metadati più importante e ampiamente utilizzato
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - un sacco di metadata specifici per oggetto
* rdf - Resource Description Framework per metadati Web semantici generici
* xmp - Extensible Metadata Platform
* xmpBJ - Job Ticketing di base

### Metadati specifici per l’applicazione {#application-specific-metadata}

>[!NOTE]
>
>I metadati specifici per le applicazioni includono metadati tecnici e descrittivi. Se utilizzate queste opzioni, altre applicazioni potrebbero non essere in grado di utilizzare i metadati. Ad esempio, se disponete di una risorsa con metadati Adobe Photoshop e un’altra applicazione per il rendering delle immagini tenta di accedere ai metadati, potrebbe non essere in grado di accedervi.
>
>Se nelle risorse sono presenti molti metadati specifici per l’applicazione, potete creare un passaggio del flusso di lavoro che modifica la proprietà specifica dell’applicazione in uno standard.

* acdsee - metadati gestiti dal programma ACDSee [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - utilizzato da Risorse AEM
* dam utilizzato da AEM Assets
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* Microsoft Photo e MP - Microsoft Photo
* pdf amd pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadati per Digital Rights Management {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* più - Sistema universale di gestione delle immagini - https://www.useplus.com/
* prisma - https://www.idealliance.org/prism-metadata di pubblicazione per metadati standard di settore
* prl - Prism
* pur - Diritti di utilizzo Prism
* xmpPlus - integrazione di PLUS con XMP

### Metadati specifici per la fotografia {#photography-specific-metadata}

* exif - molte informazioni tecniche dalla telecamera, inclusa la posizione GPS
* crs - photoshop camera raw
* Iptc4xmpCore e iptc4xmpExt
* TIFF - Metadati immagine (non solo per le immagini TIFF)

### Metadati specifici per la stampa {#print-specific-metadata}

* pdf e pdfx - Adobe PDF e applicazioni di terze parti
* prisma - [www.prismstandard.org](https://www.prismstandard.org) di pubblicazione DPS per metadati standard di settore
* XMP
* xmpPG - xmp per il testo in pagine

### Metadati specifici per contenuti multimediali {#multimedia-specific-metadata}

* xmpDM - Contenuti multimediali dinamici
* xmpMM - Gestione dei supporti

## Flussi di lavoro basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l&#39;efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro ed esegue quindi alcune azioni predefinite.

Ad esempio, potete usare alcuni dei flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha un titolo. In caso contrario, il sistema avvisa un utente specifico di aggiungere un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente la distribuzione. In caso contrario, il sistema invia la risorsa a un server. In caso contrario, il sistema invia la risorsa a un altro server.
