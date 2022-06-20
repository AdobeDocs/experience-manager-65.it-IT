---
title: Esaminare raccolte e risorse delle cartelle
description: Imposta i flussi di lavoro di revisione per le risorse all’interno di una cartella o di una raccolta e condividila con revisori o partner creativi per ottenere un feedback.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 5%

---

# Esaminare raccolte e risorse delle cartelle {#review-folder-assets-and-collections}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | Questo articolo |
| AEM 6.4 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/bulk-approval.html?lang=en) |

Imposta i flussi di lavoro di revisione per le risorse all’interno di una cartella o di una raccolta e condividila con revisori o partner creativi per ottenere un feedback.

[!DNL Adobe Experience Manager Assets] consente di impostare un flusso di lavoro di revisione ad hoc per le risorse all’interno di una cartella o di una raccolta e di condividerlo con revisori o partner creativi per ottenere un feedback.

È possibile associare il flusso di lavoro di revisione a un progetto o creare un&#39;attività di revisione indipendente.

Dopo aver condiviso le risorse, i revisori possono approvarle o rifiutarle. Le notifiche vengono inviate in varie fasi del flusso di lavoro per informare i destinatari in merito al completamento di varie attività. Ad esempio, quando si condivide una cartella o una raccolta, il revisore riceve una notifica relativa alla condivisione di una cartella o raccolta per la revisione.

Dopo che il revisore ha completato la revisione (approva o rifiuta le risorse), riceverai una notifica di completamento della revisione.

## Creazione di un&#39;attività di revisione per le cartelle {#creating-a-review-task-for-folders}

1. Da [!DNL Assets] interfaccia utente, selezionare la cartella per la quale si desidera creare un&#39;attività di revisione.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea attività di revisione]** ![crea attività di revisione](assets/do-not-localize/create-review-task.png) per aprire **[!UICONTROL Attività di revisione]** pagina. Se l’opzione non è visibile nella barra degli strumenti, fai clic su **[!UICONTROL Altro]** quindi seleziona l’opzione .

1. (Facoltativo) Dal **[!UICONTROL Progetto]** selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, la **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Solo i progetti per i quali disponi di autorizzazioni a livello di editor (o versioni successive) sono visibili nel **[!UICONTROL Progetti]** elenco.

1. Immettere un nome per l&#39;attività di revisione e selezionare un approvatore dal **[!UICONTROL Assegna a]** elenco.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nel **[!UICONTROL Assegna a]** elenco.

1. Immettere una descrizione, la priorità dell&#39;attività e la data di scadenza dell&#39;attività di revisione.

   ![task_details](assets/task_details.png)

1. Nella scheda Avanzate , immetti un’etichetta da utilizzare per creare l’URI.

   ![review_name](assets/review_name.png)

1. Fai clic su **[!UICONTROL Invia]**, quindi fai clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Assets] come Approvatore e passa alla [!DNL Assets] Interfaccia utente. Per approvare le risorse, fai clic su **[!UICONTROL Notifiche]** quindi selezionare l&#39;attività di revisione dall&#39;elenco.

   ![Notifica risorse](assets/aemAssetsNotification.png)

1. In **[!UICONTROL Attività di revisione]** esaminare i dettagli dell&#39;attività di revisione, quindi fare clic su **[!UICONTROL Revisione]**.
1. In **[!UICONTROL Attività di revisione]** , seleziona le risorse e fai clic su **[!UICONTROL Approva/Rifiuta]** approvare o respingere, a seconda dei casi.

   ![review_task](assets/review_task.png)

1. Fai clic su **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e fai clic su  **[!UICONTROL Completa]** per confermare.
1. Passa a [!DNL Assets] e apri la cartella. Le icone sullo stato di approvazione delle risorse vengono visualizzate nella vista a schede e a elenco.

   **Vista a schede**

   ![Stato della revisione nella vista a schede](assets/chlimage_1-404.png)

   **Vista a elenco**

   ![Stato della revisione nella vista a elenco](assets/review_status_listview.png)

## Creare un’attività di revisione per le raccolte {#creating-a-review-task-for-collections}

1. Nella pagina Raccolte selezionare la raccolta per la quale si desidera creare un&#39;attività di revisione.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea attività di revisione]** ![crea attività di revisione](assets/do-not-localize/create-review-task.png) per aprire **[!UICONTROL Attività di revisione]** pagina. Se l’opzione non è visibile sulla barra degli strumenti, fai clic su **[!UICONTROL Altro]** quindi seleziona l’opzione .

1. (Facoltativo) Dal **[!UICONTROL Progetto]** selezionare il progetto a cui si desidera associare l&#39;attività di revisione. Per impostazione predefinita, la **[!UICONTROL Nessuno]** è selezionata. Se non si desidera associare alcun progetto all&#39;attività di revisione, mantenere questa selezione.

   >[!NOTE]
   >
   >Solo i progetti per i quali disponi di autorizzazioni a livello di editor (o versioni successive) sono visibili nel **[!UICONTROL Progetti]** elenco.

1. Immettere un nome per l&#39;attività di revisione e selezionare un approvatore dal **[!UICONTROL Assegna a]** elenco.

   >[!NOTE]
   >
   >I membri/gruppi del progetto selezionato sono disponibili come approvatori nel **[!UICONTROL Assegna a]** elenco.

1. Immettere una descrizione, la priorità dell&#39;attività e la data di scadenza dell&#39;attività di revisione.

   ![task_details-collection](assets/task_details-collection.png)

1. Fai clic su **[!UICONTROL Invia]**, quindi fai clic su **[!UICONTROL Fine]** per chiudere il messaggio di conferma. Una notifica per la nuova attività viene inviata al responsabile approvazione.
1. Accedi a [!DNL Assets] come Approvatore e passa alla [!DNL Assets] console. Per approvare le risorse, fai clic su **[!UICONTROL Notifiche]** quindi selezionare l&#39;attività di revisione dall&#39;elenco.
1. In **[!UICONTROL Attività di revisione]** esaminare i dettagli dell&#39;attività di revisione, quindi fare clic su **[!UICONTROL Revisione]**.
1. Tutte le risorse nella raccolta sono visibili nella pagina di revisione. Seleziona le risorse e fai clic su **[!UICONTROL Approva/Rifiuta]** approvare o rifiutare le risorse, a seconda dei casi.

   ![review_task_collection](assets/review_task_collection.png)

1. Fai clic su **[!UICONTROL Completa]** dalla barra degli strumenti. Nella finestra di dialogo, immetti un commento e fai clic su **[!UICONTROL Completa]** per confermare.
1. Passa alla console Raccolte e apri la raccolta. Le icone dello stato di approvazione per le risorse vengono visualizzate nelle viste a schede e a elenco.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: Vista a schede.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: Vista a elenco.*
