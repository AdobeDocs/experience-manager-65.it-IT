---
title: Rappresentazioni video
description: Rappresentazioni video
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Rappresentazioni video {#video-renditions}

Adobe Experience Manager (AEM) Assets genera rappresentazioni video per risorse video di vari formati, inclusi OGG, FLV e così via.

AEM Assets supporta le rappresentazioni statiche e dinamiche (rappresentazioni con codifica DM) per le risorse multimediali.

Le rappresentazioni statiche vengono generate in modo nativo utilizzando FFMPEG (installato e disponibile nel percorso di sistema) e memorizzate nell’archivio dei contenuti.

Le rappresentazioni con codifica DM vengono memorizzate nel server proxy e distribuite in fase di runtime.

Le risorse AEM supportano la riproduzione di queste rappresentazioni sul lato client.

Per visualizzare le rappresentazioni di una particolare risorsa video, apri la relativa pagina delle risorse e tocca l’icona Navigazione globale . Quindi, scegli **[!UICONTROL Rendering]** dall’elenco.

![chlimage_1-478](assets/chlimage_1-478.png)

L’elenco delle rappresentazioni video viene visualizzato nel pannello **[!UICONTROL Rappresentazioni]** .

![chlimage_1-479](assets/chlimage_1-479.png)

Per configurare il server proxy per rappresentazioni con codifica DM, [configura Dynamic Media Cloud Services](config-dynamic.md).

Per generare rappresentazioni video con i parametri desiderati, [crea un profilo video corrispondente](video-profiles.md).

Dopo aver configurato il server proxy e creato i profili video, puoi includere questo predefinito video in un profilo di elaborazione e applicare il profilo di elaborazione a una cartella.

>[!NOTE]
>
>La riproduzione audio non funziona per i file OGG e WAV in Microsoft Internet Explorer 11. Nella pagina dei dettagli della risorsa viene visualizzato un errore `Invalid Source` per le risorse con estensione OGG o WAV.
>
>Su MS Edge e iPad, i file OGG non vengono riprodotti e generano un errore di formato non supportato.
