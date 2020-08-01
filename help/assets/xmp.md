---
title: Supporto per XMP metadati in [!DNL Adobe Experience Manager Assets].
description: Scoprite lo standard di metadati XMP (Extensible Metadata Platform) utilizzato [!DNL Experience Manager Assets] per la gestione dei metadati. XMP fornisce un formato standard per la creazione, l'elaborazione e lo scambio di metadati per un'ampia gamma di applicazioni.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 20%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da [!DNL Adobe Experience Manager Assets] per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un modello [di](xmp.md#xmp-core-concepts) contenuto avanzato ed è [supportato da  Adobe](xmp.md#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con [!DNL Assets] una piattaforma potente su cui costruire.

La specifica [](https://www.adobe.com/devnet/xmp.html) XMP è disponibile dal Adobe .

## Cos&#39;è XMP? {#what-is-xmp}

[!DNL Assets] supporta in modo nativo il XMP, ovvero l’Platform di metadati estensibile con  Adobe. XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato in  applicazioni  Adobi per trasmettere informazioni in più formati di file. [!DNL Assets] repository estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizzare la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di storage e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono composti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

### Adobe {#adobe}

 Adobe ha introdotto lo standard XMP come parte del prodotto software Adobe Acrobat . Da allora, lo standard XMP è stato ampiamente adottato.

### ecosistema XMP {#xmp-ecosystem}

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

## Vantaggi di XMP {#advantages-of-xmp}

XMP offre i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

### Estensibili {#extensible}

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per trasmettere dati binari in XMP, ad esempio, immagini in miniatura, è necessario codificarli in un formato XML adatto, ad esempio `Base64`.

## Concetti XMP base {#xmp-core-concepts}

Le sezioni seguenti descrivono i concetti di base di XMP, compresi spazi dei nomi e schemi, proprietà e valori, nonché alternative linguistiche.

### Spazi dei nomi e schemi {#namespaces-and-schemata}

Uno schema XMP è un insieme di nomi di proprietà in uno spazio nomi XML comune che include il tipo di dati e informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la `Creator` proprietà di due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio,  Adobe Photoshop).

### Proprietà e valori {#properties-and-values}

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni  Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP schema di base: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP schema di gestione supporti: `xmpMM:DocumentID`.

### Alternative linguistiche {#language-alternatives}

XMP consente di aggiungere una `xml:lang` proprietà alle proprietà di testo per specificare la lingua del testo.
