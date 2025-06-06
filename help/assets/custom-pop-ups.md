---
title: Creare pop-up personalizzati utilizzando Quickview
description: Il Quickview predefinito viene utilizzato nelle esperienze di e-commerce, mediante le quali viene visualizzato un pop-up con le informazioni di prodotto per stimolare un acquisto. Puoi attivare il contenuto personalizzato da visualizzare nei popup.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# Creare pop-up personalizzati utilizzando Quickview {#using-quickviews-to-create-custom-pop-ups}

Il Quickview predefinito viene utilizzato nelle esperienze di e-commerce, mediante le quali viene visualizzato un pop-up con le informazioni di prodotto per stimolare un acquisto. Tuttavia, puoi attivare il contenuto personalizzato da visualizzare nei pop-up. A seconda del visualizzatore, questa funzionalità consente agli utenti di selezionare un punto attivo, un&#39;immagine in miniatura o una mappa immagine per visualizzare informazioni o contenuti correlati.

Quickview è supportato dai seguenti visualizzatori in Dynamic Medie:

* Immagine interattiva (hotspot cliccabili)
* Video interattivo (miniature cliccabili durante la riproduzione del video)
* Banner a carosello (hotspot cliccabili o mappe immagine)

Sebbene le funzionalità di ciascun visualizzatore siano diverse, il processo di creazione di una visualizzazione rapida è lo stesso per tutti e tre i visualizzatori supportati.

**Per creare popup personalizzati utilizzando Quickview:**

1. Crea una visualizzazione rapida per una risorsa caricata.

   In genere, la creazione di una visualizzazione rapida avviene quando si modifica una risorsa per l’utilizzo con il visualizzatore in uso.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Completare questi passaggi se si desidera creare la visualizzazione rapida</strong></td>
    </tr>
    <tr>
    <td>Immagini interattive</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Aggiunta di punti attivi a un banner immagine</a>.</td>
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

1. Ottieni il codice da incorporare per integrare il visualizzatore nel tuo sito web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong><br /> </td>
    <td><strong>Completa questi passaggi se desideri integrare il visualizzatore con il tuo sito web</strong></td>
    </tr>
    <tr>
    <td>Immagine interattiva</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrazione di un'immagine interattiva con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Video interattivo<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrazione di un video interattivo con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner a carosello</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina del sito Web</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore utilizzato deve sapere come utilizzare Quickview.

   Il visualizzatore utilizza un gestore denominato `QuickViewActive`.

   **Esempio**
Supponiamo di utilizzare il seguente codice di incorporamento di esempio nella pagina web per un’immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Nell&#39;esempio di codice di incorporamento riportato sopra è presente il codice seguente:**

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

   Per ulteriori informazioni sul metodo `setHandlers()`, vedere:

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=it)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=it)

1. Configurare il gestore `quickViewActivate`.

   Il gestore `quickViewActivate` controlla Quickview nel visualizzatore. Il gestore contiene l&#39;elenco delle variabili e le chiamate di funzione da utilizzare con Quickview. Il codice di incorporamento fornisce la mappatura per la variabile SKU impostata in Quickview e un esempio di chiamata alla funzione `loadQuickView`.

   **Mappatura variabile**
Mappa le variabili da utilizzare nella pagina web al valore SKU e alle variabili generiche contenute in Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice di incorporamento fornito ha una mappatura di esempio per la variabile SKU:

   `var sku=inData.sku`

   Mappa variabili aggiuntive anche da Quickview, come nei seguenti casi:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chiamata funzione**
Il gestore richiede anche una chiamata di funzione per il funzionamento di Quickview. Si presume che la funzione sia accessibile dalla pagina host. Il codice di incorporamento fornisce una chiamata di funzione di esempio:

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esista ed è accessibile.

   Per ulteriori informazioni sul metodo `quickViewActivate`, vedere:

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=it)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=it)
   * Supporto dati interattivi nel visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=it)

1. Effettua le seguenti operazioni:

   * Rimuovi il commento dalla sezione setHandlers del codice da incorporare.
   * Mappa eventuali variabili aggiuntive contenute in Quickview.

      * Aggiornare la chiamata `loadQuickView(sku,*var1*,*var2*)` se si aggiungono variabili aggiuntive.

   * Crea una semplice funzione `loadQuickView` () sulla pagina, all&#39;esterno del visualizzatore.

     Ad esempio, il valore SKU viene scritto nella console del browser come segue:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carica una pagina di test HTML in un server web e apri.

     Con le variabili di Quickview mappate e la chiamata di funzione attiva, la console del browser scrive il valore della variabile nella console del browser utilizzando la funzione di esempio fornita.

1. È ora possibile utilizzare una funzione per richiamare una semplice finestra a comparsa in Quickview. Nell&#39;esempio seguente viene utilizzato `DIV` per un popup.
1. Applicare lo stile del popup `DIV` nel modo seguente. Se necessario, aggiungete altri stili.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserire il popup `DIV` nel corpo della pagina HTML.

   Uno degli elementi viene impostato con un ID che viene aggiornato con un valore SKU quando l’utente richiama una Quickview. L&#39;esempio include anche un semplice pulsante per nascondere nuovamente il popup quando diventa visibile.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Aggiungi una funzione in modo da poter aggiornare il valore SKU nel pop-up; rendi visibile il pop-up sostituendo la semplice funzione creata nel passaggio 5. con le seguenti caratteristiche:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carica una pagina di test HTML sul server web e apri. Il visualizzatore visualizza il popup `DIV` quando un utente richiama una visualizzazione rapida.
1. **Visualizzazione del popup personalizzato in modalità a schermo intero**

   Alcuni visualizzatori, come il visualizzatore video interattivo, supportano la visualizzazione a schermo intero. Tuttavia, se si utilizza il pop-up come descritto nei passaggi precedenti, questo viene visualizzato dietro al visualizzatore in modalità a schermo intero.

   Per visualizzare i popup sia nella modalità standard che in quella a schermo intero, collegare il popup al contenitore del visualizzatore. Utilizzare un secondo metodo di gestione, `initComplete`.

   Il gestore `initComplete` viene richiamato dopo l&#39;inizializzazione del visualizzatore.

   ```xml
   "initComplete":function() { code block }
   ```

   Per ulteriori informazioni sul metodo `init()`, vedere:

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=it)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=it](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=it)

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

   Nel codice precedente, è stato eseguito quanto segue:

   * Identificato il pop-up personalizzato.
   * Rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * Il pop-up è stato allegato al contenitore del visualizzatore.

1. L’intero codice setHandlers è simile al seguente (è stato utilizzato il visualizzatore video interattivo):

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

1. Dopo aver caricato i gestori, inizializza il visualizzatore:

   `*viewerInstance.*init()`

   **Esempio**
In questo esempio viene utilizzato il visualizzatore di immagini interattive.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, assicurarsi che l&#39;istanza del visualizzatore sia stata creata e che gli handler siano stati caricati prima che il visualizzatore venga richiamato utilizzando `init()`.
