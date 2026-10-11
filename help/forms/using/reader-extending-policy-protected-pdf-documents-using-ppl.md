---
title: Reader estende i documenti PDF protetti da criterio utilizzando la libreria di protezione portatile
description: Le estensioni Reader abilitano le funzioni interattive nei documenti di Adobe PDF tramite Acrobat Reader. È possibile utilizzare la Portable Protection Library (PPL) per estendere i documenti PDF protetti da DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security,Reader Extensions
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 3%
---
# Reader estende i documenti PDF protetti da criterio utilizzando la libreria di protezione portatile {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Conoscere i concetti di protezione dei documenti, estensione del lettore e linguaggio di programmazione Java per estendere in lettura i documenti PDF protetti tramite policy di protezione dei documenti.

È possibile utilizzare la protezione dei documenti per limitare l’accesso a documenti PDF specifici solo agli utenti autorizzati. È inoltre possibile determinare il modo in cui un destinatario può utilizzare un documento protetto. È ad esempio possibile specificare se i destinatari possono stampare, copiare o modificare il testo di un documento protetto tramite policy di protezione dei documenti. Per ulteriori informazioni sulla protezione dei documenti, consulta [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

Puoi utilizzare le estensioni Reader per abilitare le funzioni interattive nel documento di Adobe PDF tramite Acrobat Reader. Queste funzioni interattive sono normalmente disponibili solo tramite Adobe Acrobat Professional e Standard. Per informazioni sulle funzionalità interattive abilitate dall&#39;estensione Reader, vedere [Servizio Adobe Experience Manager Forms DocAssurance &#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

È possibile utilizzare la libreria di protezione portatile per applicare le policy al documento senza che sia necessario spostarlo in rete. Solo le credenziali di sicurezza e i dettagli dei criteri di protezione possono essere utilizzati in rete. Il documento effettivo non lascia mai il client e le policy di protezione vengono applicate localmente al client.

## estensione di Reader ai documenti PDF protetti tramite policy {#reader-extending-document-security-policy-protected-pdf-documents}

I documenti protetti tramite policy sono documenti crittografati. Non è possibile utilizzare le API di estensione lettura standard per applicare, rimuovere e recuperare i diritti di utilizzo di un documento PDF protetto tramite policy. Solo il servizio Reader Extensions della Libreria di protezione portatile fornisce API per l&#39;applicazione, la rimozione e il recupero dei diritti di utilizzo di documenti PDF protetti tramite policy di protezione dei documenti.

### Servizio Reader Extensions {#reader-extensions-service}

Il servizio di estensione Reader aggiunge diritti di utilizzo a un documento PDF protetto tramite policy, attivando funzionalità che non sono normalmente disponibili quando un documento PDF viene aperto tramite Adobe Acrobat Reader. Dispone inoltre di API per rimuovere e recuperare i diritti di utilizzo di un documento protetto tramite policy.

Il servizio Reader Extensions supporta completamente i documenti PDF basati su PDF Standard 1.6 e versioni successive. A parte Acrobat Reader, gli utenti di terze parti non richiedono software o plug-in aggiuntivi per utilizzare i documenti PDF protetti tramite policy.

Con il servizio Reader Extensions è possibile eseguire le seguenti attività:

* Applica i diritti di utilizzo a un documento PDF protetto tramite policy.
* Rimuovere i diritti di utilizzo di un documento PDF protetto tramite policy.
* Recuperare i diritti di utilizzo applicati a un documento PDF protetto tramite policy.

### Applicazione dei diritti di utilizzo a un documento PDF protetto tramite policy di protezione dei documenti {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

È possibile utilizzare l&#39;API Java `applyUsageRights` per applicare i diritti di utilizzo ai documenti PDF protetti tramite policy. I diritti di utilizzo riguardano funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. L’utente che apre un documento abilitato ai diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

**Sintassi:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF a cui applicare i diritti di utilizzo. Puoi utilizzare documenti LiveCycle Rights Management o AEM Forms protetti da Document Security.</p> </td>
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
   <td><p>Specifica un oggetto di tipo <a href="https://help.adobe.com/it_IT/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L'oggetto usageRights rappresenta singoli diritti che possono essere applicati a un documento PDF protetto tramite policy.</p> </td>
  </tr>
 </tbody>
</table>

### Recuperare i diritti di utilizzo applicati a un documento PDF protetto tramite policy.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

È possibile utilizzare l&#39;API Java `getDocumentUsageRights`per recuperare i diritti di utilizzo dell&#39;estensione Reader applicati a un documento PDF protetto tramite policy. Recuperando informazioni sui diritti di utilizzo, scopri le funzioni abilitate dall’estensione Reader per il documento PDF protetto tramite policy.

**Sintassi:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Specificare InputStream che rappresenta il documento PDF da cui recuperare i diritti di utilizzo. Puoi utilizzare documenti LiveCycle Rights Management o AEM Forms protetti da Document Security.</p> </td>
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

È possibile utilizzare l&#39;API Java `removeUsageRights` per rimuovere i diritti di utilizzo da un documento protetto tramite policy. La rimozione dei diritti di utilizzo da un documento PDF protetto tramite policy è necessaria per eseguire altre operazioni AEM Forms sul documento. Ad esempio, è necessario firmare digitalmente (o certificare) un documento di PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento protetto tramite policy, è necessario rimuovere i diritti di utilizzo dal documento di PDF, eseguire le altre operazioni, ad esempio la firma digitale del documento, quindi riapplicare i diritti di utilizzo al documento.

**Sintassi:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Specificare InputStream che rappresenta il documento di PDF da cui rimuovere i diritti di utilizzo<br />. Puoi utilizzare documenti LiveCycle Rights Management o AEM Forms protetti da Document Security.</td>
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
