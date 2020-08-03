---
title: Configurazione MySQL per le funzioni di abilitazione
seo-title: Configurazione MySQL per le funzioni di abilitazione
description: Connessione del server MySQL
seo-description: Connessione del server MySQL
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 2%

---


# Configurazione MySQL per le funzioni di abilitazione {#mysql-configuration-for-enablement-features}

MySQL è un database relazionale utilizzato principalmente per il tracciamento SCORM e i dati di reporting per le risorse di abilitazione. Sono incluse tabelle per altre funzioni, ad esempio per il tracciamento della pausa video/della ripresa.

Queste istruzioni descrivono come connettersi a MySQL Server, stabilire il database di abilitazione e compilare il database con i dati iniziali.

## Requisiti {#requirements}

Prima di configurare la funzione di abilitazione di MySQL for Communities, assicurarsi di

* Installare [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community Server versione 5.6:
   * La versione 5.7 non è supportata per SCORM.
   * Può trattarsi dello stesso server dell’istanza di creazione AEM.
* In tutte AEM istanze, installate il driver [JDBC ufficiale per MySQL](deploy-communities.md#jdbc-driver-for-mysql).
* Installare [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/).
* In tutte AEM istanze, installate il pacchetto [SCORM](enablement.md#scorm).

## Installazione di MySQL {#installing-mysql}

MySQL deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

### Nomi delle tabelle minuscoli {#lower-case-table-names}

Poiché SQL non fa distinzione tra maiuscole e minuscole, per i sistemi operativi con distinzione tra maiuscole e minuscole è necessario includere un&#39;impostazione per i nomi di tutte le tabelle con distinzione tra maiuscole e minuscole.

Ad esempio, per specificare tutti i nomi di tabella in lettere minuscole in un sistema operativo Linux:

* Modifica file `/etc/my.cnf`
* Nella `[mysqld]` sezione, aggiungi la seguente riga: `lower_case_table_names = 1`

### UTF8 set di caratteri {#utf-character-set}

Per fornire un supporto multilingue migliore, è necessario utilizzare il set di caratteri UTF8.

Modificate MySQL in modo che abbia UTF8 come set di caratteri:
* mysql > SET NAMES &#39;utf8&#39;;

Modificate il database MySQL impostando il valore predefinito su UTF8:
* Modifica file `/etc/my.cnf`
* Nella `[client]` sezione, aggiungi: `default-character-set=utf8`
* Nella `[mysqld]` sezione, aggiungi: `character-set-server=utf8`

## Installazione di MySQL Workbench {#installing-mysql-workbench}

Workbench SQL fornisce un&#39;interfaccia utente per l&#39;esecuzione di script SQL che installano lo schema e i dati iniziali.

MySQL Workbench deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

## Connessione abilitazione {#enablement-connection}

Al primo avvio di MySQL Workbench, a meno che non sia già in uso per altri scopi, non verrà ancora visualizzata alcuna connessione:

![mysqlconnection](assets/mysqlconnection.png)

### Nuove impostazioni di connessione {#new-connection-settings}

1. Selezionate l&#39;icona &quot;+&quot; a destra di `MySQL Connections`.
1. Nella finestra di dialogo `Setup New Connection`, immettete i valori appropriati per la piattaforma a scopo dimostrativo, con l’istanza AEM autore e MySQL sullo stesso server:
   * Nome connessione: `Enablement`
   * Metodo di connessione: `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * Nome utente: `root`
   * Password: `no password by default`
   * Schema predefinito: `leave blank`
1. Selezionare `Test Connection` per verificare la connessione al servizio MySQL in esecuzione.

**Note**:
* La porta predefinita è `3306`.
* Il `Connection Name` nome scelto viene immesso come `datasource` nome nella configurazione [OSGi](#configure-jdbc-connections)JDBC.

#### Connessione completata {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### Nuova connessione di abilitazione {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## Impostazione database {#database-setup}

All&#39;apertura della nuova connessione di abilitazione, è presente uno schema di test e gli account utente predefiniti.

![database-setup](assets/database-setup.png)

### Ottenere gli script SQL {#obtain-sql-scripts}

Gli script SQL vengono ottenuti utilizzando CRXDE Lite nell&#39;istanza di creazione. Il pacchetto [](deploy-communities.md#scorm) SCORM deve essere installato:

1. Passa al CRXDE Lite:
   * Ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Espandi la `/libs/social/config/scorm/` cartella
1. Scarica `database_scormengine.sql`
1. Scarica `database_scorm_integration.sql`

![sqlscript](assets/sqlscripts.png)

Un metodo per scaricare lo schema è:

* Selezionare il `jcr:content` nodo del file SQL.
* Il valore della `jcr:data` proprietà è un collegamento di visualizzazione.
* Selezionare il collegamento di visualizzazione per salvare i dati in un file locale.

### Crea database SCORM {#create-scorm-database}

Il database SCORM di attivazione da creare è il seguente:

* name: `ScormEngineDB`
* create da script:
   * schema: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`
Follow the steps below (
[open](#step-open-sql-file), [execute](#step-execute-sql-script)) per installare ogni script [](#obtain-sql-scripts) SQL. [Aggiorna](#refresh) se necessario per visualizzare i risultati dell&#39;esecuzione dello script.

Prima di installare i dati, assicurarsi di installare lo schema.

>[!CAUTION]
>
>Se il nome del database viene modificato, accertatevi di specificarlo correttamente in:
>
>* [Configurazione JDBC](#configure-jdbc-connections)
>* [Configurazione SCORM](#configure-scorm)

>



#### Passaggio 1: apri file SQL {#step-open-sql-file}

In MySQL Workbench

* Dal menu a discesa File
* Seleziona `Open SQL Script ...`
* In questo ordine, selezionare una delle seguenti opzioni:
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### Passaggio 2: execute SQL Script {#step-execute-sql-script}

Nella finestra Workbench per il file aperto al passaggio 1, selezionare l&#39;opzione `lightening (flash) icon` da eseguire.

L&#39;esecuzione dello `database_scormengine.sql` script per la creazione del database SCORM potrebbe richiedere alcuni minuti.

![scrom-database1](assets/scrom-database1.png)

#### Aggiorna {#refresh}

Una volta eseguiti gli script, è necessario aggiornare la `SCHEMAS` sezione del `Navigator` database per visualizzare il nuovo database. Utilizzate l&#39;icona di aggiornamento a destra di &#39;SCHEMAS&#39;:

![scrom-database2](assets/scrom-database2.png)

#### Risultato: scormenginedb {#result-scormenginedb}

Dopo l&#39;installazione e l&#39;aggiornamento degli SCHEMI, `scormenginedb` sarà visibile.

![scrom-database3](assets/scrom-database3.png)

## Configurare le connessioni JDBC {#configure-jdbc-connections}

La configurazione OSGi per il pool **di connessioni JDBC** Day Commons configura il driver JDBC MySQL.

Tutte le istanze di pubblicazione e creazione AEM devono puntare allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, il nome host del server deve essere specificato al posto di &quot;localhost&quot; nel connettore JDBC (che popola la configurazione [ScormEngine](#configurescormengineservice) ).

* Per ogni istanza di creazione e pubblicazione AEM
* Accesso con privilegi di amministratore
* Accedere alla console [Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Individua la variabile `Day Commons JDBC Connections Pool`
* Selezionate l&#39; `+` icona per creare una nuova configurazione

   ![jdbcconnection1](assets/jdbcconnection1.png)

* Immettete i seguenti valori:
   * **[!UICONTROL Classe]** driver JDBC: `com.mysql.jdbc.Driver`
   * **Connessione DBC URIJ **:`jdbc:mysql://localhost:3306/aem63reporting`specificare il server al posto di localhost se MySQL Server non è uguale a &#39;this&#39; AEM server.
   * **[!UICONTROL Nome utente]**: Radice o immettere il nome utente configurato per MySQL Server, se non &#39;root&#39;.
   * **[!UICONTROL Password]**: Deselezionare questo campo se non è impostata alcuna password per MySQL, altrimenti immettere la password configurata per il nome utente MySQL.
   * **[!UICONTROL Nome]** origine dati: Nome immesso per la connessione [](#new-connection-settings)MySQL, ad esempio &quot;enablement&quot;.
* Seleziona **[!UICONTROL Salva]**.

## Configura punteggio {#configure-scorm}

### Servizio ScormEngine AEM Communities {#aem-communities-scormengine-service}

La configurazione OSGi per il servizio **ScormEngine** AEM Communities configura SCORM per l&#39;utilizzo del server MySQL da parte di una comunità di abilitazione.

Questa configurazione è presente quando viene installato il pacchetto [](deploy-communities.md#scorm-package) SCORM.

Tutte le istanze di pubblicazione e creazione puntano allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, il nome host del server deve essere specificato al posto di &quot;localhost&quot; nel servizio ScormEngine, che in genere viene popolato dalla configurazione [JDBC Connection](#configure-jdbc-connections) .

* Per ogni istanza di creazione e pubblicazione AEM
* Accesso con privilegi di amministratore
* Accedere alla console [Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Individua la variabile `AEM Communities ScormEngine Service`
* Selezionate l’icona di modifica

   ![chlimage_1-337](assets/chlimage_1-337.png)

* Verificate che i seguenti valori di parametro siano coerenti con la configurazione [JDBC Connection](#configurejdbcconnectionspool) :
   * **[!UICONTROL URI]** connessione JDBC: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB* è il nome di database predefinito negli script SQL
   * **[!UICONTROL Nome utente]**: Root o immettere il nome utente configurato per MySQL Server, se non &#39;root&#39;
   * **[!UICONTROL Password]**: Cancella questo campo se non è impostata alcuna password per MySQL, altrimenti immetti la password configurata per MySQL Nome utente
* Per quanto riguarda il seguente parametro:
   * **[!UICONTROL Password]** utente scorm: NON MODIFICARE

      Solo per uso interno: È per un utente di servizio speciale utilizzato dai AEM Communities per comunicare con il motore di punteggio.
* Seleziona **[!UICONTROL Salva]**

### Filtro  Adobe Granite CSRF {#adobe-granite-csrf-filter}

Per garantire il corretto funzionamento dei corsi di abilitazione in tutti i browser, è necessario aggiungere Mozilla come agente utente che non è controllato dal filtro CSRF.

* Effettuate l’accesso all’istanza di pubblicazione AEM con i privilegi di amministratore.
* Accedere alla console [Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Individua `Adobe Granite CSRF Filter`.
* Selezionate l’icona di modifica.

   ![jdbcconnection2](assets/jdbcconnection2.png)

* Selezionate l&#39; `[+]` icona per aggiungere un agente utente sicuro.
* Enter `Mozilla/*`.
* Seleziona **[!UICONTROL Salva]**.

