---
title: Video in Dynamic Media
description: Scopri come utilizzare i video in Dynamic Media, ad esempio come best practice per codificare i video, pubblicare video in YouTube e visualizzare rapporti video. Scopri anche come aggiungere sottotitoli, sottotitoli o marcatori capitolo ai video.
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: a95255594ec03c152cd96df48597ced5fce4b315
workflow-type: tm+mt
source-wordcount: '8066'
ht-degree: 3%

---

# Video in Dynamic Media {#video}

Questa sezione descrive come lavorare con i video in Dynamic Media.

## Guida introduttiva: Video {#quick-start-videos}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a utilizzare i set video adattivi in Dynamic Media. Dopo ogni passaggio, sono disponibili riferimenti incrociati alle intestazioni degli argomenti in cui è possibile trovare ulteriori informazioni.

>[!IMPORTANT]
>
>Prima di lavorare con i video in Dynamic Media, accertati che l’amministratore di Adobe Experience Manager abbia già abilitato e configurato i Cloud Services Dynamic Media in modalità Dynamic Media - Scene7 o Dynamic Media - Hybrid.
>
>* Consulta [Configurare Cloud Services Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media - Modalità Scene7 e [Risoluzione dei problemi di Dynamic Media - Modalità Scene7](/help/assets/troubleshoot-dms7.md).
>
>* Consulta [Configurare Cloud Services Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media - Modalità ibrida.
>
>Problema di riproduzione video attualmente noto in Dynamic Media *solo sull&#39;Experience Manager 6.5.9.0*:
>
>* Se un video pubblicato viene aggiornato, deve essere pubblicato nuovamente per riflettere le modifiche alla consegna.
>


1. **Carica i video Dynamic Media** effettuando le seguenti operazioni:

   * Crea un tuo profilo di codifica video. Oppure, puoi semplicemente utilizzare il predefinito _Codifica video adattiva_ profilo fornito con Dynamic Media.

      * [Creare un profilo di codifica video](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Ulteriori informazioni su [Best practice per la codifica video](#best-practices-for-encoding-videos).
   * Associa il profilo di elaborazione video a una o più cartelle in cui stai per caricare i video sorgente principali.

      * [Applicare un profilo video alle cartelle](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * Ulteriori informazioni su [Best practice per organizzare le risorse digitali per utilizzare i profili di elaborazione](/help/assets/organize-assets.md).
      * Ulteriori informazioni su [Organizzare le risorse digitali](/help/assets/organize-assets.md).
   * Carica i video sorgente principali nelle cartelle. Quando aggiungi video alla cartella, questi vengono codificati in base al profilo di elaborazione video assegnato alla cartella.

      * Dynamic Media supporta principalmente video in formato breve con una durata massima di 30 minuti e una risoluzione minima superiore a 25 x 25.
      * Puoi caricare file video con una capacità massima di 15 GB ciascuno.
      * [Carica i video](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * Ulteriori informazioni su [Formati di file di input supportati](/help/assets/assets-formats.md#supported-multimedia-formats).
   * Monitorare come [codifica video in corso](#monitoring-video-encoding-and-youtube-publishing-progress) dalla vista delle risorse o del flusso di lavoro.




1. **Gestire i video Dynamic Media** effettuando una delle seguenti operazioni:

   * Organizzare, sfogliare e cercare risorse video

      * [Organizzare le risorse digitali](/help/assets/organize-assets.md)
Ulteriori informazioni su [Best practice per organizzare le risorse digitali per utilizzare i profili di elaborazione](organize-assets.md)

      * [Cercare risorse video](search-assets.md#custompredicates) o [Cercare risorse](/help/assets/search-assets.md)
   * Visualizzare in anteprima e pubblicare le risorse video

      * Visualizza il video sorgente e le rappresentazioni codificate del video insieme alle miniature associate:
         [Anteprima video](managing-video-assets.md#upload-and-preview-video-assets) o [Visualizzare in anteprima le risorse](previewing-assets.md)
         [Visualizza rappresentazioni video](video-renditions.md)
         [Gestire le rappresentazioni video](manage-assets.md#managing-renditions)

      * [Gestire i predefiniti visualizzatore](managing-viewer-presets.md)
      * [Pubblicare le risorse](publishing-dynamicmedia-assets.md)
   * Utilizzare i metadati video

      * Visualizza le proprietà di un rendering video codificato come frame rate, bitrate audio e video e codec:
         [Visualizzare le proprietà della rappresentazione video](video-renditions.md)

      * Modifica le proprietà del video come il titolo, la descrizione, i tag e i campi di metadati personalizzati:
         [Modifica proprietà video](manage-assets.md#editing-properties)

      * [Gestire i metadati per le risorse digitali](metadata.md)
      * [Schemi di metadati](metadata-schemas.md)
   * Rivedi, approva e commenta video e mantieni il controllo completo della versione

      * [Annotare i video](managing-video-assets.md#annotate-video-assets) o [Annotare risorse](manage-assets.md#annotating)

      * [Crea una versione](manage-assets.md#asset-versioning)
      * [Applicare i flussi di lavoro alle risorse](assets-workflow.md) o vedi [Avviare un flusso di lavoro su una risorsa](manage-assets.md#starting-a-workflow-on-an-asset)

      * [Esaminare le risorse della cartella](bulk-approval.md)
      * [Progetti](../sites-authoring/projects.md)




1. **Pubblicare i video Dynamic Media** effettuando una delle seguenti operazioni:

   * Se utilizzi Adobe Experience Manager come sistema di gestione dei contenuti web, puoi aggiungere video direttamente alle pagine web.

      * [Aggiungere video alle pagine web](adding-dynamic-media-assets-to-pages.md).
   * Se utilizzi un sistema di gestione dei contenuti web di terze parti, puoi collegare o incorporare video nelle pagine web.

      * Integra video tramite URL:
         [Collegamento degli URL all’applicazione Web](linking-urls-to-yourwebapplication.md).

      * Integra il video utilizzando il codice di incorporamento nella pagina web:
         [Incorporare il visualizzatore video in una pagina web](embed-code.md).
   * [Generare rapporti video](#viewing-video-reports).

   * [Aggiungi didascalie al video](#adding-captions-to-video).



## Utilizzare i video in Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media è una soluzione end-to-end che consente di pubblicare facilmente video adattivi di alta qualità per lo streaming su più schermi, tra cui desktop, iOS, Android™, BlackBerry® e dispositivi mobili Windows. Un set video adattivo raggruppa le versioni dello stesso video che sono codificate in diversi formati e bit rate, ad esempio 400 kbps, 800 kbps e 1000 kbps. Il computer desktop o il dispositivo mobile rileva la larghezza di banda disponibile.

Ad esempio, su un dispositivo mobile iOS rileva una larghezza di banda come 3G, 4G o Wi-Fi. Quindi seleziona automaticamente il video codificato giusto tra i vari bit rate video all’interno del set video adattivo. Il video viene inviato in streaming a desktop, dispositivi mobili o tablet.

Inoltre, la qualità video viene commutata automaticamente se cambiano le condizioni di rete sul desktop o sul dispositivo mobile. Inoltre, se un cliente entra in modalità a tutto schermo su un desktop, il set video adattivo risponde con una risoluzione migliore, migliorando l’esperienza di visualizzazione del cliente. L’utilizzo di set video adattivi offre la migliore riproduzione possibile per i clienti che riproducono video Dynamic Media su più schermi e dispositivi.

La logica utilizzata da un lettore video per determinare quale video codificato riprodurre o selezionare durante la riproduzione si basa sul seguente algoritmo:

1. Il lettore video carica il frammento video iniziale in base al bitrate più vicino al valore impostato per &quot;bitrate iniziale&quot; nel lettore stesso.
1. Il lettore video cambia in base alle modifiche apportate alla velocità della larghezza di banda utilizzando i seguenti criteri:

   1. Il lettore sceglie il flusso di larghezza di banda più alto al di sotto o uguale alla larghezza di banda stimata.
   1. Il lettore considera solo l&#39;80% della larghezza di banda disponibile. Tuttavia, in caso di passaggio, è più prudente con solo il 70% per evitare di sovrastimare e tornare subito indietro.

Per informazioni tecniche dettagliate sull’algoritmo, consulta [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Per la gestione di set video singoli e adattivi, sono supportati i seguenti elementi:

* Caricamento di video da numerosi formati video supportati e formati audio e codifica video in formato MP4 H.264 per la riproduzione su più schermi. È possibile utilizzare predefiniti per video adattivi, predefiniti per codifica video singola o personalizzare la propria codifica per controllare la qualità e le dimensioni del video.

   * Quando viene generato un set video adattivo, questo include video MP4.
   * **Nota**: i video principali/sorgenti non vengono aggiunti a un set di video adattivi.

* Sottotitoli video in tutti i visualizzatori video di HTML5.
* Organizza, sfoglia e cerca video con supporto completo per i metadati, per una gestione efficiente delle risorse video.
* Distribuisci set video adattivi sul web, sui desktop e sui dispositivi mobili, inclusi iPhone, iPad, Android™, BlackBerry® e Windows Phone.

Lo streaming video adattivo è supportato su varie piattaforme iOS. Consulta [Guida di riferimento per i visualizzatori di Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media supporta la riproduzione di video per dispositivi mobili per video MP4 H.264. È possibile trovare i dispositivi BlackBerry® che supportano questo formato video al seguente indirizzo: [Formati video supportati su BlackBerry®](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

I dispositivi Windows che supportano questo formato video sono disponibili nei seguenti percorsi: [Codec multimediali supportati per Windows Phone 8](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)

* Riproduci il video utilizzando i predefiniti visualizzatore video Dynamic Media, inclusi i seguenti elementi:

   * Visualizzatori video singoli.
   * Visualizzatori di file multimediali diversi che combinano contenuti sia video che immagini.

* Configura i lettori video in base alle tue esigenze di branding.
* Integra il video nel tuo sito web, sito mobile o app mobile con un semplice URL o codice da incorporare.

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Vedi anche [Visualizzatori per Experience Manager Assets e Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) e [Visualizzatori solo per risorse di Experience Manager](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## Best practice: utilizzo del visualizzatore video di HTML5 {#best-practice-using-the-html-video-viewer}

I predefiniti visualizzatore video di Dynamic Media HTML5 sono lettori video affidabili. Puoi utilizzarli per evitare molti problemi comuni associati alla riproduzione di video HTML5. Inoltre, problemi associati ai dispositivi mobili come la mancanza di distribuzione di streaming bitrate adattivo e la portata limitata del browser desktop.

Dal lato della progettazione del lettore, puoi progettare le funzionalità del lettore video utilizzando gli strumenti di sviluppo web standard. Ad esempio, puoi progettare pulsanti, controlli e sfondo personalizzato per l’immagine del poster utilizzando HTML5 e CSS per raggiungere i clienti con un aspetto personalizzato.

Sul lato di riproduzione del visualizzatore, rileva automaticamente la funzionalità video del browser. Distribuisce quindi il video utilizzando HLS (HTTP Live Streaming) o DASH (Dynamic Adaptive Streaming over HTTP) , noto anche come streaming bitrate adattivo. Oppure, se tali metodi di consegna non sono presenti, viene utilizzato invece HTML5 progressive.

Combinando in un singolo lettore quanto segue:

* Possibilità di progettare i componenti di riproduzione utilizzando HTML5 e CSS
* Avere riproduzione incorporata
* Utilizza lo streaming adattivo e progressivo a seconda delle funzionalità del browser

È possibile estendere la portata dei contenuti rich media agli utenti desktop e mobili e garantire un&#39;esperienza video semplificata.

Vedi anche [Informazioni sui visualizzatori HTML5](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### Riproduzione di video su computer desktop e dispositivi mobili mediante il visualizzatore video di HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

Per lo streaming video adattivo per desktop e dispositivi mobili, i video utilizzati per il passaggio a bit rate si basano su tutti i video MP4 nel set di video adattivi.

La riproduzione video viene eseguita utilizzando DASH o HLS oppure tramite download progressivo di video. Nelle versioni precedenti di Experience Manager, come 6.0, 6.1 e 6.2, i video venivano inviati in streaming tramite HTTP.

Nell’Experience Manager 6.3 e versioni successive, i video vengono ora inviati in streaming tramite HTTPS (ovvero DASH o HLS) perché l’URL del servizio gateway DM utilizza sempre anche HTTPS. Questo comportamento predefinito non ha alcun impatto sul cliente. In altre parole, lo streaming video si verifica sempre tramite HTTPS, a meno che non sia supportato dal browser. (vedere la tabella seguente). Pertanto,

* Se disponi di un sito web HTTPS con streaming video HTTPS, lo streaming va bene.
* Se disponi di un sito web HTTP con streaming video HTTPS, lo streaming va bene e non vi sono problemi di contenuti misti dal browser web.

DASH è lo standard internazionale e HLS è uno standard Apple. Entrambi vengono utilizzati per lo streaming video adattivo. Entrambe le tecnologie regolano automaticamente la riproduzione in base alla capacità della larghezza di banda della rete. Consente inoltre al cliente di &quot;cercare&quot; in qualsiasi punto del video senza dover attendere il download del resto del video.

Il video progressivo viene distribuito scaricando e memorizzando il video localmente sul sistema desktop o sul dispositivo mobile di un utente.

La tabella seguente descrive il dispositivo, il browser e il metodo di riproduzione dei video su computer desktop e dispositivi mobili che utilizzano il Visualizzatore video di Dynamic Media.

<table>
 <tbody>
  <tr>
   <td><strong>Dispositivo</strong></td>
   <td><strong>Browser</strong></td>
   <td><strong>Modalità di riproduzione video</strong></td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Internet Explorer 9 e 10</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Internet Explorer 11+</td>
   <td>In Windows 8 e Windows 10 - Forza l’utilizzo di HTTPS ogni volta che viene richiesto DASH* o HLS. Limitazione nota: HTTP su DASH* o HLS non funziona in questa combinazione browser/sistema operativo<br /> <br /> Su Windows 7 - Download progressivo. Utilizza la logica standard per selezionare il protocollo HTTP rispetto al protocollo HTTPS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 23-44</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Firefox 45 o versione successiva</td>
   <td>Streaming del bitrate adattivo DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Chrome</td>
   <td>Streaming del bitrate adattivo DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Desktop</td>
   <td>Safari (Mac)</td>
   <td>Streaming del bitrate adattivo HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (Android™ 6 o versioni precedenti)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (Android™ 7 o versione successiva)</td>
   <td>Streaming del bitrate adattivo DASH* o HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Android™ (browser predefinito)</td>
   <td>Download progressivo.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Safari (iOS)</td>
   <td>Streaming del bitrate adattivo HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Chrome (iOS)</td>
   <td>Streaming del bitrate adattivo HLS.</td>
  </tr>
  <tr>
   <td>Mobile</td>
   <td>Blackberry®</td>
   <td>Streaming del bitrate adattivo DASH* o HLS./td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Per utilizzare DASH per i video, è necessario prima attivarlo con l&#39;assistenza tecnica Adobe sul tuo account. Consulta [Abilita DASH sul tuo account](#enable-dash).

## Architettura della soluzione video Dynamic Media {#architecture-of-dynamic-media-video-solution}

L’immagine seguente mostra il flusso di lavoro complessivo per l’authoring dei video caricati e codificati tramite DMGateway (in modalità ibrida Dynamic Media) e resi disponibili al pubblico.

![chlimage_1-427](assets/chlimage_1-427.png)

## Architettura di pubblicazione ibrida per video {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Best practice per la codifica dei video {#best-practices-for-encoding-videos}

Il **Codifica video Dynamic Media** se hai attivato Dynamic Media e hai impostato video cloud services, workflow codifica video. Questo flusso di lavoro acquisisce la cronologia del processo del flusso di lavoro e le informazioni di errore. Se hai abilitato Dynamic Media e hai impostato Cloud Services per i video, il **[!UICONTROL Codifica video Dynamic Media]** il flusso di lavoro viene applicato automaticamente al caricamento di un video. Se non utilizzi Dynamic Media, il **[!UICONTROL Aggiorna risorsa DAM]** il flusso di lavoro ha effetto.)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### File video sorgente {#source-video-files}

Quando codificate un file video, utilizzate un file video sorgente della massima qualità possibile. Evita di utilizzare file video codificati in precedenza perché sono già compressi e un’ulteriore codifica crea un video di qualità inferiore.

* Dynamic Media supporta principalmente video in formato breve con una durata massima di 30 minuti e una risoluzione minima superiore a 25 x 25.
* È possibile caricare file video di origine primari fino a 15 GB ciascuno.

La tabella seguente descrive le dimensioni, le proporzioni e la velocità bit minima consigliate per i file video sorgente prima di codificarli:

| Dimensione | Proporzioni | Velocità bit minima |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps per la maggior parte dei video. |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps, in base alla quantità di movimento nel video. |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps, a seconda della quantità di movimento nel video. |

### Ottenere i metadati di un file {#obtaining-a-file-s-metadata}

È possibile ottenere i metadati di un file visualizzandone i metadati mediante uno strumento di modifica video o un&#39;applicazione progettata per ottenere i metadati. Di seguito sono riportate le istruzioni per l’utilizzo di MediaInfo, un’applicazione di terze parti, per ottenere i metadati di un file video:

1. Vai a [Download di MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Selezionare e scaricare il programma di installazione per la versione GUI e seguire le istruzioni di installazione.
1. Dopo l&#39;installazione, fare clic con il pulsante destro del mouse sul file video (solo Windows) e selezionare MediaInfo, oppure aprire MediaInfo e trascinare il file video nell&#39;applicazione. Puoi visualizzare tutti i metadati associati al file video, compresi quelli relativi a larghezza, altezza e fps.

### Proporzioni {#aspect-ratio}

Quando scegliete o create un predefinito di codifica video per il file video sorgente principale, assicuratevi che il predefinito abbia le stesse proporzioni del file video sorgente principale. Le proporzioni corrispondono al rapporto tra la larghezza e l&#39;altezza del video.

Per determinare le proporzioni di un file video, recuperate i metadati del file e annotate la larghezza e l&#39;altezza del file (consultate Ottenere i metadati di un file qui sopra). Quindi utilizza questa formula per determinare le proporzioni:

larghezza/altezza = proporzioni

Nella tabella seguente viene descritto come i risultati della formula si traducono in scelte di proporzioni comuni:

| Risultato formula | Proporzioni |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

Ad esempio, un video con larghezza 1440 x altezza 1080 ha proporzioni 1440/1080 o 1,33. In questo caso, scegliete un predefinito di codifica video con proporzioni 4:3 per codificare il file video.

### Bitrate {#bitrate}

Bitrate è la quantità di dati codificati per costituire un singolo secondo di riproduzione video. Il bitrate viene misurato in kilobit al secondo (Kbps).

>[!NOTE]
>
>Poiché tutti i codec utilizzano la compressione con perdita di dati, il bitrate è il fattore più importante nella qualità video. Con la compressione con perdita di dati, più si comprime un file video, più la qualità si riduce. Per questo motivo, tutte le altre caratteristiche sono uguali (risoluzione, frame rate e codec), minore è il bitrate, minore è la qualità del file compresso.

Quando si seleziona una codifica bitrate, è possibile scegliere tra due tipi:

* **[!UICONTROL Codifica bitrate costante]** (CBR) - Durante la codifica CBR, il bitrate o il numero di bit al secondo viene mantenuto invariato durante il processo di codifica. La codifica CBR mantiene la velocità dati impostata sull’impostazione per l’intero video. Inoltre, la codifica CBR non ottimizza i file multimediali per la qualità, ma consente di risparmiare spazio di archiviazione.
Utilizzate CBR se il video contiene un livello di movimento simile per l&#39;intero video. CBR viene utilizzato più comunemente per lo streaming di contenuti video. Vedi anche [Utilizzare parametri di codifica video personalizzati](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codifica bitrate variabile]** (VBR) - La codifica VBR regola la velocità dati verso il basso e al limite superiore impostato, in base ai dati richiesti dal compressore. Questa funzionalità significa che durante un processo di codifica VBR il bitrate del file multimediale aumenta o diminuisce in modo dinamico a seconda delle esigenze di bitrate dei file multimediali.
La codifica VBR richiede più tempo, ma produce i risultati più favorevoli; la qualità del file multimediale è superiore. VBR viene utilizzato in genere per la distribuzione progressiva http di contenuti video.

Quando si utilizza VBR rispetto a CRB?
Quando selezioni VBR rispetto a CBR, si consiglia quasi sempre di utilizzare VBR per i file multimediali. VBR fornisce file di qualità superiore a bitrate competitivi. Quando si utilizza VBR, assicurarsi di utilizzare con la codifica a due passate e impostare il bitrate massimo su 1,5 volte il bitrate video di destinazione.

Quando scegli un predefinito di codifica video, ricorda la velocità di connessione dell’utente finale target. Scegli un predefinito con una velocità dati pari all’80% di quella velocità. Ad esempio, se la velocità di connessione dell&#39;utente finale è di 1000 Kbps, il valore predefinito migliore è 800 Kbps.

Questa tabella descrive la velocità dati delle velocità di connessione tipiche.

| Velocità (Kbps) | Tipo di connessione |
|--- |--- |
| 256 | Connessione remota. |
| 800 | Connessione mobile tipica. Per questa connessione, esegui il targeting di una velocità di dati compresa tra 400 e un massimo di 800 per le esperienze 3G. |
| 2000 | Connessione desktop a banda larga tipica. Per questa connessione, eseguire il targeting di una velocità di dati nell&#39;intervallo 800-2000 Kbps, con la maggior parte delle destinazioni in media 1200-1500 Kbps. |
| 5000 | Tipica connessione a banda larga. La codifica in questo intervallo superiore non è consigliata perché la distribuzione di video a questa velocità non è disponibile per la maggior parte dei consumatori. |

### Risoluzione {#resolution}

**Risoluzione** descrive l&#39;altezza e la larghezza in pixel di un file video. La maggior parte dei video sorgente viene memorizzata ad alta risoluzione (ad esempio, 1920 x 1080). Ai fini dello streaming, il video sorgente viene compresso a una risoluzione inferiore (640 x 480 o inferiore).

La risoluzione e la velocità dei dati sono due fattori strettamente collegati che determinano la qualità video. Per mantenere la stessa qualità video, maggiore è il numero di pixel in un file video (maggiore è la risoluzione), maggiore è la velocità dati. Ad esempio, si consideri il numero di pixel per fotogramma in un file video con risoluzione 320 x 240 e 640 x 480:

| Risoluzione | Pixel per frame |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

Il file 640 x 480 ha un numero di pixel per frame quattro volte superiore. Per ottenere la stessa velocità dati per queste due risoluzioni di esempio, applicate una compressione quattro volte superiore al file 640 x 480, riducendo in tal modo la qualità del video. Di conseguenza, una velocità di dati video di 250 Kbps produce una visualizzazione di alta qualità con una risoluzione di 320 x 240, ma non con una risoluzione di 640 x 480.

In generale, maggiore è la velocità dati utilizzata, migliore è l&#39;aspetto del video e maggiore è la risoluzione, maggiore è la velocità dati, maggiore è la qualità di visualizzazione (rispetto alle risoluzioni più basse).

Poiché la risoluzione e la velocità dati sono collegate, durante la codifica del video sono disponibili due opzioni:

* Scegli una velocità dati e quindi codificala alla risoluzione più alta che risulti appropriata alla velocità dati scelta.
* Scegliete una risoluzione e quindi codificate alla velocità dati necessaria per ottenere video di alta qualità alla risoluzione desiderata.

Quando scegli (o crei) un predefinito di codifica video per il file video sorgente principale, utilizza questa tabella per individuare la risoluzione corretta:

| Risoluzione | Altezza (pixel) | Dimensioni dello schermo |
|--- |--- |--- |
| 240p | 240 | Schermo piccolo |
| 300p | 300 | Schermo piccolo in genere per dispositivi mobili |
| 360p | 360 | Schermo piccolo |
| 480p | 480 | Schermo medio |
| 720p | 720 | Schermo grande |
| 1080p | 1080 | Schermo ad alta definizione di grandi dimensioni |

### Fps (frame al secondo) {#fps-frames-per-second}

Negli Stati Uniti e in Giappone, la maggior parte dei video viene girata a 29,97 fps; in Europa, la maggior parte dei video viene girata a 25 fps. Il film viene girato a 24 fps.

Scegli un predefinito di codifica video che corrisponda alla velocità fps del file video sorgente principale. Ad esempio, se il video sorgente principale è a 25 fps, scegliete un predefinito di codifica con 25 fps. Per impostazione predefinita, tutta la codifica personalizzata utilizza il fps del file video sorgente principale. Per questo motivo, non è necessario specificare esplicitamente l&#39;impostazione fps quando si crea un predefinito di codifica video.

### Dimensioni di codifica video {#video-encoding-dimensions}

Per risultati ottimali, seleziona dimensioni di codifica tali che il video sorgente sia un multiplo di tutti i video codificati.

Per calcolare questo rapporto, si divide la larghezza dell&#39;origine per la larghezza codificata per ottenere il rapporto di larghezza. Quindi, per ottenere il rapporto di altezza, dividi l’altezza sorgente per altezza codificata.

Se il rapporto risultante è un numero intero, significa che il video è ridimensionato in modo ottimale. Se il rapporto risultante non è un numero intero, influisce sulla qualità video lasciando sul display gli artefatti di pixel rimanenti. Questo effetto è più evidente quando il video contiene del testo.

Ad esempio, supponiamo che il video sorgente sia 1920 x 1080. Nella tabella seguente, i tre video codificati forniscono le impostazioni di codifica ottimali da utilizzare.

| Tipo di video | Larghezza x altezza | Rapporto larghezza | Rapporto altezza |
|--- |--- |--- |--- |
| Sorgente | 1920x1080 | 1 | 1 |
| Codificato | 960 x 540 | 2 | 2 |
| Codificato | 640 x 360 | 3 | 3 |
| Codificato | 480 x 270 | 4 | 4 |

### Formato file video codificato {#encoded-video-file-format}

Dynamic Media consiglia di utilizzare i predefiniti di codifica video MP4 H.264. Poiché i file MP4 utilizzano il codec video H.264, questo offre video di alta qualità ma in dimensioni di file compressi.

### Abilita DASH sul tuo account {#enable-dash}

DASH (Digital Adaptive Streaming over HTTP) è lo standard internazionale per lo streaming video ed è ampiamente adottato tra diversi visualizzatori video. Quando DASH è abilitato sul tuo account, puoi scegliere tra DASH o HLS per lo streaming video adattivo. Oppure, è possibile optare per entrambi con cambio automatico tra i lettori quando **[!UICONTROL auto]** viene selezionato come tipo di riproduzione nel predefinito Visualizzatore.

Alcuni vantaggi chiave dell&#39;attivazione di DASH sul tuo account includono:

* Video con flusso DASH del pacchetto per lo streaming con bitrate adattivo. Questo metodo porta a una maggiore efficienza nella consegna. Lo streaming adattivo assicura la migliore esperienza di visualizzazione per i clienti.
* Lo streaming ottimizzato per il browser con i lettori Dynamic Media passa dallo streaming HLS a quello DASH per garantire la migliore qualità del servizio. Il lettore video passa automaticamente a HLS quando si utilizza un browser Safari.
* Puoi configurare il metodo di streaming preferito (HLS o DASH) modificando il predefinito visualizzatore video.
* La codifica video ottimizzata garantisce che non venga utilizzata alcuna risorsa di archiviazione aggiuntiva durante l’abilitazione della funzionalità DASH. Viene creato un unico set di codifiche video sia per HLS che per DASH per ottimizzare i costi di archiviazione video.
* Consente di rendere la distribuzione di video più accessibile ai clienti.
* Ottieni l’URL di streaming anche tramite API.

L’attivazione di DASH sul tuo account richiede due passaggi:

* Configurazione di Dynamic Media per l’utilizzo di DASH, operazione che è possibile eseguire in modo semplice.
* La configurazione dell’Experience Manager 6.5 per l’utilizzo di DASH viene eseguita tramite un caso di assistenza clienti di Adobe che hai creato e inviato.

**Per abilitare DASH sul tuo account:**

1. **Configurare Dynamic Media** - In Dynamic Media, all&#39;Experience Manager 6.5, vai a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Cerca **AEM Assets Dynamic Media Video Advanced Streaming** flag di funzione.
1. Per attivare (attivare) la funzione DASH, selezionare la casella di controllo.
1. Seleziona **[!UICONTROL Salva]**.
1. **Configurare Experience Manager 6.5** - [Utilizza l’Admin Console per avviare la creazione di un nuovo caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Per creare un caso di supporto, attieniti alle istruzioni e accertati di fornire le seguenti informazioni:

   * Nome del contatto principale, e-mail, telefono.
   * Nome dell’account Dynamic Media.
   * Specificare che si desidera che DASH sia abilitato nell&#39;Experience Manager 6.5.

1. L’Assistenza clienti Adobe ti aggiunge alla lista d’attesa dei clienti DASH in base all’ordine in cui vengono inviate le richieste.
1. Quando Adobe è pronto a gestire la richiesta, l’Assistenza clienti ti contatta per coordinare e impostare una data limite per l’abilitazione di DASH.
1. Ricevi una notifica dopo il completamento da parte dell’Assistenza clienti.
1. Crea [predefinito visualizzatore video](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) come al solito.

## Visualizzare rapporti video {#viewing-video-reports}

>[!NOTE]
>
>I rapporti video sono disponibili solo quando si esegue Dynamic Media in modalità ibrida.

I rapporti video visualizzano diverse metriche aggregate in un determinato periodo di tempo per aiutarti a monitorare che *pubblicato* i singoli video e i video aggregati funzionano come previsto. I seguenti dati sulle metriche principali sono aggregati per tutti i video pubblicati sull’intero sito web:

* Inizio video
* Percentuale completata
* Tempo medio sul video
* Tempo totale su video
* Video per visita

Una tabella di tutti *pubblicato* Sono elencati anche i video, in modo da poter tenere traccia dei video più visualizzati sul sito web in base al totale degli avvii dei video.

Quando tocchi un nome video nell’elenco, questo mostra il rapporto sulla fidelizzazione del pubblico del video (a discesa) sotto forma di un grafico a linee. Il grafico mostra il numero di visualizzazioni per un dato momento della riproduzione video. Quando si riproduce il video, la barra verticale viene sincronizzata con l&#39;indicatore di tempo nel lettore. Le cadute nei dati del grafico a linee indicano dove il pubblico abbandona il disinteresse.

Se il video è stato codificato al di fuori di Adobe Experience Manager Dynamic Media, il grafico di conservazione del pubblico (a discesa) e i dati della percentuale di riproduzione nella tabella non sono disponibili.

Vedi anche [Configurare Cloud Services Dynamic Media](/help/assets/config-dynamic.md).

>[!NOTE]
>
>I dati di tracciamento e reporting si basano esclusivamente sull’utilizzo del lettore video di Dynamic Media e del relativo predefinito per lettore video. Di conseguenza, non è possibile tracciare e creare rapporti sui video riprodotti da altri lettori video.

Per impostazione predefinita, la prima volta che si immettono i rapporti video, il rapporto visualizza i dati video a partire dal primo del mese corrente e termina con la data del mese corrente. Tuttavia, puoi sovrascrivere l’intervallo di date predefinito specificando un intervallo di date personalizzato. Alla successiva immissione di Report video, viene utilizzato l&#39;intervallo di date specificato.

Affinché i rapporti video funzionino correttamente, viene creato automaticamente un ID suite di rapporti quando vengono configurati i Cloud Services Dynamic Media. Allo stesso tempo, l’ID suite di rapporti viene inviato al server di pubblicazione, in modo che sia disponibile per la funzione Copia URL quando visualizzi l’anteprima delle risorse. Tuttavia, questa funzionalità richiede che il server di pubblicazione sia già configurato. Se il server di pubblicazione non è configurato, puoi comunque eseguire la pubblicazione per visualizzare il rapporto video. Tuttavia, devi tornare alla configurazione cloud di Dynamic Media e toccare **[!UICONTROL OK]**.

**Per visualizzare i rapporti video:**

1. Nell’angolo in alto a sinistra dell’Experience Manager, tocca il logo dell’Experience Manager, quindi nella barra a sinistra tocca **[!UICONTROL Strumenti]** (icona a forma di martello) > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti video]**.
1. Nella pagina Rapporti video eseguire una delle operazioni seguenti:

   * Nell’angolo in alto a destra, tocca il **Aggiorna rapporto video** icona.
Utilizzare Aggiorna solo se la data di fine del rapporto è il giorno corrente. In questo modo potrai vedere il tracciamento video che si è verificato dall’ultima volta che hai eseguito il rapporto.

   * Nell’angolo in alto a destra, tocca il **Selettore data** icona.
Specifica l’intervallo di date di inizio e fine per il quale desideri visualizzare i dati video, quindi tocca **[!UICONTROL Esegui rapporto]**.

   La casella di gruppo Metriche principali identifica varie misurazioni aggregate per tutti *pubblicato* video nel sito.

1. Nella tabella in cui sono elencati i video più pubblicati, tocca il nome di un video per riprodurlo e visualizzane il rapporto sulla fidelizzazione del pubblico (drop-off).

### Visualizzare rapporti video basati su un visualizzatore video creato con l’SDK del visualizzatore di Dynamic Media HTML5 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Se utilizzi un visualizzatore video predefinito fornito da Dynamic Media o se hai creato un predefinito visualizzatore personalizzato basato su un visualizzatore video predefinito, non sono necessari ulteriori passaggi per visualizzare i rapporti video. Tuttavia, se hai creato un visualizzatore video personalizzato basato sull’API SDK del visualizzatore di HTML5, utilizza i passaggi seguenti per assicurarti che il visualizzatore video invii eventi di tracciamento ai rapporti video di Dynamic Media.

Utilizza il [Guida di riferimento per i visualizzatori Dynamic Media di Adobe](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) e [API SDK di HTML5 Viewer](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) per creare visualizzatori video personalizzati.

**Per visualizzare i rapporti video basati su un visualizzatore video creato con l’SDK del visualizzatore di Dynamic Media HTML5:**

1. Passa a qualsiasi risorsa video pubblicata.
1. Seleziona **[!UICONTROL Visualizzatori]** dall’elenco a discesa dell’angolo in alto a sinistra della pagina della risorsa.
1. Seleziona un predefinito visualizzatore video e copia il codice da incorporare.
1. Nel codice di incorporamento, individua la riga con la seguente:

   `videoViewer.setParam("config2", "<value>");`

   Il `config2` Il parametro abilita il tracciamento nei visualizzatori HTML5. È anche un predefinito specifico per l’azienda che contiene le informazioni di configurazione per Video Reporting e per le configurazioni Adobe Analytics specifiche per il cliente.

   Il valore corretto per il parametro config2 si trova sia nella funzione **[!UICONTROL Incorpora codice]** che in copia **[!UICONTROL URL]**. Nell’URL dal comando di copia **[!UICONTROL URL]**, il parametro da cercare è `&config2=<value>`. Il valore è quasi sempre `companypreset`, ma in alcuni casi può anche essere `companypreset-1`, `companypreset-2` e così via.

1. Nel codice del visualizzatore video personalizzato, aggiungi AppMeasurementBridge .jsp alla pagina del visualizzatore eseguendo le seguenti operazioni:

   * Innanzitutto, determina se è necessario `&preset` parametro.

      Se il `config2` il parametro è `companypreset`, tu sì *non* bisogno `&preset=parameter`.

      Se `config2` è qualsiasi altra cosa, imposta il parametro di preselezione allo stesso modo del `config2` parametro. Ad esempio, se `config2=companypreset-2`, aggiungi `&param2=companypreset-2` all’URL AppMeasurmentBridge.jsp.

   * Quindi, aggiungi lo script AppMeasurementBridge.jsp:

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Creare il componente TrackingManager eseguendo le operazioni seguenti:

   * Dopo aver chiamato `s7sdk.Util.init();`, crea un’istanza di Tracking Manager per tenere traccia degli eventi aggiungendo gli elementi seguenti:

      `var trackingManager = new s7sdk.TrackingManager();`

   * Connettere i componenti a Tracking Manager effettuando le seguenti operazioni:

      In `s7sdk.Event.SDK_READY` , collegare il componente di cui si desidera tenere traccia a TrackingManager.

      Ad esempio, se il componente è `videoPlayer`, aggiungi

      `trackingManager.attach(videoPlayer);`

      per collegare il componente a trackingManager. Per tenere traccia di più visualizzatori su una pagina, utilizza più componenti di gestione del tracciamento.

   * Creare l&#39;oggetto AppMeasurementBridge aggiungendo gli elementi seguenti:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * Aggiungi la funzione di tracciamento aggiungendo gli elementi seguenti:

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   L&#39;oggetto appMeasurementBridge ha una funzione di tracciamento incorporata. Tuttavia, puoi fornire il tuo per supportare più sistemi di tracciamento o altre funzionalità.

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## Aggiungere sottotitoli codificati o sottotitoli al video {#adding-captions-to-video}

Puoi estendere la portata dei tuoi video ai mercati globali aggiungendo sottotitoli ai singoli video o ai set di video adattivi. Aggiungendo i sottotitoli, si evita di duplicare l&#39;audio o di utilizzare madrelingua per registrare nuovamente l&#39;audio per ogni lingua. Il video viene riprodotto nella lingua in cui è stato registrato. I sottotitoli delle lingue straniere vengono visualizzati in modo che persone di lingue diverse possano ancora comprendere la porzione audio.

I sottotitoli codificati consentono inoltre una maggiore accessibilità alle persone non udenti o ipoudenti.

>[!NOTE]
>
>Il lettore video utilizzato deve supportare la visualizzazione dei sottotitoli.

Vedi anche [Accessibilità in Dynamic Media](/help/assets/accessibility-dm.md).

Dynamic Media converte i file di didascalia in formato JSON (JavaScript Object Notation). Questa conversione ti consente di incorporare il testo JSON in una pagina web come trascrizione nascosta ma completa del video. I motori di ricerca possono quindi eseguire la ricerca per indicizzazione e indicizzare il contenuto per rendere i video più facilmente individuabili e fornire ai clienti ulteriori dettagli sul contenuto video.

Consulta [Distribuisci contenuti statici (non immagine)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) nel *Guida all’API per il server e il rendering immagini di Dynamic Media* per ulteriori informazioni sull’utilizzo della funzione JSON in un URL.

**Per aggiungere sottotitoli o sottotitoli al video:**

1. Utilizza un’applicazione o un servizio di terze parti per creare il file di sottotitoli/sottotitoli video.

   Assicurati che il file creato segua lo standard WebVTT (Web Video Text Tracks). L&#39;estensione del nome file dei sottotitoli è .vtt. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

   Consulta [WebVTT: formato per tracce di testo video Web](https://w3c.github.io/webvtt/).

   Esistono strumenti e servizi gratuiti e premium che puoi utilizzare per creare file di sottotitoli/sottotitoli al di fuori di Dynamic Media. Ad esempio, per creare un file di sottotitoli video semplice senza stile, potete utilizzare il seguente strumento di creazione e modifica di sottotitoli online gratuito:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Per ottenere risultati ottimali, utilizza lo strumento in Internet Explorer 9 o versioni successive, Google Chrome o Safari.

   Nello strumento, nella sezione **[!UICONTROL Inserisci l’URL del file video]** , incollare l&#39;URL copiato del file video e quindi fare clic su **[!UICONTROL Carica]**. Consulta [Ottenere un URL per una risorsa](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) per ottenere l’URL del file video stesso che puoi incollare nel file **[!UICONTROL Immetti l’URL del campo del file video]**. A quel punto, Internet Explorer, Chrome o Safari possono riprodurre il video in modalità nativa.

   Ora segui le istruzioni visualizzate sul sito per creare e salvare il file WebVTT. Al termine, copiare il contenuto del file di didascalia e incollarlo in un editor di testo normale e salvarlo con un `.vtt` estensione del nome file.

   >[!NOTE]
   >
   >Per il supporto globale dei sottotitoli video in più lingue, lo standard WebVTT richiede la creazione di file .vtt e chiamate separati per ogni lingua che si desidera supportare.

   In genere, si desidera assegnare al file VTT della didascalia lo stesso nome del file video e aggiungerlo alla lingua locale, ad esempio -EN, -FR o -DE. In questo modo, è possibile automatizzare la generazione degli URL video utilizzando il sistema di gestione dei contenuti web esistente.

1. Ad Experience Manager, carica il file di didascalia WebVTT in DAM.
1. Accedi a *pubblicato* risorsa video da associare al file di didascalia caricato.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse.

   Consulta [Pubblicare le risorse](/help/assets/publishing-dynamicmedia-assets.md).

1. Effettua una delle operazioni seguenti:

   * Per visualizzare un video popup, tocca **[!UICONTROL URL]**. Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo. Aggiungi all’URL copiato del video la seguente sintassi:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Osserva `,1` alla fine del percorso della didascalia. Immediatamente dopo il `.vtt` estensione del nome file nel percorso, puoi facoltativamente abilitare (attivare) o disabilitare (disattivare) il pulsante sottotitoli codificati sulla barra del lettore video impostando su `,1` o `,0`, rispettivamente.

   * Per un’esperienza di visualizzazione video incorporata, tocca **[!UICONTROL Codice di incorporamento]**. Nella finestra di dialogo Incorpora codice, seleziona e copia il codice da incorporare negli Appunti, quindi incolla il codice in un semplice editor di testo. Aggiungi il codice da incorporare copiato con la seguente sintassi:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Osserva `,1` alla fine del percorso della didascalia. Immediatamente dopo il `.vtt` estensione del nome file nel percorso, puoi facoltativamente abilitare (attivare) o disabilitare (disattivare) il pulsante sottotitoli codificati sulla barra del lettore video impostando su `,1` o `,0`, rispettivamente.

## Aggiungere marcatori capitolo al video {#adding-chapter-markers-to-video}

Per semplificare la visualizzazione e la navigazione dei video lunghi, aggiungi marcatori capitolo ai singoli video o ai set di video adattivi. Quando un utente riproduce il video, può fare clic sui contrassegni dei capitoli sulla timeline del video (nota anche come scorrimento video) per passare facilmente al punto di interesse. In alternativa, è possibile passare immediatamente a nuovi contenuti, dimostrazioni e tutorial.

>[!NOTE]
>
>Il lettore video utilizzato deve supportare l’uso dei marcatori capitolo. I lettori video Dynamic Media supportano i contrassegni dei capitoli, ma non i lettori video di terze parti.

Se lo desideri, puoi creare un visualizzatore video personalizzato con i capitoli e aggiungerlo al tuo marchio, invece di utilizzare un predefinito visualizzatore video. Per istruzioni sulla creazione di un visualizzatore HTML5 personalizzato con navigazione dei capitoli, nell’API SDK del visualizzatore AdobeHTML 5, fai riferimento all’intestazione &quot;Personalizzazione del comportamento con i modificatori&quot; sotto le classi `s7sdk.video.VideoPlayer` e `s7sdk.video.VideoScrubber`. Consulta la [API SDK di HTML5 Viewer](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) documentazione.

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Per creare un elenco di capitoli per il video è necessario seguire le stesse procedure utilizzate per creare i sottotitoli. In altre parole, si crea un file WebVTT. Si noti, tuttavia, che questo file deve essere separato da qualsiasi file di sottotitoli WebVTT che si sta utilizzando anche; non è possibile combinare sottotitoli e capitoli in un unico file WebVTT.

L&#39;esempio seguente può essere utilizzato come esempio del formato utilizzato per creare un file WebVTT con navigazione nei capitoli:

### File WebVTT con navigazione capitolo video {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

Nell’esempio precedente, `Chapter 1` è l’identificatore del cue ed è facoltativo. Il tempo di cue di `00:00:000 --> 01:04:364` specifica l&#39;ora di inizio e di fine del capitolo, in `00:00:000` formato. Le ultime tre cifre sono millisecondi e possono essere lasciate come `000`, se preferita. Titolo del capitolo di `The bicycle store behind it all` è la descrizione effettiva del contenuto del capitolo. L&#39;identificatore del cue, il tempo di cue iniziale e il titolo del capitolo vengono visualizzati in una finestra a comparsa del lettore video quando un utente passa il puntatore del mouse su un punto di cue visivo nella timeline del video.

Poiché si utilizza un visualizzatore video di HTML5, assicurarsi che il file del capitolo creato segua lo standard WebVTT (Web Video Text Tracks). L’estensione del nome file del capitolo è `.vtt`. Ulteriori informazioni sullo standard per i sottotitoli WebVTT.

Consulta [WebVTT: formato per tracce di testo video Web](https://w3c.github.io/webvtt/)

**Per aggiungere la navigazione ai capitoli video:**

1. Salva il `.vtt` file con codifica UTF8, per evitare problemi con la rappresentazione dei caratteri nel testo del titolo del capitolo.

   In genere, si desidera assegnare al file VTT del capitolo lo stesso nome del file video e aggiungerlo ai capitoli. In questo modo, è possibile automatizzare la generazione degli URL video utilizzando il sistema di gestione dei contenuti web esistente.
1. Ad Experience Manager, carica il file del capitolo WebVTT.

   Consulta [Caricamento risorse](/help/assets/manage-assets.md#uploading-assets).

1. Effettua una delle operazioni seguenti:

   <table>
     <tbody>
      <tr>
       <td>Per un'esperienza di visualizzazione video popup</td>
       <td>
       <ol>
       <li>Accedi a <i>pubblicato </i>risorsa video da associare al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Consulta <a href="/help/assets/publishing-dynamicmedia-assets.md">Pubblicazione delle risorse.</a></li>
       <li>Dal menu a discesa, quindi tocca o fai clic su <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, tocca o fai clic sul nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, fai clic su <strong>URL</strong>.</li>
       <li>Nella finestra di dialogo URL, seleziona e copia l’URL negli Appunti, quindi trascina l’URL in un semplice editor di testo.</li>
       <li>Aggiungi l’URL copiato del video con la seguente sintassi per associarlo all’URL copiato nel file del capitolo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Per un’esperienza di visualizzazione video incorporata<br /> </td>
       <td>
       <ol>
       <li>Accedi a <i>pubblicato </i>risorsa video da associare al file del capitolo caricato. Gli URL sono disponibili per la copia solo <i>dopo</i> la prima <i>pubblicazione</i> delle risorse. Consulta <a href="/help/assets/publishing-dynamicmedia-assets.md">Pubblicazione delle risorse.</a></li>
       <li>Dal menu a discesa, quindi tocca o fai clic su <strong>Visualizzatori</strong>.</li>
       <li>Nella barra a sinistra, tocca o fai clic sul nome del predefinito per visualizzatori video. Un’anteprima del video viene aperta in una pagina separata.</li>
       <li>Nella barra a sinistra, in basso, fai clic su <strong>Incorpora</strong>.</li>
       <li>Nella finestra di dialogo Incorpora codice, seleziona e copia l’intero codice negli Appunti, quindi incollalo in un semplice editor di testo.</li>
       <li>Aggiungi il codice di incorporamento del video con la seguente sintassi per associarlo all’URL copiato nel file del capitolo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Informazioni sulle miniature video in Dynamic Media - Modalità Scene7 {#about-video-thumbnails-in-dynamic-media-scene-mode}

Una miniatura video è una versione di dimensioni ridotte di un fotogramma video o di una risorsa immagine che rappresenta il video per il cliente. La miniatura serve a incoraggiare un cliente a selezionare il video.

A tutti i video dell&#39;Experience Manager deve essere associata una miniatura; non è possibile eliminare una miniatura senza sostituirla. Per impostazione predefinita, quando caricate un video in Experience Manager, il primo fotogramma viene utilizzato come miniatura. Tuttavia, puoi personalizzare la miniatura a scopo di branding o di ricerca visiva, ad esempio. Quando si personalizza una miniatura video, è possibile riprodurre il video e metterlo in pausa sul fotogramma che si desidera utilizzare. In alternativa, puoi selezionare una risorsa di immagine che hai già caricato e *pubblicato* nel gestore delle risorse digitali.

Un’immagine di miniatura video personalizzata selezionata da un video non viene estratta e salvata in DAM come risorsa separata e distinta. Tuttavia, una miniatura video personalizzata selezionata da una risorsa immagine esistente viene salvata in JCR. Il percorso della risorsa selezionata viene memorizzato nel nodo della risorsa video come nell’esempio di percorso seguente:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

La possibilità di personalizzare una miniatura video è disponibile solo dopo aver applicato un profilo video alla cartella in cui si trova il video.

Vedi anche [Informazioni sulle miniature video in Dynamic Media - Modalità ibrida](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### Aggiungi una miniatura video personalizzata {#adding-a-custom-video-thumbnail}

Questi passaggi si applicano solo a Dynamic Media in esecuzione in modalità &quot;Dynamicmedia_Scene7&quot;.

**Per aggiungere una miniatura video personalizzata:**

1. Accertati di aver già eseguito le seguenti operazioni:

   * È stata creata una cartella per le risorse video.
   * [Applicare un profilo video alla cartella](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [Ha caricato i tuoi video nella cartella](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. Passa a una risorsa video caricata di cui desideri modificare l’immagine in miniatura.
1. Nella modalità di selezione delle risorse da **[!UICONTROL Vista a elenco]** o **[!UICONTROL Vista a schede]**, tocca la risorsa video.
1. Nella barra degli strumenti, tocca **[!UICONTROL Proprietà]** (un cerchio contenente una &quot;i&quot;).
1. Nella pagina Proprietà del video, tocca **[!UICONTROL Cambia miniatura]**.
1. Nella pagina Modifica miniatura eseguire una delle operazioni seguenti:

   * Per utilizzare un fotogramma del video come nuova miniatura:

      * Sulla barra degli strumenti, tocca **[!UICONTROL Seleziona fotogramma da video]**.
      * Toccare il pulsante Riproduci, quindi toccare il pulsante Pausa sul fotogramma che si desidera catturare come nuova miniatura del video.
   * Per utilizzare una risorsa immagine come nuova miniatura:

      * Sulla barra degli strumenti, tocca **[!UICONTROL Seleziona miniatura da risorse]**.
      * Tocca **[!UICONTROL Seleziona miniatura]**.
      * Passa a una risorsa immagine caricata e pubblicata in precedenza che desideri utilizzare. La risorsa viene ridimensionata automaticamente in modo da fungere da immagine miniatura per il video.
      * Seleziona la risorsa immagine, quindi tocca **[!UICONTROL Seleziona]**.


1. Nella pagina Modifica miniatura, tocca **[!UICONTROL Salva modifica]**.
1. Nella pagina Proprietà del video, nell’angolo superiore destro, tocca **[!UICONTROL Salva e chiudi]**.

## Informazioni sulle miniature video in Dynamic Media - Modalità ibrida {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Puoi scegliere una delle dieci immagini in miniatura generate automaticamente da Dynamic Media da aggiungere al video. Il lettore video mostra la miniatura selezionata quando una risorsa video viene utilizzata con il componente Dynamic Media nell’ambiente di authoring di Experience Manager Sites, Experience Manager Mobile o Experienci Manager Screens. La miniatura funge da immagine statica che rappresenta al meglio il contenuto dell’intero video e incoraggia ulteriormente gli utenti a fare clic sul pulsante Play.

In base al tempo totale del video, Dynamic Media acquisisce dieci miniature (impostazione predefinita). Le immagini vengono acquisite a un tasso dell&#39;1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81% e 91% nel video. Le dieci miniature persistono, il che significa che se decidi di scegliere un’altra miniatura in un secondo momento, non è necessario rigenerare la serie. Puoi visualizzare in anteprima le dieci immagini in miniatura e quindi selezionare quella che desideri usare con il video. Se desideri impostare l’impostazione predefinita, puoi utilizzare CRXDE Lite per configurare l’intervallo di tempo in cui vengono generate le immagini in miniatura. Ad esempio, se desideri generare solo una serie di quattro immagini miniatura con spaziatura uniforme dal video, puoi configurare l’intervallo in modo che sia compreso tra 24%, 49%, 74% e 99%.

Idealmente, puoi aggiungere una miniatura video in qualsiasi momento dopo aver caricato il video, ma prima di pubblicarlo sul sito web.

Se lo desideri, puoi scegliere di caricare una miniatura personalizzata per rappresentare il video invece di utilizzare una miniatura generata da Dynamic Media. Ad esempio, puoi creare un’immagine miniatura personalizzata con il titolo del video, un’immagine di apertura accattivante o un’immagine specifica acquisita dal video. L’immagine miniatura video personalizzata caricata deve avere una risoluzione massima di 1280 x 720 pixel (larghezza minima di 640 pixel) e non superare i 2 MB.

Vedi anche [Informazioni sulle miniature video in Dynamic Media - Modalità Scene7](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Aggiungi una miniatura video {#adding-a-video-thumbnail}

Questi passaggi si applicano solo a Dynamic Media in esecuzione in modalità ibrida.

**Per aggiungere una miniatura video:**

1. Passa a una risorsa video caricata a cui desideri aggiungere una miniatura video.
1. Nella modalità di selezione delle risorse dalla Vista a elenco o dalla Vista a schede, tocca la risorsa video.
1. Nella barra degli strumenti, tocca **[!UICONTROL Visualizza proprietà]** (un cerchio contenente una &quot;i&quot;).
1. Nella pagina Proprietà del video, tocca **[!UICONTROL Cambia miniatura]**.
1. Nella pagina Modifica miniatura, sulla barra degli strumenti, tocca **[!UICONTROL Seleziona frame]**.

   Dynamic Media genera una serie di miniature dal video, in base all&#39;intervallo di tempo predefinito o personalizzato.

1. Visualizza l&#39;anteprima delle immagini in miniatura generate, quindi seleziona quella che desideri aggiungere al video.
1. Tocca **[!UICONTROL Salva modifica]**.

   L&#39;immagine miniatura del video viene aggiornata in modo da utilizzare la miniatura selezionata. Se successivamente decidi di modificare l’immagine miniatura, puoi tornare al **[!UICONTROL Cambia miniatura]** e selezionarne una nuova.

   Se hai configurato nuovi intervalli di tempo predefiniti o hai caricato un nuovo video per sostituire quello esistente, chiedi a Dynamic Media di rigenerare le miniature.

   Consulta [Configura l&#39;intervallo di tempo predefinito per la generazione delle miniature video](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### Configura l&#39;intervallo di tempo predefinito per la generazione delle miniature video {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

Quando configuri e salvi il nuovo intervallo di tempo predefinito, la modifica viene applicata automaticamente solo ai video caricati in futuro. Il nuovo predefinito non viene applicato automaticamente ai video caricati in precedenza. Per i video esistenti, è necessario rigenerare le miniature.

Consulta [Aggiungi una miniatura video](#adding-a-video-thumbnail).

**Per configurare l&#39;intervallo di tempo predefinito per la generazione delle miniature video:**

1. Ad Experience Manager, tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.

1. Nella pagina CRXDE Lite, nel pannello directory a sinistra, passa a `o etc/dam/imageserver/configuration/jcr:content/settings.`

   se il pannello directory non è visibile, tocca l’icona >> a sinistra della scheda Home.

1. Nel pannello in basso a destra, nella scheda Proprietà, tocca due volte `thumbnailtime`.
1. In **[!UICONTROL Modifica miniatura]** , utilizzare i campi di testo per immettere valori di intervallo come percentuali.

   * Toccare l&#39;icona del segno più (+) se si desidera aggiungere uno o più campi del valore di intervallo. Se necessario, scorrere fino alla parte inferiore della finestra di dialogo per visualizzare l&#39;icona.
   * Toccare l&#39;icona del segno meno (-) a destra di un campo del valore di intervallo per eliminarlo dall&#39;elenco.
   * Toccare l&#39;icona freccia su e l&#39;icona freccia giù se si desidera riordinare i valori di intervallo.

1. Tocca **[!UICONTROL OK]** e tornare alla scheda Proprietà.
1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, tocca **[!UICONTROL Salva tutto]**, quindi tocca l’icona Indietro Home nell’angolo in alto a sinistra per tornare a Experience Manager.

   Consulta [Aggiungi una miniatura video](#adding-a-video-thumbnail).

### Aggiungi una miniatura video personalizzata {#adding-a-custom-video-thumbnail-1}

Questi passaggi si applicano solo a Dynamic Media in esecuzione in modalità ibrida.

**Per aggiungere una miniatura video personalizzata:**

1. Passa a una risorsa video caricata per aggiungere una miniatura video personalizzata.
1. Nella modalità di selezione delle risorse dalla Vista a elenco o dalla Vista a schede, tocca la risorsa video.
1. Nella barra degli strumenti, tocca **[!UICONTROL Visualizza proprietà]** (un cerchio contenente una &quot;i&quot;).
1. Nella pagina Proprietà del video, tocca **[!UICONTROL Cambia miniatura]**.
1. Nella pagina Modifica miniatura, sulla barra degli strumenti, tocca **[!UICONTROL Carica nuova miniatura]**.
1. Passa alla miniatura da utilizzare, selezionala e tocca **[!UICONTROL Apri]** per iniziare a caricare l’immagine in Experience Manager. Dopo il caricamento, assicurati di pubblicare l’immagine.
1. Dopo aver caricato e pubblicato correttamente l’immagine, nella pagina Modifica miniatura tocca **[!UICONTROL Salva modifiche]**.

   La miniatura personalizzata viene aggiunta al video.

## Modificare l’URL di Dynamic Media per le risorse Dynamic Media {#manifest-urls}

I video elaborati in Dynamic Media possono essere utilizzati tramite visualizzatori predefiniti e anche accedendo direttamente agli URL del manifesto e riproducendoli attraverso visualizzatori personalizzati. Di seguito è riportata l’API per recuperare gli URL del manifesto di un video.

### Informazioni sull’API getVideoManifestURI

Il `getVideoManifestURI`L’API è esposta tramite c`q-scene7-api:com.day.cq.dam.scene7.api` e possono essere utilizzati per generare i seguenti URL manifesto:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Parametri API getVideoManifestURI

Questa API accetta i tre parametri seguenti:

| Parametro | Descrizione |
| --- | --- |
| `resource` | Risorsa corrispondente al video acquisito da Dynamic Media. |
| `manifestType` | Può essere `ManifestType.DASH` o `ManifestType.HLS` |
| `onlyIfPublished` | Imposta su true se l’URI del manifesto viene generato solo se è pubblicato e disponibile sul livello di consegna. |

Per recuperare gli URL del manifesto per i video utilizzando il metodo precedente, aggiungi un [profilo di codifica video](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) in una cartella &quot;carica video&quot;. Dynamic Media elabora questi video in base alle codifiche trovate nel file di codifica video assegnato alla cartella. Ora puoi richiamare la precedente API per recuperare gli URL del manifesto per i video caricati.

### Scenari di errore

L’API restituisce null in caso di errori. Le eccezioni vengono registrate nei log degli errori di Experience Manager. Tutti gli errori registrati iniziano con `Could not generate Video Manifest URI`. Gli errori possono verificarsi nei seguenti scenari:

* Un `IllegalArgumentException` viene registrato per uno dei seguenti elementi:

   * Il `resource` il parametro passato è nullo.
   * Il `resource` Il parametro passato non è un video.
   * Il `manifestType` il parametro passato è nullo.
   * Il `onlyIfPublished` Il parametro viene passato come true, ma il video non viene pubblicato.
   * Il video non è stato acquisito utilizzando un set video adattivo di Dynamic Media.

* `IOException` viene registrato quando si verifica un problema di connessione a Dynamic Media.
* `UnsupportedOperationException` viene registrato quando `manifestType` il parametro passato è `ManifestType.DASH`, mentre il video non è stato elaborato utilizzando il formato DASH.

Di seguito è riportato un esempio dell’API precedente utilizzando i servlet scritti in *HTTPWhiteBoard* specifica. Seleziona ogni scheda per la sintassi del codice.

>[!BEGINTABS]

>[!TAB Aggiungi dipendenza in pom.xml]

+++**Aggiungi dipendenza in pom.xml**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Servlet di esempio]

+++**Servlet di esempio**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Classe di risposta per il servlet]

+++**Classe di risposta per il servlet**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB File delle costanti a cui si fa riferimento nel servlet]

+++**File delle costanti a cui si fa riferimento nel servlet**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

Montare il servlet di cui sopra utilizzando un `servletContext`. Di seguito è riportato un esempio di `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### Utilizza il servlet di esempio

Il servlet viene richiamato eseguendo una `GET` operazione in `/dmSample/dynamicmedia/video/manifestUrl`. Vengono passati i seguenti parametri di query:

| Parametro query | Descrizione |
| --- | --- |
| `assetPath` | Obbligatorio. Percorso del video per il quale `manifestUrl` viene generato. |
| `manifestType` | Facoltativo. Il parametro può essere DASH o HLS. Se non viene passato, per impostazione predefinita viene usato il DASH. |
| `onlyIfPublished` | Facoltativo. Se superato, il `manifestUrl` viene restituito solo se il video è pubblicato. |

In questo esempio, supponiamo la seguente configurazione:

* L&#39;azienda è `samplecompany`.
* L’istanza di authoring è `http://sample-aem-author.com`.
* La cartella `/content/dam/video-example` dispone di un profilo di codifica video applicato.
* Il video `scenery.mp4` viene caricato nella cartella `/content/dam/video-example`.

Puoi richiamare il servlet nei seguenti modi:

| Tipo | Descrizione |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Se la consegna DASH è abilitata:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>Se la consegna DASH è disabilitata:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| TRATTINO | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>Se la consegna DASH è abilitata:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>Se la consegna DASH è disabilitata:<br>`{}` |
| Errore: percorso risorsa errato | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


