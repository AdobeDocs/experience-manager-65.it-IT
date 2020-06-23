---
title: Configurare il componente Video
seo-title: Configurare il componente Video
description: Scoprite come configurare il componente Video.
seo-description: Scoprite come configurare il componente Video.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Configurare il componente Video {#configure-the-video-component}

Il componente [](/help/sites-authoring/default-components-foundation.md#video) Video consente di inserire una risorsa video predefinita (OOTB) nella pagina.

Affinché venga eseguita la transcodifica corretta, l&#39;amministratore installa separatamente FFmpeg. Consultate [Installare FFmpeg e configurare AEM](#install-ffmpeg). Administrators also [Configure Video Profiles](#configure-video-profiles) for use with HTML5 elements.

## Configurare i profili video {#configure-video-profiles}

Per l’utilizzo di elementi HTML5, definite i profili video. Quelli scelti qui sono utilizzati in ordine. Per accedere, utilizzate la modalità [](/help/sites-authoring/default-components-designmode.md) Progettazione (solo interfaccia classica) e selezionate la scheda **[!UICONTROL Profili]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Da questa finestra di dialogo potete anche configurare la progettazione del componente Video e i parametri per [!UICONTROL Riproduzione], [!UICONTROL Flash]e [!UICONTROL Avanzato].

## Installare FFmpeg e configurare AEM {#install-ffmpeg}

Il componente Video si basa sul prodotto open-source FFmpeg di terze parti per la transcodifica di video. Scaricato da [https://ffmpeg.org/](https://ffmpeg.org/). Dopo l’installazione di FFmpeg, configurate AEM per l’utilizzo di un codec audio specifico e di opzioni di runtime specifiche.

Per installare FFmpeg in **Windows**, procedere come segue:

1. Scarica il binario compilato come `ffmpeg.zip`.
1. Annulla l’archiviazione in una cartella.
1. Impostate la variabile di ambiente del sistema `PATH` su &lt;*your-ffmpeg-location*>`\bin`.
1. Riavviate AEM.

Per installare FFmpeg in **Mac OS X**, effettuate le seguenti operazioni:

1. Installate Xcode disponibile all&#39;indirizzo [developer.apple.com/xcode](hhttps://developer.apple.com/xcode/).
1. Installazione disponibile in [XQuartz](https://www.xquartz.org) per ottenere [X11](https://support.apple.com/en-us/HT201341).
1. Installate MacPorts disponibile all&#39;indirizzo [www.macports.org](https://www.macports.org/).
1. Nella console eseguire `sudo port install ffmpeg` il comando e seguire le istruzioni visualizzate. Assicurarsi che il percorso dell&#39; `FFmpeg` eseguibile sia aggiunto alla variabile di `PATH` sistema.

Per installare FFmpeg in **Mac OS X 10.6**, utilizzando la versione precompilata, effettuate le seguenti operazioni:

1. Scaricate la versione precompilata.
1. Disarchiviarlo nella `/usr/local` directory.
1. Nella console, eseguire `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modificate i percorsi come appropriato.

Per **configurare AEM**, effettuate le seguenti operazioni:

>[!NOTE]
>
>Questi passaggi sono necessari solo se è necessaria un&#39;ulteriore personalizzazione dei codec.

1. Open [!UICONTROL CRXDE Lite] in your web browser. Accedete a [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Selezionare il `/libs/settings/dam/video/format_aac/jcr:content` nodo e assicurarsi che le proprietà del nodo siano le seguenti:

   * `audioCodec` è `aac`.
   * `customArgs` è `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Per personalizzare la configurazione, create una sovrapposizione nel `/apps/settings/` nodo e spostate la stessa struttura sotto il `/conf/global/settings/` nodo. Non può essere modificato nel `/libs` nodo. Ad esempio, per sovrapporre il percorso, `/libs/settings/dam/video/fullhd-bp`createlo in `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sovrapponi e modifica l’intero nodo del profilo e non solo la proprietà che deve essere modificata. Tali risorse non vengono risolte tramite SlingResourceMerger.

4. If you changed either of the properties, click **[!UICONTROL Save All.]**

>[!NOTE]
>
>Le modifiche apportate ai modelli di flusso di lavoro predefiniti (OOTB) non vengono mantenute quando aggiornate l’istanza di AEM. Adobe consiglia di copiare i modelli di flusso di lavoro modificati prima di modificarli. Ad esempio, copiate il modello OOTB [!UICONTROL DAM Update Asset] prima di modificare il passaggio di transcodifica FFmpeg nel modello [!UICONTROL DAM Update Asset] per scegliere i nomi dei profili video esistenti prima dell’aggiornamento. Quindi, potete sovrapporre il `/apps` nodo per consentire ad AEM di recuperare le modifiche personalizzate al modello OOTB.
