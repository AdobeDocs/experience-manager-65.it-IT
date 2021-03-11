---
title: Installazione dell’applicazione da server
seo-title: Installazione dell’applicazione da server
description: Scopri come installare AEM con un server applicazioni.
seo-description: Scopri come installare AEM con un server applicazioni.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 1%

---


# Installazione dell’applicazione da server{#application-server-install}

>[!NOTE]
>
>`JAR` e  `WAR` sono i tipi di file AEM viene rilasciato in. Questi formati sono sottoposti a garanzia della qualità per soddisfare i livelli di supporto che l&#39;Adobe si è impegnato a raggiungere.


In questa sezione viene illustrato come installare Adobe Experience Manager (AEM) con un application server. Consulta la sezione [Piattaforme supportate](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) per visualizzare i livelli di supporto specifici forniti per i singoli server delle applicazioni.

Sono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle WebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

Per ulteriori informazioni sull&#39;installazione di applicazioni web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la documentazione appropriata del server applicazioni.

>[!NOTE]
>
>Se utilizzi Dynamic Media in una distribuzione WAR, consulta la [documentazione Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

## Descrizione generale {#general-description}

### Comportamento predefinito durante l&#39;installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene fornito come un singolo file di guerra da distribuire.

Se implementato, il seguente verrà attivato per impostazione predefinita:

* la modalità di esecuzione è `author`
* l’istanza (Repository, ambiente Felix OSGI, bundle, ecc.) è installato in `${user.dir}/crx-quickstart`dove `${user.dir}` è la directory di lavoro corrente, questo percorso a crx-quickstart è chiamato `sling.home`

* la directory principale del contesto è il nome del file di guerra, ad esempio : `aem-6`

#### Configurazione {#configuration}

Puoi modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione : configura il parametro `sling.run.modes` nel file `WEB-INF/web.xml` del file di guerra AEM prima della distribuzione

* sling.home: configura il parametro `sling.home` nel file `WEB-INF/web.xml`del file di guerra AEM prima della distribuzione

* directory principale del contesto: rinominare il file di guerra AEM

#### Pubblica installazione {#publish-installation}

Per distribuire un&#39;istanza di pubblicazione è necessario impostare la modalità di esecuzione per la pubblicazione:

* Estrai il file WEB-INF/web.xml dal file di guerra AEM
* Modifica il parametro sling.run.modes in publish
* Ricomprimi il file web.xml AEM file WAR
* Distribuisci AEM file di guerra

#### Controllo dell&#39;installazione {#installation-check}

Per verificare se tutto è installato è possibile:

* tail il file `error.log`per vedere che tutto il contenuto è installato
* cerca in `/system/console` che tutti i bundle sono installati

#### Due istanze sullo stesso server applicazioni {#two-instances-on-the-same-application-server}

A scopo dimostrativo può essere opportuno installare l’istanza di authoring e pubblicazione in un unico server dell’applicazione. Per farlo, procedi come segue:

1. Modifica le variabili sling.home e le variabili sling.run.modes dell&#39;istanza Publish.
1. Estrai il file WEB-INF/web.xml dal file di guerra AEM.
1. Cambia il parametro sling.home in un percorso diverso (sono possibili percorsi assoluti e relativi).
1. Modifica le modalità sling.run.modes per pubblicare per l&#39;istanza di pubblicazione.
1. Ricomprimi il file web.xml.
1. Rinominare i file di guerra in modo che abbiano nomi diversi: Ad esempio, rinominare aemauthor.war e l&#39;altro in aempublish.war.
1. Utilizzare impostazioni di memoria più elevate, ad esempio per le istanze AEM predefinite che utilizzano ad esempio: -Xmx3072m
1. Distribuire le due applicazioni web.
1. Dopo la distribuzione, le due applicazioni Web vengono interrotte.
1. Sia nelle istanze di authoring che di pubblicazione verificare che nei file sling.properties la proprietà felix.service.urlhandlers=false sia impostata su false (l&#39;impostazione predefinita è true).
1. Riavviare le due applicazioni Web.

## Procedure di installazione dei server applicazioni {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

Prima di una distribuzione leggere la [Descrizione generale](#general-description) precedente.

**Preparazione del server**

* Lasciate passare le intestazioni di autenticazione di base:

   * Un modo per consentire AEM autenticare un utente è quello di disabilitare la sicurezza amministrativa globale del server WebSphere, per farlo: vai su Sicurezza -> Protezione globale e deseleziona la casella di controllo Abilita protezione amministrativa , salva e riavvia il server.

* set `"JAVA_OPTS= -Xmx2048m"`
* Se si desidera installare AEM utilizzando la directory principale del contesto = / allora è necessario prima modificare la directory principale del contesto dell&#39;applicazione Web predefinita esistente

**Distribuzione AEM applicazione Web**

* Scarica AEM file di guerra
* Imposta le configurazioni In web.xml se necessario (vedi sopra nella descrizione generale)

   * Annulla il pacchetto WEB-INF/web.xml file
   * cambia il parametro sling.run.modes per pubblicare
   * decommenta il parametro iniziale sling.home e imposta questo percorso come necessario
   * Repack file web.xml

* Distribuisci AEM file di guerra

   * Scegli una directory principale del contesto (se desideri impostare le modalità di esecuzione sling, devi selezionare i passaggi dettagliati della procedura guidata di distribuzione, quindi specificarlo nel passaggio 6 della procedura guidata)

* Avvia AEM applicazione Web

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

Prima di una distribuzione leggere la [Descrizione generale](#general-description) precedente.

**Preparare il server JBoss**

Imposta argomenti di memoria nel file conf (ad esempio `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

se si utilizza lo scanner di distribuzione per installare l&#39;applicazione Web AEM, potrebbe essere utile aumentare il valore `deployment-timeout,` per il quale impostare un attributo `deployment-timeout` nel file xml dell&#39;istanza (ad esempio `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**Distribuzione AEM applicazione Web**

* Carica l&#39;applicazione web AEM nella console di amministrazione JBoss.

* Abilita l&#39;applicazione web AEM.

#### Oracle WebLogic 12.1.3/12.2 {#oracle-weblogic}

Prima di una distribuzione leggere la [Descrizione generale](#general-description) precedente.

Questo utilizza un layout server semplice con solo un Admin Server.

**Preparazione del server WebLogic**

* In `${myDomain}/config/config.xml`aggiungi alla sezione security-configuration :

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` vedi su  [https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdper la posizione corretta (per impostazione predefinita, posizionarla alla fine della sezione va bene)

* Aumenta le impostazioni della memoria VM:

   * aprire `${myDomain}/bin/setDomainEnv.cmd` (risp.sh)cercare WLS_MEM_ARGS, impostare ad esempio set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * riavvia server WebLogic

* Crea in `${myDomain}` una cartella dei pacchetti e all&#39;interno di una cartella cq e in essa una cartella Plan

**Distribuzione AEM applicazione Web**

* Scarica AEM file di guerra
* Inserisci il file di guerra AEM nella cartella ${myDomain}/packages/cq
* Effettua le configurazioni In `WEB-INF/web.xml` se necessario (vedi sopra nella descrizione generale)

   * Rimuovi dal pacchetto il file `WEB-INF/web.xml`file
   * cambia il parametro sling.run.modes per pubblicare
   * decommenta il parametro iniziale sling.home e imposta questo percorso come necessario (consulta Descrizione generale)
   * Repack file web.xml

* Distribuire AEM file di guerra come applicazione (per le altre impostazioni utilizzare le impostazioni predefinite)
* L&#39;installazione può richiedere del tempo...
* Verifica che l&#39;installazione sia stata completata come indicato sopra nella Descrizione generale (ad esempio, la coda del file error.log)
* È possibile modificare la directory principale del contesto nella scheda Configurazione dell&#39;applicazione Web in WebLogic `/console`

#### Tomcat 8/8.5 {#tomcat}

Prima di una distribuzione leggere la [Descrizione generale](#general-description) precedente.

* **Prepara server Tomcat**

   * Aumenta le impostazioni della memoria VM:

      * In `bin/catalina.bat` (risp `catalina.sh` su unix) aggiungi la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat non consente né l&#39;accesso dell&#39;amministratore né del manager all&#39;installazione. Pertanto è necessario modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso a questi account:

      * Modifica `tomcat-users.xml` per includere l&#39;accesso per l&#39;amministratore e il manager. La configurazione deve essere simile all&#39;esempio seguente:

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
   * Se desideri distribuire AEM con la directory principale del contesto &quot;/&quot;, devi modificare la directory principale del contesto dell&#39;applicazione Web ROOT esistente:

      * Interrompi e disdistribuisci l&#39;applicazione Web ROOT
      * Rinomina la cartella ROOT.war nella cartella webapps di tomcat
      * Avvia di nuovo l&#39;app Web
   * Se installi l&#39;applicazione web AEM utilizzando il manager-gui allora è necessario aumentare la dimensione massima di un file caricato, in quanto la dimensione predefinita consente solo 50 MB di caricamento. Per questo aprire il web.xml dell&#39;applicazione web manager,

      `webapps/manager/WEB-INF/web.xml`

      e aumentare la dimensione massima del file e la dimensione massima della richiesta ad almeno 500 MB, vedi il seguente `multipart-config` esempio di un file `web.xml` di questo tipo.

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **Distribuzione AEM applicazione Web**

   * Scarica AEM file di guerra
   * Imposta le configurazioni In web.xml se necessario (vedi sopra nella descrizione generale)

      * Annulla il pacchetto WEB-INF/web.xml file
      * cambia il parametro sling.run.modes per pubblicare
      * decommenta il parametro iniziale sling.home e imposta questo percorso come necessario
      * Repack file web.xml
   * Rinomina AEM file di guerra in ROOT.war se desideri distribuirlo come webapp principale, rinominalo ad esempio aemauthor.war se desideri che aemauthor sia la directory principale del contesto
   * copiarlo nella cartella webapps di tomcat
   * attendere fino a quando AEM installato


## Risoluzione dei problemi {#troubleshooting}

Per informazioni sui problemi che possono verificarsi durante l&#39;installazione, vedi:

* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
