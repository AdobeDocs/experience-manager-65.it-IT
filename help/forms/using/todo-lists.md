---
title: Utilizzo degli elenchi Attività
seo-title: Working with To-do lists
description: Come aprire, lavorare e completare le attività in base alle esigenze, ad esempio approvare o rifiutare una richiesta o aggiungere ulteriori informazioni.
seo-description: How to open, work on, and complete the tasks as required, such as approving or rejecting a request or adding more information.
uuid: f9cfad8e-5d0c-4a30-8153-2a03bf7dd986
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d8546227-d78d-4fe2-a092-222482bb69c9
docset: aem65
exl-id: c80bf347-d1ed-488f-a41a-ceb05a6df9e4
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 0%

---

# Utilizzo degli elenchi Attività{#working-with-to-do-lists}

Quando si visualizzano gli elenchi attività, è possibile che vengano visualizzate le attività di un processo aziendale assegnate all&#39;utente o a qualsiasi gruppo a cui l&#39;utente appartiene o che siano attività condivise di altri utenti. È possibile aprire, lavorare e completare le attività in base alle esigenze, ad esempio approvando o rifiutando una richiesta o aggiungendo ulteriori informazioni. Dopo aver completato un&#39;attività, questa viene inviata alla persona successiva nel processo aziendale,

## Informazioni sugli elenchi attività {#about-todo-lists}

L’area di lavoro di AEM Forms include i tre tipi di elenchi attività seguenti:

* Singoli elenchi, che contengono attività assegnate direttamente all&#39;utente.
* Elenchi di gruppi, che contengono attività assegnate a un gruppo. Qualsiasi membro del gruppo può aprire e completare le attività. Per aprire un&#39;attività, un membro di un gruppo deve prima richiedere l&#39;attività.
* Elenchi condivisi, che contengono attività assegnate a un utente che ha condiviso il proprio elenco attività con te ed eventualmente con altri utenti. Qualsiasi utente che condivide un elenco può richiedere, aprire e completare attività condivise.

È possibile eseguire alcune azioni senza aprire l&#39;attività facendo clic sulle icone visualizzate quando si posiziona il puntatore del mouse su un&#39;attività.

>[!NOTE]
>
>Un&#39;icona esclamativa indica che l&#39;attività ha priorità alta.

## Attività tipiche {#typical-tasks}

Quando apri e lavori su un’attività, gli strumenti disponibili dipendono dall’attività. Attività diverse richiedono di eseguire azioni diverse e, per questo motivo, alcuni strumenti potrebbero non essere disponibili. Di seguito sono descritte le attività tipiche che potresti ricevere.

* **Fornisci informazioni**: viene visualizzata un’attività che richiede il completamento e l’invio di un modulo.

* **Informazioni sulla revisione**: ricevi un’attività che richiede di rivedere le informazioni e di approvare il contenuto.

* **Revisione multiutente**: quando altri utenti ricevono l’attività, questa viene ricevuta insieme all’attività. Tu e gli altri utenti dovete fornire informazioni o rivedere il contenuto, o entrambi. Con questo tipo di attività possono essere disponibili i seguenti strumenti:

   * Visualizzazione delle istruzioni per l&#39;attività
   * Visualizzazione dello stato di completamento di tutti gli utenti assegnati all&#39;attività
   * Visualizzazione dei commenti di tutti gli utenti assegnati all&#39;attività
   * Aggiunta di commenti all&#39;attività

Altri strumenti che possono essere disponibili con una qualsiasi delle attività di cui sopra includono:

* Inoltra
* Condividi
* Consulta
* Ritorno
* Note
* Allegati

## Apertura delle attività {#opening-tasks}

È possibile aprire e bloccare le attività dall&#39;elenco delle attività oppure richiedere e aprire le attività da un gruppo o da un elenco attività condiviso. Quando si apre un&#39;attività, questa viene visualizzata nel riquadro principale. Le altre attività vengono visualizzate nell&#39;elenco delle attività accanto all&#39;elenco Da fare.

Se è presente un URL di riepilogo attività, per impostazione predefinita viene aperta la visualizzazione Riepilogo attività, anziché il modulo associato a un&#39;attività. Anche quando un utente abilita l’opzione &quot;Apri il modulo in modalità ingrandita&quot; in Assegna attività, il modulo non si apre in modalità ingrandita.

>[!NOTE]
>
>Quando si apre un&#39;attività, a seconda delle impostazioni predefinite dell&#39;attività, è possibile che la maschera associata venga visualizzata in visualizzazione completa.

### Aprire e bloccare un&#39;attività dall&#39;elenco {#open-and-lock-a-task-from-your-list}

Quando si apre un&#39;attività dall&#39;elenco delle cose da fare, se l&#39;elenco è condiviso, è possibile bloccarla per impedire a un altro utente che ha accesso all&#39;elenco di lavorare sull&#39;attività.

1. Nella pagina Da fare, nel riquadro a sinistra, selezionare il singolo elenco Da fare. Tutte le attività vengono visualizzate nel riquadro centrale.

   >[!NOTE]
   >
   >È possibile filtrare le attività selezionando il tipo di processo nell&#39;elenco Da fare. È possibile selezionare l&#39;elenco Da fare per visualizzare di nuovo tutte le attività nell&#39;elenco Da fare.

1. Se necessario, blocca l’attività. Per bloccare un task, fare clic sull&#39;icona Tutte le opzioni del task e selezionare Blocca. Passa il puntatore del mouse sull’attività per rendere disponibile l’opzione.

   >[!NOTE]
   >
   >È inoltre possibile bloccare o sbloccare un&#39;attività in qualsiasi scheda quando l&#39;attività è aperta.

   ![lock_task](assets/lock_task.png)

   Menu Tutte le opzioni di un&#39;attività

1. Apri l’attività facendo clic su di essa.

### Aprire e richiedere un&#39;attività da un elenco condiviso o di gruppo {#open-and-claim-a-task-from-a-shared-or-group-list}

Quando si apre e si richiede un&#39;attività da un gruppo o da un elenco condiviso, l&#39;attività viene spostata dal gruppo o dall&#39;elenco condiviso al singolo elenco attività. Gli altri utenti con accesso all’elenco non possono lavorare sull’attività.

1. Nel riquadro a sinistra della pagina Da fare selezionare un gruppo o un elenco di cose da fare condiviso. Tutte le attività vengono visualizzate nel riquadro centrale.
1. Effettua una delle seguenti operazioni:

   * Per richiedere un&#39;attività, senza aprirla, da un gruppo o da un elenco attività condiviso, fare clic su  **Richiesta di rimborso** posizionando il puntatore del mouse sull&#39;attività. In alternativa, quando l&#39;attività è aperta, il pulsante Attestazione è disponibile nella barra delle azioni sotto il riquadro attività. Quando viene presentata una richiesta di rimborso, un&#39;attività viene spostata dal gruppo o dall&#39;elenco attività condivise all&#39;elenco.
   * Per richiedere e aprire un&#39;attività da un gruppo o da un elenco attività condiviso, fare clic su **Richieste di rimborso e aperte**.

## Utilizzo delle attività {#working-with-tasks}

Dopo aver aperto un&#39;attività, le schede visualizzate nel riquadro principale e gli strumenti disponibili dipendono dall&#39;attività. Di seguito sono descritte le schede che è possibile visualizzare:

* **Riepilogo attività**: all&#39;apertura di un&#39;attività, il riquadro Riepilogo attività consente di visualizzare informazioni sull&#39;attività, se presente, utilizzando un URL specificato nel processo al passaggio Assegna attività. Tramite il Riquadro di riepilogo delle attività è possibile visualizzare informazioni aggiuntive e rilevanti per un’attività, in modo da aggiungere più valore all’utente finale dell’area di lavoro di AEM Forms. Questa scheda non è disponibile se l&#39;URL di riepilogo attività non esiste.

* **Dettagli**: fornisce alcune informazioni sull&#39;attività corrente e sul processo a cui appartiene.

* **Modulo**: visualizza il modulo associato all’attività. Il modulo può essere di diversi tipi, tra cui PDF, HTML, Guide e SWF. Il modulo può avere l&#39;aspetto di un normale modulo stampabile o basato su Web oppure può essere una guida attraverso una serie di pannelli in stile procedura guidata per raccogliere informazioni.

* **Cronologia**: elenca le attività che fanno parte dell&#39;istanza del processo e il modulo associato, le assegnazioni delle attività e gli allegati per ogni attività.

* **Allegati**: visualizza gli allegati esistenti associati all’attività e, se necessario, aggiunge allegati.

* **Note**: visualizza le note esistenti associate all’attività e, se necessario, aggiunge note.

Quando lavori su un’attività, di seguito sono descritti gli strumenti che potresti visualizzare e le azioni che puoi intraprendere.

### Inoltrare, condividere o consultare un&#39;attività {#forward-share-or-consult-on-a-task}

È possibile inoltrare un&#39;attività insieme a eventuali note o allegati a un altro utente oppure condividere l&#39;attività o consultarla con un altro utente. Se si modificano i dati del modulo associati a un&#39;attività, salvare il modulo come bozza prima di inoltrare, condividere o consultare l&#39;attività. In caso contrario, l’attività viene inviata senza il modulo aggiornato. Dopo l&#39;inoltro e la condivisione di un&#39;attività, l&#39;utente che riceve l&#39;attività può richiederla e completarla oppure restituirla all&#39;utente. Se si consulta un&#39;attività, l&#39;utente può solo restituirla all&#39;utente.

1. Se si modifica un modulo associato a un&#39;attività che si desidera mantenere, fare clic su **Salva**. L’opzione Salva è disponibile nella barra delle azioni nella parte inferiore di ogni scheda. In caso contrario, l’attività viene inviata senza il modulo aggiornato.

   >[!NOTE]
   >
   >Il pulsante Salva non è disponibile per alcuni moduli, a seconda dell’attività su cui stai lavorando.

1. In una scheda qualsiasi, fare clic su uno dei pulsanti seguenti:

   * **Inoltra**
   * **Condividi**
   * **Consulta**

   >[!NOTE]
   >
   >A seconda dell&#39;attività, è possibile eseguire queste azioni anche dall&#39;elenco Da fare senza aprire l&#39;attività.

1. Nella finestra di dialogo a comparsa, cercare e selezionare il nome dell&#39;utente con cui inoltrare, condividere o consultare l&#39;attività.

### Restituire un’attività {#return-a-task}

1. In qualsiasi scheda, fai clic su **Ritorno**. L&#39;attività viene riportata nell&#39;elenco attività dell&#39;utente che l&#39;ha precedentemente inoltrata oppure condivisa o consultata con l&#39;utente.

### Disconnetti un&#39;attività {#take-a-task-offline}

Può essere consentito lavorare su un&#39;attività offline e successivamente inviare il relativo modulo da Adobe® Reader® o Adobe® Acrobat® Professional o Adobe® Acrobat® Standard. Quando il modulo viene inviato, il client e-mail viene avviato con l’indirizzo e-mail del server appropriato. A questo punto potrai inviare il modulo completato via e-mail al server.

1. In qualsiasi scheda, fai clic su **Offline**.
1. Specifica un nome file in cui salvare il modulo e fai clic su **Salva**. Il modulo associato all&#39;attività viene salvato localmente e l&#39;attività rimane nell&#39;elenco attività fino all&#39;invio del modulo.

### Utilizzare gli allegati {#work-with-attachments}

È possibile aggiungere, aggiornare, eliminare o salvare gli allegati in locale.

**Aggiungi un allegato**

1. In **Allegati** , fare clic su **Sfoglia** per selezionare il file da allegare.
1. Seleziona la **Autorizzazioni** livello dell&#39;allegato per altri utenti che partecipano al processo. Se si seleziona **Letto**, altri utenti possono salvare il file localmente. Se selezioni una delle autorizzazioni di modifica, anche altri utenti possono caricare un nuovo file per sostituire l’allegato.

   >[!NOTE]
   >
   >È inoltre possibile aggiungere commenti insieme agli allegati.

1. Clic **Carica**. Il file viene allegato al modulo.

**Visualizzare un allegato**

1. Il giorno **Allegati** fare clic sul nome file dell&#39;allegato da visualizzare.

**Salvare un allegato localmente**

1. Fare clic su un allegato per aprirlo. Salvare localmente l&#39;allegato aperto.

**Aggiornare un allegato**

1. Clic **Modifica** per l&#39;allegato. Selezionare il file con cui sostituire l&#39;allegato esistente facendo clic su **Sfoglia**.

**Eliminare un allegato**

1. Clic **Elimina** per un allegato.

### Salvare i dati senza completare l&#39;attività {#save-your-work-without-completing-the-task}

1. In qualsiasi scheda, tocca **Salva**.

   Viene visualizzata la finestra di dialogo Salva come bozza. Il nome predefinito della bozza corrisponde al nome dell&#39;attività del modello di attività.

   ![saveasdraft tdialog](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >È possibile configurare Workspace in modo da salvare automaticamente periodicamente le informazioni immesse come bozza da un utente. Se il salvataggio automatico è abilitato e un utente sta lavorando a una bozza, la bozza viene salvata periodicamente. In caso di salvataggio automatico, viene utilizzato automaticamente il nome predefinito dell&#39;attività.
   >
   >
   >Per ulteriori informazioni, consultate Salvare periodicamente una bozza in [Gestione delle preferenze](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. Nella finestra di dialogo Salva come bozza, specifica un nome univoco per l’attività e tocca **OK**.

   ![saveasdraft_dialog_name](assets/saveasdraftdialog_name.png)

   La bozza viene salvata con il nome specificato. L&#39;attività rimane nell&#39;elenco Da fare ed eventuali modifiche apportate nel modulo vengono salvate nella cartella Bozze. Inoltre, nell’elenco Da fare, puoi cercare la bozza utilizzando il nome della bozza per riprendere a lavorarci.

   ![searchfortask](assets/searchfortask.png)

## Completamento delle attività {#completing-tasks}

La modalità di completamento di un&#39;attività dipende dall&#39;attività stessa e dal ruolo svolto nel processo. Potrebbe essere richiesto di approvare o rifiutare una richiesta, fornire contenuto, rivedere e verificare le informazioni o indicare che si è agito.

È possibile completare un&#39;attività in vari modi:

* Utilizzo delle azioni disponibili in una qualsiasi delle schede
* Utilizzo delle azioni create nel modulo stesso
* Dall&#39;elenco attività, senza aprire l&#39;attività

>[!NOTE]
>
>Questa opzione è disponibile se `isMustOpenToComplete` non è selezionato in `Assign Task` durante la progettazione di un processo.

* Per e-mail, se ricevi notifiche e-mail

Quando si completa un&#39;attività, a seconda dell&#39;attività, potrebbe essere visualizzata una finestra di dialogo di conferma che conferma l&#39;azione. Ad esempio, potrebbe essere visualizzata una finestra di dialogo in cui viene richiesto di attestare la validità delle informazioni fornite.

>[!NOTE]
>
>Se si è modificata un&#39;attività ma non si è pronti per completarla, è possibile salvare il lavoro come bozza facendo clic su Salva e tornare in seguito.

### Completare un&#39;attività {#complete-a-task}

1. Effettua una delle seguenti operazioni:

   * Selezionare l&#39;attività e fare clic sul pulsante appropriato per il passaggio successivo richiesto nel processo nella parte inferiore dell&#39;elenco.
   * Se il modulo non dispone di pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms è disponibile, fai clic su **Completa**.
   * Se il modulo include pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms non è disponibile, fai clic sul pulsante appropriato nel modulo per il passaggio successivo richiesto nel processo.

   Se il modulo non dispone di pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms non è disponibile, viene visualizzato un messaggio che indica che il modulo non può essere inviato.

1. Se viene visualizzata una finestra di dialogo di conferma, eseguire una delle operazioni seguenti:

   * Clic **OK** se l&#39;attività è stata completata e si è pronti per l&#39;accesso.
   * Clic **Annulla** se si desidera tornare all&#39;attività e non si è pronti per accedervi.

>[!NOTE]
>
>È possibile che venga visualizzato un pulsante Invia all&#39;interno dei moduli HTML quando in un modulo vengono utilizzate le proprietà del processo. Questo pulsante non è visibile quando viene eseguito il rendering dello stesso modulo come PDF. Per completare un’attività, fai clic sul pulsante Invia disponibile nella parte inferiore dell’area di lavoro di AEM Forms, all’esterno del modulo e non sul pulsante Invia all’interno del modulo.

### Approva in blocco le attività {#bulk-approve-tasks}

È possibile inviare più attività dall&#39;elenco Da fare. È possibile inviare insieme solo le attività dello stesso processo, con gli stessi nomi di attività e le stesse opzioni di instradamento.

>[!NOTE]
>
>Questa opzione è disponibile se il campo isMustOpenToComplete non è selezionato nel passaggio Assegna attività di Workbench durante la progettazione di un processo.

1. Nella pagina Da fare, nel riquadro a sinistra, selezionare il singolo elenco Da fare. Tutte le attività vengono visualizzate nel riquadro centrale.
1. Seleziona **Abilita modalità collettiva**. Le caselle di controllo vengono visualizzate davanti alle attività dell&#39;elenco.

   >[!NOTE]
   >
   >Questa opzione non è disponibile per le attività per le quali è selezionato il campo isMustOpenToComplete nel passaggio Assegna attività di Workbench durante la progettazione di un processo. Le caselle di controllo di tali attività nell&#39;elenco Da fare rimangono sempre disattivate.

1. Selezionare le attività per l&#39;approvazione in blocco. È possibile selezionare più attività dello stesso processo, con gli stessi nomi di attività e le stesse opzioni di instradamento. Dopo aver selezionato un&#39;attività per l&#39;approvazione, rimangono abilitate solo le attività con lo stesso processo, con gli stessi nomi di attività e le stesse opzioni di instradamento. Gli altri sono disabilitati.

   ![1_bulkapproval](assets/1_bulkapproval.png)

1. Fare clic sull&#39;opzione di invio disponibile. Le attività selezionate vengono inviate.

   ![approvazione collettiva](assets/bulkapproval.png)

## Partecipazione alle attività tramite e-mail {#participating-in-tasks-through-email}

Puoi ricevere e completare le attività tramite e-mail. La partecipazione alle attività tramite e-mail elimina la necessità di controllare regolarmente l’elenco Attività per verificare se sono presenti nuove attività o la pagina Tracciamento per verificare lo stato di un’attività.

Innanzitutto, imposta le preferenze dell’area di lavoro AEM Forms per ricevere le notifiche e-mail. L’area di lavoro di AEM Forms può inviare notifiche e-mail per le attività incluse nell’elenco Attività o in qualsiasi elenco Attività del gruppo a cui appartieni. L’amministratore determina quando vengono inviati e chi li riceve i messaggi di notifica e-mail.

I messaggi e-mail possono contenere un collegamento che apre l’attività nell’area di lavoro di AEM Forms, un allegato del modulo utilizzato per l’attività o azioni per completare l’attività tramite e-mail. Se nel messaggio di posta elettronica è incluso un modulo, è possibile aprire il modulo e completare l&#39;attività se i pulsanti per il completamento dell&#39;attività sono incorporati nel modulo. Se le azioni per il completamento dell’attività sono incluse nel messaggio e-mail, puoi completare l’attività facendo clic sulle azioni nell’e-mail o rispondendo all’e-mail con l’azione digitata come prima riga nel corpo dell’e-mail.

>[!NOTE]
>
>* Per configurare l’area di lavoro in modo che utilizzi i modelli e-mail appropriati, consulta la sezione [Guida per l’amministratore di AEM Forms JEE](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/).
>
>* Se le bozze vengono inoltrate dopo l’invio dell’attività nell’area di lavoro di AEM Forms, vengono inviate notifiche e-mail. Se le bozze vengono inoltrate dal punto d’inizio dell’area di lavoro di AEM Forms, non vengono inviate notifiche e-mail.

Quando si completa un’attività tramite e-mail, questa viene rimossa dall’elenco Attività nell’area di lavoro di AEM Forms.

>[!NOTE]
>
>Se l’utente non ha effettuato l’accesso all’area di lavoro di AEM Forms nel browser e apre un collegamento a un’attività Da fare, il collegamento diretto non si apre e viene visualizzata un’eccezione. Accedi all’area di lavoro di AEM Forms prima di fare clic sui collegamenti nelle e-mail.

>[!NOTE]
>
>Non è possibile inoltrare una notifica e-mail per assegnare un&#39;attività a un altro utente. Puoi inoltrare le attività ad altri utenti solo dall’area di lavoro di AEM Forms.

### Ricezione di messaggi di notifica e-mail {#receive-email-notification-messages}

1. Clic **Preferenze**.
1. In **Notifica eventi attività tramite e-mail** elenco, seleziona **Sì**.
1. Per includere il modulo e i dati con il messaggio e-mail, nel **Allega Forms tramite e-mail** elenco, seleziona **Sì**.

## Partecipazione ad attività tramite dispositivi mobili {#participating-in-tasks-through-mobile-devices}

Puoi usare l’app AEM Forms Workspace per partecipare alle attività dal tuo dispositivo mobile. Prima di installare l’applicazione, rivolgiti all’amministratore di sistema per assicurarti che la tua organizzazione supporti l’utilizzo dell’app AEM Forms Workspace.

## Informazioni su scadenze e promemoria {#about-deadlines-and-reminders}

A *scadenza* determina la data e l&#39;ora entro cui è necessario completare un&#39;attività. Quando una scadenza viene superata, il server indirizza l&#39;attività alla fase successiva del processo (che può essere l&#39;elenco attività di un altro utente), quindi sull&#39;attività viene visualizzata l&#39;icona della scadenza. L’icona della scadenza viene visualizzata indipendentemente dalle regole associate al processo.

A *promemoria* notifica un&#39;attività che richiede l&#39;attenzione dell&#39;utente. I promemoria si verificano a un orario predeterminato e quindi a intervalli regolari fino al completamento dell&#39;attività associata. Quando si riceve un promemoria, sull&#39;attività viene visualizzata l&#39;icona del promemoria.

Il processo aziendale determina il comportamento e la tempistica delle scadenze e dei promemoria. Non tutti i processi hanno scadenze e promemoria. L’amministratore specifica se le notifiche e-mail vengono inviate per scadenze e promemoria. Puoi impostare le tue preferenze sulla ricezione o meno di notifiche e-mail.

## Operazioni con le operazioni da code condivise e di gruppo {#working-with-tasks-from-group-and-shared-queues}

Tutte le operazioni assegnate all&#39;utente vengono visualizzate nell&#39;elenco Da fare (coda).

Nel riquadro sinistro della pagina Da fare vengono visualizzati anche tutti i gruppi e gli elenchi di cose da fare condivisi a cui si ha accesso. È possibile completare le attività da qualsiasi elenco attività a cui si ha accesso.

Un elenco attività di gruppo può includere più membri. Un amministratore imposta gli elenchi attività di gruppo in base ai requisiti specifici dell&#39;organizzazione. Gli elenchi Attività di gruppo consentono di distribuire il lavoro tra più persone che condividono responsabilità simili.

Ad esempio, ogni membro del team elabora i moduli di richiesta di prestito. Tutte queste attività vengono inviate a un elenco di cose da fare a cui ogni membro del gruppo ha accesso. Ogni membro del gruppo può accedere alle attività da tale elenco.

Un elenco attività condiviso viene visualizzato quando un altro utente condivide con te il proprio elenco attività o condivide esplicitamente un’attività con te. Puoi quindi visualizzare le attività nell’elenco delle cose da fare di tale utente e completarle per conto di tale utente. Se ad esempio si è in vacanza, è possibile scegliere di condividere l&#39;elenco attività con un collega che completa le attività mentre si è assenti.

>[!NOTE]
>
>È inoltre possibile specificare le impostazioni fuori sede per inoltrare le attività ad altri utenti mentre si è fuori sede.

Per lavorare su un&#39;attività da un gruppo o da un elenco attività condivise, richiedere prima l&#39;attività. Diventi quindi il proprietario dell’attività fino a quando non la completi o la inoltri a un altro utente.

### Condivisione delle code {#sharing-queues}

È possibile condividere l&#39;elenco attività con un altro utente, che potrà quindi visualizzare le nuove attività nell&#39;elenco attività e agire di conseguenza. Se nell&#39;elenco attività sono presenti attività prima della condivisione dell&#39;elenco attività, l&#39;altro utente non può visualizzarle. L&#39;utente può visualizzare e richiedere solo le attività che arrivano nell&#39;elenco attività dopo aver concesso l&#39;accesso all&#39;elenco attività.

Per consentire a un utente di visualizzare un&#39;operazione in una coda condivisa, è necessario che il progettista di processi attivi l&#39;opzione Aggiungi ACL per coda condivisa nella scheda Elenco di controllo di accesso attività (ACL) del servizio utente.

>[!NOTE]
>
>Se si prevede di non essere in ufficio, è inoltre possibile specificare le impostazioni fuori sede per inoltrare le attività ad altri utenti mentre si è assenti anziché condividere l&#39;intero elenco attività.

**Condividere la coda**

1. In **Code** scheda in **Preferenze** , fare clic sull&#39;icona &#39;+&#39; per &#39;Utenti che condividono la coda&#39;.
1. Cerca e seleziona il nome dell’utente.
1. Clic **Condividi** per condividere la coda con l&#39;utente selezionato.
1. Seleziona il nome dell’utente e fai clic su **Condividi**.

   >[!NOTE]
   >
   >Per rimuovere un utente dalla condivisione dell’elenco attività, fai clic su **X** alla fine della riga in cui è elencato l’utente.

### Accesso ad altre code {#accessing-other-queues}

È possibile richiedere l&#39;accesso all&#39;elenco attività di un altro utente per visualizzare e richiedere le nuove attività nell&#39;elenco attività dell&#39;utente.

Quando si richiede l&#39;accesso all&#39;elenco attività di un altro utente, l&#39;utente riceve un&#39;attività nel proprio elenco attività per approvare o rifiutare la richiesta. Dopo che l&#39;utente ha completato l&#39;attività, si riceve una notifica nell&#39;elenco delle cose da fare.

Se si dispone dell&#39;accesso all&#39;elenco attività di un altro utente, non è possibile visualizzare le attività presenti nell&#39;elenco attività dell&#39;utente prima di ottenere l&#39;accesso. È possibile visualizzare solo le attività che arrivano nell&#39;elenco attività dell&#39;utente dopo aver ottenuto l&#39;accesso all&#39;elenco attività.

**Accedere a un&#39;altra coda**

1. In **Preferenze** , apri la scheda **Code** scheda.
1. Fare clic su &#39;+&#39; per selezionare &#39;Code utente a cui si ha accesso&#39;. Cercare il nome dell&#39;utente nella finestra di dialogo a comparsa.
1. Seleziona il nome dell’utente e fai clic su **Richiesta**.

   >[!NOTE]
   >
   >È possibile rimuovere l&#39;accesso a un altro elenco attività selezionando il nome utente dall&#39;elenco Utenti code a cui si ha accesso e facendo clic su **X** alla fine della riga che riporta il nome dell’utente. Non è possibile rimuovere l&#39;accesso a un altro elenco attività quando la richiesta di accesso all&#39;elenco attività è ancora in sospeso.

## Impostazione delle preferenze fuori sede {#setting-out-of-office-preferences}

Se si prevede di uscire dall&#39;ufficio, è possibile specificare l&#39;andamento delle attività assegnate per quel periodo.

È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine per rendere effettive le impostazioni di fuori sede. Se il fuso orario è diverso da quello del server, il fuso orario utilizzato è quello del server.

È possibile impostare una persona predefinita a cui vengono inviate tutte le attività. È inoltre possibile specificare eccezioni per le attività di processi specifici da inviare a un altro utente o da mantenere nell&#39;elenco attività fino a quando non viene restituito. Se anche la persona designata è fuori dall&#39;ufficio, l&#39;operazione viene eseguita dall&#39;utente designato. Se l&#39;attività non può essere assegnata a un utente che non è fuori sede, l&#39;attività rimane nell&#39;elenco attività.

>[!NOTE]
>
>Quando si esce dall&#39;ufficio, le attività precedentemente incluse nell&#39;elenco attività rimangono e non vengono inoltrate ad altri utenti.

### Imposta le preferenze fuori sede {#set-out-of-office-preferences}

1. Clic **Preferenze** e fai clic su **Fuori sede**.
1. Per specificare quando si è fuori sede, effettuare una delle seguenti operazioni:

   * Per specificare che si è fuori sede per un periodo di tempo indeterminato, nel **Sono attualmente** elenco, seleziona **Fuori sede** ma non aggiungere un intervallo di date.
   * Per specificare una data e un&#39;ora di inizio fuori sede e fare clic su &#39;+&#39; per **Pianificazione Fuori sede**. Utilizzare l&#39;elenco calendario e ora per specificare la data e l&#39;ora di inizio. Se non si specifica una data e un&#39;ora di fine, si viene considerati fuori dall&#39;ufficio a tempo indefinito dalla data e dall&#39;ora di inizio fino a quando non si modificano le preferenze.

1. Per specificare la modalità di gestione delle attività per impostazione predefinita, selezionare una di queste opzioni dal **Fuori sede: utente predefinito per le attività Fuori sede** elenco:

   * Seleziona **Non assegnare** per mantenere le attività nell&#39;elenco delle cose da fare fino al ritorno.
   * Seleziona **Trova utente** per cercare un utente a cui assegnare le attività. Quando selezioni un utente, puoi anche visualizzare la pianificazione fuori sede.

1. Per impostare le eccezioni sul valore predefinito, fare clic su + per **Elabora eccezioni**, selezionare il processo per il quale creare un&#39;eccezione e quindi selezionare un altro utente oppure selezionare **Non assegnare** dal **è assegnato a** elenco.

   >[!NOTE]
   >
   >Il progettista del processo può specificare che le attività di alcuni processi siano sempre private e non inoltrate ad altri utenti. Questa impostazione ha la precedenza su tutte le impostazioni effettuate.

1. Al termine, fare clic su **Salva**. Se le impostazioni indicano che al momento non sei in ufficio, le modifiche diventano effettive immediatamente. In caso contrario, hanno effetto alla data e all’ora di inizio specificate. Se si effettua l&#39;accesso mentre si è fuori sede, non si viene considerati in ufficio fino a quando non si modificano le impostazioni.
