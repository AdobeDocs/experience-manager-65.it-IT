---
title: Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms
seo-title: Generic steps for AEM Forms workspace customization
description: Come iniziare a personalizzare l’interfaccia utente dell’area di lavoro di AEM Forms.
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

I passaggi generici per eseguire eventuali personalizzazioni sono i seguenti:

1. Accedi a CRXDE Lite accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Crea un `sling:Folder` cartella denominata `ws` a `/apps`, se non esiste. Per creare una `sling:Folder` fai clic con il pulsante destro del mouse sulla cartella `apps` e seleziona **[!UICONTROL Crea]** > **[!UICONTROL Crea nodo]**. Specifica il nome come `ws`, seleziona il tipo come `sling:Folder` e fai clic su **[!UICONTROL OK]**. Fai clic su **[!UICONTROL Salva tutto]**.
1. Sfoglia per `/apps/ws`e naviga fino al **[!UICONTROL Controllo degli accessi]** scheda .
1. Seleziona la **[!UICONTROL Archivio]** opzione . In **[!UICONTROL Controllo degli accessi]** elenco, fai clic su **[!UICONTROL +]** per aggiungere una nuova voce. Fai clic su **[!UICONTROL +]** di nuovo.
1. Cerca e seleziona la **PERM_WORKSPACE_USER** Principale

   ![Selezionare l&#39;entità PERM_WORKSPACE_USER come parte dei passaggi generici per personalizzare HTML Workspace](assets/perm_workspace_user.png)

1. Dare `jcr:read` privilegio al Principale.
1. Fai clic su **[!UICONTROL Salva tutto]**.
1. Copia il `GET.jsp`, `index`e `html.jsp` file dal `/libs/ws` nella cartella `/apps/ws` cartella.
1. Copia il `/libs/ws/locales` nella cartella `/apps/ws` cartella. Fai clic su **[!UICONTROL Salva tutto]**.
1. Aggiorna i riferimenti e i percorsi relativi nel `GET.jsp` come mostrato di seguito, quindi fai clic su **[!UICONTROL Salva tutto]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Per le personalizzazioni CSS, procedi come segue:

   1. Passa a `/apps/ws` e crea una nuova cartella denominata `css`.

   1. In `css` creare un nuovo file denominato `newStyle.css`.

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
   >Posiziona la voce del file CSS definito dall&#39;utente dopo la voce di style.css, come mostrato sopra.

1. Nel file /apps/ws/html.jsp, cambia da

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   a

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Effettua le seguenti operazioni:

   1. Crea una cartella denominata `js` a `/apps/ws`. Fai clic su **[!UICONTROL Salva tutto]**.

   1. Crea una cartella denominata `libs` a `/apps/ws/js`. Fai clic su **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/libs/jqueryui` cartella a `/apps/ws/js/libs`. Fai clic su **[!UICONTROL Salva tutto]**.

1. Effettua le seguenti operazioni per le personalizzazioni di HTML:

   1. Sotto `/apps/ws/js`, crea una cartella denominata `runtime`. Fai clic su **[!UICONTROL Salva tutto]**.

   1. Sotto `/apps/ws/js/runtime`, crea una cartella denominata `templates`. Fai clic su **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/main.js` a `/apps/ws/js/main.js`.

   1. Copia /libs/ws/js/registry.js in `/apps/ws/js/registry.js`.

1. Fai clic su **[!UICONTROL Salva tutto]**, cancella la cache e aggiorna l’area di lavoro AEM Forms.

   Accedere all’URL `https://'[server]:[port]'/lc/ws` e accedi con le credenziali di amministratore/password. Il browser reindirizza a `https://'[server]:[port]'/lc/apps/ws/index.html`.
