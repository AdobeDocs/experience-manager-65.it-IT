---
title: Strategia di backup e ripristino per i moduli AEM
seo-title: Backup and recovery strategy for AEM forms
description: Scopri come implementare una strategia di backup dei dati e assicurarti che rimanga sincronizzata con i dati dei moduli AEM.
seo-description: Learn how to implement a strategy to back up data and ensuring that it remains in sync with the AEM forms data.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# Strategia di backup e ripristino per i moduli AEM{#backup-and-recovery-strategy-for-aem-forms}

Se l’implementazione dei moduli di AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia di backup di tali dati e assicurarsi che rimanga sincronizzata con i dati dei moduli di AEM. Inoltre, l&#39;applicazione deve essere progettata in modo che sia abbastanza robusta da gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. Si consiglia vivamente di eseguire qualsiasi operazione di database nel contesto di una transazione per mantenere uno stato coerente.

Dopo aver identificato la modalità di utilizzo dei moduli AEM, determinare quali file devono essere sottoposti a backup, la frequenza e la finestra di backup da rendere disponibili.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell&#39;implementazione dei moduli di AEM, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di staging prima di essere utilizzata in produzione, al fine di garantire che l&#39;intera soluzione funzioni come previsto senza perdita di dati.

Adobe Experience Manager (AEM) è parte integrante dei moduli AEM. Pertanto, è necessario eseguire il backup di AEM e in sincronia con il backup dei moduli AEM come soluzione e servizi di gestione della corrispondenza, come Forms Manager sono basati su dati memorizzati AEM parte dei moduli AEM.Per evitare perdite di dati, i dati specifici dei moduli AEM devono essere sottoposti a backup in modo da garantire che GDS e AEM (archivio) siano correlati a riferimenti al database.Il database, GDS, AEM e le directory principali di archiviazione dei contenuti devono essere ripristinati in un computer con lo stesso nome DNS originale.

## Tipi di backup {#types-of-backups}

La strategia di backup dei moduli AEM prevede due tipi di backup:

**Immagine del sistema:** Backup completo del sistema che è possibile utilizzare per ripristinare il contenuto del computer se il disco rigido o l&#39;intero computer smette di funzionare. È necessario un backup dell’immagine di sistema solo prima della distribuzione di produzione di moduli AEM. I criteri aziendali interni determinano la frequenza con cui sono necessari i backup delle immagini del sistema.

**Dati specifici dei moduli AEM:** I dati dell&#39;applicazione esistono nel database, nell&#39;archivio GDS (Global Document Storage) e nell&#39;archivio AEM e devono essere sottoposti a backup in tempo reale. GDS è una directory utilizzata per memorizzare file longevi utilizzati all’interno di un processo. Tali file possono includere PDF, criteri o modelli di moduli.

>[!NOTE]
>
>Se è installato Content Services (obsoleto), esegui anche il backup della directory principale di archiviazione dei contenuti. Vedi [Directory principale di archiviazione dei contenuti (solo Content Services)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

Il database viene utilizzato per memorizzare gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti al database ai file GDS. Se nel database è stata abilitata l’archiviazione dei documenti, anche i dati e i documenti persistenti nel GDS vengono memorizzati nel database. È possibile eseguire il backup e il ripristino del database utilizzando i seguenti metodi:

* **Backup snapshot** la modalità indica che il sistema dei moduli AEM è in modalità di backup a tempo indefinito o per un numero specificato di minuti, dopo di che la modalità di backup non è più abilitata. Per entrare o uscire dalla modalità di backup dello snapshot, è possibile utilizzare una delle opzioni seguenti. Dopo uno scenario di ripristino, la modalità di backup dello snapshot non deve essere abilitata.

   * Utilizzare la pagina Impostazioni backup in Admin Console. Per accedere alla modalità snapshot, selezionare la casella di controllo Opera in modalità backup sicuro. Deselezionare la casella di controllo per uscire dalla modalità snapshot.
   * Utilizzare lo script LCBackupMode (vedere [Esegui il backup delle directory radice del database, GDS e Content Storage](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Per uscire dalla modalità di backup dello snapshot, nell&#39;argomento script, impostare il `continuousCoverage` parametro a `false` o utilizzare `leaveContinuousCoverage` opzione .
   * Utilizzare l&#39;API di backup/ripristino fornita. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Backup continuo** La modalità indica che il sistema è sempre in modalità di backup e che viene avviata una nuova sessione in modalità di backup non appena viene rilasciata la sessione precedente. Nessun timeout associato alla modalità di backup in esecuzione. Quando lo script LCBackupMode o le API vengono chiamate per uscire dalla modalità di backup in esecuzione, inizia una nuova sessione in modalità di backup in esecuzione. Questa modalità è utile per supportare backup continui, ma consente comunque di eliminare dalla directory GDS i documenti vecchi e non necessari. La modalità di backup continuo non è supportata dalla pagina Backup e ripristino. Dopo uno scenario di ripristino, la modalità di backup continuo è ancora abilitata. È possibile uscire dalla modalità di backup continuo (modalità di backup continuo) utilizzando lo script LCBackupMode con il `leaveContinuousCoverage` opzione .

>[!NOTE]
>
>Se si esce dalla modalità di backup continuo, viene immediatamente avviata una nuova sessione in modalità di backup. Per disattivare completamente la modalità di backup continuo, utilizza la `leaveContinuousCoverage` nello script, che sovrascrive la sessione di backup continuo esistente. In modalità backup snapshot, è possibile lasciare la modalità di backup come si fa di solito.

Per evitare la perdita di dati, è necessario eseguire il backup dei dati specifici dei moduli AEM in modo da garantire la correlazione tra i documenti della directory principale di archiviazione e GDS e i riferimenti al database.

>[!NOTE]
>
>Quando il GDS viene memorizzato nel file system e non nel database, eseguire il backup del database prima del backup GDS.

## Considerazioni speciali per il backup e il ripristino {#special-considerations-for-backup-and-recovery}

Se è necessario ripristinare AEM moduli in un ambiente diverso a causa delle seguenti modifiche, attenersi alle linee guida seguenti:

* Modifica dell’indirizzo IP, del nome host o della porta del server dei moduli AEM
* Modifica delle lettere di unità o del percorso della directory
* Passare a un host di database, una porta o un nome diverso

In genere, tali scenari di ripristino sono causati da un errore hardware del server che ospita l&#39;application server, il database server o il server forms. Oltre alle configurazioni specifiche per i moduli AEM descritte in questa sezione, è necessario apportare le modifiche necessarie per altre parti della distribuzione dei moduli di AEM, ad esempio load balancer e firewall, se il nome host o l’indirizzo IP di un server AEM forms cambia.

### Cosa non può essere modificato {#what-cannot-be-changed}

Anche se è possibile modificare il server di database e molti altri parametri, non è possibile modificare il tipo di server applicazioni o il tipo di database quando si ripristinano AEM moduli da un backup. Ad esempio, se si sta recuperando un backup di moduli AEM, non è possibile modificare il server dell&#39;applicazione da JBoss a WebLogic o il database da Oracle a DB2. Inoltre, i moduli AEM recuperati devono utilizzare gli stessi percorsi del file system, ad esempio la directory dei font.

### Riavvio dopo un ripristino {#restarting-after-a-recovery}

Prima di riavviare il server dei moduli dopo un ripristino, eseguire le operazioni seguenti:

1. Avviare il sistema in modalità manutenzione.
1. Per garantire la sincronizzazione di Form Manager con AEM moduli in modalità di manutenzione, effettuare le operazioni seguenti:

   1. Vai su https://&lt;*server*>:&lt;*porta*>/lc/fm e accedi utilizzando le credenziali amministratore/password.
   1. Fai clic sul nome dell’utente (in questo caso l’amministratore avanzato) nell’angolo in alto a destra.
   1. Fai clic su **Opzioni di amministrazione**.
   1. Fai clic su **Inizio** per sincronizzare le risorse dall’archivio.

1. In un ambiente cluster, il nodo principale (rispetto a AEM) deve trovarsi in primo piano prima dei nodi secondari.
1. Assicurati che non vengano avviati processi da origini interne o esterne, quali Web, SOAP o EJB, fino a quando non viene convalidato il normale funzionamento del sistema.

Se il database dei moduli principali AEM viene spostato o modificato, consultare le guide all’installazione relative al server applicazioni per informazioni sull’aggiornamento delle informazioni sulla connessione al database per le origini dati dei moduli AEM IDP_DS e EDC_DS.

### Modifica del nome host o dell’indirizzo IP di AEM forms {#changing-the-aem-forms-hostname-or-ip-address}

In un cluster, se si utilizza il caching TCP invece di UDP, è necessario aggiornare la configurazione del localizzatore della cache. Consulta &quot;Configuring the caching locators (caching using only TCP)&quot; nella guida alla configurazione relativa al server applicativo.

### Modifica dei percorsi dei file system dei nodi AEM {#changing-the-aem-forms-node-file-system-paths}

Se si modificano i percorsi dei file system per un nodo autonomo, è necessario aggiornare i riferimenti appropriati nelle preferenze, nelle altre configurazioni di sistema, nelle applicazioni personalizzate e nelle applicazioni di moduli AEM distribuite. D&#39;altro canto, per un cluster, tutti i nodi devono utilizzare la stessa configurazione del percorso del file system. È necessario impostare la directory principale GDS (Global Document Storage) e assicurarsi che faccia riferimento a una copia del GDS recuperato che è sincronizzata con il database recuperato. L&#39;impostazione del percorso GDS è importante perché il GDS può contenere dati destinati a persistere tra i riavvii dell&#39;application server.

In un ambiente cluster, la configurazione del percorso del file system dell&#39;archivio deve essere la stessa per tutti i nodi del cluster prima del backup e dopo il ripristino.

Utilizza la `LCSetGDS`nel `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` per impostare il percorso GDS dopo aver modificato i percorsi del file system. Consulta la sezione `ReadMe.txt` nella stessa cartella per ulteriori informazioni. Se non è possibile utilizzare il vecchio percorso della directory GDS, `LCSetGDS` per impostare il nuovo percorso del GDS prima di avviare AEM moduli, è necessario utilizzare lo script.

>[!NOTE]
>
>Questa circostanza è l’unica in cui è necessario utilizzare questo script per modificare la posizione GDS. Per modificare la posizione GDS durante l’esecuzione AEM moduli, utilizzare la console di amministrazione. (Vedi [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.

Dopo aver impostato il percorso GDS, avviare il server dei moduli in modalità di manutenzione e utilizzare la console di amministrazione per aggiornare i percorsi dei file system rimanenti per il nuovo nodo. Dopo aver verificato l’aggiornamento di tutte le configurazioni necessarie, riavviare e verificare AEM moduli.
