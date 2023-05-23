---
title: Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms
seo-title: Generic steps for AEM Forms workspace customization
description: Come iniziare a personalizzare l’interfaccia utente di AEM Forms Workspace.
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

I passaggi generici per eseguire qualsiasi personalizzazione sono i seguenti:

1. Accedi a CRXDE Lite accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Creare un `sling:Folder` cartella denominata `ws` a `/apps`, se non esiste. Per creare un `sling:Folder` cartella, fare clic con il pulsante destro del mouse sulla `apps` cartella e seleziona **[!UICONTROL Crea]** > **[!UICONTROL Crea nodo]**. Specifica il nome come `ws`, seleziona digita come `sling:Folder` e fai clic su **[!UICONTROL OK]**. Clic **[!UICONTROL Salva tutto]**.
1. Sfoglia per `/apps/ws`, e passare al **[!UICONTROL Controllo dell’accesso]** scheda.
1. Seleziona la **[!UICONTROL Archivio]** opzione. In **[!UICONTROL Controllo dell’accesso]** , fare clic su **[!UICONTROL +]** per aggiungere una nuova voce. Clic **[!UICONTROL +]** di nuovo.
1. Cerca e seleziona la **PERM_WORKSPACE_USER** Principale.

   ![Selezionare l&#39;entità PERM_WORKSPACE_USER come parte dei passaggi generici per personalizzare HTML Workspace](assets/perm_workspace_user.png)

1. Assegna `jcr:read` privilegio dell&#39;entità.
1. Clic **[!UICONTROL Salva tutto]**.
1. Copia il `GET.jsp`, `index`, e `html.jsp` file da `/libs/ws` cartella al `/apps/ws` cartella.
1. Copia il `/libs/ws/locales` cartella in `/apps/ws` cartella. Clic **[!UICONTROL Salva tutto]**.
1. Aggiornare i riferimenti e i percorsi relativi in `GET.jsp` come mostrato di seguito, quindi fare clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Per le personalizzazioni CSS, effettua le seguenti operazioni:

   1. Accedi a `/apps/ws` e crea una nuova cartella denominata `css`.

   1. In `css` cartella, crea un nuovo file denominato `newStyle.css`.

   1. Apri `/apps/ws/html`.jsp e cambia da

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   a

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

   a

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Effettua le seguenti operazioni:

   1. Crea una cartella denominata `js` a `/apps/ws`. Clic **[!UICONTROL Salva tutto]**.

   1. Crea una cartella denominata `libs` a `/apps/ws/js`. Clic **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/libs/jqueryui` cartella a `/apps/ws/js/libs`. Clic **[!UICONTROL Salva tutto]**.

1. Per le personalizzazioni di HTML, effettuate le seguenti operazioni:

   1. Sotto `/apps/ws/js`, crea una cartella denominata `runtime`. Clic **[!UICONTROL Salva tutto]**.

   1. Sotto `/apps/ws/js/runtime`, crea una cartella denominata `templates`. Clic **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/main.js` a `/apps/ws/js/main.js`.

   1. Copia /libs/ws/js/registry.js in `/apps/ws/js/registry.js`.

1. Clic **[!UICONTROL Salva tutto]**, cancellare la cache e aggiornare l’area di lavoro di AEM Forms.

   Accedere all’URL `https://'[server]:[port]'/lc/ws` e accedere con le credenziali amministratore/password. Il browser reindirizza a `https://'[server]:[port]'/lc/apps/ws/index.html`.
