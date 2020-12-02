---
title: Esaminare raccolte e risorse delle cartelle
description: Configurate i flussi di lavoro di revisione per le risorse all'interno di una cartella o di una raccolta e condividetela con revisori o partner creativi per ottenere feedback.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 4%

---


# Esaminare raccolte e risorse delle cartelle {#review-folder-assets-and-collections}

Configurate i flussi di lavoro di revisione per le risorse all&#39;interno di una cartella o di una raccolta e condividetela con revisori o partner creativi per ottenere feedback.

[!DNL Adobe Experience Manager Assets] consente di impostare un flusso di lavoro di revisione ad hoc per le risorse all&#39;interno di una cartella o raccolta e di condividerlo con revisori o partner creativi per ottenere feedback.

Potete associare il flusso di lavoro di revisione a un progetto o creare un&#39;attività di revisione indipendente.

Dopo aver condiviso le risorse, i revisori possono approvarle o rifiutarle. Le notifiche vengono inviate in varie fasi del flusso di lavoro per notificare ai destinatari previsti il completamento di varie attività. Ad esempio, quando condividete una cartella o una raccolta, il revisore riceve una notifica che una cartella o una raccolta è stata condivisa per la revisione.

Dopo che il revisore ha completato la revisione (approva o rifiuta le risorse), riceverete una notifica di completamento della revisione.

## Creazione di un&#39;attività di revisione per le cartelle {#creating-a-review-task-for-folders}

1. Dall&#39;interfaccia utente [!DNL Assets], selezionate la cartella per la quale desiderate creare un&#39;attività di revisione.
1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Crea attività revisione]** ![crea attività revisione](assets/do-not-localize/create-review-task.png) per aprire la pagina **[!UICONTROL Rivedi attività]**. Se non è possibile visualizzare l&#39;opzione nella barra degli strumenti, fare clic su **[!UICONTROL Altro]**, quindi selezionare l&#39;opzione.

1. (Facoltativo) Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, è selezionata l&#39;opzione **[!UICONTROL None]**. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Nell&#39;elenco **[!UICONTROL Progetti]** sono visibili solo i progetti per i quali si dispone di autorizzazioni a livello di editor (o superiori).

1. Immettere un nome per l&#39;attività di revisione e selezionare un approver dall&#39;elenco **[!UICONTROL Assegna a]**.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nell&#39;elenco **[!UICONTROL Assegna a]**.

1. Inserire una descrizione, la priorità dell&#39;attività e la data di scadenza per l&#39;attività di revisione.

   ![task_details](assets/task_details.png)

1. Nella scheda Avanzate, inserite un&#39;etichetta da utilizzare per creare l&#39;URI.

   ![review_name](assets/review_name.png)

1. Fare clic su **[!UICONTROL Invia]**, quindi fare clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Assets] come approver e passa all&#39;interfaccia [!DNL Assets]. Per approvare le risorse, fate clic su **[!UICONTROL Notifiche]**, quindi selezionate l&#39;attività di revisione dall&#39;elenco.

   ![Notifica risorse](assets/aemAssetsNotification.png)

1. Nella pagina **[!UICONTROL Rivedi attività]**, esaminare i dettagli dell&#39;attività di revisione, quindi fare clic su **[!UICONTROL Rivedi]**.
1. Nella pagina **[!UICONTROL Rivedi attività]**, seleziona le risorse e fai clic su **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare, a seconda dei casi.

   ![review_task](assets/review_task.png)

1. Fare clic su **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, inserite un commento e fate clic su **[!UICONTROL Completa]** per confermare.
1. Passate all&#39;interfaccia [!DNL Assets] e aprite la cartella. Le icone dello stato di approvazione per le risorse vengono visualizzate nelle viste a schede e a elenco.

   **Vista a schede**

   ![Rivedere lo stato come visualizzato nella vista a schede](assets/chlimage_1-404.png)

   **Vista a elenco**

   ![Rivedere lo stato come visualizzato nella vista a elenco](assets/review_status_listview.png)

## Creazione di un&#39;attività di revisione per le raccolte {#creating-a-review-task-for-collections}

1. Nella pagina Raccolte, selezionate la raccolta per la quale desiderate creare un&#39;attività di revisione.
1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Crea attività revisione]** ![crea attività revisione](assets/do-not-localize/create-review-task.png) per aprire la pagina **[!UICONTROL Rivedi attività]**. Se non è possibile visualizzare l&#39;opzione sulla barra degli strumenti, fare clic su **[!UICONTROL Altro]**, quindi selezionare l&#39;opzione.

1. (Facoltativo) Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, è selezionata l&#39;opzione **[!UICONTROL None]**. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Nell&#39;elenco **[!UICONTROL Progetti]** sono visibili solo i progetti per i quali si dispone di autorizzazioni a livello di editor (o superiori).

1. Immettere un nome per l&#39;attività di revisione e selezionare un approver dall&#39;elenco **[!UICONTROL Assegna a]**.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nell&#39;elenco **[!UICONTROL Assegna a]**.

1. Inserire una descrizione, la priorità dell&#39;attività e la data di scadenza per l&#39;attività di revisione.

   ![task_details-collection](assets/task_details-collection.png)

1. Fare clic su **[!UICONTROL Invia]**, quindi fare clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedete a [!DNL Assets] come approver e andate alla console [!DNL Assets]. Per approvare le risorse, fate clic su **[!UICONTROL Notifiche]**, quindi selezionate l&#39;attività di revisione dall&#39;elenco.
1. Nella pagina **[!UICONTROL Rivedi attività]**, esaminare i dettagli dell&#39;attività di revisione, quindi fare clic su **[!UICONTROL Rivedi]**.
1. Tutte le risorse della raccolta sono visibili nella pagina di revisione. Selezionate le risorse e fate clic su **[!UICONTROL Approva/Rifiuta]** per approvare o rifiutare le risorse, a seconda delle necessità.

   ![review_task_collection](assets/review_task_collection.png)

1. Fare clic su **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, inserite un commento e fate clic su **[!UICONTROL Completa]** per confermare.
1. Passate alla console Raccolte e aprite la raccolta. Le icone dello stato di approvazione per le risorse vengono visualizzate nelle viste a schede e a elenco.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: Vista a schede.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: Vista a elenco.*
