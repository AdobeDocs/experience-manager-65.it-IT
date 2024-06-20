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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configurazione delle impostazioni di AEM DS{#configuring-aem-ds-settings}

Questo articolo descrive come configurare **Servizio impostazioni DS AEM**. Questa impostazione può essere utilizzata in più scenari, ad esempio:

* Nella gestione della corrispondenza

   * Per la configurazione di AEM Forms Workflow
   * Quando si utilizza il portale Forms per il salvataggio remoto di bozze/invii

* Nei moduli adattivi, nei casi in cui un modulo adattivo viene inviato dall’istanza di pubblicazione

Di seguito sono riportati i passaggi per configurare **[!UICONTROL Impostazioni di AEM DS]**:

1. Apri Configuration Manager nell’istanza di pubblicazione utilizzando l’URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configurazione console web AEM](assets/web_configuration_console_new.png)

1. In **[!UICONTROL Configurazione console Web Adobe Experience Manager]** , individuare e fare clic sul pulsante **[!UICONTROL Impostazioni di AEM DS]** opzione.

   ![Impostazioni DS](assets/ds_settings_new.png)

1. Il **[!UICONTROL Servizio impostazioni DS AEM]** visualizza le impostazioni di configurazione comuni per i componenti di AEM DS.

   ![Servizio impostazioni DS](assets/ds_settings_service_new.png)

1. Aggiungi le seguenti informazioni nei rispettivi campi:

   **[!UICONTROL Elaborazione URL server]**: il server di elaborazione è il server in cui deve essere attivato il flusso di lavoro Forms o AEM. Può essere lo stesso dell’URL dell’istanza di authoring AEM o dell’altro URL del server (ovvero https://localhost:port/).

   **[!UICONTROL Nome utente server di elaborazione]**: nome utente del flusso di lavoro [in base all’URL del server utilizzato]

   **[!UICONTROL Password server di elaborazione]**: password dell&#39;utente del flusso di lavoro

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Quando si utilizzano flussi di lavoro Forms o AEM, prima di effettuare qualsiasi invio dal server di pubblicazione è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non avrà esito positivo.
   >    
   >
