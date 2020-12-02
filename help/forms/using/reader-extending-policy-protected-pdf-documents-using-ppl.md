---
title: Reader estensione di documenti PDF protetti tramite criterio tramite la libreria Protezione portatile
seo-title: Reader estensione di documenti PDF protetti tramite criterio tramite la libreria Protezione portatile
description: Le estensioni di Reader consentono funzioni interattive  documenti Adobe PDF tramite  Acrobat Reader. È possibile utilizzare la Portable Protection Library (PPL) per l'estensione dei documenti PDF protetti da DRM.
seo-description: Le estensioni di Reader consentono funzioni interattive  documenti Adobe PDF tramite  Acrobat Reader. È possibile utilizzare la Portable Protection Library (PPL) per l'estensione dei documenti PDF protetti da DRM.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# Reader che estende i documenti PDF protetti tramite criterio utilizzando la libreria Protezione portatile {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Per estendere i documenti PDF protetti tramite criterio, è necessario avere familiarità con i concetti di protezione dei documenti, estensione dei lettori e linguaggio di programmazione Java.

È possibile utilizzare la protezione dei documenti per limitare l&#39;accesso a documenti PDF specifici solo agli utenti autorizzati. È inoltre possibile determinare in che modo un destinatario può utilizzare un documento protetto. Ad esempio, è possibile specificare se i destinatari possono stampare, copiare o modificare il testo di un documento protetto tramite criterio. Per ulteriori informazioni sulla protezione dei documenti, vedere [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

È possibile utilizzare le estensioni dei lettori per abilitare le funzioni interattive in  documento Adobe PDF tramite  Acrobat Reader. Queste funzioni interattive normalmente disponibili solo tramite  Adobe Acrobat Professional e Standard. Per informazioni sulle funzioni interattive che possono essere abilitate dall&#39;estensione del lettore, vedere [ servizio Adobe Experience Manager Forms DocAssurance ](/help/forms/using/overview-aem-document-services.md)**.**

È possibile utilizzare la libreria di protezione portatile per applicare criteri al documento senza che sia necessario che il documento viaggia in rete. Solo le credenziali di sicurezza e i dettagli relativi alle politiche di protezione viaggiano sulla rete. Il documento effettivo non lascia mai il client e i criteri di protezione vengono applicati localmente sul client.

## Reader estensione dei documenti PDF protetti tramite criterio di protezione documento {#reader-extending-document-security-policy-protected-pdf-documents}

I documenti protetti tramite criterio sono documenti crittografati. Non è possibile utilizzare le API standard per l&#39;estensione dei lettori per applicare, rimuovere e recuperare i diritti di utilizzo di documenti PDF protetti tramite criterio. Solo il servizio Estensioni di Reader della libreria Protezione portatile consente alle API di applicare, rimuovere e recuperare i diritti di utilizzo di documenti PDF protetti tramite criterio.

### Servizio Estensioni Reader {#reader-extensions-service}

Il servizio di estensione del lettore aggiunge diritti di utilizzo a un documento PDF protetto tramite criterio, attivando funzioni normalmente non disponibili quando un documento PDF viene aperto tramite  Reader Adobe Acrobat. Dispone inoltre di API per rimuovere e recuperare i diritti di utilizzo di un documento protetto tramite criterio.

Il servizio Estensioni Reader supporta completamente i documenti PDF basati sullo standard PDF 1.6 e versioni successive. A parte  Acrobat Reader, gli utenti di terze parti non richiedono software o plug-in aggiuntivi per utilizzare i documenti PDF protetti tramite criterio.

Con il servizio Estensioni di Reader potete eseguire le seguenti attività:

* Applicare diritti di utilizzo a un documento PDF protetto tramite criterio.
* Rimuovere i diritti di utilizzo di un documento PDF protetto tramite criterio.
* Ottenete i diritti di utilizzo applicati a un documento PDF protetto tramite criterio.

### Applicazione dei diritti di utilizzo a un documento PDF protetto tramite criterio {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

È possibile utilizzare l&#39;API `applyUsageRights`Java per applicare i diritti di utilizzo ai documenti PDF protetti tramite criterio. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in  Acrobat ma non in  Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono stati applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento con diritti in  Adobe Reader può eseguire operazioni abilitate per tale documento specifico.

**Sintassi:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF a cui applicare i diritti di utilizzo. È possibile utilizzare Rights Management di LiveCycle o  documenti AEM Forms protetti per la protezione dei documenti.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Specificate l'oggetto File che rappresenta un file .jks. Il file .jks è un file keystore. Indica un certificato che concede diritti di utilizzo.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Specificate la password dell'archivio di chiavi. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Specifica un oggetto di tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L'oggetto usageRights rappresenta diritti individuali che possono essere applicati a un documento PDF protetto tramite criterio.</p> </td>
  </tr>
 </tbody>
</table>

### Ottenete i diritti di utilizzo applicati a un documento PDF protetto tramite criterio.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

È possibile utilizzare l&#39;API `getDocumentUsageRights`Java per recuperare i diritti di utilizzo dell&#39;estensione del lettore applicati a un documento PDF protetto tramite criterio. Ottenendo informazioni sui diritti di utilizzo, è possibile ottenere informazioni sulle funzioni che l&#39;estensione del lettore di funzioni ha attivato per il documento PDF protetto tramite criterio.

**Sintassi:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF da cui recuperare i diritti di utilizzo. È possibile utilizzare Rights Management di LiveCycle o  documenti AEM Forms protetti per la protezione dei documenti.</p> </td>
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

System.out.println("UsageRights applied successfully to the document. ”);
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

### Rimozione dei diritti di utilizzo di un documento PDF protetto tramite criterio {#remove-usage-rights-of-a-policy-protected-pdf-document}

Potete utilizzare l&#39;API `removeUsageRights`Java per rimuovere i diritti di utilizzo da un documento protetto tramite criterio. La rimozione dei diritti di utilizzo da un documento PDF protetto tramite criterio è necessaria per eseguire altre operazioni AEM Forms  documento. Ad esempio, è necessario firmare (o certificare) digitalmente un documento PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento protetto tramite criterio, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire altre operazioni, ad esempio la firma digitale del documento e quindi riapplicare i diritti di utilizzo al documento.

**Sintassi:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Specificare InputStream che rappresenta il documento PDF da cui rimuovere i diritti di utilizzo<br />. È possibile utilizzare Rights Management di LiveCycle o  documenti AEM Forms protetti per la protezione dei documenti.</td>
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
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

