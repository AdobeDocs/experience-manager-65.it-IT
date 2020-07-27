---
title: Estensione di Multi Site Manager
seo-title: Estensione di Multi Site Manager
description: Questa pagina consente di estendere le funzionalità di Multi Site Manager
seo-description: Questa pagina consente di estendere le funzionalità di Multi Site Manager
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
translation-type: tm+mt
source-git-commit: d488b1acc789c0fb1a631e58844d9fe9a70c2662
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 2%

---


# Estensione di Multi Site Manager{#extending-the-multi-site-manager}

Questa pagina consente di estendere le funzionalità di Multi Site Manager:

* Informazioni sui membri principali dell&#39;API Java MSM.
* Create una nuova azione di sincronizzazione che possa essere utilizzata in una configurazione di rollout.
* Rimuovete il passaggio &quot;Capitoli&quot; nella procedura guidata Crea sito.
* Modificare la lingua e i codici paese predefiniti.

>[!NOTE]
>
>Questa pagina deve essere letta insieme a [Riutilizzo del contenuto: Multi Site Manager](/help/sites-administering/msm.md).
>
>Anche le seguenti sezioni sulla ristrutturazione del repository dei siti in AEM 6.4 potrebbero essere di interesse:
>* [Configurazioni Blueprint Manager multisito](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [Configurazioni di rollout di Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>Multi Site Manager e le relative API vengono utilizzate per la creazione di un sito Web, pertanto sono destinate solo all’utilizzo in un ambiente di authoring.

## Panoramica dell&#39;API Java {#overview-of-the-java-api}

Multi Site Management è costituito dai pacchetti seguenti:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

I principali oggetti API MSM interagiscono come segue (vedere anche [Termini utilizzati](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   Un `Blueprint` (come nella configurazione [](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)blueprint) specifica le pagine da cui una Live Copy può ereditare il contenuto.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * L&#39;utilizzo di una configurazione blueprint ( `Blueprint`) è facoltativo, ma:

      * Consente all’autore di utilizzare l’opzione **Rollout** sull’origine (per (in modo esplicito) le modifiche push alle Live Copy che ereditano da questa origine).
      * Consente all&#39;autore di utilizzare **Crea sito**; questo consente all&#39;utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
      * Definisce la configurazione di rollout predefinita per tutte le copie live risultanti.

* **`LiveRelationship`** Specifica `LiveRelationship` la connessione (relazione) tra una risorsa nel ramo Live Copy e la risorsa sorgente/blueprint equivalente.

   * Le relazioni vengono utilizzate quando si realizza l&#39;ereditarietà e il rollout.
   * `LiveRelationship` gli oggetti forniscono l&#39;accesso (riferimenti) alle configurazioni di rollout ( `RolloutConfig`) `LiveCopy`e `LiveStatus` agli oggetti correlati alla relazione.

   * Ad esempio, una Live Copy viene creata in `/content/copy/us` dalla sorgente o dal blueprint in `/content/we-retail/language-masters`. Le risorse `/content/we.retail/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` formano una relazione.

* **`LiveCopy`** `LiveCopy` contiene i dettagli di configurazione per le relazioni ( `LiveRelationship`) tra le risorse Live Copy e le relative risorse di origine/blueprint.

   * Utilizzate la `LiveCopy` classe per accedere al percorso della pagina, al percorso della pagina di origine/blueprint, alle configurazioni di rollout e all&#39;eventuale inclusione di pagine figlie nella `LiveCopy`.

   * Un `LiveCopy` nodo viene creato ogni volta che si utilizza **Crea sito** o **Crea Live Copy** .

* **`LiveStatus`**

   `LiveStatus` forniscono l&#39;accesso allo stato di runtime di un `LiveRelationship`. Consente di eseguire una query sullo stato di sincronizzazione di una Live Copy.

* **`LiveAction`**

   Un `LiveAction` è un&#39;azione eseguita su ogni risorsa coinvolta nel rollout.

   * LiveActions vengono generati solo da RolloutConfigs.

* **`LiveActionFactory`**

   Crea `LiveAction` oggetti in base a una `LiveAction` configurazione. Le configurazioni sono memorizzate come risorse nella directory archivio.

* **`RolloutConfig`** Contiene `RolloutConfig` un elenco di `LiveActions`, da utilizzare quando viene attivato. L&#39; `LiveCopy` eredita il risultato `RolloutConfig` e il risultato è presente nell&#39; `LiveRelationship`.

   * Quando si configura una copia dal vivo per la prima volta, viene utilizzato anche un RolloutConfig (che attiva le azioni LiveActions).

## Creazione di una nuova azione di sincronizzazione {#creating-a-new-synchronization-action}

Create azioni di sincronizzazione personalizzate da utilizzare con le configurazioni di rollout. Create un&#39;azione di sincronizzazione quando le azioni [](/help/sites-administering/msm-sync.md#installed-synchronization-actions) installate non soddisfano i requisiti specifici dell&#39;applicazione. A tale scopo, creare due classi:

* Implementazione dell&#39; [`com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) interfaccia che esegue l&#39;azione.
* Componente OSGI che implementa l’ [ interfaccia e crea le istanze della `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) `LiveAction` classe.

Crea `LiveActionFactory` le istanze della `LiveAction` classe per una determinata configurazione:

* `LiveAction` le classi includono i metodi seguenti:

   * `getName`: Restituisce il nome dell&#39;azione Il nome viene utilizzato per fare riferimento all&#39;azione, ad esempio nelle configurazioni di rollout.
   * `execute`: Esegue le attività dell&#39;azione.

* `LiveActionFactory` le classi includono i seguenti membri:

   * `LIVE_ACTION_NAME`: Campo che contiene il nome dell&#39;associato `LiveAction`. Questo nome deve coincidere con il valore restituito dal `getName` metodo della `LiveAction` classe.

   * `createAction`: Crea un&#39;istanza dell&#39; `LiveAction`. Il `Resource` parametro opzionale può essere utilizzato per fornire informazioni sulla configurazione.

   * `createsAction`: Restituisce il nome dell&#39;associato `LiveAction`.

### Accesso al nodo di configurazione LiveAction {#accessing-the-liveaction-configuration-node}

Utilizzate il nodo di `LiveAction` configurazione nell&#39;archivio per memorizzare informazioni che influiscono sul comportamento di runtime dell&#39; `LiveAction` istanza. Il nodo nell&#39;archivio che memorizza la `LiveAction` configurazione è disponibile per l&#39; `LiveActionFactory` oggetto in fase di esecuzione. Di conseguenza, puoi aggiungere proprietà al nodo di configurazione e utilizzarle nell&#39; `LiveActionFactory` implementazione, se necessario.

Ad esempio, un utente `LiveAction` deve memorizzare il nome dell’autore della blueprint. Una proprietà del nodo di configurazione include il nome della proprietà della pagina di blueprint in cui sono memorizzate le informazioni. In fase di esecuzione, il `LiveAction` recupero del nome della proprietà dalla configurazione, quindi ottiene il valore della proprietà.

Il parametro del ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` metodo è un `Resource` oggetto. Questo `Resource` oggetto rappresenta il `cq:LiveSyncAction` nodo per questa azione live nella configurazione rollout; consultate [Creazione di una configurazione](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)rollout. Come di consueto, quando si utilizza un nodo di configurazione è necessario adattarlo a un `ValueMap` oggetto:

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

### Accesso ai nodi Target, ai nodi di origine e alla LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

I seguenti oggetti sono forniti come parametri del `execute` metodo dell&#39; `LiveAction` oggetto:

* Un [`Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) oggetto che rappresenta l&#39;origine della Live Copy.
* Un `Resource` oggetto che rappresenta la destinazione di Live Copy.
* L&#39; [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) oggetto per la Live Copy.
* Il `autoSave` valore indica se `LiveAction` salvare le modifiche apportate alla directory archivio.

* Il valore reset indica la modalità di ripristino rollout.

Da questi oggetti è possibile ottenere tutte le informazioni sul `LiveCopy`. È inoltre possibile utilizzare gli `Resource` oggetti per ottenere `ResourceResolver`, `Session`e `Node` oggetti. Questi oggetti sono utili per manipolare il contenuto dell&#39;archivio:

Nella prima riga del codice seguente, source è l&#39; `Resource` oggetto della pagina di origine:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Gli `Resource` argomenti possono essere `null` o `Resources` oggetti che non si adattano agli `Node` oggetti, ad esempio [`NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) gli oggetti.

## Creating a New Rollout Configuration {#creating-a-new-rollout-configuration}

Create una configurazione di rollout quando le configurazioni di rollout installate non soddisfano i requisiti dell&#39;applicazione:

* [Crea la configurazione di rollout](#create-the-rollout-configuration).
* [Aggiungi le azioni di sincronizzazione alla configurazione di rollout](#add-synchronization-actions-to-the-rollout-configuration).

La nuova configurazione di rollout è quindi disponibile quando imposti le configurazioni di rollout su una pagina blueprint o Live Copy.

>[!NOTE]
>
>Consultate anche le [best practice per la personalizzazione dei](/help/sites-administering/msm-best-practices.md#customizing-rollouts)rollout.

### Create the Rollout Configuration {#create-the-rollout-configuration}

Per creare una nuova configurazione di rollout:

1. Aperto CRXDE Lite; ad esempio:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Accedi a :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Questa è la versione personalizzata del progetto di:
   >`/libs/msm/wcm/rolloutconfigs`
   >Deve essere creato se si tratta della prima configurazione.

   >[!NOTE]
   >
   >Non è necessario modificare nulla nel percorso /libs.
   >Questo perché il contenuto di /libs viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >* Ricreare l&#39;elemento richiesto (ovvero come esiste in /libs) in /apps
   >* Apportare modifiche all&#39;interno di /apps


1. In questa sezione **Create** un nodo con le seguenti proprietà:

   * **Nome**: Il nome del nodo della configurazione del rollout. md#installed-sync-actions), ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Aggiungi le seguenti proprietà al nodo:
   * **Nome**: `jcr:title`

      **Tipo**: `String`
      **Valore**: Titolo identificativo che verrà visualizzato nell’interfaccia utente.
   * **Nome**: `jcr:description`

      **Tipo**: `String`
      **Valore**: Una descrizione facoltativa.
   * **Nome**: `cq:trigger`

      **Tipo**: `String`
      **Valore**: Trigger [Rollout](/help/sites-administering/msm-sync.md#rollout-triggers) da utilizzare. Seleziona da:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Fate clic su **Salva tutto**.

### Add Synchronization Actions to the Rollout Configuration {#add-synchronization-actions-to-the-rollout-configuration}

Le configurazioni di rollout sono memorizzate sotto il nodo [di configurazione di](#create-the-rollout-configuration) rollout creato sotto il `/apps/msm/<your-project>/rolloutconfigs` nodo.

Aggiungete nodi secondari di tipo `cq:LiveSyncAction` per aggiungere azioni di sincronizzazione alla configurazione del rollout. L&#39;ordine dei nodi di azione della sincronizzazione determina l&#39;ordine in cui si verificano le azioni.

1. Sempre in CRXDE Lite, selezionate il nodo [Rollout Configuration](#create-the-rollout-configuration) .

   Ad esempio:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Creare** un nodo con le seguenti proprietà:

   * **Nome**: Il nome del nodo dell&#39;azione di sincronizzazione.
Il nome deve corrispondere al nome dell’ **azione** nella tabella in Azioni [di](/help/sites-administering/msm-sync.md#installed-synchronization-actions)sincronizzazione, ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Aggiungi e configura tutti i nodi di azione di sincronizzazione richiesti. Ridisporre i nodi di azione in modo che il loro ordine corrisponda all&#39;ordine in cui si desidera che si verifichino. Il nodo di azione superiore si verifica per primo.

## Creazione e utilizzo di una semplice classe LiveActionFactory {#creating-and-using-a-simple-liveactionfactory-class}

Seguite le procedure riportate in questa sezione per sviluppare un `LiveActionFactory` e utilizzarlo in una configurazione di rollout. Le procedure utilizzano Maven ed Eclipse per sviluppare e distribuire `LiveActionFactory`:

1. [Create il progetto](#create-the-maven-project) del cielo e importatelo in Eclipse.
1. [Aggiungere dipendenze](#add-dependencies-to-the-pom-file) al file POM.
1. [Implementate l’ `LiveActionFactory` interfaccia](#implement-liveactionfactory) e distribuite il bundle OSGi.
1. [Crea la configurazione di rollout](#create-the-example-rollout-configuration).
1. [Create la Live Copy](#create-the-live-copy).

Il progetto Maven e il codice sorgente della classe Java sono disponibili nel repository Git pubblico.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto Experience emanager-java-msmrollout su GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Crea progetto Paradiso {#create-the-maven-project}

La procedura seguente richiede l’aggiunta del profilo adobe-public al file delle impostazioni Maven.

* Per informazioni sul profilo adobe-public, consultate [Acquisizione del plug-in Content Package Maven](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Per informazioni sul file delle impostazioni di Paradiso, consultate il Riferimento [delle](https://maven.apache.org/settings.html)impostazioni di Paradiso.

1. Aprite una sessione di terminale o riga di comando e cambiate la directory in modo che punti alla posizione in cui creare il progetto.
1. Digitate il comando seguente:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Al prompt interattivo, specificate i seguenti valori:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. Avviate Eclipse e [importate il progetto](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)Maven.

### Aggiungere dipendenze al file POM {#add-dependencies-to-the-pom-file}

Aggiungete dipendenze in modo che il compilatore Eclipse possa fare riferimento alle classi utilizzate nel `LiveActionFactory` codice.

1. In Esplora progetti Eclipse, apri il file:

   `MyLiveActionFactory/pom.xml`

1. Nell’editor, fate clic sulla `pom.xml` scheda e individuate la `project/dependencyManagement/dependencies` sezione.
1. Aggiungete il seguente codice XML all’interno dell’ `dependencyManagement` elemento, quindi salvate il file.

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

1. Aprite il file POM per il bundle da **Esplora** progetti all&#39;indirizzo `MyLiveActionFactory-bundle/pom.xml`.
1. Nell’editor, fate clic sulla `pom.xml` scheda e individuate la sezione progetto/dipendenze. Aggiungete il seguente codice XML all’interno dell’elemento dipendenze, quindi salvate il file:

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

### Implementa LiveActionFactory {#implement-liveactionfactory}

La `LiveActionFactory` classe seguente implementa un `LiveAction` che registra i messaggi sulle pagine di origine e di destinazione e copia la `cq:lastModifiedBy` proprietà dal nodo di origine al nodo di destinazione. Il nome dell&#39;azione live è `exampleLiveAction`.

1. In Esplora progetti Eclipse, fate clic con il pulsante destro del mouse sul `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` pacchetto e fate clic su **Nuovo** > **Classe**. Per **Nome**, immettere `ExampleLiveActionFactory` e fare clic su **Fine**.
1. Aprite il `ExampleLiveActionFactory.java` file, sostituite il contenuto con il seguente codice e salvate il file.

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

1. Utilizzando il terminale o la sessione di comando, cambiate la directory nella `MyLiveActionFactory` directory (la directory del progetto Maven). Quindi, digitate il comando seguente:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   Il file AEM `error.log` indica che il bundle è stato avviato.

   Ad esempio, [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Create the Example Rollout Configuration {#create-the-example-rollout-configuration}

Create la configurazione di rollout MSM che utilizza l&#39; `LiveActionFactory` oggetto creato:

1. Create e configurate una configurazione [Rollout con la procedura](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) standard e utilizzando le proprietà:

   * **Titolo**: Esempio di configurazione del rollout
   * **Nome**: examplerolloutconfig
   * **cq:trigger**: `publish`

### Aggiungere l&#39;azione Live alla configurazione rollout di esempio {#add-the-live-action-to-the-example-rollout-configuration}

Configurate la configurazione di rollout creata nella procedura precedente in modo che utilizzi la `ExampleLiveActionFactory` classe.

1. Aperto CRXDE Lite; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Crea il nodo seguente sotto `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Fate clic su **Salva tutto**.
1. Selezionate il `exampleLiveAction` nodo e aggiungete la seguente proprietà:

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

   Questa proprietà indica alla `ExampleLiveAction` classe che la `cq:LastModifiedBy` proprietà deve essere replicata dal nodo di origine a quello di destinazione.

1. Fate clic su **Salva tutto**.

### Creare la Live Copy {#create-the-live-copy}

[Create una copia](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) dal vivo della sezione inglese/prodotti del sito di riferimento We.Retail utilizzando la configurazione di rollout:

* **Origine**: `/content/we-retail/language-masters/en/products`

* **Configurazione** rollout: Esempio di configurazione del rollout

Attiva la pagina **Prodotti** (inglese) del ramo di origine e osserva i messaggi di registro generati dalla `LiveAction` classe:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Modifica dei nomi delle lingue e dei paesi predefiniti {#changing-language-names-and-default-countries}

AEM utilizza un set predefinito di codici lingua e paese.

* Il codice della lingua predefinita è il codice di due lettere minuscoli, come definito dallo standard ISO-639-1.
* Il codice del paese predefinito è il codice di due lettere minuscolo o superiore, come definito dallo standard ISO 3166.

MSM utilizza un elenco memorizzato di codici lingua e paese per determinare il nome del paese associato al nome della versione della lingua della pagina. Se necessario, potete modificare i seguenti aspetti dell’elenco:

* Titoli della lingua
* Nomi paese
* Paesi predefiniti per le lingue (per codici quali `en`, `de`ad esempio,

L&#39;elenco delle lingue è memorizzato sotto il `/libs/wcm/core/resources/languages` nodo. Ogni nodo figlio rappresenta una lingua o un paese della lingua:

* Il nome del nodo è il codice della lingua (ad esempio `en` o `de`) o il codice della lingua_paese (ad esempio `en_us` o `de_ch`).

* La `language` proprietà del nodo memorizza il nome completo della lingua per il codice.
* La `country` proprietà del nodo memorizza il nome completo del paese per il codice.
* Quando il nome del nodo è composto solo da un codice della lingua (ad esempio `en`), la proprietà country è `*`, e una `defaultCountry` proprietà aggiuntiva memorizza il codice del paese della lingua per indicare il paese da utilizzare.

![chlimage_1-76](assets/chlimage_1-76.png)

Per modificare le lingue:

1. Aprite CRXDE Lite nel browser Web; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Selezionate la `/apps` cartella e fate clic su **Crea**, quindi su **Crea cartella.**

   Denominate la nuova cartella `wcm`.

1. Ripetete il passaggio precedente per creare la struttura delle `/apps/wcm/core` cartelle. Create un nodo di tipo `sling:Folder` in `core` denominato `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. Fare clic con il pulsante destro del mouse sul `/libs/wcm/core/resources/languages` nodo e scegliere **Copia**.
1. Fare clic con il pulsante destro del mouse sulla `/apps/wcm/core/resources` cartella e scegliere **Incolla**. Modificate i nodi secondari come necessario.
1. Fate clic su **Salva tutto**.
1. Fare clic su **Strumenti**, **Operazioni** , quindi su Console **** Web. In questa console fate clic su **OSGi**, quindi su **Configuration**.
1. Individuare e fare clic su Gestione **lingua CQ WCM** Day e modificare il valore di Elenco **** lingue in `/apps/wcm/core/resources/languages`, quindi fare clic su **Salva**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

## Configurazione di blocchi MSM sulle proprietà della pagina (interfaccia touch) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Durante la creazione di una proprietà pagina personalizzata, potrebbe essere necessario considerare se la nuova proprietà deve essere idonea per il rollout in qualsiasi Live Copy.

Ad esempio, se vengono aggiunte due nuove proprietà di pagina:

* E-mail di contatto:

   * Questa proprietà non deve essere implementata, in quanto sarà diversa in ogni paese (o marchio, ecc.).

* Stile visivo chiave:

   * Il requisito del progetto è che questa proprietà venga implementata come (di solito) comune a tutti i paesi (o marchi, ecc.).

A questo punto è necessario assicurarsi che:

* E-mail di contatto:

   * è esclusa dalle proprietà di rollout; vedere [Esclusione di proprietà e tipi di nodo dalla sincronizzazione](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Stile visivo chiave:

   * Accertatevi di non poter modificare questa proprietà nell’interfaccia touch, a meno che l’ereditarietà non venga annullata, e di poter quindi ripristinare l’ereditarietà; questo è controllato facendo clic sui collegamenti a catena o a catena interrotta che vengono attivati per indicare lo stato della connessione.

Se una proprietà di pagina è soggetta al rollout e, di conseguenza, all’annullamento/ripristino dell’ereditarietà durante la modifica, è controllata dalla proprietà dialog:

* `cq-msm-lockable`

   * è applicabile agli elementi in una finestra di dialogo dell’interfaccia touch
   * crea il simbolo del collegamento a catena nella finestra di dialogo
   * consente la modifica solo se l&#39;ereditarietà viene annullata (il collegamento a catena non funziona)
   * si applica solo al primo livello figlio della risorsa
   * **Tipo**: `String`

   * **Valore**: detiene il nome dell’immobile in questione (ed è paragonabile al valore dell’immobile `name`; ad esempio, vedete
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Una volta `cq-msm-lockable` definita, l&#39;interruzione o la chiusura della catena interagisce con MSM nel modo seguente:

* if the value of `cq-msm-lockable` is:

   * **Relativo** (ad esempio `myProperty` o `./myProperty`)

      * aggiungerà e rimuoverà la proprietà da `cq:propertyInheritanceCancelled`.
   * **Assoluto** (ad es. `/image`)

      * spezzando la catena si annullerà l&#39;ereditarietà aggiungendo il `cq:LiveSyncCancelled` mixin `./image` e impostando `cq:isCancelledForChildren` su `true`.

      * la chiusura della catena ripristina l&#39;ereditarietà.


>[!NOTE]
>
>`cq-msm-lockable` si applica al primo livello figlio della risorsa da modificare e non funziona su antenati di livello più profondo, indipendentemente dal fatto che il valore sia definito come assoluto o relativo.

>[!NOTE]
>
>Quando riattivate l&#39;ereditarietà, la proprietà Live Copy page non viene sincronizzata automaticamente con la proprietà source. Se necessario, potete richiedere manualmente una sincronizzazione.
