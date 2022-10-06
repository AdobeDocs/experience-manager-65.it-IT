---
title: Backup dei dati dei moduli AEM
seo-title: Backing up the AEM forms data
description: Questo documento descrive i passaggi necessari per completare un backup caldo o online del database dei moduli di AEM, delle directory GDS e Content Storage Root.
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

Questa sezione descrive i passaggi necessari per completare un backup caldo o online del database dei moduli di AEM, delle directory GDS e Content Storage Root.

Dopo aver installato AEM moduli e implementato nelle aree di produzione, l’amministratore del database deve eseguire un backup iniziale completo o a freddo del database. Il database deve essere arrestato per questo backup. Quindi, i backup differenziali o incrementali (o a caldo) del database devono essere eseguiti regolarmente.

Per garantire un backup e un ripristino di successo, è necessario che sia sempre disponibile un backup delle immagini di sistema. Quindi, se si verifica una perdita, è possibile ripristinare l&#39;intero ambiente a uno stato coerente.

Il backup del database contemporaneamente ai backup della directory principale GDS, AEM repository e Content Storage consente di mantenere questi sistemi sincronizzati se il ripristino è necessario.

La procedura di backup descritta in questa sezione richiede l’immissione di una modalità di backup sicura prima di eseguire il backup del database dei moduli AEM, dell’archivio AEM, di GDS e delle directory principali di archiviazione dei contenuti. Al termine del backup, è necessario uscire dalla modalità di backup sicura. La modalità di backup sicuro viene utilizzata per contrassegnare i documenti persistenti e a lunga vita che risiedono nel GDS. Questa modalità assicura che il meccanismo automatizzato di pulizia dei file (il raccoglitore di file) non elimini i file scaduti fino al rilascio della modalità di backup sicuro. È necessario mantenere un backup GDS in sincronizzazione con un backup del database.

La frequenza con cui è necessario eseguire il backup della posizione GDS dipende da come vengono utilizzati i moduli AEM e dalle finestre di backup disponibili. La finestra di backup può essere influenzata da processi di lunga durata perché possono essere eseguiti per diversi giorni. Se modifichi, aggiungi e rimuovi continuamente file in questa directory, devi eseguire più spesso il backup della posizione GDS.

Se il database è in esecuzione in modalità di registrazione, come descritto nella sezione precedente, è necessario eseguire spesso il backup dei log del database in modo che possano essere utilizzati per ripristinare il database in caso di errore del supporto.

>[!NOTE]
>
>I file a cui non si fa riferimento possono persistere nella directory GDS dopo il processo di ripristino. Questa è una limitazione nota al momento.

## Esegui il backup del database, dei GDS, dell&#39;archivio AEM e delle directory principali di archiviazione dei contenuti {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

È necessario inserire i moduli AEM in modalità backup sicuro (snapshot) o backup continuo (copertura continua). Prima di impostare AEM moduli per l’immissione di una delle modalità di backup, verificare quanto segue:

* Verificare la versione di sistema e registrare le patch o gli aggiornamenti applicati dall&#39;ultima esecuzione del backup completo dell&#39;immagine di sistema.
* Se si utilizzano backup in modalità di rotazione o snapshot, assicurarsi che il database sia configurato con le impostazioni di log corrette per consentire backup a caldo del database. (Vedi [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Inoltre, osservare le seguenti linee guida per il processo di backup/ripristino.

* Eseguire il backup della directory GDS utilizzando un sistema operativo disponibile o un&#39;utilità di backup di terze parti. (Vedi [Posizione GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Facoltativo) Eseguire il backup della directory principale di archiviazione dei contenuti utilizzando un sistema operativo disponibile o un backup e un&#39;utility di terze parti. (Vedi [Posizione principale di archiviazione dei contenuti (ambiente indipendente)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Posizione principale di archiviazione dei contenuti (ambiente cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Esegui il backup delle istanze di authoring e pubblicazione ( crx -repository backup).

   Per eseguire il backup dell&#39;ambiente della soluzione per la gestione della corrispondenza, esegui i passaggi sull&#39;istanza di authoring e pubblicazione come descritto in [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

   Quando esegui il backup delle istanze di authoring e pubblicazione, considera quanto segue:

   * Assicurati che il backup per le istanze di creazione e pubblicazione sia sincronizzato in modo che venga avviato contemporaneamente.Anche se puoi continuare a utilizzare le istanze di creazione e pubblicazione durante l&#39;esecuzione del backup, si consiglia di non pubblicare alcuna risorsa durante il backup per evitare eventuali modifiche non acquisite. Attendi la fine del backup delle istanze di authoring e pubblicazione prima di pubblicare le nuove risorse.
   * Il backup completo del nodo Autore include il backup dei dati di Forms Manager e AEM Forms Workspace.
   * Gli sviluppatori di Workbench possono continuare a lavorare sui propri processi localmente. Non devono distribuire nuovi processi durante la fase di backup.
   * La decisione sulla lunghezza di ogni sessione di backup (per la modalità di backup continuo) deve essere basata sul tempo totale impiegato per eseguire il backup di tutti i dati nei moduli AEM (DB, GDS, archivio AEM e qualsiasi altro dato personalizzato aggiuntivo).

È necessario eseguire il backup del database dei moduli AEM, compresi eventuali log delle transazioni. (Vedi [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, consulta l’articolo appropriato della knowledge base per il database:

* [Backup e ripristino di Oracle per i moduli AEM](https://www.adobe.com/go/kb403624)
* [Backup e ripristino di MySQL per i moduli AEM](https://www.adobe.com/go/kb403625)
* [Backup e ripristino di Microsoft SQL Server per i moduli AEM](https://www.adobe.com/go/kb403623)
* [Backup e ripristino DB2 per moduli AEM](https://www.adobe.com/go/kb403626)

Questi articoli forniscono indicazioni sulle funzionalità di base del database per il backup e il ripristino dei dati. Non sono concepite come guide tecniche complete per una specifica funzionalità di backup e ripristino del database di un fornitore. Consentono di delineare i comandi necessari per creare una strategia di backup affidabile del database per i dati dell&#39;applicazione AEM forms.

>[!NOTE]
>
>Il backup del database deve essere completato prima di iniziare il backup del GDS. Se il backup del database non è completo, i dati non saranno sincronizzati.

### Accesso alle modalità di backup {#entering-the-backup-modes}

È possibile utilizzare la console di amministrazione, il comando LCBackupMode o l’API disponibile con l’installazione dei moduli AEM per accedere e uscire dalle modalità di backup. Per il backup continuo (copertura continua), l&#39;opzione della console di amministrazione non è disponibile; devi utilizzare l’opzione della riga di comando o l’API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se sul server dei moduli è stato configurato SSL, non è possibile posizionare il server dei moduli in modalità di backup utilizzando lo script LCBackupMode.CMD.

**Utilizzo della console di amministrazione per accedere alla modalità di backup sicuro**

1. Accedi alla console di amministrazione.
1. Fare clic su Impostazioni > Impostazioni sistema di base > Utilità di backup.
1. Selezionare Opera in modalità di backup sicuro e fare clic su OK.

   Questo metodo mette i moduli AEM in modalità di backup a tempo indefinito (senza timeout) e entra in modalità snapshot anziché in modalità di backup a rotazione.

**Utilizzo dell&#39;opzione della riga di comando per accedere alla modalità di backup sicuro**

È possibile utilizzare l’interfaccia della riga di comando `LCBackupMode` script per l’inserimento AEM moduli in modalità di backup sicuro.

1. Imposta ADOBE_LIVECYCLE e avvia l&#39;application server.
1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo, modifica il `LCBackupMode.cmd` o `LCBackupMode.sh` per fornire i valori predefiniti appropriati per il sistema.
1. Al prompt dei comandi, eseguire il comando seguente su una singola riga:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*numero portinaio* `] [-user=`*username* `] [-password=`*password* `] [-label=`*etichetta* `] [-timeout=`*secondi* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*numero portinaio* `] [-user=`*username* `] [-password=`*password* `] [-label=`*etichetta* `]`

   Nei comandi precedenti, i segnaposto sono definiti come segue:

   `Host` è il nome dell’host in cui è in esecuzione AEM moduli.

   `port` è la porta WebServices del server applicazioni in cui sono in esecuzione AEM moduli.

   `user` è il nome utente dell’amministratore dei moduli di AEM.

   `password` è la password dell’amministratore dei moduli di AEM.

   `label` è l&#39;etichetta di testo, che può essere qualsiasi stringa, per questo backup.

   `timeout` è il numero di secondi dopo i quali la modalità di backup viene lasciata automaticamente. Può essere da 0 a 10.080. Se è 0, che è l&#39;impostazione predefinita, la modalità di backup non si interrompe mai.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando alla modalità di backup, vedere il file Readme nella directory BackupRestoreCommandline.

### Uscire dalle modalità di backup {#leaving-backup-modes}

Per uscire dalle modalità di backup è possibile utilizzare la console di amministrazione o l&#39;opzione della riga di comando.

**Lascia la modalità di backup sicuro (modalità snapshot)**

Per utilizzare la console di amministrazione per rimuovere AEM moduli dalla modalità di backup sicuro (modalità snapshot), eseguire le operazioni seguenti.

1. Accedi alla console di amministrazione.
1. Fare clic su Impostazioni > Impostazioni sistema di base > Utilità di backup.
1. Deselezionare Opera in modalità di backup sicuro e fare clic su OK.

**Lascia tutte le modalità di backup**

È possibile utilizzare l&#39;interfaccia della riga di comando per estrarre AEM moduli dalla modalità di backup sicuro (modalità snapshot) o per terminare la sessione corrente della modalità di backup (modalità di rotazione). Non è possibile utilizzare la console di amministrazione per uscire dalla modalità di backup continuo. In modalità di backup continuo, i controlli Utilità di backup nella console di amministrazione sono disabilitati. È necessario utilizzare una chiamata API o il comando LCBackupMode .

1. Vai a `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` cartella.
1. A seconda del sistema operativo, modifica il `LCBackupMode.cmd` o `LCBackupMode.sh` per fornire i valori predefiniti appropriati per il sistema.

   >[!NOTE]
   >
   >È necessario impostare la directory JAVA_HOME come descritto nel capitolo appropriato per il server applicazioni in [Preparazione all’installazione AEM moduli](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Esegui il comando seguente su una singola riga:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*numero portinaio* `] [-user=`*username* `] [-password=`*password* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*numero portinaio* `] [-user=`*username* `] [-password=`*password* `]`

      Nei comandi precedenti, i segnaposto sono definiti come segue:

      `Host` è il nome dell’host in cui è in esecuzione AEM moduli.

      `port` è la porta su cui i moduli AEM sono in esecuzione sul server dell&#39;applicazione.

      `user` è il nome utente dell’amministratore dei moduli di AEM.

      `password` è la password dell’amministratore dei moduli di AEM.

      `leaveContinuousCoverage` Utilizzare questa opzione per disabilitare completamente la modalità di backup continuo.
   >[!NOTE]
   >
   >Per il momento in cui la modalità di backup è disattivata, non è possibile ripristinare la copertura continua. Eventuali modifiche apportate durante tale periodo non sono protette.

   >[!NOTE]
   >
   >Se nel database è stata abilitata l&#39;archiviazione dei documenti, la modalità di backup dello snapshot e le modalità di backup continuo non sono applicabili.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando alla modalità di backup, vedere il file readme nella directory BackupRestoreCommandline.
