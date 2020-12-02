---
title: Configurazione delle impostazioni di AEM DS
seo-title: Configurazione delle impostazioni di AEM DS
description: È necessario specificare l'URL del server di elaborazione prima di inviare il modulo.
seo-description: È necessario specificare l'URL del server di elaborazione prima di inviare il modulo.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Configurazione AEM impostazioni DS{#configuring-aem-ds-settings}

Questo articolo descrive come configurare **AEM DS Settings Service**. Questa impostazione può essere utilizzata in più scenari, ad esempio:

* In Gestione della corrispondenza

   * Per configurare  flusso di lavoro AEM Forms
   * Durante l&#39;utilizzo del portale dei moduli per il salvataggio remoto della bozza/invio

* Nei moduli adattivi per i casi in cui il modulo adattivo viene inviato dall’istanza di pubblicazione

Seguono i passaggi per configurare le **[!UICONTROL AEM Impostazioni DS]**:

1. Aprite Configuration Manager nell&#39;istanza di pubblicazione utilizzando l&#39;URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configurazione AEM console Web](assets/web_configuration_console_new.png)

1. Nella finestra **[!UICONTROL Configurazione console Web Adobe Experience Manager]**, individuare e fare clic sull&#39;opzione **[!UICONTROL AEM Impostazioni DS]**.

   ![Impostazioni DS](assets/ds_settings_new.png)

1. Nella finestra **[!UICONTROL AEM DS Settings Service]** vengono visualizzate le impostazioni di configurazione comuni per AEM componenti DS.

   ![Servizio impostazioni DS](assets/ds_settings_service_new.png)

1. Aggiungete le seguenti informazioni nei rispettivi campi:

   **[!UICONTROL URL]** server di elaborazione: Il server di elaborazione è il server in cui è necessario attivare il flusso di lavoro Forms o AEM. Può corrispondere all’URL dell’istanza di creazione AEM o dell’altro URL server (https://localhost:port/).

   **[!UICONTROL Nome]** utente del server di elaborazione: Nome utente dell’utente del flusso di lavoro  [in base all’URL del server utilizzato]

   **[!UICONTROL Password]** del server di elaborazione: Password utente flusso di lavoro

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Durante l&#39;utilizzo di flussi di lavoro Forms o AEM, prima di inviare qualsiasi invio dal server di pubblicazione è necessario configurare il servizio Impostazioni DS. In caso contrario, la presentazione del modulo non può essere effettuata.


