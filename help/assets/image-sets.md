---
title: Set di immagini
description: Scopri come utilizzare i set di immagini in Dynamic Medie
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Image Sets,Asset Management
role: User, Admin
exl-id: 2a536745-fa13-4158-8761-2ac5b6e1893e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 5%

---

# Set di immagini {#image-sets}

I set di immagini offrono agli utenti un&#39;esperienza di visualizzazione integrata, in cui gli utenti possono visualizzare diverse visualizzazioni di un elemento selezionando una miniatura immagine. I set di immagini consentono di presentare viste alternative di un elemento e il visualizzatore offre strumenti di zoom per esaminare da vicino le immagini.

I set di immagini sono indicati da un banner con la parola `IMAGESET`. Inoltre, se il set di immagini è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![Set di immagini](assets/chlimage_1-339.png)

All&#39;interno del set di immagini, puoi anche creare dei campioni creando un set di immagini e aggiungendo miniature.

Questa applicazione è utile quando si desidera visualizzare un elemento con un colore, un motivo o una finitura diversi. Per creare un set di immagini con campioni di colore, è necessario disporre di un&#39;immagine per ogni colore, motivo o finitura da presentare agli utenti. È inoltre necessario un campione di colore, motivo o finitura per ciascun colore, motivo o finitura.

Si supponga, ad esempio, di voler presentare immagini di maiuscole con distinte di colore diverso, ovvero rosso, verde e blu. In questo caso, sono necessari tre scatti dello stesso tappo. Serve un colpo con un rosso, uno con un verde e uno con un conto blu. È inoltre necessario un campione di colore rosso, verde e blu. I campioni colore fungono da miniature selezionate dagli utenti nel Visualizzatore set di campioni per visualizzare il cappuccio con fattura rossa, verde o blu.

>[!NOTE]
>
>Per informazioni sull&#39;interfaccia utente di Assets, consulta [Gestire le risorse](/help/assets/manage-assets.md).

Quando crei un set di immagini, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| Numero di risorse duplicate per set | Nessun duplicato | 20‡ |
| Numero massimo di immagini per set | 5-10 immagini per set | 1000 |

‡ best practice prevede di non avere risorse duplicate in un set. Il limite è di 20 duplicati per una singola risorsa. Se aggiungi un altro duplicato per quella risorsa, all’interno di quel set, la richiesta restituisce un errore o ignora il duplicato.

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/limitations.md).

## Guida introduttiva: Set di immagini {#quick-start-image-sets}

**Per iniziare subito a utilizzare:**

1. [Carica le immagini di origine primarie per più visualizzazioni](#uploading-assets-in-image-sets).

   Per iniziare, carica le immagini per i set di immagini. Quando scegli le immagini, ricorda che i tuoi clienti possono ingrandire le immagini nel Visualizzatore set di immagini. Assicurati che le immagini siano di almeno 2000 pixel nella dimensione più grande per un dettaglio di zoom ottimale. Dynamic Medie è in grado di eseguire il rendering di immagini fino a 25 MP (megapixel) ciascuna. Ad esempio, è possibile utilizzare un&#39;immagine 5000 x 5000 MP o qualsiasi altra combinazione di dimensioni fino a 25 MP.

   Per un elenco dei formati supportati dai set di immagini, vedere [Dynamic Medie - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media).

<!--    Adobe Experience Manager Assets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

1. [Crea un set di immagini](#creating-image-sets).

   In Set di immagini, gli utenti selezionano le miniature nel Visualizzatore set di immagini.

   Per creare un set di immagini in Assets, vai a **[!UICONTROL Crea]** > **[!UICONTROL Set di immagini]**. Quindi, aggiungi le immagini e seleziona **[!UICONTROL Salva]**.

   È inoltre possibile creare automaticamente i set di immagini tramite [predefiniti set di batch](/help/assets/config-dms7.md).
   >[!IMPORTANT]
   >
   >I set di batch vengono creati dall’IPS (Image Production System) come parte dell’inserimento delle risorse e sono disponibili solo in modalità Dynamic Medie - Scene7.

   Consulta [Preparare le risorse del set di immagini per caricare e caricare i file](#uploading-assets-in-image-sets).

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

1. Aggiungi [predefiniti visualizzatore set di immagini](/help/assets/managing-viewer-presets.md), in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore set di immagini. Per visualizzare il set di immagini con un predefinito visualizzatore, seleziona il set di immagini e fai clic su **[!UICONTROL Visualizzatori]** nel menu a discesa della barra a sinistra.

   Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]** per creare o modificare i predefiniti visualizzatore.

1. (Facoltativo) [Visualizza un set di immagini](/help/assets/image-sets.md#viewing-image-sets) creato utilizzando predefiniti per set di batch.
1. [Anteprima set immagini](/help/assets/previewing-assets.md).

   Seleziona il set di immagini e puoi visualizzarlo in anteprima. Seleziona le icone delle miniature per esaminare il set di immagini nel visualizzatore selezionato. Puoi scegliere visualizzatori diversi dal menu **[!UICONTROL Visualizzatori]**, disponibile dal menu a discesa della barra a sinistra.

1. [Publish un set di immagini](/help/assets/publishing-dynamicmedia-assets.md).

   Quando si pubblica un set di immagini, vengono attivati l’URL e il codice di incorporamento. Inoltre, devi [pubblicare un predefinito visualizzatore personalizzato](/help/assets/managing-viewer-presets.md) creato. I predefiniti visualizzatore predefiniti sono già pubblicati.

1. [Collega URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md) o [Incorpora il visualizzatore di video o immagini](/help/assets/embed-code.md).

   Experience Manager Assets crea chiamate URL per i set di immagini e li attiva dopo la pubblicazione dei set di immagini. Puoi copiare questi URL quando visualizzi in anteprima le risorse. In alternativa, puoi incorporarli sul tuo sito web.

   Seleziona il set di immagini, quindi fai clic su **[!UICONTROL Visualizzatori]** dal menu a discesa della barra a sinistra.

   Consulta [Collegare un set di immagini a una pagina Web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporare il visualizzatore di video o immagini](/help/assets/embed-code.md).

Per modificare i set di immagini, vedere [Modifica set di immagini](#editing-image-sets). Inoltre, puoi visualizzare e modificare [le proprietà del set di immagini](/help/assets/manage-assets.md#editing-properties).

In caso di problemi durante la creazione dei set, vedere Immagini e set in [Risoluzione dei problemi di Dynamic Medie - Modalità Scene7](/help/assets/troubleshoot-dms7.md#images-and-sets).

## Caricare risorse nei set di immagini {#uploading-assets-in-image-sets}

Per iniziare, carica le immagini per i set di immagini. Quando scegli le immagini, ricorda che i tuoi clienti possono ingrandire le immagini nel Visualizzatore set di immagini. Assicurati che le immagini siano almeno 2000 pixel nella dimensione più grande. I set di immagini supportano molti formati di file immagine, ma si consiglia di utilizzare immagini TIFF, PNG e EPS senza perdita di dati.

È possibile caricare immagini per i set di immagini come si fa per [caricare qualsiasi altra risorsa in Assets](/help/assets/manage-assets.md#uploading-assets).

Per un elenco dei formati supportati dai set di immagini, vedere [Dynamic Medie - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media).

### Prepara risorse set immagini per il caricamento {#preparing-image-set-assets-for-upload}

Prima di creare i set di immagini, accertatevi che le immagini siano delle dimensioni e del formato corretti.

Per creare un set di immagini con più viste, è necessario disporre di immagini che mostrino un elemento da diversi punti di vista o che mostrino aspetti diversi dello stesso elemento. L’obiettivo è quello di evidenziare le funzioni importanti di un elemento in modo che gli utenti abbiano un’immagine completa di ciò che sembra o fa.

Poiché gli utenti possono ingrandire le immagini in Set di immagini, accertatevi che siano almeno 2000 pixel nella dimensione più grande. <!-- Assets support many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

>[!NOTE]
>
>Inoltre, se utilizzi le miniature per indicare i campioni di prodotto, devi effettuare le seguenti operazioni:
>
>Sono necessarie vignettature o diverse riprese della stessa immagine che la mostrino in diversi colori, motivi o finiture. Sono inoltre necessari file di miniature corrispondenti ai diversi colori, motivi o finiture. Ad esempio, per presentare le miniature con un set di immagini che mostra la stessa giacca in nero, marrone e verde, è necessario:
>
>* Un colpo nero, marrone e verde della stessa giacca.
>* Miniatura di colore nero, marrone e verde.

## Creare un set di immagini {#creating-image-sets}

Puoi creare set di immagini tramite l’interfaccia utente o l’API. Questa sezione descrive come creare set di immagini nell’interfaccia utente.

>[!NOTE]
>
>È inoltre possibile creare automaticamente i set di immagini tramite [predefiniti set di batch](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>**Importante:** i set di batch vengono creati dall&#39;IPS (Image Production System) come parte dell&#39;inserimento delle risorse e sono disponibili solo in modalità Dynamic Medie - Scene7.

Quando aggiungi risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo che sono state aggiunte.

>[!NOTE]
>
>I set di immagini non sono supportati per le risorse il cui nome file contiene &quot;,&quot; (virgola).

Quando crei un set di immagini, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| Numero di risorse duplicate per set | Nessun duplicato | 20‡ |
| Numero massimo di immagini per set | 5-10 immagini per set | 1000 |

‡ best practice prevede di non avere risorse duplicate in un set. Il limite è di 20 duplicati per una singola risorsa. Se aggiungi un altro duplicato per quella risorsa, all’interno di quel set, la richiesta restituisce un errore o ignora il duplicato.

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/limitations.md).

**Per creare un set di immagini:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale, quindi vai a **[!UICONTROL Navigazione]** > **[!UICONTROL Assets]**. Passa alla posizione in cui desideri creare un set di immagini, quindi vai a **[!UICONTROL Crea]** > **[!UICONTROL Set di immagini]** per aprire la pagina Editor set di immagini.

   Puoi anche creare il set dall’interno di una cartella che contiene le risorse.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Nella pagina Editor set di immagini immettere un nome per il set di immagini nel campo **[!UICONTROL Titolo]**. Il nome viene visualizzato nel banner del set di immagini. È possibile inserire una descrizione.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Effettuare una delle seguenti operazioni:

   * Nell&#39;angolo superiore sinistro della pagina Editor set di immagini, seleziona **[!UICONTROL Aggiungi risorsa]**.

   * Nella parte centrale della pagina Editor set di immagini, seleziona **[!UICONTROL Tocca per aprire il selettore risorse]**.

   Seleziona le risorse da includere nel set di immagini. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Selezionare il filtro e quindi l&#39;icona **[!UICONTROL Filtro]** sulla barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Quando aggiungi risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

   Se necessario, trascina l’icona Riordina di una risorsa a destra del nome del file della risorsa per riordinare le immagini verso l’alto o verso il basso nell’elenco dei set.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Se desideri modificare una miniatura o un campione, seleziona l&#39;icona **+** **miniatura** accanto all&#39;immagine e individua la miniatura o il campione desiderato. Dopo aver selezionato tutte le immagini, seleziona **[!UICONTROL Salva]**.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per eliminare un&#39;immagine, selezionarla e selezionare **[!UICONTROL Elimina risorsa]**.

   * Per applicare un predefinito, seleziona **[!UICONTROL Predefinito]** nell&#39;angolo superiore destro della pagina, quindi seleziona un predefinito da applicare a tutte le risorse contemporaneamente.

   >[!NOTE]
   >
   >Durante la creazione del set di immagini, puoi modificare la miniatura del set o consentire all’Experience Manager di selezionarla automaticamente in base alle risorse del set di immagini. Per selezionare una miniatura, seleziona **[!UICONTROL Cambia miniatura]** sopra il campo Titolo nella pagina Editor set di immagini, quindi seleziona un&#39;immagine qualsiasi. Per trovare le immagini, puoi passare anche ad altre cartelle. Se hai selezionato una miniatura e vuoi che Experience Manager ne generi una dal set di immagini, seleziona **[!UICONTROL Passa a]** > **[!UICONTROL Miniatura automatica]**.

1. Seleziona **[!UICONTROL Salva]**. Il set di immagini appena creato viene visualizzato nella cartella in cui è stato creato.

## Visualizzare un set di immagini {#viewing-image-sets}

Puoi creare set di immagini nell&#39;interfaccia utente o automaticamente utilizzando [predefiniti set di batch](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!IMPORTANT]
>
>I set di batch vengono creati da IPS [Image Production System] come parte dell&#39;inserimento delle risorse e sono disponibili solo in modalità Dynamic Medie - Scene7.)

Tuttavia, i set creati utilizzando predefiniti set di batch, non *not* vengono visualizzati nell&#39;interfaccia utente. È possibile visualizzare questi set in tre modi diversi. Questi metodi sono disponibili anche se avete creato i set di immagini nell&#39;interfaccia utente.

* Apri le proprietà di una singola risorsa. Le proprietà indicano i set a cui fa riferimento la risorsa selezionata o un membro di. Se desiderate visualizzare l&#39;intero set, selezionate il nome del set.

  ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* Da un’immagine inclusa in un qualsiasi set. Seleziona il menu **[!UICONTROL Set]** per visualizzare i set di cui fa parte la risorsa.

  ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Dalla ricerca, puoi selezionare **[!UICONTROL Filtro]**, quindi espandere **[!UICONTROL Dynamic Medie]** e selezionare **[!UICONTROL Set]**.

  La ricerca restituisce i set corrispondenti creati manualmente nell’interfaccia utente o automaticamente tramite i predefiniti per set di batch. Per i set automatizzati, la query di ricerca viene eseguita utilizzando il criterio di ricerca &quot;Inizia con&quot;, che è diverso dalla ricerca Experience Manager, che si basa sull’utilizzo del criterio di ricerca &quot;Contiene&quot;. L&#39;impostazione del filtro su **[!UICONTROL Set]** è l&#39;unico modo per cercare i set automatizzati.

  ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>È possibile visualizzare i set tramite l&#39;interfaccia utente come descritto in [Modifica set di immagini](#editing-image-sets).

## Modificare un set di immagini {#editing-image-sets}

È possibile eseguire varie attività di modifica sui set di immagini, ad esempio:

* Aggiunge immagini al set di immagini.
* Riordinare le immagini nel set di immagini.
* Eliminare le risorse nel set di immagini.
* Applicare i predefiniti visualizzatore.
* Elimina il set di immagini.

**Per modificare un set di immagini:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa set di immagini, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa del set di immagini, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.
   * Fai clic su una risorsa del set di immagini, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) nella barra degli strumenti.

1. Per modificare le immagini nel set di immagini, effettuate una delle seguenti operazioni:

   * Per riordinare le risorse, trascina un’immagine in una nuova posizione (seleziona l’icona Riordina per spostare gli elementi).
   * Per ordinare gli elementi in ordine crescente o decrescente, selezionare l&#39;intestazione di colonna.
   * Per aggiungere una risorsa o aggiornare una risorsa esistente, seleziona **[!UICONTROL Aggiungi risorsa]**. Passa a una risorsa, selezionala, quindi seleziona **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro della pagina.
     >[!NOTE]
     >
     >Se elimini l’immagine utilizzata da Experience Manager per la miniatura sostituendola con un’altra immagine, la risorsa originale viene comunque visualizzata.
   * Per eliminare una risorsa, selezionala e seleziona **[!UICONTROL Elimina risorsa]**.
   * Per applicare un predefinito, seleziona **[!UICONTROL Predefinito]** nell&#39;angolo superiore destro della pagina, quindi seleziona un predefinito visualizzatore.
   * Per aggiungere o modificare una miniatura, seleziona l’icona della miniatura accanto a destra della risorsa. Passa alla nuova miniatura o risorsa campione, selezionala, quindi seleziona **[!UICONTROL Seleziona]**.
   * Per eliminare un intero set di immagini, passare al set, selezionarlo e selezionare **[!UICONTROL Elimina]**.

   >[!NOTE]
   >
   >Per modificare le immagini di un set di immagini, passa al set e seleziona **[!UICONTROL Membri set]** nella barra a sinistra, quindi seleziona l&#39;icona a forma di matita su una singola risorsa per aprire la finestra di modifica.

1. Seleziona **[!UICONTROL Salva]** al termine della modifica.

## Anteprima di un set di immagini {#previewing-image-sets}

Vedi [Anteprima risorse](/help/assets/previewing-assets.md).

## Publish e set di immagini {#publishing-image-sets}

Consulta [Pubblicazione di Assets](/help/assets/publishing-dynamicmedia-assets.md).
