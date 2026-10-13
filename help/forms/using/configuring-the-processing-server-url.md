---
title: Configurazione delle impostazioni di AEM DS
description: Scopri come specificare l’URL del server di elaborazione prima di inviare un modulo.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%
---
# Configurazione delle impostazioni di AEM DS{#configuring-aem-ds-settings}

In questo articolo viene descritto come configurare il **Servizio impostazioni di AEM DS**. Questa impostazione può essere utilizzata in più scenari, ad esempio:

* Nella gestione della corrispondenza

  * Per la configurazione di AEM Forms Workflow
  * Quando si utilizza il portale Forms per il salvataggio remoto di bozze/invii

* Nei moduli adattivi, nei casi in cui un modulo adattivo viene inviato dall’istanza di pubblicazione

Di seguito sono riportati i passaggi per configurare le **[!UICONTROL impostazioni di AEM DS]**:

1. Apri Configuration Manager nell’istanza di pubblicazione utilizzando l’URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configurazione console Web AEM](assets/web_configuration_console_new.png)

1. Nella finestra **[!UICONTROL Configurazione console Web Adobe Experience Manager]**, individuare e fare clic sull&#39;opzione **[!UICONTROL Impostazioni DS AEM]**.

   ![Impostazioni DS](assets/ds_settings_new.png)

1. Nella finestra **[!UICONTROL Servizio impostazioni di AEM DS]** sono visualizzate le impostazioni di configurazione comuni per i componenti di AEM DS.

   ![Servizio impostazioni DS](assets/ds_settings_service_new.png)

1. Aggiungi le seguenti informazioni nei rispettivi campi:

   **[!UICONTROL URL server di elaborazione]**: il server di elaborazione è il server in cui deve essere attivato il flusso di lavoro di Forms o AEM. Può essere uguale all&#39;URL dell&#39;istanza di authoring di AEM o all&#39;altro URL del server (ovvero https://localhost:port/).

   **[!UICONTROL Elaborazione nome utente server]**: nome utente dell&#39;utente del flusso di lavoro [in base all&#39;URL del server utilizzato]

   **[!UICONTROL Elaborazione password server]**: password utente flusso di lavoro

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Quando si utilizzano flussi di lavoro Forms o AEM, prima di effettuare qualsiasi invio dal server di pubblicazione è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non avrà esito positivo.
   >    
   >
