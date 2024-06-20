---
title: Visualizzare le statistiche relative a Work Manager
description: Nella scheda Work Manager (Responsabile del lavoro) vengono visualizzate le statistiche relative agli elementi di Work Manager. Scopri come visualizzare e filtrare gli elementi di lavoro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---

# Visualizzare le statistiche relative a Work Manager {#view-statistics-related-to-work-manager}

Nella scheda Work Manager (Responsabile del lavoro) vengono visualizzate le statistiche relative agli elementi di Work Manager. Questi elementi di lavoro si trovano in stati diversi a seconda della posizione in cui si trovano nel processo. (vedere [Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) È possibile filtrare le informazioni per visualizzare solo un sottoinsieme degli elementi utilizzando le varie opzioni disponibili (ad esempio, Stato o Categoria). È possibile ordinare i lavori o gli elementi di lavoro risultanti (in ordine crescente o decrescente) facendo clic su una delle intestazioni di colonna. È inoltre possibile gestire gli elementi di lavoro utilizzando gli strumenti operativi visualizzati sopra l&#39;elenco degli elementi di lavoro.

## Filtrare gli elementi di lavoro {#filter-the-work-items}

1. Fare clic sulla scheda Gestione lavori.
1. Selezionare i criteri per uno o più filtri descritti di seguito e quindi fare clic su Vai.

### Categoria {#category}

**Predefinito:** Tutti gli elementi di lavoro a cui il client non ha assegnato una categoria al momento dell&#39;invio. Work Manager gestisce questi elementi, pertanto gli stati appartengono a Work Manager.

**Gestione processo:** Tutti i processi che appartengono a Gestione processi. Gestione processi gestisce i propri processi e dispone di propri stati. Consulta gli stati dei processi specifici descritti di seguito.

**Flusso di lavoro:** Tutti gli elementi di lavoro che appartengono all’esecuzione del flusso di lavoro. Il flusso di lavoro non gestisce i propri elementi di lavoro ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

**Eventi:** Tutti gli elementi di lavoro che appartengono a Gestione eventi. La gestione degli eventi non gestisce i propri elementi di lavoro ma si basa su Work Manager; pertanto, gli stati appartengono a Work Manager.

### Stato (solo per le categorie Predefinito, Flusso di lavoro o Eventi) {#status-for-default-workflow-or-events-categories-only}

**Mostra tutto:** Visualizza tutti gli elementi di lavoro correnti.

**Pianificato:** Visualizza tutti gli elementi di lavoro pronti per l&#39;esecuzione da parte del server applicazioni, ma non ancora avviati.

**In pausa:** Visualizza tutti gli elementi di lavoro programmati sospesi dall&#39;applicazione client. Questi elementi possono essere eseguiti o eliminati. Consultate Gestire gli elementi di lavoro o i job.

**In corso:** Visualizza tutti gli elementi di lavoro selezionati da Work Manager dell&#39;Application Server e completati o non riusciti. Non è possibile utilizzare operazioni su questi elementi di lavoro.

**Completato:** Visualizza tutti gli elementi di lavoro eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento dei callback ai gestori di callback. È possibile eliminare questi elementi utilizzando l&#39;operazione Elimina elementi. Consultate Gestire gli elementi di lavoro o i job.

**Non riuscito:** Visualizza tutti gli elementi di lavoro non completati correttamente a causa di una condizione di errore. Questi elementi di lavoro possono essere ritentati più volte utilizzando l&#39;operazione Riprova elementi. Consultate Gestire gli elementi di lavoro o i job. Un collegamento Errore nella colonna Stato consente di accedere ai dettagli sull&#39;errore.

**Sconosciuto:** Visualizza tutti gli elementi di lavoro con stato sconosciuto.

### Stato (solo per la categoria Responsabile del processo) {#status-for-job-manager-category-only}

**Completato:** Visualizza tutti i processi eseguiti correttamente. Gli elementi di lavoro persistenti rimangono in questo stato e gli elementi non persistenti vengono eliminati al completamento dei callback ai gestori di callback.

**Completo richiesto:** Visualizza i processi per i quali è stata effettuata una richiesta completa.

**Richiesta non riuscita:** Visualizza i processi per i quali è stata effettuata una richiesta non riuscita.

**Non riuscito:** Visualizza i processi non completati correttamente a causa di una condizione di errore. Un collegamento Errore nella colonna Stato consente di accedere ai dettagli sull&#39;errore.

**Termina richiesta:** Visualizza i processi per i quali è stata effettuata una richiesta di interruzione.

**Terminato:** Visualizza i processi terminati senza completamento.

**Sospensione richiesta:** Visualizza i processi per i quali è stata effettuata una richiesta di sospensione.

**Sospeso:** Visualizza i processi sospesi.

**Ripresa richiesta:** Visualizza i processi per i quali è stata effettuata una richiesta di ripresa.

**In coda:** Visualizza i processi presenti nella coda.

**In esecuzione:** Visualizza i processi in esecuzione.

### Nome server {#server-name}

Solo per i server cluster, selezionare il nome del nodo per visualizzare gli elementi di lavoro o di processo creati solo su tale server. Se si seleziona Mostra tutto, vengono visualizzati tutti gli elementi di lavoro per tutti i nodi di un cluster.

### Ora di creazione {#create-time}

Selezionare un&#39;opzione in questo filtro per visualizzare solo gli elementi di lavoro creati nell&#39;intervallo di tempo selezionato. Se ad esempio si seleziona 1 giorno, vengono visualizzati tutti gli elementi di lavoro creati entro 24 ore prima dell&#39;ora impostata nel filtro Precedente a.

### Prima di {#prior-to}

Imposta la data e l&#39;ora utilizzate dal filtro Ora di creazione come data di fine. Mantieni selezionata l’opzione Usa data e ora corrente per filtrare dalla data e dall’ora corrente, oppure deseleziona l’opzione e immetti i valori appropriati. Fare clic sulle icone del calendario o sull&#39;icona dell&#39;orologio per selezionare i valori utilizzando questi strumenti.

Se ad esempio si seleziona Crea ora = 1 giorno e Precedente a = Usa data e ora correnti, verranno restituiti tutti gli elementi di lavoro creati nelle ultime 24 ore.

>[!NOTE]
>
>In Oracli di distribuzioni di database, i filtri per l’intervallo di date (ovvero, Crea ora e Prima delle impostazioni) non funzionano in modo preciso. Utilizzare un altro filtro per recuperare gli elementi di lavoro.

## Informazioni sull&#39;interfaccia della scheda Gestione lavori {#about-the-work-manager-tab-interface}

Quando si esegue una query di Work Manager o si esegue un&#39;operazione su un elemento di lavoro o un job, sopra l&#39;elenco viene visualizzato un messaggio. Questo messaggio fornisce un feedback sull’azione avviata e, in alcuni casi, un collegamento Ulteriori informazioni per fornire i dettagli. Ad esempio, se l’operazione avviata non è riuscita, il messaggio viene visualizzato nello stesso modo e fornisce un collegamento per ottenere dettagli sull’errore.

Quando si fa clic su Ulteriori informazioni, nella finestra di dialogo Dettagli operazione viene visualizzato un elenco degli elementi di lavoro o dei processi selezionati durante l&#39;operazione. È possibile fare clic su ogni voce di elenco per visualizzare i dettagli errore nella parte inferiore della finestra di dialogo.

### Gestire gli elementi di lavoro o i processi {#manage-the-work-items-or-jobs}

1. Utilizzare gli strumenti di operazione descritti di seguito per gestire gli elementi di lavoro o i job nell&#39;elenco.

   >[!NOTE]
   >
   >Le operazioni sono disponibili a seconda dello stato dell’elemento.

   **Elimina elementi:** Elimina l&#39;elemento di lavoro o il processo selezionato.

   **Sospendi elementi:** Sospende l&#39;elemento di lavoro o il processo selezionato.

   **Riprendi elementi:** Riprende l&#39;elemento di lavoro o il processo selezionato dal relativo stato di pausa.

   **Riprova elementi:** Tenta di rieseguire l&#39;elemento di lavoro o il processo selezionato dal relativo stato corrente.

   Per verificare se un&#39;operazione è stata eseguita correttamente, fare clic su Ulteriori informazioni sopra l&#39;elenco. Viene visualizzata una finestra di dialogo contenente gli elementi di lavoro o i processi selezionati e i relativi stati.

## Informazioni aggiuntive sugli stati degli elementi di lavoro {#additional-information-about-work-item-statuses}

Una transizione di stato tipica per un elemento di lavoro è Nuovo > Programmato > In corso > Completo o Non riuscito.

Lo stato di pausa interrompe questo flusso normale. L&#39;applicazione client o l&#39;amministratore di sistema possono avviare questa interruzione (ad esempio, per la manutenzione o l&#39;aggiornamento). È possibile annullare questa azione utilizzando l&#39;operazione Riprendi per riportare l&#39;elemento di lavoro in uno stato Pianificato.

Un elemento di lavoro in stato Pianificato è in coda per l&#39;esecuzione non ancora iniziata. Questi elementi possono essere messi in pausa o eliminati oppure passeranno allo stato In corso quando Work Manager li rimuove dalla coda. Impossibile modificare gli elementi di lavoro in corso. Possono essere completate o non riuscite.

Lo stato Non riuscito è il risultato di una condizione di errore che si verifica durante l&#39;esecuzione dell&#39;elemento di lavoro. Se si sospetta che gli errori siano circostanziati (a causa del contesto al momento dell&#39;esecuzione), è possibile riprovare l&#39;esecuzione, rimettendo in coda l&#39;elemento di lavoro. È consentito solo un numero limitato di tentativi.
