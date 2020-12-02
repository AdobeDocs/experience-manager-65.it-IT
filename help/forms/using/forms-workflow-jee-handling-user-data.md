---
title: Flussi di lavoro Forms JEE | Gestione dei dati utente
seo-title: Flussi di lavoro Forms JEE | Gestione dei dati utente
description: Flussi di lavoro Forms JEE | Gestione dei dati utente
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---


# Flussi di lavoro Forms JEE | Gestione dei dati utente {#forms-jee-workflows-handling-user-data}

 flussi di lavoro AEM Forms JEE forniscono strumenti per progettare, creare e gestire i processi aziendali. Un processo di workflow consiste in una serie di passaggi eseguiti in un ordine specificato. Ogni passaggio esegue un’azione specifica, ad esempio l’assegnazione di un’attività a un utente o l’invio di un messaggio e-mail. Un processo può interagire con risorse, account utente e servizi e può essere attivato utilizzando uno dei seguenti metodi:

* Avvio di un processo da  AEM Forms Workspace
* Utilizzo del servizio SOAP o RESTful
* Invio di un modulo adattivo
* Utilizzo della cartella esaminata
* Utilizzo di e-mail

Per ulteriori informazioni sulla creazione  processo del flusso di lavoro AEM Forms JEE, vedere [Guida di Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

## Archivio dati utente {#user-data-and-data-stores}

Quando un processo viene avviato e in corso, acquisisce i dati sui partecipanti al processo, i dati immessi dai partecipanti nel modulo associato al processo e gli allegati aggiunti al modulo. I dati vengono memorizzati  database del server AEM Forms JEE e, se configurato, alcuni dati come gli allegati vengono memorizzati nella directory Global Document Storage (GDS). La directory GDS può essere configurata su un file system condiviso o su un database.

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

Quando viene attivato un processo, un ID univoco dell’istanza di processo e un ID di chiamata longevo vengono generati e associati all’istanza di processo. Puoi accedere ed eliminare i dati per un’istanza di processo in base all’ID chiamata longevo. Potete determinare l’ID di chiamata di lunga durata di un’istanza di processo con il nome utente dell’iniziatore del processo o dei partecipanti al processo che hanno inviato le proprie attività.

Tuttavia, non potete identificare l’ID dell’istanza di processo per un iniziatore nei seguenti scenari:

* **Processo avviato tramite una cartella** controllata: Un&#39;istanza di processo non può essere identificata utilizzando il relativo iniziatore se il processo viene avviato da una cartella esaminata. In questo caso, le informazioni utente sono codificate nei dati memorizzati.
* **Processo avviato dall’istanza** pubblica AEM: Tutte le istanze di processo attivate AEM&#39;istanza di pubblicazione non acquisiscono informazioni sull&#39;iniziatore. Tuttavia, i dati utente possono essere acquisiti nel modulo associato al processo, memorizzato nelle variabili del flusso di lavoro.
* **Processo avviato tramite e-mail**: L&#39;ID e-mail del mittente viene acquisito come proprietà in una colonna BLOB opaca della tabella del  `tb_job_instance` database, che non può essere interrogata direttamente.

### Identificare gli ID dell&#39;istanza del processo quando l&#39;iniziatore del flusso di lavoro o il partecipante è noto {#initiator-participant}

Effettuate le seguenti operazioni per identificare gli ID dell’istanza di processo per un iniziatore di flusso di lavoro o un partecipante:

1. Eseguite il seguente comando  database del server AEM Forms per recuperare l&#39;ID principale per l&#39;iniziatore del flusso di lavoro o il partecipante dalla tabella di database `edcprincipalentity`.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La query restituisce l&#39;ID principale per l&#39;elemento `user_ID` specificato.

1. (**Per l&#39;iniziatore del flusso di lavoro**) Esegui il comando seguente per recuperare tutte le attività associate all&#39;ID principale per l&#39;iniziatore dalla tabella del database `tb_task`.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La query restituisce le attività avviate dalla `initiator`_ `principal_id` specificata. Le attività sono di due tipi:

   * **Attività** completate: Queste attività sono state inviate e presentano un valore alfanumerico nel  `process_instance_id` campo. Prendete nota di tutti gli ID di istanza del processo per le attività inviate e continuate con i passaggi.
   * **Attività avviate ma non completate**: Tali attività sono iniziate ma non ancora inviate. Il valore nel campo `process_instance_id` per queste attività è **0** (zero). In questo caso, prendere nota degli ID attività corrispondenti e vedere [Operazioni con le attività orfane](#orphan).

1. (**Per i partecipanti al flusso di lavoro**) Esegui il comando seguente per recuperare gli ID dell&#39;istanza di processo associati all&#39;ID principale del partecipante al processo per l&#39;iniziatore dalla tabella di database `tb_assignment`.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La query restituisce gli ID di istanza per tutti i processi associati al partecipante, compresi quelli in cui il partecipante non ha inviato alcuna attività.

   Prendete nota di tutti gli ID di istanza del processo per le attività inviate e continuate con i passaggi.

   Per le attività o le attività orfane in cui `process_instance_id` è 0 (zero), prendere nota degli ID attività corrispondenti e vedere [Operazioni con le attività orfane](#orphan).

1. Seguite le istruzioni riportate nella sezione [Rimozione dei dati utente dalle istanze del flusso di lavoro in base agli ID di istanza del processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) per eliminare i dati utente per gli ID di istanza del processo identificati.

### Identificare gli ID dell&#39;istanza del processo quando i dati dell&#39;utente vengono memorizzati in variabili primitive {#primitive}

Un flusso di lavoro può essere progettato in modo che i dati utente vengano acquisiti in una variabile che viene memorizzata come BLOB nel database. In questi casi, potete eseguire una query sui dati utente solo se sono memorizzati in una delle seguenti variabili di tipo primitivo:

* **Stringa**: Contiene l’ID utente direttamente o sotto forma di sottostringa e può essere interrogato utilizzando SQL.
* **Numerico**: Contiene direttamente l’ID utente.
* **XML**: Contiene l’ID utente come sottostringa all’interno del testo memorizzato come colonne di testo nel database e può essere interrogato come stringhe.

Per determinare se un flusso di lavoro che memorizza i dati in variabili di tipo primitivo contiene i dati per l’utente, procedere come segue:

1. Eseguite il seguente comando del database:

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La query restituisce un nome di tabella in formato `tb_<number>` per l&#39;applicazione specificata ( `app_name`) e il flusso di lavoro ( `workflow_name`).

   >[!NOTE]
   >
   >Il valore della proprietà `name` può essere complesso se il flusso di lavoro è nidificato all&#39;interno di sottocartelle all&#39;interno dell&#39;applicazione. Assicurarsi di specificare il percorso completo esatto del flusso di lavoro, che è possibile ottenere dalla tabella del database `omd_object_type`.

1. Esaminare lo schema della tabella `tb_<number>`. La tabella contiene variabili che memorizzano i dati utente per il flusso di lavoro specificato. Le variabili della tabella corrispondono alle variabili del flusso di lavoro.

   Identificate e prendete nota della variabile corrispondente alla variabile del flusso di lavoro contenente l’ID utente. Se la variabile identificata è di tipo primitivo, potete eseguire una query per determinare le istanze del flusso di lavoro associate a un ID utente.

1. Esegui il seguente comando del database. In questo comando, `user_var` è la variabile di tipo primitivo che contiene l&#39;ID utente.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La query restituisce tutti gli ID di istanza del processo associati alla `user_ID` specificata.

1. Seguite le istruzioni riportate nella sezione [Rimozione dei dati utente dalle istanze del flusso di lavoro in base agli ID di istanza del processo](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) per eliminare i dati utente per gli ID di istanza del processo identificati.

### Elimina i dati utente dalle istanze del flusso di lavoro in base agli ID dell&#39;istanza di processo {#purge}

Dopo aver identificato gli ID dell’istanza di processo associati a un utente, effettuate le seguenti operazioni per eliminare i dati utente dalle rispettive istanze di processo.

1. Eseguite il comando seguente per recuperare l&#39;ID chiamata e lo stato di lunga durata per un&#39;istanza di processo dalla tabella `tb_process_instance`.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La query restituisce l&#39;ID chiamata longevo e lo stato per l&#39;elemento `process_instance_id` specificato.

1. Creare un&#39;istanza del client pubblico `ProcessManager` ( `com.adobe.idp.workflow.client.ProcessManager`) utilizzando un&#39;istanza `ServiceClientFactory` con le impostazioni di connessione corrette.

   Per ulteriori informazioni, consultare il riferimento alle API Java per [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. Controllare lo stato dell&#39;istanza del flusso di lavoro. Se lo stato è diverso da 2 (COMPLETE) o 4 (TERMINATED), terminare l’istanza chiamando il seguente metodo:

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Eliminate l’istanza del flusso di lavoro chiamando il seguente metodo:

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   Il metodo `purgeProcessInstance` elimina completamente tutti i dati per l&#39;ID di chiamata specificato  database del server AEM Forms e GDS, se configurato.

### Operazioni con le attività orfane {#orphan}

Le attività orfane sono le attività il cui processo di contenimento è stato avviato ma non ancora inviato. in questo caso, il `process_instance_id` è **0** (zero). Pertanto, non è possibile tracciare i dati utente memorizzati per le attività orfane utilizzando gli ID di istanza del processo. Tuttavia, è possibile tracciarlo utilizzando l&#39;ID attività per un&#39;attività orfana. È possibile identificare gli ID delle attività dalla tabella `tb_task` per un utente come descritto in [Identificare gli ID dell&#39;istanza del processo quando l&#39;iniziatore del flusso di lavoro o il partecipante è noto](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Dopo aver ottenuto gli ID attività, effettuate le seguenti operazioni per eliminare i file e i dati associati con un&#39;attività orfana da GDS e database.

1. Esegui il seguente comando  database del server AEM Forms per recuperare gli ID per gli ID attività identificati.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La query restituisce un elenco di ID. Per ciascun ID ( `fd_id`) restituito nei risultati, create un elenco di stringhe ID sessione come segue:

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. A seconda che GDS punti a un file system o a un database, eseguire una delle operazioni seguenti:

   1. **GDS nel file system**

      Nel file system GDS:

      1. Cercate file con le seguenti stringhe ID sessione come estensioni:
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      I file con queste estensioni sono i file marcatore. Sono memorizzati con nomi file nel seguente formato:

      `<file_name_guid>.session<session_id_string>`

      1. Eliminate dal file system tutti i file marcatore e altri file con il nome file esatto come `<file_name_guid>`.
   1. **GDS nel database**

      Eseguite i comandi seguenti per ciascun ID sessione:

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Per eliminare i dati per gli ID attività dal database del server AEM Forms , eseguite i seguenti comandi:

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

