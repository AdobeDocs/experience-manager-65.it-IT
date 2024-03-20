---
title: Genera solo rappresentazioni per posizionamento per Adobe InDesign
description: Genera rappresentazioni FPO di risorse nuove ed esistenti utilizzando il flusso di lavoro Experience Manager Assets e ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Genera solo rappresentazioni per posizionamento per Adobe InDesign {#fpo-renditions}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | Questo articolo |

Quando si inseriscono risorse di grandi dimensioni da Experience Manager nei documenti di Adobe InDesign, un creativo professionista deve attendere per un tempo considerevole dopo che [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, l’utente non può utilizzare l’InDesign. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. Adobe consente di inserire temporaneamente copie trasformate di piccole dimensioni nei documenti InDesign. Quando è necessario l’output finale, ad esempio per i flussi di lavoro di stampa e pubblicazione, le risorse originali a risoluzione completa sostituiscono la rappresentazione temporanea in background. Questo aggiornamento asincrono in background accelera il processo di progettazione per aumentare la produttività e non ostacola il processo creativo.

Adobe Experience Manager (AEM) fornisce copie trasformate utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni. Se per una risorsa non è disponibile una rappresentazione FPO, Adobe InDesign utilizza la risorsa originale. Questo meccanismo di fallback assicura che il flusso di lavoro creativo proceda senza interruzioni.

## Approccio per generare rappresentazioni FPO {#approach-to-generate-fpo-renditions}

Experience Manager consente di elaborare con molti metodi le immagini che possono essere utilizzate per generare le rappresentazioni FPO. I due metodi più comuni consistono nell’utilizzare flussi di lavoro di Experience Manager incorporati e nell’utilizzare ImageMagick. Utilizzando questi due metodi, puoi configurare la generazione del rendering delle risorse appena caricate e delle risorse esistenti in Experience Manager.

È possibile utilizzare ImageMagick per elaborare le immagini, anche per generare rappresentazioni FPO. Tali rappresentazioni vengono ricampionate verso il basso, ovvero le dimensioni in pixel della rappresentazione vengono ridotte proporzionalmente se l’immagine originale ha un valore PPI maggiore di 72. Consulta [installare e configurare ImageMagick per l’utilizzo con Experience Manager Assets](best-practices-for-imagemagick.md).

|  | Utilizzo del flusso di lavoro integrato di Experience Manager | Utilizzo del flusso di lavoro ImageMagick | Osservazioni |
|--- |--- |---|--- |
| Per le nuove risorse | Abilita rappresentazione FPO ([aiuto](#generate-renditions-of-new-assets-using-aem-workflow)) | Aggiungere la riga di comando ImageMagick nel flusso di lavoro di Experience Manager ([aiuto](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager esegue il flusso di lavoro Aggiorna risorse DAM per ogni caricamento. |
| Per le risorse esistenti | Abilitare la rappresentazione FPO in un nuovo flusso di lavoro di Experience Manager dedicato ([aiuto](#generate-renditions-of-existing-assets-using-aem-workflow)) | Aggiungere la riga di comando ImageMagick in un nuovo flusso di lavoro Experience Manager dedicato ([aiuto](#generate-renditions-of-existing-assets-using-imagemagick)) | Le rappresentazioni FPO delle risorse esistenti possono essere create su richiesta o in blocco. |

>[!CAUTION]
>
>Crea i flussi di lavoro per generare le rappresentazioni modificando una copia dei flussi di lavoro predefiniti. Impedisce la sovrascrittura delle modifiche quando Experience Manager viene aggiornato, ad esempio installando un nuovo service pack.

## Generare rappresentazioni di nuove risorse utilizzando il flusso di lavoro Experience Manager {#generate-renditions-of-new-assets-using-aem-workflow}

Di seguito è descritta la procedura per configurare il modello di flusso di lavoro Risorsa di aggiornamento DAM per abilitare la generazione di rendering:

1. Clic **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Seleziona **[!UICONTROL Aggiorna risorsa DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Seleziona **[!UICONTROL Elabora miniature]** e fai clic su **[!UICONTROL Configura]**.

1. Clic **[!UICONTROL Rappresentazione FPO]** scheda. Seleziona **[!UICONTROL Abilita creazione rappresentazione FPO]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. Regolare **[!UICONTROL Qualità]** e aggiungere o modificare **[!UICONTROL Elenco formati]** valori come richiesto. Per impostazione predefinita, l&#39;elenco dei tipi MIME per generare la rappresentazione FPO è pjpeg, jpeg, jpg, gif, png, x-png e tiff. Clic **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >La generazione della rappresentazione è supportata per i tipi di file JPEG, GIF, PNG, TIFF, PSD e BMP.

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizza]**.

>[!NOTE]
>
>Le immagini di dimensioni superiori a 1280 pixel su un lato non mantengono le dimensioni pixel nella rappresentazione FPO.

## Generare rappresentazioni di nuove risorse tramite ImageMagick {#generate-renditions-of-new-assets-using-imagemagick}

Ad Experience Manager, il flusso di lavoro Risorsa di aggiornamento DAM viene eseguito quando viene caricata una nuova risorsa. Per utilizzare ImageMagick per elaborare le rappresentazioni delle risorse appena caricate, aggiungi un nuovo comando al modello di flusso di lavoro.

1. Clic **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Seleziona **[!UICONTROL Aggiorna risorsa DAM]** e fai clic su **[!UICONTROL Modifica]**.

1. Clic **[!UICONTROL Attiva/Disattiva pannello laterale]** nell&#39;angolo superiore sinistro e cerca il passaggio della riga di comando.

1. Trascina **[!UICONTROL Riga di comando]** e aggiungerlo prima del **[!UICONTROL Elabora miniature]** passaggio.

1. Seleziona **[!UICONTROL Riga di comando]** e fai clic su **[!UICONTROL Configura]**.

1. Aggiungi le informazioni desiderate come personalizzate **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]**. Ad esempio, rappresentazione FPO (con tecnologia ImageMagick).

1. In **[!UICONTROL Argomenti]** , aggiungi **[!UICONTROL Tipi MIME]** per fornire un elenco dei formati di file a cui si applica il comando.

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. In **[!UICONTROL Argomenti]** , nella scheda **[!UICONTROL Comandi]** , aggiungere un comando ImageMagick appropriato per generare rappresentazioni FPO.

   Di seguito è riportato un comando di esempio che genera copie trasformate FPO in formato JPEG, ricampionate verso il basso a 72 PPI, con un&#39;impostazione di qualità del 10%, e gestisce i file Adobe Photoshop a più livelli appiattendo l&#39;output:

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizza]**.

Per informazioni dettagliate sulle funzionalità della riga di comando di ImageMagick, consulta [https://imagemagick.org](https://imagemagick.org).

## Generare rappresentazioni di risorse esistenti utilizzando il flusso di lavoro Experience Manager {#generate-renditions-of-existing-assets-using-aem-workflow}

Per utilizzare il flusso di lavoro Experience Manager per generare la rappresentazione FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza l’opzione di rappresentazione FPO incorporata.

1. Clic **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Per creare un modello, fate clic su **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**.

1. Aggiungi un valore significativo **[!UICONTROL Titolo]** e **[!UICONTROL Nome]**.

1. Selezionate il modello e fate clic su **[!UICONTROL Modifica]**. Clic **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Apri proprietà]** e quindi selezionare **[!UICONTROL Flusso di lavoro transitorio]**. Ciò migliora scalabilità e prestazioni.

1. Clic **[!UICONTROL Salva]** e **[!UICONTROL Chiudi]**.

1. Clic **[!UICONTROL Attiva/Disattiva pannello laterale]** nell&#39;angolo in alto a sinistra e cerca il passaggio Elabora miniatura.

1. Seleziona **[!UICONTROL Elabora miniature]** e fai clic su **[!UICONTROL Configura]**. Segui le [configurazione per generare il rendering delle nuove risorse tramite il flusso di lavoro Experience Manager](#generate-renditions-of-new-assets-using-aem-workflow).

1. Per attivare le modifiche, fai clic su **[!UICONTROL Sincronizza]**.


## Generare rappresentazioni di risorse esistenti utilizzando ImageMagick {#generate-renditions-of-existing-assets-using-imagemagick}

Per utilizzare le funzionalità di elaborazione ImageMagick per generare una rappresentazione FPO delle risorse esistenti, crea un modello di flusso di lavoro dedicato che utilizza la riga di comando ImageMagick.

1. Seguire i punti da 1 a 3 da [configurazione per generare il rendering delle risorse esistenti tramite il flusso di lavoro Experience Manager](#generate-renditions-of-existing-assets-using-aem-workflow) sezione.

1. Seguire il punto 4 al punto 8 da [configurazione per generare il rendering delle nuove risorse tramite ImageMagick](#generate-renditions-of-new-assets-using-imagemagick) sezione.


## Visualizza rappresentazioni FPO {#view-fpo-renditions}

Al termine del flusso di lavoro, è possibile controllare le rappresentazioni dell&#39;oggetto Criteri di gruppo generate. Nell’interfaccia utente di Experience Manager Assets, fai clic sulla risorsa per aprire un’anteprima di grandi dimensioni. Apri la barra a sinistra e seleziona Rappresentazioni. In alternativa, utilizza la scelta rapida da tastiera `Alt + 3` quando l’anteprima è aperta.

Clic **[!UICONTROL Rendering FPO]** per caricarne l’anteprima. Se necessario, è possibile fare clic con il pulsante destro del mouse sulla copia trasformata e salvarla nel file system.

![rendition_list](assets/rendition_list.png)


## Suggerimenti e limitazioni {#tips-limitations}

* Per utilizzare la configurazione basata su ImageMagick, installare ImageMagick sullo stesso computer di Experience Manager.
* Per generare rappresentazioni FPO di molte risorse o dell’intero archivio, pianifica ed esegui i flussi di lavoro per una durata di traffico ridotto. La generazione di copie trasformate FPO per un numero elevato di risorse è un&#39;attività che richiede molte risorse e i server di Experience Manager devono disporre di potenza di elaborazione e memoria sufficienti.
* Per prestazioni e scalabilità, consulta [Ottimizza ImageMagick](performance-tuning-guidelines.md).
* Per informazioni generiche sulla gestione della riga di comando delle risorse, consulta [gestore della riga di comando per elaborare le risorse](media-handlers.md).
