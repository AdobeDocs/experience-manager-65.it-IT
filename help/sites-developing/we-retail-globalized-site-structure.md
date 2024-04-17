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

1. Con il master lingua inglese selezionato, apri il **Riferimenti** nella console sites e seleziona **Copie per lingua**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Seleziona la casella di controllo accanto a **Copie per lingua** per selezionare tutte le copie per lingua. In **Aggiorna copie per lingua** nella barra, seleziona l’opzione per **Crea un nuovo progetto di traduzione**. Assegna un nome al progetto e fai clic su **Aggiorna**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Viene creato un progetto per ogni traduzione in lingua. Visualizzali in **Navigazione > Progetti**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. Fai clic su Tedesco per visualizzare i dettagli del progetto di traduzione. Lo stato è in **Bozza**. Per avviare la traduzione con il servizio di traduzione di Microsoft®, fai clic sulla freccia accanto al **Lavoro di traduzione** intestazione e selezione **Inizio**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Il progetto di traduzione inizia. Fai clic sull’ellissi nella parte inferiore della scheda etichettata Lavoro di traduzione per visualizzare i dettagli. Pagine con lo stato **Pronto per la revisione** sono già stati tradotti dal servizio di traduzione.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Seleziona una delle pagine dell’elenco e quindi **Anteprima in Sites** nella barra degli strumenti apre la pagina tradotta nell’editor pagina.

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>Questa procedura ha dimostrato l&#39;integrazione integrata con la traduzione automatica Microsoft®. Utilizzo di [Framework di integrazione della traduzione AEM](/help/sites-administering/translation.md), puoi integrarti con molti servizi di traduzione standard per orchestrare la traduzione dell’AEM.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta il documento di authoring [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) per dettagli tecnici completi.
