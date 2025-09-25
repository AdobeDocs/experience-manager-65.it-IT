---
title: Strategia di backup e ripristino di AEM Forms
description: Informazioni su come implementare una strategia per eseguire il backup dei dati e assicurarsi che rimangano sincronizzati con i dati dei moduli di AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1518'
ht-degree: 100%

---

# Strategia di backup e ripristino di AEM Forms{#backup-and-recovery-strategy-for-aem-forms}

Se l’implementazione di AEM Forms memorizza dati personalizzati aggiuntivi in un database diverso, è responsabilità dell’utente implementare una strategia per eseguire il backup di tali dati e assicurarsi che rimangano sincronizzati con i dati di AEM Forms. Inoltre, l’applicazione deve essere progettata in modo da essere sufficientemente solida per gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. Si consiglia vivamente di eseguire le operazioni di database nel contesto di una transazione per mantenere uno stato coerente.

Dopo aver identificato la modalità di utilizzo di AEM Forms, determinare quali file devono essere sottoposti a backup, la frequenza di esecuzione e la finestra di backup da rendere disponibile.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell’implementazione di AEM Forms, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di staging prima di essere utilizzata in produzione per garantire che l’intera soluzione funzioni come previsto senza perdita di dati.

Adobe Experience Manager (AEM) è parte integrante di AEM Forms. Pertanto, è necessario eseguire il backup di AEM e sincronizzarlo con il backup di AEM Forms come soluzione e servizi per la gestione della corrispondenza, come Forms Manager, che si basano sui dati memorizzati nella parte AEM di AEM forms. Per evitare perdite di dati, è necessario eseguire il backup dei dati specifici di AEM Forms in modo da garantire la correlazione tra GDS e AEM (archivio) e i riferimenti al database. Le directory radice di database, GDS, AEM e Content Storage devono essere ripristinate su un computer con lo stesso nome DNS dell’originale.

## Tipi di backup {#types-of-backups}

La strategia di backup di AEM Forms prevede due tipi di backup:

**Immagine di sistema:** backup di sistema completo che è possibile utilizzare per ripristinare il contenuto del computer, se il disco rigido o l’intero computer smette di funzionare. Il backup dell’immagine di sistema è necessario solo prima della distribuzione in produzione di AEM Forms. Le regole aziendali interne determinano la frequenza con cui vengono richiesti i backup delle immagini di sistema.

**Dati specifici di AEM Forms:** i dati dell’applicazione sono presenti nel database, nel GDS (Archiviazione documenti globale) e nell’archivio di AEM e devono essere sottoposti a backup in tempo reale. GDS è una directory utilizzata per archiviare i file di lunga durata utilizzati all’interno di un processo. Tali file possono includere PDF, criteri o modelli di modulo.

>[!NOTE]
>
>Se il servizio contenuti (obsoleto) è installato, esegui anche il backup della directory principale di archiviazione dei contenuti. Consulta [Directory principale di archiviazione dei contenuti (solo Servizio contenuti)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

Il database viene utilizzato per archiviare gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti del database ai file GDS. Se nel database è stata abilitata l’archiviazione dei documenti, anche i dati e i documenti persistenti in GDS vengono memorizzati nel database. È possibile eseguire il backup e il ripristino del database utilizzando i metodi seguenti:

* La modalità **Backup istantanea** indica che il sistema AEM Forms è in una modalità di backup, a tempo indefinito oppure per un numero specificato di minuti, dopo i quali non risulterà più abilitata. Per entrare o uscire dalla modalità di backup istantanea, è possibile utilizzare una delle opzioni seguenti. Dopo uno scenario di ripristino, la modalità di backup istantanea non deve essere abilitata.

   * Utilizza la pagina Impostazioni di backup nella console di amministrazione. Per attivare la modalità istantanea, seleziona la casella di controllo Esegui in modalità di backup sicuro. Deseleziona la casella di controllo per uscire dalla modalità istantanea.
   * Utilizza lo script LCBackupMode (consulta [Eseguire il backup del database, di GDS e delle directory principali dell’archiviazione dei contenuti](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Per uscire dalla modalità di backup istantanea, nell’argomento dello script imposta il parametro `continuousCoverage` su `false` o utilizza l’opzione `leaveContinuousCoverage`.
   * Utilizza l’API di backup/ripristino fornita. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* La modalità di **backup continuo** indica che il sistema è sempre in modalità di backup, con una nuova sessione che viene avviata non appena viene rilasciata quella precedente. Alla modalità di backup continuo non è associato alcun timeout. Quando lo script o le API LCBackupMode vengono chiamati per uscire dalla modalità di backup continuo, viene avviata una nuova sessione di tale modalità. Questa modalità è utile per supportare backup continui, ma consente comunque di eliminare dalla directory GDS i documenti vecchi e non necessari. La modalità di backup continuo non è supportata dalla pagina Backup e ripristino. Dopo uno scenario di ripristino, la modalità di backup continuo rimane abilitata. È possibile uscire dalla modalità di backup continuo (rolling backup mode) utilizzando lo script LCBackupMode con l’opzione `leaveContinuousCoverage`.

>[!NOTE]
>
>L’uscita dalla modalità di backup continuo provoca l’avvio immediato di una nuova sessione in modalità di backup. Per disabilitare completamente la modalità di backup continuo, utilizza l’opzione `leaveContinuousCoverage` nello script, che sovrascrive la sessione di backup continuo esistente. In modalità di backup istantanea, è possibile uscire dalla modalità di backup come di consueto.

Per evitare la perdita di dati, è necessario eseguire il backup dei dati specifici di AEM Forms in modo da garantire la correlazione tra i documenti della directory principale di archiviazione dei contenuti e GDS e i riferimenti al database.

>[!NOTE]
>
>Quando il GDS viene memorizzato nel file system e non nel database, esegui il backup del database prima del backup del GDS.

## Considerazioni speciali per il backup e il ripristino {#special-considerations-for-backup-and-recovery}

Utilizza le seguenti linee guida se è necessario ripristinare AEM Forms in un ambiente differente, a causa delle modifiche di cui sotto:

* Modifica dell’indirizzo IP, del nome host o della porta del server AEM Forms
* Modifica delle lettere delle unità o del percorso della directory
* Passaggio a un altro nome, porta o host di database

In genere, tali scenari di ripristino sono causati da un errore nell’hardware del server che ospita il server applicazioni, il server di database o il server Forms. Oltre alle configurazioni specifiche di AEM Forms descritte in questa sezione, se il nome host o l’indirizzo IP di un server AEM Forms cambia, è necessario apportare le modifiche appropriate anche ad altre parti dell’implementazione di AEM Forms, come i load balancer e i firewall.

### Cosa non può essere modificato {#what-cannot-be-changed}

Anche se è possibile modificare il server di database e molti altri parametri, non è possibile cambiare il tipo di server applicazioni o il tipo di database durante il ripristino di AEM Forms da un backup. Se, ad esempio, ripristini un backup di AEM Forms, non è possibile cambiare il server applicazioni da JBoss a WebLogic o database da Oracle a DB2. Inoltre, i moduli AEM ripristinati devono utilizzare gli stessi percorsi del file system, ad esempio la directory dei font.

### Riavvio dopo un ripristino {#restarting-after-a-recovery}

Prima di riavviare il server Forms dopo un ripristino, esegui le operazioni seguenti:

1. Avvia il sistema in modalità di manutenzione.
1. Effettua le seguenti operazioni per garantire che Gestione moduli sia sincronizzato con AEM Forms in modalità manutenzione:

   1. Passa a https://&lt;*server*>:&lt;*port*>/lc/fm e accedi utilizzando le credenziali amministratore/password.
   1. Fai clic sul nome dell’utente (in questo caso Amministratore privilegiato) nell’angolo in alto a destra.
   1. Quindi su **Opzioni amministratore**.
   1. In seguito su **Inizia** per sincronizzare le risorse dal repository.

1. In un ambiente cluster, il nodo principale (rispetto ad AEM) deve trovarsi prima dei nodi secondari.
1. Verifica che non vengano avviati processi da origini interne o esterne, ad esempio gli iniziatori di processi web, SOAP o EJB, fino alla convalida del normale funzionamento del sistema.

Se il database principale di AEM Forms viene spostato o modificato, rivedi le guide all’installazione relative al server applicazioni per informazioni sull’aggiornamento delle informazioni di connessione al database per le origini dati IDP_DS e EDC_DS di AEM Forms.

>[!NOTE]
> 
> Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

### Modifica del nome host o dell’indirizzo IP di AEM Forms {#changing-the-aem-forms-hostname-or-ip-address}

In un cluster, se si utilizza il caching TCP anziché UDP, è necessario aggiornare la configurazione del localizzatore di cache. Consulta “Configurazione dei localizzatori per la memorizzazione in cache (caching solo tramite TCP)” nella guida alla configurazione relativa al server applicazioni.

### Modifica dei percorsi del file system del nodo di AEM Forms {#changing-the-aem-forms-node-file-system-paths}

Se si modificano i percorsi dei file system per un nodo autonomo, è necessario aggiornare i riferimenti appropriati nelle preferenze, in altre configurazioni di sistema, in applicazioni personalizzate e in applicazioni AEM Forms distribuite. Per un cluster, invece, tutti i nodi devono utilizzare la stessa configurazione del percorso del file system. Imposta la directory principale Archiviazione globale documenti (GDS) e assicurati che punti a una copia del GDS ripristinato, sincronizzata con il database ripristinato. L’impostazione del percorso GDS è importante, perché il GDS può contenere dati destinati a persistere durante il riavvio del server applicazioni.

In un ambiente cluster, la configurazione del percorso del file system dell’archivio deve essere la stessa per tutti i nodi del cluster prima del backup e dopo il ripristino.

Utilizza lo script `LCSetGDS` nella cartella `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` per impostare il percorso GDS dopo aver modificato i percorsi del file system. Per ulteriori dettagli, consulta il file `ReadMe.txt` nella stessa cartella. Se non è possibile utilizzare il percorso della directory GDS precedente, è necessario utilizzare lo script `LCSetGDS` per impostare il nuovo percorso del GDS prima di avviare AEM Forms.

>[!NOTE]
>
>Questa circostanza è l’unica in base alla quale utilizzare questo script per modificare la posizione del GDS. Per modificare la posizione del GDS durante l’esecuzione di AEM Forms, utilizza la console di amministrazione. (Consulta [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Dopo aver impostato il percorso GDS, avvia il server Forms in modalità di manutenzione e utilizza la console di amministrazione per aggiornare i percorsi del file system rimanenti per il nuovo nodo. Dopo aver verificato che tutte le configurazioni necessarie siano state aggiornate, riavvia e verifica AEM Forms.
