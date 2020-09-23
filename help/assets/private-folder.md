---
title: Cartella privata in [!DNL Adobe Experience Manager Assets]
description: Scoprite come creare una cartella privata in [!DNL Adobe Experience Manager Assets] e condividerla con altri utenti e assegnare loro vari privilegi.
contentOwner: AG
translation-type: tm+mt
source-git-commit: be97ef4f3bb6b904dabcfcd44025a4898bcf4dee
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 1%

---


# Cartella privata in [!DNL Adobe Experience Manager Assets] {#private-folder}

Potete creare una cartella privata nell’interfaccia [!DNL Adobe Experience Manager Assets] utente disponibile esclusivamente per voi. Potete condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificarle.

>[!NOTE]
>
>La cartella privata ha almeno un membro con il ruolo Proprietario.

## Creazione e condivisione di cartelle private {#create-share-private-folder}

Per creare e condividere una cartella privata:

1. Nella [!DNL Assets] console, fate clic su **[!UICONTROL Crea]** nella barra degli strumenti, quindi scegliete **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella risorse](assets/Create-folder.png)

1. Nella finestra di dialogo **[!UICONTROL Crea cartella]** , immettete un titolo e un nome (facoltativi) per la cartella e selezionate l’opzione **[!UICONTROL Privato]** .

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una cartella privata.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![opzione info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >La cartella non è visibile ad altri utenti finché non la condividete.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Potete assegnare diversi ruoli, ad esempio Editor, Proprietario o Visualizzatore all’utente con il quale condividete la cartella. Se assegnate un ruolo Proprietario all’utente, quest’ultimo dispone dei privilegi di Modifica sulla cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se assegnate un ruolo Editor, l’utente può modificare le risorse presenti nella cartella privata. Se assegnate un ruolo di visualizzatore, l’utente può visualizzare solo le risorse presenti nella propria cartella privata.

   >[!NOTE]
   >
   >La cartella privata ha almeno un membro con il ruolo Proprietario. Pertanto, l’amministratore non può rimuovere tutti i membri del proprietario da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e lo stesso amministratore) dalla cartella privata, l&#39;amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva]**. A seconda del ruolo assegnato, all’utente viene assegnato un set di privilegi nella cartella privata al momento dell’accesso [!DNL Assets].
1. Fate clic su **[!UICONTROL OK]** per chiudere il messaggio di conferma.
1. L’utente con il quale condividete la cartella riceve una notifica di condivisione. Effettuate l&#39;accesso [!DNL Assets] con le credenziali dell&#39;utente per visualizzare la notifica.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Fate clic su Notifiche per aprire l’elenco delle notifiche.

   ![Elenco delle notifiche](assets/Assets-Notification.png)

1. Fate clic sulla voce relativa alla cartella privata condivisa dall’amministratore per aprire la cartella.

>[!NOTE]
>
>Per creare una cartella privata, è necessario disporre delle autorizzazioni [di controllo di](/help/sites-administering/security.md#permissions-in-aem) accesso Lettura e Modifica nella cartella principale in cui si desidera creare una cartella privata. Se non siete un amministratore, per impostazione predefinita tali autorizzazioni non sono abilitate per voi in `/content/dam`. In questo caso, ottenete prima queste autorizzazioni per l’ID utente o il gruppo prima di tentare di creare cartelle private.

## Eliminazione di cartelle private {#delete-private-folder}

Per eliminare una cartella, selezionatela e selezionate l’opzione [!UICONTROL Elimina] dal menu principale, oppure utilizzate il tasto Backspace della tastiera.

![opzione Elimina nel menu principale](assets/delete-option.png)

>[!CAUTION]
>
>Se eliminate una cartella privata dal CRXDE Lite , i gruppi di utenti ridondanti vengono lasciati nella directory archivio.

>[!NOTE]
>
>Se eliminate una cartella utilizzando il metodo indicato sopra dall’interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
Tuttavia, i gruppi di utenti ridondanti, inutilizzati e generati automaticamente possono essere ripuliti dall&#39;archivio utilizzando [JMX](#group-clean-up-jmx).

### Utilizzare JMX per ripulire i gruppi di utenti inutilizzati {#group-clean-up-jmx}

Per ripulire l’archivio dei gruppi di utenti non utilizzati:

1. Aprite JMX per eliminare i gruppi ridondanti per le risorse nell’istanza di [!DNL Experience Manager] creazione da `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.
Esempio, `http://no1010042068039.corp.adobe.com:4502/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.

1. Richiama il `clean` metodo da questo JMX.

Potete vedere che tutti i gruppi di utenti ridondanti o i gruppi generati automaticamente (creati al momento della creazione di una cartella con lo stesso nome di un gruppo eliminato in precedenza) vengono rimossi dal percorso `/home/groups/mac/default/<user_name>/<folder_name>`.
