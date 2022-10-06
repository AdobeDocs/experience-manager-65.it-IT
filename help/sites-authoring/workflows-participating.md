---
title: Partecipazione ai flussi di lavoro
seo-title: Participating in Workflows
description: I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa.
seo-description: Workflows typically include steps that require a person to perform an activity on a page or asset.
uuid: 15d56bcc-1e84-4cc0-8b71-7fb906cd7ff7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: f170613c-329e-446b-9ac3-350615f1bfb6
docset: aem65
exl-id: e47270e8-bace-4d0f-a088-7269b6356315
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 98%

---

# Partecipazione ai flussi di lavoro{#participating-in-workflows}

I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo che esegua l’attività e assegna loro un elemento di lavoro. L&#39;utente riceve la notifica e intraprende l&#39;azione appropriata:

* [Visualizzazione delle notifiche](#notifications-of-available-workflow-actions)
* [Completa un Passaggio Partecipante](#completing-a-participant-step)
* [Delega un Passaggio Partecipante](#delegating-a-participant-step)
* [Esegui un passo indietro su un Passaggio Partecipante](#performing-step-back-on-a-participant-step)
* [Apri un elemento del flusso di lavoro per visualizzare i dettagli (e Intraprendere Azioni)](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualizza il Payload flusso di lavoro (Risorse Multiple)](#viewing-the-workflow-payload-multiple-resources)

## Notifiche delle Azioni disponibili per il Flusso di lavoro {#notifications-of-available-workflow-actions}

Quando ti viene assegnato un elemento di lavoro (ad esempio, **Approva contenuto**) vengono visualizzati diversi avvisi e/o notifiche:

* L&#39;indicatore di [notifica](/help/sites-authoring/inbox.md) (barra degli strumenti) indica un numero incrementato di uno:

   ![](do-not-localize/wf-57.png)

* L&#39;oggetto viene inserito nelle notifiche della [Casella in entrata](/help/sites-authoring/inbox.md):

   ![wf-58](assets/wf-58.png)

* Quando utilizzi l&#39;Editor pagina, la barra di stato mostra:

   * Il nome dei flussi di lavoro applicati alla pagina, come ad esempio Richiedi attivazione.
   * Qualsiasi azione disponibile per l&#39;utente nella fase corrente del flusso di lavoro, per esempio: Completa, Delega, Visualizza dettagli.
   * Il numero di flussi di lavoro a cui è soggetta la pagina. Operazioni disponibili:

      * utilizzare la freccia sinistra/destra per navigare tra le informazioni di stato dei vari flussi di lavoro.
      * fare clic/toccare il numero totale per aprire un elenco a discesa di tutti i flussi di lavoro applicabili e quindi selezionare il flusso di lavoro che si desidera visualizzare nella barra di stato.

   ![wf-59](assets/wf-59.png)

   >[!NOTE]
   >
   >La barra di stato è visibile solo agli utenti con i privilegi del flusso di lavoro, per esempio, i membri del gruppo `workflow-users`.
   >
   >
   >Le azioni vengono visualizzate quando l&#39;utente è direttamente coinvolto nella fase corrente del flusso di lavoro.

* Quando la **Timeline** è aperta per la risorsa, verrà mostrato il passo del flusso di lavoro. Quando si fa clic o si tocca il banner di avviso, vengono anche visualizzate le azioni disponibili:

   ![screen-shot_2019-03-05at120453](assets/screen-shot_2019-03-05at120453.png)

### Completamento di un passaggio partecipante {#completing-a-participant-step}

Quando si completa un elemento di lavoro, il flusso di lavoro procede al passaggio successivo.

Per questa azione è possibile indicare:

* **Passaggio successivo**: il passaggio successivo da compiere (è possibile selezionarlo da un elenco)
* **Commento**: se necessario

È possibile completare un passaggio partecipante a partire da:

* [Casella in entrata](#completing-a-participant-step-inbox)
* [Editor pagina](#completing-a-participant-step-page-editor)
* [Timeline ](#completing-a-participant-step-timeline)
* all&#39;[apertura di un elemento del flusso di lavoro per visualizzarne i dettagli](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Completare un Passaggio partecipante: Casella in entrata {#completing-a-participant-step-inbox}

Utilizza la seguente procedura per completare l’elemento di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-authoring/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Seleziona **Completa** dalla barra degli strumenti.
1. Si apre la finestra di dialogo **Completa elemento di lavoro**. Seleziona il **Passaggio successivo** dal menu a discesa e aggiungi un **Commento** se richiesto.
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Annulla** per interrompere l’azione).

#### Completare un Passaggio partecipante: Editor pagina {#completing-a-participant-step-page-editor}

Utilizza la seguente procedura per completare l’elemento di lavoro:

1. Apri la [pagina da modificare](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleziona **Completa** dalla barra di stato in alto.
1. Si apre la finestra di dialogo **Completa elemento di lavoro**. Seleziona il **Passaggio successivo** dal menu a discesa e aggiungi un **Commento** se richiesto.
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Cancel** per interrompere l’azione).

#### Completare un Passaggio partecipante: Timeline {#completing-a-participant-step-timeline}

È possibile utilizzare la timelineper completare un passaggio e avanzare:

1. Seleziona la pagina richiesta e apri la **Timeline** (oppure, apri la **Timeline** e seleziona la pagina):

   ![screen-shot_2019-03-05at120744](assets/screen-shot_2019-03-05at120744.png)

1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Avanti**:

   ![screen-shot_2019-03-05at120453-1](assets/screen-shot_2019-03-05at120453-1.png)

1. A seconda del flusso di lavoro, è possibile selezionare la fase successiva:

   ![screen-shot_2019-03-05at120905](assets/screen-shot_2019-03-05at120905.png)

1. Seleziona **Avanti** per confermare l&#39;azione.

### Delega di un passaggio partecipante {#delegating-a-participant-step}

Se ti è stato assegnato un passaggio, ma per qualche motivo non ti è possibile procedere, puoi delegarlo a un altro utente o gruppo.

Gli utenti disponibili per la delega dipendono dal tipo di assegnatario:

* Se l’elemento di lavoro è stato assegnato a un gruppo, sono disponibili i membri del gruppo.
* Se l’elemento di lavoro è stato assegnato a un gruppo e poi è stato delegato a un utente, sono disponibili i membri del gruppo e il gruppo.
* Se l&#39;elemento di lavoro è stato assegnato a un singolo utente, l’elemento di lavoro non può essere delegato.

Per questa azione è possibile indicare:

* **Utente**: l&#39;utente a cui si vuole delegare. È possibile scegliere da un elenco
* **Commento**: se necessario

È possibile delegare un passaggio partecipante a partire da:

* [Casella in entrata](#delegating-a-participant-step-inbox)
* [Editor pagina](#delegating-a-participant-step-page-editor)
* [Timeline ](#delegating-a-participant-step-timeline)
* all&#39;[apertura di un elemento del flusso di lavoro per visualizzarne i dettagli](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegare un Passaggio partecipante: Casella in entrata {#delegating-a-participant-step-inbox}

Segui la procedura seguente per delegare un elemento di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-authoring/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Seleziona **Delega** dalla barra degli strumenti.
1. Viene aperta una finestra di dialogo. Specifica l’**Utente** dal menu a discesa (può anche essere un gruppo) e aggiungi un **Commento** se necessario. 
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Annulla** per interrompere l’azione).

#### Delegare un Passaggio partecipante: Editor pagina {#delegating-a-participant-step-page-editor}

Segui la procedura seguente per delegare un elemento di lavoro:

1. Apri la [pagina da modificare](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleziona **Delega** dalla barra di stato in alto.
1. Viene aperta una finestra di dialogo. Specifica l’**Utente** dal menu a discesa (può anche essere un gruppo) e aggiungi un **Commento** se necessario. 
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Annulla** per interrompere l’azione).

#### Delegare un Passaggio partecipante: Timeline {#delegating-a-participant-step-timeline}

È anche possibile utilizzare la timeline per delegare e/o assegnare un passaggio:

1. Seleziona la pagina richiesta e apri la **Timeline** (oppure, apri la **Timeline** e seleziona la pagina).
1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Cambia assegnatario**:

   ![screen-shot_2019-03-05at120453-2](assets/screen-shot_2019-03-05at120453-2.png)

1. Specifica un nuovo assegnatario:

   ![screen-shot_2019-03-05at121025](assets/screen-shot_2019-03-05at121025.png)

1. Seleziona **Assegna** per confermare l’azione.

### Tornare indietro di un passaggio {#performing-step-back-on-a-participant-step}

Se devi ripetere un passaggio o una serie di passaggi, puoi tornare indietro. Puoi quindi selezionare un passaggio precedente nel flusso di lavoro, per rielaborarlo. Il flusso di lavoro torna al passaggio specificato e procede da tale punto.

Per questa azione è possibile indicare:

* **Passaggio precedente:** il passaggio da cui si vuole ripartire. È possibile selezionarlo da un elenco.
* **Commento**: se necessario

È possibile eseguire un passo indietro su un passaggio partecipante a partire da:

* [Casella in entrata](#performing-step-back-on-a-participant-step-inbox)
* [Editor pagina](#performing-step-back-on-a-participant-step-page-editor)
* [Timeline ](#performing-step-back-on-a-participant-step-timeline)
* all&#39;[apertura di un elemento del flusso di lavoro per visualizzarne i dettagli](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Eseguire un passo indietro su un Passaggio partecipante: Casella in entrata {#performing-step-back-on-a-participant-step-inbox}

Utilizza la seguente procedura per fare un passo indietro:

1. Apri la **[Casella in entrata AEM](/help/sites-authoring/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Seleziona **Passo indietro** per aprire la finestra di dialogo.

1. Specifica il **Passaggio precedente** e aggiungi un **Commento** se necessario.
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Annulla** per interrompere l’azione).

#### Eseguire un passo indietro su un Passaggio partecipante: Editor pagina {#performing-step-back-on-a-participant-step-page-editor}

Utilizza la seguente procedura per fare un passo indietro:

1. Apri la [pagina da modificare](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleziona **Passo indietro** dalla barra di stato in alto.
1. Specifica il **Passaggio precedente** e aggiungi un **Commento** se necessario.
1. Utilizza il tasto **OK** per completare il passaggio (o il tasto **Annulla** per interrompere l’azione).

#### Eseguire un passo indietro su un Passaggio partecipante: Timeline {#performing-step-back-on-a-participant-step-timeline}

È anche possibile utilizzare la timeline per tornare a un passaggio precedente:

1. Seleziona la pagina richiesta e apri la **Timeline** (oppure, apri la **Timeline** e seleziona la pagina).
1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Ripristina versione precedente**:

   ![screen-shot_2019-03-05at121131](assets/screen-shot_2019-03-05at121131.png)

1. Specifica il passaggio precedente a cui il flusso di lavoro deve tornare:

   ![screen-shot_2019-03-05at121158](assets/screen-shot_2019-03-05at121158.png)

1. Seleziona **Ripristina versione precedente** per confermare l’azione.

### Aprire un elemento del flusso di lavoro per visualizzare i dettagli (e Intraprendere Azioni) {#opening-a-workflow-item-to-view-details-and-take-actions}

Visualizzare i dettagli dell&#39;elemento del flusso di lavoro e intraprendere le azioni appropriate.

I dettagli del flusso di lavoro vengono visualizzati in schede e le relative azioni appropriate sono disponibili nella barra degli strumenti:

* Scheda **ELEMENTO DI LAVORO:**

   ![wf-72](assets/wf-72.png)

* Scheda **INFORMAZIONI SUL FLUSSO DI LAVORO**:

   ![wf-73](assets/wf-73.png)

   Se per il modello sono stati configurati gli [Stadi del Flusso di lavoro](/help/sites-developing/workflows.md#workflow-stages), è possibile visualizzare lo stato di avanzamento in base a questi:

   ![wf-107](assets/wf-107.png)

* Scheda **COMMENTI**:

   ![wf-75](assets/wf-75.png)

È possibile aprire i dettagli dell&#39;elemento di lavoro in uno a partire da:

* [Casella in entrata](#performing-step-back-on-a-participant-step-inbox)
* [Editor pagina](#performing-step-back-on-a-participant-step-page-editor)

#### Aprire dei dettagli del flusso di lavoro: Casella in entrata {#opening-workflow-details-inbox}

Per aprire un elemento del flusso di lavoro e visualizzare i dettagli:

1. Apri la **[Casella in entrata AEM](/help/sites-authoring/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Seleziona **Apri** per aprire le schede informative.

1. Se necessario, seleziona l’azione appropriata, inserisci tutte le informazioni richieste e conferma con **OK** (o **Annulla**).
1. Usa il comando **Salva** o **Annulla** per uscire.

#### Apertura dei dettagli del flusso di lavoro: Editor pagina {#opening-workflow-details-page-editor}

Per aprire un elemento del flusso di lavoro e visualizzare i dettagli:

1. Apri la [pagina da modificare](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing).
1. Seleziona **Visualizza dettagli** dalla barra di stato per aprire le schede informative.

1. Se necessario, seleziona l’azione appropriata, inserisci tutte le informazioni richieste e conferma con **OK** (o **Annulla**).
1. Usa il comando **Salva** o **Annulla** per uscire.

### Visualizzare il Payload flusso di lavoro (Risorse Multiple) {#viewing-the-workflow-payload-multiple-resources}

È possibile visualizzare i dettagli del carico utile associato al singolo flusso di lavoro. All&#39;inizio vengono visualizzate le risorse nel pacchetto. È possibile, poi, scorrere per visualizzare le singole pagine.

Per visualizzare il carico utile e le risorse del singolo flusso di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-authoring/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Seleziona **Visualizza payload** dalla barra degli strumenti per aprire la finestra di dialogo.

   Poiché un pacchetto di flusso di lavoro è semplicemente un insieme di puntatori ai percorsi all&#39;interno della libreria, è possibile aggiungere, rimuovere e modificare le voci qui indicate per regolare i riferimenti del pacchetto del flusso di lavoro. Usa il componente **Definizione risorsa** per aggiungere nuove voci.

   ![wf-78](assets/wf-78.png)

1. I link possono essere usati per aprire le singole pagine.
