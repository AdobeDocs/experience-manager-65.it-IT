---
title: Panoramica Live Copy
seo-title: Live Copy Overview Console
description: Scopri le nozioni di base della console Panoramica di Live Copy.
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 37%

---

# Panoramica Live Copy{#live-copy-overview-console}

La **Panoramica Live Copy** consente di:

* Visualizzare/gestire l’ereditarietà in un sito:

   * Visualizza la struttura della blueprint e la struttura della Live Copy corrispondente, insieme al relativo stato di ereditarietà
   * Modificare lo stato di ereditarietà; ad esempio, sospendere, riprendere
   * Visualizzare le proprietà blueprint e Live Copy

* Eseguire azioni di rollout

## Apertura della Panoramica Live Copy {#opening-the-live-copy-overview}

Puoi aprire la Panoramica Live Copy da:

* [Pannello laterale Riferimenti di una pagina blueprint (console Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Proprietà di una pagina blueprint](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Apertura della panoramica di Live Copy - Riferimenti per una pagina di blueprint {#opening-live-copy-overview-references-for-a-blueprint-page}

La **Panoramica Live Copy** può essere aperto dal pannello laterale **Riferimenti** nella console **Sites**:

1. Nella console **Sites**, [passa alla pagina blueprint e selezionala](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri **[Riferimenti](/help/sites-authoring/basic-handling.md#references)** e seleziona **Live Copy**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >È inoltre possibile aprire prima i Riferimenti e quindi selezionare la blueprint.

1. Seleziona **Panoramica di Live Copy** per mostrare e utilizzare la panoramica di tutte le Live Copy relative alla blueprint selezionata.
1. Utilizza **Chiudi** per uscire e tornare alla console **Sites**.

### Apertura della panoramica di Live Copy - Proprietà di una pagina blueprint {#opening-live-copy-overview-properties-of-a-blueprint-page}

La **Panoramica Live Copy** può essere aperta quando si visualizzano le proprietà di una pagina blueprint:

1. Apri **Proprietà** per la pagina blueprint appropriata.
1. Apri la scheda **Blueprint**: l’opzione **Panoramica Live Copy** è disponibile nella barra degli strumenti superiore:

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. Seleziona **Panoramica di Live Copy** per mostrare e utilizzare la panoramica di tutte le Live Copy relative al modello corrente.

   >[!NOTE]
   >
   >Per ulteriori dettagli vedi anche l&#39;articolo della Knowledge Base [Messaggio di stato di Livecopy - Up-to-date/Green/In Sync](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. Utilizza **Chiudi** per uscire e tornare alla console **Sites**.

## Utilizzo della Panoramica Live Copy {#using-the-live-copy-overview}

La **Panoramica di Live Copy** può essere utilizzato anche per eseguire azioni sulla Live Copy:

1. Apri **Panoramica Live Copy**.
1. Seleziona la pagina blueprint o Live Copy richiesta. La barra degli strumenti verrà aggiornata per mostrare le azioni disponibili. La [azioni](/help/sites-administering/msm.md#terms-used) disponibile a seconda che sia stata selezionata una [blueprint](#actions-for-a-blueprint-page) o [Live Copy](#actions-for-a-live-copy-page) pagina:

### Azioni per una pagina blueprint {#actions-for-a-blueprint-page}

Quando selezioni una pagina blueprint, sono disponibili le seguenti azioni:

![chlimage_1-361](assets/chlimage_1-361.png)

* Modifica

   * Apri la pagina blueprint per la modifica.

* [Rollout](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Esegui un rollout per inviare le modifiche dall’origine alla Live Copy.

### Azioni per una pagina Live Copy {#actions-for-a-live-copy-page}

Quando selezioni una pagina Live Copy sono disponibili le seguenti azioni:

![chlimage_1-362](assets/chlimage_1-362.png)

* Modifica

   * Apri la pagina Live Copy per la modifica.

* [Stato di relazione](#relationship-status)

   * Visualizza informazioni sullo stato e sull’ereditarietà.

* [Sincronizza](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Sincronizza una Live Copy per estrarre le modifiche dall’origine alla Live Copy.

* [Ripristina](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Reimposta una pagina Live Copy per rimuovere tutte le cancellazioni di ereditarietà e ripristinare la pagina sullo stesso stato della pagina sorgente.

* [Sospendi](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Disattiva temporaneamente la relazione live tra una Live Copy e la relativa pagina blueprint.

* [Riprendi](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * Riprendi consente di ripristinare una relazione sospesa.

* [Stacca](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Rimuove definitivamente la relazione live tra una Live Copy e la relativa pagina blueprint.

## Stato di relazione {#relationship-status}

La console **Stato relazione** dispone di due schede che forniscono una serie di funzionalità:

* [Informazioni sullo stato della relazione](#relationship-status-information)
* [Informazioni su Live Copy](#live-copy-information)

### Informazioni sullo stato della relazione {#relationship-status-information}

Questa scheda fornisce informazioni dettagliate sullo stato della relazione tra blueprint e live copy:

![chlimage_1-363](assets/chlimage_1-363.png)

### Informazioni su Live Copy {#live-copy-information}

Questa scheda ti consente di visualizzare e modificare la configurazione della Live Copy:

![chlimage_1-364](assets/chlimage_1-364.png)
