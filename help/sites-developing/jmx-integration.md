---
title: Integrazione dei servizi con la console JMX
seo-title: Integrazione dei servizi con la console JMX
description: Esporre gli attributi e le operazioni del servizio per consentire l'esecuzione delle attività di amministrazione tramite la creazione e la distribuzione di MBeans per gestire i servizi tramite la console JMX
seo-description: Esporre gli attributi e le operazioni del servizio per consentire l'esecuzione delle attività di amministrazione tramite la creazione e la distribuzione di MBeans per gestire i servizi tramite la console JMX
uuid: 4a489a24-af10-4505-8333-aafc0c81dd3e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 83c590e0-2e6c-4499-a6ea-216e4c7bc43c
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---


# Integrazione dei servizi con la console JMX{#integrating-services-with-the-jmx-console}

Crea e distribuisci MBeans per gestire i servizi tramite la console JMX. Esporre gli attributi e le operazioni del servizio per consentire l&#39;esecuzione delle attività di amministrazione.

Per informazioni sull&#39;utilizzo della console JMX, consultate [Monitoring Server Resources Using the JMX Console](/help/sites-administering/jmx-console.md).

## Framework JMX in Felix e CQ5 {#the-jmx-framework-in-felix-and-cq}

Sulla piattaforma Apache Felix, distribuisci MBeans come servizi OSGi. Quando un servizio MBean viene registrato nel Registro di sistema OSGi Service, il modulo lavagna Aries JMX registra automaticamente il file MBean con il server MBean. MBean è quindi disponibile per la console JMX che espone gli attributi e le operazioni pubblici.

![jmxwhiteboard](assets/jmxwhiteboard.png)

## Creazione di MBeans per CQ5 e CRX {#creating-mbeans-for-cq-and-crx}

Gli MBeans creati per gestire le risorse CQ5 o CRX si basano sull’interfaccia javax.management.DynamicMBean. Per crearli, seguite i consueti pattern di progettazione definiti nella specifica JMX:

* Create l&#39;interfaccia di gestione, compresi get, set ed è un metodo per definire gli attributi e altri metodi per definire le operazioni.
* Creare la classe di implementazione. La classe deve implementare DynamicMBean oppure estendere una classe di implementazione di DynamicMBean.
* Seguite la convenzione di denominazione standard in modo che il nome della classe di implementazione sia il nome dell&#39;interfaccia con il suffisso MBean.

Oltre a definire l&#39;interfaccia di gestione, l&#39;interfaccia definisce anche l&#39;interfaccia del servizio OSGi. La classe di implementazione implementa il servizio OSGi.

### Utilizzo delle annotazioni per fornire informazioni MBean {#using-annotations-to-provide-mbean-information}

Il pacchetto [com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) fornisce diverse annotazioni e classi per fornire facilmente metadati MBean alla console JMX. Utilizzare queste annotazioni e classi invece di aggiungere informazioni direttamente all&#39;oggetto MBeanInfo di MBeanInfo.

**Annotazioni**

Aggiungete annotazioni all&#39;interfaccia di gestione per specificare i metadati MBean. Le informazioni vengono visualizzate nella console JMX per ciascuna classe di implementazione distribuita. Sono disponibili le seguenti annotazioni (per informazioni complete, vedere [com.adobe.granite.jmx.annotation JavaDocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html)):

* **Descrizione:** Fornisce una descrizione della classe o del metodo MBean. Quando viene utilizzata nella dichiarazione della classe, la descrizione viene visualizzata nella pagina Console JMX per l&#39;MBean. Quando viene utilizzata su un metodo, la descrizione viene visualizzata come testo al passaggio del mouse per l&#39;attributo o l&#39;operazione corrispondente.
* **Impatto:** l&#39;impatto di un metodo. I valori di parametro validi sono i campi definiti da [javax.management.MBeanOperationInfo](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html).

* **Nome:** Specifica il nome da visualizzare per un parametro dell&#39;operazione. Utilizzate questa annotazione per ignorare il nome effettivo del parametro del metodo utilizzato nell&#39;interfaccia.
* **OpenTypeInfo:** specifica la classe da utilizzare per rappresentare dati compositi o tabulari nella console JMX. Da usare con Open MBeans
* **TabularTypeInfo:** utilizzata per annotare la classe utilizzata per rappresentare i dati tabulari.

**Classi**

Sono disponibili classi per la creazione di MBeans dinamici che utilizzano le annotazioni aggiunte alle rispettive interfacce:

* **AnnotatedStandardMBean:** una sottoclasse della classe javax.management.StandardMBean che fornisce automaticamente alla console JMX i metadati dell&#39;annotazione.
* **OpenAnnotatedStandardMBean:** una sottoclasse della classe AnnotatedStandardMBean per la creazione di fave aperte che utilizzano l&#39;annotazione OpenTypeInfo.

### Sviluppo di MBeans {#developing-mbeans}

In genere, il file MBean riflette il servizio OSGi che si desidera gestire. Sulla piattaforma Felix, potete creare il file MBean come fareste per la distribuzione su altre piattaforme server Java. Una differenza principale consiste nel fatto che è possibile utilizzare le annotazioni per specificare le informazioni MBean:

* Interfaccia di gestione: Definisce gli attributi utilizzando i metodi getter, setter e is. Definisce le operazioni utilizzando qualsiasi altro metodo pubblico. Utilizza le annotazioni per fornire i metadati per l&#39;oggetto BeanInfo.
* Classe MBean: Implementa l&#39;interfaccia di gestione. Estende la classe AnnotatedStandardMBean in modo che elabori le annotazioni nell&#39;interfaccia.

Nell&#39;esempio seguente, MBean fornisce informazioni sull&#39;archivio CRX. L&#39;interfaccia utilizza l&#39;annotazione Descrizione per fornire informazioni alla console JMX.

#### Interfaccia di gestione {#management-interface}

```java
package com.adobe.example.myapp;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes repository properties.")
public interface ExampleMBean {

    @Description("The name of the repository.")
    String getRepositoryName();

    @Description("The vendor of the repository.")
    String   getRepositoryVendor();

    @Description("The URL of repository vendor.")
    String getVendorUrl();
}
```

La classe di implementazione utilizza il servizio SlingRepository per recuperare informazioni sull&#39;archivio CRX.

#### Classe di implementazione MBean {#mbean-implementation-class}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

L’immagine seguente mostra la pagina per questo MBean nella console JMX.

![jmxdescription](assets/jmxdescription.png)

### Registrazione MBeans {#registering-mbeans}

Quando si registra MBeans come servizio OSGi, questi vengono registrati automaticamente con il server MBean. Per installare un MBean su CQ5, includetelo in un bundle ed esportate il servizio MBean come qualsiasi altro servizio OSGi.

Oltre ai metadati relativi a OSGi, è necessario fornire anche i metadati richiesti dal modulo lavagna Aries JMX per registrare MBean con il server MBean:

* **Il nome dell&#39;interfaccia DynamicMBean:** Dichiarare che il servizio MBean implementa l&#39;interfaccia  `javax.management.DynamicMBea`n. Questa dichiarazione notifica al modulo della lavagna Aries JMX che il servizio è un servizio MBean.

* **Il dominio e le proprietà chiave MBean:** Su Felix, queste informazioni vengono fornite come proprietà del servizio OSGi di MBean. Si tratta delle stesse informazioni normalmente fornite al server MBean in un oggetto `javax.management.ObjectName`.

Se il file MBean riflette un servizio singolo, è necessaria solo un&#39;istanza singola del servizio MBean. In questo caso, se si utilizza il plugin Maven Felix SCR, è possibile utilizzare le annotazioni Apache Felix Service Component Runtime (SCR) nella classe di implementazione MBean per specificare i metatdata relativi a JMX. Per creare un&#39;istanza di più istanze MBean, è possibile creare un&#39;altra classe che esegua la registrazione del servizio OSGi di MBean. In questo caso, i metadati relativi a JMX vengono generati in fase di esecuzione.

**MBean singolo**

MBeans per i quali è possibile definire tutti gli attributi e le operazioni in fase di progettazione possono essere distribuiti utilizzando le annotazioni SCR nella classe di implementazione MBean. Nell&#39;esempio seguente, l&#39;attributo `value` dell&#39;annotazione `Service` dichiara che il servizio implementa l&#39;interfaccia `DynamicMBean`. L&#39;attributo `name` dell&#39;annotazione `Property` specifica il dominio JMX e le proprietà chiave.

#### Classe di implementazione MBean con annotazioni SCR {#mbean-implementation-class-with-scr-annotations}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

@Component(immediate = true)
@Property(name = "jmx.objectname", value="com.adobe.example:type=CRX")
@Service(value = DynamicMBean.class)
public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

**Più istanze di servizio MBean**

Per gestire più istanze di un servizio gestito, potete creare più istanze del servizio MBean corrispondente. Inoltre, le istanze del servizio MBean devono essere create o rimosse quando le istanze gestite vengono avviate o arrestate. È possibile creare una classe Manager MBean per creare un&#39;istanza dei servizi MBean in fase di esecuzione e gestire il ciclo di vita del servizio.

Utilizzate BundleContext per registrare l&#39;MBean come servizio OSGi. Includere le informazioni relative a JMX nell&#39;oggetto Dictionary utilizzato come argomento del metodo BundleContext.registerService.

Nell&#39;esempio di codice seguente, il servizio EsempioMBean viene registrato a livello di programmazione. L&#39;oggetto componentContext è ComponentContext, che fornisce l&#39;accesso a BundleContext.

#### Frammento di codice: Registrazione programmatica del servizio MBean {#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

L&#39;esempio MBean nella sezione successiva fornisce ulteriori dettagli.

Un gestore di servizi MBean è utile quando le configurazioni di servizio sono memorizzate nella directory archivio. Il manager può recuperare le informazioni sul servizio e utilizzarle per configurare e creare l&#39;MBean corrispondente. La classe manager può inoltre ascoltare gli eventi di modifica del repository e aggiornare di conseguenza i servizi MBean.

## Esempio: Monitoraggio dei modelli di flussi di lavoro con JMX {#example-monitoring-workflow-models-using-jmx}

MBean in questo esempio fornisce informazioni sui modelli di flussi di lavoro CQ5 memorizzati nella directory archivio. Una classe Manager MBean crea MBeans basati su modelli Workflow memorizzati nell&#39;archivio e registra il servizio OSGi in fase di esecuzione. Questo esempio è costituito da un singolo bundle contenente i membri seguenti:

* WorkflowMBean: Interfaccia di gestione.
* WorkflowMBeanImpl: Classe di implementazione MBean.
* WorkflowMBeanManager: Interfaccia della classe Manager MBean.
* WorkflowMBeanManagerImpl: La classe di implementazione del manager MBean.

**Nota:** per semplicità, il codice di questo esempio non esegue la registrazione o reagisce alle eccezioni generate.

WorkflowMBeanManagerImpl include un metodo di attivazione dei componenti. Quando il componente viene attivato, il metodo esegue le seguenti operazioni:

* Ottiene un BundleContext per il bundle.
* Interroga il repository per ottenere i percorsi dei modelli di workflow esistenti.
* Crea MBean per ogni modello Workflow.
* Registra gli MBeans con il registro del servizio OSGi.

I metadati MBean vengono visualizzati nella console JMX con il dominio com.adobe.example, il tipo workflow_model e Proprietà è il percorso del nodo di configurazione del modello di workflow.

![jmxworkflowmè](assets/jmxworkflowmbean.png)

### Esempio MBean {#the-example-mbean}

Questo esempio richiede un&#39;interfaccia e un&#39;implementazione MBean che riflettano sull&#39;interfaccia `com.day.cq.workflow.model.WorkflowModel`. MBean è molto semplice e l&#39;esempio può concentrarsi sugli aspetti di configurazione e distribuzione della progettazione. MBean espone un singolo attributo, il nome del modello.

#### Interfaccia WorkflowMBean {#workflowmbean-interface}

```java
package com.adobe.example.myapp.api;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes Workflow model properties.")
public interface WorkflowMBean {

 @Description("The name of the Workflow model.")
 String getModelName();
}
```

#### WorkflowMBeanImpl {#workflowmbeanimpl}

```java
package com.adobe.example.myapp.impl;

import javax.management.NotCompliantMBeanException;

import com.day.cq.workflow.model.WorkflowModel;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

public class WorkflowMBeanImpl extends AnnotatedStandardMBean implements WorkflowMBean {

 WorkflowModel model;

 protected WorkflowMBeanImpl(WorkflowModel inmodel)
   throws NotCompliantMBeanException {
  super(WorkflowMBean.class);
  model=inmodel;
 }

 public String getModelName() {
  return model.getTitle();
 }
}
```

### Esempio MBean Manager {#the-example-mbean-manager}

Il servizio WorkflowMBeanManager include il metodo di attivazione del componente che crea i servizi WorkflowMBean. L&#39;implementazione del servizio include i metodi seguenti:

* activate: Attivatore del componente. Crea la sessione JCR per la lettura dei nodi di configurazione WorkflowModel. Il nodo principale in cui sono memorizzate le configurazioni del modello è definito in un campo statico. Il nome del nodo di configurazione è definito anche in un campo statico. Questo metodo richiama altri metodi che ottengono i percorsi del modello dei nodi e creano il modello WorkflowMBeans.
* getModelIds: Naviga nel repository sotto il nodo principale e recupera il percorso di ciascun nodo del modello.
* makeMBean: Utilizza il percorso del modello per creare un oggetto WorkflowModel, crea un oggetto WorkflowMBean e registra il servizio OSGi corrispondente.

>[!NOTE]
>
>L’implementazione WorkflowMBeanManager crea solo servizi MBean per le configurazioni di modelli esistenti quando il componente viene attivato. Un&#39;implementazione più affidabile ascolta gli eventi del repository relativi alle nuove configurazioni del modello e alle modifiche o eliminazioni della configurazione del modello esistente. Quando si verifica una modifica, il manager può creare, modificare o rimuovere il servizio WorkflowMBean corrispondente.


#### Interfaccia WorkflowMBeanManager {#workflowmbeanmanager-interface}

```java
package com.adobe.example.myapp.api;

public interface WorkflowMBeanManager {

}
```

#### WorkflowMBeanManagerImpl {#workflowmbeanmanagerimpl}

```java
package com.adobe.example.myapp.impl;

import java.util.*;

import org.apache.felix.scr.annotations.*;

import javax.jcr.Session;
import javax.jcr.Node;
import javax.jcr.NodeIterator;
import javax.jcr.RepositoryException;
import javax.management.ObjectName;

import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.framework.ServiceRegistration;
import org.osgi.service.component.ComponentContext;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.workflow.WorkflowService;
import com.day.cq.workflow.WorkflowSession;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.example.myapp.api.WorkflowMBeanManager;

/**Instantiates and registers WorkflowMBean services */
@Component(immediate=true)
@Service(value=WorkflowMBeanManager.class)
public class WorkflowMBeanManagerImpl implements WorkflowMBeanManager {
 //The ComponentContext provides access to the BundleContext
 private ComponentContext componentContext;

 //Use the SlingRepository service to read model nodes
 @Reference
        private SlingRepository repository = null;

 //Use the WorkflowService service to create WorkflowModel objects
 @Reference
 private WorkflowService workflowservice = null;

  private Session session;

         //Details about model nodes
  private static final String MODEL_ROOT ="/etc/workflow/models";
  private static final String MODEL_NODE = "model";

  private Set<String> modelIds = new HashSet<String>();

        //Storage for ServiceRegistrations for MBean services
  private Collection<ServiceRegistration> mbeanRegistrations= new Vector<ServiceRegistration>(0,1);

 @Activate
        protected void activate(ComponentContext ctx) {
             //Traverse the repository and load the model nodes
             try {
                   session = repository.loginAdministrative(null);
                   // load and store model node paths
                   if (session.nodeExists(MODEL_ROOT)) {
                          getModelIds(session.getNode(MODEL_ROOT));
                   }
                   //Create MBeans for each model
                   for(String modid: modelIds){
                    makeMBean(modid);
                    }
             }catch(Exception e){ }
          }

        /**
         * Add JMX domain and key properties to a collection
         * Instantiate a WorkflowModel and its WorkflowMBeanImpl object
         * Register the MBean OSGi service
         */
 private void makeMBean(String modelId) {
             // create MBean for the model
             try {
                 Dictionary<String, String> mbeanProps = new Hashtable<String, String>();
                 //These properties appear on the JMX Console home page
                 mbeanProps.put("jmx.objectname", "com.adobe.example:type=workflow_model,id=" + ObjectName.quote(modelId));
                 WorkflowSession wfsession = workflowservice.getWorkflowSession(session);
                 WorkflowMBeanImpl mbean = new WorkflowMBeanImpl(wfsession.getModel(modelId));

                ServiceRegistration serviceregistration = componentContext.getBundleContext().registerService(WorkflowMBean.class.getName(), mbean, mbeanProps);
                //Store the ServiceRegistration objects for deactivation
                mbeanRegistrations.add(serviceregistration);
             } catch (Throwable t) {}
         }

        /**
         * Traverses the repository branch below a given Node. Stores the path of each model node.
         */
 private void getModelIds(Node node) throws RepositoryException {
  try{
                     NodeIterator iter = node.getNodes();
                     while (iter.hasNext()) {
                           Node n = iter.nextNode();
                           //Look for "jcr:content" nodes
                           if (n.getName().equals("jcr:content")) {
                                //get the path of the model node and save it
                                if(n.hasNode(MODEL_NODE)){
                                      modelIds.add(n.getNode(MODEL_NODE).getPath());
                                 }
                           } else{
                                   //Scan child nodes
                                   getModelIds(n);
                           }
                       }
  }catch(Exception e){ }
       }

        /**
         * Log out of the JCR session and unregister WorkflowMBean services
         */
        @Deactivate
        protected void deactivate() {
          session.logout();
          session=null;
          for(ServiceRegistration sr:mbeanRegistrations){
         sr.unregister();
          }
        }
}
```

### Il file POM per l&#39;esempio MBean {#the-pom-file-for-the-example-mbean}

Per comodità, potete copiare e incollare il seguente codice XML nel file pom.xml del progetto per creare il bundle di componenti. Il POM fa riferimento a diversi plug-in e dipendenze richiesti.

**Plug-in:**

* Plug-in Apache Maven Compiler: Compila le classi Java dal codice sorgente.
* Plug-in Apache Felix Maven Bundle: Crea il bundle e il manifesto
* Plugin Apache Felix Maven SCR: Crea il file descrittore del componente e configura l’intestazione del manifesto service-component.

**Nota:** Al momento della scrittura, il plugin maven scr non è compatibile con il plugin m2e per Eclipse. (Vedere [Felix bug 3170](https://issues.apache.org/jira/browse/FELIX-3170).) Per utilizzare l&#39;IDE Eclipse, installare Maven e utilizzare l&#39;interfaccia della riga di comando per eseguire le build.

#### Esempio di file POM {#example-pom-file}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.2-SNAPSHOT</version>
  <name>mbean-simple</name>
  <url>www.adobe.com</url>
  <description>A simple MBean</description>
  <packaging>bundle</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-scr-plugin</artifactId>
                <version>1.7.2</version>
                <executions>
                    <execution>
                        <id>generate-scr-scrdescriptor</id>
              <goals>
                 <goal>scr</goal>
              </goals>
            </execution>
         </executions>
            </plugin>
             <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.6.0</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.api</artifactId>
            <version>2.0.8</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr</artifactId>
            <version>1.6.1-R1236132</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.jcr.api</artifactId>
            <version>2.0.4</version>
        </dependency>
        <dependency>
            <groupId>com.adobe.granite</groupId>
            <artifactId>com.adobe.granite.jmx</artifactId>
            <version>0.1.6</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
       <groupId>com.day.cq.wcm</groupId>
       <artifactId>cq-wcm-mobile-api</artifactId>
       <version>5.5.2</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>com.day.cq.workflow</groupId>
       <artifactId>cq-workflow-api</artifactId>
       <version>5.5.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>javax.jcr</groupId>
       <artifactId>jcr</artifactId>
       <version>2.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
                <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.6.4</version>
  <scope>provided</scope>
 </dependency>
    </dependencies>
</project>
```

Aggiungete il seguente profilo al file delle impostazioni del sito Web per utilizzare il repository del Adobe  pubblico.

#### Profilo del cielo {#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```
