---
title: Servizio QuickStart (SOAP) per API Java di Signature Service
description: Utilizzare il servizio Firma per aggiungere un campo firma a un documento PDF, recuperare i nomi dei campi firma, modificare un campo firma, firmare digitalmente un documento PDF, firmare digitalmente un modulo basato su XFA, certificare un documento PDF, verificare una firma digitale, verificare più firme digitali e rimuovere una firma digitale.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 34069505-a6cf-4540-932b-604f81823178
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Guida introduttiva all’API Java di Signature Service (SOAP) {#signature-service-java-api-quickstart-soap}

Per il servizio AEM Forms JEE Signature sono disponibili le seguenti funzioni di avvio rapido (SOAP) dell’API Java:

[Guida rapida (modalità SOAP): aggiunta di un campo firma a un documento PDF tramite l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): recupero dei nomi dei campi della firma utilizzando l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Quick Start (modalità SOAP): modifica di un campo firma tramite API Java](signature-service-java-api-quick.md#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api)

[Quick Start (modalità SOAP): firma digitale di un documento PDF tramite l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): firma digitale di un modulo basato su XFA tramite API Java](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)

[Quick Start (modalità SOAP): certificazione di un documento PDF tramite API Java](signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): verifica di una firma digitale tramite l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Quick Start (modalità SOAP): verifica di più firme digitali tramite l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Quick Start (modalità SOAP): rimozione di una firma digitale tramite l’API Java](signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Guida rapida (modalità SOAP): applicare la marca temporale del documento utilizzando l’API Java](#quick-start-soap-mode-apply-document-timestamp-using-the-java-api)

Le operazioni di AEM Forms JEE possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>La Guida introduttiva alla programmazione con AEM Forms si basa sul server Forms distribuito su JBoss Application Server e sul sistema operativo Microsoft Windows. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Consulta [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Guida rapida (modalità SOAP): aggiunta di un campo firma a un documento PDF tramite l’API Java {#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api}

Nell&#39;esempio di codice Java seguente viene aggiunto un campo di firma denominato *SignatureField1* a un documento PDF basato su un file PDF denominato *Loan.pdf*. Il documento PDF contenente il nuovo campo firma viene salvato come file PDF denominato *LoanSig.pdf*. (vedere [Aggiunta di campi firma](/help/forms/developing/digitally-signing-certifying-documents.md#adding-signature-fields).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AddSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
         try
         {
          //Set connection properties required to invoke AEM Forms using SOAP mode
          Properties connectionProps = new Properties();
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
           //Create a ServiceClientFactory instance
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
           //Create a SignatureServiceClient object
           SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
           //Specify a PDF document to which a signature field is added
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
           Document inDoc = new Document (fileInputStream);
 
           //Specify the name of the signature field
           String fieldName = "SignatureField1";
 
           //Create a  PositionRectangle object that specifies
           //the signature fields location
           PositionRectangle post = new  PositionRectangle(193,47,133,12);
 
           //Specify the page number that will contain the signature field
           java.lang.Integer pageNum = new java.lang.Integer(1);
 
           //Add a signature field to the PDF document
           Document sigFieldPDF = signClient.addSignatureField(
              inDoc,
              fieldName,
              pageNum,
              post,
              null,
              null);
 
           //Save the PDF document that contains the signature field
           File outFile = new File("C:\\Adobe\LoanSig.pdf");
           sigFieldPDF.copyToFile(outFile);
             }
 
         catch (Exception ee)
             {
                 ee.printStackTrace();
             }
     }
 }
 
 
```

## Quick Start (modalità SOAP): recupero dei nomi dei campi della firma utilizzando l’API Java {#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono recuperati i nomi dei campi firma in un documento PDF denominato *LoanSig.pdf*. (vedere [Recupero dei nomi dei campi firma](/help/forms/developing/digitally-signing-certifying-documents.md#retrieving-signature-field-names).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class GetSignatureFieldsSOAP {
 
 public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains signature fields
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Retrieve the name of the document’s signature fields
         List fieldNames = signClient.getSignatureFieldList(inDoc);
 
         //Obtain the name of each signature field by iterating through the
         //List object
         Iterator iter = fieldNames.iterator();
         int i = 0 ;
         String fieldName="";
         while (iter.hasNext()) {
             PDFSignatureField signatureField = (PDFSignatureField)iter.next();
             fieldName = signatureField.getName();
             System.out.println("The name of the signature field is " +fieldName);
             i++;
              }
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
```

## Quick Start (modalità SOAP): modifica di un campo firma tramite API Java {#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene modificato un campo di firma denominato SignatureField1 bloccando tutti i campi del modulo quando viene applicata una firma al campo di firma e garantendo che non siano consentite modifiche. Dopo che il servizio di firma restituisce il documento PDF contenente il campo di firma modificato, il documento PDF viene salvato come file PDF denominato LoanSig.pdf. In questo esempio viene sovrascritto il file PDF passato al servizio di firma. (vedere [Modifica dei campi della firma](/help/forms/developing/digitally-signing-certifying-documents.md#modifying-signature-fields).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ModifySignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains a signature field to modify
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Create a PDFSignatureFieldProperties
         PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();
 
          //Create a PDFSeedValueOptionSpec object that stores
          //seed value dictionary information.
          PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();
 
          //Disallow changes to the PDF document. Any change to the document invalidates
          //the signature
          seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);
 
          //Create a FieldMDPOptionSpec object that stores
          //signature field lock dictionary information.
          FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();
 
          //Lock all fields in the PDF document
          fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);
 
          //Set dictionary information
          fieldProperties.setSeedValue(seedOptionsSpec);
          fieldProperties.setFieldMDP(fieldMDPOptionsSpec);
 
          //Modify the signature field
          Document modSignatureField =  signClient.modifySignatureField(inDoc,fieldName,fieldProperties);
 
          //Save the PDF document that contains modified signature field
          File file = new File("C:\\Adobe\LoanSig.pdf");
          modSignatureField.copyToFile(file);
 
     }
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     }
 }
 
```

## Quick Start (modalità SOAP): firma digitale di un documento PDF tramite l’API Java {#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene apposta una firma digitale a un documento di PDF basato su un file di PDF denominato *LoanSig.pdf*. L&#39;alias specificato per le credenziali di protezione è protetto e viene eseguito il controllo della revoca. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato utilizzato per firmare digitalmente il documento PDF. Il documento firmato viene salvato come file PDF denominato *LoanSigned.pdf*. (vedere [Firma digitale dei documenti di PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignDocumentSOAP {
 
 public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to sign
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "New York HQ";
 
       //Specify contact information
       String contactInfo = "Tony Blue";
 
       //Create a PDFSignatureAppearanceOptions object
       //and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
       appear.setShowReason(true);
 
       //Set revocation checking to false
       java.lang.Boolean revCheck = new Boolean(true);
 
       //Create an OCSPOptionSpec object to pass to the sign method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
            //Create a CRLOptionSpec object to pass to the sign method
            CRLOptionSpec crlSpec = new CRLOptionSpec();
 
            //Create a TSPOptionSpec object to pass to the sign method
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
       //Sign the PDF document
       Document signedDoc = signClient.sign(
          credDoc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
              crlSpec,
              tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanSigned.pdf");
       signedDoc.copyToFile (outFile);
       }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 }
 
 
```

## Quick Start (modalità SOAP): firma digitale di un modulo basato su XFA tramite API Java {#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene firmato un modulo interattivo di cui il servizio Forms esegue il rendering. Il `com.adobe.idp.Document` L&#39;istanza restituita dal servizio Forms viene passata al servizio Signature. Il modulo interattivo firmato viene salvato come file PDF denominato *LoanXFASigned.pdf*.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.livecycle.formsservice.client.FormsResult;
 import com.adobe.livecycle.formsservice.client.FormsServiceClient;
 import com.adobe.livecycle.formsservice.client.PDFFormRenderSpec;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignXFAFormsSOAP {
 
 public static void main(String[] args) {
 
     try
     {
 
      //Set connection properties required to invoke AEM Forms using SOAP mode
      Properties connectionProps = new Properties();
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
      //Create a ServiceClientFactory instance
      ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
      //Get the XFA form to sign
      Document myForm = GetForm(myFactory);
 
     //Sign the XFA form
     SignXFA(myForm,myFactory);
     }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 
 
 //Creates an interactive PDF form based on a XFA form
 private static Document GetForm(ServiceClientFactory myFactory)
 {
 
     try
     {
     //Create a FormsServiceClient object
     FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
     //Specify a PDF document to sign
     FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigXFA.pdf");
     Document xfaForm = new Document (fileInputStream);
 
     //Retrieve form data
     FileInputStream cData = new FileInputStream("C:\\Adobe\Loan.xml");
     Document oInputData = new Document(cData);
 
     //Cache the PDF form
     PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
     pdfFormRenderSpec.setGenerateServerAppearance(true);
 
     //Invoke the renderPDFForm2 method
     FormsResult formOut = formsClient.renderPDFForm2(
             xfaForm,               //formQuery
             oInputData,             //inDataDoc
             pdfFormRenderSpec,      //PDFFormRenderSpec
             null,                //urlSpec
             null            //attachments
             );
 
     //Create a Document object that stores form data
     Document myForm = formOut.getOutputContent();
     return myForm;
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     return null;
 
 }
 
 //Sign the PDF document
 private static void SignXFA(Document doc, ServiceClientFactory myFactory)
 {
     try
     {
 
     //Create a SignatureServiceClient object
      SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
      //Specify the name of the signature field
      String fieldName = "SignatureField1";
 
      //Create a Credential object
      Credential myCred = Credential.getInstance("secure");
 
      //Specify the reason to sign the document
      String reason = "The document was reviewed";
 
      //Specify the location of the signer
      String location  = "New York HQ";
 
      //Specify contact information
      String contactInfo = "Tony Blue";
 
      //Create a PDFSignatureAppearanceOptions object
      //and show date information
      PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
      appear.setShowDate(true);
      appear.setShowReason(true);
 
      //Set revocation checking to false
      java.lang.Boolean revCheck = new Boolean(true);
 
      //Create an OCSPOptionSpec object to pass to the sign method
      OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
      //Create a CRLOptionSpec object to pass to the sign method
      CRLOptionSpec crlSpec = new CRLOptionSpec();
 
      //Create a TSPOptionSpec object to pass to the sign method
      TSPOptionSpec tspSpec = new TSPOptionSpec();
 
      //Sign the PDF document
       Document signedDoc = signClient.sign(
          doc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
         crlSpec,
         tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanXFASigned.pdf");
       signedDoc.copyToFile (outFile);
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
      }
 }
 
```

## Quick Start (modalità SOAP): certificazione di un documento PDF tramite API Java {#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene certificato un documento PDF basato su un file PDF denominato *LoanSig.pdf*. L&#39;alias specificato per le credenziali di protezione è protetto e il controllo della revoca non viene eseguito. Il documento certificato viene salvato come file PDF denominato *LoanCertified.pdf*. (vedere [Certificazione dei documenti di PDF](/help/forms/developing/digitally-signing-certifying-documents.md#certifying-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CertifyDocumentSOAP {
 
     public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to certify
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "My company";
 
       //Specify contact information
           String contactInfo = "New York, New York";
 
       //Create a PDFSignatureAppearanceOptions object and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
 
       //Set revocation checking to false
            java.lang.Boolean revCheck = new Boolean(false);
 
            //Set locking to false
            java.lang.Boolean lockField = new Boolean(false);
 
            //Specify a legalAttestation value
            String msg = "Any change to this document will invalidate the certificate";
 
            //Create objects to pass to the certify method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
            CRLOptionSpec crlSpec = new CRLOptionSpec();
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
            //Certify the PDF document
            Document signedDoc = signClient.certify(
               credDoc,
               fieldName,
               myCred,
               HashAlgorithm.SHA1,
               reason,
               location,
               contactInfo,
               MDPPermissions.NoChanges,
               msg,
               appear,
               revCheck,
               lockField,
              ocspSpec,
              crlSpec,
              tspSpec);
 
         //Save the signed PDF document
              File outFile = new File("C:\\Adobe\LoanCertified.pdf");
              signedDoc.copyToFile (outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }
```

## Quick Start (modalità SOAP): verifica di una firma digitale tramite l’API Java {#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene verificata una firma digitale contenuta in un documento PDF firmato basato su un file PDF denominato LoanSigned.pdf. L&#39;ora di verifica è impostata sull&#39;ora corrente e l&#39;opzione di controllo delle revoche è impostata sullo sforzo migliore. (vedere [Verifica delle firme digitali](#verifying-digital-signatures).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifySignatureSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains a digital signature
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify the digital signature
       PDFSignatureVerificationInfo  signInfo = signClient.verify2(
          inDoc,
          fieldName,
          pkiOptions,
          null);
 
       //Get the Signature Status
       SignatureStatus sigStatus = signInfo.getStatus();
       String myStatus="";
 
       //Determine the status of the signature
       if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
              myStatus = "The signatures in the dynamic PDF form are unknown";
          else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
              myStatus = "The signatures in the PDF document are unknown";
          else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
              myStatus = "The signatures in a certified PDF form are valid";
          else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
              myStatus = "The signatures in a signed dynamic PDF form are valid";
          else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
              myStatus = "The signatures in a certified PDF document are valid";
          else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
              myStatus = "The signatures in a signed PDF document are valid";
          else if (sigStatus == SignatureStatus.SignatureFormatError)
              myStatus = "The format of a signature in a signed document is invalid";
          else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
              myStatus = "No changes were made to the signed dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
              myStatus = "No changes were made to the signed PDF document";
          else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
              myStatus = "No changes were made to the certified dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
              myStatus = "No changes were made to the certified PDF document";
          else if (sigStatus == SignatureStatus.DocSigWithChanges)
              myStatus = "There were changes to a signed PDF document";
         else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
              myStatus = "There were changes made to the PDF document.";
 
       //Get the signature type
       SignatureType sigType = signInfo.getSignatureType();
       String myType = "";
 
       if (sigType.getType() == PDFSignatureType.AUTHORSIG)
              myType="Certification";
       else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
              myType="Recipient";
 
       //Get the identity of the signer
       IdentityInformation signerId = signInfo.getSigner();
       String signerMsg = "";
 
      if (signerId.getStatus() == IdentityStatus.UNKNOWN)
          signerMsg = "Identity Unknown";
      else if (signerId.getStatus() == IdentityStatus.TRUSTED)
          signerMsg = "Identity Trusted";
      else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
          signerMsg = "Identity Not Trusted";
 
      //Get the Signature properties returned by the Signature service
      SignatureProperties sigProps = signInfo.getSignatureProps();
      String signerName =  sigProps.getSignerName();
 
     System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
 
 
```

## Quick Start (modalità SOAP): verifica di più firme digitali tramite l’API Java {#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono verificate più firme digitali presenti in un documento PDF firmato basato su un file PDF denominato LoanAllSigs.pdf. L&#39;ora di verifica è impostata sull&#39;ora corrente e l&#39;opzione di controllo delle revoche è impostata sullo sforzo migliore. (vedere [Verifica di più firme digitali](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifyAllSignaturesSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains multiple digital signatures
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanAllSigs.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify all digital signatures that are in a PDF document
       PDFDocumentVerificationInfo  allSig = signClient.verifyPDFDocument(
          inDoc,
          pkiOptions,
          null);
 
       //Get a list of all signatures that are in the PDF document
       List allSignatures = allSig.getVerificationInfos();
 
     //Create an Iterator object and iterate through
     //the List object
     Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();
 
     while (iter.hasNext()) {
            PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();
 
            //Get the Signature Status
               SignatureStatus sigStatus = signInfo.getStatus();
               String myStatus="";
 
             //Determine the status of the signature
               if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                   myStatus = "The signatures in the dynamic PDF form are unknown";
               else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                   myStatus = "The signatures in the PDF document are unknown";
               else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                   myStatus = "The signatures in a certified PDF form are valid";
               else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                   myStatus = "The signatures in a signed dynamic PDF form are valid";
               else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                   myStatus = "The signatures in a certified PDF document are valid";
               else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                   myStatus = "The signatures in a signed PDF document are valid";
               else if (sigStatus == SignatureStatus.SignatureFormatError)
                   myStatus = "The format of a signature in a signed document is invalid";
               else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                   myStatus = "No changes were made to the signed dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                   myStatus = "No changes were made to the signed PDF document";
               else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified PDF document";
               else if (sigStatus == SignatureStatus.DocSigWithChanges)
                   myStatus = "There were changes to a signed PDF document";
              else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                   myStatus = "There were changes made to the PDF document.";
 
               //Get the signature type
              SignatureType sigType = signInfo.getSignatureType();
              String myType = "";
 
              if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                  myType="Certification";
              else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                  myType="Recipient";
 
              //Get the Signature properties returned by the Signature service
              SignatureProperties sigProps = signInfo.getSignatureProps();
              String signerName =  sigProps.getSignerName();
 
             System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
         }
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
```

## Quick Start (modalità SOAP): rimozione di una firma digitale tramite l’API Java {#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api}

Esempio Nell&#39;esempio di codice Java seguente viene rimossa una firma digitale da un campo di firma denominato *SignatureField1*. Il nome del file PDF che contiene il campo firma è *LoanSigned.pdf*. (vedere [Rimozione di firme digitali](/help/forms/developing/digitally-signing-certifying-documents.md#removing-digital-signatures).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ClearSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains the signature to remove
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Clear the signature field
         Document outPDF = signClient.clearSignatureField(inDoc,fieldName);
 
         //Save the PDF document
         File outFile = new File("C:\\Adobe\Loan.pdf");
         outPDF.copyToFile(outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }


 
 
 
```

## Guida rapida (modalità SOAP): applicare la marca temporale del documento utilizzando l’API Java {#quick-start-soap-mode-apply-document-timestamp-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito viene applicata una marca temporale a un documento PDF:

```java
 /*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-signatures-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. commons-httpclient-<version>.jar
 * 6. axis.jar (required for SOAP mode)
 * 7. jaxrpc-api.jar (required for SOAP mode)
 * 8. commons-logging.jar (required for SOAP mode)
 * 9. commons-discovery.jar (required for SOAP mode)
 * 10. wsdl4j.jar (required for SOAP mode)
 * 11. adobe-utilities.jar (required for SOAP mode)
 *
 *
 * These JAR files are in the following path:
 * <install directory>/sdk/client-libs/common
 *
 * The adobe-utilities.jar file is in the following path:
 * <install directory>/sdk/client-libs/jboss
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
import java.io.File;
import java.io.FileInputStream;
import java.util.Properties;

import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.signatures.client.SignatureServiceClient;
import com.adobe.livecycle.signatures.client.types.AddSignatureValidationOptionSpec;
import com.adobe.livecycle.signatures.client.types.TSPOptionSpec;

public class ApplyDocumentTimeStamp {

    public static void main(String args[]){
        {

            try
            {
                //Set connection properties required to invoke AEM Forms using SOAP mode
                Properties connectionProps = new Properties();
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

                //Create a ServiceClientFactory instance
                ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

                //Create a SignatureServiceClient object
                SignatureServiceClient signClient = new SignatureServiceClient(myFactory);

                //Specify a PDF document to sign
                FileInputStream fileInputStream = new FileInputStream("test.pdf");

                //Sign the PDF document
                Document inPDFDoc = new Document (fileInputStream);

                // create AddSignatureValidationOptionSpec Object. later we will set the required OptionSpecs
                AddSignatureValidationOptionSpec addSigValidiationSpec =  new AddSignatureValidationOptionSpec();

                //Create a TSPOptionSpec object to pass to in AddSignatureValidationOptionSpec
                TSPOptionSpec tspSpec = new TSPOptionSpec();
                tspSpec.setTspServerURL("https://tsp-server-url.com");
                tspSpec.setTspServerPassword("provide Timestamp server password");
                tspSpec.setTspServerUsername("provide Timestamp server username");
                addSigValidiationSpec.setTSPOptionSpec(tspSpec);

                Document signedDoc = signClient.applyDocumentTimeStamp(inPDFDoc,addSigValidiationSpec);

                //Save the signed PDF document
                File outFile = new File("testout.pdf");
                signedDoc.copyToFile (outFile);

            }

            catch (Exception ee)
            {
                ee.printStackTrace();
            }
        }
    }
}
```
