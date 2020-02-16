---
title: Passaggi generici per la personalizzazione dell'area di lavoro di AEM Forms
seo-title: Passaggi generici per la personalizzazione dell'area di lavoro di AEM Forms
description: Come iniziare a personalizzare l’interfaccia utente dell’area di lavoro Moduli AEM.
seo-description: Come iniziare a personalizzare l’interfaccia utente dell’area di lavoro Moduli AEM.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms{#generic-steps-for-aem-forms-workspace-customization}

I passaggi generici per eseguire eventuali personalizzazioni sono:

1. Accedete a CRXDE Lite accedendo `https://[server]:[port]/lc/crx/de/index.jsp`.
1. Create una cartella denominata `ws`in `/apps`, se non esiste. Fate clic su **[!UICONTROL Salva tutto]**.
1. Individuare `/apps/ws`e passare alla scheda Controllo **** accesso.
1. Nell&#39;elenco Controllo **** accesso, fare clic su **[!UICONTROL +]** per aggiungere una nuova voce. Fate di nuovo clic **[!UICONTROL +]** .
1. Cercate e selezionate **PERM_WORKSPACE_USER** Principal.

   ![Selezionate l&#39;entità PERM_WORKSPACE_USER come parte dei passaggi generici per personalizzare l&#39;area di lavoro HTML](assets/perm_workspace_user.png)

1. Dia `jcr:read` dei privilegi al Principal.
1. Fate clic su **[!UICONTROL Salva tutto]**.
1. Copiate i `GET.jsp` file e `html.jsp`i file dalla `/libs/ws`cartella alla `/apps/ws` cartella.
1. Copiate la `/libs/ws/locales` cartella nella `/apps/ws` cartella. Fate clic su **[!UICONTROL Salva tutto]**.
1. Aggiornate i riferimenti e i percorsi relativi nel `GET.jsp` file, come illustrato di seguito, quindi fate clic su **[!UICONTROL Salva tutto]**.

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Effettuate le seguenti operazioni per le personalizzazioni CSS:

   1. Passate alla `/apps/ws` cartella e create una nuova cartella denominata `css`.

   1. Nella cartella della `css`cartella, create un nuovo file denominato `newStyle.css`.

   1. Open `/apps/ws/html`.jsp e modifica da

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   a

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Inserite la voce del file CSS definito dall&#39;utente dopo la voce newStyle.css, come illustrato sopra.

1. Nel file /apps/ws/html.jsp, modificare da

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   a

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Effettua le seguenti operazioni:

   1. Create una cartella denominata `js`in `/apps/ws`. Fate clic su **[!UICONTROL Salva tutto]**.

   1. Create una cartella denominata `libs`in `/apps/ws/js`. Fate clic su **[!UICONTROL Salva tutto]**.

   1. Create una cartella denominata `jqueryui`in `/apps/ws/js/libs`. Fate clic su **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` in `/apps/ws/js/libs/jqueryui`. Fate clic su **[!UICONTROL Salva tutto]**.

1. Effettuate le seguenti operazioni per le personalizzazioni HTML:

   1. In `/apps/ws/js`, create una cartella denominata `runtime`. Fate clic su **[!UICONTROL Salva tutto]**.

   1. In `/apps/ws/js/runtime`, create una cartella denominata `templates`. Fate clic su **[!UICONTROL Salva tutto]**.

   1. Copia `/libs/ws/js/main.js` in `/apps/ws/js/main.js`.

   1. Copiate /libs/ws/js/registry.js in `/apps/ws/js/registry.js`.

1. Fai clic su **[!UICONTROL Salva tutto]**, cancella la cache e aggiorna l&#39;area di lavoro di AEM Forms.

   Accedete all’URL `https://[server]:[port]/lc/ws` e accedete con le credenziali di amministratore/password. Il browser si reindirizzerà a `https://[server]:[port]/lc/apps/ws/index.html`.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
