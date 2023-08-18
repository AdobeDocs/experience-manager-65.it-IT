---
title: Report transazioni API fatturabili
seo-title: Transaction Reports Billable APIs
description: Elenco di tutte le API contabilizzate come transazioni
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: d636d987f5d62c9169bc4015d7ac50090e362faa
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 6%

---

# Report transazioni API fatturabili{#transaction-reports-billable-apis}

AEM Forms fornisce diverse API per inviare moduli, elaborare documenti ed eseguire il rendering di documenti. Alcune API sono contabilizzate come transazioni e altre sono libere di utilizzare. Questo documento fornisce un elenco di tutte le API contabilizzate come transazioni in un report sulle transazioni. Di seguito sono riportati alcuni scenari comuni in cui viene utilizzata un’API fatturabile:

* Invio di un modulo adattivo, di un modulo HTML5 e di un set di moduli
* Rendering di una versione stampata o web di una comunicazione interattiva
* Conversione di un documento da un formato a un altro
* Appiattimento di un documento di Dynamic PDF
* Generazione di un documento di record
* Unione di un documento PDF interattivo con un altro documento PDF
* Utilizzo dei passaggi Assegna attività e Servizi documentali dei flussi di lavoro AEM
* Utilizzo di un modulo adattivo all’interno di un modulo adattivo

Le API di fatturazione non tengono conto del numero di pagine, della lunghezza di un documento o modulo o del formato finale del documento sottoposto a rendering. Un report di transazioni suddivide le transazioni in due categorie: Documenti sottoposti a rendering e Forms inviati.

* **Forms inviato:** Quando i dati vengono inviati da qualsiasi tipo di modulo creato con AEM Forms e vengono inviati a qualsiasi archivio di dati o database, viene considerato invio modulo. L’invio di un modulo adattivo, di un modulo HTML5, di PDF forms e di un set di moduli, ad esempio, viene considerato come moduli inviati. Ogni modulo di un set di moduli è considerato un inoltro. Ad esempio, se una serie di moduli contiene 5 moduli, quando la serie di moduli viene sottomessa, il servizio di reporting delle transazioni conteggia tale serie come 5 invii.

* **Documenti sottoposti a rendering:** La generazione di un documento mediante la combinazione di un modello e di dati, la firma o la certificazione digitale di un documento, l&#39;utilizzo di un&#39;API di servizi di gestione dei documenti fatturabile per i servizi di gestione dei documenti o la conversione di un documento da un formato a un altro vengono considerati documenti sottoposti a rendering.

>[!NOTE]
>
>Nell’interfaccia utente Rapporti transazioni sono visualizzate tre categorie: Forms Inviato, Documenti sottoposti a rendering ed Elaborati. Sia i documenti sottoposti a rendering che i documenti elaborati vengono considerati documenti sottoposti a rendering.

## API di Document Services fatturabili {#billable-document-services-apis}

### Genera servizio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converte Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converte Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converte Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crea PDF dalle pagine HTML.</p> </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crea PDF dagli URL che puntano a una pagina HTML.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crea PDF dagli URL che puntano a una pagina HTML.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Ottimizza PDF per ridurre le dimensioni dei file eliminando i metadati non necessari senza influire sulla qualità.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>Questa API consente di proteggere il documento. Puoi utilizzare l’API per firmare, certificare, estendere o crittografare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td>Vengono fatturate solo le operazioni di firma e certificazione di secureDocument.</td>
  </tr>
 </tbody>
</table>


### Servizio Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio documenti di record (servizio DoR) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">rendering</a></td>
   <td>Richiama il metodo di rendering specificato per generare un documento di record utilizzando i parametri forniti.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio di output {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Unisce dati e modelli per creare un set di documenti PDF.</td>
   <td>Documenti elaborati</td>
   <td> L’API generatePDFOutputBatch combina un modello di modulo con un record e genera un PDF. Quando si elabora un batch di record, il servizio di reporting delle transazioni conta ogni record come una rappresentazione PDF separata. <br> È possibile utilizzare <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag per combinare più rappresentazioni in un singolo file PDF. Indipendentemente dallo stato del flag, il servizio conta ogni record come una rappresentazione PDF separata. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte un set di documenti XDP e PDF in un set di formati di file PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> L’API generatePDFOutputBatch combina un modello di modulo con un record e genera un PDF. Quando si elabora un batch di record, il servizio di reporting delle transazioni conta ogni record come una rappresentazione PDF separata. <br> È possibile utilizzare <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag per combinare più rappresentazioni in un singolo file PDF. Indipendentemente dallo stato del flag, il servizio conta ogni record come una rappresentazione PDF separata. </td>
  </tr>
 </tbody>
</table>

### Servizio Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Esegue il rendering del modulo PDF dai modelli XDP. I modelli XP vengono creati in Forms Designer.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Estrae dati da un modulo PDF o da modelli XDP</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Converti servizio PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converte un documento PDF in un elenco di documenti immagine. I formati di immagine supportati sono JPEG, JPEG2K, PNG e TIFF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converte un file Flat PDF in formato PostScript utilizzando le opzioni specificate nella specifica dell'opzione.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio Forms con codice a barre {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decodificare</a></td>
   <td>Decodifica tutti i codici a barre in un oggetto Document e restituisce un oggetto org.w3c.dom.Document contenente dati recuperati dal codice a barre.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio assemblatore {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">richiamare</a></td>
   <td>Esegue il documento DDX specificato e restituisce un <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> oggetto contenente i documenti risultanti. </td>
   <td>Documenti elaborati</td>
   <td>Le seguenti operazioni non sono contabilizzate come operazioni:
    <ul>
     <li>Creazione di pacchetti o portfolio</li>
     <li>Unione di più XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">richiamare</a></td>
   <td>Esegue il documento DDX specificato e restituisce un <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> oggetto contenente i documenti risultanti. </td>
   <td>Documenti elaborati</td>
   <td>Tutti i formati di file di input supportati dai servizi PDF Generator, Forms e Output, il servizio Assembler supporta tutti questi formati come formati di file di output. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

L’utilizzo dell’API di richiamo viene conteggiato come una transazione, quando si eseguono una o più delle seguenti operazioni:
1. Conversione da formati non PDF a formati PDF. Ad esempio, la conversione dal formato XDP al formato PDF, che include forme di comunicazione interattive e non interattive, e la conversione da Word a PDF.
1. Conversione dal formato PDF al formato PDF/A.
1. Conversione dal formato PDF a formati non PDF. Gli esempi includono la trasformazione da PDF a formato immagine o la conversione da PDF a formato testo.

>[!NOTE]
>
>* L’API di richiamo del servizio assembler può chiamare internamente un’API fatturabile di un altro servizio a seconda dell’input. Pertanto, l’API di richiamo può essere contabilizzata come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dall’input e dalle API interne richiamate.
>* Un singolo documento PDF prodotto utilizzando il servizio assembler può essere contabilizzato come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dal codice DDX fornito.

### Servizio Utilità PDF  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converte un documento PDF in un file XDP. Affinché un documento PDF possa essere convertito in un file XDP, il documento PDF deve contenere un flusso XFA nel dizionario AcroForm.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API di acquisizione dati fatturabili {#billable-data-capture-apis}

Tutti gli eventi di invio di moduli adattivi, HTML5 Forms e set di moduli vengono contabilizzati come transazioni. Per impostazione predefinita, l’invio di un modulo PDF non viene contabilizzato come una transazione. Utilizza il fornito [API registratore transazioni](record-transaction-custom-implementation.md) per registrare un invio di PDF forms come transazione.

### Moduli adattivi {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso d’uso </p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un modulo adattivo</td>
   <td>Invia un modulo adattivo all’azione di invio configurata. </td>
   <td>Moduli inviati</td>
   <td>
    <ul>
     <li>Account invio corretto per una o due transazioni. Il numero di transazioni conteggiate dipende dal tipo di azione di invio utilizzato per la sottomissione. Ad esempio, l’invio di PDF tramite un’azione di invio tramite e-mail tiene conto di due conteggi di transazioni. Una transazione per l’invio di moduli e un’altra per PDF generata utilizzando il servizio Document of Record (DOR). </li>
     <li>L’utilizzo del modulo adattivo all’interno di un modulo adattivo (set di moduli adattivi) contabilizza una sola transazione. All’interno di un modulo adattivo è possibile disporre di un numero qualsiasi di moduli adattivi.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Moduli HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso d’uso </p> </td>
   <td>Descrizione </td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un modulo HTML5</td>
   <td>Invia un modulo HTML5 per inviare l’URL configurato nel modulo.</td>
   <td>Moduli inviati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Set di moduli {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un set di moduli</td>
   <td>Invia il set di moduli all’URL di invio configurato nel set di moduli.</td>
   <td>Moduli inviati</td>
   <td>
    <ul>
     <li>L’utilizzo del modulo adattivo all’interno di un modulo adattivo (set di moduli adattivi) contabilizza una sola transazione. All’interno di un modulo adattivo è possibile disporre di un numero qualsiasi di moduli adattivi.</li>
     <li>Ogni modulo di un set di moduli HTML5 Forms viene contabilizzato come transazione separata. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Flussi di lavoro AEM basati su moduli e comunicazione interattiva fatturabili sulle API OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assegna i passaggi dei servizi relativi alle attività e ai documenti dei flussi di lavoro AEM basati su moduli su OSGi e tutte le rappresentazioni della comunicazione interattiva e vengono contabilizzati come transazioni. L’anteprima di una comunicazione interattiva sull’istanza di authoring e l’anteprima sull’istanza di pubblicazione utilizzando l’interfaccia utente dell’agente non vengono considerate transazioni. Se un passaggio del flusso di lavoro contabilizza una transazione e il flusso di lavoro non viene completato, il conteggio delle transazioni non viene stornato.

### Comunicazione interattiva - Canale web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Rendering di un canale web</td>
   <td>Apre la versione Web di una comunicazione interattiva.</td>
   <td>Documenti sottoposti a rendering</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Comunicazione interattiva - Canale di stampa {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">rendering</a> (converti in PDF)</td>
   <td>Genera la versione PDF di una comunicazione interattiva.</td>
   <td>Documenti sottoposti a rendering</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Flussi di lavoro AEM basati su moduli su OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso d’uso</p> </td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td>Invio di un passaggio Assegna attività</td>
   <td>Moduli inviati</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Invio di un punto d'inizio di un'applicazione del flusso di lavoro </td>
   <td>Moduli inviati</td>
   <td> </td>
  </tr>
  <tr>
   <td>Invio di una comunicazione interattiva (canale di stampa) dall’interfaccia utente dell’agente a un flusso di lavoro</td>
   <td>Documenti sottoposti a rendering</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrazione di API fatturabili come transazioni per il codice personalizzato {#recording-billable-apis-as-transactions-for-custom-code}

Azioni come l’invio di un modulo PDF, l’utilizzo dell’interfaccia utente dell’agente per visualizzare in anteprima una comunicazione interattiva, l’utilizzo di un invio di modulo non standard e le implementazioni personalizzate non vengono considerate come transazioni. AEM Forms fornisce un’API per registrare azioni quali le transazioni. Puoi richiamare l’API dalle implementazioni personalizzate a [registrare una transazione](/help/forms/using/record-transaction-custom-implementation.md).

## Articoli correlati {#related-articles}

* [Panoramica dei rapporti sulle transazioni](../../forms/using/transaction-reports-overview.md)
* [Visualizzazione e comprensione dei rapporti sulle transazioni](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrare una transazione per le implementazioni personalizzate](/help/forms/using/record-transaction-custom-implementation.md)
