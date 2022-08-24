---
title: Concetti di metadati
description: Scopri la necessità e i tipi di metadati che consentono di organizzare e classificare più facilmente le risorse.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2720'
ht-degree: 9%

---

# Concetti di metadati {#why-we-need-metadata}

Metadati significa dati relativi ai dati. A questo proposito, i dati si riferiscono alla risorsa digitale, ad esempio un’immagine. I metadati sono fondamentali per una gestione efficiente delle risorse.

I metadati sono la raccolta di tutti i dati disponibili per una risorsa, ma non necessariamente contenuti in tale immagine. Alcuni esempi di metadati sono:

* Nome della risorsa.
* Ora e data dell’ultima modifica.
* Dimensione della risorsa così come era memorizzata nell’archivio.
* Nome della cartella in cui è contenuta.
* Risorse correlate o tag applicati.

Queste sono le proprietà di metadati di base che [!DNL Experience Manager] può gestire le risorse, consentendo agli utenti di vedere tutte le risorse. Ad esempio, ordinare le risorse per data dell’ultima modifica è utile quando si tenta di individuare le risorse aggiunte di recente.

Puoi aggiungere ulteriori dati di alto livello alle risorse digitali, ad esempio:

* Tipo di risorsa (immagine, video, clip audio o documento).
* Proprietario della risorsa.
* Titolo della risorsa.
* Descrizione della risorsa.
* Tag assegnati a una risorsa.

Ulteriori metadati ti aiutano a categorizzare ulteriormente le risorse ed è utile man mano che la quantità di informazioni digitali cresce. È possibile gestire poche centinaia di file in base solo ai nomi dei file. Tuttavia, questo approccio non è scalabile. Non è sufficiente che il numero di persone coinvolte e il numero di risorse gestite aumentino.

Con l’aggiunta dei metadati, il valore di una risorsa digitale aumenta, perché la risorsa diventa:

* Più accessibile: i sistemi e gli utenti possono trovarla facilmente.
* Più semplice da gestire: puoi trovare e modificare più facilmente le risorse che hanno uno stesso set di proprietà.
* Completa: la risorsa contiene più informazioni e contesto grazie a un maggior numero di metadati.

Per queste ragioni, [!DNL Assets] offre le modalità giuste per creare, gestire e scambiare metadati per le risorse digitali.

## Tipi di metadati {#types-of-metadata}

I due tipi di metadati di base sono i metadati tecnici e i metadati descrittivi.

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere mantenuti manualmente. [!DNL Experience Manager Assets] e altri software determinano automaticamente i metadati tecnici e i metadati possono cambiare quando la risorsa viene modificata. I metadati tecnici disponibili di una risorsa dipendono in larga misura dal tipo di file della risorsa. Alcuni esempi di metadati tecnici sono:

* Dimensioni di un file.
* Dimension (altezza e larghezza) di un’immagine.
* Bit rate di un file audio o video.
* Risoluzione (livello di dettaglio) di un&#39;immagine.

I metadati descrittivi sono metadati relativi al dominio dell&#39;applicazione, ad esempio, l&#39;azienda da cui proviene una risorsa. Impossibile determinare automaticamente i metadati descrittivi. Viene creato manualmente o semiautomatico. Ad esempio, una fotocamera con GPS abilitato può tracciare automaticamente la latitudine e la longitudine e aggiungere il geotag all&#39;immagine.

Il costo della creazione manuale di informazioni descrittive sui metadati è elevato. Pertanto, vengono stabiliti degli standard per facilitare lo scambio di metadati tra sistemi software e organizzazioni. [!DNL Experience Manager Assets] supporta tutti gli standard pertinenti per la gestione dei metadati.

## Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. Sono supportati diversi standard di codifica:

* XMP: utilizzato da [!DNL Assets] per memorizzare i metadati estratti all’interno dell’archivio.
* ID3: per file audio e video.
* Exif: per i file di immagine.
* Altro/Legacy: da [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e così via.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) è uno standard aperto utilizzato da [!DNL Experience Manager Assets] per la gestione di tutti i metadati. Lo standard offre una codifica universale dei metadati che può essere incorporata in tutti i formati di file. Adobe e altre aziende supportano XMP standard in quanto fornisce un modello di contenuti avanzati. Utenti di XMP standard e di [!DNL Experience Manager Assets] avere una piattaforma potente su cui costruire. Per ulteriori informazioni, consulta [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Informazioni aggiuntive sui formati:

* I tag ID3 funzionano nei file MP3 e mp3PRO.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l’implementazione open-source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di assegnazione tag proprietario.

### Exif {#exif}

Il formato Exif (Exchangeable image file format) è il formato di metadati più diffuso utilizzato nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in molti formati di file, come JPEG, TIFF, RIFF e WAV. Exif memorizza i metadati come coppie di un nome di metadati e di un valore di metadati. Queste coppie nome-valore-metadati sono anche denominate tag, da non confondere con l’assegnazione tag in [!DNL Experience Manager]. Le moderne fotocamere digitali creano metadati Exif e il software di grafica moderno lo supportano. Il formato Exif è il denominatore più basso per la gestione dei metadata, in particolare per le immagini.

Una limitazione importante di Exif è che alcuni formati di file immagine popolari come BMP, GIF o PNG non lo supportano.

I campi metadati definiti da Exif sono tipicamente di natura tecnica e sono di uso limitato per la gestione dei metadati descrittivi. Per questo motivo, [!DNL Experience Manager Assets] offre la mappatura delle proprietà Exif in [schemi di metadati comuni](metadata-schemas.md) e [XMP](xmp-writeback.md).

### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file includono [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e così via.

## Comprendere gli schemi di metadati {#metadata-schemata}

Gli schemi di metadati sono insiemi predefiniti di definizioni di proprietà di metadati che possono essere utilizzati in varie applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che le proprietà sono &#39;Info&#39; sulla risorsa.

Puoi anche progettare i tuoi schemi di metadati personalizzati, se non ne esistono alcuno che soddisfi le tue esigenze. Non duplicare le informazioni esistenti. All’interno di un’organizzazione, la separazione degli schemi facilita la condivisione dei metadati. [!DNL Experience Manager] fornisce un elenco predefinito degli schemi di metadati più comuni. L&#39;elenco ti aiuta a rilanciare la strategia dei metadati e a scegliere rapidamente le proprietà di metadati necessarie.

Gli schemi di metadati supportati sono elencati di seguito.

### Metadati standard {#standard-metadata}

* DC - [!DNL Dublin Core] è un set di metadati importante e ampiamente utilizzato.
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` e `iptc4xmpExt` - International Press Communications Standard contiene molti metadata specifici per il soggetto.
* RDF - Resource Description Framework - per metadati web semantici generici.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Ticketing di base dei processi.

### Metadati specifici dell&#39;applicazione {#application-specific-metadata}

I metadati specifici dell&#39;applicazione includono metadati tecnici e descrittivi. Se si utilizzano tali metadati, altre applicazioni potrebbero non essere in grado di utilizzarli. Ad esempio, un&#39;applicazione diversa per il rendering delle immagini potrebbe non essere in grado di accedere a [!DNL Adobe Photoshop] metadati. Puoi creare un passaggio del flusso di lavoro che modifica una proprietà specifica di un&#39;applicazione in una proprietà standard.

* ACDSee - Metadati gestiti dal [!DNL ACDSee] programma. Vedi [www.acdsee.com](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Utilizzato da [!DNL Experience Manager Assets].
* DAM - Utilizzato da [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] è una raccolta di strumenti per la gestione di metadati e file per i sistemi operativi Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadati del Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Sistema universale di licenze delle immagini](https://www.useplus.com).
* PRISM - [Requisiti di pubblicazione per metadati standard di settore](https://www.idealliance.org/prism-metadata).
* PRL - Lingua dei diritti PRISM.
* PUR - Diritti di utilizzo PRISM.
* `xmpPlus` - Integrazione di PLUS con XMP.

### Metadati specifici per la fotografia {#photography-specific-metadata}

* Exif - Informazioni tecniche provenienti dalla fotocamera, inclusa la posizione GPS.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF : metadati immagine (non solo per le immagini TIFF).

### Metadati specifici per la stampa {#print-specific-metadata}

* PDF e PDF/X - Applicazioni Adobe PDF e di terze parti.
* PRISM - [Requisiti di pubblicazione per metadati standard di settore](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadati XMP per il testo di paging.

### Metadati specifici per contenuti multimediali {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestione dei supporti.

## Riferimento a schemi di metadati {#metadata-schemata-reference}

Il riferimento seguente include informazioni su uno specifico schema di metadati (in ordine alfabetico), nonché un elenco di proprietà e relative definizioni.

### Dublin Core {#dublin-core}

I metadati Dublin Core forniscono un set standardizzato di convenzioni per la descrizione delle risorse al fine di facilitarne la ricerca. In [!DNL Assets], Dublin Core descrive risorse digitali quali video, audio, immagini e documenti.

Il semplice set di elementi di metadati di base di Dublino (DCMES) contiene 15 elementi di metadati, come indicato nella tabella seguente. Ogni elemento Dublin Core è facoltativo e può essere ripetuto. Puoi aggiungere o eliminare le informazioni sui metadati di base di Dublino come faresti per i metadati specifici per i tipi di file multimediali.

Oltre al DCMES, esistono altri elementi di metadati creati dall&#39;iniziativa di base di Dublino. Consulta la sezione [iniziativa Dublin Core](https://dublincore.org/) per ulteriori informazioni.

| Proprietà | Descrizione |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| collaboratore | La persona o la società responsabile del contributo al contenuto. |
| copertura | La posizione geografica o il periodo di tempo coperto dall&#39;attività. |
| creatore | La persona o l’azienda responsabile della creazione del contenuto. |
| data | Data o periodo di tempo associato all’attività. |
| descrizione | Ulteriori informazioni sulla risorsa. |
| format | Il formato file, il supporto fisico o le dimensioni della risorsa. [!DNL Experience Manager] utilizza `dc:format` per indicare il tipo MIME della risorsa. |
| identifier | Un riferimento univoco alla risorsa. |
| language | La lingua della risorsa (ad esempio, `en` per inglese). |
| editore | La persona o l’azienda responsabile della messa a disposizione del bene. |
| relation | Una risorsa correlata. |
| diritti | Informazioni su chi ha i diritti per questa risorsa. |
| source | Attività correlata da cui deriva l’attività. |
| soggetto | Argomento della risorsa. |
| titolo | Nome della risorsa. |
| tipo | La natura o il genere del bene. |

### IPTC {#iptc}

L&#39;International Press Telecommunications Council (IPTC) è un consorzio di agenzie di stampa in tutto il mondo - uno dei suoi obiettivi è quello di sviluppare e mantenere standard tecnici. L&#39;IPTC ha definito una serie di standard di metadata per le immagini che sono quasi universalmente accettati dai fotografi. Questi standard di metadati facevano parte dello standard più ampio noto come IPTC Information Interchange Model (IIM) creato negli anni &#39;90.

Sebbene le informazioni di intestazione IPTC siano state sostituite principalmente da XMP, per XMP sono disponibili uno schema di base IPTC e uno schema di estensione. Nei programmi immagine, le proprietà XMP e IPTC sono sincronizzate.

## Workflow basati su metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati su metadati consente di automatizzare alcuni processi, migliorando l’efficienza. In un flusso di lavoro basato su metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro e, di conseguenza, esegue alcune azioni predefinite. Ad esempio, alcuni dei modi per utilizzare flussi di lavoro basati su metadati:

* Il flusso di lavoro può verificare se un’immagine ha o meno un titolo. In caso contrario, il sistema notifica l’aggiunta di un titolo.
* Il flusso di lavoro può verificare se una notifica di copyright su una risorsa consente o meno la distribuzione. Pertanto, il sistema invia la risorsa a un server o all’altro.
* Un flusso di lavoro può controllare le risorse senza metadati o risorse predefiniti e obbligatori con *non valido* metadati.

## Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da [!DNL Adobe Experience Manager Assets] per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia varietà di applicazioni.

Oltre ad offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP [modello di contenuto](#xmp-core-concepts) e [supportato da Adobe](#advantages-of-xmp) e altre società, in modo che gli utenti di XMP in combinazione con [!DNL Assets] avere una piattaforma potente su cui costruire.

La [Specifica XMP](https://www.adobe.com/devnet/xmp.html) è disponibile dall’Adobe.

### Cos&#39;è XMP? {#what-is-xmp}

Adobe ha introdotto lo standard XMP come parte del prodotto software Adobe Acrobat. Da allora, lo standard XMP è stato ampiamente adottato. [!DNL Assets] Supporta in modo nativo la XMP, la piattaforma di metadati estensibili guidata da Adobe. XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto integrato XMP all&#39;interno delle applicazioni Adobe per trasmettere informazioni in più formati di file. [!DNL Assets] repository estrae i metadati XMP e li utilizza per gestire il ciclo di vita dei contenuti e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza il modo in cui i metadati vengono definiti, creati ed elaborati fornendo un modello di dati, un modello di archiviazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono tradotti automaticamente in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un insieme di proprietà. Tali proprietà sono sempre associate a una particolare entità indicata come risorsa; in altre parole, le proprietà riguardano la risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

### ecosistema XMP {#xmp-ecosystem}

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP presenta i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e precisi.
* XMP consente di avere più valori per una proprietà.
* XMP codifica standard, che consente di scambiare facilmente i metadati.
* XMP estensibile. Puoi aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati di XMP. EXIF, d&#39;altro canto, no - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per includere i dati binari in XMP, ad esempio le immagini in miniatura, è necessario codificarli in un formato XML come `Base64`.

### Concetti XMP {#xmp-core-concepts}

Le sezioni seguenti descrivono i concetti di base di XMP, compresi namespace e schemi, proprietà e valori e alternative linguistiche.

#### Namespace e schemi {#namespaces-and-schemata}

Uno schema XMP è un insieme di nomi di proprietà in uno spazio dei nomi XML comune che include il tipo di dati e le informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L’utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, il `Creator` in due schemi progettati in modo indipendente, potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

#### Proprietà e valori {#properties-and-values}

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni di Adobe potrebbe includere quanto segue:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* Schema di base XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP schema di gestione file multimediali: `xmpMM:DocumentID`.

#### Alternative linguistiche {#language-alternatives}

XMP consente di aggiungere un `xml:lang` per specificare la lingua del testo.

## Utilizzare i metadati IPTC {#support-for-iptc-metadata}

Scopri come [!DNL Adobe Experience Manager Assets] supporta i metadati IPTC, le valutazioni creative e le parole chiave aggiunte alle risorse tramite [!DNL Adobe Bridge] e altri [!DNL Adobe Creative Cloud] app.

[!DNL Adobe Experience Manager Assets] supporta lo standard di metadati IPTC, ampiamente utilizzato per descrivere le risorse. In questo modo, [!DNL Assets] Migliora l&#39;accettazione delle sue immagini tra vari partiti, tra cui fotografi, agenzie creative, biblioteche, musei e così via.

Lo schema metadati predefinito per le risorse ora incorpora gli schemi di metadati IPTC Core e IPTC Extension per definire proprietà di metadati complete che consentono agli utenti di aggiungere dati precisi e affidabili su persone, posizioni e prodotti visualizzati in un&#39;immagine. Supporta inoltre date, nomi e identificatori relativi alla creazione dell&#39;immagine e un modo flessibile per esprimere le informazioni sui diritti.

La pagina Proprietà per le risorse ora include schede separate per visualizzare i metadati IPTC Core e IPTC Extension nei campi modificabili.

1. Da [!DNL Assets] interfaccia utente, seleziona un’immagine.
1. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Fai clic sul pulsante **[!UICONTROL IPTC]** per visualizzare i metadati IPTC della risorsa.
1. Modifica le proprietà dei metadati IPTC, a seconda delle necessità.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Fai clic sul pulsante **[!UICONTROL Estensione IPTC]** scheda per visualizzare i metadati dell’estensione IPTC per la risorsa.
1. Modifica le proprietà dei metadati dell&#39;estensione IPTC, a seconda delle esigenze.
1. Fai clic su **[!UICONTROL Salva e chiudi]** per salvare le modifiche.

### Supporto di valutazione creativa {#creative-rating-support}

Oltre a visualizzare le valutazioni dei singoli utenti e le valutazioni aggregate, la pagina Proprietà visualizza ora le valutazioni assegnate alle risorse tramite Adobe Bridge e altre app Creative

Queste valutazioni sono disponibili nella sezione **[!UICONTROL Valutazione creativa]** della scheda **[!UICONTROL Avanzate]**.

Questa valutazione è una proprietà di sola lettura e ha un intervallo compreso tra 1 e 5. Puoi cercare le risorse in base al loro rating creativo dal pannello di ricerca.

Tuttavia, questa proprietà non è attualmente indicizzata per evitare conflitti con le modifiche personalizzate apportate dagli utenti.

### Supporto per parole chiave {#keyword-support}

La **[!UICONTROL IPTC]** della scheda [!UICONTROL Proprietà] In questa pagina sono inoltre visualizzate le parole chiave aggiunte alle risorse tramite Adobe Bridge e altre app Adobe Creative Cloud. È inoltre possibile modificare queste parole chiave e aggiungere ulteriori parole chiave dal **[!UICONTROL IPTC]** scheda .

![keywords](assets/keywords-in-iptc-tab.png)
