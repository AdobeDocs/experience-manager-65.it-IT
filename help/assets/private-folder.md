---
title: Cartelle private per condividere le risorse
description: Scopri come creare una cartella privata in  [!DNL Adobe Experience Manager Assets] e condividerla con altri utenti e assegnare loro vari privilegi.
contentOwner: AG
role: Business Practitioner
feature: Collaboration
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Cartella privata in [!DNL Adobe Experience Manager Assets] {#private-folder}

È possibile creare una cartella privata nell’ interfaccia utente [!DNL Adobe Experience Manager Assets] disponibile esclusivamente all’utente. Puoi condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificare le risorse.

>[!NOTE]
>
>La cartella privata ha almeno un membro con ruolo Proprietario.

## Creazione e condivisione di cartelle private {#create-share-private-folder}

Per creare e condividere una cartella privata:

1. Nella console [!DNL Assets], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti, quindi scegli **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella risorse](assets/Create-folder.png)

1. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immetti un titolo e un nome (facoltativo) per la cartella e seleziona l&#39;opzione **[!UICONTROL Privato]** .

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una cartella privata.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Per condividere la cartella con altri utenti e assegnare loro i privilegi, seleziona la cartella e fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

   ![opzione info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >La cartella non è visibile ad altri utenti finché non la condividi.

1. Nella pagina **[!UICONTROL Proprietà cartella]**, seleziona un utente dall&#39;elenco **[!UICONTROL Aggiungi utente]**, assegna un ruolo all&#39;utente nella cartella privata e fai clic su **[!UICONTROL Aggiungi]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Puoi assegnare vari ruoli, ad esempio `Editor`, `Owner` o `Viewer` all’utente con cui condividi la cartella. Se assegni un ruolo `Owner` all&#39;utente, quest&#39;ultimo dispone di privilegi `Editor` nella cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se assegni un ruolo `Editor`, l’utente può modificare le risorse nella tua cartella privata. Se assegni un ruolo di visualizzatore, l’utente può visualizzare solo le risorse presenti nella cartella privata.

   >[!NOTE]
   >
   >La cartella privata ha almeno un membro con il ruolo `Owner`. Pertanto, l&#39;amministratore non può rimuovere tutti i membri proprietari da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e l&#39;amministratore stesso) dalla cartella privata, l&#39;amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva]**. A seconda del ruolo assegnato, all’utente viene assegnato un set di privilegi sulla cartella privata quando accede a [!DNL Assets].
1. Fai clic su **[!UICONTROL Ok]** per chiudere il messaggio di conferma.
1. L’utente con cui condividi la cartella riceve una notifica di condivisione. Accedi a [!DNL Assets] con le credenziali dell&#39;utente per visualizzare la notifica.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Fai clic su [!UICONTROL Notifiche] per aprire un elenco di notifiche.

   ![Elenco delle notifiche](assets/Assets-Notification.png)

1. Fai clic sulla voce della cartella privata condivisa dall’amministratore per aprire la cartella.

>[!NOTE]
>
>Per creare una cartella privata, è necessario leggere e modificare [le autorizzazioni di controllo accessi](/help/sites-administering/security.md#permissions-in-aem) nella cartella principale in cui si desidera creare una cartella privata. Se non sei un amministratore, per impostazione predefinita queste autorizzazioni non sono abilitate in `/content/dam`. In questo caso, prima di cercare di creare cartelle private, ottieni queste autorizzazioni per il tuo ID utente/gruppo.

## Eliminazione di cartelle private {#delete-private-folder}

È possibile eliminare una cartella selezionando la cartella e selezionando l&#39;opzione [!UICONTROL Elimina] dal menu principale, oppure utilizzando il tasto Backspace sulla tastiera.

![opzione elimina nel menu principale](assets/delete-option.png)

>[!CAUTION]
>
>Se si elimina una cartella privata da CRXDE Lite, i gruppi di utenti ridondanti vengono lasciati nell’archivio.

>[!NOTE]
>
>Se elimini una cartella utilizzando il metodo precedente dall&#39;interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
>
>Tuttavia, i gruppi di utenti ridondanti, inutilizzati e generati automaticamente possono essere rimossi dall’archivio utilizzando il metodo `clean` in JMX nell’istanza di authoring (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
