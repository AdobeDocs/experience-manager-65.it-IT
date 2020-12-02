---
title: Supporto RDBMS in AEM 6.4
seo-title: Supporto RDBMS in AEM 6.4
description: Ulteriori informazioni sul supporto della persistenza del database relazionale in AEM 6.4 e sulle opzioni di configurazione disponibili.
seo-description: Ulteriori informazioni sul supporto della persistenza del database relazionale in AEM 6.4 e sulle opzioni di configurazione disponibili.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Supporto RDBMS in AEM 6.4{#rdbms-support-in-aem}

## Panoramica {#overview}

Il supporto per la persistenza relazionale del database in AEM viene implementato utilizzando il Document Microkernel. Document Microkernel è la base utilizzata anche per implementare la persistenza MongoDB.

È costituita da un&#39;API Java basata sull&#39;API Java di Mongo. Viene inoltre fornita un&#39;implementazione di un&#39;API BlobStore. Per impostazione predefinita, i BLOB sono memorizzati nel database.

Per ulteriori informazioni sull&#39;implementazione, consultare la documentazione relativa a [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>È inoltre disponibile il supporto per **PostgreSQL 9.4**, ma solo a scopo dimostrativo. Non sarà disponibile per gli ambienti di produzione.

## Database supportati {#supported-databases}

Per ulteriori informazioni sul livello di supporto del database relazionale in AEM, vedere la pagina [Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

## Passaggi di configurazione {#configuration-steps}

Il repository viene creato configurando il servizio `DocumentNodeStoreService` OSGi. È stato esteso per supportare la persistenza relazionale del database oltre a MongoDB.

Per consentirne il funzionamento, è necessario configurare un&#39;origine dati con AEM. Questa operazione viene eseguita tramite il file `org.apache.sling.datasource.DataSourceFactory.config`. I driver JDBC per il rispettivo database devono essere forniti separatamente come bundle OSGi all&#39;interno della configurazione locale.

Per informazioni sulla creazione di pacchetti OSGi per i driver JDBC, consultate questa [documentazione](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) nel sito Web Apache Sling.

Una volta installati i bundle, attenetevi alla seguente procedura per configurare AEM con la persistenza RDB:

1. Accertatevi che il demone del database sia avviato e che sia presente un database attivo da utilizzare con AEM.
1. Copiate il AEM 6.3 jar nella directory di installazione.
1. Create una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configurare l&#39;archivio dei nodi del documento creando un file di configurazione con il seguente nome nella directory `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configurate l&#39;origine dati e i parametri JDBC creando un altro file di configurazione con il seguente nome nella cartella `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Per informazioni dettagliate sulla configurazione dell&#39;origine dati per ciascun database supportato, vedere [Opzioni di configurazione dell&#39;origine dati](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Quindi, preparate i bundle JDBC OSGi da utilizzare con AEM:

   1. Nella cartella `crx-quickstart/install`, create una cartella denominata `9`.

   1. Inserite il JDBC nella nuova cartella.

1. Infine, iniziare AEM con le modalità di esecuzione `crx3` e `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opzioni di configurazione origine dati {#data-source-configuration-options}

La configurazione `org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi viene utilizzata per configurare i parametri necessari per la comunicazione tra AEM e il livello di persistenza del database.

Sono disponibili le seguenti opzioni di configurazione:

* `datasource.name:` Il nome dell&#39;origine dati. Il valore predefinito è `oak`.

* `url:` Stringa URL del database che deve essere utilizzata con JDBC. Ogni tipo di database ha un proprio formato di stringa URL. Per ulteriori informazioni, vedere [Formati di stringa URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) di seguito.

* `driverClassName:` Il nome della classe del driver JDBC. Ciò varia a seconda del database che si desidera utilizzare e, successivamente, del driver necessario per connettersi ad esso. Di seguito sono riportati i nomi delle classi per tutti i database supportati da AEM:

   * `org.postgresql.Driver` per PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` per DB2;
   * `oracle.jdbc.OracleDriver` per  Oracle;
   * `com.mysql.jdbc.Driver` per MySQL e MariaDB (sperimentale);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` per Microsoft SQL Server (sperimentale).

* `username:` Il nome utente utilizzato dal database.

* `password:` La password del database.

### Formati stringa URL {#url-string-formats}

Nella configurazione dell&#39;origine dati viene utilizzato un formato di stringa URL diverso a seconda del tipo di database da utilizzare. Di seguito è riportato un elenco di formati per i database che AEM attualmente supportano:

* `jdbc:postgresql:databasename` per PostgreSQL;
* `jdbc:db2://localhost:port/databasename` per DB2;
* `jdbc:oracle:thin:localhost:port:SID` per  Oracle;
* `jdbc:mysql://localhost:3306/databasename` per MySQL e MariaDB (sperimentale);
* `jdbc:sqlserver://localhost:1453;databaseName=name` per Microsoft SQL Server (sperimentale).

## Limitazioni note {#known-limitations}

Anche se l&#39;uso simultaneo di più istanze AEM con un singolo database è supportato dalla persistenza RDBMS, le installazioni simultanee non lo sono.

Per risolvere il problema, accertatevi di eseguire prima l&#39;installazione con un singolo membro e di aggiungere gli altri al termine della prima installazione.

