---
title: API fatturabili report transazioni
seo-title: API fatturabili report transazioni
description: Elenco di tutte le API contabilizzate come transazioni
seo-description: Elenco di tutte le API contabilizzate come transazioni
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 13016df927448d93af86899f746199e1815fdfe7
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 7%

---


# API fatturabili report transazioni{#transaction-reports-billable-apis}

 AEM Forms fornisce diverse API per l&#39;invio di moduli, l&#39;elaborazione di documenti e il rendering di documenti. Alcune API sono considerate come transazioni e altre sono gratuite da utilizzare. Questo documento fornisce un elenco di tutte le API contabilizzate come transazioni in un rapporto sulle transazioni. Di seguito sono riportati alcuni scenari comuni in cui viene utilizzata un&#39;API fatturabile:

* Invio di un modulo adattivo, un modulo HTML5 e un set di moduli
* Rendering di una versione per la stampa o il Web di una comunicazione interattiva
* Conversione di un documento da un formato a un altro
* Appiattimento di un documento PDF dinamico
* Generazione di un documento di record
* Unione di un documento PDF interattivo con un altro documento PDF
* Utilizzo della fase di assegnazione delle attività e dei passi dei servizi doc di AEM Flussi di lavoro
* Uso di moduli adattivi all&#39;interno di un modulo adattivo

Le API di fatturazione non tengono conto del numero di pagine, della lunghezza di un documento o modulo o del formato finale del documento di cui è stato effettuato il rendering. Un rapporto sulle transazioni divide le transazioni in due categorie: Documenti sottoposti a rendering e Forms inviati.

* **Forms inviato:** Quando i dati vengono inviati da qualsiasi tipo di modulo creato con  AEM Forms e i dati vengono inviati a qualsiasi archivio dati o database è considerato invio del modulo. Ad esempio, l&#39;invio di un modulo adattivo, di un modulo HTML5, di PDF forms e di un set di moduli viene contabilizzato come moduli inviati. Ciascun modulo in un set di moduli è considerato un invio. Ad esempio, se un set di moduli contiene 5 moduli, all&#39;invio del set di moduli il servizio di reporting delle transazioni li conteggia come 5 invii.

* **Documenti sottoposti a rendering:** La generazione di un documento mediante la combinazione di un modello e dati, la firma digitale o la certificazione di un documento, l&#39;utilizzo di API Document Services fatturabili per Document Services o la conversione di un documento da un formato a un altro vengono contabilizzate come documenti sottoposti a rendering.

>[!NOTE]
>
>L&#39;interfaccia utente Rapporti transazione presenta tre categorie: Forms Inviato, Documenti sottoposti a rendering e Documenti elaborati. Sia i documenti sottoposti a rendering che i documenti elaborati vengono considerati come documenti sottoposti a rendering.

## API Document Services fatturabili {#billable-document-services-apis}

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
   <td>Crea  Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea  Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converte  Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converte  Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converte  Adobe PDF in tipi di file supportati. </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crea PDF da pagine HTML.</p> </td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crea PDF da URL che puntano a una pagina HTML.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crea PDF da URL che puntano a una pagina HTML.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Ottimizza i file PDF per ridurne le dimensioni eliminando i metadati non necessari senza comprometterne la qualità.</td>
   <td>Documenti elaborati<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

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
   <td>Crea  Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crea  Adobe PDF dai tipi di file supportati.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Servizio Document of Record (DoR Service) {#document-of-record-service-dor-service}

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
   <td> L'API generatePDFOutputBatch combina un modello di modulo con un record e genera un PDF. Quando si elabora un batch di record, il servizio di reporting delle transazioni conteggia ogni record come rappresentazione PDF separata. <br> È possibile utilizzare il flag <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> per combinare più rappresentazioni in un singolo file PDF. Indipendentemente dallo stato del contrassegno, il servizio conteggia ogni record come rappresentazione PDF separata. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF nei formati PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte i documenti XDP e PDF nei formati PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte un set di documenti XDP e PDF in un set di formati di file PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documenti elaborati</td>
   <td> L'API generatePDFOutputBatch combina un modello di modulo con un record e genera un PDF. Quando si elabora un batch di record, il servizio di reporting delle transazioni conteggia ogni record come rappresentazione PDF separata. <br> È possibile utilizzare il flag <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> per combinare più rappresentazioni in un singolo file PDF. Indipendentemente dallo stato del contrassegno, il servizio conteggia ogni record come rappresentazione PDF separata. </td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderingPDFForm</a></td>
   <td>Consente di renderizzare i moduli PDF dai modelli XDP. I modelli XP vengono creati in Forms Designer.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Estrai dati da un modulo PDF o da modelli XDP</td>
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
   <td>Converte un documento PDF in un elenco di documenti immagine. I formati immagine supportati sono JPEG, JPEG2K, PNG e TIFF.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converte un file PDF semplice in formato PostScript utilizzando le opzioni specificate nella specifica delle opzioni.</td>
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
   <td>Decodifica tutti i codici a barre in un oggetto Document e restituisce un oggetto org.w3c.dom.Document contenente i dati recuperati dai codici a barre.</td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invoke</a></td>
   <td>Esegue il documento DDX specificato e restituisce un oggetto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenente i documenti risultanti. </td>
   <td>Documenti elaborati</td>
   <td>Le seguenti operazioni non sono contabilizzate come transazioni:
    <ul>
     <li>Creazione di pacchetti o portfolio</li>
     <li>Stitching di più XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invoke</a></td>
   <td>Esegue il documento DDX specificato e restituisce un oggetto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenente i documenti risultanti. </td>
   <td>Documenti elaborati</td>
   <td>Tutti i formati di file di input supportati da PDF Generator, Forms e Output Services, il servizio Assembler supporta tutti questi formati come formati di file di output. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convertire un documento specificato in PDF/A utilizzando le opzioni specificate.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* L&#39;API invoke del servizio assembler può chiamare internamente un&#39;API fatturabile di un altro servizio a seconda dell&#39;input. Pertanto, l&#39;API invoke può essere considerata come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dall&#39;input e dalle API interne richiamate.
>* Un singolo documento PDF prodotto utilizzando il servizio di assemblaggio può essere contabilizzato come nessuna, singola o più transazioni. Il numero di transazioni conteggiate dipende dal codice DDX fornito.

>



### PDF Utility Service  {#pdf-utility-service}

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
   <td>Converte un documento PDF in un file XDP. Affinché un documento PDF possa essere convertito correttamente in un file XDP, il documento PDF deve contenere un flusso XFA nel dizionario AcroForm.</td>
   <td>Documenti elaborati</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API Billable Data Capture {#billable-data-capture-apis}

Tutti gli eventi di invio di moduli adattivi, Forms HTML5 e set di moduli sono considerati transazioni. Per impostazione predefinita, l&#39;invio di un modulo PDF non viene contabilizzato come transazione. Utilizzate l&#39;API [di registrazione](record-transaction-custom-implementation.md) delle transazioni fornita per registrare l&#39;invio di PDF forms come transazione.

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
   <td>Invia un modulo adattivo a un'azione di invio configurata. </td>
   <td>Moduli inviati</td>
   <td>
    <ul>
     <li>Conto di invio riuscito per una o due transazioni. Il numero di transazioni conteggiate dipende dal tipo di azione di invio utilizzata per l'invio. Ad esempio, l'invio di PDF tramite e-mail invia account azione per due conteggi di transazioni. Una transazione per l'invio del modulo e un'altra per i PDF generati mediante il servizio DOR (Document of Record). </li>
     <li>L'utilizzo del modulo adattivo all'interno di un modulo adattivo (modulo adattivo) consente di gestire solo transazioni singole. All'interno di un modulo adattivo è possibile utilizzare un numero qualsiasi di moduli adattivi.</li>
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
   <td>Invia il modulo impostato all'URL di invio configurato nel set di moduli.</td>
   <td>Moduli inviati</td>
   <td>
    <ul>
     <li>L'utilizzo del modulo adattivo all'interno di un modulo adattivo (modulo adattivo) consente di gestire solo transazioni singole. All'interno di un modulo adattivo è possibile utilizzare un numero qualsiasi di moduli adattivi.</li>
     <li>Ogni modulo in un modulo Forms HTML5 imposta i conti come transazione separata. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Comunicazione interattiva fatturabile e flussi di lavoro AEM basati su moduli sulle API OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assegna i passaggi di task e servizi documenti dei flussi di lavoro AEM basati su modulo su OSGi e di tutte le rappresentazioni delle comunicazioni interattive e sono contabilizzati come transazioni. L’anteprima di una comunicazione interattiva sull’istanza di creazione e l’anteprima sull’istanza di pubblicazione mediante l’interfaccia utente dell’agente non vengono considerate come transazioni. Se una fase del flusso di lavoro registra una transazione e il flusso di lavoro non viene completato, il conteggio delle transazioni non viene stornato.

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
   <td>Rendering di un canale Web</td>
   <td>Apre la versione Web di una comunicazione interattiva.</td>
   <td>Documenti sottoposti a rendering</td>
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
   <td>Descrizione</td>
   <td>Categoria report transazioni</td>
   <td>Informazioni aggiuntive</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">rendering</a> (convertire in PDF)</td>
   <td>Genera la versione PDF di una comunicazione interattiva.</td>
   <td>Documenti sottoposti a rendering</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Flussi di lavoro AEM incentrati sui moduli in OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso di utilizzo</p> </td>
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
   <td>Invio di un punto di inizio applicazione di workflow </td>
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

## Registrazione di API fatturabili come transazioni per codice personalizzato {#recording-billable-apis-as-transactions-for-custom-code}

Azioni come l&#39;invio di un modulo PDF, l&#39;utilizzo dell&#39;interfaccia utente dell&#39;agente per visualizzare l&#39;anteprima di una comunicazione interattiva, l&#39;utilizzo di sottomoduli non standard e l&#39;implementazione personalizzata non vengono considerate come transazioni.  AEM Forms fornisce un&#39;API per registrare azioni come le transazioni. Puoi richiamare l&#39;API dalle tue implementazioni personalizzate per [registrare una transazione](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Panoramica dei report sulle transazioni](../../forms/using/transaction-reports-overview.md)
* [Visualizzazione e comprensione di rapporti sulle transazioni](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrazione di una transazione per le implementazioni personalizzate](/help/forms/using/record-transaction-custom-implementation.md)

