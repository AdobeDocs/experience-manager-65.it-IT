---
title: Utilizzo dei punti iniziali
seo-title: Working with Startpoints
description: Passaggi per lavorare con un processo AEM Forms dal dispositivo mobile definito in Workbench.
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Utilizzo dei punti iniziali{#working-with-startpoints}

Un punto di avvio richiama un processo creato in Workbench. È associato a un modulo che richiama il processo al momento dell’invio del modulo.

>[!NOTE]
>
>I termini start point, start process e form vengono utilizzati in modo intercambiabile quando si fa riferimento a questo concetto.

Per avviare un processo dall’app AEM Forms, devi disporre di un punto di partenza di tipo **Area di lavoro** nel tuo processo. Inoltre, è necessario selezionare il **[!UICONTROL Visibile in Workspace mobile]** per il punto iniziale.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Per avviare un processo definito in Workbench**

1. Per visualizzare i punti iniziali disponibili nell’app AEM Forms, passa a [Schermata principale](../../forms/using/home-screen.md).
1. Sulla **[!UICONTROL Pagina principale]** per impostazione predefinita, la **[!UICONTROL Tutti i Forms]** viene visualizzato l&#39;elenco.

   Il punto iniziale è associato a un modulo. Toccare il modulo associato all’interno dell’elenco per aprirlo.

   Viene visualizzato il modulo associato al punto iniziale.

1. Immetti i dettagli nella **[!UICONTROL Startpoint]** modulo.

   È possibile aggiungere annotazioni a questa attività utilizzando [attacco](../../forms/using/add-attachments.md) pulsante .

1. Dopo aver compilato il modulo, tocca **[!UICONTROL Invia]** pulsante .

Se l’app è offline, il modulo e i relativi dati vengono salvati nella cartella Posta in uscita.

Se l’app è online, l’attività viene sincronizzata con il server AEM Forms e assegnata all’utente specificato nel processo.

Per utilizzare l&#39;attività nell&#39;elenco delle attività, vedere [Apertura di un’attività](/help/forms/using/open-task.md).
