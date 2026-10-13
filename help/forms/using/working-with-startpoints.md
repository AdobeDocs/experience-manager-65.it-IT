---
title: Utilizzo dei punti iniziali
description: Passaggi per lavorare con un processo Adobe Experience Manager Forms dal dispositivo mobile definito in Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%
---

# Utilizzo dei punti iniziali{#working-with-startpoints}

>[!NOTE]
>
>L’app AEM Forms è attualmente obsoleta. Per domande o assistenza, contattare [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Un punto iniziale richiama un processo creato in Workbench. È associata a un modulo che richiama il processo quando il modulo viene inviato.

>[!NOTE]
>
>I termini punti iniziali, processo iniziale e modulo vengono utilizzati in modo intercambiabile quando si fa riferimento a questo concetto.

Per avviare un processo dall&#39;app Adobe Experience Manager (AEM) Forms, devi avere un punto d&#39;inizio di tipo **Workspace** nel processo. È inoltre necessario selezionare l&#39;opzione **[!UICONTROL Visibile in Mobile Workspace]** per il punto iniziale.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Per avviare un processo definito in Workbench**

1. Per visualizzare i punti iniziali disponibili nell&#39;app AEM Forms, vai alla [schermata iniziale](../../forms/using/home-screen.md).
1. Nella schermata **[!UICONTROL Home]**, per impostazione predefinita, viene visualizzato l&#39;elenco **[!UICONTROL All Forms]**.

   Il punto iniziale è associato a un modulo. Selezionare il modulo associato al punto d&#39;inizio nell&#39;elenco per aprirlo.

   Viene aperto il modulo associato al punto d&#39;inizio.

1. Immetti i dettagli nel modulo **[!UICONTROL Startpoint]**.

   Puoi aggiungere annotazioni a questa attività utilizzando il pulsante [allegato](../../forms/using/add-attachments.md).

1. Dopo aver compilato il modulo, seleziona il pulsante **[!UICONTROL Invia]**.

Se l&#39;app non è in linea, il modulo e i relativi dati vengono salvati nella cartella Posta in uscita.

Se l&#39;app è online, l&#39;attività viene sincronizzata con il server AEM Forms e assegnata all&#39;utente specificato nel processo.

Per utilizzare l&#39;attività nell&#39;elenco delle attività, vedere [Apertura di un&#39;attività](/help/forms/using/open-task.md).
