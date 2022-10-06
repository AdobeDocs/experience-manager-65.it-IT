---
title: Rappresentazioni video
description: Rappresentazioni video
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Rappresentazioni video {#video-renditions}

Adobe Experience Manager Assets genera rappresentazioni video per risorse video di vari formati, inclusi OGG, FLV e così via.

Experience Manager Assets supporta le rappresentazioni statiche e dinamiche (rappresentazioni con codifica DM) per le risorse multimediali.

Le rappresentazioni statiche vengono generate in modo nativo utilizzando FFMPEG (installato e disponibile nel percorso di sistema) e memorizzate nell’archivio dei contenuti.

Le rappresentazioni con codifica DM vengono memorizzate nel server proxy e distribuite in fase di runtime.

Experience Manager Assets supporta la riproduzione di queste rappresentazioni sul lato client.

Per visualizzare le rappresentazioni di una particolare risorsa video, apri la relativa pagina delle risorse e seleziona l’icona Navigazione globale . Quindi, scegli **[!UICONTROL Rendering]** dall&#39;elenco.

![chlimage_1-478](assets/chlimage_1-478.png)

L’elenco delle rappresentazioni video viene visualizzato in **[!UICONTROL Rendering]** pannello.

![chlimage_1-479](assets/chlimage_1-479.png)

Per configurare il server proxy per le rappresentazioni con codifica DM, [configurare i servizi Dynamic Media Cloud](config-dynamic.md).

Per generare rappresentazioni video con i parametri desiderati, [creare un profilo video corrispondente](video-profiles.md).

Dopo aver configurato il server proxy e creato i profili video, puoi includere questo predefinito video in un profilo di elaborazione e applicare il profilo di elaborazione a una cartella.

>[!NOTE]
>
>La riproduzione audio non funziona per i file OGG e WAV su Microsoft® Internet Explorer 11. Errore `Invalid Source` viene visualizzato nella pagina dei dettagli della risorsa per le risorse con estensione OGG o WAV.
>
>Su MS® Edge e iPad, i file OGG non vengono riprodotti e generano un errore di formato non supportato.
