---
title: Gestione di applicazioni e attività per moduli in AEM Inbox
seo-title: Gestione di applicazioni e attività per moduli in AEM Inbox
description: AEM Inbox consente di avviare flussi di lavoro incentrati su Forms inviando applicazioni e gestendo attività.
seo-description: AEM Inbox consente di avviare flussi di lavoro incentrati su Forms inviando applicazioni e gestendo attività.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Gestione di applicazioni e attività per moduli in AEM Inbox{#manage-forms-applications-and-tasks-in-aem-inbox}

Uno dei molti modi per avviare o attivare un flusso di lavoro incentrato sui moduli è tramite le applicazioni in AEM Inbox. Per rendere disponibile un flusso di lavoro Forms come applicazione in Casella in entrata, è necessario creare un&#39;applicazione per il flusso di lavoro. Per ulteriori informazioni sull&#39;applicazione del flusso di lavoro e altri modi per avviare flussi di lavoro Forms, vedere [Avviare un flusso di lavoro incentrato sui moduli in OSGi](../../forms/using/aem-forms-workflow.md#launch).

Inoltre, AEM Inbox consolida le notifiche e le attività da vari componenti AEM, compresi i flussi di lavoro per Forms. Quando viene attivato un flusso di lavoro dei moduli contenente un passaggio dell&#39;attività Assegna, l&#39;applicazione associata viene elencata come un&#39;attività nella Casella in entrata dell&#39;assegnatario. Se l’assegnatario è un gruppo, l’attività viene visualizzata nella Casella in entrata di tutti i membri del gruppo fino a quando un singolo chiede o delega l’attività.

L&#39;interfaccia utente Inbox fornisce le viste elenco e calendario per visualizzare le attività. Potete anche configurare le impostazioni di visualizzazione. Potete filtrare le attività in base a vari parametri. Per ulteriori informazioni su visualizzazione e filtri, vedere [Casella in entrata](/help/sites-authoring/inbox.md).

In sintesi, Inbox consente di creare una nuova applicazione e di gestire le attività assegnate.

>[!NOTE] {graybox=&quot;true&quot;}
>
>Per poter utilizzare AEM Inbox, dovete far parte del gruppo di utenti del flusso di lavoro.

## Creare l&#39;applicazione {#create-application}

1. Andate alla Casella in entrata AEM all&#39;indirizzo https://[server]:[porta]/aem/inbox.
1. Nell’interfaccia utente Inbox, toccate **[!UICONTROL Crea > Applicazione]**. Viene visualizzata la pagina Seleziona applicazione.
1. Selezionate un’applicazione e fate clic su **[!UICONTROL Crea]**. Viene aperto il modulo adattivo associato all&#39;applicazione. Compila le informazioni nel modulo adattivo e tocca **[!UICONTROL Invia]**. Avvia il flusso di lavoro associato e crea un&#39;attività nella Casella in entrata dell&#39;assegnatario.

## Gestione attività {#manage-tasks}

Quando si attiva un flusso di lavoro Forms e si è assegnatari o membri del gruppo assegnatari, nella Casella in entrata viene visualizzata un&#39;attività. È possibile visualizzare i dettagli dell&#39;attività ed eseguire le azioni disponibili sull&#39;attività dall&#39;interno di Casella in entrata.

### Attività di attestazione o delegata {#claim-or-delegate-tasks}

Le attività assegnate a un gruppo vengono visualizzate nella casella in entrata di tutti i membri del gruppo. Qualsiasi membro del gruppo può reclamare tale attività o delegarla a un altro membro del gruppo. A questo scopo:

1. Toccate per selezionare la miniatura dell’attività. Le opzioni per aprire o delegare l’attività vengono visualizzate nella parte superiore.

   ![select-task](assets/select-task.png)

1. Effettua una delle operazioni seguenti:

   * Per delegare l&#39;attività, toccate **[!UICONTROL Delega]**. Si Apre La Finestra Di Dialogo Delega Elemento. Selezionate un utente, aggiungete eventualmente un commento e toccate **[!UICONTROL OK]**.
   ![delegate](assets/delegate.png)

   * Per attivare l’attività, toccate **[!UICONTROL Apri]**. Viene visualizzata la finestra di dialogo Assegna a se stesso. Toccate **[!UICONTROL Procedi]** per attivare l’attività. L’attività richiesta viene visualizzata insieme all’utente come assegnatario nella Casella in entrata.
   ![reclamo](assets/claim.png)

### Visualizzazione dei dettagli ed esecuzione di azioni sulle attività {#view-details-and-perform-actions-on-tasks}

Quando si apre un&#39;attività, è possibile visualizzare i dettagli dell&#39;attività ed eseguire le azioni disponibili. Le azioni disponibili per un&#39;attività sono definite nel passaggio attività Assegna del flusso di lavoro Forms associato.

1. Toccate per selezionare la miniatura dell’attività. Le opzioni per aprire o delegare l&#39;attività selezionata vengono visualizzate nella parte superiore.
1. Toccate **Apri** per visualizzare i dettagli delle attività e intervenire. Viene visualizzata la visualizzazione dettagliata delle attività. In questa visualizzazione è possibile visualizzare i dettagli dell&#39;attività e intervenire sull&#39;attività.

   >[!NOTE]
   >
   >Se un&#39;attività è assegnata a un gruppo, è necessario dichiararla in grado di aprirla in visualizzazione dettagliata.

![task-details](assets/task-details.png)

La visualizzazione dettagliata delle attività comprende le seguenti sezioni:

* Dettagli attività
* Modulo
* Dettagli del flusso di lavoro
* Azioni, barra degli strumenti

#### Task details {#task-details}

Nella sezione Dettagli attività sono visualizzate informazioni sull&#39;attività. Le informazioni visualizzate dipendono dalle impostazioni di configurazione del passaggio [Attività](/help/sites-developing/workflows-step-ref.md) Assegna nel flusso di lavoro. Nell&#39;esempio riportato sopra vengono visualizzati la descrizione, lo stato, la data di inizio e il flusso di lavoro utilizzati per l&#39;attività. Consente inoltre di allegare un file all&#39;attività.

#### Modulo {#form}

La scheda Modulo nell&#39;area di contenuto principale visualizza il modulo inviato e gli eventuali allegati a livello di campo.

#### Workflow details {#workflow-details}

La scheda Dettagli flusso di lavoro nella parte superiore mostra l’avanzamento dell’attività nelle varie fasi del flusso di lavoro. Mostra le fasi completate, correnti e in sospeso per l&#39;attività. Le fasi di un flusso di lavoro sono definite nel passaggio [attività](/help/sites-developing/workflows-step-ref.md) Assegna del flusso di lavoro associato.

Inoltre, nella scheda viene visualizzata la cronologia delle attività per ogni fase completata del flusso di lavoro. Toccate **[!UICONTROL Visualizza dettagli]** per una fase completata per conoscere i dettagli relativi a tale fase. Visualizza commenti, allegati a moduli e attività, stato, date di inizio e fine e così via.

![workflow-details](assets/workflow-details.png)

#### Actions toolbar {#actions-toolbar}

La barra degli strumenti Azioni mostra tutte le opzioni disponibili per l’attività. Salva, Reimposta e Delega sono azioni predefinite, mentre altre azioni disponibili sono configurate nel passaggio [](/help/sites-developing/workflows-step-ref.md)Assegna attività. Nell&#39;esempio precedente, Approva e Rifiuta sono configurati nel flusso di lavoro.

Quando si interviene sull&#39;attività, questa continua a essere implementata nel flusso di lavoro.

### Visualizza attività completate {#view-completed-tasks}

AEM Inbox visualizza solo le attività attive. Le attività completate non vengono visualizzate nell&#39;elenco. È tuttavia possibile utilizzare i filtri Inbox per filtrare le attività in base a diversi parametri, quali tipo di attività, stato, date di inizio e fine e così via. Per visualizzare le attività completate:

1. In AEM Inbox, toccate ![toggle-side-panel1](assets/toggle-side-panel1.png) per aprire il selettore dei filtri.
1. Toccate **[!UICONTROL Stato]** attività a soffietto e selezionate **[!UICONTROL Completa]**. Vengono visualizzate tutte le attività completate.

   ![filter](assets/filter.png)

1. Toccate per selezionare un&#39;attività e fate clic su **[!UICONTROL Apri]**.

Viene visualizzata l&#39;attività per visualizzare il documento o il modulo adattivo associato all&#39;attività. Per i moduli adattivi, l&#39;attività visualizza il modulo adattivo di sola lettura o il relativo documento di record PDF configurato nella scheda Modulo/Documento del passaggio [del flusso di lavoro](/help/sites-developing/workflows-step-ref.md)Assegna attività.

Nella sezione dei dettagli dell&#39;attività sono visualizzate informazioni quali l&#39;azione eseguita, lo stato dell&#39;attività, la data di inizio e la data di fine.

![task completato](assets/completed-task.png)

La scheda Dettagli **** flusso di lavoro mostra ogni passaggio del flusso di lavoro. Toccate **[!UICONTROL Visualizza dettagli]** per un passaggio per informazioni dettagliate.

![completato-task-workflow](assets/completed-task-workflow.png)

