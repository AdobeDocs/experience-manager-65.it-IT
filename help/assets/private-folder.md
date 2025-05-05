---
title: Cartelle private per condividere le risorse
description: Scopri come creare una cartella privata in  [!DNL Adobe Experience Manager Assets]  e condividerla con altri utenti e assegnare loro vari privilegi.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---

# Cartella privata in [!DNL Adobe Experience Manager Assets] {#private-folder}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=it) |
| AEM 6.5 | Questo articolo |

Nell&#39;interfaccia utente di [!DNL Adobe Experience Manager Assets] è possibile creare una cartella privata disponibile esclusivamente per l&#39;utente. Puoi condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificarle.

>[!NOTE]
>
>La cartella privata ha almeno un membro con il ruolo Proprietario.

## Creazione e condivisione di cartelle private {#create-share-private-folder}

Per creare e condividere una cartella privata:

1. Nella console [!DNL Assets], fare clic su **[!UICONTROL Crea]** nella barra degli strumenti e quindi scegliere **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella risorse](assets/Create-folder.png)

1. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immetti un titolo e un nome (facoltativo) per la cartella, quindi seleziona l&#39;opzione **[!UICONTROL Privato]**.

1. Fai clic su **[!UICONTROL Crea]**. Viene creata una cartella privata.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Per condividere la cartella con altri utenti e assegnare loro i privilegi, selezionare la cartella e fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

   ![opzione info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >La cartella non è visibile a nessun altro utente finché non la condividi.

1. Nella pagina **[!UICONTROL Proprietà cartella]**, seleziona un utente dall&#39;elenco **[!UICONTROL Aggiungi utente]**, assegna un ruolo all&#39;utente nella tua cartella privata, quindi fai clic su **[!UICONTROL Aggiungi]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >È possibile assegnare vari ruoli, ad esempio `Editor`, `Owner` o `Viewer` all&#39;utente con cui si condivide la cartella. Se si assegna un ruolo `Owner` all&#39;utente, quest&#39;ultimo dispone di privilegi `Editor` sulla cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se assegni un ruolo `Editor`, l&#39;utente può modificare le risorse nella tua cartella privata. Se assegni un ruolo di visualizzatore, l’utente può visualizzare solo le risorse presenti nella cartella privata.

   >[!NOTE]
   >
   >La cartella privata ha almeno un membro con la mansione `Owner`. Pertanto, l&#39;amministratore non può rimuovere tutti i membri del proprietario da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e l’amministratore stesso) dalla cartella privata, l’amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva]**. A seconda del ruolo assegnato, all&#39;utente viene assegnato un set di privilegi sulla cartella privata quando accede a [!DNL Assets].
1. Fare clic su **[!UICONTROL Ok]** per chiudere il messaggio di conferma.
1. L&#39;utente con cui si condivide la cartella riceve una notifica di condivisione. Accedere a [!DNL Assets] con le credenziali dell&#39;utente per visualizzare la notifica.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Fai clic su [!UICONTROL Notifiche] per aprire un elenco di notifiche.

   ![Elenco di notifiche](assets/Assets-Notification.png)

1. Fare clic sulla voce relativa alla cartella privata condivisa dall&#39;amministratore per aprire la cartella.

>[!NOTE]
>
>Per creare una cartella privata, è necessario disporre delle autorizzazioni di lettura e modifica [per il controllo degli accessi](/help/sites-administering/security.md#permissions-in-aem) nella cartella principale in cui si desidera creare una cartella privata. Se non si è un amministratore, queste autorizzazioni non sono abilitate per impostazione predefinita in `/content/dam`. In questo caso, prima di creare cartelle private, è necessario ottenere queste autorizzazioni per l&#39;ID utente o il gruppo.

## Eliminazione cartella privata {#delete-private-folder}

Per eliminare una cartella, selezionala e seleziona l&#39;opzione [!UICONTROL Elimina] dal menu principale oppure usa il tasto Backspace.

![elimina opzione nel menu principale](assets/delete-option.png)

>[!CAUTION]
>
>Se elimini una cartella privata da CRXDE Lite, i gruppi di utenti ridondanti vengono lasciati nell’archivio.

>[!NOTE]
>
>Se elimini una cartella utilizzando il metodo descritto sopra dall’interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
>
>Tuttavia, i gruppi di utenti ridondanti, inutilizzati e generati automaticamente possono essere rimossi dall&#39;archivio utilizzando il metodo `clean` in JMX nell&#39;istanza di authoring (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
