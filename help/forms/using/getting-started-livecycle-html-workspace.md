---
title: Guida introduttiva all’area di lavoro di AEM Forms
description: Come iniziare a utilizzare l’area di lavoro LiveCycle di AEM Forms per gestire i processi di automazione aziendale.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Guida introduttiva all’area di lavoro di AEM Forms {#getting-started-with-aem-forms-workspace}

Puoi utilizzare l’area di lavoro di AEM Forms per eseguire le seguenti attività:

* Avviare un processo aziendale
* Visualizzare e intervenire sulle attività assegnate all&#39;utente o ad altri elenchi di cose da fare a cui ha accesso
* Tenere traccia delle attività che fanno parte dei processi avviati o ai quali si è partecipato

## Navigazione nell’area di lavoro di AEM Forms {#navigating-html-workspace}

Nell’interfaccia utente dell’area di lavoro di AEM Forms vengono visualizzati elementi diversi a seconda del processo e dell’attività su cui stai lavorando. È possibile visualizzare o meno le schede Riepilogo, Forms, Dettagli, Cronologia, Allegati o Note oppure tutti i pulsanti descritti nella presente Guida in linea.

Puoi navigare nell’interfaccia utente principale dell’area di lavoro di AEM Forms utilizzando uno dei seguenti metodi:

* Fare clic sugli elementi nella barra di navigazione superiore per accedere all&#39;opzione Avvia processo, Elenco attività, Preferenze, Tracciamento, Guida in linea e Disconnetti.
* Fare clic sulla scheda Avvia processo, Da fare o Tracciamento per accedere alle tre aree di lavoro principali.
* Nelle schede Avvia processo, Da fare e Tracciamento fare clic sugli elementi nell&#39;elenco nel pannello a sinistra per accedere ai preferiti, alle categorie di processo, ai modelli di ricerca, alle bozze o alle attività assegnate. Utilizzare la barra di scorrimento per visualizzare ulteriori elementi nell&#39;elenco.
* Tutti i pulsanti di azione Approva, Rifiuta, Inoltra, Consulta, Blocca e Condividi vengono visualizzati sia nel documento che nella Proprietà.
* Fare clic sull&#39;icona Tutte le opzioni nella barra di navigazione, nella parte inferiore della pagina, per inoltrare l&#39;attività a un altro utente, per condividerla con un altro utente, per consultarla con un altro utente o per bloccare l&#39;attività.
* Nella scheda Cronologia selezionare un task per visualizzare le schede Allegati e Assegnazioni relative a tale task.
* Utilizza il tasto TAB, i tasti freccia e la barra spaziatrice per spostarti all’interno dell’area di lavoro di AEM Forms senza utilizzare il mouse.

## Utilizzo dell’area di lavoro di AEM Forms con gli assistenti vocali {#using-html-workspace-with-screen-readers}

AEM Forms Workspace è un’applicazione HTML basata su web ed è compatibile con gli assistenti vocali. Puoi navigare attraverso l’interfaccia dell’area di lavoro di AEM Forms utilizzando la tastiera.

Per utilizzare l’area di lavoro di AEM Forms con un’utilità per la lettura dello schermo, tieni presente quanto segue:

* AEM Forms Workspace è un’applicazione HTML standard conforme a qualsiasi strumento di lettura dello schermo standard. Non è necessario alcuno script specifico per eseguire uno strumento per la lettura dello schermo.
* Tutta la navigazione nell’area di lavoro di AEM Forms avviene tramite tag di ancoraggio, facilmente accessibili tramite schede.
* Il caricamento di Forms può richiedere alcuni secondi. L’assistente vocale non informa in modo udibile che il modulo è in fase di caricamento e che è necessario attendere.

## Navigazione nell’area di lavoro di AEM Forms tramite tastiera {#navigating-html-workspace-using-a-keyboard}

Quando si accede all’area di lavoro di AEM Forms utilizzando una tastiera, la navigazione è conforme alle convenzioni HTML di accessibilità. In alcune situazioni, l&#39;ordine di tabulazione non segue il tipico ordine convenzionale. I seguenti suggerimenti aiutano a navigare nell’interfaccia:

* In caso di problemi durante l&#39;estrazione dalle barre degli strumenti nella parte superiore del browser, premere Ctrl+Tab per passare al contenuto della finestra del browser.
* La Guida dell’area di lavoro di AEM Forms si apre in una finestra del browser separata. Dopo aver visualizzato la Guida in linea, viene visualizzata nuovamente la finestra del browser che contiene l&#39;area di lavoro di AEM Forms. Il menu Aiuto rimane attivo quando lo stato attivo viene ripristinato.
* Quando si apre un modulo per avviare un processo o completare un&#39;attività, lo stato attivo rimane sull&#39;elemento esistente e non viene modificato nel modulo. Utilizzare TAB per spostare lo stato attivo sul modulo e sfogliarlo. L&#39;ordine di tabulazione nel modulo dipende dal tipo e dalla struttura del modulo.

  Per i PDF forms, quando si passa alla fine del modulo o si invia il modulo, lo stato attivo del cursore si sposta sulla barra degli indirizzi del browser. Passare di nuovo ai menu, ma non all&#39;intero modulo, per passare ai pulsanti delle azioni del modulo, ad esempio Salva come bozza e Completa. Se la maschera è ancora aperta, è anche possibile passare oltre i pulsanti e tornare alla maschera.

## Gestione delle preferenze {#managing-preferences}

Puoi impostare le varie preferenze dell’area di lavoro di AEM Forms nelle seguenti categorie:

**Fuori sede:** Impostare le preferenze per controllare il modo in cui le attività vengono assegnate ad altre persone mentre si è fuori sede. Consulta [Impostazione delle preferenze fuori sede](todo-lists.md#setting-out-of-office-preferences).

**Code:** Impostare le preferenze per la condivisione dell&#39;elenco attività con altri utenti o per la richiesta di accesso all&#39;elenco di un altro utente. Consulta [Operazioni con le operazioni da code condivise e di gruppo](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Impostazioni interfaccia utente:** Imposta le preferenze per la modalità di interazione con l’area di lavoro di AEM Forms. Consulta [Impostare le preferenze dell’interfaccia utente](#set-user-interface-preferences).

### Impostare le preferenze dell’interfaccia utente {#set-user-interface-preferences}

Impostare le preferenze dell&#39;interfaccia utente nella scheda Preferenze > Impostazioni interfaccia utente. Sono disponibili le seguenti preferenze.

* **Posizione iniziale:** Specifica la pagina visualizzata all’accesso all’area di lavoro di AEM Forms. Le quattro opzioni disponibili sono Avvia processo, Da fare, Tracciamento e Preferiti.
* **Richiesta disconnessione:** Specifica se viene richiesto di confermare la disconnessione dopo aver fatto clic su Disconnetti.
* **Formato data:** Specifica il formato di visualizzazione della data utilizzato nell’area di lavoro AEM Forms.
* **Formato ora**: specifica il formato di visualizzazione dell’ora utilizzato nell’area di lavoro di AEM Forms.
* **Notifica eventi attività tramite e-mail:** Specifica se si ricevono notifiche e-mail per eventi di attività, incluse assegnazioni di attività, promemoria e scadenze per le attività nell&#39;elenco attività e negli elenchi attività di gruppo a cui si appartiene.
* **Allega Forms tramite e-mail:** Specifica se una copia del modulo viene allegata ai messaggi di notifica e-mail. Gli allegati sono supportati solo per i moduli PDF e XDP.
* **Salva bozza periodicamente:** Specifica se le bozze dei moduli vengono salvate automaticamente periodicamente o meno. Per salvare le bozze periodicamente, abilita questa opzione e imposta la durata del salvataggio automatico da 1 a 30 minuti. Quando è abilitato il salvataggio automatico e un utente sta lavorando a una bozza, la bozza viene salvata periodicamente dopo il numero di minuti specificato. La bozza viene salvata automaticamente solo se è stata apportata una modifica rispetto all&#39;ultimo salvataggio o salvataggio automatico. Quando la bozza viene salvata, sullo schermo viene visualizzato un messaggio di avviso.
