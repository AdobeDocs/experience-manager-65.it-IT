---
title: Gestione dei processi
seo-title: Managing Processes
description: La pagina Elenco processi mostra i processi avviati da un utente o avviati automaticamente. Ulteriori informazioni sulla gestione dei processi.
seo-description: The Process List page shows the processes that a user has initiated or that were started automatically. Learn more about managing the processes.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
exl-id: 21a2317d-3542-4ccb-98db-3cedf20c89ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 0%

---

# Gestione dei processi {#managing-processes}

La pagina Elenco processi mostra i processi avviati da un utente o avviati automaticamente.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms. L&#39;elenco dei processi mostra le seguenti informazioni:

   **Nome processo - Versione:** Nome del processo, come definito in Workbench.

   **Applicazione:** Applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo significa che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data creazione:** Data e ora di distribuzione del processo.

1. Fare clic su un nome di processo per visualizzare le istanze di processo nella pagina Istanza di processo.

## Utilizzo delle istanze di processo {#working-with-process-instances}

Se si accede alla pagina Istanza processo dalla pagina Elenco processi, vengono elencate tutte le istanze del processo selezionato. Se si accede alla pagina Istanza di processo dopo aver eseguito una ricerca, vengono elencate solo le istanze di processo trovate.

Per ogni istanza di processo, l’elenco mostra le seguenti informazioni:

**ID processo:** Identificatore assegnato dal flusso di lavoro del modulo quando viene creata un&#39;istanza del processo, ovvero quando un utente o un passaggio automatico avvia un processo. Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** Nome del processo, come definito in Workbench.

**Stato:** Indica se l&#39;istanza di processo è in esecuzione normale, se cambia stato o se è stata arrestata. (Consultare Informazioni sugli stati delle istanze del processo.)

**Data creazione:** Data e ora di creazione dell&#39;istanza del processo.

**Data aggiornamento:** Data e ora dell’ultima modifica dello stato dell’istanza del processo.

Nella pagina Istanza del processo è possibile effettuare le seguenti operazioni:

* Selezionare un&#39;istanza di processo per visualizzarne i dettagli, ad esempio le operazioni e i sottoprocessi. Quando selezioni un&#39;istanza di processo, viene visualizzata la pagina Dettagli istanza processo .
* Sospendi, annulla sospensione o interrompi le istanze del processo.
* Cerca un&#39;istanza di processo. Per iniziare una ricerca, fare clic su Cerca.

### Informazioni sugli stati delle istanze del processo {#about-process-instance-statuses}

Un&#39;istanza di processo, inclusi i sottoprocessi, può avere i seguenti stati:

**COMPLETO:** Tutti i rami e le operazioni nell&#39;istanza di processo sono stati completati. COMPLETE è lo stato finale di un&#39;istanza di processo.

**COMPLETAMENTO:** Lo stato dell&#39;istanza di processo sta per cambiare in COMPLETE.

**AVVIATO:** L&#39;istanza di processo è stata creata ma non è ancora in esecuzione. INITIATED è il primo stato di un&#39;istanza di processo.

**IN ESECUZIONE:** L&#39;istanza del processo è in esecuzione normale. Potrebbe essere in corso un passaggio automatico, oppure l&#39;istanza di processo potrebbe ricevere l&#39;input dell&#39;utente o attendere l&#39;interazione dell&#39;utente.

**SOSPESO:** L&#39;istanza del processo è stata sospesa da un amministratore o da un passaggio del processo. Non verranno eseguite ulteriori operazioni finché lo stato non viene modificato.

**SOSPENSIONE:** Lo stato sta per cambiare in SOSPESO. Se un’operazione è stata progettata per ignorare le richieste di sospensione e non è ancora stata completata, l’operazione deve essere completata prima che l’istanza di processo sia sospesa.

**TERMINATO:** L&#39;istanza del processo è stata terminata da un amministratore.

**TERMINAZIONE:** Lo stato sta per cambiare in TERMINATO. Se un&#39;operazione è stata progettata per ignorare le richieste di terminazione e non è ancora stata completata, è necessario completare l&#39;operazione prima che l&#39;istanza di processo venga terminata.

**SOSPENSIONE:** Lo stato sta per cambiare in ESECUZIONE dopo essere stato SOSPESO.

>[!NOTE]
>
>Quando viene effettuata una richiesta per modificare lo stato di un’istanza di processo (ad esempio per sospendere o terminare), la richiesta entra nella coda di comando per il flusso di lavoro dei moduli. A seconda delle dimensioni della coda e della velocità di elaborazione complessiva, lo stato visualizzato potrebbe non cambiare finché la pagina non viene ricaricata una o più volte.

### Sospendi o annulla la sospensione delle istanze del processo {#suspend-or-unsuspend-process-instances}

Se hai bisogno di risolvere un problema o se sai che un&#39;istanza di processo incontrerà un problema in un secondo momento a causa di una condizione esterna, puoi sospendere temporaneamente l&#39;istanza di processo.

È possibile sospendere le istanze del processo con stato RUNNING.

Dopo aver sospeso un&#39;istanza di processo, il suo stato cambia in SOSPENSIONE, quindi SOSPESO e il processo si mette in pausa al suo funzionamento corrente. L&#39;istanza di processo rimane in questo stato finché lo stato non viene modificato in NON SOSPESO.

Solo le istanze del processo con stato SOSPESO possono essere modificate in NON SOSPESO.

Quando si annulla la sospensione di un&#39;istanza di processo, il suo stato diventa IN ESECUZIONE e continua con l&#39;operazione in cui era stata sospesa.

Quando si sospende un&#39;istanza di processo che ha richiamato altri processi (processi figlio) utilizzando l&#39;operazione di chiamata, vengono sospesi anche i processi figlio.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza di processo, seleziona il processo e fai clic su Sospendi o Annulla sospensione.

### Termina istanze del processo {#terminate-a-process-instances}

Se un&#39;operazione di un&#39;istanza di processo si è bloccata o si è verificata un&#39;altra condizione di errore, o se è necessario forzare un&#39;istanza di processo a interrompere l&#39;esecuzione, è possibile terminare l&#39;istanza di processo.

È possibile terminare le istanze del processo con qualsiasi stato.

Quando si interrompe un&#39;istanza di processo, il suo stato cambia in TERMINATING, quindi TERMINATED e il processo si arresta al suo funzionamento corrente. Non vengono eseguite ulteriori operazioni e tutte le operazioni e le attività associate vengono terminate.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza di processo selezionare il processo e fare clic su Termina.

## Utilizzo dei dettagli dell’istanza di processo {#working-with-process-instance-details}

La pagina Dettagli istanza processo mostra la cronologia di un&#39;istanza di processo.

L&#39;area Riepilogo mostra informazioni di base sull&#39;istanza del processo.

Nella scheda Operazioni viene visualizzata ogni operazione per l&#39;istanza di processo in ordine di completamento dal primo all&#39;ultimo con le seguenti informazioni:

**Nome operazione:** Nome dell’operazione, come definito in Workbench.

**Stato:** Indica se l&#39;operazione è in esecuzione normale o se è stata interrotta. (Consultare Informazioni sugli stati delle istanze del processo.)

**Nome filiale:** Nome del ramo, come definito in Workbench.

**Data di inizio:** Data e ora di inizio dell&#39;operazione.

**Data completamento:** Data e ora del completamento dell’operazione.

Un sottoprocesso è un&#39;istanza di processo avviata da un altro processo ed eseguita indipendentemente da tale altro processo. I sottoprocessi vengono visualizzati solo se sono stati progettati come parte del processo in Workbench. Nella scheda Sottoprocessi viene visualizzato ogni sottoprocesso con le seguenti informazioni:

**ID processo:** Questo numero intero positivo che il flusso di lavoro dei moduli assegna quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatizzato avvia il processo). Puoi utilizzare questo identificatore per tenere traccia dell&#39;istanza di processo nel suo ciclo di vita.

**Nome processo - Versione:** Nome del processo, come definito in Designer.

**Stato:** Indica se l&#39;istanza di processo è in esecuzione normale, se cambia stato o se è interrotta. (Consultare Informazioni sugli stati delle istanze del processo.)

**Data creazione:** Data e ora di creazione del sottoprocesso.

**Data aggiornamento:** Data e ora dell’ultima modifica dello stato del sottoprocesso.

Nella pagina Dettagli istanza processo è possibile eseguire le seguenti operazioni:

* Seleziona un’operazione per visualizzarne i dettagli. Quando si seleziona un&#39;operazione, viene visualizzata la pagina Dettagli operazione.
* Selezionare un sottoprocesso per visualizzarne i dettagli. Quando si seleziona un sottoprocesso, viene visualizzata la pagina Dettagli istanza processo.
* Termina o riavvia operazioni o sottoprocessi, a seconda del loro stato.

### Informazioni sugli stati delle operazioni {#about-operation-statuses}

Un&#39;operazione (un passaggio di un processo) può avere i seguenti stati:

**COMPLETO:** Operazione completata.

**IN ESECUZIONE:** L&#39;operazione viene eseguita normalmente. Potrebbe ricevere l&#39;input dell&#39;utente o attendere l&#39;interazione dell&#39;utente, oppure potrebbe essere in corso un passaggio automatico.

**STALLED** Errore durante l&#39;elaborazione dell&#39;operazione. Controlla l&#39;errore o l&#39;eccezione nella pagina Operazioni in stallo.

**TERMINATO:** Operazione terminata da un amministratore.

### Termina operazioni o sottoprocessi {#terminate-operations-or-subprocesses}

Se un&#39;operazione o un sottoprocesso si è arrestato o ha rilevato altre condizioni di errore o se è necessario forzare un&#39;operazione o un sottoprocesso a interrompere l&#39;esecuzione, è possibile interromperlo.

È possibile terminare un&#39;operazione in ESECUZIONE.

Quando si interrompe un&#39;operazione, il suo stato cambia in TERMINATO. L&#39;operazione non viene completata e l&#39;istanza del processo si interrompe.

È possibile terminare un processo secondario con qualsiasi stato.

Quando si interrompe un sottoprocesso, il suo stato cambia in TERMINATING, quindi TERMINATED e l&#39;istanza del processo si arresta alle sue operazioni correnti. Non vengono eseguite ulteriori operazioni nel sottoprocesso, anche se l&#39;istanza del processo padre continua a essere eseguita.

Non è possibile terminare i processi che contengono elementi gateway nel diagramma del processo. Se si tenta di terminare questi tipi di processi, le operazioni all&#39;interno degli elementi del gateway non vengono influenzate. Per terminare le operazioni all&#39;interno di un elemento gateway, è necessario terminare direttamente le operazioni.

1. Nella pagina Dettagli istanza processo fare clic sulla scheda Operazioni o Sottoprocessi.
1. Selezionare l&#39;operazione o il sottoprocesso e fare clic su Termina.

### Riprovare un&#39;operazione {#retry-an-operation}

È possibile riprovare l&#39;operazione con lo stato STALLED.

Quando si ripete un&#39;operazione, al flusso di lavoro Forms viene inviata una richiesta per riavviare l&#39;operazione. Se la richiesta ha esito positivo, lo stato cambia in ESECUZIONE. Se l&#39;operazione non può essere riavviata, rimane STALLED e potrebbe essere necessario interromperla.

1. Nella pagina Dettagli istanza processo fare clic sulla scheda Operazioni.
1. Seleziona l’operazione e fai clic su Riprova.

## Utilizzo delle operazioni {#working-with-operations}

Nella pagina Dettagli operazione viene visualizzato un riepilogo di un&#39;operazione in un processo e delle relative assegnazioni utente correnti.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Fare clic sul nome di un processo per visualizzare le relative istanze del processo. Fare clic su un&#39;istanza di processo per visualizzare la pagina Dettagli istanza di processo, quindi selezionare un&#39;operazione per visualizzare la pagina Dettagli operazione.

   Per ogni attività, l’elenco mostra le seguenti informazioni:

   **Nome processo - Versione:** Nome del processo, come definito in Workbench.

   **Applicazione:** Applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo significa che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data creazione:** Data e ora di distribuzione del processo.
