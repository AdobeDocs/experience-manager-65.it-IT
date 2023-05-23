---
title: Provare la struttura globalizzata del sito in We.Retail
seo-title: Trying out the Globalized Site Structure in We.Retail
description: Provare la struttura globalizzata del sito in We.Retail
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

# Provare la struttura globalizzata del sito in We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail è stato creato con una struttura del sito globalizzata che offre master in lingua che possono essere copiati in tempo reale su siti web specifici del paese. Tutto è configurato per consentire di sperimentare questa struttura e le funzionalità di traduzione incorporate.

## Prova {#trying-it-out}

1. Apri la console Sites da **Navigazione globale -> Sites**.
1. Passa alla vista a colonne (se non è già attiva) e seleziona We.Retail. Si noti l&#39;esempio di struttura dei paesi con Svizzera, Stati Uniti, Francia, ecc., accanto ai master di lingua.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selezionare Svizzera e vedere le radici della lingua per le lingue di quel paese. Tieni presente che non è ancora presente alcun contenuto sotto queste directory principali.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Passa alla vista a elenco e verifica che le copie per lingua dei paesi siano tutte Live Copy.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Torna alla vista a colonne, fai clic su Master lingua e visualizza le directory principali del master lingua con il contenuto. Tieni presente che solo l&#39;inglese ha contenuto.

   We.Retail non include alcun contenuto tradotto, ma è presente una struttura e una configurazione che consentono di dimostrare i servizi di traduzione.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con il master lingua inglese selezionato, apri il **Riferimenti** nella console sites e seleziona **Copie per lingua**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Seleziona la casella di controllo accanto a **Copie per lingua** per selezionare tutte le copie per lingua. In **Aggiorna copie per lingua** nella barra, seleziona l’opzione per **Crea un nuovo progetto di traduzione**. Assegna un nome al progetto e fai clic su **Aggiorna**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Viene creato un progetto per ogni traduzione in lingua. Visualizzali in **Navigazione -> Progetti**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Fai clic sul tedesco per visualizzare i dettagli del progetto di traduzione. Lo stato è in **Bozza**. Per avviare la traduzione con il servizio di traduzione di Microsoft, fai clic sulla freccia accanto al **Lavoro di traduzione** intestazione e selezione **Inizio**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Il progetto di traduzione inizia. Fai clic sui puntini di sospensione nella parte inferiore della scheda con l’etichetta Lavoro di traduzione per visualizzare i dettagli. Pagine con lo stato **Pronto per la revisione** sono già stati tradotti dal servizio di traduzione.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Seleziona una delle pagine dell’elenco e quindi **Anteprima in Sites** nella barra degli strumenti apre la pagina tradotta nell’editor pagina.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Questa procedura illustra l’integrazione integrata con la traduzione automatica Microsoft. Utilizzo di [Framework di integrazione della traduzione AEM](/help/sites-administering/translation.md), puoi integrarti con molti servizi di traduzione standard per orchestrare la traduzione dell’AEM.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta il documento di authoring [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) per dettagli tecnici completi.
