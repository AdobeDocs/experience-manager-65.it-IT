---
title: Produttore catalogo
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: Produttore catalogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Produttore catalogo{#catalog-producer}

Scopri come utilizzare Catalog Producer in AEM Assets per generare cataloghi di prodotti utilizzando le risorse digitali.

Con Adobe Experience Manager (AEM) Assets Catalog Producer, puoi creare cataloghi per i prodotti del tuo marchio utilizzando modelli InDesign importati da un’applicazione InDesign. Per importare modelli InDesign, devi prima integrare AEM Assets con un server InDesign.

## Integrazione con il server InDesign {#integrating-with-indesign-server}

Come parte del processo di integrazione, configura il **Aggiorna risorsa DAM** flusso di lavoro, adatto per l’integrazione con InDesign. Inoltre, configura un processo di lavoro proxy per il server InDesign. Per ulteriori informazioni, consulta [Integrazione di AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Puoi generare modelli InDesign da file InDesign prima di importarli in AEM Assets. Per ulteriori informazioni, consulta [Utilizzo di file e modelli](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Puoi mappare gli elementi nei modelli InDesign ai tag XML. I tag mappati vengono visualizzati come proprietà quando mappate le proprietà del prodotto con le proprietà del modello in Catalog Producer. Per informazioni sull&#39;assegnazione tag XML nei file InDesign, vedere [Assegnazione di tag al contenuto per XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo i file InDesign (.indd) vengono utilizzati come modelli. I file con estensione .indt non sono supportati.

## Creazione di un catalogo {#creating-a-catalog}

Catalog Producer utilizza i dati PIM (Product Information Management) per mappare le proprietà del prodotto con le proprietà XML visualizzate nel modello. Per creare un catalogo, effettua le seguenti operazioni:

1. Nell’interfaccia utente di Assets, fai clic su **Logo AEM**, e vai a **Risorse > Cataloghi**.
1. In **Cataloghi** pagina, fai clic su **Crea** dalla barra degli strumenti, quindi seleziona **Catalogo** dall&#39;elenco.
1. In **Crea catalogo** , immettere un nome e una descrizione (facoltativa) per il catalogo e specificare eventuali tag. Puoi anche aggiungere una miniatura per il catalogo.

   ![create_catalog](assets/create_catalog.png)

1. Clic **Salva**. Una finestra di dialogo di conferma notifica che il catalogo è stato creato. Clic **Fine** per chiudere la finestra di dialogo
1. Per aprire il catalogo creato, fare clic su di esso dal **Cataloghi** pagina.

   >[!NOTE]
   >
   >Per aprire il catalogo, puoi anche fare clic su **Apri** nella finestra di dialogo di conferma di cui al passaggio precedente.

1. Per aggiungere pagine al catalogo, fai clic su **Crea** dalla barra degli strumenti, quindi scegliere **Nuova pagina** opzione.
1. Dalla procedura guidata, seleziona un modello InDesign per la pagina. Quindi, fai clic su **Successivo**.
1. Specifica un nome per la pagina e una descrizione facoltativa. Specifica gli eventuali tag.
1. Fai clic su **Crea** dalla barra degli strumenti. Quindi, fai clic su **Apri** dalla finestra di dialogo. Le proprietà del prodotto vengono visualizzate nel riquadro a sinistra. Le proprietà predefinite del modello InDesign vengono visualizzate nel riquadro di destra.
1. Dal riquadro di sinistra, trascina le proprietà del prodotto nelle proprietà del modello InDesign e crea un mapping tra di esse.

   Per visualizzare l&#39;aspetto della pagina in tempo reale, fare clic sul pulsante **Anteprima** nel riquadro di destra.

1. Per creare altre pagine, ripetere i passaggi 6-9. Per creare pagine simili per altri prodotti, seleziona la pagina e fai clic su **Crea pagine simili** dalla barra degli strumenti.

   ![create_like_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Puoi creare pagine simili solo per prodotti con struttura simile.

   Fai clic sull’icona Aggiungi, seleziona i prodotti dal selettore prodotti, quindi fai clic su **Seleziona** dalla barra degli strumenti.

   ![select_product](assets/select_product.png)

1. Dalla barra degli strumenti, fai clic su **Crea**. Clic **Fine** per chiudere la finestra di dialogo Pagine simili sono incluse nel catalogo.
1. Per aggiungere al catalogo un file InDesign esistente, fai clic su **Crea** dalla barra degli strumenti e scegli **Aggiungi a pagina esistente** opzione.
1. Seleziona il file InDesign e fai clic su **Aggiungi** dalla barra degli strumenti. Quindi, fai clic su **OK** per chiudere la finestra di dialogo

   Se i metadati dei prodotti a cui si fa riferimento nelle pagine del catalogo vengono modificati, le modifiche non vengono applicate automaticamente alle pagine del catalogo. Banner etichettato **Non aggiornato** viene visualizzato nelle immagini del prodotto nelle pagine del catalogo di riferimento, a indicare che i metadati per i prodotti di riferimento non sono aggiornati.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Per fare in modo che le immagini del prodotto riflettano le ultime modifiche apportate ai metadati, seleziona la pagina nella console Catalogo e fai clic su **Aggiorna pagina** dalla barra degli strumenti.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Per modificare i metadati di un prodotto a cui si fa riferimento, accedi alla console Prodotti (**Logo AEM** > **Commerce** > **Prodotti**) e selezionare il prodotto. Quindi, fai clic su **Visualizza proprietà** nella barra degli strumenti e modificare i metadati nella pagina Proprietà della risorsa.

1. Per ridisporre le pagine nel catalogo, fare clic su **Crea** dalla barra degli strumenti, quindi scegliere **Unisci** dal menu. Nella procedura guidata, il carosello nella parte superiore consente di riordinare le pagine trascinandole. È inoltre possibile rimuovere le pagine.

1. Fai clic su **Avanti**. Per aggiungere un file InDesign esistente come pagina di copertina, fai clic su **Sfoglia** accanto al **Scegli copertina** e specificare il percorso per il modello del frontespizio.
1. Clic **Salva** e quindi fare clic su **Fine** per chiudere la finestra di conferma.
Quando si seleziona **Fine** , viene visualizzata una finestra di dialogo che consente di scegliere se si desidera una copia trasformata pdf.
   ![esporta in pdf](assets/CatalogPDF.png)
Se è selezionata l’opzione Acrobat(PDF), viene creata una rappresentazione pdf in  **/jcr:content/renditions** oltre alla rappresentazione di indesign. Puoi scaricare tutte le rappresentazioni selezionando la casella di controllo &quot;Rappresentazioni&quot; nella finestra di dialogo di download.

1. Per generare un&#39;anteprima per il catalogo creato, selezionatela nel **Cataloghi** e quindi fare clic sul pulsante **Anteprima** dalla barra degli strumenti.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Rivedi le pagine del catalogo nell’anteprima. Clic **Chiudi** per chiudere l&#39;anteprima.
