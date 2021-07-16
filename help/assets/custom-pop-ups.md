---
title: Creare pop-up personalizzati utilizzando Quickview
seo-title: Utilizza Quickview per creare pop-up personalizzati
description: La visualizzazione rapida predefinita viene utilizzata nelle esperienze e-commerce in cui viene visualizzato un pop-up con le informazioni sul prodotto per promuovere un acquisto. Puoi attivare il contenuto personalizzato da visualizzare nei pop-up.
seo-description: La visualizzazione rapida predefinita viene utilizzata nelle esperienze e-commerce in cui viene visualizzato un pop-up con le informazioni sul prodotto per promuovere un acquisto. Puoi attivare il contenuto personalizzato da visualizzare nei pop-up.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Visualizzatori
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: 5192a284c38eb10c214c67a8727de0f7dd4d1ee2
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---

# Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

La visualizzazione rapida predefinita viene utilizzata nelle esperienze e-commerce in cui viene visualizzato un pop-up con le informazioni sul prodotto per promuovere un acquisto. Tuttavia, puoi attivare il contenuto personalizzato da visualizzare nei pop-up. A seconda del visualizzatore, questa funzionalità consente agli utenti di selezionare un punto attivo, un&#39;immagine in miniatura o una mappa immagine per visualizzare informazioni o contenuti correlati.

Quickview è supportato dai seguenti visualizzatori in Dynamic Media:

* Immagine interattiva (punti attivi cliccabili)
* Video interattivo (immagini thumbnail cliccabili durante la riproduzione del video)
* Banner a carosello (punti attivi cliccabili o mappe immagine)

Sebbene le funzionalità di ciascun visualizzatore siano diverse, il processo di creazione di una visualizzazione rapida è lo stesso in tutti e tre i visualizzatori supportati.

**Per creare pop-up personalizzati utilizzando Quickview:**

1. Crea una visualizzazione rapida per una risorsa caricata.

   In genere, quando modifichi una risorsa da utilizzare con il visualizzatore in uso, crei una visualizzazione rapida.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Completa questi passaggi se desideri creare la visualizzazione rapida</strong></td>
    </tr>
    <tr>
    <td>Immagini interattive</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Aggiunta di punti attivi a un banner</a> immagine.</td>
    </tr>
    <tr>
    <td>Video interattivi</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Aggiunta di interattività al video</a>.</td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Aggiunta di punti attivi o mappe immagine a un banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Ottieni il codice di incorporamento del visualizzatore per integrare il visualizzatore all’interno del tuo sito web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong><br /> </td>
    <td><strong>Completa questi passaggi se desideri integrare il visualizzatore con il tuo sito web</strong></td>
    </tr>
    <tr>
    <td>Immagine interattiva</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrazione di un’immagine interattiva con il sito web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Video interattivo<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrazione di un video interattivo con il sito web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina</a> del sito web.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore che stai utilizzando ora deve sapere come utilizzare la visualizzazione rapida.

   Il visualizzatore utilizza un gestore chiamato `QuickViewActive`.

   ****
EsempioSupponiamo di utilizzare il seguente codice di incorporamento nella pagina web per un&#39;immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizzando l&#39;esempio di codice di incorporamento di esempio riportato sopra, è disponibile il seguente codice:**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Per ulteriori informazioni sul metodo `setHandlers()`, consulta:

   * Visualizzatore di immagini interattive: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. È ora necessario configurare il gestore `quickViewActivate`.

   Il gestore `quickViewActivate` controlla la visualizzazione rapida nel visualizzatore. Il gestore contiene l&#39;elenco di variabili e le chiamate di funzioni da utilizzare con Quickview. Il codice di incorporamento fornisce la mappatura della variabile SKU impostata in Quickview e una chiamata della funzione di esempio `loadQuickView`.

   **Variabili**
mappingMap da utilizzare nella pagina Web in base al valore SKU e alle variabili generiche contenute in Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice di incorporamento fornito ha una mappatura di esempio per la variabile SKU:

   `var sku=inData.sku`

   Mappa anche altre variabili dalla visualizzazione rapida, come illustrato di seguito:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **La funzione**
callL&#39;handler richiede anche una chiamata di funzione affinché Quickview funzioni. Si presume che la funzione sia accessibile dalla pagina host. Il codice di incorporamento fornisce un esempio di chiamata della funzione :

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esista e sia accessibile.

   Per ulteriori informazioni sul metodo `quickViewActivate`, consulta:

   * Visualizzatore di immagini interattive: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Supporto dei dati interattivi nel visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Effettua le seguenti operazioni:

   * Rimuovi il commento alla sezione setHandlers del codice di incorporamento.
   * Mappa eventuali variabili aggiuntive contenute nella visualizzazione rapida.

      * Aggiorna la chiamata `loadQuickView(sku,*var1*,*var2*)` se aggiungi ulteriori variabili.
   * Crea una semplice funzione `loadQuickView` () sulla pagina, all’esterno del visualizzatore.

      Ad esempio, il seguente scrive il valore di SKU nella console del browser:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carica una pagina HTML di prova su un server web e apri.

      Con le variabili mappate da Quickview e la chiamata della funzione in atto, la console del browser scrive il valore della variabile nella console del browser utilizzando la funzione di esempio fornita.



1. È ora possibile utilizzare una funzione per richiamare un semplice pop-up in Quickview. Nell&#39;esempio seguente viene utilizzato un elemento `DIV` per un elemento a comparsa.
1. Assegna uno stile al pop-up `DIV` nel modo seguente. Aggiungi lo stile aggiuntivo desiderato.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Posiziona il pop-up `DIV` nel corpo della pagina HTML.

   Uno degli elementi viene impostato con un ID aggiornato con il valore SKU quando l’utente richiama un Quickview. L’esempio include anche un semplice pulsante per nascondere nuovamente la finestra a comparsa quando diventa visibile.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Aggiungi una funzione per aggiornare il valore SKU nel pop-up; rendere il pop-up visibile sostituendo la funzione semplice creata al punto 5. con le seguenti caratteristiche:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carica una pagina HTML di prova sul tuo server web e apri. Il visualizzatore visualizza il pop-up `DIV` quando un utente richiama una visualizzazione rapida.
1. **Come visualizzare il pop-up personalizzato in modalità a schermo intero**

   Alcuni visualizzatori, come il visualizzatore video interattivo, supportano la visualizzazione in modalità a schermo intero. Tuttavia, se si utilizza il pop-up come descritto nei passaggi precedenti, questo viene visualizzato dietro il visualizzatore in modalità a schermo intero.

   Per visualizzare la visualizzazione a comparsa sia in modalità standard che a schermo intero, allegare la finestra a comparsa al contenitore del visualizzatore. Utilizzare un secondo metodo di gestione, `initComplete`.

   Il gestore `initComplete` viene richiamato dopo l&#39;inizializzazione del visualizzatore.

   ```xml
   "initComplete":function() { code block }
   ```

   Per ulteriori informazioni sul metodo `init()`, consulta:

   * Visualizzatore di immagini interattive: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Per allegare al visualizzatore il pop-up descritto nei passaggi precedenti, utilizza il seguente codice:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   Nel codice precedente, è stato fatto quanto segue:

   * Identificato il pop-up personalizzato.
   * È stato rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * È stato allegato il pop-up al contenitore del visualizzatore.

1. L&#39;intero codice setHandlers è simile al seguente (è stato utilizzato il visualizzatore video interattivo):

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. Dopo il caricamento dei gestori, inizializza il visualizzatore:

   `*viewerInstance.*init()`

   ****
EsempioQuesto esempio utilizza il visualizzatore di immagini interattivo.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, assicurati che l’istanza del visualizzatore sia creata e che i gestori siano caricati prima che il visualizzatore venga richiamato utilizzando `init()`.
