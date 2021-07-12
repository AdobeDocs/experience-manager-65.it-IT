---
title: Configurazione MySQL per DSRP
seo-title: Configurazione MySQL per DSRP
description: Come connettersi al server MySQL e stabilire il database UGC
seo-description: Come connettersi al server MySQL e stabilire il database UGC
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Configurazione MySQL per DSRP {#mysql-configuration-for-dsrp}

MySQL è un database relazionale che può essere utilizzato per memorizzare il contenuto generato dall&#39;utente (UGC).

Queste istruzioni descrivono come connettersi al server MySQL e stabilire il database UGC.

## Requisiti {#requirements}

* [Feature pack per le community più recenti](deploy-communities.md#latestfeaturepack)
* [Driver JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Database relazionale:

   * [MySQL ](https://dev.mysql.com/downloads/mysql/) serverCommunity Server versione 5.6 o successiva

      * Può essere eseguito sullo stesso host AEM o eseguito in remoto
   * [Workbench di lavoro MySQL](https://dev.mysql.com/downloads/tools/workbench/)


## Installazione di MySQL {#installing-mysql}

[](https://dev.mysql.com/downloads/mysql/) MySQLdeve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

### Nomi delle tabelle minuscoli {#lower-case-table-names}

Poiché SQL non distingue tra maiuscole e minuscole, per i sistemi operativi con distinzione tra maiuscole e minuscole, è necessario includere un&#39;impostazione per tutte le tabelle con distinzione tra maiuscole e minuscole.

Ad esempio, per specificare tutti i nomi di tabella minuscolo su un sistema operativo Linux:

* Modifica file `/etc/my.cnf`
* Nella sezione `[mysqld]`, aggiungi la seguente riga:

   `lower_case_table_names = 1`

### Set di caratteri UTF8 {#utf-character-set}

Per fornire un supporto multilingue migliore, è necessario utilizzare il set di caratteri UTF8.

Modificare MySQL in modo che UTF8 sia impostato come set di caratteri:

* mysql > IMPOSTA NOMI &#39;utf8&#39;;

Impostare il database MySQL come predefinito su UTF8:

* Modifica file `/etc/my.cnf`
* Nella sezione `[client]`, aggiungi la seguente riga:

   `default-character-set=utf8`

* Nella sezione `[mysqld]`, aggiungi la seguente riga:

   `character-set-server=utf8`

## Installazione di Workbench MySQL {#installing-mysql-workbench}

Workbench di MySQL fornisce un&#39;interfaccia utente per l&#39;esecuzione di script SQL che installano lo schema e i dati iniziali.

MySQL Workbench deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

## Connessione community {#communities-connection}

Al primo avvio di MySQL Workbench, a meno che non sia già in uso per altri scopi, non verrà ancora visualizzata alcuna connessione:

![mysqlconnection](assets/mysqlconnection.png)

### Nuove impostazioni di connessione {#new-connection-settings}

1. Seleziona l’icona `+` a destra di `MySQL Connections`.
1. Nella finestra di dialogo `Setup New Connection`, immetti i valori appropriati per la piattaforma

   A scopo dimostrativo, con l&#39;istanza AEM autore e MySQL sullo stesso server:

   * Nome connessione: `Communities`
   * Metodo di connessione: `Standard (TCP/IP)`
   * Nome host: `127.0.0.1`
   * Nome utente: `root`
   * Password: `no password by default`
   * Schema predefinito: `leave blank`

1. Selezionare `Test Connection` per verificare la connessione al servizio MySQL in esecuzione

**Note**:

* La porta predefinita è `3306`
* Il nome di connessione scelto viene immesso come nome dell&#39;origine dati nella configurazione [JDBC OSGi](#configurejdbcconnections)

#### Nuova connessione community {#new-communities-connection}

![connessione](assets/community-connection.png)

## Configurazione del database {#database-setup}

Apri la connessione Communities per installare il database.

![install-database](assets/install-database.png)

### Ottenere lo script SQL {#obtain-the-sql-script}

Lo script SQL viene ottenuto dal repository AEM:

1. Sfoglia CRXDE Lite

   * Ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Seleziona la cartella /libs/social/config/datastore/dsrp/schema
1. Scarica `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

Un metodo per scaricare lo schema è:

* Selezionare il nodo `jcr:content` per il file sql
* Il valore della proprietà `jcr:data` è un collegamento di visualizzazione

* Selezionare il collegamento di visualizzazione per salvare i dati in un file locale

### Creare il database DSRP {#create-the-dsrp-database}

Per installare il database, effettua le seguenti operazioni. Il nome predefinito del database è `communities`.

Se il nome del database viene modificato nello script, assicurati di modificarlo anche nella [configurazione JDBC](#configurejdbcconnections).

#### Passaggio 1: apri file SQL {#step-open-sql-file}

In MySQL Workbench

* Dal menu a discesa File, selezionare l&#39;opzione **[!UICONTROL Apri script SQL]**
* Seleziona lo script `init_schema.sql` scaricato

![select-sql-script](assets/select-sql-script.png)

#### Passaggio 2: esegui script SQL {#step-execute-sql-script}

Nella finestra Workbench relativa al file aperto al passaggio 1, selezionare il percorso `lightening (flash) icon` per eseguire lo script.

Nell&#39;immagine seguente, il file `init_schema.sql` è pronto per essere eseguito:

![execute-sql-script](assets/execute-sql-script.png)

#### Aggiorna {#refresh}

Una volta eseguito lo script, è necessario aggiornare la sezione `SCHEMAS` del `Navigator` per visualizzare il nuovo database. Utilizza l’icona di aggiornamento a destra di &quot;SCHEMAS&quot;:

![refresh-schema](assets/refresh-schema.png)

## Configurare la connessione JDBC {#configure-jdbc-connection}

La configurazione OSGi per **Day Commons JDBC Connections Pool** configura il driver JDBC MySQL.

Tutte le istanze di pubblicazione e creazione AEM devono puntare allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, il nome host del server deve essere specificato al posto di &quot;localhost&quot; nel connettore JDBC.

* Su ogni istanza di authoring e pubblicazione AEM.
* Accesso con privilegi di amministratore.
* Accedi alla [console Web](../../help/sites-deploying/configuring-osgi.md).

   * Ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Individua il `Day Commons JDBC Connections Pool`
* Seleziona l’icona `+` per creare una nuova configurazione di connessione.

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Immetti i seguenti valori:

   * **[!UICONTROL Classe]** del driver JDBC:  `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI]** di connessione JDBC:  `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Specificare il server al posto di localhost se MySQL Server non è lo stesso del server *communities* è il nome predefinito del database (schema).

   * **[!UICONTROL Nome utente]**:  `root`

      In alternativa, immettere il nome utente configurato per il server MySQL, se non &quot;root&quot;.

   * **[!UICONTROL Password]**:

      Cancella questo campo se non è impostata alcuna password per MySQL,

      in alternativa, immettere la password configurata per il nome utente MySQL.

   * **[!UICONTROL Nome]** origine dati: nome immesso per la connessione  [MySQL](#new-connection-settings), ad esempio &quot;communities&quot;.

* Seleziona **[!UICONTROL Salva]**
