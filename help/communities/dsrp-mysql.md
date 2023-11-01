---
title: Configurazione MySQL per DSRP
seo-title: MySQL Configuration for DSRP
description: Come connettersi al server MySQL e stabilire il database UGC
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# Configurazione MySQL per DSRP {#mysql-configuration-for-dsrp}

MySQL è un database relazionale che può essere utilizzato per memorizzare il contenuto generato dall&#39;utente (UGC, User Generated Content).

Queste istruzioni descrivono come connettersi al server MySQL e stabilire il database UGC.

## Requisiti {#requirements}

* [Feature pack per le community più recenti](deploy-communities.md#latestfeaturepack)
* [Driver JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Un database relazionale:

   * [Server MySQL](https://dev.mysql.com/downloads/mysql/) Server community versione 5.6 o successiva

      * Può essere eseguito sullo stesso host dell&#39;AEM o in remoto

   * [Workbench MySQL](https://dev.mysql.com/downloads/tools/workbench/)

## Installazione di MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) devono essere scaricati e installati seguendo le istruzioni per il sistema operativo di destinazione.

### Nomi di tabella minuscoli {#lower-case-table-names}

Poiché SQL non distingue tra maiuscole e minuscole, per i sistemi operativi che distinguono tra maiuscole e minuscole è necessario includere un&#39;impostazione che preveda l&#39;utilizzo di lettere minuscole per tutti i nomi di tabella.

Ad esempio, per specificare tutti i nomi di tabella minuscoli in un sistema operativo Linux:

* Modifica file `/etc/my.cnf`
* In `[mysqld]` , aggiungi la seguente riga:

  `lower_case_table_names = 1`

### Set di caratteri UTF8 {#utf-character-set}

Per fornire un migliore supporto multilingue, è necessario utilizzare il set di caratteri UTF8.

Modificare MySQL in modo che il set di caratteri sia UTF8:

* mysql > SET NAMES &#39;utf8&#39;;

Impostare il database MySQL su UTF8 come predefinito:

* Modifica file `/etc/my.cnf`
* In `[client]` , aggiungi la seguente riga:

  `default-character-set=utf8`

* In `[mysqld]` , aggiungi la seguente riga:

  `character-set-server=utf8`

## Installazione di MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench fornisce un&#39;interfaccia utente per l&#39;esecuzione di script SQL che installano lo schema e i dati iniziali.

MySQL Workbench deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

## Connessione community {#communities-connection}

Quando MySQL Workbench viene avviato per la prima volta, a meno che non sia già utilizzato per altri scopi, non mostrerà ancora alcuna connessione:

![mysqlconnection](assets/mysqlconnection.png)

### Nuove impostazioni di connessione {#new-connection-settings}

1. Seleziona la `+` a destra di `MySQL Connections`.
1. Nella finestra di dialogo `Setup New Connection`, immettere i valori appropriati per la piattaforma

   A scopo dimostrativo, con l’istanza AEM dell’autore e MySQL sullo stesso server:

   * Nome connessione: `Communities`
   * Metodo di connessione: `Standard (TCP/IP)`
   * Nome host: `127.0.0.1`
   * Nome utente: `root`
   * Password: `no password by default`
   * Schema predefinito: `leave blank`

1. Seleziona `Test Connection` per verificare la connessione al servizio MySQL in esecuzione

**Note**:

* La porta predefinita è `3306`
* Il nome di connessione scelto viene immesso come nome dell’origine dati in [Configurazione JDBC OSGi](#configurejdbcconnections)

#### Nuova connessione community {#new-communities-connection}

![community-connection](assets/community-connection.png)

## Impostazione database {#database-setup}

Apri la connessione Communities per installare il database.

![install-database](assets/install-database.png)

### Ottenere lo script SQL {#obtain-the-sql-script}

Lo script SQL viene ottenuto dall’archivio AEM:

1. Passa a CRXDE Liti

   * Ad esempio: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Seleziona la cartella /libs/social/config/datastore/dsrp/schema
1. Download `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

Un metodo per scaricare lo schema è:

* Seleziona la `jcr:content` nodo per il file sql
* Osserva il valore per `jcr:data` La proprietà è un collegamento di visualizzazione

* Selezionare il collegamento di visualizzazione per salvare i dati in un file locale

### Creare il database DSRP {#create-the-dsrp-database}

Per installare il database, eseguire la procedura seguente. Il nome predefinito del database è `communities`.

Se il nome del database viene modificato nello script, assicurarsi di modificarlo anche nel [Configurazione JDBC](#configurejdbcconnections).

#### Passaggio 1: aprire il file SQL {#step-open-sql-file}

Nel workbench MySQL

* Dal menu a discesa File, selezionare **[!UICONTROL Apri script SQL]** opzione
* Seleziona il download `init_schema.sql` script

![select-sql-script](assets/select-sql-script.png)

#### Passaggio 2: eseguire lo script SQL {#step-execute-sql-script}

Nella finestra del workbench per il file aperto nel passaggio 1, selezionare `lightening (flash) icon` per eseguire lo script.

Nell&#39;immagine seguente, il `init_schema.sql` file pronto per l&#39;esecuzione:

![execute-sql-script](assets/execute-sql-script.png)

#### Aggiorna {#refresh}

Una volta eseguito lo script, è necessario aggiornare `SCHEMAS` sezione del `Navigator` per visualizzare il nuovo database. Utilizza l’icona di aggiornamento a destra di &quot;SCHEMAS&quot;:

![refresh-schema](assets/refresh-schema.png)

## Configura connessione JDBC {#configure-jdbc-connection}

Configurazione OSGi per **Pool connessioni JDBC Day Commons** configura il driver JDBC MySQL.

Tutte le istanze AEM di pubblicazione e creazione devono puntare allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, è necessario specificare il nome host del server al posto di &quot;localhost&quot; nel connettore JDBC.

* Su ogni istanza AEM di authoring e pubblicazione.
* Accesso eseguito con privilegi di amministratore.
* Accedere a [console web](../../help/sites-deploying/configuring-osgi.md).

   * Ad esempio: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Individua il `Day Commons JDBC Connections Pool`
* Seleziona la `+` per creare una nuova configurazione di connessione.

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Immetti i seguenti valori:

   * **[!UICONTROL Classe driver JDBC]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI connessione JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     Specificare il server al posto di localhost se il server MySQL non è uguale al server AEM &#39;this&#39; *community* è il nome predefinito del database (schema).

   * **[!UICONTROL Nome utente]**: `root`

     In alternativa, immettere il nome utente configurato per il server MySQL, se non &quot;root&quot;.

   * **[!UICONTROL Password]**:

     Cancellare questo campo se non è stata impostata alcuna password per MySQL.

     In caso contrario, immettere la password configurata per il nome utente MySQL.

   * **[!UICONTROL Nome origine dati]**: nome immesso per [Connessione MySQL](#new-connection-settings), ad esempio, &quot;community&quot;.

* Seleziona **[!UICONTROL Salva]**
