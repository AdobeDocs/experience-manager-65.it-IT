---
title: Configurare il componente Video
seo-title: Configure the Video component
description: Scopri come configurare il componente video.
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Configurare il componente Video {#configure-the-video-component}

La [Componente video](/help/sites-authoring/default-components-foundation.md#video) consente di inserire una risorsa video predefinita (OOTB) nella pagina.

Affinché si verifichi una transcodifica corretta, un amministratore installa separatamente FFmpeg. Vedi [Installare FFmpeg e configurare AEM](#install-ffmpeg). Anche gli amministratori [Configurare i profili video](#configure-video-profiles) da utilizzare con gli elementi di HTML5.

>[!CAUTION]
>
>Questo componente di base è stato dichiarato obsoleto. L’Adobe consiglia di utilizzare [Componente di incorporamento componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come standard senza un’ampia personalizzazione a livello di progetto.

## Configurare i profili video {#configure-video-profiles}

Per utilizzare gli elementi di HTML5, definisci i profili video. Quelli scelti qui sono utilizzati in ordine. Per accedere, utilizza [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) (Solo interfaccia classica) e seleziona la **[!UICONTROL Profili]** scheda:

![chlimage_1-317](assets/chlimage_1-317.png)

Da questa finestra di dialogo, puoi anche configurare la progettazione del componente Video e i parametri per [!UICONTROL Riproduzione], [!UICONTROL Flash]e [!UICONTROL Avanzate].

## Installare FFmpeg e configurare AEM {#install-ffmpeg}

Il componente Video si basa sul prodotto open-source di terze parti FFmpeg per la transcodifica dei video. Scaricato da [https://ffmpeg.org/](https://ffmpeg.org/). Dopo aver installato FFmpeg, configura AEM per utilizzare un codec audio specifico e specifiche opzioni di runtime.

Per installare FFmpeg su **Windows**, segui questi passaggi:

1. Scarica il binario compilato come `ffmpeg.zip`.
1. Annulla l’archiviazione in una cartella.
1. Imposta la variabile di ambiente del sistema `PATH` a &lt;*your-ffmpeg-location*>`\bin`.
1. Riavvia AEM.

Per installare FFmpeg su **Mac OS X**, segui questi passaggi:

1. Installa Xcode disponibile all&#39;indirizzo [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Installa disponibile all&#39;indirizzo [XQuartz](https://www.xquartz.org) per ottenere [X11](https://support.apple.com/en-us/HT201341).
1. Installa MacPorts disponibile in [www.macports.org](https://www.macports.org/).
1. Nella console esegui `sudo port install ffmpeg` e seguire le istruzioni visualizzate. Assicurati che il percorso del `FFmpeg` eseguibile aggiunto al `PATH` variabile di sistema.

Per installare FFmpeg su **Mac OS X 10.6**, utilizzando la versione precompilata, segui questi passaggi:

1. Scarica la versione precompilata.
1. Annulla l’archiviazione nel `/usr/local` directory.
1. Nella console, esegui `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modificate i percorsi in base alle necessità.

A **configurare AEM**, segui questi passaggi:

>[!NOTE]
>
>Questi passaggi sono necessari solo se è necessaria un&#39;ulteriore personalizzazione dei codec.

1. Apri [!UICONTROL CRXDE Lite] nel browser web. Accesso [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleziona la `/libs/settings/dam/video/format_aac/jcr:content` e assicurati che le proprietà del nodo siano le seguenti:

   * `audioCodec` è `aac`.
   * `customArgs` è `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Per personalizzare la configurazione, crea una sovrapposizione in `/apps/settings/` e spostare la stessa struttura sotto `/conf/global/settings/` nodo. Non può essere modificato in `/libs` nodo. Ad esempio, per sovrapporre il percorso `/libs/settings/dam/video/fullhd-bp`, crea `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sovrapponi e modifica l’intero nodo del profilo e non solo la proprietà che deve essere modificata. Tali risorse non vengono risolte tramite SlingResourceMerger.

4. Se hai modificato una delle proprietà, fai clic su **[!UICONTROL Salva tutto]**.

>[!NOTE]
>
>Le modifiche ai modelli di flusso di lavoro predefiniti (OOTB) non vengono mantenute quando aggiorni l’istanza di AEM. Adobe consiglia di copiare i modelli di flusso di lavoro modificati prima di modificarli. Ad esempio, copia l’OOTB [!UICONTROL Risorsa di aggiornamento DAM] prima di modificare il passaggio Transcodifica FFmpeg nel [!UICONTROL Risorsa di aggiornamento DAM] modello per scegliere i nomi dei profili video esistenti prima dell&#39;aggiornamento. Quindi puoi sovrapporre il `/apps` per consentire AEM recuperare le modifiche personalizzate al modello OOTB.
