---
title: Conversione di file tramite PDF Generator
seo-title: Conversione di file tramite PDF Generator
description: Come convertire i file con PDF Generator.
seo-description: Come convertire i file con PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---


# Conversione di file tramite PDF Generator{#converting-files-using-pdf-generator}

Per convertire i file è possibile utilizzare le pagine Web di PDF Generator.

## Creare un file PDF {#create-a-pdf-file}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Crea PDF.
1. Fate clic su Sfoglia per trovare e selezionare il file.

   >[!NOTE]
   >
   >PDF Generator è in grado di rilevare automaticamente il tipo di file dei file .doc, .xls, .ppt e .rtf, anche quando l&#39;estensione del file manca al nome del file. Questa funzione non funziona con file .docx, .xlsx e .pptx.

1. In Impostazioni di configurazione, selezionate Usa impostazioni personalizzate o Carica file impostazioni.

   * Se utilizzate impostazioni personalizzate, selezionate un&#39;impostazione Adobe PDF , un&#39;impostazione di protezione e un&#39;impostazione del tipo di file e specificate un timeout.

      Le impostazioni Adobe PDF  sono applicabili solo alle conversioni da PS a PDF, da EPS a PDF, da PRN a PDF, da immagine a PDF con OCR attivato e da nativa a PDF. L’impostazione di timeout specifica il tempo massimo di completamento della conversione. Il valore predefinito è 270 secondi. Queste impostazioni non vengono utilizzate durante le conversioni da immagine a PDF e da OpenOffice a PDF.

   * Se caricate un file di impostazioni, digitatene il percorso e il nome nella casella oppure fate clic su Sfoglia per trovare e selezionare il file.

1. (Facoltativo) In XMP file di metadati, digitate il percorso e il nome del file XMP oppure fate clic su Sfoglia per individuare e selezionare il file. Un file XMP può essere utilizzato per includere informazioni di metadati standard. (Vedere [Informazioni XMP file](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Quando il file viene creato, viene visualizzato un collegamento. Se si verifica un errore durante la conversione, viene visualizzato un avviso. Se si sta creando un file Postscript, l&#39;avviso contiene anche un collegamento al file di registro.
1. Fare clic sul collegamento per il file PDF. Il file si apre in  Acrobat.

### Informazioni sui file XMP {#about-xmp-files}

I documenti PDF creati da PDF Generator in  Acrobat 5.0 o versioni successive contengono i metadati del documento in formato XML. *I* metadati contengono informazioni sul documento e il relativo contenuto, ad esempio il nome dell&#39;autore, le parole chiave e le informazioni sul copyright utilizzabili dalle utilità di ricerca.

I metadati del documento contengono (ma non sono limitati a) informazioni che vengono visualizzate anche nella scheda Descrizione della finestra di dialogo Proprietà documento in  Acrobat. Le modifiche apportate nella scheda Descrizione vengono riportate nei metadati del documento. I metadati del documento possono essere estesi e modificati utilizzando prodotti di terze parti.

 Adobe Extensible Metadata Platform (XMP) fornisce  applicazioni di Adobe con un framework XML comune che standardizza la creazione, l&#39;elaborazione e lo scambio di metadati di documento tra i flussi di lavoro di pubblicazione. È possibile salvare e importare il codice sorgente XML dei metadati del documento in XMP formato, semplificando la condivisione dei metadati tra i vari documenti. Per ulteriori informazioni sui XMP file, vedere [Extensible Metadata Platform (XMP)](https://www.adobe.com/products/xmp/) e [ Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html).

Potete creare XMP file in  Acrobat.

## Convertire un file HTML o ZIP in PDF {#convert-an-html-file-or-zip-file-to-pdf}

PDF Generator consente di convertire in  Adobe PDF i seguenti tipi di file:

* File HTML, che potete convertire caricando un file HTML o specificando l&#39;URL di una pagina Web o di un sito Web.
* File archiviati (ZIP), che possono contenere file HTML, file immagine o entrambi.

Se il file ZIP contiene più di un file HTML al livello più basso della gerarchia delle cartelle, il file ZIP deve contenere anche un file index.htm o index.html.

>[!NOTE]
>
>* La funzione da HTML a PDF richiede alcuni font nella directory dei font di sistema. Nei sistemi Linux, Solaris e AIX, la directory dei font di sistema deve contenere il font Courier. Nei sistemi Windows, la directory dei font di sistema deve contenere Times New Roman.
   >
   >
* (Solo sistema basato su UNIX) Uno dei seguenti font giapponesi dovrebbe essere disponibile  server AEM Forms per convertire una pagina Web con font giapponese in un documento PDF.
   >
   >  
* &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot; Adobe Heiti Std&quot;
>  * &quot; Adobe Song Std&quot;

   >
   >
* Per caricare un file dal file system locale, usate l’opzione Carica file nella pagina da HTML a PDF.


1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > da HTML a PDF.
1. Specificare il file da convertire effettuando una delle seguenti operazioni:

   * In Carica file, digitate il percorso e il nome del file HTML o ZIP oppure fate clic su Sfoglia per individuarlo e selezionarlo.
   * Nella casella Specifica URL, digitate l’URL della pagina o del sito Web da convertire.

   >[!NOTE]
   >
   >Il file che si sta convertendo deve avere un’estensione di file .html, .htm o .zip.

1. Specificate le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, selezionate Usa impostazioni personalizzate, specificate le impostazioni di protezione e tipo di file e specificate un valore di timeout. Il valore predefinito è 270 secondi.
   >[!NOTE]
   >
   >Se il servizio Genera PDF è stato configurato per l&#39;utilizzo  Acrobat WebCapture, le impostazioni relative al tipo di file selezionate in questa pagina non influiscono sul PDF prodotto. Apportate le modifiche necessarie alla versione di  Acrobat installata sul server.

   * Per usare un file di impostazioni esistente, selezionate Carica file impostazioni e fate clic su Sfoglia per passare al percorso del file.


1. Per caricare un file XMP, fate clic su Sfoglia e passate al percorso del file. Un file XMP può essere utilizzato per includere informazioni di metadati standard. (Vedere [Informazioni XMP file](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Quando il file viene creato, viene visualizzato un collegamento al file PDF.
1. Fare clic sul collegamento per visualizzare il documento PDF in  Acrobat.

## Esportare un file PDF in un altro formato (solo Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

È possibile esportare i file PDF in vari formati, come descritto nel capitolo Generate PDF Service di [Services Reference](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Export PDF.
1. Fare clic su Sfoglia per individuare il file PDF da esportare.
1. Nell&#39;elenco del file di Export PDF , selezionare il formato in cui esportare il file PDF.
1. Nella casella Specificare un timeout, specificare il tempo di attesa prima che l&#39;applicazione si esaurisca. Il valore predefinito è 270 secondi.

   Il tempo di conversione visualizzato quando il file viene convertito può essere maggiore del valore qui specificato. Il Tempo di conversione include il tempo trascorso in attesa del thread o del processo, il tempo impiegato per convertire il file e il tempo impiegato dal convertitore di fallback (se applicabile). time. Il valore Specificate un timeout corrisponde solo al tempo necessario per convertire il file.

1. (Facoltativo) Nell&#39;opzione **Specifica profilo di verifica preliminare personalizzato**, fare clic su Sfoglia e selezionare un [profilo di verifica preliminare personalizzato](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). I profili di verifica preliminare vengono utilizzati solo durante la conversione di documenti in formato PDF (PDF/A).
1. Fate clic su Esporta. Al termine della conversione, viene visualizzato un collegamento al file esportato.
1. Fate clic sul collegamento per visualizzare il file convertito.

## Ottimizzare un PDF (solo Windows) {#optimize-a-pdf}

PDF Generator supporta la riduzione delle dimensioni dei file PDF.

>[!NOTE]
>
>L&#39;ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Optimize PDF.
1. Fare clic su Sfoglia per individuare il file PDF da ottimizzare.
1. Specificate le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, selezionate Usa impostazioni personalizzate, specificate le impostazioni del tipo di file e specificate un valore di timeout. Il valore predefinito è 270 secondi.
   * Per usare un file di impostazioni esistente, selezionate Carica file impostazioni e fate clic su Sfoglia per passare al percorso del file.

1. Fai clic su Crea.

