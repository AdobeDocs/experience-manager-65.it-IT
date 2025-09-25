---
title: Recupero dei dati di AEM Forms
description: Questo documento descrive i passaggi necessari per recuperare i dati di AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1118'
ht-degree: 100%

---

# Recupero dei dati di AEM Forms {#recovering-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per recuperare i dati di AEM Forms. Consulta anche [Considerazioni speciali per il backup e il ripristino](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>È necessario ripristinare il database, il GDS, l’archivio AEM e le directory principali di archiviazione dei contenuti in un computer con lo stesso nome DNS dell’originale.

AEM Forms deve essere ripristinato in modo affidabile dai seguenti errori:

**Errore disco:** per ripristinare il contenuto del database è necessario il supporto di backup più recente.

**Danneggiamento dati:** i file system non registrano le transazioni passate e i sistemi potrebbero accidentalmente sovrascrivere i dati di processo richiesti.

**Errore utente:** il recupero è limitato ai dati resi disponibili dal database. Se i dati sono stati memorizzati e sono disponibili, il ripristino è semplificato.

**Interruzione dell’alimentazione, arresto anomalo del sistema:** le API del file system spesso non sono progettate o utilizzate in modo affidabile per evitare errori di sistema imprevisti. Se si verifica un’interruzione dell’alimentazione o un arresto anomalo del sistema, è più probabile che sia aggiornato il contenuto del documento memorizzato nel database rispetto al contenuto memorizzato in un file system.

Se utilizzi la modalità di backup continuo, è ancora attiva la modalità di backup dopo il ripristino. Se utilizzi la modalità di backup di istantanee, non è attiva la modalità di backup dopo il ripristino.

Quando esegui il ripristino da un backup in un nuovo sistema, le seguenti configurazioni possono essere diverse. Questa differenza non dovrebbe influire sul corretto ripristino dell’applicazione AEM Forms:

* Indirizzo IP
* Configurazione del sistema fisico (CPU, disco, memoria)
* Posizione GDS

>[!NOTE]
>
>Il backup della directory principale di archiviazione dei contenuti deve essere ripristinato nella posizione della directory in base a come era impostata durante la configurazione di Content Services.

Se un singolo nodo di un cluster multinodo non viene eseguito con successo e i nodi rimanenti del cluster funzionano correttamente, esegui la procedura di ripristino del cluster a nodo singolo.

## Recuperare i dati di AEM Forms {#recover-the-aem-forms-data}

1. Arresta il server applicazioni e i servizi di AEM Forms se in esecuzione.
1. Se necessario, ricrea il sistema fisico da un’immagine di sistema. Ad esempio, questo passaggio potrebbe non essere necessario se il motivo del ripristino è un server di database difettoso.
1. Applica patch o aggiornamenti ad AEM Forms che sono stati applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate nella procedura di backup. Per AEM Forms è necessario eseguire l’operazione patch allo stesso livello di patch utilizzato al momento del backup.
1. (Server applicazioni WebSphere®) Se si stai eseguendo il ripristino in una nuova istanza del server applicazioni WebSphere®, esegui il comando restoreConfig.bat/sh.
1. Recupera il database di AEM Forms eseguendo prima un’operazione di ripristino del database tramite i file di backup del database, dopodiché applica i registri di ripetizione delle transazioni al database ripristinato. Consulta [database di AEM forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database). Per ulteriori informazioni, consulta uno di questi articoli della knowledge base:

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Backup e ripristino Oracle per AEM Forms](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [Backup e ripristino MySQL per AEM Forms](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Recupera la directory GDS eliminando prima il contenuto della directory GDS nell’installazione esistente di AEM Forms e quindi copiando il contenuto della directory GDS da quella di cui è stato eseguito il backup. Se hai modificato il percorso della directory GDS, consulta [Modificare il percorso GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Rinomina la directory di backup GDS da ripristinare come illustrato negli esempi seguenti:

   >[!NOTE]
   >
   >Se la directory /restore esiste già, eseguirne il backup e quindi eliminarla prima di rinominare la directory /backup che contiene i dati più recenti.

   * (JBoss®) Rinomina `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` in:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Rinomina `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` in:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Rinomina `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` in:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Ripristina la directory principale di archiviazione dei contenuti eliminando prima il contenuto della directory principale di archiviazione dei contenuti nell’installazione esistente di AEM Forms e quindi recuperando il contenuto seguendo le attività per gli ambienti autonomi o cluster:

   >[!NOTE]
   >
   >Il backup della directory principale di archiviazione dei contenuti deve essere ripristinato nella posizione di quella impostata durante la configurazione di Content Services (obsoleto).

   **Standalone:** durante il processo di ripristino, ripristina tutte le directory di cui è stato eseguito il backup. Quando queste directory vengono ripristinate, se è presente la directory /backup-lucene-indexes, rinominala /lucene-indexes. In caso contrario, la directory degli indici di tipo Lucene dovrebbe già esistere e non è richiesta alcuna azione.

   **Cluster:** durante il processo di ripristino, ripristina tutte le directory di cui è stato eseguito il backup. Per ripristinare la directory principale dell’indice, effettua le seguenti operazioni su ciascun nodo del cluster:

   * Elimina tutto il contenuto nella directory principale dell’indice.
   * Se la directory /backup-lucene-indexes è presente, copia il contenuto della *directory principale dell’archiviazione dei contenuti*/backup-lucene-indexes nella directory principale dell’indice ed elimina la *directory principale dell’archiviazione dei contenuti*/backup-lucene-indexes.
   * Se la directory /lucene-indexes è presente, copia il contenuto della *directory principale di archiviazione del contenuto*/lucene-indexes nella directory principale dell’indice.

1. Ripristina/recupera l’archivio CRX.

   * **Standalone**

     *Ripristina istanze di authoring e pubblicazione*: se si verifica un errore irreversibile, puoi ripristinare l’ultimo stato di backup del repository eseguendo i passaggi descritti in [Backup e ripristino.](https://helpx.adobe.com/it/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

     Il ripristino completo del nodo di authoring verifica anche il ripristino dei dati di Forms Manager e AEM Forms Workspace.

   * **Cluster**

     Per il ripristino in un ambiente cluster, consulta [Strategia di backup e ripristino in un ambiente cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Elimina tutti i file temporanei di AEM Form creati nella directory java.io.temp o nella directory temporanea di Adobe.
1. Avvia AEM Forms (consulta [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modificare la posizione GDS durante il ripristino {#changing-the-gds-location-during-recovery}

Se il GDS viene ripristinato in una posizione diversa da quella originale, esegui lo script LCSetGDS per impostare il GDS nella nuova posizione. Lo script si trova nella cartella `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Lo script accetta due parametri, `defaultGDS` e `newGDS`. Per istruzioni su come eseguire lo script, consulta il file `ReadMe.txt` nella stessa cartella.

>[!NOTE]
>
>Se hai abilitato l’archiviazione dei documenti nel database, non è necessario che modifichi la posizione di GDS.

>[!NOTE]
>
>Questa circostanza è l’unica in base alla quale utilizzare questo script per modificare la posizione del GDS. Per modificare la posizione del GDS durante l’esecuzione di AEM Forms, utilizza la console di amministrazione. Consulta [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

>[!NOTE]
>
>La distribuzione dei componenti non andrà a buon fine in Windows se la directory GDS si trova nella directory principale dell’unità (ad esempio, D:\). Per GDS, devi assicurarti che la directory non si trovi al livello principale dell’unità, ma in una sottodirectory. Ad esempio, la directory dovrebbe essere D:\GDS e non semplicemente D:\.

## Ripristino di GDS in un ambiente cluster {#recovering-the-gds-to-a-clustered-environment}

Per modificare la posizione GDS in un ambiente cluster, arresta l’intero cluster ed esegui lo script LCSetGDS su un singolo nodo del cluster. Consulta [Modifica del percorso GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery). Avvia solo tale nodo. Quando il nodo è completamente avviato, gli altri nodi del cluster possono essere avviati in modo sicuro e punteranno correttamente al nuovo GDS.

>[!NOTE]
>
>Se non puoi assicurarti di avviare completamente un nodo prima di avviarne altri, prima di avviare il cluster, devi eseguire lo script LCSetGDS su ogni suo nodo.
