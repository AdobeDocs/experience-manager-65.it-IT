---
title: Configurazione di MySQL per le funzionalità di abilitazione
seo-title: Configurazione di MySQL per le funzionalità di abilitazione
description: Connessione del server MySQL
seo-description: Connessione del server MySQL
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Admin
exl-id: 2d33e6ba-cd32-40d1-8983-58f636b21470
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 2%

---

# Configurazione di MySQL per le funzionalità di abilitazione {#mysql-configuration-for-enablement-features}

MySQL è un database relazionale utilizzato principalmente per il tracciamento SCORM e i dati di reporting per le risorse di abilitazione. Sono incluse tabelle per altre funzioni quali il tracciamento della pausa/ripresa del video.

Queste istruzioni descrivono come connettersi al server MySQL, stabilire il database di abilitazione e popolare il database con i dati iniziali.

## Requisiti {#requirements}

Prima di configurare la funzionalità di abilitazione di MySQL for Communities, assicurati di

* Installa [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server versione 5.6:
   * La versione 5.7 non è supportata per SCORM.
   * Può essere lo stesso server dell’istanza AEM autore.
* In tutte le istanze AEM, installare il driver ufficiale [JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql).
* Installa [Workbench di MySQL](https://dev.mysql.com/downloads/tools/workbench/).
* Su tutte le istanze AEM, installa il [pacchetto SCORM](enablement.md#scorm).

## Installazione di MySQL {#installing-mysql}

MySQL deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

### Nomi delle tabelle minuscoli {#lower-case-table-names}

Poiché SQL non distingue tra maiuscole e minuscole, per i sistemi operativi con distinzione tra maiuscole e minuscole, è necessario includere un&#39;impostazione per tutte le tabelle con distinzione tra maiuscole e minuscole.

Ad esempio, per specificare tutti i nomi di tabella minuscolo su un sistema operativo Linux:

* Modifica file `/etc/my.cnf`
* Nella sezione `[mysqld]`, aggiungi la seguente riga: `lower_case_table_names = 1`

### Set di caratteri UTF8 {#utf-character-set}

Per fornire un supporto multilingue migliore, è necessario utilizzare il set di caratteri UTF8.

Modificare MySQL in modo che UTF8 sia impostato come set di caratteri:
* mysql > IMPOSTA NOMI &#39;utf8&#39;;

Impostare il database MySQL come predefinito su UTF8:
* Modifica file `/etc/my.cnf`
* Nella sezione `[client]` aggiungi: `default-character-set=utf8`
* Nella sezione `[mysqld]` aggiungi: `character-set-server=utf8`

## Installazione di Workbench MySQL {#installing-mysql-workbench}

Workbench di MySQL fornisce un&#39;interfaccia utente per l&#39;esecuzione di script SQL che installano lo schema e i dati iniziali.

MySQL Workbench deve essere scaricato e installato seguendo le istruzioni per il sistema operativo di destinazione.

## Connessione abilitazione {#enablement-connection}

Al primo avvio di MySQL Workbench, a meno che non sia già in uso per altri scopi, non verrà ancora visualizzata alcuna connessione:

![mysqlconnection](assets/mysqlconnection.png)

### Nuove impostazioni di connessione {#new-connection-settings}

1. Seleziona l’icona &quot;+&quot; a destra di `MySQL Connections`.
1. Nella finestra di dialogo `Setup New Connection`, immetti i valori appropriati per la piattaforma a scopo dimostrativo, con l’istanza di authoring AEM e MySQL sullo stesso server:
   * Nome connessione: `Enablement`
   * Metodo di connessione: `Standard (TCP/IP)`
   * Nome host: `127.0.0.1`
   * Nome utente: `root`
   * Password: `no password by default`
   * Schema predefinito: `leave blank`
1. Selezionare `Test Connection` per verificare la connessione al servizio MySQL in esecuzione.

**Note**:
* La porta predefinita è `3306`.
* Il `Connection Name` scelto viene immesso come nome `datasource` in [Configurazione JDBC OSGi](#configure-jdbc-connections).

#### Connessione riuscita {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### Nuova connessione di abilitazione {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## Configurazione del database {#database-setup}

All&#39;apertura della nuova connessione di abilitazione, noterai che esiste uno schema di test e account utente predefiniti.

![configurazione del database](assets/database-setup.png)

### Ottenere gli script SQL {#obtain-sql-scripts}

Gli script SQL vengono ottenuti utilizzando CRXDE Lite nell&#39;istanza di authoring. Il [pacchetto SCORM](deploy-communities.md#scorm) deve essere installato:

1. Passa a CRXDE Lite:
   * Ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Espandi la cartella `/libs/social/config/scorm/`
1. Scarica `database_scormengine.sql`
1. Scarica `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

Un metodo per scaricare lo schema è:

* Selezionare il nodo `jcr:content` per il file sql.
* Nota che il valore della proprietà `jcr:data` è un collegamento di visualizzazione.
* Selezionare il collegamento di visualizzazione per salvare i dati in un file locale.

### Crea database SCORM {#create-scorm-database}

Il database SCORM di abilitazione da creare è:

* name: `ScormEngineDB`
* create dagli script:
   * schema: `database_scormengine.sql`
   * dati: `database_scorm_integration.sql`
Segui i passaggi seguenti (
[aprire](#step-open-sql-file),  [eseguire](#step-execute-sql-script)) per installare ogni script [ ](#obtain-sql-scripts) SQL. [](#refresh) Si aggiorna quando necessario per visualizzare i risultati dell’esecuzione dello script.

Prima di installare i dati, assicurati di installare lo schema.

>[!CAUTION]
>
>Se il nome del database viene modificato, assicurarsi di specificarlo correttamente in:
>
>* [Configurazione JDBC](#configure-jdbc-connections)
* [Configurazione SCORM](#configure-scorm)


#### Passaggio 1: apri file SQL {#step-open-sql-file}

In MySQL Workbench

* Dal menu a discesa File
* Seleziona `Open SQL Script ...`
* In questo ordine, seleziona una delle seguenti opzioni:
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### Passaggio 2: esegui script SQL {#step-execute-sql-script}

Nella finestra Workbench relativa al file aperto al passaggio 1, selezionare il percorso `lightening (flash) icon` per eseguire lo script.

Tieni presente che l’esecuzione dello script `database_scormengine.sql` per creare il database SCORM può richiedere un minuto per essere completata.

![scrom-database1](assets/scrom-database1.png)

#### Aggiorna {#refresh}

Una volta eseguiti gli script, è necessario aggiornare la sezione `SCHEMAS` del `Navigator` per visualizzare il nuovo database. Utilizza l’icona di aggiornamento a destra di &quot;SCHEMAS&quot;:

![scrom-database2](assets/scrom-database2.png)

#### Risultato: scormenginedb {#result-scormenginedb}

Dopo aver installato e aggiornato gli SCHEMI, il `scormenginedb` sarà visibile.

![scrom-database3](assets/scrom-database3.png)

## Configurare le connessioni JDBC {#configure-jdbc-connections}

La configurazione OSGi per **Day Commons JDBC Connections Pool** configura il driver JDBC MySQL.

Tutte le istanze di pubblicazione e creazione AEM devono puntare allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, il nome host del server deve essere specificato al posto di &quot;localhost&quot; nel connettore JDBC (che compila la configurazione [ScormEngine](#configurescormengineservice)).

* Su ogni istanza di authoring e pubblicazione AEM
* Accesso con privilegi di amministratore
* Accedi alla [console Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Individua il `Day Commons JDBC Connections Pool`
* Seleziona l’icona `+` per creare una nuova configurazione

   ![jdbcconnection1](assets/jdbcconnection1.png)

* Immetti i seguenti valori:
   * **[!UICONTROL Classe]** del driver JDBC:  `com.mysql.jdbc.Driver`
   * **Connessione DBC URIJ**:  `jdbc:mysql://localhost:3306/aem63reporting` specificare il server al posto di localhost se MySQL server non è lo stesso del server AEM &#39;this&#39;.
   * **[!UICONTROL Nome utente]**: Radice o immettere il nome utente configurato per il server MySQL, se non &quot;root&quot;.
   * **[!UICONTROL Password]**: Deselezionare questo campo se non è impostata alcuna password per MySQL, altrimenti immettere la password configurata per il nome utente MySQL.
   * **[!UICONTROL Nome]** origine dati: Nome immesso per la connessione  [MySQL](#new-connection-settings), ad esempio &quot;enablement&quot;.
* Seleziona **[!UICONTROL Salva]**.

## Configurare lo scorm {#configure-scorm}

### Servizio ScormEngine di AEM Communities {#aem-communities-scormengine-service}

La configurazione OSGi per **AEM Communities ScormEngine Service** configura SCORM per l&#39;utilizzo del server MySQL da parte della community di abilitazione.

Questa configurazione è presente quando è installato il [pacchetto SCORM](deploy-communities.md#scorm-package).

Tutte le istanze di pubblicazione e creazione puntano allo stesso server MySQL.

Quando MySQL viene eseguito su un server diverso da AEM, il nome host del server deve essere specificato al posto di &quot;localhost&quot; nel servizio ScormEngine, che in genere viene popolato dalla configurazione [JDBC Connection](#configure-jdbc-connections).

* Su ogni istanza di authoring e pubblicazione AEM
* Accesso con privilegi di amministratore
* Accedi alla [console Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Individua il `AEM Communities ScormEngine Service`
* Seleziona l’icona di modifica

   ![motore a scroto](assets/scrom-engine.png)

* Verifica che i seguenti valori dei parametri siano coerenti con la configurazione [JDBC Connection](#configurejdbcconnectionspool):
   * **[!UICONTROL URI]** di connessione JDBC:  `jdbc:mysql://localhost:3306/ScormEngineDB` ** ScormEngineDBè il nome di database predefinito negli script SQL
   * **[!UICONTROL Nome utente]**: Radice o immettere il nome utente configurato per il server MySQL, se non &quot;root&quot;
   * **[!UICONTROL Password]**: Cancella questo campo se non è impostata alcuna password per MySQL, altrimenti immetti la password configurata per il nome utente MySQL
* Per quanto riguarda il seguente parametro:
   * **[!UICONTROL Password]** utente scorm: NON MODIFICARE

      Solo per uso interno: È per un utente di servizio speciale utilizzato da AEM Communities per comunicare con il motore di punteggio.
* Seleziona **[!UICONTROL Salva]**

### Filtro CSRF Granite Adobe {#adobe-granite-csrf-filter}

Per garantire il corretto funzionamento dei corsi di abilitazione in tutti i browser, è necessario aggiungere Mozilla come Agente utente che non è controllato dal filtro CSRF.

* Accedi all&#39;istanza di pubblicazione AEM con privilegi di amministratore.
* Accedi alla [console Web](../../help/sites-deploying/configuring-osgi.md)
   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Individua `Adobe Granite CSRF Filter`.
* Seleziona l’icona di modifica.

   ![jdbcconnection2](assets/jdbcconnection2.png)

* Selezionare l&#39;icona `[+]` per aggiungere un agente utente sicuro.
* Immettere `Mozilla/*`.
* Seleziona **[!UICONTROL Salva]**.
