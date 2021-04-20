---
title: Video 360/VR
description: Scopri come lavorare con i video 360 e Virtual Reality (VR) in Dynamic Media.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR Video
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---


# Video 360/VR {#vr-video}

I video a 360 gradi registrano contemporaneamente una visualizzazione in ogni direzione. Le riprese vengono effettuate con una telecamera omnidirezionale o con una serie di telecamere. Durante la riproduzione su un display piatto l&#39;utente ha il controllo dell&#39;angolo di visione; la riproduzione su dispositivi mobili solitamente sfrutta i controlli giroscopici incorporati.

La modalità Dynamic Media - Scene7 include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. È possibile distribuire video 360 utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

Questa sezione descrive come lavorare con il visualizzatore video 360/VR per riprodurre video equirettangolari per un’esperienza di visualizzazione coinvolgente di una stanza, una proprietà, un luogo, un paesaggio, una procedura medica e così via.

L&#39;audio spaziale non è attualmente supportato; se l&#39;audio è mixato in stereo, il bilanciamento (L/R) non cambia quando il cliente cambia l&#39;angolo di visione della telecamera.

Consulta anche [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

## 360 Video in azione {#video-in-action}

Toccare [Stazione Spaziale 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) per aprire una finestra del browser e guardare un video a 360 gradi. Durante la riproduzione del video, trascinare il puntatore del mouse in una nuova posizione per modificare l&#39;angolo di visualizzazione.

![360 Video ](assets/6_5_360videoiss_simplified.png)
*campioneFrame video da Space Station 360*

## Video e Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

È possibile utilizzare Adobe Premier Pro per visualizzare e modificare le riprese a 360/VR. Ad esempio, è possibile inserire correttamente loghi e testo in una scena e applicare effetti e transizioni progettati appositamente per i supporti equirettangolari.

Vedi [Modifica video 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Caricamento delle risorse da utilizzare con il visualizzatore video 360 {#uploading-assets-for-use-with-the-video-viewer}

360 risorse video caricate in AEM sono etichettate come **Multimedia** in una pagina delle risorse, in modo simile alla normale risorsa video.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selecttopreviewUna risorsa video 360 caricata visualizzata nella vista a schede. La risorsa è etichettata come Multimedia.*

**Per caricare le risorse da utilizzare con il visualizzatore video 360:**

1. È stata creata una cartella dedicata alla risorsa video 360.
1. [Applica un profilo video adattivo alla cartella.](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)

   Il rendering di contenuti video a 360° richiede una risoluzione video sorgente e una risoluzione delle rappresentazioni codificate superiori a quella dei contenuti video standard non a 360°.

   Puoi utilizzare il profilo video adattivo predefinito già fornito con Dynamic Media. Tuttavia, è importante notare che si otterrà una qualità video di 360 livelli notevolmente inferiori rispetto a quella dei video non-360 codificati con le stesse impostazioni renderizzate con un visualizzatore video non-360. Pertanto, se è necessario un video di alta qualità 360, procedi come segue:

   * Idealmente, il contenuto video 360 originale dovrebbe avere una delle seguenti risoluzioni:

      * 1080p - 1920 x 1080, noto come risoluzione Full HD o FHD o,
      * 2160p - 3840 x 2160, noto come risoluzione 4K, UHD o HD Ultra. Questa grande risoluzione del display si trova più spesso su televisori premium e monitor per computer. La risoluzione 2160p viene spesso chiamata &quot;4K&quot; perché la larghezza è vicina a 4000 pixel. In altre parole, offre quattro volte i pixel di 1080p.
   * [Crea un ](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) profilo video adattivo personalizzato con rappresentazioni di qualità superiore. Ad esempio, puoi creare un profilo video adattivo contenente le tre impostazioni seguenti:

      * width=auto; height=720; bitrate=2500 kbps
      * width=auto; height=1080; bitrate=5000 kbps
      * width=auto; height=1440; bitrate=6600 kbps
   * Elabora 360 contenuti video in una cartella dedicata esclusivamente a 360 risorse video.

   Tieni presente che questo approccio richiederà anche maggiori richieste alla rete e alla CPU dell’utente finale.

1. [Carica il video nella cartella](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## Ignorare le proporzioni predefinite di 360 video {#overriding-the-default-aspect-ratio-of-videos}

Affinché una risorsa caricata possa qualificarsi come video 360 da usare con il visualizzatore video 360, la risorsa deve avere una proporzione di 2.

Per impostazione predefinita, AEM rileva il video come &quot;360&quot; se il suo rapporto di formato (larghezza/altezza) è 2,0. Se sei un amministratore, puoi ignorare l’impostazione predefinita del rapporto di formato 2 impostando la proprietà opzionale `s7video360AR` in CRXDE Lite come segue:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Tipo** di proprietà: Doppio
   * **Valore**: rapporto di formato a virgola mobile, predefinito 2.0.

Dopo aver impostato questa proprietà, essa ha effetto immediatamente sia sui video esistenti che sui video appena caricati.

Il rapporto di formato si applica a 360 risorse video per la pagina dei dettagli della risorsa e al componente [Video 360 Media WCM](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Inizia caricando 360 video.

## Anteprima dei video 360 {#previewing-video}

Puoi usare Anteprima per vedere come si presenta ai clienti il tuo video 360 e assicurarti che funzioni come previsto.

Consulta anche [Modifica dei predefiniti visualizzatore](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

Quando sei soddisfatto del video 360, puoi pubblicarlo.

Consulta [Incorporamento del visualizzatore di video o immagini in una pagina web.](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)
Consulta  [Collegamento di URL all’applicazione web](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine AEM Sites.
Consulta [Aggiunta di risorse Dynamic Media alle pagine.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)

**Per visualizzare in anteprima 360 video**

1. In **[!UICONTROL Risorse]**, individua un video 360 esistente creato. Tocca la risorsa video 360 per aprirla in modalità anteprima.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Tocca la risorsa video 360 per visualizzare l’anteprima del video.

1. Nella pagina di anteprima, nell’angolo in alto a sinistra della pagina, tocca l’elenco a discesa, quindi seleziona **[!UICONTROL Visualizzatori.]**

   ![6_5_360visualizzatori di anteprima video](assets/6_5_360video-preview-viewers.png)

   Dall’elenco Visualizzatori, tocca **[!UICONTROL Video360_social]**, quindi effettua una delle seguenti operazioni:

   * Trascinare il puntatore del mouse sul video per modificare l&#39;angolo di visualizzazione della scena statica.
   * Toccare il pulsante **[!UICONTROL Play]** del video per iniziare la riproduzione; durante la riproduzione del video, trascinare il puntatore del mouse sul video per modificare l&#39;angolo di visualizzazione.

   ![Schermata video 6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360.*

   * Dall&#39;elenco Visualizzatori, tocca **[!UICONTROL Video360VR.]**

      Il video Virtual Reality (VR) è un video coinvolgente a cui si accede tramite l&#39;utilizzo di cuffie di realtà virtuale. Come per i video ordinari, si creano video VR all&#39;inizio quando un video viene registrato o catturato utilizzando videocamere a 360 gradi.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Schermata video VR a 360°.*

1. Vicino all&#39;angolo superiore destro della pagina di anteprima, tocca **[!UICONTROL Chiudi.]**

## Pubblicazione di video 360 {#publishing-video}

Per utilizzarlo, è necessario pubblicare il video 360. La pubblicazione di un video 360 attiva l’URL e il codice di incorporamento. Pubblica anche il video 360 sul cloud Dynamic Media, integrato con una rete CDN per una distribuzione scalabile e performante.

Per informazioni dettagliate su come pubblicare video 360, consulta [Pubblicazione di risorse Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md) .
Vedere anche [Incorporamento del visualizzatore di video o immagini in una pagina Web](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html).
Consulta anche [Collegamento di URL all&#39;applicazione web](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine AEM Sites.
Consulta anche [Aggiunta di risorse Dynamic Media alle pagine.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)
