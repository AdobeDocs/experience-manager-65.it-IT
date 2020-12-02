---
title: Console Panoramica Live Copy
seo-title: Console Panoramica Live Copy
description: Scopri le basi della console Panoramica di Live Copy.
seo-description: Scopri le basi della console Panoramica di Live Copy.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 3%

---


# Console Panoramica Live Copy{#live-copy-overview-console}

La **Live Copy Overview** consente di:

* Visualizzare/gestire l&#39;ereditarietà in un sito:

   * Visualizzare la struttura ad albero della blueprint e la struttura Live Copy corrispondente, insieme al relativo stato di ereditarietà
   * Modificare lo stato di ereditarietà; ad esempio, sospensione, ripresa
   * Visualizza proprietà blueprint e Live Copy

* Eseguire azioni di rollout

## Apertura della panoramica Live Copy {#opening-the-live-copy-overview}

Puoi aprire la panoramica Live Copy da:

* [Pannello laterale Riferimenti di una pagina blueprint (console Siti)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Proprietà di una pagina di blueprint](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Apertura di una panoramica Live Copy - Riferimenti per una pagina Blueprint {#opening-live-copy-overview-references-for-a-blueprint-page}

La **Live Copy Overview** può essere aperta dal pannello laterale **References** della console **Sites**:

1. Nella console **Siti**, [passare alla pagina di blueprint e selezionarla](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Aprire il pannello **[Riferimenti](/help/sites-authoring/basic-handling.md#references)** e selezionare **Live Copy**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >Potete anche aprire prima i Riferimenti e quindi selezionare il blueprint.

1. Selezionare **Live Copy Overview** per visualizzare e utilizzare la panoramica di tutte le Live Copy correlate al progetto selezionato.
1. Utilizzare **Close** per uscire e tornare alla console **Sites**.

### Apertura di una panoramica Live Copy - Proprietà di una pagina Blueprint {#opening-live-copy-overview-properties-of-a-blueprint-page}

È possibile aprire la **Live Copy Overview** quando si visualizzano le proprietà di una pagina di blueprint:

1. Aprire **Properties** per la pagina di blueprint appropriata.
1. Aprite la scheda **Blueprint** - l&#39;opzione **Live Copy Overview** verrà visualizzata nella barra degli strumenti superiore:

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. Selezionare **Live Copy Overview** per visualizzare e utilizzare la panoramica di tutte le Live Copy correlate al modello corrente.

   >[!NOTE]
   >
   >Per ulteriori dettagli, vedere anche l&#39;articolo della Knowledge Base [Livecopy status message - Up-to-date/Green/In Sync](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. Utilizzare **Close** per uscire e tornare alla console **Sites**.

## Utilizzo della panoramica Live Copy {#using-the-live-copy-overview}

È inoltre possibile utilizzare la **Live Copy Overview** per eseguire azioni sulla Live Copy:

1. Aprite la **Live Copy Overview**.
1. Selezionate la pagina di blueprint o Live Copy richiesta; la barra degli strumenti verrà aggiornata per visualizzare le azioni disponibili. Le [azioni](/help/sites-administering/msm.md#terms-used) disponibili dipendono dalla selezione di una pagina [blueprint](#actions-for-a-blueprint-page) o [Live Copy](#actions-for-a-live-copy-page):

### Azioni per una pagina Blueprint {#actions-for-a-blueprint-page}

Quando selezionate una pagina di blueprint, sono disponibili le azioni seguenti:

![chlimage_1-361](assets/chlimage_1-361.png)

* Modifica

   * Aprite la pagina di blueprint per la modifica.

* [Rollout](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Eseguite un rollout per spostare le modifiche dall’origine alla Live Copy.

### Azioni per una pagina Live Copy {#actions-for-a-live-copy-page}

Quando selezionate una pagina Live Copy, sono disponibili le azioni seguenti:

![chlimage_1-362](assets/chlimage_1-362.png)

* Modifica

   * Aprite la pagina Live Copy per la modifica.

* [Stato di relazione](#relationship-status)

   * Visualizzare informazioni sullo stato e l&#39;ereditarietà.

* [Sincronizza](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Sincronizzate una Live Copy per effettuare il pulling delle modifiche dall’origine alla Live Copy.

* [Ripristina](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Reimpostare una pagina Live Copy per rimuovere tutte le cancellazioni di ereditarietà e riportare la pagina allo stesso stato della pagina di origine.

* [Sospendi](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Disattiva temporaneamente la relazione dal vivo tra una Live Copy e la relativa pagina blueprint.

* [Riprendi](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * Riprendi consente di ripristinare una relazione sospesa.

* [Stacca](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Rimuove definitivamente la relazione dal vivo tra una Live Copy e la relativa pagina blueprint.

## Stato di relazione {#relationship-status}

La console **Stato relazione** dispone di due schede che forniscono una serie di funzionalità:

* [Informazioni sullo stato della relazione](#relationship-status-information)
* [Informazioni Live Copy](#live-copy-information)

### Informazioni sullo stato della relazione {#relationship-status-information}

Questa scheda fornisce informazioni dettagliate sullo stato della relazione tra blueprint e live copy:

![chlimage_1-363](assets/chlimage_1-363.png)

### Informazioni Live Copy {#live-copy-information}

Questa scheda consente di visualizzare e modificare la configurazione della Live Copy:

![chlimage_1-364](assets/chlimage_1-364.png)

