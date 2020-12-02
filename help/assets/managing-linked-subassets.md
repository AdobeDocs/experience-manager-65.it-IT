---
title: Gestire le risorse composte con riferimenti e più pagine
description: Scopri come creare riferimenti a risorse digitali dall'interno di [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. La funzione Visualizzatore pagina consente di visualizzare le singole pagine delle risorse secondarie di file con più pagine, ad esempio file PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---


# Gestire risorse composte e con più pagine {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già presenti nella directory archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a risorse [!DNL Experience Manager], viene creato un collegamento bidirezionale tra le risorse caricate e quelle a cui viene fatto riferimento.

Oltre ad eliminare la ridondanza, il riferimento alle risorse nelle applicazioni [!DNL Adobe Creative Cloud] migliora la collaborazione e aumenta l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta il riferimento bidirezionale. Potete trovare le risorse di riferimento nella pagina dei dettagli delle risorse del file caricato. Inoltre, potete visualizzare i file che fanno riferimento alla risorsa nella pagina dei dettagli della risorsa di riferimento.

I riferimenti vengono risolti in base a percorso, ID documento e ID istanza delle risorse a cui viene fatto riferimento.

## Aggiungere risorse digitali come riferimenti in [!DNL Adobe Illustrator] {#refai}

È possibile fare riferimento a risorse digitali esistenti da un file [!DNL Adobe Illustrator].

1. Utilizzando l&#39;app [[!DNL Experience Manager] desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recuperate le risorse digitali nel file system locale. Andate alla posizione del file system della risorsa a cui desiderate fare riferimento.
1. Trascinate la risorsa dalla cartella locale al file [!DNL Illustrator].

1. Salvate il file [!DNL Illustrator] nell&#39;unità montata oppure [caricate](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].

1. Al termine del flusso di lavoro, passate alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** nella colonna **[!UICONTROL Riferimenti]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dependencies]** possono essere utilizzate anche come riferimento da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento per una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fare clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti. Nella pagina [!UICONTROL Proprietà], l&#39;elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato nella colonna **[!UICONTROL Riferimenti]** nella scheda **[!UICONTROL Base]**.

   ![visualizzare i riferimenti di Risorse  Experience Manager nella colonna Riferimenti nei dettagli della risorsa](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse.*

## Aggiungere risorse digitali come riferimenti in [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento a risorse digitali da un file [!DNL InDesign], trascinate le risorse nel file [!DNL InDesign] o esportate il file [!DNL InDesign] come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. È possibile estrarre le risorse secondarie configurando  InDesign Server[. ](indesign.md) Le risorse incorporate in un file [!DNL InDesign] vengono estratte come risorse secondarie.

>[!NOTE]
>
>Se il file [!DNL InDesign Server] è proxy, i file [!DNL InDesign] presentano l&#39;anteprima incorporata nei metadati XMP. In questo caso, l&#39;estrazione delle miniature non è obbligatoria in modo esplicito. Tuttavia, se il file [!DNL InDesign Server] non è proxy, le miniature devono essere estratte in modo esplicito per i file [!DNL InDesign].

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [aggiungere risorse digitali come riferimenti in  Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Per creare un nuovo flusso di lavoro, eseguite i passaggi descritti in [Crea modelli di flusso di lavoro](/help/sites-developing/workflows-models.md).
1. Utilizzate la funzione Pacchetto di [!DNL Adobe InDesign] per esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come un pacchetto. In questo caso, la cartella esportata contiene una cartella Links contenente risorse secondarie nel file [!DNL InDesign].
1. Create un file ZIP e caricatelo nell&#39;archivio [!DNL Experience Manager].
1. Avviare il flusso di lavoro `Unarchiver`.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Links vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse indicate, andate alla pagina dei dettagli delle risorse della risorsa [!DNL InDesign] e chiudete la barra [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

## Aggiungere risorse digitali come riferimenti in [!DNL Adobe Photoshop] {#refps}

1. Utilizzate l&#39;app desktop [!DNL Experience Manager] per accedere a [!DNL Experience Manager Assets]. Scaricate e visualizzate le risorse nel file system locale. Utilizzate la funzionalità [!UICONTROL Inserisci collegato] in [!DNL Adobe Photoshop]. Consultate [inserire risorse nell&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Salvare in [!DNL Photoshop] file sull&#39;unità montata o [caricare](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].
1. Al termine del flusso di lavoro, i riferimenti alle risorse [!DNL Experience Manager] esistenti sono elencati nella pagina dei dettagli della risorsa.

   Per visualizzare le risorse di riferimento, chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli della risorsa.

1. Le risorse a cui viene fatto riferimento contengono anche l’elenco delle risorse a cui fanno riferimento. Per visualizzare un elenco delle risorse di riferimento, andate alla pagina dei dettagli delle risorse e chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al relativo ID documento e all’ID istanza. Questa funzionalità è disponibile solo nelle versioni [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa composta principale, come già fatto nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati con più pagine — File PDF, file AI, file [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] e [!DNL Adobe InDesign] file — [!DNL Experience Manager] può generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Queste risorse secondarie sono collegate alla risorsa *principale* e semplificano la visualizzazione di più pagine. Per tutti gli altri scopi, le attività secondarie sono trattate come attività normali in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per attivare la generazione di risorse secondarie, effettuate le seguenti operazioni:

1. Accedete a [!DNL Experience Manager] come amministratore. Accedete a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Selezionare il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** e fare clic su **[!UICONTROL Modifica]**.
1. Fare clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** e individuare il passaggio **[!UICONTROL Crea risorsa secondaria]**. Aggiungete il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettuate una delle seguenti operazioni:

* Nuove risorse: Il flusso di lavoro [!UICONTROL Risorse aggiornamento DAM] viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse multipagina.
* Risorse multipagina esistenti: Eseguire manualmente il flusso di lavoro [!UICONTROL DAM Update Assets] seguendo una delle seguenti procedure:

   * Selezionate una risorsa e fate clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizzare la scelta rapida da tastiera `alt + 3`. Fate clic su [!UICONTROL Avvia flusso di lavoro], selezionate [!UICONTROL Aggiorna risorsa DAM], fate clic su [!UICONTROL Avvia] e fate clic su [!UICONTROL Procedi].
   * Selezionate una risorsa e fate clic su [!UICONTROL Crea] > [!UICONTROL Workflow] nella barra degli strumenti. Dalla finestra di dialogo a comparsa, selezionate il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM], fate clic su [!UICONTROL Avvia] e fate clic su [!UICONTROL Procedi].

Per i documenti di Microsoft Word, eseguire il flusso di lavoro **[!UICONTROL DAM Parse Word Documents]**. Viene generato un componente `cq:Page` dal contenuto del documento di Microsoft Word. Alle immagini estratte dal documento viene fatto riferimento dal componente `cq:Page`. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

## Visualizza risorse secondarie {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se sono state generate delle risorse secondarie e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, aprite la risorsa con più pagine. Nell&#39;area in alto a sinistra della pagina, fare clic su ![Opzione per aprire la barra laterale sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) e fare clic su **[!UICONTROL Risorse secondarie]** dall&#39;elenco. Quando si seleziona **[!UICONTROL Risorse secondarie]** dall&#39;elenco. In alternativa, utilizzare la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie per una risorsa con più pagine](assets/view_subassets_simulation.gif)

## Visualizzare le pagine di un file con più pagine {#view-pages-of-a-multi-page-file}

Potete visualizzare un file con più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, utilizzando la funzione Visualizzatore pagina di [!DNL Experience Manager Assets]. Aprite una risorsa con più pagine e fate clic su **[!UICONTROL Visualizza pagine]** nell’angolo in alto a sinistra della pagina. Il visualizzatore pagina che apre mostra le pagine della risorsa e i controlli per scorrere e ingrandire ciascuna pagina.

![Visualizzare e visualizzare le pagine di una risorsa con più pagine](assets/view_multipage_asset_fmr.gif)

Per [!DNL InDesign], è possibile estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante la creazione di file [!DNL InDesign], [!DNL InDesign Server] non è richiesto per l&#39;estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni]** desktop per aprire o visualizzare una risorsa secondaria specifica mediante l’app  [!DNL Experience Manager] desktop. Scopri come [configurare Azioni desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se utilizzi un&#39;app desktop [!DNL Experience Manager].

* **[!UICONTROL L’]** opzione Proprietà consente di aprire la pagina   Proprietà della risorsa secondaria specifica.

* **[!UICONTROL L’opzione]** Annota consente di aggiungere annotazioni alla risorsa secondaria specifica. Le annotazioni utilizzate in risorse secondarie separate vengono raccolte e visualizzate insieme all’apertura della risorsa principale per la visualizzazione.

* **[!UICONTROL L’opzione]** Anteprima pagina visualizza tutte le risorse secondarie contemporaneamente.

* **[!UICONTROL L&#39;opzione]** Timelineantenella parte sinistra dopo aver fatto clic su  ![Opzione per aprire la ](assets/do-not-localize/aem_leftrail_contentonly.png) barra laterale sinistra visualizza il flusso di attività per il file.

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere molte risorse per qualsiasi distribuzione [!DNL Experience Manager]. Se generate risorse secondarie quando vengono caricate risorse complesse, aggiungete il passaggio nel flusso di lavoro Aggiorna risorsa DAM. Se generate risorse secondarie su richiesta, create un flusso di lavoro separato per generare le risorse secondarie. Un flusso di lavoro dedicato consente di saltare gli altri passaggi del flusso di lavoro DAM Update Asset e di salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Usa app desktop Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurare le azioni desktop in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Creare Smart Object collegati in  Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserire grafica in  Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

