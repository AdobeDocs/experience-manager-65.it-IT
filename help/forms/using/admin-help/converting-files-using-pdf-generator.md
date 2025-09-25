---
title: Conversione di file con PDF Generator
description: Il servizio PDF Generator converte i formati di file nativi in PDF. Converte inoltre i PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1185'
ht-degree: 100%

---

# Conversione di file con PDF Generator{#converting-files-using-pdf-generator}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi utilizzare le pagine Web di PDF Generator per convertire i file.

## Creare un file PDF {#create-a-pdf-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Crea PDF.
1. Fai clic su Sfoglia per individuare e selezionare il file.

   >[!NOTE]
   >
   >PDF Generator è in grado di rilevare automaticamente il tipo di file con estensione .doc, .xls, .ppt e .rtf, anche quando nel nome del file manca l&#39;estensione. Questa funzionalità non funziona con i file .docx, .xlsx e .pptx.

1. In Impostazioni di configurazione, seleziona Usa impostazioni personalizzate o Carica il file delle impostazioni.

   * Se utilizzi impostazioni personalizzate, seleziona un’impostazione Adobe PDF, un’impostazione di sicurezza e un’impostazione del tipo di file, quindi specifica un timeout.

     Le impostazioni di Adobe PDF sono applicabili solo alle conversioni Da PS a PDF, Da EPS a PDF, Da PRN a PDF, Da immagine a PDF con OCR e Da nativo a PDF. L’impostazione di timeout specifica il tempo massimo necessario per il completamento della conversione. Il valore predefinito è 270 secondi. Queste impostazioni non vengono utilizzate durante le conversioni Da Immagine a PDF e Da OpenOffice a PDF.

   * Se stai caricando un file di impostazioni, digitane il percorso e il nome nella casella, oppure fare clic su Sfoglia per individuare e selezionare il file.

1. (Facoltativo) In File metadati XMP digita il percorso e il nome del file XMP, oppure fare clic su Sfoglia per individuare e selezionare il file. Per includere informazioni sui metadati standard, può essere utilizzato un file XMP. Consulta le [informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files).
1. Fai clic su crea. Quando il file viene creato, viene visualizzato un collegamento. Se, durante la conversione si verifica un errore, viene visualizzato un avviso. Se stai creando un file PostScript, l&#39;avviso contiene anche un collegamento al file di registro.
1. Fai clic sul collegamento del file PDF. Il file viene aperto in Acrobat.

### Informazioni sui file XMP {#about-xmp-files}

I documenti PDF creati da PDF Generator in Acrobat 5.0 o versione successiva contengono metadati di documento in formato XML. I *metadati* includono informazioni sul documento e sul relativo contenuto, ad esempio il nome dell’autore, le parole chiave e le informazioni sul copyright utilizzabili dalle utilità di ricerca.

I metadati del documento contengono informazioni (ma non solo) che vengono visualizzate anche nella scheda Descrizione della finestra di dialogo Proprietà documento in Acrobat. Le modifiche apportate nella scheda Descrizione vengon riflesse nei metadati del documento. I metadati del documento possono essere estesi e modificati utilizzando prodotti di terze parti.

Adobe Extensible Metadata Platform (XMP) fornisce alle applicazioni Adobe un framework XML comune che standardizza la creazione, l’elaborazione e lo scambio di metadati del documento tra i flussi di lavoro di pubblicazione. Puoi salvare e importare il codice sorgente XML dei metadati del documento in formato XMP per semplificare la condivisione dei metadati tra vari documenti. Per ulteriori informazioni sui file di XMP, consulta [Extensible Metadata Platform (XMP)](https://www.adobe.com/products/xmp/) e il [centro sviluppatori Adobe XMP](https://www.adobe.com/devnet/xmp.html).

Puoi creare file XMP in Acrobat.

## Convertire un file HTML o ZIP in PDF {#convert-an-html-file-or-zip-file-to-pdf}

Puoi utilizzare PDF Generator per convertire in Adobe PDF i seguenti tipi di file:

* File HTML, che è possibile convertire caricando un file HTML o specificando l’URL di una pagina Web o di un sito Web.
* File archiviati (ZIP), che possono contenere file HTML, file di immagine o entrambi.

Se il file ZIP contiene più di un file HTML al livello più basso della relativa gerarchia delle cartelle, il file ZIP deve contenere anche un file index.htm o index.html.

>[!NOTE]
>
>* La funzione da HTML a PDF richiede alcuni tipi di font nella directory dei font di sistema. Nei sistemi Linux, Solaris e AIX, la directory dei font di sistema deve contenere il font Courier. Nei sistemi Windows, la directory dei font di sistema deve contenere Times New Roman.
>
>* (Solo sistemi basati su UNIX) Per convertire una pagina Web con font giapponesi in un documento PDF, nel server AEM Forms deve essere disponibile uno dei seguenti font giapponesi.
>
>  * “Sazanami Gothic”
>  * “Kozuka Gothic Pro-VI”
>  * “Kozuka Mincho Pro-VI”
>  * “Sazanami Gothic”
>  * “Kozuka Mincho Pr6N”
>  * “Sazanami Mincho”
>  * “Adobe Heiti Std”
>  * “Adobe Song Std”
>
>* Per caricare un file dal file system locale, utilizza l’opzione Carica file, nella pagina Da HTML a PDF.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Da HTML a PDF.
1. Specifica il file da convertire eseguendo una delle operazioni seguenti:

   * In Carica file, digita il percorso e il nome del file HTML o ZIP oppure fai clic su Sfoglia per individuarlo e selezionarlo.
   * Nella casella Specifica URL, digita l’URL della pagina o del sito web da convertire.

   >[!NOTE]
   >
   >Il file da convertire deve avere un’estensione .html, .htm o .zip.

1. Specifica le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, seleziona Usa impostazioni personalizzate, specifica le impostazioni di sicurezza e del tipo di file, quindi, un valore di timeout. Il valore predefinito è 270 secondi.

   >[!NOTE]
   >
   >Se il servizio di generazione PDF è stato configurato per l’utilizzo di Acrobat WebCapture, le impostazioni dei tipi di file selezionate in questa pagina non influiscono sul PDF prodotto. Apporta invece le modifiche appropriate alla versione di Acrobat installata sul server.

   * Per utilizzare un file di impostazioni esistente, seleziona Carica file di impostazioni e fai clic su Sfoglia per passare alla posizione del file.

1. Per caricare un file XMP, fai clic su Sfoglia e passa alla posizione del file. Per includere informazioni sui metadati standard, può essere utilizzato un file XMP. (Consulta [Informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files)).
1. Fai clic su Crea. Al momento della creazione del file, viene visualizzato un collegamento al file PDF.
1. Fai clic sul collegamento per visualizzare il documento PDF in Acrobat.

## Esportare un file PDF in un altro formato di file (solo Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

È possibile esportare i file PDF in vari formati di file, come descritto nel capitolo Servizio di generazione PDF di [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Esporta PDF.
1. Fai clic su Sfoglia per individuare il file PDF da esportare.
1. Nell’elenco Esporta file PDF in, seleziona il formato in cui esportare il file PDF.
1. Nella casella Specifica un timeout, immetti il tempo di attesa prima del timeout dell’applicazione. Il valore predefinito è 270 secondi.

   Il tempo di conversione visualizzato quando il file viene convertito potrebbe essere maggiore del valore specificato in questo campo. Il tempo di conversione include il tempo trascorso in attesa del thread o del processo, il tempo impiegato per convertire il file e quello impiegato dal convertitore di fallback (se applicabile). tempo. Il valore relativo a Specifica un timeout corrisponde al tempo necessario per convertire il file.

1. (Facoltativo) Nell’opzione **Specifica profilo di verifica preliminare personalizzato**, fai clic su Sfoglia e seleziona un [profilo di verifica preliminare personalizzato](https://helpx.adobe.com/it/acrobat/using/preflight-profiles-acrobat-pro.html). I profili di verifica preliminare vengono utilizzati solo durante la conversione di documenti in formato archivio PDF (PDF/A).
1. Fai clic su Esporta. Al termine della conversione, viene visualizzato un collegamento al file esportato.
1. Fai clic sul collegamento per visualizzare il file convertito.

## Ottimizzare un PDF (solo Windows) {#optimize-a-pdf}

PDF Generator supporta la riduzione delle dimensioni dei file PDF.

>[!NOTE]
>
>L’ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Ottimizza PDF.
1. Fai clic su Sfoglia per individuare il file PDF da ottimizzare.
1. Specifica le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, seleziona Usa impostazioni personalizzate, specifica le impostazioni del tipo di file, quindi un valore di timeout. Il valore predefinito è 270 secondi.
   * Per utilizzare un file di impostazioni esistente, seleziona Carica file di impostazioni e fai clic su Sfoglia per passare alla posizione del file.

1. Fai clic su Crea.
