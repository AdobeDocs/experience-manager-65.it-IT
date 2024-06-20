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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 0%

---

# Gestione dei processi {#managing-processes}

La pagina Elenco processi mostra i processi avviati da un utente o che sono stati avviati automaticamente.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms. Nell&#39;elenco dei processi sono visualizzate le informazioni riportate di seguito.

   **Nome processo - Versione:** Il nome del processo, come definito in Workbench.

   **Applicazione:** Applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo significa che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data di creazione:** La data e l’ora in cui il processo è stato distribuito.

1. Fare clic sul nome di un processo per visualizzarne le istanze nella pagina Istanza processo.

## Utilizzo delle istanze del processo {#working-with-process-instances}

Se si accede alla pagina Istanza processo dalla pagina Elenco processi, vengono elencate tutte le istanze di processo del processo selezionato. Se si accede alla pagina Istanza processo dopo aver eseguito una ricerca, vengono elencate solo le istanze di processo trovate.

Per ogni istanza di processo, l&#39;elenco mostra le seguenti informazioni:

**ID processo:** Identificatore assegnato dal flusso di lavoro dei moduli quando viene creata un&#39;istanza del processo, ovvero quando un utente o un passaggio automatico avvia un processo. È possibile utilizzare questo identificatore per tenere traccia dell&#39;istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** Il nome del processo, come definito in Workbench.

**Stato:** Indica se l&#39;istanza del processo è in esecuzione normalmente, se cambia lo stato o se è stata arrestata. Consultate Informazioni sugli stati delle istanze di processo.

**Data di creazione:** Data e ora di creazione dell&#39;istanza di processo.

**Data aggiornamento:** Data e ora dell&#39;ultima modifica dello stato dell&#39;istanza del processo.

Nella pagina Istanza processo è possibile effettuare le operazioni riportate di seguito.

* Selezionare un&#39;istanza di processo per visualizzarne i dettagli, ad esempio le operazioni e i sottoprocessi. Quando si seleziona un&#39;istanza di processo, viene visualizzata la pagina Dettagli istanza di processo.
* Sospendi, rimuovi la sospensione o interrompi le istanze del processo.
* Cercare un&#39;istanza di processo. Per iniziare una ricerca, fare clic su Cerca.

### Informazioni sugli stati delle istanze di processo {#about-process-instance-statuses}

Un&#39;istanza di processo, inclusi i sottoprocessi, può avere i seguenti stati:

**COMPLETATO:** Tutti i rami e le operazioni nell&#39;istanza del processo sono stati completati. COMPLETE è lo stato finale di un&#39;istanza di processo.

**COMPLETAMENTO:** Lo stato dell&#39;istanza del processo sta per essere impostato su COMPLETE.

**AVVIATO:** L&#39;istanza di processo è stata creata ma non è ancora in esecuzione. INITIATED è il primo stato di un&#39;istanza di processo.

**IN ESECUZIONE:** L&#39;istanza del processo viene eseguita normalmente. È possibile che sia in corso un passaggio automatico oppure che l&#39;istanza del processo riceva l&#39;input dell&#39;utente o sia in attesa dell&#39;interazione dell&#39;utente.

**SOSPESO:** L&#39;istanza del processo è stata sospesa da un amministratore o da un passaggio del processo. Non si verificheranno ulteriori operazioni finché lo stato non viene modificato.

**SOSPENSIONE:** Lo stato sta per diventare SOSPESO. Se un&#39;operazione è stata progettata per ignorare le richieste di sospensione e non è ancora stata completata, è necessario completarla prima che l&#39;istanza del processo venga sospesa.

**TERMINATO:** L&#39;istanza del processo è stata terminata da un amministratore.

**TERMINAZIONE:** Lo stato sta per essere modificato in TERMINATED. Se un&#39;operazione è stata progettata per ignorare le richieste terminate e non è ancora stata completata, è necessario completarla prima che l&#39;istanza del processo venga terminata.

**ANNULLAMENTO DELLA SOSPENSIONE:** Lo stato sta per essere modificato in IN ESECUZIONE dopo essere stato SOSPESO.

>[!NOTE]
>
>Quando viene richiesta la modifica dello stato di un&#39;istanza del processo, ad esempio la sospensione o l&#39;interruzione, la richiesta entra nella coda di comandi per il flusso di lavoro Forms. A seconda delle dimensioni della coda e della velocità di elaborazione complessiva, lo stato visualizzato potrebbe non cambiare fino a quando la pagina non viene ricaricata una o più volte.

### Sospendi o rimuovi la sospensione delle istanze di processo {#suspend-or-unsuspend-process-instances}

Se è necessario risolvere un problema o se si è certi che un&#39;istanza del processo incontrerà un problema in un passaggio successivo a causa di una condizione esterna, è possibile sospendere temporaneamente l&#39;istanza del processo.

È possibile sospendere le istanze di processo con stato IN ESECUZIONE.

Dopo aver sospeso un&#39;istanza del processo, lo stato cambia in SOSPESO, quindi SOSPESO e il processo si interrompe al momento dell&#39;operazione corrente. L&#39;istanza di processo rimane in questo stato fino a quando lo stato non viene modificato in UNSUSPENDED.

Solo le istanze di processo con stato SOSPESO possono essere modificate in NON SOSPESO.

Quando si annulla la sospensione di un&#39;istanza di processo, lo stato cambia in ESECUZIONE e continua con l&#39;operazione in cui era stata sospesa.

Quando si sospende un&#39;istanza di processo che ha richiamato altri processi (processi figlio) tramite l&#39;operazione di richiamo, anche i processi figlio vengono sospesi.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza processo selezionare il processo e fare clic su Sospendi o Annulla sospensione.

### Terminare un&#39;istanza di processo {#terminate-a-process-instances}

Se un&#39;operazione di un&#39;istanza di processo è stata interrotta o si è verificata un&#39;altra condizione di errore oppure se è necessario forzare l&#39;interruzione dell&#39;esecuzione di un&#39;istanza di processo, è possibile terminare l&#39;istanza di processo.

È possibile terminare le istanze di processo con qualsiasi stato.

Quando si termina un&#39;istanza di processo, lo stato cambia in TERMINATING, quindi TERMINATED e il processo si arresta al momento dell&#39;operazione corrente. Non vengono eseguite ulteriori operazioni e tutte le operazioni e le attività associate vengono terminate.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Nella pagina Istanza processo selezionare il processo e fare clic su Termina.

## Utilizzo dei dettagli dell’istanza del processo {#working-with-process-instance-details}

La pagina Dettagli istanza di processo mostra la cronologia di un&#39;istanza di processo.

Nell&#39;area Riepilogo vengono visualizzate informazioni di base sull&#39;istanza del processo.

Nella scheda Operazioni, ogni operazione per l&#39;istanza di processo viene visualizzata in ordine di completamento dal primo all&#39;ultimo con le seguenti informazioni:

**Nome operazione:** Il nome dell’operazione, come definito in Workbench.

**Stato:** Indica se l&#39;operazione viene eseguita normalmente o è stata interrotta. Consultate Informazioni sugli stati delle istanze di processo.

**Nome filiale:** Il nome del ramo, come definito in Workbench.

**Data di inizio:** Data e ora di inizio dell&#39;operazione.

**Data completamento:** Data e ora in cui è stata completata l&#39;operazione.

Un sottoprocesso è un&#39;istanza di processo avviata da un altro processo ed eseguita indipendentemente da quest&#39;ultimo. I sottoprocessi vengono visualizzati solo se sono stati progettati come parte del processo in Workbench. Nella scheda Sottoprocessi, ogni sottoprocesso viene visualizzato con le seguenti informazioni:

**ID processo:** Questo numero intero positivo assegnato dal flusso di lavoro per i moduli quando viene creata un&#39;istanza del processo, ovvero quando un utente o un passaggio automatico avvia il processo. È possibile utilizzare questo identificatore per tenere traccia dell&#39;istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** Nome del processo, come definito in Designer.

**Stato:** Indica se l&#39;istanza del processo viene eseguita normalmente, se cambia lo stato o se è interrotta. Consultate Informazioni sugli stati delle istanze di processo.

**Data di creazione:** Data e ora di creazione del sottoprocesso.

**Data aggiornamento:** Data e ora dell&#39;ultima modifica dello stato del sottoprocesso.

Nella pagina Dettagli istanza processo è possibile effettuare le operazioni riportate di seguito.

* Selezionare un&#39;operazione per visualizzarne i dettagli. Quando si seleziona un&#39;operazione, viene visualizzata la pagina Dettagli operazione.
* Selezionare un processo secondario per visualizzare i dettagli relativi. Quando si seleziona un processo secondario, viene visualizzata la pagina Dettagli istanza processo.
* Termina o riprova operazioni o processi secondari, a seconda del loro stato.

### Informazioni sugli stati delle operazioni {#about-operation-statuses}

Un&#39;operazione (una fase di un processo) può avere i seguenti stati:

**COMPLETATO:** Operazione completata.

**IN ESECUZIONE:** L&#39;operazione viene eseguita normalmente. Potrebbe ricevere l&#39;input dell&#39;utente o attendere l&#39;interazione dell&#39;utente, oppure potrebbe essere in corso un passaggio automatico.

**ARRESTATO:** Problema durante l&#39;elaborazione dell&#39;operazione. Verificare l&#39;errore o l&#39;eccezione nella pagina Operazioni bloccate.

**TERMINATO:** Operazione terminata da un amministratore.

### Termina operazioni o processi secondari {#terminate-operations-or-subprocesses}

Se un&#39;operazione o un sottoprocesso si è arrestato o ha rilevato un&#39;altra condizione di errore oppure se è necessario forzare l&#39;interruzione di un&#39;operazione o di un sottoprocesso, è possibile terminarlo.

È possibile terminare un&#39;operazione in ESECUZIONE.

Quando si termina un&#39;operazione, lo stato cambia in TERMINATO. L&#39;operazione non viene completata e l&#39;istanza del processo viene arrestata.

È possibile terminare un sottoprocesso con qualsiasi stato.

Quando si termina un processo secondario, lo stato del processo cambia in TERMINATING, quindi TERMINATED e l&#39;istanza del processo si arresta in corrispondenza delle operazioni correnti. Non vengono eseguite ulteriori operazioni nel processo secondario, anche se l&#39;istanza del processo padre continua a essere eseguita.

Non è possibile terminare i processi che contengono elementi gateway nel diagramma dei processi. Se si tenta di terminare questi tipi di processi, le operazioni all&#39;interno degli elementi del gateway non vengono influenzate. Per terminare le operazioni che si trovano all&#39;interno di un elemento gateway, è necessario terminare direttamente le operazioni.

1. Nella pagina Dettagli istanza processo fare clic sulla scheda Operazioni o sulla scheda Sottoprocessi.
1. Selezionare l&#39;operazione o il processo secondario e fare clic su Termina.

### Riprovare un&#39;operazione {#retry-an-operation}

È possibile ritentare l&#39;operazione con lo stato STALLED.

Quando si ritenta un&#39;operazione, al flusso di lavoro di Forms viene inviata una richiesta per riavviare l&#39;operazione. Se la richiesta ha esito positivo, lo stato diventa RUNNING (IN ESECUZIONE). Se non è possibile riavviare l&#39;operazione, questa rimane BLOCCATA e potrebbe essere necessario terminarla.

1. Nella pagina Dettagli istanza processo fare clic sulla scheda Operazioni.
1. Selezionare l&#39;operazione e fare clic su Riprova.

## Utilizzo delle operazioni {#working-with-operations}

Nella pagina Dettagli operazione viene visualizzato un riepilogo di un&#39;operazione in un processo e delle relative assegnazioni utente correnti.

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro Forms > Flusso di lavoro Forms.
1. Fare clic sul nome di un processo per visualizzarne le istanze. Fare clic su un&#39;istanza di processo per visualizzare la pagina Dettagli istanza di processo, quindi selezionare un&#39;operazione per visualizzare la pagina Dettagli operazione.

   Per ogni attività, l&#39;elenco mostra le seguenti informazioni:

   **Nome processo - Versione:** Il nome del processo, come definito in Workbench.

   **Applicazione:** Applicazione a cui appartiene il processo, come definito in Workbench.

   **Stato:** Attivo significa che il processo è quello attivato per la versione del processo. Inattivo significa che il processo è una versione precedente che contiene ancora istanze di processo.

   **Data di creazione:** La data e l’ora in cui il processo è stato distribuito.
