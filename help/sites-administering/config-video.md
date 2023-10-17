---
title: Configurare il componente Video
description: Scopri come utilizzare il componente Video in Adobe Experience Manager per inserire nella pagina una risorsa video predefinita e pronta all’uso.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Configurare il componente Video {#configure-the-video-component}

Il [Componente video](/help/sites-authoring/default-components-foundation.md#video) consente di inserire nella pagina una risorsa video predefinita e pronta all’uso.

Affinché la trascodifica venga eseguita correttamente, l&#39;amministratore installa FFmpeg separatamente. Consulta [Installare FFmpeg e configurare AEM](#install-ffmpeg). Anche gli amministratori [Configurare i profili video](#configure-video-profiles) da utilizzare con elementi HTML5.

>[!CAUTION]
>
>Questo componente di base è stato dichiarato obsoleto. L’Adobe consiglia di utilizzare [Componente core Incorpora](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) invece.

>[!CAUTION]
>
>Non è più previsto che questo componente funzioni come preconfigurato senza un’ampia personalizzazione a livello di progetto.

## Configurare i profili video {#configure-video-profiles}

Per l’utilizzo degli elementi HTML5, definisci i profili video. Quelli scelti qui sono usati in ordine. Per accedere a, utilizza [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) (Solo interfaccia classica) e seleziona il **[!UICONTROL Profili]** scheda:

![chlimage_1-317](assets/chlimage_1-317.png)

Da questa finestra di dialogo, puoi anche configurare la progettazione del componente Video e i parametri per [!UICONTROL Riproduzione], [!UICONTROL Flash], e [!UICONTROL Avanzate].

## Installare FFmpeg e configurare AEM {#install-ffmpeg}

Il componente Video si basa sul prodotto open-source FFmpeg per la transcodifica dei video. Scaricato da [https://ffmpeg.org/](https://ffmpeg.org/). Dopo aver installato FFmpeg, configurare AEM per utilizzare un codec audio specifico e opzioni di runtime specifiche.

Per installare FFmpeg su **Windows**, effettua le seguenti operazioni:

1. Scarica il file binario compilato come `ffmpeg.zip`.
1. Annulla l’archiviazione in una cartella.
1. Impostare la variabile di ambiente di sistema `PATH` a &lt;*your-ffmpeg-location*>`\bin`.
1. Riavviare AEM.

Per installare FFmpeg su **MACOS X**, effettua le seguenti operazioni:

1. Installa Xcode disponibile all’indirizzo [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Installazione disponibile all’indirizzo [XQuartz](https://www.xquartz.org) per ottenere [X11](https://support.apple.com/en-us/100724).
1. Installare le porte Mac disponibili all&#39;indirizzo [www.macports.org](https://www.macports.org/).
1. Nella console, esegui `sudo port install ffmpeg` e seguire le istruzioni visualizzate. Assicurati che il percorso del `FFmpeg` l&#39;eseguibile viene aggiunto al `PATH` variabile di sistema.

Per installare FFmpeg su **macOS X 10.6**, utilizzando la versione precompilata, effettua le seguenti operazioni:

1. Scarica la versione precompilata.
1. Annulla l’archiviazione in `/usr/local` directory.
1. Nella console, esegui `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modificare il percorso in modo appropriato.

A **configurare AEM**, effettua le seguenti operazioni:

>[!NOTE]
>
>Questi passaggi sono necessari solo se è richiesta un’ulteriore personalizzazione dei codec.

1. Apri [!UICONTROL CRXDE Liti] nel browser. Accesso [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Seleziona la `/libs/settings/dam/video/format_aac/jcr:content` e assicurati che le proprietà del nodo siano le seguenti:

   * `audioCodec` è `aac`.
   * `customArgs` è `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Per personalizzare la configurazione, crea una sovrapposizione in `/apps/settings/` e spostare la stessa struttura in `/conf/global/settings/` nodo. Non può essere modificato in `/libs` nodo. Ad esempio, per sovrapporre il percorso `/libs/settings/dam/video/fullhd-bp`, creala in `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sovrapponi e modifica l’intero nodo-profilo e non solo la proprietà che deve essere modificata. Tali risorse non vengono risolte tramite SlingResourceMerger.

4. Se è stata modificata una delle proprietà, fare clic su **[!UICONTROL Salva tutto]**.

>[!NOTE]
>
>Le modifiche ai modelli di flusso di lavoro predefiniti non vengono mantenute quando si aggiorna l’istanza AEM. L’Adobe consiglia di copiare i modelli di flusso di lavoro modificati prima di modificarli. Ad esempio, copia la [!UICONTROL Aggiorna risorsa DAM] prima di modificare il passaggio Transcodifica FFmpeg in [!UICONTROL Aggiorna risorsa DAM] modello per scegliere i nomi dei profili video esistenti prima dell&#39;aggiornamento. Quindi, puoi sovrapporre `/apps` per consentire all&#39;AEM di recuperare le modifiche personalizzate al modello OOTB.
