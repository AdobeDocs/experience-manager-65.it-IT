---
title: Preparazione di AEM Forms per il backup
seo-title: Preparazione di AEM Forms per il backup
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Preparazione di AEM Forms per il backup {#preparing-aem-forms-for-backup}

## Informazioni sul servizio di backup e ripristino {#about-the-backup-and-restore-service}

Il servizio Backup e ripristino consente di inserire AEM Forms nella modalità *di* backup, che consente di eseguire backup a caldo. Il servizio Backup e ripristino non esegue effettivamente un backup di AEM Forms né ripristina il sistema. Il server viene invece messo in stato per backup coerenti e affidabili, consentendo al contempo al server di continuare l&#39;esecuzione. È necessario eseguire il backup di Global Document Storage (GDS) e del database connesso al server dei moduli. GDS è una directory utilizzata per memorizzare i file utilizzati in un processo di lunga durata.

La modalità di backup è uno stato immesso dal server in modo che i file nel GDS non vengano eliminati durante la procedura di backup. Al contrario, le sottodirectory vengono create nella directory GDS per mantenere un record di file da eliminare dopo il termine della modalità di salvataggio del backup. Un file è destinato a sopravvivere al riavvio del sistema e può estendere giorni, o anche anni. Questi file sono una parte fondamentale dello stato generale del server dei moduli e possono includere file PDF, criteri o modelli di modulo. Se uno di questi file viene perso o danneggiato, i processi sul server dei moduli potrebbero diventare instabili e i dati potrebbero andare persi.

È possibile scegliere di eseguire backup di snapshot, dove in genere si entra in modalità di backup per un periodo e poi si esce dalla modalità di backup dopo aver completato le attività di backup. È necessario uscire dalla modalità di backup in modo che i file possano essere eliminati dal GDS per garantire che non crescano inutilmente. È possibile lasciare la modalità di backup in modo esplicito o attendere che scada il tempo in una sessione in modalità di backup.

È inoltre possibile lasciare il server in modalità di backup perpetuo, tipica delle strategie di backup per il ripristino di backup o la copertura continua del sistema. La modalità di backup continuo indica che il sistema è sempre in modalità di backup, con una nuova sessione in modalità di backup avviata non appena viene rilasciata la sessione precedente. In modalità di backup continuo, un file viene eliminato dopo due sessioni in modalità di backup e non viene più utilizzato il riferimento.

È possibile utilizzare il servizio Backup e ripristino per aggiungere alle applicazioni esistenti o alle nuove applicazioni create per eseguire backup del GDS o del database connesso al server dei moduli.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell’implementazione di AEM Forms, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di pre-produzione prima di essere utilizzata in produzione per garantire che l’intera soluzione funzioni come previsto senza perdita di dati.

È possibile eseguire le seguenti operazioni utilizzando il servizio Backup e ripristino:

* Immettere la modalità di backup.
* Lasciare la modalità di backup.

>[!NOTE]
>
>Per ulteriori informazioni su cosa considerare quando si eseguono i backup per AEM Forms, consultate la guida [](https://www.adobe.com/go/learn_aemforms_admin_63)di amministrazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Inserimento della modalità di backup nel server dei moduli {#entering-backup-mode-on-the-forms-server}

È possibile accedere alla modalità di backup per consentire il backup a caldo di un server moduli. Quando si attiva la modalità di backup, vengono specificate le seguenti informazioni in base alle procedure di backup dell&#39;azienda:

* Etichetta univoca per identificare la sessione di modalità di backup che potrebbe essere utile per i processi di backup.
* Tempo necessario per il completamento della procedura di backup.
* Flag che indica se la modalità di backup continuo è utile solo se si eseguono backup periodici.

Prima di scrivere le applicazioni per passare alla modalità di backup, è consigliabile comprendere le procedure di backup che verranno utilizzate dopo aver messo il server dei moduli in modalità di backup. Per ulteriori informazioni su cosa considerare quando si eseguono i backup per AEM Forms, consultate la guida [](https://www.adobe.com/go/learn_aemforms_admin_63)di amministrazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione che entra in modalità di backup, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto client BackupService.
1. Determinare un&#39;etichetta univoca, il tempo necessario per eseguire il backup e se eseguire il backup continuo.
1. Immettere la modalità di backup.
1. (Facoltativo) Recuperare informazioni sulla sessione della modalità di backup sul server.
1. Eseguire il backup del GDS (Global Data Store) e del database.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Questi file sono importanti da includere nel progetto per la corretta compilazione del codice e l&#39;utilizzo dell&#39;API del servizio Backup e ripristino.

Per informazioni sulla posizione di questi file, consultate [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un oggetto BackupService Client API**

Per uscire dalla modalità di backup a livello di programmazione, è necessario creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Scegliere un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se eseguire il backup continuo**

Prima di passare alla modalità di backup, è necessario stabilire un&#39;etichetta univoca, determinare il tempo da allocare per eseguire il backup e decidere se il server dei moduli deve rimanere in modalità di backup. Queste considerazioni sono importanti per l&#39;integrazione con le procedure di backup stabilite dall&#39;organizzazione. (vedere [la guida](https://www.adobe.com/go/learn_aemforms_admin_63)di amministrazione.)

**Modalità di backup**

Accedete alla modalità di backup con i parametri coerenti con le procedure di backup dell&#39;organizzazione.

**Ottenere informazioni sulla sessione della modalità di backup sul server**

Dopo aver attivato la modalità di backup, potete recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup

**Eseguire il backup del GDS e del database**

Dopo aver immesso correttamente la modalità di backup, è possibile eseguire un backup di Global Document Storage (GDS) e del database a cui è connesso il server dei moduli. Questo passaggio è specifico dell&#39;organizzazione, in quanto è possibile eseguire questo passaggio manualmente oppure eseguire altri strumenti per eseguire la procedura di backup.

### Accedete alla modalità di backup mediante l&#39;API Java {#enter-backup-mode-using-the-java-api}

Accedete alla modalità di backup utilizzando l&#39;API del servizio Backup e ripristino:

1. Includi file di progetto

   Includete i file JAR client necessari, ad esempio adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare l&#39;applicazione client Java, i seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

1. Creare un oggetto BackupService Client API

   È possibile utilizzare insieme un oggetto `ServiceClientFactory` e l&#39;oggetto client BackupService.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `BackupService` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Scegliere un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se eseguire il backup continuo

   Stabilire un&#39;etichetta univoca, determinare il tempo che si desidera allocare per eseguire il backup e decidere se si desidera che il server dei moduli rimanga in modalità di backup continuo.

1. Modalità di backup

   Attivate la modalità di backup richiamando il `enterBackupMode` metodo con i seguenti parametri:

   * Un `String` valore che specifica un&#39;etichetta univoca leggibile dall&#39;utente che identifica la sessione della modalità di backup. È consigliabile non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * Un `int` valore che specifica il numero di minuti per rimanere in modalità di backup. Potete specificare un valore da `1` a `10080` (il numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * Un `Boolean` valore che specifica se deve essere in modalità di backup continuo. Un valore di `True` specifica la modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti di permanenza in modalità di backup viene ignorato.

      La modalità di backup continuo indica che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente. Un valore `False` indica che la modalità di backup continuo non è utilizzata e, dopo aver lasciato la modalità di backup, l&#39;eliminazione dei file dal GDS riprende.

1. Ottenere informazioni sulla sessione della modalità di backup sul server

   Recuperate le informazioni utilizzando l&#39; `BackupModeEntryResult` oggetto restituito dopo aver richiamato il `enterBackupMode` metodo. Le informazioni recuperabili dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

1. Eseguire il backup del GDS e del database

   Eseguire il backup di Global Document Storage (GDS) e del database a cui è connesso il server dei moduli. Le azioni per eseguire il backup non fanno parte dell’SDK di AEM Forms e possono includere anche passaggi manuali specifici per le procedure di backup nell’organizzazione.

### Accedere alla modalità di backup utilizzando l&#39;API del servizio Web {#enter-backup-mode-using-the-web-service-api}

Accedete alla modalità di backup utilizzando il servizio Web fornito dall&#39;API del servizio Backup e ripristino:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL dell&#39;API del servizio Backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto BackupService Client API

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `BackupServiceService` oggetto richiamando il relativo costruttore predefinito e specificare le credenziali utilizzando il `Credentials` metodo.

1. Scegliere un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se eseguire il backup continuo

   Stabilire un&#39;etichetta univoca, determinare il tempo che si desidera allocare per eseguire il backup e decidere se si desidera che il server dei moduli rimanga in modalità di backup continuo.

1. Modalità di backup

   Per passare alla modalità di backup, richiamare il metodo enterBackupMode e passare i seguenti valori:

   * Un `String` valore che specifica un&#39;etichetta univoca leggibile dall&#39;utente che identifica la sessione della modalità di backup. È consigliabile non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * Un `Uint32` valore che specifica il numero di minuti per rimanere in modalità di backup. Potete specificare un valore da `1` a `10080` (numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * Un `Boolean` valore che specifica se deve essere in modalità di backup continuo. Un valore di `True` specifica la modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti di permanenza in modalità di backup viene ignorato. La modalità di backup continuo indica che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente.

      Un valore `False` indica che la modalità di backup continuo non è utilizzata e, dopo aver lasciato la modalità di backup, l&#39;eliminazione dei file dal GDS riprende.

1. Ottenere informazioni sulla sessione della modalità di backup sul server

   Recuperare informazioni sulla sessione in modalità di backup dopo aver richiamato il metodo enterBackupMode da BackupModeEntryResult restituito per verificare che sia stato eseguito correttamente. Le informazioni recuperabili dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

1. Eseguire il backup del GDS e del database

   Eseguire il backup di Global Document Storage (GDS) e del database a cui è connesso il server dei moduli. Le azioni per eseguire il backup non fanno parte dell’SDK di AEM Forms e possono includere anche passaggi manuali specifici per le procedure di backup nell’organizzazione.

## Uscita dalla modalità di backup sul server dei moduli {#leaving-backup-mode-on-the-forms-server}

È possibile uscire dalla modalità di backup in modo che il server dei moduli riprenda la rimozione dei file da GDS (Global Document Storage) sul server dei moduli.

Prima di scrivere le applicazioni per passare alla modalità di uscita, è consigliabile comprendere le procedure di backup utilizzate con AEM Forms. Per ulteriori informazioni su cosa considerare quando si eseguono i backup per AEM Forms, consultate la guida [](https://www.adobe.com/go/learn_aemforms_admin_63)di amministrazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per uscire dalla modalità di backup, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto client BackupService.
1. Lasciare la modalità di backup.
1. (Facoltativo) Recuperare informazioni sulla sessione della modalità di backup in esecuzione sul server dei moduli.

**Includi file di progetto**

Includete tutti i file necessari nel progetto di sviluppo. Questi file sono importanti per la corretta compilazione del codice e per l’utilizzo dell’API del servizio Backup e ripristino.

Per informazioni sulla posizione di questi file, consultate [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un oggetto BackupService Client API**

Per uscire dalla modalità di backup a livello di programmazione, è necessario creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Esci dalla modalità di backup**

Lasciare la modalità di backup per riprendere la normale eliminazione dei file da Global Document Storage (GDS). Prima di uscire dalla modalità di backup, verificare che le procedure di backup siano state completate.

**Recupero delle informazioni sulla sessione di modalità di backup terminata**

Dopo aver lasciato la modalità di backup, potete recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup.

### Lasciare la modalità di backup mediante l&#39;API Java {#leave-backup-mode-using-the-java-api}

Lasciate la modalità di backup utilizzando l&#39;API del servizio Backup e ripristino (Java):

1. Includi file di progetto

   Includete i file JAR client necessari, ad esempio adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare un&#39;applicazione client Java, è necessario aggiungere i seguenti file JAR al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

1. Creare un oggetto BackupService Client API

   È possibile utilizzare insieme un oggetto `ServiceClientFactory` e l&#39;oggetto client BackupService.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `BackupService` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto come parametro.

1. Modalità di backup

   Lasciare la modalità di backup richiamando il `leaveBackupMode` metodo.

1. Ottenere informazioni sulla sessione della modalità di backup sul server

   Recuperare informazioni sull&#39;operazione utilizzando l&#39; `BackupModeResult` oggetto restituito. Le informazioni recuperabili dopo l&#39;accesso alla modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi dei file per la procedura di backup.

### Uscire dalla modalità di backup mediante l&#39;API del servizio Web {#leave-backup-mode-using-the-web-service-api}

Lasciate la modalità di backup utilizzando l&#39;API del servizio Backup e ripristino (servizio Web):

1. Includi file di progetto

   Per utilizzare i servizi Web, è necessario includere i file proxy. Per configurare il progetto in modo che utilizzi l’API del servizio di backup e ripristino come servizio Web, effettuate le seguenti operazioni.

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL dell&#39;API del servizio Backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto BackupService Client API

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `BackupServiceService` oggetto richiamando il relativo costruttore predefinito.

1. Modalità di backup

   Uscire dalla modalità di backup richiamando l&#39;operazione del servizio `leaveBackupMode` Web.

1. Ottenere informazioni sulla sessione della modalità di backup sul server

   Recuperare l&#39;identificatore della modalità di backup dopo l&#39;operazione per verificare che sia stato eseguito correttamente. Le informazioni recuperabili dopo aver lasciato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup.

