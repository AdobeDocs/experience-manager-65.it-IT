---
title: Integrazione con ExactTarget
seo-title: Integrazione con ExactTarget
description: Scoprite come integrare AEM con ExactTarget.
seo-description: Scoprite come integrare AEM con ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---


# Integrazione con ExactTarget{#integrating-with-exacttarget}

L’integrazione di AEM con Exact Target consente di gestire e inviare e-mail create in AEM tramite Exact Target. Consente inoltre di utilizzare le funzioni di gestione dei lead di Exact Target tramite moduli AEM su AEM pagine.

L&#39;integrazione offre le seguenti funzionalità:

* La possibilità di creare e AEM e pubblicarli su Exact Target per la distribuzione.
* Possibilità di impostare l&#39;azione di un modulo AEM per creare un utente iscritto a Exact Target.

Una volta configurato ExactTarget, potete pubblicare newsletter o e-mail su ExactTarget. Consultate [Pubblicazione di newsletter su un servizio e-mail](/help/sites-authoring/personalization.md).

## Creazione di una configurazione ExactTarget {#creating-an-exacttarget-configuration}

Le configurazioni ExactTarget possono essere aggiunte tramite Cloudservices o Strumenti. Entrambi i metodi sono descritti in questa sezione.

### Configurazione di ExactTarget tramite Cloudservices {#configuring-exacttarget-via-cloudservices}

Per creare una configurazione ExactTarget in Cloud Services:

1. Nella pagina di benvenuto, fate clic su **Cloud Services**. (oppure accedere direttamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Fare clic su **ExactTarget**, quindi su **Configura**. Viene visualizzata la finestra di configurazione ExactTarget.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Immettete un titolo ed eventualmente un nome e fate clic su **Crea**. Viene visualizzata la finestra di configurazione **ExactTarget Settings**.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Inserite il nome utente e la password e selezionate un endpoint API (ad esempio, **https://webservice.exacttarget.com/Service.asmx**).
1. Fate clic su **Connetti a ExactTarget.** Una volta stabilita la connessione, viene visualizzata una finestra di dialogo di successo. Fare clic su **OK** per uscire dalla finestra.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selezionate un account, se disponibile. L&#39;account è per i clienti Enterprise 2.0. Fai clic su **OK**.

   ExactTarget è stato configurato. È possibile modificare la configurazione facendo clic su **Modifica**. Per accedere a ExactTarget, fai clic su **Vai a ExactTarget**.

1. AEM ora offre una funzione di estensione dei dati. Potete importare le colonne delle estensioni di dati ExactTarget. Per configurarlo, fate clic sul segno &quot;+&quot; visualizzato insieme alla configurazione ExactTarget creata correttamente. Qualsiasi estensione di dati esistente può essere selezionata dall&#39;elenco a discesa. Per ulteriori informazioni sulla configurazione delle estensioni di dati, consultare la [documentazione ExactTarget](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   Le colonne di estensione dei dati importate possono essere utilizzate in seguito tramite il componente **Testo e personalizzazione**.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configurazione di ExactTarget tramite gli strumenti {#configuring-exacttarget-via-tools}

Per creare una configurazione ExactTarget in Strumenti:

1. Nella pagina di benvenuto, fate clic su **Strumenti**. Oppure andate direttamente a `https://<hostname>:<port>/misadmin#/etc`.
1. Selezionare **Strumenti**, quindi **Configurazioni Cloud Services,** quindi **ExactTarget**.
1. Fare clic su **New** per aprire la finestra **Create Page **(Crea pagina).

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Immettere il **Titolo** e facoltativamente il **Nome**, quindi fare clic su **Crea**.
1. Immettete le informazioni di configurazione come indicato al punto 4 della procedura precedente. Seguite questa procedura per completare la configurazione di ExactTarget.

### Aggiunta di configurazioni multiple {#adding-multiple-configurations}

Per aggiungere più configurazioni:

1. Nella pagina di benvenuto, fate clic su **Cloud Services** e fate clic su **ExactTarget**. Fate clic sul pulsante **Mostra configurazioni** che viene visualizzato se sono disponibili una o più configurazioni ExactTarget. Vengono elencate tutte le configurazioni disponibili.
1. Fare clic sul segno **+** accanto alle configurazioni disponibili. Si apre la finestra **Crea configurazioni**. Seguite la procedura di configurazione precedente per creare una nuova configurazione.