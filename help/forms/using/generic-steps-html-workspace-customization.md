---
title: Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms
description: Come iniziare a personalizzare l’interfaccia utente di Adobe Experience Manager Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

I passaggi generici per eseguire qualsiasi personalizzazione sono i seguenti:

1. Accedere a CRXDE Lite accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Creare una cartella `sling:Folder` denominata `ws` in `/apps`, se non esiste. Per creare una cartella `sling:Folder`, fare clic con il pulsante destro del mouse sulla cartella `apps` e selezionare **[!UICONTROL Crea]** > **[!UICONTROL Crea nodo]**. Specificare il nome come `ws`, selezionare il tipo come `sling:Folder` e fare clic su **[!UICONTROL OK]**. Fare clic su **[!UICONTROL Salva tutto]**.
1. Passare a `/apps/ws` e passare alla scheda **[!UICONTROL Controllo dell&#39;accesso]**.
1. Selezionare l&#39;opzione **[!UICONTROL Archivio]**. Nell&#39;elenco **[!UICONTROL Controllo di accesso]** fare clic su **[!UICONTROL +]** per aggiungere una voce. Fai di nuovo clic su **[!UICONTROL +]**.
1. Cerca e seleziona l&#39;entità **PERM_WORKSPACE_USER**.

   ![Selezionare l&#39;entità PERM_WORKSPACE_USER come parte dei passaggi generici per personalizzare HTML Workspace](assets/perm_workspace_user.png)

1. Assegnare il privilegio `jcr:read` all&#39;entità.
1. Fare clic su **[!UICONTROL Salva tutto]**.
1. Copiare i file `GET.jsp`, `index` e `html.jsp` dalla cartella `/libs/ws` nella cartella `/apps/ws`.
1. Copiare la cartella `/libs/ws/locales` nella cartella `/apps/ws`. Fare clic su **[!UICONTROL Salva tutto]**.
1. Aggiornare i riferimenti e i percorsi relativi nel file `GET.jsp`, come illustrato di seguito, e fare clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Per le personalizzazioni CSS, effettua le seguenti operazioni:

   1. Passare alla cartella `/apps/ws` e creare una cartella denominata `css`.

   1. Nella cartella `css` creare un file denominato `newStyle.css`.

   1. Apri `/apps/ws/html`.jsp e cambia da

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   in

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Posiziona la voce del file CSS definito dall&#39;utente dopo la voce style.css, come mostrato sopra.

1. Nel file /apps/ws/html.jsp, cambia da

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   in

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Effettua le seguenti operazioni:

   1. Creare una cartella denominata `js` in `/apps/ws`. Fare clic su **[!UICONTROL Salva tutto]**.

   1. Creare una cartella denominata `libs` in `/apps/ws/js`. Fare clic su **[!UICONTROL Salva tutto]**.

   1. Copia la cartella `/libs/ws/js/libs/jqueryui` in `/apps/ws/js/libs`. Fare clic su **[!UICONTROL Salva tutto]**.

1. Per le personalizzazioni di HTML, effettuate le seguenti operazioni:

   1. In `/apps/ws/js` creare una cartella denominata `runtime`. Fare clic su **[!UICONTROL Salva tutto]**.

   1. In `/apps/ws/js/runtime` creare una cartella denominata `templates`. Fare clic su **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/main.js` in `/apps/ws/js/main.js`.

   1. Copia /libs/ws/js/registry.js in `/apps/ws/js/registry.js`.

1. Fai clic su **[!UICONTROL Salva tutto]**, cancella la cache e aggiorna l&#39;area di lavoro di AEM Forms.

   Accedere all&#39;URL `https://'[server]:[port]'/lc/ws` e accedere con le credenziali amministratore/password. Il browser viene reindirizzato a `https://'[server]:[port]'/lc/apps/ws/index.html`.
