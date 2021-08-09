---
title: Collegamento di URL all’applicazione web
description: Come collegare gli URL alla tua applicazione web in Dynamic Media
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configurazione
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 10%

---

# Collegamento di URL all’applicazione web {#linking-urls-to-your-web-application}

I siti web e le applicazioni accedono ai servizi Dynamic Media tramite chiamate URL. Dopo la pubblicazione di una risorsa, Dynamic Media attiva una stringa URL che fa riferimento a tale risorsa. Puoi incollare questi URL in un browser web per eseguire test.

Puoi effettuare il collegamento agli URL solo se *non* utilizzi Experience Manager come WCM. Il collegamento (rispetto a incorporamento) viene utilizzato quando si desidera distribuire un lettore video come finestra a comparsa o modale. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente sulla pagina](adding-dynamic-media-assets-to-pages.md).

Per inserire queste stringhe URL nelle pagine web e nelle applicazioni, copiale da Dynamic Media.

>[!NOTE]
>
>Le stringhe URL sono disponibili solo per le rappresentazioni dinamiche delle risorse. Al momento non sono disponibili per le risorse statiche che risiedono in DAM e non nel server Dynamic Media. Il pulsante URL non viene visualizzato per le rappresentazioni statiche.

Vedere anche [Incorporamento del visualizzatore di video o immagini in una pagina Web](embed-code.md).

Consulta anche [Collegamento di URL YouTube all&#39;applicazione Web](video.md).

Vedi anche [Distribuzione di immagini ottimizzate per un sito reattivo](responsive-site.md).

Consulta anche [Caricamento delle risorse](manage-assets.md#uploading-assets).

## Ottenimento di un URL per una risorsa {#obtaining-a-url-for-an-asset}

Puoi ottenere una stringa URL generata da un predefinito per immagini o da un predefinito per visualizzatori. Dopo aver copiato l’URL, questo viene inserito negli Appunti in modo da poterlo incollare come necessario nelle pagine del sito web o dell’applicazione.

>[!NOTE]
>
>L’URL può essere copiato solo dopo la pubblicazione della risorsa selezionata. Inoltre, devi pubblicare il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).
>
>Consulta [Pubblicazione dei predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblicazione di predefiniti immagine](managing-image-presets.md#publishing-image-presets).

Esistono diversi modi per ottenere una stringa URL. Tuttavia, i passaggi seguenti mostrano un solo metodo possibile.

**Per ottenere un URL per una risorsa**

1. Passa alla risorsa *pubblicata* il cui URL predefinito per immagini o URL predefinito per visualizzatori da copiare, quindi tocca la risorsa per aprirla.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consulta [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).

   Consulta [Pubblicazione dei predefiniti visualizzatore](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblicazione di predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. In base alla risorsa selezionata, effettua una delle seguenti operazioni:

   * Se hai selezionato un’immagine, nel menu a discesa tocca **[!UICONTROL Rappresentazioni]**.

      Sotto l’intestazione **[!UICONTROL Dinamico]**, tocca un nome predefinito per visualizzarne il rendering nel fotogramma giusto. Se necessario, scorri l’elenco Rendering per visualizzare l’intestazione Dinamica .

      Nella parte inferiore della barra a sinistra, tocca **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se hai selezionato un set 360 gradi, un set di immagini, un set carosello o un video, nel menu a discesa tocca **[!UICONTROL Visualizzatori]**.

      Nella barra a sinistra, tocca un nome predefinito per visualizzatori. Un&#39;anteprima del set o del video viene aperta in una pagina separata.

      Nella barra a sinistra, nella parte inferiore, tocca **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Seleziona e copia il testo nel browser web in modo da poter visualizzare l’anteprima della risorsa o aggiungerla alla pagina del contenuto web.

   Per uscire dalla finestra URL, tocca **[!UICONTROL X]** o tocca **[!UICONTROL Chiudi]**.

## Ottenimento di un URL per una risorsa statica {#obtaining-a-url-for-a-static-asset}

Dynamic Media supporta la distribuzione di risorse statiche, che sono risorse aggiuntive oltre alle sole immagini e ai video. I formati di risorse statiche supportati per la distribuzione includono:

* File 3D
* GIF animata
* File audio
* CSS
* JavaScript (quando la società è configurata con un proprio dominio)
* PDF
* SVG
* XML
* ZIP

**Per ottenere un URL per una risorsa statica**

1. Passa alla risorsa statica *pubblicata* di cui desideri copiare l’URL e tocca la risorsa per aprirla.

   Gli URL sono disponibili solo per copiare *dopo* la prima *pubblicazione* risorsa statica.

   Consulta [Pubblicazione di risorse](publishing-dynamicmedia-assets.md).

1. Utilizza uno dei seguenti metodi per ottenere l’URL della risorsa statica pubblicata:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Esempio, `https://aem.com/is/content/adobe/image.gif`.
   * Tocca **[!UICONTROL Risorsa > Rendering dinamici]**, quindi tocca un rendering dinamico della risorsa statica e copia l’URL.

      Modifica l’URL copiato in modo che utilizzi `is/content` nel percorso invece di `is/image/`.


## Ottenimento di un URL video per un rendering video pubblicato {#obtaining-a-video-url-for-a-published-video-rendition}

1. Ad Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all’intestazione **[!UICONTROL Servizi cloud per elementi multimediali dinamici]**, quindi tocca **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, tocca il nome della configurazione desiderata.

1. Nella pagina **[!UICONTROL Impostazioni di Dynamic Media Cloud]**, in **[!UICONTROL URL del servizio video]**, copia l’intero percorso URL. Devi visualizzare l’URL copiato più avanti nei passaggi descritti.

   Ad esempio, il percorso URL potrebbe essere simile al seguente:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (Il percorso sopra è solo un esempio; non è il percorso effettivo copiato.)

1. In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID.

   Ad esempio, se l’ID di registrazione era `87654321|MyCompany`, il nome del cliente sarebbe `MyCompany`.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Cloud Services]**, quindi tocca il logo dell’Experience Manager e passa a **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Copia l’intero percorso di rendering video dal JCR (Java™ Content Repository).

   Ad esempio, il percorso di rendering del video potrebbe essere simile al seguente:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (Il percorso sopra è solo un esempio; non è il percorso effettivo copiato.)

1. Disporre le informazioni copiate nel seguente ordine in modo che formi un percorso URL completo:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Ad esempio, utilizzando i percorsi di esempio e il nome del cliente di esempio dei passaggi precedenti, il percorso completo viene visualizzato come segue:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Questo esempio è l’URL video completo per un rendering video pubblicato.

## Ottenimento di un URL video per lo streaming adattivo (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. Ad Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all’intestazione **[!UICONTROL Servizi cloud per elementi multimediali dinamici]**, quindi tocca **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, tocca il nome della configurazione desiderata.
1. Nella pagina **[!UICONTROL Impostazioni Cloud Services Dynamic Media]** , procedi come segue:

   * In **[!UICONTROL URL servizio video]**, copia l’intero percorso URL. Successivamente, segui il percorso dell’URL copiato in questi passaggi. Ad esempio, il percorso URL potrebbe essere simile al seguente:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (Il percorso sopra è solo un esempio; non è il percorso effettivo copiato.)

   * In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID. Successivamente, è necessario copiare il nome del cliente in questi passaggi.

      Ad esempio, se l’ID di registrazione è `87654321|demoCo`, il nome del cliente copiato sarà `demoCo`.


1. In base al protocollo di consegna video utilizzato, copia il rispettivo selettore di protocollo. Successivamente, è necessario utilizzare il selettore di protocollo copiato in questi passaggi.

   | Protocollo di distribuzione video utilizzato | Selettore di protocollo da utilizzare |
   |---|---|
   | HTTP <br> Se utilizzi HTTP (distribuzione video non protetta), assicurati di modificare https in http nel valore URL del servizio video copiato in precedenza. | `public/` |
   | HTTPS | `public-ssl/` |

1. Copia il percorso completo della risorsa video in Experience Manager, come elaborato da Dynamic Media. In seguito, segui questi passaggi per trovare il percorso della risorsa video copiata.

   Esempio:

   `/content/dam/marketing/MyVideo.mp4`

1. Combina tutti gli elementi copiati in precedenza per creare una stringa nell&#39;ordine seguente:

   &lt;>>&lt;> > &lt;> > &lt;>>`video service URL``protocol selector``customer name``video asset path`

   Ad esempio, utilizzando le informazioni copiate dagli esempi descritti in questi passaggi, la stringa verrà visualizzata come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Completa l’URL aggiungendo `.m3u8` alla fine della stringa. Ad esempio, aggiungendo `.m3u8` alla stringa del passaggio precedente, il percorso completo dell’URL verrà visualizzato come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Utilizzo di HTTP/2 per fornire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media può ora avvenire tramite HTTP/2, garantendo tempi di risposta e caricamento migliori.

Per informazioni dettagliate su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media, consulta [Distribuzione di contenuti HTTP2](http2.md) .
