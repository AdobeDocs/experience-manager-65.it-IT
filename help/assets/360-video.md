---
title: Video 360/VR
description: Scopri come utilizzare il 360 e il video VR (Virtual Reality) in Dynamic Media.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR Video
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: c0a60ec39e35fa8113ce9e1795561709b9c7e289
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# Video 360/VR {#vr-video}

I video a 360 gradi registrano una vista in ogni direzione contemporaneamente. Le riprese vengono effettuate utilizzando una telecamera omnidirezionale o una serie di telecamere. Durante la riproduzione su uno schermo piatto, l&#39;utente ha il controllo dell&#39;angolo di visione; le riproduzioni su dispositivi mobili usano solitamente i controlli giroscopici integrati.

La modalità Dynamic Media - Scene7 include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Puoi distribuire video 360 utilizzando le estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

Questa sezione descrive come lavorare con il visualizzatore video 360/VR per riprodurre video equirettangolari per un&#39;esperienza di visualizzazione coinvolgente di una stanza, una proprietà, una posizione, un paesaggio, una procedura medica e così via.

L&#39;audio spaziale non è attualmente supportato; se l&#39;audio è mixato in stereo, il bilanciamento (L/R) non cambia quando il cliente cambia l&#39;angolo di visualizzazione della telecamera.

Vedi anche [Gestione dei predefiniti per i visualizzatori](/help/assets/managing-viewer-presets.md).

## Video in azione a 360° {#video-in-action}

Seleziona [Stazione spaziale 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) per aprire una finestra del browser e guardare un video a 360 gradi. Durante la riproduzione di un video, trascinare il puntatore del mouse in una nuova posizione per modificare l&#39;angolo di visualizzazione.

![360-video campione con la stazione spaziale internazionale galleggiante nello spazio esterno e la terra e il sole dietro di esso.](assets/6_5_360videoiss_simplified.png)
*Fotogramma video da Space Station 360*

## Video e Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

È possibile utilizzare Adobe Premier Pro per visualizzare e modificare il metraggio 360/VR. Ad esempio, potete inserire correttamente loghi e testo in una scena e applicare effetti e transizioni progettati appositamente per gli elementi multimediali equirettangolari.

Consulta [Modifica video 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Carica le risorse da utilizzare con il visualizzatore video 360 {#uploading-assets-for-use-with-the-video-viewer}

360 risorse video caricate in Adobe Experience Manager sono etichettate come **Multimedia** su una pagina di risorse, come una normale risorsa video.

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*Una risorsa video 360 caricata visualizzata nella vista a schede. La risorsa è etichettata come Multimedia.*

**Carica le risorse da utilizzare con il visualizzatore video 360:**

1. È stata creata una cartella dedicata alla risorsa video 360.
1. [Applicare un profilo video adattivo alla cartella](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   Il rendering di contenuti video a 360° richiede requisiti più elevati per la risoluzione del video sorgente e delle rappresentazioni codificate rispetto ai contenuti video standard non a 360°.

   Puoi utilizzare il profilo video adattivo fornito con Dynamic Media. Tuttavia, risulta in una qualità video 360-inferiore rispetto a quella che si otterrebbe per un video non 360 codificato con le stesse impostazioni sottoposte a rendering con un visualizzatore video non 360. Pertanto, se è richiesta una qualità video 360 elevata, effettuare le seguenti operazioni:

   * Idealmente, il contenuto video originale a 360 è ideale per avere una delle seguenti risoluzioni:

      * 1080p - 1920 x 1080, risoluzione Full HD o FHD oppure
      * 2160p - 3840 x 2160, nota come risoluzione 4k, UHD o HD Ultra. Questa risoluzione elevata del display si trova più spesso su televisori e monitor per computer di alta qualità. La risoluzione 2160p è spesso chiamata &quot;4k&quot; perché la larghezza è vicina a 4000 pixel. In altre parole, offre quattro volte i pixel di 1080p.
   * [Creare un profilo video adattivo personalizzato](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) con rappresentazioni di qualità superiore. Ad esempio, crea un profilo video adattivo contenente le tre impostazioni seguenti:

      * width=auto; height=720; bitrate=2500 kbps
      * width=auto; height=1080; bitrate=5000 kbps
      * width=auto; height=1440; bitrate=6600 kbps
   * Elabora contenuti video 360 in una cartella dedicata esclusivamente alle risorse video 360.

   Questo approccio aumenta le esigenze della rete e della CPU dell&#39;utente finale.

1. [Carica il video nella cartella](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## Ignora le proporzioni predefinite di 360 video  {#overriding-the-default-aspect-ratio-of-videos}

Affinché una risorsa caricata possa essere considerata un video 360 che intendi utilizzare con il visualizzatore video 360, la risorsa deve avere proporzioni 2.

Per impostazione predefinita, Experience Manager rileva il video come &quot;360&quot; se le proporzioni (larghezza/altezza) sono 2,0. Se si è un amministratore, è possibile ignorare l&#39;impostazione di default delle proporzioni 2 impostando il `s7video360AR` proprietà in CRXDE Lite al seguente indirizzo:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Tipo di proprietà** - Doppio
   * **Valore** - proporzioni in virgola mobile, impostazione predefinita 2,0.

Dopo aver impostato questa proprietà, questa ha effetto immediato sia sui video esistenti che sui video appena caricati.

Le proporzioni si applicano alle risorse video 360 per la pagina dei dettagli della risorsa e [Componente WCM per contenuti video 360](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Per iniziare, carica 360 video.

## Anteprima video 360 {#previewing-video}

È possibile utilizzare Anteprima per vedere come si presenta il video 360 ai clienti e assicurarsi che si comporti come previsto.

Vedi anche [Modifica predefiniti visualizzatore](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

Quando sei soddisfatto del video 360, puoi pubblicarlo.

Consulta [Incorporare il visualizzatore di video o immagini in una pagina Web](/help/assets/embed-code.md).
Consulta [Collegare gli URL all’applicazione web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Consulta [Aggiungere risorse Dynamic Media alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Per visualizzare l&#39;anteprima di un video a 360°:**

1. In entrata **[!UICONTROL Risorse]**, passa a un video 360 esistente creato. Seleziona la risorsa video 360 per aprirla in modalità anteprima.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Seleziona la risorsa video 360 per visualizzare l’anteprima del video.

1. Nella pagina di anteprima, nell’angolo superiore sinistro della pagina, seleziona l’elenco a discesa, quindi fai clic su **[!UICONTROL Visualizzatori]**.

   ![6_5_360visualizzatori-anteprima-video](assets/6_5_360video-preview-viewers.png)

   Dall’elenco Visualizzatori, seleziona **[!UICONTROL Video360_social]**, quindi eseguire una delle operazioni seguenti:

   * Trascinare il puntatore del mouse sul video per modificare l&#39;angolo di visualizzazione della scena statica.
   * Seleziona il **[!UICONTROL Play]** per iniziare la riproduzione. Durante la riproduzione del video, trascinare il puntatore del mouse sul video per modificare l&#39;angolo di visualizzazione.

   ![Uno screenshot della stazione spaziale internazionale che galleggia nello spazio con la terra e il sole sullo sfondo ](assets/6_5_360video-preview-video360-social.png)*Una schermata di 360 video.*

   * Dall’elenco Visualizzatori, seleziona **[!UICONTROL Video360VR]**.

      Il video VR (Virtual Reality) è un video coinvolgente a cui si accede utilizzando cuffie per realtà virtuale. Come per i video ordinari, puoi creare video VR all’inizio quando un video viene registrato o catturato utilizzando videocamere a 360 gradi.
   ![Schermata di un primo piano della stazione spaziale internazionale galleggiante nello spazio con la terra e il sole parzialmente visibili sullo sfondo](assets/6_5_360video-preview-video360vr.png)
   *Una schermata video 360 VR.*

1. Nella parte superiore destra della pagina di anteprima, seleziona **[!UICONTROL Chiudi]**.

## Pubblicazione di video 360 {#publishing-video}

Pubblica il video 360 in modo da poterlo utilizzare. La pubblicazione di un video 360 attiva l’URL e il codice di incorporamento. Pubblica inoltre il video 360 sul cloud Dynamic Media, integrato con una rete CDN per una distribuzione scalabile e performante.

Consulta [Pubblicare risorse Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate su come pubblicare video a 360°.
Vedi anche [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md).
Vedi anche [Collegare gli URL all’applicazione web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo presenta collegamenti con URL relativi, in particolare collegamenti a pagine Experience Manager Sites.
Vedi anche [Aggiungere risorse Dynamic Media alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).
