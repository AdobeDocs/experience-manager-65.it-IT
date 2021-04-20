---
title: Preparazione di AEM Forms per il backup
seo-title: Preparazione di AEM Forms per il backup
description: Scopri come utilizzare il servizio Backup e ripristino per accedere e uscire dalla modalità Backup per il server AEM Forms utilizzando l’API Java e l’API del servizio Web.
seo-description: Scopri come utilizzare il servizio Backup e ripristino per accedere e uscire dalla modalità Backup per il server AEM Forms utilizzando l’API Java e l’API del servizio Web.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2555'
ht-degree: 0%

---


# Preparazione di AEM Forms per il backup {#preparing-aem-forms-for-backup}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio di backup e ripristino {#about-the-backup-and-restore-service}

Il servizio Backup e ripristino consente di inserire AEM Forms nella modalità *backup*, che consente l&#39;esecuzione di backup a caldo. Il servizio Backup e ripristino non esegue effettivamente un backup di AEM Forms o ripristina il sistema. Invece, mette il server in uno stato per backup coerenti e affidabili, consentendo al server di continuare l&#39;esecuzione. L’utente è responsabile delle azioni di backup del GDS (Global Document Storage) e del database connessi al server dei moduli. Il GDS è una directory utilizzata per memorizzare i file utilizzati in un processo di lunga durata.

La modalità di backup è uno stato immesso dal server in modo che i file nel GDS non vengano eliminati durante una procedura di backup. Al contrario, le sottodirectory vengono create nella directory GDS per mantenere un record di file da eliminare dopo la fine della modalità di backup del salvataggio. Un file ha lo scopo di sopravvivere al riavvio del sistema e può durare giorni, o anche anni. Questi file rappresentano una parte critica dello stato generale del server dei moduli e possono includere file PDF, criteri o modelli di moduli. Se uno di questi file viene perso o danneggiato, i processi sul server dei moduli potrebbero diventare instabili e i dati potrebbero andare persi.

È possibile scegliere di eseguire i backup delle copie istantanee, in cui di solito si entra in modalità di backup per un periodo e poi lasciare la modalità di backup dopo aver completato le attività di backup. È necessario lasciare la modalità di backup in modo che i file possano essere eliminati dal GDS per garantire che non crescano inutilmente grandi. È possibile uscire dalla modalità di backup esplicitamente o attendere la scadenza del tempo per una sessione in modalità di backup.

È inoltre possibile lasciare il server in modalità di backup perpetuo, tipica delle strategie di backup per il backup continuo o la copertura continua del sistema. La modalità di backup continuo indica che il sistema è sempre in modalità di backup, con una nuova sessione in modalità di backup avviata non appena viene rilasciata la sessione precedente. In modalità di backup continuo, un file viene eliminato dopo due sessioni in modalità di backup e non viene più fatto riferimento.

È possibile utilizzare il servizio Backup e ripristino per aggiungere alle applicazioni esistenti o alle nuove applicazioni create per eseguire backup del GDS o del database connesso al server dei moduli.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell&#39;implementazione AEM Forms, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di staging prima di essere utilizzata in produzione per garantire che l&#39;intera soluzione funzioni come previsto senza perdita di dati.

È possibile eseguire queste operazioni utilizzando il servizio Backup e ripristino:

* Accedere alla modalità di backup.
* Lascia la modalità di backup.

>[!NOTE]
>
>Per ulteriori informazioni su cosa considerare durante l&#39;esecuzione dei backup per AEM Forms, vedere [Guida all&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Accesso alla modalità di backup sul server dei moduli {#entering-backup-mode-on-the-forms-server}

È possibile accedere alla modalità di backup per consentire il backup a caldo di un server dei moduli. Quando si accede alla modalità di backup, è possibile specificare le seguenti informazioni in base alle procedure di backup dell&#39;organizzazione:

* Etichetta univoca per identificare la sessione di modalità di backup che può essere utile per i processi di backup.
* Tempo necessario per il completamento della procedura di backup.
* Flag che indica se è attiva la modalità di backup continuo, utile solo se si eseguono backup continui.

Prima di scrivere applicazioni per accedere alla modalità di backup, è consigliabile comprendere le procedure di backup che verranno utilizzate dopo aver messo il server dei moduli in modalità di backup. Per ulteriori informazioni su cosa considerare durante l&#39;esecuzione dei backup per AEM Forms, vedere [Guida all&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione che entra in modalità di backup, esegui i seguenti passaggi:

1. Includi file di progetto.
1. Creare un oggetto client BackupService.
1. Determinare un&#39;etichetta univoca, la quantità di tempo necessario per eseguire il backup e se utilizzare la modalità di backup continuo.
1. Accedere alla modalità di backup.
1. (Facoltativo) Recupera informazioni sulla sessione della modalità di backup sul server.
1. Esegui il backup del GDS (Global Data Store) e del database.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Questi file sono importanti da includere nel progetto per compilare correttamente il codice e utilizzare l&#39;API del servizio di backup e ripristino.

Per informazioni sulla posizione di questi file, consulta [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client BackupService**

Per uscire dalla modalità di backup a livello di programmazione, creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Stabilire un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se utilizzare la modalità di backup continuo**

Prima di passare alla modalità di backup, è necessario stabilire un&#39;etichetta univoca, determinare il tempo da allocare per eseguire il backup e decidere se si desidera che il server dei moduli rimanga in modalità di backup. Queste considerazioni sono importanti per l&#39;integrazione con le procedure di backup stabilite dall&#39;organizzazione. (Consultare [guida all&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Modalità backup**

Accedi alla modalità di backup con i parametri coerenti con le procedure di backup della tua organizzazione.

**Recupera informazioni sulla sessione in modalità di backup sul server**

Dopo aver attivato la modalità di backup, è possibile recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup

**Esegui il backup del GDS e del database**

Dopo aver attivato correttamente la modalità di backup, è possibile eseguire un backup del GDS (Global Document Storage) e del database a cui è connesso il server dei moduli. Questo passaggio è specifico dell&#39;organizzazione, in quanto è possibile eseguire manualmente questo passaggio o eseguire altri strumenti per eseguire la procedura di backup.

### Attiva la modalità di backup utilizzando l&#39;API Java {#enter-backup-mode-using-the-java-api}

Immettere la modalità di backup utilizzando l&#39;API del servizio Backup e ripristino:

1. Includi file di progetto

   Includi i file JAR client necessari, come adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare l’applicazione client Java, i seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

1. Creare un oggetto API client BackupService

   Utilizzare insieme un oggetto `ServiceClientFactory` e l&#39;oggetto API client BackupService.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `BackupService` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Stabilire un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se utilizzare la modalità di backup continuo

   Scegliere un&#39;etichetta univoca, determinare il tempo da allocare per eseguire il backup e decidere se si desidera che il server dei moduli rimanga in modalità di backup continuo.

1. Modalità backup

   Attiva la modalità di backup richiamando il metodo `enterBackupMode` con i seguenti parametri:

   * Valore `String` che specifica un&#39;etichetta univoca leggibile dall&#39;utente che identifica la sessione di modalità di backup. È consigliabile non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * Valore `int` che specifica il numero di minuti in cui rimanere in modalità di backup. Puoi specificare un valore compreso tra `1` e `10080` (il numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * Valore `Boolean` che specifica se è in modalità di backup continuo. Un valore di `True` specifica di essere in modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti da rimanere in modalità di backup viene ignorato.

      Modalità di backup continuo significa che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente. Il valore `False` indica che la modalità di backup continuo non viene utilizzata e, dopo aver lasciato la modalità di backup, riprende l&#39;eliminazione dei file dal GDS.

1. Recupera informazioni sulla sessione in modalità di backup sul server

   Recupera le informazioni utilizzando l&#39;oggetto `BackupModeEntryResult` restituito dopo aver richiamato il metodo `enterBackupMode` . Le informazioni che è possibile recuperare dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l’etichetta, l’ID di backup e l’ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

1. Esegui il backup del GDS e del database

   Eseguire il backup di GDS (Global Document Storage) e del database a cui è connesso il server dei moduli. Le azioni per eseguire il backup non fanno parte dell’SDK AEM Forms e possono includere anche passaggi manuali specifici per le procedure di backup all’interno dell’organizzazione.

### Accedi alla modalità di backup utilizzando l&#39;API del servizio Web {#enter-backup-mode-using-the-web-service-api}

Accedere alla modalità di backup utilizzando il servizio Web fornito dall&#39;API del servizio di backup e ripristino:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL API del servizio di backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto API client BackupService

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `BackupServiceService` richiamando il relativo costruttore predefinito e specificare le credenziali utilizzando il metodo `Credentials` .

1. Stabilire un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se utilizzare la modalità di backup continuo

   Scegliere un&#39;etichetta univoca, determinare il tempo da allocare per eseguire il backup e decidere se si desidera che il server dei moduli rimanga in modalità di backup continuo.

1. Modalità backup

   Per accedere alla modalità di backup, richiamare il metodo enterBackupMode e passare i seguenti valori:

   * Valore `String` che specifica un&#39;etichetta univoca leggibile dall&#39;utente che identifica la sessione di modalità di backup. È consigliabile non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * Valore `Uint32` che specifica il numero di minuti in cui rimanere in modalità di backup. Puoi specificare un valore compreso tra `1` e `10080` (numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * Valore `Boolean` che specifica se è in modalità di backup continuo. Un valore di `True` specifica di essere in modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti da rimanere in modalità di backup viene ignorato. Modalità di backup continuo significa che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente.

      Il valore `False` indica che la modalità di backup continuo non viene utilizzata e, dopo aver lasciato la modalità di backup, riprende l&#39;eliminazione dei file dal GDS.

1. Recupera informazioni sulla sessione in modalità di backup sul server

   Recuperare le informazioni sulla sessione in modalità di backup dopo aver richiamato il metodo enterBackupMode da BackupModeEntryResult restituito per verificare che sia stato eseguito correttamente. Le informazioni che è possibile recuperare dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l’etichetta, l’ID di backup e l’ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

1. Esegui il backup del GDS e del database

   Eseguire il backup di GDS (Global Document Storage) e del database a cui è connesso il server dei moduli. Le azioni per eseguire il backup non fanno parte dell’SDK AEM Forms e possono includere anche passaggi manuali specifici per le procedure di backup all’interno dell’organizzazione.

## Uscita dalla modalità di backup sul server dei moduli {#leaving-backup-mode-on-the-forms-server}

È possibile uscire dalla modalità di backup in modo che il server dei moduli riprenda l’eliminazione dei file da GDS (Global Document Storage) sul server dei moduli.

Prima di scrivere applicazioni per entrare in modalità di uscita, è consigliabile comprendere le procedure di backup utilizzate con AEM Forms. Per ulteriori informazioni su cosa considerare durante l&#39;esecuzione dei backup per AEM Forms, vedere [Guida all&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per uscire dalla modalità di backup, esegui i seguenti passaggi:

1. Includi file di progetto.
1. Creare un oggetto client BackupService.
1. Lascia la modalità di backup.
1. (Facoltativo) Recupera informazioni sulla sessione della modalità di backup in esecuzione sul server dei moduli.

**Includi file di progetto**

Includi tutti i file necessari nel progetto di sviluppo. Questi file sono importanti per la corretta compilazione del codice e per l&#39;utilizzo dell&#39;API del servizio di backup e ripristino.

Per informazioni sulla posizione di questi file, consulta [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client BackupService**

Per uscire dalla modalità di backup a livello di programmazione, creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Esci dalla modalità di backup**

Lasciare la modalità di backup per riprendere la normale eliminazione dei file da Global Document Storage (GDS). Prima di uscire dalla modalità di backup, verificare che le procedure di backup siano state completate.

**Recupera informazioni sulla sessione della modalità di backup terminata**

Dopo aver lasciato la modalità di backup, è possibile recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup.

### Lascia la modalità di backup utilizzando l’ API Java {#leave-backup-mode-using-the-java-api}

Lascia la modalità di backup utilizzando l’API del servizio Backup e ripristino (Java):

1. Includi file di progetto

   Includi i file JAR client necessari, come adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare un’applicazione client Java, i seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

1. Creare un oggetto API client BackupService

   Utilizzare insieme un oggetto `ServiceClientFactory` e l&#39;oggetto API client BackupService.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `BackupService` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory` come parametro.

1. Modalità backup

   Esci dalla modalità di backup richiamando il metodo `leaveBackupMode` .

1. Recupera informazioni sulla sessione in modalità di backup sul server

   Recupera informazioni sull&#39;operazione utilizzando l&#39;oggetto `BackupModeResult` restituito. Le informazioni che è possibile recuperare dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l’etichetta, l’ID di backup e l’ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

### Lascia la modalità di backup utilizzando l&#39;API del servizio Web {#leave-backup-mode-using-the-web-service-api}

Lascia la modalità di backup utilizzando l&#39;API del servizio Backup e ripristino (servizio Web):

1. Includi file di progetto

   Per utilizzare i servizi Web, è necessario assicurarsi di includere i file proxy. Segui questi passaggi per configurare il progetto per l’utilizzo dell’API del servizio Backup e ripristino come servizio Web.

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL API del servizio di backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto API client BackupService

   Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `BackupServiceService` richiamando il relativo costruttore predefinito.

1. Modalità backup

   Esci dalla modalità di backup richiamando l&#39;operazione del servizio Web `leaveBackupMode`.

1. Recupera informazioni sulla sessione in modalità di backup sul server

   Recupera l&#39;identificatore della modalità di backup dopo l&#39;operazione per verificare che sia stato eseguito correttamente. Le informazioni che è possibile recuperare dopo aver lasciato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup.

