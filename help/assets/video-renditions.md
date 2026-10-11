---
title: Rappresentazioni video
description: Scopri come utilizzare Adobe Experience Manager Assets per generare rappresentazioni video per risorse video di vari formati, tra cui OGG, FLV e così via.
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
solution: Experience Manager, Experience Manager Assets
feature: Video
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: cb04d42d-1b70-43b0-9951-45998eb6e842
    internal-label: Video
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%
---
# Rappresentazioni video {#video-renditions}

Adobe Experience Manager Assets genera rappresentazioni video per risorse video di vari formati, tra cui OGG, FLV e così via.

Experience Manager Assets supporta le rappresentazioni statiche e dinamiche (rappresentazioni con codifica DM) per le risorse multimediali.

Le rappresentazioni statiche vengono generate in modo nativo utilizzando FFMPEG (installato e disponibile nel percorso del sistema) e memorizzate nell’archivio dei contenuti.

Le rappresentazioni con codifica DM vengono memorizzate nel server proxy e distribuite in fase di esecuzione.

Experience Manager Assets fornisce il supporto per la riproduzione di queste rappresentazioni sul lato client.

Per visualizzare le rappresentazioni di una particolare risorsa video, apri la pagina della risorsa e seleziona l’icona Navigazione globale. Scegliere quindi **[!UICONTROL Rappresentazioni]** dall&#39;elenco.

![chlimage_1-478](assets/chlimage_1-478.png)

L&#39;elenco delle rappresentazioni video viene visualizzato nel pannello **[!UICONTROL Rappresentazioni]**.

![chlimage_1-479](assets/chlimage_1-479.png)

Per configurare il server proxy per le rappresentazioni con codifica DM, [configurare i servizi cloud per elementi multimediali dinamici](config-dynamic.md).

Per generare le rappresentazioni video con i parametri desiderati, [crea un profilo video corrispondente](video-profiles.md).

Dopo aver configurato il server proxy e creato i profili video, puoi includere questo predefinito video in un profilo di elaborazione e applicare il profilo di elaborazione a una cartella.

>[!NOTE]
>
>La riproduzione audio non funziona per i file OGG e WAV su Microsoft® Internet Explorer 11. Nella pagina dei dettagli delle risorse con estensione OGG o WAV viene visualizzato l&#39;errore `Invalid Source`.
>
>In MS® Edge e iPad, i file OGG non vengono riprodotti e viene generato un errore di formato non supportato.
