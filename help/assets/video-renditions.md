---
title: Rappresentazioni video
description: Rappresentazioni video
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
translation-type: tm+mt
source-git-commit: 66f46a34832254af74c72da16ec8ebe3eb8cd46d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Rappresentazioni video {#video-renditions}

Adobe Experience Manager (AEM) Assets genera rappresentazioni video per risorse video di vari formati, inclusi OGG, FLV e così via.

 AEM Assets supporta rappresentazioni statiche e dinamiche (rappresentazioni con codifica DM) per risorse multimediali.

Le rappresentazioni statiche vengono generate in modo nativo utilizzando FFMPEG (installato e disponibile nel percorso di sistema) e memorizzate nell&#39;archivio dei contenuti.

Le rappresentazioni con codifica DM vengono memorizzate nel server proxy e servite in fase di esecuzione.

AEM risorse supportano la riproduzione per queste rappresentazioni sul lato client.

Per visualizzare le rappresentazioni di una particolare risorsa video, aprite la relativa pagina di risorse e toccate l’icona Navigazione globale. Quindi, scegliete **[!UICONTROL Rendering]** dall&#39;elenco.

![chlimage_1-478](assets/chlimage_1-478.png)

L&#39;elenco delle rappresentazioni video viene visualizzato nel pannello **[!UICONTROL Rappresentazioni]**.

![chlimage_1-479](assets/chlimage_1-479.png)

Per configurare il server proxy per le rappresentazioni con codifica DM, [configurare i servizi Dynamic Media Cloud.](config-dynamic.md)

Per generare rappresentazioni video con i parametri desiderati, [create un profilo video corrispondente](video-profiles.md).

Dopo aver configurato il server proxy e creato i profili video, potete includere questo predefinito video in un profilo di elaborazione e applicare il profilo di elaborazione a una cartella.

>[!NOTE]
>
>La riproduzione audio non funziona per i file OGG e WAV in Microsoft Internet Explorer 11. Nella pagina dei dettagli della risorsa viene visualizzato un errore `Invalid Source` per le risorse con estensione OGG o WAV.
>
>In MS Edge e iPad, i file OGG non vengono riprodotti e generano un errore di formato non supportato.
