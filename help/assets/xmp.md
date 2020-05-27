---
title: Supporto per i metadati XMP in Risorse Adobe Experience Manager.
description: Scoprite lo standard di metadati XMP (Extensible Metadata Platform) utilizzato da Experience Manager Assets per la gestione dei metadati. XMP fornisce un formato standard per la creazione, l'elaborazione e lo scambio di metadati per un'ampia gamma di applicazioni.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 19%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da Adobe Experience Manager Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica di metadati universale che può essere incorporata in tutti i formati di file, XMP fornisce un modello [di](xmp.md#xmp-core-concepts) contenuto avanzato ed è [supportato da Adobe](xmp.md#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con Assets dispongano di una piattaforma potente su cui basarsi.

La specifica [](https://www.adobe.com/devnet/xmp.html) XMP è disponibile da Adobe.

## Cos&#39;è XMP? {#what-is-xmp}

Assets supporta in modo nativo XMP, la piattaforma per metadati estensibili guidata da Adobe. XMP è uno standard per l&#39;elaborazione e la memorizzazione di metadati standard e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato nelle applicazioni Adobe per trasmettere informazioni in più formati di file. L’archivio delle risorse estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di memorizzazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

### Adobe {#adobe}

Adobe ha introdotto lo standard XMP come parte del prodotto software Adobe Acrobat. Da allora, lo standard XMP è stato ampiamente adottato.

### ecosistema XMP {#xmp-ecosystem}

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

## Vantaggi di XMP {#advantages-of-xmp}

XMP presenta i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP ha una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

### Estensibili {#extensible}

Lo standard XMP è progettato per essere estensibile, consentendo di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporamento di tipi di dati binari. Per poter includere dati binari in XMP, ad esempio immagini in miniatura, questi devono essere codificati in un formato adatto a XML, ad esempio `Base64`.

## Concetti di base XMP {#xmp-core-concepts}

Le sezioni seguenti descrivono i concetti di base di XMP, inclusi spazi dei nomi e schemi, proprietà e valori, nonché le alternative linguistiche.

### Spazi dei nomi e schemi {#namespaces-and-schemata}

Uno schema XMP è un insieme di nomi di proprietà in uno spazio nomi XML comune che include il tipo di dati e informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la `Creator` proprietà di due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

### Proprietà e valori {#properties-and-values}

XMP può includere proprietà di uno o più schemi.

Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: dc:title, dc:creator, dc:subject, dc:format, dc:rights
* Schema di base XMP: xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* Schema di gestione diritti XMP: xmpRights:WebStatement, xmpRights:Contrassegnato
* Schema di gestione file multimediali XMP: xmpMM:DocumentID

### Alternative linguistiche {#language-alternatives}

XMP consente di aggiungere una `xml:lang` proprietà alle proprietà di testo per specificare la lingua del testo.
