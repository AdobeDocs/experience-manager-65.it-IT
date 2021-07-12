---
title: FFmpeg per Communities
seo-title: FFmpeg per Communities
description: Come installare e configurare FFmpeg per Communities
seo-description: Come installare e configurare FFmpeg per Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---

# FFmpeg per Communities {#ffmpeg-for-communities}

## Panoramica {#overview}

FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installato, viene utilizzato per la corretta transcodifica di [risorse video](../../help/sites-authoring/default-components-foundation.md#video) e per la funzione di abilitazione di AEM Communities.

FFmpeg viene utilizzato nell’ambiente di authoring per ottenere i metadati per le risorse di abilitazione caricate e generare una miniatura da visualizzare quando si elenca la risorsa di abilitazione.

## Installazione di FFmpeg {#installing-ffmpeg}

FFmpeg deve essere installato sui server che ospitano l&#39;istanza AEM *author* .

1. Vai a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Scarica la versione più recente di FFmpeg per il tuo ambiente specifico (Macintosh, Windows o Linux).

   * È importante mantenere aggiornato FFmpeg a causa di vulnerabilità di sicurezza nelle versioni precedenti.

1. Installa FFmpeg seguendo le istruzioni per il sistema operativo.

1. Assicurati che l&#39;eseguibile FFmpeg sia impostato nel percorso del sistema.

   Dovresti essere in grado di eseguire FFmpeg da qualsiasi directory del sistema.

   * Esempio, `ffmpeg -version`.

## Configurare il servizio di transcodifica FFmpeg {#configure-ffmpeg-transcoding-service}

Per impostazione predefinita, quando FFmpeg è installato, vengono configurate più rappresentazioni (transcodings) in base alla definizione del flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] .

Poiché le transcodings sono ad alta intensità di CPU, si consiglia di modificare l’elenco delle rappresentazioni di destinazione. Nella maggior parte dei casi, la transcodifica non è necessaria.

Per modificare il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] e, in questo esempio, per disattivare la transcodifica:

* Accedi all’istanza di authoring con privilegi amministrativi.
* Dalla navigazione globale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
* Individua **[!UICONTROL Risorsa di aggiornamento DAM]**.
* Fai doppio clic per aprire il flusso di lavoro per la modifica nell’interfaccia classica.

   Posizione risultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Fai doppio clic sul passaggio **[!UICONTROL Transcodifica FFmpeg]** per accedere alla finestra di dialogo Proprietà passaggio .
* Nella scheda **[!UICONTROL Processo]** :

   * **[!UICONTROL Argomenti]**: Cancella tutte le voci per disabilitare la transcodifica Valori predefiniti:  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Selezionare **[!UICONTROL OK]** per chiudere la finestra di dialogo `Step Properties`.

* Seleziona **[!UICONTROL Salva]** per salvare il flusso di lavoro `DAM Update Asset`.
