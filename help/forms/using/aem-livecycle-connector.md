---
title: Collegamento di AEM Forms con Adobe LiveCycle
seo-title: Collegamento di AEM Forms con Adobe LiveCycle
description: Il connettore AEM LiveCycle consente di avviare LiveCycle ES4 Document Services dall'interno delle app e dei flussi di lavoro AEM.
seo-description: Il connettore AEM LiveCycle consente di avviare LiveCycle ES4 Document Services dall'interno delle app e dei flussi di lavoro AEM.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---


# Collegamento di AEM Forms con Adobe LiveCycle {#connecting-aem-forms-with-adobe-livecycle}

 connettore LiveCycle (AEM) di Adobe Experience Manager consente di invocare senza soluzione di continuità Adobe LiveCycle ES4 Document Services dalle app Web e dai flussi di lavoro AEM. LiveCycle fornisce un SDK client avanzato che consente alle applicazioni client di avviare i servizi LiveCycle utilizzando le API Java. AEM LiveCycle Connector semplifica l&#39;utilizzo di queste API nell&#39;ambiente OSGi.

## Connessione del server AEM ad Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector fa parte del pacchetto [del componente aggiuntivo](/help/forms/using/installing-configuring-aem-forms-osgi.md)AEM Forms. Dopo aver installato il pacchetto del componente aggiuntivo AEM Forms, eseguite i seguenti passaggi per aggiungere i dettagli del server LiveCycle alla console Web di AEM.

1. In Gestione configurazione console Web AEM, individua il componente di configurazione Adobe LiveCycle Client SDK.
1. Fate clic sul componente per modificare l’URL, il nome utente e la password del server di configurazione.
1. Esaminate le impostazioni e fate clic su **Salva**.

Anche se le proprietà sono auto-esplicative, quelle importanti sono le seguenti:

* **URL** server - Specifica l&#39;URL del server LiveCycle. Se desiderate che LiveCycle e AEM comunichino mediante https, avviate AEM con la seguente JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   opzione.

* **Nome** utente - Specifica il nome utente dell&#39;account utilizzato per stabilire la comunicazione tra AEM e LiveCycle. L&#39;account è un account utente di LiveCycle che dispone delle autorizzazioni necessarie per avviare Document Services.
* **Password**- Specifica la password.
* **Nome** servizio - Specifica i servizi avviati utilizzando le credenziali utente fornite nei campi Nome utente e Password. Per impostazione predefinita, non vengono passate credenziali all&#39;avvio dei servizi LiveCycle.

## Avvio di Document Services {#starting-document-services}

Le applicazioni client possono avviare i servizi LiveCycle a livello di programmazione utilizzando un&#39;API Java, servizi Web, eventi remoti e REST. Per i client Java, l&#39;applicazione può utilizzare LiveCycle SDK. L&#39;SDK di LiveCycle fornisce un&#39;API Java per avviare questi servizi in remoto. Ad esempio, per convertire un documento di Microsoft Word in PDF, il client avvia GeneratePDFService. Il flusso di chiamata è costituito dai seguenti passaggi:

1. Creare un&#39;istanza ServiceClientFactory.
1. Ogni servizio fornisce una classe client. Per avviare un servizio, create un&#39;istanza client del servizio.
1. Avviare il servizio ed elaborare il risultato.

AEM LiveCycle Connector semplifica il flusso esponendo queste istanze client come servizi OSGi a cui è possibile accedere utilizzando i mezzi OSGi standard. Il connettore LiveCycle offre le seguenti funzionalità:

* Istanze client come servizio OSGi: I client inclusi in pacchetti OSGI sono elencati nella sezione Elenco [di](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) Document Services. Ogni Jar client registra l’istanza client come servizio OSGi con il Registro di servizio OSGi.
* Propagazione credenziali utente: I dettagli di connessione necessari per connettersi al server LiveCycle sono gestiti in una posizione centrale.
* ServiceClientFactory: Per avviare i processi, l&#39;applicazione client può accedere all&#39;istanza ServiceClientFactory.

### Avvio tramite i riferimenti di servizio dal Registro di sistema OSGi {#starting-via-service-references-from-osgi-service-registry}

Per avviare un servizio esposto dall’interno di AEM, effettuate le seguenti operazioni:

1. Determinare le dipendenze del cielo. Aggiungi la dipendenza al Jar client richiesto nel file pom.xml maven. Come minimo, aggiungete una dipendenza agli jar adobe-livecycle-client e adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Per avviare un servizio, aggiungete la corrispondente dipendenza Maven per il servizio. Per l&#39;elenco delle dipendenze, vedere Elenco [servizi](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)documenti. Ad esempio, per il servizio Genera PDF aggiungere la seguente dipendenza:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Ottenete il riferimento del servizio. Ottenere un handle per l&#39;istanza del servizio. Se si scrive una classe Java, è possibile utilizzare le annotazioni dei servizi dichiarativi.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   Lo snippet di codice riportato sopra avvia l&#39;API createPDF di GeneratePdfServiceClient per convertire un documento in PDF. È possibile eseguire chiamate simili in una JSP utilizzando il seguente codice. La differenza principale sta nel seguente codice che utilizza Sling ScriptHelper per accedere a GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Avvio tramite ServiceClientFactory {#starting-via-serviceclientfactory}

In alcuni casi, la classe ServiceClientFactory è obbligatoria. Ad esempio, per chiamare i processi è necessario ServiceClientFactory.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Supporto RunAs {#runas-support}

In LiveCycle, quasi tutti i Document Service richiedono l&#39;autenticazione. Potete utilizzare una delle seguenti opzioni per avviare questi servizi senza fornire credenziali esplicite nel codice:

### Configurazione  Inserì nell&#39;elenco Consentiti {#allowlist-configuration}

La configurazione dell&#39;SDK del client LiveCycle contiene un&#39;impostazione relativa ai nomi dei servizi. Questa configurazione è un elenco di servizi per i quali la logica di chiamata utilizza le credenziali dell&#39;amministratore. Ad esempio, se si aggiungono servizi DirectoryManager (parte dell&#39;API di gestione utente) a questo elenco, qualsiasi codice client può utilizzare direttamente il servizio e il livello di chiamata trasmette automaticamente le credenziali configurate come parte della richiesta inviata al server LiveCycle

### RunAsManager {#runasmanager}

Come parte dell&#39;integrazione, viene fornito un nuovo servizio RunAsManager. Consente di controllare a livello di programmazione le credenziali da utilizzare per effettuare una chiamata al server LiveCycle.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Se si desidera trasmettere credenziali diverse, è possibile utilizzare il metodo overload che accetta un&#39;istanza PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest, proprietà {#invocationrequest-property}

Se si chiama un processo o si utilizza direttamente la classe ServiceClientFactory e si crea una richiesta di chiamata, è possibile specificare una proprietà per indicare che il livello di chiamata deve utilizzare le credenziali configurate.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Elenco di Document Services {#document-services-list}

### Bundle API Adobe LiveCycle Client SDK {#adobe-livecycle-client-sdk-api-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dipendenze Paradiso {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Client SDK Bundle {#adobe-livecycle-client-sdk-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dipendenze Paradiso {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Pacchetto Adobe LiveCycle TaskManager Client {#adobe-livecycle-taskmanager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dipendenze Paradiso {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Workflow Client Bundle {#adobe-livecycle-workflow-client-bundle}

È disponibile il seguente servizio:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dipendenze Paradiso {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dipendenze Paradiso {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dipendenze Paradiso {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Assembler {#adobe-livecycle-assembler-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dipendenze Paradiso {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto Adobe LiveCycle Form Data Integration Client {#adobe-livecycle-form-data-integration-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dipendenze Paradiso {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto Adobe LiveCycle Forms Client {#adobe-livecycle-forms-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dipendenze Paradiso {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto Adobe LiveCycle Output Client {#adobe-livecycle-output-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.output.client.OutputClient

#### Dipendenze Paradiso {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Reader Extensions {#adobe-livecycle-reader-extensions-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dipendenze Paradiso {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto Adobe LiveCycle Rights Manager Client {#adobe-livecycle-rights-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dipendenze Paradiso {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto Adobe LiveCycle Signatures Client {#adobe-livecycle-signatures-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dipendenze Paradiso {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Truststore {#adobe-livecycle-truststore-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dipendenze Paradiso {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client di repository di Adobe LiveCycle {#adobe-livecycle-repository-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dipendenze Paradiso {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
