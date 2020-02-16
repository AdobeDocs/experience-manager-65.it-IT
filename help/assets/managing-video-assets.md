---
title: Gestire le risorse video
description: Scoprite come caricare, visualizzare in anteprima, annotare e pubblicare risorse video.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gestire le risorse video {#manage-video-assets}

Scopri come gestire e modificare le risorse video in Risorse Adobe Experience Manager (AEM). Inoltre, se disponete di una licenza per l’utilizzo di contenuti multimediali dinamici, consultate la documentazione [video sui file multimediali](/help/assets/video.md)dinamici.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

Risorse Adobe Experience Manager genera anteprime per risorse video con estensione MP4. Se il formato della risorsa non è MP4, installate il pacchetto FFmpeg per generare un&#39;anteprima. FFmpeg crea rappresentazioni video di tipo OGG e MP4. Puoi visualizzare l’anteprima di queste rappresentazioni nell’interfaccia utente di Risorse AEM.

1. Nella cartella o nelle sottocartelle Risorse digitali, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare la risorsa, toccate o fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti, quindi scegliete **[!UICONTROL File]**. In alternativa, rilasciatelo direttamente nell’area delle risorse. Per informazioni dettagliate sull’operazione di caricamento, consultate [Caricamento delle risorse](managing-assets-touch-ui.md#uploading-assets) .
1. Per visualizzare un’anteprima del video nella vista a schede, toccate il pulsante **[!UICONTROL Riproduci]** sulla risorsa video.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   Potete mettere in pausa o riprodurre il video solo nella vista a schede. I pulsanti [!UICONTROL Riproduci] e [!UICONTROL Pausa] non sono disponibili nella vista a elenco.

1. Per visualizzare l&#39;anteprima del video nella pagina dei dettagli della risorsa, toccate o fate clic sull&#39;icona **[!UICONTROL Modifica]** sulla scheda.

   Il video viene riprodotto nel lettore video nativo del browser. Potete riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## Configurazione per il caricamento di risorse di dimensioni superiori a 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Per impostazione predefinita, Experience Manager Assets non consente di caricare risorse maggiori di 2 GB a causa di un limite di dimensione file. Tuttavia, potete sovrascrivere questo limite entrando in CRXDE Lite e creando un nodo sotto la `/apps` directory. Il nodo deve avere lo stesso nome di nodo, la stessa struttura di directory e le stesse proprietà di nodo confrontabili dell&#39;ordine.

Oltre alla configurazione Experience Manager Assets, puoi modificare le seguenti configurazioni per caricare risorse di grandi dimensioni:

* Aumenta l’ora di scadenza del token. Consulta Servlet [!UICONTROL CSRF] Adobe Granite nella console Web all’indirizzo `https://[aem_server]:[port]/system/console/configMgr`. Per ulteriori informazioni, vedere [Protezione](/help/sites-developing/csrf-protection.md)CSRF.
* Aumentare la configurazione `receiveTimeout` del dispatcher. Per ulteriori informazioni, consulta Configurazione [del dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)Experience Manager.

>[!NOTE]
>
>L&#39;interfaccia utente di AEM Classic non presenta un limite di dimensione file di 2 GB. Inoltre, il flusso di lavoro end-to-end per video di grandi dimensioni non è completamente supportato.

Per configurare un limite di dimensione file più elevato, eseguire i seguenti passaggi nella `/apps` directory.

1. In AEM, toccate **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. In CRXDE Lite, passare a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Per visualizzare la finestra della directory, toccate l&#39; `>>` icona.
1. Dalla barra degli strumenti, toccate il nodo **** Sovrapposizione. In alternativa, selezionate **[!UICONTROL Overlay Node]** dal menu di scelta rapida.
1. Nella finestra di dialogo Nodo **** sovrapposizione, toccate **[!UICONTROL OK]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. Aggiorna il browser. Il nodo di sovrapposizione `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` è selezionato.
1. Nella scheda **[!UICONTROL Proprietà]** , immettete il valore appropriato in byte per aumentare il limite delle dimensioni fino alla dimensione desiderata. Ad esempio, per aumentare il limite di dimensione a 30 GB, immettete `{sizeLimit : "32212254720"}` un valore.

1. Dalla barra degli strumenti, toccate **[!UICONTROL Salva tutto]**.
1. In AEM, toccate **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.
1. Nella pagina Bundle della console Web di Adobe Experience Manager, nella colonna Nome della tabella, individua e tocca il gestore **[!UICONTROL processi esterni di]** Adobe Granite Workflow.
1. Nella pagina Gestione processi esterni flusso di lavoro di Adobe Granite, impostate i secondi per i campi Timeout **** predefinito e Timeout **** massimo su `18000` (cinque ore).
1. Toccate **[!UICONTROL Salva]**.
1. In AEM, toccate **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli di workflow, seleziona **[!UICONTROL Dynamic Media Encode Video]**, quindi tocca **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, toccate due volte il componente **[!UICONTROL Dynamic Media Video Service Process]** .
1. Nella finestra di dialogo Proprietà  passo, nella scheda **[!UICONTROL Comune]** , espandere **Impostazioni** avanzate.
1. Nel campo **[!UICONTROL Timeout]** , specificate un valore di `18000`, quindi toccate **[!UICONTROL OK]** per tornare alla pagina del flusso di lavoro Codifica video **[!UICONTROL elemento multimediale]** dinamico.
1. Nella parte superiore della pagina, sotto il titolo della pagina Codifica video elemento multimediale dinamico, toccate **[!UICONTROL Salva]**.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, le risorse video sono disponibili per l’inclusione in una pagina Web mediante un URL o l’incorporazione in una pagina Web. Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).

## Annotazione delle risorse video {#annotate-video-assets}

1. Dalla console Risorse, tocca o fai clic sull’icona [!UICONTROL Modifica] sulla scheda della risorsa per visualizzare la pagina dei dettagli della risorsa.
1. Per riprodurre il video, toccate o fate clic sull’icona [!UICONTROL Anteprima] .
1. Per annotare il video, fate clic sul pulsante **[!UICONTROL Annota]** . Un’annotazione viene aggiunta al particolare punto temporale (fotogramma) del video. Durante l&#39;annotazione, è possibile disegnare sul quadro e inserire un commento con il disegno. I commenti vengono salvati automaticamente.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   Per uscire dalla procedura guidata di annotazione, fate clic su **[!UICONTROL Chiudi]**.

1. Cercate un punto specifico del video, specificate il tempo in secondi nel campo di **testo** e fate clic su **Salta**. Ad esempio, per saltare i primi 10 secondi di video, immettete 20 nel campo di testo.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fate clic su **[!UICONTROL Elimina]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
