---
title: Integrazione con ExactTarget
description: Scopri come integrare Adobe Experience Manager con ExactTarget.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Integrazione con ExactTarget{#integrating-with-exacttarget}

L’integrazione di Adobe Experience Manager (AEM) con Exact Target consente di gestire e inviare e-mail create nell’AEM tramite Exact Target. Consente inoltre di utilizzare le funzioni di gestione dei lead di Exact Target tramite i moduli AEM sulle pagine AEM.

L’integrazione offre le seguenti funzioni:

* La possibilità di creare e-mail in AEM e pubblicarle in Exact Target per la distribuzione.
* Possibilità di impostare l’azione di un modulo AEM per creare un abbonato a Exact Target.

Una volta configurato ExactTarget, puoi pubblicare newsletter o e-mail in ExactTarget. Consulta [Pubblicazione di newsletter su un servizio e-mail](/help/sites-authoring/personalization.md).

## Creazione di una configurazione ExactTarget {#creating-an-exacttarget-configuration}

È possibile aggiungere configurazioni ExactTarget tramite Cloud Services o Strumenti. Entrambi i metodi sono descritti in questa sezione.

### Configurazione di ExactTarget tramite Cloud Services {#configuring-exacttarget-via-cloudservices}

Per creare una configurazione ExactTarget in Cloud Services:

1. Nella pagina di benvenuto, fai clic su **Cloud Services**. (oppure accedere direttamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Clic **ExactTarget** e poi **Configura**. Viene visualizzata la finestra di configurazione ExactTarget.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Inserisci un titolo e, facoltativamente, un nome e fai clic su **Crea**. Il **Impostazioni ExactTarget** viene visualizzata la finestra di configurazione.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Inserisci il nome utente e la password, quindi seleziona un endpoint API (ad esempio, **https://webservice.exacttarget.com/Service.asmx**).
1. Clic **Connettiti a ExactTarget.** Una volta stabilita la connessione, viene visualizzata una finestra di dialogo di successo. casella Clic **OK** per uscire dalla finestra.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleziona un account, se disponibile. L’account è per i clienti Enterprise 2.0. Fai clic su **OK**.

   ExactTarget configurato. Puoi modificare la configurazione facendo clic su **Modifica**. Puoi passare a ExactTarget facendo clic su **Vai a ExactTarget**.

1. AEM fornisce ora una funzione di estensione dei dati. Puoi importare colonne di estensione dati ExactTarget. Per configurarlo, fai clic sul segno &quot;+&quot; accanto alla configurazione ExactTarget creata correttamente. Puoi selezionare una qualsiasi delle estensioni di dati esistenti dall’elenco a discesa. Per ulteriori informazioni su come configurare le estensioni dati, consulta [Documentazione di ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   Le colonne di estensione dei dati importate possono essere successivamente utilizzate tramite **Testo e personalizzazione** componente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configurazione di ExactTarget tramite Strumenti {#configuring-exacttarget-via-tools}

Per creare una configurazione ExactTarget in Strumenti:

1. Nella pagina di benvenuto, fai clic su **Strumenti**. Oppure naviga direttamente da `https://<hostname>:<port>/misadmin#/etc`.
1. Seleziona **Strumenti**, quindi **Configurazioni Cloud Services,** allora **ExactTarget**.
1. Clic **Nuovo** per aprire la finestra **Crea pagina **.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Inserisci il **Titolo** e facoltativamente **Nome** e fai clic su **Crea**.
1. Immettere le informazioni di configurazione come descritto al punto 4 della procedura precedente. Segui questa procedura per completare la configurazione di ExactTarget.

### Aggiunta di più configurazioni {#adding-multiple-configurations}

Per aggiungere più configurazioni:

1. Nella pagina di benvenuto, fai clic su **Cloud Services** e fai clic su **ExactTarget**. Clic **Mostra configurazioni** che viene visualizzato se sono disponibili una o più configurazioni ExactTarget. Sono elencate tutte le configurazioni disponibili.
1. Fai clic su **+** Accanto a Configurazioni disponibili. Verrà aperto il **Creare configurazioni** finestra. Per creare una configurazione, segui la procedura di configurazione precedente.
