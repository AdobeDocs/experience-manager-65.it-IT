---
title: Backup dei dati dei moduli AEM
seo-title: Backing up the AEM forms data
description: Questo documento descrive i passaggi necessari per completare un backup online o a caldo del database dei moduli AEM, delle directory GDS e della directory principale di archiviazione dei contenuti.
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 0%

---

# Backup dei dati dei moduli AEM {#backing-up-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per completare un backup online o a caldo del database dei moduli AEM, delle directory GDS e della directory principale di archiviazione dei contenuti.

Dopo l&#39;installazione e la distribuzione dei moduli AEM nelle aree di produzione, l&#39;amministratore del database deve eseguire un backup iniziale completo o a freddo del database. È necessario chiudere il database per questo backup. Quindi, i backup differenziali o incrementali (o a caldo) del database devono essere eseguiti regolarmente.

Per garantire un backup e un ripristino corretti, è necessario disporre sempre di un backup dell&#39;immagine di sistema. In questo modo, in caso di perdita, è possibile ripristinare lo stato coerente dell&#39;intero ambiente.

Il backup del database contemporaneamente ai backup delle directory radice di archiviazione dei contenuti, del repository AEM e di GDS consente di mantenere questi sistemi sincronizzati nel caso in cui sia necessario eseguire il ripristino.

La procedura di backup descritta in questa sezione richiede di attivare la modalità di backup sicura prima di eseguire il backup del database dei moduli AEM, dell&#39;archivio AEM, di GDS e delle directory principali di archiviazione dei contenuti. Al termine del backup, è necessario uscire dalla modalità di backup sicuro. La modalità di backup sicuro viene utilizzata per contrassegnare i documenti di lunga durata e persistenti che risiedono nel GDS. Questa modalità assicura che il meccanismo di pulizia automatica dei file (l&#39;agente di raccolta file) non elimini i file scaduti fino al rilascio della modalità di backup sicura. È necessario mantenere un backup GDS sincronizzato con un backup del database.

La frequenza con cui è necessario eseguire il backup del percorso GDS dipende da come vengono utilizzati i moduli AEM e dalle finestre di backup disponibili. La finestra di backup può essere influenzata da processi di lunga durata perché possono essere eseguiti per diversi giorni. Se si modificano, aggiungono e rimuovono continuamente file in questa directory, è consigliabile eseguire il backup del percorso GDS più spesso.

Se il database è in esecuzione in modalità di registrazione, come descritto nella sezione precedente, è inoltre necessario eseguire frequentemente il backup dei registri del database in modo che possano essere utilizzati per ripristinare il database in caso di errore del supporto.

>[!NOTE]
>
>I file non referenziati possono persistere nella directory GDS dopo il processo di ripristino. Questa è una limitazione nota al momento.

## Eseguire il backup del database, del GDS, dell&#39;archivio AEM e delle directory principali di archiviazione dei contenuti {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

È necessario impostare i moduli AEM in modalità backup sicuro (snapshot) o backup continuo (copertura continua). Prima di impostare i moduli AEM per l&#39;immissione di una delle modalità di backup, verificare quanto segue:

* Verificare la versione del sistema e registrare le patch o gli aggiornamenti applicati dall&#39;ultimo backup completo dell&#39;immagine del sistema.
* Se si utilizzano backup in modalità di scorrimento o snapshot, verificare che il database sia configurato con le impostazioni di registro corrette per consentire backup a caldo del database. (vedere [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Inoltre, osservare le seguenti linee guida per il processo di backup/ripristino.

* Eseguire il backup della directory GDS utilizzando un sistema operativo disponibile o un&#39;utilità di backup di terze parti. (vedere [Posizione GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Facoltativo) Eseguire il backup della directory principale di archiviazione dei contenuti utilizzando un sistema operativo disponibile o un programma di backup e utility di terze parti. (vedere [Percorso directory principale di archiviazione dei contenuti (ambiente autonomo)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Percorso directory principale di archiviazione dei contenuti (ambiente in cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Eseguire il backup delle istanze di authoring e pubblicazione ( crx -repository backup).

   Per eseguire il backup dell’ambiente della soluzione Gestione della corrispondenza, esegui i passaggi sulle istanze di authoring e pubblicazione come descritto in [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

   Quando esegui il backup delle istanze di authoring e pubblicazione, considera quanto segue:

   * Assicurati che il backup per le istanze di authoring e pubblicazione sia sincronizzato per essere avviato allo stesso tempo. Sebbene sia possibile continuare a utilizzare le istanze di authoring e pubblicazione durante l’esecuzione del backup, si consiglia di non pubblicare alcuna risorsa durante il backup per evitare modifiche non acquisite. Prima di pubblicare nuove risorse, attendi la fine del backup delle istanze di authoring e pubblicazione.
   * Il backup completo del nodo Author include il backup dei dati di Forms Manager e AEM Forms Workspace.
   * Gli sviluppatori di Workbench possono continuare a lavorare sui propri processi a livello locale. Durante la fase di backup non devono distribuire nuovi processi.
   * La decisione sulla durata di ciascuna sessione di backup (per la modalità di backup continuo) deve essere basata sul tempo totale impiegato per eseguire il backup di tutti i dati nei moduli AEM (DB, GDS, archivio AEM ed eventuali altri dati personalizzati aggiuntivi).

È necessario eseguire il backup del database dei moduli AEM, inclusi eventuali log delle transazioni. (vedere [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, vedere l&#39;articolo della Knowledge Base appropriato per il database:

* [Oracle di backup e ripristino per i moduli AEM](https://www.adobe.com/go/kb403624)
* [Backup e ripristino MySQL per moduli AEM](https://www.adobe.com/go/kb403625)
* [Backup e ripristino di Microsoft SQL Server per moduli AEM](https://www.adobe.com/go/kb403623)
* [Backup e ripristino DB2 per moduli AEM](https://www.adobe.com/go/kb403626)

Questi articoli forniscono indicazioni sulle funzioni di base del database per il backup e il recupero dei dati. Non sono intesi come guide tecniche complete delle funzioni di backup e ripristino del database di un fornitore specifico. Vengono descritti i comandi necessari per creare una strategia di backup del database affidabile per i dati delle applicazioni AEM Forms.

>[!NOTE]
>
>Il backup del database deve essere completato prima di iniziare il backup di GDS. Se il backup del database non è completo, i dati non saranno sincronizzati.

### Immissione delle modalità di backup {#entering-the-backup-modes}

È possibile utilizzare la console di amministrazione, il comando LCBackupMode o l&#39;API disponibile con l&#39;installazione di moduli AEM per accedere e uscire dalle modalità di backup. Per il backup continuo (copertura continua), l’opzione della console di amministrazione non è disponibile; è necessario utilizzare l’opzione della riga di comando o l’API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se SSL è stato configurato nel server Forms, non è possibile impostare il server Forms in modalità di backup utilizzando lo script LCBackupMode.CMD.

**Utilizzo della console di amministrazione per attivare la modalità di backup sicuro**

1. Accedere alla console di amministrazione.
1. Fai clic su Impostazioni > Impostazioni sistema core > Utilità di backup.
1. Selezionare Operate In Safe Backup Mode e fare clic su OK.

   Questo metodo mette i moduli AEM in modalità di backup a tempo indefinito (senza timeout) ed entra in modalità snapshot anziché rollback.

**Utilizzo dell&#39;opzione della riga di comando per attivare la modalità di backup sicuro**

È possibile utilizzare l&#39;interfaccia della riga di comando `LCBackupMode` script per mettere i moduli AEM in modalità di backup sicuro.

1. Impostare ADOBE_LIVECYCLE e avviare il server applicazioni.
1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo in uso, modificare `LCBackupMode.cmd` o `LCBackupMode.sh` script per fornire valori predefiniti appropriati per il sistema.
1. Al prompt dei comandi eseguire il comando seguente su un&#39;unica riga:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*secondi* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `] [-label=`*labelname* `]`

   Nei comandi precedenti, i segnaposto sono definiti come segue:

   `Host` è il nome dell’host in cui è in esecuzione il modulo AEM.

   `port` è la porta WebServices del server applicazioni in cui sono in esecuzione i moduli AEM.

   `user` è il nome utente dell’amministratore di AEM forms.

   `password` è la password dell’amministratore dei moduli AEM.

   `label` è l&#39;etichetta di testo, che può essere qualsiasi stringa, per questo backup.

   `timeout` è il numero di secondi dopo i quali la modalità di backup viene lasciata automaticamente. Può essere compreso tra 0 e 10.080. Se è 0, che è l&#39;impostazione predefinita, la modalità di backup non si interrompe mai.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file Leggimi nella directory BackupRestoreCommandline.

### Uscita dalle modalità di backup {#leaving-backup-modes}

È possibile utilizzare la console di amministrazione o l&#39;opzione della riga di comando per uscire dalla modalità di backup.

**Lascia la modalità di backup sicura (modalità snapshot)**

Per utilizzare la console di amministrazione per rimuovere i moduli AEM dalla modalità di backup sicuro (modalità snapshot), effettuare le seguenti operazioni.

1. Accedere alla console di amministrazione.
1. Fai clic su Impostazioni > Impostazioni sistema core > Utilità di backup.
1. Deselezionare Operate In modalità di backup sicuro e fare clic su OK.

**Lascia tutte le modalità di backup**

È possibile utilizzare l&#39;interfaccia della riga di comando per eliminare i moduli AEM dalla modalità di backup sicuro (modalità snapshot) o per terminare la sessione in modalità di backup corrente (modalità di rollback). Non è possibile utilizzare la console di amministrazione per uscire dalla modalità di backup continuo. In modalità di backup continuo, i controlli Utilità di backup nella console di amministrazione sono disattivati. È necessario utilizzare una chiamata API o il comando LCBackupMode.

1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo in uso, modificare `LCBackupMode.cmd` o `LCBackupMode.sh` script per fornire valori predefiniti appropriati per il sistema.

   >[!NOTE]
   >
   >È necessario impostare la directory JAVA_HOME come descritto nel capitolo appropriato per il server applicazioni in [Preparazione all’installazione dei moduli AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Esegui il comando seguente su una singola riga:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `]`

      Nei comandi precedenti, i segnaposto sono definiti come segue:

      `Host` è il nome dell’host in cui è in esecuzione il modulo AEM.

      `port` è la porta su cui i moduli AEM sono in esecuzione sul server applicazioni.

      `user` è il nome utente dell’amministratore di AEM forms.

      `password` è la password dell’amministratore dei moduli AEM.

      `leaveContinuousCoverage` Utilizzare questa opzione per disattivare completamente la modalità di backup continuo.
   >[!NOTE]
   >
   >Per il periodo di tempo in cui la modalità di backup è disattivata, non è possibile ristabilire la copertura continua. Eventuali modifiche apportate durante tale periodo di tempo non sono protette.

   >[!NOTE]
   >
   >Se è stata abilitata l&#39;archiviazione dei documenti nel database, la modalità di backup delle copie istantanee e le modalità di backup continuo non sono applicabili.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file readme nella directory BackupRestoreCommandline.
