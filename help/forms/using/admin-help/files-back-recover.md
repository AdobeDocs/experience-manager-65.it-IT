---
title: File di backup e ripristino
description: Questo documento descrive l'applicazione e i file di dati di cui è necessario eseguire il backup.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---

# File di backup e ripristino {#files-to-back-up-and-recover}

L&#39;applicazione e i file di dati di cui è necessario eseguire il backup sono descritti più dettagliatamente nelle sezioni seguenti.

Considerare i seguenti punti relativi al backup e al ripristino:

* Il backup del database deve essere eseguito prima dell’archivio GDS e AEM.
* Se è necessario arrestare i nodi di un ambiente cluster cluster per il backup, assicurarsi che i nodi secondari vengano arrestati prima del nodo principale. In caso contrario, potrebbe causare incoerenza nel cluster o nel server. Inoltre, il nodo principale deve essere reso attivo prima di qualsiasi nodo secondario.
* Per l&#39;operazione di ripristino di un cluster, è necessario arrestare il server applicazioni per ogni nodo del cluster.

## Directory di archiviazione documenti globale {#global-document-storage-directory}

Il GDS è una directory utilizzata per memorizzare i file di lunga durata utilizzati all&#39;interno di un processo. Il ciclo di vita dei file a lunga durata ha lo scopo di abbracciare uno o più lanci di un sistema AEM forms e può estendersi per giorni e persino anni. Questi file di lunga durata possono includere PDF, criteri e modelli di modulo. I file di lunga durata sono una parte critica dello stato generale di molte distribuzioni di moduli AEM. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server Forms potrebbe diventare instabile.

I documenti di input per la chiamata asincrona del processo sono memorizzati anche nel GDS e devono essere disponibili per elaborare le richieste. È quindi importante considerare l&#39;affidabilità del file system che ospita il GDS e utilizzare un array ridondante di dischi indipendenti (RAID) o altra tecnologia appropriata per soddisfare i requisiti di qualità e livello di servizio.

La posizione del GDS viene determinata durante il processo di installazione dei moduli AEM o successivamente utilizzando la console di amministrazione. Oltre a mantenere una posizione di elevata disponibilità per GDS, è possibile abilitare anche l&#39;archiviazione del database per i documenti. Vedere [Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Posizione GDS {#gds-location}

Se si lascia vuota l&#39;impostazione relativa al percorso durante l&#39;installazione, per impostazione predefinita viene utilizzata una directory nell&#39;installazione del server applicazioni. Eseguire il backup della seguente directory per il server applicazioni:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se la posizione GDS è stata modificata in una posizione non predefinita, è possibile determinarla nel modo seguente:

* Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
* Registrare il percorso specificato nella casella Directory di archiviazione documenti globale.

In un ambiente cluster, GDS in genere punta a una directory condivisa in rete e accessibile in lettura/scrittura per ogni nodo cluster.

La posizione del GDS può essere modificata durante un ripristino se la posizione originale non è più disponibile. (Vedi [Modifica del percorso GDS durante il ripristino](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti {#backup-options-when-database-is-used-for-document-storage}

È possibile abilitare l’archiviazione dei documenti dei moduli AEM nel database dei moduli AEM utilizzando la console di amministrazione. Anche se questa opzione mantiene tutti i documenti persistenti nel database, i moduli AEM richiedono ancora la directory GDS basata sul file system perché viene utilizzata per memorizzare i file permanenti e temporanei e le risorse relative alle sessioni e alle chiamate dei moduli AEM.

Quando si seleziona l&#39;opzione &quot;Abilita archiviazione documenti nel database&quot; in Impostazioni sistema core nella console di amministrazione o utilizzando Configuration Manager, i moduli AEM non consentono la modalità di backup snapshot e rollback. Pertanto, non è necessario gestire le modalità di backup utilizzando i moduli AEM. Se si utilizza questa opzione, è consigliabile eseguire il backup del GDS una sola volta dopo aver abilitato l&#39;opzione. Quando si ripristinano i moduli AEM da un backup, non è necessario rinominare la directory di backup per GDS o ripristinare GDS.

## Archivio AEM {#aem-repository}

L’archivio AEM (crx-repository) viene creato se crx-repository è configurato durante l’installazione dei moduli AEM. La posizione della directory crx-repository viene determinata durante il processo di installazione di AEM forms. Il backup e il ripristino dell’archivio AEM sono necessari insieme al database e al GDS per garantire la coerenza dei dati dei moduli AEM nei moduli AEM. L’archivio AEM contiene dati per la soluzione per la gestione della corrispondenza, Forms Manager e AEM Forms Workspace.

### Soluzione per la gestione della corrispondenza {#correspondence-management-solution}

La soluzione per la gestione della corrispondenza centralizza e gestisce la creazione, l&#39;assemblaggio e la distribuzione di corrispondenza sicura, personalizzata e interattiva. Consente di assemblare rapidamente la corrispondenza dai contenuti pre-approvati e personalizzati in un processo semplificato, dalla creazione all’archiviazione. In questo modo, i vostri clienti ottengono comunicazioni tempestive, accurate, convenienti, sicure e pertinenti. La vostra azienda ottimizza il valore delle interazioni con i clienti e riduce al minimo costi e rischi grazie a un processo semplificato per la facilità, la velocità e la produttività.

Una configurazione di una soluzione per la gestione della corrispondenza semplice include un’istanza di authoring e un’istanza di pubblicazione sullo stesso computer o su computer diversi

### gestione moduli {#forms-manager}

gestione moduli semplifica il processo di aggiornamento, gestione e ritiro dei moduli.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace corrisponde alle funzionalità di (obsoleto per i moduli AEM su JEE) Flex Workspace e aggiunge nuove funzionalità per estendere e integrare Workspace e renderlo più semplice da usare.

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

Consente la gestione delle attività sui client senza Flash Player e Adobe Reader. Semplifica il rendering di HTML Forms, oltre ai PDF forms e ai moduli Flex.

## Database dei moduli AEM {#aem-forms-database}

Il database dei moduli AEM memorizza il contenuto, ad esempio gli artefatti dei moduli, le configurazioni dei servizi, lo stato del processo e i riferimenti ai file contenuti nel GDS e nella directory principale di archiviazione dei contenuti (per Content Services). I backup del database possono essere eseguiti in tempo reale senza interruzioni del servizio e il ripristino può essere eseguito in un determinato momento o a una specifica modifica. In questa sezione viene descritto come configurare il database in modo che possa essere sottoposto a backup in tempo reale.

Su un sistema AEM forms configurato correttamente, l&#39;amministratore di sistema e l&#39;amministratore del database possono collaborare facilmente per ripristinare il sistema a uno stato coerente e noto.

Per eseguire il backup del database in tempo reale, è necessario utilizzare la modalità snapshot o configurare il database per l&#39;esecuzione nella modalità log specificata. In questo modo è possibile eseguire il backup dei file di database mentre il database è aperto e disponibile per l&#39;uso. Inoltre, il database conserva il rollback e i registri delle transazioni quando è in esecuzione in queste modalità.

>[!NOTE]
>
>Adobe ® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 12/31/2014. Consulta [Adobe documento sul ciclo di vita del prodotto](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configurare il database DB2 per l&#39;esecuzione in modalità log archivio.

>[!NOTE]
>
>Se l&#39;ambiente dei moduli AEM è stato aggiornato da una versione precedente di moduli AEM e utilizza DB2, il backup online non è supportato. In questo caso, è necessario chiudere i moduli AEM ed eseguire un backup offline. Le versioni future dei moduli AEM supporteranno il backup online per i clienti che eseguono l&#39;aggiornamento.

IBM dispone di una suite di strumenti e sistemi di assistenza che consentono agli amministratori di database di gestire le attività di backup e ripristino:

* IBM DB2 Archive Log Accelerator
* Esperto di IBM DB2 Data Archive

DB2 dispone di funzionalità incorporate per eseguire il backup di un database in Tivoli Storage Manager. Utilizzando Tivoli Storage Manager, i backup DB2 possono essere archiviati su altri supporti o sul disco rigido locale.

### Oracle {#oracle}

Utilizza i backup delle copie istantanee o configura il database Oracle per l’esecuzione in modalità registro archivio. (Vedi [Backup Oracle: Introduzione](https://www.databasedesign-resource.com/oracle-backup.md).) Per ulteriori informazioni sul backup e il ripristino del database Oracle, visitare i seguenti siti:

[Oracle di backup e ripristino:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Vengono illustrati i concetti di backup e ripristino e le tecniche più comuni per l&#39;utilizzo di Recovery Manager (RMAN) per il backup, il ripristino e il reporting in modo più dettagliato e vengono fornite ulteriori informazioni su come pianificare una strategia di backup e ripristino.

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Fornisce informazioni approfondite sull&#39;architettura RMAN, sui concetti e i meccanismi di backup e ripristino, sulle tecniche di ripristino avanzate, quali il ripristino point-in-time e le funzionalità di flashback del database, nonché sul tuning delle prestazioni di backup e ripristino. Vengono inoltre trattati i processi di backup e ripristino gestiti dall&#39;utente, utilizzando le funzionalità del sistema operativo host anziché RMAN. Questo volume è essenziale per il backup e il ripristino di implementazioni di database più sofisticate e per scenari di ripristino avanzati.

[Oracle di riferimento per il backup e il recupero del database:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Fornisce informazioni complete sulla sintassi e la semantica di tutti i comandi RMAN e descrive le visualizzazioni del database disponibili per il reporting sulle attività di backup e recupero.

### SQL Server {#sql-server}

Utilizzare i backup snapshot o configurare il database SQL Server per l&#39;esecuzione in modalità log delle transazioni.

SQL Server fornisce inoltre due strumenti di backup e ripristino:

* Interfaccia grafica di SQL Server Management Studio
* T-SQL (riga di comando)

Per ulteriori informazioni, vedere [Backup e ripristino](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilizzare MySQLAdmin o modificare i file INI in Windows per configurare il database MySQL in modo che venga eseguito in modalità di log binaria. (Vedi [Registrazione binaria MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) È inoltre disponibile uno strumento di backup a caldo per MySQL dal software InnoBase. (Vedi [Backup a caldo Innobase](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>La modalità di registrazione binaria predefinita per MySQL è &quot;Statement&quot;, incompatibile con le tabelle utilizzate da Content Services (obsoleto). Se si utilizza la registrazione binaria in questa modalità predefinita, Content Services (obsoleto) non riesce. Se il sistema include Content Services (obsoleto), utilizza la modalità di registrazione &quot;Mista&quot;. Per abilitare la registrazione &quot;mista&quot;, aggiungere il seguente argomento al file my.ini: `binlog_format=mixed log-bin=logname`

È possibile utilizzare l&#39;utilità mysqldump per ottenere il backup completo del database. I backup completi sono necessari, ma non sempre sono comodi. Producono file di backup di grandi dimensioni e richiedono tempo per la generazione. Per eseguire un backup incrementale, assicurarsi di avviare il server con l&#39;opzione - `log-bin` come descritto nella sezione precedente. Ogni volta che il server MySQL viene riavviato, smette di scrivere nel registro binario corrente, ne crea uno nuovo e, da quel momento in poi, quello nuovo diventa quello corrente. È possibile forzare un&#39;opzione manualmente con il comando `FLUSH LOGS SQL`. Dopo il primo backup completo, i successivi backup incrementali vengono eseguiti utilizzando l&#39;utilità mysqladmin con il comando `flush-logs`, che crea il file di log successivo.

Consulta [Riepilogo strategia di backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directory principale di archiviazione dei contenuti (solo Content Services) {#content-storage-root-directory-content-services-only}

La directory principale di archiviazione dei contenuti contiene l&#39;archivio Content Services (obsoleto) in cui sono archiviati tutti i documenti, gli artefatti e gli indici. È necessario eseguire il backup della struttura di directory radice dell&#39;archiviazione dei contenuti. In questa sezione viene descritto come determinare la posizione della directory principale di archiviazione dei contenuti per gli ambienti standalone e cluster.

### Percorso directory principale di archiviazione dei contenuti (ambiente autonomo) {#content-storage-root-location-stand-alone-environment}

La directory principale di archiviazione dei contenuti viene creata quando è installato Content Services (obsoleto). La posizione della directory principale di archiviazione dei contenuti viene determinata durante il processo di installazione dei moduli AEM.

Il percorso predefinito per la directory radice dell&#39;archiviazione dei contenuti è `[aem-forms root]/lccs_data`.

Eseguire il backup delle seguenti directory nella directory principale di archiviazione dei contenuti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, eseguire il backup della directory /lucene-indexes, anche nella directory radice di archiviazione dei contenuti. Se la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes in quanto potrebbe causare errori.

### Percorso directory principale di archiviazione dei contenuti (ambiente in cluster) {#content-storage-root-location-clustered-environment}

Quando si installa Content Services (obsoleto) in un ambiente cluster, la directory principale di archiviazione dei contenuti viene divisa in due directory separate:

**Directory radice archiviazione contenuto:** In genere, una directory di rete condivisa accessibile in lettura/scrittura per tutti i nodi del cluster

**Directory principale indice:** Directory creata in ogni nodo del cluster, con sempre lo stesso percorso e lo stesso nome di directory

Il percorso predefinito per la directory radice dell&#39;archiviazione dei contenuti è `[GDS root]/lccs_data`, dove `[GDS root]` è il percorso descritto in [percorso GDS](files-back-recover.md#gds-location). Eseguire il backup delle seguenti directory nella directory principale di archiviazione dei contenuti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, eseguire il backup della directory /lucene-indexes, anche nella directory radice di archiviazione dei contenuti. Se la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes in quanto potrebbe causare errori.

La posizione predefinita per la directory radice indice è `[aem-forms root]/lucene-indexes` su ciascun nodo.

## Font installati dal cliente {#customer-installed-fonts}

Se nell&#39;ambiente dei moduli AEM sono stati installati altri tipi di carattere, è necessario eseguirne separatamente il backup. Esegui il backup di tutte le directory dei font di Adobe e cliente specificate nella console di amministrazione in Impostazioni > Sistema core > Configurazioni. Assicurarsi di eseguire il backup dell&#39;intera directory dei caratteri.

>[!NOTE]
>
>Per impostazione predefinita, i tipi di carattere Adobe installati con i moduli AEM si trovano nella directory `[aem-forms root]/fonts`.

Se si sta reinizializzando il sistema operativo sul computer host e si desidera utilizzare i caratteri del sistema operativo precedente, è necessario eseguire anche il backup del contenuto della directory dei caratteri del sistema. Per istruzioni specifiche, consultare la documentazione del sistema operativo in uso.
