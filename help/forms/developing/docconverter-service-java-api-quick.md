---
title: QuickStart API Java servizio DocConverter (SOAP)
seo-title: QuickStart API Java servizio DocConverter (SOAP)
description: 'null'
seo-description: 'null'
uuid: a02e13a5-4557-4c8a-a4be-e8d017127128
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ea4b26c8-b9cf-42c2-b4da-2884336014a9
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Avvio rapido API Java del servizio DocConverter (SOAP) {#docconverter-service-java-api-quickstart-soap}

Java API Quick Start(SOAP) è disponibile per il servizio DocConverter.

[Avvio rapido (modalità SOAP): Determinazione della conformità PDF/A tramite l&#39;API Java](docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Avvio rapido (modalità SOAP): Conversione di un documento in un documento PDF/A mediante l&#39;API Java](docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

Le operazioni AEM Forms possono essere eseguite utilizzando l&#39;API con tipizzazione forte di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

***Nota **: Gli avvii rapidi disponibili nella programmazione con i moduli AEM si basano sulla distribuzione di Forms Server su JBoss Application Server e sul sistema operativo Microsoft Windows. Tuttavia, se si utilizza un altro sistema operativo, come UNIX, sostituire percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Allo stesso modo, se utilizzate un altro server applicazione J2EE, accertatevi di specificare proprietà di connessione valide. (Vedere[Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)*

## Avvio rapido (modalità SOAP): Conversione di un documento in un documento PDF/A mediante l&#39;API Java {#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api}

Nell&#39;esempio di codice Java riportato di seguito viene convertito un documento PDF denominato *Loan.pdf* in un documento PDF/A salvato come file PDF denominato *LoanArchive.pdf*. (Vedere [Conversione di documenti in documenti](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A.)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-docconverter-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
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
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
 import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec;
 import com.adobe.livecycle.docconverter.client.PDFAConversionResult;
 
 public class CreatePDFADocumentSOAP {
 
     public static void main(String[] args) {
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a DocConverterServiceClient object
         DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);
 
         //Reference a PDF document to convert to a PDF/A document
         FileInputStream myPDF = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inDoc = new Document(myPDF);
 
         //Create a PDFAConversionOptionSpec object and set
         //tracking information
         PDFAConversionOptionSpec spec = new PDFAConversionOptionSpec();
         spec.setLogLevel("FINE");
 
         //Convert the PDF document to a PDF/A document
         PDFAConversionResult result =  docConverter.toPDFA(inDoc,spec);
 
         //Save the PDF/A file
         Document pdfADoc= result.getPDFADocument();
         File pdfAFile = new File("C:\\Adobe\LoanArchive.pdf");
         pdfADoc.copyToFile(pdfAFile);
       }catch (Exception e) {
         e.printStackTrace();
     }
      }
 }
```

## Avvio rapido (modalità SOAP): Determinazione della conformità PDF/A tramite l&#39;API Java {#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api}

Il seguente esempio di codice Java determina se il documento PDF di input è conforme allo standard PDF/A. Il documento PDF di input passato al servizio DocConverter è denominato *LoanArchive.pdf*. I risultati della convalida vengono scritti in un file XML denominato *ValidationResults.xml*. (Vedere Determinazione [programmatica della conformità](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)PDF/A.)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-docconverter-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
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
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
 import com.adobe.livecycle.docconverter.client.PDFAValidationOptionSpec;
 import com.adobe.livecycle.docconverter.client.PDFAValidationResult;
 
 public class IsDocumentPDFASOAP {
 
     public static void main(String[] args) {
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a DocConverterServiceClient object
         DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);
 
         //Reference a PDF document used to determine PDF/A compliancy
         FileInputStream myPDF = new FileInputStream("C:\\Adobe\LoanArchive.pdf");
         Document inDoc = new Document(myPDF);
 
         //Create a PDFAValidationOptionSpec object and set
         //run-time values
         PDFAValidationOptionSpec spec = new PDFAValidationOptionSpec();
         spec.setCompliance(PDFAValidationOptionSpec.Compliance.PDFA_1B);
         spec.setResultLevel(PDFAValidationOptionSpec.ResultLevel.DETAILED);
         spec.setLogLevel("FINE");
         spec.setIgnoreUnusedResource(true);
 
         //Determine if the PDF document is PDF/A compliant
         PDFAValidationResult result =  docConverter.isPDFA(inDoc,spec)    ;
 
         //Get the results of the operation
         Boolean isPDFA = result.getIsPDFA();
 
         //Get XML data that contains validaction results
         Document validationResults =  result.getValidationLog();
         File file= new File("C:\\Adobe\ValidationResults.xml");
         validationResults .copyToFile(file);
 
     }catch (Exception e) {
         e.printStackTrace();
     }
      }
 }
```

