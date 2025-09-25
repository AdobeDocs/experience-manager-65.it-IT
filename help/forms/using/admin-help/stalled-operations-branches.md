---
title: Utilizzo di operazioni e rami bloccati
description: Le pagine Operazioni bloccate e Rami bloccati mostrano i processi bloccati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '719'
ht-degree: 100%

---

# Utilizzo di operazioni e rami bloccati {#working-with-stalled-operations-and-branches}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Le pagine Operazioni bloccate e Rami bloccati mostrano i processi bloccati. Un processo può bloccarsi quando si verifica un errore durante o dopo l’esecuzione di un’operazione oppure a causa di un’operazione di arresto intenzionale nel processo:

* Le operazioni possono bloccarsi a causa di un errore imprevisto. Tuttavia, un’operazione di ramo bloccato in un processo interrompe deliberatamente l’ulteriore esecuzione di un processo e richiede l’intervento dell’amministratore.
* I rami possono bloccarsi tra le operazioni durante la valutazione di una regola.

Quando un processo si arresta, non vengono eseguite ulteriori operazioni finché il problema non viene risolto e l’operazione o il ramo non viene riavviato.

Per ogni elemento bloccato, l’elenco mostra le seguenti informazioni:

**Nome operazione o nome ramo:** nome dell’operazione o del ramo.

**Stato:** sempre BLOCCATO per gli elementi bloccati.

**Errore:** una breve descrizione del problema.

**ID processo:** il numero intero positivo assegnato da Forms workflow quando viene creata un’istanza del processo (vale a dire quando un utente o un passaggio automatico avvia un processo). Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** il nome del processo assegnato in Workbench.

**Data di blocco:** la data e l’ora in cui l’operazione o il ramo si è bloccato.

Nella pagina Operazioni bloccate o Rami bloccati è possibile eseguire le operazioni seguenti:

* Seleziona un errore per visualizzarne i dettagli. Quando si seleziona un errore, viene visualizzata la pagina Dettagli errore.
* Terminare oppure provare a eseguire di nuovo le operazioni bloccate o i rami bloccati.

## Interruzione o nuovo tentativo di esecuzione di operazioni o rami bloccati {#terminating-or-retrying-stalled-operations-or-branches}

Nella pagina Operazioni bloccate, è possibile terminare le istanze di processo visualizzate.

Quando si termina un’istanza di processo, l’esecuzione viene interrotta e non vengono eseguite ulteriori operazioni. In genere, un processo viene terminato solo se si blocca o diventa inutilizzabile a causa di un errore e non può essere corretto e riavviato.

Nella pagina Operazioni bloccate o Rami bloccati è possibile ritentare l’operazione o il ramo.

Quando ritenti un’operazione, a Forms Workflow viene inviata una richiesta per riavviare l’operazione. Se l’errore che ha causato l’arresto del processo è stato corretto e la richiesta di nuovo tentativo ha esito positivo, il processo riprende a funzionare dal punto in cui era stato arrestato e il suo stato cambia in ESECUZIONE. Se non è possibile riavviare l’operazione, questa rimane BLOCCATA e potrebbe essere necessario terminarla.

### Come terminare un’operazione bloccata {#terminate-a-stalled-operation}

1. Nella console di amministrazione, fare clic su Servizi > Forms workflow > Errori operazioni bloccate.
1. Nella pagina Operazioni bloccate, selezionare l’elemento che si desidera terminare e fare clic su Termina.

### Nuova esecuzione di un’operazione o di un ramo bloccato {#retry-a-stalled-operation-or-branch}

1. Nella console di amministrazione, fare clic su Servizi > Forms workflow, quindi fare clic su Errori di operazioni bloccate o Errori di ramo bloccati.
1. Nella pagina Operazioni bloccate o Rami bloccati selezionare l’elemento che si desidera riprovare e fare clic su Riprova.

## Visualizzazione dei dettagli di errore relativi alle operazioni o ai rami bloccati {#viewing-error-details-about-stalled-operations-or-branches}

Se si seleziona un errore dall’elenco degli elementi bloccati nella pagina Operazioni bloccate o Rami bloccati, viene visualizzata la pagina Dettagli errore, che mostra i dettagli dell’errore, i quali possono facilitare la risoluzione del problema.

La casella nella parte inferiore della pagina contiene le informazioni sull’errore.

Dalla pagina Dettagli errore è inoltre possibile terminare o riprovare a eseguire le operazioni bloccate e riprovare i rami bloccati.

## Il processo non si arresta quando l’utente di escalation non esiste {#process-does-not-stall-when-escalation-user-does-not-exist}

Si verificano errori quando l’operazione Assegna attività nel servizio Utente di AEM Forms è configurata per l’inoltro dell’attività a un altro utente dopo un periodo di tempo specifico e l’utente dell’inoltro viene eliminato dopo l’esecuzione dell’operazione Assegna attività, ma prima dell’inoltro.

Quando si verifica questa situazione, lo stato del processo e dell’attività non cambia al momento dell’escalation configurata e l’escalation non si verifica, ma il processo non si arresta. Nel registro del server viene visualizzato il seguente messaggio:

&quot;L’entità principale specificata per l’escalation non è valida per taskID: *numero*, coda specificata: *numero*.&quot;

Se l’utente di escalation viene eliminato prima della generazione dell’attività (prima dell’esecuzione dell’operazione Assegna attività), il processo si arresta oppure viene generato l’evento di eccezione InvalidPrincipal.

Per evitare questo problema, quando si elimina un utente, cercare le attività appartenenti a tale utente e gestirle di conseguenza. Vedere [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).
