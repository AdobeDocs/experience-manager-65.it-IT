---
title: Gestione dei processi
seo-title: Gestione dei processi
description: La pagina Elenco processi mostra i processi avviati da un utente o avviati automaticamente. Ulteriori informazioni sulla gestione dei processi.
seo-description: La pagina Elenco processi mostra i processi avviati da un utente o avviati automaticamente. Ulteriori informazioni sulla gestione dei processi.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---


# Gestione dei processi {#managing-processes}

La pagina Elenco processi mostra i processi avviati da un utente o avviati automaticamente.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms. L&#39;elenco dei processi contiene le informazioni seguenti:

   **Nome processo - Versione:** nome del processo, come definito in Workbench.

   **Applicazione:** l&#39;applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo indica che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data creazione:** la data e l&#39;ora in cui il processo è stato distribuito.

1. Fate clic sul nome di un processo per visualizzarne le istanze nella pagina Istanza processo.

## Utilizzo delle istanze di processo {#working-with-process-instances}

Se si accede alla pagina Istanza processo dalla pagina Elenco processi, vengono elencate tutte le istanze del processo selezionate. Se accedete alla pagina Istanza di processo dopo aver eseguito una ricerca, vengono elencate solo le istanze di processo trovate.

Per ogni istanza di processo, l&#39;elenco mostra le informazioni seguenti:

**ID processo:** identificatore assegnato dal flusso di lavoro del modulo quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatico avvia un processo). Potete utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** nome del processo, come definito in Workbench.

**Stato:** indica se l&#39;istanza di processo è in esecuzione normalmente, cambia stato o è stata arrestata. (Vedere Informazioni sugli stati delle istanze di processo.)

**Data creazione:** la data e l&#39;ora in cui è stata creata l&#39;istanza del processo.

**Data aggiornamento:** la data e l&#39;ora dell&#39;ultima modifica dello stato dell&#39;istanza del processo.

Nella pagina Istanza processo è possibile effettuare le seguenti operazioni:

* Selezionate un’istanza di processo per visualizzarne i dettagli, ad esempio le operazioni e i sottoprocessi. Quando si seleziona un&#39;istanza di processo, viene visualizzata la pagina Dettagli istanza processo.
* Sospendere, annullare la sospensione o terminare le istanze del processo.
* Cercare un’istanza di processo. Per iniziare una ricerca, fate clic su Cerca.

### Informazioni sugli stati dell&#39;istanza di processo {#about-process-instance-statuses}

Un&#39;istanza di processo, compresi i sottoprocessi, può presentare i seguenti stati:

**COMPLETE:** tutti i rami e le operazioni nell&#39;istanza di processo sono stati completati. COMPLETE è lo stato finale di un’istanza di processo.

**COMPLETAMENTO:** Lo stato dell&#39;istanza di processo sta per essere COMPLETATO.

**AVITIATED:** L&#39;istanza di processo è stata creata ma non è ancora in esecuzione. AVITIATED è il primo stato di un’istanza di processo.

**ESECUZIONE:** L&#39;istanza di processo viene eseguita normalmente. Potrebbe essere in corso un passaggio automatico, oppure l&#39;istanza di processo potrebbe ricevere l&#39;input dell&#39;utente o attendere l&#39;interazione dell&#39;utente.

**SOSPESO:** L&#39;istanza di processo è stata sospesa da un amministratore o da un passaggio del processo. Non si verificheranno altre operazioni finché lo stato non viene modificato.

**SOSPENSIONE:** lo stato sta per cambiare in SOSPESO. Se un&#39;operazione è stata progettata per ignorare le richieste di sospensione e non è ancora stata completata, l&#39;operazione deve essere completata prima che l&#39;istanza di processo sia sospesa.

**TERMINATO:** L&#39;istanza di processo è stata terminata da un amministratore.

**TERMINAZIONE:** Lo stato sta per essere modificato in TERMINATO. Se un&#39;operazione è stata progettata per ignorare le richieste di interruzione e non è ancora stata completata, l&#39;operazione deve essere completata prima che l&#39;istanza del processo venga terminata.

**UNSOSPENDENTE:** lo stato sta per cambiare in ESECUZIONE dopo essere stato SOSPESO.

>[!NOTE]
>
>Quando viene eseguita una richiesta per modificare lo stato di un&#39;istanza di processo (ad esempio per sospendere o terminare), la richiesta entra nella coda di comando del flusso di lavoro dei moduli. A seconda delle dimensioni della coda e della velocità di elaborazione complessiva, lo stato visualizzato potrebbe non cambiare finché la pagina non viene ricaricata una o più volte.

### Sospendere o annullare la sospensione delle istanze del processo {#suspend-or-unsuspend-process-instances}

Se è necessario risolvere un problema o se si è a conoscenza del fatto che un&#39;istanza di processo si troverà in un secondo momento in presenza di un problema a causa di una condizione esterna, è possibile sospendere temporaneamente l&#39;istanza di processo.

È possibile sospendere le istanze del processo con stato RUNNING.

Dopo aver sospeso un&#39;istanza di processo, il suo stato cambia in SOSPENSIONE, SOSPESO e il processo viene messo in pausa durante l&#39;operazione corrente. L&#39;istanza di processo rimane nello stato finché non viene cambiato in NON SOSPESO.

Solo le istanze di processo con stato SOSPESO possono essere modificate in NON SOSPESO.

Quando si annulla la sospensione di un&#39;istanza di processo, il suo stato cambia in ESECUZIONE e continua con l&#39;operazione in cui era stata sospesa.

Quando si sospende un&#39;istanza di processo che ha richiamato altri processi (processi secondari) utilizzando l&#39;operazione di richiamo, anche i processi secondari vengono sospesi.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza di processo, selezionate il processo e fate clic su Sospendi o Annulla sospensione.

### Terminare le istanze di processo {#terminate-a-process-instances}

Se un&#39;operazione di un&#39;istanza di processo è stata bloccata o ha rilevato un&#39;altra condizione di errore, oppure se è necessario forzare un&#39;istanza di processo a interrompere l&#39;esecuzione, è possibile terminare l&#39;istanza di processo.

È possibile terminare le istanze del processo con qualsiasi stato.

Quando si interrompe un&#39;istanza di processo, il suo stato cambia in TERMINAZIONE, TERMINATA, e il processo si arresta al suo funzionamento corrente. Non vengono eseguite altre operazioni e tutte le operazioni e le attività associate vengono terminate.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza processo, selezionate il processo e fate clic su Termina.

## Utilizzo dei dettagli dell&#39;istanza di processo {#working-with-process-instance-details}

La pagina Dettagli istanza processo mostra la cronologia di un’istanza di processo.

L&#39;area Riepilogo mostra informazioni di base sull&#39;istanza di processo.

Nella scheda Operazioni, ogni operazione per l&#39;istanza di processo viene visualizzata in ordine di completamento dal primo all&#39;ultimo con le seguenti informazioni:

**Nome operazione:** il nome dell&#39;operazione, come definito in Workbench.

**Stato:** indica se l&#39;operazione è in esecuzione normale o se è stata arrestata. (Vedere Informazioni sugli stati delle istanze di processo.)

**Nome ramo:** il nome del ramo, come definito in Workbench.

**Data inizio:** la data e l&#39;ora di inizio dell&#39;operazione.

**Data completamento:** la data e l&#39;ora in cui è stata completata l&#39;operazione.

Un sottoprocesso è un&#39;istanza di processo avviata da un altro processo ed eseguita indipendentemente da tale altro processo. I processi secondari vengono visualizzati solo se sono stati progettati come parte del processo in Workbench. Nella scheda Sottomoduli, ogni sottoprocesso viene visualizzato con le informazioni seguenti:

**ID processo:** questo numero intero positivo che il flusso di lavoro dei moduli assegna quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatico avvia il processo). Potete utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** il nome del processo, come definito in Designer.

**Stato:** indica se l&#39;istanza di processo è in esecuzione normalmente, cambia stato o arrestata. (Vedere Informazioni sugli stati delle istanze di processo.)

**Data creazione:** data e ora di creazione del sottoprocesso.

**Data aggiornamento: data e ora** dell&#39;ultima modifica dello stato del sottoprocesso.

Nella pagina Dettagli istanza processo è possibile effettuare le seguenti operazioni:

* Selezionate un’operazione per visualizzarne i dettagli. Quando si seleziona un&#39;operazione, viene visualizzata la pagina Dettagli operazione.
* Selezionate una sottoprocedura per visualizzarne i dettagli. Quando si seleziona un sottoprocesso, viene visualizzata la pagina Dettagli istanza processo.
* Terminare o riprovare le operazioni o i processi secondari, a seconda del loro stato.

### Informazioni sugli stati delle operazioni {#about-operation-statuses}

Un&#39;operazione (un passaggio di un processo) può avere i seguenti stati:

**COMPLETE:** Operazione completata.

**ESECUZIONE:** L&#39;operazione viene eseguita normalmente. Potrebbe ricevere l&#39;input dell&#39;utente o attendere l&#39;interazione dell&#39;utente, oppure potrebbe essere in corso un passaggio automatico.

**STALLED:** si è verificato un problema durante l&#39;elaborazione dell&#39;operazione. Verificare l’errore o l’eccezione nella pagina Operazioni bloccate.

**TERMINATO:** L&#39;operazione è stata terminata da un amministratore.

### Terminare le operazioni o i processi secondari {#terminate-operations-or-subprocesses}

Se un&#39;operazione o un sottoprocesso è stato bloccato o ha rilevato un&#39;altra condizione di errore, oppure se è necessario forzare un&#39;operazione o un sottoprocesso per interromperne l&#39;esecuzione, è possibile interromperlo.

È possibile terminare un&#39;operazione in esecuzione.

Quando si interrompe un&#39;operazione, il suo stato diventa TERMINATO. L&#39;operazione non viene completata e l&#39;istanza di processo si arresta.

È possibile terminare un sottoprocesso con qualsiasi stato.

Quando si termina un sottoprocesso, il suo stato cambia in TERMINAZIONE, TERMINATA, e l&#39;istanza di processo si arresta alle operazioni correnti. Durante il sottoprocesso non vengono eseguite altre operazioni, anche se l&#39;istanza del processo padre continua a essere eseguita.

Non è possibile terminare i processi con elementi gateway nel diagramma del processo. Se si tenta di terminare questi tipi di processi, le operazioni all&#39;interno degli elementi del gateway non vengono influenzate. Per terminare le operazioni all&#39;interno di un elemento gateway, è necessario terminare direttamente le operazioni.

1. Nella pagina Dettagli istanza processo fare clic sulla scheda Operazioni o Sottoprocessi.
1. Selezionare l&#39;operazione o il sottoprocesso e fare clic su Termina.

### Ripetere un&#39;operazione {#retry-an-operation}

È possibile ritentare l&#39;operazione con stato STALLED.

Quando si ripete un&#39;operazione, al flusso di lavoro Forms viene inviata una richiesta per riavviare l&#39;operazione. Se la richiesta ha esito positivo, lo stato cambia in ESECUZIONE. Se l&#39;operazione non può essere riavviata, rimane STALLED e potrebbe essere necessario interromperla.

1. Nella pagina Dettagli istanza processo, fare clic sulla scheda Operazioni.
1. Selezionate l’operazione e fate clic su Riprova.

## Operazioni {#working-with-operations}

La pagina Dettagli operazione mostra un riepilogo di un’operazione in un processo e delle assegnazioni utente correnti.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Fate clic sul nome di un processo per visualizzarne le istanze. Fate clic su un&#39;istanza di processo per visualizzare la pagina Dettagli istanza processo, quindi selezionate un&#39;operazione per visualizzare la pagina Dettagli operazione.

   Per ogni attività, l&#39;elenco mostra le informazioni seguenti:

   **Nome processo - Versione:** nome del processo, come definito in Workbench.

   **Applicazione:** l&#39;applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo indica che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data creazione:** la data e l&#39;ora in cui il processo è stato distribuito.

