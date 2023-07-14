---
title: Installazione server applicazioni
description: Scopri come installare Adobe Experience Manager con un server applicazioni.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Installazione server applicazioni{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` sono i tipi di file Adobe Experience Manager (AEM) rilasciati in. Questi formati sono sottoposti a un controllo di qualità che tiene conto dei livelli di supporto a cui l’Adobe si è impegnato.
>

Questa sezione spiega come installare Adobe Experience Manager (AEM) con un server applicazioni. Consulta la [Piattaforme supportate](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) per informazioni sui livelli di supporto specifici forniti per i singoli server applicazioni.

Vengono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8,5](#tomcat)

Per ulteriori informazioni sull&#39;installazione di applicazioni Web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la documentazione del server applicazioni appropriato.

>[!NOTE]
>
>Se utilizzi Dynamic Media in una distribuzione WAR, consulta [Documentazione di Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrizione generale {#general-description}

### Comportamento predefinito durante l’installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene distribuito come un singolo file .war.

Se implementato, si verifica quanto segue per impostazione predefinita:

* la modalità di esecuzione è `author`
* l’istanza (archivio, ambiente Felix OSGI, bundle e così via) è installata in `${user.dir}/crx-quickstart`dove `${user.dir}` è la directory di lavoro corrente, il percorso di crx-quickstart viene chiamato `sling.home`

* la directory principale del contesto è il nome del file .war, ad esempio : `aem-6`

#### Configurazione {#configuration}

È possibile modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione : configura `sling.run.modes` parametro in `WEB-INF/web.xml` file del file .war dell’AEM prima della distribuzione

* sling.home: configurare `sling.home` parametro in `WEB-INF/web.xml`file del file .war dell’AEM prima della distribuzione

* directory principale del contesto: rinominare il file war dell’AEM

#### Pubblica installazione {#publish-installation}

Per distribuire un’istanza Publish, devi impostare la modalità di esecuzione su Pubblica:

* Decomprimi il WEB-INF/web.xml dal file .war dell’AEM
* Cambia il parametro sling.run.modes in publish
* Ripristina il file web.xml nel file .war dell’AEM
* Distribuisci file .war AEM

#### Controllo dell’installazione {#installation-check}

Per verificare se è installato tutto, è possibile:

* coda `error.log`per verificare che tutto il contenuto sia installato
* guarda in `/system/console` che tutti i bundle siano installati

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

Prima di una distribuzione, leggi [Descrizione generale](#general-description) sopra.

**Preparazione server**

* Consenti alle intestazioni di autenticazione di base di passare:

   * Un modo per consentire all&#39;AEM di autenticare un utente consiste nel disabilitare la sicurezza amministrativa globale del server WebSphere®. A tale scopo, passare a Sicurezza -> Sicurezza globale e deselezionare la casella di controllo Abilita sicurezza amministrativa, salvare e riavviare il server.

* set `"JAVA_OPTS= -Xmx2048m"`
* Se si desidera installare AEM utilizzando la directory principale del contesto = /, modificare la directory principale del contesto dell&#39;applicazione Web predefinita esistente.

**Distribuire l’applicazione web AEM**

* Scarica file .war AEM
* Configurare le configurazioni in web.xml se necessario (vedi sopra nella Descrizione generale)

   * Decomprimi file WEB-INF/web.xml
   * cambiare il parametro sling.run.modes in publish
   * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario
   * Ripristina file web.xml

* Distribuisci file .war AEM

   * Scegli una directory principale di contesto (se desideri impostare le modalità di esecuzione sling, seleziona i passaggi dettagliati della procedura guidata di distribuzione, quindi specificala al passaggio 6 della procedura guidata)

* Avviare l’applicazione web AEM

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

Prima di una distribuzione, leggi [Descrizione generale](#general-description) sopra.

**Preparare il server JBoss®**

Impostare gli argomenti di memoria nel file conf (ad esempio, `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

Se si utilizza lo scanner di distribuzione per per installare l&#39;applicazione Web AEM, potrebbe essere opportuno aumentare il `deployment-timeout,` per il set a `deployment-timeout` nel file xml dell&#39;istanza (ad es. `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Distribuire l’applicazione web AEM**

* Carica l’applicazione web AEM nella console di amministrazione JBoss®.

* Abilita l’applicazione web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Prima di una distribuzione, leggi [Descrizione generale](#general-description) sopra.

Questo utilizza un layout server semplice con un solo server amministratore.

**Preparazione server WebLogic**

* In entrata `${myDomain}/config/config.xml`aggiungi alla sezione configurazione protezione:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` vedi su [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) per la posizione corretta (per impostazione predefinita, posizionarlo alla fine della sezione è ok)

* Aumentare le impostazioni della memoria VM:

   * apri `${myDomain}/bin/setDomainEnv.cmd` (resp .sh) cerca WLS_MEM_ARGS, impostato, ad esempio, set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * riavviare il server WebLogic

* Crea in `${myDomain}` una cartella di pacchetti e all’interno di una cartella cq e in essa una cartella Plan

**Distribuire l’applicazione web AEM**

* Scarica file .war AEM
* Metti il file di guerra dell&#39;AEM in ${myDomain}cartella /packages/cq
* Configurare in `WEB-INF/web.xml` se necessario (vedi sopra nella Descrizione generale)

   * Decomprimi `WEB-INF/web.xml`file
   * cambiare il parametro sling.run.modes in publish
   * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario (vedi Descrizione generale)
   * Ripristina file web.xml

* Distribuire il file .war dell&#39;AEM come applicazione (per le altre impostazioni utilizzare le impostazioni predefinite)
* L&#39;installazione può richiedere tempo...
* Verifica che l’installazione sia stata completata come indicato in precedenza nella Descrizione generale (ad esempio, coda del file error.log).
* È possibile modificare la directory principale del contesto nella scheda Configurazione dell’applicazione web in WebLogic `/console`

#### Tomcat 8/8,5 {#tomcat}

Prima di una distribuzione, leggi [Descrizione generale](#general-description) sopra.

* **Prepara server Tomcat**

   * Aumentare le impostazioni della memoria VM:

      * In entrata `bin/catalina.bat` (resp `catalina.sh` in UNIX®) aggiungere la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat consente l&#39;accesso non amministratore o manager al momento dell&#39;installazione. Pertanto, devi modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso a questi account:

      * Modifica `tomcat-users.xml` per includere l’accesso per amministratore e manager. La configurazione deve essere simile al seguente esempio:

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

     e aumentare le dimensioni massime dei file e delle richieste ad almeno 500 MB, vedere quanto segue `multipart-config` esempio di tale `web.xml` file.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Distribuire l’applicazione web AEM**

   * Scarica file .war AEM
   * Configurare le configurazioni in web.xml se necessario (vedi sopra nella Descrizione generale)

      * Decomprimi file WEB-INF/web.xml
      * cambiare il parametro sling.run.modes in publish
      * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario
      * Ripristina file web.xml

   * Rinomina il file .war dell’AEM in ROOT.war se desideri distribuirlo come web app principale, rinominalo ad esempio aemauthor.war se desideri avere aemauthor come directory principale del contesto
   * copiarlo nella cartella webapps di tomcat
   * attendi l’installazione di AEM

## Risoluzione dei problemi {#troubleshooting}

Per informazioni su come risolvere i problemi che possono verificarsi durante l&#39;installazione, vedere:

* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
