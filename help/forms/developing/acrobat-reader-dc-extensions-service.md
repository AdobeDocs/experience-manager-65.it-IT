---
title: Servizio estensioni Acrobat Reader DCGuida introduttiva API Java (SOAP)
description: Utilizzare il servizio Acrobat Reader DC Extensions per applicare i diritti di utilizzo a un documento PDF, rimuovere i diritti di utilizzo dai documenti PDF e recuperare informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo a un documento PDF abilitato ai diritti denominato LoanUsageRights.pdf.
contentOwner: admin
content-type: reference
topic-tags: develop
role: Developer
exl-id: 82f0b6c1-ca0c-48c7-b7f6-b54704ac0830
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Reader Extensions,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Servizio estensioni Acrobat Reader DCGuida introduttiva API Java (SOAP) {#acrobat-reader-dc-extensions-servicejava-api-quick-start-soap}

Per il servizio Acrobat Reader DC Extensions sono disponibili i seguenti servizi di avvio rapido.

[Quick Start (modalità SOAP):Applicazione dei diritti di utilizzo tramite API Java](#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Rimozione dei diritti di utilizzo dai documenti di PDF](#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): recupero delle informazioni sulle credenziali tramite l’API Java](acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>I Quick Starts in Programming with AEM Forms si basano sul sistema operativo del server Forms. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Quick Start (modalità SOAP):Applicazione dei diritti di utilizzo tramite API Java {#quick-start-soap-mode-applying-usage-rights-using-the-java-api}

Nell&#39;esempio di codice Java seguente vengono applicati diritti di utilizzo a un documento PDF denominato *Loan.pdf*. Il documento PDF con abilitazione dei diritti è stato salvato come file PDF denominato *LoanUsageRights.pdf*. I seguenti diritti di utilizzo sono applicati al documento di PDF: `enabledComments`, `enabledFormFillIn` e `enabledDigitalSignatures`. (Vedi [Applicazione dei diritti di utilizzo ai documenti di PDF](/help/forms/developing/assigning-usage-rights.md).)


```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
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
     * 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class ApplyUsageRightsSOAP{ 
  
     public static void main(String[] args) { 
       try{ 
                   
           //Set connection properties required to invoke AEM Forms using SOAP mode                                 
           Properties connectionProps = new Properties(); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
           //Create a ServiceClientFactory object 
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
          
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve the PDF document to which to apply usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Create a UsageRight object and specify specific usage rights 
           UsageRights useRight = new UsageRights();  
           useRight.setEnabledDynamicFormFields(true); 
           useRight.setEnabledComments(true); 
           useRight.setEnabledFormFillIn(true); 
           useRight.setEnabledDigitalSignatures(true); 
          
           //Create a ReaderExtensionsOptions object 
           ReaderExtensionsOptionSpec reOptions = new ReaderExtensionsOptionSpec();  
                   
           //Set the usage rights  
           reOptions.setUsageRights(useRight);  
           reOptions.setMessage("This is a Rights-Enabled PDF Document"); 
          
           //Apply usage rights to a PDF document 
           Document rightsEnabledPDF = reClient.applyUsageRights( 
              inputPDF, 
              "RE2", 
             null, 
             reOptions);  
          
           //Create a PDF file that represents the rights-enabled PDF document 
           File resultFile = new File("C:\\Adobe\LoanUsageRights.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
  
  
```

## Guida rapida (modalità SOAP): rimozione dei diritti di utilizzo da un documento PDF tramite l’API Java {#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono rimossi i diritti di utilizzo da un documento PDF abilitato per i diritti denominato *LoanUsageRights.pdf*. (Vedi [Rimozione dei diritti di utilizzo dai documenti di PDF](/help/forms/developing/assigning-usage-rights.md).)

```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote Forms Server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms Java library files" in Programming  
     * with AEM Forms 
     */ 
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RemoveUsageRights{ 
  
     public static void main(String[] args) { 
       try{ 
           //Set connection properties required to invoke AEM Forms                                 
           Properties connectionProps = new Properties(); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
           //Create a ServiceClientFactory object 
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
                //Retrieve a rights-enabled PDF document from 
                //which to remove usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Remove usage rights from the PDF document 
           Document rightsEnabledPDF = reClient.removeUsageRights(inputPDF);  
          
           //Save the PDF document as a PDF file 
           File resultFile = new File("C:\\Adobe\noUsageRightsLoan.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
           System.out.println("Usage rights were removed from the document");  
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Quick Start (modalità SOAP): recupero delle informazioni sulle credenziali tramite l’API Java {#quick-start-soap-mode-retrieving-credential-information-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono recuperate informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo a un documento di PDF abilitato ai diritti denominato *LoanUsageRights.pdf*. (Vedi [Recupero delle informazioni sulle credenziali](/help/forms/developing/assigning-usage-rights.md).)

```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote Forms Server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms Java library files" in Programming  
     * with AEM Forms 
     */ 
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RetrieveCredentialInformation { 
  
     public static void main(String[] args) { 
       try{ 
                   
           //Set connection properties required to invoke AEM Forms                             
           Properties connectionProps = new Properties(); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
           //Create a ServiceClientFactory object 
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve a rights-enabled PDF document 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Retrieve credential information 
           GetUsageRightsResult usageRightsResult = reClient.getDocumentUsageRights(inputPDF);  
          
           //Get the date after which the credential is no longer valid 
           Date endDate = usageRightsResult.getNotAfter(); 
          
           //Get the message displayed in Adobe Reader when the rights-enabled 
           //document is opened 
           String message = usageRightsResult.getMessage(); 
          
           //Get usage rights to see if the enableFormFillIn is enabled 
           UsageRights myRights = usageRightsResult.getRights(); 
           boolean ans = myRights.isEnabledFormFillIn(); 
          
           if (ans==true) 
              System.out.println("The enableFormFillIn usage right is enabled"); 
           else 
             System.out.println("The enableFormFillIn usage right is not enabled"); 
                                                   
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
                  
     } 
 } 
 
```
