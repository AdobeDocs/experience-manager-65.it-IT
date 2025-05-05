---
title: Gestisci predefiniti visualizzatore
description: Come creare, modificare e gestire i predefiniti per visualizzatori in Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Viewer Presets
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
solution: Experience Manager, Experience Manager Assets
source-git-commit: 13c495b8b7e9824c5de8469df96bec00c74c8dbc
workflow-type: tm+mt
source-wordcount: '4397'
ht-degree: 8%

---

# Gestisci predefiniti visualizzatore{#managing-viewer-presets}

Un predefinito visualizzatore è una raccolta di impostazioni che determinano il modo in cui gli utenti visualizzano le risorse rich media sugli schermi dei loro computer e sui loro dispositivi mobili. Gli amministratori possono creare predefiniti visualizzatore. Le impostazioni sono disponibili per un array di opzioni di configurazione del visualizzatore. Ad esempio, è possibile modificare le dimensioni di visualizzazione o il comportamento di zoom del visualizzatore.

Per istruzioni su come creare e personalizzare i predefiniti visualizzatore di HTML5, consulta la *Documentazione dell&#39;API SDK del visualizzatore di Adobe HTML Dynamic Media*. Il SDK è disponibile sul server di pubblicazione IS incorporato nel SDK stesso. Ogni versione della libreria include la propria documentazione di SDK.

Percorso: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
Ad esempio, 3.10 SDK: [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

Consulta anche la [Guida di riferimento per i visualizzatori Dynamic Media di Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=it).

Questa sezione descrive come creare, modificare e gestire i predefiniti visualizzatore. Puoi applicare un predefinito visualizzatore a una risorsa in qualsiasi momento in cui la visualizzi in anteprima. Vedere [Applicazione dei predefiniti visualizzatore](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>La modifica di *predefiniti visualizzatore predefiniti* non è uno scenario supportato. Se tenti di modificare un predefinito visualizzatore predefinito, ti viene richiesto di salvare il predefinito visualizzatore utilizzando un nuovo nome.

## Accessibilità da tastiera per i visualizzatori {#keyboard-accessibility-for-viewers}

Tutti i visualizzatori predefiniti supportano l’accessibilità da tastiera.

Vedi anche [Accesso facilitato alla tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=it).

## Gestisci predefiniti visualizzatore {#managing-viewer-presets-1}

Per aggiungere, modificare, eliminare, pubblicare, annullare la pubblicazione e visualizzare in anteprima i predefiniti visualizzatore in Adobe Experience Manager, tocca **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>Per impostazione predefinita, quando selezioni Visualizzatori nella vista Dettaglio di una risorsa, il sistema mostra 15 predefiniti visualizzatore. Puoi aumentare questo limite. Consulta la sezione [Aumento del numero di predefiniti visualizzatore](#increasing-the-number-of-viewer-presets-that-display).

### Supporto del visualizzatore per pagine web dinamiche {#viewer-support-for-responsive-designed-web-pages}

Pagine web diverse hanno esigenze diverse. Ad esempio, a volte può essere utile una pagina web che fornisca un collegamento per aprire HTML5 Viewer in una finestra del browser separata. In altri casi, potrebbe essere necessario incorporare il visualizzatore HTML5 direttamente nella pagina di hosting. In quest’ultimo caso, la pagina web potrebbe avere un layout statico. In alternativa, può essere &quot;reattivo&quot; e visualizzato in modo diverso su dispositivi diversi o per diverse dimensioni della finestra del browser. Per soddisfare queste esigenze, tutti i visualizzatori HTML5 predefiniti e forniti con Dynamic Media supportano sia le pagine web statiche che quelle reattive.

Per ulteriori informazioni su come incorporare i visualizzatori reattivi nelle pagine Web, consulta la [Libreria immagini reattive](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html?lang=it).

>[!NOTE]
>
>Pubblica tutti i visualizzatori predefiniti prima di utilizzarli per la prima volta.
>Consulta [Pubblicazione dei predefiniti visualizzatore].(#publishing-viewer-presets)

### Compatibilità del sistema con il predefinito per visualizzatori {#viewer-preset-system-compatibility}

Tutti i predefiniti per visualizzatori forniti con Dynamic Media sono completamente compatibili con i seguenti sistemi:

* Desktop
* Apple iPhone
* Apple iPad
* Smartphone Android™
* Android™ Tablet
* Per il video, è disponibile il supporto aggiuntivo per la riproduzione MP4 per [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) e [Windows Phone](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs).

### Tipi di contenuti multimediali avanzati per predefiniti visualizzatore {#rich-media-types-for-viewer-presets}

Durante la creazione dei predefiniti visualizzatore, gli amministratori possono aggiungere e personalizzare i seguenti tipi di contenuti rich media.

<table>
 <tbody>
  <tr>
   <td><strong>Set carosello</strong><br /> </td>
   <td><p>I punti attivi, le mappe immagine o entrambi vengono aggiunti a una serie di due o più immagini. Un cliente può effettuare la panoramica delle immagini a sinistra o a destra e quindi selezionare un hotspot su un’immagine per ulteriori dettagli o per effettuare acquisti direttamente dalla categoria, dalla home o dalle pagine di destinazione di un sito web.</p> </td>
  </tr>
  <tr>
   <td><strong>Dimensionale</strong><br /> </td>
   <td><p>Visualizza le scene 3D che consentono di ruotare, scorrere, ingrandire o ricentrare la fotocamera.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom a comparsa</strong></td>
   <td><p>Visualizza una seconda immagine dell'area ingrandita accanto all'immagine originale. Nessun controllo da utilizzare: gli utenti spostano la selezione sull'area che desiderano visualizzare.</p> <p>Quando determini l’utilizzo completo della larghezza di banda per questo visualizzatore, tieni presente che sia l’immagine principale che l’immagine a comparsa vengono fornite nel visualizzatore. Le dimensioni dell'immagine principale (larghezza e altezza stage) e il fattore di zoom determinano le dimensioni dell'immagine a comparsa. Per evitare che le dimensioni del file a comparsa diventino troppo grandi, bilancia questi due valori: se hai un'immagine principale di grandi dimensioni, abbassa il valore del fattore di zoom. Le opzioni Larghezza elemento a comparsa e Altezza elemento a comparsa determinano le dimensioni della finestra a comparsa, ma non le dimensioni dell'immagine a comparsa trasmessa al visualizzatore.</p> <p>Ad esempio, se la dimensione dell'immagine principale è 350 x 350 pixel, con un fattore di zoom pari a 3, l'immagine a comparsa risultante sarà 1050 x 1050 pixel. Se la dimensione dell'immagine principale è di 300 x 300 pixel, con un fattore di zoom pari a 4, l'immagine a comparsa è di 1200 x 1200 pixel. A seconda dell'impostazione di qualità di JPEG (le impostazioni consigliate sono comprese tra 80 e 90), è possibile ridurre notevolmente le dimensioni del file. I fattori di zoom consigliati sono da 2,5 a 4, a seconda delle dimensioni dell'immagine principale.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom in linea</strong></td>
   <td>Visualizza un'immagine dell'area ingrandita all'interno del visualizzatore originale. Nessun controllo da utilizzare. In altre parole, gli utenti spostano la selezione sull’area che desiderano visualizzare.</td>
  </tr>
  <tr>
   <td><strong>Set immagini</strong></td>
   <td>Nel visualizzatore Set immagini, gli utenti possono visualizzare diverse visualizzazioni o varianti di colore di un elemento selezionando una miniatura. Questo visualizzatore offre anche strumenti di zoom per esaminare le immagini da vicino.</td>
  </tr>
  <tr>
   <td><strong>Immagine interattiva</strong></td>
   <td>I punti attivi vengono aggiunti alle parti di un’immagine che un cliente può selezionare per ulteriori dettagli o per l’acquisto diretto dalla categoria, dalla home o dalle pagine di destinazione di un sito web.</td>
  </tr>
  <tr>
   <td><strong>Video interattivo</strong></td>
   <td>Le miniature vengono aggiunte ai segmenti della timeline in un video che un cliente può selezionare per ulteriori dettagli o per l’acquisto diretto dalla categoria, dalla home o dalle pagine di destinazione di un sito web.</td>
  </tr>
  <tr>
   <td><strong>File multimediali diversi</strong></td>
   <td>Visualizza diversi tipi di file multimediali in un solo visualizzatore. Puoi includere set 360 gradi, set di immagini, immagini e video.</td>
  </tr>
  <tr>
   <td><strong>Immagine panoramica</strong></td>
   <td><p>I visualizzatori Immagine panoramica e PanoramicaVR offrono immagini panoramiche sferiche per immergere gli utenti in un’esperienza di visione a 360 gradi di una stanza, una proprietà, una posizione o un paesaggio.</p> <p>Affinché un'immagine caricata possa essere considerata un panorama sferico, deve avere una o entrambe le caratteristiche seguenti:</p>
    <ul>
     <li>Rapporto di formato 2:1.</li>
     <li>Taggato con le parole chiave <code>equirectangular</code>, o <code>spherical</code> e <code>panorama</code>, o <code>spherical </code>e <code>panoramic</code>. Vedi <a href="/help/sites-authoring/tags.md">Utilizzo dei tag</a>.</li>
    </ul> <p>Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dei dettagli della risorsa e al componente WCM "Elemento multimediale panoramico".</p> <p><strong>Importante</strong>: questo visualizzatore è disponibile solo in Dynamic Media - modalità Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Ritaglio video automatico</strong><br /> </td>
   <td><p>Usa questo visualizzatore per rilevare e ritagliare automaticamente il punto focale in qualsiasi video.</p> </td>
  </tr>
  <tr>
   <td><strong>Set 360 gradi</strong></td>
   <td>Fornisce più viste di un'immagine in modo che gli utenti possano ruotare l'oggetto per esaminare i diversi lati e angoli.</td>
  </tr>
  <tr>
   <td><strong>Video a 360°</strong></td>
   <td><p>Utilizza il visualizzatore video 360/VR per riprodurre video equirettangolari per un’esperienza di visualizzazione coinvolgente di una stanza, una proprietà, una posizione, un paesaggio o una procedura medica.</p> <p>Durante la riproduzione su uno schermo piatto, l'utente ha il controllo dell'angolo di visualizzazione; la riproduzione su dispositivi mobili applica di solito i controlli giroscopici incorporati.</p> <p>Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Puoi distribuire video 360 utilizzando le estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.</p> <p><strong>Importante</strong>: questo visualizzatore è disponibile solo in Dynamic Media - modalità Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Video</strong></td>
   <td><p>Riproduce il video utilizzando lo streaming con bitrate progressivo o adattivo. Lo streaming con bitrate adattivo esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per fornire la giusta qualità video nel formato giusto.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom verticale</strong></td>
   <td><p>Il visualizzatore con zoom verticale consente di massimizzare l’esperienza di visualizzazione delle immagini del prodotto, per offrire agli utenti la migliore rappresentazione possibile di un prodotto. La posizione verticale dei campioni è la seguente:</p>
    <ul>
     <li>Assicura che i campioni siano "sopra la piega".<br/> I campioni orizzontali, a seconda delle dimensioni dello schermo del desktop dell'utente, non sono visibili finché l'utente non scorre la pagina verso il basso. Posizionando i campioni verticalmente nel visualizzatore, si garantisce che siano visibili indipendentemente dalle dimensioni dello schermo dell'utente.</li>
     <li>Ingrandisce le dimensioni dell'immagine principale.<br /> Con i campioni orizzontali, è necessario riservare spazio sulla pagina per assicurarsi che siano visibili. Questo posizionamento riduce le dimensioni dell'immagine principale. Con un layout di campione verticale, tuttavia, non è necessario allocare questo spazio. È quindi possibile ingrandire l'immagine principale.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoom</strong></td>
   <td>Consente agli utenti di ingrandire l’area selezionandola. Gli utenti possono selezionare i controlli per ingrandire, ridurre e ripristinare le dimensioni predefinite dell'immagine.</td>
  </tr>
 </tbody>
</table>

### Elenco dei predefiniti per visualizzatori {#list-of-out-of-the-box-viewer-presets}

La tabella seguente identifica tutti i predefiniti visualizzatore predefiniti che sono forniti con Dynamic Media.

Vedi anche [Demo live](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

Per informazioni sulle versioni supportate del browser web e del sistema operativo per i visualizzatori, consulta le Note sulla versione dei visualizzatori.

Consultare le note sulla versione dei visualizzatori nel sommario della [Guida di riferimento dei visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=it).

>[!NOTE]
>
>Tutti i predefiniti visualizzatore in Dynamic Media sono già attivati (attivati), ma è necessario pubblicarli.
>Consulta [Pubblicazione dei predefiniti visualizzatore](#publishing-viewer-presets).
>
>Tutti i nuovi predefiniti visualizzatore creati e aggiunti devono essere attivati *e *pubblicati.
>Vedere [Attivazione o disattivazione dei predefiniti visualizzatore](#activating-or-deactivating-viewer-presets) e [Pubblicazione dei predefiniti visualizzatore](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>Titolo predefinito visualizzatore</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome file CSS</strong><br /> </td>
  </tr>
  <tr>
   <td>Carosello_Punteggiato_scuro</td>
   <td>Set_carosello</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carosello_Luce_Punteggiata</td>
   <td>Set_carosello</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carosello_Numeric_dark</td>
   <td>Set_carosello</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carosello_Luce_Numerica</td>
   <td>Set_carosello</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Dimensionale</td>
   <td>Dimensionale</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>A comparsa</td>
   <td>Zoom_a_comparsa</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_dark</td>
   <td>Set immagini</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>Set immagini</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>File_multimediali_misti</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>File_multimediali_misti</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Zoom_a_comparsa</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>File_multimediali_misti</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>File_multimediali_misti</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>Immagine panoramica</td>
   <td>Immagine_Panoramica</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Immagine_Panoramica</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Banner_Shoppable</td>
   <td>Immagine_interattiva</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Video_interattivo</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Video_interattivo</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Ritaglio_avanzato_video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Ritaglio_avanzato_video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Set360_scuro</td>
   <td>Set_360_gradi</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Set_360_gradi</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Video</p> <p>(include il supporto per i sottotitoli)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(include i controlli di riproduzione video di base, il rendering video viene eseguito in modalità stereo, il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato e non è disponibile alcuna funzione per i social media)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Progettato per gli utenti finali che utilizzano occhiali di realtà virtuale. Include controlli di riproduzione video di base e funzioni per social media)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(include il supporto per sottotitoli e social media)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_scuro<br /> </td>
   <td>Zoom<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Luce_zoom<br /> </td>
   <td>Zoom</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Zoom_verticale</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Zoom_verticale</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Matrice di movimenti dei visualizzatori mobili supportati {#supported-mobile-viewers-gestures-matrix}

La tabella seguente identifica i movimenti del visualizzatore mobile supportati sui dispositivi iOS, Android™ 2.x e Android™ 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesto</strong></td>
   <td><strong>Zoom a comparsa</strong></td>
   <td><strong>Zoom</strong></td>
   <td><strong>Set 360 gradi</strong></td>
  </tr>
  <tr>
   <td><p><strong>Trascina</strong></p> </td>
   <td><p>Pannelli</p> </td>
   <td><p>Pannelli</p> </td>
   <td><p>Pannelli</p> </td>
  </tr>
  <tr>
   <td><p><strong>Seleziona</strong></p> </td>
   <td><p>Mostra la finestra a comparsa</p> </td>
   <td><p>Mostra o nasconde l'interfaccia utente</p> </td>
   <td><p>Mostra o nasconde l'interfaccia utente</p> </td>
  </tr>
  <tr>
   <td><p><strong>Doppia selezione</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Ingrandisce o ripristina</p> </td>
   <td><p>Ingrandisce o ripristina</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pizzicare</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Ingrandisce (solo iOS e Android™ 3x)</p> </td>
   <td><p>Ingrandisce (solo iOS e Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pizzicare</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Esegue lo zoom indietro (solo iOS e Android™ 3x)</p> </td>
   <td><p>Esegue lo zoom indietro (solo iOS e Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Passaggio del dito</strong></p> </td>
   <td><p>Scorre la barra dei campioni</p> </td>
   <td><p>Scorre le immagini</p> </td>
   <td><p>Rotazioni</p> </td>
  </tr>
  <tr>
   <td><p><strong>Gesto rapido</strong></p> </td>
   <td><p>Scorre la barra dei campioni</p> </td>
   <td><p>Scorre le immagini</p> </td>
   <td><p>Rotazioni</p> </td>
  </tr>
 </tbody>
</table>

## Aumentare il numero di predefiniti visualizzatore visualizzati {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager mostra un&#39;ampia varietà di predefiniti visualizzatore quando si visualizza una risorsa da **[!UICONTROL Visualizzazione dettagli]** > **[!UICONTROL Visualizzatori]**. Puoi aumentare o diminuire il numero di visualizzatori visualizzati.

**Aumenta il numero di predefiniti visualizzatore visualizzati:**

1. Passa a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Passa al nodo dell’elenco di predefiniti visualizzatore nella posizione seguente:

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Passa all&#39;origine dati del predefinito visualizzatore in `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. Nella proprietà limit, modifica il numero impostando il numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Seleziona **[!UICONTROL Salva tutto]**.

## Creare un predefinito per visualizzatori {#creating-a-new-viewer-preset}

La creazione di predefiniti visualizzatore consente di applicare varie impostazioni per visualizzare e interagire con le risorse. Tuttavia, non è necessario creare predefiniti visualizzatore. Se lo desideri, puoi utilizzare i predefiniti predefiniti visualizzatori che sono già disponibili in AEM Assets.

Se scegli di creare un predefinito visualizzatore, dopo averlo salvato lo stato del visualizzatore viene attivato automaticamente (impostato su **[!UICONTROL Il]**) nella pagina Predefiniti visualizzatore. Questo stato indica che è visibile nel componente Dynamic Media e nel componente File multimediali interattivi e ogni volta che visualizzi l’anteprima di un’immagine o di un video.

Alcuni predefiniti visualizzatore hanno impostazioni esclusive che possono influenzare l’uso e il comportamento complessivo del visualizzatore. A seconda del predefinito visualizzatore che crei, potrebbe essere utile tenere presenti queste considerazioni speciali.

Consulta [Considerazioni speciali per la creazione di un predefinito visualizzatore interattivo](#special-considerations-for-creating-an-interactive-viewer-preset).

Consulta [Considerazioni speciali per la creazione di un predefinito per visualizzatore banner carosello](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**Per creare un predefinito visualizzatore:**

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Assets] > [!UICONTROL Predefiniti visualizzatore]**.

   ![6_5_visualizzatori predefiniti](assets/6_5_viewerpresets.png)

1. Nella pagina Predefiniti visualizzatore selezionare **[!UICONTROL Crea]** sulla barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Nuovo predefinito visualizzatore]** immettere il nome del nuovo predefinito nel campo **[!UICONTROL Nome predefinito]**. Scegli il nome con attenzione: dopo aver selezionato **[!UICONTROL Crea]**, non sarà più possibile modificarlo.

   Quando salvi il predefinito più avanti in questi passaggi, il nome viene visualizzato nella pagina Predefiniti visualizzatore sotto l&#39;intestazione della colonna Titolo predefinito.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona il tipo di predefinito visualizzatore da creare, quindi nell&#39;angolo superiore destro della pagina seleziona **[!UICONTROL Crea]**.

   Consulta [Tipi di contenuti multimediali avanzati per predefiniti visualizzatore](#rich-media-types-for-viewer-presets).

1. Nella pagina Editor predefiniti per visualizzatori, seleziona la scheda **[!UICONTROL Aspetto]**.
1. Effettua una delle seguenti operazioni:

   * Nel menu a discesa **[!UICONTROL Tipo selezionato]**, selezionare un componente di cui si desidera personalizzare la struttura visiva. In alternativa, puoi selezionare qualsiasi elemento visivo nel visualizzatore per configurarlo.

     L’editor visivo consente di vedere l’effetto di una determinata proprietà su uno stile. Imposta o regola qualsiasi proprietà per vedere immediatamente quale effetto ha sul visualizzatore utilizzando l&#39;esempio a sinistra dell&#39;editor.

     Le proprietà di stile CSS per ogni tipo di predefinito visualizzatore sono descritte nell&#39;argomento della Guida &quot;Personalizzazione del visualizzatore *`<viewer name>`*&quot; nella [Guida di riferimento visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=it). Ad esempio, se stai creando un predefinito visualizzatore di tipo `Mixed_Media`, consulta [Personalizzazione del visualizzatore di file multimediali diversi](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html?lang=it) per un elenco e una descrizione di ciascuna proprietà.

   * Se hai definito le impostazioni stile in un file CSS separato, puoi caricarlo in AEM Assets. Seleziona **[!UICONTROL Importa CSS]** sotto il menu a discesa **[!UICONTROL Tipo selezionato]** (se necessario, scorri l&#39;editor visivo per visualizzarlo) in modo da trovare il file CSS caricato e associarlo al predefinito visualizzatore.

     Quando importi un file CSS, l’editor visivo controlla se il CSS utilizza i marcatori visualizzatore corretti. Ad esempio, se crei un visualizzatore Zoom, tutte le regole CSS importate devono essere definite utilizzando il nome della classe di visualizzatore `.s7mixedmediaviewer` definito in un elemento visualizzatore padre.

     Puoi importare file CSS arbitrari e fatti a mano, purché definiscano correttamente i marcatori CSS per un determinato visualizzatore. (I marcatori CSS sono descritti in qualsiasi argomento della Guida relativo alla personalizzazione di *&lt;nome visualizzatore>* Visualizzatore nella [Guida di riferimento visualizzatori](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=it). Ad esempio, per informazioni sui marcatori CSS per il Visualizzatore zoom, vedere [Personalizzazione del Visualizzatore zoom](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html?lang=it). È possibile, tuttavia, che l&#39;editor visivo non comprenda alcuni valori CSS. In questi casi, l’editor visivo tenta di ignorare gli errori in modo che il CSS possa ancora funzionare.

   >[!NOTE]
   >
   >Se preferisci modificare il CSS direttamente nel relativo modulo non elaborato, seleziona **[!UICONTROL Mostra/Nascondi CSS]** nel menu a discesa Tipo selezionato (se necessario, scorri l&#39;editor visivo per visualizzarlo).
   >Come per l’editor visivo, quando modifichi una proprietà direttamente nel CSS, puoi vedere immediatamente l’effetto che ha sull’esempio di visualizzatore. Inoltre, la stessa proprietà viene aggiornata automaticamente allo stesso tempo nell’editor visivo. Pertanto, puoi utilizzare l’editor CSS non elaborato, l’editor visivo o entrambi in modo intercambiabile.

   >[!NOTE]
   >
   >Per la grafica dei pulsanti, scegliete l&#39;immagine 2x e caricate la grafica ad alta risoluzione. Quando lavori con immagini interattive e banner acquistabili, puoi anche selezionare tra vari pulsanti di hotspot preconfigurati.

1. (Facoltativo) Nella parte superiore della pagina Modifica predefinito visualizzatore, seleziona **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** o **[!UICONTROL Telefono]** per definire in modo univoco gli stili visivi per dispositivi e tipi di schermo diversi.
1. Nella pagina Editor predefiniti per visualizzatore, seleziona la scheda **[!UICONTROL Comportamento]**. In alternativa, puoi selezionare qualsiasi elemento visivo nel visualizzatore per configurarlo.
Ad esempio, per il tipo *VideoPlayer*, in **[!UICONTROL Modificatori]** > **[!UICONTROL Riproduzione]**, puoi selezionare una delle tre opzioni di streaming bitrate adattivo:

   * **[!UICONTROL trattino]** - I video vengono trasmessi solo come trattino. Tuttavia, sui dispositivi Safari/iOS è necessario selezionare **[!UICONTROL hls]** come tipo.
   * **[!UICONTROL hls]** - I video vengono trasmessi solo come hls.
   * **[!UICONTROL auto]** - Procedure consigliate. La creazione di flussi DASH e HLS è ottimizzata per l’archiviazione. Adobe consiglia pertanto di selezionare sempre **[!UICONTROL auto]** come tipo di riproduzione. I video vengono trasmessi come dash, hls o progressive, come nell&#39;ordine di riproduzione seguente:
      * Se il browser supporta DASH, viene utilizzato prima il flusso DASH.
      * Se il browser non supporta DASH, viene utilizzato lo streaming HLS, secondo.
      * Se il browser non supporta DASH o HLS, viene utilizzata la riproduzione progressiva.

1. Dal menu a discesa **[!UICONTROL Tipo selezionato]**, scegli un componente di cui vuoi modificare i comportamenti.

   A molti componenti dell’editor visivo è associata una descrizione dettagliata. Queste descrizioni vengono visualizzate all’interno di caselle blu quando espandi un componente per visualizzarne i parametri associati.

   Alcuni tipi di Visualizzatore dispongono di componenti che consentono di specificare i comandi Image Server in un campo di testo **[!UICONTROL Comando IS]**. Per un elenco dei comandi utilizzabili, consulta la sezione [Riferimento API di Server immagini](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html?lang=it).

   >[!NOTE]
   >
   >**Se si utilizza un dispositivo touch, ad esempio un telefono o un tablet...**
   >
   >
   >Dopo aver digitato un valore nel campo di testo, selezionare un&#39;altra posizione nell&#39;interfaccia utente per inviare la modifica e chiudere la tastiera virtuale. Se si seleziona Invio, non viene eseguita alcuna azione.

1. Seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina.
1. Pubblica il nuovo predefinito visualizzatore in modo da poterlo utilizzare sul tuo sito web.

   Consulta [Pubblicazione dei predefiniti visualizzatore](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >Per i vecchi video che utilizzano un profilo di streaming con bitrate adattivo, l&#39;URL continua a essere riprodotto come di consueto, con lo streaming HLS, fino a [la rielaborazione delle risorse video](/help/assets/processing-profiles.md#reprocessing-assets). Dopo la rielaborazione, lo stesso URL continua a funzionare, ma ora con *entrambi* DASH e streaming HLS abilitati.

### Considerazioni speciali per la creazione di un predefinito visualizzatore interattivo {#special-considerations-for-creating-an-interactive-viewer-preset}

**Informazioni sulle modalità di visualizzazione delle miniature delle immagini nel pannello**

Quando crei o modifichi un predefinito visualizzatore video interattivo, puoi scegliere l&#39;impostazione Modalità di visualizzazione da usare quando selezioni `InteractiveSwatches` dal menu **[!UICONTROL Componente selezionato]** nella scheda **[!UICONTROL Comportamento]**. La modalità di visualizzazione selezionata influisce sulla modalità e sul momento in cui vengono visualizzate le miniature durante la riproduzione del video. È possibile scegliere la modalità di visualizzazione `segment` (predefinita) o `continuous`.

<table>
 <tbody>
  <tr>
   <td><strong>Modalità di visualizzazione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Segmento</td>
   <td><p><code>Segment </code>è la modalità di visualizzazione predefinita per i predefiniti del Visualizzatore video interattivo <code>Shoppable_Video_light</code> e <code>Shoppable_Video_dark</code> predefiniti e per tutti i predefiniti del Visualizzatore video interattivo creati dall'utente.</p> <p>In questa modalità, quando a un segmento video sono assegnate meno miniature del numero di punti visibili nel pannello di visualizzazione. Inoltre, le miniature dei sottosegmenti successivi o precedenti sono <i>non </i>trascinate per riempire gli spazi vuoti nel pannello. In altre parole, mantiene la visualizzazione dei campioni assegnati a un particolare segmento video.</p> </td>
  </tr>
  <tr>
   <td>Continuo</td>
   <td><p>In modalità di visualizzazione <code>continuous </code>, se il numero di miniature in un segmento è inferiore al numero visibile nel pannello, il visualizzatore include automaticamente la visualizzazione delle miniature del segmento successivo. In alternativa, nel caso in cui venga visualizzata l’ultima miniatura, il visualizzatore include automaticamente anche la visualizzazione delle miniature del segmento precedente.</p> <p>Il <a href="/help/assets/interactive-videos.md">video in questo argomento</a> è un esempio della <code>continuous </code>modalità di visualizzazione.</p> </td>
  </tr>
 </tbody>
</table>

**Informazioni sul comportamento di scorrimento automatico nel visualizzatore video interattivo**

Il comportamento di scorrimento automatico delle miniature nel visualizzatore video interattivo funziona indipendentemente dalla modalità di visualizzazione scelta.

Quando crei o modifichi un predefinito visualizzatore video interattivo, puoi accedere a Scorrimento automatico dalla scheda Comportamento. Nella scheda Comportamento selezionare **[!UICONTROL InteractiveSwatches]** dal menu a discesa **[!UICONTROL Componenti selezionati]**. La casella di controllo Scorrimento automatico è elencata sotto il campo di testo Comando IS.

Se nel predefinito visualizzatore disattivi **[!UICONTROL Scorrimento automatico]** deselezionando la casella di controllo, durante la riproduzione del video da parte dell’utente il pannello visualizza solo la prima miniatura per l’intera durata del video. Tuttavia, un utente può scorrere manualmente le miniature utilizzando le icone di freccia su e giù, se necessario.

Durante la riproduzione del video, se hai abilitato tramite selezione l’opzione **[!UICONTROL Scorrimento automatico]** nel predefinito visualizzatore, le immagini in miniatura assegnate a un segmento video scorrono all’inizio di un segmento. Tuttavia, in alcuni casi, determinate miniature all’interno di un segmento vengono visualizzate con una durata raddoppiata rispetto alle altre miniature precedenti o successive. Questo comportamento si verifica perché il numero di miniature in un segmento è maggiore rispetto al numero visibile nel pannello e non è divisibile in modo uniforme.

Supponiamo di avere un segmento video di 30 secondi. In totale, sono presenti nove miniature da visualizzare in 30 secondi. Il browser viene ridimensionato in modo che nel pannello di visualizzazione siano visibili quattro miniature. Il segmento di tempo video di 30 secondi è diviso in tre sottosegmenti. La tabella seguente mostra il raggruppamento delle miniature visualizzate per un dato sottosegmento temporale:

| **Sottosegmento video** | **Tempo del sottosegmento in secondi** | **Miniature visibili nel pannello** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20 — 30 | 6, 7, 8, 9 |

Il sottosegmento video 3 non si estende oltre le miniature ad esso assegnate. Inoltre, le miniature 4, 6 e 7 sono visibili nel pannello con una lunghezza doppia rispetto alle altre miniature.

La logica utilizzata dal visualizzatore per il numero di miniature visualizzate nel pannello in base al numero di posizioni disponibili è la seguente:

* Numero di segmenti secondari = arrotonda al sottosegmento successivo (numero di miniature / numero di slot visibili nel pannello delle miniature, in base alle dimensioni della finestra del browser).
Utilizzando l’esempio riportato nella tabella precedente, 9 miniature/4 slot = 2,25; la logica di visualizzazione lo arrotonda a tre sottosegmenti.

* Numero di miniature = arrotonda alla miniatura successiva (numero di miniature/numero di sottosegmenti video).
Utilizzando l’esempio riportato nella tabella precedente, 9 miniature / 3 sottosegmenti video = 3 miniature.

* Durata del sottosegmento = durata video totale / numero di sottosegmenti video.
Utilizzando l’esempio riportato nella tabella precedente, 30 secondi/3 sottosegmenti video = visualizzazione di 10 secondi di ciascun sottosegmento video.

#### Considerazioni speciali per la creazione di predefiniti per visualizzatori di banner carosello {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

Durante la creazione dei predefiniti visualizzatore di banner carosello, è possibile accedere come segue per modificare lo stile dei punti attivi:

| | **Descrizione** | **Azioni** |
|---|---|---|
| **[!UICONTROL Icona punto attivo]** | Modifica l&#39;icona utilizzata per il punto attivo | Per modificare l&#39;immagine dell&#39;icona punto attivo, nella scheda **[!UICONTROL Aspetto]**, in **[!UICONTROL Componente selezionato]**, selezionare **[!UICONTROL ImageMapEffect]**. In **[!UICONTROL Icona]**, seleziona **[!UICONTROL Sfondo]** e nel campo **[!UICONTROL Immagine]** individua l&#39;immagine di sfondo desiderata. |

## Attivare o disattivare i predefiniti visualizzatore {#activating-or-deactivating-viewer-presets}

I predefiniti visualizzatore disponibili nell’interfaccia utente dipendono da quali sono attivi in modalità Creazione. Per impostazione predefinita, un predefinito visualizzatore è attivato dopo la sua creazione. Se disattivate il predefinito, non viene visualizzato in modalità Creazione. Se il predefinito viene pubblicato, viene sempre pubblicato indipendentemente dal fatto che sia attivato o disattivato. Se l’elenco risulta troppo complesso o non si desidera rendere disponibile un predefinito visualizzatore, potrebbe essere utile disattivare i predefiniti visualizzatore.

**Per attivare o disattivare i predefiniti visualizzatore:**

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Nella pagina Predefinito visualizzatore, nell&#39;intestazione della colonna **[!UICONTROL Stato]**, seleziona l&#39;interruttore per attivare o disattivare un predefinito visualizzatore.

   I predefiniti visualizzatore attivati hanno l&#39;interruttore visualizzato a destra, all&#39;interno di una casella blu; i predefiniti visualizzatore disattivati hanno l&#39;interruttore visualizzato a sinistra, all&#39;interno di una casella grigio chiaro.

## Pubblica predefiniti visualizzatore {#publishing-viewer-presets}

Attivando (o attivando) lo stato di un predefinito visualizzatore, questo diventa visibile nel componente Dynamic Media, nel componente Interactive Media e ogni volta che visualizzi una risorsa.

Tuttavia, per *distribuire* una risorsa con un predefinito visualizzatore, è necessario pubblicare anche il predefinito visualizzatore. Per ottenere l&#39;URL o il codice di incorporamento di una risorsa, tutti i predefiniti visualizzatore devono essere attivati *e* pubblicati. Assicurati di attivare e pubblicare tutti i predefiniti visualizzatore forniti con Dynamic Media. I predefiniti visualizzatore personalizzati che crei e aggiungi vengono attivati automaticamente, ma devono anche essere pubblicati.

Vedere [Attivazione o disattivazione dei predefiniti visualizzatore](#activating-or-deactivating-viewer-presets).

Vedi anche [Anteprima di Assets](/help/assets/previewing-assets.md).

**Per pubblicare i predefiniti visualizzatore:**

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Seleziona uno o più predefiniti visualizzatore da pubblicare.
1. Sulla barra degli strumenti, seleziona l&#39;icona **[!UICONTROL Pubblica]**.

## Ordina predefiniti visualizzatore {#sorting-viewer-presets}

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Seleziona **[!UICONTROL Titolo predefinito]**, **[!UICONTROL Tipo]**, **[!UICONTROL Pubblicato]** o **[!UICONTROL Stato]** per ordinare in base all&#39;intestazione di colonna. Ad esempio, seleziona **[!UICONTROL Tipo]** per ordinare i tipi di predefiniti visualizzatore in ordine alfabetico o inverso.

## Modifica predefiniti visualizzatore {#editing-viewer-presets}

La modifica di *predefiniti visualizzatore predefiniti* non è uno scenario supportato. Se modifichi un predefinito visualizzatore predefinito, ti viene richiesto di salvarlo con un nuovo nome.

**Per modificare i predefiniti visualizzatore:**

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorsa]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Seleziona un predefinito selezionando la casella a sinistra del titolo del predefinito del visualizzatore.
1. Sulla barra degli strumenti, selezionare **[!UICONTROL Modifica]**.
1. Nella pagina **[!UICONTROL Editor predefiniti visualizzatore]**, apporta le modifiche desiderate al predefinito visualizzatore, utilizzando le opzioni disponibili nelle schede **[!UICONTROL Aspetto]** e **[!UICONTROL Comportamento]**.

   Dalla scheda **[!UICONTROL Aspetto]**, nell&#39;angolo superiore sinistro della pagina Editor predefiniti per visualizzatore, seleziona **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** o **[!UICONTROL Telefono]** per modificare la modalità di presentazione della risorsa.

1. Nell&#39;angolo superiore destro della pagina eseguire una delle operazioni seguenti:

   * Seleziona **[!UICONTROL Salva]** per salvare le modifiche e tornare alla pagina Predefinito visualizzatore.
   * Seleziona **[!UICONTROL Annulla]** per annullare le modifiche apportate e tornare alla pagina Predefinito visualizzatore.

## Elimina predefiniti visualizzatore personalizzati {#deleting-custom-viewer-presets}

Puoi eliminare i predefiniti visualizzatore creati e aggiunti a Dynamic Media.

**Per eliminare i predefiniti visualizzatore personalizzati:**

1. Nell&#39;angolo superiore sinistro di Experience Manager, seleziona il logo Experience Manager, quindi nella barra a sinistra seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) **[!UICONTROL Assets]** > **[!UICONTROL Predefiniti visualizzatore]**.
1. Nella pagina Predefiniti visualizzatore, seleziona un Titolo predefinito, quindi seleziona l&#39;icona **[!UICONTROL Elimina]**.
1. Seleziona **[!UICONTROL Elimina]**.

## Applicare un predefinito visualizzatore a una risorsa {#applying-a-viewer-preset-to-an-asset}

Se hai già pubblicato sia la risorsa che il visualizzatore selezionato, dopo aver selezionato un predefinito visualizzatore vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL Incorpora]**.

**Per applicare un predefinito visualizzatore a una risorsa:**

1. Apri la risorsa e seleziona il menu a discesa nell&#39;angolo superiore sinistro della pagina, quindi seleziona **[!UICONTROL Visualizzatori]**.

   >[!NOTE]
   >
   >Se hai già pubblicato sia la risorsa che il visualizzatore selezionato, dopo aver selezionato un predefinito visualizzatore vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL Incorpora]**.

1. Seleziona un predefinito visualizzatore nel riquadro a sinistra per applicarlo alla risorsa.

   Puoi [copiare l&#39;URL per condividere](/help/assets/linking-urls-to-yourwebapplication.md) con altri utenti.

## Distribuire risorse con i predefiniti visualizzatore {#delivering-assets-with-viewer-presets}

Per ottenere gli URL per i predefiniti visualizzatore, vedere [Collegamento degli URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md). Vedere anche [Incorporazione del visualizzatore video in una pagina Web](/help/assets/embed-code.md).

Se utilizzi Experience Manager come WCM, puoi aggiungere risorse utilizzando i predefiniti visualizzatore direttamente nella pagina. Consulta [Aggiunta di Dynamic Media Assets alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).
