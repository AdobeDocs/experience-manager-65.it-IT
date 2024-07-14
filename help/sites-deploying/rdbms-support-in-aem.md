---
title: Supporto RDBMS nell’AEM 6.4
description: Scopri il supporto per la persistenza del database relazionale in AEM 6.4 e le opzioni di configurazione disponibili.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Supporto RDBMS nell’AEM 6.4{#rdbms-support-in-aem}

## Panoramica {#overview}

Il supporto per la persistenza del database relazionale nell&#39;AEM viene implementato utilizzando il Document Microkernel. Il Document Microkernel è la base utilizzata anche per implementare la persistenza di MongoDB.

È costituito da un’API Java basata sull’API Java Mongo. Viene inoltre fornita un’implementazione di un’API BlobStore. Per impostazione predefinita, i BLOB vengono memorizzati nel database.

Per ulteriori informazioni sui dettagli di implementazione, consulta la documentazione [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>È inoltre disponibile il supporto per **PostgreSQL 9.4**, ma solo a scopo dimostrativo. Non sarà disponibile per gli ambienti di produzione.

## Database supportati {#supported-databases}

Per ulteriori informazioni sul livello di supporto del database relazionale in AEM, vedere la [pagina Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

## Passaggi di configurazione {#configuration-steps}

L&#39;archivio viene creato configurando il servizio OSGi `DocumentNodeStoreService`. È stato esteso per supportare la persistenza del database relazionale oltre a MongoDB.

Affinché funzioni, è necessario configurare un’origine dati con l’AEM. Questa operazione viene eseguita tramite il file `org.apache.sling.datasource.DataSourceFactory.config`. I driver JDBC per il rispettivo database devono essere forniti separatamente come bundle OSGi all’interno della configurazione locale.

Per i passaggi relativi alla creazione di bundle OSGi per driver JDBC, consulta questa [documentazione](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) sul sito web Apache Sling.

Una volta che i bundle sono in posizione, segui i passaggi seguenti per configurare AEM con persistenza RDB:

1. Verificare che il daemon del database sia avviato e che sia disponibile un database attivo per l&#39;utilizzo con AEM.
1. Copia il file jar di AEM 6.3 nella directory di installazione.
1. Creare una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configurare l&#39;archivio dei nodi di documento creando un file di configurazione con il nome seguente nella directory `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configurare l&#39;origine dati e i parametri JDBC creando un altro file di configurazione con il nome seguente nella cartella `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >Per informazioni dettagliate sulla configurazione dell&#39;origine dati per ogni database supportato, vedere [Opzioni di configurazione di Data Source](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Quindi, prepara i bundle JDBC OSGi da utilizzare con AEM:

   1. Nella cartella `crx-quickstart/install`, creare una cartella denominata `9`.

   1. Posiziona il file jar JDBC nella nuova cartella.

1. Infine, avviare AEM con le modalità di esecuzione `crx3` e `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opzioni di configurazione di Data Source {#data-source-configuration-options}

La configurazione OSGi `org.apache.sling.datasource.DataSourceFactory-oak.config` viene utilizzata per configurare i parametri necessari per la comunicazione tra AEM e il livello di persistenza del database.

Sono disponibili le seguenti opzioni di configurazione:

* `datasource.name:` Nome dell&#39;origine dati. Il valore predefinito è `oak`.

* `url:` Stringa URL del database che deve essere utilizzato con JDBC. Ogni tipo di database ha il proprio formato di stringa URL. Per ulteriori informazioni, consulta [Formati stringa URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) di seguito.

* `driverClassName:` Il nome della classe del driver JDBC. Questo varia a seconda del database che si desidera utilizzare e, successivamente, del driver necessario per connettersi al database. Di seguito sono riportati i nomi delle classi per tutti i database supportati da AEM:

   * `org.postgresql.Driver` per PostgreSQL
   * `com.ibm.db2.jcc.DB2Driver` per DB2;
   * `oracle.jdbc.OracleDriver` ad Oracle;
   * `com.mysql.jdbc.Driver` per MySQL e MariaDB (sperimentale);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` per Microsoft SQL Server (sperimentale).

* `username:` Il nome utente in cui viene eseguito il database.

* `password:` La password del database.

### Formati stringa URL {#url-string-formats}

Nella configurazione dell’origine dati viene utilizzato un formato di stringa URL diverso a seconda del tipo di database da utilizzare. Di seguito è riportato un elenco di formati per i database attualmente supportati dall&#39;AEM:

* `jdbc:postgresql:databasename` per PostgreSQL
* `jdbc:db2://localhost:port/databasename` per DB2;
* `jdbc:oracle:thin:localhost:port:SID` ad Oracle;
* `jdbc:mysql://localhost:3306/databasename` per MySQL e MariaDB (sperimentale);
* `jdbc:sqlserver://localhost:1453;databaseName=name` per Microsoft SQL Server (sperimentale).

## Limitazioni note {#known-limitations}

Anche se l&#39;uso simultaneo di più istanze AEM con un singolo database è supportato dalla persistenza RDBMS, le installazioni simultanee non lo sono.

Per ovviare a questo problema, assicurarsi di eseguire prima l&#39;installazione con un singolo membro e aggiungere gli altri dopo che l&#39;installazione del primo ha terminato.
