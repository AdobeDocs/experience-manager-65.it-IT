---
title: Conversione di file tramite PDF Generator
seo-title: Converting files using PDF Generator
description: Scopri come convertire i file utilizzando PDF Generator.
seo-description: Learn how to convert files using PDF Generator.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Conversione di file tramite PDF Generator{#converting-files-using-pdf-generator}

È possibile utilizzare le pagine web di PDF Generator per convertire i file.

## Creare un file PDF {#create-a-pdf-file}

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > Crea PDF.
1. Fai clic su Sfoglia per trovare e selezionare il file.

   >[!NOTE]
   >
   >PDF Generator è in grado di rilevare automaticamente il tipo di file dei file .doc, .xls, .ppt e .rtf, anche quando l’estensione del file manca al nome del file. Questa funzione non funziona con file .docx, .xlsx e .pptx.

1. In Impostazioni di configurazione, seleziona Usa impostazioni personalizzate o Carica file impostazioni.

   * Se utilizzi impostazioni personalizzate, seleziona un’impostazione Adobe PDF, un’impostazione di protezione e un tipo di file e specifica un timeout.

      Le impostazioni di Adobe PDF sono applicabili solo alle conversioni da PS a PDF, da EPS a PDF, da PRN a PDF, da immagine a PDF con OCR attivo e da nativo a PDF. L’impostazione time-out specifica il tempo massimo necessario al completamento della conversione. Il valore predefinito è 270 secondi. Queste impostazioni non vengono utilizzate durante le conversioni da Image-to-PDF e da OpenOffice-to-PDF.

   * Se si sta caricando un file di impostazioni, digitare il percorso e il nome nella casella oppure fare clic su Sfoglia per trovare e selezionare il file.

1. (Facoltativo) In XMP file metadati, digitare il percorso e il nome del file di XMP oppure fare clic su Sfoglia per trovare e selezionare il file. Un file XMP può essere utilizzato per includere informazioni di metadati standard. (Vedi [Informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Quando il file viene creato, viene visualizzato un collegamento a esso. Se si verifica un errore durante la conversione, viene visualizzato un avviso. Se si sta creando un file Postscript, l&#39;avviso contiene anche un collegamento al file di registro.
1. Fare clic sul collegamento relativo al file PDF. Il file viene aperto in Acrobat.

### Informazioni sui file XMP {#about-xmp-files}

I documenti PDF creati da PDF Generator in Acrobat 5.0 o versioni successive contengono i metadati del documento in formato XML. *Metadati* include informazioni sul documento e sul relativo contenuto, ad esempio nome dell&#39;autore, parole chiave e informazioni sul copyright utilizzabili dalle utilità di ricerca.

I metadati del documento contengono (ma non sono limitati a) informazioni che vengono visualizzate anche nella scheda Descrizione della finestra di dialogo Proprietà documento in Acrobat. Le modifiche apportate nella scheda Descrizione vengono riportate nei metadati del documento. I metadati dei documenti possono essere estesi e modificati utilizzando prodotti di terze parti.

Adobe Extensible Metadata Platform (XMP) fornisce alle applicazioni di Adobe un framework XML comune che standardizza la creazione, l’elaborazione e lo scambio di metadati dei documenti tra flussi di lavoro di pubblicazione. È possibile salvare e importare il codice sorgente XML dei metadati del documento in XMP formato, facilitando la condivisione dei metadati tra i vari documenti. Per ulteriori informazioni sui file XMP, vedi [Piattaforma di metadati estensibili (XMP)](https://www.adobe.com/products/xmp/) e [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html).

È possibile creare file XMP in Acrobat.

## Convertire un file HTML o ZIP in PDF {#convert-an-html-file-or-zip-file-to-pdf}

È possibile utilizzare PDF Generator per convertire i seguenti tipi di file in Adobe PDF:

* File HTML, che è possibile convertire caricando un file HTML o specificando l’URL di una pagina web o di un sito web.
* File archiviati (ZIP), che possono contenere file HTML, file immagine o entrambi.

Se il file ZIP contiene più di un file HTML al livello più basso della gerarchia delle cartelle, anche il file ZIP deve contenere un file index.htm o index.html.

>[!NOTE]
>
>* La funzione da HTML a PDF richiede alcuni font nella directory dei font di sistema. Nei sistemi Linux, Solaris e AIX, la directory dei font di sistema deve contenere il font Courier. Nei sistemi Windows, la directory dei font di sistema deve contenere Times New Roman.
>
>* (Solo sistema basato su UNIX) Uno dei seguenti font giapponesi deve essere disponibile sul server AEM Forms per convertire una pagina web con font giapponese in un documento PDF.
>
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* Per caricare un file dal file system locale, utilizza l’opzione Carica file nella pagina HTML-PDF.


1. Nella console di amministrazione, fare clic su Servizi > Generatore di PDF > da HTML a PDF.
1. Specificare il file da convertire eseguendo una delle operazioni seguenti:

   * In Carica file digitare il percorso e il nome del file HTML o del file ZIP oppure fare clic su Sfoglia per individuarlo e selezionarlo.
   * Nella casella Specifica URL digitare l’URL della pagina o del sito Web da convertire.

   >[!NOTE]
   >
   >Il file che si sta convertendo deve avere un&#39;estensione del nome del file .html, .htm o .zip.

1. Specifica le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, selezionare Usa impostazioni personalizzate, specificare la protezione e le impostazioni del tipo di file e specificare un valore di timeout. Il valore predefinito è 270 secondi.
   >[!NOTE]
   >
   >Se il servizio Generate PDF è stato configurato per l&#39;utilizzo di Acrobat WebCapture, le impostazioni relative al tipo di file selezionate in questa pagina non influiscono sul PDF prodotto. Apporta le modifiche appropriate alla versione di Acrobat installata sul server.

   * Per utilizzare un file di impostazioni esistente, selezionare Carica file di impostazioni e fare clic su Sfoglia per passare al percorso del file.


1. Per caricare un file XMP, fare clic su Sfoglia e passare al percorso del file. Un file XMP può essere utilizzato per includere informazioni di metadati standard. (Vedi [Informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Quando il file viene creato, viene visualizzato un collegamento al file PDF.
1. Fai clic sul collegamento per visualizzare il documento PDF in Acrobat.

## Esportare un file PDF in un altro formato di file (solo Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

È possibile esportare i file PDF in vari formati di file, come descritto nel capitolo Generate PDF Service di [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Export PDF.
1. Fare clic su Sfoglia per individuare il file PDF da esportare.
1. Nell’elenco File di Export PDF in, selezionare il formato in cui esportare il file PDF.
1. Nella casella Specifica un timeout immettere il tempo di attesa prima che l&#39;applicazione si esaurisca. Il valore predefinito è 270 secondi.

   Il tempo di conversione visualizzato quando il file viene convertito può essere maggiore del valore qui specificato. Il Tempo di conversione include il tempo trascorso in attesa del thread o del processo, il tempo impiegato per convertire il file e il tempo impiegato dal convertitore di fallback (se applicabile). time. Il valore Specifica un timeout è solo il tempo impiegato per convertire il file.

1. (Facoltativo) In **Specifica profilo di verifica preliminare personalizzato** fare clic su Sfoglia e selezionare un&#39;opzione [profilo di verifica preliminare personalizzato](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). I profili di verifica preliminare vengono utilizzati solo durante la conversione dei documenti in formato archivio PDF (PDF/A).
1. Fai clic su Esporta. Al termine della conversione, viene visualizzato un collegamento al file esportato.
1. Fai clic sul collegamento per visualizzare il file convertito.

## Ottimizzare un PDF (solo Windows) {#optimize-a-pdf}

PDF Generator supporta la riduzione delle dimensioni dei file PDF.

>[!NOTE]
>
>L’ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > Optimize PDF.
1. Fare clic su Sfoglia per individuare il file PDF da ottimizzare.
1. Specifica le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, selezionare Usa impostazioni personalizzate, specificare le impostazioni del tipo di file e specificare un valore di timeout. Il valore predefinito è 270 secondi.
   * Per utilizzare un file di impostazioni esistente, selezionare Carica file di impostazioni e fare clic su Sfoglia per passare al percorso del file.

1. Fai clic su Crea.
