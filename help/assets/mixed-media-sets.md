---
title: Set di file multimediali diversi
description: Scopri come lavorare con i set di file multimediali diversi in Dynamic Media
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Set di file multimediali diversi{#mixed-media-sets}

I set di file multimediali diversi consentono di fornire immagini, set di immagini, set 360 gradi e video in un’unica presentazione.

I set di file multimediali diversi sono contrassegnati da un banner con la parola **[!UICONTROL MixedMediaSet]**. Inoltre, se il set di file multimediali diversi è pubblicato, la data di pubblicazione, indicata dall’icona **[!UICONTROL Mondo]** , si trova sul banner insieme all’ultima data di modifica, indicata dall’icona **[!UICONTROL Matita]** .

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Per informazioni sull’interfaccia utente Risorse, consulta [Gestione delle risorse con l’interfaccia](/help/assets/managing-assets-touch-ui.md)touch.

## Avvio rapido: Set di file multimediali diversi {#quick-start-mixed-media-sets}

Per iniziare rapidamente a usare i set di file multimediali diversi, effettuate le seguenti operazioni:

1. [Caricate le risorse](#uploading-assets).

   Per iniziare, caricate le immagini e i video per i set di file multimediali diversi. Se necessario, create i set [di](/help/assets/image-sets.md) immagini e i set [](/help/assets/spin-sets.md)360 gradi. Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di file multimediali diversi, quando scegliete le immagini tenete conto dello zoom. Verificate che le immagini abbiano una dimensione maggiore di almeno 2000 pixel.

1. [Creare set di file multimediali diversi.](#creating-mixed-media-sets)

   Per creare un set di file multimediali diversi, dalla pagina Risorse toccate **[!UICONTROL Crea > Set]** di file multimediali diversi, quindi assegnate un nome al set, scegliete le risorse e scegliete l’ordine in cui vengono visualizzate le immagini.

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Impostate i predefiniti [per visualizzatori](/help/assets/managing-viewer-presets.md)di file multimediali diversi in base alle esigenze.

   Gli amministratori possono creare o modificare i predefiniti per visualizzatori di set di file multimediali diversi. Per visualizzare i file multimediali diversi con un predefinito per visualizzatori, selezionate il set di file multimediali diversi e, nel menu a discesa a sinistra, selezionate **[!UICONTROL Visualizzatori]**.

   Consultate **[!UICONTROL Strumenti > Risorse > Predefiniti]** visualizzatore per creare o modificare i predefiniti per visualizzatori.

   Consultate [Aggiunta e modifica dei predefiniti per visualizzatori.](/help/assets/managing-viewer-presets.md)

1. [Anteprima set di file multimediali diversi.](#previewing-mixed-media-sets)

   Selezionate il set di file multimediali diversi ed effettuate l’anteprima. Fate clic sulle icone delle miniature per esaminare il set di file multimediali diversi nel visualizzatore selezionato. Potete scegliere diversi visualizzatori dal menu **[!UICONTROL Visualizzatori]** , disponibile dal menu a discesa della barra a sinistra.

1. [Pubblicare Set Di File Multimediali Diversi](#publishing-mixed-media-sets)

   La pubblicazione di un set di file multimediali diversi attiva la stringa URL e incorpora. Inoltre, dovete [pubblicare il predefinito](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)per visualizzatori.

1. [Collegare gli URL all’applicazione](/help/assets/linking-urls-to-yourwebapplication.md) Web o [incorporare il visualizzatore](/help/assets/embed-code.md)video o immagini.

   Risorse AEM crea richieste di URL per i set di file multimediali diversi e le attiva dopo la pubblicazione dei set di file multimediali diversi. Potete copiare questi URL quando visualizzate l’anteprima delle risorse. In alternativa, potete incorporarli nel sito Web.

   Selezionate il set di file multimediali diversi, quindi selezionate **[!UICONTROL Visualizzatori dal menu a discesa a sinistra]**.

   Consultate [Collegamento di un set di file multimediali diversi a una pagina](/help/assets/linking-urls-to-yourwebapplication.md) Web e [Incorporazione del visualizzatore](/help/assets/embed-code.md)video o immagini.

Se necessario, potete modificare i set [di file multimediali](#editing-mixed-media-sets)diversi. Inoltre, potete visualizzare e modificare le proprietà [dei set di file multimediali](/help/assets/managing-assets-touch-ui.md#editing-properties)diversi.

>[!NOTE]
>
>In caso di problemi durante la creazione dei set, consultate [Risoluzione dei problemi relativi ai file multimediali dinamici - modalità](/help/assets/troubleshoot-dms7.md)Scene7.

## Caricamento delle risorse {#uploading-assets}

Per iniziare, caricate le immagini e i video per i set di file multimediali diversi. Poiché gli utenti possono eseguire lo zoom sulle immagini nel visualizzatore di set di file multimediali diversi, quando scegliete le immagini tenete conto dello zoom. Verificate che le immagini abbiano una dimensione maggiore di almeno 2000 pixel.

Inoltre, se desiderate aggiungere set 360 gradi o set di immagini al set di file multimediali diversi, create anche questi.

## Creazione di set di file multimediali diversi {#creating-mixed-media-sets}

Potete aggiungere immagini, set di immagini, set 360 gradi e video al set di file multimediali diversi. Assicuratevi che i file, i set di immagini e i set 360 gradi siano pronti per la pubblicazione prima di aggiungerli al set di file multimediali diversi.

Quando aggiungete delle risorse al set, queste vengono automaticamente aggiunte in ordine alfanumerico. Potete riordinare o ordinare manualmente le risorse dopo averle aggiunte.

**Per creare un set di file multimediali diversi**

1. In Risorse, andate nel punto in cui desiderate creare un set di file multimediali diversi, fate clic su **[!UICONTROL Crea]**, quindi selezionate Set di file multimediali **[!UICONTROL diversi]**. Potete anche creare il set dall’interno di una cartella contenente le risorse. Viene visualizzato l’Editor set di file multimediali diversi.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Nell’editor di set di file multimediali diversi, in **[!UICONTROL Titolo]**, inserite un nome per il set di file multimediali diversi. Il nome viene visualizzato nel banner lungo il set di file multimediali diversi. Facoltativamente, immettete una descrizione.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Quando create un set di file multimediali diversi, potete modificare la miniatura del set di file multimediali diversi o consentire ad AEM di selezionare la miniatura automaticamente in base alle risorse del set di file multimediali diversi. Per selezionare una miniatura, fate clic su **[!UICONTROL Cambia miniatura]** e selezionate una qualsiasi immagine (per trovare anche le immagini potete spostarvi in altre cartelle). Se avete selezionato una miniatura e desiderate che AEM ne generi una dal set di file multimediali diversi, selezionate **[!UICONTROL Passa alla miniatura]** automatica.

1. Toccate il selettore delle risorse per selezionare le risorse che desiderate includere nel set di file multimediali diversi. Selezionateli e fate clic su **[!UICONTROL Seleziona]**.

   Con il selettore delle risorse, potete cercare le risorse digitando una parola chiave e toccando **[!UICONTROL Invio]**. Potete anche applicare filtri per perfezionare i risultati della ricerca. Potete filtrare per percorso, raccolta, tipo di file e tag. Selezionate il filtro e toccate l’icona **[!UICONTROL Filtro]** dalla barra degli strumenti. Per modificare la visualizzazione, selezionate l’icona **[!UICONTROL Visualizza]** e selezionate Visualizzazione **** elenco, Visualizzazione **** colonne o Visualizzazione **[!UICONTROL a]** schede.

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Riordinare le risorse trascinandole verso l’alto o verso il basso nell’elenco (se necessario, selezionate l’icona **[!UICONTROL Riordina]** ).

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Per aggiungere delle miniature, fate clic sull’icona **+****[!UICONTROL miniatura]** accanto all’immagine e individuate la miniatura desiderata. Dopo aver selezionato tutte le miniature, fate clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Per aggiungere risorse, toccate **[!UICONTROL Aggiungi risorsa]**.

1. Per eliminare una risorsa, selezionate la casella di controllo corrispondente e toccate **[!UICONTROL Elimina risorsa]**.
1. Per applicare un predefinito, toccate **[!UICONTROL Predefinito]** nell’angolo in alto a destra e selezionate un predefinito da applicare alle risorse.
1. Fai clic su **[!UICONTROL Salva]**. Il set di file multimediali diversi appena creato viene visualizzato nella cartella in cui è stato creato.

## Modifica di set di file multimediali diversi {#editing-mixed-media-sets}

Potete eseguire diverse attività di modifica delle risorse in set di file multimediali diversi direttamente nell’interfaccia utente, [come qualsiasi risorsa in Risorse](/help/assets/managing-assets-touch-ui.md). In Set di file multimediali diversi potete inoltre effettuare le seguenti operazioni:

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
   * Per aggiungere risorse, toccate **[!UICONTROL Aggiungi risorsa]** nella barra degli strumenti. Andate alle risorse. Per ciascuna risorsa da aggiungere, passate il mouse sull&#39;immagine della risorsa (non sul nome della risorsa), quindi toccate l&#39;icona del segno di spunta. Nell&#39;angolo superiore destro, toccate **[!UICONTROL Seleziona]**.

   * Per eliminare una risorsa, toccate **[!UICONTROL Risorse]** (icona immagine) nel pannello a sinistra, quindi selezionate la risorsa. Nella barra degli strumenti toccate **[!UICONTROL Elimina risorsa]**.

   * Per ordinare le risorse in ordine crescente o decrescente in base al nome, toccate **[!UICONTROL Risorse]** nel pannello a sinistra (icona immagine). A destra dell’intestazione **[!UICONTROL Risorse]** , toccate le icone del carrello su o giù.

      >[!NOTE]
      >
      >    * Per eliminare un intero set di file multimediali diversi, passate al set di file multimediali diversi da qualsiasi modalità di visualizzazione (ad esempio **[!UICONTROL vista]** a schede o vista **[!UICONTROL a]** colonne). Passate il mouse sulla risorsa e toccate l&#39;icona del segno di spunta per selezionarla. Premere **[!UICONTROL Backspace]** sulla tastiera oppure fare clic su **[!UICONTROL Altro]** (tre punti) sulla barra degli strumenti, quindi toccare **[!UICONTROL Elimina]**.
         >
         >    
      * Per modificare le risorse in un set di file multimediali diversi, passate al set, fate clic su **Set Members]** nella parte sinistra, quindi toccate l’icona **[!UICONTROL Matita]** su una singola risorsa per aprire la finestra di modifica.


1. Toccate **[!UICONTROL Salva]** al termine della modifica.

   >[!NOTE]
   >
   >* Per modificare le risorse in un set di file multimediali diversi, passate al set di file multimediali diversi. Toccate (non selezionate) il set per aprirlo nella pagina Anteprima set AEM. Nella barra a sinistra, fate clic sul punto a discesa per aprire l&#39;elenco a discesa, quindi toccate **[!UICONTROL Imposta membri]**. Nella pagina Set Members (Imposta membri), passate il mouse su una risorsa, quindi toccate **** Edit (icona matita) per aprire la pagina di modifica.
      >
      >
   * Per eliminare un intero set di file multimediali diversi - Da qualsiasi modalità di visualizzazione (come la vista a schede o a colonne), passate al set di file multimediali diversi. Passa il mouse sul set, quindi tocca **Seleziona]** (icona a forma di segno di spunta). Premere **[!UICONTROL Backspace]** sulla tastiera oppure toccare **[!UICONTROL Altro]** (riga di tre punti), quindi toccare **[!UICONTROL Elimina]**.


## Anteprima dei set di file multimediali diversi {#previewing-mixed-media-sets}

Consultate [Anteprima delle risorse](/help/assets/previewing-assets.md) per informazioni sull’anteprima dei set di file multimediali diversi.

## Pubblicazione di set di file multimediali diversi {#publishing-mixed-media-sets}

Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione dei set di file multimediali diversi.

>[!NOTE]
>
>Se il set di file multimediali diversi non viene visualizzato completamente nel servizio di distribuzione al primo pubblicazione, potrebbe essere necessario pubblicare il set di file multimediali diversi una seconda volta.

