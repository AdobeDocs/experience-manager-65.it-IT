---
title: Prova della struttura del sito globalizzata in We.Retail
seo-title: Prova della struttura del sito globalizzata in We.Retail
description: 'null'
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 3%

---


# Prova della struttura del sito globalizzata in We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail è stato costruito con una struttura del sito globalizzata che offre un master di lingua che può essere live-copiato su siti web specifici per paese. Tutto è configurato per consentirvi di sperimentare con questa struttura e le capacità di traduzione integrate.

## Prova {#trying-it-out}

1. Aprite la console Siti da **Navigazione globale -> Siti**.
1. Passate alla vista a colonne (se non già attiva) e selezionate We.Retail. Si noti l&#39;esempio di struttura del paese con Svizzera, Stati Uniti, Francia, ecc., accanto ai master di lingua.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selezionare la Svizzera e vedere le radici linguistiche per le lingue di quel paese. Al di sotto di tali radici non è ancora presente alcun contenuto.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Passate alla vista a elenco e verificate che le copie della lingua per i paesi siano tutte copie dal vivo.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Tornate alla vista a colonne e fate clic sulla Lingua principale per visualizzare le radici della lingua principale con il contenuto. Solo l&#39;inglese ha contenuto.

   We.Retail non viene fornito con alcun contenuto tradotto, ma la struttura e la configurazione sono in atto per consentire di dimostrare i servizi di traduzione.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con l&#39;opzione Lingua principale inglese selezionata, aprite la barra laterale **Riferimenti** nella console Siti e selezionate Copie lingua ****.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Fare clic sulla casella di controllo accanto all&#39;etichetta **Copie lingua** per selezionare tutte le copie della lingua. Nella sezione **Aggiorna copie lingua** della barra laterale, selezionare l&#39;opzione per **Creare un nuovo progetto di traduzione**. Specifica un nome per il progetto e fai clic su **Aggiorna**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Viene creato un progetto per ogni traduzione in lingua. Visualizzarli in **Navigazione -> Progetti**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Clicca sul tedesco per vedere i dettagli del progetto di traduzione. Lo stato è in **Bozza**. Per avviare la traduzione con il servizio di traduzione di Microsoft, fare clic sulla freccia accanto all&#39;intestazione **Processo di traduzione** e selezionare **Start**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Viene avviato il progetto di traduzione. Fate clic sui puntini di sospensione nella parte inferiore della scheda denominata Processo di traduzione per visualizzare i dettagli. Le pagine con lo stato **Pronto per la revisione** sono già state tradotte dal servizio di traduzione.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Se si seleziona una delle pagine nell&#39;elenco e quindi **Anteprima in Siti** nella barra degli strumenti, la pagina tradotta viene aperta nell&#39;editor pagina.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Questa procedura ha dimostrato l&#39;integrazione integrata con la traduzione automatica Microsoft. Utilizzando [AEM Translation Integration Framework](/help/sites-administering/translation.md), è possibile integrarsi con molti servizi di traduzione standard per orchestrare la traduzione di AEM.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consultare il documento di authoring [Translating Content for Multilingual Sites](/help/sites-administering/translation.md) per informazioni tecniche complete.
