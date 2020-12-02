---
title: Ripristino dei dati dei moduli AEM
seo-title: Ripristino dei dati dei moduli AEM
description: Questo documento descrive i passaggi necessari per recuperare i dati dei moduli AEM.
seo-description: Questo documento descrive i passaggi necessari per recuperare i dati dei moduli AEM.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---


# Ripristino dei dati dei moduli AEM {#recovering-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per recuperare i dati dei moduli AEM. Vedere anche [Considerazioni speciali per il backup e il ripristino](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>Le directory di database, GDS, AEM repository e Content Storage Root devono essere ripristinate su un computer con lo stesso nome DNS dell&#39;originale.

AEM moduli devono essere ripristinati in modo affidabile a seguito dei seguenti errori:

**Errore del disco:** per recuperare il contenuto del database è necessario il supporto di backup più recente.

**Corruzione dei dati: i** file system non registrano le transazioni passate e i sistemi potrebbero sovrascrivere accidentalmente i dati di processo richiesti.

**Errore utente: il** recupero è limitato ai dati resi disponibili dal database. Se i dati sono stati memorizzati e sono disponibili, il ripristino è semplificato.

**Power Outage, System Crash:Le API del** file system spesso non sono progettate o utilizzate in modo affidabile per evitare errori di sistema imprevisti. Se si verifica un&#39;interruzione di corrente o di sistema, è più probabile che il contenuto del documento memorizzato nel database sia aggiornato rispetto al contenuto memorizzato in un file system.

Se si utilizza la modalità di backup a rotazione, si è ancora in modalità di backup dopo il ripristino. Se si utilizza la modalità di backup snapshot, non si è in modalità di backup dopo il ripristino.

Durante il ripristino da backup a un nuovo sistema, le seguenti configurazioni potrebbero essere diverse. Questa differenza non deve incidere sul recupero corretto dell&#39;applicazione dei moduli AEM:

* Indirizzo IP
* Configurazione fisica del sistema (CPU, disco, memoria)
* Posizione GDS

>[!NOTE]
>
>Il backup della directory principale dell&#39;archivio dei contenuti deve essere ripristinato nel percorso della directory così come è stato impostato durante la configurazione di Content Services.

Se un singolo nodo di un cluster multinodo non riesce e i nodi rimanenti del cluster funzionano correttamente, eseguire la procedura di ripristino a nodo singolo del cluster.

## Recuperare i dati dei moduli AEM {#recover-the-aem-forms-data}

1. Arrestare i servizi AEM moduli e il server applicazioni se in esecuzione.
1. Se necessario, ricreate il sistema fisico da un&#39;immagine del sistema. Ad esempio, questo passaggio potrebbe non essere necessario se il motivo del ripristino è un server di database difettoso.
1. Applicare patch o aggiornamenti ai moduli AEM applicati dopo la creazione dell&#39;immagine. Queste informazioni sono state registrate nella procedura di backup. AEM moduli devono essere patch allo stesso livello di patch esistente al momento del backup del sistema.
1. (WebSphere Application Server) Se si sta eseguendo il ripristino in una nuova istanza di WebSphere Application Server, eseguire il comando restoreConfig.bat/sh.
1. Recuperare il database dei moduli AEM eseguendo prima un&#39;operazione di ripristino del database utilizzando i file di backup del database e quindi applicando i redo log delle transazioni al database recuperato. (Vedere [AEM database moduli](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, consultate uno dei seguenti articoli della knowledge base:

   * [ Oracle Backup e ripristino per i moduli AEM](https://www.adobe.com/go/kb403624)
   * [Backup e ripristino di MySQL per moduli AEM](https://www.adobe.com/go/kb403625)
   * [Backup e ripristino di Microsoft SQL Server per i moduli AEM](https://www.adobe.com/go/kb403623)
   * [Backup e ripristino DB2 per i moduli AEM](https://www.adobe.com/go/kb403626)

1. Recuperare la directory GDS eliminando prima il contenuto della directory GDS sull&#39;installazione esistente dei moduli AEM e quindi copiando il contenuto della directory GDS dal GDS di backup. Se hai modificato il percorso della directory GDS, vedi [Modifica del percorso GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Rinominare la directory di backup GDS da ripristinare come mostrato negli esempi seguenti:

   >[!NOTE]
   >
   >Se la directory /restore esiste già, eseguitene il backup ed eliminatela prima di rinominare la directory /backup che contiene i dati più recenti.

   * (JBoss) Rinominare `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` in:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Rinominare `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` in:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Rinominare `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` in:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Ripristinare la directory principale di memorizzazione dei contenuti eliminando innanzitutto il contenuto della directory principale di memorizzazione dei contenuti nell&#39;installazione esistente dei moduli AEM e recuperando quindi i contenuti seguendo le operazioni per gli ambienti standalone o cluster:

   >[!NOTE]
   >
   >Il backup della directory principale di Content Storage deve essere ripristinato nel percorso della directory principale di Content Storage, così come è stato impostato durante la configurazione di Content Services (obsoleto).

   **Standalone:** Durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Quando queste directory vengono ripristinate, se la directory /backup-lucene-index è presente, rinominatela in /lucene-indexes. In caso contrario, la directory lucene-index dovrebbe già esistere e non è richiesta alcuna azione.

   **Cluster:** durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Per ripristinare la directory radice dell&#39;indice, eseguire i seguenti passaggi su ciascun nodo del cluster:

   * Eliminate tutto il contenuto nella directory radice dell&#39;indice.
   * Se la directory /backup-lucene-index è presente, copiate il contenuto della directory *directory radice di memorizzazione dei contenuti*/backup-lucene-index nella directory radice dell&#39;indice ed eliminate la directory *directory radice di memorizzazione dei contenuti*/backup-lucene-index.
   * Se la directory /lucene-indexes è presente, copiate il contenuto della directory *directory radice dell&#39;archivio dei contenuti*/lucene-indexes nella directory radice dell&#39;indice.

1. Ripristinare/ripristinare l&#39;archivio CRX.

   * **Standalone**

      *Ripristinare le istanze* di creazione e pubblicazione: Se si verifica un errore, è possibile ripristinare il repository all&#39;ultimo stato di backup eseguendo i passaggi descritti in  [Backup e ripristino.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      Il ripristino completo del nodo Author consente di ripristinare anche i dati di Forms Manager e  AEM Forms Workspace.

   * **Cluster**

      Per il ripristino in un ambiente cluster, vedere [Strategia per il backup e il ripristino in un ambiente cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Eliminate i file temporanei AEM moduli creati nella directory java.io.temp o nella directory temporanea del Adobe .
1. Avviare AEM moduli (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modifica della posizione GDS durante il ripristino {#changing-the-gds-location-during-recovery}

Se il GDS viene ripristinato in una posizione diversa da quella in cui era originariamente, eseguite lo script LCSetGDS per impostare il GDS sulla nuova posizione. Lo script si trova nella cartella `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Lo script richiede due parametri, `defaultGDS` e `newGDS`. Per istruzioni sull&#39;esecuzione dello script, vedere il file `ReadMe.txt` nella stessa cartella.

>[!NOTE]
>
>Se nel database è stata abilitata l&#39;archiviazione dei documenti, non è necessario modificare il percorso GDS.

>[!NOTE]
>
>Questa circostanza è l&#39;unica in base alla quale si dovrebbe utilizzare questo script per modificare la posizione GDS. Per modificare la posizione GDS durante l&#39;esecuzione AEM moduli, utilizzare la console di amministrazione. (Vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La distribuzione del componente non riuscirà in Windows se la directory GDS si trova nella directory principale dell&#39;unità (ad esempio, D:\). Per GDS, è necessario assicurarsi che la directory non si trovi nella directory principale dell&#39;unità, ma che si trovi in una sottodirectory. Ad esempio, la directory deve essere D:\GDS and not simply D:\.

## Ripristino di GDS in un ambiente cluster {#recovering-the-gds-to-a-clustered-environment}

Per modificare la posizione GDS in un ambiente cluster, chiudete l&#39;intero cluster ed eseguite lo script LCSetGDS su un singolo nodo del cluster. (Vedere [Modifica della posizione GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Inizia solo quel nodo. Quando il nodo è completamente avviato, altri nodi del cluster potrebbero essere avviati in modo sicuro e verranno correttamente indirizzati al nuovo GDS.

>[!NOTE]
>
>Se non è possibile garantire l&#39;avvio completo di un nodo prima di avviare altri nodi, è necessario eseguire lo script LCSetGDS su ogni nodo del cluster prima di avviare il cluster.

