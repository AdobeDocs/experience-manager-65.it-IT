---
title: Visualizzare le statistiche relative a Work Manager
description: Nella scheda Work Manager vengono visualizzate le statistiche che si riferiscono ai relativi elementi. Scopri come visualizzare e filtrare gli elementi di lavoro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1215'
ht-degree: 100%

---

# Visualizzare le statistiche relative a Work Manager {#view-statistics-related-to-work-manager}

Nella scheda Work Manager vengono visualizzate le statistiche che si riferiscono ai relativi elementi. Questi elementi di lavoro si trovano in stati diversi a seconda della fase del processo. (Consulta [Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only). È possibile filtrare le informazioni per visualizzare solo un sottoinsieme degli elementi utilizzando le varie opzioni disponibili (ad esempio, Stato o Categoria). È possibile ordinare gli elementi di lavoro o di processo risultanti (in ordine crescente o decrescente) facendo clic su una delle intestazioni di colonna. È inoltre possibile gestire gli elementi di lavoro utilizzando gli strumenti operativi visualizzati sopra l’elenco degli elementi di lavoro.

## Filtrare gli elementi di lavoro {#filter-the-work-items}

1. Fai clic sulla scheda Work Manager.
1. Seleziona i criteri per uno o più filtri descritti di seguito, quindi fai clic su Applica.

### Categoria {#category}

**Predefinito:** tutti gli elementi di lavoro a cui il client non ha assegnato una categoria al momento dell’invio. Work Manager gestisce questi elementi, pertanto gli stati appartengono a Work Manager.

**Gestione processi:** tutti i processi che appartengono a Gestione processi. Gestione processi gestisce i propri processi e dispone dei rispettivi stati. Consulta gli stati dei processi specifici descritti di seguito.

**Flusso di lavoro:** tutti gli elementi di lavoro che appartengono all’esecuzione del flusso di lavoro. Flusso di lavoro non gestisce i propri elementi di lavoro ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

**Eventi:** tutti gli elementi di lavoro che appartengono a Gestione eventi. Gestione eventi non gestisce i propri elementi di lavoro ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

### Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi) {#status-for-default-workflow-or-events-categories-only}

**Mostra tutto:** visualizza tutti gli elementi di lavoro correnti.

**Pianificato:** visualizza tutti gli elementi di lavoro pronti per l’esecuzione da parte del server applicazioni, ma non ancora avviati.

**In pausa:** visualizza tutti gli elementi di lavoro pianificati messi in pausa dall’applicazione client. Questi elementi possono essere eseguiti o eliminati. (Consulta Gestire gli elementi di lavoro o i processi).

**In corso:** visualizza tutti gli elementi di lavoro che Work Manager del server applicazioni ha raccolto e che verranno completati o che non riusciranno. Non è possibile eseguire operazioni su questi elementi di lavoro.

**Completo:** visualizza tutti gli elementi di lavoro eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato, mentre gli elementi non persistenti vengono eliminati al completamento dei callback ai rispettivi gestori. È possibile eliminare questi elementi tramite l’operazione Elimina elementi. (Consulta Gestire gli elementi di lavoro o i processi).

**Non riuscito:** visualizza tutti gli elementi di lavoro non completati correttamente a causa di una condizione di errore. Questi elementi di lavoro possono essere ritentati più volte tramite l’operazione Riprova elementi. (Consulta Gestire gli elementi di lavoro o i processi). Un collegamento di errore nella colonna Stato consente di accedere ai dettagli relativi a tale errore.

**Sconosciuto:** visualizza tutti gli elementi di lavoro il cui stato è sconosciuto.

### Stato (solo per la categoria Gestione processi) {#status-for-job-manager-category-only}

**Completato:** visualizza tutti i processi eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato, mentre gli elementi non persistenti vengono eliminati al completamento dei callback ai rispettivi gestori.

**Completamento richiesto:** visualizza i processi per i quali è stata effettuata una richiesta completa.

**Non riuscito quando richiesto:** visualizza i processi per i quali è stata effettuata una richiesta che non è riuscita.

**Non riuscito:** visualizza i processi non completati correttamente a causa di una condizione di errore. Un collegamento di errore nella colonna Stato consente di accedere ai dettagli relativi a tale errore.

**Terminato quando richiesto:** visualizza i processi per i quali è stata effettuata una richiesta di terminazione.

**Terminato:** visualizza i processi terminati senza completamento.

**Sospeso quando richiesto:** visualizza i processi per i quali è stata effettuata una richiesta di sospensione.

**Sospeso:** visualizza i processi sospesi.

**Ripreso quando richiesto:** visualizza i processi per i quali è stata effettuata una richiesta di ripresa.

**In coda:** mostra i processi presenti nella coda.

**In esecuzione:** mostra i processi in esecuzione.

### Nome server {#server-name}

Solo per i server in cluster, seleziona il nome del nodo per visualizzare gli elementi di lavoro o di processo creati solo su tale server. Se selezioni Mostra tutto, vengono visualizzati tutti gli elementi di lavoro per tutti i nodi di un cluster.

### Ora di creazione {#create-time}

Seleziona un’opzione in questo filtro per visualizzare solo gli elementi di lavoro creati nell’intervallo di tempo selezionato. Se ad esempio selezioni 1 giorno, vengono visualizzati tutti gli elementi di lavoro creati entro 24 ore prima dell’ora impostata nel filtro Precedente a.

### Precedente a {#prior-to}

Imposta la data e l’ora utilizzate dal filtro Ora di creazione come data di fine. Mantieni selezionata l’opzione Usa data e ora corrente per filtrare dalla data e dall’ora correnti, oppure deseleziona l’opzione e inserisci i valori appropriati. Fai clic sulle icone del calendario o sull’icona dell’orologio per selezionare i valori utilizzando questi strumenti.

Se ad esempio selezioni Crea ora = 1 giorno e Precedente a = Usa data e ora correnti, verranno visualizzati tutti gli elementi di lavoro creati nelle ultime 24 ore.

>[!NOTE]
>
>Nelle distribuzioni del database di Oracle, i filtri per l’intervallo di date (ovvero le impostazioni Ora di creazione e Precedente a) non funzionano in modo accurato. Utilizza un altro filtro per recuperare gli elementi di lavoro.

## Informazioni sull’interfaccia della scheda Work Manager {#about-the-work-manager-tab-interface}

Quando esegui una query di Work Manager o un’operazione su un elemento di lavoro o un processo, sopra l’elenco viene visualizzato un messaggio. Questo messaggio fornisce un feedback sull’azione avviata e, in alcuni casi, un collegamento Ulteriori informazioni per fornire i dettagli. Ad esempio, se l’operazione avviata non è riuscita, il messaggio viene visualizzato nello stesso modo e fornisce un collegamento per ottenere dettagli sull’errore.

Quando fai clic su Ulteriori informazioni, nella finestra di dialogo Dettagli operazione viene visualizzato un elenco degli elementi di lavoro o dei processi selezionati durante l’operazione. È possibile fare clic su ogni voce di elenco per visualizzare i dettagli errore nella parte inferiore della finestra di dialogo.

### Gestire gli elementi di lavoro o i processi {#manage-the-work-items-or-jobs}

1. Utilizza gli strumenti di operazione descritti di seguito per gestire gli elementi di lavoro o i processi nell’elenco.

   >[!NOTE]
   >
   >Le operazioni sono disponibili a seconda dello stato dell’elemento.

   **Elimina elementi:** elimina l’elemento di lavoro o il processo selezionato.

   **Sospendi elementi:** sospende l’elemento di lavoro o il processo selezionato.

   **Riprendi elementi:** riprende l’elemento di lavoro o il processo selezionato dal relativo stato di pausa.

   **Riprova elementi:** tenta di rieseguire l’elemento di lavoro o il processo selezionato dal relativo stato corrente.

   Per verificare se un’operazione è stata eseguita correttamente, fai clic su Ulteriori informazioni sopra l’elenco. Viene visualizzata una finestra di dialogo contenente gli elementi di lavoro o i processi selezionati e i relativi stati.

## Informazioni aggiuntive sugli stati degli elementi di lavoro {#additional-information-about-work-item-statuses}

Una transizione di stato tipica per un elemento di lavoro è Nuovo > Programmato > In corso > Completo o Errore.

Lo stato di pausa interrompe questo flusso normale. L’applicazione client o l’amministratore di sistema possono avviare questa interruzione (ad esempio, per la manutenzione o l’aggiornamento). È possibile annullare questa azione utilizzando l’operazione Riprendi per riportare l’elemento di lavoro allo stato Pianificato.

Un elemento di lavoro in stato Pianificato è in coda per l’esecuzione non ancora iniziata. Questi elementi possono essere messi in pausa o eliminati oppure passeranno allo stato In corso una volta rimossi dalla coda da Work Manager. Gli elementi di lavoro in corso non possono essere modificati. Verranno completati o avranno esito negativo.

Lo stato Errore è il risultato di una condizione di errore che si verifica durante l’esecuzione dell’elemento di lavoro. Se sospetti che gli errori siano circostanziati (a causa del contesto al momento dell’esecuzione), è possibile riprovare l’esecuzione, rimettendo in coda l’elemento di lavoro. È consentito solo un numero limitato di tentativi.
