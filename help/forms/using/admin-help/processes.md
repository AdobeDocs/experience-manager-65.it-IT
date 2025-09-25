---
title: Gestione dei processi
description: La pagina Elenco processi mostra i processi avviati da un utente o che sono stati avviati automaticamente. Ulteriori informazioni sulla gestione dei processi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 21a2317d-3542-4ccb-98db-3cedf20c89ea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1643'
ht-degree: 100%

---

# Gestione dei processi {#managing-processes}

La pagina Elenco processi mostra i processi avviati da un utente o che sono stati avviati automaticamente.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Forms Workflow. L’elenco dei processi mostra le informazioni seguenti:

   **Nome processo - Versione:** il nome del processo definito in Workbench.

   **Applicazione:** l’applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** se attivo significa che il processo è quello attivato per la versione del processo. Se inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data di creazione:** la data e l’ora in cui il processo è stato implementato.

1. Fai clic sul nome di un processo per visualizzarne le istanze nella pagina Istanza processo.

## Utilizzare le istanze del processo {#working-with-process-instances}

Se accedi alla pagina Istanza processo dalla pagina Elenco processi, vengono elencate tutte le istanze di processo del processo selezionato. Se accedi alla pagina Istanza processo dopo aver eseguito una ricerca, vengono elencate solo le istanze di processo trovate.

Per ogni istanza di processo, l’elenco mostra le seguenti informazioni:

**ID processo:** l’identificatore assegnato da Forms Workflow quando viene creata un’istanza di processo, ovvero quando un utente o un passaggio automatico avvia un processo. Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** il nome del processo definito in Workbench.

**Stato:** indica se l’istanza di processo è in esecuzione normalmente, se sta modificando lo stato o se è stata interrotta. Consulta le Informazioni sugli stati delle istanze di processo.

**Data di creazione:** la data e l’ora di creazione dell’istanza di processo.

**Data di aggiornamento:** la data e l’ora dell’ultima modifica dello stato dell’istanza di processo.

Nella pagina Istanza processo è possibile effettuare le seguenti operazioni:

* Selezionare un’istanza di processo per visualizzarne i dettagli, ad esempio le operazioni e i processi secondari. Quando selezioni un’istanza di processo, viene visualizzata la pagina Dettagli istanza di processo.
* Sospendere, annullare la sospensione o terminare le istanze di processo.
* Cercare un’istanza di processo. Per iniziare una ricerca, fai clic su Ricerca.

### Informazioni sugli stati delle istanze di processo {#about-process-instance-statuses}

Un’istanza di processo, inclusi i processi secondari, può disporre dei seguenti stati:

**COMPLETATO:** tutti i rami e le operazioni nell’istanza di processo sono stati completati. COMPLETATO è lo stato finale di un’istanza di processo.

**IN COMPLETAMENTO:** lo stato dell’istanza del processo sta per essere cambiato in COMPLETATO.

**AVVIATO:** l’istanza di processo è stata creata ma non è ancora in esecuzione. AVVIATO è il primo stato di un’istanza di processo.

**IN ESECUZIONE:** l’istanza di processo è in esecuzione normalmente. È possibile che sia in corso un passaggio automatico oppure che l’istanza di processo riceva l’input dell’utente o sia in attesa dell’interazione dell’utente.

**SOSPESO:** l’istanza di processo è stata sospesa da un amministratore o da un passaggio del processo. Non verranno eseguite ulteriori operazioni finché lo stato non viene modificato.

**IN SOSPENSIONE:** lo stato sta per essere cambiato in SOSPESO. Se un’operazione è stata progettata per ignorare le richieste di sospensione e non è ancora stata completata, è necessario completarla prima che l’istanza di processo venga sospesa.

**TERMINATO:** l’istanza del processo è stata terminata da un amministratore.

**IN TERMINAZIONE:** lo stato sta per essere cambiato in TERMINATO. Se un’operazione è stata progettata per ignorare le richieste terminate e non è ancora stata completata, è necessario completarla prima che l’istanza di processo venga terminata.

**ANNULLAMENTO DELLA SOSPENSIONE:** lo stato sta per essere cambiato in ESECUZIONE dopo essere stato SOSPESO.

>[!NOTE]
>
>Quando viene richiesta la modifica dello stato di un’istanza di processo, ad esempio la sospensione o il termine, la richiesta entra nella coda di comandi per Forms Workflow. A seconda delle dimensioni della coda e della velocità di elaborazione complessiva, lo stato mostrato potrebbe non cambiare fino a quando la pagina non viene ricaricata una o più volte.

### Sospendere o annullare la sospensione delle istanze di processo {#suspend-or-unsuspend-process-instances}

Se è necessario risolvere un problema o sei hai la certezza che un’istanza di processo risconterà un problema in un passaggio successivo a causa di una condizione esterna, è possibile sospenderla temporaneamente.

È possibile sospendere le istanze di processo con stato IN ESECUZIONE.

Dopo aver sospeso un’istanza del processo, lo stato cambia in IN SOSPESO e poi in SOSPESO e il processo si interrompe al momento dell’operazione corrente. L’istanza di processo rimane in questo stato fino a quando lo stato non viene modificato in NON SOSPESO.

Solo le istanze di processo con stato SOSPESO possono essere modificate in NON SOSPESO.

Quando annulli la sospensione di un’istanza di processo, lo stato cambia in ESECUZIONE e continua l’operazione in cui era stata sospesa.

Quando sospendi un’istanza di processo che ha richiamato altri processi (processi secondari) tramite l’operazione di richiamo, anche i processi secondari vengono sospesi.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Forms Workflow.
1. Nella pagina Istanza processo seleziona il processo e fai clic su Sospendi o Annulla sospensione.

### Terminare un’istanza di processo {#terminate-a-process-instances}

Se un’operazione di un’istanza di processo è stata interrotta o si è verificata un&#39;altra condizione di errore, oppure se è necessario forzare l’interruzione dell’esecuzione di un’istanza di processo, è possibile terminare l’istanza di processo.

È possibile terminare le istanze di processo con qualsiasi stato.

Quando si termina un’istanza di processo, lo stato cambia in IN TERMINAZIONE, quindi TERMINATO e il processo si arresta al momento dell’operazione corrente. Non vengono eseguite ulteriori operazioni e tutte le operazioni e le attività associate vengono terminate.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Forms Workflow.
1. Nella pagina Istanza processo seleziona il processo e faI clic su Termina.

## Utilizzo dei dettagli dell’istanza dI processo {#working-with-process-instance-details}

La pagina Dettagli istanza di processo che mostra la cronologia di un’istanza di processo.

Nell’area Riepilogo vengono mostrare le informazioni di base sull’istanza di processo.

Nella scheda Operazioni, ciascuna operazione per l’istanza di processo viene mostrata in ordine di completamento dalla prima all’ultima con le informazioni seguenti:

**Nome dell’operazione:** il nome dell’operazione, definito in Workbench.

**Stato:** indica se l’operazione è in esecuzione o è stata interrotta. Consulta le Informazioni sugli stati delle istanze di processo.

**Nome del ramo:** il nome del ramo, definito in Workbench.

**Data di inizio:** la data e l’ora di inizio dell’operazione.

**Data di completamento:** la data e l’ora in cui è stata completata l’operazione.

Un processo secondario è un’istanza di processo avviata da un altro processo ed eseguita indipendentemente da quest’ultimo. I processi secondari vengono visualizzati solo se sono stati progettati come parte del processo in Workbench. Nella scheda Processi secondari, ciascun processo secondario viene mostrato con le informazioni seguenti:

**ID processo:** questo numero intero positivo assegnato Forms Workflow quando viene creata un’istanza del processo, ovvero quando un utente o un passaggio automatico avvia il processo. Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** il nome del processo definito in Designer.

**Stato:** indica se l’istanza di processo è in esecuzione normalmente, se cambia lo stato o se è stata interrotta. Consulta le Informazioni sugli stati delle istanze di processo.

**Data di creazione:** la data e l’ora di creazione del processo secondario.

**Data di aggiornamento:** la data e l’ora dell’ultima modifica dello stato del processo secondario.

Nella pagina Dettagli istanza processo è possibile effettuare le seguenti operazioni:

* Selezionare un’operazione per visualizzarne i dettagli. Quando selezioni un’operazione, viene visualizzata la pagina Dettagli operazione.
* Selezionare un processo secondario per visualizzare i relativi dettagli. Quando selezioni un processo secondario, viene visualizzata la pagina Dettagli istanza processo.
* Termina o riprova operazioni o processi secondari, a seconda dello stato.

### Informazioni sugli stati delle operazioni {#about-operation-statuses}

Un’operazione (una fase di un processo) può disporre dei seguenti stati:

**COMPLETATO:** l’operazione è stata completata.

**IN ESECUZIONE:** l’operazione viene eseguita normalmente. Potrebbe ricevere l’input o attendere l’interazione dell’utente, oppure potrebbe essere in corso un passaggio automatico.

**BLOCCATO:** si è verificato un problema durante l’elaborazione dell’operazione. Verifica la presenza di errori o eccezioni nella pagina Operazioni bloccate.

**TERMINATO:** l’operazione è stata terminata da un amministratore.

### Terminare le operazioni o i processi secondari {#terminate-operations-or-subprocesses}

Se un’operazione o un processo secondario è bloccato o è stata riscontrata un’altra condizione di errore, oppure se è necessario forzare l’interruzione dell’esecuzione di un’operazione o di un processo secondario, è possibile terminarla.

È possibile terminare un’operazione in ESECUZIONE.

Quando termini un’operazione, lo stato cambia in TERMINATO. L’operazione non viene completata e l’istanza di processo viene interrotta.

È possibile terminare un processo secondario con qualsiasi stato.

Quando termini un processo secondario, lo stato del processo cambia in IN TERMINAZIONE, quindi TERMINATO e l’istanza di processo viene interrotta in corrispondenza delle operazioni correnti. Non vengono eseguite ulteriori operazioni nel processo secondario, anche se l’istanza di processo principale continua a essere eseguita.

Non è possibile terminare i processi che contengono elementi gateway nel diagramma dei processi. Se tenti di terminare questi tipi di processi, le operazioni all’interno degli elementi del gateway non vengono interessate. Per terminare le operazioni che si trovano all’interno di un elemento gateway, è necessario terminarle direttamente.

1. Nella pagina Dettagli istanza processo fai clic sulla scheda Operazioni o sulla scheda Processi secondari.
1. Seleziona l’operazione o il processo secondario e fai clic su Termina.

### Ritentare un’operazione {#retry-an-operation}

È possibile ritentare l’operazione con lo stato BLOCCATO.

Quando ritenti un’operazione, a Forms Workflow viene inviata una richiesta per riavviare l’operazione. Se la richiesta ha esito positivo, lo stato cambia in IN ESECUZIONE. Se non è possibile riavviare l’operazione, questa rimane BLOCCATA e potrebbe essere necessario terminarla.

1. Nella pagina Dettagli istanza processo fai clic sulla scheda Operazioni.
1. Seleziona l’operazione e fai clic su Riprova.

## Utilizzo delle operazioni {#working-with-operations}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Nella pagina Dettagli operazione viene visualizzato un riepilogo di un’operazione in un processo e delle relative assegnazioni utente correnti.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Forms Workflow.
1. Fai clic sul nome di un processo per visualizzarne le istanze di processo. Fai clic su un’istanza di processo per visualizzare la pagina Dettagli istanza di processo, quindi seleziona un’operazione per visualizzare la pagina Dettagli operazione.

   Per ogni attività, l’elenco mostra le seguenti informazioni:

   **Nome processo - Versione:** il nome del processo definito in Workbench.

   **Applicazione:** l’applicazione a cui appartiene il processo in Workbench.

   **Stato:** se attivo, significa che il processo è quello attivato per la versione del processo. Se inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data di creazione:** la data e l’ora in cui il processo è stato implementato.
