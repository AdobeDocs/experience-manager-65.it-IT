---
title: Installazione dell’applicazione da server
seo-title: Installazione dell’applicazione da server
description: Scopri come installare AEM con un server applicazione.
seo-description: Scopri come installare AEM con un server applicazione.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Installazione dell’applicazione da server{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` i tipi di file in cui AEM viene rilasciato. Questi formati sono sottoposti a controllo qualità per soddisfare i livelli di supporto a cui Adobe si è impegnata.


Questa sezione descrive come installare Adobe Experience Manager (AEM) con un server applicazione. Consultate la sezione Piattaforme [](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) supportate per visualizzare i livelli di supporto specifici forniti per i singoli server applicazione.

Sono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Per ulteriori informazioni sull&#39;installazione delle applicazioni Web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la relativa documentazione del server applicazione.

>[!NOTE]
>
>Se utilizzi Dynamic Media in una distribuzione WAR, consulta la documentazione [relativa ai contenuti multimediali](/help/assets/config-dynamic.md#enabling-dynamic-media)dinamici.

## Descrizione generale {#general-description}

### Comportamento predefinito durante l&#39;installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene fornito come un singolo file di guerra da distribuire.

Se distribuito, per impostazione predefinita si verifica quanto segue:

* la modalità di esecuzione è `author`
* l’istanza (repository, ambiente Felix OSGI, pacchetti, ecc.) è installato in `${user.dir}/crx-quickstart`cui `${user.dir}` si trova la directory di lavoro corrente, questo percorso a crx-quickstart viene chiamato `sling.home`

* la radice del contesto è il nome del file di guerra, ad esempio: `aem-6`

#### Configurazione {#configuration}

Potete modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione: configura il `sling.run.modes` parametro nel `WEB-INF/web.xml` file del file AEM prima della distribuzione

* sling.home: configura il `sling.home` parametro nel `WEB-INF/web.xml`file del file AEM prima della distribuzione

* context root: rinominare il file di guerra di AEM

#### Installazione di Publish {#publish-installation}

Per implementare un’istanza di pubblicazione è necessario impostare la modalità di esecuzione per la pubblicazione:

* Estrarre il file WEB-INF/web.xml dal file di guerra di AEM
* Cambia il parametro sling.run.mode in pubblicazione
* Reimballaggio del file web.xml nel file di guerra di AEM
* Implementare il file di guerra AEM

#### Controllo dell&#39;installazione {#installation-check}

Per verificare se è installato tutto, potete:

* chiudi il `error.log`file per vedere che tutto il contenuto è installato
* verificare `/system/console` che tutti i bundle siano installati

#### Due istanze sullo stesso server applicazioni {#two-instances-on-the-same-application-server}

A scopo dimostrativo può essere opportuno installare l’istanza di creazione e pubblicazione in un unico server applicazione. Per farlo, effettuate le seguenti operazioni:

1. Modificate le variabili sling.home e sling.run.mode dell’istanza di pubblicazione.
1. Rimuovete il file WEB-INF/web.xml dal file di guerra di AEM.
1. Modificate il parametro sling.home impostando un percorso diverso (sono possibili percorsi assoluti e relativi).
1. Modificate sling.run.mode per pubblicare l’istanza di pubblicazione.
1. Reimpacchettare il file web.xml.
1. Rinominare i file di guerra in modo che abbiano nomi diversi: Ad esempio, rinominate aemauthor.war e aempublish.war.
1. Utilizzate impostazioni di memoria più elevate, ad esempio per le istanze predefinite di AEM che utilizzano ad esempio: -Xmx3072m
1. Distribuire le due applicazioni Web.
1. Dopo la distribuzione, le due applicazioni Web vengono arrestate.
1. Sia nelle istanze di creazione che di pubblicazione verificare che nei file sling.properties la proprietà felix.service.urlhandlers=false sia impostata su false (l’impostazione predefinita è true).
1. Avviate di nuovo le due applicazioni Web.

## Procedure di installazione dei server applicazioni {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Prima di una distribuzione, leggete la Descrizione [](#general-description) generale riportata qui sopra.

**Preparazione server**

* Lasciate passare le intestazioni di autenticazione di base:

   * Un modo per consentire ad AEM di autenticare un utente consiste nel disattivare la sicurezza amministrativa globale del server WebSphere per eseguire questa operazione: andate a Protezione > Sicurezza globale e deselezionate la casella di controllo Abilita protezione amministrativa, salvate e riavviate il server.

* imposta `"JAVA_OPTS= -Xmx2048m"`
* Se desideri installare AEM utilizzando la radice contestuale = /, devi prima cambiare la radice contestuale dell’applicazione Web predefinita esistente

**Implementare l’applicazione Web AEM**

* Scarica il file di guerra AEM
* Configurare le configurazioni In web.xml se necessario (vedere sopra nella Descrizione generale)

   * Rimuovi pacchetto WEB-INF/web.xml file
   * modifica il parametro sling.run.mode da pubblicare
   * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come necessario
   * Reimballaggio del file web.xml

* Implementare il file di guerra AEM

   * Scegliere una directory principale di contesto (se si desidera impostare le modalità di esecuzione sling, è necessario selezionare i passaggi dettagliati della procedura guidata di distribuzione, quindi specificarla nel passaggio 6 della procedura guidata)

* Avviare l’applicazione Web AEM

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Prima di una distribuzione, leggete la Descrizione [](#general-description) generale riportata qui sopra.

**Preparazione del server JBoss**

Impostate gli argomenti di memoria nel file conf (ad es. `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

se utilizzate lo scanner di distribuzione per installare l’applicazione Web AEM, potrebbe essere utile aumentare il `deployment-timeout,` relativo valore impostando un `deployment-tiimeout` attributo nel file xml dell’istanza (ad esempio `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Implementare l’applicazione Web AEM**

* Caricate l’applicazione Web AEM nella console di amministrazione JBoss.

* Abilita l’applicazione Web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Prima di una distribuzione, leggete la Descrizione [](#general-description) generale riportata qui sopra.

Questo utilizza un layout server semplice con un solo Admin Server.

**Preparazione server WebLogic**

* In `${myDomain}/config/config.xml`aggiunta alla sezione sicurezza-configurazione:

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` consultate [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) per la posizione corretta (per impostazione predefinita, posizionarla alla fine della sezione è ok)

* Aumenta le impostazioni della memoria VM:

   * open `${myDomain}/bin/setDomainEnv.cmd` (risp.sh) search for WLS_MEM_ARGS, set ad esempio set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * riavvio del server WebLogic

* Creare in `${myDomain}` una cartella di pacchetti e all’interno di una cartella cq e all’interno di una cartella Plan

**Implementare l’applicazione Web AEM**

* Scarica il file di guerra AEM
* Inserire il file di guerra AEM nella cartella ${myDomain}/packages/cq
* Configurare le configurazioni in `WEB-INF/web.xml` base alle esigenze (vedere sopra nella Descrizione generale)

   * Separa `WEB-INF/web.xml`file
   * modifica il parametro sling.run.mode da pubblicare
   * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come desiderate (consultate Descrizione generale)
   * Reimballaggio del file web.xml

* Distribuire il file di guerra di AEM come applicazione (per le altre impostazioni utilizzare le impostazioni predefinite)
* L&#39;installazione può richiedere del tempo...
* Verificate che l&#39;installazione sia stata completata come indicato sopra nella Descrizione generale (ad es., il file error.log)
* È possibile modificare la radice del contesto nella scheda Configurazione dell&#39;applicazione Web in WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Prima di una distribuzione, leggete la Descrizione [](#general-description) generale riportata qui sopra.

* **Prepara server Tomcat**

   * Aumenta le impostazioni della memoria VM:

      * In `bin/catalina.bat` (risp `catalina.sh` su unix) aggiungete la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat non consente né l&#39;accesso dell&#39;amministratore né del manager all&#39;installazione. Pertanto è necessario modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso ai seguenti account:

      * Modifica `tomcat-users.xml` per includere l&#39;accesso per l&#39;amministratore e il manager. La configurazione deve essere simile all&#39;esempio seguente:
      * 
         ```
         <?xml version='1.0' encoding='utf-8'?>
          <tomcat-users>
          <role rolename="manager"/>
          <role rolename="tomcat"/>
          <role rolename="admin"/>
          <role rolename="role1"/>
          <role rolename="manager-gui"/>
          <user username="both" password="tomcat" roles="tomcat,role1"/>
          <user username="tomcat" password="tomcat" roles="tomcat"/>
          <user username="admin" password="admin" roles="admin,manager-gui"/>
          <user username="role1" password="tomcat" roles="role1"/>
          </tomcat-users>
         ```
   * Se desideri distribuire AEM con la radice contestuale &quot;/&quot;, devi modificare la radice contestuale dell’app Web principale esistente:

      * Arrestare e annullare la distribuzione dell&#39;app Web ROOT
      * Rinomina cartella ROOT.war nella cartella delle app Web di Tomcat
      * Avvia di nuovo l&#39;app Web
   * Se installate l’applicazione Web AEM tramite manager-gui, dovete aumentare la dimensione massima di un file caricato, in quanto l’impostazione predefinita consente solo 50 MB di caricamento. Per aprire il file web.xml dell&#39;applicazione Web manager,

      `webapps/manager/WEB-INF/web.xml`

      e aumentare le dimensioni massime dei file e massime delle richieste ad almeno 500 MB, vedere l&#39; `multipart-config` esempio seguente di tale `web.xml` file:

      ```
        <multipart-config>
         <!-- 500MB max -->
         <max-file-size>524288000</max-file-size>
         <max-request-size>524288000</max-request-size>
         <file-size-threshold>0</file-size-threshold>
         </multipart-config>
      ```




* **Implementare l’applicazione Web AEM**

   * Scarica il file di guerra AEM
   * Configurare le configurazioni In web.xml se necessario (vedere sopra nella Descrizione generale)

      * Rimuovi pacchetto WEB-INF/web.xml file
      * modifica il parametro sling.run.mode da pubblicare
      * rimuovete il commento dal parametro iniziale sling.home e impostate il percorso come necessario
      * Reimballaggio del file web.xml
   * Rinominare il file di guerra AEM in ROOT.war se si desidera distribuirlo come app Web principale, rinominarlo ad esempio aemauthor.war se si desidera avere aemauthor come radice del contesto
   * copiarlo nella cartella delle app Web di tomcat
   * attendere l&#39;installazione di AEM


## Risoluzione dei problemi {#troubleshooting}

Per informazioni sulla gestione dei problemi che possono verificarsi durante l&#39;installazione, vedete:

* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)

