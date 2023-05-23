---
title: FFmpeg per community
seo-title: FFmpeg for Communities
description: Come installare e configurare FFmpeg per Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# FFmpeg per community {#ffmpeg-for-communities}

## Panoramica {#overview}

FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installata, viene utilizzata per la corretta trascodifica di [risorse video](../../help/sites-authoring/default-components-foundation.md#video).

## Installazione di FFmpeg {#installing-ffmpeg}

FFmpeg deve essere installato sui server che ospitano l’AEM *autore* istanze.

1. Vai a [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Scarica la versione più recente di FFmpeg per l’ambiente specifico (Macintosh, Windows o Linux).

   * È importante mantenere FFmpeg aggiornato a causa di vulnerabilità di sicurezza nelle versioni precedenti.

1. Installare FFmpeg seguendo le istruzioni per il sistema operativo.

1. Verificare che l&#39;eseguibile FFmpeg sia impostato nel percorso di sistema.

   Dovresti essere in grado di eseguire FFmpeg da qualsiasi directory del sistema.

   * Esempio: `ffmpeg -version`.

## Configura servizio di trascodifica FFmpeg {#configure-ffmpeg-transcoding-service}

Per impostazione predefinita, quando è installato FFmpeg, vengono configurate (transcodifiche) più rappresentazioni in base a [!UICONTROL Aggiorna risorsa DAM] definizione del flusso di lavoro.

Poiché le trascodifiche richiedono un uso intensivo della CPU, si consiglia di modificare l’elenco delle rappresentazioni di destinazione. Nella maggior parte dei casi, la transcodifica non è necessaria.

Per modificare [!UICONTROL Aggiorna risorsa DAM] e, in questo esempio, per disattivare la transcodifica:

* Accedi all’istanza di authoring con privilegi di amministratore.
* Dalla navigazione globale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
* Individua **[!UICONTROL Aggiorna risorsa DAM]**.
* Fai doppio clic per aprire il flusso di lavoro per la modifica nell’interfaccia classica.

   Posizione risultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Fai doppio clic su **[!UICONTROL Transcodifica FFmpeg]** per accedere alla finestra di dialogo Proprietà passaggio.
* Sotto **[!UICONTROL Processo]** scheda:

   * **[!UICONTROL Argomenti]**: cancella tutte le voci per disabilitare la transcodifica. Valori predefiniti: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Seleziona **[!UICONTROL OK]** per chiudere `Step Properties` .

* Seleziona **[!UICONTROL Salva]** per salvare `DAM Update Asset` flusso di lavoro.
