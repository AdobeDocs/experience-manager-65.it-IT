---
title: Preparazione di AEM Forms per il backup
description: Scopri come utilizzare il servizio Backup e ripristino per accedere e uscire dalla modalità di backup per il server AEM Forms utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 0%

---

# Preparazione di AEM Forms per il backup {#preparing-aem-forms-for-backup}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Informazioni sul servizio Backup e ripristino {#about-the-backup-and-restore-service}

Il servizio di backup e ripristino consente di inserire AEM Forms in *modalità di backup*, che consente di eseguire backup a caldo. Il servizio Backup e ripristino non esegue effettivamente il backup di AEM Forms o il ripristino del sistema. In questo modo, il server si trova in uno stato che consente di eseguire backup coerenti e affidabili e al tempo stesso di continuare l&#39;esecuzione del server. L&#39;utente è responsabile delle azioni di backup di GDS (Global Document Storage) e del database connesso al server Forms. Il GDS è una directory utilizzata per memorizzare i file utilizzati in un processo di lunga durata.

La modalità di backup è uno stato immesso dal server in modo che i file nel GDS non vengano eliminati durante una procedura di backup. Al contrario, le sottodirectory vengono create nella directory GDS per mantenere un record di file da eliminare al termine della modalità di backup del salvataggio. Un file ha lo scopo di sopravvivere ai riavvii del sistema e può durare giorni o anche anni. Questi file rappresentano una parte critica dello stato generale di Forms Server e possono includere file PDF, criteri o modelli di modulo. Se uno di questi file viene perso o danneggiato, i processi sul server Forms potrebbero diventare instabili e i dati potrebbero andare perduti.

È possibile scegliere di eseguire i backup delle copie istantanee, in cui in genere si entra in modalità di backup per un determinato periodo e quindi si esce dalla modalità di backup dopo aver completato le attività di backup. È necessario lasciare la modalità di backup in modo che i file possano essere eliminati dal GDS per evitare che crescano inutilmente. È possibile uscire dalla modalità di backup in modo esplicito oppure attendere la scadenza di una sessione in modalità di backup.

È inoltre possibile lasciare il server in modalità di backup permanente, tipica delle strategie di backup per i backup continui o la copertura continua del sistema. La modalità di backup continua indica che il sistema è sempre in modalità di backup, con una nuova sessione in modalità di backup avviata non appena viene rilasciata la sessione precedente. In modalità di backup continuo, un file viene eliminato dopo due sessioni in modalità di backup e non vi viene più fatto riferimento.

È possibile utilizzare il servizio Backup e ripristino per aggiungere applicazioni esistenti o nuove applicazioni create per eseguire backup del GDS o del database connesso al server Forms.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell&#39;implementazione di AEM Forms, prima di essere utilizzata in produzione, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di staging per garantire che l&#39;intera soluzione funzioni come previsto senza perdita di dati.

È possibile eseguire queste operazioni utilizzando il servizio Backup e ripristino:

* Accedi alla modalità di backup.
* Lascia la modalità di backup.

>[!NOTE]
>
>Per ulteriori informazioni su cosa considerare durante l’esecuzione dei backup per AEM Forms, consulta [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Accesso alla modalità di backup sul server Forms {#entering-backup-mode-on-the-forms-server}

È possibile attivare la modalità di backup per consentire backup a caldo di un server Forms. Quando si entra in modalità di backup, è possibile specificare le seguenti informazioni in base alle procedure di backup dell&#39;organizzazione:

* Etichetta univoca per identificare la sessione in modalità di backup che può essere utile per i processi di backup.
* Tempo necessario per il completamento della procedura di backup.
* Un flag per indicare se deve essere in modalità di backup continuo, utile solo se si eseguono backup continui.

Prima di scrivere applicazioni per l&#39;immissione in modalità di backup, è consigliabile comprendere le procedure di backup utilizzate dopo aver impostato Forms Server in modalità di backup. Per ulteriori informazioni su cosa considerare durante l’esecuzione dei backup per AEM Forms, consulta [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione che entra in modalità di backup, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client BackupService.
1. Determinare un&#39;etichetta univoca, la quantità di tempo per l&#39;esecuzione del backup e l&#39;eventuale modalità di backup continuo.
1. Accedi alla modalità di backup.
1. (Facoltativo) Recupera informazioni sulla sessione in modalità di backup sul server.
1. Eseguire il backup del GDS (Global Data Store) e del database.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Questi file sono importanti da includere nel progetto per compilare correttamente il codice e utilizzare l’API del servizio Backup e ripristino.

Per informazioni sulla posizione di questi file, vedere [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client BackupService**

Per uscire dalla modalità di backup a livello di programmazione, è necessario creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Decidere su un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se attivare la modalità di backup continuo**

Prima di attivare la modalità di backup, è necessario scegliere un&#39;etichetta univoca, determinare il tempo da allocare per eseguire il backup e decidere se si desidera che Forms Server rimanga in modalità di backup. Queste considerazioni sono importanti per l&#39;integrazione con le procedure di backup stabilite dall&#39;organizzazione. (vedere [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Accedi alla modalità di backup**

Attiva la modalità di backup con i parametri coerenti con le procedure di backup dell’organizzazione.

**Recuperare informazioni sulla sessione in modalità di backup sul server**

Dopo aver attivato la modalità di backup, è possibile recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup

**Eseguire il backup di GDS e database**

Dopo aver immesso la modalità di backup, è possibile eseguire un backup di GDS (Global Document Storage) e del database a cui è connesso Forms Server. Questo passaggio è specifico per la tua organizzazione, in quanto puoi eseguirlo manualmente oppure puoi eseguire altri strumenti per eseguire la procedura di backup.

### Entra in modalità di backup utilizzando l’API Java {#enter-backup-mode-using-the-java-api}

Attiva la modalità di backup utilizzando l’API del servizio Backup e ripristino:

1. Includi file di progetto

   Includi i file JAR client necessari, ad esempio adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare l’applicazione client Java, è necessario aggiungere i seguenti file JAR al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

1. Creare un oggetto API client BackupService

   Utilizzi un `ServiceClientFactory` e l&#39;oggetto API del client BackupService.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un `BackupService` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Decidere su un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se attivare la modalità di backup continuo

   Decidere su un&#39;etichetta univoca, determinare la quantità di tempo che si desidera allocare per eseguire il backup e decidere se si desidera che Forms Server rimanga in modalità di backup continuo.

1. Accedi alla modalità di backup

   Entra in modalità di backup richiamando `enterBackupMode` metodo con i seguenti parametri:

   * A `String` valore che specifica un&#39;etichetta univoca leggibile che identifica la sessione in modalità di backup. Si consiglia di non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * Un `int` valore che specifica il numero di minuti necessari per rimanere in modalità di backup. È possibile specificare un valore da `1` a `10080` (il numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * A `Boolean` valore che specifica se attivare la modalità di backup continuo. Un valore di `True` specifica di essere in modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti da mantenere in modalità di backup viene ignorato.

     La modalità di backup continuo indica che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente. Un valore di `False` significa che non viene utilizzata la modalità di backup continuo e, dopo aver lasciato la modalità di backup, riprende lo svuotamento dei file dal GDS.

1. Recuperare informazioni sulla sessione in modalità di backup sul server

   Recuperare le informazioni utilizzando `BackupModeEntryResult` oggetto restituito dopo aver richiamato `enterBackupMode` metodo. Le informazioni che è possibile recuperare dopo aver attivato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi di file per la procedura di backup.

1. Eseguire il backup di GDS e database

   Eseguire il backup di GDS (Global Document Storage) e del database a cui è connesso Forms Server. Le azioni per eseguire il backup non fanno parte dell’SDK di AEM Forms e possono anche includere passaggi manuali specifici per le procedure di backup dell’organizzazione.

### Entra in modalità di backup utilizzando l’API del servizio web {#enter-backup-mode-using-the-web-service-api}

Attiva la modalità di backup utilizzando il servizio Web fornito dall&#39;API del servizio Backup e ripristino:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza l&#39;API WSDL del servizio di backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto API client BackupService

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `BackupServiceService` richiamando il costruttore predefinito e specificando le credenziali utilizzando il `Credentials` metodo.

1. Decidere su un&#39;etichetta univoca, determinare il tempo necessario per eseguire il backup e decidere se attivare la modalità di backup continuo

   Decidere su un&#39;etichetta univoca, determinare la quantità di tempo che si desidera allocare per eseguire il backup e decidere se si desidera che Forms Server rimanga in modalità di backup continuo.

1. Accedi alla modalità di backup

   Per attivare la modalità di backup, richiamare il metodo enterBackupMode e passare i valori seguenti:

   * A `String` valore che specifica un&#39;etichetta univoca leggibile che identifica la sessione in modalità di backup. Si consiglia di non utilizzare spazi o caratteri che non possono essere codificati in formato XML.
   * A `Uint32` valore che specifica il numero di minuti necessari per rimanere in modalità di backup. È possibile specificare un valore da `1` a `10080` (numero di minuti in una settimana). Questo valore viene ignorato quando si utilizza la modalità di backup continuo.
   * A `Boolean` valore che specifica se attivare la modalità di backup continuo. Un valore di `True` specifica di essere in modalità di backup continuo. In modalità di backup continuo, il valore specificato per il numero di minuti da mantenere in modalità di backup viene ignorato. La modalità di backup continuo indica che una nuova sessione in modalità di backup viene avviata dopo il completamento di quella corrente.

     Un valore di `False` significa che non viene utilizzata la modalità di backup continuo e, dopo aver lasciato la modalità di backup, riprende lo svuotamento dei file dal GDS.

1. Recuperare informazioni sulla sessione in modalità di backup sul server

   Recuperare le informazioni sulla sessione in modalità di backup dopo aver richiamato il metodo enterBackupMode da BackupModeEntryResult restituito per verificare che sia stato eseguito correttamente. Le informazioni che è possibile recuperare dopo aver attivato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi di file per la procedura di backup.

1. Eseguire il backup di GDS e database

   Eseguire il backup di GDS (Global Document Storage) e del database a cui è connesso Forms Server. Le azioni per eseguire il backup non fanno parte dell’SDK di AEM Forms e possono anche includere passaggi manuali specifici per le procedure di backup dell’organizzazione.

## Uscita dalla modalità di backup sul server Forms {#leaving-backup-mode-on-the-forms-server}

Uscire dalla modalità di backup in modo che Forms Server riprenda la rimozione dei file da GDS (Global Document Storage) sul server Forms.

Prima di scrivere le applicazioni per passare alla modalità di congedo, è consigliabile comprendere le procedure di backup utilizzate con AEM Forms. Per ulteriori informazioni su cosa considerare durante l’esecuzione dei backup per AEM Forms, consulta [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Backup e ripristino, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per uscire dalla modalità di backup, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client BackupService.
1. Lascia la modalità di backup.
1. (Facoltativo) Recuperare informazioni sulla sessione in modalità di backup in esecuzione sul server Forms.

**Includi file di progetto**

Includi tutti i file necessari nel progetto di sviluppo. Questi file sono importanti per la corretta compilazione del codice e per l&#39;utilizzo dell&#39;API del servizio Backup e ripristino.

Per informazioni sulla posizione di questi file, vedere [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client BackupService**

Per uscire dalla modalità di backup a livello di programmazione, è necessario creare un oggetto client BackupService per utilizzare l&#39;API del servizio Backup e ripristino.

**Esci dalla modalità di backup**

Lasciare la modalità di backup per riprendere la normale eliminazione dei file da Global Document Storage (GDS). Prima di uscire dalla modalità di backup, è necessario verificare che le procedure di backup siano state completate.

**Recupera informazioni sulla sessione in modalità di backup terminata**

Dopo aver lasciato la modalità di backup, è possibile recuperare informazioni sulla sessione. Queste informazioni possono essere utilizzate per l&#39;integrazione con le procedure di backup.

### Lascia la modalità di backup utilizzando l’API Java {#leave-backup-mode-using-the-java-api}

Uscire dalla modalità di backup utilizzando l’API del servizio Backup e ripristino (Java):

1. Includi file di progetto

   Includi i file JAR client necessari, ad esempio adobe-backup-restore-client-sdk.jar, nel percorso di classe del progetto Java. Per creare un’applicazione client Java, è necessario aggiungere i seguenti file JAR al percorso di classe del progetto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
   * jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

1. Creare un oggetto API client BackupService

   Utilizzi un `ServiceClientFactory` e l&#39;oggetto API del client BackupService.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un `BackupService` mediante il costruttore e passando il `ServiceClientFactory` oggetto come parametro.

1. Accedi alla modalità di backup

   Lascia la modalità di backup richiamando `leaveBackupMode` metodo.

1. Recuperare informazioni sulla sessione in modalità di backup sul server

   Recuperare informazioni sull&#39;operazione utilizzando `BackupModeResult` oggetto restituito. Le informazioni che è possibile recuperare dopo aver attivato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup. Ad esempio, l&#39;etichetta, l&#39;ID di backup e l&#39;ora di inizio possono essere utili come input per i nomi di file per la procedura di backup.

### Lascia la modalità di backup utilizzando l’API del servizio web {#leave-backup-mode-using-the-web-service-api}

Uscire dalla modalità di backup utilizzando l’API del servizio Backup e ripristino (servizio web):

1. Includi file di progetto

   Per utilizzare i servizi Web, è necessario assicurarsi di includere i file proxy. Per configurare il progetto in modo che utilizzi l’API del servizio Backup e ripristino come servizio web, segui la procedura riportata di seguito.

   * Creare un assembly client Microsoft .NET che utilizza l&#39;API WSDL del servizio di backup e ripristino.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un oggetto API client BackupService

   Utilizzando l&#39;assembly client Microsoft .NET, creare un `BackupServiceService` richiamando il relativo costruttore predefinito.

1. Accedi alla modalità di backup

   Lascia la modalità di backup richiamando `leaveBackupMode` operazione del servizio web.

1. Recuperare informazioni sulla sessione in modalità di backup sul server

   Recupera l’identificatore della modalità di backup dopo l’operazione per verificarne il corretto funzionamento. Le informazioni che è possibile recuperare dopo aver lasciato la modalità di backup possono essere utili per l&#39;integrazione con le procedure di backup.
