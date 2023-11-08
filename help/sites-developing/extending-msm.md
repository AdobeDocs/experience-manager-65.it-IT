---
title: Estensione di Multi Site Manager
description: Questa pagina consente di estendere le funzionalità del gestore multisito
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2582'
ht-degree: 2%

---

# Estensione di Multi Site Manager{#extending-the-multi-site-manager}

Questa pagina consente di estendere le funzionalità del gestore multisito:

* Scopri i membri principali dell’API Java MSM.
* Crea un&#39;azione di sincronizzazione che può essere utilizzata in una configurazione di rollout.
* Modificare la lingua e i codici paese predefiniti.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Questa pagina deve essere letta insieme a [Riutilizzo del contenuto: Gestore multisito](/help/sites-administering/msm.md).
>
>Anche le seguenti sezioni di Ristrutturazione dell’archivio Sites potrebbero essere di interesse:
>* [Configurazioni blueprint per Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-blueprint-configurations)
>* [Configurazioni di rollout di Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-rollout-configurations)

>[!CAUTION]
>
>Multi Site Manager e la relativa API vengono utilizzati per la creazione di un sito web, quindi sono destinati solo all’ambiente di authoring.

## Panoramica dell’API Java {#overview-of-the-java-api}

La gestione multisito è costituita dai seguenti pacchetti:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

I principali oggetti API MSM interagiscono come segue (vedi anche [Termini utilizzati](/help/sites-administering/msm.md#terms-used)):

![Oggetti API MSM principali](assets/chlimage_1-73.png)

* **`Blueprint`**

  A `Blueprint` (come in [configurazione blueprint](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) specifica le pagine da cui una live copy può ereditare il contenuto.

  ![Blueprint](assets/chlimage_1-74.png)

   * Utilizzo di una configurazione blueprint ( `Blueprint`) è facoltativo, ma:

      * Consente all&#39;autore di utilizzare **Rollout** sull’origine (per inviare (esplicitamente) le modifiche alle live copy che ereditano da questa origine).
      * Consente all’autore di utilizzare **Crea sito**; questo consente all’utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
      * Definisce la configurazione di rollout predefinita per tutte le Live Copy risultanti.

* **`LiveRelationship`**

  Il `LiveRelationship` specifica la connessione (relazione) tra una risorsa nel ramo live copy e la relativa risorsa sorgente/blueprint equivalente.

   * Le relazioni vengono utilizzate per la realizzazione dell’ereditarietà e del rollout.
   * `LiveRelationship` Gli oggetti forniscono accesso (riferimenti) alle configurazioni di rollout ( `RolloutConfig`), `LiveCopy`, e `LiveStatus` oggetti correlati alla relazione.

   * Ad esempio, una Live Copy viene creata in `/content/copy/us` dalla sorgente/blueprint in `/content/we-retail/language-masters`. Le risorse `/content/we.retail/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` creare una relazione.

* **`LiveCopy`**

  `LiveCopy` contiene i dettagli di configurazione per le relazioni ( `LiveRelationship`) tra le risorse live copy e le relative risorse sorgente/blueprint.

   * Utilizza il `LiveCopy` classe per accedere al percorso della pagina, al percorso della pagina sorgente/blueprint, alle configurazioni di rollout e se le pagine figlie sono incluse anche nel `LiveCopy`.

   * A `LiveCopy` viene creato ogni volta **Crea sito** o **Crea Live Copy** viene utilizzato.

* **`LiveStatus`**

  `LiveStatus` gli oggetti forniscono accesso allo stato di runtime di un `LiveRelationship`. Utilizza per eseguire una query sullo stato di sincronizzazione di una Live Copy.

* **`LiveAction`**

  A `LiveAction` è un’azione eseguita su ogni risorsa coinvolta nel rollout.

   * Le LiveActions vengono generate solo da RolloutConfigs.

* **`LiveActionFactory`**

  Crea `LiveAction` oggetti a cui è stato assegnato un `LiveAction` configurazione. Le configurazioni vengono memorizzate come risorse nell’archivio.

* **`RolloutConfig`**

  Il `RolloutConfig` contiene un elenco di `LiveActions`, da utilizzare quando viene attivato. Il `LiveCopy` eredita il `RolloutConfig` e il risultato è presente nel `LiveRelationship`.

   * Quando si imposta una Live Copy per la prima volta, viene utilizzato anche un RolloutConfig (che attiva le LiveActions).

## Creazione di una nuova azione di sincronizzazione {#creating-a-new-synchronization-action}

Crea azioni di sincronizzazione personalizzate da utilizzare con le configurazioni di rollout. Creare un&#39;azione di sincronizzazione quando [azioni installate](/help/sites-administering/msm-sync.md#installed-synchronization-actions) non soddisfano i requisiti specifici dell&#39;applicazione. A tale scopo, crea due classi:

* Un&#39;implementazione del [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) che esegue l&#39;azione.
* Un componente OSGI che implementa [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) e crea istanze della `LiveAction` classe.

Il `LiveActionFactory` crea istanze del `LiveAction` classe per una determinata configurazione:

* `LiveAction` le classi includono i seguenti metodi:

   * `getName`: restituisce il nome dell’azione. Il nome viene utilizzato per fare riferimento all&#39;azione, ad esempio, nelle configurazioni di rollout.
   * `execute`: esegue le attività dell’azione.

* `LiveActionFactory` le classi includono i seguenti membri:

   * `LIVE_ACTION_NAME`: campo che contiene il nome del campo associato `LiveAction`. Questo nome deve coincidere con il valore restituito da `getName` metodo del `LiveAction` classe.

   * `createAction`: crea un’istanza del `LiveAction`. L&#39;opzione `Resource` Il parametro può essere utilizzato per fornire informazioni di configurazione.

   * `createsAction`: restituisce il nome del associato `LiveAction`.

### Accesso al nodo di configurazione LiveAction {#accessing-the-liveaction-configuration-node}

Utilizza il `LiveAction` nel repository per memorizzare le informazioni che influiscono sul comportamento in fase di esecuzione del `LiveAction` dell&#39;istanza. Il nodo nell’archivio in cui è memorizzato `LiveAction` è disponibile per `LiveActionFactory` oggetto in fase di runtime. Pertanto, puoi aggiungere proprietà al nodo di configurazione e utilizzarle nel tuo `LiveActionFactory` all&#39;occorrenza.

Ad esempio, un `LiveAction` deve memorizzare il nome dell’autore blueprint. Una proprietà del nodo di configurazione include il nome della proprietà della pagina blueprint in cui sono memorizzate le informazioni. In fase di runtime, `LiveAction` recupera il nome della proprietà dalla configurazione, quindi ottiene il valore della proprietà.

Il parametro del [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) è un metodo `Resource` oggetto. Questo `Resource` l&#39;oggetto rappresenta `cq:LiveSyncAction` per questa azione live nella configurazione di rollout; vedi [Creazione di una configurazione di rollout](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). Come sempre quando si utilizza un nodo di configurazione, è necessario adattarlo a un `ValueMap` oggetto:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Accesso ai nodi di destinazione, ai nodi di origine e alla LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

I seguenti oggetti vengono forniti come parametri del `execute` metodo del `LiveAction` oggetto:

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) oggetto che rappresenta l’origine della Live Copy.
* A `Resource` oggetto che rappresenta la destinazione della Live Copy.
* Il [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) oggetto per la live copy.
* Il `autoSave` il valore indica se il `LiveAction` deve salvare le modifiche apportate all’archivio.

* Il valore reset indica la modalità di rollout reset.

Da questi oggetti è possibile ottenere tutte le informazioni relative al `LiveCopy`. È inoltre possibile utilizzare `Resource` oggetti da ottenere `ResourceResolver`, `Session`, e `Node` oggetti. Questi oggetti sono utili per la manipolazione del contenuto del repository:

Nella prima riga del codice seguente, l’origine è `Resource` oggetto della pagina sorgente:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Il `Resource` possono essere `null` o `Resources` oggetti che non si adattano `Node` oggetti, come [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/NonExistingResource.html) oggetti.

## Creazione di una nuova configurazione di rollout {#creating-a-new-rollout-configuration}

Crea una configurazione di rollout quando le configurazioni di rollout installate non soddisfano i requisiti dell’applicazione:

* [Creare la configurazione di rollout](#create-the-rollout-configuration).
* [Aggiungere azioni di sincronizzazione alla configurazione di rollout](#add-synchronization-actions-to-the-rollout-configuration).

La nuova configurazione di rollout è quindi disponibile quando imposti le configurazioni di rollout su una pagina blueprint o Live Copy.

>[!NOTE]
>
>Consulta anche [best practice per personalizzare i rollout](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Creare la configurazione di rollout {#create-the-rollout-configuration}

1. Apri CRXDE Liti; ad esempio:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Accedi a :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Questa è la versione personalizzata del tuo progetto di:
   >`/libs/msm/wcm/rolloutconfigs`
   >Se si tratta della prima configurazione, `/libs` il ramo deve essere utilizzato come modello per creare il nuovo ramo in `/apps`.

   >[!NOTE]
   >
   >Non è necessario modificare nulla nel `/libs` percorso.
   >Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe benissimo essere sovrascritto quando applichi un hotfix o un feature pack).
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >* Ricrea l&#39;elemento richiesto, ovvero come esiste in `/libs`) in `/apps`
   >* Apporta le modifiche in `/apps`

1. Sotto questo **Crea** un nodo con le seguenti proprietà:

   * **Nome**: nome del nodo della configurazione di rollout. md#install-synchronization-actions), ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Aggiungi le seguenti proprietà a questo nodo:
   * **Nome**: `jcr:title`
     **Tipo**: `String`
     **Valore**: titolo che verrà visualizzato nell’interfaccia utente di.
   * **Nome**: `jcr:description`
     **Tipo**: `String`
     **Valore**: descrizione facoltativa.
   * **Nome**: `cq:trigger`
     **Tipo**: `String`
     **Valore**: Il [Attivatore rollout](/help/sites-administering/msm-sync.md#rollout-triggers) da utilizzare. Seleziona da:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Clic **Salva tutto**.

### Aggiungere azioni di sincronizzazione alla configurazione di rollout {#add-synchronization-actions-to-the-rollout-configuration}

Le configurazioni di rollout sono memorizzate sotto [nodo di configurazione rollout](#create-the-rollout-configuration) che hai creato in `/apps/msm/<your-project>/rolloutconfigs` nodo.

Aggiungi nodi figlio di tipo `cq:LiveSyncAction` per aggiungere azioni di sincronizzazione alla configurazione di rollout. L&#39;ordine dei nodi delle azioni di sincronizzazione determina l&#39;ordine in cui si verificano le azioni.

1. Sempre in CRXDE Liti, seleziona il tuo [Configurazione rollout](#create-the-rollout-configuration) nodo.

   Ad esempio:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Crea** un nodo con le seguenti proprietà:

   * **Nome**: nome del nodo dell’azione di sincronizzazione.
Il nome deve essere uguale al **Nome azione** nella tabella sotto [Azioni di sincronizzazione](/help/sites-administering/msm-sync.md#installed-synchronization-actions)ad esempio: `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Aggiungere e configurare tutti i nodi delle azioni di sincronizzazione necessari. Ridisponi i nodi delle azioni in modo che il loro ordine corrisponda all’ordine in cui desideri che si verifichino. Il nodo di azione più in alto si verifica per primo.

## Creazione e utilizzo di una classe LiveActionFactory semplice {#creating-and-using-a-simple-liveactionfactory-class}

Segui le procedure descritte in questa sezione per sviluppare un’ `LiveActionFactory` e utilizzalo in una configurazione di rollout. Le procedure utilizzano Maven ed Eclipse per sviluppare e distribuire `LiveActionFactory`:

1. [Creare il progetto Maven](#create-the-maven-project) e importalo in Eclipse.
1. [Aggiungi dipendenze](#add-dependencies-to-the-pom-file) nel file POM.
1. [Implementare `LiveActionFactory` interfaccia](#implement-liveactionfactory) e implementa il bundle OSGi.
1. [Creare la configurazione di rollout](#create-the-example-rollout-configuration).
1. [Creare la Live Copy](#create-the-live-copy).

Il progetto Maven e il codice sorgente della classe Java sono disponibili nell’archivio Git pubblico.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto experiencemanager-java-msmrollout su GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Creare il progetto Maven {#create-the-maven-project}

La procedura seguente richiede che tu abbia aggiunto il profilo adobe-public al file delle impostazioni Maven.

* Per informazioni sul profilo pubblico di Adobe, consulta [Ottenere il plug-in Maven del pacchetto di contenuti](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Per informazioni sul file di impostazioni Maven, vedi Maven [Riferimento impostazioni](https://maven.apache.org/settings.html).

1. Apri un terminale o una sessione della riga di comando e cambia la directory in modo che punti alla posizione in cui creare il progetto.
1. Immetti il comando seguente:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Specifica i seguenti valori al prompt interattivo:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. Avvia Eclipse e [importare il progetto Maven](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Aggiungi dipendenze al file POM {#add-dependencies-to-the-pom-file}

Aggiungere le dipendenze in modo che il compilatore Eclipse possa fare riferimento alle classi utilizzate nel `LiveActionFactory` codice.

1. Da Esplora progetto Eclipse, apri il file:

   `MyLiveActionFactory/pom.xml`

1. Nell’editor, fai clic su `pom.xml` e individuare il `project/dependencyManagement/dependencies` sezione.
1. Aggiungi il seguente XML all&#39;interno del `dependencyManagement` e quindi salvare il file.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Apri il file POM del bundle da **Gestione progetti** a `MyLiveActionFactory-bundle/pom.xml`.
1. Nell’editor, fai clic su `pom.xml` e individuare la sezione progetto/dipendenze. Aggiungi il seguente XML all’interno dell’elemento dependencies, quindi salva il file:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementare LiveActionFactory {#implement-liveactionfactory}

I seguenti elementi `LiveActionFactory` la classe implementa una `LiveAction` che registra i messaggi sulle pagine di origine e di destinazione e copia i `cq:lastModifiedBy` dal nodo di origine al nodo di destinazione. Il nome dell’azione live è `exampleLiveAction`.

1. In Eclipse Project Explorer, fai clic con il pulsante destro del mouse sul `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` pacchetto e fai clic su **Nuovo** > **Classe**. Per **Nome**, immetti `ExampleLiveActionFactory` e quindi fare clic su **Fine**.
1. Apri `ExampleLiveActionFactory.java` , sostituire il contenuto con il codice seguente e salvare il file.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Utilizzando il terminale o la sessione di comando, modificare la directory in `MyLiveActionFactory` (la directory del progetto Maven). Quindi, immetti il seguente comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   L&#39;AEM `error.log` Il file deve indicare che il bundle è stato avviato.

   Ad esempio: [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creare la configurazione di rollout di esempio {#create-the-example-rollout-configuration}

Crea la configurazione di rollout MSM che utilizza `LiveActionFactory` creato:

1. Creare e configurare un [Rollout della configurazione con la procedura standard](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) - e utilizzando le proprietà:

   * **Titolo**: esempio di configurazione di rollout
   * **Nome**: examplerolloutconfig
   * **cq:trigger**: `publish`

### Aggiungi l’azione live alla configurazione di rollout di esempio {#add-the-live-action-to-the-example-rollout-configuration}

Configura la configurazione di rollout creata nella procedura precedente in modo che utilizzi `ExampleLiveActionFactory` classe.

1. Apri CRXDE Liti; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Crea il seguente nodo sotto `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Clic **Salva tutto**.
1. Seleziona la `exampleLiveAction` e aggiungi la seguente proprietà:

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

   Questa proprietà indica al `ExampleLiveAction` classe che `cq:LastModifiedBy` deve essere replicata dal nodo di origine a quello di destinazione.

1. Clic **Salva tutto**.

### Creare la Live Copy {#create-the-live-copy}

[Creare una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) della sezione inglese/prodotti del sito di riferimento We.Retail utilizzando la configurazione di rollout:

* **Origine**: `/content/we-retail/language-masters/en/products`

* **Configurazione rollout**: esempio di configurazione di rollout

Attiva il **Prodotti** (inglese) del ramo di origine e osserva i messaggi di registro che `LiveAction` la classe genera:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Modifica dei nomi delle lingue e dei paesi predefiniti {#changing-language-names-and-default-countries}

L’AEM utilizza un set predefinito di codici per lingua e paese.

* Il codice lingua predefinito è il codice a due lettere minuscole, come definito dallo standard ISO-639-1.
* Il codice predefinito del paese è il codice a due lettere minuscole o maiuscole, come definito dallo standard ISO 3166.

MSM utilizza un elenco memorizzato di codici di lingua e paese per determinare il nome del paese associato al nome della versione della lingua della pagina. Se necessario, puoi modificare i seguenti aspetti dell’elenco:

* Titoli delle lingue
* Nomi paesi
* Paesi predefiniti per le lingue (per codici come `en`, `de`, tra gli altri)

L&#39;elenco delle lingue è memorizzato sotto `/libs/wcm/core/resources/languages` nodo. Ogni nodo figlio rappresenta una lingua o un paese della lingua:

* Il nome del nodo è il codice della lingua (ad esempio `en` o `de`) o il codice language_country (ad esempio `en_us` o `de_ch`).

* Il `language` del nodo memorizza il nome completo della lingua per il codice.
* Il `country` del nodo memorizza il nome completo del paese per il codice.
* Quando il nome del nodo è costituito solo da un codice della lingua (ad esempio `en`), la proprietà country è `*`, e un&#39;ulteriore `defaultCountry` La proprietà memorizza il codice della lingua-paese per indicare il paese da utilizzare.

![Definizione lingua](assets/chlimage_1-76.png)

Per modificare le lingue:

1. Apri CRXDE Liti nel browser web; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Seleziona la `/apps` cartella e fai clic su **Crea**, quindi **Crea cartella.**

   Denomina la nuova cartella `wcm`.

1. Ripeti il passaggio precedente per creare `/apps/wcm/core` struttura di cartelle. Creare un nodo di tipo `sling:Folder` in `core` ha chiamato `resources`. <!-- ![Resources](assets/chlimage_1-77.png) -->

1. Fare clic con il pulsante destro del mouse `/libs/wcm/core/resources/languages` e fai clic su **Copia**.
1. Fare clic con il pulsante destro del mouse `/apps/wcm/core/resources` cartella e fai clic su **Incolla**. Modificare i nodi figlio come richiesto.
1. Clic **Salva tutto**.
1. Clic **Strumenti**, **Operazioni** allora **Console web**. Da questa console fai clic su **OSGi**, quindi **Configurazione**.
1. Individua e fai clic su **Gestione lingua WCM Day CQ** e modificare il valore di **Elenco lingue** a `/apps/wcm/core/resources/languages`, quindi fai clic su **Salva**.

   ![Gestione lingua WCM Day CQ](assets/chlimage_1-78.png)

## Configurazione dei blocchi MSM nelle proprietà della pagina (interfaccia touch) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Quando crei una proprietà di pagina personalizzata, potrebbe essere necessario considerare se la nuova proprietà può essere idonea per il rollout in qualsiasi Live Copy.

Ad esempio, se vengono aggiunte due nuove proprietà di pagina:

* E-mail di contatto:

   * Non è necessario implementare questa proprietà, in quanto sarà diversa in ciascun paese (o marchio, ecc.).

* Stile visivo chiave:

   * Il requisito del progetto è che questa proprietà venga implementata in quanto è (di solito) comune a tutti i paesi (o marchi, e così via).

Quindi è necessario assicurarsi che:

* E-mail di contatto:

* è escluso dalle proprietà di rollout; vedi [Esclusione di proprietà e tipi di nodo dalla sincronizzazione](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Stile visivo chiave:

* Assicurati di non essere autorizzato a modificare questa proprietà nell’interfaccia utente touch a meno che l’ereditarietà non venga annullata, e di poter quindi ripristinare l’ereditarietà; questo viene controllato facendo clic sui collegamenti a catena o a catena interrotta che attivano per indicare lo stato della connessione.

Se una proprietà di pagina è soggetta a rollout e quindi, in caso di annullamento/ripristino dell’ereditarietà durante la modifica, è controllata dalla proprietà della finestra di dialogo:

* `cq-msm-lockable`

   * è applicabile agli elementi in una finestra di dialogo dell’interfaccia touch
   * creerà il simbolo del collegamento a catena nella finestra di dialogo
   * consente la modifica solo se l’ereditarietà viene annullata (il collegamento a catena è interrotto)
   * si applica solo al primo livello figlio della risorsa
      * **Tipo**: `String`

      * **Valore**: detiene il nome della proprietà in questione (ed è paragonabile al valore della proprietà) `name`; ad esempio, vedi
        `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Quando `cq-msm-lockable` è stato definito, la rottura/chiusura della catena interagirà con MSM nel modo seguente:

* se il valore di `cq-msm-lockable` è:

   * **Relativo** (ad esempio, `myProperty` o `./myProperty`)

      * aggiungerà e rimuoverà la proprietà da `cq:propertyInheritanceCancelled`.

   * **Assoluto** (ad esempio, `/image`)

      * interrompendo la catena, l’ereditarietà verrà annullata aggiungendo il `cq:LiveSyncCancelled` mixin a `./image` e l&#39;impostazione `cq:isCancelledForChildren` a `true`.

      * la chiusura della catena ripristina l’ereditarietà.

>[!NOTE]
>
>`cq-msm-lockable` si applica al primo livello figlio della risorsa da modificare e non funziona su nessun livello precedente più profondo, a prescindere dal fatto che il valore sia definito come assoluto o relativo.

>[!NOTE]
>
>Quando riabiliti l’ereditarietà, la proprietà della pagina Live Copy non viene sincronizzata automaticamente con la proprietà sorgente. Se necessario, è possibile richiedere manualmente una sincronizzazione.
