---
title: Gestione delle applicazioni e delle attività di Forms nella casella in entrata AEM
description: Casella in entrata AEM consente di avviare flussi di lavoro incentrati su Forms tramite l’invio di applicazioni e la gestione di attività.
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 2%

---

# Gestione delle applicazioni e delle attività di Forms nella casella in entrata AEM{#manage-forms-applications-and-tasks-in-aem-inbox}

Uno dei modi per avviare o attivare un flusso di lavoro incentrato su Forms è tramite le applicazioni nella casella in entrata AEM. Per rendere un flusso di lavoro Forms disponibile come applicazione nella Casella in entrata, creare un&#39;applicazione flusso di lavoro. Per ulteriori informazioni sull&#39;applicazione del flusso di lavoro e su altri modi per avviare i flussi di lavoro di Forms, vedere [Avviare un flusso di lavoro incentrato su Forms in OSGi](../../forms/using/aem-forms-workflow.md#launch).

Inoltre, la Casella in entrata AEM consolida le notifiche e le attività da vari componenti AEM, inclusi i flussi di lavoro Forms. Quando viene attivato un flusso di lavoro dei moduli contenente un passaggio Assegna attività, l’applicazione associata viene elencata come attività nella casella in entrata dell’assegnatario. Se l&#39;assegnatario è un gruppo, l&#39;attività viene visualizzata nella Posta in arrivo di tutti i membri del gruppo fino a quando un singolo utente non richiede o delega l&#39;attività.

L&#39;interfaccia utente Casella in entrata fornisce viste elenco e calendario per visualizzare le attività. È inoltre possibile configurare le impostazioni di visualizzazione. Puoi filtrare le attività in base a vari parametri. Per ulteriori informazioni sulla visualizzazione e sui filtri, vedere [Posta in arrivo](/help/sites-authoring/inbox.md).

In sintesi, Casella in entrata consente di creare un&#39;applicazione e gestire le attività assegnate.

>[!NOTE]
>
>Per poter utilizzare la casella in entrata AEM, è necessario essere membri del gruppo utenti flusso di lavoro.

## Crea applicazione {#create-application}

1. Vai alla casella in entrata AEM all&#39;indirizzo https://&#39;[server]:[porta]&#39;/aem/inbox.
1. Nell&#39;interfaccia utente Posta in arrivo, selezionare **[!UICONTROL Crea > Applicazione]**. Viene visualizzata la pagina Seleziona applicazione.
1. Selezionare un&#39;applicazione e fare clic su **[!UICONTROL Crea]**. Viene aperto il modulo adattivo associato all’applicazione. Inserisci le informazioni nel modulo adattivo e seleziona **[!UICONTROL Invia]**. Avvia il flusso di lavoro associato e crea un&#39;attività nella Posta in arrivo dell&#39;assegnatario.

## Gestione attività {#manage-tasks}

Quando viene attivato un flusso di lavoro di Forms e l&#39;utente è un assegnatario o parte del gruppo dell&#39;assegnatario, un&#39;attività viene visualizzata nella Posta in arrivo. È possibile visualizzare i dettagli dell&#39;attività ed eseguire le azioni disponibili sull&#39;attività dalla casella in entrata.

### Richiedi o delega attività {#claim-or-delegate-tasks}

Le attività assegnate a un gruppo vengono visualizzate nella cartella Posta in arrivo di tutti i membri del gruppo. Qualsiasi membro del gruppo può rivendicare tale attività o delegarla a un altro membro del gruppo. Per eseguire questa operazione:

1. Selezionare per selezionare la miniatura dell&#39;attività. Le opzioni per aprire o delegare l&#39;attività vengono visualizzate nella parte superiore.

   ![attività selezionata](assets/select-task.png)

1. Effettua una delle operazioni seguenti:

   * Per delegare l&#39;attività, selezionare **[!UICONTROL Delega]**. Viene visualizzata la finestra di dialogo Delega elemento. Selezionare un utente, aggiungere un commento e selezionare **[!UICONTROL OK]**.

   ![delegato](assets/delegate.png)

   * Per richiedere l&#39;attività, selezionare **[!UICONTROL Apri]**. Viene visualizzata la finestra di dialogo Assegna a sé. Seleziona **[!UICONTROL Procedi]** per richiedere l&#39;attività. L&#39;attività richiesta viene visualizzata come assegnatario nella cartella Posta in arrivo.

   ![attestazione](assets/claim.png)

### Visualizzare i dettagli ed eseguire azioni sulle attività {#view-details-and-perform-actions-on-tasks}

Quando si apre un&#39;attività, è possibile visualizzarne i dettagli ed eseguire le azioni disponibili. Le azioni disponibili per un&#39;attività sono definite nel passaggio Assegna attività del flusso di lavoro Forms associato.

1. Selezionare per selezionare la miniatura dell&#39;attività. Le opzioni per aprire o delegare l&#39;attività selezionata vengono visualizzate nella parte superiore.
1. Seleziona **Apri** per visualizzare i dettagli dell&#39;attività. Viene visualizzata la vista dettagliata dell&#39;operazione. In questa visualizzazione è possibile visualizzare i dettagli dell&#39;attività e lavorare sull&#39;attività.

   >[!NOTE]
   >
   >Se un&#39;attività è assegnata a un gruppo, è necessario dichiararla per essere in grado di aprirla in visualizzazione dettagliata.

![dettagli attività](assets/task-details.png)

La vista dettagliata delle attività comprende le sezioni riportate di seguito.

* Dettagli attività
* Modulo
* Dettagli flusso di lavoro
* Barra delle azioni

#### Dettagli attività {#task-details}

Nella sezione Dettagli attività vengono visualizzate informazioni sull&#39;attività. Le informazioni visualizzate dipendono dalle impostazioni di configurazione del [Passaggio attività ](/help/sites-developing/workflows-step-ref.md) nel flusso di lavoro. Nell&#39;esempio precedente vengono visualizzati la descrizione, lo stato, la data di inizio e il flusso di lavoro utilizzati per l&#39;attività. Consente inoltre di allegare un file all&#39;operazione.

#### Modulo {#form}

La scheda Modulo nell’area del contenuto principale visualizza il modulo inviato e gli eventuali allegati a livello di campo.

#### Dettagli flusso di lavoro {#workflow-details}

La scheda Dettagli flusso di lavoro nella parte superiore mostra l’avanzamento dell’attività attraverso le varie fasi del flusso di lavoro. Vengono visualizzate le fasi completata, corrente e in sospeso per l&#39;attività. Le fasi di un flusso di lavoro sono definite nel [Passaggio di assegnazione attività](/help/sites-developing/workflows-step-ref.md) del flusso di lavoro associato.

Inoltre, nella scheda viene visualizzata la cronologia delle attività per ogni fase completata del flusso di lavoro. È possibile selezionare **[!UICONTROL Visualizza dettagli]** per una fase completata per conoscere i dettagli della fase. Vengono visualizzati i commenti, gli allegati del modulo e dell&#39;attività, lo stato, le date di inizio e di fine e così via relativi all&#39;attività.

![dettagli-flusso di lavoro](assets/workflow-details.png)

#### Barra delle azioni {#actions-toolbar}

La barra degli strumenti Azioni mostra tutte le opzioni disponibili per l&#39;attività. Mentre Salva, Reimposta e Delega sono azioni predefinite, altre azioni disponibili sono configurate in [Assegna passaggio attività](/help/sites-developing/workflows-step-ref.md). Nell’esempio precedente, Approve (Approva) e Reject (Rifiuta) sono configurati nel flusso di lavoro.

Mentre si lavora sull&#39;attività, questa procede ulteriormente nel flusso di lavoro.

### Visualizza attività completate {#view-completed-tasks}

Nella casella in entrata AEM vengono visualizzate solo le attività attive. Le attività completate non vengono visualizzate nell&#39;elenco. È tuttavia possibile utilizzare i filtri Posta in arrivo per filtrare le attività in base a diversi parametri, ad esempio il tipo di attività, lo stato e le date di inizio e fine. Per visualizzare le attività completate:

1. Nella casella in entrata AEM, seleziona ![toggle-side-panel1](assets/toggle-side-panel1.png) per aprire il selettore di filtri.
1. Seleziona il pannello a soffietto **[!UICONTROL Stato attività]** e seleziona **[!UICONTROL Completa]**. Vengono visualizzate tutte le attività completate.

   ![filtro](assets/filter.png)

1. Seleziona per selezionare un&#39;attività e fai clic su **[!UICONTROL Apri]**.

L’attività si apre per visualizzare il documento o il modulo adattivo associato all’attività. Per il modulo adattivo, l&#39;attività visualizza il modulo adattivo di sola lettura o il relativo documento di record PDF come configurato nella scheda Modulo/Documento del passaggio [Assegna attività del flusso di lavoro](/help/sites-developing/workflows-step-ref.md).

Nella sezione dei dettagli dell&#39;attività vengono visualizzate informazioni quali l&#39;azione intrapresa, lo stato dell&#39;attività, la data di inizio e la data di fine.

![attività completata](assets/completed-task.png)

La scheda **[!UICONTROL Dettagli flusso di lavoro]** mostra ogni passaggio del flusso di lavoro. Selezionare **[!UICONTROL Visualizza dettagli]** per un passaggio per informazioni dettagliate.

![attività-flusso di lavoro completato](assets/completed-task-workflow.png)

## Risoluzione dei problemi {#troubleshooting-workflows}

### Impossibile visualizzare gli elementi relativi al flusso di lavoro AEM nella casella in entrata AEM {#unable-to-see-aem-worklow-items}

Il proprietario di un modello di flusso di lavoro non è in grado di visualizzare gli elementi relativi al flusso di lavoro AEM nella casella in entrata AEM. Per risolvere il problema, aggiungi gli indici elencati di seguito al tuo archivio AEM e ricostruisci l’indice.

1. Per aggiungere indici, utilizzate uno dei seguenti metodi:

   * Creare i nodi seguenti in CRX DE alle `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` con le rispettive proprietà come specificato nella tabella seguente:

     | Nodo | Proprietà | Tipo |
     |---|---|---|
     | sharedWith | sharedWith | STRINGA |
     | protetto | protetto | BOOLEANO |
     | ha restituito | ha restituito | BOOLEANO |
     | allowInboxSharing | allowInboxSharing | BOOLEANO |
     | allowExplicitSharing | allowExplicitSharing | BOOLEANO |


   * Distribuire gli indici tramite un pacchetto AEM. È possibile utilizzare un progetto [Archetipo AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=it) per creare un pacchetto AEM distribuibile. Utilizza il seguente codice di esempio per aggiungere indici a un progetto dell’archetipo AEM:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Creare un indice delle proprietà e impostarlo su true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=it#the-property-index).

1. Dopo la configurazione degli indici in CRX DE o la distribuzione tramite un pacchetto, [reindicizza l&#39;archivio](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=it
