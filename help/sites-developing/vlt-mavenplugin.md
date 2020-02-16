---
title: Gestione dei pacchetti con il cielo
seo-title: Gestione dei pacchetti con il cielo
description: Utilizzate il plugin Content Package Maven per integrare le attività di gestione dei pacchetti nei vostri progetti Maven
seo-description: Utilizzate il plugin Content Package Maven per integrare le attività di gestione dei pacchetti nei vostri progetti Maven
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Gestione dei pacchetti con il cielo{#managing-packages-using-maven}

Utilizzate il plug-in Content Package Maven per integrare le attività di gestione dei pacchetti nei vostri progetti Maven. Gli obiettivi e i parametri del plug-in consentono di automatizzare molte delle attività che normalmente si eseguono utilizzando la pagina Gestione pacchetti o la riga di comando FileVault:

* Creare nuovi pacchetti da file nel file system.
* Installate e disinstallate i pacchetti sul server CRX o CQ.
* Creare pacchetti già definiti sul server.
* Ottenete un elenco dei pacchetti installati sul server.
* Rimuovete un pacchetto dal server.

## Aggiunta del plug-in Content Package Maven al file POM {#adding-the-content-package-maven-plugin-to-the-pom-file}

Per utilizzare il plug-in Content Package Maven, aggiungete il seguente elemento plug-in all’interno dell’elemento build del file POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Per consentire a Maven di scaricare il plug-in, utilizzate il profilo fornito nella sezione [Acquisizione del plug-in](#obtaining-the-content-package-maven-plugin) di Content Package Maven in questa pagina.

## Obiettivi del plug-in Content Package Maven {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri dell&#39;obiettivo forniti dal plug-in Content Package sono descritti nelle sezioni che seguono. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

**Prefisso plug-in**

Il prefisso del plug-in è content-package. Utilizzate questo prefisso per eseguire un obiettivo dalla riga di comando, come nell&#39;esempio seguente:

```shell
mvn content-package:build
```

**Prefisso parametro**

Salvo diversa indicazione, gli obiettivi e i parametri del plugin usano il prefisso vault, come nell&#39;esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**Proxy**

Gli obiettivi che utilizzano i proxy per il server CRX o CQ utilizzano la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Vedete il parametro useProxy nella sezione Impostazioni comuni.

### Parametri comuni {#common-parameters}

I parametri riportati nella tabella seguente sono comuni a tutti gli obiettivi, tranne se indicati nella colonna Obiettivi.

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obbligatorio</th>
   <th>Valore predefinito</th>
   <th>Descrizione</th>
   <th>Obiettivi</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>booleano</td>
   <td>No</td>
   <td>false</td>
   <td>Un valore di <code>true</code> causa il fallimento della build in caso di errore. Un valore di <code>false</code> fa sì che la build ignori l'errore.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>nome</td>
   <td>Stringa</td>
   <td>build: Sì<br /> , installazione: No<br /> rm:Yes</td>
   <td>Build: Nessuna impostazione predefinita.<br /> install: Il valore della proprietà artifactId del progetto Maven.</td>
   <td>Nome del pacchetto su cui agire.</td>
   <td>Tutti gli obiettivi tranne ls.</td>
  </tr>
  <tr>
   <td>password</td>
   <td>Stringa</td>
   <td>Sì</td>
   <td>admin</td>
   <td>La password utilizzata per l'autenticazione con il server CRX.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>Stringa</td>
   <td>No</td>
   <td></td>
   <td>L'ID server da cui recuperare il nome utente e la password per l'autenticazione.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>Stringa</td>
   <td>Sì</td>
   <td>http://localhost:4502/<br /> crx/packmgr/<br /> service.jsp</td>
   <td>L'URL dell'API del servizio HTTP del gestore pacchetti CRX.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>No</td>
   <td>5</td>
   <td>Timeout della connessione per la comunicazione con il servizio di gestione pacchetti, in secondi.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>booleano</td>
   <td>No</td>
   <td>vero</td>
   <td>Stabilisce se utilizzare le configurazioni proxy dal file delle impostazioni Maven. Un valore di <code>true</code> causa l'utilizzo della prima configurazione proxy attiva trovata per le richieste proxy al gestore pacchetti. Il valore false non causa l'utilizzo di alcun proxy.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>Stringa</td>
   <td>Sì</td>
   <td>admin</td>
   <td>Nome utente da autenticare con il server CRX.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>booleano</td>
   <td>No</td>
   <td>false</td>
   <td>Abilita o disabilita la registrazione dettagliata. Un valore di <code>true</code> abilita la registrazione dettagliata.</td>
   <td>Tutti gli obiettivi tranne il pacchetto.</td>
  </tr>
 </tbody>
</table>

### build {#build}

Crea un pacchetto di contenuti già definito in un’istanza di AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all&#39;interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l&#39;obiettivo di compilazione sono descritti nella sezione Parametri [](#common-parameters) comuni.

#### Esempio {#example}

Nell’esempio seguente viene creato il pacchetto workflow-fagioli installato nell’istanza AEM con l’indirizzo IP 10.36.79.223. L&#39;obiettivo viene eseguito utilizzando il seguente comando:

```shell
mvn content-package:build
```

Il seguente file POM si trova nella directory corrente dello strumento della riga di comando. Il POM specifica il nome del pacchetto e l’URL del servizio del pacchetto.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

Installa un pacchetto nel repository. L&#39;esecuzione di questo obiettivo non richiede un progetto Maven. L&#39;obiettivo è legato alla fase di installazione del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, vedete le descrizioni nella sezione Parametri [comuni](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obbligatorio</th>
   <th>Valore predefinito</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>manufatto</td>
   <td>Stringa</td>
   <td>No</td>
   <td> Il valore della proprietà artifactId del progetto Maven.</td>
   <td>Una stringa del modulo groupId:artifactId:version[:package].</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>Stringa</td>
   <td>No</td>
   <td></td>
   <td>ID dell'artifact da installare</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>Stringa</td>
   <td>No</td>
   <td></td>
   <td>Il groupId dell'artifact da installare</td>
  </tr>
  <tr>
   <td>install</td>
   <td>booleano</td>
   <td>No</td>
   <td>vero</td>
   <td>Determina se rimuovere automaticamente il pacchetto quando viene caricato. Il valore true decomprime il pacchetto e false non decomprime il pacchetto.</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artefatto. repository.<br /> ArtifactRepository</td>
   <td>No</td>
   <td>Il valore della variabile di sistema localRepository.</td>
   <td>Il repository locale di Maven. Impossibile configurare questo parametro con la configurazione del plug-in. La proprietà di sistema viene sempre utilizzata.</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>No</td>
   <td>Il manufatto principale definito per il progetto Maven.</td>
   <td>Il nome del file del pacchetto da installare.</td>
  </tr>
  <tr>
   <td>imballaggio</td>
   <td>Stringa</td>
   <td>No</td>
   <td>zip</td>
   <td>Tipo di imballaggio dell'artefatto da installare</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>Sì</td>
   <td>Il valore della proprietà remoteActiveRepositories definita per il progetto Maven.</td>
   <td>Impossibile configurare questo valore con la configurazione del plug-in. Il valore deve essere specificato nel progetto. </td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sì</td>
   <td>Progetto per il quale è configurato il plug-in.</td>
   <td>Il progetto Maven. Il progetto è implicito perché il progetto contiene la configurazione del plug-in.</td>
  </tr>
  <tr>
   <td>repositoryId <i>(POM)</i><br /> repoID <i>(riga di comando)</i></td>
   <td>Stringa</td>
   <td>No</td>
   <td>temp</td>
   <td>ID del repository da cui viene recuperato l'artifact. In un POM, utilizzare repositoryID. In una riga di comando, utilizzare repoID.</td>
  </tr>
  <tr>
   <td>repositoryUrl <i>(POM)</i><br /> repoURL <i>(riga di comando)</i></td>
   <td>Stringa</td>
   <td>No</td>
   <td></td>
   <td>URL del repository da cui viene recuperato l'artifact. In un POM, utilizzate repositoryURL. In una riga di comando, utilizzate repoURL.</td>
  </tr>
  <tr>
   <td>version</td>
   <td>Stringa</td>
   <td>No</td>
   <td></td>
   <td>Versione dell'artifact da installare.</td>
  </tr>
 </tbody>
</table>

#### Esempio {#example-1}

Nell&#39;esempio seguente viene creato un pacchetto contenente il pacchetto OSGi del flusso di lavoro (vedere l&#39;esempio per l&#39;obiettivo di [compilazione](#build) ) e quindi installato il pacchetto. Poiché l&#39;obiettivo di installazione è associato alla fase di installazione del pacchetto, il seguente comando esegue l&#39;obiettivo di installazione:

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

Elenca i pacchetti distribuiti in Gestione pacchetti.

#### Parametri {#parameters-2}

Tutti i parametri dell&#39;obiettivo ls sono descritti nella sezione Parametri [](#common-parameters) comuni.

#### Esempio {#example-2}

Nell’esempio seguente sono elencati i pacchetti installati nell’istanza di AEM con l’indirizzo IP 10.36.79.223. L&#39;obiettivo viene eseguito utilizzando il seguente comando:

```shell
mvn content-package:ls
```

Il seguente file POM si trova nella directory corrente dello strumento della riga di comando. Il POM specifica l’URL del servizio del pacchetto.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

Rimuove un pacchetto da Gestione pacchetti.

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nella sezione Parametri [](#common-parameters) comuni.

#### Esempio {#example-3}

Nell’esempio seguente viene rimosso il pacchetto workfow-mia installato nell’istanza AEM con l’indirizzo IP 10.36.79.223. L&#39;obiettivo viene eseguito utilizzando il seguente comando:

```shell
mvn content-package:rm
```

Il seguente file POM si trova nella directory corrente dello strumento della riga di comando. Il POM specifica l’URL del servizio pacchetto e il nome del pacchetto.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane sul server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nella sezione Parametri [](#common-parameters) comuni.

#### Esempio {#example-4}

L’esempio seguente disinstalla il pacchetto workflow-fagioli installato nell’istanza AEM con l’indirizzo IP 10.36.79.223. L&#39;obiettivo viene eseguito utilizzando il seguente comando:

```shell
mvn content-package:uninstall
```

Il seguente file POM si trova nella directory corrente dello strumento della riga di comando. Il POM specifica il nome del pacchetto e l’URL del servizio del pacchetto.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L&#39;esecuzione dell&#39;obiettivo del pacchetto richiede il completamento della fase di compilazione. L&#39;obiettivo del pacchetto è legato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, vedete la descrizione del `name` parametro nella sezione Parametri [comuni](#common-parameters) .

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Tipo</th>
   <th>Obbligatorio</th>
   <th>Valore predefinito</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> archiver.<br /> MavenArchiveConfiguration</td>
   <td>No</td>
   <td></td>
   <td>Configurazione dell'archivio da utilizzare. Consulta <a href="https://maven.apache.org/shared/maven-archiver/index.html">la documentazione per Maven Archiver</a>.</td>
  </tr>
  <tr>
   <td>buildContentDirectory</td>
   <td>java.io.File</td>
   <td>Sì</td>
   <td>Il valore della directory di output della build Maven.</td>
   <td>La directory che contiene il contenuto da includere nel pacchetto.</td>
  </tr>
  <tr>
   <td> dipendenze</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddeds</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>booleano</td>
   <td>Sì</td>
   <td>false</td>
   <td>Se si imposta il valore true, la build non riesce se non viene trovato un artifact incorporato nelle dipendenze del progetto. Un valore disattivato fa sì che la build ignori l'errore.</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>No</td>
   <td></td>
   <td>Un file che specifica l'origine del filtro dell'area di lavoro. I filtri specificati nella configurazione e iniettati tramite incorporamenti o pacchetti secondari vengono uniti al contenuto del file.</td>
  </tr>
  <tr>
   <td>filter</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>No</td>
   <td></td>
   <td>Contiene elementi di filtro che definiscono il contenuto del pacchetto. Una volta eseguiti, i filtri vengono inclusi nel file filter.xml. Vedere la sezione Utilizzo dei filtri di seguito.</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>Sì</td>
   <td>Il nome finale definito nel progetto Maven (fase di costruzione).</td>
   <td>Il nome del file ZIP del pacchetto generato, senza l'estensione .zip.</td>
  </tr>
  <tr>
   <td>gruppo</td>
   <td>java.lang.String</td>
   <td>Sì</td>
   <td>GroupID definito nel progetto Maven.</td>
   <td>Il groupId del pacchetto di contenuto generato. Questo valore fa parte del percorso di installazione di destinazione per il pacchetto di contenuti.</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>Sì</td>
   <td>La directory di compilazione definita nel progetto Maven.</td>
   <td>La directory locale in cui viene salvato il pacchetto di contenuto.</td>
  </tr>
  <tr>
   <td>prefix</td>
   <td>java.lang.String</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br /> project.MavenProject</td>
   <td>Sì</td>
   <td></td>
   <td>Il progetto Maven.</td>
  </tr>
  <tr>
   <td>proprietà</td>
   <td>java.util.Map</td>
   <td>No</td>
   <td></td>
   <td>Ulteriori proprietà che è possibile impostare nel file properties.xml. Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite:
    <ul>
     <li>group: Utilizzare il parametro group per impostare</li>
     <li>name: Utilizzate il parametro name per impostare</li>
     <li>version: Utilizzare il parametro version per impostare</li>
     <li>descrizione: Impostato dalla descrizione del progetto</li>
     <li>groupId: groupId del descrittore del progetto Maven</li>
     <li>artifactId: artifactId del descrittore del progetto Maven</li>
     <li>dipendenze: Utilizzare il parametro dipendenze per impostare</li>
     <li>createBy: Il valore della proprietà di sistema user.name</li>
     <li>create: Ora del sistema corrente</li>
     <li>requirementsRoot: Utilizzare il parametro requirementsRoot per impostare</li>
     <li>packagePath: Generazione automatica dal nome del gruppo e del pacchetto</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requirementsRoot</td>
   <td>booleano</td>
   <td>Sì</td>
   <td>false</td>
   <td>Definisce se il pacchetto richiede root. Questo diventerà la proprietà &lt;code&gt;requirementsRoot&lt;/code&gt; del file properties.xml.</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>No</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>Sì</td>
   <td>La versione definita nel progetto Maven</td>
   <td>Versione del pacchetto di contenuto.</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>Sì</td>
   <td>La directory definita nel progetto Maven (fase di costruzione).</td>
   <td>La directory che contiene il contenuto da includere nel pacchetto.</td>
  </tr>
 </tbody>
</table>

#### Utilizzo dei filtri {#using-filters}

Utilizzate l&#39;elemento filter per definire il contenuto del pacchetto. I filtri vengono aggiunti all&#39;elemento workspaceFilter nel `META-INF/vault/filter.xml` file del pacchetto.

L&#39;esempio di filtro seguente mostra la struttura XML da utilizzare:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**Modalità di importazione**

L&#39; `mode` elemento definisce in che modo il contenuto del repository viene interessato quando il pacchetto viene importato. È possibile utilizzare i seguenti valori:

* **** Unisci: Viene aggiunto il contenuto del pacchetto che non è già presente nella directory archivio. Il contenuto presente nel pacchetto e nell&#39;archivio rimane invariato. Nessun contenuto viene rimosso dalla directory archivio.
* **** Sostituisci: Il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto viene rimosso dalla directory archivio quando non esiste nel pacchetto.
* **** Aggiorna: Il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto esistente viene rimosso dalla directory archivio.

Se il filtro non contiene `mode` elementi, viene utilizzato il valore predefinito di `replace` .

#### Esempio {#example-5}

Nell&#39;esempio seguente viene creato un pacchetto che contiene il bundle OSGi di workflow-fagioli. Il file POM identifica la directory jcr_root come valore della proprietà buildContentDirectory. La directory jcr_root contiene il file JAR del bundle nella struttura di directory che riflette il repository:

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

Poiché l&#39;obiettivo è associato alla fase di creazione del pacchetto, il seguente comando esegue l&#39;obiettivo del pacchetto:

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

Invece di esprimere l&#39;obiettivo nella `package` sezione del plug-in `executions` , potete utilizzare `content-package` come valore dell&#39; `packaging` elemento di progetto:

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### aiuto {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| detail | booleano | No | false | Determina se visualizzare tutte le proprietà impostabili per ciascun obiettivo. Il valore true visualizza tutte le proprietà impostabili. |
| goal | Stringa | No |  | Nome dell&#39;obiettivo per il quale visualizzare l&#39;aiuto. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| indentSize | int | No | 2 | Il numero di spazi da utilizzare per il rientro di ciascun livello. Se si specifica un valore, il valore deve essere positivo. |
| lineLength | int | No | 80 | Lunghezza massima di una linea di visualizzazione. Se si specifica un valore, il valore deve essere positivo. |

## Come ottenere il plug-in Contenuti Package Maven {#obtaining-the-content-package-maven-plugin}

Il plug-in è disponibile nell&#39;archivio pubblico di Adobe. Per scaricare il plugin, aggiungete il seguente profilo Maven al file delle impostazioni Maven e attivatelo. Quando si utilizza un comando Maven, il plug-in viene scaricato nel repository locale, se necessario.

>[!NOTE]
>
>L’archivio delle versioni pubbliche di Adobe non è accessibile da browser, pertanto la navigazione all’URL dell’archivio tramite il browser Web genera un errore Non trovato. Tuttavia, Maven è in grado di accedere alle directory del repository.

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

## Incorporazione di pacchetti OSGi in un pacchetto di contenuti {#embedding-osgi-bundles-in-a-content-package}

Utilizzate il plug-in Content Package Maven per incorporare i bundle OSGi nel pacchetto di contenuti. Per incorporare il bundle, implementate le seguenti configurazioni:

* Il bundle deve essere dichiarato come una dipendenza dal progetto Maven.
* La configurazione del plug-in fa riferimento al bundle utilizzando il percorso desiderato del bundle nel pacchetto.

Nell’esempio seguente POM crea un pacchetto contenente il bundle Apache Sling JCR UserManager. Nel pacchetto, il bundle JAR si trova nella `jcr_root/apps/myapp/install` cartella:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## Inclusione di un&#39;immagine miniatura o di un file di proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituite i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includete una miniatura per distinguere il pacchetto in Gestione pacchetti e Condivisione pacchetti.

Nel pacchetto, i file specifici di FileVault si trovano nella cartella /META-INF/vault. I file sorgente possono trovarsi ovunque nel file system. Nel file POM, definite le risorse di build per copiare i file sorgente nel file target/vault-work/META-INF per l’inclusione nel pacchetto.

Il seguente codice POM aggiunge al pacchetto i file nella cartella META-INF dell’origine del progetto:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Il seguente codice POM aggiunge al pacchetto solo una miniatura. L’immagine in miniatura deve essere denominata thumbnail.png e deve trovarsi nella cartella META-INF/vault/definition del pacchetto. In questo esempio, il file di origine si trova nella cartella /src/main/content/META-INF/vault/definition del progetto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Utilizzo Dei Tipi Di Archivi Per Generare Progetti AEM {#using-archetypes-to-generate-aem-projects}

Numerosi archetipi Maven sono disponibili per la generazione di progetti AEM. Utilizzate l&#39;archetipo corrispondente ai vostri obiettivi di sviluppo:

* Un pacchetto di contenuti che installa le risorse per un’applicazione AEM: [simple-content-package-archetype](#simple-content-package-archetype)
* Un pacchetto di contenuti che include artefatti di terze parti: [simple-content-package-with-embedded-archetype](#simple-content-package-with-embedded-archetype).
* Applicazione multi-modulo che accompagna lo sviluppo di classi Java e unit test: [multimodulo-content-package-archetype](#multimodule-content-package-archetype).

>[!NOTE]
>
>Il progetto Apache Sling offre anche archetipi utili nello sviluppo di AEM. Questi sono documentati all&#39;indirizzo [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

Ogni tipo di archetipo genera i seguenti elementi:

* Struttura delle cartelle del progetto.
* File POM.
* FileVault di configurazione.

Gli artefatti Archetype sono disponibili nell&#39;archivio pubblico di Adobe Maven. Per scaricare ed eseguire un archetype, identificare l&#39;archetype e l&#39;archivio Adobe utilizzando i parametri del archetype Maven:generate command:

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Il plugin Maven archetype utilizza la modalità interattiva nella shell o nella riga di comando per raccogliere informazioni sul progetto. Le informazioni fornite vengono utilizzate per configurare diverse proprietà del progetto, come i nomi delle cartelle e gli ID degli artifact.

**File POM**

I file POM generati includono comandi per la compilazione del codice, la creazione dei bundle e la distribuzione in AEM nei pacchetti. Le `groupID`proprietà `artifactId`, `version`e `name` le proprietà del progetto Maven vengono popolate automaticamente utilizzando i valori forniti al prompt `archetype:generate` interattivo Maven.

Potreste voler modificare i seguenti valori predefiniti nel file pom.xml generato:

* Nome del server CQ o indirizzo IP: Il valore predefinito è `localhost`. L&#39; `crx.host` elemento seguente `project/properties` contiene questo valore.

* Numero di porta per il server CQ: Il valore predefinito è `4502`. L&#39; `crx.port` elemento seguente `project/properties` contiene questo valore.

* Versione del plug-in Content Package Maven: Utilizzate la versione più recente come contenuto dell&#39; `version` elemento per il plug-in con `artifactId` di `content-package-maven-plugin`. Il valore predefinito è `0.0.24`.

**Utilizzo degli archetipi**

1. In una finestra shell o in un prompt dei comandi, immettere il `archetype:generate` comando Paradiso. Quando richiesto, immettete i valori per i parametri rimanenti.

   Per informazioni su ciascun parametro, fare riferimento alla sezione relativa al tipo di archetipo utilizzato.

1. Usate un editor di testo per aprire il file pom.xml e modificare i valori predefiniti in base alle vostre esigenze.
1. Compilate le cartelle generate con le risorse.
1. Immettere il `mvn clean install` comando.

### simple-content-package-archetype {#simple-content-package-archetype}

Crea un progetto maven adatto all’installazione di risorse per una semplice applicazione AEM. La struttura delle cartelle è quella utilizzata sotto la `/apps` cartella dell’archivio AEM. Il POM definisce i comandi per creare pacchetti delle risorse inserite nelle cartelle e installare i pacchetti nell’istanza di AEM.

**Proprietà artefatto Archetype:**

* ID gruppo: `com.day.jcr.vault`
* ID artefatto: `simple-content-package-archetype`
* Versione: `1.0.2`
* Archivio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parametri Archetype:**

* groupId: GroupId del pacchetto di contenuto generato da Maven. Il valore viene utilizzato automaticamente nel file POM.
* artifactId: Nome del pacchetto di contenuti. Il valore viene utilizzato anche come nome della cartella del progetto.
* version:Versione del pacchetto di contenuto.
* pacchetto: Questo valore non viene utilizzato per il tipo semplice-content-package-archetype.
* appsFolderName: Nome della cartella sotto /apps.
* artifactName: Descrizione del pacchetto di contenuti.
* packageGroup: Nome del gruppo di pacchetti di contenuto. Questo valore configura il parametro del gruppo per l&#39;obiettivo Package del plug-in Content Package Maven.

**Struttura delle cartelle:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-embedded-archetype {#simple-content-package-with-embedded-archetype}

Esegue le stesse attività del tipo semplice-content-package-archetype, nonché i download e include un artefatto proveniente da un repository pubblico di Maven.

**Proprietà bundle Archetype:**

* ID gruppo: `com.day.jcr.vault`
* ID artefatto: `simple-content-package-with-embedded-archetype`
* Versione: `1.0.2`
* Archivio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parametri Archetype:**

* groupId: GroupId del pacchetto di contenuto generato da Maven. Il valore viene utilizzato automaticamente nel file POM.
* artifactId: Nome del pacchetto di contenuti. Il valore viene utilizzato anche come nome della cartella del progetto.
* version:Versione del pacchetto di contenuto.
* pacchetto: Parametro non utilizzato.
* appsFolderName: Nome della cartella sotto /apps.
* artifactName: Descrizione del pacchetto di contenuti.
* embeddedArtifactId: L&#39;ID dell&#39;artifact da incorporare nel pacchetto di contenuto.
* embeddedGroupId: L&#39;ID gruppo dell&#39;artifact da incorporare.
* embeddedVersion: Versione dell’artefatto da incorporare.
* packageGroup: Nome del gruppo di pacchetti di contenuto. Questo valore configura il parametro del gruppo per l&#39;obiettivo Package del plug-in Content Package Maven.

**Struttura delle cartelle:**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodulo-content-package-archetype {#multimodule-content-package-archetype}

Crea un progetto maven che include la struttura di cartelle per lo sviluppo di un’applicazione AEM e l’installazione di risorse sul server.

La `bundle` cartella contiene la struttura di cartelle in cui sono memorizzati i file sorgente Java e JUnit che vengono sviluppati. Il file pom.xml in questa cartella crea il bundle OSGi. I seguenti valori nel POM identificano l’artefatto e il bundle:

* artifactID: `${artifactID}-bundle`.
* Bundle-SymbolicName: `${groupId}.${artifactId}-bundle`.

`${artifactID}` e `${groupId}` sono i valori forniti per questi parametri durante l&#39;esecuzione degli archetipi.

La `content` cartella contiene le risorse installate nell’istanza AEM. Il valore di artifactID è `${artifactID}multimodule-bundle`.

La cartella principale contiene il POM principale che gestisce i plug-in e le dipendenze di Maven.

**Proprietà bundle Archetype:**

* ID gruppo: `com.day.jcr.vault`
* ID artefatto: `multimodule-content-package-archetype`
* Versione: `1.0.2`
* Archivio: `adobe-public-releases`

**Maven, comando:**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**Parametri Archetype:**

* groupId: GroupId del pacchetto di contenuto generato da Maven. Il valore viene utilizzato automaticamente nel file POM.
* artifactId: Nome del pacchetto di contenuti. Il valore viene utilizzato anche come nome della cartella del progetto.
* version:Versione del pacchetto di contenuto.
* pacchetto: Questo valore non viene utilizzato per multimodulo-content-package-archetype.
* appsFolderName: Nome della cartella sotto /apps.
* artifactName: Descrizione del pacchetto di contenuti.
* packageGroup: Nome del gruppo di pacchetti di contenuto. Questo valore configura il parametro del gruppo per l&#39;obiettivo Package del plug-in Content Package Maven.

**Struttura delle cartelle:**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

