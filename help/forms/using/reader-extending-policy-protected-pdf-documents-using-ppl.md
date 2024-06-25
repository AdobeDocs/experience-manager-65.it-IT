---
title: Reader che estende i documenti di PDF protetti tramite policy utilizzando la Libreria di protezione portatile
description: Le estensioni di Reader abilitano le funzioni interattive nei documenti di Adobe PDF tramite Acrobat Reader. È possibile utilizzare la Portable Protection Library (PPL) per estendere i documenti PDF protetti da DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security,Reader Extensions
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Reader che estende i documenti di PDF protetti tramite policy utilizzando la Libreria di protezione portatile {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Acquisisci familiarità con i concetti di protezione dei documenti, estensione del lettore e linguaggio di programmazione Java per estendere in modalità lettura i documenti PDF protetti tramite policy di protezione dei documenti.

È possibile utilizzare la protezione dei documenti per limitare l’accesso a documenti PDF specifici solo agli utenti autorizzati. È inoltre possibile determinare il modo in cui un destinatario può utilizzare un documento protetto. È ad esempio possibile specificare se i destinatari possono stampare, copiare o modificare il testo di un documento protetto tramite policy di protezione dei documenti. Per ulteriori informazioni sulla protezione dei documenti, consulta [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

Puoi utilizzare le estensioni Reader per abilitare le funzioni interattive nel documento di Adobe PDF tramite Acrobat Reader. Queste funzioni interattive sono normalmente disponibili solo tramite Adobe Acrobat Professional e Standard. Per informazioni sulle funzioni interattive abilitate dall’estensione Reader, consulta [Servizio Adobe Experience Manager Forms DocAssurance ](/help/forms/using/overview-aem-document-services.md)**.**

È possibile utilizzare la libreria di protezione portatile per applicare le policy al documento senza che sia necessario spostarlo in rete. Solo le credenziali di sicurezza e i dettagli dei criteri di protezione possono essere utilizzati in rete. Il documento effettivo non lascia mai il client e le policy di protezione vengono applicate localmente al client.

## Reader che estende i documenti di PDF protetti tramite policy di protezione dei documenti {#reader-extending-document-security-policy-protected-pdf-documents}

I documenti protetti tramite policy sono documenti crittografati. Non è possibile utilizzare le API di estensione lettura standard per applicare, rimuovere e recuperare i diritti di utilizzo di un documento PDF protetto tramite policy. Il servizio Solo estensioni di Reader della Libreria di protezione portatile fornisce API per applicare, rimuovere e recuperare i diritti di utilizzo di un documento PDF protetto tramite policy di protezione dei documenti.

### Servizio Reader Extensions {#reader-extensions-service}

Il servizio di estensione Reader aggiunge diritti di utilizzo a un documento PDF protetto tramite policy, attivando funzionalità che non sono normalmente disponibili quando un documento PDF viene aperto tramite Adobe Acrobat Reader. Dispone inoltre di API per rimuovere e recuperare i diritti di utilizzo di un documento protetto tramite policy.

Il servizio Reader Extensions supporta completamente i documenti PDF basati sullo standard PDF 1.6 e versioni successive. A parte Acrobat Reader, gli utenti di terze parti non richiedono software o plug-in aggiuntivi per utilizzare i documenti PDF protetti tramite policy.

Con il servizio Estensioni di Reader è possibile eseguire le seguenti attività:

* Applica i diritti di utilizzo a un documento PDF protetto tramite policy.
* Rimuovere i diritti di utilizzo di un documento PDF protetto tramite policy.
* Recupera i diritti di utilizzo applicati a un documento PDF protetto tramite policy.

### Applicare i diritti di utilizzo a un documento PDF protetto tramite policy di protezione dei documenti {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

È possibile utilizzare `applyUsageRights`API Java per applicare i diritti di utilizzo ai documenti PDF protetti tramite policy. I diritti di utilizzo riguardano funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. L’utente che apre un documento abilitato ai diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

**Sintassi:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF al quale applicare i diritti di utilizzo. Puoi utilizzare documenti protetti da LiveCycle Rights Management o AEM Forms document security.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Specificare l'oggetto File che rappresenta un file con estensione jks. Il file .jks è un file keystore. Fa riferimento a un certificato che concede diritti di utilizzo.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Specifica la password del keystore. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Specifica un oggetto di tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L'oggetto usageRights rappresenta singoli diritti che possono essere applicati a un documento PDF protetto tramite policy.</p> </td>
  </tr>
 </tbody>
</table>

### Recupera i diritti di utilizzo applicati a un documento PDF protetto tramite policy.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

È possibile utilizzare `getDocumentUsageRights`API Java per recuperare i diritti di utilizzo dell’estensione Reader applicati a un documento PDF protetto tramite policy. Recuperando informazioni sui diritti di utilizzo, scopri le funzioni abilitate dall’estensione Reader per il documento PDF protetto tramite policy.

**Sintassi:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF dal quale recuperare i diritti di utilizzo. Puoi utilizzare documenti protetti da LiveCycle Rights Management o AEM Forms document security.</p> </td>
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

### Rimuovere i diritti di utilizzo di un documento PDF protetto tramite policy {#remove-usage-rights-of-a-policy-protected-pdf-document}

È possibile utilizzare `removeUsageRights`API Java per rimuovere i diritti di utilizzo da un documento protetto tramite policy. La rimozione dei diritti di utilizzo da un documento PDF protetto tramite policy è necessaria per eseguire altre operazioni AEM Forms sul documento. È ad esempio necessario firmare digitalmente (o certificare) un documento di PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento protetto tramite policy, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire le altre operazioni, ad esempio la firma digitale del documento, quindi riapplicare i diritti di utilizzo al documento.

**Sintassi:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Specificare InputStream che rappresenta il documento PDF da cui viene utilizzato<br /> i diritti devono essere rimossi. Puoi utilizzare documenti protetti da LiveCycle Rights Management o AEM Forms document security.</td>
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
