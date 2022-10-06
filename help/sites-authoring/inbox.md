---
title: Casella in entrata
seo-title: Your Inbox
description: Gestione delle attività con la casella in entrata
seo-description: Managing your tasks with the inbox
uuid: ddd48019-ce69-4a47-be2b-5b66ae2fe3c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8b607b55-2412-469f-856b-0a3dea4b0efb
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 77%

---

# Casella in entrata  {#your-inbox}

Puoi ricevere notifiche da diverse aree di AEM, inclusi flussi di lavoro e progetti; ad esempio, informazioni su:

* Attività:

   * possono essere create anche in diversi punti nell’interfaccia di AEM, ad esempio in **Progetti**;
   * possono essere il prodotto del passaggio **Crea attività** o **Crea attività per progetto** di un flusso di lavoro.

* Flussi di lavoro:

   * elementi di lavoro che rappresentano le azioni da eseguire sul contenuto di una pagina;

      * sono il prodotto dei passaggi **Partecipante** di un flusso di lavoro;
   * elementi con errori, per consentire agli amministratori di ripetere il passaggio non riuscito.


Queste notifiche arrivano nella casella in entrata, dove puoi visualizzarle e intraprendere le azioni necessarie.

>[!NOTE]
>
>AEM viene fornito con attività amministrative preconfigurate assegnate al gruppo degli utenti amministratore. Consulta le [Attività amministrative pronte all&#39;uso](#out-of-the-box-administrative-tasks) per i dettagli.

>[!NOTE]
>
>Per ulteriori informazioni sui tipi di elementi vedi anche:
>
>* [Progetti](/help/sites-authoring/touch-ui-managing-projects.md)
>* [Progetti: lavorare con le attività](/help/sites-authoring/task-content.md) 
>* [Flussi di lavoro](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/home.md)
>


## Casella in entrata nell’intestazione {#inbox-in-the-header}

Per le varie console, il numero corrente di elementi nella casella in entrata è riportato nell’intestazione. Mediante questo indicatore è possibile accedere rapidamente alle pagine che richiedono interventi o alla casella in entrata:

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>Alcune azioni sono anche visualizzate nella [vista a schede della relativa risorsa](/help/sites-authoring/basic-handling.md#card-view).

## Attività amministrative pronte all&#39;uso  {#out-of-the-box-administrative-tasks}

AEM pronto all&#39;uso è precaricato con quattro attività assegnate al gruppo di utenti amministratore.

* [Configura Analytics e Targeting](/help/sites-administering/opt-in.md)
* [Applica elenco di controllo sicurezza AEM](/help/sites-administering/security-checklist.md)
* Abilita raccolta di statistiche di utilizzo aggregati
* [Configura HTTPS](/help/sites-administering/ssl-by-default.md)

## Apertura della casella in entrata  {#opening-the-inbox}

Per aprire la casella in entrata delle notifiche AEM:

1. Tocca o fai clic sull’indicatore nella barra degli strumenti.

1. Seleziona **Visualizza tutto**. Viene aperta la **Casella in entrata AEM**. La casella in entrata mostra gli elementi dei flussi di lavoro, delle attività e dei progetti.
1. La vista predefinita è [Vista elenco](#inbox-list-view), ma puoi anche passare alla [Vista calendario](#inbox-calendar-view). Questa operazione viene effettuata con il selettore vista (barra degli strumenti, in alto a destra).

   Per entrambe le viste puoi inoltre definire le [Visualizza impostazioni](#inbox-view-settings); le opzioni disponibili dipendono dalla vista corrente.

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>La casella in entrata funziona come una console; puoi quindi utilizzare le funzioni di [Navigazione globale](/help/sites-authoring/basic-handling.md#global-navigation) o [Ricerca](/help/sites-authoring/search.md) per passare a un’altra posizione al termine dell’operazione.

### Casella in entrata - Vista a elenco {#inbox-list-view}

Questa vista mostra tutti gli elementi con le relative informazioni chiave:

![wf-82](assets/wf-82.png)

### Casella in entrata - Vista calendario {#inbox-calendar-view}

Questa vista mostra gli elementi in base alla loro posizione nel calendario e alla visualizzazione precisa selezionata:

![wf-93](assets/wf-93.png)

Operazioni disponibili:

* selezionare una vista specifica: **Timeline**,**Colonna**, **Elenco**

* specificare le attività da visualizzare in base a **Programma**; **Tutto**, **Pianificato**, **In corso**, **In scadenza**, **Scaduto**

* approfondire per ottenere informazioni più dettagliate su un elemento
* selezionare un intervallo di date per restringere la visualizzazione:

![wf-91](assets/wf-91.png)

### Casella in entrata - Impostazioni {#inbox-view-settings}

Puoi definire le impostazioni per entrambe le viste (Elenco e Calendario):

* **Vista calendario**

   Per la **Vista calendario** puoi configurare:

   * **Raggruppa per**
   * **Pianificazione** o **Nessuna**
   * **Dimensioni scheda**

   ![wf-92](assets/wf-92.png)

* **Vista a elenco**

   Per la **Vista a elenco** puoi configurare il metodo di ordinamento:

   * **Campo di ordinamento**
   * **Ordinamento**

   ![wf-83](assets/inbox-settings.png)

### Casella in entrata - Controllo amministratore {#inbox-admin-control}

L’opzione Controllo amministratore consente agli amministratori di:

* Personalizzare le colonne della casella in entrata AEM

* Personalizzare il testo e il logo dell’intestazione

* Controllare la visualizzazione dei collegamenti di navigazione disponibili nell&#39;intestazione

L’opzione Controllo amministratore è visibile solo ai membri del gruppo `administrators` o `workflow-administrators` gruppo.

* **Personalizzazione colonna**: Personalizza una casella in entrata AEM per modificare il titolo predefinito di una colonna, riordinare la posizione di una colonna e visualizzare colonne aggiuntive in base ai dati di un flusso di lavoro.
   * **Aggiungi colonna**: Selezionare una colonna da aggiungere AEM casella in entrata.
   * **Modifica colonna**: Passa il puntatore del mouse sul titolo della colonna e tocca ![modifica](assets/edit.svg) per immettere un nome visualizzato per la colonna.
   * **Elimina colonna**: Tocca ![delete](assets/delete_updated.svg) per eliminare la colonna AEM casella in entrata.
   * **Sposta colonna**: Trascina ![spostare](assets/move_updated.svg) per spostare una colonna in una nuova posizione in AEM casella in entrata.

   ![admin-control](assets/admin-control-column-customize.png)

* **Personalizzazione branding**

   * **Personalizza il testo dell’intestazione:** Specifica il testo da visualizzare nell’intestazione per sostituire il valore predefinito **Adobe Experience Manager** testo.

   * **Personalizza logo:** Specifica l’immagine da visualizzare nell’intestazione come logo. Carica un’immagine in Digital Asset Management (DAM) e fai riferimento a tale immagine nel campo .

* **Navigazione utente**
   * **Nascondi opzioni di navigazione:** Seleziona questa opzione per nascondere le opzioni di navigazione disponibili nell’intestazione. Le opzioni di navigazione includono collegamenti ad altre soluzioni, collegamento Aiuto e opzioni di authoring disponibili quando si tocca il logo o il testo di Adobe Experience Manager.
* **Salva:** Tocca o fai clic su questa opzione per salvare le impostazioni.

## Intervenire su un elemento {#taking-action-on-an-item}

>[!NOTE]
>
>Sebbene sia possibile selezionare più elementi, le azioni possono essere eseguite solo su un elemento alla volta.


1. Per intervenire su un elemento, seleziona la miniatura dell’elemento appropriato. Le icone per le azioni applicabili per l’elemento in questione sono disponibili nella barra degli strumenti:

   ![wf-84](assets/wf-84.png)

   Le azioni dipendono dall’elemento selezionato e includono:

   * **Completa** l’azione; ad esempio, un&#39;attività o un elemento di flusso di lavoro.
   * **Riassegna**/**Delega** un elemento.
   * **Apri** un elemento; a seconda del tipo di elemento, questa azione può:

      * mostrare le proprietà dell&#39;elemento
      * aprire un dashboard o una procedura guidata per ulteriori azioni
      * aprire la documentazione correlata
   * **Indietro** per tornare a un passaggio precedente.
   * Visualizzazione del payload di un flusso di lavoro.
   * Creazione di un progetto dall’elemento.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta:
   >
   >* Elementi di flussi di lavoro - [Partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md)


1. A seconda dell’elemento selezionato, verrà avviata un’azione; ad esempio:

   * Viene aperta la finestra di dialogo relativa all’azione.
   * Viene avviata un’azione guidata.
   * Viene aperta una pagina della documentazione.

   Ad esempio, selezionando **Riassegna** viene aperta una finestra di dialogo:

   ![wf-85](assets/wf-85.png)

   A seconda della finestra di dialogo, procedura guidata o pagina di documentazione aperta, è possibile:

   * Confermare l’azione appropriata; ad es. Riassegna.
   * Annullare l’azione.
   * Freccia indietro; ad esempio, se è stata aperta una procedura guidata per un’azione o una pagina della documentazione, puoi tornare alla casella in entrata.


## Creazione di un’attività {#creating-a-task}

Dalla casella in entrata è possibile creare le attività:

1. Seleziona **Crea**, quindi **Attività**.
1. Compila i campi richiesti nelle schede **Base** e **Avanzate**; solo il **Titolo** è obbligatorio, tutti gli altri campi sono facoltativi:

   * **Base**:

      * **Titolo**
      * **Progetto**
      * **Assegnatario**
      * **Contenuto**; simile a Payload, si tratta di un riferimento dall&#39;attività a una posizione nell’archivio
      * **Descrizione**
      * **Priorità attività**
      * **Data iniziale**
      * **Data di scadenza**

   ![wf-86](assets/wf-86.png)

   * **Avanzate**

      * **Nome**: verrà utilizzato per formare l’URL; se vuoto, verrà basato sul **Titolo**.

   ![wf-87](assets/wf-87.png)

1. Seleziona **Invia**.

## Creazione di un progetto  {#creating-a-project}

Per determinate attività, puoi creare un [Progetto](/help/sites-authoring/projects.md) basato su tale attività:

1. Seleziona l’attività appropriata toccando o facendo clic sulla miniatura.

   >[!NOTE]
   >
   >Per creare un progetto, è possibile utilizzare solo le attività create con l’opzione **Crea** della **Casella in entrata**.
   >
   >Gli elementi di lavoro (da un flusso di lavoro) non possono essere utilizzati per creare un progetto.

1. Dalla barra degli strumenti, seleziona **Crea progetto** per aprire la procedura guidata.
1. Seleziona il modello appropriato, quindi **Avanti**.
1. Specifica le proprietà richieste:

   * **Base**

      * **Titolo**
      * **Descrizione**
      * **Data iniziale**
      * **Data di scadenza**
      * **Utente** e ruolo
   * **Avanzate**

      * **Nome**
   >[!NOTE]
   >
   >Per maggiori informazioni, consulta [Creazione di un progetto](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project).

1. Seleziona **Crea** per confermare l’azione.

## Filtrare gli elementi nella Casella in entrata AEM {#filtering-items-in-the-aem-inbox}

Puoi filtrare gli elementi elencati:

1. Apri la **Casella in entrata AEM**.

1. Apri il selettore del filtro:

   ![wf-88](assets/wf-88.png)

1. Puoi filtrare gli elementi elencati in base a diversi criteri, molti dei quali possono essere regolati; ad esempio:

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >Con [Impostazioni vista](#inbox-view-settings) è anche possibile configurare l’ordinamento quando si utilizza la [Vista a elenco](#inbox-list-view).
