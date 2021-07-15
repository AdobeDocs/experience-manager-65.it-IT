---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO di risorse nuove ed esistenti utilizzando AEM flusso di lavoro e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Rendering FPO, rappresentazioni
exl-id: null
source-git-commit: dab3bf47fbc59abab2c8a7972653aaece2b4bcdb
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

Quando si inseriscono risorse di grandi dimensioni da AEM nei documenti Adobe InDesign, un creativo professionista deve aspettare un periodo di tempo notevole dopo che [inserisce una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, all’utente è impedito di utilizzare InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. L’Adobe consente di iniziare temporaneamente il posizionamento di rappresentazioni di piccole dimensioni nei documenti InDesign. Quando l’output finale è necessario, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono il rendering temporaneo in background. Questo aggiornamento asincrono in background velocizza il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

AEM fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste rappresentazioni FPO hanno dimensioni file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile un rendering FPO, Adobe InDesign utilizza invece la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

## Approccio per generare rappresentazioni FPO {#approach-to-generate-fpo-renditions}

AEM consente diversi metodi per elaborare le immagini che possono essere utilizzati per generare le rappresentazioni FPO. I due metodi più comuni sono quelli di utilizzare flussi di lavoro AEM incorporati e ImageMagick. Utilizzando questi due metodi, puoi configurare la generazione di rendering delle risorse appena caricate e delle risorse esistenti in AEM.

È possibile utilizzare ImageMagick per elaborare le immagini, anche per generare rappresentazioni FPO. Tali rappresentazioni vengono sottoposte a sottocampionamento, ovvero le dimensioni in pixel del rendering vengono ridotte proporzionalmente se l&#39;immagine originale ha un PPI superiore a 72. Consulta [installare e configurare ImageMagick per l&#39;utilizzo con AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/best-practices-for-imagemagick.html).

|  | Utilizzo di AEM flusso di lavoro integrato | Utilizzo del flusso di lavoro ImageMagick | Osservazioni |
| | |—|— |
| Per le nuove attività | Abilita rendering FPO ([help](#generate-renditions-of-new-assets-using-aem-workflow)) | Aggiungi la riga di comando ImageMagick nel flusso di lavoro AEM ([help](#generate-renditions-of-new-assets-using-imagemagick)) | AEM esegue il flusso di lavoro Aggiorna risorse DAM per ogni caricamento. |
| Attività esistenti | Abilita il rendering FPO in un nuovo flusso di lavoro AEM dedicato ([help](#generate-renditions-of-existing-assets-using-aem-workflow)) | Aggiungi la riga di comando ImageMagick in un nuovo flusso di lavoro AEM dedicato ([help](#generate-renditions-of-existing-assets-using-imagemagick)) | Le rappresentazioni FPO delle risorse esistenti possono essere create on-demand o in massa. |

>[!CAUTION]
>
>Crea i flussi di lavoro per generare rappresentazioni modificando una copia dei flussi di lavoro predefiniti. Impedisce che le modifiche vengano sovrascritte quando AEM viene aggiornato, ad esempio installando un nuovo service pack.

## Generare rappresentazioni di nuove risorse tramite AEM flusso di lavoro {#generate-renditions-of-new-assets-using-aem-workflow}

Di seguito sono riportati i passaggi per configurare il modello di flusso di lavoro Risorsa di aggiornamento DAM per abilitare la generazione del rendering:

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Seleziona il modello **[!UICONTROL Risorsa di aggiornamento DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona il passaggio **[!UICONTROL Elabora miniature]** e fai clic su **[!UICONTROL Configura]**.

1. Fare clic sulla scheda **[!UICONTROL Rendering FPO]**. Selezionare **[!UICONTROL Abilita creazione rendering FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Regolare i valori **[!UICONTROL Quality]** e aggiungere o modificare i valori **[!UICONTROL Format List]** come necessario. Per impostazione predefinita, l’elenco dei tipi MIME per generare il rendering FPO è pjpeg, jpeg, jpg, gif, png, x-png e tiff. Fare clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >La generazione del rendering è supportata per i tipi di file JPEG, GIF, PNG, TIFF, PSD e BMP.

1. Per attivare le modifiche, fare clic su **[!UICONTROL Sincronizza]**.

>[!NOTE]
>
>Le immagini di dimensioni superiori a 1280 pixel su un lato non conservano le dimensioni dei pixel nel rendering FPO.

## Generare rappresentazioni di nuove risorse utilizzando ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

In AEM, il flusso di lavoro Aggiorna risorsa DAM viene eseguito quando viene caricata una nuova risorsa. Per utilizzare ImageMagick per elaborare le rappresentazioni delle risorse appena caricate, aggiungi un nuovo comando al modello di flusso di lavoro.

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Seleziona il modello **[!UICONTROL Risorsa di aggiornamento DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell&#39;angolo superiore sinistro. Cerca il passaggio della riga di comando.

1. Trascina il passaggio **[!UICONTROL Riga di comando]** e aggiungilo prima del passaggio **[!UICONTROL Elabora miniature]** .

1. Seleziona il passaggio **[!UICONTROL Riga di comando]** e fai clic su **[!UICONTROL Configura]**.

1. Aggiungi le informazioni desiderate come personalizzate **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]**. Ad esempio, il rendering FPO (basato su ImageMagick).

1. Nella scheda **[!UICONTROL Argomenti]** , aggiungi **[!UICONTROL Tipi di MIME]** per fornire un elenco di formati di file ai quali si applica il comando.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. Nella scheda **[!UICONTROL Argomenti]**, nella sezione **[!UICONTROL Comandi]**, aggiungi un comando ImageMagick pertinente per generare rappresentazioni FPO.

   Di seguito è riportato un comando di esempio che genera rappresentazioni FPO in formato JPEG, ricampionato verso il basso a 72 PPI, con un’impostazione di qualità del 10%, e gestisce file Adobe Photoshop a più livelli appiattendo l’output:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Per attivare le modifiche, fare clic su **[!UICONTROL Sincronizza]**.

Per informazioni dettagliate sulle funzionalità della riga di comando ImageMagick, vedere https://imagemagick.org.

## Genera rendering delle risorse esistenti tramite AEM flusso di lavoro {#generate-renditions-of-existing-assets-using-aem-workflow}

Per utilizzare AEM flusso di lavoro per generare il rendering FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza l’opzione di rendering FPO integrata.

1. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Per creare un modello, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**. Aggiungi un **[!UICONTROL Titolo]** significativo e un **[!UICONTROL Nome]** significativo.

1. Seleziona il modello e fai clic su **[!UICONTROL Modifica]**. Fare clic su **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Apri proprietà]**. Seleziona **[!UICONTROL Flusso di lavoro transitorio]**. Ciò migliora la scalabilità e le prestazioni. Fai clic su ******[!UICONTROL Salva e chiudi]**.

1. Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell&#39;angolo superiore sinistro. Passaggio della miniatura del processo di ricerca. Trascina il passaggio **[!UICONTROL Elabora miniature]** .

1. Seleziona **[!UICONTROL Elabora miniature]** e fai clic su **[!UICONTROL Configura]**. Segui la [configurazione per generare il rendering delle nuove risorse utilizzando AEM flusso di lavoro](#generate-renditions-of-new-assets-using-aem-workflow). Per attivare le modifiche, fare clic su **[!UICONTROL Sincronizza]**.


## Generare rappresentazioni di risorse esistenti utilizzando ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Per utilizzare le funzionalità di elaborazione ImageMagick per generare il rendering FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza la riga di comando ImageMagick per farlo.

1. Segui i passaggi da 1 a 3 della sezione [configurazione per generare il rendering delle risorse esistenti utilizzando AEM flusso di lavoro](#generate-renditions-of-existing-assets-using-aem-workflow) .

1. Per generare il rendering delle nuove risorse utilizzando la sezione ImageMagick](#generate-renditions-of-new-assets-using-imagemagick), segui i passaggi 4-8 della configurazione [.


## Visualizzare le rappresentazioni FPO {#view-fpo-renditions}

Puoi controllare le rappresentazioni FPO generate al termine del flusso di lavoro. Nell’interfaccia utente di AEM Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona Rappresentazioni . In alternativa, utilizza la scelta rapida da tastiera `Alt + 3` quando l’anteprima è aperta.

Fai clic su **[!UICONTROL Rendering FPO]** per caricare la relativa anteprima. Facoltativamente, puoi fare clic con il pulsante destro del mouse sul rendering e salvarlo nel file system.

![rendition_list](assets/rendition_list.png)


## Suggerimenti e limitazioni {#tips-limitations}

* Per utilizzare la configurazione basata su ImageMagick, installare ImageMagick sullo stesso computer di AEM.
* Per generare rappresentazioni FPO di molte risorse o dell’intero archivio, pianifica ed esegui i flussi di lavoro durante una breve durata del traffico. La generazione di rappresentazioni FPO per un numero elevato di risorse è un’attività ad alta intensità di risorse e i server AEM devono disporre di una potenza di elaborazione e di una memoria sufficienti.
* Per prestazioni e scalabilità, consulta [Ottimizzare ImageMagick](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html).
* Per la gestione generica della riga di comando delle risorse, consulta [gestore della riga di comando per elaborare le risorse](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/media-handlers.html).