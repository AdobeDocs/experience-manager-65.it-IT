---
title: Flussi di lavoro di Forms JEE | Gestione dei dati utente
description: Scopri come utilizzare i flussi di lavoro di AEM Forms JEE per progettare, creare e gestire i processi aziendali.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Flussi di lavoro di Forms JEE | Gestione dei dati utente {#forms-jee-workflows-handling-user-data}

I flussi di lavoro di AEM Forms JEE forniscono gli strumenti necessari per progettare, creare e gestire i processi aziendali. Un processo del flusso di lavoro è costituito da una serie di passaggi che vengono eseguiti in un ordine specificato. Ogni passaggio esegue un’azione specifica, ad esempio l’assegnazione di un’attività a un utente o l’invio di un messaggio e-mail. Un processo può interagire con risorse, account utente e servizi e può essere attivato utilizzando uno dei seguenti metodi:

* Avvio di un processo da AEM Forms Workspace
* Utilizzo del servizio SOAP o RESTful
* Invio di un modulo adattivo
* Utilizzo della cartella controllata
* Utilizzo dell’e-mail

Per ulteriori informazioni sulla creazione del processo del flusso di lavoro AEM Forms JEE, consulta la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65_it).

## Dati utente e archivi dati {#user-data-and-data-stores}

Quando un processo viene attivato e durante l&#39;avanzamento, acquisisce i dati relativi ai partecipanti al processo, i dati immessi dai partecipanti nel modulo associato al processo e gli allegati aggiunti al modulo. I dati vengono memorizzati nel database del server AEM Forms JEE e, se configurati, alcuni dati, come gli allegati, vengono memorizzati nella directory Global Document Storage (GDS). La directory GDS può essere configurata in un file system condiviso o in un database.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

Quando viene attivato un processo, vengono generati un ID univoco dell&#39;istanza del processo e un ID di chiamata di lunga durata associati all&#39;istanza del processo. Puoi accedere ai dati di un’istanza di processo ed eliminarli in base all’ID di chiamata di lunga durata. È possibile dedurre l&#39;ID di chiamata di lunga durata di un&#39;istanza di processo con il nome utente dell&#39;iniziatore del processo o dei partecipanti al processo che hanno inviato le proprie attività.

Tuttavia, non è possibile identificare l&#39;ID istanza processo per un iniziatore nei seguenti scenari:

* **Processo attivato tramite una cartella controllata**: impossibile identificare un&#39;istanza del processo utilizzando il relativo iniziatore se il processo è attivato da una cartella controllata. In questo caso, le informazioni utente vengono codificate nei dati memorizzati.
* **Processo avviato dall&#39;istanza di pubblicazione dell&#39;AEM**: tutte le istanze di processo attivate dall&#39;istanza di pubblicazione dell&#39;AEM non acquisiscono informazioni sull&#39;iniziatore. Tuttavia, i dati utente possono essere acquisiti nel modulo associato al processo, memorizzato nelle variabili del flusso di lavoro.
* **Processo avviato tramite e-mail**: l&#39;ID e-mail del mittente viene acquisito come proprietà in una colonna BLOB opaca della tabella del database `tb_job_instance`, che non può essere interrogata direttamente.

### Identificare gli ID delle istanze di processo quando è noto l&#39;iniziatore o il partecipante del flusso di lavoro {#initiator-participant}

Per identificare gli ID delle istanze di processo per un iniziatore del flusso di lavoro o un partecipante, effettuare le seguenti operazioni:

1. Eseguire il comando seguente nel database di AEM Forms Server per recuperare l&#39;ID entità per l&#39;iniziatore o il partecipante del flusso di lavoro dalla tabella del database `edcprincipalentity`.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La query restituisce l&#39;ID entità per `user_ID` specificato.

1. (**Per l&#39;iniziatore del flusso di lavoro**) Eseguire il comando seguente per recuperare dalla tabella del database `tb_task` tutte le attività associate all&#39;ID entità per l&#39;iniziatore.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La query restituisce le attività avviate dal `initiator`_ `principal_id` specificato. Le attività sono di due tipi:

   * **Attività completate**: queste attività sono state inviate e visualizzano un valore alfanumerico nel campo `process_instance_id`. Prendi nota di tutti gli ID istanza processo per le attività inviate e continua con i passaggi.
   * **Attività avviate ma non completate**: queste attività sono state avviate ma non ancora inviate. Il valore nel campo `process_instance_id` per queste attività è **0** (zero). In questo caso, prendere nota degli ID attività corrispondenti e vedere [Operazioni con attività orfane](#orphan).

1. (**Per i partecipanti al flusso di lavoro**) Eseguire il comando seguente per recuperare gli ID istanza processo associati all&#39;ID entità del partecipante processo per l&#39;iniziatore dalla tabella del database `tb_assignment`.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La query restituisce gli ID istanza per tutti i processi associati al partecipante, inclusi quelli in cui il partecipante non ha sottomesso alcun task.

   Prendi nota di tutti gli ID istanza processo per le attività inviate e continua con i passaggi.

   Per le attività orfane o per le attività in cui `process_instance_id` è 0 (zero), prendere nota degli ID delle attività corrispondenti e vedere [Operazioni con le attività orfane](#orphan).

1. Segui le istruzioni riportate nella sezione [Eliminare i dati utente dalle istanze del flusso di lavoro in base agli ID istanza processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) in modo da poter eliminare i dati utente per gli ID istanza processo identificati.

### Identificare gli ID delle istanze di processo quando i dati utente vengono memorizzati in variabili primitive {#primitive}

Un flusso di lavoro può essere progettato in modo che i dati utente vengano acquisiti in una variabile che viene memorizzata come BLOB nel database. In questi casi, è possibile eseguire query sui dati utente solo se sono memorizzati in una delle seguenti variabili di tipo primitivo:

* **Stringa**: contiene l&#39;ID utente direttamente o come sottostringa e può essere interrogato utilizzando SQL.
* **Numerico**: contiene direttamente l&#39;ID utente.
* **XML**: contiene l&#39;ID utente come sottostringa all&#39;interno del testo memorizzato come colonne di testo nel database ed è possibile eseguire query come stringhe.

Effettua le seguenti operazioni per determinare se un flusso di lavoro che memorizza i dati in variabili di tipo primitivo contiene dati per l’utente:

1. Eseguire il comando di database seguente:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La query restituisce un nome di tabella in formato `tb_<number>` per l&#39;applicazione specificata ( `app_name`) e il flusso di lavoro ( `workflow_name`).

   >[!NOTE]
   >
   >Il valore della proprietà `name` può essere complesso se il flusso di lavoro è nidificato nelle sottocartelle all&#39;interno dell&#39;applicazione. Assicurarsi di specificare il percorso completo esatto del flusso di lavoro, che è possibile ottenere dalla tabella del database `omd_object_type`.

1. Esaminare lo schema della tabella `tb_<number>`. La tabella contiene variabili che memorizzano i dati utente per il flusso di lavoro specificato. Le variabili nella tabella corrispondono alle variabili nel flusso di lavoro.

   Identifica e prendi nota della variabile corrispondente alla variabile del flusso di lavoro contenente l’ID utente. Se la variabile identificata è di tipo primitivo, puoi eseguire una query per determinare le istanze del flusso di lavoro associate a un ID utente.

1. Eseguire il comando seguente del database. In questo comando, `user_var` è la variabile di tipo primitivo che contiene l&#39;ID utente.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La query restituisce tutti gli ID istanza processo associati al `user_ID` specificato.

1. Segui le istruzioni riportate nella sezione [Eliminare i dati utente dalle istanze del flusso di lavoro in base agli ID istanza processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) in modo da poter eliminare i dati utente per gli ID istanza processo identificati.

### Rimuovi i dati utente dalle istanze del flusso di lavoro in base agli ID delle istanze del processo {#purge}

Dopo aver identificato gli ID delle istanze di processo associati a un utente, effettuare le seguenti operazioni per eliminare i dati utente dalle rispettive istanze di processo.

1. Eseguire il comando seguente per recuperare dalla tabella `tb_process_instance` l&#39;ID e lo stato di chiamata di lunga durata per un&#39;istanza di processo.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La query restituisce l&#39;ID e lo stato di chiamata di lunga durata per l&#39;oggetto `process_instance_id` specificato.

1. Creare un&#39;istanza del client `ProcessManager` pubblico ( `com.adobe.idp.workflow.client.ProcessManager`) utilizzando un&#39;istanza `ServiceClientFactory` con le impostazioni di connessione corrette.

   Per ulteriori informazioni, vedere Riferimento API Java™ per [Class ProcessManager](https://helpx.adobe.com/it/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Controlla lo stato dell’istanza del flusso di lavoro. Se lo stato è diverso da 2 (COMPLETE) o 4 (TERMINATED), terminare prima l&#39;istanza chiamando il metodo seguente:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Rimuovi l’istanza del flusso di lavoro chiamando il metodo seguente:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   Il metodo `purgeProcessInstance` elimina completamente tutti i dati per l&#39;ID di chiamata specificato dal database di AEM Forms Server e da GDS, se configurato.

### Operazioni con le attività orfane {#orphan}

Le attività orfane sono le attività il cui processo contenitore è stato avviato ma non ancora inviato. In questo caso, `process_instance_id` è **0** (zero). Pertanto, non è possibile tracciare i dati utente archiviati per le attività orfane utilizzando gli ID delle istanze di processo. Tuttavia, è possibile tracciarla utilizzando l&#39;ID attività per un&#39;attività orfana. È possibile identificare gli ID delle attività dalla tabella `tb_task` per un utente come descritto in [Identificare gli ID delle istanze del processo quando è noto l&#39;iniziatore del flusso di lavoro o il partecipante](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Una volta ottenuti gli ID delle attività, eseguire le operazioni seguenti per eliminare i file e i dati associati a un&#39;attività orfana da GDS e dal database.

1. Esegui il comando seguente sul database di AEM Forms Server per recuperare gli ID delle attività identificate.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La query restituisce un elenco di ID. Per ogni ID ( `fd_id`) restituito nei risultati, crea un elenco di stringhe di ID sessione come segue:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. A seconda che il GDS punti a un file system o a un database, effettuare una delle seguenti operazioni:

   1. **GDS nel file system**

      Nel file system GDS:

      1. Cerca file con le seguenti stringhe ID sessione come estensioni:

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      I file con queste estensioni sono i file marcatore. Vengono memorizzati con i nomi file nel seguente formato:

      `<file_name_guid>.session<session_id_string>`

      1. Eliminare dal file system tutti i file dei marcatori e gli altri file con il nome di file esatto `<file_name_guid>`.

   1. **GDS nel database**

      Esegui i seguenti comandi per ogni ID sessione:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. Eseguire i seguenti comandi per eliminare i dati per gli ID attività dal database di AEM Forms Server:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
