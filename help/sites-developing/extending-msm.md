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
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 2%

---

# Estensione di Multi Site Manager{#extending-the-multi-site-manager}

Questa pagina consente di estendere le funzionalità di Multi Site Manager:

* Scopri i membri principali dell’API Java MSM.
* Crea una nuova azione di sincronizzazione che può essere utilizzata in una configurazione di rollout.
* Modificare la lingua e i codici paese predefiniti.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Questa pagina deve essere letta insieme a [Riutilizzo del contenuto: Multi Site Manager](/help/sites-administering/msm.md).
>
>Potrebbero interessare anche le seguenti sezioni della ristrutturazione dell’archivio siti nella AEM 6.4:
>* [Configurazioni blueprint di Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [Configurazioni di rollout di Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>Multi Site Manager e le relative API vengono utilizzate per la creazione di siti web, quindi sono destinate solo all’utilizzo in un ambiente di authoring.

## Panoramica dell’API Java {#overview-of-the-java-api}

Multi Site Management è costituito dai seguenti pacchetti:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

I principali oggetti API MSM interagiscono come segue (vedi anche [Termini utilizzati](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   Una `Blueprint` (come in [configurazione blueprint](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) specifica le pagine da cui una Live Copy può ereditare il contenuto.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * L’utilizzo di una configurazione blueprint ( `Blueprint`) è facoltativo, ma:

      * Consente all’autore di utilizzare l’opzione **Rollout** sull’origine (per inviare in modo esplicito le modifiche alle Live Copy che ereditano da questa origine).
      * Consente all&#39;autore di utilizzare **Crea sito**; questo consente all’utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
      * Definisce la configurazione di rollout predefinita per tutte le Live Copy risultanti.

* **`LiveRelationship`**

   Il parametro `LiveRelationship` specifica la connessione (relazione) tra una risorsa nel ramo Live Copy e la relativa risorsa sorgente/blueprint equivalente.

   * Le relazioni vengono utilizzate per la realizzazione dell’ereditarietà e del rollout.
   * `LiveRelationship` Gli oggetti forniscono l’accesso (riferimenti) alle configurazioni di rollout (  `RolloutConfig`),  `LiveCopy` e  `LiveStatus` agli oggetti correlati alla relazione.

   * Ad esempio, una Live Copy viene creata in `/content/copy/us` dall’origine/blueprint in `/content/we-retail/language-masters`. Le risorse `/content/we.retail/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` formano una relazione.

* **`LiveCopy`**

   `LiveCopy` contiene i dettagli di configurazione delle relazioni (  `LiveRelationship`) tra le risorse Live Copy e le relative risorse di origine/blueprint.

   * Utilizza la classe `LiveCopy` per accedere al percorso della pagina, al percorso della pagina sorgente/blueprint, alle configurazioni di rollout e al fatto che anche le pagine figlie siano incluse nel percorso `LiveCopy`.

   * Un nodo `LiveCopy` viene creato ogni volta che si utilizza **Crea sito** o **Crea Live Copy**.

* **`LiveStatus`**

   `LiveStatus` Gli oggetti forniscono l&#39;accesso allo stato di runtime di un  `LiveRelationship`. Utilizza per eseguire una query sullo stato di sincronizzazione di una Live Copy.

* **`LiveAction`**

   Un `LiveAction` è un&#39;azione eseguita su ogni risorsa coinvolta nel rollout.

   * Le LiveActions sono generate solo da RolloutConfigs.

* **`LiveActionFactory`**

   Crea oggetti `LiveAction` in base a una configurazione `LiveAction`. Le configurazioni vengono memorizzate come risorse nell’archivio.

* **`RolloutConfig`**

   Il `RolloutConfig` contiene un elenco di `LiveActions` da utilizzare quando viene attivato. Il `LiveCopy` eredita il `RolloutConfig` e il risultato è presente nel `LiveRelationship`.

   * L&#39;impostazione di una Live Copy per la prima volta utilizza anche un RolloutConfig (che attiva le LiveActions).

## Creazione di una nuova azione di sincronizzazione {#creating-a-new-synchronization-action}

Crea azioni di sincronizzazione personalizzate da utilizzare con le configurazioni di rollout. Crea un&#39;azione di sincronizzazione quando le [azioni installate](/help/sites-administering/msm-sync.md#installed-synchronization-actions) non soddisfano i requisiti specifici dell&#39;applicazione. Per eseguire questa operazione, creare due classi:

* Implementazione dell&#39;interfaccia [ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) che esegue l&#39;azione.
* Componente OSGI che implementa l&#39;interfaccia [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) e crea istanze della classe `LiveAction`.

Il `LiveActionFactory` crea istanze della classe `LiveAction` per una determinata configurazione:

* `LiveAction` le classi includono i metodi seguenti:

   * `getName`: Restituisce il nome dell&#39;azione Il nome viene utilizzato per fare riferimento all&#39;azione, ad esempio nelle configurazioni di rollout.
   * `execute`: Esegue le attività dell&#39;azione.

* `LiveActionFactory` le classi includono i seguenti membri:

   * `LIVE_ACTION_NAME`: Un campo contenente il nome del associato  `LiveAction`. Questo nome deve coincidere con il valore restituito dal metodo `getName` della classe `LiveAction`.

   * `createAction`: Crea un&#39;istanza del  `LiveAction`. Il parametro opzionale `Resource` può essere utilizzato per fornire informazioni sulla configurazione.

   * `createsAction`: Restituisce il nome del associato  `LiveAction`.

### Accesso al nodo di configurazione LiveAction {#accessing-the-liveaction-configuration-node}

Utilizza il nodo di configurazione `LiveAction` nell&#39;archivio per memorizzare informazioni che influiscono sul comportamento di runtime dell&#39;istanza `LiveAction`. Il nodo nell&#39;archivio che memorizza la configurazione `LiveAction` è disponibile per l&#39;oggetto `LiveActionFactory` in fase di esecuzione. Pertanto, puoi aggiungere proprietà al nodo di configurazione a e utilizzarle nell&#39;implementazione `LiveActionFactory` in base alle esigenze.

Ad esempio, un `LiveAction` deve memorizzare il nome dell’autore della blueprint. Una proprietà del nodo di configurazione include il nome della proprietà della pagina blueprint che memorizza le informazioni. In fase di esecuzione, il `LiveAction` recupera il nome della proprietà dalla configurazione, quindi ottiene il valore della proprietà.

Il parametro del metodo ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` è un oggetto `Resource`. Questo oggetto `Resource` rappresenta il nodo `cq:LiveSyncAction` per questa azione live nella configurazione di rollout; consulta [Creazione di una configurazione di rollout](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). Come di consueto, quando utilizzi un nodo di configurazione, devi adattarlo a un oggetto `ValueMap` :

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

### Accesso ai nodi di Target, ai nodi sorgente e alla LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

I seguenti oggetti vengono forniti come parametri del metodo `execute` dell&#39;oggetto `LiveAction` :

* Un oggetto [ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) che rappresenta l&#39;origine della Live Copy.
* Un oggetto `Resource` che rappresenta la destinazione della Live Copy.
* L&#39;oggetto [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) per la Live Copy.
* Il valore `autoSave` indica se `LiveAction` deve salvare le modifiche apportate al repository.

* Il valore di reset indica la modalità di ripristino del rollout.

Da questi oggetti è possibile ottenere tutte le informazioni sul `LiveCopy`. È inoltre possibile utilizzare gli oggetti `Resource` per ottenere gli oggetti `ResourceResolver`, `Session` e `Node`. Questi oggetti sono utili per manipolare il contenuto dell’archivio:

Nella prima riga del codice seguente, source è l&#39;oggetto `Resource` della pagina di origine:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Gli argomenti `Resource` possono essere oggetti `null` o `Resources` che non si adattano agli oggetti `Node`, ad esempio oggetti [ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html).

## Creazione di una nuova configurazione di rollout {#creating-a-new-rollout-configuration}

Crea una configurazione di rollout quando le configurazioni di rollout installate non soddisfano i requisiti dell&#39;applicazione:

* [Crea la configurazione di rollout](#create-the-rollout-configuration).
* [Aggiungi le azioni di sincronizzazione alla configurazione di rollout](#add-synchronization-actions-to-the-rollout-configuration).

La nuova configurazione di rollout è quindi disponibile quando imposti le configurazioni di rollout su una pagina blueprint o Live Copy.

>[!NOTE]
>
>Vedi anche le [best practice per personalizzare i rollout](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Creare la configurazione di rollout {#create-the-rollout-configuration}

Per creare una nuova configurazione di rollout:

1. CRXDE Lite aperto; ad esempio:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Accedi a :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Questa è la versione personalizzata del progetto di:
   >`/libs/msm/wcm/rolloutconfigs`
   >Deve essere creato se si tratta della prima configurazione.

   >[!NOTE]
   >
   >Non devi modificare nulla nel percorso /libs.
   >Questo perché il contenuto di /libs viene sovrascritto la prossima volta che aggiorni l&#39;istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >* Ricrea l&#39;elemento richiesto (cioè come esiste in /libs) sotto /apps
   >* Apporta modifiche a /apps


1. Sotto questo **Crea** un nodo con le seguenti proprietà:

   * **Nome**: Nome del nodo della configurazione di rollout. md#install-sync-actions), ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Aggiungi le seguenti proprietà a questo nodo:
   * **Nome**: `jcr:title`

      **Tipo**: `String`
      **Valore**: Titolo di identificazione che verrà visualizzato nell’interfaccia utente.
   * **Nome**: `jcr:description`

      **Tipo**: `String`
      **Valore**: Una descrizione facoltativa.
   * **Nome**: `cq:trigger`

      **Tipo**: `String`
      **Valore**: Attivazione  [di rollout ](/help/sites-administering/msm-sync.md#rollout-triggers) da utilizzare. Seleziona da:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Fare clic su **Salva tutto**.

### Aggiungere azioni di sincronizzazione alla configurazione del rollout {#add-synchronization-actions-to-the-rollout-configuration}

Le configurazioni di rollout sono memorizzate sotto il nodo di configurazione di rollout ](#create-the-rollout-configuration) creato sotto il nodo `/apps/msm/<your-project>/rolloutconfigs`.[

Aggiungi nodi figlio di tipo `cq:LiveSyncAction` per aggiungere azioni di sincronizzazione alla configurazione di rollout. L’ordine dei nodi di azione di sincronizzazione determina l’ordine in cui si verificano le azioni.

1. Sempre in CRXDE Lite, seleziona il nodo [Rollout configurazione](#create-the-rollout-configuration).

   Esempio:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **** Crea un nodo con le seguenti proprietà del nodo:

   * **Nome**: Nome del nodo dell&#39;azione di sincronizzazione.
Il nome deve essere lo stesso di **Nome azione** nella tabella in [Azioni di sincronizzazione](/help/sites-administering/msm-sync.md#installed-synchronization-actions), ad esempio `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Aggiungi e configura tutti i nodi di azione di sincronizzazione necessari. Ridisponi i nodi di azione in modo che il loro ordine corrisponda all’ordine in cui desideri che si verifichino. Il nodo di azione più in alto si verifica per primo.

## Creazione e utilizzo di una semplice classe LiveActionFactory {#creating-and-using-a-simple-liveactionfactory-class}

Segui le procedure descritte in questa sezione per sviluppare un `LiveActionFactory` e utilizzarlo in una configurazione di rollout. Le procedure utilizzano Maven e Eclipse per sviluppare e distribuire `LiveActionFactory`:

1. [Crea il ](#create-the-maven-project) progetto Maven e importalo in Eclipse.
1. [Aggiungi le dipendenze ](#add-dependencies-to-the-pom-file) al file POM.
1. [Implementa l’ `LiveActionFactory` ](#implement-liveactionfactory) interfaccia e implementa il bundle OSGi.
1. [Crea la configurazione di rollout](#create-the-example-rollout-configuration).
1. [Crea la Live Copy](#create-the-live-copy).

Il progetto Maven e il codice sorgente della classe Java sono disponibili nell’archivio Git pubblico.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto experiencemanager-java-msmrollout su GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Crea progetto Maven {#create-the-maven-project}

La procedura seguente richiede l’aggiunta del profilo adobe-public al file delle impostazioni Maven.

* Per informazioni sul profilo pubblico adobe, consulta [Ottenere il plug-in Maven del pacchetto di contenuti](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Per informazioni sul file delle impostazioni Maven, consulta Maven [Settings Reference](https://maven.apache.org/settings.html) (Riferimento impostazioni Maven).

1. Apri un terminale o una sessione della riga di comando e modifica la directory in modo che punti alla posizione in cui creare il progetto.
1. Immetti il seguente comando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Al prompt interattivo, specifica i seguenti valori:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. Avvia Eclipse e [importa il progetto Maven](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Aggiungi dipendenze al file POM {#add-dependencies-to-the-pom-file}

Aggiungi le dipendenze in modo che il compilatore Eclipse possa fare riferimento alle classi utilizzate nel codice `LiveActionFactory`.

1. In Esplora progetti Eclipse, apri il file:

   `MyLiveActionFactory/pom.xml`

1. Nell’editor, fai clic sulla scheda `pom.xml` e individua la sezione `project/dependencyManagement/dependencies` .
1. Aggiungi il seguente XML all&#39;interno dell&#39;elemento `dependencyManagement` e salva il file.

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

1. Apri il file POM per il bundle da **Project Explorer** in `MyLiveActionFactory-bundle/pom.xml`.
1. Nell’editor, fai clic sulla scheda `pom.xml` e individua la sezione progetto/dipendenze . Aggiungi il seguente XML all’interno dell’elemento dipendenze, quindi salva il file:

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

La seguente classe `LiveActionFactory` implementa un `LiveAction` che registra i messaggi relativi alle pagine di origine e di destinazione e copia la proprietà `cq:lastModifiedBy` dal nodo di origine al nodo di destinazione. Il nome dell’azione live è `exampleLiveAction`.

1. In Esplora progetti Eclipse, fai clic con il pulsante destro del mouse sul pacchetto `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` e fai clic su **Nuovo** > **Classe**. Per il **Nome**, immetti `ExampleLiveActionFactory`, quindi fai clic su **Fine**.
1. Apri il file `ExampleLiveActionFactory.java`, sostituisci il contenuto con il codice seguente e salva il file .

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

1. Utilizzando il terminale o la sessione di comando, cambia la directory nella directory `MyLiveActionFactory` (la directory di progetto Maven). Quindi, immetti il comando seguente:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   Il file AEM `error.log` deve indicare che il bundle è avviato.

   Ad esempio, [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creare la configurazione di rollout di esempio {#create-the-example-rollout-configuration}

Crea la configurazione di rollout MSM che utilizza la `LiveActionFactory` creata:

1. Crea e configura una [Configurazione di rollout con la procedura standard](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) e utilizzando le proprietà:

   * **Titolo**: Esempio di configurazione del rollout
   * **Nome**: examplerolloutconfig
   * **cq:trigger**:  `publish`

### Aggiungi l’azione live alla configurazione di rollout di esempio {#add-the-live-action-to-the-example-rollout-configuration}

Configura la configurazione di rollout creata nella procedura precedente in modo che utilizzi la classe `ExampleLiveActionFactory` .

1. CRXDE Lite aperto; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Crea il seguente nodo sotto `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Fare clic su **Salva tutto**.
1. Seleziona il nodo `exampleLiveAction` e aggiungi la seguente proprietà:

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valore**:  `true`

   Questa proprietà indica alla classe `ExampleLiveAction` che la proprietà `cq:LastModifiedBy` deve essere replicata dall&#39;origine al nodo di destinazione.

1. Fare clic su **Salva tutto**.

### Creare la Live Copy {#create-the-live-copy}

[Crea una Live ](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) Copy del ramo Inglese/Prodotti del sito di riferimento We.Retail utilizzando la configurazione di rollout:

* **Origine**:  `/content/we-retail/language-masters/en/products`

* **Configurazione** rollout: Esempio di configurazione del rollout

Attiva la pagina **Prodotti** (inglese) del ramo di origine e osserva i messaggi di log generati dalla classe `LiveAction`:

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

* Il codice della lingua predefinito è il codice a due lettere minuscolo come definito dallo standard ISO-639-1.
* Il codice del paese predefinito è il codice a due lettere minuscolo o superiore, come definito dalla norma ISO 3166.

MSM utilizza un elenco memorizzato di codici lingua e paese per determinare il nome del paese associato al nome della versione della lingua della pagina. Se necessario, è possibile modificare i seguenti aspetti dell’elenco:

* Titoli in lingua
* Nomi dei paesi
* Paesi predefiniti per le lingue (per codici quali `en`, `de`, tra gli altri)

L&#39;elenco delle lingue viene memorizzato sotto il nodo `/libs/wcm/core/resources/languages`. Ogni nodo figlio rappresenta una lingua o un paese della lingua:

* Il nome del nodo è il codice della lingua (ad esempio `en` o `de`), o il codice della lingua_del paese (ad esempio `en_us` o `de_ch`).

* La proprietà `language` del nodo memorizza il nome completo della lingua per il codice.
* La proprietà `country` del nodo memorizza il nome completo del paese per il codice.
* Quando il nome del nodo è costituito solo da un codice della lingua (ad esempio `en`), la proprietà del paese è `*` e una proprietà `defaultCountry` aggiuntiva memorizza il codice del paese della lingua per indicare il paese da utilizzare.

![chlimage_1-76](assets/chlimage_1-76.png)

Per modificare le lingue:

1. Apri CRXDE Lite nel browser Web; ad esempio, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Seleziona la cartella `/apps` e fai clic su **Crea**, quindi **Crea cartella.**

   Denomina la nuova cartella `wcm`.

1. Ripeti il passaggio precedente per creare la struttura ad albero delle cartelle `/apps/wcm/core`. Crea un nodo di tipo `sling:Folder` in `core` denominato `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. Fai clic con il pulsante destro del mouse sul nodo `/libs/wcm/core/resources/languages` e fai clic su **Copia**.
1. Fai clic con il pulsante destro del mouse sulla cartella `/apps/wcm/core/resources` e fai clic su **Incolla**. Modifica i nodi figlio come necessario.
1. Fare clic su **Salva tutto**.
1. Fare clic su **Strumenti**, **Operazioni**, quindi **Console web**. Da questa console fare clic su **OSGi**, quindi su **Configurazione**.
1. Individua e fai clic su **Day CQ WCM Language Manager** e modifica il valore di **Language List** in `/apps/wcm/core/resources/languages`, quindi fai clic su **Salva**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

## Configurazione dei blocchi MSM nelle proprietà di pagina (interfaccia touch) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Quando crei una proprietà pagina personalizzata, potrebbe essere necessario considerare se la nuova proprietà deve essere idonea per il rollout in qualsiasi Live Copy.

Ad esempio, se vengono aggiunte due nuove proprietà di pagina:

* E-mail di contatto:

   * Questa proprietà non deve essere implementata, in quanto sarà diversa in ogni paese (o marchio, ecc.).

* Stile visivo chiave:

   * Il requisito del progetto è che questa proprietà deve essere implementata così come è (di solito) comune a tutti i paesi (o marchi, ecc.).

Poi devi assicurarti che:

* E-mail di contatto:

   * è escluso dalle proprietà di rollout; vedere [Esclusione di proprietà e tipi di nodo dalla sincronizzazione](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Stile visivo chiave:

   * Assicurati di non poter modificare questa proprietà nell’interfaccia touch a meno che l’ereditarietà non venga annullata e di poter quindi ripristinare l’ereditarietà; questa opzione è controllata facendo clic sui collegamenti a catena o a catena interrotta che si attivano per indicare lo stato della connessione.

Il fatto che una proprietà di pagina sia soggetta a rollout e, quindi, soggetta a annullamento/ripristino dell’ereditarietà durante la modifica, sia controllata dalla proprietà di dialogo:

* `cq-msm-lockable`

   * è applicabile agli elementi in una finestra di dialogo dell’interfaccia touch
   * crea il simbolo di collegamento a catena nella finestra di dialogo
   * consente la modifica solo se l’ereditarietà viene annullata (il collegamento a catena è interrotto)
   * si applica solo al primo livello figlio della risorsa
   * **Tipo**: `String`

   * **Valore**: contiene il nome dell’immobile in questione (ed è comparabile al valore dell’immobile  `name`; ad esempio, vedi
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Quando `cq-msm-lockable` è stato definito, interrompere/chiudere la catena interagisce con MSM nel modo seguente:

* se il valore di `cq-msm-lockable` è:

   * **Relativo**  (ad esempio  `myProperty` o  `./myProperty`)

      * aggiungerà e rimuoverà la proprietà da `cq:propertyInheritanceCancelled`.
   * **Assoluto**  (ad es.  `/image`)

      * l’interruzione della catena annullerà l’ereditarietà aggiungendo il mixin `cq:LiveSyncCancelled` a `./image` e impostando `cq:isCancelledForChildren` su `true`.

      * la chiusura della catena ripristina l’ereditarietà.


>[!NOTE]
>
>`cq-msm-lockable` si applica al primo livello figlio della risorsa da modificare e non funziona su alcun predecessore di livello più profondo, indipendentemente dal fatto che il valore sia definito come assoluto o relativo.

>[!NOTE]
>
>Quando riattivi l’ereditarietà, la proprietà della pagina Live Copy non viene sincronizzata automaticamente con la proprietà sorgente. Se necessario, è possibile richiedere manualmente una sincronizzazione.
