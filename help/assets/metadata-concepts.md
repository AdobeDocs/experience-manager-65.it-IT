---
title: Comprendere i concetti relativi ai metadati
description: Scopri la necessità di e i tipi di metadati che consentono di categorizzare e organizzare le risorse in modo più semplice.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 7%

---

# Comprendere i concetti relativi ai metadati {#why-we-need-metadata}

I metadati indicano i dati sui dati. A questo proposito, i dati si riferiscono alla tua risorsa digitale, ad esempio un’immagine. I metadati sono fondamentali per una gestione efficiente delle risorse.

I metadati sono la raccolta di tutti i dati disponibili per una risorsa, ma che non sono necessariamente contenuti in tale immagine. Alcuni esempi di metadati sono:

* Nome della risorsa.
* Ora e data dell’ultima modifica.
* Dimensione della risorsa così come è stata memorizzata nell’archivio.
* Nome della cartella in cui è contenuto.
* Risorse correlate o tag applicati.

Le proprietà di metadati di base che [!DNL Experience Manager] può gestire per le risorse consentono agli utenti di visualizzare tutte le risorse. Ad esempio, ordinare le risorse per data dell’ultima modifica è utile quando si tenta di individuare le risorse aggiunte di recente.

Puoi aggiungere più dati di alto livello alle risorse digitali, ad esempio:

* Tipo di risorsa (immagine, video, clip audio o documento).
* Proprietario della risorsa.
* Titolo della risorsa.
* Descrizione della risorsa.
* Tag assegnati a una risorsa.

L&#39;utilizzo di più metadati consente di categorizzare ulteriormente le risorse ed è utile in caso di crescita della quantità di informazioni digitali. È possibile gestire alcune centinaia di file in base solo ai nomi dei file. Tuttavia, questo approccio non è scalabile. Non è sufficiente quando aumentano il numero di persone coinvolte e il numero di risorse gestite.

Con l’aggiunta dei metadati, il valore di una risorsa digitale aumenta, perché la risorsa diventa:

* Più accessibile: i sistemi e gli utenti possono trovarla facilmente.
* Più semplice da gestire: puoi trovare e modificare più facilmente le risorse che hanno uno stesso set di proprietà.
* Completa: la risorsa contiene più informazioni e contesto grazie a un maggior numero di metadati.

Per questi motivi, [!DNL Assets] offre i mezzi giusti per creare, gestire e scambiare metadati per le risorse digitali.

## Tipi di metadati {#types-of-metadata}

I due tipi di metadati di base sono metadati tecnici e metadati descrittivi.

I metadati tecnici sono utili per le applicazioni software che si occupano di risorse digitali e non devono essere conservati manualmente. [!DNL Experience Manager Assets] e altro software determinano automaticamente i metadati tecnici e i metadati possono cambiare quando la risorsa viene modificata. I metadati tecnici disponibili di una risorsa dipendono in larga misura dal tipo di file della risorsa. Alcuni esempi di metadati tecnici sono:

* Dimensione di un file.
* Dimension (altezza e larghezza) di un&#39;immagine.
* Bitrate di un file audio o video.
* Risoluzione (livello di dettaglio) di un&#39;immagine.

I metadati descrittivi riguardano il dominio dell’applicazione, ad esempio l’azienda da cui proviene una risorsa. I metadati descrittivi non possono essere determinati automaticamente. Viene creato manualmente o in modo semi-automatico. Ad esempio, una fotocamera abilitata per il GPS può tracciare automaticamente la latitudine e la longitudine e aggiungere il geotag all&#39;immagine.

Il costo della creazione manuale di informazioni descrittive sui metadati è elevato. Vengono quindi stabiliti standard per facilitare lo scambio di metadati tra sistemi software e organizzazioni. [!DNL Experience Manager Assets] supporta tutti gli standard pertinenti per la gestione dei metadati.

## Standard di codifica {#encoding-standards}

Esistono diversi modi per incorporare i metadati nei file. È disponibile il supporto di una serie di standard di codifica:

* XMP: utilizzato da [!DNL Assets] per memorizzare i metadati estratti all&#39;interno dell&#39;archivio.
* ID3: per file audio e video.
* Exif: per file di immagine.
* Altro/Legacy: da [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e così via.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) è uno standard aperto utilizzato da [!DNL Experience Manager Assets] per la gestione di tutti i metadati. Lo standard offre una codifica universale dei metadati che può essere incorporata in tutti i formati di file. Adobe e altre aziende supportano lo standard XMP in quanto fornisce un modello di contenuti avanzati. Gli utenti dello standard XMP e di [!DNL Experience Manager Assets] dispongono di una piattaforma potente su cui basarsi. Per ulteriori informazioni, vedere [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

I dati memorizzati in questi tag ID3 vengono visualizzati quando si riproduce un file audio digitale sul computer o su un lettore MP3 portatile.

I tag ID3 sono progettati per il formato di file MP3. Informazioni aggiuntive sui formati:

* I tag ID3 funzionano in file MP3 e mp3PRO.
* WAV non ha tag.
* WMA dispone di tag proprietari che non consentono l’implementazione open-source.
* Ogg Vorbis utilizza i commenti Xiph incorporati nel contenitore Ogg.
* AAC utilizza un formato di tag proprietario.

### Exif {#exif}

Exchangeable image file format (Exif) è il formato di metadati più diffuso nella fotografia digitale. Fornisce un modo per incorporare un vocabolario fisso di proprietà di metadati in molti formati di file, come JPEG, TIFF, RIFF e WAV. Exif memorizza i metadati come coppie di un nome di metadati e un valore di metadati. Queste coppie nome-valore-metadati sono anche denominate tag, da non confondere con l&#39;assegnazione tag in [!DNL Experience Manager]. Le moderne fotocamere digitali creano metadati Exif e i moderni software di grafica lo supportano. Il formato Exif è il minimo comune denominatore per la gestione dei metadati, in particolare per le immagini.

Una limitazione importante di Exif è che alcuni formati di file di immagine popolari come BMP, GIF o PNG non lo supportano.

I campi di metadati definiti da Exif sono tipicamente di natura tecnica e sono di uso limitato per la gestione dei metadati descrittivi. Per questo motivo, [!DNL Experience Manager Assets] offre la mappatura delle proprietà Exif in [schemi di metadati comuni](metadata-schemas.md) e in [XMP](xmp-writeback.md).

### Altri metadati {#other-metadata}

Altri metadati che possono essere incorporati dai file includono [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e così via.

## Comprendere gli schemi di metadati {#metadata-schemata}

Gli schemi di metadati sono insiemi predefiniti di definizioni di proprietà di metadati che possono essere utilizzati in varie applicazioni. Le proprietà sono sempre associate a una risorsa, il che significa che si riferiscono alla risorsa.

Puoi anche progettare i tuoi schemi di metadati se non ne esiste alcuno che soddisfi le tue esigenze. Non duplicare le informazioni esistenti. All’interno di un’organizzazione, la separazione dei dati di schema semplifica la condivisione dei metadati. [!DNL Experience Manager] fornisce un elenco predefinito degli schemi di metadati più comuni. L’elenco ti consente di avviare rapidamente la strategia per i metadati e di scegliere le proprietà dei metadati necessarie.

Di seguito sono elencati gli schemi di metadati supportati.

### Metadati standard {#standard-metadata}

* DC - [!DNL Dublin Core] è un insieme importante e ampiamente utilizzato di metadati.
* DICOM - Imaging digitale e comunicazioni nella medicina.
* `Iptc4xmpCore` e `iptc4xmpExt` - International Press Communications Standard contiene molti metadati specifici dell&#39;oggetto.
* RDF - Resource Description Framework - per metadati web semantici generici.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Job ticket di base.

### Metadati specifici dell’applicazione {#application-specific-metadata}

I metadati specifici dell’applicazione includono metadati tecnici e descrittivi. Se si utilizzano tali metadati, è possibile che altre applicazioni non siano in grado di utilizzarli. Ad esempio, un&#39;altra applicazione per il rendering di immagini potrebbe non essere in grado di accedere ai metadati [!DNL Adobe Photoshop]. È possibile creare un passaggio del flusso di lavoro che modifichi una proprietà specifica dell&#39;applicazione in una proprietà standard.

* ACDSee: metadati gestiti dal programma [!DNL ACDSee]. Vedi [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Utilizzato da [!DNL Experience Manager Assets].
* DAM - Utilizzato da [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] è una raccolta di strumenti per la gestione dei metadati e dei file per i sistemi operativi Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/it/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Foto Microsoft.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadati Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Sistema universale di licenze per le foto](https://www.useplus.com).
* PRISM - [Requisiti di pubblicazione per i metadati standard del settore](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* PRL - PriSM Rights Language.
* PUR - Diritti di utilizzo PRISM.
* `xmpPlus` - Integrazione di PLUS con XMP.

### Metadati specifici per la fotografia {#photography-specific-metadata}

* Exif - Informazioni tecniche dalla fotocamera, inclusa la posizione GPS.
* CRS - Schema [!DNL Camera Raw].
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF: metadati di immagini (non solo per immagini TIFF).

### Metadati specifici per la stampa {#print-specific-metadata}

* PDF e PDF/X: applicazioni Adobe PDF e di terze parti.
* PRISM - [Requisiti di pubblicazione per i metadati standard del settore](https://www.w3.org/submissions/2020/SUBM-prism-20200910/Image_Guide.pdf).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadati XMP per testo impaginato.

### Metadati specifici per contenuti multimediali {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestione file multimediali.

## Riferimento schemi metadati {#metadata-schemata-reference}

Il seguente riferimento include informazioni su un particolare schema di metadati (in ordine alfabetico) e un elenco di proprietà e relative definizioni.

### Dublin Core {#dublin-core}

I metadati core di Dublino forniscono un set standardizzato di convenzioni per la descrizione delle risorse al fine di facilitarne la ricerca. In [!DNL Assets], il Dublin Core descrive risorse digitali quali video, audio, immagini e documenti.

Il set di elementi di metadati core di Dublino (DCMES) semplice contiene 15 elementi di metadati come elencato nella tabella seguente. Ogni elemento core di Dublino è facoltativo e può essere ripetuto. Puoi aggiungere o eliminare le informazioni sui metadati Dublin Core come faresti per i metadati specifici per il tipo di file multimediale.

Oltre ai DCMES, esistono altri elementi di metadati creati dall’iniziativa di base di Dublino. Per ulteriori informazioni, consulta l&#39;[iniziativa Core di Dublino](https://dublincore.org/).

| Proprietà | Descrizione |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| collaboratore | La persona o l’azienda responsabile di fornire contributi al contenuto. |
| copertura | La posizione geografica o il periodo di tempo coperto dall’attività. |
| creatore | Persona o società responsabile della creazione del contenuto. |
| data | Data o periodo di tempo associato alla risorsa. |
| descrizione | Ulteriori informazioni sulla risorsa. |
| formato | Il formato del file, il supporto fisico o le dimensioni della risorsa. [!DNL Experience Manager] utilizza `dc:format` per indicare il tipo MIME della risorsa. |
| identificatore | Riferimento univoco alla risorsa. |
| lingua | La lingua della risorsa (ad esempio, `en` per l&#39;inglese). |
| editore | La persona o l’azienda responsabile della messa a disposizione del bene. |
| relazione | Una risorsa correlata. |
| diritti | Informazioni su chi dispone dei diritti per questa risorsa. |
| sorgente | Una risorsa correlata da cui deriva la risorsa. |
| soggetto | Argomento della risorsa. |
| titolo | Nome della risorsa. |
| tipo | La natura o il genere della risorsa. |

### IPTC {#iptc}

L&#39;International Press Telecommunications Council (IPTC) è un consorzio di agenzie di stampa di tutto il mondo che ha come obiettivo lo sviluppo e il mantenimento di standard tecnici. L&#39;IPTC ha definito una serie di standard per i metadati fotografici per le immagini, che è quasi universalmente accettata dai fotografi. Questi standard di metadati facevano parte dello standard più ampio noto come IPTC Information Interchange Model (IIM) creato negli anni &#39;90&#39;.

Sebbene le informazioni dell’intestazione IPTC siano state per lo più sostituite dall’XMP, per l’XMP sono disponibili uno schema di base IPTC e uno schema di estensione. Nei programmi immagine, le proprietà XMP e IPTC sono sincronizzate.

## Flussi di lavoro basati sui metadati {#metadata-driven-workflows}

La creazione di flussi di lavoro basati sui metadati consente di automatizzare alcuni processi, migliorando l’efficienza. In un flusso di lavoro basato sui metadati, il sistema di gestione del flusso di lavoro legge il flusso di lavoro e di conseguenza esegue alcune azioni predefinite. Ad esempio, puoi utilizzare i flussi di lavoro basati sui metadati in alcuni modi:

* Il flusso di lavoro può verificare se un’immagine ha un titolo o meno. In caso contrario, il sistema notifica l&#39;aggiunta di un titolo.
* Il flusso di lavoro può verificare se un avviso di copyright su una risorsa ne consente la distribuzione o meno. In questo modo, il sistema invia la risorsa a un server o all&#39;altro.
* Un flusso di lavoro può verificare la presenza di risorse senza metadati predefiniti e obbligatori o risorse con metadati *non validi*.

## Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da [!DNL Adobe Experience Manager Assets] per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia varietà di applicazioni.

Oltre a offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un [modello di contenuto](#xmp-core-concepts) avanzato ed è [supportato da Adobe](#advantages-of-xmp) e altre aziende, in modo che gli utenti XMP in combinazione con [!DNL Assets] abbiano una piattaforma potente su cui basarsi.

La [specifica XMP](https://www.adobe.com/devnet/xmp.html) è disponibile da Adobe.

### Che cos’è l’XMP? {#what-is-xmp}

L’Adobe ha introdotto per la prima volta lo standard XMP come parte del prodotto software Adobe Acrobat. Da allora, lo standard XMP è stato ampiamente adottato. [!DNL Assets] supporta in modo nativo l&#39;XMP, la piattaforma di metadati estensibili guidata dall&#39;Adobe. L’XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari in risorse digitali. XMP è progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto integrato XMP nelle applicazioni Adobe per trasmettere informazioni su più formati di file. L&#39;archivio [!DNL Assets] estrae i metadati XMP e li utilizza per gestire il ciclo di vita dei contenuti e offre la possibilità di creare flussi di lavoro di automazione.

L’XMP standardizza il modo in cui i metadati vengono definiti, creati ed elaborati fornendo un modello di dati, un modello di archiviazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente tradotti in XMP, che può essere esteso per supportare schemi di metadati specifici del cliente, ad esempio i cataloghi di prodotti.

I metadati dell’XMP sono costituiti da un insieme di proprietà. Queste proprietà sono sempre associate a un
particolare entità definita risorsa; ovvero, le proprietà sono &quot;relative&quot; alla risorsa. In presenza di XMP, la risorsa è sempre la risorsa.

### Ecosistema XMP {#xmp-ecosystem}

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi dell’XMP {#advantages-of-xmp}

L’XMP presenta i seguenti vantaggi rispetto ad altri standard e schemi di codifica:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP ha una codifica standardizzata che consente di scambiare facilmente i metadati.
* L&#39;XMP è estensibile. Puoi aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile, consentendo di aggiungere tipi personalizzati di metadati ai dati dell’XMP. EXIF, invece, no - ha un elenco fisso di proprietà che non possono essere estese.

>[!NOTE]
>
>L’XMP generalmente non consente l’incorporamento di tipi di dati binari. Per inserire dati binari in XMP, ad esempio immagini di miniature, è necessario codificarli in un formato compatibile con XML, ad esempio `Base64`.

### Concetti XMP {#xmp-core-concepts}

Le sezioni seguenti descrivono i concetti fondamentali dell’XMP, inclusi gli spazi dei nomi e gli schemi, le proprietà e i valori e le alternative linguistiche.

#### Spazi dei nomi e schemi {#namespaces-and-schemata}

Uno schema XMP è un insieme di nomi di proprietà in uno spazio dei nomi XML comune che include
il tipo di dati e le informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L’utilizzo degli spazi dei nomi evita conflitti tra proprietà in schemi diversi che hanno lo stesso nome ma un significato diverso.

Ad esempio, la proprietà `Creator` in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l&#39;applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

#### Proprietà e valori {#properties-and-values}

L’XMP può includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni Adobe potrebbe includere quanto segue:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* Schema di base XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Schema gestione diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* Schema gestione supporti XMP: `xmpMM:DocumentID`.

#### Alternative linguistiche {#language-alternatives}

XMP consente di aggiungere una proprietà `xml:lang` alle proprietà di testo per specificare la lingua del testo.

## Utilizzo dei metadati IPTC {#support-for-iptc-metadata}

Scopri come [!DNL Adobe Experience Manager Assets] supporta i metadati IPTC, le valutazioni di Creative e le parole chiave aggiunte alle risorse tramite [!DNL Adobe Bridge] e altre app [!DNL Adobe Creative Cloud].

[!DNL Adobe Experience Manager Assets] supporta lo standard dei metadati IPTC ampiamente utilizzato per descrivere le risorse. In questo modo, [!DNL Assets] favorisce l&#39;accettazione delle sue immagini da parte di vari soggetti, tra cui fotografi, agenzie creative, biblioteche, musei e così via.

Lo schema metadati predefinito per le risorse ora incorpora gli schemi metadati IPTC Core e IPTC Extension per definire proprietà di metadati complete che consentono agli utenti di aggiungere dati precisi e affidabili su persone, posizioni e prodotti mostrati in un’immagine. Supporta anche date, nomi e identificatori relativi alla creazione dell’immagine e un modo flessibile per esprimere informazioni sui diritti.

La pagina Proprietà delle risorse ora include schede separate per visualizzare i metadati Core IPTC ed Estensione IPTC nei campi modificabili.

1. Dall&#39;interfaccia utente [!DNL Assets], selezionare un&#39;immagine.
1. Fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Fare clic sulla scheda **[!UICONTROL IPTC]** per visualizzare i metadati IPTC della risorsa.
1. Modificare le proprietà dei metadati IPTC in base alle esigenze.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Fare clic sulla scheda **[!UICONTROL Estensione IPTC]** per visualizzare i metadati dell&#39;estensione IPTC per la risorsa.
1. Modificare le proprietà dei metadati dell&#39;estensione IPTC in base alle esigenze.
1. Fai clic su **[!UICONTROL Salva e chiudi]** per salvare le modifiche.

### Supporto per valutazione creativa {#creative-rating-support}

Oltre a visualizzare le valutazioni dei singoli utenti e le valutazioni aggregate, la pagina Proprietà mostra ora le valutazioni assegnate alle risorse tramite Adobe Bridge e altre app creative

Queste valutazioni sono disponibili nella sezione **[!UICONTROL Valutazione creativa]** della scheda **[!UICONTROL Avanzate]**.

Questa valutazione è di sola lettura e varia da 1 a 5. Puoi cercare le risorse in base alla loro valutazione creativa dal pannello di ricerca.

Tuttavia, questa proprietà non è attualmente indicizzata per evitare conflitti con le modifiche personalizzate apportate dagli utenti.

### Supporto parole chiave {#keyword-support}

Nella scheda **[!UICONTROL IPTC]** della pagina [!UICONTROL Proprietà] sono inoltre visualizzate le parole chiave aggiunte alle risorse tramite Adobe Bridge e altre app Adobe Creative Cloud. È inoltre possibile modificare queste parole chiave e aggiungerne altre dalla scheda **[!UICONTROL IPTC]**.

![parole chiave](assets/keywords-in-iptc-tab.png)
