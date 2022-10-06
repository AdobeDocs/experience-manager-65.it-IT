---
title: Supporto RDBMS in AEM 6.4
seo-title: RDBMS Support in AEM 6.4
description: Scopri il supporto per la persistenza del database relazionale in AEM 6.4 e le opzioni di configurazione disponibili.
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Supporto RDBMS in AEM 6.4{#rdbms-support-in-aem}

## Panoramica {#overview}

Il supporto per la persistenza del database relazionale in AEM viene implementato utilizzando il Microsoft Document. Il Document Microkernel è la base utilizzata anche per implementare la persistenza MongoDB.

È costituito da un’API Java basata sull’API Java Mongo. Viene inoltre fornita un’implementazione di un’API BlobStore. Per impostazione predefinita, i BLOB sono memorizzati nel database.

Per ulteriori informazioni sui dettagli di implementazione, consulta la [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) documentazione.

>[!NOTE]
>
>Supporto per **PostgreSQL 9.4** viene fornito anche, ma solo a scopo dimostrativo. Non sarà disponibile per gli ambienti di produzione.

## Database supportati {#supported-databases}

Per ulteriori informazioni sul livello di supporto del database relazionale in AEM, vedere la [Pagina Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

## Passaggi di configurazione {#configuration-steps}

L’archivio viene creato configurando il `DocumentNodeStoreService` Servizio OSGi. È stato esteso per supportare la persistenza del database relazionale oltre a MongoDB.

Affinché funzioni, è necessario configurare un’origine dati con AEM. Questo avviene tramite il `org.apache.sling.datasource.DataSourceFactory.config` file. I driver JDBC per il rispettivo database devono essere forniti separatamente come bundle OSGi all&#39;interno della configurazione locale.

Per i passaggi sulla creazione di bundle OSGi per i driver JDBC, consulta questo [documentazione](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) sul sito web Apache Sling.

Una volta installati i bundle, segui i passaggi seguenti per configurare AEM con la persistenza RDB:

1. Assicurati che il daemon di database sia avviato e che sia presente un database attivo da utilizzare con AEM.
1. Copia il jar AEM 6.3 nella directory di installazione.
1. Crea una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configura l&#39;archivio dei nodi del documento creando un file di configurazione con il seguente nome nel `crx-quickstart\install` directory:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configura l’origine dati e i parametri JDBC creando un altro file di configurazione con il seguente nome nella `crx-quickstart\install` cartella:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Per informazioni dettagliate sulla configurazione dell&#39;origine dati per ciascun database supportato, vedere [Opzioni di configurazione dell’origine dati](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Quindi, prepara i bundle JDBC OSGi da utilizzare con AEM:

   1. In `crx-quickstart/install` cartella, creare una cartella denominata `9`.

   1. Posiziona il jar JDBC nella nuova cartella.

1. Infine, inizia AEM con il `crx3` e `crx3rdb` modalità di esecuzione:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opzioni di configurazione dell’origine dati {#data-source-configuration-options}

La `org.apache.sling.datasource.DataSourceFactory-oak.config` La configurazione OSGi viene utilizzata per configurare i parametri necessari per la comunicazione tra AEM e il livello di persistenza del database.

Sono disponibili le seguenti opzioni di configurazione:

* `datasource.name:` Nome dell&#39;origine dati. Il valore predefinito è `oak`.

* `url:` Stringa URL del database che deve essere utilizzata con JDBC. Ogni tipo di database ha il proprio formato stringa URL. Per ulteriori informazioni, consulta [Formati di stringa URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) sotto.

* `driverClassName:` Nome della classe del driver JDBC. Questo varia a seconda del database che si desidera utilizzare e, successivamente, del driver necessario per connettersi ad esso. Di seguito sono riportati i nomi delle classi per tutti i database supportati da AEM:

   * `org.postgresql.Driver` per PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` per DB2;
   * `oracle.jdbc.OracleDriver` per Oracle;
   * `com.mysql.jdbc.Driver` per MySQL e MariaDB (sperimentale);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` per Microsoft SQL Server (sperimentale).

* `username:` Il nome utente con cui viene eseguito il database.

* `password:` Password del database.

### Formati di stringa URL {#url-string-formats}

Nella configurazione dell’origine dati viene utilizzato un formato di stringa URL diverso a seconda del tipo di database che deve essere utilizzato. Di seguito è riportato un elenco dei formati per i database che AEM attualmente supportano:

* `jdbc:postgresql:databasename` per PostgreSQL;
* `jdbc:db2://localhost:port/databasename` per DB2;
* `jdbc:oracle:thin:localhost:port:SID` per Oracle;
* `jdbc:mysql://localhost:3306/databasename` per MySQL e MariaDB (sperimentale);
* `jdbc:sqlserver://localhost:1453;databaseName=name` per Microsoft SQL Server (sperimentale).

## Limitazioni note {#known-limitations}

Mentre l’utilizzo simultaneo di più istanze AEM con un singolo database è supportato dalla persistenza RDBMS, le installazioni simultanee non lo sono.

Per risolvere il problema, assicurati di eseguire prima l&#39;installazione con un singolo membro e di aggiungere gli altri al termine della prima installazione.
