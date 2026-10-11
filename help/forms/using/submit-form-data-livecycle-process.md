---
title: Configurazione di AEM Forms per inviare dati a un processo AEM Forms on JEE
description: Integra i moduli adattivi con i processi di AEM Forms su JEE per l’elaborazione dei dati dei moduli.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%
---
# Configurazione di AEM Forms per inviare i dati del modulo a un modulo AEM durante il processo JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

I moduli adattivi supportano l’invio di dati al processo AEM Forms su JEE per l’ulteriore elaborazione. Consente di attivare un processo AEM Forms su JEE con i dati disponibili nel modulo inviato. Effettua le seguenti operazioni per consentire all’istanza di AEM Forms di inviare un modulo adattivo ad AEM Forms durante il processo JEE:

## Configurare il server AEM Forms {#configure-your-aem-forms-server}

Effettua le seguenti operazioni per consentire al tuo server AEM Forms di inviare dati a un server AEM Forms su JEE:

1. Vai alla console di configurazione Web di AEM all&#39;indirizzo https://[*host*]:[*porta*]/system/console/configMgr.

1. Individua e fai clic sul componente **Configurazione SDK client Adobe LiveCycle**.
1. Fai clic su per modificare l’URL, il nome utente e la password del server di configurazione per AEM Forms sul server JEE.
1. Rivedi le impostazioni e fai clic su **Salva**.

![Configurazione SDK client Adobe LiveCycle](assets/clientsdkconfiguration.jpg)

## Mappare i dati con i campi del processo {#map-data-with-process-fields}

Dopo aver configurato AEM Forms, mappa l’XML dati e gli allegati dal modulo inviato ai campi nel processo AEM Forms on JEE. Effettua le seguenti operazioni:

1. Nella console di configurazione Web di AEM, fare clic per modificare la configurazione **Guide LiveCycle Process Locator and Invoker**.
1. Specifica i seguenti parametri:

   * **Nome del parametro XML dati** (obbligatorio): specificare il file di proprietà XML del processo AEM Forms su JEE che deve elaborare i dati inviati. Il valore predefinito è **dataxml**.

   * **Nome del parametro dei file allegati** (facoltativo): specificare l&#39;elenco degli oggetti documento che il processo AEM Forms su JEE deve elaborare. Il valore predefinito è **fileAttachmentsList**.

1. Rivedi le impostazioni e fai clic su **Salva**.

![Guida a LiveCycle Process Locator e Invoker](assets/test3.jpg)

Una volta configurata, l’azione Invia a Forms Workflow elenca i processi del server AEM Forms su JEE contenenti il parametro xml dei dati specificato.
