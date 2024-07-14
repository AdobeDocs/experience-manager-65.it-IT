---
title: Set 360 gradi
description: Scopri come creare un set 360 gradi in Dynamic Medie per simulare l’atto reale di trasformare un oggetto per visualizzarlo da qualsiasi angolazione in modo da poter vedere i dettagli.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 8%

---

# Set 360 gradi{#spin-sets}

Un set 360 gradi simula l&#39;atto reale di girare un oggetto per esaminarlo. I set 360 gradi consentono di visualizzare gli elementi da qualsiasi angolazione, ottenendo i dettagli visivi chiave da qualsiasi angolazione.

Un set 360 gradi simula un’esperienza di visione a 360 gradi. Dynamic Medie offre set 360 gradi a asse singolo in cui gli utenti possono ruotare un elemento. Inoltre, gli utenti possono eseguire lo zoom e la panoramica delle visualizzazioni con pochi semplici clic del mouse. In questo modo, gli utenti possono esaminare un elemento più da vicino da un punto di vista particolare.

I set 360 gradi sono indicati da un banner con la parola **[!UICONTROL SPINSET]**. Inoltre, se il set 360 gradi è pubblicato, la data di pubblicazione, indicata dall&#39;icona **[!UICONTROL Mondo]**, è riportata sul banner insieme all&#39;ultima data di modifica, contrassegnata dall&#39;icona **[!UICONTROL Matita]**.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Per informazioni sull&#39;interfaccia utente di Assets, consulta [Gestire le risorse](/help/assets/manage-assets.md).

Quando crei un set 360 gradi, Adobe consiglia le best practice seguenti e applica i limiti seguenti:

| Tipo di limite | Best practice | Limite imposto |
| --- | --- | --- |
| Numero massimo di righe/colonne per set 2D | 12-18 immagini per set | 1000 |

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/limitations.md).

## Guida introduttiva: Set 360 gradi {#quick-start-spin-sets}

Per iniziare a usare rapidamente i set 360 gradi, effettua le seguenti operazioni:

1. [Carica le immagini per più visualizzazioni](#uploading-assets-for-spin-sets).

   Sono necessari almeno 8-12 scatti di un elemento per un set 360 gradi monodimensionale e 16-24 per un set 360 gradi bidimensionale. Gli scatti devono essere effettuati a intervalli regolari per dare l&#39;impressione che l&#39;elemento stia ruotando e sia capovolto. Ad esempio, se un set 360/12) include 12 scatti, ruotate l&#39;elemento di 30° per ogni scatto.

   Per un elenco dei formati supportati dai set 360 gradi, vedere [Dynamic Medie - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media).

1. [Crea un set 360 gradi](#creating-spin-sets).

   Per creare un set 360 gradi, seleziona **[!UICONTROL Crea > Set 360 gradi]**, quindi assegna un nome al set, scegli le risorse e stabilisci l&#39;ordine di visualizzazione delle immagini.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >Puoi anche creare in automatico i set 360 gradi da [predefiniti set di batch](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:** i set di batch vengono creati dall&#39;IPS (Image Production System) come parte dell&#39;inserimento delle risorse e sono disponibili solo in modalità Dynamic Medie - Scene7.

1. Imposta [predefiniti visualizzatore set 360 gradi](/help/assets/managing-viewer-presets.md), in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set 360 gradi. Per visualizzare il set 360 con un predefinito visualizzatore, seleziona il set 360 gradi e fai clic su **Visualizzatori** nel menu a discesa della barra a sinistra.

   Se desideri creare o modificare i predefiniti visualizzatore, consulta **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.

   Consulta [Aggiungere e modificare i predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

1. [Visualizza un set 360 gradi](#viewing-spin-sets).

   È possibile visualizzare e accedere ai set creati mediante i predefiniti set di batch in tre modi diversi. (I set creati utilizzando predefiniti set di batch, non *not* vengono visualizzati nell&#39;interfaccia utente.)

1. [Anteprima set 360 gradi](/help/assets/previewing-assets.md).

   Selezionate il set 360 gradi e potete visualizzarne l&#39;anteprima. Ruota il set 360 gradi. Puoi scegliere visualizzatori diversi dal menu **[!UICONTROL Visualizzatori]**, disponibile dal menu a discesa della barra a sinistra.

1. [Publish un set 360 gradi](/help/assets/publishing-dynamicmedia-assets.md).

   La pubblicazione di un set 360 gradi attiva l’URL e la stringa di incorporamento. Inoltre, devi [pubblicare il predefinito visualizzatore](/help/assets/managing-viewer-presets.md).

1. [Collega URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md) o [Incorpora il visualizzatore di video o immagini](/help/assets/embed-code.md).

   Adobe Experience Manager Assets crea chiamate URL per i set 360 gradi e li attiva dopo la pubblicazione dei set 360 gradi. Puoi copiare questi URL quando visualizzi in anteprima le risorse. In alternativa, puoi incorporarli nel sito web.

   Seleziona il set a 360 gradi, quindi fai clic su **[!UICONTROL Visualizzatori]** nel menu a discesa della barra a sinistra.

   Consulta [Collegare un set 360 gradi a una pagina Web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporare il visualizzatore di video o immagini](/help/assets/embed-code.md).

Se necessario, puoi [modificare un set 360 gradi](#editing-spin-sets). Inoltre, puoi visualizzare e modificare [le proprietà del set 360 gradi](/help/assets/manage-assets.md#editing-properties).

## Caricare risorse per un set 360 gradi {#uploading-assets-for-spin-sets}

Sono necessari almeno 8-12 scatti di un elemento per un set 360 gradi monodimensionale e 16-24 per un set 360 gradi bidimensionale. Gli scatti devono essere effettuati a intervalli regolari per dare l&#39;impressione che l&#39;elemento stia ruotando e sia capovolto. Ad esempio, se un set 360/12) include 12 scatti, ruotate l&#39;elemento di 30° per ogni scatto.

È possibile caricare immagini per i set 360 gradi come si fa per [caricare qualsiasi altra risorsa in Experience Manager Assets](/help/assets/manage-assets.md).

Per un elenco dei formati supportati dai set 360 gradi, vedere [Dynamic Medie - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media).

### Linee guida per l’acquisizione di immagini per il set 360 gradi {#guidelines-for-shooting-spin-set-images}

Di seguito sono riportate alcune best practice relative alle immagini dei set 360 gradi. In generale, più immagini si hanno in un set 360 gradi, migliore è l&#39;effetto di rotazione dell&#39;immagine. Tuttavia, l’inclusione di molte immagini nel set aumenta anche il tempo necessario per caricare le immagini. L’Experience Manager consiglia di seguire queste linee guida per la ripresa di immagini da utilizzare nei set 360 gradi:

* Utilizzare almeno 8-12 immagini in un set 360 gradi monodimensionale e 16-24 immagini in un set 360 gradi bidimensionale. Per girare a 360 gradi sono necessarie almeno 8 immagini. I set 360 gradi unidimensionali sono più comuni in quanto la creazione di set 360 gradi bidimensionali richiede molto lavoro.
* Utilizza un formato senza perdita di dati; si consiglia di usare TIFF e PNG.
* Mascherare tutte le immagini in modo che l&#39;elemento appaia su uno sfondo bianco puro o su un altro sfondo ad alto contrasto. Se necessario, aggiungete delle ombre.
* Assicurati che i dettagli del prodotto siano ben illuminati e a fuoco.
* Scattare immagini di spin per abbigliamento di moda con un manichino o modello. Spesso il manichino è mascherato (usando un manichino di vetro) o un manichino stilizzato/dressform è mostrato nell&#39;immagine. Potete creare un set 360 gradi nel modello definendo il numero di angoli. Contrassegna ogni angolo con del nastro sul pavimento in modo da guidare il modello a passo e guardare nella direzione di ogni ripresa.

## Creare un set 360 gradi {#creating-spin-sets}

In questa sezione viene descritto come creare un set 360 gradi in Experience Manager.

>[!NOTE]
>
>Puoi anche creare in automatico i set 360 gradi da [predefiniti set di batch](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:** i set di batch vengono creati dall&#39;IPS (Image Production System) come parte dell&#39;inserimento delle risorse e sono disponibili solo in modalità Dynamic Medie - Scene7.
>
>Consulta &quot;Creazione di set di batch predefiniti per la generazione automatica di set di immagini e set 360 gradi&quot; in [Configurazione di Dynamic Medie - Modalità Scene7](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>

>[!NOTE]
>
>L&#39;ordine in cui le immagini vengono visualizzate in un set 360 gradi è importante. Assicurati di ordinarli in modo che la rotazione sia una visualizzazione uniforme a 360 gradi.

Quando crei un set 360 gradi, Adobe consiglia le best practice seguenti e applica i limiti seguenti:

| Tipo di limite | Best practice | Limitata imposta |
| --- | --- | --- |
| Numero massimo di righe/colonne per set 2D | 12-18 immagini per set | 1000 |

Vedi anche [Limitazioni di Dynamic Medie](/help/assets/limitations.md).

**Per creare un set 360 gradi:**

1. In Assets, individua il punto in cui vuoi creare un set 360 gradi, seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set 360 gradi]**. Puoi anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set 360 gradi.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. Nel campo **[!UICONTROL Titolo]** dell&#39;Editor set 360 gradi immettere un nome per il set 360 gradi. Il nome viene visualizzato nel banner del set 360 gradi. È possibile inserire una descrizione.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Durante la creazione del set 360 gradi, puoi modificare la miniatura del set 360 gradi o consentire all’Experience Manager di selezionarla automaticamente in base alle risorse del set 360 gradi. Per selezionare una miniatura, selezionare **[!UICONTROL Cambia miniatura]** e selezionare un&#39;immagine (è possibile passare ad altre cartelle per trovare le immagini). Se hai selezionato una miniatura e vuoi che Experience Manager ne generi una dal set 360 gradi, seleziona **[!UICONTROL Passa alla miniatura automatica]**.

1. Effettuare una delle seguenti operazioni:

   * Nell&#39;angolo superiore sinistro della pagina Editor set 360 gradi selezionare **[!UICONTROL Aggiungi risorsa]**.

   * Nella parte centrale della pagina Editor set 360 gradi, seleziona **[!UICONTROL Seleziona per aprire il selettore risorse]**.

   Seleziona per selezionare le risorse da includere nel set 360 gradi. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Selezionare il filtro e quindi l&#39;icona **[!UICONTROL Filtro]** sulla barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco]**.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Quando aggiungi risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

   Se necessario, trascina l’icona Riordina di una risorsa a destra del nome del file della risorsa per riordinare le immagini verso l’alto o verso il basso nell’elenco dei set.

   ![Riordinare il frame 11 nel set 360 gradi trascinandolo in una nuova posizione](assets/6_5_spinset-reorderassets.png).

   Riordinamento del frame 11 nel set 360 gradi trascinandolo in una nuova posizione.

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per eliminare un&#39;immagine, selezionarla e selezionare **[!UICONTROL Elimina risorsa]**.

   * Per applicare un predefinito, seleziona **[!UICONTROL Predefinito]** nell&#39;angolo superiore destro della pagina, quindi seleziona un predefinito da applicare a tutte le risorse contemporaneamente.

1. Seleziona **[!UICONTROL Salva]**. Il set 360 gradi appena creato viene visualizzato nella cartella in cui è stato creato.

## Visualizzare un set 360 gradi {#viewing-spin-sets}

Puoi creare i set 360 gradi nell&#39;interfaccia utente o automaticamente utilizzando [set di batch predefiniti](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). Tuttavia, i set creati utilizzando predefiniti set di batch, non *not* vengono visualizzati nell&#39;interfaccia utente. È possibile accedere ai set creati tramite i predefiniti set di batch in tre modi diversi. (Questi metodi sono disponibili anche se hai creato i set 360 gradi nell’interfaccia utente).

>[!NOTE]
>
>È inoltre possibile visualizzare i set tramite l&#39;interfaccia utente come descritto in [Modifica set 360 gradi](#editing-spin-sets).

**Per visualizzare un set 360 gradi:**

1. All’apertura delle proprietà di una singola risorsa. Le proprietà indicano i set di cui la risorsa selezionata è membro (in **[!UICONTROL Membro di set]**). Selezionate il nome del set per visualizzare l&#39;intero set.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Da un’immagine inclusa in un qualsiasi set. Seleziona il menu **[!UICONTROL Set]** per visualizzare i set di cui fa parte la risorsa.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Dalla ricerca, puoi selezionare **[!UICONTROL Filtri]**, quindi espandere **[!UICONTROL Dynamic Media]** e fare clic su **[!UICONTROL Set]**.

   La ricerca restituisce i set corrispondenti creati manualmente nell’interfaccia utente o automaticamente tramite i predefiniti per set di batch. Per i set automatizzati, la query di ricerca viene eseguita utilizzando i criteri di ricerca `Starts with`, che sono diversi dalla ricerca Experience Manager basata sull&#39;utilizzo dei criteri di ricerca `Contains`. L&#39;impostazione del filtro su **[!UICONTROL Set]** è l&#39;unico modo per cercare i set automatizzati.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Modificare un set 360 gradi {#editing-spin-sets}

È possibile eseguire varie attività di modifica sui set 360 gradi, ad esempio:

* Aggiunge immagini al set 360 gradi.
* Riordinare le immagini nel set 360 gradi.
* Eliminare le risorse nel set 360 gradi.
* Applicare i predefiniti visualizzatore.
* Elimina il set 360 gradi.

**Per modificare un set 360 gradi:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa set 360 gradi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa del set 360 gradi, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Fai clic su una risorsa set 360 gradi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) sulla barra degli strumenti.

1. Per modificare il set 360 gradi, effettuate una delle seguenti operazioni:

   * Per riordinare le immagini, trascinatele in una nuova posizione (selezionate l&#39;icona Riordina per spostare gli elementi).
   * Per ordinare gli elementi in ordine crescente o decrescente, selezionare l&#39;intestazione di colonna.
   * Per aggiungere una risorsa o aggiornare una risorsa esistente, seleziona **[!UICONTROL Aggiungi risorsa]**. Passa a una risorsa, selezionala, quindi seleziona **[!UICONTROL Seleziona]** nell&#39;angolo superiore destro.
Se elimini l’immagine utilizzata da Experience Manager per la miniatura sostituendola con un’altra immagine, la risorsa originale viene comunque visualizzata.
   * Per eliminare una risorsa, selezionala e seleziona **[!UICONTROL Elimina risorsa]**.
   * Per applicare un predefinito, fai clic sull’icona Predefinito e seleziona un predefinito.
   * Per eliminare un intero set 360 gradi, passare al set 360 gradi, selezionarlo e selezionare **[!UICONTROL Elimina]**
   >[!NOTE]
   >
   >Per modificare le immagini di un set 360 gradi, passa al set e seleziona **[!UICONTROL Membri set]** nella barra a sinistra, quindi seleziona l&#39;icona a forma di matita su una singola risorsa per aprire la finestra di modifica.

1. Al termine della modifica, seleziona **[!UICONTROL Salva]**.

## Anteprima di un set 360 gradi {#previewing-spin-sets}

Vedi [Anteprima risorse](/help/assets/previewing-assets.md).

## Publish un set 360 gradi {#publishing-spin-sets}

Consulta [Risorse Publish](/help/assets/publishing-dynamicmedia-assets.md).
