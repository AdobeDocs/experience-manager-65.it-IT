---
title: Gestire le risorse composte con riferimenti e più pagine
description: Scopri come creare riferimenti a risorse digitali dall’interno [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. La funzione Visualizzatore pagina consente di visualizzare le singole pagine delle risorse secondarie di file con più pagine, ad esempio file PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---


# Gestione di risorse composte e multipagina {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già presenti nella directory archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a [!DNL Experience Manager] risorse, viene creato un collegamento bidirezionale tra le risorse caricate e quelle a cui viene fatto riferimento.

Oltre ad eliminare la ridondanza, il riferimento alle risorse nelle [!DNL Adobe Creative Cloud] applicazioni migliora la collaborazione e aumenta l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta il riferimento bidirezionale. Potete trovare le risorse di riferimento nella pagina dei dettagli delle risorse del file caricato. Inoltre, potete visualizzare i file che fanno riferimento alla risorsa nella pagina dei dettagli della risorsa di riferimento.

I riferimenti vengono risolti in base a percorso, ID documento e ID istanza delle risorse a cui viene fatto riferimento.

## Aggiungi risorse digitali come riferimenti in [!DNL Adobe Illustrator] {#refai}

È possibile fare riferimento a risorse digitali esistenti direttamente da un [!DNL Adobe Illustrator] file.

1. Utilizzando [app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)desktop di Experience Manager, recuperate le risorse digitali nel file system locale. Andate alla posizione del file system della risorsa a cui desiderate fare riferimento.
1. Trascinate la risorsa dalla cartella locale al [!DNL Illustrator] file.

1. Salvate il [!DNL Illustrator] file nell&#39;unità montata o [caricatelo](/help/assets/manage-assets.md#uploading-assets) nell&#39; [!DNL Experience Manager] archivio.

1. Al termine del flusso di lavoro, passate alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** nella colonna **[!UICONTROL Riferimenti]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dipendenze]** possono essere utilizzate anche da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento per una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fare clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti. Nella pagina [!UICONTROL Proprietà] , l’elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato nella colonna **[!UICONTROL Riferimenti]** della scheda **[!UICONTROL Base]** .

   ![visualizzare i riferimenti di Risorse  Experience Manager nella colonna Riferimenti nei dettagli della risorsa](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse.*

## Aggiungi risorse digitali come riferimenti in [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento a risorse digitali da un [!DNL InDesign] file, trascinate le risorse sul [!DNL InDesign] file o esportate il [!DNL InDesign] file come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. Potete estrarre le risorse secondarie [configurando  InDesign Server](indesign.md). Le risorse incorporate in un [!DNL InDesign] file vengono estratte come risorse secondarie.

>[!NOTE]
>
>Se il file [!DNL InDesign Server] è proxy, [!DNL InDesign] l’anteprima dei file viene incorporata nei metadati XMP. In questo caso, l&#39;estrazione delle miniature non è obbligatoria in modo esplicito. Tuttavia, se il file non [!DNL InDesign Server] è proxy, le miniature devono essere esplicitamente estratte per [!DNL InDesign] i file.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile all’ [aggiunta di risorse digitali come riferimenti in  Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Per creare un nuovo flusso di lavoro, effettua i passaggi descritti in [Creazione di modelli](/help/sites-developing/workflows-models.md) di flusso di lavoro.
1. Utilizzate la funzione Pacchetto di per [!DNL Adobe InDesign] esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come un pacchetto. In questo caso, la cartella esportata contiene una cartella di collegamenti che contiene risorse secondarie nel [!DNL InDesign] file.
1. Create un file ZIP e caricatelo nella [!DNL Experience Manager] directory archivio.
1. Avviate il `Unarchiver` flusso di lavoro.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Links vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse di riferimento, andate alla pagina dei dettagli delle risorse della [!DNL InDesign] risorsa e chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

## Aggiungi risorse digitali come riferimenti in [!DNL Adobe Photoshop] {#refps}

1. Utilizzate [!DNL Experience Manager] l&#39;app desktop per accedere [!DNL Experience Manager Assets]. Scaricate e visualizzate le risorse nel file system locale. Utilizzate la funzionalità [!UICONTROL Inserisci collegato] in [!DNL Adobe Photoshop]. Consultate [Inserire risorse nell’app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)desktop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Salvate nel [!DNL Photoshop] file l&#39;unità montata o [caricate](/help/assets/manage-assets.md#uploading-assets) nella [!DNL Experience Manager] directory archivio.
1. Al termine del flusso di lavoro, i riferimenti alle [!DNL Experience Manager] risorse esistenti sono elencati nella pagina dei dettagli della risorsa.

   Per visualizzare le risorse a cui si fa riferimento, chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli della risorsa.

1. Le risorse a cui viene fatto riferimento contengono anche l’elenco delle risorse a cui fanno riferimento. Per visualizzare un elenco delle risorse di riferimento, andate alla pagina dei dettagli delle risorse e chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al relativo ID documento e all’ID istanza. Questa funzionalità è disponibile solo con [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] versioni. Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa composta principale, come già fatto nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati con più pagine — File PDF, file AI [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] file e [!DNL Adobe InDesign] file — [!DNL Experience Manager] potete generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Tali risorse secondarie sono collegate alla risorsa *principale* e facilitano la visualizzazione di più pagine. Per tutti gli altri scopi, le attività secondarie sono trattate come attività normali in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per attivare la generazione di risorse secondarie, effettuate le seguenti operazioni:

1. Accedete come [!DNL Experience Manager] amministratore. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Selezionate il flusso di lavoro Aggiorna risorsa **** DAM e fate clic su **[!UICONTROL Modifica]**.
1. Fate clic su **[!UICONTROL Attiva pannello]** laterale e individuate il passaggio **[!UICONTROL Crea risorsa]** secondaria. Aggiungete il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettuate una delle seguenti operazioni:

* Nuove risorse: Il flusso di lavoro [!UICONTROL DAM Update Assets] viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse multipagina.
* Risorse multipagina esistenti: Esegui manualmente il flusso di lavoro [!UICONTROL DAM Update Assets] seguendo una delle seguenti procedure:

   * Selezionate una risorsa e fate clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizzare la scelta rapida da tastiera `alt + 3`. Fate clic su [!UICONTROL Avvia flusso di lavoro], selezionate [!UICONTROL DAM Update Asset](Aggiorna risorsa [!UICONTROL DAM), fate clic su]Avvia [!UICONTROL e fate clic su]Procedi.
   * Selezionate una risorsa e fate clic su [!UICONTROL Crea] > [!UICONTROL Flusso di lavoro] dalla barra degli strumenti. Dalla finestra di dialogo a comparsa, selezionate Flusso di lavoro di aggiornamento risorse  DAM, fate clic su [!UICONTROL Avvia]e quindi su [!UICONTROL Procedi].

In modo specifico per i documenti di Microsoft Word, eseguite il flusso di lavoro **[!UICONTROL di analisi dei documenti]** di Word DAM. Viene generato un `cq:Page` componente dal contenuto del documento di Microsoft Word. Il `cq:Page` componente fa riferimento alle immagini estratte dal documento. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

## View subassets {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se sono state generate delle risorse secondarie e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, aprite la risorsa con più pagine. Nell’area in alto a sinistra della pagina, fate clic su ![Opzione per aprire la barra](assets/do-not-localize/aem_leftrail_contentonly.png) a sinistra, quindi fate clic su **[!UICONTROL Risorse]** secondarie dall’elenco. Quando selezionate **[!UICONTROL Risorse]** secondarie dall’elenco. In alternativa, utilizzare la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie per una risorsa con più pagine](assets/view_subassets_simulation.gif)

## Visualizzare le pagine di un file con più pagine {#view-pages-of-a-multi-page-file}

Potete visualizzare un file con più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, utilizzando la funzione Visualizzatore pagina di [!DNL Experience Manager Assets]. Aprite una risorsa con più pagine e fate clic su **[!UICONTROL Visualizza pagine]** nell’angolo in alto a sinistra della pagina. Il visualizzatore pagina che apre mostra le pagine della risorsa e i controlli per scorrere e ingrandire ciascuna pagina.

![Visualizzare e visualizzare le pagine di una risorsa con più pagine](assets/view_multipage_asset_fmr.gif)

Ad [!DNL InDesign]esempio, è possibile estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante la creazione del [!DNL InDesign] file, non [!DNL InDesign Server] è necessario per l’estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni]** desktop per aprire o visualizzare una risorsa secondaria specifica mediante l’app [!DNL Experience Manager] desktop. Scoprite come [configurare le azioni](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) desktop se utilizzate l&#39;app [!DNL Experience Manager] desktop.

* **[!UICONTROL L’opzione Proprietà]** consente di aprire la pagina [!UICONTROL Proprietà] della risorsa secondaria specifica.

* **[!UICONTROL L’opzione Annota]** consente di inserire note sulla risorsa secondaria specifica. Le annotazioni utilizzate in risorse secondarie separate vengono raccolte e visualizzate insieme all’apertura della risorsa principale per la visualizzazione.

* **[!UICONTROL L’opzione Panoramica]** pagina consente di visualizzare tutte le risorse secondarie contemporaneamente.

* **[!UICONTROL L&#39;opzione Timeline]** dalla barra a sinistra dopo aver fatto clic su ![Opzione per aprire la barra](assets/do-not-localize/aem_leftrail_contentonly.png) a sinistra mostra il flusso di attività per il file.

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere molte risorse per qualsiasi [!DNL Experience Manager] implementazione. Se generate risorse secondarie quando vengono caricate risorse complesse, aggiungete il passaggio nel flusso di lavoro Aggiorna risorsa DAM. Se generate risorse secondarie su richiesta, create un flusso di lavoro separato per generare le risorse secondarie. Un flusso di lavoro dedicato consente di saltare gli altri passaggi del flusso di lavoro DAM Update Asset e di salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Usa app desktop Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [Configurare le azioni desktop in Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Creare Smart Object collegati in  Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserire grafica in  Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

