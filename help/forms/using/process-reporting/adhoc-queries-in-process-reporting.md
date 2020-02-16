---
title: Query ad hoc in Process Reporting
seo-title: Query ad hoc in Process Reporting
description: Creazione di query personalizzate per la ricerca di AEM Forms su processi JEE e dettagli sulle attività in Process Reporting
seo-description: Creazione di query personalizzate per la ricerca di AEM Forms su processi JEE e dettagli sulle attività in Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Query ad hoc in Process Reporting{#ad-hoc-queries-in-process-reporting}

## Query ad hoc in Process Reporting {#ad-hoc-queries-in-process-reporting-1}

Query ad hoc in Process Reporting (Generazione di rapporti di processo) consentono di creare query personalizzate da utilizzare per cercare i dettagli di processo e attività relativi alle istanze di processo definite nell&#39;ambiente AEM Forms.

È inoltre possibile definire query ad hoc utilizzando i filtri di proprietà processo e attività. Questi filtri possono quindi essere salvati e utilizzati per eseguire i report in un secondo momento.

[**Ricerca **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)processo: Cercare le istanze di processo con un filtro di ricerca definito dall&#39;utente basato sugli attributi di processo.

[**Dettagli **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)processo: Visualizzare i dettagli di un&#39;istanza di processo specificando l&#39;ID del processo.

**Ricerca** attività: Cercare le istanze delle attività con un filtro di ricerca definito dall&#39;utente basato sugli attributi delle attività.

**Dettagli** attività: Visualizzare i dettagli di un&#39;istanza di attività specificando l&#39;ID attività.

### Processi e attività {#processes-and-tasks}

La procedura seguita per creare filtri ed eseguire query per i dettagli del processo è la stessa utilizzata per le attività.

Ciò significa che le interfacce utente per Process Search e Task Search differiscono solo nei campi che è possibile cercare e nei campi restituiti nei risultati della ricerca. Ciò è dovuto semplicemente al fatto che, sebbene molti campi siano identici, alcuni campi sono specifici dei processi e alcuni campi sono specifici delle attività.

In questo articolo vengono descritte le sezioni Processo/Ricerca attività e Dettagli processo/attività. Nei luoghi appropriati, eventuali differenze specifiche saranno richiamate in modo specifico.

## Ricerca processo/attività {#process-task-search}

È possibile utilizzare Process/Task Search per definire i filtri per la query delle istanze di processi/attività.

### Per creare una query di ricerca di processo/attività {#to-create-a-process-task-search-query}

1. Per visualizzare le query di ricerca di processi/attività salvate o per creare una query, fare clic su Query **ad hoc** , quindi fare clic su **Processo/Ricerca** attività.

   ![search_nodes](assets/search_nodes.png)

   Il pannello Filtri **** personali viene visualizzato a destra della struttura ad albero.

   Nel pannello **Filtri** personali, potete creare nuove query ad hoc e fare clic per eseguire le query salvate in precedenza.

   ![my_Filters_panel](assets/my_filters_panel.png)

1. Per eseguire una query esistente, è sufficiente fare clic sulla query nel pannello **Filtri** personali.
1. Per creare una query, fare clic su **Aggiungi** (+).

   Viene visualizzato il pannello **Crea filtro** .

   ![create_filter_panel](assets/create_filter_panel.png)

   Una query è costituita da uno o più filtri di query. Per creare un filtro, aggiungete una riga di filtro alla query. Per impostazione predefinita, alla query viene aggiunta una riga di filtro.

   **Definizione di un filtro**

   1. Selezionare un campo.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >L&#39;elenco dei campi contiene i campi specifici per il processo o l&#39;attività di AEM Forms.

   1. Selezionare una condizione.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >Le condizioni elencate dipendono dall&#39;attributo selezionato per il filtraggio.

   1. Immettere un valore.

      ![filter_value](assets/filter_value.png)

   1. Per aggiungere un altro filtro alla query, fare clic su **Aggiungi (+)** a destra della riga del filtro.

      Per rimuovere un filtro dalla query, fate clic su **Elimina (-)** a destra della riga del filtro.

      ![filter_add_del](assets/filter_add_del.png)

Dopo aver creato una query, utilizzate le opzioni nell’angolo superiore destro del pannello **Crea filtro** per:

* **Annulla**: Annulla le modifiche e torna al pannello **Filtri** personali.
* **Esegui**: Esegui la query corrente per visualizzare e/o verificare i risultati. In questo caso, non è necessario salvare la query prima di eseguire la query. È possibile verificare i risultati, apportare modifiche se necessario, quindi salvare la query quando si è soddisfatti dell&#39;output.
* **Salva**:Salvate il filtro. Il filtro può essere visualizzato ed eseguito dal pannello **Filtri** personali.

### Opzioni nel pannello Filtri personali {#options-in-my-filters-panel}

Utilizzate le opzioni nel pannello **Filtri** personali per **aggiungere** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **modificare** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)**** ![](assets/lc_pr_edit_filter.png), o eliminarelc_pr_edit_filteran ad hoc query.

![my_filter_options](assets/my_filters_options.png)

### Per eseguire una query di ricerca {#to-execute-a-search-query}

1. Per eseguire una query, fate clic sul filtro nel pannello **Filtri** personali o fate clic sul pulsante **Esegui** se state creando o modificando un filtro.
1. I risultati della query vengono visualizzati nel pannello **Rapporto** della finestra **Report** processo.

   ![process_search_result](assets/process_search_result.png)

   È possibile impaginare i risultati di ricerca con l’aiuto del pannello di impaginazione visualizzato nella parte inferiore del rapporto.

   ![process_result_png](assets/process_result_pgn.png)

   Nell’elenco a discesa **Visualizza** , scegliete il numero di risultati da visualizzare per pagina.

   Nella casella di testo **Pagina** , immettere un numero di pagina da inserire direttamente nella pagina.

1. In un risultato di Process Search vengono visualizzati i seguenti campi:

   * **ID** processo: ID del processo. Il campo è ipercollegato. Se fate clic su un ID processo in questo campo, verrete reindirizzati al pannello Dettagli **** processo relativo al processo.
   * **Iniziatore**: Utente di AEM Forms che ha avviato l’istanza di processo
   * **Ora** di creazione: Data e ora di inizio dell’istanza di processo
   * **Ora** completamento: Data e ora in cui è stata completata l&#39;istanza del processo
   * **Durata**: Durata dall’inizio al completamento dell’istanza di processo
   * **Stato**: Lo stato corrente dell&#39;istanza di processo.
   Per impostazione predefinita, il risultato è ordinato per ID processo. Tuttavia, per ordinare il risultato per uno dei campi, fare clic sul titolo del campo.

   Poiché l’ordinamento è un’operazione di attivazione/disattivazione, fate clic su un’intestazione di colonna per ordinare il risultato crescente e fate di nuovo clic su di esso per ordinare il risultato decrescente.

   Analogamente, i campi seguenti vengono visualizzati in un risultato di Ricerca attività:

   * **ID** attività: ID dell’attività. Il campo è ipercollegato. Se si fa clic su un ID attività in questo campo, si viene reindirizzati al pannello Dettagli **** attività per l&#39;attività.
   * **Iniziatore**: Utente di AEM Forms che ha avviato l’istanza di processo
   * **Ora** di creazione: Data e ora di inizio dell’istanza di processo
   * **Ora** completamento: Data e ora in cui è stata completata l&#39;istanza del processo
   * **Durata**: Durata dall’inizio al completamento dell’istanza di processo
   * **Stato**: Lo stato corrente dell&#39;istanza di processo.
   Per impostazione predefinita, il risultato è ordinato per ID attività. Tuttavia, per ordinare il risultato per uno dei campi, fare clic sul titolo del campo. Il risultato è ordinato in base alla colonna indicata da una freccia scura accanto all’intestazione della colonna.

   Poiché l’ordinamento è un’operazione di attivazione/disattivazione, fate clic su un’intestazione di campo per ordinare il risultato crescente e fate di nuovo clic su di esso per ordinare il risultato decrescente. L’ordine corrente (crescente/decrescente) è indicato dalla direzione della freccia scura accanto all’intestazione della colonna.

   ![task_search_result](assets/task_search_result.png)

1. Fate clic sul pulsante della barra laterale ![lc_pr_rail_button](assets/lc_pr_rail_button.png) in alto a sinistra per comprimere il riquadro Filtri **** personali ed espandere lo spazio disponibile per il pannello **Rapporto** .
1. Utilizzate le opzioni nell&#39;angolo superiore destro del pannello **Report **per eseguire operazioni sul risultato della query.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nello storage

   * **Esporta in CSV**: Esportate i dati del rapporto in un file separato da virgole.
   >[!NOTE]
   >
   >Quando esportate un rapporto, l’intero risultato della ricerca viene esportato in un file CSV e non solo nella pagina corrente

## Dettagli processo/attività {#process-task-details}

Il pannello Dettagli **** processo consente di visualizzare i dettagli di un processo specifico.

Allo stesso modo, potete utilizzare il pannello Dettagli **** attività per visualizzare i dettagli di una specifica attività.

### Visualizzazione dei dettagli processo/attività {#to-view-process-task-details}

È possibile visualizzare i dettagli di un&#39;attività o di un processo AEM Forms specifico:

* **Da un risultato di ricerca di processi/attività**
* **Immettendo l’ID processo/attività nel pannello Dettagli processo/attività**

#### Da un risultato di ricerca di processi/attività {#from-a-process-task-search-result}

1. Eseguire una ricerca di processo/attività. Per informazioni dettagliate, vedere [Esecuzione di una query](#to-execute-a-search-query)di ricerca dei processi.

   Si noti che gli ID del processo visualizzati e restituiti nel risultato sono collegati in modo ipertestuale.

   ![process_id_list](assets/process_id_list.png)

1. Fate clic su un ID processo nell’elenco per visualizzare i dettagli di questo processo nel pannello Dettagli **** processo.

   Il risultato della query **Processo/Dettagli** attività visualizza i dettagli delle attività/moduli contenuti nel processo/attività.

   Per impostazione predefinita, il risultato è ordinato per ID modulo/attività. Tuttavia, per ordinare il risultato per uno dei campi, fare clic sul titolo del campo. La colonna in base alla quale il risultato è ordinato è indicata da una freccia scura accanto all’intestazione della colonna.

   Poiché l’ordinamento è un’operazione di attivazione/disattivazione, fate clic su un’intestazione di campo per ordinare il risultato crescente e fate di nuovo clic su di esso per ordinare il risultato decrescente. L’ordine corrente (crescente/decrescente) è indicato dalla direzione della freccia scura accanto all’intestazione della colonna.

   **Risultato dettagli processo**

   ![process_details](assets/process_details.png)

   **** Pannello sinistro: Visualizza i seguenti dettagli del processo selezionato:

   * Nome del processo
   * Ora data creazione processo
   * Ora completamento processo
   * Durata processo
   * Stato processo
   * Iniziatore processo
   **** Pannello superiore destro: Visualizza i dettagli seguenti delle attività che compongono il processo selezionato:

   * ID attività
   * Nome attività
   * Proprietario attività
   * Data creazione attività
   * Ora aggiornamento attività
   * Ora completamento attività
   * Durata attività
   * Stato attività
   **** Pannello inferiore destro: Visualizza i seguenti dettagli della cronologia del processo selezionato:

   * Nome processo
   * Iniziatore processo
   * Ora data aggiornamento processo
   * Ora completamento processo
   * Stato processo
   **Risultato dettagli attività**

   ![task_details](assets/task_details.png)

   **** Pannello sinistro: Visualizza i dettagli seguenti dell&#39;attività selezionata:

   * Nome attività
   * ID processo a cui appartiene l&#39;attività
   * Descrizione attività
   * Data creazione attività
   * Ora completamento attività
   * Durata attività
   * Stato attività
   * Ciclo di attività selezionato
   **** Pannello superiore destro: Visualizza i dettagli seguenti dei moduli che compongono l&#39;attività selezionata:

   * ID modulo
   * Ora data creazione modulo
   * Ora data aggiornamento modulo
   * URL modello modulo
   **** Pannello inferiore destro: Visualizza i dettagli seguenti della cronologia del processo dell&#39;attività selezionata:

   * Tipo assegnazione task
   * Proprietario attività
   * Data creazione assegnazione attività
   * Ora aggiornamento attività






1. Fare clic su **Torna a Ricerca** processo/attività per tornare al risultato della ricerca dal quale sono stati trascinati i dettagli processo/attività.

   ![back_to_search](assets/back_to_search.png)

   Tuttavia, se i dettagli processo/attività sono stati trovati immettendo un ID processo/attività specifico, facendo clic su Torna a Ricerca processo/attività si torna a Ricerca **processo/attività**, senza visualizzare alcun risultato di ricerca.

#### Immettendo l’ID processo/attività nel pannello Dettagli processo/attività {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vai al pannello **Dettagli** processo/attività.

   ![details_nodes](assets/details_nodes.png)

1. Nella casella di testo ID processo/attività, immettere l&#39;ID processo/attività.

   ![process_details-1](assets/process_details-1.png)

   I campi del risultato della query **Processo/Dettagli** attività sono campi specifici di un processo/attività AEM Forms.

   Per un processo, il risultato della query visualizza i dettagli delle attività contenute nel processo.

   Per un&#39;attività, il risultato della query visualizza i dettagli dei moduli contenuti nell&#39;attività.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
