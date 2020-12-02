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
source-git-commit: c3ae4447581d946554d792c68d31b47a6b67d5df
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 27%

---


# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire immagini, set di immagini, set 360 gradi e video in un’unica presentazione.

I set di file multimediali diversi sono indicati da un banner con la parola **[!UICONTROL MixedMediaSet.]** Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL mondo]**, è riportata sul banner insieme all’ultima data di modifica, contrassegnata dall’icona a forma di **[!UICONTROL matita]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull&#39;interfaccia utente di Assets, vedi [Gestione risorse](/help/assets/manage-assets.md).

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettuate le seguenti operazioni:

1. [Caricate le risorse](#uploading-assets).

   Per iniziare, carica le immagini e i video per i set di file multimediali diversi. Se necessario, crea i [Set di immagini](/help/assets/image-sets.md) e i [Set 360 gradi](/help/assets/spin-sets.md). Poiché gli utenti possono eseguire lo zoom sulle immagini nel Visualizzatore set di file multimediali diversi, calcola lo zoom al momento di scegliere le immagini. Verifica che le immagini abbiano una dimensione maggiore che sia di almeno 2000 pixel.

1. [Creare set di file multimediali diversi.](#creating-mixed-media-sets)

   Per creare un set di file multimediali diversi, dalla pagina Risorse tocca **[!UICONTROL Crea > Set di file multimediali diversi]**, quindi assegna un nome al set, scegli le risorse e stabilisci l’ordine in cui vengono visualizzate le immagini.

   Vedere [Uso dei selettori.](/help/assets/working-with-selectors.md)

1. Impostate [Predefiniti per visualizzatori di file multimediali diversi](/help/assets/managing-viewer-presets.md) in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti visualizzatore di set di file multimediali diversi predefiniti. Per visualizzare i file multimediali diversi con un predefinito per visualizzatori, selezionate il set di file multimediali diversi e, nel menu a discesa a sinistra, selezionate **[!UICONTROL Visualizzatori.]**

   Per creare o modificare i predefiniti per visualizzatori, consultate **[!UICONTROL Strumenti > Risorse > Predefiniti visualizzatore]**.

   Consultate [Aggiunta e modifica dei predefiniti per visualizzatori.](/help/assets/managing-viewer-presets.md)

1. [Anteprima set di file multimediali diversi.](#previewing-mixed-media-sets)

   Selezionate il set di file multimediali diversi ed effettuate l’anteprima. Fate clic sulle icone delle miniature per esaminare il set di file multimediali diversi nel visualizzatore selezionato. Potete scegliere diversi visualizzatori dal menu **[!UICONTROL Visualizzatori]**, disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare Set Di File Multimediali Diversi](#publishing-mixed-media-sets)

   La pubblicazione di un set di file multimediali diversi attiva la stringa URL e incorpora. Inoltre, è necessario [pubblicare il predefinito per visualizzatori](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Collegate gli URL all’](/help/assets/linking-urls-to-yourwebapplication.md) applicazione Web o  [incorporate il visualizzatore](/help/assets/embed-code.md) video o immagini.

    AEM Assets crea richieste di URL per i set di file multimediali diversi e li attiva dopo la pubblicazione dei set di file multimediali diversi. Potete copiare questi URL quando visualizzate l’anteprima delle risorse. In alternativa, potete incorporarli nel sito Web.

   Selezionate il set di file multimediali diversi, quindi, nel menu a discesa della barra a sinistra, selezionate **[!UICONTROL Visualizzatori.]**

   Consulta le sezioni [Collegamento di un set di file multimediali diversi a una pagina web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporamento di un visualizzatore di video o immagini](/help/assets/embed-code.md).

Se necessario, è possibile modificare i [Set di file multimediali diversi](#editing-mixed-media-sets). Inoltre, potete visualizzare e modificare le proprietà dei set di file multimediali diversi [](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>In caso di problemi durante la creazione dei set, vedere [Risoluzione di problemi relativi ai file multimediali dinamici - modalità Scene7](/help/assets/troubleshoot-dms7.md).

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
   >Quando create il set di file multimediali diversi, potete modificare la miniatura del set di file multimediali diversi o consentire AEM selezionare la miniatura automaticamente in base alle risorse del set di file multimediali diversi. Per selezionare una miniatura, fare clic su **[!UICONTROL Cambia miniatura]** e selezionare una qualsiasi immagine (per trovare anche le immagini, è possibile passare ad altre cartelle). Se è stata selezionata una miniatura e si decide AEM generare una miniatura dal set di file multimediali diversi, selezionare **[!UICONTROL Passa alla miniatura automatica.]**

1. Toccate il selettore delle risorse per selezionare le risorse che desiderate includere nel set di file multimediali diversi. Selezionateli e fate clic su **[!UICONTROL Seleziona.]**

   Con il Selettore risorse, puoi cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio.]** Per perfezionare i risultati della ricerca, puoi anche applicare i filtri. Puoi filtrare in base a percorso, raccolta, tipo di file e tag. Seleziona il filtro e tocca l’icona **[!UICONTROL Filtro]** nella barra degli strumenti. Per modificare la visualizzazione, seleziona l’icona **[!UICONTROL Visualizza]** e fai clic su **[!UICONTROL Vista a elenco]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a schede.]**

   Vedere [Utilizzo dei selettori](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Riordinare le risorse trascinandole verso l’alto o verso il basso nell’elenco (se necessario, selezionate l’icona **[!UICONTROL Riordina]**).

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere delle miniature, fai clic sull’icona **+** **[!UICONTROL miniatura]** accanto all’immagine e individua la miniatura desiderata. Dopo aver selezionato tutte le miniature, fai clic su **[!UICONTROL Salva.]**

   >[!NOTE]
   >
   >Per aggiungere risorse, toccate **[!UICONTROL Aggiungi risorsa.]**

1. Per eliminare una risorsa, selezionate la casella di controllo corrispondente e toccate **[!UICONTROL Elimina risorsa.]**
1. Per applicare un predefinito, toccate **[!UICONTROL Preset]** nell’angolo in alto a destra e selezionate un predefinito da applicare alle risorse.
1. Fai clic su **[!UICONTROL Salva.]** Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modifica di set di file multimediali diversi {#editing-mixed-media-sets}

Potete eseguire diverse attività di modifica alle risorse in set di file multimediali diversi direttamente nell’interfaccia utente [come per qualsiasi risorsa in Assets](/help/assets/manage-assets.md). In Set di file multimediali diversi potete inoltre effettuare le seguenti operazioni:

* Aggiungete le risorse al set di file multimediali diversi.
* Riordinare le risorse nel set di file multimediali diversi.
* Potete eliminare le risorse nel set di file multimediali diversi.
* Applicate i predefiniti per visualizzatori.
* Modificare la miniatura predefinita.

**Per modificare un set di file multimediali diversi**

1. Effettuate una delle seguenti operazioni:

   * Passate il puntatore del mouse su una risorsa del set di file multimediali diversi, quindi toccate **[!UICONTROL Modifica]** (icona matita).
   * Passate il puntatore del mouse su una risorsa del set di file multimediali diversi, toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta), quindi toccate **[!UICONTROL Modifica]** sulla barra degli strumenti.

   * Toccate una risorsa di set di file multimediali diversi, quindi toccate **[!UICONTROL Modifica]** (icona matita) sulla barra degli strumenti.

1. Nell’editor di set di file multimediali diversi, effettuate una delle seguenti operazioni:

   * Per riordinare le risorse: nel pannello a sinistra, toccate **[!UICONTROL Risorse]** (icona immagine), trascinate una risorsa in una nuova posizione.
   * Per aggiungere risorse - Nella barra degli strumenti, toccate **[!UICONTROL Aggiungi risorsa.]** Andate alle risorse. Per ciascuna risorsa da aggiungere, passate il mouse sull&#39;immagine della risorsa (non sul nome della risorsa), quindi toccate l&#39;icona del segno di spunta. Nell&#39;angolo superiore destro, toccare **[!UICONTROL Seleziona.]**

   * Per eliminare una risorsa, toccate **[!UICONTROL Risorse]** (icona immagine) nel pannello a sinistra, quindi selezionate la risorsa. Nella barra degli strumenti, toccate **[!UICONTROL Elimina risorsa.]**

   * Per ordinare le risorse in ordine crescente o decrescente in base al nome, nel pannello a sinistra toccate **[!UICONTROL Risorse]** (icona immagine). A destra dell&#39;intestazione **[!UICONTROL Risorse]**, toccate le icone del carrello su o giù.

      >[!NOTE]
      >
      >* Per eliminare un intero set di file multimediali diversi, dalla modalità di visualizzazione (ad esempio **[!UICONTROL Visualizzazione a schede]** o **[!UICONTROL Visualizzazione a colonne]**) passate al set di file multimediali diversi. Passa il puntatore del mouse sulla risorsa, quindi tocca l’icona del segno di spunta per selezionarla. Premere **[!UICONTROL Backspace]** sulla tastiera oppure fare clic su **[!UICONTROL Altro]** (tre punti) sulla barra degli strumenti, quindi toccare **[!UICONTROL Elimina.]**
         >
         >
      * Per modificare le risorse in un set di file multimediali diversi, andate al set, fate clic su **[!UICONTROL Imposta membri]** nella barra a sinistra, quindi toccate l&#39;icona **[!UICONTROL Matita]** su una singola risorsa per aprire la finestra di modifica.


1. Toccate **[!UICONTROL Salva]** al termine della modifica.

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passa a Set di file multimediali diversi. Per aprire il set nella pagina Anteprima set AEM, toccalo ma non selezionarlo. Nella barra a sinistra, fate clic sul punto a discesa per aprire l&#39;elenco a discesa, quindi toccate **[!UICONTROL Imposta membri.]** Nella pagina Set Members (Imposta membri), passate il mouse su una risorsa, quindi toccate  **[!UICONTROL Edit]** (icona matita) per aprire la pagina di modifica.
      >
      >
   * Per eliminare un intero set di file multimediali diversi: da qualsiasi modalità di visualizzazione (come Vista a schede o Vista a colonne), vai al set di file multimediali diversi. Passa il mouse sul set, quindi tocca **Seleziona** (icona a forma di segno di spunta). Premere **[!UICONTROL Backspace]** sulla tastiera oppure toccare **[!UICONTROL Altro]** (riga di tre punti), quindi toccare **[!UICONTROL Elimina.]**


## Anteprima dei set di file multimediali diversi {#previewing-mixed-media-sets}

Per informazioni sull&#39;anteprima dei set di file multimediali diversi, consultate [Anteprima delle risorse](/help/assets/previewing-assets.md).

## Pubblicazione di set di file multimediali diversi {#publishing-mixed-media-sets}

Per informazioni dettagliate sulla pubblicazione dei set di file multimediali diversi, consultate [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md).

>[!NOTE]
>
>Se il set di file multimediali diversi non viene visualizzato completamente nel servizio di distribuzione al primo pubblicazione, potrebbe essere necessario pubblicare il set di file multimediali diversi una seconda volta.

