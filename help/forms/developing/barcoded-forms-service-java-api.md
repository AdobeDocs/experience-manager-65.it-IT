---
title: Servizio Forms in codice a barre Java&trade; API Quick Start(SOAP)
description: Scopri in che modo il Servizio Forms in codice a barre Java&trade; API Quick Start (SOAP) in AEM Forms consente l’elaborazione fluida dei codici a barre.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 907c12be-dab4-48b5-9da1-a76b711f49f2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Guida introduttiva rapida (SOAP) dell’API Java™ di Forms Service in codice a barre {#barcoded-forms-service-java-apiquick-start-soap}

Java™ API Quick Start(SOAP) è disponibile per il servizio Barcoded Forms:

[Guida rapida (modalità SOAP): decodificare i dati dei moduli con codice a barre utilizzando Java](barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>Gli avvii rapidi nella programmazione con AEM Forms si basano sul server Forms distribuito su JBoss® Application Server e sul sistema operativo Microsoft® Windows. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX®, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Quick Start (modalità SOAP): decodifica dei dati dei moduli codificati a barre tramite l’API Java™ {#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api}

Il seguente codice Java™ decodifica i dati del modulo presenti in un modulo di PDF salvato come Loan.pdf. I dati decodificati vengono salvati come file XML denominato extractedData.xml. Questo esempio di codice converte un oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document`. (Vedi [Decodifica dei dati del modulo con codice a barre](/help/forms/developing/barcoded-forms.md#decoding-barcoded-form-data).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-barcodedforms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.*;
 import java.util.Iterator;
 import java.util.List;
 import java.util.Properties;
 import javax.xml.transform.*;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 import com.adobe.livecycle.barcodedforms.CharSet;
 import com.adobe.livecycle.barcodedforms.Delimiter ;
 import com.adobe.livecycle.barcodedforms.XMLFormat ;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.barcodedforms.client.*;
 
 public class DecodeFormDataSOAP {
 
     public static void main(String[] args) {
 
     try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         BarcodedFormsServiceClient barClient = new BarcodedFormsServiceClient(myFactory);
 
         //Specify a PDF document to convert to an XDP file
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanBarForms.pdf");
         Document inDoc = new Document (fileInputStream);
 
         java.lang.Boolean myFalse = new java.lang.Boolean(false);
         java.lang.Boolean myTrue = new java.lang.Boolean(true);
 
         //Decode barcoded form data
         org.w3c.dom.Document decodeXML = barClient.decode(
             inDoc,
             myTrue,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             myFalse,
             CharSet.UTF_8);
 
         //Convert the decoded data to XDP data
         List extractedData = barClient.extractToXML(
             decodeXML,
             Delimiter.Carriage_Return,
             Delimiter.Tab,
             XMLFormat.XDP);
 
         //Create an Iterator object and iterate through
         //the List object
         Iterator iter = extractedData.iterator();
         int i = 0 ;
 
         while (iter.hasNext()) {
 
             //Get the org.w3c.dom.Document object in each element
             org.w3c.dom.Document myDom = (org.w3c.dom.Document)iter.next();
 
             //Convert the org.w3c.dom.Document object to a
             //com.adobe.idp.Document object
             com.adobe.idp.Document myDocument = convertDOM(decodeXML);
 
             //Save the XML data to extractedData.xml
             File myFile = new File("C:\\Adobe\extractedData"+i+".xml");
 
             myDocument.copyToFile(myFile);
             i++;
             }
         }
     catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 
 
     //This user-defined method converts an org.w3c.dom.Document to a
     //com.adobe.idp.Document object
     public static com.adobe.idp.Document convertDOM(org.w3c.dom.Document doc)
         {
 
             byte[] mybytes = null ;
         com.adobe.idp.Document myDocument = null;
         try
             {
 
             //Create a Java Transformer object
          TransformerFactory transFact = TransformerFactory.newInstance();
          Transformer transForm = transFact.newTransformer();
 
          //Create a Java ByteArrayOutputStream object
          ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
 
         //Create a Java Source object
          Source myInput = new DOMSource(doc);
 
         //Create a Java Result object
          Result myOutput = new StreamResult(myOutStream);
 
         //Populate the Java ByteArrayOutputStream object
          transForm.transform(myInput,myOutput);
 
         //Get the size of the ByteArrayOutputStream buffer
          int myByteSize = myOutStream.size();
 
         //Allocate myByteSize to the byte array
         mybytes = new byte[myByteSize];
 
         //Copy the content to the byte array
         mybytes = myOutStream.toByteArray();
         com.adobe.idp.Document myDoc = new com.adobe.idp.Document(mybytes);
 
          myDocument = myDoc ;
          }
 
         catch(Exception ee)
         {
             ee.printStackTrace();
         }
 
     return myDocument;
       }
 }
```

>[!NOTE]
>
>Quando si utilizzano sia un oggetto `org.w3c.dom.Document` che un oggetto `com.adobe.idp.Document` nella stessa logica dell&#39;applicazione, è consigliabile qualificare entrambi gli oggetti.
