---
title: Consente di gestire le risorse video in [!DNL Adobe Experience Manager].
description: Caricate, visualizzate in anteprima, annotate e pubblicate le risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8c481c9a5052ff057ae0857c2ac825cec2b26269
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 7%

---


# Gestire le risorse video {#manage-video-assets}

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scoprite come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. Inoltre, se disponete di una licenza per l’utilizzo [!DNL Dynamic Media], consultate la documentazione [video](/help/assets/video.md)Dynamic Media.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera anteprime per le risorse video con l’estensione MP4. Se il formato della risorsa non è MP4, installate il pacchetto FFmpeg per generare un&#39;anteprima. FFmpeg crea rappresentazioni video di tipo OGG e MP4. Puoi visualizzare l’anteprima delle rappresentazioni nell’interfaccia utente di Risorse.

1. Nella cartella o nelle sottocartelle Risorse digitali, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare la risorsa, fate clic su **[!UICONTROL Crea]** nella barra degli strumenti, quindi scegliete **[!UICONTROL File]**. In alternativa, rilasciatelo direttamente nell’area delle risorse. Per informazioni dettagliate sull’operazione di caricamento, consultate [Caricare le risorse](managing-assets-touch-ui.md#uploading-assets) .
1. Per visualizzare un’anteprima del video nella vista a schede, fate clic sull’opzione **[!UICONTROL Riproduci]** ![riproduzione](assets/do-not-localize/play.png) nella risorsa video. Potete mettere in pausa o riprodurre il video solo nella vista a schede. Le opzioni [!UICONTROL Riproduci] e [!UICONTROL Pausa] non sono disponibili nella vista a elenco.

1. Per visualizzare l&#39;anteprima del video nella pagina dei dettagli della risorsa, fate clic su **[!UICONTROL Modifica]** nella scheda. Il video viene riprodotto nel lettore video nativo del browser. Potete riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

   ![Controlli per la riproduzione video](assets/video-playback-controls.png)

## Configurazione per il caricamento di risorse di dimensioni superiori a 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Per impostazione predefinita, [!DNL Assets] non consente di caricare risorse maggiori di 2 GB a causa di un limite di dimensione file. Tuttavia, potete sovrascrivere questo limite entrando nel CRXDE Lite e creando un nodo sotto la `/apps` directory. Il nodo deve avere lo stesso nome di nodo, la stessa struttura di directory e le stesse proprietà di nodo confrontabili dell&#39;ordine.

Oltre alla [!DNL Assets] configurazione, modificate le seguenti configurazioni per caricare risorse di grandi dimensioni:

* Aumenta l’ora di scadenza del token. Consulta [!UICONTROL servlet] CSRF Granite Adobe nella console Web all’indirizzo `https://[aem_server]:[port]/system/console/configMgr`. Per ulteriori informazioni, vedere [Protezione](/help/sites-developing/csrf-protection.md)CSRF.
* Aumentare la configurazione `receiveTimeout` in Dispatcher. Per ulteriori informazioni, consultate [Experience Manager di configurazione](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)Dispatcher.

>[!NOTE]
>
>L&#39;interfaccia utente [!DNL Experience Manager] classica non ha un limite di dimensione file di 2 GB. Inoltre, il flusso di lavoro end-to-end per i video di grandi dimensioni non è completamente supportato.

Per configurare un limite di dimensione file più elevato, eseguire i seguenti passaggi nella `/apps` directory.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. In CRXDE Lite, andate a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Per visualizzare la finestra della directory, fare clic su `>>`.
1. From the toolbar, click the **[!UICONTROL Overlay Node]**. In alternativa, seleziona **[!UICONTROL Sovrapponi nodo]** dal menu di scelta rapida.
1. In the **[!UICONTROL Overlay Node]** dialog, click **[!UICONTROL OK]**.

   ![Sovrapposizione, nodo](assets/overlay-node-path.png)

1. Aggiorna il browser. Il nodo di sovrapposizione `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` è selezionato.
1. Nella scheda **[!UICONTROL Proprietà]** , immettete il valore appropriato in byte per aumentare il limite delle dimensioni fino alla dimensione desiderata. Ad esempio, per aumentare il limite di dimensione a 30 GB, immettete `{sizeLimit : "32212254720"}` un valore.

1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Salva tutto]**.
1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Nella pagina Bundle [!DNL Adobe Experience Manager] della console [!UICONTROL Web, nella colonna Nome della tabella, individuare e fare clic su] Gestoreprocesso esterno di Adobe flusso di lavoro granito ****.
1. On the [!UICONTROL Adobe Granite Workflow External Process Job Handler] page, set the seconds for both **[!UICONTROL Default Timeout]** and **[!UICONTROL Max Timeout]** fields to `18000` (five hours). Fai clic su **[!UICONTROL Salva]**.
1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli di workflow, seleziona **[!UICONTROL Dynamic Media Encode Video]**, quindi fai clic su **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, fate doppio clic sul componente **[!UICONTROL Dynamic Media Video Service Process]** .
1. Nella finestra di dialogo [!UICONTROL Step Properties (Proprietà passo)], nella scheda **[!UICONTROL Common (Comune)]**, espandi **Impostazioni avanzate**.
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then click **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. Nella parte superiore della pagina, sotto il titolo della pagina [!UICONTROL Dynamic Media Encode Video] , fate clic su **[!UICONTROL Salva]**.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, potete includere le risorse video in una pagina Web come URL o incorporarle direttamente. Per informazioni dettagliate, consultate [pubblicare risorse](/help/assets/publishing-dynamicmedia-assets.md)multimediali dinamiche.

## Annotazione delle risorse video {#annotate-video-assets}

1. Dalla console Risorse, fate clic su [!UICONTROL Modifica] nella scheda della risorsa per visualizzare la pagina dei dettagli della risorsa.
1. Per riprodurre il video, fate clic su [!UICONTROL Anteprima].
1. Per annotare il video, fate clic sul pulsante **[!UICONTROL Annota]** . Un’annotazione viene aggiunta alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, è possibile disegnare sul quadro e inserire un commento con il disegno. I commenti vengono salvati automaticamente.

   ![Disegnare e annotare su un fotogramma video](assets/annotate-video.png)

   Per uscire dalla procedura guidata di annotazione, fate clic su **[!UICONTROL Chiudi]**.

1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 10 secondi del video, inserisci 20 nel campo di testo.

   ![Cercare un&#39;ora in un video per saltare per secondi specificati](assets/seek-in-video.png)

1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fate clic su **[!UICONTROL Elimina]**.

   ![Visualizzare le annotazioni e i dettagli nella timeline](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gestione delle risorse digitali nelle risorse  Experience Manager](/help/assets/managing-assets-touch-ui.md)
>* [Gestire le raccolte in  risorse Experience Manager](/help/assets/managing-collections-touch-ui.md)

