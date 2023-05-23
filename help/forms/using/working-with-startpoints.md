---
title: Utilizzo dei punti d'inizio
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

# Utilizzo dei punti d&#39;inizio{#working-with-startpoints}

Un punto iniziale richiama un processo creato in Workbench. È associata a un modulo che richiama il processo quando il modulo viene inviato.

>[!NOTE]
>
>I termini punti iniziali, processo iniziale e modulo vengono utilizzati in modo intercambiabile quando si fa riferimento a questo concetto.

Per avviare un processo dall’app AEM Forms, devi disporre di un punto d’inizio di tipo **Workspace** nel processo. Inoltre, è necessario selezionare **[!UICONTROL Visibile in Mobile Workspace]** per il punto d&#39;inizio.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Per avviare un processo definito in Workbench**

1. Per visualizzare i punti d&#39;inizio disponibili nell&#39;app AEM Forms, vai a [Schermata iniziale](../../forms/using/home-screen.md).
1. Il giorno **[!UICONTROL Home]** schermata, per impostazione predefinita, la **[!UICONTROL Tutti i Forms]** viene visualizzato l&#39;elenco.

   Il punto iniziale è associato a un modulo. Toccare il modulo associato al punto d&#39;inizio nell&#39;elenco per aprirlo.

   Viene aperto il modulo associato al punto d&#39;inizio.

1. Inserisci i dettagli in **[!UICONTROL Punto d&#39;inizio]** modulo.

   È possibile aggiungere annotazioni a questa attività utilizzando [allegato](../../forms/using/add-attachments.md) pulsante.

1. Dopo aver compilato il modulo, tocca il **[!UICONTROL Invia]** pulsante.

Se l&#39;app non è in linea, il modulo e i relativi dati vengono salvati nella cartella Posta in uscita.

Se l&#39;app è online, l&#39;attività viene sincronizzata con il server AEM Forms e assegnata all&#39;utente specificato nel processo.

Per utilizzare l&#39;attività nell&#39;elenco delle attività, vedere [Apertura di un’attività](/help/forms/using/open-task.md).
