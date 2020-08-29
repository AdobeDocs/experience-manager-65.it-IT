---
title: Utilizzo dei punti di avvio
seo-title: Utilizzo dei punti di avvio
description: Procedura per utilizzare un processo AEM Forms  dal dispositivo mobile definito in Workbench.
seo-description: Procedura per utilizzare un processo AEM Forms  dal dispositivo mobile definito in Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Utilizzo dei punti di avvio{#working-with-startpoints}

Un startpoint richiama un processo creato in Workbench. È associato a un modulo che richiama il processo al momento dell&#39;invio del modulo.

>[!NOTE]
>
>I termini startpoint, processo di avvio e modulo vengono utilizzati in modo intercambiabile quando si fa riferimento a questo concetto.

Per avviare un processo dall&#39;app AEM Forms , è necessario che nel processo sia presente un punto di partenza di tipo **Workspace** . Inoltre, devi selezionare l&#39;opzione **[!UICONTROL Visibile in Mobile Workspace]** per il punto di avvio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Avvio di un processo definito in Workbench**

1. Per visualizzare i punti di partenza disponibili nell&#39;app AEM Forms , andate alla schermata [](../../forms/using/home-screen.md)iniziale.
1. Nella schermata **[!UICONTROL Home]** , per impostazione predefinita, viene visualizzato l’elenco **[!UICONTROL Tutti i Forms]** .

   Il punto di avvio è associato a un modulo. Toccate il modulo associato all&#39;punto di avvio nell&#39;elenco per aprirlo.

   Viene aperto il modulo associato al punto di avvio.

1. Immettere i dettagli nel modulo **[!UICONTROL Start]** .

   È possibile aggiungere annotazioni a questa attività utilizzando il pulsante [Allegato](../../forms/using/add-attachments.md) .

1. Dopo aver compilato il modulo, toccare il pulsante **[!UICONTROL Invia]** .

Se l&#39;app è offline, il modulo e i relativi dati vengono salvati nella cartella Posta in uscita.

Se l&#39;app è online, l&#39;attività viene sincronizzata con il server AEM Forms  e assegnata all&#39;utente specificato nel processo.

Per utilizzare l&#39;attività nell&#39;elenco delle attività, vedere [Apertura di un&#39;attività](/help/forms/using/open-task.md).
