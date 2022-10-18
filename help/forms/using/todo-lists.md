---
title: Utilizzo degli elenchi A-do
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
source-git-commit: 51e36e874fe84eab8558271b5c84b1c2e2f58ef0
workflow-type: tm+mt
source-wordcount: '4034'
ht-degree: 0%

---

# Utilizzo degli elenchi A-do{#working-with-to-do-lists}

Quando si visualizzano gli elenchi A-do, è possibile che vengano visualizzate le attività di un processo aziendale assegnato all&#39;utente o a qualsiasi gruppo a cui appartiene o che sono le attività condivise di altri utenti. È possibile aprire, lavorare e completare le attività in base alle esigenze, ad esempio approvare o rifiutare una richiesta o aggiungere ulteriori informazioni. Dopo aver completato un&#39;attività, questa viene inviata alla persona successiva nel processo aziendale,

## Informazioni sugli elenchi Da fare {#about-todo-lists}

L’area di lavoro di AEM Forms presenta i tre tipi seguenti di elenchi Da eseguire:

* Singoli elenchi, che contengono attività assegnate direttamente all’utente.
* Elenchi di gruppi, che contengono attività assegnate a un gruppo. Qualsiasi membro del gruppo può aprire e completare le attività. Per aprire un&#39;attività, un membro di un gruppo deve prima reclamare l&#39;attività.
* Elenchi condivisi, che contengono attività assegnate a un utente che ha condiviso il proprio elenco To-do con l&#39;utente e, eventualmente, con altri utenti. Qualsiasi utente che condivide un elenco può richiedere, aprire e completare attività condivise.

È possibile eseguire alcune azioni senza aprire l&#39;attività facendo clic sulle icone visualizzate quando si posiziona il puntatore del mouse su un&#39;attività.

>[!NOTE]
>
>Un’icona esclamativa indica che l’attività ha priorità elevata.

## Attività tipiche {#typical-tasks}

Quando si apre e si lavora su un&#39;attività, gli strumenti disponibili dipendono dall&#39;attività. Per diverse attività è necessario eseguire diverse azioni e, per questo motivo, alcuni strumenti potrebbero non essere disponibili. Di seguito sono descritte le attività tipiche che è possibile ricevere.

**Fornire informazioni**: Viene visualizzata un’attività che richiede la compilazione e l’invio di un modulo.

**Informazioni sulla revisione**: Ricevi un’attività che richiede di rivedere le informazioni e di disconnettersi dal contenuto.

**Recensione multiutente**: Ricevi un’attività contemporaneamente da altri utenti. Tu e gli altri utenti dovete fornire informazioni o rivedere il contenuto, o entrambi. Con questo tipo di attività possono essere disponibili i seguenti strumenti:

* Visualizzazione delle istruzioni per l&#39;attività
* Visualizzazione dello stato di completamento di tutti gli utenti a cui è stata assegnata l’attività
* Visualizzazione dei commenti di tutti gli utenti a cui è stata assegnata l’attività
* Aggiunta di commenti all&#39;attività da solo

Gli strumenti aggiuntivi che possono essere disponibili con una delle attività di cui sopra includono:

* Inoltra
* Condividi
* Consulta
* Ritorno
* Note
* Allegati

## Apertura delle attività {#opening-tasks}

È possibile aprire e bloccare le attività dall&#39;elenco To-do o reclamare e aprire le attività da un gruppo o dall&#39;elenco To-do condiviso. Quando si apre un&#39;attività, questa viene visualizzata nel riquadro principale. Le altre attività vengono visualizzate nell&#39;elenco delle attività accanto all&#39;elenco A.

Se esiste un URL di riepilogo attività, viene visualizzata la visualizzazione Riepilogo attività per impostazione predefinita, anziché il modulo associato a un&#39;attività. Anche quando un utente abilita l’opzione &quot;Apri il modulo in modalità ingrandita&quot; in Assegna attività, il modulo non si apre in modalità ingrandita.

>[!NOTE]
>
>Quando si apre un&#39;attività, a seconda delle impostazioni predefinite dell&#39;attività, il modulo associato potrebbe essere visualizzato in visualizzazione completa.

### Aprire e bloccare un&#39;attività dall&#39;elenco {#open-and-lock-a-task-from-your-list}

Quando si apre un&#39;attività dall&#39;elenco A, se l&#39;elenco è condiviso, è possibile bloccare l&#39;attività per impedire a un altro utente che ha accesso all&#39;elenco di lavorare sull&#39;attività.

1. Nella pagina Da fare, nel riquadro a sinistra, selezionare l&#39;elenco dei singoli Da fare. Tutte le attività vengono visualizzate nel riquadro centrale.

   >[!NOTE]
   >
   >È possibile filtrare le attività selezionando il tipo di processo all&#39;interno dell&#39;elenco A. È possibile selezionare l&#39;elenco Da fare per visualizzare di nuovo tutte le attività nell&#39;elenco Da fare.

1. Se necessario, bloccare l&#39;attività. Per bloccare un&#39;attività, fare clic sull&#39;icona Tutte le opzioni dell&#39;attività e selezionare Blocca. Posiziona il puntatore sull’attività per rendere disponibile l’opzione.

   >[!NOTE]
   >
   >È inoltre possibile bloccare o sbloccare un&#39;attività in qualsiasi scheda quando l&#39;attività è aperta.

   ![lock_task](assets/lock_task.png)

   Menu Tutte le opzioni di un&#39;attività

1. Apri l’attività facendo clic su di essa.

### Aprire e richiedere un&#39;attività da un elenco condiviso o di gruppi {#open-and-claim-a-task-from-a-shared-or-group-list}

Quando si apre e si dichiara un&#39;attività da un gruppo o da un elenco condiviso, l&#39;attività viene spostata dal gruppo o dall&#39;elenco condiviso nel proprio elenco di attività individuale. Ad altri utenti con accesso all’elenco non è consentito lavorare sull’attività.

1. Nella pagina Da fare, nel riquadro a sinistra selezionare un gruppo o un elenco Da fare condiviso. Tutte le attività vengono visualizzate nel riquadro centrale.
1. Esegui uno dei seguenti passaggi:

   * Per richiedere un&#39;attività, senza aprirla, da un gruppo o da un elenco di attività condivise, fare clic su  **Richiesta** passando il puntatore sull&#39;attività. In alternativa, quando l&#39;attività è aperta, il pulsante Attestazione è disponibile nella barra delle azioni sotto il riquadro attività. Al momento della richiesta, un&#39;attività si sposta dal gruppo o dall&#39;elenco Condivisi To-do all&#39;elenco.
   * Per richiedere e aprire un&#39;attività da un gruppo o da un elenco Condiviso fare, fare clic su **Rivendicazione e apertura**.

## Utilizzo delle attività {#working-with-tasks}

Dopo aver aperto un&#39;attività, le schede visualizzate nel riquadro principale e gli strumenti disponibili dipendono dall&#39;attività. Le schede che potresti vedere sono descritte di seguito:

**Riepilogo attività**: Quando si apre un&#39;attività, il riquadro Riepilogo attività consente di visualizzare informazioni sull&#39;attività, se esistente, utilizzando un URL specificato nel processo al passaggio Assegna attività. È possibile visualizzare informazioni aggiuntive e rilevanti relative a un&#39;attività utilizzando il riquadro di riepilogo attività per aggiungere ulteriori valori all&#39;utente finale dell&#39;area di lavoro di AEM Forms. Questa scheda non è disponibile, se l’URL di riepilogo attività non esiste.

**Dettagli**: Fornisce alcune informazioni sull&#39;attività corrente e sul processo a cui appartiene.

**Modulo**: Visualizza il modulo associato all’attività. Il modulo può essere di molti tipi di file, inclusi file PDF, HTML, Guide e SWF. Per raccogliere informazioni, il modulo può avere l’aspetto di un modulo normale stampabile o basato su Web oppure può essere utilizzato come guida attraverso una serie di pannelli in stile guidato.

**Cronologia**: Elenca le attività che fanno parte dell&#39;istanza di processo e il modulo associato, le assegnazioni delle attività e gli allegati per ogni attività.

**Allegati**: Visualizza gli allegati esistenti associati all&#39;attività e, se necessario, aggiunge gli allegati.

**Note**: Visualizza le note esistenti associate all&#39;attività e, se necessario, aggiunge note.

Quando si lavora a un&#39;attività, di seguito sono descritti gli strumenti che è possibile visualizzare e le azioni che è possibile eseguire.

### Inoltrare, condividere o consultare un&#39;attività {#forward-share-or-consult-on-a-task}

È possibile inoltrare un&#39;attività insieme a note o allegati a un altro utente o condividere l&#39;attività o consultare l&#39;attività con un altro utente. Se si modificano i dati del modulo associati a un&#39;attività, salvare il modulo come bozza prima di inoltrare, condividere o consultare l&#39;attività. In caso contrario, l’attività viene inviata senza il modulo aggiornato. Dopo aver inoltrato e condiviso un&#39;attività, l&#39;utente che riceve l&#39;attività può reclamarla e completarla o restituirla. Se si consulta un’attività, l’utente può solo restituirla.

1. Se si modifica un modulo associato a un&#39;attività che si desidera mantenere, fare clic su **Salva**. L’opzione Salva è disponibile nella barra delle azioni nella parte inferiore di ciascuna scheda. In caso contrario, l’attività viene inviata senza il modulo aggiornato.

   >[!NOTE]
   >
   >Il pulsante Salva non è disponibile per alcuni moduli, a seconda dell’attività su cui si sta lavorando.

1. In una scheda, fare clic su uno dei pulsanti seguenti:

   * **Inoltra**
   * **Condividi**
   * **Consulta**

   >[!NOTE]
   >
   >A seconda dell&#39;attività, è anche possibile eseguire queste azioni dall&#39;elenco A-do senza aprire l&#39;attività.

1. Nella finestra di dialogo a comparsa, cerca e seleziona il nome dell&#39;utente con cui inoltrare, condividere o consultare l&#39;attività.

### Restituire un’attività {#return-a-task}

1. In qualsiasi scheda, fai clic su **Ritorno**. L&#39;attività viene restituita all&#39;elenco A-do dell&#39;utente che in precedenza ha inoltrato l&#39;attività all&#39;utente oppure ha condiviso o consultato l&#39;attività.

### Esegui attività offline {#take-a-task-offline}

Può essere consentito lavorare su un&#39;attività offline e successivamente inviare il relativo modulo da Adobe® Reader® o Adobe® Acrobat® Professional o Adobe® Acrobat® Standard. Quando il modulo viene inviato, il client e-mail viene avviato con l’indirizzo e-mail del server appropriato. È quindi possibile inviare il modulo completato al server tramite e-mail.

1. In qualsiasi scheda, fai clic su **Offline**.
1. Specificare un nome file in cui salvare il modulo e fare clic su **Salva**. Il modulo associato all’attività viene salvato localmente e l’attività rimane nell’elenco A fino all’invio del modulo.

### Utilizzare gli allegati {#work-with-attachments}

È possibile aggiungere, aggiornare, eliminare o salvare localmente gli allegati.

**Aggiungere un allegato**

1. In **Allegati** scheda , fai clic su **Sfoglia** per selezionare il file da allegare.
1. Seleziona la **Autorizzazioni** livello dell&#39;allegato per gli altri utenti che partecipano al processo. Se si seleziona **Leggi**, altri utenti possono salvare il file localmente. Se selezioni una delle autorizzazioni di modifica, altri utenti possono caricare anche un nuovo file per sostituire l&#39;allegato.

   >[!NOTE]
   >
   >È inoltre possibile aggiungere commenti insieme agli allegati.

1. Fai clic su **Carica**. Il file viene allegato al modulo.

**Visualizzare un allegato**

1. Sulla **Allegati** fare clic sul nome del file dell&#39;allegato da visualizzare.

**Salvare un allegato localmente**

1. Fare clic su un allegato per aprirlo. Salvare localmente l&#39;allegato aperto.

**Aggiornare un allegato**

1. Fai clic su **Modifica** per l&#39;allegato. Selezionare il file con cui sostituire l&#39;allegato esistente facendo clic su **Sfoglia**.

**Eliminare un allegato**

1. Fai clic su **Elimina** per un allegato.

### Salvare il lavoro senza completare l’attività {#save-your-work-without-completing-the-task}

1. Su qualsiasi scheda, tocca **Salva**.

   Viene visualizzata la finestra di dialogo Salva come bozza. Il nome predefinito della bozza è il nome dell&#39;attività del modello di attività.

   ![finestra di dialogo saveasredper](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >Puoi configurare l’area di lavoro in modo da salvare periodicamente automaticamente le informazioni immesse da un utente come bozza. Se il salvataggio automatico è abilitato e un utente sta lavorando a una bozza, la bozza viene salvata periodicamente. In caso di salvataggio automatico, il nome predefinito dell&#39;attività viene assunto automaticamente.
   >
   >
   >Per ulteriori informazioni, consulta Salva bozza periodicamente in [Gestione delle preferenze](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. Nella finestra di dialogo Salva come bozza , specifica un nome univoco per l’attività e tocca **OK**.

   ![nome_dialogo saveasrednome](assets/saveasdraftdialog_name.png)

   La bozza viene salvata con il nome specificato. L’attività rimane nell’elenco A e tutte le modifiche apportate al modulo vengono salvate nella cartella Bozze. Inoltre, nell&#39;elenco Da fare è possibile cercare la bozza utilizzando il nome della bozza per riprendere a lavorare su di essa.

   ![ricerca](assets/searchfortask.png)

## Completamento delle attività {#completing-tasks}

La modalità di completamento di un&#39;attività dipende dall&#39;attività stessa e dal ruolo svolto nel processo. È possibile che ti venga chiesto di approvare o negare una richiesta, fornire contenuto, rivedere e verificare le informazioni o indicare che hai agito.

Puoi completare un’attività in vari modi:

* Utilizzo delle azioni disponibili in una qualsiasi delle schede
* Utilizzo delle azioni integrate nel modulo stesso
* Dall&#39;elenco A-do, senza aprire l&#39;attività

>[!NOTE]
>
>Questa opzione è disponibile se `isMustOpenToComplete` campo non selezionato nel `Assign Task` in Workbench, durante la progettazione di un processo.

* Per e-mail, se ricevi notifiche e-mail

Quando si completa un&#39;attività, a seconda dell&#39;attività, potrebbe apparire una finestra di dialogo di conferma che riafferma l&#39;azione. Ad esempio, potrebbe essere visualizzata una finestra di dialogo che richiede di attestare la validità delle informazioni fornite.

>[!NOTE]
>
>Se un’attività è stata modificata ma non è ancora pronta per essere completata, è possibile salvarla come bozza facendo clic su Salva e tornare ad essa in un secondo momento.

### Completa un’attività {#complete-a-task}

1. Esegui uno dei seguenti passaggi:

   * Seleziona l’attività e fai clic sul pulsante appropriato per il passaggio successivo richiesto nel processo in fondo all’elenco.
   * Se il modulo non dispone di pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms è disponibile, fai clic su **Completa**.
   * Se il modulo contiene pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms non è disponibile, fare clic sul pulsante appropriato del modulo per il passaggio successivo richiesto nel processo.

   Se il modulo non dispone di pulsanti e il pulsante Completa nell’area di lavoro di AEM Forms non è disponibile, viene visualizzato un messaggio che indica che non è possibile inviare il modulo.

1. Se viene visualizzata una finestra di dialogo di conferma, effettuare una delle seguenti operazioni:

   * Fai clic su **OK** se hai completato l’attività e sei pronto per disconnetterla.
   * Fai clic su **Annulla** se desideri tornare all&#39;attività e non sei pronto per disconnetterti.

>[!NOTE]
>
>È possibile visualizzare un pulsante Invia all’interno dei moduli di HTML quando si utilizzano in un modulo le proprietà del processo. Questo pulsante non è visibile quando viene eseguito il rendering dello stesso modulo di PDF. Per completare un’attività, fare clic sul pulsante Invia disponibile nella parte inferiore dell’area di lavoro di AEM Forms, all’esterno del modulo e non sul pulsante Invia all’interno del modulo.

### Attività di approvazione in blocco {#bulk-approve-tasks}

È possibile inviare più attività dall&#39;elenco A fare. È possibile inviare insieme solo i task dello stesso processo, con gli stessi nomi di task e le stesse opzioni di route.

>[!NOTE]
>
>Questa opzione è disponibile se il campo isMustOpenToComplete non è selezionato nel passaggio Assegna attività in Workbench durante la progettazione di un processo.

1. Nella pagina Da fare, nel riquadro a sinistra, selezionare l&#39;elenco dei singoli Da fare. Tutte le attività vengono visualizzate nel riquadro centrale.
1. Seleziona **Attiva modalità in blocco**. Le caselle di controllo vengono visualizzate davanti alle attività dell&#39;elenco.

   >[!NOTE]
   >
   >Questa opzione non è disponibile per le attività per le quali il campo isMustOpenToComplete è selezionato nel passaggio Assegna attività in Workbench durante la progettazione di un processo. Le caselle di controllo di tali attività nell&#39;elenco TO-DO rimangono sempre disabilitate.

1. Selezionare le attività per l&#39;approvazione in blocco. È possibile selezionare più attività dello stesso processo, con gli stessi nomi di task e le stesse opzioni di route. Dopo aver selezionato un&#39;attività per l&#39;approvazione, rimangono abilitate solo le attività con lo stesso processo, con gli stessi nomi di attività e le stesse opzioni di route. Gli altri sono disabilitati.

   ![1_approvazione](assets/1_bulkapproval.png)

1. Fare clic sull’opzione Invia disponibile. Le attività selezionate vengono inviate.

   ![omologazione](assets/bulkapproval.png)

## Partecipazione alle attività tramite e-mail {#participating-in-tasks-through-email}

Puoi ricevere e completare le attività tramite e-mail. Partecipare alle attività tramite e-mail elimina la necessità di controllare regolarmente l&#39;elenco A-do per le nuove attività o controllare la pagina Tracking per verificare lo stato di un&#39;attività.

Innanzitutto, imposta le preferenze dell’area di lavoro di AEM Forms per ricevere le notifiche e-mail. L’area di lavoro di AEM Forms può inviare notifiche e-mail per attività nell’elenco A-do o in qualsiasi elenco A-do del gruppo a cui appartieni. L’amministratore determina quando i messaggi di notifica e-mail vengono inviati e chi li riceve.

I messaggi e-mail possono contenere un collegamento che apre l’attività nell’area di lavoro di AEM Forms, un allegato del modulo utilizzato per l’attività o azioni per completare l’attività tramite e-mail. Se un modulo è incluso nel messaggio e-mail, è possibile aprire il modulo e completare l’attività se nel modulo sono presenti i pulsanti per completare l’attività. Se le azioni per completare l’attività sono incluse nel messaggio e-mail, puoi completare l’attività facendo clic sulle azioni contenute nell’e-mail o rispondendo all’e-mail con l’azione digitata come prima riga nel corpo dell’e-mail.

>[!NOTE]
>
>* Per configurare l’area di lavoro in modo che utilizzi i modelli e-mail appropriati, consulta la sezione [Guida per l’amministratore JEE di AEM Forms](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/).
>
>* Se le bozze vengono inoltrate dopo l’invio dell’attività nell’area di lavoro di AEM Forms, vengono inviate notifiche e-mail. Se le bozze vengono inoltrate dal punto iniziale dell’area di lavoro di AEM Forms, non vengono inviate notifiche e-mail.


Quando si completa un&#39;attività tramite e-mail, l&#39;attività viene rimossa dall&#39;elenco A-do nell&#39;area di lavoro di AEM Forms.

>[!NOTE]
>
>Se l&#39;utente non ha effettuato l&#39;accesso all&#39;area di lavoro AEM Forms nel browser e apre un collegamento a un&#39;attività Da fare, il collegamento diretto A non si apre e visualizza un&#39;eccezione. Accedi all’area di lavoro di AEM Forms prima di fare clic sui collegamenti nelle e-mail.

>[!NOTE]
>
>Non è possibile inoltrare una notifica e-mail per assegnare un’attività a un altro utente. Puoi inoltrare attività solo ad altri utenti dall’area di lavoro di AEM Forms.

### Ricevi messaggi di notifica e-mail {#receive-email-notification-messages}

1. Fai clic su **Preferenze**.
1. In **Notifica eventi attività tramite e-mail** elenco, selezionare **Sì**.
1. Per includere il modulo e i dati con il messaggio e-mail, nella **Allega Forms in e-mail** elenco, selezionare **Sì**.

## Partecipazione a attività tramite dispositivi mobili {#participating-in-tasks-through-mobile-devices}

Puoi utilizzare l’app Workspace di AEM Forms per partecipare alle attività dal tuo dispositivo mobile. Prima di installare l’applicazione, rivolgiti all’amministratore di sistema per assicurarti che l’organizzazione supporti l’utilizzo dell’app Workspace di AEM Forms.

## Informazioni su scadenze e promemoria {#about-deadlines-and-reminders}

A *scadenza* determina la data e l’ora in cui è necessario completare un’attività. Quando una scadenza viene superata, il server indirizza l&#39;attività al passaggio successivo del processo (che può essere l&#39;elenco To-do di un altro utente) e quindi sull&#39;attività viene visualizzata l&#39;icona della scadenza. L’icona della scadenza viene visualizzata indipendentemente dalle regole associate al processo.

A *promemoria* notifica un&#39;attività che richiede attenzione. I promemoria si verificano in un momento predeterminato e quindi a intervalli regolari fino a quando non si completa l&#39;attività associata. Quando ricevi un promemoria, sull’attività viene visualizzata l’icona del promemoria.

Il processo aziendale determina il comportamento e la tempistica di scadenze e promemoria. Non tutti i processi hanno scadenze e promemoria. L’amministratore specifica se le notifiche e-mail vengono inviate per scadenze e promemoria. Puoi impostare le tue preferenze se ricevere notifiche e-mail.

## Utilizzo delle attività dalle code di gruppo e condivise {#working-with-tasks-from-group-and-shared-queues}

Tutte le attività assegnate all&#39;utente vengono visualizzate nell&#39;elenco Da fare (coda).

Nella pagina Da fare vengono visualizzati nel riquadro a sinistra anche gli elenchi dei gruppi e delle operazioni condivise a cui si ha accesso. È possibile completare le attività da qualsiasi elenco A-do a cui si ha accesso.

Un elenco di operazioni di gruppo può avere più di un membro. Un amministratore imposta gli elenchi di attività del gruppo in base ai requisiti specifici dell&#39;organizzazione. Gli elenchi di attività di gruppo forniscono un modo per distribuire il lavoro tra diverse persone che condividono responsabilità simili.

Ad esempio, ogni membro del team elabora i moduli di richiesta di prestito. Tutte queste attività vengono inviate a un elenco di attività del gruppo a cui ogni membro del gruppo ha accesso. Ogni membro del gruppo può accedere alle attività dall&#39;elenco A-do.

Un elenco di cose da fare condivise viene visualizzato quando un altro utente condivide con te il proprio elenco di cose da fare o condivide esplicitamente con te un&#39;attività. È quindi possibile visualizzare le attività nell’elenco Da fare dell’utente e completarle per conto di quest’ultimo. Ad esempio, se ti trovi in vacanza, puoi scegliere di condividere la tua lista di cose da fare con un collega che completa le tue attività mentre sei via.

>[!NOTE]
>
>È inoltre possibile specificare le impostazioni fuori sede per inoltrare le attività ad altri utenti mentre si è fuori sede.

Per lavorare su un&#39;attività da un gruppo o da un elenco Condivisi A, registrare prima l&#39;attività. Diventa quindi proprietario dell’attività fino a quando non la completa o la inoltra a un altro utente.

### Condivisione delle code {#sharing-queues}

È possibile condividere l&#39;elenco To-do con un altro utente, che può quindi visualizzare le nuove attività nell&#39;elenco To-do e agire su di esse per conto proprio. Se nell&#39;elenco Da eseguire sono presenti attività prima di condividere l&#39;elenco Da fare, l&#39;altro utente non può visualizzarle. L&#39;utente può visualizzare e richiedere solo le attività che arrivano nell&#39;elenco Da fare dopo aver concesso l&#39;accesso all&#39;elenco Da fare.

Tieni presente che per consentire a un utente di visualizzare un&#39;attività in una coda condivisa, il designer del processo deve abilitare l&#39;opzione Aggiungi ACL per coda condivisa nella scheda Elenco controllo accesso attività (ACL) del servizio utente.

>[!NOTE]
>
>Se si prevede di essere lontani dall&#39;ufficio, è anche possibile specificare le impostazioni fuori sede per inoltrare le attività ad altri utenti mentre si è in viaggio, invece di condividere l&#39;intero elenco cose da fare.

**Condividere la coda**

1. In **Code** nella scheda **Preferenze** , fai clic sull’icona &quot;+&quot; per &quot;Utenti che condividono la mia coda&quot;.
1. Cerca e seleziona il nome dell’utente.
1. Fai clic su **Condividi** per condividere la coda con l&#39;utente selezionato.
1. Seleziona il nome dell’utente e fai clic su **Condividi**.

   >[!NOTE]
   >
   >È possibile rimuovere un utente dalla condivisione dell&#39;elenco Da fare facendo clic su **X** alla fine della riga in cui è elencato l’utente.

### Accesso ad altre code {#accessing-other-queues}

È possibile richiedere l’accesso all’elenco To-do di un altro utente per visualizzare e richiedere eventuali nuove attività nell’elenco To-do dell’utente.

Quando si richiede l&#39;accesso all&#39;elenco To-do di un altro utente, l&#39;utente riceve un&#39;attività nel proprio elenco To-do per approvare o negare la richiesta. Una volta completata l&#39;attività, l&#39;utente riceverà una notifica nell&#39;elenco A-do.

Se si dispone dell&#39;accesso all&#39;elenco To-do di un altro utente, non è possibile visualizzare le attività presenti nell&#39;elenco To-do dell&#39;utente prima che sia stato concesso l&#39;accesso. È possibile visualizzare solo le attività che arrivano nell’elenco A-do dell’utente dopo aver ottenuto l’accesso all’elenco A-do.

**Accedere a un&#39;altra coda**

1. In **Preferenze** apri la scheda **Code** scheda .
1. Fai clic su &quot;+&quot; per le &quot;code utente a cui ho accesso&quot;. Cerca il nome dell’utente nella finestra di dialogo a comparsa.
1. Seleziona il nome dell’utente e fai clic su **Richiesta**.

   >[!NOTE]
   >
   >È possibile rimuovere l&#39;accesso a un altro elenco Da fare selezionando il nome utente dall&#39;elenco Code utenti a cui ho accesso e facendo clic su **X** alla fine della riga in cui viene indicato il nome dell&#39;utente. Non è possibile rimuovere l&#39;accesso a un altro elenco To-do quando la richiesta di accesso all&#39;elenco To-do è ancora in sospeso.

## Impostazione delle preferenze fuori sede {#setting-out-of-office-preferences}

Se si prevede di uscire dall&#39;ufficio, è possibile specificare cosa accade alle attività assegnate per quel periodo.

Puoi specificare una data e un’ora di inizio e una data e un’ora di fine per rendere effettive le impostazioni fuori sede. Se il fuso orario è diverso dal server, viene utilizzato quello del server.

È possibile impostare una persona predefinita a cui vengono inviate tutte le attività. È inoltre possibile specificare le eccezioni per le attività di processi specifici da inviare a un utente diverso o da rimanere nell&#39;elenco Da fare fino a quando non si ritorna. Se la persona designata è anche fuori dall&#39;ufficio, l&#39;attività va all&#39;utente che ha designato. Se l&#39;attività non può essere assegnata a un utente che non è fuori ufficio, l&#39;attività rimane nell&#39;elenco A-do.

>[!NOTE]
>
>Quando non sei in ufficio, tutte le attività precedentemente incluse nell&#39;elenco To-do rimangono lì e non vengono inoltrate ad altri utenti.

### Impostare le preferenze fuori sede {#set-out-of-office-preferences}

1. Fai clic su **Preferenze** e fai clic su **Fuori sede**.
1. Per specificare quando si è fuori ufficio, eseguire una delle operazioni seguenti:

   * Per specificare di essere fuori ufficio ora per un periodo di tempo indefinito, nella **Attualmente** elenco, selezionare **Fuori sede** ma non aggiungere un intervallo di date.
   * Per specificare una data e un&#39;ora di inizio fuori sede e fare clic su &#39;+&#39; per **Pianificazione fuori sede**. Utilizzare l’elenco calendario e ora per specificare la data e l’ora di inizio. Se non si specifica una data e un&#39;ora di fine, si viene considerati fuori ufficio a tempo indefinito dalla data e dall&#39;ora di inizio fino a quando non si modificano le preferenze.

1. Per specificare come le attività devono essere gestite per impostazione predefinita, selezionare una delle opzioni seguenti nella **Quando fuori dall&#39;ufficio: Utente predefinito per le attività fuori sede** elenco:

   * Seleziona **Non assegnare** per mantenere le attività nell&#39;elenco Da fare fino a quando non si ritorna.
   * Seleziona **Trova utente** per cercare un utente a cui assegnare le attività. Quando selezioni un utente, puoi anche visualizzarne la pianificazione fuori sede.

1. Per impostare le eccezioni al valore predefinito, fare clic su + per **Eccezioni al processo**, seleziona il processo per cui creare un&#39;eccezione, quindi seleziona un utente diverso o seleziona **Non assegnare** dal **è assegnato a** elenco.

   >[!NOTE]
   >
   >Il progettista del processo può specificare che le attività di alcuni processi vengono sempre mantenute private e non inoltrate ad altri utenti. Questa impostazione sostituisce tutte le impostazioni effettuate.

1. Al termine dell&#39;impostazione delle preferenze, fai clic su **Salva**. Se le impostazioni indicano che al momento non sei in ufficio, le modifiche avranno effetto immediatamente. In caso contrario, hanno effetto alla data e all&#39;ora di inizio specificate. Se effettui l&#39;accesso quando sei fuori ufficio, non sei considerato in ufficio fino a quando non cambi le impostazioni.
