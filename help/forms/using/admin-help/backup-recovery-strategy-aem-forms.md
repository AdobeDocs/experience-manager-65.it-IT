---
title: Strategia di backup e ripristino dei moduli AEM
seo-title: Strategia di backup e ripristino dei moduli AEM
description: Scoprite come implementare una strategia per il backup dei dati e garantire che rimanga sincronizzata con i dati dei moduli AEM.
seo-description: Scoprite come implementare una strategia per il backup dei dati e garantire che rimanga sincronizzata con i dati dei moduli AEM.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---


# Strategia di backup e ripristino dei moduli AEM{#backup-and-recovery-strategy-for-aem-forms}

Se l&#39;implementazione dei moduli AEM memorizza dati personalizzati aggiuntivi in un database diverso, è necessario implementare una strategia di backup dei dati e assicurarsi che questi rimangano sincronizzati con i dati dei moduli AEM. Inoltre, l&#39;applicazione deve essere progettata in modo da essere sufficientemente robusta per gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. È vivamente consigliato che qualsiasi operazione del database eseguita sia eseguita nel contesto di una transazione per aiutare a mantenere uno stato coerente.

Dopo aver identificato AEM modalità di utilizzo dei moduli, determinare quali file devono essere sottoposti a backup, con quale frequenza e la finestra di backup da rendere disponibile.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell&#39;implementazione dei moduli di AEM, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di pre-produzione prima di essere utilizzata in produzione per garantire che l&#39;intera soluzione funzioni come previsto senza perdita di dati.

Adobe Experience Manager (AEM) è parte integrante dei moduli AEM. Pertanto, è necessario eseguire il backup AEM e sincronizzato con AEM backup dei moduli come soluzione e servizi di gestione della corrispondenza, come Forms Manager, sono basati su dati memorizzati AEM parte di moduli AEM. Per evitare eventuali perdite di dati, i dati specifici dei moduli AEM devono essere sottoposti a backup in modo da garantire che GDS e AEM (repository) siano correlati ai riferimenti ai database.Le directory di database, GDS, AEM e Content Storage Root devono essere ripristinate a un computer con lo stesso nome DNS originale.

## Tipi di backup {#types-of-backups}

La strategia di backup dei moduli AEM prevede due tipi di backup:

**Immagine del sistema:** Un backup completo del sistema che è possibile utilizzare per ripristinare il contenuto del computer se il disco rigido o l&#39;intero computer smette di funzionare. Un backup delle immagini di sistema è necessario solo prima della distribuzione di produzione di moduli AEM. I criteri aziendali interni stabiliscono quindi la frequenza con cui i backup delle immagini del sistema sono richiesti.

**AEM dati specifici dei moduli:i dati** dell&#39;applicazione sono contenuti nel database, nell&#39;archivio globale dei documenti (GDS) e AEM repository e devono essere sottoposti a backup in tempo reale. GDS è una directory utilizzata per memorizzare file longevi utilizzati all’interno di un processo. Tali file possono includere PDF, criteri o modelli di modulo.

>[!NOTE]
>
>Se è installato Content Services (obsoleto), eseguire il backup della directory principale di Content Storage. Vedere [Directory principale dell&#39;archiviazione dei contenuti (solo Content Services)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

Il database viene utilizzato per memorizzare gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti al database nei file GDS. Se nel database è stata abilitata la memorizzazione dei documenti, anche i dati e i documenti persistenti presenti nel GDS vengono memorizzati nel database. È possibile eseguire il backup e il ripristino del database utilizzando i seguenti metodi:

* **La modalità** di backup dell&#39;istantanea indica che il sistema dei moduli AEM è in modalità di backup a tempo indeterminato o per un numero specificato di minuti, dopo di che la modalità di backup non è più abilitata. Per entrare o uscire dalla modalità di backup dello snapshot, è possibile utilizzare una delle seguenti opzioni. Dopo uno scenario di ripristino, la modalità di backup dello snapshot non deve essere abilitata.

   * Utilizzare la pagina Impostazioni di backup in Admin Console. Per passare alla modalità snapshot, selezionare la casella di controllo Opera in modalità di backup sicuro. Deselezionate la casella di controllo per uscire dalla modalità snapshot.
   * Utilizzare lo script LCBackupMode (vedere [Eseguire il backup delle directory radice del database, GDS e Content Storage](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Per uscire dalla modalità di backup dello snapshot, nell&#39;argomento script impostare il parametro `continuousCoverage` su `false` o utilizzare l&#39;opzione `leaveContinuousCoverage`.
   * Utilizzare l&#39;API di backup/ripristino fornita. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **La** modalità Rolling Backupmode indica che il sistema è sempre in modalità di backup e che una nuova sessione in modalità di backup viene avviata non appena viene rilasciata la sessione precedente. Nessun timeout è associato alla modalità di backup continuo. Quando lo script o le API LCBackupMode vengono chiamate per uscire dalla modalità di backup continuo, viene avviata una nuova sessione di backup continuo. Questa modalità è utile per supportare backup continui, ma consente comunque di eliminare documenti vecchi e inutili dalla directory GDS. La modalità di backup cumulativo non è supportata dalla pagina Backup e ripristino. Dopo uno scenario di ripristino, la modalità di backup continuo è ancora abilitata. È possibile uscire dalla modalità di backup continuo (modalità di backup continuo) utilizzando lo script LCBackupMode con l&#39;opzione `leaveContinuousCoverage`.

>[!NOTE]
>
>Se si esce dalla modalità di backup a rotazione, viene immediatamente avviata una nuova sessione in modalità di backup. Per disattivare completamente la modalità di backup a scorrimento, utilizzate l&#39;opzione `leaveContinuousCoverage` nello script, che sovrascrive la sessione di backup a rotazione esistente. In modalità backup snapshot, è possibile lasciare la modalità di backup come di solito.

Per evitare la perdita di dati, è necessario eseguire il backup dei dati specifici dei moduli di AEM in modo da garantire la correlazione tra i documenti di directory radice di GDS e di Content Storage con i riferimenti al database.

>[!NOTE]
>
>Quando il GDS è memorizzato nel file system e non nel database, eseguire il backup del database prima del backup GDS.

## Considerazioni speciali per il backup e il ripristino {#special-considerations-for-backup-and-recovery}

Se è necessario ripristinare AEM moduli in un ambiente diverso a causa delle seguenti modifiche, attenersi alle linee guida seguenti:

* Modifica dell&#39;indirizzo IP, del nome host o della porta del server moduli AEM
* Modifica nelle lettere di unità o nel percorso della directory
* Passaggio a un host, una porta o un nome di database diverso

In genere, tali scenari di ripristino sono causati da errori hardware del server che ospita il server dell&#39;applicazione, il server del database o il server dei moduli. Oltre alle configurazioni specifiche dei moduli di AEM descritte in questa sezione, è necessario apportare le modifiche necessarie per altre parti della distribuzione dei moduli di AEM, ad esempio i sistemi di bilanciamento del carico e i firewall, se il nome host o l&#39;indirizzo IP di un server AEM moduli vengono modificati.

### Cosa non può essere modificato {#what-cannot-be-changed}

Anche se è possibile modificare il server di database e molti altri parametri, non è possibile modificare il tipo di server applicazioni o di database quando si ripristinano AEM moduli da un backup. Ad esempio, se si sta recuperando un backup dei moduli AEM, non è possibile modificare il server dell&#39;applicazione da JBoss a WebLogic o il database da  Oracle a DB2. Inoltre, i moduli AEM recuperati devono utilizzare gli stessi percorsi del file system, ad esempio la directory dei font.

### Riavvio dopo un ripristino {#restarting-after-a-recovery}

Prima di riavviare il server dei moduli dopo un ripristino, effettuare le seguenti operazioni:

1. Avviate il sistema in modalità manutenzione.
1. Per assicurarsi che Form Manager sia sincronizzato con AEM moduli in modalità di manutenzione, effettuare le seguenti operazioni:

   1. Andate a https://&lt;*server*>:&lt;*porta*>/lc/fm ed effettuate l&#39;accesso utilizzando le credenziali di amministratore/password.
   1. Fate clic sul nome dell’utente (in questo caso, Amministratore avanzato) nell’angolo in alto a destra.
   1. Fare clic su **Opzioni amministratore**.
   1. Fate clic su **Start** per sincronizzare le risorse dalla directory archivio.

1. In un ambiente cluster, il nodo primario (rispetto a AEM) deve essere superiore rispetto ai nodi secondari.
1. Assicurarsi che non vengano avviati processi da origini interne o esterne, quali Web, SOAP o gli iniziatori di processi EJB, fino alla convalida del normale funzionamento del sistema.

Se il database dei moduli AEM principale viene spostato o modificato, consultare le Guide all&#39;installazione relative al server applicazione per informazioni sull&#39;aggiornamento delle informazioni sulla connessione al database per le origini dati dei moduli AEM IDP_DS e EDC_DS.

### Modifica del nome host del modulo AEM o dell&#39;indirizzo IP {#changing-the-aem-forms-hostname-or-ip-address}

In un cluster, se si utilizza il caching TCP invece di UDP, è necessario aggiornare la configurazione del locatore della cache. Consultate &quot;Configuring the caching locators (caching using TCP only)&quot; (Configurazione delle localizzatori nella cache (caching utilizzando solo TCP) nella guida alla configurazione relativa al server dell&#39;applicazione in uso.

### Modifica dei percorsi del file system del nodo AEM moduli {#changing-the-aem-forms-node-file-system-paths}

Se si modificano i percorsi del file system per un nodo standalone, è necessario aggiornare i riferimenti appropriati nelle preferenze, nelle altre configurazioni di sistema, nelle applicazioni personalizzate e nelle applicazioni AEM moduli distribuite. Per un cluster, invece, tutti i nodi devono utilizzare la stessa configurazione di percorso del file system. È necessario impostare la directory principale Global Document Storage (GDS) e assicurarsi che faccia riferimento a una copia del GDS recuperato che è sincronizzata con il database recuperato. L&#39;impostazione del percorso GDS è importante perché il GDS può contenere dati destinati a persistere tra i riavvii del server applicazioni.

In un ambiente cluster, la configurazione del percorso del file system del repository deve essere la stessa per tutti i nodi del cluster prima del backup e dopo il ripristino.

Utilizzare lo script `LCSetGDS`nella cartella `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` per impostare il percorso GDS dopo aver modificato i percorsi del file system. Per ulteriori informazioni, vedere il file `ReadMe.txt` nella stessa cartella. Se non è possibile utilizzare il vecchio percorso della directory GDS, è necessario utilizzare lo script `LCSetGDS` per impostare il nuovo percorso del GDS prima di avviare AEM moduli.

>[!NOTE]
>
>Questa circostanza è l&#39;unica in base alla quale si dovrebbe utilizzare questo script per modificare la posizione GDS. Per modificare la posizione GDS durante l&#39;esecuzione AEM moduli, utilizzare la console di amministrazione. (Vedere [Configurare le impostazioni generali dei moduli AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Dopo aver impostato il percorso GDS, avviare il server dei moduli in modalità di manutenzione e utilizzare la console di amministrazione per aggiornare i percorsi dei file system rimanenti per il nuovo nodo. Dopo aver verificato l&#39;aggiornamento di tutte le configurazioni necessarie, riavviare e verificare AEM moduli.
