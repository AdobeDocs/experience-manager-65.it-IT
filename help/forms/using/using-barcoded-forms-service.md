---
title: Servizio Forms con codice a barre
seo-title: Utilizzo  AEM Forms Barcoded Forms Service
description: 'Utilizzate  servizio Forms con codice a barre AEM Forms per estrarre dati da immagini elettroniche di codici a barre. '
seo-description: 'Utilizzate  servizio Forms con codice a barre AEM Forms per estrarre dati da immagini elettroniche di codici a barre. '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---


# Servizio Forms con codice a barre{#barcoded-forms-service}

## Panoramica {#overview}

Il servizio Forms Barcoded estrae i dati dalle immagini elettroniche dei codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input e li estrae. I dati del codice a barre possono essere formattati in vari modi, inclusi XML, stringhe delimitate o qualsiasi formato personalizzato creato con JavaScript.

Il servizio Forms con codice a barre supporta le seguenti simbologie **bidimensionali (2D)** fornite come documenti TIFF o PDF sottoposti a scansione:

* PDF417
* Data Matrix
* Codice QR

Il servizio supporta anche le seguenti **simologie monodimensionali** fornite come documenti TIFF o PDF sottoposti a scansione:

* Codabar
* Codice 128
* Codice 3 di 9
* EAN13
* EAN8

Potete utilizzare il servizio Forms con codice a barre per eseguire le seguenti attività:

* Estrarre i dati dei codici a barre dalle immagini dei codici a barre (TIFF o PDF). I dati vengono memorizzati come testo delimitato.
* Conversione di dati di testo delimitati in XML (XDP o XFDF). I dati XML sono più facili da analizzare rispetto al testo delimitato. Inoltre, i dati in formato XDP o XFDF possono essere utilizzati come input per altri servizi in  AEM Forms.

Per ciascun codice a barre di un&#39;immagine, il servizio Forms con codice a barre individua il codice a barre, lo decodifica ed estrae i dati. Il servizio restituisce i dati del codice a barre (utilizzando la codifica di entità dove richiesto) in un elemento di contenuto di un documento XML. Ad esempio, la seguente immagine TIFF digitalizzata di un modulo contiene due codici a barre:

![esempio](assets/example.png)

Il servizio Forms con codice a barre restituisce il seguente documento XML dopo la decodifica dei codici a barre:

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## Considerazioni per il servizio {#considerations}

### Flussi di lavoro che utilizzano moduli con codice a barre {#workflows-that-use-barcoded-forms}

Gli autori dei moduli creano moduli interattivi con codice a barre utilizzando Designer. (Vedere [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).) Quando un utente compila un modulo con codice a barre utilizzando  Adobe Reader o  Acrobat, il codice a barre viene aggiornato automaticamente per codificare i dati del modulo.

Il servizio Forms Barcoded è utile per convertire i dati esistenti sulla carta in formato elettronico. Ad esempio, quando un modulo con codice a barre viene compilato e stampato, la copia stampata può essere digitalizzata e utilizzata come input per il servizio Forms con codice a barre.

Gli endpoint delle cartelle esaminate vengono generalmente utilizzati per avviare applicazioni che utilizzano il servizio Forms con codice a barre. Ad esempio, gli scanner documenti possono salvare immagini TIFF o PDF di moduli con codice a barre in una cartella esaminata. L’endpoint cartella controllato trasmette le immagini al servizio per la decodifica.

### Formati di codifica e decodifica consigliati {#recommended-encoding-and-decoding-formats}

È consigliabile che gli autori di moduli con codice a barre utilizzino un formato semplice e delimitato (ad esempio, delimitato da tabulazioni) durante la codifica dei dati nei codici a barre. Inoltre, evitate di usare Ritorno a capo come delimitatore di campo. Designer fornisce una selezione di codifiche delimitate che generano automaticamente script JavaScript per la codifica dei codici a barre. I dati decodificati hanno i nomi dei campi sulla prima riga e i relativi valori sulla seconda riga, con schede tra ciascun campo.

Durante la decodifica dei codici a barre, specificare il carattere utilizzato per delimitare i campi. Il carattere specificato per la decodifica deve essere lo stesso utilizzato per codificare il codice a barre. Ad esempio, se si utilizza il formato delimitato da tabulazioni consigliato, l&#39;operazione Estrai in XML deve utilizzare il valore predefinito di Tab per il delimitatore di campo.

### Set di caratteri specificati dall&#39;utente {#user-specified-character-sets}

Se gli autori dei moduli aggiungono oggetti codice a barre ai moduli utilizzando Designer, è possibile specificare una codifica dei caratteri. Le codifiche riconosciute sono UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16. Per impostazione predefinita, tutti i dati sono codificati nei codici a barre come UTF-8.

Durante la decodifica dei codici a barre, è possibile specificare la codifica dei set di caratteri da utilizzare. Per garantire che tutti i dati siano decodificati correttamente, specificare lo stesso set di caratteri specificato dall&#39;autore del modulo al momento della progettazione del modulo.

### Limitazioni API {#api-limitations}

Quando utilizzate le API BCF, considerate le seguenti limitazioni:

* I moduli dinamici non sono supportati.
* I moduli interattivi non vengono decodificati correttamente, a meno che non siano appiattiti.
* I codici a barre 1D devono contenere solo valori alfanumerici (se supportati). I codici a barre 1D contenenti simboli speciali non vengono decodificati.

### Altre limitazioni {#other-limitations}

Inoltre, considerate le seguenti limitazioni quando utilizzate il servizio Forms Barcoded:

* Il servizio supporta completamente AcroForms e moduli statici contenenti codici a barre 2D salvati con  Adobe Reader o  Acrobat. Tuttavia, per i codici a barre 1D, appiattire il modulo o fornirlo come documento PDF o TIFF acquisito mediante scansione.
* I moduli XFA dinamici non sono completamente supportati. Per decodificare correttamente i codici a barre 1D e 2D in un modulo dinamico, appiattire il modulo o fornirlo come documento PDF o TIFF acquisito mediante scansione.

Inoltre, il servizio può decodificare qualsiasi codice a barre che utilizza la simbologia supportata, se vengono osservate le limitazioni di cui sopra. Per ulteriori informazioni sulla creazione di moduli con codice a barre interattivi, vedere [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Configurare le proprietà del servizio   {#configureproperties}

È possibile utilizzare il **servizio Forms con codice a barre AEMFD** nella AEM Console per configurare le proprietà per questo servizio. L&#39;URL predefinito di AEM console è `https://[host]:'port'/system/console/configMgr`.

## Utilizzo del servizio {#using}

Il servizio Forms con codice a barre fornisce le due API seguenti:

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Decodifica tutti i codici a barre disponibili in un documento PDF di input o in un&#39;immagine tiff. Restituisce un altro documento XML contenente i dati recuperati da tutti i codici a barre disponibili nel documento o nell&#39;immagine di input.

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Convertire i dati decodificati utilizzando l&#39;API di decodifica in dati XML. È possibile unire questi dati XML a un modulo XFA. Restituisce un elenco di documenti XML, uno per ciascun codice a barre.

### Utilizzo del servizio BCF con un JSP o servlet {#using-bcf-service-with-a-jsp-or-servlets}

Il seguente codice di esempio decodifica un codice a barre in un documento e salva il codice XML di output sul disco.

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // Please see Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // Please see javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### Utilizzo del servizio BCF con flussi di lavoro AEM {#using-the-bcf-service-with-aem-workflows}

L&#39;esecuzione del servizio Forms con codice a barre da un flusso di lavoro è simile all&#39;esecuzione del servizio da JSP/Servlet. L&#39;unica differenza consiste nell&#39;eseguire il servizio da JSP/Servlet l&#39;oggetto document recupera automaticamente un&#39;istanza dell&#39;oggetto ResourceResolver dall&#39;oggetto ResourceResolverHelper. Questo meccanismo automatico non funziona quando il codice viene chiamato da un flusso di lavoro.

Per un flusso di lavoro, passare esplicitamente un&#39;istanza dell&#39;oggetto ResourceResolver al costruttore della classe Document. Quindi, l&#39;oggetto Document utilizza l&#39;oggetto ResourceResolver fornito per leggere il contenuto dalla directory archivio.

Il seguente processo di flusso di lavoro di esempio decodifica un codice a barre in un documento e salva il risultato su disco. Il codice viene scritto in ECMAScript e il documento viene trasmesso come payload del flusso di lavoro:

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

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

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```

