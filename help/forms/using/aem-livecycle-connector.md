---
title: Collegamento di AEM Forms con il LiveCycle Adobe
seo-title: Collegamento di AEM Forms con il LiveCycle Adobe
description: AEM connettore di LiveCycle consente di avviare LiveCycle ES4 Document Services dall'interno AEM applicazioni e flussi di lavoro.
seo-description: AEM connettore di LiveCycle consente di avviare LiveCycle ES4 Document Services dall'interno AEM applicazioni e flussi di lavoro.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---

# Collegamento di AEM Forms con il LiveCycle Adobe {#connecting-aem-forms-with-adobe-livecycle}

Il connettore di LiveCycle Adobe Experience Manager (AEM) consente di invocare facilmente i servizi documentali Adobe ES4 da applicazioni e flussi di lavoro AEM Web. LiveCycle fornisce un SDK client avanzato, che consente alle applicazioni client di avviare i servizi di LiveCycle utilizzando le API Java. AEM connettore di LiveCycle semplifica l’utilizzo di queste API all’interno dell’ambiente OSGi.

## Collegamento AEM server al LiveCycle Adobe {#connecting-aem-server-to-adobe-livecycle}

AEM connettore LiveCycle fa parte del [pacchetto aggiuntivo di AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Dopo aver installato il pacchetto aggiuntivo di AEM Forms, esegui i seguenti passaggi per aggiungere i dettagli del server di LiveCycle a AEM console Web.

1. In AEM gestione della configurazione della console Web, individua il componente di configurazione Adobe LiveCycle Client SDK.
1. Fai clic sul componente per modificare l’URL, il nome utente e la password del server di configurazione.
1. Rivedi le impostazioni e fai clic su **Salva**.

Sebbene le proprietà siano auto esplicative, quelle importanti sono le seguenti:

* **URL server**  - Specifica l&#39;URL del server di LiveCycle. Se desideri che LiveCycle e AEM comunichino su https, inizia AEM con la seguente JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   opzione .

* **Nome utente** - Specifica il nome utente dell&#39;account utilizzato per stabilire la comunicazione tra AEM e LiveCycle. L&#39;account è un account utente LiveCycle che dispone delle autorizzazioni necessarie per avviare Document Services.
* **Password** - Specifica la password.
* **Nome servizio**  - Specifica i servizi avviati utilizzando le credenziali utente fornite nei campi Nome utente e Password. Per impostazione predefinita, non vengono passate credenziali all&#39;avvio dei servizi di LiveCycle.

## Avvio di document services {#starting-document-services}

Le applicazioni client possono avviare i servizi di LiveCycle in modo programmatico utilizzando un’API Java, servizi Web, Remoting e REST. Per i client Java, l&#39;applicazione può utilizzare LiveCycle SDK. L’SDK per LiveCycli fornisce un’API Java per avviare questi servizi in remoto. Ad esempio, per convertire un documento di Microsoft Word in PDF, il client avvia GeneratePDFService. Il flusso di chiamata consiste dei seguenti passaggi:

1. Crea un&#39;istanza ServiceClientFactory.
1. Ogni servizio fornisce una classe client. Per avviare un servizio, crea un’istanza client del servizio.
1. Avvia il servizio ed elabora il risultato.

AEM connettore LiveCycle semplifica il flusso esponendo queste istanze client come servizi OSGi a cui è possibile accedere utilizzando i mezzi OSGi standard. Il connettore del LiveCycle offre le seguenti caratteristiche:

* Istanze client come servizio OSGi: I client inclusi nei pacchetti OSGI sono elencati nella sezione [Elenco servizi documenti](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) . Ogni jar client registra l&#39;istanza client come servizio OSGi con il registro del servizio OSGi.
* Propagazione credenziali utente: I dettagli di connessione necessari per la connessione al server di LiveCycle vengono gestiti in una posizione centrale.
* Servizio ServiceClientFactory: Per avviare i processi, l&#39;applicazione client può accedere all&#39;istanza ServiceClientFactory.

### Avvio tramite i riferimenti al servizio dal Registro di sistema del servizio OSGi {#starting-via-service-references-from-osgi-service-registry}

Per avviare un servizio esposto da AEM, esegui i seguenti passaggi:

1. Determina le dipendenze Maven. Aggiungi la dipendenza al jar client richiesto nel file pom.xml maven. Come minimo, aggiungi la dipendenza ai jar adobe-livecycle-client e adobe-usermanager-client.

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

   Per avviare un servizio, aggiungi la corrispondente dipendenza Maven per il servizio. Per l&#39;elenco delle dipendenze, vedere [Elenco servizi documenti](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Ad esempio, per il servizio Genera PDF aggiungi la seguente dipendenza:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Ottieni il riferimento al servizio. Individua un handle per l&#39;istanza di servizio. Se si scrive una classe Java, è possibile utilizzare le annotazioni di Declarative Services.

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

   Lo snippet di codice riportato sopra avvia l&#39;API createPDF di GeneratePdfServiceClient per convertire un documento in PDF. Puoi eseguire chiamate simili in un JSP utilizzando il seguente codice. La differenza principale è che il codice seguente utilizza Sling ScriptHelper per accedere a GeneratePdfServiceClient.

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

La classe ServiceClientFactory è obbligatoria in alcuni casi. Ad esempio, è necessario che ServiceClientFactory chiami i processi.

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

Quasi tutti i servizi documenti del LiveCycle richiedono l’autenticazione. È possibile utilizzare una delle seguenti opzioni per avviare questi servizi senza fornire credenziali esplicite nel codice:

### Configurazione Inserire nell&#39;elenco Consentiti {#allowlist-configuration}

La configurazione LiveCycle Client SDK contiene un&#39;impostazione sui nomi dei servizi. Questa configurazione è un elenco di servizi per i quali la logica di chiamata utilizza le credenziali di amministratore predefinite. Ad esempio, se aggiungi servizi DirectoryManager (parte dell&#39;API User Management) a questo elenco, qualsiasi codice client può utilizzare direttamente il servizio e il livello di chiamata passa automaticamente le credenziali configurate come parte della richiesta inviata al server di LiveCycle

### RunAsManager {#runasmanager}

Come parte dell&#39;integrazione, viene fornito un nuovo servizio RunAsManager. Consente di controllare programmaticamente le credenziali da utilizzare quando si effettua una chiamata al server di LiveCycle.

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

Se si desidera passare credenziali diverse, è possibile utilizzare il metodo overload che accetta un&#39;istanza PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### Proprietà InvocationRequest {#invocationrequest-property}

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

## Elenco servizi documentali {#document-services-list}

### Bundle API SDK client di Adobe LiveCycle {#adobe-livecycle-client-sdk-api-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dipendenze Maven {#maven-dependencies}

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

### Bundle SDK client di Adobe LiveCycle {#adobe-livecycle-client-sdk-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dipendenze Maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Adobe LiveCycle pacchetto client TaskManager {#adobe-livecycle-taskmanager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dipendenze Maven {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client di Adobe LiveCycle Workflow {#adobe-livecycle-workflow-client-bundle}

È disponibile il seguente servizio:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dipendenze Maven {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dipendenze Maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client di Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dipendenze Maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client dell&#39;assembly del LiveCycle di Adobe {#adobe-livecycle-assembler-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dipendenze Maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client di integrazione dei dati del modulo di LiveCycle di Adobe {#adobe-livecycle-form-data-integration-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dipendenze Maven {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client Adobe LiveCycle Forms {#adobe-livecycle-forms-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dipendenze Maven {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client Adobe LiveCycle Output {#adobe-livecycle-output-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.output.client.OutputClient

#### Dipendenze Maven {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client Adobe LiveCycle Reader Extensions {#adobe-livecycle-reader-extensions-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dipendenze Maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dipendenze Maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client di Adobe LiveCycle Signatures {#adobe-livecycle-signatures-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dipendenze Maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client di Adobe LiveCycle Truststore {#adobe-livecycle-truststore-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dipendenze Maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client dell’archivio dei LiveCycli Adobe {#adobe-livecycle-repository-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dipendenze Maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
