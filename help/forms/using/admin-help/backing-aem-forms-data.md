---
title: Backup dei dati dei moduli AEM
seo-title: Backup dei dati dei moduli AEM
description: Questo documento descrive i passaggi necessari per completare un backup attivo o online del database dei moduli AEM, delle directory GDS e Content Storage Root.
seo-description: Questo documento descrive i passaggi necessari per completare un backup attivo o online del database dei moduli AEM, delle directory GDS e Content Storage Root.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Backup dei dati dei moduli AEM {#backing-up-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per completare un backup a caldo o online del database dei moduli AEM, delle directory GDS e Content Storage Root.

Dopo aver installato e distribuito AEM moduli nelle aree di produzione, l&#39;amministratore del database deve eseguire un backup iniziale completo o freddo del database. Il database deve essere chiuso per questo backup. Quindi, i backup differenziali o incrementali (o a caldo) del database dovrebbero essere eseguiti regolarmente.

Per garantire un backup e un ripristino efficaci, è necessario che sia sempre disponibile un backup delle immagini di sistema. Quindi, se si verifica una perdita, è possibile ripristinare l&#39;intero ambiente a uno stato coerente.

Il backup del database nello stesso momento dei backup di directory GDS, AEM repository e Content Storage Root consente di mantenere sincronizzati i sistemi in caso di necessità di ripristino.

La procedura di backup descritta in questa sezione richiede l&#39;immissione di una modalità di backup sicura prima di eseguire il backup delle directory radice del database dei moduli AEM, AEM repository, GDS e Content Storage. Al termine del backup, è necessario uscire dalla modalità di backup sicura. La modalità di backup sicuro è utilizzata per contrassegnare documenti longevi e persistenti che risiedono nel GDS. Questa modalità assicura che il meccanismo automatico di pulizia dei file (il raccoglitore di file) non elimini i file scaduti fino al rilascio della modalità di backup sicura. È necessario mantenere un backup GDS in sincronizzazione con un backup del database.

La frequenza con cui è necessario eseguire il backup del percorso GDS dipende dalla modalità di utilizzo dei moduli AEM e dalle finestre di backup disponibili. La finestra di backup può essere influenzata da processi a lunga durata perché possono funzionare per diversi giorni. Se state cambiando, aggiungendo e rimuovendo continuamente i file in questa directory, dovete eseguire più spesso il backup del percorso GDS.

Se il database è in esecuzione in modalità di registrazione, come descritto nella sezione precedente, è necessario eseguire spesso il backup dei log del database, in modo che possano essere utilizzati per ripristinare il database in caso di errore del supporto.

>[!NOTE]
>
>I file a cui non viene fatto riferimento possono persistere nella directory GDS dopo il processo di ripristino. Questa è una limitazione nota al momento.

## Eseguire il backup delle directory radice di database, GDS, AEM repository e Content Storage {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

È necessario inserire AEM moduli in modalità backup sicuro (snapshot) o backup continuo (copertura continua). Prima di impostare AEM moduli per l&#39;immissione di una delle modalità di backup, assicurarsi di disporre dei seguenti elementi:

* Verificare la versione del sistema e registrare le patch o gli aggiornamenti applicati dopo l&#39;ultimo backup completo dell&#39;immagine del sistema.
* Se utilizzate backup in modalità di scorrimento o snapshot, accertatevi che il database sia configurato con le impostazioni di registro corrette per consentire il backup a caldo del database. (Vedere [AEM database moduli](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Inoltre, attenersi alle seguenti linee guida per il processo di backup/ripristino.

* Eseguire il backup della directory GDS utilizzando un sistema operativo disponibile o un&#39;utility di backup di terze parti. (Vedere [Posizione GDS](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Facoltativo) Eseguire il backup della directory principale di Content Storage utilizzando un sistema operativo disponibile o un&#39;utility e un backup di terze parti. (Vedere [Posizione radice memorizzazione contenuto (ambiente autonomo)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) o [Posizione radice memorizzazione contenuto (ambiente cluster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Eseguire il backup   creare e pubblicare le istanze (crx -repository backup).

   Per eseguire il backup dell&#39;ambiente della soluzione di gestione della corrispondenza, eseguire i passaggi sulle istanze di creazione e pubblicazione come descritto in [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

   Durante il backup delle istanze di creazione e pubblicazione, tenete presenti i seguenti punti:

   * Assicuratevi che il backup delle istanze di creazione e pubblicazione sia sincronizzato in modo che venga avviato allo stesso tempo. Sebbene sia possibile continuare a utilizzare le istanze di creazione e pubblicazione durante l’esecuzione del backup, si consiglia di non pubblicare alcuna risorsa durante il backup per evitare modifiche non acquisite. Attendete che il backup delle istanze di creazione e pubblicazione termini prima di pubblicare le nuove risorse.
   * Il backup completo del nodo Author include il backup di Forms Manager e  dati di AEM Forms Workspace.
   * Gli sviluppatori di Workbench possono continuare a lavorare sui propri processi localmente. Non devono distribuire nuovi processi durante la fase di backup.
   * La decisione relativa alla lunghezza di ciascuna sessione di backup (per la modalità di backup continuo) deve basarsi sul tempo totale impiegato per eseguire il backup di tutti i dati nei moduli AEM (DB, GDS, AEM repository e qualsiasi altro dato personalizzato aggiuntivo).

Eseguire il backup del database dei moduli AEM, compresi eventuali log delle transazioni. (Vedere [AEM database moduli](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, consultate l&#39;articolo appropriato della knowledge base per il database:

* [ Oracle Backup e ripristino per i moduli AEM](https://www.adobe.com/go/kb403624)
* [Backup e ripristino di MySQL per moduli AEM](https://www.adobe.com/go/kb403625)
* [Backup e ripristino di Microsoft SQL Server per i moduli AEM](https://www.adobe.com/go/kb403623)
* [Backup e ripristino DB2 per i moduli AEM](https://www.adobe.com/go/kb403626)

Questi articoli forniscono indicazioni sulle funzionalità di base del database per il backup e il ripristino dei dati. Non sono concepite come guide tecniche complete per una specifica funzionalità di backup e ripristino del database di un fornitore. Consentono di delineare i comandi necessari per creare una strategia di backup affidabile del database per i dati dell&#39;applicazione dei moduli AEM.

>[!NOTE]
>
>Il backup del database deve essere completato prima di iniziare il backup del GDS. Se il backup del database non è completo, i dati non saranno sincronizzati.

### Immissione delle modalità di backup {#entering-the-backup-modes}

È possibile utilizzare la console di amministrazione, il comando LCBackupMode o l&#39;API disponibile con l&#39;installazione dei moduli AEM per accedere e uscire dalle modalità di backup. Tenere presente che per il backup a rotazione (copertura continua), l&#39;opzione della console di amministrazione non è disponibile; utilizzare l&#39;opzione della riga di comando o l&#39;API. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Se sul server dei moduli è stato configurato SSL, non è possibile posizionare il server dei moduli in modalità di backup utilizzando lo script LCBackupMode.CMD.

**Utilizzo della console di amministrazione per accedere alla modalità di backup sicura**

1. Accedete alla console di amministrazione.
1. Fate clic su Impostazioni > Impostazioni di sistema di base > Utility di backup.
1. Selezionate Opera in modalità di backup sicuro e fate clic su OK.

   Questo metodo mette AEM moduli in modalità di backup a tempo indeterminato (senza timeout) e passa alla modalità snapshot anziché alla modalità di backup a rotazione.

**Utilizzo dell&#39;opzione della riga di comando per passare alla modalità di backup sicura**

È possibile utilizzare gli script dell&#39;interfaccia della riga di comando `LCBackupMode` per posizionare AEM moduli in modalità di backup sicuro.

1. Impostate  ADOBE_LIVECYCLE e avviate il server applicazione.
1. Andate alla cartella `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. A seconda del sistema operativo in uso, modificare lo script `LCBackupMode.cmd` o `LCBackupMode.sh` per fornire i valori predefiniti appropriati al sistema in uso.
1. Al prompt dei comandi, eseguire il comando seguente su una sola riga:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*nomehost* `] [-port=`*numeroporta* `] [-user=`*nomeutente* `] [-password=`*password* `] [-label=`*nomeetichetta* `] [-timeout=`*secondi* `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   Nei comandi precedenti, i segnaposto sono definiti come segue:

   `Host` è il nome dell&#39;host in cui sono in esecuzione AEM moduli.

   `port` è la porta WebServices del server applicazioni su cui sono in esecuzione AEM moduli.

   `user` è il nome utente dell&#39;amministratore dei moduli di AEM.

   `password` è la password dell&#39;amministratore dei moduli AEM.

   `label` è l&#39;etichetta di testo, che può essere una qualsiasi stringa, per questo backup.

   `timeout` è il numero di secondi dopo il quale la modalità di backup viene lasciata automaticamente. Può essere da 0 a 10.080. Se il valore predefinito è 0, la modalità di backup non si verifica mai un timeout.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file Leggimi nella directory BackupRestoreCommand.

### Uscire dalle modalità di backup {#leaving-backup-modes}

È possibile utilizzare la console di amministrazione o l&#39;opzione della riga di comando per uscire dalle modalità di backup.

**Modalità di backup sicura (modalità snapshot)**

Per utilizzare la console di amministrazione per estrarre AEM moduli dalla modalità di backup sicuro (modalità snapshot), eseguire le operazioni seguenti.

1. Accedi alla console di amministrazione.
1. Fate clic su Impostazioni > Impostazioni di sistema di base > Utility di backup.
1. Deselezionare Opera in modalità di backup sicuro e fare clic su OK.

**Lascia tutte le modalità di backup**

È possibile utilizzare l&#39;interfaccia della riga di comando per estrarre AEM moduli dalla modalità di backup sicura (modalità snapshot) o per terminare la sessione corrente della modalità di backup (modalità di scorrimento). Non è possibile utilizzare la console di amministrazione per uscire dalla modalità di backup continuo. In modalità di backup continuo, i controlli Utilità di backup nella console di amministrazione sono disabilitati. È necessario utilizzare una chiamata API o il comando LCBackupMode.

1. Andate alla cartella `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`.
1. A seconda del sistema operativo in uso, modificare lo script `LCBackupMode.cmd` o `LCBackupMode.sh` per fornire i valori predefiniti appropriati al sistema in uso.

   >[!NOTE]
   >
   >È necessario impostare la directory JAVA_HOME come descritto nel capitolo appropriato per il server applicazione in [Preparazione all&#39;installazione di moduli AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Eseguire il comando seguente su una sola riga:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`

      Nei comandi precedenti, i segnaposto sono definiti come segue:

      `Host` è il nome dell&#39;host in cui sono in esecuzione AEM moduli.

      `port` è la porta su cui AEM moduli è in esecuzione sul server dell&#39;applicazione.

      `user` è il nome utente dell&#39;amministratore dei moduli di AEM.

      `password` è la password dell&#39;amministratore dei moduli AEM.

      `leaveContinuousCoverage` Utilizzate questa opzione per disabilitare completamente la modalità di backup.
   >[!NOTE]
   >
   >Per il momento in cui la modalità di backup è disattivata, non è possibile ripristinare la copertura continua. Eventuali modifiche durante tale periodo non sono protette.

   >[!NOTE]
   >
   >Se nel database è stata attivata l&#39;archiviazione dei documenti, la modalità di backup delle copie istantanee e le modalità di backup a scorrimento non sono applicabili.

   Per ulteriori informazioni sull&#39;interfaccia della riga di comando per la modalità di backup, vedere il file Leggimi nella directory BackupRestoreCommandline.

