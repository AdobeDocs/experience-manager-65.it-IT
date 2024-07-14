---
title: Produttore catalogo
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: Produttore catalogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 1%

---

# Produttore catalogo{#catalog-producer}

Scopri come utilizzare Catalog Producer in AEM Assets per generare cataloghi di prodotti utilizzando le risorse digitali.

Con Adobe Experience Manager (AEM) Assets Catalog Producer, puoi creare cataloghi per i prodotti del tuo marchio utilizzando modelli InDesign importati da un’applicazione InDesign. Per importare modelli InDesign, devi prima integrare AEM Assets con un server InDesign.

## Integrazione con il server InDesign {#integrating-with-indesign-server}

Come parte del processo di integrazione, configura il flusso di lavoro **Risorsa di aggiornamento DAM**, ideale per l&#39;integrazione con InDesign. Inoltre, configura un processo di lavoro proxy per il server InDesign. Per ulteriori dettagli, vedere [Integrazione di AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Puoi generare modelli InDesign da file InDesign prima di importarli in AEM Assets. Per ulteriori dettagli, vedere [Utilizzo di file e modelli](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Puoi mappare gli elementi nei modelli InDesign ai tag XML. I tag mappati vengono visualizzati come proprietà quando mappate le proprietà del prodotto con le proprietà del modello in Catalog Producer. Per informazioni sui tag XML nei file InDesign, vedere [Contenuto tag per XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo i file InDesign (.indd) vengono utilizzati come modelli. I file con estensione .indt non sono supportati.

## Creazione di un catalogo {#creating-a-catalog}

Catalog Producer utilizza i dati PIM (Product Information Management) per mappare le proprietà del prodotto con le proprietà XML visualizzate nel modello. Per creare un catalogo, effettua le seguenti operazioni:

1. Nell&#39;interfaccia utente di Assets, fare clic sul logo **AEM** e passare a **Assets > Cataloghi**.
1. Nella pagina **Cataloghi**, fai clic su **Crea** nella barra degli strumenti, quindi seleziona **Catalogo** dall&#39;elenco.
1. Nella pagina **Crea catalogo**, immetti un nome e una descrizione (facoltativa) per il catalogo e specifica eventuali tag. Puoi anche aggiungere una miniatura per il catalogo.

   ![crea_catalogo](assets/create_catalog.png)

1. Fai clic su **Salva**. Una finestra di dialogo di conferma notifica che il catalogo è stato creato. Fai clic su **Fine** per chiudere la finestra di dialogo.
1. Per aprire il catalogo creato, selezionarlo dalla pagina **Cataloghi**.

   >[!NOTE]
   >
   >Per aprire il catalogo, puoi anche fare clic su **Apri** nella finestra di dialogo di conferma indicata nel passaggio precedente.

1. Per aggiungere pagine al catalogo, fare clic su **Crea** nella barra degli strumenti, quindi scegliere l&#39;opzione **Nuova pagina**.
1. Dalla procedura guidata, seleziona un modello InDesign per la pagina. Quindi fare clic su **Avanti**.
1. Specifica un nome per la pagina e una descrizione facoltativa. Specifica gli eventuali tag.
1. Fai clic su **Crea** nella barra degli strumenti. Quindi fai clic su **Apri** nella finestra di dialogo. Le proprietà del prodotto vengono visualizzate nel riquadro a sinistra. Le proprietà predefinite del modello InDesign vengono visualizzate nel riquadro di destra.
1. Dal riquadro di sinistra, trascina le proprietà del prodotto nelle proprietà del modello InDesign e crea un mapping tra di esse.

   Per visualizzare la visualizzazione della pagina in tempo reale, fare clic sulla scheda **Anteprima** nel riquadro di destra.

1. Per creare altre pagine, ripetere i passaggi 6-9. Per creare pagine simili per altri prodotti, selezionare la pagina e fare clic sull&#39;icona **Crea pagine simili** nella barra degli strumenti.

   ![crea_pagine_simili](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Puoi creare pagine simili solo per prodotti con struttura simile.

   Fai clic sull&#39;icona Aggiungi, seleziona i prodotti dal selettore prodotti, quindi fai clic su **Seleziona** nella barra degli strumenti.

   ![select_product](assets/select_product.png)

1. Dalla barra degli strumenti, fare clic su **Crea**. Fai clic su **Fine** per chiudere la finestra di dialogo. Pagine simili sono incluse nel catalogo.
1. Per aggiungere un file InDesign esistente al catalogo, fai clic su **Crea** nella barra degli strumenti e scegli l&#39;opzione **Aggiungi a pagina esistente**.
1. Selezionare il file InDesign e fare clic su **Aggiungi** nella barra degli strumenti. Quindi fare clic su **OK** per chiudere la finestra di dialogo.

   Se i metadati dei prodotti a cui si fa riferimento nelle pagine del catalogo vengono modificati, le modifiche non vengono applicate automaticamente alle pagine del catalogo. Un banner con etichetta **Non aggiornato** viene visualizzato nelle immagini del prodotto nelle pagine del catalogo di riferimento, a indicare che i metadati per i prodotti di riferimento non sono aggiornati.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Per fare in modo che le immagini del prodotto riflettano le ultime modifiche apportate ai metadati, seleziona la pagina nella console Catalogo e fai clic sull&#39;icona **Aggiorna pagina** nella barra degli strumenti.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Per modificare i metadati per un prodotto a cui si fa riferimento, accedi alla console Prodotti (**Logo AEM** > **Commerce** > **Prodotti**) e seleziona il prodotto. Quindi, fai clic sull&#39;icona **Visualizza proprietà** nella barra degli strumenti e modifica i metadati nella pagina Proprietà della risorsa.

1. Per ridisporre le pagine nel catalogo, fai clic sull&#39;icona **Crea** nella barra degli strumenti, quindi scegli **Unisci** dal menu. Nella procedura guidata, il carosello nella parte superiore consente di riordinare le pagine trascinandole. È inoltre possibile rimuovere le pagine.

1. Fai clic su **Avanti**. Per aggiungere un file InDesign esistente come frontespizio, fare clic su **Sfoglia** accanto alla casella **Scegli frontespizio** e specificare il percorso per il modello di frontespizio.
1. Fai clic su **Salva**, quindi su **Fine** per chiudere la finestra di dialogo di conferma.
Quando si seleziona l&#39;opzione **Fine**, viene visualizzata una finestra di dialogo che consente di scegliere se si desidera una copia trasformata PDF.
   ![esporta in pdf](assets/CatalogPDF.png)
Se è selezionata l&#39;opzione Acrobat(PDF), viene creata una copia trasformata pdf in **/jcr:content/renditions** oltre alla copia trasformata indesign. Puoi scaricare tutte le rappresentazioni selezionando la casella di controllo &quot;Rappresentazioni&quot; nella finestra di dialogo di download.

1. Per generare un&#39;anteprima per il catalogo creato, selezionarla nella console **Cataloghi**, quindi fare clic sull&#39;icona **Anteprima** nella barra degli strumenti.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Rivedi le pagine del catalogo nell’anteprima. Fai clic su **Chiudi** per chiudere l&#39;anteprima.
