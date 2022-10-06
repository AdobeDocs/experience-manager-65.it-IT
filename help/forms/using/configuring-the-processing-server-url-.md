---
title: Configurazione delle impostazioni di AEM DS
seo-title: Configuring AEM DS settings
description: È necessario specificare l’URL del server di elaborazione prima di inviare un modulo.
seo-description: You need to specify the processing server URL before you submit a form.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Configurazione delle impostazioni di AEM DS{#configuring-aem-ds-settings}

Questo articolo descrive come configurare **Servizio impostazioni di DS AEM**. Questa impostazione può essere utilizzata in più scenari, ad esempio:

* In Gestione della corrispondenza

   * Per configurare il flusso di lavoro AEM Forms
   * Durante l’utilizzo del portale dei moduli per il salvataggio remoto della bozza/invio

* Nei moduli adattivi per i casi in cui il modulo adattivo viene inviato dall’istanza di pubblicazione

Di seguito sono riportati i passaggi per configurare il **[!UICONTROL Impostazioni di AEM DS]**:

1. Apri Configuration Manager nell&#39;istanza di pubblicazione utilizzando l&#39;URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configurazione della console Web AEM](assets/web_configuration_console_new.png)

1. In **[!UICONTROL Configurazione della console Web di Adobe Experience Manager]** finestra, individuare e fare clic **[!UICONTROL Impostazioni di AEM DS]** opzione .

   ![Impostazioni DS](assets/ds_settings_new.png)

1. La **[!UICONTROL Servizio impostazioni di DS AEM]** In questa finestra sono visualizzate le impostazioni di configurazione comuni per i componenti DS AEM.

   ![Servizio impostazioni DS](assets/ds_settings_service_new.png)

1. Aggiungi le seguenti informazioni nei rispettivi campi:

   **[!UICONTROL URL server di elaborazione]**: Il server di elaborazione è il server in cui deve essere attivato il flusso di lavoro Forms o AEM. Può essere lo stesso dell’URL dell’istanza di authoring AEM o dell’altro URL del server (cioè, https://localhost:port/).

   **[!UICONTROL Nome utente del server di elaborazione]**: Nome utente dell’utente del flusso di lavoro [in base all’URL del server utilizzato]

   **[!UICONTROL Password server di elaborazione]**: Password dell&#39;utente del flusso di lavoro

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Durante l&#39;utilizzo dei flussi di lavoro Forms o AEM, prima di effettuare invii dal server di pubblicazione, è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non verrà eseguita.

