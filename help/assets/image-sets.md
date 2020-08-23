---
title: Set di immagini
description: Scopri come lavorare con i set di immagini in Dynamic Media
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 17%

---


# Set di immagini {#image-sets}

I set di immagini offrono agli utenti un’esperienza di visualizzazione integrata, grazie alla quale gli utenti possono vedere diverse viste di un elemento facendo clic su una miniatura. I set di immagini consentono di presentare visualizzazioni alternative di un elemento e il visualizzatore offre strumenti di zoom per esaminare le immagini da vicino.

I set di immagini sono indicati da un banner con la parola `IMAGESET`. Inoltre, se il set di immagini è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-133](assets/chlimage_1-339.png)

All’interno del set di immagini, potete anche creare dei campioni creando un set di immagini e aggiungendo delle miniature.

Questa applicazione è particolarmente utile per visualizzare un elemento con un colore, un motivo o una finitura diversi. Per creare un set di immagini con campioni colore, è necessaria un’immagine per ciascun colore, motivo o finitura differente che desiderate presentare agli utenti. È inoltre necessario disporre di un campione di colore, motivo o finitura per ciascun colore, motivo o finitura.

Ad esempio, supponete di voler presentare immagini di berretti con diverse bollette di colore; le bollette sono rosse, verdi e blu. In questo caso, avete bisogno di tre scatti dello stesso berretto. Avete bisogno di uno scatto con un rosso, uno con un verde, e uno con una bolletta blu. È inoltre necessario disporre di un campione colore rosso, verde e blu. I campioni colore fungono da miniature su cui gli utenti possono fare clic nel visualizzatore di set di campioni per visualizzare il berretto con la visiera rossa, quello con la visiera verde o quello con la visiera blu.

>[!NOTE]
>
>Per informazioni sull’interfaccia utente di Assets, consulta [Gestione delle risorse con l’interfaccia](/help/assets/managing-assets-touch-ui.md)touch.

## Avvio rapido: Set di immagini {#quick-start-image-sets}

Per iniziare subito a lavorare:

1. [Caricate le immagini sorgente principali per più viste.](#uploading-assets-in-image-sets)

   Per iniziare, caricate le immagini per i set di immagini. Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di immagini, tenete conto dello zoom quando scegliete le immagini. Accertatevi che la dimensione massima delle immagini sia di almeno 2000 pixel per garantire dettagli di zoom ottimali. Dynamic Media consente di eseguire il rendering delle immagini fino a 25 megapixel ciascuna. Ad esempio, potete usare un’immagine da 5000 x 5000 megapixel o qualsiasi altra combinazione di dimensioni fino a 25 megapixel.

    AEM Assets supporta molti formati di file immagine, ma si consigliano immagini senza perdita di dati TIFF, PNG ed EPS.

1. [Creare set di immagini.](#creating-image-sets)

   In Set immagini, gli utenti fanno clic sulle miniature nel visualizzatore di set di immagini.

   Per creare un set di immagini nelle risorse, toccate o fate clic su **[!UICONTROL Crea > Set immagini.]** Quindi, aggiungete le immagini e fate clic su **[!UICONTROL Salva.]**

   You can also create image sets automatically through [batch set presets](/help/assets/config-dms7.md).
   >[!IMPORTANT]
   >
   >I set di batch vengono creati dall’IPS (Image Production System) come parte dell’assimilazione delle risorse e sono disponibili solo in modalità Dynamic Media - Scene7.

   Consultate [Preparazione delle risorse di set di immagini per il caricamento e Caricamento dei file](#uploading-assets-in-image-sets).

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Aggiungete i predefiniti [per visualizzatori di set di](/help/assets/managing-viewer-presets.md)immagini in base alle vostre esigenze.

   Gli amministratori possono creare o modificare i predefiniti per visualizzatori di set di immagini. To see your image set with a viewer preset, select the image set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers.]**

   Consultate **[!UICONTROL Strumenti > Risorse > Predefiniti]** visualizzatore per creare o modificare i predefiniti per visualizzatori.

1. (Facoltativo) [Visualizzazione di set](/help/assets/image-sets.md#viewing-image-sets) di immagini creati con predefiniti per set di batch.
1. [Anteprima set di immagini.](/help/assets/previewing-assets.md)

   Selezionate il set di immagini ed effettuate l’anteprima. Fate clic sulle icone delle miniature per esaminare il set di immagini nel visualizzatore selezionato. Potete scegliere diversi visualizzatori dal menu **[!UICONTROL Visualizzatori]** , disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare i set di immagini.](/help/assets/publishing-dynamicmedia-assets.md)

   Quando si pubblica un set di immagini, vengono attivati l’URL e il codice da incorporare. Inoltre, dovete [pubblicare qualsiasi predefinito](/help/assets/managing-viewer-presets.md) per visualizzatori personalizzato creato. I predefiniti per visualizzatori forniti sono già stati pubblicati.

1. [Collegare gli URL all’applicazione](/help/assets/linking-urls-to-yourwebapplication.md) Web o [incorporare il visualizzatore](/help/assets/embed-code.md)video o immagini.

    AEM Assets crea richieste URL per i set di immagini e le attiva dopo la pubblicazione dei set di immagini. Potete copiare questi URL quando visualizzate l’anteprima delle risorse. In alternativa, potete incorporarli nel sito Web.

   Select the Image Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers.]**

   Consulta le sezioni [Collegamento di un set di immagini a una pagina web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporamento di un visualizzatore di video o immagini](/help/assets/embed-code.md).

Per modificare i set di immagini, consultate [Modifica dei set di immagini.](#editing-image-sets) Inoltre, potete visualizzare e modificare le proprietà [dei set di](/help/assets/managing-assets-touch-ui.md#editing-properties)immagini.

In caso di problemi durante la creazione di set, consulta Immagini e set in [Risoluzione di problemi relativi a file multimediali dinamici - modalità](/help/assets/troubleshoot-dms7.md#images-and-sets)Scene7.

## Caricamento delle risorse nei set di immagini {#uploading-assets-in-image-sets}

Per iniziare, caricate le immagini per i set di immagini. Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di immagini, tenete conto dello zoom quando scegliete le immagini. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel. I set di immagini supportano molti formati di file immagine, ma sono consigliate immagini senza perdita di dati TIFF, PNG ed EPS.

Potete caricare le immagini per i set di immagini come fareste per [caricare qualsiasi altra risorsa in Risorse](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Preparazione delle risorse di set di immagini per il caricamento {#preparing-image-set-assets-for-upload}

Prima di creare i set di immagini, accertatevi che le immagini siano delle dimensioni e del formato corretti.

Per creare un set di immagini a visualizzazione multipla, sono necessarie immagini che mostrino un elemento da diversi punti di vista o che mostrino diversi aspetti dello stesso elemento. L’obiettivo è quello di evidenziare le funzioni importanti di un elemento in modo che gli utenti possano avere un’immagine completa dell’aspetto o della funzione dell’elemento.

Poiché gli utenti possono eseguire lo zoom delle immagini in set di immagini, accertatevi che la dimensione maggiore delle immagini sia di almeno 2000 pixel. Le risorse supportano molti formati di file immagine, ma sono consigliate immagini senza perdita di dati TIFF, PNG ed EPS.

>[!NOTE]
>
>Inoltre, se usate delle miniature per indicare i campioni di prodotto, dovete effettuare le seguenti operazioni:
>
>È necessario disporre di vignettature o diversi scatti della stessa immagine che la mostrino in diversi colori, motivi o finiture. Sono inoltre necessari file di miniature corrispondenti ai diversi colori, motivi o finiture. Ad esempio, per presentare le miniature con un set di immagini che mostra la stessa giacca in nero, marrone e verde, è necessario disporre di:
>
>* Una ripresa nera, marrone e verde della stessa giacca.
>* Miniatura di colore nera, marrone e verde.


## Creazione di set di immagini {#creating-image-sets}

Potete creare i set di immagini tramite l’interfaccia utente o l’API. Questa sezione descrive come creare i set di immagini nell’interfaccia utente.

>[!NOTE]
>
>You can also create image sets automatically through [batch set presets](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets).
>**Importante:** I set di batch vengono creati dall’IPS (Image Production System) come parte dell’assimilazione delle risorse e sono disponibili solo in modalità Dynamic Media - Scene7.

Quando aggiungete delle risorse al set, queste vengono automaticamente aggiunte in ordine alfanumerico. Potete riordinare o ordinare manualmente le risorse dopo averle aggiunte.

>[!NOTE]
>
>I set di immagini non sono supportati per le risorse con &quot;,&quot; (virgola) nel nome del file.

**Per creare un set di immagini**

1. In AEM, tocca il logo AEM per accedere alla console di navigazione globale, quindi tocca **[!UICONTROL Navigazione > Risorse.]** Vai nel punto in cui vuoi creare un set di immagini, quindi tocca **[!UICONTROL Crea > Set di immagini]** per aprire la pagina Editor set di immagini.

   Puoi anche creare il set dall’interno di una cartella contenente le risorse.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Nella pagina Editor set di immagini, nel campo **[!UICONTROL Titolo]** , inserite un nome per il set di immagini. Il nome viene visualizzato nel banner lungo il set di immagini. Facoltativamente, immettete una descrizione.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Effettuate una delle seguenti operazioni:

   * Nell’angolo in alto a sinistra della pagina Editor set di immagini, toccate **[!UICONTROL Aggiungi risorsa.]**

   * Nella parte centrale della pagina Editor set di immagini, toccate **[!UICONTROL Toccate per aprire il selettore delle risorse.]**
   Toccate per selezionare le risorse da includere nel set di immagini. Le risorse selezionate dispongono di un’icona a forma di segno di spunta. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select.]**

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando o facendo clic su **[!UICONTROL Invio.]** Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e tocca l’icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, tocca l’icona Visualizza e fai clic su **[!UICONTROL Vista a colonne]**, **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a elenco.]**

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Quando aggiungete delle risorse al set, queste vengono automaticamente aggiunte in ordine alfanumerico. Potete riordinare o ordinare manualmente le risorse dopo averle aggiunte.

   Se necessario, trascinate l’icona Riordina di una risorsa a destra del nome del file della risorsa per riordinare le immagini verso l’alto o verso il basso nell’elenco dei set.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Per modificare una miniatura o un campione, fai clic sull’icona **+** **miniatura** accanto all’immagine e individua la miniatura o il campione desiderato. Dopo aver selezionato tutte le immagini, fai clic su **[!UICONTROL Salva.]**

1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Per eliminare un’immagine, selezionatela e toccate **[!UICONTROL Elimina risorsa.]**

   * To apply a preset, near the upper-right corner of the page, tap **[!UICONTROL Preset]**, then select a preset to apply to all the assets at once.
   >[!NOTE]
   >
   >Quando crei il set di immagini, puoi modificare la miniatura del set o consentire ad AEM di selezionarla automaticamente in base alle risorse del set di immagini. Per selezionare una miniatura, tocca l’opzione **[!UICONTROL Cambia miniatura]** posta sopra il campo Titolo nella pagina Editor set di immagini, quindi seleziona un’immagine a piacere. Per trovare le immagini, puoi esplorare anche altre cartelle. Se hai selezionato una miniatura e vuoi che AEM ne generi una dal set di immagini, fai clic su **[!UICONTROL Passa alla]** **[!UICONTROL Miniatura automatica.]**

1. Fai clic su **[!UICONTROL Salva.]** Il set di immagini appena creato viene visualizzato nella cartella in cui è stato creato.

## Visualizzazione di set di immagini {#viewing-image-sets}

Potete creare i set di immagini nell’interfaccia utente o automaticamente utilizzando i predefiniti [per set di](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets)batch.

>[!IMPORTANT]
>
>I set di batch vengono creati da IPS [Image Production System] come parte dell’assimilazione delle risorse e sono disponibili solo in modalità Dynamic Media - Scene7.)

Tuttavia, i set creati utilizzando i predefiniti per set di batch *non* vengono visualizzati nell’interfaccia utente. Potete visualizzare questi set in tre modi diversi. (Questi metodi sono disponibili anche se avete creato i set di immagini nell’interfaccia utente).

* Aprite le proprietà di una singola risorsa. Le proprietà indicano i set di risorse selezionate a cui viene fatto riferimento per un membro. Fate clic sul nome del set per visualizzare l’intero set.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* Da un’immagine inclusa in un qualsiasi set. Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![6_5_imageset-setspullmenu](assets/6_5_imageset-setspulldownmenu.png)

* From search, you can select **[!UICONTROL Filter]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets.]**

   La ricerca restituisce i set corrispondenti creati manualmente nell’interfaccia utente o automaticamente tramite i predefiniti per set di batch. Per i set automatizzati, la query di ricerca viene eseguita utilizzando i criteri di ricerca &quot;Inizia con&quot;, diversi dalla ricerca AEM basata sull&#39;utilizzo dei criteri di ricerca &quot;Contiene&quot;. L&#39;impostazione del filtro su **[!UICONTROL Set]** è l&#39;unico modo per eseguire la ricerca nei set automatizzati.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Potete visualizzare i set mediante l’interfaccia utente come descritto in [Modifica dei set](#editing-image-sets)di immagini.

## Modifica dei set di immagini {#editing-image-sets}

Potete eseguire diverse attività di modifica sui set di immagini, ad esempio:

* Aggiungete immagini al set di immagini.
* Riordinare le immagini nel set di immagini.
* Potete eliminare le risorse nel set di immagini.
* Applicate i predefiniti per visualizzatori.
* Eliminate il set di immagini.

**Per modificare i set di immagini**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa del set di immagini, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa del set di immagini, toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi toccate **[!UICONTROL Modifica]** sulla barra degli strumenti.
   * Toccate una risorsa set di immagini, quindi toccate **[!UICONTROL Modifica]** (icona matita) sulla barra degli strumenti.

1. Per modificare le immagini nel set di immagini, effettuate una delle seguenti operazioni:

   * Per riordinare le risorse, trascinate un’immagine in una nuova posizione (selezionate l’icona di riordinamento per spostare gli elementi).
   * Per ordinare gli elementi in ordine crescente o decrescente, fate clic sull’intestazione della colonna.
   * Per aggiungere una risorsa o aggiornare una risorsa esistente, fate clic su **[!UICONTROL Aggiungi risorsa.]** Passate a una risorsa, selezionatela, quindi toccate **[!UICONTROL Seleziona]** vicino all’angolo superiore destro della pagina.

      >[!NOTE]
      >
      >Se eliminate l’immagine che AEM usata per la miniatura sostituendola con un’altra immagine, viene comunque visualizzata la risorsa originale.
   * Per eliminare una risorsa, selezionatela e toccate o fate clic su **[!UICONTROL Elimina risorsa.]**
   * To apply a preset, near the upper-right corner of the page, tap **[!UICONTROL Preset]**, then select a viewer preset.
   * Per aggiungere o modificare una miniatura, selezionate l’icona della miniatura accanto alla parte destra della risorsa. Passate alla nuova miniatura o alla nuova risorsa campione, selezionatela, quindi toccate **[!UICONTROL Seleziona.]**
   * Per eliminare un intero set di immagini, selezionatelo e toccate **[!UICONTROL Elimina.]**

   >[!NOTE]
   >
   >Per modificare le immagini di un Set di immagini, tocca il set e, dalla barra a sinistra, seleziona **[!UICONTROL Membri set]**. Per aprire la finestra di modifica, tocca una singola risorsa con l’icona a forma di matita.

1. Toccate **[!UICONTROL Salva]** al termine della modifica.

## Anteprima dei set di immagini {#previewing-image-sets}

Consultate [Anteprima delle risorse](/help/assets/previewing-assets.md).

## Pubblicazione di set di immagini {#publishing-image-sets}

Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).
