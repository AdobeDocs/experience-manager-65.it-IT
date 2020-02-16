---
title: Catalog Producer
seo-title: Catalog Producer
seo-description: Scopri come utilizzare Catalog Producer in Risorse AEM per generare cataloghi di prodotti utilizzando le risorse digitali.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Catalog Producer{#catalog-producer}

Scopri come utilizzare Catalog Producer in Risorse AEM per generare cataloghi di prodotti utilizzando le risorse digitali.

Con Adobe Experience Manager (AEM) Assets Catalog Producer, potete creare cataloghi per i prodotti di marca utilizzando i modelli InDesign importati da un’applicazione InDesign. Per importare i modelli di InDesign, integrate prima AEM Assets con un server InDesign.

## Integrating with InDesign server {#integrating-with-indesign-server}

Come parte del processo di integrazione, configurate il flusso di lavoro **DAM Update Asset** , adatto per l&#39;integrazione con InDesign. Inoltre, configurate un lavoratore proxy per il server InDesign. Per informazioni dettagliate, consultate [Integrazione di AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Potete generare modelli InDesign da file InDesign prima di importarli in Risorse AEM. Per informazioni dettagliate, consultate [Utilizzo di file e modelli](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>Potete mappare gli elementi dei modelli InDesign a tag XML. I tag mappati vengono visualizzati come proprietà quando mappate le proprietà del prodotto con le proprietà del modello in Catalog Producer. Per informazioni sui tag XML nei file InDesign, consultate [Assegnazione di tag ai contenuti XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo i file InDesign (.indd) sono utilizzati come modelli. I file con estensione .indt non sono supportati.

## Creazione di un catalogo {#creating-a-catalog}

Catalog Producer utilizza i dati PIM (Product Information Management) per mappare le proprietà del prodotto con le proprietà XML visualizzate nel modello. Per creare un catalogo, effettuate le seguenti operazioni:

1. Dall’interfaccia utente Risorse, toccate/fate clic sul logo **** AEM, quindi passate a **Risorse > Cataloghi**.
1. Nella pagina **Cataloghi** , toccate o fate clic su **Crea** dalla barra degli strumenti, quindi selezionate **Catalogo** dall’elenco.
1. Nella pagina **Crea catalogo** , inserite un nome e una descrizione (facoltativi) per il catalogo e specificate eventuali tag. Potete anche aggiungere una miniatura al catalogo.

   ![create_catalog](assets/create_catalog.png)

1. Tap/click **Save**. Una finestra di dialogo di conferma notifica che il catalogo viene creato. Toccate o fate clic su **Fine** per chiudere la finestra di dialogo.
1. Per aprire il catalogo che avete creato, toccate o fate clic su di esso nella pagina **Cataloghi** .

   >[!NOTE]
   >
   >Per aprire il catalogo, potete anche toccare o fare clic su **Apri** nella finestra di dialogo di conferma indicata nel passaggio precedente.

1. Per aggiungere delle pagine al catalogo, toccate o fate clic su **Crea** dalla barra degli strumenti, quindi scegliete l’opzione **Nuova pagina** .
1. Dalla procedura guidata, selezionate un modello InDesign per la pagina. Quindi toccate o fate clic su **Avanti**.
1. Specificate un nome per la pagina e una descrizione facoltativa. Specificate eventuali tag.
1. Tap/click the **Create** from the toolbar. Quindi toccate o fate clic su **Apri** nella finestra di dialogo. Le proprietà del prodotto vengono visualizzate nel riquadro a sinistra. Le proprietà predefinite per il modello InDesign vengono visualizzate nel riquadro di destra.
1. Dal riquadro a sinistra, trascinate le proprietà del prodotto nelle proprietà del modello InDesign e create una mappatura tra di esse.

   Per visualizzare l’aspetto della pagina in tempo reale, toccate o fate clic sulla scheda **Anteprima** nel riquadro a destra.

1. Per creare altre pagine, ripetete i passaggi da 6 a 9. Per creare pagine simili per altri prodotti, selezionate la pagina e toccate o fate clic sull’icona **Crea pagine** simili dalla barra degli strumenti.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Potete creare solo pagine simili per prodotti con struttura simile.

   Toccate/fate clic sull&#39;icona Aggiungi, selezionate i prodotti dal selettore prodotti, quindi toccate/fate clic su **Seleziona** nella barra degli strumenti.

   ![select_product](assets/select_product.png)

1. Dalla barra degli strumenti, fate clic o toccate **Crea**. Toccate o fate clic su **Fine** per chiudere la finestra di dialogo. Pagine simili sono incluse nel catalogo.
1. Per aggiungere un file InDesign esistente al catalogo, toccate o fate clic su **Crea** dalla barra degli strumenti e scegliete l’opzione **Aggiungi alla pagina** esistente.
1. Selezionate il file InDesign, quindi toccate o fate clic su **Aggiungi** dalla barra degli strumenti. Quindi toccate o fate clic su **OK** per chiudere la finestra di dialogo.

   Se i metadati dei prodotti a cui si fa riferimento nelle pagine del catalogo vengono modificati, le modifiche non vengono applicate automaticamente alle pagine del catalogo. Sulle immagini del prodotto presenti nelle pagine del catalogo di riferimento viene visualizzato un banner con etichetta **Stale** , a indicare che i metadati per i prodotti di riferimento non sono aggiornati.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Per fare in modo che le immagini del prodotto riflettano le ultime modifiche ai metadati, selezionate la pagina nella console Catalogo e toccate o fate clic sull’icona **Aggiorna pagina** dalla barra degli strumenti.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Per modificare i metadati di un prodotto di riferimento, andate alla console Prodotti (Logo **** AEM > **Commerce** > **Products**) e selezionate il prodotto. Quindi, toccate o fate clic sull’icona **Visualizza proprietà** dalla barra degli strumenti e modificate i metadati nella pagina Proprietà della risorsa.

1. Per ridisporre le pagine nel catalogo, toccate o fate clic sull’icona **Crea** nella barra degli strumenti, quindi scegliete **Unisci** dal menu. Nella procedura guidata, il carosello nella parte superiore consente di riordinare le pagine trascinandole. È inoltre possibile rimuovere delle pagine.

1. Tap/click **Next**. Per aggiungere un file InDesign esistente come copertina, toccate o fate clic su **Sfoglia** accanto alla casella **Scegli pagina** copertina e specificate il percorso per il modello di copertina.
1. Toccate o fate clic su **Salva**, quindi toccate o fate clic su **Fine** per chiudere la finestra di dialogo di conferma.
Selezionando l&#39;opzione **Fine** , si apre una finestra di dialogo per selezionare se si desidera una rappresentazione .pdf.
   ![esportazione in PDF](assets/CatalogPDF.png)Se è selezionata l’opzione Acrobat(PDF), viene creata una rappresentazione PDF in **/jcr:content/renditions** , oltre alla rappresentazione per indesign. Potete scaricare tutte le rappresentazioni selezionando la casella di controllo &quot;Rappresentazioni&quot; nella finestra di dialogo di download.

1. Per generare un’anteprima per il catalogo creato, selezionatelo nella console **Cataloghi** , quindi fate clic sull’icona **Anteprima** nella barra degli strumenti.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Rivedete le pagine del catalogo nell’anteprima. Toccate o fate clic su **Chiudi** per chiudere l’anteprima.

