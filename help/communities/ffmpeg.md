---
title: FFmpeg per community
description: Come installare e configurare FFmpeg per Communities
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 1%
---
# FFmpeg per community {#ffmpeg-for-communities}

## Panoramica {#overview}

FFmpeg è una soluzione per la conversione e lo streaming di audio e video e, se installata, viene utilizzata per la trascodifica corretta di [risorse video](../../help/sites-authoring/default-components-foundation.md#video).

## Installazione di FFmpeg {#installing-ffmpeg}

FFmpeg deve essere installato sui server che ospitano le *istanze Autore* di AEM.

1. Vai a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Scarica la versione più recente di FFmpeg per l’ambiente specifico (Macintosh, Windows o Linux).

   * È importante mantenere FFmpeg aggiornato a causa di vulnerabilità di sicurezza nelle versioni precedenti.

1. Installare FFmpeg seguendo le istruzioni per il sistema operativo.

1. Verificare che l&#39;eseguibile FFmpeg sia impostato nel percorso di sistema.

   Dovresti essere in grado di eseguire FFmpeg da qualsiasi directory del sistema.

   * Ad esempio, `ffmpeg -version`.

## Configura servizio di trascodifica FFmpeg {#configure-ffmpeg-transcoding-service}

Per impostazione predefinita, quando è installato FFmpeg, vengono configurate più rappresentazioni (transcodifiche) in base alla definizione del flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].

Poiché le trascodifiche sono molto complesse per CPU, si consiglia di modificare l’elenco delle rappresentazioni di destinazione. Nella maggior parte dei casi, la transcodifica non è necessaria.

Per modificare il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] e, in questo esempio, disattivare la transcodifica:

* Accedi all’istanza di authoring con privilegi di amministratore.
* Dalla navigazione globale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
* Individua **[!UICONTROL Risorsa di aggiornamento DAM]**.
* Fai doppio clic per aprire il flusso di lavoro per la modifica nell’interfaccia classica.

  Percorso risultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Fai doppio clic sul passaggio **[!UICONTROL Transcodifica FFmpeg]** per accedere alla finestra di dialogo Proprietà passaggio.
* Nella scheda **[!UICONTROL Processo]**:

  * **[!UICONTROL Argomenti]**: cancella tutte le voci per disabilitare la trascodifica. Valori predefiniti: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Selezionare **[!UICONTROL OK]** per chiudere la finestra di dialogo `Step Properties`.

* Seleziona **[!UICONTROL Salva]** per salvare il flusso di lavoro `DAM Update Asset`.
