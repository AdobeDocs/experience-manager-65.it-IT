---
title: Utilizzo di operazioni e rami bloccati
description: Le pagine Operazioni bloccate e Rami bloccati mostrano i processi bloccati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Utilizzo di operazioni e rami bloccati {#working-with-stalled-operations-and-branches}

Le pagine Operazioni bloccate e Rami bloccati mostrano i processi bloccati. Un processo può bloccarsi quando si verifica un errore durante o dopo l&#39;esecuzione di un&#39;operazione o a causa di un&#39;operazione di arresto intenzionale nel processo:

* Le operazioni possono bloccarsi a causa di un errore imprevisto. Tuttavia, un’operazione Stall Branch in un processo interrompe deliberatamente l’ulteriore esecuzione di un processo e richiede l’intervento dell’amministratore.
* I rami possono bloccarsi tra le operazioni durante la valutazione di una regola.

Quando un processo si arresta, non vengono eseguite ulteriori operazioni finché il problema non viene risolto e l&#39;operazione o il ramo non viene riavviato.

Per ogni elemento in stallo, l&#39;elenco mostra le seguenti informazioni:

**Nome operazione o nome ramo:** Nome dell&#39;operazione o del ramo.

**Stato:** Sempre BLOCCATO per gli elementi in stallo.

**Errore:** Breve descrizione del problema.

**ID processo:** Numero intero positivo assegnato dal flusso di lavoro di Forms quando viene creata un&#39;istanza del processo, ovvero quando un utente o un passaggio automatico avvia un processo. È possibile utilizzare questo identificatore per tenere traccia dell&#39;istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** Il nome del processo assegnato in Workbench.

**Data di blocco:** La data e l&#39;ora in cui l&#39;operazione o il ramo si è arrestato.

Nella pagina Operazioni bloccate o Rami bloccati è possibile eseguire le operazioni seguenti:

* Seleziona un errore per visualizzare i dettagli su di esso. Quando si seleziona un errore, viene visualizzata la pagina Dettagli errore.
* Termina o riprova le operazioni bloccate o riprova i rami bloccati.

## Interruzione o nuovo tentativo di operazioni o rami bloccati {#terminating-or-retrying-stalled-operations-or-branches}

Nella pagina Operazioni bloccate è possibile terminare le istanze di processo visualizzate.

Quando si termina un&#39;istanza di processo, l&#39;esecuzione viene interrotta e non vengono eseguite ulteriori operazioni. In genere, un processo viene terminato solo se diventa bloccato o inutilizzabile a causa di un errore e non può essere corretto e riavviato.

Nella pagina Operazioni bloccate o Rami bloccati è possibile ritentare l&#39;operazione o il ramo.

Quando si ritenta un&#39;operazione, al flusso di lavoro di Forms viene inviata una richiesta per riavviare l&#39;operazione. Se l&#39;errore che ha causato l&#39;arresto del processo è stato corretto e la richiesta di nuovo tentativo ha esito positivo, il processo riprende a funzionare dal punto in cui era stato arrestato e il suo stato cambia in ESECUZIONE. Se non è possibile riavviare l&#39;operazione, questa rimane BLOCCATA e potrebbe essere necessario terminarla.

### Termina un&#39;operazione in stallo {#terminate-a-stalled-operation}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Errori operazioni bloccate.
1. Nella pagina Operazioni bloccate selezionare l&#39;elemento che si desidera terminare e fare clic su Termina.

### Riprovare un&#39;operazione o un ramo bloccato {#retry-a-stalled-operation-or-branch}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli, quindi fai clic su Errori di operazioni bloccate o Errori di ramo bloccati.
1. Nella pagina Operazioni bloccate o Rami bloccati selezionare l&#39;elemento che si desidera riprovare e fare clic su Riprova.

## Visualizzazione dei dettagli di errore relativi alle operazioni o ai rami bloccati {#viewing-error-details-about-stalled-operations-or-branches}

Se si seleziona un errore dall&#39;elenco degli elementi bloccati nella pagina Operazioni bloccate o Rami bloccati, viene visualizzata la pagina Dettagli errore, che mostra i dettagli dell&#39;errore che possono facilitare la risoluzione del problema.

La casella nella parte inferiore della pagina contiene le informazioni sull&#39;errore.

Dalla pagina Dettagli errore è inoltre possibile terminare o riprovare le operazioni bloccate e riprovare i rami bloccati.

## Il processo non si arresta quando l&#39;utente di riassegnazione non esiste {#process-does-not-stall-when-escalation-user-does-not-exist}

Si verificano errori quando l&#39;operazione Assegna attività nel servizio Utente di AEM Forms è configurata per l&#39;inoltro dell&#39;attività a un altro utente dopo un periodo di tempo specifico e l&#39;utente dell&#39;inoltro viene eliminato dopo l&#39;esecuzione dell&#39;operazione Assegna attività, ma prima dell&#39;inoltro.

Quando si verifica questa situazione, lo stato del processo e dell&#39;attività non cambia al momento dell&#39;escalation configurata e l&#39;escalation non si verifica, ma il processo non si arresta. Nel registro del server viene visualizzato il seguente messaggio:

&quot;L&#39;entità specificata per l&#39;escalation non è valida per taskID: *numero*, coda specificata: *numero*.&quot;

Se l&#39;utente di escalation viene eliminato prima della generazione dell&#39;attività (prima dell&#39;esecuzione dell&#39;operazione Assegna attività), il processo si arresta oppure viene generato l&#39;evento di eccezione InvalidPrincipal.

Per evitare questo problema, quando si elimina un utente, cercare le attività appartenenti a tale utente e gestirle di conseguenza. (vedere [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
