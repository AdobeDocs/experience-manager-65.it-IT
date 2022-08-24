---
title: Reader che estende i documenti PDF protetti da policy utilizzando la Libreria di protezione portatile
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Le estensioni di Reader abilitano funzioni interattive nei documenti Adobe PDF tramite Acrobat Reader. È possibile utilizzare la Portable Protection Library (PPL) per estendere i documenti PDF protetti DRM.
seo-description: Reader extensions enable interactive features in Adobe PDF documents through Acrobat Reader. You can use the Portable Protection Library (PPL) to reader extend the DRM protected PDF documents.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Reader che estende i documenti PDF protetti da policy utilizzando la Libreria di protezione portatile {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Per estendere i documenti PDF protetti da policy di protezione dei documenti, è necessario conoscere i concetti di sicurezza dei documenti, estensione del lettore e linguaggio di programmazione Java.

È possibile utilizzare la protezione dei documenti per limitare l’accesso a specifici documenti PDF solo agli utenti autorizzati. È inoltre possibile determinare in che modo un destinatario può utilizzare un documento protetto. Ad esempio, è possibile specificare se i destinatari possono stampare, copiare o modificare il testo di un documento protetto da policy di protezione. Per ulteriori informazioni sulla protezione dei documenti, consulta [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

È possibile utilizzare le estensioni dei lettori per abilitare le funzioni interattive nel documento Adobe PDF tramite Acrobat Reader. Queste funzioni interattive normalmente disponibili solo in Adobe Acrobat Professional e Standard. Per informazioni sulle funzioni interattive che l’estensione del lettore può abilitare, consulta [Servizio Adobe Experience Manager Forms DocAssurance ](/help/forms/using/overview-aem-document-services.md)**.**

È possibile utilizzare la libreria di protezione portatile per applicare criteri sul documento senza la necessità di documenti che viaggiano in rete. Solo le credenziali di sicurezza e i dettagli delle politiche di protezione viaggiano sulla rete. Il documento effettivo non lascia mai il client e i criteri di protezione vengono applicati localmente sul client.

## Reader che estende i documenti PDF protetti da policy di protezione dei documenti {#reader-extending-document-security-policy-protected-pdf-documents}

I documenti protetti da policy sono documenti crittografati. Non è possibile utilizzare API standard per l’estensione dell’assistente vocale per applicare, rimuovere e recuperare i diritti di utilizzo di documenti PDF protetti da policy. Solo il servizio Estensioni di Reader della Libreria di protezione portatile fornisce alle API di applicare, rimuovere e recuperare i diritti di utilizzo di un documento protetto da policy di protezione dei documenti PDF.

### Servizio Estensioni Reader {#reader-extensions-service}

Il servizio di estensione del lettore aggiunge diritti di utilizzo a un documento PDF protetto da policy, attivando funzioni che normalmente non sono disponibili quando un documento PDF viene aperto con Adobe Acrobat Reader. Dispone inoltre di API per rimuovere e recuperare i diritti di utilizzo di un documento protetto da policy.

Il servizio Estensioni di Reader supporta completamente i documenti PDF basati sullo standard PDF 1.6 e versioni successive. Oltre ad Acrobat Reader, gli utenti di terze parti non richiedono alcun software o plug-in aggiuntivo per utilizzare i documenti PDF protetti da policy.

Con il servizio Estensioni di Reader puoi eseguire le seguenti attività:

* Applicare diritti di utilizzo a un documento PDF protetto da policy.
* Rimuovere i diritti di utilizzo di un documento PDF protetto da policy.
* Recupera i diritti di utilizzo applicati a un documento PDF protetto da policy.

### Applicazione dei diritti di utilizzo a un documento PDF protetto da policy di protezione dei documenti {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

È possibile utilizzare `applyUsageRights`API Java per applicare i diritti di utilizzo ai documenti PDF protetti da policy. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento abilitato per i diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

**Sintassi:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF a cui applicare i diritti di utilizzo. È possibile utilizzare documenti protetti da protezione dei documenti di LiveCycle o AEM Forms.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Specificare l'oggetto File che rappresenta un file .jks. Il file .jks è un file keystore. Fa riferimento a un certificato che concede diritti di utilizzo.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Specifica la password del keystore. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Specifica un oggetto di tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L'oggetto usageRights rappresenta diritti individuali che possono essere applicati a un documento PDF protetto da policy.</p> </td>
  </tr>
 </tbody>
</table>

### Recupera i diritti di utilizzo applicati a un documento PDF protetto da policy.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

È possibile utilizzare `getDocumentUsageRights`API Java per recuperare i diritti di utilizzo dell’estensione del lettore applicati a un documento PDF protetto da policy. Recuperando informazioni sui diritti di utilizzo, è possibile ottenere informazioni sull’estensione del lettore di funzioni abilitata per il documento PDF protetto da policy.

**Sintassi:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF da cui recuperare i diritti di utilizzo. È possibile utilizzare documenti protetti da protezione dei documenti di LiveCycle o AEM Forms.</p> </td>
  </tr>
 </tbody>
</table>

#### Esempio di codice {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ");
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Rimuovere i diritti di utilizzo di un documento PDF protetto da policy {#remove-usage-rights-of-a-policy-protected-pdf-document}

È possibile utilizzare `removeUsageRights`API Java per rimuovere i diritti di utilizzo da un documento protetto da policy. La rimozione dei diritti di utilizzo da un documento PDF protetto da policy è necessaria per eseguire altre operazioni AEM Forms sul documento. Ad esempio, è necessario firmare (o certificare) digitalmente un documento PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento protetto da policy, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire le altre operazioni, ad esempio la firma digitale del documento e quindi riapplicare i diritti di utilizzo al documento.

**Sintassi:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Specifica InputStream che rappresenta il documento PDF da cui viene utilizzato l'utilizzo<br /> i diritti devono essere rimossi. È possibile utilizzare documenti protetti da protezione dei documenti di LiveCycle o AEM Forms.</td>
  </tr>
 </tbody>
</table>

#### Esempio di codice {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
