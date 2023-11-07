---
title: Backup dei dati di Adobe Experience Manager Forms
description: Questo documento descrive i passaggi necessari per completare un backup online del database dei moduli di Adobe Experience Manager (AEM), delle directory GDS e della directory principale di archiviazione dei contenuti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 0%

---

# Backup dei dati Adobe Experience Manager (AEM) Forms {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

Questa sezione descrive i passaggi necessari per completare un backup online o a caldo del database AEM Forms, delle directory GDS e della directory principale di archiviazione dei contenuti.

Dopo l’installazione e la distribuzione di AEM Forms nelle aree di produzione, l’amministratore del database deve eseguire un backup iniziale completo o a freddo del database. È necessario chiudere il database per questo backup. Quindi, i backup differenziali o incrementali (o a caldo) del database devono essere eseguiti regolarmente.

Per garantire un backup e un ripristino corretti, è necessario disporre sempre di un backup dell&#39;immagine di sistema. In questo modo, in caso di perdita, è possibile ripristinare lo stato coerente dell&#39;intero ambiente.

Il backup del database contemporaneamente ai backup delle directory radice di archiviazione dei contenuti, del repository AEM e di GDS consente di mantenere questi sistemi sincronizzati nel caso in cui sia necessario eseguire il ripristino.

La procedura di backup descritta in questa sezione richiede di attivare la modalità di backup sicura prima di eseguire il backup del database AEM Forms, dell’archivio AEM, di GDS e delle directory principali di archiviazione dei contenuti. Al termine del backup, è necessario uscire dalla modalità di backup sicuro. La modalità di backup sicuro viene utilizzata per contrassegnare i documenti di lunga durata e persistenti che risiedono nel GDS. Questa modalità assicura che il meccanismo di pulizia automatica dei file (l&#39;agente di raccolta file) non elimini i file scaduti fino a quando non viene rilasciata la modalità di backup sicura. È necessario mantenere un backup GDS sincronizzato con un backup del database.

La frequenza con cui è necessario eseguire il backup del percorso GDS dipende da come viene utilizzato AEM Forms e dalle finestre di backup disponibili. La finestra di backup può essere influenzata da processi di lunga durata perché possono essere eseguiti per diversi giorni. Se si modificano, aggiungono e rimuovono continuamente file in questa directory, è consigliabile eseguire il backup del percorso GDS più spesso.

Se il database è in esecuzione in modalità di registrazione, come descritto nella sezione precedente, è necessario eseguire frequentemente anche il backup dei log del database, in modo che possano essere utilizzati per ripristinare il database in caso di errore del supporto.

>[!NOTE]
>
>I file non referenziati possono persistere nella directory GDS dopo il processo di ripristino. Attualmente si tratta di una limitazione nota.

## Eseguire il backup del database, del GDS, dell&#39;archivio AEM e delle directory principali di archiviazione dei contenuti {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

È necessario impostare AEM Forms in modalità di backup sicuro (snapshot) o di backup continuo (copertura continua). Prima di impostare AEM Forms per l&#39;immissione di una delle modalità di backup, verificare quanto segue:

* Verificare la versione del sistema e registrare le patch o gli aggiornamenti applicati dall&#39;ultimo backup completo dell&#39;immagine del sistema.
* Se si utilizzano backup in modalità di scorrimento o snapshot, verificare che il database sia configurato con le impostazioni di registro corrette per consentire backup a caldo del database. (vedere [database AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Inoltre, osservare le seguenti linee guida per il processo di backup/ripristino.

* Eseguire il backup della directory GDS utilizzando un sistema operativo disponibile o un&#39;utilità di backup di terze parti. (vedere [Posizione GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Facoltativo) Eseguire il backup della directory principale di archiviazione dei contenuti utilizzando un sistema operativo disponibile o un programma di backup e utility di terze parti. (vedere [Percorso directory principale di archiviazione dei contenuti (ambiente autonomo)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Percorso directory principale di archiviazione dei contenuti (ambiente in cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Eseguire il backup delle istanze di authoring e pubblicazione ( crx -repository backup).

  Per eseguire il backup dell’ambiente della soluzione Gestione della corrispondenza, esegui i passaggi sulle istanze di authoring e pubblicazione come descritto in [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

  Quando esegui il backup delle istanze di authoring e pubblicazione, considera quanto segue:

   * Assicurati che il backup per le istanze di authoring e pubblicazione sia sincronizzato e venga avviato allo stesso tempo. Sebbene sia possibile continuare a utilizzare le istanze di authoring e pubblicazione durante l’esecuzione del backup, si consiglia di non pubblicare alcuna risorsa durante il backup per evitare modifiche non acquisite. Prima di pubblicare nuove risorse, attendi la fine del backup delle istanze di authoring e pubblicazione.
   * Il backup completo del nodo Author include il backup dei dati di Forms Manager e AEM Forms Workspace.
   * Gli sviluppatori di Workbench possono continuare a lavorare sui propri processi a livello locale. Durante la fase di backup non devono distribuire nuovi processi.
   * La decisione sulla durata di ciascuna sessione di backup (per la modalità di backup continuo) deve essere basata sul tempo totale impiegato per eseguire il backup di tutti i dati in AEM Forms (database, GDS, archivio AEM ed eventuali altri dati personalizzati aggiuntivi).

Esegui il backup del database di AEM Forms, compresi eventuali registri delle transazioni. Consulta [database AEM Forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

Per ulteriori informazioni, vedere l&#39;articolo della Knowledge Base appropriato per il database:
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [Oracle di backup e ripristino per AEM Forms](https://www.adobe.com/go/kb403624)
* [Backup e ripristino MySQL per AEM Forms](https://www.adobe.com/go/kb403625)
* [Backup e ripristino di Microsoft® SQL Server per AEM Forms](https://www.adobe.com/go/kb403623)
* [Backup e ripristino DB2® per AEM Forms](https://www.adobe.com/go/kb403626)

Questi articoli forniscono indicazioni sulle funzioni di base del database per il backup e il recupero dei dati. Non sono intesi come guide tecniche complete delle funzioni di backup e ripristino del database di un fornitore specifico. Descrivono i comandi necessari per creare una strategia di backup del database affidabile per i dati dell’applicazione AEM Forms.

>[!NOTE]
>
>Il backup del database deve essere completato prima di iniziare il backup di GDS. Se il backup del database non è completo, i dati non sono sincronizzati.

### Immissione delle modalità di backup {#entering-the-backup-modes}

È possibile utilizzare la console di amministrazione, il comando LCBackupMode o l&#39;API disponibile con l&#39;installazione di AEM Forms per attivare e disattivare le modalità di backup. Per il backup continuo (copertura continua), l’opzione della console di amministrazione non è disponibile; è necessario utilizzare l’opzione della riga di comando o l’API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se SSL è stato configurato sul server Forms, non è possibile attivare la modalità di backup del server Forms utilizzando lo script LCBackupMode.CMD.

**Utilizzo della console di amministrazione per attivare la modalità di backup sicuro**

1. Accedere alla console di amministrazione.
1. Fai clic su Impostazioni > Impostazioni sistema core > Utilità di backup.
1. Selezionare Operate In Safe Backup Mode e fare clic su OK.

   Questo metodo mette AEM Forms in modalità di backup a tempo indefinito (senza timeout) ed entra in modalità snapshot anziché rollback.

**Utilizzo dell&#39;opzione della riga di comando per attivare la modalità di backup sicuro**

È possibile utilizzare l&#39;interfaccia della riga di comando `LCBackupMode` script per mettere AEM Forms in modalità di backup sicuro.

1. Impostare ADOBE_LIVECYCLE e avviare il server applicazioni.
1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo in uso, modificare `LCBackupMode.cmd` o `LCBackupMode.sh` script per fornire valori predefiniti appropriati per il sistema.
1. Al prompt dei comandi eseguire il comando seguente su un&#39;unica riga:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*secondi* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh enter [-host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `] [-label=`*labelname* `]`

   Nei comandi precedenti, i segnaposto sono definiti come segue:

   `Host` è il nome dell’host in cui è in esecuzione AEM Forms.

   `port` è la porta WebServices del server applicazioni in cui è in esecuzione AEM Forms.

   `user` è il nome utente dell’amministratore di AEM Forms.

   `password` è la password dell’amministratore di AEM Forms.

   `label` è l&#39;etichetta di testo, che può essere qualsiasi stringa, per questo backup.

   `timeout` è il numero di secondi dopo i quali la modalità di backup viene lasciata automaticamente. Può essere 0-10.080. Se è 0, che è l&#39;impostazione predefinita, la modalità di backup non si interrompe mai.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file Leggimi nella directory BackupRestoreCommandline.

### Uscita dalle modalità di backup {#leaving-backup-modes}

Per uscire dalla modalità di backup è possibile utilizzare la console di amministrazione o l&#39;opzione della riga di comando.

**Lascia la modalità di backup sicura (modalità snapshot)**

Per utilizzare la console di amministrazione per escludere AEM Forms dalla modalità di backup sicuro (modalità snapshot), esegui le seguenti attività.

1. Accedere alla console di amministrazione.
1. Fai clic su Impostazioni > Impostazioni sistema core > Utilità di backup.
1. Deselezionare Operate In modalità di backup sicuro e fare clic su OK.

**Lascia tutte le modalità di backup**

Puoi utilizzare l’interfaccia della riga di comando per escludere AEM Forms dalla modalità di backup sicuro (modalità snapshot) o per terminare la sessione in modalità di backup corrente (modalità continua). Non è possibile utilizzare la console di amministrazione per uscire dalla modalità di backup continuo. In modalità di backup continuo, i controlli Utilità di backup nella console di amministrazione sono disattivati. Utilizzare la chiamata API o il comando LCBackupMode.

1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo in uso, modificare `LCBackupMode.cmd` o `LCBackupMode.sh` script per fornire valori predefiniti appropriati per il sistema.

   >[!NOTE]
   >
   >Impostare la directory JAVA_HOME come descritto nel capitolo appropriato per il server applicazioni in [Preparazione all’installazione di AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Esegui il comando seguente su una singola riga:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `]`
   * (Linux®, UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*nome host* `] [-port=`*portnumber* `] [-user=`*nome utente* `] [-password=`*password* `]`

     Nei comandi precedenti, i segnaposto sono definiti come segue:

     `Host` è il nome dell’host in cui è in esecuzione AEM Forms.

     `port` è la porta su cui AEM Forms è in esecuzione sul server applicazioni.

     `user` è il nome utente dell’amministratore di AEM Forms.

     `password` è la password dell’amministratore di AEM Forms.

     `leaveContinuousCoverage` Utilizzare questa opzione per disattivare completamente la modalità di backup continuo.

   >[!NOTE]
   >
   >Per il periodo di tempo in cui la modalità di backup è disattivata, non è possibile ristabilire la copertura continua. Eventuali modifiche apportate durante tale periodo di tempo non sono protette.

   >[!NOTE]
   >
   >Se è stata abilitata l&#39;archiviazione dei documenti nel database, la modalità di backup delle copie istantanee e le modalità di backup continuo non sono applicabili.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file readme nella directory BackupRestoreCommandline.
