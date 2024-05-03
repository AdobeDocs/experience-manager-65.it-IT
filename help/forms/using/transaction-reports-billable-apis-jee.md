---
title: Rapporti sulle transazioni API fatturabili per AEM Forms su JEE.
description: Elenco di tutte le API contabilizzate come transazioni per AEM Forms su JEE.
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 3%

---

# Segnalazione delle transazioni API fatturabili per AEM Forms su JEE {#transaction-reports-billable-apis}

AEM Forms su JEE fornisce diverse API per inviare, elaborare ed eseguire il rendering di documenti. Alcune API sono contabilizzate come transazioni e altre sono libere di utilizzare. Questo documento fornisce un elenco di tutte le API contabilizzate come transazioni. Di seguito sono riportati alcuni scenari comuni in cui viene utilizzata un’API fatturabile:

* Conversione di un documento da un formato a un altro
* Appiattimento di un documento di Dynamic PDF
* Unione di un documento PDF interattivo con un altro documento PDF

Le API di fatturazione non tengono conto del numero di pagine, della lunghezza di un documento o modulo o del formato finale del documento sottoposto a rendering.
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

Di seguito è riportato l’elenco delle API JEE fatturabili. Trova l’elenco di [API fatturabili per AEM Forms su OSGi](/help/forms/using/transaction-reports-billable-apis.md).

## API di Document Services fatturabili {#billable-document-services-apis}

### Genera servizio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
  </tr>
   <tr>
   <td><a>CreaPDF</a></td>
   <td>Crea Adobe PDF per i tipi di file supportati.</td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>CreaPDF3</a></td>
   <td>Crea Adobe PDF per i tipi di file supportati. </td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>Converte il file HTML in Adobe PDF. </td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>Esporta PDF in tipi di file supportati. </td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>Esporta PDF in tipi di file supportati.</p> </td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF3</a></td>
   <td>Esporta PDF in tipi di file supportati.</td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>Converte il file HTML in PDF.</td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>Converte il file HTML in PDF.</td>
   <td>Conversione<br /> </td>
  </tr>
  <tr>
   <td><a>OptimizePDF</a></td>
   <td>Ottimizza PDF per ridurre le dimensioni dei file eliminando i metadati non necessari senza influire sulla qualità.</td>
   <td>Conversione<br /> </td>
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
  </tr>
  <tr>
   <td><a>Firma/Certifica</a><br /> </td>
   <td>Questa API consente di proteggere il documento. Puoi utilizzare l’API per firmare e certificare un documento PDF.</td>
   <td>Conversione</td>
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
  </tr>
  <tr>
  <tr>
   <td><a>CreaPDF</a></td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Conversione</td>
  </tr>
  <tr>
   <td><a>CreaPDF2</a></td>
   <td>Crea Adobe PDF dai tipi di file supportati.</td>
   <td>Conversione</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Servizio di output {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti sottoposti a rendering</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti sottoposti a rendering</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>Unisce dati e modelli per creare un documento PDF.</td>
   <td>Documenti sottoposti a rendering</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti sottoposti a rendering</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>Converte i documenti XDP e PDF in formati PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documenti sottoposti a rendering</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>Converte un set di documenti XDP e PDF in un set di formati di file PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Conversione documenti</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Converti servizio PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>Converte un documento PDF in un elenco di documenti immagine. I formati di immagine supportati sono JPEG, JPEG2K, PNG e TIFF.</td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>Converte un file Flat PDF in formato PostScript utilizzando le opzioni specificate nella specifica dell'opzione.</td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>Converte un file Flat PDF in formato SWF utilizzando le opzioni specificate nella specifica dell'opzione.</td>
   <td>Conversione documenti</td>
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
  </tr>
  <tr>
   <td><a>decodificare</a></td>
   <td>Decodifica tutti i codici a barre in un oggetto Document e restituisce un oggetto org.w3c.dom.Document contenente dati recuperati dal codice a barre.</td>
   <td>Conversione documenti</td>
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
  </tr>
  <tr>
   <td><a>richiamare</a></td>
   <td>Esegue il documento DDX specificato e restituisce un oggetto AssemblerResult contenente i documenti risultanti. </td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>Esegue il documento DDX specificato e restituisce un oggetto AssemblerResult contenente i documenti risultanti. </td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Conversione documenti</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Conversione documenti</td>
  </tr>
 </tbody>
</table>

L’utilizzo dell’API di richiamo viene conteggiato come una transazione, quando si eseguono una o più delle seguenti operazioni:
1. Conversione da formati non PDF a formati PDF. Ad esempio, la conversione dal formato XDP al formato PDF.<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversione dal formato PDF al formato PDF/A.
1. Conversione dal formato PDF a formati non PDF. Gli esempi includono la trasformazione da PDF a formato immagine o la conversione da PDF a formato testo.

>[!NOTE]
>
>* L’API di richiamo del servizio assembler può chiamare internamente un’API fatturabile di un altro servizio a seconda dell’input. Quindi, il `invoke API` può essere contabilizzata come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dall’input e dalle API interne richiamate.
>* Un singolo documento PDF prodotto utilizzando il servizio Assembler come `invoke` e `invokeDDX`, può essere contabilizzata come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dalla <!--DDX--> codice.

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## API di acquisizione dati fatturabili {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Moduli {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>Invia il modulo.</td>
   <td>Moduli inviati</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>Invia il modulo.</td>
   <td>Moduli inviati</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>Invia il modulo.</td>
   <td>Forms con rendering</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## Articoli correlati

* [Abilitazione e visualizzazione del rapporto sulle transazioni per AEM Forms su JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Registrare una transazione per le API dei componenti personalizzati per AEM Forms su JEE](/help/forms/using/record-transaction-custom-component-jee.md)
