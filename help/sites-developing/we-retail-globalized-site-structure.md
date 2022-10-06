---
title: Prova la struttura del sito globale in We.Retail
seo-title: Trying out the Globalized Site Structure in We.Retail
description: Prova la struttura del sito globale in We.Retail
seo-description: null
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 2%

---

# Prova la struttura del sito globale in We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail è stato creato con una struttura del sito globalizzata che offre master in lingua che possono essere live copiati su siti web specifici per ciascun paese. Tutto è pronto per sperimentare questa struttura e le funzionalità di traduzione integrate.

## Prova {#trying-it-out}

1. Apri la console Sites da **Navigazione globale -> Sites**.
1. Passa alla vista a colonne (se non è già attiva) e seleziona We.Retail. Si noti l&#39;esempio di struttura del paese con Svizzera, Stati Uniti, Francia, ecc., accanto ai master di lingua.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selezionare la Svizzera e vedere le radici linguistiche per le lingue di quel paese. Tieni presente che non esiste ancora alcun contenuto al di sotto di queste radici.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Passa alla vista a elenco e osserva che le copie della lingua per i paesi sono tutte Live Copy.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Torna alla vista a colonne e fai clic su Lingua master e visualizza le radici principali della lingua con il contenuto. Solo l’inglese ha del contenuto.

   We.Retail non viene fornito con contenuti tradotti, ma la struttura e la configurazione sono in atto per consentirti di dimostrare i servizi di traduzione.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con l’opzione English Language Master selezionata, apri le **Riferimenti** nella console Sites e seleziona **Copie per lingua**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Seleziona la casella di controllo accanto a **Copie per lingua** per selezionare tutte le copie della lingua. In **Aggiorna copie in lingua** nella sezione della barra, seleziona l’opzione per **Crea un nuovo progetto di traduzione**. Specifica un nome per il progetto e fai clic su **Aggiorna**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Viene creato un progetto per ogni traduzione in lingua. Visualizza sotto **Navigazione -> Progetti**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Clicca sul tedesco per vedere i dettagli del progetto di traduzione. Lo stato è in **Bozza**. Per avviare la traduzione con il servizio di traduzione Microsoft, fai clic sulla freccia accanto al **Processo di traduzione** e seleziona **Inizio**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Viene avviato il progetto di traduzione. Fai clic sull&#39;ellissi nella parte inferiore della scheda denominata Processo di traduzione per visualizzare i dettagli. Pagine con lo stato **Pronto per la revisione** sono già stati tradotti dal servizio di traduzione.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selezione di una delle pagine dell’elenco e quindi **Anteprima in Sites** nella barra degli strumenti apre la pagina tradotta nell’editor di pagine.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Questa procedura illustra l’integrazione integrata con la traduzione automatica Microsoft. Utilizzo della [Framework di integrazione della traduzione AEM](/help/sites-administering/translation.md), è possibile integrare con molti servizi di traduzione standard per orchestrare la traduzione di AEM.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta il documento di authoring [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) per informazioni tecniche complete.
