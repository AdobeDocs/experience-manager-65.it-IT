---
title: Recupero dei dati dei moduli dell’AEM
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Recupero dei dati dei moduli dell’AEM {#recovering-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per recuperare i dati dei moduli AEM. Vedi anche [Considerazioni speciali per il backup e il ripristino](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>È necessario ripristinare il database, il GDS, l&#39;archivio AEM e le directory radice di archiviazione del contenuto in un computer con lo stesso nome DNS dell&#39;originale.

Le forme di AEM devono recuperare in modo affidabile dai seguenti fallimenti:

**Errore disco:** Per ripristinare il contenuto del database è necessario disporre del supporto di backup più recente.

**Danneggiamento dei dati:** I file system non registrano le transazioni passate e possono sovrascrivere accidentalmente i dati di processo richiesti.

**Errore utente:** Il recupero è limitato ai dati resi disponibili dal database. Se i dati sono stati memorizzati e sono disponibili, il ripristino è semplificato.

**Interruzione di corrente, Arresto anomalo del sistema:** Le API del file system spesso non sono progettate o utilizzate in modo affidabile per evitare errori di sistema imprevisti. Se si verifica un&#39;interruzione dell&#39;alimentazione o un arresto anomalo del sistema, è più probabile che il contenuto del documento memorizzato nel database sia aggiornato rispetto al contenuto memorizzato in un file system.

Se si utilizza la modalità di backup continuo, è ancora attiva la modalità di backup dopo il ripristino. Se si utilizza la modalità di backup delle copie istantanee, non è attiva la modalità di backup dopo il ripristino.

Quando si esegue il ripristino da un backup in un nuovo sistema, le seguenti configurazioni possono essere diverse. Questa differenza non dovrebbe influire sul corretto recupero dell’applicazione dei moduli AEM:

* Indirizzo IP
* Configurazione del sistema fisico (CPU, disco, memoria)
* Posizione GDS

>[!NOTE]
>
>Il backup della directory radice di archiviazione dei contenuti deve essere ripristinato nella posizione della directory impostata durante la configurazione di Content Services.

Se un singolo nodo di un cluster multinodo non riesce e i nodi rimanenti del cluster funzionano correttamente, eseguire la procedura di ripristino del cluster a nodo singolo.

## Recuperare i dati dei moduli AEM {#recover-the-aem-forms-data}

1. Arrestare il server applicazioni e i servizi di moduli AEM se in esecuzione.
1. Se necessario, ricreare il sistema fisico da un&#39;immagine di sistema. Ad esempio, questo passaggio potrebbe non essere necessario se il motivo del ripristino è un server di database difettoso.
1. Applica patch o aggiornamenti ai moduli AEM applicati dal momento in cui è stata creata l’immagine. Queste informazioni sono state registrate nella procedura di backup. I moduli AEM devono essere sottoposti a patch allo stesso livello di patch utilizzato al momento del backup del sistema.
1. (Server applicazioni WebSphere®) Se si sta eseguendo il ripristino in una nuova istanza dell&#39;Application Server WebSphere®, eseguire il comando restoreConfig.bat/sh.
1. Recuperare il database dei moduli AEM eseguendo prima un&#39;operazione di ripristino del database utilizzando i file di backup del database e quindi applicando i redo log delle transazioni al database ripristinato. (vedere [Database dei moduli AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, consulta uno dei seguenti articoli della knowledge base:

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Oracle di backup e ripristino per i moduli AEM](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [Backup e ripristino MySQL per moduli AEM](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Recuperare la directory GDS eliminando prima il contenuto della directory GDS sull&#39;installazione esistente dei moduli AEM e quindi copiando il contenuto della directory GDS dal GDS di cui è stato eseguito il backup. Se è stato modificato il percorso della directory GDS, vedere [Modifica della posizione GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Rinominare la directory di backup GDS da ripristinare come illustrato negli esempi seguenti:

   >[!NOTE]
   >
   >Se la directory /restore esiste già, eseguirne il backup e quindi eliminarla prima di rinominare la directory /backup che contiene i dati più recenti.

   * (JBoss®) Rinomina `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` a:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Rinomina `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` a:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Rinomina `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` a:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Ripristinare la directory radice di archiviazione dei contenuti eliminando prima il contenuto della directory radice di archiviazione dei contenuti nell’installazione esistente dei moduli AEM e quindi recuperando i contenuti seguendo le attività per gli ambienti autonomi o cluster:

   >[!NOTE]
   >
   >Il backup della directory radice di archiviazione dei contenuti deve essere ripristinato nella posizione della directory radice di archiviazione dei contenuti impostata durante la configurazione di Content Services (obsoleto).

   **Standalone:** Durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Quando queste directory vengono ripristinate, se è presente la directory /backup-lucene-indexes, rinominarla in /lucene-indexes. In caso contrario, la directory degli indici di tipo Lucene dovrebbe già esistere e non è richiesta alcuna azione.

   **Cluster:** Durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Per ripristinare la directory principale dell&#39;indice, effettuare le seguenti operazioni su ciascun nodo del cluster:

   * Elimina tutto il contenuto nella directory radice indice.
   * Se è presente la directory /backup-lucene-indexes, copia il contenuto della *Directory principale archiviazione contenuti*/backup-lucene-indexes nella directory principale dell&#39;indice ed eliminare *Directory principale archiviazione contenuti* directory /backup-lucene-indexes.
   * Se è presente la directory /lucene-indexes, copia il contenuto della *Directory principale archiviazione contenuti*/lucene-indicizza la directory nella directory radice indice.

1. Ripristina/ripristina l’archivio CRX.

   * **Standalone**

     *Ripristinare le istanze di authoring e pubblicazione*: in caso di guasto, è possibile ripristinare l&#39;ultimo stato di backup dell&#39;archivio eseguendo i passaggi descritti in [Backup e ripristino.](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

     Il ripristino completo del nodo Author verifica anche il ripristino dei dati di Forms Manager e AEM Forms Workspace.

   * **Clustered**

     Per il ripristino in un ambiente cluster, vedere [Strategia di backup e ripristino in un ambiente cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Eliminare tutti i file temporanei dei moduli AEM creati nella directory java.io.temp o nella directory temporanea di Adobe.
1. Avviare i moduli AEM (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modifica della posizione GDS durante il ripristino {#changing-the-gds-location-during-recovery}

Se il GDS viene ripristinato in una posizione diversa da quella originale, eseguire lo script LCSetGDS per impostare il GDS nella nuova posizione. Lo script è nel `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` cartella. Lo script accetta due parametri: `defaultGDS` e `newGDS`. Consulta la `ReadMe.txt` nella stessa cartella per istruzioni su come eseguire lo script.

>[!NOTE]
>
>Se nel database è stata abilitata l&#39;archiviazione dei documenti, non è necessario modificare la posizione di GDS.

>[!NOTE]
>
>Questa circostanza è l&#39;unica in base alla quale utilizzare questo script per modificare la posizione di GDS. Per modificare la posizione di GDS mentre i moduli AEM sono in esecuzione, utilizzare la console di amministrazione. (vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La distribuzione dei componenti non riuscirà in Windows se la directory GDS si trova nella directory principale dell&#39;unità (ad esempio, D:\). Per GDS, è necessario assicurarsi che la directory non si trovi nella radice dell&#39;unità, ma in una sottodirectory. Ad esempio, la directory dovrebbe essere D:\GDS e non semplicemente D:\.

## Ripristino di GDS in un ambiente cluster {#recovering-the-gds-to-a-clustered-environment}

Per modificare la posizione GDS in un ambiente cluster, arrestare l&#39;intero cluster ed eseguire lo script LCSetGDS su un singolo nodo del cluster. (vedere [Modifica della posizione GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Avvia solo quel nodo. Quando il nodo è completamente avviato, gli altri nodi del cluster possono essere avviati in modo sicuro e punteranno correttamente al nuovo GDS.

>[!NOTE]
>
>Se non è possibile assicurarsi di avviare completamente un nodo prima di avviare altri nodi, è necessario eseguire lo script LCSetGDS su ogni nodo del cluster prima di avviare il cluster.
