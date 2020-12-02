---
title: Visualizzare le statistiche relative a Work Manager
seo-title: Visualizzare le statistiche relative a Work Manager
description: Nella scheda Gestione lavoro sono visualizzate le statistiche relative agli elementi di Gestione lavoro. Scoprite come visualizzare e filtrare gli elementi di lavoro.
seo-description: Nella scheda Gestione lavoro sono visualizzate le statistiche relative agli elementi di Gestione lavoro. Scoprite come visualizzare e filtrare gli elementi di lavoro.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---


# Visualizzare le statistiche relative a Work Manager {#view-statistics-related-to-work-manager}

Nella scheda Gestione lavoro sono visualizzate le statistiche relative agli elementi di Gestione lavoro. Questi elementi di lavoro si trovano in stati diversi a seconda di dove si trovano nel processo. (Vedere [Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Potete filtrare le informazioni per visualizzare solo un sottoinsieme degli elementi utilizzando le varie opzioni disponibili (ad esempio, Stato o Categoria). Potete ordinare gli elementi di lavoro o di processo risultanti (in ordine crescente o decrescente) facendo clic su una delle intestazioni di colonna. È inoltre possibile gestire gli elementi di lavoro utilizzando gli strumenti operativi visualizzati sopra l&#39;elenco degli elementi di lavoro.

## Filtrare gli elementi di lavoro {#filter-the-work-items}

1. Fare clic sulla scheda Work Manager.
1. Selezionate i criteri per uno o più dei filtri descritti di seguito e fate clic su Vai.

### Categoria {#category}

**Impostazione predefinita:** tutti gli elementi di lavoro a cui il cliente non ha assegnato una categoria al momento dell&#39;invio. Work Manager gestisce questi elementi, pertanto gli stati appartengono a Work Manager.

**Job Manager:** tutti i processi appartenenti a Job Manager. Job Manager gestisce i propri processi e ha i propri stati. Consultate gli stati specifici del processo descritti di seguito.

**Flusso di lavoro:** tutti gli elementi di lavoro appartenenti all’esecuzione del flusso di lavoro. Workflow non gestisce i propri elementi di lavoro, ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

**Eventi:** tutti gli elementi di lavoro che appartengono a Gestione evento. Gestione eventi non gestisce i propri elementi di lavoro, ma si affida a Work Manager; pertanto, gli stati appartengono a Work Manager.

### Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi) {#status-for-default-workflow-or-events-categories-only}

**Mostra tutto:** visualizza tutti gli elementi di lavoro correnti.

**Pianificato:** visualizza tutti gli elementi di lavoro pronti per l&#39;esecuzione da parte del server dell&#39;applicazione ma non ancora avviati.

**Sospeso:** visualizza tutti gli elementi di lavoro pianificati messi in pausa dall&#39;applicazione client. Questi elementi possono essere eseguiti o eliminati. Consultate Gestire gli elementi di lavoro o i processi.

**In corso:** visualizza tutti gli elementi di lavoro estratti dal manager del server dell’applicazione e che verranno completati o meno. Non è possibile utilizzare le operazioni su questi elementi di lavoro.

**Completa:** visualizza tutti gli elementi di lavoro eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento delle callback ai gestori di callback. È possibile eliminare questi elementi utilizzando l&#39;operazione Elimina elementi. Consultate Gestire gli elementi di lavoro o i processi.

**Non riuscito:** visualizza tutti gli elementi di lavoro che non sono stati completati correttamente a causa di una condizione di errore. Questi elementi di lavoro possono essere riprovati alcune volte mediante l&#39;operazione Riprova elementi. Consultate Gestire gli elementi di lavoro o i processi. Un collegamento di errore nella colonna Stato consente di accedere ai dettagli relativi all’errore.

**Sconosciuto:** visualizza tutti gli elementi di lavoro il cui stato è sconosciuto.

### Stato (solo per la categoria Job Manager) {#status-for-job-manager-category-only}

**Completato:** visualizza tutti i processi eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento delle callback ai gestori di callback.

**Completa richiesta:** visualizza i processi per i quali è stata effettuata una richiesta completa.

**Richiesta non riuscita:** visualizza i processi per i quali è stata eseguita una richiesta di errore.

**Non riuscito:** visualizza i processi che non sono stati completati correttamente a causa di una condizione di errore. Un collegamento di errore nella colonna Stato consente di accedere ai dettagli relativi all’errore.

**Termina richiesta:** visualizza i processi per i quali è stata effettuata una richiesta di interruzione.

**Terminato:** visualizza i processi terminati senza essere completati.

**Sospendi richiesto:** visualizza i processi per i quali è stata effettuata una richiesta di sospensione.

**Sospeso:** visualizza i processi sospesi.

**Riprendi richiesta:** visualizza i processi per i quali è stata effettuata una richiesta di ripresa.

**In coda:** visualizza i processi in coda.

**Esecuzione:** visualizza i processi in esecuzione.

### Nome server {#server-name}

Solo per i server cluster, selezionate il nome del nodo per visualizzare gli elementi di lavoro o di processo creati solo su tale server. Se Mostra tutto è selezionato, vengono visualizzati tutti gli elementi di lavoro per tutti i nodi di un cluster.

### Tempo di creazione {#create-time}

Selezionate un’opzione in questo filtro per mostrare solo gli elementi di lavoro creati entro il periodo di tempo selezionato. Ad esempio, selezionando 1 giorno vengono visualizzati tutti gli elementi di lavoro creati entro 24 ore prima dell&#39;ora impostata nel filtro Precedente a.

### Precedente a {#prior-to}

Imposta la data e l’ora utilizzate dal filtro Crea ora come data di fine. Mantenere l’opzione Usa data e ora correnti selezionata per filtrare la data e l’ora correnti, oppure deselezionare l’opzione e immettere i valori appropriati. Fate clic sulle icone del calendario o dell’orologio per selezionare i valori utilizzando tali strumenti.

Ad esempio, selezionando Crea ora = 1 giorno e Precedente a = Usa data e ora correnti vengono restituiti tutti gli elementi di lavoro creati nelle ultime 24 ore.

>[!NOTE]
>
>Nelle  distribuzioni del database Oracle, i filtri dell&#39;intervallo di date (ovvero Crea ora e Precedente alle impostazioni) non funzionano correttamente. Usate un altro filtro per recuperare gli elementi di lavoro.

## Informazioni sull&#39;interfaccia della scheda Work Manager {#about-the-work-manager-tab-interface}

Quando si esegue una query di Work Manager o si esegue un&#39;operazione su un elemento di lavoro o un processo, viene visualizzato un messaggio sopra l&#39;elenco. Questo messaggio fornisce un feedback sull’azione avviata e, in alcuni casi, un collegamento Ulteriori informazioni per fornire i dettagli. Ad esempio, se l&#39;operazione avviata non è riuscita, il messaggio indica la quantità e fornisce un collegamento per ottenere dettagli sull&#39;errore.

Quando si fa clic su Ulteriori informazioni, nella finestra di dialogo Dettagli operazione viene visualizzato un elenco degli elementi di lavoro o dei processi selezionati durante l&#39;operazione. È possibile fare clic su ciascuna voce dell&#39;elenco per visualizzare i Dettagli errore nella parte inferiore della finestra di dialogo.

### Gestire gli elementi di lavoro o i processi {#manage-the-work-items-or-jobs}

1. Utilizzate gli strumenti operativi descritti di seguito per gestire gli elementi di lavoro o i processi elencati.

   >[!NOTE]
   >
   >Le operazioni sono disponibili a seconda dello stato dell’elemento.

   **Elimina elementi:** elimina l’elemento di lavoro o il processo selezionato.

   **Pausa elementi:** mette in pausa l’elemento di lavoro o il processo selezionato.

   **Riprendi elementi:** riprende l’elemento di lavoro o il processo selezionato dallo stato di pausa.

   **Riprova elementi:** tenta di eseguire nuovamente l&#39;elemento di lavoro o il processo selezionato dallo stato corrente.

   Per verificare se un&#39;operazione ha avuto esito positivo, fare clic su Ulteriori informazioni sopra l&#39;elenco. Viene visualizzata una finestra di dialogo contenente gli elementi di lavoro o i processi selezionati e i relativi stati.

## Ulteriori informazioni sugli stati degli elementi di lavoro {#additional-information-about-work-item-statuses}

Una transizione di stato tipica per un elemento di lavoro è Nuovo > Pianificato > In corso > Completato o Non riuscito.

Lo stato Pausa interrompe questo flusso normale. L&#39;applicazione client o l&#39;amministratore di sistema possono avviare questa interruzione (ad esempio, per la manutenzione o l&#39;aggiornamento). È possibile invertire questa azione utilizzando l&#39;operazione Riprendi per riportare l&#39;elemento di lavoro in uno stato Pianificato.

Un elemento di lavoro nello stato Pianificato viene messo in coda per l&#39;esecuzione che non è ancora iniziata. Questi elementi possono essere messi in pausa o eliminati, oppure passeranno allo stato In corso quando Work Manager li prenderà dalla coda. Gli elementi di lavoro in corso non possono essere modificati. Completano o falliscono.

Lo stato Non riuscito si verifica a seguito di una condizione di errore che si verifica durante l&#39;esecuzione dell&#39;elemento di lavoro. Se si sospetta che gli errori siano circostanziali (a causa del contesto al momento dell&#39;esecuzione), è possibile riprovare l&#39;esecuzione, riportando l&#39;elemento di lavoro nella coda. È consentito solo un numero limitato di tentativi.
