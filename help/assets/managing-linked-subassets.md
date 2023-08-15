---
title: Gestire le risorse composte con riferimenti e più pagine
description: Scopri come creare riferimenti alle risorse digitali da [!DNL Adobe InDesign], [!DNL Adobe Illustrator], e [!DNL Adobe Photoshop]. Utilizza la funzione Visualizzatore pagina per visualizzare singole pagine di risorse secondarie di file di più pagine come PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 0%

---

# Gestire le risorse composte e multipagina {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già esistenti nell’archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a [!DNL Experience Manager] risorse, viene creato un collegamento bidirezionale tra le risorse caricate e di riferimento.

Oltre a eliminare la ridondanza, fare riferimento alle risorse in [!DNL Adobe Creative Cloud] le applicazioni migliorano la collaborazione e l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta il riferimento bidirezionale. Puoi trovare le risorse di riferimento nella pagina dei dettagli delle risorse del file caricato. Inoltre, puoi visualizzare i file di riferimento nella pagina dei dettagli della risorsa di riferimento.

I riferimenti vengono risolti in base al percorso, all’ID documento e all’ID istanza delle risorse di riferimento.

## [!DNL Adobe Illustrator]: aggiungi risorse digitali come riferimenti {#refai}

Puoi fare riferimento alle risorse digitali esistenti da un [!DNL Adobe Illustrator] file.

1. Utilizzo di [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recupera le risorse digitali nel file system locale. Passa alla posizione del file system della risorsa a cui desideri fare riferimento.
1. Trascina la risorsa dalla cartella locale al [!DNL Illustrator] file.

1. Salva il [!DNL Illustrator] sull&#39;unità montata, oppure [caricare](/help/assets/manage-assets.md#uploading-assets) al [!DNL Experience Manager] archivio.

1. Al termine del flusso di lavoro, vai alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** nel **[!UICONTROL Riferimenti]** colonna.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dipendenze]** possono essere utilizzati anche da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento di una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Clic **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti. In [!UICONTROL Proprietà] , l’elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato sotto **[!UICONTROL Riferimenti]** colonna nella **[!UICONTROL Base]** scheda.

   ![visualizzare i riferimenti di Experience Manager Assets nella colonna Riferimenti nei dettagli della risorsa;](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse.*

## [!DNL Adobe InDesign]: aggiungi risorse digitali come riferimenti {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento a risorse digitali da un [!DNL InDesign] file, trascina le risorse sul file [!DNL InDesign] file o esporta [!DNL InDesign] file come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. Puoi estrarre le risorse secondarie per [configurazione di InDesign Server](indesign.md). Risorse incorporate in un [!DNL InDesign] I file vengono estratti come risorse secondarie.

>[!NOTE]
>
>Se il [!DNL InDesign Server] è proxy, [!DNL InDesign] l&#39;anteprima dei file è incorporata nei relativi metadati XMP. In questo caso, l’estrazione delle miniature non è esplicitamente richiesta. Tuttavia, se [!DNL InDesign Server] non è un proxy, le miniature devono essere estratte esplicitamente per [!DNL InDesign] file.

Quando viene caricato un file INDD, i riferimenti vengono recuperati eseguendo una query sulle risorse con `xmpMM:InstanceID` e `xmpMM:DocumentID` nell&#39;archivio.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [aggiungere risorse digitali come riferimenti in Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Eseguire i passaggi descritti in [Creare modelli di flusso di lavoro](/help/sites-developing/workflows-models.md) per creare un nuovo workflow.
1. Utilizza il [Funzione pacchetto](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) di [!DNL Adobe InDesign] per esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come pacchetto. In questo caso, la cartella esportata contiene `Links` cartella che contiene risorse secondarie in [!DNL InDesign] file. Il `Links` è presente nella stessa cartella del file INDD.
1. Creare un file ZIP e caricarlo in [!DNL Experience Manager] archivio.
1. Avvia il `Unarchiver` flusso di lavoro.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Collegamenti vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli delle risorse del [!DNL InDesign] e chiudere [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: aggiungi risorse digitali come riferimenti {#refps}

1. Utilizzare [!DNL Experience Manager] app desktop a cui accedere [!DNL Experience Manager Assets]. Scarica e mostra le risorse sul file system locale. Utilizza il [!UICONTROL Inserisci con collegamento] funzionalità in [!DNL Adobe Photoshop]. Consulta [collocare le risorse nell’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salva in [!DNL Photoshop] file sull&#39;unità montata oppure [caricare](/help/assets/manage-assets.md#uploading-assets) al [!DNL Experience Manager] archivio.
1. Al termine del flusso di lavoro, i riferimenti a [!DNL Experience Manager] le risorse sono elencate nella pagina dettagli risorsa.

   Per visualizzare le risorse a cui si fa riferimento, chiudi [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dettagli risorsa.

1. Le risorse di riferimento contengono anche l’elenco delle risorse da cui fanno riferimento. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli delle risorse e chiudi [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al loro ID documento e ID istanza. Questa funzionalità è disponibile con [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] solo versioni. Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa principale composta, come nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati multipagina: file PDF, file AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] file e [!DNL Adobe InDesign] file — [!DNL Experience Manager] può generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Queste risorse secondarie sono collegate a *principale* e facilitare la visualizzazione multipagina. Per tutti gli altri scopi, le sottoattività sono trattate come attività normali in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per abilitare la generazione di risorse secondarie, effettua le seguenti operazioni:

1. Accedi a [!DNL Experience Manager] come amministratore. Accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona **[!UICONTROL Aggiorna risorsa DAM]** workflow e clic su **[!UICONTROL Modifica]**.
1. Clic **[!UICONTROL Attiva/Disattiva pannello laterale]** e individuare **[!UICONTROL Crea risorsa secondaria]** passaggio. Aggiungi il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettuate una delle seguenti operazioni:

* Nuove risorse: [!UICONTROL Aggiorna risorse DAM] il flusso di lavoro viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse con più pagine.
* Risorse multipagina esistenti: esegui manualmente il [!UICONTROL Aggiorna risorse DAM] flusso di lavoro che segue uno dei passaggi seguenti:

   * Seleziona una risorsa e fai clic su [!UICONTROL Timeline] per aprire il pannello sinistro. In alternativa, utilizza la scelta rapida da tastiera `alt + 3`. Clic [!UICONTROL Avvia flusso di lavoro], seleziona [!UICONTROL Aggiorna risorsa DAM], fai clic su [!UICONTROL Inizio]e fai clic su [!UICONTROL Procedi].
   * Seleziona una risorsa e fai clic su [!UICONTROL Crea] > [!UICONTROL Flusso di lavoro] dalla barra degli strumenti. Dalla finestra di dialogo a comparsa, seleziona [!UICONTROL Aggiorna risorsa DAM] workflow, fai clic su [!UICONTROL Inizio]e fai clic su [!UICONTROL Procedi].

In particolare per i documenti di Microsoft Word, eseguire **[!UICONTROL Analisi documenti Word DAM]** flusso di lavoro. Genera un `cq:Page` componente dal contenuto del documento di Microsoft Word. Le immagini estratte dal documento sono referenziate dal `cq:Page` componente. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

>[!NOTE]
>
>In [!UICONTROL Processo Crea risorsa secondaria - Proprietà passaggio] in [!UICONTROL Argomenti processo], puoi specificare il numero di risorse secondarie che [!DNL Experience Manager] genera. Il valore predefinito è 5. Per generare tutte le risorse secondarie, lascia vuoto il campo. Se il campo ha un valore negativo, non vengono generate risorse secondarie.

## Visualizzare le risorse secondarie {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se vengono generate e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, apri la risorsa multipagina. Nell’area superiore sinistra della pagina, fai clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) e fai clic su **[!UICONTROL Risorse secondarie]** dall&#39;elenco. Quando selezioni **[!UICONTROL Risorse secondarie]** dall&#39;elenco. In alternativa, utilizza la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie di una risorsa multipagina](assets/view_subassets_simulation.gif)

## Visualizzare le pagine di un file con più pagine {#view-pages-of-a-multi-page-file}

È possibile visualizzare un file di più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, utilizzando la funzione Visualizzatore pagina di [!DNL Experience Manager Assets]. Apri una risorsa multipagina e fai clic su **[!UICONTROL Visualizza pagine]** nell&#39;angolo superiore sinistro della pagina. Il Visualizzatore pagine che viene aperto visualizza le pagine della risorsa e i controlli per sfogliare ed eseguire lo zoom di ogni pagina.

![Visualizzare e visualizzare le pagine di una risorsa multipagina](assets/view_multipage_asset_fmr.gif)

Per [!DNL InDesign], è possibile estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante [!DNL InDesign] creazione di file, quindi [!DNL InDesign Server] non è richiesto per l’estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni desktop]** per aprire o visualizzare una risorsa secondaria specifica utilizzando [!DNL Experience Manager] app desktop. Scopri come [configurare le azioni desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se sta usando [!DNL Experience Manager] app desktop.

* **[!UICONTROL Proprietà]** apre il [!UICONTROL Proprietà] della risorsa secondaria specifica.

* **[!UICONTROL Annota]** consente di annotare la risorsa secondaria specifica. Le annotazioni utilizzate su risorse secondarie separate vengono raccolte e visualizzate insieme quando la risorsa principale viene aperta per la visualizzazione.

* **[!UICONTROL Panoramica pagina]** visualizza tutte le risorse secondarie contemporaneamente.

* **[!UICONTROL Timeline]** dalla barra a sinistra dopo aver fatto clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) visualizza il flusso di attività del file.

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere molte risorse su qualsiasi [!DNL Experience Manager] distribuzione. Se generi risorse secondarie durante il caricamento di risorse complesse, aggiungi il passaggio nel flusso di lavoro Aggiorna risorsa DAM. Se generi risorse secondarie on-demand, crea un flusso di lavoro separato per generarle. Un flusso di lavoro dedicato consente di saltare gli altri passaggi del flusso di lavoro Risorsa di aggiornamento DAM e di salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Utilizzare l’app desktop Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurare azioni desktop in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Creazione di oggetti avanzati collegati in Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Posizionare gli elementi grafici in Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)
