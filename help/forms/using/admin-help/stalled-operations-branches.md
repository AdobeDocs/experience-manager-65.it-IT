---
title: Operazioni con operazioni e rami in stallo
seo-title: Operazioni con operazioni e rami in stallo
description: Le pagine Operazioni in stallo e Rami in stallo mostrano i processi che si sono bloccati.
seo-description: Le pagine Operazioni in stallo e Rami in stallo mostrano i processi che si sono bloccati.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# Operazioni con operazioni e rami in stallo {#working-with-stalled-operations-and-branches}

Le pagine Operazioni in stallo e Rami in stallo mostrano i processi che si sono bloccati. Un processo può arrestarsi quando si verifica un errore durante o dopo l&#39;esecuzione di un&#39;operazione o a causa di un&#39;operazione di arresto deliberato nel processo:

* Le operazioni possono terminare a causa di un errore imprevisto. Tuttavia, un&#39;operazione Stall Branch in un processo impedisce deliberatamente l&#39;esecuzione di un processo e richiede l&#39;intervento dell&#39;amministratore.
* Le diramazioni possono rimanere bloccate tra le operazioni durante una valutazione di una regola.

Quando un processo si arresta, non vengono eseguite ulteriori operazioni finché il problema non viene risolto e l&#39;operazione o il ramo non viene riavviato.

Per ogni elemento in stallo, l&#39;elenco mostra le seguenti informazioni:

**Nome operazione o Nome ramo:** il nome dell&#39;operazione o del ramo.

**Stato:** Sempre STALLATO per gli elementi in stallo.

**Errore:** breve descrizione del problema.

**ID processo:** il numero intero positivo assegnato dal flusso di lavoro del modulo quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatico avvia un processo). Potete utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** il nome del processo assegnato in Workbench.

**Data di arresto:** la data e l&#39;ora in cui l&#39;operazione o il ramo è bloccato.

Nella pagina Operazioni bloccate o Brani bloccati potete effettuare le seguenti operazioni:

* Selezionate un errore per visualizzarne i dettagli. Quando si seleziona un errore, viene visualizzata la pagina Dettagli errore.
* Terminare o riprovare le operazioni in stallo o ripetere i rami in stallo.

## Terminazione o ripristino di operazioni o rami in stallo {#terminating-or-retrying-stalled-operations-or-branches}

Nella pagina Operazioni bloccate, è possibile terminare le istanze del processo visualizzate.

Quando si interrompe un&#39;istanza di processo, questa si interrompe e non si eseguono altre operazioni. In genere, un processo viene interrotto solo se bloccato o inutilizzabile a causa di un errore e non può essere risolto e riavviato.

Nella pagina Operazioni in stallo o Filiali in stallo è possibile ritentare l&#39;operazione o il ramo.

Quando si ripete un&#39;operazione, al flusso di lavoro Forms viene inviata una richiesta per riavviare l&#39;operazione. Se l&#39;errore che ha causato l&#39;arresto del processo è stato risolto e la richiesta del nuovo tentativo è stata completata, il processo inizia nuovamente a essere eseguito dal punto in cui era stato bloccato e il suo stato cambia in ESECUZIONE. Se l&#39;operazione non può essere riavviata, rimane STALLED e potrebbe essere necessario interromperla.

### Terminare un&#39;operazione in stallo {#terminate-a-stalled-operation}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Errori operazioni interrotte.
1. Nella pagina Operazioni bloccate, selezionate l’elemento da terminare e fate clic su Termina.

### Ritentare un&#39;operazione o un ramo in stallo {#retry-a-stalled-operation-or-branch}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli, quindi fare clic su Errori operazioni in stato o Errori rami in stato di arresto.
1. Nella pagina Operazioni in stallo o Rami in stallo, selezionare l&#39;elemento da riprovare e fare clic su Riprova.

## Visualizzazione dei dettagli degli errori relativi alle operazioni in stallo o ai rami {#viewing-error-details-about-stalled-operations-or-branches}

Se si seleziona un errore dall&#39;elenco degli elementi in stallo nella pagina Operazioni in stallo o Branches in stallo, viene visualizzata la pagina Dettagli errore, che mostra i dettagli sull&#39;errore che può essere utile per risolvere il problema.

La casella nella parte inferiore della pagina contiene le informazioni sull’errore.

Dalla pagina Dettagli errore è inoltre possibile terminare o riprovare le operazioni in stallo e riprovare i rami in stallo.

## Il processo non si arresta quando l&#39;utente di escalation non esiste {#process-does-not-stall-when-escalation-user-does-not-exist}

Gli errori si verificano quando l&#39;operazione Assegna attività nei moduli AEM Il servizio Utente è configurato per inoltrare l&#39;attività a un altro utente dopo un determinato periodo di tempo e l&#39;utente dell&#39;inoltro viene eliminato dopo l&#39;esecuzione dell&#39;operazione Assegna attività ma prima che l&#39;inoltro venga eseguito.

Quando si verifica questa situazione, lo stato del processo e dell&#39;attività non cambia al momento dell&#39;escalation configurata, e l&#39;escalation non si verifica ma il processo non si arresta. Nel registro del server viene visualizzato il seguente messaggio:

&quot;L&#39;entità specificata per l&#39;inoltro non è valida, per taskID: *number*, coda specificata: *number*.&quot;

Se l&#39;utente dell&#39;escalation viene eliminato prima della generazione dell&#39;attività (prima dell&#39;esecuzione dell&#39;operazione Assign Task), il processo si arresta o viene generato l&#39;evento di eccezione InvalidPrincipal.

Per evitare questo problema, quando eliminate un utente, cercate le attività che appartengono a tale utente e gestitele di conseguenza. (Vedere [Uso delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
