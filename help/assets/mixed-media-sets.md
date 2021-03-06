---
title: Set di file multimediali diversi
description: Scopri come utilizzare i set di file multimediali diversi in Dynamic Media
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Mixed Media Sets,Asset Management
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 7b29fc96768dc2238ebf9596b136ec10fa71aca9
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 17%

---

# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire un mix di immagini, set di immagini, set 360 gradi e video in una presentazione.

I set di file multimediali diversi sono indicati da un banner con la parola **[!UICONTROL MixedMediaSet]**. Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente di Assets, consulta [Gestire le risorse](/help/assets/manage-assets.md).

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettua le seguenti operazioni:

1. [Caricare le risorse](#uploading-assets).

   Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Se necessario, crea i [Set di immagini](/help/assets/image-sets.md) e i [Set 360 gradi](/help/assets/spin-sets.md). Poiché gli utenti possono effettuare lo zoom sulle immagini nel Visualizzatore set di file multimediali diversi, scegli con attenzione le immagini. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel.

   Vedi [Dynamic Media - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) per un elenco dei formati supportati dai set di file multimediali diversi.

1. [Creare set di file multimediali diversi](#creating-mixed-media-sets).

   Per creare un set di file multimediali diversi, dalla pagina Risorse seleziona **[!UICONTROL Crea]** > **[!UICONTROL Set di file multimediali diversi]** quindi assegna un nome al set, scegli le risorse e scegli l’ordine in cui vengono visualizzate le immagini.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

1. Configurazione [Predefiniti visualizzatore di file multimediali diversi](/help/assets/managing-viewer-presets.md), se necessario.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set di file multimediali diversi predefiniti. Per visualizzare i file multimediali diversi con un predefinito per visualizzatori, seleziona il set di file multimediali diversi e fai clic su **[!UICONTROL Visualizzatori]** nel menu a discesa della barra a sinistra.

   Per creare o modificare i predefiniti visualizzatore, consulta **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti visualizzatore]**.

   Vedi [Aggiungere e modificare i predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

1. [Anteprima set di file multimediali diversi](#previewing-mixed-media-sets).

   Seleziona il set di file multimediali diversi e puoi visualizzarlo in anteprima. Seleziona le icone delle miniature per esaminare il set di file multimediali diversi nel visualizzatore selezionato. Puoi scegliere diversi visualizzatori dal **[!UICONTROL Visualizzatori]** disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare set di file multimediali diversi](#publishing-mixed-media-sets).

   La pubblicazione di un set di file multimediali diversi attiva l’URL e la stringa di incorporamento. Inoltre, devi [pubblicare il predefinito visualizzatore](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Collegare gli URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md) o [Incorporare il visualizzatore di video o immagini](/help/assets/embed-code.md).

   Adobe Experience Manager Assets crea chiamate URL per set di file multimediali diversi e li attiva dopo la pubblicazione dei set di file multimediali diversi. Puoi copiare questi URL quando visualizzi l’anteprima delle risorse. In alternativa è possibile incorporarli sul sito Web.

   Seleziona il set di file multimediali diversi, quindi seleziona dal menu a discesa della barra a sinistra **[!UICONTROL Visualizzatori]**.

   Vedi [Collegamento di un set di file multimediali diversi a una pagina web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporare il visualizzatore di video o immagini](/help/assets/embed-code.md).

Se necessario, puoi modificare [Set di file multimediali diversi](#editing-mixed-media-sets). Inoltre, puoi visualizzare e modificare [Proprietà set di file multimediali diversi](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>In caso di problemi nella creazione dei set, vedi [Risoluzione dei problemi Dynamic Media - Modalità Scene7](/help/assets/troubleshoot-dms7.md).

## Carica risorse {#uploading-assets}

Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Poiché gli utenti possono effettuare lo zoom sulle immagini nel Visualizzatore set di file multimediali diversi, scegli con attenzione le immagini. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel.

Inoltre, se desideri aggiungere set 360 gradi o set di immagini al set di file multimediali diversi, crea anche questi set.

Vedi [Dynamic Media - Formati immagine raster supportati](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) per un elenco dei formati supportati dai set di file multimediali diversi.

## Creare un set di file multimediali diversi {#creating-mixed-media-sets}

Puoi aggiungere immagini, set di immagini, set 360 gradi e video al set di file multimediali diversi. Assicurati che i file, i set di immagini e i set 360 gradi siano pronti per la pubblicazione prima di aggiungerli al set di file multimediali diversi.

Quando aggiungi delle risorse al set, queste vengono aggiunte automaticamente in ordine alfanumerico. Puoi riordinare o ordinare manualmente le risorse dopo averle aggiunte.

**Per creare un set di file multimediali diversi:**

1. In Assets, individua il punto in cui vuoi creare un set di file multimediali diversi e seleziona **[!UICONTROL Crea]**, quindi seleziona **[!UICONTROL Set di file multimediali diversi]**. Puoi anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set di file multimediali diversi.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Nell’Editor set di file multimediali diversi, in **[!UICONTROL Titolo]**, immetti un nome per il set di file multimediali diversi. Il nome viene visualizzato nel banner nel set di file multimediali diversi. Facoltativamente, immetti una descrizione.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Quando crei il set di file multimediali diversi, puoi modificare la miniatura del set di file multimediali diversi o consentire ad Experience Manager di selezionarla automaticamente in base alle risorse nel set di file multimediali diversi. Per selezionare una miniatura, seleziona **[!UICONTROL Modifica miniatura]** e seleziona qualsiasi immagine (puoi passare ad altre cartelle per trovare anche le immagini). Se hai selezionato una miniatura e poi decidi che desideri che Experience Manager ne generi una dal set di file multimediali diversi, seleziona **[!UICONTROL Passa alla miniatura automatica]**.

1. Seleziona il Selettore risorse per selezionare le risorse da includere nel set di file multimediali diversi. Selezionali e seleziona **[!UICONTROL Seleziona]**.

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio]**. Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e quindi seleziona la **[!UICONTROL Filtro]** dalla barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona **[!UICONTROL Visualizza]** e fai clic su **[!UICONTROL Vista a elenco]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a schede]**.

   Vedi [Utilizzare i selettori](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Riordinare le risorse trascinandole verso l’alto o verso il basso nell’elenco (è necessario selezionare la **[!UICONTROL Riordina]** (icona), se necessario.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere le miniature, seleziona la **+** **[!UICONTROL miniatura]** accanto all’immagine e passa alla miniatura desiderata. Dopo aver selezionato tutte le miniature, seleziona **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Per aggiungere risorse, seleziona **[!UICONTROL Aggiungi risorsa]**.

1. Per eliminare una risorsa, seleziona la casella di controllo corrispondente e seleziona **[!UICONTROL Elimina risorsa]**.
1. Per applicare un predefinito, seleziona **[!UICONTROL Predefinito]** nell’angolo in alto a destra e seleziona un predefinito da applicare alle risorse.
1. Seleziona **[!UICONTROL Salva]**. Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modificare un set di file multimediali diversi {#editing-mixed-media-sets}

Puoi eseguire varie attività di modifica alle risorse in Set di file multimediali diversi direttamente nell’interfaccia utente [come qualsiasi risorsa in Assets](/help/assets/manage-assets.md). In Set di file multimediali diversi è inoltre possibile effettuare le seguenti operazioni:

* Aggiungi le risorse al set di file multimediali diversi.
* Riordinare le risorse nel set di file multimediali diversi.
* Elimina le risorse nel set di file multimediali diversi.
* Applica i predefiniti visualizzatore.
* Modifica la miniatura predefinita.

**Per modificare un set di file multimediali diversi:**

1. Effettua una delle seguenti operazioni:

   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita).
   * Passa il puntatore del mouse su una risorsa del set di file multimediali diversi, seleziona **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi seleziona **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Seleziona una risorsa Set di file multimediali diversi, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) sulla barra degli strumenti.

1. Nell’Editor set di file multimediali diversi, effettua una delle seguenti operazioni:

   * Per riordinare le risorse: nel pannello a sinistra, seleziona **[!UICONTROL Risorse]** (icona immagine), trascina una risorsa in una nuova posizione.
   * Per aggiungere risorse, seleziona nella barra degli strumenti **[!UICONTROL Aggiungi risorsa]**. Passa alle risorse. Per ogni risorsa da aggiungere, passa il cursore del mouse sull’immagine della risorsa (non sul nome della risorsa), quindi seleziona l’icona a forma di segno di spunta. Nell’angolo in alto a destra, seleziona **[!UICONTROL Seleziona]**.

   * Per eliminare una risorsa - Nel pannello a sinistra, seleziona **[!UICONTROL Risorse]** (icona immagine), quindi seleziona la risorsa. Nella barra degli strumenti, seleziona **[!UICONTROL Elimina risorsa]**.

   * Per ordinare le risorse in base al loro nome in ordine crescente o decrescente, nel pannello a sinistra seleziona **[!UICONTROL Risorse]** (icona immagine). A destra del **[!UICONTROL Risorse]** intestazione, selezionare le icone del cursore verso l’alto o verso il basso.

      >[!NOTE]
      >
      >* Per eliminare un intero set di file multimediali diversi da qualsiasi modalità di visualizzazione (ad esempio **[!UICONTROL Vista a schede]** o **[!UICONTROL Vista a colonne]**) passa al set di file multimediali diversi. Passa il puntatore del mouse sulla risorsa e seleziona l’icona del segno di spunta per selezionarla. Press **[!UICONTROL Backspace]** sulla tastiera, oppure seleziona **[!UICONTROL Altro]** (tre punti) sulla barra degli strumenti, quindi seleziona **[!UICONTROL Elimina]**.
      >
      >* Per modificare le risorse di un set di file multimediali diversi, passa al set e fai clic su **[!UICONTROL Imposta membri]** nella barra a sinistra. Seleziona la **[!UICONTROL Matita]** su una singola risorsa per aprirla nella finestra di modifica.


1. Seleziona **[!UICONTROL Salva]** al termine della modifica.

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passa a Set di file multimediali diversi. Toccate (non selezionate) il set per aprirlo nella pagina Anteprima set di Experienci Manager . Nella barra a sinistra, seleziona il cursore verso il basso per aprire l’elenco a discesa, quindi seleziona **[!UICONTROL Imposta membri]**. Nella pagina Membri set , passa il puntatore del mouse su una risorsa, quindi seleziona **[!UICONTROL Modifica]** (icona a forma di matita) per aprire la pagina di modifica.
   >
   >* Per eliminare un intero set di file multimediali diversi: da qualsiasi modalità di visualizzazione (come Vista a schede o Vista a colonne), vai al set di file multimediali diversi. Passa il puntatore del mouse sul set, quindi seleziona **Seleziona** (icona a forma di segno di spunta). Press **[!UICONTROL Backspace]** sulla tastiera, oppure seleziona **[!UICONTROL Altro]** (riga di tre punti), quindi seleziona **[!UICONTROL Elimina]**.


## Anteprima di un set di file multimediali diversi {#previewing-mixed-media-sets}

Vedi [Anteprima risorse](/help/assets/previewing-assets.md) per informazioni dettagliate su come visualizzare in anteprima i set di file multimediali diversi.

## Pubblicare un set di file multimediali diversi {#publishing-mixed-media-sets}

Vedi [Pubblicare le risorse](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare set di file multimediali diversi.

>[!NOTE]
>
>Se il set di file multimediali diversi non termina completamente nel servizio di consegna al primo momento della pubblicazione, pubblica il set di file multimediali diversi una seconda volta.
