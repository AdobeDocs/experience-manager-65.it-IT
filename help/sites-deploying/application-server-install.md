---
title: Installazione server applicazioni
description: Scopri come installare Adobe Experience Manager con un server applicazioni.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Installazione server applicazioni{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` sono i tipi di file Adobe Experience Manager (AEM) rilasciati in. Questi formati sono sottoposti a un controllo di qualità che tiene conto dei livelli di supporto a cui l’Adobe si è impegnato.
>

In questa sezione viene descritto come installare Adobe Experience Manager (AEM) con un server applicazioni. Consulta la sezione [Piattaforme supportate](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) per informazioni sui livelli di supporto specifici forniti per i singoli server applicazioni.

Vengono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8,5](#tomcat)

Per ulteriori informazioni sull&#39;installazione di applicazioni Web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la documentazione del server applicazioni appropriato.

>[!NOTE]
>
>Se utilizzi Dynamic Medie in una distribuzione WAR, consulta la [documentazione di Dynamic Medie](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrizione generale {#general-description}

### Comportamento predefinito durante l’installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene distribuito come un singolo file .war.

Se implementato, si verifica quanto segue per impostazione predefinita:

* la modalità di esecuzione è `author`
* l&#39;istanza (archivio, ambiente Felix OSGI, bundle e così via) è installata in `${user.dir}/crx-quickstart` dove `${user.dir}` è la directory di lavoro corrente, il percorso a crx-quickstart è denominato `sling.home`

* la radice del contesto è il nome del file .war, ad esempio `aem-6`

#### Configurazione {#configuration}

È possibile modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione : configura il parametro `sling.run.modes` nel file `WEB-INF/web.xml` del file .war AEM prima della distribuzione

* sling.home: configura il parametro `sling.home` nel file `WEB-INF/web.xml` del file .war dell&#39;AEM prima della distribuzione

* directory principale del contesto: rinominare il file war dell’AEM

#### Installazione di Publish {#publish-installation}

Per distribuire un’istanza Publish, devi impostare la modalità di esecuzione su Pubblica:

* Decomprimi il WEB-INF/web.xml dal file .war dell’AEM
* Cambia il parametro sling.run.modes in publish
* Ripristina il file web.xml nel file .war dell’AEM
* Distribuisci file .war AEM

#### Controllo dell’installazione {#installation-check}

Per verificare se è installato tutto, è possibile:

* coda il file `error.log` per verificare che tutto il contenuto sia installato
* verifica in `/system/console` che tutti i bundle siano installati

#### Due istanze sullo stesso server applicazioni {#two-instances-on-the-same-application-server}

A scopo dimostrativo, può essere opportuno installare l’istanza di authoring e pubblicazione in un server applicazioni. Per eseguire questa operazione:

1. Modifica le variabili sling.home e sling.run.modes dell’istanza Publish.
1. Decomprimi il file WEB-INF/web.xml dal file .war dell’AEM.
1. Modifica il parametro sling.home in un percorso diverso (sono possibili percorsi assoluti e relativi).
1. Modifica sling.run.modes per pubblicare l’istanza Publish.
1. Ripristina il file web.xml.
1. Rinominare i file di guerra in modo che abbiano nomi diversi. Ad esempio, uno rinomina aemauthor.war e l’altro in aempublish.war.
1. Usa impostazioni di memoria superiori. Ad esempio, le istanze AEM predefinite utilizzano `-Xmx3072m`
1. Distribuisci le due applicazioni web.
1. Dopo l’implementazione, arresta le due applicazioni web.
1. Sia nelle istanze di authoring che in quelle di pubblicazione, assicurati che nei file sling.properties la proprietà felix.service.urlhandlers=false sia impostata su false (per impostazione predefinita è impostata su true).
1. Avvia di nuovo le due applicazioni web.

## Procedure di installazione degli Application Server {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

**Preparazione server**

* Consenti alle intestazioni di autenticazione di base di passare:

   * Un modo per consentire all&#39;AEM di autenticare un utente consiste nel disabilitare la sicurezza amministrativa globale del server WebSphere®. A tale scopo, passare a Sicurezza > Sicurezza globale e deselezionare la casella di controllo Abilita sicurezza amministrativa, salvare e riavviare il server.

* imposta `"JAVA_OPTS= -Xmx2048m"`
* Se si desidera installare AEM utilizzando la directory principale del contesto = /, modificare la directory principale del contesto dell&#39;applicazione Web predefinita esistente.

**Distribuisci applicazione Web AEM**

* Scarica file .war AEM
* Configurare le configurazioni in web.xml se necessario (vedi sopra nella Descrizione generale)

   * Decomprimi file WEB-INF/web.xml
   * cambiare il parametro sling.run.modes in publish
   * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario
   * Ripristina file web.xml

* Distribuisci file .war AEM

   * Scegli una directory principale di contesto (per impostare le modalità di esecuzione sling, seleziona i passaggi dettagliati della procedura guidata di distribuzione, quindi specificala al passaggio 6 della procedura guidata).

* Avviare l’applicazione web AEM

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

**Prepara server JBoss®**

Impostare gli argomenti di memoria nel file conf (ad esempio, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Se si utilizza lo scanner di distribuzione per installare l&#39;applicazione Web AEM, potrebbe essere opportuno aumentare `deployment-timeout,` per tale impostazione di un attributo `deployment-timeout` nel file xml dell&#39;istanza (ad esempio, `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Distribuisci applicazione Web AEM**

* Carica l’applicazione web AEM nella console di amministrazione JBoss®.

* Abilita l’applicazione web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

Questo utilizza un layout server semplice con un solo server amministratore.

**Preparazione server WebLogic**

* In `${myDomain}/config/config.xml`aggiungi alla sezione di configurazione della protezione:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` vedere il [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) per la posizione corretta (per impostazione predefinita, la posizione alla fine della sezione è ok)

* Aumentare le impostazioni della memoria VM:

   * apri `${myDomain}/bin/setDomainEnv.cmd` (resp .sh) ricerca WLS_MEM_ARGS, impostato, ad esempio, impostato `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * riavviare il server WebLogic

* Creare in `${myDomain}` una cartella di pacchetti e all&#39;interno di una cartella cq e in essa una cartella Plan

**Distribuisci applicazione Web AEM**

* Scarica file .war AEM
* Inserisci il file .war dell&#39;AEM nella cartella ${myDomain}/packages/cq
* Configurare In `WEB-INF/web.xml` se necessario (vedi sopra nella Descrizione generale)

   * Decomprimi `WEB-INF/web.xml` file
   * cambiare il parametro sling.run.modes in publish
   * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario (vedi Descrizione generale)
   * Ripristina file web.xml

* Distribuire il file .war AEM come applicazione (per le altre impostazioni, utilizzare le impostazioni predefinite)
* L&#39;installazione può richiedere tempo...
* Verifica che l’installazione sia stata completata come indicato in precedenza nella Descrizione generale (ad esempio, coda del file error.log).
* È possibile modificare la directory principale del contesto nella scheda Configurazione dell&#39;applicazione Web in WebLogic `/console`

#### Tomcat 8/8,5 {#tomcat}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

* **Prepara server Tomcat**

   * Aumentare le impostazioni della memoria VM:

      * In `bin/catalina.bat` (resp `catalina.sh` su UNIX®) aggiungere la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat consente l&#39;accesso non amministratore o manager al momento dell&#39;installazione. Pertanto, è necessario modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso a questi account:

      * Modificare `tomcat-users.xml` per includere l&#39;accesso per l&#39;amministratore e il manager. La configurazione deve essere simile al seguente esempio:

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * Se desideri distribuire l’AEM con la directory principale del contesto &quot;/&quot;, devi modificare la directory principale del contesto dell’app web ROOT esistente:

      * Arresta e annulla la distribuzione di ROOT Web app
      * Rinomina cartella ROOT.war nella cartella webapps di tomcat
      * Avvia di nuovo l&#39;app Web

   * Se installi l’applicazione web AEM utilizzando il gestore-gui, devi aumentare le dimensioni massime di un file caricato, poiché l’impostazione predefinita consente solo 50 MB di dimensioni di caricamento. Per aprire il file web.xml dell’applicazione web manager,

     `webapps/manager/WEB-INF/web.xml`

     e aumentare le dimensioni max-file-size e max-request-size ad almeno 500 MB, vedi il seguente esempio `multipart-config` di un file `web.xml` di questo tipo.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Distribuisci applicazione Web AEM**

   * Scarica il file .war dell&#39;AEM.
   * Se necessario, effettua le configurazioni in web.xml (vedi sopra nella Descrizione generale).

      * Decomprimi il file WEB-INF/web.xml.
      * Modifica il parametro sling.run.modes in publish.
      * Rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario.
      * Ripristina il file web.xml.

   * Rinomina il file .war dell’AEM in ROOT.war se desideri distribuirlo come web app principale. Rinominalo in aemauthor.war se vuoi avere aemauthor come directory principale del contesto.
   * Copiatelo nella cartella Webapps di Tomcat.
   * Attendere l&#39;installazione dell&#39;AEM.

## Risoluzione dei problemi {#troubleshooting}

Per informazioni su come risolvere i problemi che possono verificarsi durante l&#39;installazione, vedere:

* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
