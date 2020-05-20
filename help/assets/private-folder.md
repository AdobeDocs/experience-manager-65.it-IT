---
title: Creazione e condivisione di una cartella privata in AEM
description: Scopri come creare una cartella privata in Risorse Adobe Experience Manager (AEM) e condividerla con altri utenti e assegnare loro vari privilegi.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Condivisione di cartelle private {#private-folder-sharing}

Puoi creare una cartella privata nell’interfaccia utente di Risorse Adobe Experience Manager (AEM), disponibile esclusivamente per l’utente. Potete condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificarle.

>[!NOTE]
>
> La cartella privata ha almeno un membro con il ruolo Proprietario.


1. Nella console Risorse, fate clic su **[!UICONTROL Crea]** nella barra degli strumenti, quindi scegliete **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella risorse](assets/Create-folder.png)

1. Nella finestra di dialogo **[!UICONTROL Crea cartella]** , immettete un titolo e un nome (facoltativi) per la cartella e selezionate **[!UICONTROL Privato]**.

   ![Selezionate la casella di controllo Privato per rendere privata la cartella](assets/private-folder.png)

1. Fai clic su **[!UICONTROL Crea]**. Nell’interfaccia utente viene creata una cartella privata.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click the **[!UICONTROL Properties]** icon from the toolbar.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >La cartella non è visibile ad altri utenti finché non la condividete.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Potete assegnare diversi ruoli, ad esempio Editor, Proprietario o Visualizzatore all’utente con il quale condividete la cartella. Se assegnate un ruolo Proprietario all’utente, quest’ultimo dispone dei privilegi di Modifica sulla cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se assegnate un ruolo Editor, l’utente può modificare le risorse presenti nella cartella privata. Se assegnate un ruolo Visualizzatore, l’utente può visualizzare solo le risorse presenti nella propria cartella privata.

   >[!NOTE]
   >
   > La cartella privata ha almeno un membro con il ruolo Proprietario. Pertanto, l’amministratore non può rimuovere tutti i membri del proprietario da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e lo stesso amministratore) dalla cartella privata, l&#39;amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva]**. A seconda del ruolo assegnato, all’utente viene assegnato un set di privilegi nella cartella privata quando accede a Risorse AEM.
1. Fate clic su **[!UICONTROL OK]** per chiudere il messaggio di conferma.
1. L’utente con il quale condividete la cartella riceve una notifica di condivisione. Accedi a Risorse AEM con le credenziali dell’utente per visualizzare la notifica.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Fate clic sull&#39;icona Notifica per aprire l&#39;elenco delle notifiche.

   ![Elenco delle notifiche](assets/Assets-Notification.png)

1. Fate clic sulla voce relativa alla cartella privata condivisa dall’amministratore per aprire la cartella.

>[!NOTE]
>
>Per creare una cartella privata, è necessario disporre delle autorizzazioni di lettura e modifica ACL per la cartella principale in cui si desidera creare una cartella privata. Se non siete un amministratore, per impostazione predefinita tali autorizzazioni non sono abilitate per voi in `/content/dam`. In questo caso, ottenete prima queste autorizzazioni per l’ID utente o il gruppo prima di tentare di creare cartelle private o visualizzare le impostazioni delle cartelle.
