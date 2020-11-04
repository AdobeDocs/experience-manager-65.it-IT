---
title: Comprendere i concetti dei metadati
description: Scoprite la necessità e i tipi di metadati che consentono di semplificare la categorizzazione e l’organizzazione delle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 6%

---


# Comprendere i concetti dei metadati {#why-we-need-metadata}

Metadati significa dati sui dati. A questo proposito, i dati si riferiscono alla risorsa digitale, ad esempio un&#39;immagine. I metadati sono fondamentali per una gestione efficiente delle risorse.

I metadati sono la raccolta di tutti i dati disponibili per una risorsa, ma non necessariamente contenuti in tale immagine. Alcuni esempi di metadati sono:

* Nome della risorsa.
* Ora e data dell’ultima modifica.
* Dimensione della risorsa così come è stata memorizzata nella directory archivio.
* Nome della cartella in cui è contenuta.
* Risorse correlate o tag applicati.

Le proprietà di metadati di base che [!DNL Experience Manager] possono essere gestite per le risorse, permettono agli utenti di visualizzare tutte le risorse. Ad esempio, ordinare le risorse per data dell’ultima modifica è utile quando si tenta di individuare le risorse aggiunte di recente.

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
* Dimension (altezza e larghezza) di un’immagine.
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

[!DNL Extensible Metadata Platform] (XMP) è uno standard aperto utilizzato da [!DNL Experience Manager Assets] per la gestione di tutti i metadati. Lo standard offre una codifica universale dei metadati che può essere incorporata in tutti i formati di file.  Adobe e altre aziende supportano XMP standard in quanto fornisce un modello di contenuto avanzato. Gli utenti di XMP standard e di [!DNL Experience Manager Assets] hanno una piattaforma potente su cui costruire. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Ulteriori informazioni sui formati:

* I tag ID3 funzionano nei file MP3 e mp3PRO.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l&#39;implementazione open-source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di tag proprietario.

### Exif {#exif}

Exchangeable image file format (Exif) è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in molti formati di file, come JPEG, TIFF, RIFF e WAV. Exif memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Le coppie nome-valore dei metadati sono anche denominate tag, da non confondere con i tag in [!DNL Experience Manager]. Le moderne fotocamere digitali creano i metadata Exif e il software di grafica moderna lo supportano. Il formato Exif è il denominatore più basso per la gestione dei metadati, in particolare per le immagini.

Un importante limite di Exif è dato dal fatto che alcuni formati di file immagine popolari come BMP, GIF o PNG non lo supportano.

I campi di metadati definiti da Exif sono generalmente di natura tecnica e sono di utilizzo limitato per la gestione dei metadati descrittivi. Per questo motivo, [!DNL Experience Manager Assets] offre la mappatura delle proprietà Exif in [comuni schemi](metadata-schemas.md) di metadati e in [XMP](xmp-writeback.md).

### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file sono [!DNL Microsoft Word], [!DNL PowerPoint][!DNL Excel], e così via.

## Comprendere gli schemi di metadati {#metadata-schemata}

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

### Metadati Digital Rights Management (DRM) {#digital-rights-management-metadata}

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

* PDF e PDF/X -  applicazioni Adobe PDF e di terze parti.
* PRISM - Requisiti [di pubblicazione per metadati](https://www.idealliance.org/prism-metadata)standard di settore.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadati XMP per il testo a pagina.

### Metadati multimediali specifici {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestione dei supporti.

## Riferimento schemi metadati {#metadata-schemata-reference}

Il riferimento seguente contiene informazioni su uno specifico schema di metadati (in ordine alfabetico), un elenco delle proprietà e delle relative definizioni.

### Dublin Core {#dublin-core}

I metadati Dublin Core forniscono un set standardizzato di convenzioni per la descrizione delle risorse, al fine di facilitarne la ricerca. In [!DNL Assets]Dublin Core descrive le risorse digitali come video, audio, immagini e documenti.

Il semplice set di metadati Dublin Core Metadata Element Set (DCMES) contiene 15 elementi di metadati, come elencato nella tabella seguente. Ciascun elemento Dublin Core è facoltativo e può essere ripetuto. Potete aggiungere o eliminare i metadati Dublin Core come fareste per i metadati specifici per i tipi di supporti.

Oltre al DCMES, esistono altri elementi di metadati creati dall&#39;iniziativa Dublin Core. Per ulteriori informazioni, consulta [Dublin Core Initiative](https://dublincore.org/) .

| Proprietà | Descrizione |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| collaboratore | La persona o la società responsabile del contributo al contenuto. |
| cover | La posizione geografica o il periodo di tempo coperto dall&#39;attività. |
| creatore | La persona o la società responsabile della creazione del contenuto. |
| data | Data o periodo di tempo associato alla risorsa. |
| descrizione | Ulteriori informazioni sulla risorsa. |
| format | Il formato file, il supporto fisico o le dimensioni della risorsa. [!DNL Experience Manager] utilizza `dc:format` per indicare il tipo MIME della risorsa. |
| identifier | Un riferimento univoco alla risorsa. |
| language | La lingua della risorsa (ad esempio, en per l’inglese). |
| publisher | La persona o la società responsabile della messa a disposizione della risorsa. |
| relation | Una risorsa correlata. |
| rights | Informazioni su chi dispone dei diritti per questa risorsa. |
| source | Un&#39;attività correlata da cui è derivata l&#39;attività. |
| subject | Argomento della risorsa. |
| titolo | Un nome per la risorsa. |
| tipo | La natura o il genere del bene. |

### IPTC {#iptc}

L&#39;International Press Telecommunications Council (IPTC) è un consorzio di agenzie di informazione di tutto il mondo, uno dei suoi obiettivi è quello di sviluppare e mantenere gli standard tecnici. L&#39;IPTC ha definito una serie di standard di metadati fotografici per le immagini che sono quasi universalmente accettati dai fotografi. Questi standard di metadati facevano parte dello standard più ampio noto come IPTC Information Interchange Model (IIM) creato negli anni &#39;90.

Sebbene le informazioni dell&#39;intestazione IPTC siano state in gran parte sostituite da XMP, per XMP sono disponibili uno schema di base IPTC e uno schema di estensione. Nei programmi di immagini, le proprietà XMP e IPTC sono sincronizzate.

## Flussi di lavoro basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l&#39;efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro ed esegue quindi alcune azioni predefinite. Ad esempio, potete usare alcuni dei flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha o meno un titolo. In caso contrario, il sistema notifica l’aggiunta di un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente o meno la distribuzione. Pertanto, il sistema invia la risorsa a un server o all’altro.
* Un flusso di lavoro può verificare la presenza di risorse senza metadati obbligatori predefiniti o risorse con metadati *non validi* .

## Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da [!DNL Adobe Experience Manager Assets] per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un modello [di](#xmp-core-concepts) contenuto avanzato ed è [supportato da  Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con [!DNL Assets] una piattaforma potente su cui costruire.

La specifica [](https://www.adobe.com/devnet/xmp.html) XMP è disponibile dal Adobe .

### Cos&#39;è XMP? {#what-is-xmp}

 Adobe ha introdotto lo standard XMP come parte del prodotto software Adobe Acrobat . Da allora, lo standard XMP è stato ampiamente adottato. [!DNL Assets] supporta in modo nativo il XMP - l&#39;Extensible Metadata Platform, diretto da  Adobe. XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato in  applicazioni  Adobi per trasmettere informazioni in più formati di file. [!DNL Assets] repository estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizzare la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di storage e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono composti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

### ecosistema XMP {#xmp-ecosystem}

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP offre i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per trasmettere dati binari in XMP, ad esempio, immagini in miniatura, è necessario codificarli in un formato XML adatto, ad esempio `Base64`.

### Concetti XMP {#xmp-core-concepts}

Le sezioni seguenti descrivono i concetti di base di XMP, compresi spazi dei nomi e schemi, proprietà e valori, nonché alternative linguistiche.

#### Spazi dei nomi e schemi {#namespaces-and-schemata}

Uno schema XMP è un insieme di nomi di proprietà in uno spazio nomi XML comune che include il tipo di dati e informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la `Creator` proprietà di due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio,  Adobe Photoshop).

#### Proprietà e valori {#properties-and-values}

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni  Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP schema di base: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP schema di gestione supporti: `xmpMM:DocumentID`.

#### Lingue alternative {#language-alternatives}

XMP consente di aggiungere una `xml:lang` proprietà alle proprietà di testo per specificare la lingua del testo.

## Utilizzo dei metadati IPTC {#support-for-iptc-metadata}

Scoprite come [!DNL Adobe Experience Manager Assets] supporta i metadati IPTC, le valutazioni creative e le parole chiave aggiunte alle risorse tramite [!DNL Adobe Bridge] e altre [!DNL Adobe Creative Cloud] app.

[!DNL Adobe Experience Manager Assets] supporta lo standard di metadati IPTC, ampiamente utilizzato per descrivere le risorse. In questo modo, [!DNL Assets] migliora l&#39;accettazione delle immagini tra vari partiti, tra cui fotografi, agenzie creative, biblioteche, musei e così via.

Lo schema di metadati predefinito per le risorse ora include gli schemi di metadati IPTC Core e IPTC Extension per definire proprietà complete di metadati che consentono agli utenti di aggiungere dati precisi e affidabili sulle persone, le posizioni e i prodotti visualizzati in un&#39;immagine. Supporta inoltre date, nomi e identificatori relativi alla creazione dell&#39;immagine e un modo flessibile per esprimere le informazioni sui diritti.

La pagina Proprietà delle risorse ora include schede separate per visualizzare i metadati IPTC Core e IPTC Extension nei campi modificabili.

1. Dall’interfaccia [!DNL Assets] utente, selezionate un’immagine.
1. Click **[!UICONTROL Properties]** from the toolbar.
1. Fate clic sulla scheda **[!UICONTROL IPTC]** per visualizzare i metadati IPTC per la risorsa.
1. Modificate le proprietà dei metadati IPTC, a seconda delle necessità.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. Modificate le proprietà dei metadati dell’estensione IPTC, a seconda delle necessità.
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

### Supporto per valutazione creativa {#creative-rating-support}

Oltre a visualizzare le valutazioni dei singoli utenti e le valutazioni aggregate, nella pagina Proprietà vengono ora visualizzate le valutazioni assegnate alle risorse tramite  Adobe Bridge e altre app Creative

Queste valutazioni sono disponibili nella sezione **[!UICONTROL Valutazione creativa]** della scheda **[!UICONTROL Avanzate]**.

Questa valutazione è una proprietà di sola lettura e ha un intervallo compreso tra 1 e 5. Potete cercare le risorse in base alla loro valutazione creativa dal pannello di ricerca.

Tuttavia, questa proprietà non è attualmente indicizzata per evitare conflitti con le modifiche personalizzate apportate dagli utenti.

### Supporto parole chiave {#keyword-support}

La scheda **[!UICONTROL IPTC]** della pagina [!UICONTROL Proprietà] mostra anche le parole chiave aggiunte alle risorse tramite  Adobe Bridge e altre app Adobe Creative Cloud. Potete anche modificare queste parole chiave e aggiungere altre parole chiave dalla scheda **[!UICONTROL IPTC]** .

![keywords](assets/keywords-in-iptc-tab.png)
