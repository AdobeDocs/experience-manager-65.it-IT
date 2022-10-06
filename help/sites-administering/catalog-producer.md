---
title: Produttore catalogo
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Produttore catalogo
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Produttore catalogo{#catalog-producer}

Scopri come utilizzare Catalog Producer in AEM Assets per generare cataloghi di prodotti utilizzando le risorse digitali.

Con Adobe Experience Manager (AEM) Assets Catalog Producer, puoi creare cataloghi per i tuoi prodotti di marca utilizzando i modelli di InDesign importati da un’applicazione InDesign. Per importare i modelli di InDesign, è necessario prima integrare AEM Assets con un server InDesign.

## Integrazione con il server InDesign {#integrating-with-indesign-server}

Come parte del processo di integrazione, configura il **Risorsa di aggiornamento DAM** , ideale per l’integrazione con InDesign. Inoltre, configura un processo di lavoro proxy per il server InDesign. Per maggiori dettagli, vedi [Integrazione di AEM Assets con InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>È possibile generare modelli di InDesign dai file InDesign prima di importarli in AEM Assets. Per maggiori dettagli, vedi [Utilizzo di file e modelli](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>È possibile mappare gli elementi nei modelli di InDesign a tag XML. I tag mappati vengono visualizzati come proprietà quando mappi le proprietà del prodotto con le proprietà del modello in Catalog Producer. Per informazioni sull’assegnazione tag XML nei file InDesign, consulta [Assegnazione di tag al contenuto per XML](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Solo i file InDesign (.indd) vengono utilizzati come modelli. I file con estensione .indt non sono supportati.

## Creazione di un catalogo {#creating-a-catalog}

Catalog Producer utilizza i dati di gestione delle informazioni di prodotto (PIM) per mappare le proprietà del prodotto con le proprietà XML visualizzate nel modello. Per creare un catalogo, effettua le seguenti operazioni:

1. Dall’interfaccia utente Assets, tocca o fai clic sul pulsante **Logo AEM** e vai a **Risorse > Cataloghi**.
1. In **Cataloghi** pagina, tocca/fai clic **Crea** dalla barra degli strumenti, quindi seleziona **Catalogo** dall&#39;elenco.
1. In **Crea catalogo** , immetti un nome e una descrizione (facoltativi) per il catalogo e specifica eventuali tag. Puoi anche aggiungere un’immagine in miniatura per il catalogo.

   ![create_catalog](assets/create_catalog.png)

1. Tocca o fai clic su **Salva**. Una finestra di dialogo di conferma notifica la creazione del catalogo. Tocca o fai clic su **Fine** per chiudere la finestra di dialogo.
1. Per aprire il catalogo creato, toccalo o fai clic su di esso nel **Cataloghi** pagina.

   >[!NOTE]
   >
   >Per aprire il catalogo, puoi anche toccare o fare clic su **Apri** nella finestra di dialogo di conferma indicata nel passaggio precedente.

1. Per aggiungere pagine al catalogo, tocca o fai clic su **Crea** dalla barra degli strumenti, quindi scegli la **Nuova pagina** opzione .
1. Dalla procedura guidata, seleziona un modello di InDesign per la pagina. Quindi, tocca o fai clic su **Successivo**.
1. Specifica un nome per la pagina e una descrizione facoltativa. Specifica eventuali tag.
1. Tocca o fai clic sul pulsante **Crea** dalla barra degli strumenti. Quindi, tocca o fai clic su **Apri** dalla finestra di dialogo. Le proprietà del prodotto vengono visualizzate nel riquadro a sinistra. Le proprietà predefinite per il modello di InDesign vengono visualizzate nel riquadro di destra.
1. Dal riquadro a sinistra, trascina le proprietà del prodotto nelle proprietà del modello di InDesign e crea una mappatura tra di esse.

   Per visualizzare l’aspetto della pagina in tempo reale, tocca o fai clic sul pulsante **Anteprima** nel riquadro a destra.

1. Per creare più pagine, ripeti i passaggi 6-9. Per creare pagine simili per altri prodotti, seleziona la pagina e tocca o fai clic sul pulsante **Creare pagine simili** dalla barra degli strumenti.

   ![create_alike_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >È possibile creare solo pagine simili per prodotti con struttura simile.

   Tocca o fai clic sull’icona Aggiungi , seleziona prodotti dal selettore prodotti, quindi tocca o fai clic su **Seleziona** dalla barra degli strumenti.

   ![select_product](assets/select_product.png)

1. Dalla barra degli strumenti, tocca o fai clic su **Crea**. Tocca o fai clic su **Fine** per chiudere la finestra di dialogo. Pagine simili sono incluse nel catalogo.
1. Per aggiungere un file InDesign esistente al catalogo, tocca o fai clic su **Crea** dalla barra degli strumenti e scegli la **Aggiungi alla pagina esistente** opzione .
1. Seleziona il file InDesign e tocca o fai clic su **Aggiungi** dalla barra degli strumenti. Quindi, tocca o fai clic su **OK** per chiudere la finestra di dialogo.

   Se i metadati dei prodotti a cui si fa riferimento nelle pagine del catalogo vengono modificati, le modifiche non verranno applicate automaticamente nelle pagine del catalogo. Banner etichettato **Stabile** appare sulle immagini del prodotto nelle pagine del catalogo di riferimento, indicando che i metadati per i prodotti di riferimento non sono aggiornati.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Per fare in modo che le immagini del prodotto riflettano le ultime modifiche ai metadati, seleziona la pagina nella console Catalogo e tocca o fai clic sul pulsante **Aggiorna pagina** dalla barra degli strumenti.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Per modificare i metadati di un prodotto di riferimento, passa alla console Prodotti (**Logo AEM** > **Commerce** > **Prodotti**) e seleziona il prodotto. Quindi, tocca o fai clic sul pulsante **Visualizza proprietà** dalla barra degli strumenti e modifica i metadati nella pagina Proprietà della risorsa.

1. Per ridisporre le pagine del catalogo, tocca o fai clic sul pulsante **Crea** dalla barra degli strumenti, quindi scegli **Unisci** dal menu. Nella procedura guidata, il carosello nella parte superiore consente di riordinare le pagine trascinandole. È inoltre possibile rimuovere le pagine.

1. Tocca o fai clic su **Successivo**. Per aggiungere un file InDesign esistente come pagina di copertina, tocca o fai clic su **Sfoglia** accanto al **Scegli pagina copertina** e specificare il percorso per il modello della pagina di copertina.
1. Tocca o fai clic su **Salva**, quindi tocca o fai clic su **Fine** per chiudere la finestra di dialogo di conferma.
Alla selezione della **Fine** viene visualizzata una finestra di dialogo per selezionare se si desidera eseguire il rendering .pdf.
   ![esporta in pdf](assets/CatalogPDF.png)
Se è selezionata l’opzione Acrobat(PDF), viene creato un rendering pdf in  **/jcr:content/renditions** oltre al rendering indesign. Puoi scaricare tutte le rappresentazioni selezionando la casella di controllo &quot;Rendering&quot; nella finestra di dialogo di download.

1. Per generare un’anteprima per il catalogo creato, selezionalo nella **Cataloghi** , quindi fai clic su **Anteprima** dalla barra degli strumenti.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Esamina le pagine del catalogo nell’anteprima. Tocca o fai clic su **Chiudi** per chiudere l&#39;anteprima.
