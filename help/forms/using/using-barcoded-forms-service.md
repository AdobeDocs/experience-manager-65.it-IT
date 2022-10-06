---
title: Servizio Forms barcoded
seo-title: Using AEM Forms Barcoded Forms Service
description: Utilizza il servizio Forms Barcoded AEM Forms per estrarre dati da immagini elettroniche di codici a barre.
seo-description: Use AEM Forms Barcoded Forms service to extract data from electronic images of barcodes.
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Servizio Forms barcoded{#barcoded-forms-service}

## Panoramica {#overview}

Il servizio Forms Barcoded estrae i dati dalle immagini elettroniche dei codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input ed estrae i dati dei codici a barre. I dati dei codici a barre possono essere formattati in vari modi, inclusi XML, stringa delimitata o qualsiasi formato personalizzato creato con JavaScript.

Il servizio Forms con codice a barre supporta quanto segue **bidimensionale (2D)** simbologie fornite come documenti TIFF o PDF digitalizzati:

* PDF417
* Data Matrix
* Codice QR

Il servizio supporta anche quanto segue **unidimensionale** simbologie fornite come documenti TIFF o PDF digitalizzati:

* Codabar
* Codice 128
* Codice 3 di 9
* EAN13
* EAN8

Puoi utilizzare il servizio Forms con codice a barre per eseguire le seguenti attività:

* Estrarre dati dai codici a barre dalle immagini dei codici a barre (TIFF o PDF). I dati vengono memorizzati come testo delimitato.
* Converti dati di testo delimitati in XML (XDP o XFDF). I dati XML sono più facili da analizzare rispetto al testo delimitato. Inoltre, i dati in formato XDP o XFDF possono essere utilizzati come input per altri servizi in AEM Forms.

Per ogni codice a barre di un’immagine, il servizio Forms a barre individua il codice a barre, lo decodifica ed estrae i dati. Il servizio restituisce i dati del codice a barre (utilizzando la codifica delle entità, se necessario) in un elemento di contenuto di un documento XML. Ad esempio, la seguente immagine TIFF digitalizzata di un modulo contiene due codici a barre:

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

Gli autori dei moduli creano moduli interattivi con codice a barre utilizzando Designer. (Vedi [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).) Quando un utente compila un modulo con codice a barre utilizzando Adobe Reader o Acrobat, il codice a barre viene aggiornato automaticamente per codificare i dati del modulo.

Il servizio Forms Barcoded è utile per convertire i dati esistenti su carta in formato elettronico. Ad esempio, quando un modulo con codice a barre viene compilato e stampato, la copia stampata può essere scansionata e utilizzata come input per il servizio Forms con codice a barre.

Gli endpoint per cartelle controllate vengono generalmente utilizzati per avviare applicazioni che utilizzano il servizio Forms Barcoded. Ad esempio, gli scanner documenti possono salvare immagini TIFF o PDF di moduli con codice a barre in una cartella controllata. L&#39;endpoint della cartella controllata trasmette le immagini al servizio per la decodifica.

### Formati di codifica e decodifica consigliati {#recommended-encoding-and-decoding-formats}

Gli autori di moduli con codice a barre sono invitati a utilizzare un formato semplice e delimitato, ad esempio delimitato da tabulazioni, durante la codifica dei dati nei codici a barre. Inoltre, evita di utilizzare Ritorno a capo come delimitatore di campo. Designer fornisce una selezione di codifiche delimitate che generano automaticamente script JavaScript per la codifica dei codici a barre. I dati decodificati presentano i nomi dei campi nella prima riga e i relativi valori nella seconda riga, con schede tra ciascun campo.

Quando si decodificano i codici a barre, specificare il carattere utilizzato per delimitare i campi. Il carattere specificato per la decodifica deve essere lo stesso utilizzato per la codifica del codice a barre. Ad esempio, se si utilizza il formato delimitato da tabulazioni consigliato, l’operazione Extract to XML deve utilizzare il valore predefinito Tab per il delimitatore di campo.

### Set di caratteri specificati dall’utente {#user-specified-character-sets}

Quando gli autori di moduli aggiungono oggetti codice a barre ai moduli utilizzando Designer, possono specificare una codifica dei caratteri. Le codifiche riconosciute sono UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16. Per impostazione predefinita, tutti i dati vengono codificati nei codici a barre come UTF-8.

Quando si decodificano i codici a barre, è possibile specificare la codifica del set di caratteri da utilizzare. Per garantire la corretta decodifica di tutti i dati, specificare lo stesso set di caratteri specificato dall’autore del modulo al momento della progettazione.

### Limitazioni delle API {#api-limitations}

Quando utilizzi le API BCF, prendi in considerazione le seguenti limitazioni:

* I moduli dinamici non sono supportati.
* I moduli interattivi non vengono decodificati correttamente, a meno che non siano appiattiti.
* I codici a barre 1-D devono contenere solo valori alfanumerici (se supportati). I codici a barre 1D contenenti simboli speciali non vengono decodificati.

### Altre limitazioni {#other-limitations}

Inoltre, quando utilizzi il servizio Forms Barcoded, considera le seguenti limitazioni:

* Il servizio supporta completamente AcroForms e moduli statici contenenti codici a barre 2D salvati con Adobe Reader o Acrobat. Tuttavia, per i codici a barre 1D, appiattire il modulo o fornirlo come documento PDF o TIFF digitalizzato.
* I moduli XFA dinamici non sono completamente supportati. Per decodificare correttamente i codici a barre 1D e 2D in un modulo dinamico, appiattire il modulo o fornirlo come documento PDF o TIFF digitalizzato.

Inoltre, il servizio può decodificare qualsiasi codice a barre che utilizza la simbologia supportata se vengono osservate le limitazioni di cui sopra. Per ulteriori informazioni sulla creazione di moduli interattivi con codice a barre, consultare [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Configurare le proprietà del servizio   {#configureproperties}

È possibile utilizzare **Servizio Forms con codice a barre AEM** in AEM Console per configurare le proprietà per questo servizio. L’URL predefinito di AEM console è `https://[host]:'port'/system/console/configMgr`.

## Utilizzo del servizio {#using}

Il servizio Forms con codice a barre fornisce le due API seguenti:

* **[decodificare](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Decodifica tutti i codici a barre disponibili in un documento di input PDF o in un’immagine tiff. Restituisce un altro documento XML contenente i dati recuperati da tutti i codici a barre disponibili nel documento di input o nell&#39;immagine.

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: Converti i dati decodificati utilizzando l’API di decodifica in dati XML. È possibile unire questi dati XML con un modulo XFA. Restituisce un elenco di documenti XML, uno per ciascun codice a barre.

### Utilizzo del servizio BCF con JSP o Servlet {#using-bcf-service-with-a-jsp-or-servlets}

Il codice di esempio seguente decodifica un codice a barre in un documento e salva il codice XML di output sul disco.

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

L’esecuzione del servizio Forms con codice a barre da un flusso di lavoro è simile all’esecuzione del servizio da JSP/Servlet. L&#39;unica differenza consiste nell&#39;eseguire il servizio da JSP/Servlet l&#39;oggetto document recupera automaticamente un&#39;istanza dell&#39;oggetto ResourceResolver dall&#39;oggetto ResourceResolverHelper. Questo meccanismo automatico non funziona quando il codice viene richiamato da un flusso di lavoro.

Per un flusso di lavoro, passare esplicitamente un&#39;istanza dell&#39;oggetto ResourceResolver al costruttore della classe Document. Quindi, l&#39;oggetto Document utilizza l&#39;oggetto ResourceResolver fornito per leggere il contenuto dal repository.

Il seguente processo di flusso di lavoro di esempio decodifica un codice a barre in un documento e salva il risultato su disco. Il codice viene scritto in ECMAScript e il documento viene passato come payload del flusso di lavoro:

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
