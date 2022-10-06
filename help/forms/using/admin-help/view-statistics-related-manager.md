---
title: Visualizza le statistiche relative a Work Manager
seo-title: View statistics related to Work Manager
description: Nella scheda Work Manager sono visualizzate le statistiche relative agli elementi di Work Manager. Scopri come visualizzare e filtrare gli elementi di lavoro.
seo-description: The Work Manager tab displays statistics that relate to Work Manager items. Learn how you can view and filter the work items.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Visualizza le statistiche relative a Work Manager {#view-statistics-related-to-work-manager}

Nella scheda Work Manager sono visualizzate le statistiche relative agli elementi di Work Manager. Questi elementi di lavoro si trovano in stati diversi a seconda di dove si trovano nel loro processo. (Vedi [Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) È possibile filtrare le informazioni per visualizzare solo un sottoinsieme di elementi utilizzando le varie opzioni disponibili (ad esempio, Stato o Categoria). È possibile ordinare gli elementi di lavoro o di lavoro risultanti (in ordine crescente o decrescente) facendo clic su una delle intestazioni di colonna. Inoltre, è possibile gestire gli elementi di lavoro utilizzando gli strumenti operativi visualizzati sopra l&#39;elenco degli elementi di lavoro.

## Filtrare gli elementi di lavoro {#filter-the-work-items}

1. Fare clic sulla scheda Work Manager.
1. Seleziona i criteri per uno o più filtri descritti di seguito e fai clic su Vai.

### Categoria {#category}

**Predefinito:** Tutti gli elementi di lavoro a cui il cliente non ha assegnato una categoria al momento dell&#39;invio. Work Manager gestisce questi elementi, pertanto gli stati appartengono a Work Manager.

**Gestione processi:** Tutti i processi che appartengono a Job Manager. Job Manager gestisce i propri lavori e dispone dei propri stati di lavoro. Vedi gli stati specifici del processo descritti di seguito.

**Flusso di lavoro:** Tutti gli elementi di lavoro che appartengono all&#39;esecuzione del flusso di lavoro. Workflow non gestisce i propri elementi di lavoro, ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

**Eventi:** Tutti gli elementi di lavoro appartenenti a Gestione eventi. Gestione eventi non gestisce i propri elementi di lavoro, ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

### Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi) {#status-for-default-workflow-or-events-categories-only}

**Mostra tutto:** Visualizza tutti gli elementi di lavoro correnti.

**Pianificato:** Visualizza tutti gli elementi di lavoro pronti per l&#39;esecuzione da parte del server applicazioni ma non ancora avviati.

**In pausa:** Visualizza tutti gli elementi di lavoro pianificati messi in pausa dall&#39;applicazione client. Questi elementi possono essere eseguiti o eliminati. (Vedere Gestione degli elementi di lavoro o dei processi.)

**In corso:** Visualizza tutti gli elementi di lavoro raccolti da Work Manager dell&#39;applicazione e completati o non riusciti. Non è possibile utilizzare le operazioni su questi elementi di lavoro.

**Completa:** Visualizza tutti gli elementi di lavoro eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento dei callback ai gestori callback. È possibile eliminare questi elementi utilizzando l’operazione Elimina elementi. (Vedere Gestione degli elementi di lavoro o dei processi.)

**Non riuscito:** Visualizza tutti gli elementi di lavoro che non sono stati completati correttamente a causa di una condizione di errore. Questi elementi di lavoro possono essere riprovati alcune volte utilizzando l&#39;operazione Riprova elementi. (Vedere Gestione degli elementi di lavoro o dei processi.) Un collegamento Errore nella colonna Stato consente di accedere ai dettagli dell’errore.

**Sconosciuto:** Visualizza tutti gli elementi di lavoro il cui stato è sconosciuto.

### Stato (solo per la categoria Job Manager) {#status-for-job-manager-category-only}

**Completato:** Visualizza tutti i processi eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento dei callback ai gestori callback.

**Completa richiesta:** Visualizza i processi per i quali è stata effettuata una richiesta completa.

**Richiesta non riuscita:** Visualizza i processi per i quali è stata effettuata una richiesta di errore.

**Non riuscito:** Visualizza i processi che non sono stati completati correttamente a causa di una condizione di errore. Un collegamento Errore nella colonna Stato consente di accedere ai dettagli dell’errore.

**Termina richiesta:** Visualizza i processi per i quali è stata effettuata una richiesta di chiusura.

**Terminato:** Visualizza i processi terminati senza completamento.

**Sospendi richiesto:** Visualizza i processi per i quali è stata effettuata una richiesta di sospensione.

**Sospeso:** Visualizza i processi sospesi.

**Riprendi richiesto:** Visualizza i processi per i quali è stata effettuata una richiesta di ripresa.

**In coda:** Visualizza i lavori in coda.

**In esecuzione:** Visualizza i processi in esecuzione.

### Nome server {#server-name}

Solo per i server cluster, selezionare il nome del nodo per visualizzare gli elementi di lavoro o di lavoro creati solo su quel server. Se l&#39;opzione Mostra tutto è selezionata, vengono visualizzati tutti gli elementi di lavoro per tutti i nodi di un cluster.

### Crea ora {#create-time}

Selezionare un&#39;opzione in questo filtro per mostrare solo gli elementi di lavoro creati entro il periodo di tempo selezionato. Ad esempio, selezionando 1 giorno vengono visualizzati tutti gli elementi di lavoro creati entro 24 ore prima del tempo impostato nel filtro Precedente a.

### Prima di {#prior-to}

Imposta la data e l’ora utilizzate dal filtro Crea ora come data di fine. Mantieni selezionata l’opzione Usa data e ora corrente per filtrare dalla data e dall’ora correnti oppure deseleziona l’opzione e immetti i valori appropriati. Fai clic sulle icone del calendario o dell’orologio per selezionare i valori utilizzando tali strumenti.

Ad esempio, selezionando Crea ora = 1 giorno e Precedente a = Usa data e ora corrente vengono restituiti tutti gli elementi di lavoro creati nelle ultime 24 ore.

>[!NOTE]
>
>Ad Oracle, nelle implementazioni del database, i filtri dell’intervallo di date (ovvero Crea ora e Precedente alle impostazioni) non funzionano correttamente. Utilizza un altro filtro per recuperare gli elementi di lavoro.

## Informazioni sull’interfaccia della scheda Work Manager {#about-the-work-manager-tab-interface}

Quando si esegue una query di Work Manager o si esegue un&#39;operazione su un elemento di lavoro o un processo, viene visualizzato un messaggio sopra l&#39;elenco. Questo messaggio fornisce un feedback sull’azione avviata e, in alcuni casi, un collegamento Ulteriori informazioni per fornire i dettagli. Ad esempio, se l’operazione avviata non è riuscita, il messaggio indica lo stesso valore e fornisce un collegamento per ottenere informazioni sull’errore.

Quando si fa clic su Ulteriori informazioni, nella finestra di dialogo Dettagli operazione viene visualizzato un elenco degli elementi di lavoro o dei processi selezionati durante l&#39;operazione. È possibile fare clic su ogni voce dell’elenco per visualizzare i Dettagli errore nella parte inferiore della finestra di dialogo.

### Gestire gli elementi o i processi di lavoro {#manage-the-work-items-or-jobs}

1. Utilizzare gli strumenti operativi descritti di seguito per gestire gli elementi di lavoro o i processi nell&#39;elenco.

   >[!NOTE]
   >
   >Le operazioni sono disponibili a seconda dello stato dell’elemento.

   **Elimina elementi:** Elimina l&#39;elemento di lavoro o il processo selezionato.

   **Pausa elementi:** Sospende l&#39;elemento di lavoro o il processo selezionato.

   **Riprendi elementi:** Riprende l&#39;elemento di lavoro o il processo selezionato dallo stato di sospensione.

   **Riprova elementi:** Tenta di eseguire nuovamente l&#39;elemento di lavoro o il processo selezionato dal relativo stato corrente.

   Per verificare se un&#39;operazione ha avuto esito positivo, fare clic su Ulteriori informazioni nell&#39;elenco. Viene visualizzata una finestra di dialogo contenente gli elementi di lavoro o i processi selezionati e i relativi stati.

## Informazioni aggiuntive sugli stati degli elementi di lavoro {#additional-information-about-work-item-statuses}

Una transizione di stato tipica per un elemento di lavoro è Nuovo > Pianificato > In corso > Completato o Non riuscito.

Lo stato Pausa interrompe questo flusso normale. L’applicazione client o l’amministratore di sistema possono avviare l’interruzione (ad esempio, per la manutenzione o l’aggiornamento). È possibile annullare questa azione utilizzando l&#39;operazione Riprendi per spostare nuovamente l&#39;elemento di lavoro in uno stato Pianificato.

Un elemento di lavoro in stato Pianificato viene messo in coda per l&#39;esecuzione che non è ancora iniziata. Questi elementi possono essere messi in pausa o eliminati oppure passeranno allo stato In corso quando Work Manager li porterà dalla coda. Impossibile modificare gli elementi di lavoro in corso. Completano o falliscono.

Lo stato Non riuscito si verifica in seguito a una condizione di errore che si verifica durante l&#39;esecuzione dell&#39;elemento di lavoro. Se si sospetta che gli errori siano circostanziali (a causa del contesto al momento dell&#39;esecuzione), è possibile riprovare l&#39;esecuzione, riportando l&#39;elemento di lavoro nella coda. Sono consentiti solo un numero limitato di tentativi.
