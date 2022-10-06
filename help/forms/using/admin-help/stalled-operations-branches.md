---
title: Utilizzo di operazioni e rami bloccati
seo-title: Working with stalled operations and branches
description: La pagina Operazioni in stallo e la pagina Rami in stallo mostrano i processi in stallo.
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Utilizzo di operazioni e rami bloccati {#working-with-stalled-operations-and-branches}

La pagina Operazioni in stallo e la pagina Rami in stallo mostrano i processi in stallo. Un processo può arrestarsi quando si verifica un errore durante o dopo l&#39;esecuzione di un&#39;operazione o a causa di un&#39;operazione di arresto deliberato nel processo:

* Le operazioni possono arrestarsi a causa di un errore imprevisto. Tuttavia, un&#39;operazione di Stallo in un processo impedisce deliberatamente l&#39;esecuzione di un processo e richiede l&#39;intervento dell&#39;amministratore.
* I rami possono essere bloccati tra le operazioni durante una valutazione di una regola.

Quando un processo si arresta, non vengono eseguite ulteriori operazioni fino a quando il problema non viene risolto e l&#39;operazione o il ramo non viene riavviato.

Per ogni elemento in stallo, l’elenco mostra le seguenti informazioni:

**Nome operazione o nome filiale:** Nome dell&#39;operazione o del ramo.

**Stato:** Sempre STALLED per gli elementi in stallo.

**Errore:** Breve descrizione del problema.

**ID processo:** Numero intero positivo che il flusso di lavoro dei moduli assegna quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatizzato avvia un processo). Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** Nome del processo assegnato in Workbench.

**Data di stallo:** Data e ora in cui l’operazione o il ramo si è arrestato.

Nella pagina Operazioni in stallo o Rami in stallo è possibile effettuare le seguenti operazioni:

* Seleziona un errore per visualizzarne i dettagli. Quando si seleziona un errore, viene visualizzata la pagina Dettagli errore.
* Terminare o riprovare le operazioni in stallo o riprovare i rami in stallo.

## Terminazione o ripristino di operazioni o rami bloccati {#terminating-or-retrying-stalled-operations-or-branches}

Nella pagina Operazioni in stallo è possibile interrompere le istanze del processo visualizzate.

Quando si interrompe un&#39;istanza di processo, questa smette di essere in esecuzione e non si verificano ulteriori operazioni. In genere si interrompe un processo solo se viene bloccato o inutilizzabile a causa di un errore e non può essere risolto e riavviato.

Nella pagina Operazioni in stallo o nella pagina Rami in stallo è possibile riprovare l&#39;operazione o il ramo.

Quando si ripete un&#39;operazione, al flusso di lavoro Forms viene inviata una richiesta per riavviare l&#39;operazione. Se l&#39;errore che ha causato l&#39;arresto del processo è stato risolto e la richiesta di nuovo tentativo è riuscita, il processo inizia a essere eseguito nuovamente dal punto in cui era stato bloccato e il suo stato cambia in IN ESECUZIONE. Se l&#39;operazione non può essere riavviata, rimane STALLED e potrebbe essere necessario interromperla.

### Termina un&#39;operazione in stallo {#terminate-a-stalled-operation}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro dei moduli > Errori di operazioni in stallo.
1. Nella pagina Operazioni in stallo selezionare l&#39;elemento da terminare e fare clic su Termina.

### Riprova un&#39;operazione o un ramo in stallo {#retry-a-stalled-operation-or-branch}

1. Nella console di amministrazione, fare clic su Servizi > flusso di lavoro moduli, quindi fare clic su Errori di operazioni in stallo o su Errori di ramo in stallo.
1. Nella pagina Operazioni in stallo o Rami in stallo selezionare l&#39;elemento da riprovare e fare clic su Riprova.

## Visualizzazione dei dettagli degli errori relativi alle operazioni o ai rami bloccati {#viewing-error-details-about-stalled-operations-or-branches}

Se si seleziona un errore dall&#39;elenco degli elementi in stallo nella pagina Operazioni in stallo o Rami in stallo, viene visualizzata la pagina Dettagli errore, che mostra i dettagli dell&#39;errore che può aiutarti a risolvere il problema.

La casella nella parte inferiore della pagina contiene le informazioni sull’errore.

È inoltre possibile terminare o riprovare le operazioni in stallo e riprovare i rami in stallo dalla pagina Dettagli errore.

## Il processo non si arresta quando l&#39;utente di inoltro per moderazione non esiste {#process-does-not-stall-when-escalation-user-does-not-exist}

Gli errori si verificano quando l’operazione Assegna attività nel servizio moduli AEM è configurata per inoltrare l’attività a un altro utente dopo un determinato periodo di tempo e l’utente dell’inoltro viene eliminato dopo l’esecuzione dell’operazione Assegna attività ma prima che l’inoltro venga eseguito.

Quando si verifica questa situazione, lo stato del processo e dell&#39;attività non cambia al momento dell&#39;inoltro per moderazione configurato e l&#39;escalation non si verifica ma il processo non si arresta. Nel registro server viene visualizzato il seguente messaggio:

&quot;L&#39;entità principale specificata per l&#39;inoltro non è valida, per taskID: *numero*, coda specificata: *numero*.&quot;

Se l&#39;utente di inoltro per moderazione viene eliminato prima che l&#39;attività venga generata (prima dell&#39;esecuzione dell&#39;operazione Assegna attività), il processo si arresta o viene generato l&#39;evento di eccezione InvalidPrincipal.

Per evitare questo problema, quando elimini un utente, cerca le attività appartenenti a tale utente e gestisci di conseguenza. (Vedi [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
