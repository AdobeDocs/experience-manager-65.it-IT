---
title: Come creare progetti AEM con Apache Maven
seo-title: Come creare progetti AEM con Apache Maven
description: Questo documento descrive come impostare un progetto AEM basato su Apache Maven
seo-description: Questo documento descrive come impostare un progetto AEM basato su Apache Maven
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 3b64b1fe5d47f115681608f38e7e53d078c4698e
workflow-type: tm+mt
source-wordcount: '2424'
ht-degree: 0%

---


# Come creare progetti AEM con Apache Maven{#how-to-build-aem-projects-using-apache-maven}

## Panoramica {#overview}

Questo documento descrive come impostare un progetto AEM basato su [Apache Maven](https://maven.apache.org/).

Apache Maven è uno strumento open source per la gestione di progetti software automatizzando le build e fornendo informazioni di progetto di qualità. È lo strumento di gestione della build consigliato per i progetti AEM.

La creazione del progetto AEM basato su Maven offre diversi vantaggi:

* Un ambiente di sviluppo basato sull&#39;IDE
* Utilizzo di archetipi e artefatti del cielo forniti da Adobe
* Utilizzo dei set di strumenti Apache Sling e Apache Felix per le impostazioni di sviluppo basate su Maven
* Facilità di importazione in un IDE; ad esempio, Eclipse e/o IntelliJ
* Integrazione semplice con i sistemi di integrazione continua

### Archetipi di progetto Maven {#maven-project-archetypes}

Adobe fornisce due tipi di archetipo utilizzabili come base per i progetti AEM. Per maggiori informazioni, consulta i link seguenti:

* [archetipo progetto AEM](https://github.com/adobe/aem-project-archetype)
* [archetype Maven per il kit di avvio per applicazioni a pagina singola](https://github.com/adobe/aem-spa-project-archetype)

##  dipendenze API Experience Manager {#experience-manager-api-dependencies}

### Cos&#39;è UberJar? {#what-is-the-uberjar}

&quot;UberJar&quot; è il nome informale assegnato al file JAR (Java Archives) speciale fornito da Adobe. Questi file JAR contengono tutte le API Java pubbliche esposte da  Adobe Experience Manager. Sono incluse anche librerie esterne limitate, in particolare tutte le API pubbliche disponibili in AEM che provengono da Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava e due librerie utilizzate per l&#39;elaborazione delle immagini (la libreria CYMK JPEG ImageIO di Werner Randelshofer e la libreria delle immagini di dodici scimmie). UberJars contiene solo interfacce e classi API, il che significa che contengono solo interfacce e classi esportate da un bundle OSGi in AEM. Contengono anche un file *MANIFEST.MF* contenente le versioni corrette per l&#39;esportazione di pacchetti per tutti questi pacchetti esportati, garantendo così che i progetti creati con UberJar abbiano gli intervalli di importazione corretti.

### Perché Adobe ha creato gli UberJars? {#why-did-adobe-create-the-uberjars}

In passato, gli sviluppatori dovevano gestire un numero relativamente elevato di dipendenze individuali per diverse librerie AEM e, quando veniva utilizzata ogni nuova API, era necessario aggiungere al progetto una o più dipendenze singole. Su un progetto, l&#39;introduzione di UberJar causava la rimozione di 30 dipendenze separate dal progetto.

A partire da AEM 6.5, Adobe fornisce due UberJars: che include interfacce obsolete e una che rimuove quelle obsolete. Facendo riferimento esplicito a uno di essi al momento della creazione, i clienti sono certi di comprendere se hanno una dipendenza da codice obsoleto.

Il secondo Uber Jar elimina tutte le classi, i metodi e le proprietà obsoleti in modo che i clienti possano compilarli e capire se il codice personalizzato è a prova di futuro.

### Quale UberJar utilizzare? {#which-uberjar-to-use}

AEM 6.5 presenta due tipi di Uber Jar:

1. Uber Jar - Include solo le interfacce pubbliche non contrassegnate per la rimozione. Questo è l&#39;UberJar **consigliato** da utilizzare in quanto aiuta la base di codice a garantire il futuro facendo affidamento su API obsolete.
1. Uber Jar con API obsolete - Include tutte le interfacce pubbliche, incluse quelle contrassegnate per essere obsolete in una versione futura di AEM.

### Come si utilizzano gli UberJars? {#how-do-i-use-the-uberjars}

Se utilizzi Apache Maven come sistema di compilazione (come avviene per la maggior parte dei progetti AEM Java), dovrai aggiungere uno o due elementi al file *pom.xml* . Il primo è un elemento di *dipendenza* che aggiunge la dipendenza effettiva al progetto:

**Dipendenza Uber Jar *(senza API obsolete)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**Dipendenza Uber Jar con API obsolete**

>[!CAUTION]
>
>Adobe consiglia di implementare con Uber Jar che ***non* contiene le API obsolete per essere certi che le applicazioni verranno eseguite correttamente sulle versioni future di AEM.
>
>Utilizzate Uber Jar con supporto API obsoleto solo nel caso in cui il codice che si basa sulle API obsolete non possa essere modificato per tenere conto delle modifiche.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

Se la vostra azienda utilizza già un repository Manager di Maven come Sonype Nexus, Apache Archiva o JFrog Artifactory, aggiungete la configurazione appropriata al progetto per fare riferimento a questo repository manager e aggiungere l&#39;archivio di Adobe Maven ([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/)) al repository manager.

Se non si utilizza un repository manager, sarà necessario aggiungere un elemento *repository* al file *pom.xml* :

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### Cosa posso fare con UberJar? {#what-can-i-do-with-the-uberjar}

Con UberJar, puoi compilare il codice del progetto che dipende dalle API di AEM (e dalle API utilizzate dai progetti menzionati sopra). È inoltre possibile generare informazioni OSGi Service Component Runtime (SCR) e OSGi Mettype. Con alcune limitazioni, è anche possibile scrivere ed eseguire unit test.

### Cosa non posso fare con UberJar? {#what-can-t-i-do-with-the-uberjar}

Poiché UberJar contiene **solo** API, non è eseguibile e non può essere utilizzato per **eseguire**  Adobe Experience Manager. Per eseguire AEM, è necessario disporre del modulo AEM Quickstart, Standalone o Archivio applicazioni Web (WAR).

### Hai menzionato i limiti dei unit test. Per favore, spieghi di più. {#you-mentioned-limitations-on-unit-tests-please-explain-further}

I test di unità interagiscono generalmente con le API del prodotto in tre modi diversi, ciascuno dei quali ha un impatto leggermente diverso da UberJar.

#### Caso d’uso n. 1 - Codice personalizzato che richiama un’interfaccia API {#use-case-custom-code-which-calls-a-api-interface}

Questo caso, che è il più comune, include codice personalizzato che esegue metodi su un&#39;interfaccia Java definita dall&#39;API AEM. L&#39;implementazione di questa interfaccia può essere fornita direttamente o può essere iniettata utilizzando il pattern di iniezione dipendenza. **Questo caso di utilizzo può essere gestito con UberJar.**

Un esempio del primo sarebbe:

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

Un esempio di quest&#39;ultimo sarebbe:

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

Per eseguire il test unitario di uno di questi metodi, uno sviluppatore utilizza un framework di schermatura come [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/)o [Easymock](https://easymock.org/) per creare un oggetto fittizio per l&#39;API AEM a cui si fa riferimento. Questi esempi utilizzano JMockit, ma per questo caso specifico la differenza tra questi framework è in gran parte sintattica.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### Caso d’uso n. 2 - Codice personalizzato che richiama una classe di implementazione API {#use-case-custom-code-which-calls-an-api-implementation-class}

Questo caso d’uso prevede la chiamata a un metodo statico o di istanza di una classe nell’API AEM, in cui si fa riferimento a una classe concreta, anziché a un’interfaccia come nel caso d’uso n. 1.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**Questo caso di utilizzo può essere gestito con UberJar**. Tuttavia, è comunque consigliabile prendere in giro l&#39;API laddove possibile per i test eseguiti.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### Caso d’uso n. 3 - Codice personalizzato che estende una classe base dall’API {#use-case-custom-code-which-extends-a-base-class-from-the-api}

Come per la generazione SCR, se il codice estende una classe base (astratta o concreta) dall’API AEM, **dovete** utilizzare UberJar per testarla.

## Attività comuni di sviluppo con il cielo {#common-development-tasks-with-maven}

### Procedura per aggiungere percorsi al modulo contenuto {#how-to-add-paths-to-the-content-module}

Il modulo del contenuto contiene un file src/main/content/META-INF/vault/filter.xml che definisce i filtri per il pacchetto AEM creato da Maven. Il file creato dall&#39;archetipo di Maven è simile al seguente:

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Questo file viene utilizzato in diversi modi:

* mediante `content-package-maven-plugin` la quale determinare quale contenuto includere nel pacchetto
* mediante lo strumento VLT per determinare quali percorsi considerare
* se il pacchetto viene rigenerato in AEM Package Manager, vengono definiti anche i percorsi da includere

A seconda dei requisiti dell&#39;applicazione, potrebbe essere utile aggiungere a questi percorsi altri contenuti, ad esempio:

* Configurazioni rollout
* Blueprint
* Modelli flusso di lavoro
* Pagine di progettazione
* Contenuto di esempio

Per aggiungere altri `<filter>` elementi ai percorsi:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### Aggiunta di percorsi al pacchetto senza sincronizzarli {#adding-paths-to-the-package-without-syncing-them}

Se avete dei file che devono essere aggiunti al pacchetto creato dal plug-in content-package-maven-plug ma che non devono essere sincronizzati tra il file system e l&#39;archivio, potete usare `.vltignore` dei file. Questi file hanno la stessa sintassi dei file [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) .

Ad esempio, archetype utilizza un `.vltignore` file per impedire che il file JAR installato come parte del pacchetto venga sincronizzato nuovamente nel file system:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### Sincronizzazione dei percorsi senza aggiungerli al pacchetto {#syncing-paths-without-adding-them-to-the-package}

In alcuni casi, potrebbe essere utile mantenere specifici percorsi sincronizzati tra il file system e l&#39;archivio, ma non includerli nel pacchetto creato per essere installato in AEM.

Un caso tipico è il `/libs/foundation` percorso. A scopo di sviluppo, potrebbe essere necessario avere il contenuto di questo percorso disponibile nel file system, in modo che, ad esempio, l&#39;IDE possa risolvere le inclusioni JSP che includono JSP in `/libs`. Tuttavia, non desiderate includere tale parte nel pacchetto creato, in quanto la `/libs` parte contiene codice prodotto che non deve essere modificato dalle implementazioni personalizzate.

A questo scopo, potete fornire un file `src/main/content/META-INF/vault/filter-vlt.xml`. Se il file esiste, verrà utilizzato dallo strumento VLT, ad esempio quando si esegue `vlt up` e `vlt ci`, o quando si è impostata `vlt sync` la configurazione. Il content-package-maven-plugin continuerà a utilizzare il file `src/main/content/META-INF/vault/filter.xml` durante la creazione del pacchetto.

Ad esempio, per rendere `/libs/foundation` disponibile localmente per lo sviluppo, ma includerlo solo `/apps/myproject` nel pacchetto, utilizzate i due file seguenti.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Dovrete inoltre riconfigurare il maven-resources-plugin per non includere questi file nel pacchetto: il file filter.xml non viene applicato quando il pacchetto è installato, ma solo quando il pacchetto viene rigenerato utilizzando il gestore pacchetti.

Modificate di conseguenza la `<resources>` sezione nel contenuto del contenuto:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### How to Work with JSPs {#how-to-work-with-jsps}

La configurazione di Maven descritta finora crea un pacchetto di contenuti che può includere anche i componenti e i relativi JSP. Tuttavia, Maven li tratta come qualsiasi altro file che fa parte del pacchetto di contenuti e non li riconosce nemmeno come JSP.

I componenti risultanti funzionano allo stesso modo in AEM, ma rendere Maven consapevole dei JSP presenta due vantaggi principali

* consente a Maven di fallire se i JSP contengono errori, in modo che questi vengano visualizzati in fase di creazione e non quando vengono compilati per la prima volta in AEM
* Per gli IDE che possono importare progetti Maven, questo consente anche il completamento del codice e il supporto della libreria di tag nei JSP

Per abilitare questa configurazione, sono necessari due elementi:

1. aggiungere dipendenze tra librerie di tag
1. compilare i JSP come parte del processo di compilazione Maven

#### Aggiunta di dipendenze della libreria di tag {#adding-tag-library-dependencies}

Le dipendenze sotto devono essere aggiunte al POM del `content` modulo.

>[!NOTE]
>
>A meno che non importate le dipendenze di prodotto come descritto in [Importazione di dipendenze](#importingaemproductdependencies) di prodotti AEM, queste devono essere aggiunte al POM principale insieme alla versione che corrisponde alla configurazione di AEM, come descritto in [Aggiunta di dipendenze](#addingdependencies) sopra. I commenti in ciascuna voce di seguito mostrano il pacchetto da cercare in Dependency Finder.

>[!NOTE]
>
>L’ `com.adobe.granite.xssprotection` artefatto non è incluso nel POM delle dipendenze tra cq-quickstart e richiede le coordinate Maven complete come ottenuto dal Finder dipendenze.

#### Compilazione di JSP come parte della fase di compilazione del cielo {#compiling-jsps-as-part-of-the-maven-compile-phase}

Per compilare i JSP nella `compile` fase di Maven, utilizziamo il plug-in [JspC](https://sling.apache.org/documentation/development/jspc.html) Maven di Apache Sling come mostrato di seguito:

* abbiamo impostato un&#39;esecuzione per l&#39; `jspc` obiettivo (che per impostazione predefinita si collega alla `compile` fase, quindi non è necessario specificare la fase in modo esplicito)

* si consiglia di compilare eventuali JSP in `${project.build.directory}/jsps-to-compile`
* e restituisce il risultato a `${project.build.directory}/ignoredjspc` (che si traduce in `myproject/content/target/ignoredjspc`)

* abbiamo impostato maven-resources-plugin per copiare i JSP `${project.build.directory}/jsps-to-compile` nella fase di generazione delle fonti e configurarlo per non copiare la `libs/` cartella (perché si tratta del codice prodotto AEM e non vogliamo incorrere nelle dipendenze per la compilazione del nostro progetto, né dobbiamo convalidare la compilazione.

Il nostro obiettivo principale, come indicato sopra, è quello di convalidare le JSP e assicurarsi che il processo di creazione non riesca se contengono errori. Per questo li compiliamo in una directory separata che viene ignorata (e di fatto subito eliminata dopo, come vedrete in un minuto).

Il risultato del plug-in JspC Maven può anche essere incluso e distribuito come parte di un pacchetto OSGi, ma questo ha altre implicazioni ed effetti collaterali e va oltre il nostro obiettivo di convalidare i JSP.

Per ottenere l&#39;eliminazione delle classi compilate dai JSP, abbiamo impostato il Maven Clean Plugin come mostrato di seguito. Se si desidera ispezionare il risultato del plugin JspC Maven, eseguire `mvn compile` in `myproject/content` — dopo, si troverà il risultato in `myproject/content/target/ignoredjspc`).

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>A seconda che si faccia effettivamente uso del codice JSP in `/libs` (cioè includere JSP da lì), sarà necessario definire quali JSP vengono copiati per la compilazione.
>
>Ad esempio, se includete `/libs/foundation/global.jsp`, potete utilizzare la seguente configurazione per il `maven-resources-plugin` posto della configurazione sopra la quale saltare completamente `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### Come lavorare con i sistemi SCM {#how-to-work-with-scm-systems}

Quando lavorate con Gestione configurazione origine (SCM), accertatevi che

* La VCS ignora gli artefatti non sorgente nel file system
* VLT ignora gli artefatti del VCS e non li archivia nell&#39;archivio

>[!NOTE]
>
>Questa descrizione non copre come configurare Maven per lavorare con il vostro SCM, che è descritto in modo esaustivo nel riferimento [Maven POM e nella documentazione](https://maven.apache.org/pom.html#SCM) del [](https://maven.apache.org/scm/)Maven SCM Plugin.

#### Pattern da escludere da SCM {#patterns-to-exclude-from-scm}

Di seguito è riportato un elenco tipico di pattern da includere da SCM. Ad esempio, se utilizzi git, puoi aggiungerli al `.gitignore` file del progetto.

#### esempio .gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### Ignorare i file di controllo SCM in VLT {#ignoring-scm-control-files-in-vlt}

In alcuni casi, è possibile che nella struttura dell&#39;origine di contenuto siano presenti file di controllo SCM che non si desidera archiviare nella directory archivio.

Si consideri la situazione seguente:

archetype ha già creato un file .vltignore per impedire che il file Jar del bundle installato venga nuovamente sincronizzato nel file system:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

Ovviamente, non si desidera questo file neanche nel vostro SCM, quindi se ad esempio si sta utilizzando git, si aggiungerà un corrispondente . `gitignore` file:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

Come il . `gitignore` il file non deve entrare nella directory archivio, il . `vltignore` il file deve essere esteso per includere il . `gitignore` file:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### Procedura per l&#39;utilizzo dei profili di distribuzione {#how-to-work-with-deployment-profiles}

Se il processo di creazione fa parte di una configurazione di gestione del ciclo di vita per lo sviluppo più ampia, ad esempio un processo di integrazione continua, spesso è necessario eseguire l&#39;implementazione su altri computer, non solo sull&#39;istanza locale dello sviluppatore.

Per tali scenari, è possibile aggiungere facilmente nuovi profili [Maven Build](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) al POM del progetto.

Nell&#39;esempio seguente viene aggiunto un profilo `integrationServer`, che ridefinisce i nomi host e le porte per le istanze di creazione e pubblicazione. È possibile eseguire la distribuzione su questi server eseguendo il server dall&#39;elemento principale del progetto, come illustrato di seguito.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### Utilizzo dei AEM Communities {#how-to-work-with-aem-communities}

Quando si dispone di una licenza per la funzionalità AEM Communities, è necessario un&#39;ulteriore vasca API.

Per informazioni dettagliate, consultate [Utilizzo di Paradiso per le community](/help/communities/maven.md)
