---
title: Gestire le risorse composte con riferimenti e pagine multiple
description: Scopri come creare riferimenti a risorse digitali da [!DNL Adobe InDesign], [!DNL Adobe Illustrator]e [!DNL Adobe Photoshop]. Utilizza la funzione Visualizzatore pagina per visualizzare le singole pagine delle risorse secondarie di file multipagina quali file PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Gestire risorse composte e multipagina {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già esistenti nell’archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a [!DNL Experience Manager] risorse, viene creato un collegamento bidirezionale tra le risorse caricate e a cui si fa riferimento.

Oltre a eliminare la ridondanza, il riferimento alle risorse in [!DNL Adobe Creative Cloud] le applicazioni migliorano la collaborazione e aumentano l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta i riferimenti bidirezionali. Puoi trovare le risorse a cui si fa riferimento nella pagina dei dettagli della risorsa del file caricato. Inoltre, puoi visualizzare i file che fanno riferimento alla risorsa nella pagina dei dettagli della risorsa a cui si fa riferimento.

I riferimenti vengono risolti in base al percorso, all’ID documento e all’ID istanza delle risorse a cui si fa riferimento.

## [!DNL Adobe Illustrator]: Aggiungere risorse digitali come riferimenti {#refai}

Puoi fare riferimento a risorse digitali esistenti da un [!DNL Adobe Illustrator] file.

1. Utilizzo [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recupera le risorse digitali nel file system locale. Passa alla posizione del file system della risorsa a cui desideri fare riferimento.
1. Trascina la risorsa dalla cartella locale al [!DNL Illustrator] file.

1. Salva il [!DNL Illustrator] all&#39;unità montata, oppure [caricare](/help/assets/manage-assets.md#uploading-assets) al [!DNL Experience Manager] archivio.

1. Al termine del flusso di lavoro, passa alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** in **[!UICONTROL Riferimenti]** colonna.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dipendenze]** può essere fatto riferimento anche a file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento di una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fai clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti. In [!UICONTROL Proprietà] nella pagina viene visualizzato l’elenco dei file che fanno riferimento alla risorsa corrente **[!UICONTROL Riferimenti]** nella colonna **[!UICONTROL Base]** scheda .

   ![visualizzare i riferimenti di Experience Manager Assets nella colonna Riferimenti nei dettagli della risorsa](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse.*

## [!DNL Adobe InDesign]: Aggiungere risorse digitali come riferimenti {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento a risorse digitali da un [!DNL InDesign] trascinate le risorse nel file [!DNL InDesign] file o esportazione [!DNL InDesign] come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. Puoi estrarre le risorse secondarie per [configurazione di InDesign Server](indesign.md). Risorse incorporate in un [!DNL InDesign] vengono estratti come risorse secondarie.

>[!NOTE]
>
>Se la [!DNL InDesign Server] è proxy, [!DNL InDesign] i file presentano l’anteprima incorporata nei metadati XMP. In questo caso, l’estrazione delle miniature non è esplicitamente richiesta. Tuttavia, se [!DNL InDesign Server] non è proxy, le miniature devono essere estratte in modo esplicito per [!DNL InDesign] file.

Quando un file INDD viene caricato, i riferimenti vengono recuperati eseguendo una query sulle risorse che hanno `xmpMM:InstanceID` e `xmpMM:DocumentID` nella directory archivio.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [aggiungere risorse digitali come riferimenti in Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Esegui i passaggi descritti in [Creare modelli di flusso di lavoro](/help/sites-developing/workflows-models.md) per creare un nuovo flusso di lavoro.
1. Utilizza la [Funzione pacchetto](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) di [!DNL Adobe InDesign] per esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come pacchetto. In questo caso, la cartella esportata contiene un `Links` cartella contenente risorse secondarie nel [!DNL InDesign] file. La `Links` cartella presente nella stessa cartella del file INDD.
1. Crea un file ZIP e caricalo su [!DNL Experience Manager] archivio.
1. Avvia la `Unarchiver` workflow.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Collegamenti vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli della risorsa [!DNL InDesign] e chiudere [Ferrovia](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Aggiungere risorse digitali come riferimenti {#refps}

1. Utilizzo [!DNL Experience Manager] app desktop a cui accedere [!DNL Experience Manager Assets]. Scarica e visualizza le risorse sul file system locale. Utilizza il [!UICONTROL Inserisci collegato] funzionalità in [!DNL Adobe Photoshop]. Vedi [inserire risorse nell’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salva in [!DNL Photoshop] file sull&#39;unità montata o [caricare](/help/assets/manage-assets.md#uploading-assets) al [!DNL Experience Manager] archivio.
1. Al termine del flusso di lavoro, i riferimenti a [!DNL Experience Manager] le risorse sono elencate nella pagina dei dettagli della risorsa.

   Per visualizzare le risorse a cui si fa riferimento, chiudi la [Ferrovia](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli della risorsa.

1. Le risorse a cui si fa riferimento contengono anche l’elenco delle risorse a cui fanno riferimento. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli della risorsa e chiudi la [Ferrovia](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al relativo ID documento e ID istanza. Questa funzionalità è disponibile con [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] solo versioni. Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa composta principale, come fatto nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati a più pagine: file PDF, file AI, [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] file e [!DNL Adobe InDesign] file — [!DNL Experience Manager] può generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Queste risorse secondarie sono collegate al *parent* e facilita la visualizzazione su più pagine. Per tutti gli altri scopi, le attività secondarie sono trattate come attività normali in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per abilitare la generazione di risorse secondarie, procedi come segue:

1. Accedi a [!DNL Experience Manager] come amministratore. Accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona **[!UICONTROL Risorsa di aggiornamento DAM]** workflow e fai clic su **[!UICONTROL Modifica]**.
1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** e individua le **[!UICONTROL Crea risorsa secondaria]** passo. Aggiungi il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettua una delle seguenti operazioni:

* Nuove risorse: La [!UICONTROL Aggiorna risorse DAM] viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse multipagina.
* Risorse multipagina esistenti: Esegui manualmente il [!UICONTROL Aggiorna risorse DAM] flusso di lavoro seguendo uno dei passaggi seguenti:

   * Seleziona una risorsa e fai clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizza la scelta rapida da tastiera `alt + 3`. Fai clic su [!UICONTROL Avvia flusso di lavoro], seleziona [!UICONTROL Risorsa di aggiornamento DAM], fai clic su [!UICONTROL Inizio]e fai clic su [!UICONTROL Procedi].
   * Seleziona una risorsa e fai clic su [!UICONTROL Crea] > [!UICONTROL Flusso di lavoro] dalla barra degli strumenti. Dalla finestra di dialogo a comparsa, seleziona [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro, fai clic su [!UICONTROL Inizio]e fai clic su [!UICONTROL Procedi].

Specificamente per i documenti Microsoft Word, eseguire il **[!UICONTROL Documenti Word analisi DAM]** workflow. Genera un `cq:Page` dal contenuto del documento di Microsoft Word. Le immagini estratte dal documento sono referenziate dal `cq:Page` componente. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

>[!NOTE]
>
>In [!UICONTROL Crea processo risorse secondarie - Proprietà passaggio] in [!UICONTROL Argomenti del processo], puoi specificare il numero di risorse secondarie [!DNL Experience Manager] genera. Il valore predefinito è 5. Per generare tutte le risorse secondarie, lascia vuoto il campo . Se il campo è negativo, non vengono generate risorse secondarie.

## Visualizzare le risorse secondarie {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se sono generate e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, apri la risorsa multipagina. Nell’area in alto a sinistra della pagina, fai clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) e fai clic su **[!UICONTROL Risorse secondarie]** dall&#39;elenco. Quando selezioni **[!UICONTROL Risorse secondarie]** dall&#39;elenco. In alternativa, utilizza la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie di una risorsa multipagina](assets/view_subassets_simulation.gif)

## Visualizzare pagine di un file multipagina {#view-pages-of-a-multi-page-file}

È possibile visualizzare un file con più pagine, ad esempio file PDF, INDD, PPT, PPTX e AI, utilizzando la funzione Visualizzatore pagina di [!DNL Experience Manager Assets]. Apri una risorsa multipagina e fai clic su **[!UICONTROL Visualizza pagine]** dall’angolo in alto a sinistra della pagina. Il visualizzatore pagina visualizzato mostra le pagine della risorsa e i controlli per sfogliare e ingrandire ciascuna pagina.

![Visualizzare e visualizzare le pagine di una risorsa multipagina](assets/view_multipage_asset_fmr.gif)

Per [!DNL InDesign], puoi estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante [!DNL InDesign] creazione di file, quindi [!DNL InDesign Server] non è necessario per l’estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni desktop]** per aprire o visualizzare una risorsa secondaria specifica utilizzando [!DNL Experience Manager] app desktop. Scopri come [configurare le azioni desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se utilizzi [!DNL Experience Manager] app desktop.

* **[!UICONTROL Proprietà]** apre la [!UICONTROL Proprietà] della risorsa secondaria specifica.

* **[!UICONTROL Annota]** consente di annotare la risorsa secondaria specifica. Le annotazioni utilizzate in risorse secondarie separate vengono raccolte e visualizzate insieme all’apertura della risorsa principale per la visualizzazione.

* **[!UICONTROL Panoramica della pagina]** visualizza tutte le risorse secondarie simultaneamente.

* **[!UICONTROL Timeline]** dalla barra a sinistra dopo aver fatto clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) visualizza il flusso di attività per il file .

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere un utilizzo intensivo delle risorse [!DNL Experience Manager] distribuzione. Se generi risorse secondarie quando vengono caricate risorse complesse, aggiungi il passaggio nel flusso di lavoro Aggiorna risorsa DAM . Se generi risorse secondarie su richiesta, crea un flusso di lavoro separato per generare le risorse secondarie. Un flusso di lavoro dedicato ti consente di saltare gli altri passaggi del flusso di lavoro Aggiorna risorsa DAM e salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Utilizzare l’app desktop Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurare azioni desktop in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Creare oggetti avanzati collegati in Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserire elementi grafici in Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

