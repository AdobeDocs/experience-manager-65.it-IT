---
title: Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate
seo-title: Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate
description: La visualizzazione rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Potete attivare il contenuto personalizzato da visualizzare nelle finestre a comparsa.
seo-description: La visualizzazione rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Potete attivare il contenuto personalizzato da visualizzare nelle finestre a comparsa.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 2%

---


# Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

La visualizzazione rapida predefinita viene utilizzata nelle esperienze eCommerce per le quali viene visualizzato un pop-up con le informazioni sul prodotto per guidare un acquisto. Tuttavia, potete attivare il contenuto personalizzato per la visualizzazione nelle finestre a comparsa. A seconda del visualizzatore in uso, questa funzione consente agli utenti di fare clic su un punto di attivazione, una miniatura o una mappa immagine per visualizzare informazioni o contenuti correlati.

Le visualizzazioni rapide sono supportate dai seguenti visualizzatori in Dynamic Media:

* Immagini interattive (aree sensibili selezionabili)
* Video interattivo (immagini in miniatura cliccabili durante la riproduzione di un video)
* Banner carosello (aree sensibili selezionabili o mappe immagine)

Sebbene le funzionalità di ciascun visualizzatore siano diverse, il processo di creazione di una visualizzazione rapida è lo stesso per tutti e tre i visualizzatori supportati.

**Per utilizzare le viste rapida per creare finestre a comparsa personalizzate**

1. Create una visualizzazione rapida per una risorsa caricata.

   In genere, potete creare una visualizzazione rapida contemporaneamente a una risorsa da usare con il visualizzatore in uso.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong></td>
    <td><strong>Completate i seguenti passaggi per creare la visualizzazione rapida</strong></td>
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

1. Ottenete il codice da incorporare del visualizzatore per integrare il visualizzatore nel vostro sito Web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizzatore in uso</strong><br /> </td>
    <td><strong>Completate i seguenti passaggi per integrare il visualizzatore con il sito Web</strong></td>
    </tr>
    <tr>
    <td>Immagine interattiva</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrazione di un’immagine interattiva con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Video interattivo<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrazione di un video interattivo con il sito Web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner carosello</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Aggiunta di un banner carosello alla pagina</a> del sito Web.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Il visualizzatore che state utilizzando ora deve essere in grado di utilizzare la visualizzazione rapida.

   A questo scopo, il visualizzatore utilizza un gestore denominato `QuickViewActive`.

   **Esempio:**
Supponete di usare il seguente codice da incorporare nella pagina Web per un’immagine interattiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   Il gestore viene caricato nel visualizzatore utilizzando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizzando l&#39;esempio di codice da incorporare riportato sopra, è disponibile il seguente codice:**

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

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. È ora necessario configurare il gestore `quickViewActivate`.

   Il gestore `quickViewActivate` controlla le visualizzazioni rapide nel visualizzatore. Il gestore contiene l&#39;elenco di variabili e le chiamate di funzioni da utilizzare con la visualizzazione rapida. Il codice embed fornisce la mappatura per la variabile SKU impostata in Quickview e per una chiamata di funzione `loadQuickView` di esempio.

   **Variabili**
mappingMappa da usare nella pagina Web per ottenere il valore SKU e le variabili generiche contenute in Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   Il codice da incorporare fornito include un esempio di mappatura per la variabile SKU:

   `var sku=inData.sku`

   Mappate anche altre variabili dalla visualizzazione rapida, come segue:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Funzione**
callIl gestore richiede anche una chiamata di funzione per il funzionamento di Quickview. Si presume che la funzione sia accessibile dalla pagina host. Il codice embed fornisce un esempio di chiamata di funzione:

   `loadQuickView(sku)`

   La chiamata della funzione di esempio presuppone che la funzione `loadQuickView()` esista e sia accessibile.

   Per ulteriori informazioni sul metodo `quickViewActivate`, consulta:

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Supporto dei dati interattivi nel visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Effettua le seguenti operazioni:

   * Rimuovete il commento dalla sezione setHandlers del codice da incorporare.
   * Mappare eventuali ulteriori variabili contenute nella visualizzazione rapida.

      * Aggiorna la chiamata `loadQuickView(sku,*var1*,*var2*)` se stai aggiungendo ulteriori variabili.
   * Create una semplice funzione `loadQuickView` () sulla pagina, all&#39;esterno del visualizzatore.

      Ad esempio, il valore sku riportato di seguito viene scritto nella console del browser:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Caricate una pagina HTML di prova su un server Web e apritela.

      Con le variabili di Quickview mappate e la chiamata della funzione in essere, la console del browser scrive il valore della variabile nella console del browser utilizzando la funzione di esempio fornita.



1. È ora possibile utilizzare una funzione per richiamare una semplice finestra a comparsa nella visualizzazione rapida. Nell&#39;esempio seguente viene utilizzato un `DIV` per un popup.
1. Formattare la finestra a comparsa `DIV` nel modo seguente. Aggiungete il vostro stile aggiuntivo come desiderate.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserite il pop-up `DIV` nel corpo della pagina HTML.

   Uno degli elementi è impostato con un ID aggiornato con il valore sku quando l&#39;utente richiama una visualizzazione rapida. L’esempio include anche un semplice pulsante per nascondere nuovamente la finestra a comparsa dopo che questa diventa visibile.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Aggiungete una funzione per aggiornare il valore sku nella finestra a comparsa; rendere il pop-up visibile sostituendo la semplice funzione creata al punto 5. con le seguenti caratteristiche:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Caricate una pagina HTML di prova nel server Web e apritela. Il visualizzatore visualizza la finestra a comparsa `DIV` quando un utente richiama una visualizzazione rapida.
1. **Come visualizzare il pop-up personalizzato in modalità a schermo intero**

   Alcuni visualizzatori, come il visualizzatore per video interattivi, supportano la visualizzazione in modalità a schermo intero. Tuttavia, se si utilizza la finestra a comparsa come descritto nei passaggi precedenti, viene visualizzata dietro il visualizzatore in modalità a schermo intero.

   Per visualizzare la visualizzazione a comparsa sia in modalità standard che a schermo intero, allegate la finestra a comparsa al contenitore del visualizzatore. A tal fine, è possibile utilizzare un secondo metodo di gestione, `initComplete`.

   Il gestore `initComplete` viene richiamato dopo l&#39;inizializzazione del visualizzatore.

   ```xml
   "initComplete":function() { code block }
   ```

   Per ulteriori informazioni sul metodo `init()`, consulta:

   * Visualizzatore immagini interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizzatore video interattivo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Per allegare al visualizzatore la finestra a comparsa descritta nei passaggi precedenti, usate il seguente codice:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   Nel codice riportato sopra, abbiamo fatto quanto segue:

   * Identificato il nostro pop-up personalizzato.
   * Rimosso dal DOM.
   * Identificato il contenitore del visualizzatore.
   * Associata la finestra a comparsa al contenitore del visualizzatore.

1. Il codice setHandlers deve ora essere simile al seguente (è stato utilizzato il visualizzatore video interattivo):

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

1. Dopo aver caricato i gestori, inizializzate il visualizzatore:

   `*viewerInstance.*init()`

   ****
Esempio: in questo esempio viene utilizzato il visualizzatore di immagini interattivo.

   `s7interactiveimageviewer.init()`

   Dopo aver incorporato il visualizzatore nella pagina host, accertatevi che l&#39;istanza del visualizzatore venga creata e che i gestori vengano caricati prima che il visualizzatore venga richiamato utilizzando `init()`.

