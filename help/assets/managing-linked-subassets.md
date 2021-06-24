---
title: Gestire le risorse composte con riferimenti e pagine multiple
description: Scopri come creare riferimenti a risorse digitali da [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. Utilizza la funzione Visualizzatore pagina per visualizzare le singole pagine delle risorse secondarie di file multipagina, come file PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Gestione risorse
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: a564f158cf1040ef43cb9f5dde9f7cb22769587f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Gestire risorse composte e multipagina {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] può identificare se un file caricato contiene riferimenti a risorse già esistenti nell’archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a risorse [!DNL Experience Manager], viene creato un collegamento bidirezionale tra le risorse caricate e quelle a cui si fa riferimento.

Oltre a eliminare la ridondanza, il riferimento alle risorse nelle applicazioni [!DNL Adobe Creative Cloud] migliora la collaborazione e aumenta l&#39;efficienza e la produttività degli utenti.

[!DNL Experience Manager Assets] supporta i riferimenti bidirezionali. Puoi trovare le risorse a cui si fa riferimento nella pagina dei dettagli della risorsa del file caricato. Inoltre, puoi visualizzare i file che fanno riferimento alla risorsa nella pagina dei dettagli della risorsa a cui si fa riferimento.

I riferimenti vengono risolti in base al percorso, all’ID documento e all’ID istanza delle risorse a cui si fa riferimento.

## [!DNL Adobe Illustrator]: Aggiungere risorse digitali come riferimenti {#refai}

Puoi fare riferimento a risorse digitali esistenti all’interno di un file [!DNL Adobe Illustrator] .

1. Utilizzando l’ [[!DNL Experience Manager] app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html), recupera le risorse digitali dal file system locale. Passa alla posizione del file system della risorsa a cui desideri fare riferimento.
1. Trascina la risorsa dalla cartella locale al file [!DNL Illustrator] .

1. Salva il file [!DNL Illustrator] nell&#39;unità montata o [carica](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].

1. Al termine del flusso di lavoro, passa alla pagina dei dettagli della risorsa. I riferimenti alle risorse digitali esistenti sono elencati in **[!UICONTROL Dipendenze]** nella colonna **[!UICONTROL Riferimenti]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dipendenze]** possono essere referenziate anche da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento per una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fai clic su **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti. Nella pagina [!UICONTROL Proprietà] , l’elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato sotto la colonna **[!UICONTROL Riferimenti]** nella scheda **[!UICONTROL Base]** .

   ![visualizzare i riferimenti di Risorse Experience Manager nella colonna Riferimenti nei dettagli della risorsa](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse.*

## [!DNL Adobe InDesign]: Aggiungere risorse digitali come riferimenti {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento alle risorse digitali da un file [!DNL InDesign], trascina le risorse nel file [!DNL InDesign] o esporta il file [!DNL InDesign] come archivio ZIP.

Le risorse di riferimento esistono già in [!DNL Experience Manager Assets]. È possibile estrarre le risorse secondarie configurando [InDesign Server](indesign.md). Le risorse incorporate in un file [!DNL InDesign] vengono estratte come risorse secondarie.

>[!NOTE]
>
>Se il file [!DNL InDesign Server] è proxy, i file [!DNL InDesign] presentano l’anteprima incorporata nei metadati XMP. In questo caso, l’estrazione delle miniature non è esplicitamente richiesta. Tuttavia, se il file [!DNL InDesign Server] non è proxy, le miniature devono essere estratte in modo esplicito per i file [!DNL InDesign].

Quando un file INDD viene caricato, i riferimenti vengono recuperati eseguendo una query sulle risorse con proprietà `xmpMM:InstanceID` e `xmpMM:DocumentID` nell’archivio.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [aggiungi risorse digitali come riferimenti in Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Esegui i passaggi descritti in [Creare modelli di flusso di lavoro](/help/sites-developing/workflows-models.md) per creare un nuovo flusso di lavoro.
1. Utilizza la [funzionalità Pacchetto](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) di [!DNL Adobe InDesign] per esportare il documento. [!DNL Adobe InDesign] può esportare un documento e le risorse collegate come pacchetto. In questo caso, la cartella esportata contiene una cartella `Links` contenente risorse secondarie nel file [!DNL InDesign]. La cartella `Links` è presente nella stessa cartella del file INDD.
1. Crea un file ZIP e caricalo nell&#39;archivio [!DNL Experience Manager].
1. Avvia il flusso di lavoro `Unarchiver`.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Collegamenti vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse indicate, passa alla pagina dei dettagli della risorsa [!DNL InDesign] e chiudi la barra [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Aggiungere risorse digitali come riferimenti {#refps}

1. Utilizza l’ app desktop [!DNL Experience Manager] per accedere a [!DNL Experience Manager Assets]. Scarica e visualizza le risorse sul file system locale. Utilizza la funzionalità [!UICONTROL Inserisci collegato] in [!DNL Adobe Photoshop]. Consulta [inserire risorse nell’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Salva il file [!DNL Photoshop] nell&#39;unità montata o [carica](/help/assets/manage-assets.md#uploading-assets) nell&#39;archivio [!DNL Experience Manager].
1. Al termine del flusso di lavoro, i riferimenti alle risorse [!DNL Experience Manager] esistenti sono elencati nella pagina dei dettagli della risorsa.

   Per visualizzare le risorse a cui si fa riferimento, chiudi la barra [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli delle risorse.

1. Le risorse a cui si fa riferimento contengono anche l’elenco delle risorse a cui fanno riferimento. Per visualizzare un elenco delle risorse a cui si fa riferimento, passa alla pagina dei dettagli della risorsa e chiudi la barra [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al relativo ID documento e ID istanza. Questa funzionalità è disponibile solo nelle versioni [!DNL Adobe Illustrator] e [!DNL Adobe Photoshop] . Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa composta principale, come fatto nelle versioni precedenti di [!DNL Experience Manager].

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati multipagina: file PDF, file AI, file [!DNL Microsoft PowerPoint] e [!DNL Apple Keynote] e file [!DNL Adobe InDesign] [!DNL Experience Manager] possono generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Queste risorse secondarie sono collegate alla risorsa *principale* e facilitano la visualizzazione multipagina. Per tutti gli altri scopi, le attività secondarie vengono trattate come attività normali in [!DNL Experience Manager].

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per abilitare la generazione di risorse secondarie, procedi come segue:

1. Accedi a [!DNL Experience Manager] come amministratore. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Seleziona il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** e fai clic su **[!UICONTROL Modifica]**.
1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** e individua il passaggio **[!UICONTROL Crea sottorisorsa]** . Aggiungi il passaggio al flusso di lavoro. Fai clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettua una delle seguenti operazioni:

* Nuove risorse: Il flusso di lavoro [!UICONTROL Aggiorna risorse DAM] viene eseguito su qualsiasi nuova risorsa caricata in [!DNL Experience Manager]. Le risorse secondarie vengono generate automaticamente per le nuove risorse multipagina.
* Risorse multipagina esistenti: Esegui manualmente il flusso di lavoro [!UICONTROL Aggiorna risorse DAM] seguendo uno dei passaggi seguenti:

   * Seleziona una risorsa e fai clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizza la scelta rapida da tastiera `alt + 3`. Fai clic su [!UICONTROL Avvia flusso di lavoro], seleziona [!UICONTROL Aggiorna risorsa DAM], fai clic su [!UICONTROL Avvia] e fai clic su [!UICONTROL Procedi].
   * Seleziona una risorsa e fai clic su [!UICONTROL Crea] > [!UICONTROL Flusso di lavoro] nella barra degli strumenti. Dalla finestra di dialogo a comparsa, seleziona [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro, fai clic su [!UICONTROL Avvia] e fai clic su [!UICONTROL Procedi].

Specificamente per i documenti Microsoft Word, eseguire il flusso di lavoro **[!UICONTROL DAM Parse Word Documents]**. Viene generato un componente `cq:Page` dal contenuto del documento di Microsoft Word. Le immagini estratte dal documento sono referenziate dal componente `cq:Page` . Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

## Visualizzare le risorse secondarie {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se sono generate e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, apri la risorsa multipagina. Nell&#39;area in alto a sinistra della pagina, fai clic su ![Opzione per aprire la barra a sinistra](assets/do-not-localize/aem_leftrail_contentonly.png) e fai clic su **[!UICONTROL Risorse secondarie]** dall&#39;elenco. Quando selezioni **[!UICONTROL Risorse secondarie]** dall’elenco. In alternativa, utilizza la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie di una risorsa multipagina](assets/view_subassets_simulation.gif)

## Visualizzare pagine di un file multipagina {#view-pages-of-a-multi-page-file}

È possibile visualizzare un file con più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, utilizzando la funzione Visualizzatore pagina di [!DNL Experience Manager Assets]. Apri una risorsa multipagina e fai clic su **[!UICONTROL Visualizza pagine]** nell’angolo in alto a sinistra della pagina. Il visualizzatore pagina visualizzato mostra le pagine della risorsa e i controlli per sfogliare e ingrandire ciascuna pagina.

![Visualizzare e visualizzare le pagine di una risorsa multipagina](assets/view_multipage_asset_fmr.gif)

Per [!DNL InDesign] è possibile estrarre le pagine utilizzando [!DNL InDesign Server]. Se le anteprime delle pagine vengono salvate durante la creazione di file [!DNL InDesign], [!DNL InDesign Server] non è necessario per l’estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni desktop]** per aprire o visualizzare una risorsa secondaria specifica utilizzando l’app  [!DNL Experience Manager] desktop. Scopri come [configurare le azioni desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) se utilizzi l’app desktop [!DNL Experience Manager].

* **** L’opzione Proprietà apre la pagina   Proprietà della risorsa secondaria specifica.

* **[!UICONTROL L’opzione]** Annota consente di annotare la risorsa secondaria specifica. Le annotazioni utilizzate in risorse secondarie separate vengono raccolte e visualizzate insieme all’apertura della risorsa principale per la visualizzazione.

* **[!UICONTROL L’opzione]** Panoramica pagina visualizza tutte le risorse secondarie simultaneamente.

* **** L’opzione Timeline dalla barra a sinistra dopo aver fatto clic su  ![Opzione per aprire ](assets/do-not-localize/aem_leftrail_contentonly.png) la barra a sinistra mostra il flusso di attività per il file.

## Best practice e limitazioni {#best-practice-limitation-tips}

* La generazione di risorse secondarie può richiedere un utilizzo intensivo delle risorse in qualsiasi implementazione [!DNL Experience Manager]. Se generi risorse secondarie quando vengono caricate risorse complesse, aggiungi il passaggio nel flusso di lavoro Aggiorna risorsa DAM . Se generi risorse secondarie su richiesta, crea un flusso di lavoro separato per generare le risorse secondarie. Un flusso di lavoro dedicato ti consente di saltare gli altri passaggi del flusso di lavoro Aggiorna risorsa DAM e salvare le risorse di calcolo.

>[!MORELIKETHIS]
>
>* [Utilizzare l’app desktop Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configurare azioni desktop in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Creare oggetti avanzati collegati in Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Inserire elementi grafici in Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

