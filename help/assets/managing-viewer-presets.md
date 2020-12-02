---
title: Gestione dei predefiniti per visualizzatori
description: Come creare e gestire i predefiniti per visualizzatori
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '4353'
ht-degree: 15%

---


# Gestione dei predefiniti per visualizzatori{#managing-viewer-presets}

Un predefinito per visualizzatori è un insieme di impostazioni che determinano in che modo gli utenti possono visualizzare le risorse multimediali sullo schermo del computer e sui dispositivi mobili. Un amministratore può creare dei predefiniti per visualizzatori. Sono disponibili impostazioni per una serie di opzioni di configurazione del visualizzatore. Ad esempio, potete modificare le dimensioni di visualizzazione o il comportamento di zoom del visualizzatore.

Per istruzioni su come creare e personalizzare i predefiniti per visualizzatori HTML5, consultate l’SDK per visualizzatori HTML5 per  Adobe Scene7 **. L’SDK è disponibile nel server di pubblicazione IS incorporato nell’SDK stesso. Ogni versione della libreria include una propria documentazione SDK.

Percorso: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
Ad esempio, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

Consultate anche la [Guida di riferimento dei visualizzatori di Adobi ](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

Questa sezione descrive come creare, modificare e gestire i predefiniti per visualizzatori. Potete applicare un predefinito per visualizzatori a una risorsa ogni volta che la visualizzate in anteprima. Consultate [Applicazione dei predefiniti per visualizzatori](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>Tenete presente che la modifica di eventuali predefiniti per visualizzatori *predefiniti* non è uno scenario supportato. Se tentate di modificare un predefinito per visualizzatori preimpostato, vi verrà richiesto di salvare il predefinito per visualizzatori con un nuovo nome.

## Accessibilità da tastiera per visualizzatori {#keyboard-accessibility-for-viewers}

Tutti i visualizzatori integrati supportano l&#39;accessibilità da tastiera.

Vedere anche [Accessibilità della tastiera e navigazione](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## Gestione dei predefiniti per visualizzatori {#managing-viewer-presets-1}

Per aggiungere, modificare, eliminare, pubblicare, annullare la pubblicazione e visualizzare in AEM i predefiniti per visualizzatori, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse > Predefiniti visualizzatore.]**

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>Per impostazione predefinita, quando selezionate Visualizzatori nella visualizzazione Dettagli di una risorsa, il sistema mostra 15 predefiniti per visualizzatori. Puoi aumentare questo limite. Consulta la sezione [Aumento del numero di predefiniti visualizzatore](#increasing-the-number-of-viewer-presets-that-display).

### Supporto visualizzatore per pagine Web reattive {#viewer-support-for-responsive-designed-web-pages}

Diverse pagine Web hanno esigenze diverse. Ad esempio, a volte desiderate una pagina Web che fornisca un collegamento per aprire il visualizzatore HTML5 in una finestra browser separata. In altri casi, potrebbe essere necessario incorporare il visualizzatore HTML5 direttamente nella pagina host. In quest’ultimo caso, la pagina Web potrebbe avere un layout statico. Oppure può essere &quot;reattivo&quot; e può essere visualizzato in modo diverso su diversi dispositivi o per diverse dimensioni della finestra del browser. Per soddisfare queste esigenze, tutti i visualizzatori HTML5 predefiniti forniti con Dynamic Media supportano sia le pagine Web statiche che quelle reattive.

Per ulteriori informazioni su come incorporare visualizzatori reattivi nelle pagine Web, consultate [Libreria immagini reattive](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) nella *Guida API di Scene7 Image Serving*.

>[!NOTE]
>
>Prima di iniziare a utilizzarli, è necessario pubblicare tutti i visualizzatori inclusi.
>Consultate [Predefiniti per visualizzatori di pubblicazione.](#publishing-viewer-presets)

### Compatibilità del sistema dei predefiniti per visualizzatori {#viewer-preset-system-compatibility}

Tutti i predefiniti per visualizzatori forniti con gli elementi multimediali dinamici sono completamente compatibili con i seguenti sistemi:

* Desktop
* Apple iPhone
* Apple iPad
* Smartphone Android
* Tablet Android
* Per i video, è disponibile un supporto aggiuntivo per la riproduzione MP4 per [Blackberry](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) e [Windows Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx).

### Tipi di contenuti multimediali avanzati per i predefiniti per visualizzatori {#rich-media-types-for-viewer-presets}

Gli amministratori possono aggiungere e personalizzare i seguenti tipi di contenuti multimediali quando creano nuovi predefiniti per visualizzatori.

<table>
 <tbody>
  <tr>
   <td><strong>Set carosello</strong><br /> </td>
   <td><p>I punti attivi, le mappe immagine o entrambi vengono aggiunti a una serie di due o più immagini. Un cliente può scorrere le immagini a sinistra o a destra e quindi fare clic su un punto di attivazione su un'immagine per ulteriori dettagli o per acquistare direttamente dalla categoria, dalla pagina principale o dalle pagine di destinazione di un sito Web.</p> </td>
  </tr>
  <tr>
   <td><strong>Dimensionale</strong><br /> </td>
   <td><p>Visualizza le scene 3D che consentono di ruotare, scorrere, ingrandire o rientrare nella fotocamera.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom a comparsa</strong></td>
   <td><p>Visualizza una seconda immagine dell’area ingrandita accanto all’immagine originale. Nessun controllo da utilizzare: gli utenti possono spostare la selezione sull’area da visualizzare.</p> <p>Quando calcolate l’utilizzo di larghezza di banda totale per questo visualizzatore, tenete presente che nel visualizzatore vengono servite sia l’immagine principale che l’immagine a comparsa. Le dimensioni dell’immagine principale (larghezza e altezza dell’area di visualizzazione) e il fattore di zoom determinano le dimensioni dell’immagine a comparsa. Per evitare che le dimensioni del file a comparsa diventino eccessive, bilanciate i due valori seguenti: se l’immagine principale è di grandi dimensioni, riducete il fattore di zoom. Larghezza a comparsa e Altezza comparsa determinano le dimensioni della finestra a comparsa, ma non dell’immagine a comparsa caricata nel visualizzatore.</p> <p>Ad esempio, se le dimensioni dell’immagine principale sono 350 x 350 pixel, con un fattore di zoom pari a 3 l’immagine a comparsa risultante sarà di 1050 x 1050 pixel. Se le dimensioni dell’immagine principale sono 300 x 300 pixel, con un fattore di zoom pari a 4 l’immagine a comparsa sarà di 1200 x 1200 pixel. A seconda dell’impostazione di qualità JPEG (le impostazioni consigliate sono comprese tra 80 e 90), potete ridurre notevolmente la dimensione del file. I fattori di zoom consigliati sono compresi tra 2,5 e 4, a seconda delle dimensioni dell’immagine principale.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom in linea</strong></td>
   <td>Visualizza un’immagine dell’area ingrandita all’interno del visualizzatore originale. Nessun controllo da utilizzare. In altre parole, gli utenti spostano la selezione sull'area da visualizzare.</td>
  </tr>
  <tr>
   <td><strong>Set immagini</strong></td>
   <td>Nel visualizzatore di set di immagini, gli utenti possono vedere diverse viste o varianti di colore di un elemento facendo clic su una miniatura. Questo visualizzatore offre anche strumenti di zoom per esaminare le immagini da vicino.</td>
  </tr>
  <tr>
   <td><strong>Immagine interattiva</strong></td>
   <td>Gli hotspot vengono aggiunti a porzioni di un'immagine su cui il cliente può fare clic per ulteriori dettagli o per acquistare direttamente dalla categoria del sito Web, dalla home page o dalle pagine di destinazione.</td>
  </tr>
  <tr>
   <td><strong>Video interattivo</strong></td>
   <td>Le miniature vengono aggiunte ai segmenti della timeline di un video al quale un cliente può fare clic per ulteriori dettagli o per acquistare direttamente dalla categoria, dalla pagina principale o dalle pagine di destinazione di un sito Web.</td>
  </tr>
  <tr>
   <td><strong>File multimediali diversi</strong></td>
   <td>Consente di visualizzare diversi tipi di supporti in un visualizzatore. Potete includere set 360 gradi, set di immagini, immagini e video.</td>
  </tr>
  <tr>
   <td><strong>Immagine panoramica</strong></td>
   <td><p>I visualizzatori Panoramic Image (Immagine panoramica) e PanoramicVR (VR panoramico) consentono di riprodurre immagini panoramiche sferiche per consentire agli utenti di visualizzare a 360° una stanza, una proprietà, un luogo o un paesaggio.</p> <p>Affinché un’immagine caricata possa essere definita come panorama sferico, deve avere una o entrambe le caratteristiche seguenti:</p>
    <ul>
     <li>Proporzioni di 2:1.</li>
     <li>Tag con le parole chiave <code>equirectangular</code>, <code>spherical</code> e <code>panorama</code>, oppure <code>spherical </code>e <code>panoramic</code>. Vedere <a href="/help/sites-authoring/tags.md">Utilizzo dei tag</a>.</li>
    </ul> <p>Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche per la pagina dei dettagli delle risorse che per il componente WCM "File multimediali panoramici".</p> <p><strong>Importante</strong>: Questo visualizzatore è disponibile solo in modalità Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Ritaglio video automatico</strong><br /> </td>
   <td><p>Usate questo visualizzatore per rilevare e ritagliare automaticamente il punto focale in qualsiasi video.</p> </td>
  </tr>
  <tr>
   <td><strong>Set 360 gradi</strong></td>
   <td>Fornisce diverse viste di un’immagine in modo che gli utenti possano ruotare l’oggetto per esaminare i diversi lati e angolazioni.</td>
  </tr>
  <tr>
   <td><strong>Video 360</strong></td>
   <td><p>Usate il visualizzatore video 360/VR per effettuare il rendering di video equirettangolari per un’esperienza di visualizzazione coinvolgente di una stanza, una proprietà, un luogo, un paesaggio o una procedura medica.</p> <p>Durante la riproduzione su un display piatto, l'utente ha il controllo dell'angolo di visione; la riproduzione su dispositivi mobili solitamente utilizza i controlli giroscopici incorporati.</p> <p>Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Potete distribuire video a 360 gradi utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.</p> <p><strong>Importante</strong>: Questo visualizzatore è disponibile solo in modalità Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Video</strong></td>
   <td><p>Riproduce video con streaming a bitrate progressivo o adattivo. Lo streaming con bitrate adattivo esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per trasmettere il video di qualità ottimale nel formato corretto.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom verticale</strong></td>
   <td><p>Il visualizzatore zoom verticale consente di ottimizzare l’esperienza di visualizzazione di un prodotto per offrire agli utenti la migliore rappresentazione di un prodotto. La posizione verticale dei campioni effettua le seguenti operazioni:</p>
    <ul>
     <li>Assicurarsi che i campioni siano "al di sopra della piega".<br/> Con i campioni orizzontali, a seconda delle dimensioni dello schermo del desktop dell’utente, i campioni non erano visibili finché l’utente non scorreva la pagina verso il basso. Posizionando i campioni in verticale nel visualizzatore, questi vengono visualizzati indipendentemente dalle dimensioni dello schermo dell’utente.</li>
     <li>Ottimizza le dimensioni dell’immagine principale.<br /> Con i campioni orizzontali, è necessario riservare spazio sulla pagina per assicurarsi che siano visibili. Questo posizionamento ha ridotto le dimensioni dell'immagine principale. Con un layout di campioni verticale, tuttavia, non è necessario allocare questo spazio. Potete quindi ingrandire le dimensioni dell’immagine principale.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoom</strong></td>
   <td>Consente agli utenti di ingrandire l’area facendo clic su di essa. Gli utenti possono fare clic sui controlli per ingrandire, ridurre e ripristinare le dimensioni predefinite dell’immagine.</td>
  </tr>
 </tbody>
</table>

### Elenco di predefiniti per visualizzatori forniti con Scene7 {#list-of-out-of-the-box-viewer-presets}

La tabella seguente identifica tutti i predefiniti per visualizzatori predefiniti forniti con gli elementi multimediali dinamici.

Vedere anche [Live Demos](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html).

Per informazioni sui browser Web e sulle versioni del sistema operativo supportati per i visualizzatori, consultate le Note sulla versione dei visualizzatori.

Consultate &quot;Note sulla versione dei visualizzatori&quot; nel sommario della [Guida di riferimento dei visualizzatori](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

>[!NOTE]
>
>Tutti i predefiniti per visualizzatori inclusi in Contenuti multimediali dinamici sono già attivati (attivato), ma è necessario pubblicarli.
>Consultate [Predefiniti visualizzatore pubblicazione](#publishing-viewer-presets).
>
>Eventuali nuovi predefiniti per visualizzatori creati e aggiunti devono essere attivati *e *pubblicati.
>Consultate [Attivazione o disattivazione dei predefiniti per visualizzatori](#activating-or-deactivating-viewer-presets) e [Pubblicazione dei predefiniti per visualizzatori](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>Titolo predefinito per visualizzatori</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome file CSS</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Dotted_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Dotted_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Dimensionale</td>
   <td>Dimensionale</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>A comparsa</td>
   <td>Flyout_Zoom</td>
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
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>Immagine panoramica</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interactive_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_dark</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Video</p> <p>(Comprende il supporto per sottotitoli codificati)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(Comprende i controlli di riproduzione video di base, il rendering video viene eseguito in modalità stereo, il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato e nessuna funzione social media)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Progettato per gli utenti finali che utilizzano occhiali di realtà virtuale. Comprende controlli di riproduzione video di base e funzioni per social media)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>(Comprende il supporto per sottotitoli codificati e social media)</p> </td>
   <td>Video</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>Zoom<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>Zoom</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Matrice di gesti supportati dai visualizzatori per dispositivi mobili {#supported-mobile-viewers-gestures-matrix}

La tabella seguente identifica i gesti del visualizzatore mobile supportati sui dispositivi iOS, Android 2.x e Android 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesto</strong></td>
   <td><strong>Zoom a comparsa</strong></td>
   <td><strong>Zoom</strong></td>
   <td><strong>Set 360 gradi</strong></td>
  </tr>
  <tr>
   <td><p><strong>Trascinamento</strong></p> </td>
   <td><p>Pannelli</p> </td>
   <td><p>Pannelli</p> </td>
   <td><p>Pannelli</p> </td>
  </tr>
  <tr>
   <td><p><strong>Toccare</strong></p> </td>
   <td><p>Visualizza la finestra a comparsa</p> </td>
   <td><p>Mostra o nasconde l’interfaccia utente</p> </td>
   <td><p>Mostra o nasconde l’interfaccia utente</p> </td>
  </tr>
  <tr>
   <td><p><strong>Doppio tocco</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Effettua uno zoom in o reimposta</p> </td>
   <td><p>Effettua uno zoom in o reimposta</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pizzico</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Effettua uno zoom in (solo iOS e Android 3x)</p> </td>
   <td><p>Effettua uno zoom in (solo iOS e Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Chiudi con il dito</strong></p> </td>
   <td><p>Non applicabile</p> </td>
   <td><p>Effettua uno zoom out (solo iOS e Android 3x)</p> </td>
   <td><p>Effettua uno zoom out (solo iOS e Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Passaggio del dito</strong></p> </td>
   <td><p>Fa scorrere la barra dei campioni</p> </td>
   <td><p>Fa scorrere le immagini</p> </td>
   <td><p>Rotazione</p> </td>
  </tr>
  <tr>
   <td><p><strong>Flick</strong></p> </td>
   <td><p>Fa scorrere la barra dei campioni</p> </td>
   <td><p>Fa scorrere le immagini</p> </td>
   <td><p>Rotazione</p> </td>
  </tr>
 </tbody>
</table>

## Aumento del numero di predefiniti per visualizzatori visualizzati {#increasing-the-number-of-viewer-presets-that-display}

AEM mostra un’ampia varietà di predefiniti per visualizzatori quando visualizzate una risorsa da **[!UICONTROL Visualizzazione dettagli > Visualizzatori.]** Potete aumentare o diminuire il numero di visualizzatori.

**Per aumentare il numero di predefiniti per visualizzatori visualizzati**

1. Andate al CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Andate al nodo di elenco dei predefiniti per visualizzatori in `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Andate all&#39;origine dati del predefinito per visualizzatori in `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. Nella proprietà limit, modificare il numero in base al numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toccare **[!UICONTROL Salva tutto.]**

## Creazione di un predefinito per visualizzatori {#creating-a-new-viewer-preset}

La creazione di predefiniti per visualizzatori consente di applicare diverse impostazioni per visualizzare e interagire con le risorse. Tuttavia, non è necessario creare nuovi predefiniti per visualizzatori. Se preferite, potete usare i predefiniti per visualizzatori predefiniti forniti con  AEM Assets.

Se scegliete di creare un nuovo predefinito per visualizzatori, dopo averlo salvato, lo stato del visualizzatore viene attivato automaticamente (impostato su **[!UICONTROL On]**) nella pagina Predefiniti visualizzatore. Questo stato significa che è visibile nel componente Contenuti multimediali dinamici e nel componente Contenuti multimediali interattivi e ogni volta che visualizzate l’anteprima di un’immagine o di un video.

Alcuni predefiniti per visualizzatori dispongono di impostazioni esclusive che possono influenzare l’utilizzo e il comportamento generale del visualizzatore. A seconda del predefinito per visualizzatori che state creando, potete essere consapevoli di queste considerazioni speciali.

Consultate [Considerazioni speciali per la creazione di un predefinito per visualizzatori interattivi](#special-considerations-for-creating-an-interactive-viewer-preset).

Consultate [Considerazioni speciali per la creazione di un predefinito per visualizzatori di banner carosello](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**Per creare un predefinito per visualizzatori**

1. Nell&#39;angolo superiore sinistro del AEM, toccate il logo AEM, quindi nella barra a sinistra, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse] > [!UICONTROL Predefiniti visualizzatore]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. Nella pagina Predefiniti visualizzatore, nella barra degli strumenti, toccate **[!UICONTROL Crea.]**
1. Nella finestra di dialogo **[!UICONTROL Nuovo predefinito per visualizzatori]**, immettete il nome del nuovo predefinito nel campo **[!UICONTROL Nome predefinito]**. Scegli il nome attentamente, poiché non potrai modificarlo, dopo aver toccato **[!UICONTROL Crea.]**

   Quando salvate il predefinito in seguito, il nome viene visualizzato nella pagina Predefiniti visualizzatore, sotto l’intestazione della colonna Titolo predefinito.

1. Dal menu a discesa Tipo di file multimediali avanzati, selezionate il tipo di predefinito per visualizzatori da creare, quindi toccate **[!UICONTROL Crea nell&#39;angolo superiore destro della pagina.]**

   Consultate [Tipi di contenuti multimediali avanzati per i predefiniti per visualizzatori](#rich-media-types-for-viewer-presets).

1. Nella pagina Editor predefiniti per visualizzatori, tocca la scheda **[!UICONTROL Appearance (Aspetto)]**.
1. Effettua una delle operazioni seguenti:

   * Nel menu a discesa **[!UICONTROL Tipo selezionato]**, selezionate un componente di cui desiderate personalizzare la progettazione visiva. In alternativa, puoi toccare o fare clic su qualsiasi elemento visivo del visualizzatore per configurarlo.

      L&#39;editor visivo consente di visualizzare l&#39;effetto di una determinata proprietà su uno stile. È sufficiente impostare o regolare una qualsiasi proprietà per vedere immediatamente quale effetto ha sul visualizzatore utilizzando l’esempio a sinistra dell’editor.

      Le proprietà di stile CSS per ciascun tipo di predefinito per visualizzatori sono descritte nell&#39;argomento della guida &quot;Personalizzazione *`<viewer name>`* del visualizzatore&quot; nella [Guida di riferimento dei visualizzatori](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html). Ad esempio, se state creando un predefinito per visualizzatori di tipo `Mixed_Media`, consultate [Customizing Mixed Media Viewer](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) per un elenco e una descrizione di ciascuna proprietà.

   * Se hai definito le impostazioni stile in un file CSS separato, puoi caricarlo in AEM Assets. Toccate **[!UICONTROL Importa CSS]** sotto il menu a discesa **[!UICONTROL Tipo selezionato]** (potrebbe essere necessario scorrere l&#39;editor visivo per visualizzarlo) per trovare il file CSS caricato e associarlo al predefinito per visualizzatori.

      Quando importate un file CSS, l&#39;editor visivo verifica se il CSS utilizza i marcatori visualizzatore corretti. Ad esempio, se create un visualizzatore zoom, tutte le regole CSS importate devono essere definite utilizzando il nome della classe del visualizzatore `.s7mixedmediaviewer` definito su un elemento visualizzatore principale.

      Potete importare CSS arbitrario, a mano, purché definisca correttamente i marcatori CSS per un determinato visualizzatore. (I marcatori CSS sono descritti in un qualsiasi argomento della guida &quot;Personalizzazione *&lt;nome visualizzatore>* del visualizzatore&quot; nella [Guida di riferimento dei visualizzatori](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html). Ad esempio, per informazioni sui marcatori CSS per il visualizzatore zoom, consultate [Personalizzazione del visualizzatore zoom](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html). È tuttavia possibile che l&#39;editor visivo non comprenda alcuni valori CSS. In tali casi, l&#39;editor visivo tenta di ignorare gli errori in modo che il CSS possa funzionare comunque.
   >[!NOTE]
   >
   >Se preferisci modificare il CSS direttamente nel relativo modulo non elaborato, tocca **[!UICONTROL Mostra/Nascondi CSS]** nel menu a discesa Tipo selezionato (potrebbe essere necessario scorrere l’editor visivo per visualizzare l’opzione).
   >Come nell’editor visivo, quando apportate una modifica a una proprietà direttamente nel CSS, potete vedere immediatamente quale effetto produce sull’esempio del visualizzatore. Inoltre, la stessa proprietà viene automaticamente aggiornata nello stesso momento nell&#39;editor visivo. Potete quindi utilizzare l&#39;editor CSS non elaborato o l&#39;editor visivo oppure entrambi in modo intercambiabile.

   >[!NOTE]
   >
   >Per la grafica di un pulsante, scegliete l&#39;immagine 2x e caricate la grafica ad alta risoluzione. Quando lavorate con immagini interattive e banner acquistabili, potete anche scegliere tra diversi pulsanti out-of-the-box.

1. (Facoltativo) Nella parte superiore della pagina Modifica predefinito visualizzatore, tocca **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** o **[!UICONTROL Telefono]** per definire in modo univoco gli stili visivi per dispositivi e tipi di schermo diversi.
1. Nella pagina Editor predefinito per visualizzatori, toccate la scheda **[!UICONTROL Comportamento]**. In alternativa, puoi toccare o fare clic su qualsiasi elemento visivo del visualizzatore per configurarlo.
1. Dal menu a discesa **[!UICONTROL Tipo selezionato]**, scegli un componente di cui vuoi modificare i comportamenti.

   A molti componenti nell’editor visivo è associata una descrizione dettagliata. Queste descrizioni vengono visualizzate all’interno di caselle blu quando si espande un componente per visualizzarne i parametri associati.

   Alcuni tipi di Visualizzatore dispongono di componenti che consentono di specificare i comandi Image Server in un campo di testo **[!UICONTROL Comando IS]**. Per un elenco dei comandi utilizzabili, consulta la sezione [Riferimento API di Server immagini](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html).

   >[!NOTE]
   >
   >**Se utilizzi un dispositivo touch, ad esempio un telefono o un tablet...**
   >
   >
   >Dopo aver digitato un valore nel campo di testo, toccate altrove nell&#39;interfaccia utente per inviare la modifica e chiudere la tastiera virtuale. Se toccate Invio, non viene eseguita alcuna azione.

1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva.]**
1. Pubblicate il nuovo predefinito per visualizzatori. Per poter usare il predefinito nel sito Web, è necessario pubblicarlo.

   Consultate [Predefiniti visualizzatore pubblicazione](#publishing-viewer-presets).

### Considerazioni speciali per la creazione di un predefinito per visualizzatori interattivi {#special-considerations-for-creating-an-interactive-viewer-preset}

**Modalità di visualizzazione per le miniature delle immagini nel pannello**

Quando create o modificate un predefinito per visualizzatori video interattivi, potete scegliere quale impostazione utilizzare per la modalità di visualizzazione quando selezionate `InteractiveSwatches` dal menu a discesa **[!UICONTROL Componente selezionato]** nella scheda **[!UICONTROL Comportamento]**. La modalità di visualizzazione selezionata influisce su come e quando vengono visualizzate le miniature durante la riproduzione del video. È possibile scegliere una modalità `segment`di visualizzazione (impostazione predefinita) o una modalità di visualizzazione `continuous`.

<table>
 <tbody>
  <tr>
   <td><strong>Modalità di visualizzazione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Segmento</td>
   <td><p><code>Segment </code>è la modalità di visualizzazione predefinita per i predefiniti per visualizzatori video interattivi preimpostati <code>Shoppable_Video_light</code> e <code>Shoppable_Video_dark</code> e per tutti i predefiniti per visualizzatori video interattivi creati dall’utente.</p> <p>In questa modalità, se a un segmento video sono assegnate meno miniature rispetto al numero di punti visibili nel pannello di visualizzazione, le miniature dei segmenti secondari successivi o precedenti sono <i>non </i>trascinate per riempire eventuali punti vuoti nel pannello. In altre parole, mantiene la visualizzazione dei campioni assegnati al segmento video specifico.</p> </td>
  </tr>
  <tr>
   <td>Continuo</td>
   <td><p>In <code>continuous </code>modalità di visualizzazione, se il numero di miniature in un segmento è inferiore al numero visibile nel pannello, il visualizzatore include automaticamente la visualizzazione delle miniature del segmento successivo, o del segmento precedente, nei casi in cui viene visualizzata l'ultima miniatura.</p> <p>Il <a href="/help/assets/interactive-videos.md">video in questo argomento</a> è un esempio della <code>continuous </code>modalità di visualizzazione.</p> </td>
  </tr>
 </tbody>
</table>

**Informazioni sul comportamento di scorrimento automatico nel visualizzatore video interattivo**

Il comportamento di scorrimento automatico delle miniature nel visualizzatore video interattivo funziona indipendentemente dalla modalità di visualizzazione scelta.

Quando crei o modifichi un predefinito visualizzatore video interattivo, puoi accedere a Scorrimento automatico dalla scheda Comportamento. Nella scheda Comportamento, seleziona il menu a discesa **[!UICONTROL Componenti selezionati]** e tocca **[!UICONTROL InteractiveSwatches.]** La casella di controllo Scorrimento automatico è elencata sotto il campo di testo Comando IS.

Se nel predefinito visualizzatore disattivi **[!UICONTROL Scorrimento automatico]** deselezionando la casella di controllo, durante la riproduzione del video da parte dell’utente il pannello visualizza solo la prima miniatura per l’intera durata del video. Tuttavia, un utente può scorrere manualmente le miniature utilizzando le icone di freccia su e giù, se necessario.

Durante la riproduzione del video, se hai abilitato tramite selezione l’opzione **[!UICONTROL Scorrimento automatico]** nel predefinito visualizzatore, le immagini in miniatura assegnate a un segmento video scorrono all’inizio di un segmento. Tuttavia, in alcuni casi, determinate miniature all’interno di un segmento vengono visualizzate con una durata raddoppiata rispetto alle altre miniature precedenti o successive. Questo comportamento si verifica perché il numero di miniature in un segmento è maggiore rispetto al numero visibile nel pannello e non è divisibile in modo uniforme.

Ad esempio, supponete di avere un segmento video di 30 secondi. Ci sono nove miniature da visualizzare in totale nei 30 secondi. Il browser viene ridimensionato in modo che nel pannello di visualizzazione siano presenti quattro miniature visibili. Il segmento di tempo video di 30 secondi è diviso in tre sottosegmenti. La tabella seguente mostra la suddivisione delle miniature visualizzate per un determinato sottosegmento di tempo:

| **Sottosegmento video** | **Tempo del sottosegmento in secondi** | **Miniature visibili nel pannello** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

Il sottosegmento video 3 non si estende oltre le miniature ad esso assegnate. Le miniature 4, 6 e 7 sono visibili nel pannello due volte più a lungo delle altre miniature.

La logica usata dal visualizzatore per il numero di miniature visualizzate nel pannello in base al numero di posizioni disponibili è la seguente:

* Numero di sottosegmenti = arrotondamento al sottosegmento successivo (numero di miniature/numero di slot visibili nel pannello delle miniature, in base alle dimensioni della finestra del browser).
Utilizzando l&#39;esempio nella tabella precedente, 9 miniature / 4 slot = 2,25; la logica del visualizzatore lo arrotonda a 3 sottosegmenti.

* Numero di miniature = arrotondamento alla miniatura successiva (numero di miniature/numero di sottosegmenti video).
Utilizzando l&#39;esempio nella tabella precedente, 9 miniature / 3 sottosegmenti video = 3 miniature.

* Durata del sottosegmento = durata video totale/numero di sottosegmenti video.
Utilizzando l’esempio nella tabella precedente, 30 secondi / 3 sottosegmenti video = 10 secondi di visualizzazione di ciascun sottosegmento video.

#### Considerazioni speciali per la creazione di predefiniti per visualizzatori di banner carosello {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

Quando create i predefiniti per visualizzatori Carosello Banner, è possibile accedere alle modifiche dello stile dei punti di attivazione nel modo seguente:

|  | **Descrizione** | **Azioni** |
|---|---|---|
| **[!UICONTROL Icona punto di attivazione]** | Modifica dell’icona utilizzata per il punto di attivazione | Per modificare l&#39;immagine dell&#39;icona del punto di attivazione, nella scheda **[!UICONTROL Aspetto]**, in **[!UICONTROL Componente selezionato]** toccare **[!UICONTROL ImageMapEffect.]** Seleziona **[!UICONTROL Sfondo]** alla voce **[!UICONTROL Icona]** e, nel campo **[!UICONTROL Immagine]**, individua l’immagine di sfondo desiderata. |

## Attivazione o disattivazione dei predefiniti per visualizzatori {#activating-or-deactivating-viewer-presets}

I predefiniti per visualizzatori disponibili nell’interfaccia utente dipendono da quelli attivi in modalità Autore. Per impostazione predefinita, un predefinito per visualizzatori è &quot;attivato&quot; dopo averlo creato. Se disattivate il predefinito, questo non verrà visualizzato in modalità Autore. Se il predefinito viene pubblicato. verranno sempre pubblicati indipendentemente dal fatto che siano attivati o disattivati. Potete disattivare i predefiniti per visualizzatori se l’elenco diventa troppo ingombrante o se non desiderate che sia disponibile un predefinito per visualizzatori da usare.

**Per attivare o disattivare i predefiniti per visualizzatori**

1. Nell&#39;angolo superiore sinistro del AEM, toccate il logo AEM, quindi nella barra a sinistra, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse] > [!UICONTROL Predefiniti visualizzatore.]**
1. Nella pagina Predefinito visualizzatore, nell’intestazione della colonna **[!UICONTROL Stato]**, toccate l’opzione per attivare o disattivare un predefinito per visualizzatori.

   I predefiniti per visualizzatori attivati presentano l’interruttore a destra, all’interno di una casella blu; i predefiniti per visualizzatori disattivati presentano l’interruttore a sinistra, all’interno di una casella di colore grigio chiaro.

## Predefiniti visualizzatore di pubblicazione {#publishing-viewer-presets}

Attivando (o attivando &quot;Attivato&quot;) lo stato di un predefinito per visualizzatori significa che è visibile nel componente Contenuti multimediali dinamici, nel componente Contenuti multimediali interattivi e ogni volta che visualizzate una risorsa.

Tuttavia, per fornire* *una risorsa con un predefinito visualizzatore, è necessario pubblicare anche esso. Per ottenere l’URL o il codice da incorporare per una risorsa, tutti i predefiniti visualizzatore devono essere attivati *e* pubblicati. Devi attivare e pubblicare tutti i predefiniti visualizzatore che sono forniti con i Dynamic Media. I predefiniti visualizzatore personalizzati che crei e aggiungi vengono attivati automaticamente, ma devono anche essere pubblicati.

Consultate [Attivazione o disattivazione dei predefiniti per visualizzatori](#activating-or-deactivating-viewer-presets).

Vedere anche [Anteprima delle risorse](/help/assets/previewing-assets.md).

**Per pubblicare i predefiniti per visualizzatori**

1. Nell&#39;angolo superiore sinistro del AEM, toccate il logo AEM, quindi nella barra a sinistra, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse] > [!UICONTROL Predefiniti visualizzatore.]**
1. Selezionate uno o più predefiniti per visualizzatori da pubblicare.
1. Sulla barra degli strumenti, toccate l&#39;icona **[!UICONTROL Pubblica]**.

## Ordinamento dei predefiniti per visualizzatori {#sorting-viewer-presets}

1. Nell&#39;angolo superiore sinistro del AEM, toccate il logo AEM, quindi nella barra a sinistra, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse] > [!UICONTROL Predefiniti visualizzatore.]**
1. Per ordinare in base all’intestazione della colonna, fai clic su **[!UICONTROL Titolo del predefinito]**, **[!UICONTROL Tipo]**, **[!UICONTROL Pubblicato]** o **[!UICONTROL Stato]**. Ad esempio, fai clic su **[!UICONTROL Tipo]** per ordinare i tipi di predefiniti visualizzatore in ordine alfabetico o inverso.

## Modifica dei predefiniti per visualizzatori {#editing-viewer-presets}

Tenete presente che la modifica di eventuali predefiniti per visualizzatori *predefiniti* non è uno scenario supportato. Se modificate un predefinito per visualizzatori preimpostato, vi verrà richiesto di salvarlo con un nuovo nome.

**Per modificare i predefiniti per visualizzatori**

1. Nell&#39;angolo superiore sinistro del AEM, toccate il logo AEM, quindi nella barra a sinistra, toccate **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse] > [!UICONTROL Predefiniti visualizzatore.]**
1. Selezionate un predefinito selezionando la casella a sinistra del titolo del predefinito per visualizzatori.
1. Sulla barra degli strumenti, toccare **[!UICONTROL Modifica.]**
1. Nella pagina **[!UICONTROL Editor predefiniti per visualizzatore]**, apporta le modifiche necessarie al predefinito visualizzatore, utilizzando le opzioni disponibili nelle schede **[!UICONTROL Aspetto]** e **[!UICONTROL Comportamento]**.

   Dalla scheda **[!UICONTROL Aspetto]**, nell’angolo in alto a sinistra della pagina Editor predefiniti per visualizzatore, tocca **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** o **[!UICONTROL Telefono]** per modificare la modalità di presentazione della risorsa.

1. Nell’angolo superiore destro della pagina, effettuate una delle seguenti operazioni:

   * Toccate **[!UICONTROL Salva]** per salvare le modifiche e tornare alla pagina Predefinito visualizzatore.
   * Toccate **[!UICONTROL Annulla]** per annullare le modifiche apportate e tornare alla pagina Predefinito visualizzatore.

## Eliminazione dei predefiniti per visualizzatori personalizzati {#deleting-custom-viewer-presets}

Potete eliminare i predefiniti per visualizzatori creati e aggiunti agli elementi multimediali dinamici.

**Per eliminare i predefiniti per visualizzatori personalizzati**

1. Nell’angolo in alto a sinistra di AEM, tocca il logo AEM, quindi, nella barra a sinistra, seleziona **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse > Predefiniti visualizzatore.]**
1. Nella pagina Predefiniti visualizzatore, selezionate un titolo predefinito, quindi toccate l&#39;icona **[!UICONTROL Cestino]**.
1. Toccare **[!UICONTROL Elimina.]**

## Applicazione di un predefinito per visualizzatori a una risorsa {#applying-a-viewer-preset-to-an-asset}

Se hai già pubblicato sia la risorsa che il visualizzatore selezionato, dopo aver selezionato un predefinito visualizzatore vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL Incorpora]**.

**Per applicare un predefinito per visualizzatori a una risorsa**

1. Aprite la risorsa e, accanto all&#39;angolo superiore sinistro della pagina, toccate il menu a discesa, quindi selezionate **[!UICONTROL Visualizzatori.]**

   >[!NOTE]
   >
   >Se hai già pubblicato sia la risorsa che il visualizzatore selezionato, dopo aver selezionato un predefinito visualizzatore vengono visualizzati i pulsanti **[!UICONTROL URL]** e **[!UICONTROL Incorpora]**.

1. Selezionate un predefinito per visualizzatori dal riquadro a sinistra per applicarlo alla risorsa.

   Potete [copiare l&#39;URL da condividere](/help/assets/linking-urls-to-yourwebapplication.md) con altri utenti.

## Distribuzione delle risorse con i predefiniti per visualizzatori {#delivering-assets-with-viewer-presets}

Per ottenere gli URL per i predefiniti per visualizzatori, consultate [Collegamento degli URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md). Consultate anche [Incorporamento del visualizzatore video in una pagina Web](/help/assets/embed-code.md).

Se usate AEM WCM, potete aggiungere risorse utilizzando i predefiniti per visualizzatori direttamente sulla pagina. Consultate [Aggiunta di risorse multimediali dinamiche alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).
