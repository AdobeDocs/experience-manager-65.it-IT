---
title: FFmpeg for Communities
seo-title: FFmpeg for Communities
description: Come installare e configurare FFmpeg for Communities
seo-description: Come installare e configurare FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: 299c4cb377c65e49b94383704a906fdd0bb38d06
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---


# FFmpeg for Communities {#ffmpeg-for-communities}

## Panoramica {#overview}

FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installato, viene utilizzato per la corretta transcodifica di [risorse video](../../help/sites-authoring/default-components-foundation.md#video) e per la funzione di abilitazione di AEM Communities.

FFmpeg viene utilizzato nell’ambiente di authoring per ottenere i metadati per le risorse di abilitazione caricate e generare una miniatura da visualizzare quando si elenca le risorse di abilitazione.

## Installazione di FFmpeg {#installing-ffmpeg}

FFmpeg deve essere installato sui server che ospitano le istanze *author* AEM.

1. Andate a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Scaricate la versione più recente di FFmpeg per il vostro ambiente specifico (Macintosh, Windows o Linux).

   * È importante tenere FFmpeg aggiornato a causa di vulnerabilità di sicurezza nelle versioni precedenti.

1. Installate FFmpeg seguendo le istruzioni per il sistema operativo.

1. Accertatevi che l&#39;eseguibile di FFmpeg sia impostato nel percorso di sistema.

   Dovrebbe essere possibile eseguire FFmpeg da qualsiasi directory del sistema.

   * Esempio, `ffmpeg -version`.

## Configurare il servizio di transcodifica FFmpeg {#configure-ffmpeg-transcoding-service}

Per impostazione predefinita, quando FFmpeg è installato, vengono configurate più rappresentazioni (transcodifiche) in base alla definizione del flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].

Poiché le transcodifiche richiedono molta CPU, si consiglia di modificare l&#39;elenco delle rappresentazioni di destinazione. Nella maggior parte dei casi, la transcodifica non è necessaria.

Per modificare il flusso di lavoro [!UICONTROL DAM Update Asset] e, in questo esempio, disattivare la transcodifica:

* Effettuate l’accesso all’istanza di creazione con privilegi amministrativi.
* Dalla navigazione globale, passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
* Individuare **[!UICONTROL DAM Update Asset]**.
* Fate doppio clic per aprire il flusso di lavoro per la modifica nell’interfaccia classica.

   Posizione risultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Fare doppio clic sul passaggio **[!UICONTROL Transcodifica FFmpeg]** per accedere alla finestra di dialogo Proprietà passaggio.
* Nella scheda **[!UICONTROL Processo]**:

   * **[!UICONTROL Articoli]**: Cancella tutte le voci per disabilitare la transcodifica di valori predefiniti:  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![chlimage_1-372](assets/chlimage_1-372.png)

* Selezionare **[!UICONTROL OK]** per chiudere la finestra di dialogo `Step Properties`.

* Selezionare **[!UICONTROL Salva]** per salvare il flusso di lavoro `DAM Update Asset`.



