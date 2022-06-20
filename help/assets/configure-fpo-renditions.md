---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO di risorse nuove ed esistenti utilizzando il flusso di lavoro Experience Manager Assets e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Questo articolo |

Quando si inseriscono risorse di grandi dimensioni dall’Experience Manager ai documenti Adobe InDesign, un professionista deve aspettare per un periodo di tempo considerevole dopo che hanno [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, all’utente è impedito di utilizzare InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. L’Adobe consente di iniziare temporaneamente il posizionamento di rappresentazioni di piccole dimensioni nei documenti InDesign. Quando l’output finale è necessario, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono il rendering temporaneo in background. Questo aggiornamento asincrono in background velocizza il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

Adobe Experience Manager (AEM) fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste rappresentazioni FPO hanno dimensioni file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile un rendering FPO, Adobe InDesign utilizza invece la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

## Approccio per generare rappresentazioni FPO {#approach-to-generate-fpo-renditions}

L’Experience Manager consente di elaborare diversi metodi per le immagini che possono essere utilizzate per generare le rappresentazioni FPO. I due metodi più comuni consistono nell’utilizzo di flussi di lavoro di Experience Manager incorporati e nell’utilizzo di ImageMagick. Utilizzando questi due metodi, puoi configurare la generazione di rendering delle risorse appena caricate e delle risorse esistenti in Experience Manager.

È possibile utilizzare ImageMagick per elaborare le immagini, anche per generare rappresentazioni FPO. Tali rappresentazioni vengono sottoposte a sottocampionamento, ovvero le dimensioni in pixel del rendering vengono ridotte proporzionalmente se l&#39;immagine originale ha un PPI superiore a 72. Vedi [installa e configura ImageMagick per lavorare con Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Utilizzo del flusso di lavoro integrato di Experience Manager | Utilizzo del flusso di lavoro ImageMagick | Osservazioni |
|--- |--- |---|--- |
| Per nuove risorse | Abilita rendering FPO ([help](#generate-renditions-of-new-assets-using-aem-workflow)) | Aggiungi la riga di comando ImageMagick nel flusso di lavoro di Experience Manager ([help](#generate-renditions-of-new-assets-using-imagemagick)) | In Experience Manager viene eseguito il flusso di lavoro Aggiorna risorse DAM per ogni caricamento. |
| Per le risorse esistenti | Abilita il rendering FPO in un nuovo flusso di lavoro dedicato di Experience Manager ([help](#generate-renditions-of-existing-assets-using-aem-workflow)) | Aggiungi la riga di comando ImageMagick in un nuovo flusso di lavoro dedicato di Experience Manager ([help](#generate-renditions-of-existing-assets-using-imagemagick)) | Le rappresentazioni FPO delle risorse esistenti possono essere create on-demand o in blocco. |

>[!CAUTION]
>
>Crea i flussi di lavoro per generare rappresentazioni modificando una copia dei flussi di lavoro predefiniti. Impedisce la sovrascrittura delle modifiche quando Experience Manager viene aggiornato, ad esempio installando un nuovo service pack.

## Generare rappresentazioni di nuove risorse tramite il flusso di lavoro Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

Di seguito sono riportati i passaggi per configurare il modello di flusso di lavoro Risorsa di aggiornamento DAM per abilitare la generazione del rendering:

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Seleziona **[!UICONTROL Risorsa di aggiornamento DAM]** modello e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona **[!UICONTROL Miniature del processo]** fai clic su **[!UICONTROL Configura]**.

1. Fai clic su **[!UICONTROL Rendering FPO]** scheda . Seleziona **[!UICONTROL Abilita creazione rendering FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Regolare la **[!UICONTROL Qualità]** e aggiungere o modificare **[!UICONTROL Elenco formati]** i valori richiesti. Per impostazione predefinita, l’elenco dei tipi MIME per generare il rendering FPO è pjpeg, jpeg, jpg, gif, png, x-png e tiff. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >La generazione del rendering è supportata per i tipi di file JPEG, GIF, PNG, TIFF, PSD e BMP.

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizzazione]**.

>[!NOTE]
>
>Le immagini di dimensioni superiori a 1280 pixel su un lato non conservano le dimensioni dei pixel nel rendering FPO.

## Generare rappresentazioni di nuove risorse utilizzando ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

Ad Experience Manager, il flusso di lavoro Aggiorna risorsa DAM viene eseguito quando viene caricata una nuova risorsa. Per utilizzare ImageMagick per elaborare le rappresentazioni delle risorse appena caricate, aggiungi un nuovo comando al modello di flusso di lavoro.

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Seleziona **[!UICONTROL Risorsa di aggiornamento DAM]** modello e fai clic su **[!UICONTROL Modifica]**.

1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell&#39;angolo in alto a sinistra e cerca il passaggio della riga di comando.

1. Trascina **[!UICONTROL Riga di comando]** aggiungilo prima della **[!UICONTROL Miniature del processo]** passo.

1. Seleziona **[!UICONTROL Riga di comando]** fai clic su **[!UICONTROL Configura]**.

1. Aggiungi le informazioni desiderate come personalizzate **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]**. Ad esempio, il rendering FPO (basato su ImageMagick).

1. In **[!UICONTROL Argomenti]** scheda , aggiungi pertinente **[!UICONTROL Tipi di mime]** fornire un elenco dei formati di file su cui si applica il comando.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. In **[!UICONTROL Argomenti]** nella scheda **[!UICONTROL Comandi]** aggiungi un comando ImageMagick pertinente per generare rappresentazioni FPO.

   Di seguito è riportato un comando di esempio che genera rappresentazioni FPO in formato JPEG, ricampionate verso il basso fino a 72 PPI, con un’impostazione di qualità del 10% e gestisce file Adobe Photoshop a più livelli appiattendo l’output:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizzazione]**.

Per informazioni dettagliate sulle funzionalità della riga di comando ImageMagick, consulta [https://imagemagick.org](https://imagemagick.org).

## Genera rendering delle risorse esistenti tramite il flusso di lavoro di Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Per utilizzare un flusso di lavoro di Experience Manager per generare il rendering FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza l’opzione di rendering FPO integrata.

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Per creare un modello, fate clic su **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**.

1. Aggiungi un significato **[!UICONTROL Titolo]** e **[!UICONTROL Nome]**.

1. Seleziona il modello e fai clic su **[!UICONTROL Modifica]**. Fai clic su **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Apri proprietà]**, quindi seleziona **[!UICONTROL Flusso di lavoro transitorio]**. Ciò migliora la scalabilità e le prestazioni.

1. Fai clic su ******[!UICONTROL Salva e chiudi]**.

1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra e cerca il passaggio Elabora miniature .

1. Seleziona **[!UICONTROL Miniature del processo]** e fai clic su **[!UICONTROL Configura]**. Segui [configurazione per generare il rendering delle nuove risorse utilizzando il flusso di lavoro Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizzazione]**.


## Generare rappresentazioni di risorse esistenti utilizzando ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Per utilizzare le funzionalità di elaborazione ImageMagick per generare il rendering FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza la riga di comando ImageMagick per farlo.

1. Segui i punti da 1 a 3 da [configurazione per generare il rendering delle risorse esistenti utilizzando il flusso di lavoro Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow) sezione .

1. Segui il passaggio 4 al passaggio 8 da [configurazione per generare il rendering delle nuove risorse utilizzando ImageMagick](#generate-renditions-of-new-assets-using-imagemagick) sezione .


## Visualizzare le rappresentazioni FPO {#view-fpo-renditions}

Puoi controllare le rappresentazioni FPO generate al termine del flusso di lavoro. Nell’interfaccia utente di Experience Manager Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona Rappresentazioni . In alternativa, utilizza la scelta rapida da tastiera `Alt + 3` quando l&#39;anteprima è aperta.

Fai clic su **[!UICONTROL Rendering FPO]** per caricare la relativa anteprima. Facoltativamente, puoi fare clic con il pulsante destro del mouse sul rendering e salvarlo nel file system.

![rendition_list](assets/rendition_list.png)


## Suggerimenti e limitazioni {#tips-limitations}

* Per utilizzare la configurazione basata su ImageMagick, installare ImageMagick sullo stesso computer di Experience Manager.
* Per generare rappresentazioni FPO di molte risorse o dell’intero archivio, pianifica ed esegui i flussi di lavoro durante una breve durata del traffico. La generazione di rappresentazioni FPO per un numero elevato di risorse è un’attività ad alta intensità di risorse e i server di Experience Manager devono disporre di una potenza di elaborazione e di una memoria sufficienti.
* Per prestazioni e scalabilità, consulta [ImmagineMagick con ottimizzazione](performance-tuning-guidelines.md).
* Per la gestione generica della riga di comando delle risorse, consulta [gestore della riga di comando per elaborare le risorse](media-handlers.md).
