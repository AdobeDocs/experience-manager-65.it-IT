---
title: Gestione di risorse composte con riferimenti e risorse con più pagine in Experience Manager
description: Scoprite come creare riferimenti a risorse AEM da InDesign, Illustrator e Photoshop. La funzione Visualizzatore pagina consente di visualizzare le singole pagine delle risorse secondarie di file con più pagine, ad esempio file PDF, INDD, PPT, PPTX e AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Gestione di risorse composte e multipagina {#managing-compound-assets}

Risorse Adobe Experience Manager (AEM) può identificare se un file caricato contiene riferimenti a risorse già presenti nell’archivio. Questa funzione è disponibile solo per i formati di file supportati. Se la risorsa caricata contiene riferimenti a risorse AEM, viene creato un collegamento bidirezionale tra le risorse caricate e quelle a cui viene fatto riferimento.

Oltre ad eliminare la ridondanza, il riferimento alle risorse AEM nelle applicazioni Adobe Creative Cloud migliora la collaborazione e aumenta l&#39;efficienza e la produttività degli utenti.

Risorse AEM supporta il riferimento bidirezionale. Potete trovare le risorse di riferimento nella pagina dei dettagli delle risorse del file caricato. Inoltre, potete visualizzare i file di riferimento per le risorse AEM nella pagina dei dettagli delle risorse della risorsa di riferimento.

I riferimenti vengono risolti in base a percorso, ID documento e ID istanza delle risorse a cui viene fatto riferimento.

## Aggiunta di Risorse AEM come riferimenti in Adobe Illustrator {#refai}

Potete fare riferimento a risorse AEM esistenti direttamente da un file Adobe Illustrator.

1. Utilizzando l’app [desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)AEM, installa l’archivio Risorse AEM come unità nel computer locale. Nell’unità montata, andate alla posizione della risorsa a cui desiderate fare riferimento.
1. Trascinate la risorsa dall’unità montata al file Illustrator.

1. Salvate il file Illustrator nell’unità montata o [caricatelo](/help/assets/managing-assets-touch-ui.md#uploading-assets) nell’archivio di AEM.

1. Al termine del flusso di lavoro, passate alla pagina dei dettagli della risorsa. I riferimenti alle risorse AEM esistenti sono elencati in **[!UICONTROL Dipendenze]** nella colonna **[!UICONTROL Riferimenti]** .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Le risorse di riferimento visualizzate in **[!UICONTROL Dipendenze]** possono essere utilizzate anche da file diversi da quello corrente. Per visualizzare un elenco dei file di riferimento per una risorsa, fai clic sulla risorsa in **[!UICONTROL Dipendenze]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Fare clic su **[!UICONTROL Visualizza proprietà]** dalla barra degli strumenti. Nella pagina [!UICONTROL Proprietà] , l’elenco dei file che fanno riferimento alla risorsa corrente viene visualizzato nella colonna **[!UICONTROL Riferimenti]** della scheda **[!UICONTROL Base]** .

   ![visualizzare i riferimenti di Experience Manager Assets nella colonna Riferimenti nei dettagli delle risorse](assets/asset-references.png)

   *Figura: Riferimenti alle risorse nei dettagli delle risorse*

## Aggiunta di risorse AEM come riferimenti in Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Per fare riferimento a risorse AEM da un file InDesign, trascinate le risorse AEM nel file InDesign oppure esportate il file InDesign come file ZIP.

Le risorse di riferimento esistono già in AEM Assets. Potete estrarre le risorse secondarie [configurando InDesign Server](/help/assets/indesign.md). Le risorse incorporate in un file InDesign vengono estratte come risorse secondarie.

>[!NOTE]
>
>Se il server InDesign è proxy, i file InDesign hanno la loro anteprima incorporata nei metadati XMP. In questo caso, l&#39;estrazione delle miniature non è obbligatoria in modo esplicito. Tuttavia, se il server InDesign non è proxy, le miniature devono essere estratte in modo esplicito per i file InDesign.

### Creare riferimenti trascinando le risorse {#create-references-by-dragging-aem-assets}

Questa procedura è simile a [Aggiungi risorse AEM come riferimenti in Adobe Illustrator](#refai).

### Creare riferimenti alle risorse esportando un file ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Per creare un nuovo flusso di lavoro, effettua i passaggi descritti in [Creazione di modelli](/help/sites-developing/workflows-models.md) di flusso di lavoro.
1. Utilizzate la funzione Pacchetto di Adobe InDesign per esportare il documento.
Adobe InDesign può esportare come pacchetto un documento e le risorse collegate. In questo caso, la cartella esportata contiene una cartella Links che contiene risorse secondarie nel file InDesign.
1. Create un file ZIP e caricatelo nell’archivio AEM.
1. Avviate il `Unarchiver` flusso di lavoro.
1. Al termine del flusso di lavoro, i riferimenti nella cartella Links vengono automaticamente indicati come risorse secondarie. Per visualizzare un elenco delle risorse di riferimento, andate alla pagina dei dettagli delle risorse di InDesign e chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

## Aggiungere risorse AEM come riferimenti in Adobe Photoshop {#refps}

1. Utilizzando un client WebDav, caricate Risorse AEM come unità.
1. Per creare riferimenti a risorse AEM in un file Photoshop, passa alle risorse corrispondenti nell’unità montata utilizzando la funzione Inserisci collegamento di Photoshop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Salvate il file in Photoshop nell’unità montata o [caricatelo](/help/assets/managing-assets-touch-ui.md#uploading-assets) nell’archivio AEM.
1. Al termine del flusso di lavoro, i riferimenti alle risorse AEM esistenti sono elencati nella pagina dei dettagli della risorsa.

   Per visualizzare le risorse a cui si fa riferimento, chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector) nella pagina dei dettagli della risorsa.

1. Le risorse a cui viene fatto riferimento contengono anche l’elenco delle risorse a cui fanno riferimento. Per visualizzare un elenco delle risorse di riferimento, andate alla pagina dei dettagli delle risorse e chiudete la [Barra](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>È inoltre possibile fare riferimento alle risorse all’interno delle risorse composte in base al relativo ID documento e all’ID istanza. Questa funzionalità è disponibile solo nelle versioni Adobe Illustrator e Adobe Photoshop. Per altri, il riferimento viene fatto sulla base del percorso relativo delle risorse collegate nella risorsa composta principale, come già fatto nelle versioni precedenti di AEM.

## Creare risorse secondarie {#generate-subassets}

Per le risorse supportate con formati con più pagine — File PDF, file AI, file Microsoft PowerPoint e Apple Keynote e file Adobe InDesign AEM può generare risorse secondarie corrispondenti a ogni singola pagina della risorsa originale. Tali risorse secondarie sono collegate alla risorsa *principale* e facilitano la visualizzazione di più pagine. Per tutti gli altri scopi, le risorse secondarie vengono trattate come risorse normali in AEM.

La generazione di risorse secondarie è disabilitata per impostazione predefinita. Per attivare la generazione di risorse secondarie, effettuate le seguenti operazioni:

1. Accedi a Experience Manager come amministratore. Accedere **[!UICONTROL a Strumenti > Flusso di lavoro > Modelli]**.
1. Selezionate il flusso di lavoro Aggiorna risorsa **** DAM e fate clic su **[!UICONTROL Modifica]**.
1. Fate clic su **[!UICONTROL Attiva pannello]** laterale e individuate il passaggio **[!UICONTROL Crea risorsa]** secondaria. Aggiungete il passaggio al flusso di lavoro. Fate clic su **[!UICONTROL Sincronizza]**.

Per generare le risorse secondarie, effettuate una delle seguenti operazioni:

* Nuove risorse: Il flusso di lavoro Risorse [!UICONTROL aggiornamento] DAM viene eseguito su qualsiasi nuova risorsa caricata in AEM. Le risorse secondarie vengono generate automaticamente per le nuove risorse multipagina.
* Risorse multipagina esistenti: Esegui manualmente il flusso di lavoro [!UICONTROL DAM Update Assets] seguendo una delle seguenti procedure:

   * Selezionate una risorsa e fate clic su [!UICONTROL Timeline] per aprire il pannello a sinistra. In alternativa, utilizzare la scelta rapida da tastiera `alt + 3`. Fate clic su [!UICONTROL Avvia flusso di lavoro], selezionate [!UICONTROL DAM Update Asset](Aggiorna risorsa [!UICONTROL DAM), fate clic su]Avvia [!UICONTROL e fate clic su]Procedi.
   * Selezionate una risorsa e fate clic su [!UICONTROL Crea > Flusso di lavoro] nella barra degli strumenti. Dalla finestra di dialogo a comparsa, selezionate Flusso di lavoro di aggiornamento risorse  DAM, fate clic su [!UICONTROL Avvia]e quindi su [!UICONTROL Procedi].

In modo specifico per i documenti di Microsoft Word, eseguite il flusso di lavoro **[!UICONTROL di analisi dei documenti]** di Word DAM. Viene generato un `cq:Page` componente dal contenuto del documento di Microsoft Word. Il `cq:Page` componente fa riferimento alle immagini estratte dal documento. Queste immagini vengono estratte anche se la generazione di risorse secondarie è disabilitata.

## View subassets {#viewing-subassets}

Le risorse secondarie vengono visualizzate solo se sono state generate delle risorse secondarie e sono disponibili per la risorsa multipagina selezionata. Per visualizzare le risorse secondarie generate, aprite la risorsa con più pagine. Nell’area in alto a sinistra della pagina, fate clic sull’icona ![della barra a](assets/do-not-localize/aem_leftrail_contentonly.png) sinistra e fate clic su Risorse **** secondarie dall’elenco. Quando selezionate **[!UICONTROL Risorse]** secondarie dall’elenco. In alternativa, utilizzare la scelta rapida da tastiera `alt + 5`.

![Visualizzare le risorse secondarie per una risorsa con più pagine](assets/view_subassets_simulation.gif)

## Visualizzare le pagine di un file con più pagine {#view-pages-of-a-multi-page-file}

Potete visualizzare un file con più pagine, ad esempio PDF, INDD, PPT, PPTX e AI, mediante la funzione Visualizzatore pagina di Risorse AEM. Aprite una risorsa con più pagine e fate clic su **[!UICONTROL Visualizza pagine]** nell’angolo in alto a sinistra della pagina. Il visualizzatore pagina che apre mostra le pagine della risorsa e i controlli per scorrere e ingrandire ciascuna pagina.

![Visualizzare e visualizzare le pagine di una risorsa con più pagine](assets/view_multipage_asset_fmr.gif)

Per InDesign, potete estrarre le pagine utilizzando il server InDesign. Se le anteprime delle pagine vengono salvate durante la creazione di file InDesign, InDesign Server non è richiesto per l&#39;estrazione della pagina.

Le seguenti opzioni sono disponibili nella barra degli strumenti, nella barra a sinistra e nei controlli Visualizzatore pagina:

* **[!UICONTROL Azioni]** desktop per aprire o visualizzare una risorsa secondaria specifica mediante l’app desktop AEM. Scoprite come [configurare le azioni](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) desktop se utilizzate l&#39;app desktop AEM.

* **[!UICONTROL L’opzione Proprietà]** consente di aprire la pagina [!UICONTROL Proprietà] della risorsa secondaria specifica.

* **[!UICONTROL L’opzione Annota]** consente di inserire note sulla risorsa secondaria specifica. Le annotazioni utilizzate in risorse secondarie separate vengono raccolte e visualizzate insieme all’apertura della risorsa principale per la visualizzazione.

* **[!UICONTROL L’opzione Panoramica]** pagina consente di visualizzare tutte le risorse secondarie contemporaneamente.

* **[!UICONTROL L&#39;opzione Timeline]** dalla barra a sinistra dopo aver fatto clic sull&#39;icona ![della barra a](assets/do-not-localize/aem_leftrail_contentonly.png) sinistra mostra il flusso di attività per il file.
