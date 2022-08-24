---
title: File di backup e ripristino
seo-title: Files to back up and recover
description: Questo documento descrive l'applicazione e i file di dati che devono essere sottoposti a backup.
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# File di backup e ripristino {#files-to-back-up-and-recover}

I file di applicazione e di dati che devono essere sottoposti a backup sono descritti più dettagliatamente nelle sezioni seguenti.

Considera i seguenti punti relativi al backup e al ripristino:

* Il backup del database deve essere eseguito prima di GDS e AEM repository.
* Se devi disattivare i nodi in un ambiente cluster cluster per il backup, assicurati che i nodi secondari siano spenti prima del nodo principale. In caso contrario, può causare incoerenza nel cluster o nel server. Inoltre, il nodo primario deve essere reso attivo prima di qualsiasi nodo secondario.
* Per l&#39;operazione di ripristino di un cluster, il server applicazioni deve essere arrestato per ogni nodo del cluster.

## Directory di archiviazione dei documenti globali {#global-document-storage-directory}

Il GDS è una directory utilizzata per memorizzare file longevi utilizzati all’interno di un processo. La durata dei file di lunga durata è destinata ad estendersi su uno o più lanci di un sistema di moduli AEM e può estendersi su giorni e anche anni. Questi file di lunga durata possono includere PDF, criteri e modelli di moduli. I file longevi sono una parte critica dello stato generale di molte distribuzioni di moduli AEM. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server dei moduli potrebbe diventare instabile.

I documenti di input per la chiamata asincrona del processo sono inoltre memorizzati nel GDS e devono essere disponibili per elaborare le richieste. Pertanto, è importante considerare l&#39;affidabilità del file system che ospita il GDS e utilizzare un array ridondante di dischi indipendenti (RAID) o altra tecnologia appropriata per la qualità e il livello dei requisiti di servizio.

La posizione del GDS viene determinata durante il processo di installazione dei moduli di AEM o successivamente utilizzando la console di amministrazione. Oltre a mantenere una posizione di elevata disponibilità per GDS, puoi anche abilitare la memorizzazione del database per i documenti. Vedi [Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### Posizione GDS {#gds-location}

Se l&#39;impostazione della posizione viene lasciata vuota durante l&#39;installazione, viene impostata automaticamente una directory sotto l&#39;installazione dell&#39;application server. È necessario eseguire il backup della seguente directory per il server applicazioni:

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

Se hai modificato la posizione GDS in una posizione non predefinita, puoi determinarla come segue:

* Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema di base > Configurazioni.
* Registrare il percorso specificato nella casella Directory di archiviazione globale dei documenti.

In un ambiente cluster, il GDS in genere punta a una directory condivisa sulla rete ed è accessibile in lettura/scrittura per ogni nodo del cluster.

Se la posizione originale non è più disponibile, la posizione del GDS può essere modificata durante il recupero. (Vedi [Modifica della posizione GDS durante il ripristino](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti {#backup-options-when-database-is-used-for-document-storage}

È possibile abilitare l’archiviazione dei documenti AEM moduli nel database dei moduli AEM utilizzando la console di amministrazione. Anche se questa opzione mantiene tutti i documenti persistenti nel database, AEM moduli richiede ancora la directory GDS basata su file system perché viene utilizzata per memorizzare file permanenti e temporanei e risorse relative alle sessioni e alle chiamate dei moduli AEM.

Quando si seleziona l’opzione &quot;Abilita archiviazione documenti nel database&quot; nelle impostazioni del sistema di base nella console di amministrazione o utilizzando Configuration Manager, i moduli AEM non consentono la modalità di backup delle copie istantanee e la modalità di backup continuo. Pertanto, non è necessario gestire le modalità di backup utilizzando moduli AEM. Se utilizzi questa opzione, devi eseguire il backup di GDS una sola volta dopo aver abilitato l’opzione. Quando si recuperano AEM moduli da un backup, non è necessario rinominare la directory di backup per GDS o ripristinare GDS.

## archivio AEM {#aem-repository}

AEM repository (crx-repository) viene creato se crx-repository è configurato durante l&#39;installazione AEM moduli. La posizione della directory dell&#39;archivio crx è determinata durante il processo di installazione dei moduli AEM. È necessario AEM backup e ripristino dell’archivio, insieme al database e al GDS, per garantire la coerenza dei dati dei moduli AEM nei moduli AEM. AEM archivio contiene dati per la soluzione di gestione della corrispondenza, Forms Manager e AEM Forms Workspace.

### Soluzione per la gestione della corrispondenza {#correspondence-management-solution}

La soluzione di gestione della corrispondenza centralizza e gestisce la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive. Consente di assemblare rapidamente la corrispondenza da contenuti pre-approvati e personalizzati in un processo semplificato, dalla creazione all’archiviazione. Di conseguenza, i clienti ottengono comunicazioni puntuali, precise, convenienti, sicure e pertinenti. La vostra azienda massimizza il valore delle interazioni con i clienti e riduce al minimo i costi e i rischi con un processo che sia semplificato per facilità, velocità e produttività.

Una semplice configurazione della soluzione per la gestione della corrispondenza include un&#39;istanza di authoring e un&#39;istanza di pubblicazione sullo stesso computer o su computer diversi

### Forms Manager {#forms-manager}

forms manager semplifica il processo di aggiornamento, gestione e ritiro dei moduli.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace corrisponde alle funzionalità di (obsoleto per i moduli AEM su JEE) Flex Workspace e aggiunge nuove funzionalità per estendere e integrare Workspace e renderlo più semplice da usare.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

Consente la gestione delle attività sui client senza Flash Player e Adobe Reader. Semplifica il rendering di HTML Forms, oltre ai PDF forms e ai moduli Flex.

## Database dei moduli AEM {#aem-forms-database}

Il database dei moduli AEM memorizza il contenuto, ad esempio gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti al database, nei file GDS e nella directory principale di archiviazione dei contenuti (per Content Services). I backup del database possono essere eseguiti in tempo reale senza interruzione del servizio e il ripristino può essere in un determinato momento o a una particolare modifica. Questa sezione descrive come configurare il database in modo che possa essere sottoposto a backup in tempo reale.

In un sistema di moduli AEM configurato correttamente, l&#39;amministratore di sistema e l&#39;amministratore di database possono collaborare facilmente per ripristinare il sistema a uno stato coerente e noto.

Per eseguire il backup del database in tempo reale, è necessario utilizzare la modalità snapshot o configurare il database per l&#39;esecuzione nella modalità di log specificata. Questo consente il backup dei file di database mentre il database è aperto e disponibile per l&#39;uso. Inoltre, il database conserva il suo rollback e i registri delle transazioni quando è in esecuzione in queste modalità.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con il LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare processi incentrati sulle persone. Il supporto per Content Services (obsoleto) termina il 31/12/2014. Vedi [Adobe del documento sul ciclo di vita del prodotto](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

Configura il database DB2 da eseguire in modalità log archivio.

>[!NOTE]
>
>Se l’ambiente dei moduli AEM è stato aggiornato da una versione precedente di moduli AEM e utilizza DB2, il backup online non è supportato. In questo caso, è necessario arrestare AEM moduli ed eseguire un backup offline. Le versioni future dei moduli AEM supporteranno il backup online per i clienti che eseguono l’aggiornamento.

IBM dispone di una suite di strumenti e sistemi di aiuto per aiutare gli amministratori di database a gestire le attività di backup e ripristino:

* Acceleratore di log dell&#39;archivio IBM DB2
* Esperto di IBM DB2 Data Archive

DB2 dispone di funzionalità integrate per il backup di un database su Tivoli Storage Manager. Utilizzando Tivoli Storage Manager, i backup DB2 possono essere archiviati su altri supporti o sul disco rigido locale.

### Oracle {#oracle}

Utilizzare i backup di snapshot o configurare il database di Oracle per l&#39;esecuzione in modalità di log di archiviazione. (Vedi [Oracle di backup: Introduzione](https://www.databasedesign-resource.com/oracle-backup.md).) Per ulteriori informazioni sul backup e il ripristino del database di Oracle, visitare i seguenti siti:

[Oracle di backup e ripristino:](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Illustra i concetti di backup e ripristino e le tecniche più comuni per l&#39;utilizzo di Recovery Manager (RMAN) per il backup, il ripristino e il reporting in modo più dettagliato, oltre a fornire ulteriori informazioni su come pianificare una strategia di backup e ripristino.

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Fornisce informazioni approfondite sull&#39;architettura RMAN, sui concetti e i meccanismi di backup e ripristino, sulle tecniche di ripristino avanzate, come il ripristino point-in-time e le funzionalità di flashback del database, e sulla configurazione delle prestazioni di backup e ripristino. Vengono inoltre trattati il backup e il ripristino gestiti dall&#39;utente, utilizzando le strutture del sistema operativo host invece di RMAN. Questo volume è essenziale per il backup e il ripristino di implementazioni di database più sofisticate e per scenari di ripristino avanzati.

[Riferimento per il backup e il ripristino del database di Oracle:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Fornisce informazioni complete sulla sintassi e la semantica per tutti i comandi RMAN e descrive le visualizzazioni del database disponibili per il reporting sulle attività di backup e ripristino.

### SQL Server {#sql-server}

Utilizzare i backup di snapshot o configurare il database di SQL Server per l&#39;esecuzione in modalità di log delle transazioni.

SQL Server fornisce inoltre due strumenti di backup e ripristino:

* SQL Server Management Studio (GUI)
* T-SQL (riga di comando)

Per ulteriori informazioni, consulta [Backup e ripristino](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Utilizza MySQLAdmin o modifica i file INI in Windows per configurare il database MySQL da eseguire in modalità di log binario. (Vedi [Registrazione binaria MySQL](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) Uno strumento di backup a caldo per MySQL è disponibile anche dal software InnoBase. (Vedi [Backup a caldo innobase](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>La modalità di registrazione binaria predefinita per MySQL è &quot;Istruzione&quot;, incompatibile con le tabelle utilizzate da Content Services (obsoleto). L&#39;utilizzo della registrazione binaria in questa modalità predefinita causa l&#39;errore di Content Services (obsoleto). Se il sistema include Content Services (obsoleto), utilizza la modalità di registrazione &quot;mista&quot;. Per abilitare la registrazione &quot;mista&quot;, aggiungi il seguente argomento al file my.ini: `binlog_format=mixed log-bin=logname`

È possibile utilizzare l&#39;utilità mysqldump per ottenere il backup completo del database. I backup completi sono necessari, ma non sempre sono convenienti. Producono file di backup di grandi dimensioni e richiedono tempo per generare. Per eseguire un backup incrementale, assicurati di avviare il server con - `log-bin` come descritto nella sezione precedente. Ogni volta che il server MySQL si riavvia, smette di scrivere nel registro binario corrente, ne crea uno nuovo e, da quel momento in poi, quello nuovo diventa quello corrente. È possibile forzare manualmente un interruttore con la `FLUSH LOGS SQL` comando. Dopo il primo backup completo, i successivi backup incrementali vengono eseguiti utilizzando l&#39;utility mysqladmin con il `flush-logs` che crea il file di log successivo.

Vedi [Riepilogo della strategia di backup](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## Directory principale di archiviazione dei contenuti (solo Content Services) {#content-storage-root-directory-content-services-only}

La directory principale di archiviazione dei contenuti contiene l’archivio Content Services (obsoleto) in cui sono archiviati tutti i documenti, gli artefatti e gli indici. È necessario eseguire il backup della struttura della directory principale di archiviazione dei contenuti. Questa sezione descrive come determinare la posizione della directory principale di archiviazione dei contenuti sia per gli ambienti autonomi che per quelli cluster.

### Posizione principale di archiviazione dei contenuti (ambiente indipendente) {#content-storage-root-location-stand-alone-environment}

La directory principale di archiviazione dei contenuti viene creata quando viene installato Content Services (obsoleto). La posizione della directory principale di archiviazione dei contenuti viene determinata durante il processo di installazione dei moduli AEM.

Il percorso predefinito per la directory principale di archiviazione dei contenuti è `[aem-forms root]/lccs_data`.

Esegui il backup delle seguenti directory situate nella directory principale di archiviazione dei contenuti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, esegui il backup della directory /lucene-indexes, anch&#39;essa situata nella directory principale di archiviazione dei contenuti. Se la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes perché potrebbe causare errori.

### Posizione principale di archiviazione dei contenuti (ambiente cluster) {#content-storage-root-location-clustered-environment}

Quando installi Content Services (obsoleto) in un ambiente cluster, la directory principale di archiviazione dei contenuti viene divisa in due directory separate:

**Directory principale di archiviazione dei contenuti:** In genere, una directory di rete condivisa accessibile in lettura/scrittura per tutti i nodi del cluster

**Directory principale indice:** Una directory creata su ogni nodo del cluster, sempre con lo stesso percorso e nome della directory

Il percorso predefinito per la directory principale di archiviazione dei contenuti è `[GDS root]/lccs_data`, dove `[GDS root]` è la posizione descritta in [Posizione GDS](files-back-recover.md#gds-location). Esegui il backup delle seguenti directory situate nella directory principale di archiviazione dei contenuti:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Se la directory /backup-lucene-indexes non è presente, esegui il backup della directory /lucene-indexes, anch&#39;essa situata nella directory principale di archiviazione dei contenuti. Se la directory /backup-lucene-indexes è presente, non eseguire il backup della directory /lucene-indexes perché potrebbe causare errori.

Il percorso predefinito per la directory radice indice è `[aem-forms root]/lucene-indexes` su ogni nodo.

## Font installati dal cliente {#customer-installed-fonts}

Se nell’ambiente dei moduli AEM sono stati installati font aggiuntivi, è necessario eseguirne il backup separatamente. Esegui il backup di tutte le directory dei font Adobe e del cliente specificate nella console di amministrazione in Impostazioni > Sistema di base > Configurazioni. Assicurarsi di eseguire il backup dell&#39;intera directory dei font.

>[!NOTE]
>
>Per impostazione predefinita, i font di Adobe installati con AEM moduli si trovano nella `[aem-forms root]/fonts` directory.

Se si sta reinizializzando il sistema operativo sul computer host e si desidera utilizzare i font del sistema operativo precedente, è necessario eseguire il backup anche del contenuto della directory dei font del sistema. (Per istruzioni specifiche, consulta la documentazione relativa al sistema operativo in uso).
