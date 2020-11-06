---
title: Profili per l’elaborazione di metadati, immagini e video
description: Un profilo rappresenta un insieme di regole relative alle opzioni da applicare alle risorse caricate in una cartella. Specificate il profilo di metadati e il profilo di codifica video da applicare alle risorse video caricate. Per le risorse di immagini, potete anche specificare quale profilo di immagine applicare alle risorse di immagine per poterle ritagliare correttamente.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 141a1783f275c0b3587ebc374bde19a21e107409
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# Profili per l’elaborazione di metadati, immagini e video{#profiles-for-processing-metadata-images-and-videos}

Un profilo è una ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, potete specificare quale profilo di metadati e quale profilo di codifica video applicare alle risorse video caricate. Oppure, quale profilo di imaging applicare alle risorse di immagine per ritagliarle correttamente.

Tali regole possono includere l’aggiunta di metadati, il ritaglio avanzato delle immagini o la definizione di profili di codifica video. In AEM, potete creare tre tipi di profili, descritti dettagliatamente nei seguenti collegamenti:

* [Profili metadati](/help/assets/metadata-config.md#metadata-profiles)
* [Profili immagine](/help/assets/image-profiles.md)
* [Profili video](/help/assets/video-profiles.md)

È necessario disporre dei diritti di amministratore per creare, modificare ed eliminare metadati, immagini o profili video.

Dopo aver creato i metadati, l’immagine o il profilo video, potete assegnarli a una o più cartelle da usare come destinazione per le nuove risorse caricate.

Un concetto importante per l’utilizzo dei profili in  AEM Assets è che vengono assegnati alle cartelle. All’interno di un profilo sono disponibili impostazioni sotto forma di profili di metadati, nonché profili video o profili immagine. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle relative sottocartelle. Di conseguenza, il modo in cui denominate file e cartelle, le modalità di disposizione delle sottocartelle e la gestione dei file all’interno di tali cartelle hanno un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.
Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, potete sfruttare al meglio la raccolta di risorse digitali e assicurarvi che i file corretti vengano elaborati dal profilo corretto.

>[!NOTE]
>
>Le risorse spostate da una cartella all’altra non vengono rielaborate. Ad esempio, supponiamo che alla cartella 1 sia assegnato il profilo A e che alla cartella 2 sia assegnato il profilo B. Se spostate le risorse dalla cartella 1 alla cartella 2, le risorse spostate conservano l’elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche per lo spostamento di risorse tra due cartelle alle quali è assegnato lo stesso profilo.

## Rielaborazione delle risorse in una cartella {#reprocessing-assets}

>[!NOTE]
>
>Applicabile a *Contenuti multimediali dinamici - Modalità* Scene7 solo in AEM 6.4.6.0 o versioni successive.

Potete rielaborare le risorse in una cartella che dispone già di un profilo di elaborazione esistente modificato in seguito.

Ad esempio, se avete creato un profilo Immagine e lo avete assegnato a una cartella, Per tutte le risorse immagine caricate nella cartella, il profilo Immagine veniva applicato automaticamente alle risorse. Tuttavia, in seguito si decide di aggiungere al profilo un nuovo rapporto di ritaglio avanzato. Ora, invece di dover selezionare e ricaricare nuovamente le risorse nella cartella, è sufficiente eseguire l’ *Scene7: Rielabora il flusso di lavoro delle risorse* .

Potete eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale l&#39;elaborazione non è riuscita per la prima volta. Anche se non avete modificato un profilo di elaborazione o non avete applicato un profilo di elaborazione, potete comunque eseguire il flusso di lavoro di rielaborazione in una cartella di risorse in qualsiasi momento.

Facoltativamente potete regolare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse fino a 1000 risorse. Quando si esegue l&#39; _Scene7: Elaborate nuovamente il flusso di lavoro delle risorse_ in una cartella, le risorse vengono raggruppate in batch e quindi inviate al server per l’elaborazione. Dopo l’elaborazione, i metadati di ciascuna risorsa dell’intero set di batch vengono aggiornati in AEM. Se le dimensioni del batch sono molto grandi, potrebbe verificarsi un ritardo nell&#39;elaborazione. Oppure, se la dimensione del batch è troppo piccola, può causare troppi viaggi di andata e ritorno al server Dynamic Media.

Consultate [Regolazione delle dimensioni batch del flusso di lavoro](#adjusting-load)di rielaborazione.

>[!NOTE]
>
>Se state eseguendo una migrazione di massa delle risorse da Dynamic Media Classic a AEM, dovete attivare l’agente di replica della migrazione sul server Dynamic Media. Al termine della migrazione, accertatevi di disabilitare l’agente.
>
>L’agente di pubblicazione della migrazione deve essere disabilitato sul server di contenuti multimediali dinamici, in modo che il flusso di lavoro di rielaborazione funzioni come previsto.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Per rielaborare le risorse in una cartella**:
1. In AEM, dalla pagina Risorse, individuate la cartella di risorse a cui è assegnato un profilo di elaborazione e per la quale desiderate applicare l’ **Scene7: Rielabora flusso di lavoro risorse** ,

   Le cartelle a cui è già stato assegnato un profilo di elaborazione sono indicate dalla visualizzazione del nome del profilo direttamente sotto il nome della cartella in visualizzazione a schede.

1. Selezionate una cartella.

   * Il flusso di lavoro considera in modo ricorsivo tutti i file presenti nella cartella selezionata.
   * Se sono presenti una o più sottocartelle con le risorse nella cartella principale selezionata, il flusso di lavoro rielaborerà tutte le risorse nella gerarchia delle cartelle.
   * Come procedura ottimale, evitate di eseguire questo flusso di lavoro in una gerarchia di cartelle con più di 1000 risorse.

1. Near the upper-left corner of the page, from the drop-down list, click **[!UICONTROL Timeline.]**
1. Nell&#39;angolo inferiore sinistro della pagina, a destra del campo Commento, fate clic sull&#39;icona del carrello ( **^** ) .

   ![Rielabora flusso di lavoro risorse 1](/help/assets/assets/reprocess-assets1.png)

1. Fate clic su **[!UICONTROL Avvia flusso di lavoro.]**
1. Dall’elenco a discesa **[!UICONTROL Avvia flusso di lavoro]** , scegliete **[!UICONTROL Scene7: Rielabora risorse.]**
1. (Facoltativo) Nel campo di testo **Immettere il titolo del flusso di lavoro** , immettere un nome per il flusso di lavoro. Se necessario, potete usare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Rielaborare le risorse 2](/help/assets/assets/reprocess-assets2.png)

1. Fate clic su **[!UICONTROL Avvia]**, quindi su **[!UICONTROL Conferma.]**

   Per monitorare il flusso di lavoro o controllarne l’avanzamento, nella pagina della console principale AEM fare clic su **[!UICONTROL Strumenti > Flusso di lavoro.]** Nella pagina Istanze flusso di lavoro, selezionate un flusso di lavoro. Nella barra dei menu, fate clic su **[!UICONTROL Apri cronologia.]** È inoltre possibile terminare, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regolazione delle dimensioni batch del flusso di lavoro di rielaborazione {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è 50 risorse per processo. Questa dimensione batch ottimale è regolata dalla dimensione media delle risorse e dai tipi MIME di risorse su cui viene eseguita la rielaborazione. Con un valore più elevato potete inserire molti file in un singolo processo di rielaborazione. Di conseguenza, il banner di elaborazione rimane AEM risorse per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola-1 MB o inferiore  Adobe consiglia di aumentare il valore a diverse centinaia, ma mai più di 1000. Se la dimensione media del file è di grandi centinaia di MB- Adobe si consiglia di ridurre la dimensione del batch fino a 10.

**Per regolare facoltativamente la dimensione batch del flusso di lavoro di rielaborazione**

1. In Experience Manager, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL Workflow > Models.]**
1. Nella pagina Modelli flusso di lavoro, nella vista a schede o a elenco, selezionate **[!UICONTROL Scene7: Rielabora risorse]**.

   ![Pagina Modelli di workflow con Scene7: Rielabora flusso di lavoro risorse selezionato nella vista a schede](/help/assets/assets-dm/reprocess-assets7.png)

1. Nella barra degli strumenti, fate clic su **[!UICONTROL Modifica.]** Una nuova scheda del browser apre l&#39;Scene7: Rielabora la pagina del modello del flusso di lavoro Risorse.
1. Su Scene7: Rielabora la pagina del flusso di lavoro delle risorse, nell’angolo in alto a destra, fai clic su **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, selezionate il componente Caricamento batch Scene7 per aprire la barra degli strumenti, quindi fate clic su **[!UICONTROL Configura]** nella barra degli strumenti.

   ![Componente Caricamento batch Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. Nella finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà]** passaggio, impostate le seguenti opzioni:
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * Selezionate **[!UICONTROL Avanzamento]** gestore se il gestore procederà al passaggio successivo.
   * Nel campo **[!UICONTROL Timeout]** , immettere il timeout del processo esterno (secondi).
   * Nel campo **[!UICONTROL Periodo]** , immettete un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * Selezionate **[!UICONTROL Anticipo su timeout]** se desiderate avanzare quando viene raggiunto il timeout. Deselezionate questa opzione se desiderate passare alla inbox quando viene raggiunto il timeout.

   ![Proprietà, finestra di dialogo](/help/assets/assets-dm/reprocess-assets3.png)

1. Nell’angolo in alto a destra della finestra di dialogo Caricamento **[!UICONTROL batch in Scene7 - Proprietà]** passaggio, fate clic su **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro dell&#39;Scene7: Rielabora la pagina del modello di flusso di lavoro Risorse, fai clic su **[!UICONTROL Sincronizza]**. Quando viene visualizzato **[!UICONTROL Sincronizzato]**, il modello runtime del flusso di lavoro viene sincronizzato correttamente e pronto per rielaborare le risorse in una cartella.

   ![Sincronizzazione del modello di workflow](/help/assets/assets-dm/reprocess-assets1.png)

1. Chiudete la scheda del browser che mostra l’Scene7: Rielabora il modello di flusso di lavoro Risorse.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite.]**
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add.]** The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
