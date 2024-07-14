---
title: Provare la struttura globalizzata del sito in We.Retail
description: Scopri come provare una struttura globalizzata del sito in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 5%

---

# Provare la struttura globalizzata del sito in We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail è stato creato con una struttura del sito globalizzata che offre un master in lingua che può essere copiato in tempo reale su siti web specifici del paese. Tutto è configurato per consentire di sperimentare questa struttura e le funzionalità di traduzione incorporate.

## Prova {#trying-it-out}

1. Apri la console Sites da **Navigazione globale > Sites**.
1. Passa alla vista a colonne (se non è già attiva) e seleziona We.Retail. Prendi nota dell’esempio di struttura dei paesi con Svizzera, Stati Uniti, Francia e così via, accanto al master lingua.

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. Selezionare Svizzera e vedere le radici della lingua per le lingue di quel paese. Non c&#39;è ancora alcun contenuto sotto queste radici.

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. Passa alla vista a elenco e verifica che le copie per lingua dei paesi siano tutte Live Copy.

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. Torna alla vista a colonne, fai clic sulla Master lingua e visualizza le directory principali della lingua con il contenuto. Solo l&#39;inglese ha dei contenuti.

   We.Retail non include alcun contenuto tradotto, ma la struttura e la configurazione sono implementate per consentirti di dimostrare i servizi di traduzione.

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. Con il master in lingua inglese selezionato, apri la barra **Riferimenti** nella console Sites e seleziona **Copie per lingua**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Seleziona tutte le copie per lingua selezionando la casella di controllo accanto all&#39;etichetta **Copie per lingua**. Nella sezione **Aggiorna copie per lingua** della barra, seleziona l&#39;opzione per **Creare un nuovo progetto di traduzione**. Specifica un nome per il progetto e fai clic su **Aggiorna**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Viene creato un progetto per ogni traduzione in lingua. Visualizzali in **Navigazione > Progetti**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Fai clic su Tedesco per visualizzare i dettagli del progetto di traduzione. Stato in **Bozza**. Per avviare la traduzione con il servizio di traduzione di Microsoft®, fai clic sulla freccia accanto all&#39;intestazione **Processo di traduzione** e seleziona **Inizio**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Il progetto di traduzione inizia. Fai clic sull’ellissi nella parte inferiore della scheda etichettata Lavoro di traduzione per visualizzare i dettagli. Le pagine con lo stato **Pronto per la revisione** sono già state tradotte dal servizio di traduzione.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Selezionando una delle pagine dell&#39;elenco e quindi **Anteprima in Sites** nella barra degli strumenti, la pagina tradotta verrà aperta nell&#39;editor di pagine.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Questa procedura ha dimostrato l&#39;integrazione integrata con la traduzione automatica Microsoft®. Utilizzando il [framework di integrazione della traduzione AEM](/help/sites-administering/translation.md), puoi integrarti con molti servizi di traduzione standard per orchestrare la traduzione dell&#39;AEM.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, vedere il documento di authoring [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) per i dettagli tecnici completi.
