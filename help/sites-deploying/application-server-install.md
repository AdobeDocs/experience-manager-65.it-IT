---
title: Installazione dell’applicazione da server
seo-title: Installazione dell’applicazione da server
description: Scoprite come installare AEM con un server applicazioni.
seo-description: Scoprite come installare AEM con un server applicazioni.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 0a082d3cff66b82ef6de551a735a16a001446a1e
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Installazione dell’applicazione da server{#application-server-install}

>[!NOTE]
>
>`JAR` e  `WAR` sono i tipi di file AEM vengono rilasciati in. Questi formati sono sottoposti a controllo qualità per soddisfare i livelli di supporto  Adobe si è impegnato a raggiungere.


In questa sezione viene illustrato come installare Adobe Experience Manager (AEM) con un server applicazioni. Consultare la sezione [Piattaforme supportate](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) per visualizzare i livelli di supporto specifici forniti per i singoli server delle applicazioni.

Sono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [ Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Per ulteriori informazioni sull&#39;installazione delle applicazioni Web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la relativa documentazione del server applicazione.

>[!NOTE]
>
>Se utilizzi contenuti multimediali dinamici in una distribuzione WAR, consulta la [documentazione relativa ai supporti dinamici](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrizione generale {#general-description}

### Comportamento predefinito durante l&#39;installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene fornito come un singolo file di guerra da distribuire.

Se distribuito, per impostazione predefinita si verifica quanto segue:

* la modalità di esecuzione è `author`
* l’istanza (repository, ambiente Felix OSGI, pacchetti, ecc.) è installato in `${user.dir}/crx-quickstart`dove `${user.dir}` è la directory di lavoro corrente, il percorso di crx-quickstart è denominato `sling.home`

* la radice del contesto è il nome del file di guerra, ad esempio: `aem-6`

#### Configurazione {#configuration}

Potete modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione: configurare il parametro `sling.run.modes` nel file `WEB-INF/web.xml` del file di AEM prima della distribuzione

* sling.home: configurare il parametro `sling.home` nel file `WEB-INF/web.xml`del file di AEM prima della distribuzione

* context root: rinominare il file AEM guerra

#### Installazione di pubblicazione {#publish-installation}

Per implementare un’istanza di pubblicazione è necessario impostare la modalità di esecuzione per la pubblicazione:

* Rimuovere il WEB-INF/web.xml dal file di guerra AEM
* Cambia il parametro sling.run.mode in pubblicazione
* Repack file web.xml in AEM file di guerra
* Distribuisci AEM file di guerra

#### Controllo installazione {#installation-check}

Per verificare se è installato tutto, è possibile:

* chiudere il file `error.log`per vedere che tutto il contenuto è installato
* verificare in `/system/console` che tutti i bundle siano installati

#### Due istanze sullo stesso server applicazione {#two-instances-on-the-same-application-server}

A scopo dimostrativo può essere opportuno installare l’istanza di creazione e pubblicazione in un unico server applicazione. Per farlo, effettuate le seguenti operazioni:

1. Modificate le variabili sling.home e sling.run.mode dell’istanza di pubblicazione.
1. Rimuovete il file WEB-INF/web.xml dal file di guerra AEM.
1. Modificate il parametro sling.home impostando un percorso diverso (sono possibili percorsi assoluti e relativi).
1. Modificate le modalità sling.run.mode per pubblicare l’istanza di pubblicazione.
1. Reimpacchettare il file web.xml.
1. Rinominare i file di guerra in modo che abbiano nomi diversi: Ad esempio, rinominate aemauthor.war e aempublish.war.
1. Utilizzate impostazioni di memoria più elevate, ad esempio per le istanze di AEM predefinite che utilizzano ad esempio: -Xmx3072m
1. Distribuire le due applicazioni Web.
1. Dopo la distribuzione, le due applicazioni Web vengono arrestate.
1. Sia nelle istanze di creazione che di pubblicazione verificare che nei file sling.properties la proprietà felix.service.urlhandlers=false sia impostata su false (l’impostazione predefinita è true).
1. Avviate di nuovo le due applicazioni Web.

## Procedure di installazione dei server applicazioni {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) precedente.

**Preparazione server**

* Lasciate passare le intestazioni di autenticazione di base:

   * Un modo per consentire AEM autenticare un utente è disabilitare la protezione amministrativa globale del server WebSphere, per eseguire questa operazione: andate a Protezione > Sicurezza globale e deselezionate la casella di controllo Abilita protezione amministrativa, salvate e riavviate il server.

* imposta `"JAVA_OPTS= -Xmx2048m"`
* Se si desidera installare AEM utilizzando context root = /, è prima necessario modificare il context root dell&#39;applicazione Web predefinita esistente

**Implementare AEM&#39;applicazione Web**

* Scarica AEM file di guerra
* Configurare le configurazioni In web.xml se necessario (vedere sopra nella Descrizione generale)

   * Scomprimi file WEB-INF/web.xml
   * modifica il parametro sling.run.mode da pubblicare
   * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come necessario
   * Reimballaggio del file web.xml

* Distribuisci AEM file di guerra

   * Scegliere una directory principale di contesto (se si desidera impostare le modalità di esecuzione sling, è necessario selezionare i passaggi dettagliati della procedura guidata di distribuzione, quindi specificarla nel passaggio 6 della procedura guidata)

* Avvia AEM applicazione Web

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) precedente.

**Preparazione del server JBoss**

Impostate gli argomenti di memoria nel file conf (ad es. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

se si utilizza lo scanner di distribuzione per installare l&#39;applicazione Web AEM, potrebbe essere utile aumentare l&#39;attributo `deployment-timeout,` per l&#39;impostazione di un attributo `deployment-timeout` nel file xml dell&#39;istanza (ad esempio `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implementare AEM&#39;applicazione Web**

* Caricate l’applicazione Web AEM nella console di amministrazione JBoss.

* Abilitare l&#39;applicazione Web AEM.

####  Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) precedente.

Questo utilizza un layout server semplice con un solo Admin Server.

**Preparazione server WebLogic**

* In `${myDomain}/config/config.xml`aggiungere alla sezione di configurazione della sicurezza:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` vedere su  [https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdper la posizione corretta (per impostazione predefinita, posizionarla alla fine della sezione è ok)

* Aumenta le impostazioni della memoria VM:

   * aprire `${myDomain}/bin/setDomainEnv.cmd` (risp.sh) la ricerca per WLS_MEM_ARGS, impostare ad esempio `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * riavvio del server WebLogic

* Crea in `${myDomain}` una cartella di pacchetti e all&#39;interno di una cartella cq e in una cartella Plan

**Implementare AEM&#39;applicazione Web**

* Scarica AEM file di guerra
* Inserire il file di guerra AEM nella cartella ${myDomain}/packages/cq
* Se necessario, eseguire le configurazioni in `WEB-INF/web.xml` (vedere sopra nella Descrizione generale)

   * Rimuovi `WEB-INF/web.xml`file
   * modifica il parametro sling.run.mode da pubblicare
   * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come desiderate (consultate Descrizione generale)
   * Reimballaggio del file web.xml

* Distribuire AEM file di guerra come applicazione (per le altre impostazioni utilizzare le impostazioni predefinite)
* L&#39;installazione può richiedere del tempo...
* Verificate che l&#39;installazione sia stata completata come indicato sopra nella Descrizione generale (ad es., il file error.log)
* È possibile modificare la radice del contesto nella scheda Configurazione dell&#39;applicazione Web in WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) precedente.

* **Prepara server Tomcat**

   * Aumenta le impostazioni della memoria VM:

      * In `bin/catalina.bat` (risp. `catalina.sh` su unix) aggiungere la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat non consente né l&#39;accesso dell&#39;amministratore né del manager all&#39;installazione. Pertanto è necessario modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso a questi account:

      * Modificate `tomcat-users.xml` per includere l&#39;accesso per l&#39;amministratore e il manager. La configurazione deve essere simile all&#39;esempio seguente:

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
   * Se desideri distribuire AEM con la radice contestuale &quot;/&quot;, devi modificare la radice contestuale dell&#39;app Web principale esistente:

      * Arrestare e annullare la distribuzione dell&#39;app Web ROOT
      * Rinominare la cartella ROOT.war nella cartella delle app Web di Tomcat
      * Avvia di nuovo l&#39;app Web
   * Se installate l&#39;applicazione Web AEM utilizzando manager-gui, dovete aumentare la dimensione massima di un file caricato, in quanto l&#39;impostazione predefinita consente solo 50 MB di caricamento. Per questo aprire il web.xml dell&#39;applicazione Web manager,

      `webapps/manager/WEB-INF/web.xml`

      e aumentare le dimensioni massime dei file e massime delle richieste ad almeno 500 MB, vedere l&#39;esempio seguente di un file `multipart-config` di questo tipo.`web.xml`

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Implementare AEM&#39;applicazione Web**

   * Scarica AEM file di guerra
   * Configurare le configurazioni In web.xml se necessario (vedere sopra nella Descrizione generale)

      * Scomprimi file WEB-INF/web.xml
      * modifica il parametro sling.run.mode da pubblicare
      * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come necessario
      * Reimballaggio del file web.xml
   * Rinominare AEM file di guerra in ROOT.war se si desidera distribuirlo come root webapp, rinominarlo ad esempio aemauthor.war se si desidera avere aemauthor come context root
   * copiarlo nella cartella delle app Web di tomcat
   * attendere fino a quando AEM installato


## Risoluzione dei problemi {#troubleshooting}

Per informazioni su come risolvere i problemi che possono verificarsi durante l&#39;installazione, vedete:

* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
