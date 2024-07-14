---
title: Gestire le risorse composte con riferimenti e più pagine
description: Scopri come creare riferimenti alle risorse digitali da  [!DNL Adobe InDesign], [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Utilizza la funzione Visualizzatore pagina per visualizzare singole pagine di risorse secondarie di file di più pagine come PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---

# Gestire le risorse composte e multipagina {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già esistenti nell&#39;archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a [!DNL Experience Manager] risorse, viene creato un collegamento bidirezionale tra le risorse caricate e di riferimento.

Oltre a eliminare la ridondanza, il riferimento alle risorse nelle applicazioni [!DNL Adobe Creative Cloud] migliora la collaborazione e aumenta l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta riferimenti bidirezionali. Puoi trovare le risorse di riferimento nella pagina dei dettagli delle risorse del file caricato. Inoltre, puoi visualizzare i file di riferimento nella pagina dei dettagli della risorsa di riferimento.

I riferimenti vengono risolti in base al percorso, all’ID documento e all’ID istanza delle risorse di riferimento.

## [!DNL Adobe Illustrator]: aggiungi risorse digitali come riferimenti {#refai}

È possibile fare riferimento alle risorse digitali esistenti da un file [!DNL Adobe Illustrator].

1. Utilizzando l&#39;[[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recupera le risorse digitali nel file system locale. Passa alla posizione del file system della risorsa a cui desideri fare riferimento.
1. Trascina la risorsa dalla cartella locale al file [!DNL Illustrator].

1. Salvare il file [!DNL Illustrator] nell&#39;unità montata o [caricare](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].

1. Al termine del flusso di lavoro, vai alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** nella colonna **[!UICONTROL Riferimenti]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse a cui si fa riferimento visualizzate in **[!UICONTROL Dipendenze]** possono essere referenziate anche da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento per una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fare clic su **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti. Nella pagina [!UICONTROL Proprietà], l&#39;elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato nella colonna **[!UICONTROL Riferimenti]** della scheda **[!UICONTROL Base]**.

   ![visualizza i riferimenti di Experience Manager Assets nella colonna Riferimenti nei dettagli della risorsa](assets/asset-references.png)

   *Figura: riferimenti alle risorse nei dettagli delle risorse.*

## [!DNL Adobe InDesign]: aggiungi risorse digitali come riferimenti {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento alle risorse digitali da un file [!DNL InDesign], trascinare le risorse nel file [!DNL InDesign] o esportare il file [!DNL InDesign] come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. Puoi estrarre le risorse secondarie [configurando InDesign Server](indesign.md). Le risorse incorporate in un file [!DNL InDesign] vengono estratte come risorse secondarie.

>[!NOTE]
>
>Se [!DNL InDesign Server] è proxy, l&#39;anteprima di [!DNL InDesign] file è incorporata nei metadati XMP. In questo caso, l’estrazione delle miniature non è esplicitamente richiesta. Tuttavia, se [!DNL InDesign Server] non è proxy, le miniature devono essere estratte in modo esplicito per i file [!DNL InDesign].

Quando viene caricato un file INDD, i riferimenti vengono recuperati eseguendo una query sulle risorse con proprietà `xmpMM:InstanceID` e `xmpMM:DocumentID` nell&#39;archivio.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [aggiungere risorse digitali come riferimenti in Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Segui i passaggi descritti in [Creare modelli di flusso di lavoro](/help/sites-developing/workflows-models.md) per creare un flusso di lavoro.
1. Utilizza la [funzionalità pacchetto](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) di [!DNL Adobe InDesign] per esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come pacchetto. In questo caso, la cartella esportata contiene una cartella `Links` che contiene risorse secondarie nel file [!DNL InDesign]. La cartella `Links` è presente nella stessa cartella del file INDD.
1. Creare un file ZIP e caricarlo nell&#39;archivio [!DNL Experience Manager].
1. Avvia il flusso di lavoro `Unarchiver`.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Collegamenti vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli della risorsa [!DNL InDesign] e chiudi la [barra](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: aggiungi risorse digitali come riferimenti {#refps}

1. Utilizza l&#39;app desktop [!DNL Experience Manager] per accedere a [!DNL Experience Manager Assets]. Scarica e mostra le risorse sul file system locale. Utilizza la funzionalità [!UICONTROL Inserisci con collegamento] in [!DNL Adobe Photoshop]. Consulta [posizionare risorse nell&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salvare nel file [!DNL Photoshop] nell&#39;unità montata o [caricare](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].
1. Al termine del flusso di lavoro, i riferimenti alle risorse [!DNL Experience Manager] esistenti sono elencati nella pagina dei dettagli delle risorse.

   Per visualizzare le risorse a cui si fa riferimento, chiudi la [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli delle risorse.

1. Le risorse di riferimento contengono anche l’elenco delle risorse da cui fanno riferimento. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli delle risorse e chiudi la [barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al loro ID documento e ID istanza. Questa funzionalità è disponibile solo nelle versioni [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop]. Per altri, il riferimento viene fatto in base al percorso relativo delle risorse collegate nella risorsa principale composta, come nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati a più pagine, ovvero file PDF, file AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] file e [!DNL Adobe InDesign] file, [!DNL Experience Manager] può generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Queste risorse secondarie sono collegate alla risorsa *principale* e facilitano la visualizzazione multipagina. Per tutti gli altri scopi, le risorse secondarie vengono trattate come normali risorse in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per abilitare la generazione di risorse secondarie, effettua le seguenti operazioni:

1. Accedere a [!DNL Experience Manager] come amministratore. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** e fai clic su **[!UICONTROL Modifica]**.
1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** e individua il passaggio **[!UICONTROL Crea risorsa secondaria]**. Aggiungi il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettuate una delle seguenti operazioni:

* Nuove risorse: il flusso di lavoro [!UICONTROL DAM Update Assets] viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse con più pagine.
* Risorse a più pagine esistenti: esegui manualmente il flusso di lavoro [!UICONTROL DAM Update Assets] seguendo uno dei passaggi seguenti:

   * Seleziona una risorsa e fai clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizzare la scelta rapida da tastiera `alt + 3`. Fai clic su [!UICONTROL Avvia flusso di lavoro], seleziona [!UICONTROL Risorsa di aggiornamento DAM], fai clic su [!UICONTROL Inizia] e fai clic su [!UICONTROL Procedi].
   * Seleziona una risorsa e fai clic su [!UICONTROL Crea] > [!UICONTROL Flusso di lavoro] nella barra degli strumenti. Dalla finestra di dialogo a comparsa, seleziona il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM], fai clic su [!UICONTROL Inizia] e fai clic su [!UICONTROL Procedi].

Per i documenti di Microsoft Word, eseguire il flusso di lavoro **[!UICONTROL Analisi documenti Word DAM]**. Genera un componente `cq:Page` dal contenuto del documento di Microsoft Word. Il componente `cq:Page` fa riferimento alle immagini estratte dal documento. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

>[!NOTE]
>
>Nel processo [!UICONTROL Crea risorsa secondaria - Proprietà passaggio] in [!UICONTROL Argomenti processo], puoi specificare il numero di risorse secondarie generate da [!DNL Experience Manager]. Il valore predefinito è 5. Per generare tutte le risorse secondarie, lascia vuoto il campo. Se il campo ha un valore negativo, non vengono generate risorse secondarie.

## Visualizzare le risorse secondarie {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se vengono generate e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, apri la risorsa multipagina. Nell&#39;area superiore sinistra della pagina, fai clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) e fai clic su **[!UICONTROL Risorse secondarie]** dall&#39;elenco. Quando selezioni **[!UICONTROL Risorse secondarie]** dall&#39;elenco. In alternativa, utilizzare la scelta rapida da tastiera `alt + 5`.

![Visualizzare risorse secondarie per una risorsa multipagina](assets/view_subassets_simulation.gif)

## Visualizzare le pagine di un file con più pagine {#view-pages-of-a-multi-page-file}

È possibile visualizzare un file di più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, utilizzando la funzionalità Visualizzatore pagine di [!DNL Experience Manager Assets]. Apri una risorsa multipagina e fai clic su **[!UICONTROL Visualizza pagine]** dall&#39;angolo superiore sinistro della pagina. Il Visualizzatore pagine che viene aperto visualizza le pagine della risorsa e i controlli per sfogliare ed eseguire lo zoom di ogni pagina.

![Visualizzare e visualizzare le pagine di una risorsa con più pagine](assets/view_multipage_asset_fmr.gif)

Per [!DNL InDesign], è possibile estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante la creazione del file [!DNL InDesign], [!DNL InDesign Server] non è necessario per l&#39;estrazione delle pagine.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni desktop]** per aprire o visualizzare una risorsa secondaria specifica tramite l&#39;app desktop [!DNL Experience Manager]. Scopri come [configurare le azioni desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se utilizzi [!DNL Experience Manager] app desktop.

* L&#39;opzione **[!UICONTROL Proprietà]** apre la pagina [!UICONTROL Proprietà] della risorsa secondaria specifica.

* L&#39;opzione **[!UICONTROL Annota]** consente di annotare la risorsa secondaria specifica. Le annotazioni utilizzate su risorse secondarie separate vengono raccolte e visualizzate insieme quando la risorsa principale viene aperta per la visualizzazione.

* L&#39;opzione **[!UICONTROL Panoramica pagina]** visualizza tutte le risorse secondarie contemporaneamente.

* L&#39;opzione **[!UICONTROL Timeline]** dalla barra a sinistra dopo aver fatto clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) visualizza il flusso di attività per il file.

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere molte risorse in qualsiasi distribuzione di [!DNL Experience Manager]. Se generi risorse secondarie durante il caricamento di risorse complesse, aggiungi il passaggio nel flusso di lavoro Aggiorna risorsa DAM. Se generi risorse secondarie on-demand, crea un flusso di lavoro separato per generarle. Un flusso di lavoro dedicato consente di saltare gli altri passaggi del flusso di lavoro Risorsa di aggiornamento DAM e di salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Utilizza l&#39;app desktop Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurare le azioni desktop in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Crea oggetti avanzati collegati in Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Posizionare elementi grafici in Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
