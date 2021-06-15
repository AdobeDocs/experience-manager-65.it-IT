---
title: Profili per elaborazione di metadati, immagini e video
description: Un profilo rappresenta un insieme di regole relative alle opzioni da applicare alle risorse caricate in una cartella. Specifica il profilo di metadati e il profilo di codifica video da applicare alle risorse video caricate. Per le risorse di immagini, puoi anche specificare quale profilo di immagine applicare alle risorse di immagini per ritagliarle correttamente.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
role: Business Practitioner, Administrator
feature: Flusso di lavoro, Gestione risorse, rappresentazioni
exl-id: 3d9367ed-5a02-43aa-abd9-24fae457d4c5
source-git-commit: 4ad5237939289b5411a988424b2a3ecad15ca029
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 1%

---

# Profili per l&#39;elaborazione di metadati, immagini e video{#profiles-for-processing-metadata-images-and-videos}

Un profilo è una ricetta delle opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare il profilo di metadati e il profilo di codifica video da applicare alle risorse video caricate. Oppure, quale profilo di imaging applicare alle risorse di immagini per ritagliarle correttamente.

Tali regole possono includere l’aggiunta di metadati, il ritaglio avanzato delle immagini o la definizione di profili di codifica video. In Adobe Experience Manager puoi creare tre tipi di profili, descritti in dettaglio nei seguenti collegamenti:

* [Profili metadati](/help/assets/metadata-config.md#metadata-profiles)
* [Profili immagine](/help/assets/image-profiles.md)
* [Profili video](/help/assets/video-profiles.md)

Per creare, modificare ed eliminare metadati, immagini o profili video, è necessario disporre dei diritti di amministratore.

Dopo aver creato i metadati, le immagini o il profilo video, li assegni a una o più cartelle che utilizzi come destinazione per le risorse appena caricate.

Un concetto importante per l’utilizzo dei profili in Experience Manager Assets è che vengono assegnati alle cartelle. All’interno di un profilo, le impostazioni sono sotto forma di profili di metadati, insieme a profili video o di immagini. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle relative sottocartelle. Pertanto, la modalità di denominazione di file e cartelle, la modalità di organizzazione delle sottocartelle e la gestione dei file all’interno di tali cartelle hanno un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.
Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate e buone pratiche in materia di metadati, puoi sfruttare al massimo la tua raccolta di risorse digitali e accertarti che i file giusti siano elaborati dal profilo giusto.

>[!NOTE]
>
>Le risorse spostate da una cartella all’altra non vengono rielaborate. Ad esempio, supponiamo che alla cartella 1 sia assegnato il profilo A e alla cartella 2 il cui profilo B è assegnato. Se si spostano le risorse dalla cartella 1 alla cartella 2, le risorse spostate conservano l&#39;elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche quando si spostano le risorse tra due cartelle a cui è stato assegnato lo stesso profilo.

## Rielaborazione delle risorse in una cartella {#reprocessing-assets}

>[!NOTE]
>
>Si applica a *Dynamic Media - Modalità Scene7* solo in Experience Manager 6.4.6.0 o versione successiva.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo di elaborazione esistente che hai successivamente modificato.

Ad esempio, supponi di aver creato un profilo immagine e di averlo assegnato a una cartella. A tutte le risorse immagine caricate nella cartella veniva automaticamente applicato il profilo Immagine alle risorse. Tuttavia, in seguito decidi di aggiungere al profilo una nuova proporzione di ritaglio avanzato. Invece di selezionare e ricaricare nuovamente le risorse nella cartella, esegui semplicemente il *Scene7: Rielaborazione del flusso di lavoro Assets*.

Puoi eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale l’elaborazione non è riuscita la prima volta. Di conseguenza, anche se non hai modificato un profilo di elaborazione o applicato un profilo di elaborazione, puoi comunque eseguire il flusso di lavoro di rielaborazione su una cartella di risorse in qualsiasi momento.

Facoltativamente, puoi regolare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse fino a 1000 risorse. Quando esegui _Scene7: Rielabora il flusso di lavoro Assets_ in una cartella. Le risorse vengono raggruppate in batch e quindi inviate al server Dynamic Media per l’elaborazione. Dopo l’elaborazione, i metadati di ogni risorsa nell’intero set di batch vengono aggiornati ad Experience Manager. Se le dimensioni del batch sono grandi, si potrebbe verificare un ritardo nell&#39;elaborazione. Oppure, se la dimensione del batch è troppo piccola, può causare troppi viaggi di andata e ritorno al server Dynamic Media.

Consulta [Regolazione della dimensione batch del flusso di lavoro di rielaborazione](#adjusting-load).

>[!NOTE]
>
>Se esegui una migrazione di massa delle risorse da Dynamic Media Classic ad Experience Manager, devi abilitare l’agente di replica di migrazione sul server Dynamic Media. Al termine della migrazione, assicurati di disabilitare l’agente.
>
>L’agente di pubblicazione della migrazione deve essere disabilitato sul server Dynamic Media in modo che il flusso di lavoro Rielabora funzioni come previsto.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Per rielaborare le risorse in una cartella:**

1. Ad Experience Manager, dalla pagina Risorse, passa a una cartella di risorse a cui è assegnato un profilo di elaborazione e alla quale desideri applicare il **[!UICONTROL Scene7: Rielaborazione del flusso di lavoro Asset]**,

   Le cartelle a cui è già stato assegnato un profilo di elaborazione sono indicate dalla visualizzazione del nome del profilo che si trova direttamente sotto il nome della cartella nella Vista a schede.

1. Seleziona una cartella.

   * Il flusso di lavoro considera in modo ricorsivo tutti i file presenti nella cartella selezionata.
   * Se sono presenti una o più sottocartelle con risorse nella cartella principale selezionata, il flusso di lavoro rielabora ogni risorsa nella gerarchia delle cartelle.
   * Come best practice, evita di eseguire questo flusso di lavoro in una gerarchia di cartelle con più di 1000 risorse.

1. Fai clic su **[!UICONTROL Timeline]** dall’elenco a discesa nell’angolo in alto a sinistra della pagina.
1. Fai clic sull’icona del carrello ( **^** ) nell’angolo in basso a sinistra della pagina, a destra del campo Commento .

   ![Rielaborazione del flusso di lavoro delle risorse 1](/help/assets/assets/reprocess-assets1.png)

1. Fai clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Dall’elenco a discesa **[!UICONTROL Avvia flusso di lavoro]** , scegli **[!UICONTROL Scene7: Rielabora le risorse]**.
1. (Facoltativo) Nel campo di testo **Immetti il titolo del flusso di lavoro** , immetti un nome per il flusso di lavoro. Se necessario, puoi utilizzare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Rielaborazione delle risorse 2](/help/assets/assets/reprocess-assets2.png)

1. Fai clic su **[!UICONTROL Start]**, quindi fai clic su **[!UICONTROL Conferma]**.

   Per monitorare il flusso di lavoro o controllarne l’avanzamento, dalla pagina della console principale Experience Manager fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]**. Nella pagina Istanze flusso di lavoro , seleziona un flusso di lavoro. Nella barra dei menu, fai clic su **[!UICONTROL Apri cronologia]**. Puoi anche interrompere, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regolazione della dimensione batch del flusso di lavoro di rielaborazione {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è 50 risorse per processo. Questa dimensione batch ottimale è governata dalla dimensione media delle risorse e dai tipi MIME delle risorse su cui viene eseguita la rielaborazione. Un valore più alto indica che in un singolo processo di rielaborazione sono presenti molti file. Pertanto, il banner di elaborazione rimane sulle risorse di Experience Manager per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola - 1 MB o inferiore - l&#39;Adobe consiglia di aumentare il valore a diversi 100, ma mai più di 1000. Se la dimensione media del file è grande, ad esempio centinaia di MB, Adobe consiglia di ridurre la dimensione del batch fino a 10.

**Per regolare facoltativamente la dimensione batch del flusso di lavoro di rielaborazione:**

1. Ad Experience Manager, fai clic su **[!UICONTROL Adobe Experience Manager]** per accedere alla console di navigazione globale, quindi fai clic sull&#39;icona **[!UICONTROL Strumenti]** (martello) > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli flusso di lavoro, in Vista a schede o Vista a elenco, seleziona **[!UICONTROL Scene7: Rielabora le risorse]**.

   ![Pagina Modelli di flusso di lavoro con Scene7: Rielaborazione del flusso di lavoro delle risorse selezionato nella vista a schede](/help/assets/assets-dm/reprocess-assets7.png)

1. Nella barra degli strumenti, fai clic su **[!UICONTROL Modifica]**. Viene visualizzata una nuova scheda del browser Scene7: Rielabora la pagina del modello di flusso di lavoro Assets.
1. Su Scene7: Rielabora la pagina del flusso di lavoro Assets, nell’angolo in alto a destra, fai clic su **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, seleziona il componente Caricamento in batch di Scene7 per aprire la barra degli strumenti, quindi fai clic su **[!UICONTROL Configura]** sulla barra degli strumenti.

   ![Componente Caricamento in batch di Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. Nella finestra di dialogo **[!UICONTROL Caricamento in batch in Scene7 - Proprietà passaggio]** , imposta quanto segue:
   * Nei campi di testo **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]**, immetti un nuovo titolo e una nuova descrizione per il processo, se necessario.
   * Seleziona **[!UICONTROL Handler Advance]** se il tuo handler andrà avanti al passaggio successivo.
   * Nel campo **[!UICONTROL Timeout]** , immetti il timeout del processo esterno (secondi).
   * Nel campo **[!UICONTROL Punto]**, immettere un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * Nel **[!UICONTROL Campo batch]**, immetti il numero massimo di risorse (50-1000) da elaborare in un processo di caricamento batch di elaborazione batch del server Dynamic Media.
   * Seleziona **[!UICONTROL Avanzamento su timeout]** se desideri avanzare quando viene raggiunto il timeout. Annulla selezione se desideri passare alla casella in entrata quando viene raggiunto il timeout.

   ![Finestra di dialogo Proprietà](/help/assets/assets-dm/reprocess-assets3.png)

1. Nell&#39;angolo in alto a destra della finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà passaggio]**, fai clic su **[!UICONTROL Fine]**.

1. Nell’angolo in alto a destra di Scene7: Rielabora la pagina del modello di flusso di lavoro Assets, fai clic su **[!UICONTROL Sincronizza]**. Quando vedi **[!UICONTROL Sincronizzato]**, il modello di runtime del flusso di lavoro viene sincronizzato correttamente e pronto per rielaborare le risorse in una cartella.

   ![Sincronizzazione del modello di flusso di lavoro](/help/assets/assets-dm/reprocess-assets1.png)

1. Chiudi la scheda del browser che mostra Scene7: Rielabora il modello di flusso di lavoro Assets.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
