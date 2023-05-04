---
title: Ripristino dei dati dei moduli AEM
seo-title: Recovering the AEM forms data
description: Questo documento descrive i passaggi necessari per recuperare i dati dei moduli AEM.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# Ripristino dei dati dei moduli AEM {#recovering-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per recuperare i dati dei moduli AEM. Vedi anche [Considerazioni speciali per il backup e il ripristino](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>È necessario ripristinare il database, GDS, AEM repository e le directory principali di archiviazione dei contenuti in un computer con lo stesso nome DNS dell&#39;originale.

AEM moduli devono essere ripristinati in modo affidabile dai seguenti errori:

**Errore disco:** Il supporto di backup più recente è necessario per recuperare il contenuto del database.

**Corruzione dei dati:** I file system non registrano le transazioni passate e i sistemi potrebbero accidentalmente sovrascrivere i dati di processo richiesti.

**Errore utente:** Il recupero è limitato ai dati resi disponibili dal database. Se i dati sono stati memorizzati e sono disponibili, il ripristino è semplificato.

**Interruzione di corrente, crash di sistema:** Le API del file system spesso non sono progettate o utilizzate in modo affidabile per evitare errori di sistema imprevisti. Se si verifica un&#39;interruzione dell&#39;alimentazione o un arresto anomalo del sistema, è più probabile che il contenuto del documento memorizzato nel database sia aggiornato rispetto al contenuto memorizzato in un file system.

Se si utilizza la modalità di backup a rotazione, si è ancora in modalità di backup dopo il ripristino. Se si utilizza la modalità di backup dello snapshot, non si è in modalità di backup dopo il ripristino.

Quando si esegue il ripristino da un backup a un nuovo sistema, le configurazioni seguenti possono essere diverse. Questa differenza non dovrebbe incidere sul corretto recupero dell’applicazione dei moduli di AEM:

* Indirizzo IP
* Configurazione fisica del sistema (CPU, disco, memoria)
* Posizione GDS

>[!NOTE]
>
>Il backup della directory principale di archiviazione dei contenuti deve essere ripristinato nel percorso di tale directory così come è stato impostato durante la configurazione di Content Services.

Se un singolo nodo di un cluster multinode non è riuscito e i nodi rimanenti del cluster funzionano correttamente, eseguire la procedura di ripristino a nodo singolo del cluster.

## Recuperare i dati dei moduli AEM {#recover-the-aem-forms-data}

1. Arrestare i servizi e il server applicazioni di AEM forms se in esecuzione.
1. Se necessario, ricreare il sistema fisico da un&#39;immagine di sistema. Ad esempio, questo passaggio potrebbe non essere necessario se il motivo del ripristino è un database server difettoso.
1. Applicare patch o aggiornamenti ai moduli AEM applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate nella procedura di backup. AEM moduli devono essere patch allo stesso livello di patch di quando è stato eseguito il backup del sistema.
1. (WebSphere® Application Server) Se si esegue il ripristino in una nuova istanza di WebSphere® Application Server, eseguire il comando restoreConfig.bat/sh.
1. Ripristinare il database dei moduli AEM eseguendo prima un&#39;operazione di ripristino del database utilizzando i file di backup del database e quindi applicando i redo log delle transazioni al database recuperato. (Vedi [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, vedere uno dei seguenti articoli della knowledge base:

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Backup e ripristino di Oracle per i moduli AEM](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [Backup e ripristino di MySQL per i moduli AEM](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Recuperare la directory GDS eliminando prima il contenuto della directory GDS sull&#39;installazione esistente di moduli AEM e quindi copiando il contenuto della directory GDS dal GDS di backup. Se hai modificato la posizione della directory GDS, vedi [Modifica della posizione GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Rinomina la directory di backup GDS da ripristinare come mostrato nei seguenti esempi:

   >[!NOTE]
   >
   >Se la directory /restore esiste già, eseguine il backup e quindi eliminala prima di rinominare la directory /backup che contiene i dati più recenti.

   * Rinomina (JBoss®) `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` a:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * Rinomina (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` a:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * Rinomina (WebSphere®) `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` a:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Ripristinare la directory principale di archiviazione dei contenuti eliminando prima il contenuto della directory principale di archiviazione dei contenuti nell&#39;installazione esistente dei moduli AEM e quindi recuperando il contenuto seguendo le attività per gli ambienti stand-alone o cluster:

   >[!NOTE]
   >
   >Il backup della directory principale di archiviazione dei contenuti deve essere ripristinato nel percorso della directory principale di archiviazione dei contenuti come è stato impostato durante la configurazione di Content Services (obsoleto).

   **Standalone:** Durante il processo di ripristino, ripristinare tutte le directory sottoposte a backup. Quando queste directory vengono ripristinate, se la directory /backup-lucene-indexes è presente, rinominala in /lucene-indexes. In caso contrario, la directory lucene-indexes dovrebbe già esistere e non è necessaria alcuna azione.

   **Cluster:** Durante il processo di ripristino, ripristinare tutte le directory sottoposte a backup. Per ripristinare la directory principale indice, esegui i seguenti passaggi su ciascun nodo del cluster:

   * Elimina tutto il contenuto della directory radice indice.
   * Se la directory /backup-lucene-indexes è presente, copia il contenuto del *Directory principale di archiviazione dei contenuti*/backup-lucene-indexes directory alla directory radice indice ed elimina il *Directory principale di archiviazione dei contenuti*/backup-lucene-indexes directory.
   * Se la directory /lucene-indexes è presente, copia il contenuto del *Directory principale di archiviazione dei contenuti*/lucene-indexes nella directory radice indice.

1. Ripristina/ripristina l&#39;archivio CRX.

   * **Standalone**

      *Ripristinare le istanze di authoring e pubblicazione*: Se si verifica un problema, puoi ripristinare l’archivio all’ultimo stato di backup eseguendo i passaggi descritti in [Backup e ripristino.](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      Il ripristino completo del nodo Author verifica il ripristino dei dati di Forms Manager e AEM Forms Workspace.

   * **Cluster**

      Per il ripristino in un ambiente cluster, consulta [Strategia di backup e ripristino in un ambiente cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Elimina i file temporanei dei moduli AEM creati nella directory java.io.temp o nella directory temporanea di Adobe.
1. Avvia AEM moduli (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modifica della posizione GDS durante il ripristino {#changing-the-gds-location-during-recovery}

Se il GDS viene ripristinato in una posizione diversa da quella in cui era originariamente, esegui lo script LCSetGDS per impostare il GDS nella nuova posizione. Lo script è nel `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` cartella. Lo script prende due parametri, `defaultGDS` e `newGDS`. Consulta la sezione `ReadMe.txt` nella stessa cartella per istruzioni su come eseguire lo script.

>[!NOTE]
>
>Se nel database è stata abilitata l’archiviazione dei documenti, non è necessario modificare il percorso GDS.

>[!NOTE]
>
>Questa circostanza è l’unica in cui è necessario utilizzare questo script per modificare la posizione GDS. Per modificare la posizione GDS durante l’esecuzione AEM moduli, utilizzare la console di amministrazione. (Vedi [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La distribuzione dei componenti avrà esito negativo su Windows se la directory GDS si trova nella directory principale dell’unità (ad esempio, D:\). Per GDS, è necessario assicurarsi che la directory non si trovi nella directory principale dell&#39;unità ma si trovi in una sottodirectory. Ad esempio, la directory deve essere D:\GDS and not simply D:\.

## Ripristino degli GDS in un ambiente cluster {#recovering-the-gds-to-a-clustered-environment}

Per modificare la posizione GDS in un ambiente cluster, arresta l&#39;intero cluster ed esegui lo script LCSetGDS su un singolo nodo del cluster. (Vedi [Modifica della posizione GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Avvia solo quel nodo. Quando quel nodo è completamente avviato, altri nodi del cluster possono essere avviati in modo sicuro e punteranno correttamente al nuovo GDS.

>[!NOTE]
>
>Se non è possibile garantire l&#39;avvio completo di un nodo prima di avviare altri nodi, è necessario eseguire lo script LCSetGDS su ogni nodo del cluster prima di avviare il cluster.
