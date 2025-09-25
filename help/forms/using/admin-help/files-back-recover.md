---
title: File da sottoporre a backup e da ripristinare
description: Questo documento descrive l’applicazione e i file di dati di cui è necessario eseguire il backup.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '2029'
ht-degree: 100%

---

# File da sottoporre a backup e da ripristinare {#files-to-back-up-and-recover}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

L’applicazione e i file di dati di cui è necessario eseguire il backup sono descritti più dettagliatamente nelle sezioni seguenti.

Prendi in considerazione i seguenti punti relativi al backup e al ripristino:

* Il backup del database deve essere eseguito prima di GDS e dell’archivio AEM.
* Se è necessario disattivare i nodi di un ambiente cluster per il backup, verifica che i nodi secondari vengano arrestati prima del nodo principale. In caso contrario, potrebbe causare incoerenza nel cluster o nel server. Inoltre, il nodo principale deve essere reso attivo prima di qualsiasi nodo secondario.
* Per l’operazione di ripristino di un cluster, è necessario arrestare il server applicazioni per ogni nodo del cluster.

## Directory di archiviazione globale dei documenti {#global-document-storage-directory}

GDS è una directory utilizzata per archiviare i file di lunga durata utilizzati all’interno di un processo. Il ciclo di vita dei file di lunga durata si estende su uno o più avvii di un sistema AEM Forms e può estendersi su giorni e persino anni. Questi file di lunga durata possono includere PDF, criteri e modelli di modulo. I file di lunga durata sono una parte fondamentale dello stato complessivo di molte distribuzioni di AEM Forms. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server Forms potrebbe diventare instabile.

I documenti di input per la chiamata asincrona del processo sono archiviati anche in GDS e devono essere disponibili per elaborare le richieste. È quindi importante considerare l’affidabilità del file system che ospita il GDS e utilizzare un array ridondante di dischi indipendenti (RAID) o altra tecnologia appropriata per soddisfare i requisiti di qualità e livello di servizio.

La posizione del GDS viene determinata durante il processo di installazione di AEM Forms o successivamente utilizzando la console di amministrazione. Oltre a mantenere una posizione di elevata disponibilità per GDS, è possibile abilitare anche l’archiviazione del database per i documenti. Consulta [Opzioni di backup quando il database viene utilizzato per l’archiviazione dei documenti](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Posizione GDS {#gds-location}

Lasciando vuota l’impostazione relativa al percorso durante l’installazione, per impostazione predefinita viene utilizzata una directory nell’installazione del server applicazioni. Esegui il backup della seguente directory per il server applicazioni:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se la posizione GDS è stata modificata in una posizione non predefinita, è possibile determinarla nel modo seguente:

* Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
* Registra il percorso specificato nella casella Directory di archiviazione documenti globale.

In un ambiente cluster, GDS in genere punta a una directory condivisa in rete e accessibile in lettura/scrittura per ogni nodo cluster.

La posizione di GDS può essere modificata durante un ripristino se quella originale non è più disponibile. (Consulta [Modificare il percorso GDS durante il ripristino](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)).

### Opzioni di backup quando il database viene utilizzato per l’archiviazione dei documenti {#backup-options-when-database-is-used-for-document-storage}

È possibile abilitare l’archiviazione dei documenti di AEM Forms nel database di AEM Forms utilizzando la console di amministrazione. Anche se questa opzione mantiene tutti i documenti persistenti nel database, AEM Forms richiede ancora la directory GDS basata sul file system perché viene utilizzata per archiviare i file permanenti e temporanei e le risorse relative alle sessioni e alle chiamate di AEM Forms.

Selezionando l’opzione “Abilita archiviazione documenti nel database” in Impostazioni sistema core nella console di amministrazione o utilizzando Configuration Manager, AEM Forms non consente la modalità di backup snapshot e di rollback. Pertanto, non è necessario gestire le modalità di backup utilizzando AEM Forms. Se utilizzi questa opzione, è consigliabile eseguire il backup di GDS una sola volta dopo aver abilitato l’opzione. Quando ripristini AEM Forms da un backup, non è necessario rinominare la directory di backup per GDS o ripristinare GDS.

## Archivio AEM {#aem-repository}

L’archivio AEM (crx-repository) viene creato se crx-repository è configurato durante l’installazione di AEM Forms. La posizione della directory crx-repository viene determinata durante il processo di installazione di AEM Forms. Per garantire la coerenza dei dati dei moduli AEM in AEM Forms, è necessario eseguire il backup e il ripristino dell’archivio AEM insieme al database e a GDS. L’archivio AEM contiene dati per la soluzione di gestione della corrispondenza, Forms Manager e AEM Forms Workspace.

### Soluzione di gestione della corrispondenza {#correspondence-management-solution}

La Soluzione di gestione della corrispondenza centralizza e gestisce la creazione, l’assemblaggio e la distribuzione di corrispondenza sicura, personalizzata e interattiva. Consente di assemblare rapidamente la corrispondenza dai contenuti pre-approvati e personalizzati in un processo semplificato, dalla creazione all’archiviazione. In questo modo, la clientela ottiene comunicazioni tempestive, accurate, convenienti, sicure e pertinenti. L’azienda ottimizza il valore delle interazioni con la clientela e riduce al minimo costi e rischi grazie a un processo semplificato per la facilità, la velocità e la produttività.

Una semplice configurazione di una soluzione di gestione della corrispondenza include un’istanza di authoring e un’istanza di pubblicazione sullo stesso computer o su computer diversi

### Gestione moduli {#forms-manager}

gestione moduli semplifica il processo di aggiornamento, gestione e ritiro dei moduli.

### Area di lavoro di AEM Forms {#html-workspace}

AEM Forms Workspace corrisponde alle funzionalità di (obsoleto per AEM Forms su JEE) Flex Workspace e aggiunge nuove funzionalità per estendere e integrare Workspace e renderlo più semplice da usare.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

Consente la gestione delle attività sui client senza Flash Player e Adobe Reader. Semplifica il rendering di HTML Forms, oltre a PDF forms e Flex Forms.

## Database di AEM Forms {#aem-forms-database}

Il database di AEM Forms memorizza il contenuto, ad esempio gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti del database ai file presenti in GDS e nella directory principale di archiviazione dei contenuti (per Content Services). I backup del database possono essere eseguiti in tempo reale senza interruzioni del servizio e il ripristino può essere eseguito in un determinato momento o per una specifica modifica. Questa sezione descrive come configurare il database in modo che possa essere sottoposto a backup in tempo reale.

Su un sistema AEM Forms configurato correttamente, l’amministratore di sistema e l’amministratore del database possono collaborare facilmente per ripristinare il sistema a uno stato coerente e noto.

Per eseguire il backup del database in tempo reale, è necessario utilizzare la modalità snapshot o configurare il database per l’esecuzione nella modalità di registro specificata. In questo modo è possibile eseguire il backup dei file di database mentre il database è aperto e disponibile per l’uso. Inoltre, il database conserva il rollback e i registri delle transazioni quando è in esecuzione in queste modalità.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Consulta [il documento sul ciclo di vita del prodotto Adobe](https://helpx.adobe.com/it/support/programs/eol-matrix.html).

### DB2 {#db2}

Configurare il database DB2 per l’esecuzione in modalità registro di archivio.

>[!NOTE]
>
>Se l’ambiente AEM Forms è stato aggiornato da una versione precedente di AEM Forms e utilizza DB2, il backup online non è supportato. In questo caso, è necessario arrestare AEM Forms ed eseguire un backup offline. Le versioni future di AEM Forms supporteranno il backup online per i clienti che eseguono l’aggiornamento.

IBM dispone di una suite di strumenti e sistemi di assistenza che consentono agli amministratori di database di gestire le attività di backup e ripristino:

* IBM DB2 Archive Log Accelerator
* IBM DB2 Data Archive Expert

DB2 dispone di funzionalità incorporate per eseguire il backup di un database in Tivoli Storage Manager. Utilizzando Tivoli Storage Manager, i backup DB2 possono essere archiviati su altri supporti o sul disco rigido locale.

### Oracle {#oracle}

Utilizza i backup delle copie istantanee o configura il database Oracle per l’esecuzione in modalità registro archivio. (Consulta [Backup di Oracle: introduzione](https://www.databasedesign-resource.com/oracle-backup.md)). Per ulteriori informazioni sul backup e il ripristino del database di Oracle, visita i seguenti siti:

[Backup e ripristino di Oracle:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) illustra i concetti di backup e ripristino e le tecniche più comuni per l’utilizzo di Recovery Manager (RMAN) per il backup, il ripristino e il reporting in modo più dettagliato e fornisce ulteriori informazioni su come pianificare una strategia di backup e ripristino.

[Guida per l’utente al backup e ripristino del database di Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) fornisce informazioni approfondite sull’architettura RMAN, sui concetti e i meccanismi di backup e ripristino, sulle tecniche di ripristino avanzate, quali il ripristino in un momento preciso e le funzionalità di flashback del database, nonché sull’ottimizzazione delle prestazioni di backup e ripristino. Vengono inoltre trattati i processi di backup e ripristino gestiti dall’utente, utilizzando le funzionalità del sistema operativo host anziché RMAN. Questo volume è essenziale per il backup e il ripristino di implementazioni di database più sofisticate e per scenari di ripristino avanzati.

[Riferimento per il backup e il recupero del database di Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) fornisce informazioni complete sulla sintassi e la semantica di tutti i comandi RMAN e descrive le visualizzazioni del database disponibili per il reporting sulle attività di backup e recupero.

### SQL Server {#sql-server}

Utilizza i backup snapshot o configurare il database SQL Server per l’esecuzione in modalità registro delle transazioni.

SQL Server fornisce inoltre due strumenti di backup e ripristino:

* Interfaccia grafica di SQL Server Management Studio
* T-SQL (riga di comando)

Per ulteriori informazioni, consulta [Backup e ripristino](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilizza MySQLAdmin o modifica i file INI in Windows per configurare il database MySQL in modo che venga eseguito in modalità registro binario. Consulta [Registrazione binaria MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html). È disponibile anche uno strumento di backup a caldo per MySQL dal software InnoBase. Consulta [Backup a caldo Innobase](https://www.innodb.com/hot-backup/features.md).

>[!NOTE]
>
>La modalità di registrazione binaria predefinita per MySQL è “Istruzioni”, che non è compatibile con le tabelle utilizzate da Content Services (obsoleto). Se utilizzi la registrazione binaria in questa modalità predefinita, Content Services (obsoleto) non riesce. Se il sistema include Content Services (obsoleto), utilizza la modalità di registrazione “Mista”. Per abilitare la registrazione “Mista”, aggiungi il seguente argomento al file my.ini: `binlog_format=mixed log-bin=logname`

Per ottenere il backup completo del database, è possibile utilizzare l’utilità mysqldump. I backup completi sono necessari, ma non sempre sono pratici. Producono file di backup di grandi dimensioni e richiedono tempo per la generazione. Per eseguire un backup incrementale, assicurati di avviare il server con l’opzione - `log-bin` come descritto nella sezione precedente. Ogni volta che il server MySQL viene riavviato, smette di scrivere nel registro binario corrente, ne crea uno nuovo e, da quel momento in poi, quello nuovo diventa quello corrente. È possibile forzare un’opzione manualmente con il comando `FLUSH LOGS SQL`. Dopo il primo backup completo, i backup incrementali successivi vengono eseguiti utilizzando l’utilità mysqladmin con il comando `flush-logs`, che crea il file di registro successivo.

Consulta [Riepilogo sulla strategia di backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directory principale di archiviazione dei contenuti (solo Content Services) {#content-storage-root-directory-content-services-only}

La directory principale di archiviazione dei contenuti contiene l’archivio Content Services (obsoleto) in cui sono archiviati tutti i documenti, gli artefatti e gli indici. È necessario eseguire il backup della struttura della directory principale dell’archiviazione dei contenuti. In questa sezione viene descritto come determinare la posizione della directory principale di archiviazione dei contenuti per gli ambienti autonomi e cluster.

### Percorso directory principale di archiviazione dei contenuti (ambiente autonomo) {#content-storage-root-location-stand-alone-environment}

La directory principale di archiviazione dei contenuti viene creata quando è installato Content Services (obsoleto). Il percorso della directory principale di archiviazione dei contenuti viene determinato durante il processo di installazione di AEM Forms.

Il percorso predefinito per la directory principale di archiviazione dei contenuti è `[aem-forms root]/lccs_data`.

Nella directory principale di archiviazione dei contenuti, esegui il backup delle directory seguenti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, esegui il backup della directory /lucene-indexes, anche nella directory principale di archiviazione dei contenuti. Se invece la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes in quanto potrebbe causare errori.

### Percorso directory principale di archiviazione dei contenuti (ambiente cluster) {#content-storage-root-location-clustered-environment}

Quando installi Content Services (obsoleto) in un ambiente cluster, la directory principale di archiviazione dei contenuti viene suddivisa in due directory separate:

**Directory principale archiviazione dei contenuti:** in genere, una directory di rete condivisa accessibile in lettura/scrittura per tutti i nodi del cluster

**Directory principale indice:** directory creata in ogni nodo del cluster, con sempre lo stesso percorso e lo stesso nome di directory

Il percorso predefinito per la directory principale di archiviazione dei contenuti è `[GDS root]/lccs_data`, dove `[GDS root]` è il percorso descritto in [percorso GDS](files-back-recover.md#gds-location). Nella directory principale di archiviazione dei contenuti, esegui il backup delle directory seguenti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, esegui il backup della directory /lucene-indexes, anche nella directory principale di archiviazione dei contenuti. Se invece la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes in quanto potrebbe causare errori.

Il percorso predefinito per la directory principale dell’indice è `[aem-forms root]/lucene-indexes` su ciascun nodo.

## Font installati dal cliente {#customer-installed-fonts}

Se nell&#39;ambiente AEM Form sono stati installati altri tipi di font, è necessario eseguirne il backup separatamente. Esegui il backup di tutte le directory dei font di Adobe e del cliente specificate nella console di amministrazione in Impostazioni > Sistema di base > Configurazioni. Assicurati di eseguire il backup dell’intera directory dei font.

>[!NOTE]
>
>Per impostazione predefinita, i font di Adobe installati con AEM Forms si trovano nella directory `[aem-forms root]/fonts`.

Se stai inizializzando nuovamente il sistema operativo sul computer host e desideri utilizzare i font del sistema operativo precedente, è necessario eseguire anche il backup del contenuto della directory dei font del sistema. Per istruzioni specifiche, consulta la documentazione del sistema operativo in uso.
