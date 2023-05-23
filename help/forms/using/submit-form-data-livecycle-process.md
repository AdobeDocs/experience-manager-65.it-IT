---
title: Configurazione di AEM Forms per inviare i dati del modulo a un processo AEM Forms on JEE
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms consente di integrare i moduli adattivi con i processi di AEM Forms su JEE per l’elaborazione dei dati dei moduli.
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Configurazione di AEM Forms per inviare i dati del modulo a un processo AEM Forms on JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

I moduli adattivi supportano l’invio di dati a un processo AEM Forms su JEE per l’ulteriore elaborazione. Consente di attivare un processo AEM Forms su JEE con i dati disponibili nel modulo inviato. Per consentire all’istanza di AEM Forms di inviare un modulo adattivo al processo AEM Forms on JEE, effettua le seguenti operazioni:

## Configurare il server AEM Forms {#configure-your-aem-forms-server}

Per consentire al server AEM forms di inviare dati a un server AEM Forms su JEE, effettua le seguenti operazioni:

1. Vai alla console di configurazione web AEM all’indirizzo https://[*host*]:[*porta*]/system/console/configMgr.

1. Individua e fai clic su **Adobe configurazione dell’SDK del client del LiveCycle** componente.
1. Fai clic su per modificare l’URL, il nome utente e la password del server di configurazione per AEM Forms sul server JEE.
1. Rivedi le impostazioni e fai clic su **Salva**.

![Adobe configurazione dell’SDK client del LiveCycle](assets/clientsdkconfiguration.jpg)

## Mappare i dati con i campi del processo {#map-data-with-process-fields}

Una volta configurato AEM Forms, mappa l’XML dati e gli allegati dal modulo inviato ai campi nel processo AEM Forms on JEE. Per effettuare questo collegamento:

1. Nella console di configurazione web dell’AEM, fai clic su per modificare **Individuazione processo e richiamo LiveCycle guida** configurazione.
1. Specifica i seguenti parametri:

   * **Nome del parametro XML dati** (obbligatorio): specifica il file di proprietà XML del processo AEM Forms on JEE che deve elaborare i dati inviati. Il valore predefinito è **dataxml**.

   * **Nome del parametro dei file allegati** (facoltativo): specifica l’elenco degli oggetti documento che il processo AEM Forms su JEE deve elaborare. Il valore predefinito è **fileAttachmentsList**.

1. Rivedi le impostazioni e fai clic su **Salva**.

![Individuazione processo e richiamo LiveCycle guida](assets/test3.jpg)

Una volta configurata, l’azione Invia al Forms Workflow elenca i processi del server AEM Forms su JEE contenenti il parametro xml dei dati specificato.
