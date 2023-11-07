---
title: Cartelle private per condividere le risorse
description: Scopri come creare una cartella privata in [!DNL Adobe Experience Manager Assets] e condividerlo con altri utenti e assegnare loro vari privilegi.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 3%

---

# Cartella privata in [!DNL Adobe Experience Manager Assets] {#private-folder}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | Questo articolo |

Puoi creare una cartella privata in [!DNL Adobe Experience Manager Assets] un&#39;interfaccia utente disponibile esclusivamente per l&#39;utente. Puoi condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificarle.

>[!NOTE]
>
>La cartella privata ha almeno un membro con il ruolo Proprietario.

## Creazione e condivisione di cartelle private {#create-share-private-folder}

Per creare e condividere una cartella privata:

1. In [!DNL Assets] console, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti, quindi scegli **[!UICONTROL Cartella]** dal menu.

   ![Creare una cartella di risorse](assets/Create-folder.png)

1. In **[!UICONTROL Crea cartella]** , immetti un titolo e un nome (facoltativo) per la cartella, quindi seleziona **[!UICONTROL Privato]** opzione.

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una cartella privata.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Per condividere la cartella con altri utenti e assegnare loro i privilegi, selezionare la cartella e fare clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.

   ![opzione info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >La cartella non è visibile a nessun altro utente finché non la condividi.

1. In **[!UICONTROL Proprietà cartella]** , selezionare un utente dalla **[!UICONTROL Aggiungi utente]** , assegna un ruolo all&#39;utente nella tua cartella privata e fai clic su **[!UICONTROL Aggiungi]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Puoi assegnare vari ruoli, ad esempio `Editor`, `Owner`, o `Viewer` all&#39;utente con cui si condivide la cartella. Se si assegna un `Owner` all&#39;utente, l&#39;utente ha `Editor` privilegi sulla cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se si assegna un `Editor` ruolo, l’utente può modificare le risorse nella cartella privata. Se assegni un ruolo di visualizzatore, l’utente può visualizzare solo le risorse presenti nella cartella privata.

   >[!NOTE]
   >
   >La cartella privata ha almeno un membro con `Owner` ruolo. Pertanto, l&#39;amministratore non può rimuovere tutti i membri del proprietario da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e l’amministratore stesso) dalla cartella privata, l’amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva]**. A seconda del ruolo assegnato, all’utente viene assegnato un set di privilegi sulla cartella privata quando accede a [!DNL Assets].
1. Clic **[!UICONTROL Ok]** per chiudere il messaggio di conferma.
1. L&#39;utente con cui si condivide la cartella riceve una notifica di condivisione. Accedi a [!DNL Assets] con le credenziali dell’utente per visualizzare la notifica.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clic [!UICONTROL Notifiche] per aprire un elenco di notifiche.

   ![Elenco delle notifiche](assets/Assets-Notification.png)

1. Fare clic sulla voce relativa alla cartella privata condivisa dall&#39;amministratore per aprire la cartella.

>[!NOTE]
>
>Per creare una cartella privata, è necessario disporre di Leggi e Modifica [autorizzazioni di controllo degli accessi](/help/sites-administering/security.md#permissions-in-aem) nella cartella principale in cui si desidera creare una cartella privata. Se non sei un amministratore, per impostazione predefinita queste autorizzazioni non sono abilitate su `/content/dam`. In questo caso, prima di creare cartelle private, è necessario ottenere queste autorizzazioni per l&#39;ID utente o il gruppo.

## Eliminazione cartella privata {#delete-private-folder}

Puoi eliminare una cartella selezionandola e selezionando [!UICONTROL Elimina] dal menu principale o utilizzando il tasto Backspace sulla tastiera.

![elimina opzione nel menu superiore](assets/delete-option.png)

>[!CAUTION]
>
>Se elimini una cartella privata da CRXDE Liti, i gruppi di utenti ridondanti vengono lasciati nell’archivio.

>[!NOTE]
>
>Se elimini una cartella utilizzando il metodo descritto sopra dall’interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
>
>Tuttavia, i gruppi di utenti ridondanti, inutilizzati e generati automaticamente possono essere rimossi dall’archivio utilizzando `clean` metodo in JMX nell’istanza di authoring (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
