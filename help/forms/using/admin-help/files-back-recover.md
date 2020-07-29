---
title: File per il backup e il ripristino
seo-title: File per il backup e il ripristino
description: Questo documento descrive l’applicazione e i file di dati da sottoporre a backup.
seo-description: Questo documento descrive l’applicazione e i file di dati da sottoporre a backup.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: ac3d18bf0b39efbe927c10aef557296140628e19
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# File per il backup e il ripristino {#files-to-back-up-and-recover}

I file di applicazione e di dati da sottoporre a backup sono descritti più dettagliatamente nelle sezioni seguenti.

Considerare i seguenti punti relativi a backup e ripristino:

* Il backup del database deve essere eseguito prima di GDS e AEM repository.
* Se è necessario disattivare i nodi in un ambiente cluster cluster per il backup, assicurarsi che i nodi secondari vengano chiusi prima del nodo principale. In caso contrario, potrebbe causare incoerenza nel cluster o nel server. Inoltre, il nodo primario deve essere reso attivo prima di qualsiasi nodo secondario.
* Per l&#39;operazione di ripristino di un cluster, il server applicazione deve essere arrestato per ogni nodo del cluster.

## Directory Global Document Storage {#global-document-storage-directory}

GDS è una directory utilizzata per memorizzare i file longevi utilizzati all’interno di un processo. La durata dei file di lunga durata ha lo scopo di estendere uno o più avvii di un sistema di moduli AEM e può estendersi su giorni e anni. Questi file di lunga durata possono includere PDF, criteri e modelli di modulo. I file di lunga durata rappresentano una parte fondamentale dello stato generale di molte distribuzioni di moduli AEM. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server dei moduli potrebbe diventare instabile.

I documenti di input per la chiamata asincrona del processo sono inoltre memorizzati nel GDS e devono essere disponibili per l’elaborazione delle richieste. Pertanto, è importante considerare l&#39;affidabilità del file system che ospita il GDS e utilizzare un array ridondante di dischi indipendenti (RAID) o altre tecnologie, in base alla qualità e al livello di servizio richiesti.

La posizione del GDS è determinata durante il processo di installazione dei moduli AEM o successivamente utilizzando la console di amministrazione. Oltre a mantenere una posizione di elevata disponibilità per GDS, puoi anche abilitare la memorizzazione del database per i documenti. Vedere Opzioni [di backup quando il database viene utilizzato per l&#39;archiviazione](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)dei documenti.

### Posizione GDS {#gds-location}

Se lasciate vuota l&#39;impostazione del percorso durante l&#39;installazione, per impostazione predefinita il percorso corrisponde a una directory nell&#39;installazione del server dell&#39;applicazione. È necessario eseguire il backup della seguente directory per il server applicazione:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se avete modificato la posizione GDS in una posizione non predefinita, potete determinarla come segue:

* Accedete alla console di amministrazione e fate clic su Impostazioni > Impostazioni di sistema principali > Configurazioni.
* Registrare il percorso specificato nella casella Directory di archiviazione documenti globale.

In un ambiente cluster, il GDS in genere punta a una directory condivisa in rete e accessibile in lettura/scrittura per ogni nodo del cluster.

Se la posizione originale non è più disponibile, la posizione del GDS può essere modificata durante il ripristino. (Vedere [Modifica della posizione GDS durante il ripristino](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti {#backup-options-when-database-is-used-for-document-storage}

È possibile abilitare l&#39;archiviazione dei documenti AEM moduli nel database dei moduli AEM utilizzando la console di amministrazione. Anche se questa opzione mantiene tutti i documenti persistenti nel database, AEM moduli richiede comunque la directory GDS basata su file system, perché viene utilizzata per memorizzare file e risorse permanenti e temporanee correlate alle sessioni e alle chiamate dei moduli AEM.

Se si seleziona l&#39;opzione &quot;Abilita archiviazione documenti nel database&quot; nelle Impostazioni di sistema principali nella console di amministrazione o utilizzando Configuration Manager, AEM moduli non consentono la modalità di backup snapshot e la modalità di backup rollout. Pertanto, non è necessario gestire le modalità di backup utilizzando AEM moduli. Se utilizzate questa opzione, è necessario eseguire il backup di GDS solo una volta dopo aver attivato l&#39;opzione. Quando si ripristinano AEM moduli da un backup, non è necessario rinominare la directory di backup per GDS o ripristinare GDS.

## AEM repository {#aem-repository}

AEM repository (crx-repository) viene creato se è configurato crx-repository durante l&#39;installazione AEM moduli. La posizione della directory del repository crx è determinata durante il processo di installazione dei moduli AEM. AEM repository è necessario eseguire il backup e il ripristino, insieme al database e al GDS, per garantire la coerenza dei dati AEM moduli nei moduli AEM. AEM repository contiene i dati per la soluzione di gestione della corrispondenza, Forms Manager e l&#39;area di lavoro AEM Forms.

### Soluzione per la gestione della corrispondenza {#correspondence-management-solution}

La soluzione di gestione della corrispondenza centralizza e gestisce la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive. Consente di assemblare rapidamente la corrispondenza da contenuti già approvati e personalizzati in un processo semplificato, dalla creazione all’archiviazione. Di conseguenza, i clienti ottengono comunicazioni tempestive, accurate, pratiche, sicure e pertinenti. La vostra azienda massimizza il valore delle interazioni con i clienti e minimizza costi e rischi con un processo ottimizzato per facilità, velocità e produttività.

Una semplice configurazione della soluzione di gestione della corrispondenza include un&#39;istanza di creazione e un&#39;istanza di pubblicazione sullo stesso computer o su computer diversi

### forms manager {#forms-manager}

gestione moduli semplifica il processo di aggiornamento, gestione e ritiro dei moduli.

### Area di lavoro AEM Forms {#html-workspace}

AEM Forms Workspace combina le funzionalità di Flex Workspace (obsoleto per i moduli AEM su JEE) e aggiunge nuove funzionalità per estendere e integrare Workspace e renderlo più semplice da usare.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

Consente la gestione delle attività sui client senza Flash Player e  Adobe Reader. Consente la rappresentazione di HTML Forms, oltre ai PDF forms e ai moduli Flex.

## database moduli AEM {#aem-forms-database}

Il database dei moduli AEM memorizza il contenuto, ad esempio artefatti del modulo, configurazioni del servizio, stato del processo e riferimenti al database, nei file GDS e nella directory principale di Content Storage (per Content Services). I backup del database possono essere eseguiti in tempo reale senza interruzione del servizio e il ripristino può essere effettuato in un momento specifico o in un momento specifico. Questa sezione descrive come configurare il database in modo che possa essere sottoposto a backup in tempo reale.

In un sistema AEM moduli configurato correttamente, l&#39;amministratore di sistema e l&#39;amministratore di database possono collaborare facilmente per ripristinare lo stato del sistema in modo coerente e noto.

Per eseguire il backup del database in tempo reale, è necessario utilizzare la modalità snapshot o configurare il database per l&#39;esecuzione in modalità log specificata. Questo consente il backup dei file di database mentre il database è aperto e disponibile per l&#39;uso. Inoltre, il database mantiene il rollback e i log delle transazioni quando è in esecuzione in queste modalità.

>[!NOTE]
>
> Adobe® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle LiveCycle®. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulle persone. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Consulta [documento](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)sul ciclo di vita del prodotto di Adobe. Per informazioni sulla configurazione di Content Services (obsoleto), consulta [Amministrazione di Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

### DB2 {#db2}

Configurare il database DB2 per l&#39;esecuzione in modalità log di archivio.

>[!NOTE]
>
>Se l&#39;ambiente AEM dei moduli è stato aggiornato da una versione precedente di AEM moduli e utilizza DB2, il backup online non è supportato. In questo caso, è necessario chiudere AEM moduli ed eseguire un backup offline. Le versioni future dei moduli AEM supporteranno il backup online per i clienti che effettuano l&#39;aggiornamento.

IBM dispone di una suite di strumenti e sistemi di aiuto per aiutare gli amministratori di database a gestire le attività di backup e ripristino:

* IBM DB2 Archive Log Accelerator (vedere [IBM DB2 Archive Log Accelerator per z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true)).
* IBM DB2 Data Archive Expert (vedere [IBM DB2 Data Archive Expert User&#39;s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)).

DB2 dispone di funzionalità integrate per il backup di un database su Tivoli Storage Manager. Utilizzando Tivoli Storage Manager, i backup DB2 possono essere memorizzati su altri supporti o sul disco rigido locale.

Per ulteriori informazioni sul backup e il ripristino del database DB2, vedere [Sviluppo di una strategia di backup e ripristino per DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm).

### Oracle {#oracle}

Utilizzare i backup degli snapshot o configurare il database Oracle per l&#39;esecuzione in modalità log di archivio. (Vedere [Oracle Backup: Introduzione](https://www.databasedesign-resource.com/oracle-backup.md).) Per ulteriori informazioni sul backup e il ripristino del database Oracle, visitare i seguenti siti:

[Backup e ripristino Oracle:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Illustra i concetti di backup e ripristino e le tecniche più comuni per utilizzare Recovery Manager (RMAN) per backup, ripristino e reporting in modo più dettagliato, oltre a fornire ulteriori informazioni su come pianificare una strategia di backup e ripristino.

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Fornisce informazioni approfondite sull&#39;architettura RMAN, sui concetti e sui meccanismi di backup e ripristino, sulle tecniche di ripristino avanzate come il ripristino point-in-time e le funzionalità di flashback del database, nonché sul tuning delle prestazioni di backup e ripristino. Vengono inoltre trattati il backup e il ripristino gestiti dall&#39;utente, utilizzando le strutture del sistema operativo host invece di RMAN. Questo volume è essenziale per il backup e il ripristino di installazioni di database più sofisticate e per scenari di ripristino avanzati.

[Riferimento per backup e ripristino del database Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Fornisce informazioni complete sulla sintassi e la semantica per tutti i comandi RMAN e descrive le visualizzazioni del database disponibili per il reporting sulle attività di backup e ripristino.

### SQL Server {#sql-server}

Utilizzare i backup degli snapshot o configurare il database SQL Server per l&#39;esecuzione in modalità log delle transazioni.

SQL Server offre inoltre due strumenti di backup e ripristino:

* SQL Server Management Studio (GUI)
* T-SQL (riga di comando)

Per ulteriori informazioni, vedere [Backup e ripristino](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilizzare MySQLAdmin o modificare i file INI in Windows per configurare il database MySQL da eseguire in modalità di registro binario. Consultate Registrazione [binaria](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)MySQL. Uno strumento di backup a caldo per MySQL è disponibile anche dal software InnoBase. (Vedete Backup [a caldo](https://www.innodb.com/hot-backup/features.md)Innobase.)

>[!NOTE]
>
>La modalità di registrazione binaria predefinita per MySQL è &quot;Istruzione&quot;, incompatibile con le tabelle utilizzate da Content Services (obsoleto). L&#39;utilizzo della registrazione binaria in questa modalità predefinita causa la mancata riuscita di Content Services (obsoleto). Se il sistema include Content Services (obsoleto), utilizza la modalità di registrazione &quot;mista&quot;. Per abilitare la registrazione &quot;mista&quot;, aggiungete il seguente argomento al file my.ini file:*
`binlog_format=mixed log-bin=logname`

È possibile utilizzare l&#39;utility mysqldump per ottenere il backup completo del database. I backup completi sono necessari, ma non sempre sono convenienti. Producono file di backup di grandi dimensioni e richiedono tempo per la generazione. Per eseguire un backup incrementale, assicurarsi di avviare il server con l&#39;opzione - `log-bin` come descritto nella sezione precedente. Ogni volta che il server MySQL si riavvia, interrompe la scrittura nel registro binario corrente, ne crea uno nuovo e, da quel momento in poi, quello nuovo diventa quello corrente. È possibile forzare un interruttore manualmente con il `FLUSH LOGS SQL` comando. Dopo il primo backup completo, i successivi backup incrementali vengono eseguiti utilizzando l&#39;utility mysqladmin con il `flush-logs` comando, che crea il file di registro successivo.

Consulta Riepilogo strategia di [backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directory principale dell&#39;archivio contenuti (solo Content Services) {#content-storage-root-directory-content-services-only}

La directory principale di Content Storage contiene l&#39;archivio di Content Services (obsoleto) in cui sono memorizzati tutti i documenti, gli artefatti e gli indici. È necessario eseguire il backup della struttura di directory principale dell&#39;archivio contenuti. In questa sezione viene descritto come determinare la posizione della directory principale di memorizzazione dei contenuti per gli ambienti sia standalone che cluster.

### Posizione di origine dell&#39;archiviazione dei contenuti (ambiente autonomo) {#content-storage-root-location-stand-alone-environment}

La directory principale dell&#39;archivio contenuti viene creata quando è installato Content Services (obsoleto). La posizione della directory principale di memorizzazione dei contenuti è determinata durante il processo di installazione dei moduli AEM.

Il percorso predefinito per la directory principale dell&#39;archiviazione dei contenuti è `[aem-forms root]/lccs_data`.

Esegui il backup delle seguenti directory che si trovano nella directory principale di Content Storage:

/audit.contentstore

/contentStore

/contentstore.deleted

/backup-lucene-index

Se la directory /backup-lucene-indexes non è presente, eseguite il backup della directory /lucene-indexes, anch&#39;essa presente nella directory principale dell&#39;archiviazione dei contenuti. Se la directory /backup-lucene-index è presente, non eseguire il backup della directory /lucene-index perché potrebbe causare errori.

### Posizione radice memorizzazione contenuto (ambiente cluster) {#content-storage-root-location-clustered-environment}

Quando installate Content Services (obsoleto) in un ambiente cluster, la directory principale di Content Storage viene suddivisa in due directory separate:

**Directory principale dell&#39;archivio contenuti:** In genere, una directory di rete condivisa con accesso in lettura/scrittura per tutti i nodi del cluster

**Directory radice indice:** Una directory creata su ciascun nodo del cluster, sempre con lo stesso percorso e lo stesso nome di directory

Il percorso predefinito per la directory principale dell&#39;archivio dei contenuti è `[GDS root]/lccs_data`, dove `[GDS root]` si trova il percorso descritto nel percorso [](files-back-recover.md#gds-location)GDS. Esegui il backup delle seguenti directory che si trovano nella directory principale di Content Storage:

/audit.contentstore

/contentStore

/contentstore.deleted

/backup-lucene-index

Se la directory /backup-lucene-indexes non è presente, eseguite il backup della directory /lucene-indexes, anch&#39;essa presente nella directory principale dell&#39;archiviazione dei contenuti. Se la directory /backup-lucene-index è presente, non eseguire il backup della directory /lucene-index perché potrebbe causare errori.

La posizione predefinita per la directory radice dell&#39;indice è `[aem-forms root]/lucene-indexes` su ciascun nodo.

## Font installati dal cliente {#customer-installed-fonts}

Se sono stati installati font aggiuntivi nell&#39;ambiente AEM moduli, è necessario eseguire il backup separatamente. Esegui il backup di tutte  directory di Adobi e di font cliente specificate nella console di amministrazione in Impostazioni > Sistema di base > Configurazioni. Assicurarsi di eseguire il backup dell&#39;intera directory dei font.

>[!NOTE]
>
>Per impostazione predefinita, i font  Adobe installati con AEM moduli si trovano nella `[aem-forms root]/fonts` directory.

Se si sta reinizializzando il sistema operativo sul computer host e si desidera utilizzare i font del sistema operativo precedente, è necessario eseguire il backup anche del contenuto della directory dei font di sistema. Per istruzioni specifiche, consultate la documentazione del sistema operativo in uso.
