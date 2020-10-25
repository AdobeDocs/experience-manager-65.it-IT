---
title: Set di file multimediali diversi
description: Scoprite come utilizzare i set di file multimediali diversi in Contenuti multimediali dinamici
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 27%

---


# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire immagini, set di immagini, set 360 gradi e video in un’unica presentazione.

I set di file multimediali diversi sono indicati da un banner con la parola **[!UICONTROL MixedMediaSet.]** Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente di Assets, consulta [Gestione delle risorse con l’interfaccia](/help/assets/manage-assets.md)touch.

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettuate le seguenti operazioni:

1. [Caricate le risorse](#uploading-assets).

   Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Se necessario, crea i [Set di immagini](/help/assets/image-sets.md) e i [Set 360 gradi](/help/assets/spin-sets.md). Poiché gli utenti possono eseguire lo zoom sulle immagini nel Visualizzatore set di file multimediali diversi, calcola lo zoom al momento di scegliere le immagini. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel.

1. [Creare set di file multimediali diversi.](#creating-mixed-media-sets)

   Per creare un set di file multimediali diversi, dalla pagina Risorse tocca **[!UICONTROL Crea > Set di file multimediali diversi]**, quindi assegna un nome al set, scegli le risorse e stabilisci l’ordine in cui vengono visualizzate le immagini.

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Impostate i predefiniti [per visualizzatori](/help/assets/managing-viewer-presets.md)di file multimediali diversi in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set di file multimediali diversi predefiniti. To see your mixed media with a viewer preset, select the mixed media set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers.]**

   Consultate **[!UICONTROL Strumenti > Risorse > Predefiniti]** visualizzatore per creare o modificare i predefiniti per visualizzatori.

   Consultate [Aggiunta e modifica dei predefiniti per visualizzatori.](/help/assets/managing-viewer-presets.md)

1. [Anteprima set di file multimediali diversi.](#previewing-mixed-media-sets)

   Selezionate il set di file multimediali diversi ed effettuate l’anteprima. Fate clic sulle icone delle miniature per esaminare il set di file multimediali diversi nel visualizzatore selezionato. Potete scegliere diversi visualizzatori dal menu **[!UICONTROL Visualizzatori]** , disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare Set Di File Multimediali Diversi](#publishing-mixed-media-sets)

   La pubblicazione di un set di file multimediali diversi attiva la stringa URL e incorpora. Inoltre, dovete [pubblicare il predefinito](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)per visualizzatori.

1. [Collegare gli URL all’applicazione](/help/assets/linking-urls-to-yourwebapplication.md) Web o [incorporare il visualizzatore](/help/assets/embed-code.md)video o immagini.

    AEM Assets crea richieste di URL per i set di file multimediali diversi e li attiva dopo la pubblicazione dei set di file multimediali diversi. Potete copiare questi URL quando visualizzate l’anteprima delle risorse. In alternativa, potete incorporarli nel sito Web.

   Select the Mixed Media Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers.]**

   Consulta le sezioni [Collegamento di un set di file multimediali diversi a una pagina web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporamento di un visualizzatore di video o immagini](/help/assets/embed-code.md).

Se necessario, potete modificare i set [di file multimediali](#editing-mixed-media-sets)diversi. Inoltre, potete visualizzare e modificare le proprietà [dei set di file multimediali](/help/assets/manage-assets.md#editing-properties)diversi.

>[!NOTE]
>
>In caso di problemi durante la creazione dei set, consulta [Risoluzione dei problemi relativi ai file multimediali dinamici - Modalità](/help/assets/troubleshoot-dms7.md)Scene7.

## Caricamento delle risorse {#uploading-assets}

Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di file multimediali diversi, quando scegliete le immagini tenete conto dello zoom. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel.

Inoltre, se desiderate aggiungere set 360 gradi o set di immagini al set di file multimediali diversi, create anche questi.

## Creazione di set di file multimediali diversi {#creating-mixed-media-sets}

Potete aggiungere immagini, set di immagini, set 360 gradi e video al set di file multimediali diversi. Assicuratevi che i file, i set di immagini e i set 360 gradi siano pronti per la pubblicazione prima di aggiungerli al set di file multimediali diversi.

Quando aggiungete delle risorse al set, queste vengono automaticamente aggiunte in ordine alfanumerico. Potete riordinare o ordinare manualmente le risorse dopo averle aggiunte.

**Per creare un set di file multimediali diversi**

1. In Assets, individua il punto in cui vuoi creare un set di file multimediali diversi, fai clic su **[!UICONTROL Crea]** e seleziona **[!UICONTROL Set di file multimediali diversi.]** Puoi anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set di file multimediali diversi.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Nell’editor di set di file multimediali diversi, in **[!UICONTROL Titolo]**, inserite un nome per il set di file multimediali diversi. Il nome viene visualizzato nel banner all’interno del set di file multimediali diversi. Facoltativamente, immettete una descrizione.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Quando create il set di file multimediali diversi, potete modificare la miniatura del set di file multimediali diversi o consentire AEM selezionare la miniatura automaticamente in base alle risorse del set di file multimediali diversi. Per selezionare una miniatura, fate clic su **[!UICONTROL Cambia miniatura]** e selezionate una qualsiasi immagine (per trovare anche le immagini potete spostarvi in altre cartelle). If you have selected a thumbnail and then decide that you want AEM to generate one from the mixed media set, select **[!UICONTROL Switch to Automatic thumbnail.]**

1. Toccate il selettore delle risorse per selezionare le risorse che desiderate includere nel set di file multimediali diversi. Selezionateli e fate clic su **[!UICONTROL Seleziona.]**

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio.]** Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e tocca l’icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona **[!UICONTROL Visualizza]** e fai clic su **[!UICONTROL Vista a elenco]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a schede.]**

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Riordinate le risorse trascinandole verso l’alto o verso il basso nell’elenco (se necessario, selezionate l’icona **[!UICONTROL Riordina]** ).

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere delle miniature, fai clic sull’icona **+** **[!UICONTROL miniatura]** accanto all’immagine e individua la miniatura desiderata. Dopo aver selezionato tutte le miniature, fai clic su **[!UICONTROL Salva.]**

   >[!NOTE]
   >
   >Per aggiungere delle risorse, toccate **[!UICONTROL Aggiungi risorsa.]**

1. Per eliminare una risorsa, selezionate la casella di controllo corrispondente e toccate **[!UICONTROL Elimina risorsa.]**
1. Per applicare un predefinito, toccate **[!UICONTROL Predefinito]** nell’angolo in alto a destra e selezionate un predefinito da applicare alle risorse.
1. Fai clic su **[!UICONTROL Salva.]** Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modifica di set di file multimediali diversi {#editing-mixed-media-sets}

Potete eseguire diverse attività di modifica delle risorse in set di file multimediali diversi direttamente nell’interfaccia utente, [come qualsiasi risorsa in Risorse](/help/assets/manage-assets.md). In Set di file multimediali diversi potete inoltre effettuare le seguenti operazioni:

* Aggiungete le risorse al set di file multimediali diversi.
* Riordinare le risorse nel set di file multimediali diversi.
* Potete eliminare le risorse nel set di file multimediali diversi.
* Applicate i predefiniti per visualizzatori.
* Modificare la miniatura predefinita.

**Per modificare un set di file multimediali diversi**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa del set di file multimediali diversi, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa di set di file multimediali diversi, toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi toccate **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Toccate una risorsa di set di file multimediali diversi, quindi toccate **[!UICONTROL Modifica]** (icona matita) sulla barra degli strumenti.

1. Nell’editor di set di file multimediali diversi, effettuate una delle seguenti operazioni:

   * Per riordinare le risorse - Nel pannello a sinistra, toccate **[!UICONTROL Risorse]** (icona immagine), trascinate una risorsa in una nuova posizione.
   * Per aggiungere risorse, toccate **[!UICONTROL Aggiungi risorsa nella barra degli strumenti.]** Andate alle risorse. Per ciascuna risorsa da aggiungere, passate il mouse sull&#39;immagine della risorsa (non sul nome della risorsa), quindi toccate l&#39;icona del segno di spunta. Nell&#39;angolo superiore destro, toccate **[!UICONTROL Seleziona.]**

   * Per eliminare una risorsa, toccate **[!UICONTROL Risorse]** (icona immagine) nel pannello a sinistra, quindi selezionate la risorsa. Nella barra degli strumenti toccate **[!UICONTROL Elimina risorsa.]**

   * Per ordinare le risorse in ordine crescente o decrescente in base al nome, toccate **[!UICONTROL Risorse]** nel pannello a sinistra (icona immagine). A destra dell’intestazione **[!UICONTROL Risorse]** , toccate le icone del carrello su o giù.

      >[!NOTE]
      >
      >* To delete an entire Mixed Media Set, from any viewing mode (such as **[!UICONTROL Card View]** or **[!UICONTROL Column View]**) navigate to the Mixed Media Set. Passa il puntatore del mouse sulla risorsa, quindi tocca l’icona del segno di spunta per selezionarla. Press **[!UICONTROL Backspace]** on the keyboard, or click **[!UICONTROL More]** (three dots) on the toolbar, then tap **[!UICONTROL Delete.]**
         >
         >
      * You can edit the assets in a Mixed Media Set by navigating to the set, clicking **[!UICONTROL Set Members]** in the left rail, and then tapping the **[!UICONTROL Pencil]** icon on an individual asset to open the editing window.


1. Toccate **[!UICONTROL Salva]** al termine della modifica.

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passa a Set di file multimediali diversi. Per aprire il set nella pagina Anteprima set AEM, toccalo ma non selezionarlo. In the left rail, click the down caret to open the drop-down list, then tap **[!UICONTROL Set Members.]** Nella pagina Set Members (Imposta membri), passate il mouse su una risorsa, quindi toccate **** Edit (icona matita) per aprire la pagina di modifica.
      >
      >
   * Per eliminare un intero set di file multimediali diversi: da qualsiasi modalità di visualizzazione (come Vista a schede o Vista a colonne), vai al set di file multimediali diversi. Hover on the set, then tap **Select** (checkmark icon). Press **[!UICONTROL Backspace]** on your keyboard, or tap **[!UICONTROL More]** (row of three dots), then tap **[!UICONTROL Delete.]**


## Anteprima dei set di file multimediali diversi {#previewing-mixed-media-sets}

Consultate [Anteprima delle risorse](/help/assets/previewing-assets.md) per informazioni sull’anteprima dei set di file multimediali diversi.

## Pubblicazione di set di file multimediali diversi {#publishing-mixed-media-sets}

Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione dei set di file multimediali diversi.

>[!NOTE]
>
>Se il set di file multimediali diversi non viene visualizzato completamente nel servizio di distribuzione al primo pubblicazione, potrebbe essere necessario pubblicare il set di file multimediali diversi una seconda volta.

