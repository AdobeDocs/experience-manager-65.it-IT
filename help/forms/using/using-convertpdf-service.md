---
title: Servizio ConvertPDF
seo-title: ConvertPDF Service
description: Utilizzare il servizio AEM Forms ConvertPDF per convertire i documenti PDF in file PostScript o di immagine.
seo-description: Use AEM Forms ConvertPDF service to convert PDF documents to PostScript or image files.
uuid: 7fa94c8c-485b-4a77-bcd3-ed716e3cf316
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 5ec4f0ec-a9fd-4571-9b9a-278f4622c028
exl-id: 575bab27-d973-47fa-a0da-fa889cec6f27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Servizio ConvertPDF {#convertpdf-service}

## Panoramica {#overview}

Il servizio Convert PDF converte i documenti PDF in file PostScript o di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano documenti PDF.

Con il servizio Convert PDF puoi effettuare le seguenti operazioni:

* Convertire documenti PDF in PostScript. Durante la conversione in PostScript, è possibile utilizzare l&#39;operazione di conversione per specificare il documento di origine e se convertire in PostScript di livello 2 o 3. Il documento PDF convertito in un file PostScript deve essere non interattivo.
* Convertire i documenti PDF in formati immagine JPEG, JPEG 2000, PNG e TIFF. Durante la conversione in uno qualsiasi di questi formati immagine, è possibile utilizzare l&#39;operazione di conversione per specificare il documento di origine e le specifiche delle opzioni immagine. La specifica contiene varie preferenze, come il formato di conversione delle immagini, la risoluzione delle immagini e la conversione del colore.

## Configurare le proprietà del servizio   {#properties}

È possibile utilizzare **Servizio Converti PDF AEMFD** in AEM Console per configurare le proprietà per questo servizio. L’URL predefinito di AEM console è `https://[host]:'port'/system/console/configMgr`.

## Utilizzo del servizio {#using-the-service}

Il servizio ConvertPDF fornisce le due API seguenti:

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**: Converte un documento PDF in un file PostScript.

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**: Converte un documento PDF in un file di immagine. I formati immagine supportati sono JPEG, JPEG2000, PNG e TIFF.

### Utilizzo dell’API toPS con JSP o Servlets {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript langauge
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### Utilizzo dell’API toImage con JSP o Servlets {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### Utilizzo del servizio ConvertPDF con flussi di lavoro AEM {#using-convertpdf-service-with-aem-workflows}

L&#39;esecuzione del servizio ConvertPDF da un flusso di lavoro è simile all&#39;esecuzione da JSP/Servlet.

L&#39;unica differenza consiste nell&#39;eseguire il servizio da JSP/Servlet l&#39;oggetto document recupera automaticamente un&#39;istanza dell&#39;oggetto ResourceResolver dall&#39;oggetto ResourceResolverHelper. Questo meccanismo automatico non funziona quando il codice viene richiamato da un flusso di lavoro. Per un flusso di lavoro, passare esplicitamente un&#39;istanza dell&#39;oggetto ResourceResolver al costruttore della classe Document. Quindi, l&#39;oggetto Document utilizza l&#39;oggetto ResourceResolver fornito per leggere il contenuto dal repository.

Il seguente processo di flusso di lavoro di esempio converte il documento di input in un documento PostScript. Il codice viene scritto in ECMAScript e il documento viene passato come payload del flusso di lavoro:

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from
 * crx repository.
 */

/* get ResourceResolverFactory service reference , used
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path
var inputDocument = new Document(payload_path, resourceResolver);

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
