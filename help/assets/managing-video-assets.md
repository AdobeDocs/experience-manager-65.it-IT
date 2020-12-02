---
title: Gestire le risorse video
description: Caricate, visualizzate in anteprima, annotate e pubblicate le risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 7%

---


# Gestire le risorse video {#manage-video-assets}

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, è possibile tramite l&#39;integrazione [!DNL Dynamic Media].

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera anteprime per le risorse video con l’estensione MP4. Se il formato della risorsa non è MP4, installate il pacchetto FFmpeg per generare un&#39;anteprima. FFmpeg crea rappresentazioni video di tipo OGG e MP4. Potete visualizzare l&#39;anteprima delle rappresentazioni nell&#39;interfaccia utente [!DNL Assets].

1. Nella cartella o nelle sottocartelle delle risorse digitali, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare la risorsa, fate clic su **[!UICONTROL Crea]** nella barra degli strumenti e scegliete **[!UICONTROL File]**. In alternativa, trascinare un file nell’interfaccia utente. Per informazioni, consultate [caricare risorse](manage-assets.md#uploading-assets).
1. Per visualizzare l&#39;anteprima di un video nella vista a schede, fate clic sull&#39;opzione **[!UICONTROL Riproduci]** ![Riproduci](assets/do-not-localize/play.png) nella risorsa video. Potete mettere in pausa o riprodurre il video solo nella vista a schede. Le opzioni [!UICONTROL Riproduci] e [!UICONTROL Pausa] non sono disponibili nella vista a elenco.

1. Per visualizzare l&#39;anteprima del video nella pagina dei dettagli della risorsa, fate clic su **[!UICONTROL Modifica]** nella scheda. Il video viene riprodotto nel lettore video nativo del browser. Potete riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

   ![Controlli per la riproduzione video](assets/video-playback-controls.png)

## Configurazione per il caricamento di risorse superiori a 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Per impostazione predefinita, [!DNL Assets] non consente di caricare risorse maggiori di 2 GB a causa di un limite di dimensione file. Tuttavia, potete sovrascrivere questo limite entrando nel CRXDE Lite e creando un nodo sotto la directory `/apps`. Il nodo deve avere lo stesso nome di nodo, la stessa struttura di directory e le stesse proprietà di nodo confrontabili dell&#39;ordine.

Oltre alla configurazione [!DNL Assets], modificate le seguenti configurazioni per caricare risorse di grandi dimensioni:

* Aumenta l’ora di scadenza del token. Vedere [!UICONTROL  Adobe Granite CSRF Servlet] nella console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`. Per ulteriori informazioni, vedere [Protezione CSRF](/help/sites-developing/csrf-protection.md).
* Aumentare la `receiveTimeout` nella configurazione del dispatcher. Per ulteriori informazioni, vedere [ configurazione del dispatcher di Experienci Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>L&#39;interfaccia utente classica [!DNL Experience Manager] non presenta un limite di dimensione file di 2 GB. Inoltre, il flusso di lavoro end-to-end per i video di grandi dimensioni non è completamente supportato.

Per configurare un limite di dimensione file più elevato, eseguire i seguenti passaggi nella directory `/apps`.

1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. In CRXDE Lite , passare a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Per visualizzare la finestra della directory, fare clic su `>>`.
1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Overlay Node]**. In alternativa, seleziona **[!UICONTROL Sovrapponi nodo]** dal menu di scelta rapida.
1. Nella finestra di dialogo **[!UICONTROL Overlay Node]**, fare clic su **[!UICONTROL OK]**.

   ![Sovrapposizione, nodo](assets/overlay-node-path.png)

1. Aggiorna il browser. Il nodo di sovrapposizione `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` è selezionato.
1. Nella scheda **[!UICONTROL Proprietà]**, immettere il valore appropriato in byte per aumentare il limite di dimensione alla dimensione desiderata. Ad esempio, per aumentare il limite di dimensione a 30 GB, immettete il valore `32212254720`.

1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Salva tutto]**.
1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Nella pagina [!DNL Adobe Experience Manager] [!UICONTROL Pacchetti console Web], nella colonna Nome della tabella individuare e fare clic su **[!UICONTROL Adobe Gestore processo esterno flusso di lavoro granito]**.
1. Nella pagina [!UICONTROL  Adobe Granite Workflow External Process Handler], impostare i secondi per i campi **[!UICONTROL Default Timeout]** e **[!UICONTROL Max Timeout]** su `18000` (cinque ore). Fai clic su **[!UICONTROL Salva]**.
1. In [!DNL Experience Manager], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli flusso di lavoro, selezionare **[!UICONTROL Codifica video multimediale dinamica]**, quindi fare clic su **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, fate doppio clic sul componente **[!UICONTROL Processo di servizio video multimediale dinamico]**.
1. Nella finestra di dialogo [!UICONTROL Step Properties (Proprietà passo)], nella scheda **[!UICONTROL Common (Comune)]**, espandi **Impostazioni avanzate**.
1. Nel campo **[!UICONTROL Timeout]**, specificate un valore di `18000`, quindi fate clic su **[!UICONTROL OK]** per tornare alla pagina del flusso di lavoro **[!UICONTROL Codifica video elemento multimediale dinamico]**.
1. Nella parte superiore della pagina, sotto il titolo della pagina [!UICONTROL Codifica video elemento multimediale dinamico], fare clic su **[!UICONTROL Salva]**.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, potete includere le risorse video in una pagina Web come URL o incorporarle direttamente. Per informazioni dettagliate, consultate [pubblicare risorse per file multimediali dinamici](/help/assets/publishing-dynamicmedia-assets.md).

## Annotazione delle risorse video {#annotate-video-assets}

1. Dalla console [!DNL Assets], selezionate **[!UICONTROL Modifica]** nella scheda delle risorse per visualizzare la pagina dei dettagli delle risorse.
1. Per riprodurre il video, fare clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fare clic su **[!UICONTROL Annota]**. Un’annotazione viene aggiunta alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, è possibile disegnare sul quadro e inserire un commento con il disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata di annotazione, fare clic su **[!UICONTROL Chiudi]**.

   ![Disegnare e annotare su un fotogramma video](assets/annotate-video.png)

1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.

   ![Cercare un&#39;ora in un video per saltare per secondi specificati](assets/seek-in-video.png)

1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l&#39;annotazione dalla cronologia, fare clic su **[!UICONTROL Elimina]**.

   ![Visualizzare le annotazioni e i dettagli nella timeline](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gestione delle risorse digitali nelle risorse  Experience Manager](/help/assets/manage-assets.md)
>* [Gestire le raccolte in  risorse Experience Manager](/help/assets/manage-collections.md)
>* [Documentazione](/help/assets/video.md) video per contenuti multimediali dinamici.

