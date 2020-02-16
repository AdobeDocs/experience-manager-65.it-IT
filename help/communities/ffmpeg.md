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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# FFmpeg for Communities {#ffmpeg-for-communities}

## Panoramica {#overview}

FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installata, viene utilizzata per la corretta transcodifica delle risorse [](../../help/sites-authoring/default-components-foundation.md#video) video e per la funzione di abilitazione di AEM Communities.

FFmpeg viene utilizzato nell’ambiente di authoring per ottenere i metadati per le risorse di abilitazione caricate e generare una miniatura da visualizzare quando si elenca le risorse di abilitazione.

## Installazione di FFmpeg {#installing-ffmpeg}

FFmpeg deve essere installato sui server in cui sono ospitate le istanze di *creazione* di AEM.

1. Vai a [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. Scaricate la versione più recente di FFmpeg per il vostro ambiente specifico (Macintosh, Windows o Linux)

   * è importante mantenere FFmpeg aggiornato a causa di vulnerabilità di sicurezza nelle versioni precedenti

1. Installate FFmpeg seguendo le istruzioni per il sistema operativo.

1. Accertatevi che l&#39;eseguibile FFmpeg sia impostato nel percorso di sistema.

   Dovrebbe essere possibile eseguire FFmpeg da qualsiasi directory del sistema.

   * for example, `ffmpeg -version`

## Configurare il servizio di transcodifica FFmpeg {#configure-ffmpeg-transcoding-service}

Per impostazione predefinita, quando è installato FFmpeg, vengono configurate più rappresentazioni (transcodifiche) in base alla definizione del flusso di lavoro di aggiornamento DAM.

Poiché le transcodifiche richiedono molta CPU, si consiglia di modificare l&#39;elenco delle rappresentazioni di destinazione. Nella maggior parte dei casi, la transcodifica non è necessaria.

Per modificare il flusso di lavoro Aggiorna risorsa DAM e, in questo esempio, disattivare la transcodifica:

* Accesso all’istanza di creazione con privilegi amministrativi
* Dalla navigazione globale: **[!UICONTROL Strumenti > Workflow > Modelli]**
* Individua risorsa di aggiornamento **[!UICONTROL DAM]**
* Fate doppio clic per aprire il flusso di lavoro per la modifica nell’interfaccia classica

   Posizione risultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Fate doppio clic sul passaggio di transcodifica **[!UICONTROL FFmpeg]** per accedere alla finestra di dialogo Proprietà passaggio
* Nella scheda **[!UICONTROL Processo]** :

   * **[!UICONTROL Articoli]**: Cancella tutte le voci per disabilitare la transcodifica di valori predefiniti: `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Selezionare **[!UICONTROL OK]** per chiudere la `Step Properties` finestra di dialogo

* Selezionate **[!UICONTROL Salva]** per salvare il `DAM Update Asset` flusso di lavoro

   (angolo superiore sinistro)

