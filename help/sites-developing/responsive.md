---
title: Design reattivo per le pagine Web
seo-title: Design reattivo per le pagine Web
description: Con un design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi, in più orientamenti
seo-description: Con un design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi, in più orientamenti
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '5339'
ht-degree: 1%

---


# Design reattivo per pagine Web{#responsive-design-for-web-pages}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad esempio _React_). [Per saperne di più](/help/sites-developing/spa-overview.md).


Progettate le pagine Web in modo che si adattino alla finestra del client in cui vengono visualizzate. Con la progettazione reattiva, le stesse pagine possono essere visualizzate su più dispositivi in entrambi gli orientamenti. L&#39;immagine seguente illustra alcuni modi in cui una pagina può rispondere alle modifiche nelle dimensioni della finestra:

* Layout: Utilizzate i layout a colonna singola per le finestre più piccole e i layout a più colonne per le finestre più grandi.
* Dimensione testo: Utilizzate dimensioni di testo maggiori (se appropriato, come le intestazioni) nelle finestre più grandi.
* Contenuto: Includete solo il contenuto più importante per la visualizzazione su dispositivi più piccoli.
* Navigazione: Sono disponibili strumenti specifici per dispositivi per accedere ad altre pagine.
* Immagini: Trasmissione di rappresentazioni di immagini appropriate per la finestra del client. in base alle dimensioni della finestra.

![chlimage_1-4](assets/chlimage_1-4a.png)

Sviluppare applicazioni Adobe Experience Manager (AEM) che generano pagine HTML5 adattabili a diverse dimensioni e orientamenti di finestre. Ad esempio, i seguenti intervalli di larghezze di visualizzazione corrispondono a vari tipi di dispositivi e orientamenti

* Larghezza massima di 480 pixel (telefono, verticale)
* Larghezza massima di 767 pixel (telefono, orizzontale)
* Larghezza tra 768 pixel e 979 pixel (tablet, verticale)
* Larghezza tra 980 pixel e 1199 pixel (tablet, orizzontale)
* Larghezza uguale o superiore a 1200 px (desktop)

Per informazioni sull’implementazione di comportamenti di progettazione reattivi, consultate i seguenti argomenti:

* [Media query](/help/sites-developing/responsive.md#using-media-queries)
* [Griglie fluide](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Immagini adattive](/help/sites-developing/responsive.md#using-adaptive-images)

Durante la progettazione, utilizzate la barra laterale **[!UICONTROL Sidekick]** per visualizzare in anteprima le pagine per diverse dimensioni di schermo.

## Prima di sviluppare {#before-you-develop}

Prima di sviluppare l’applicazione AEM che supporta le pagine Web, è necessario adottare diverse decisioni di progettazione. Ad esempio, è necessario disporre delle informazioni seguenti:

* I dispositivi di destinazione.
* Dimensioni delle finestre di destinazione.
* Layout di pagina per ciascuna dimensione di visualizzazione di destinazione.

### Struttura dell&#39;applicazione {#application-structure}

La struttura tipica AEM applicazione supporta tutte le implementazioni di design reattivo:

* I componenti della pagina risiedono sotto /apps/*nome_applicazione*/components
* I modelli risiedono sotto /apps/*nome_applicazione*/templates
* Le progettazioni risiedono sotto /etc/designs

## Utilizzo di media query {#using-media-queries}

Le media query consentono l&#39;uso selettivo di stili CSS per il rendering della pagina. AEM strumenti e funzionalità di sviluppo consentono di implementare in modo efficace ed efficiente le media query nelle applicazioni.

Il gruppo W3C fornisce la raccomandazione [Media Query](https://www.w3.org/TR/css3-mediaqueries/) che descrive questa funzione CSS3 e la sintassi.

### Creazione del file CSS {#creating-the-css-file}

Nel file CSS, definite le query multimediali in base alle proprietà dei dispositivi di destinazione. La seguente strategia di implementazione è efficace per la gestione degli stili per ogni media query:

* Utilizzate ClientLibraryFolder per definire il CSS assemblato al momento del rendering della pagina.
* Definite ogni media query e gli stili associati in file CSS separati. È utile utilizzare nomi di file che rappresentano le caratteristiche del dispositivo della query multimediale.
* Definire stili comuni a tutti i dispositivi in un file CSS separato.
* Nel file css.txt di ClientLibraryFolder, ordinate i file CSS dell&#39;elenco come richiesto nel file CSS assemblato.

L’esempio We.Retail Media utilizza questa strategia per definire gli stili nella progettazione del sito. Il file CSS utilizzato da We.Retail si trova in `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

Nella tabella seguente sono elencati i file presenti nella cartella figlio css.

<table>
 <tbody>
  <tr>
   <th>Nome file</th>
   <th>Descrizione</th>
   <th>Media Query</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Stili comuni.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Stili comuni, definiti dall’Bootstrap di Twitter.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Stili per tutti i file multimediali con larghezza o larghezza pari a 1200 pixel.</td>
   <td><p>@media (larghezza minima: 1200px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Stili per file multimediali con una larghezza compresa tra 980 e 1199 pixel.</td>
   <td><p>@media (larghezza minima: 980 px) e (max-width: 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Stili per file multimediali con una larghezza compresa tra 768 e 979 pixel. </td>
   <td><p>@media (larghezza minima: 768 px) e (max-width: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Stili per tutti i file multimediali con larghezza inferiore a 768 pixel.</td>
   <td><p>@media (larghezza max: 767px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Stili per tutti i file multimediali con larghezza inferiore a 481 pixel.</td>
   <td>@media (larghezza max: 480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

Il file css.txt presente nella cartella `/etc/designs/weretail/clientlibs` elenca i file CSS inclusi nella cartella della libreria client. L&#39;ordine dei file implementa la precedenza degli stili. Gli stili sono più specifici quando la dimensione del dispositivo diminuisce.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**Suggerimento**: I nomi dei file descrittivi consentono di identificare facilmente le dimensioni della finestra di destinazione.

### Utilizzo di Media Query con AEM pagine {#using-media-queries-with-aem-pages}

Includete la cartella della libreria client nello script JSP del componente della pagina per generare il file CSS che include le media query e per fare riferimento al file.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>La cartella della libreria client `apps.weretail.all` contiene la libreria clientlibs.

Lo script JSP genera il seguente codice HTML che fa riferimento ai fogli di stile:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Anteprima per dispositivi specifici {#previewing-for-specific-devices}

Potete vedere le anteprime delle pagine in diverse dimensioni di visualizzazione per verificare il comportamento del design reattivo. In modalità **[!UICONTROL Anteprima]**, **[!UICONTROL Barra laterale]** include un menu a discesa **[!UICONTROL Dispositivi]** che consente di selezionare un dispositivo. Quando selezionate un dispositivo, la pagina cambia per adattarsi alle dimensioni della finestra.

![chlimage_1-5](assets/chlimage_1-5a.png)

Per abilitare l&#39;anteprima del dispositivo in **[!UICONTROL Barra laterale]**, è necessario configurare la pagina e il servizio **[!UICONTROL MobileEmulatorProvider]**. Un&#39;altra configurazione di pagina controlla l&#39;elenco dei dispositivi che viene visualizzato nell&#39;elenco **[!UICONTROL Dispositivi]**.

### Aggiunta dell&#39;elenco dei dispositivi {#adding-the-devices-list}

L&#39;elenco **[!UICONTROL Dispositivi]** viene visualizzato in **[!UICONTROL Barra laterale]** quando la pagina include lo script JSP che esegue il rendering dell&#39;elenco **[!UICONTROL Dispositivi]**. Per aggiungere l&#39;elenco **[!UICONTROL Dispositivi]** a **[!UICONTROL Barra laterale]**, includete lo script `/libs/wcm/mobile/components/simulator/simulator.jsp` nella sezione `head` della pagina.

Includete il seguente codice nella JSP che definisce la sezione `head`:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Per visualizzare un esempio, aprire il file `/apps/weretail/components/page/head.jsp` in CRXDE Lite.

### Registrazione dei componenti pagina per la simulazione {#registering-page-components-for-simulation}

Per abilitare il simulatore dispositivo per il supporto delle pagine, registrate i componenti di pagina con il servizio di fabbrica MobileEmulatorProvider e definite la proprietà `mobile.resourceTypes`.

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Ad esempio, per creare un nodo ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` nell&#39;applicazione:

* Cartella principale: `/apps/application_name/config`
* Nome: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   Il suffisso - `*alias*` è richiesto perché il servizio MobileEmulatorProvider è un servizio di fabbrica. Utilizzate qualsiasi alias univoco per la fabbrica.

* jcr:primaryType: `sling:OsgiConfig`

Aggiungi la seguente proprietà node:

* Nome: `mobile.resourceTypes`
* Tipo: `String[]`
* Valore: I percorsi dei componenti della pagina che eseguono il rendering delle pagine Web. Ad esempio, l&#39;app geometrixx-media utilizza i valori seguenti:

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Specifica dei gruppi di dispositivi {#specifying-the-device-groups}

Per specificare i gruppi di dispositivi che vengono visualizzati nell&#39;elenco Dispositivi, aggiungere una proprietà `cq:deviceGroups` al nodo `jcr:content` della pagina principale del sito. Il valore della proprietà è un array di percorsi ai nodi del gruppo di dispositivi.

I nodi dei gruppi di dispositivi si trovano nella cartella `/etc/mobile/groups`.

Ad esempio, la pagina principale del sito Geometrixx Media è `/content/geometrixx-media`. Il nodo `/content/geometrixx-media/jcr:content` include la proprietà seguente:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valore: `/etc/mobile/groups/responsive`

Utilizzare la console Strumenti per [creare e modificare gruppi di dispositivi](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Per i gruppi di dispositivi utilizzati per la progettazione reattiva, modificate il gruppo di dispositivi e, nella scheda Generale, selezionate Disattiva emulatore. Questa opzione impedisce la visualizzazione del carosello dell&#39;emulatore, che non è pertinente alla progettazione reattiva.


## Utilizzo di immagini adattive {#using-adaptive-images}

Potete utilizzare le media query per selezionare una risorsa immagine da visualizzare nella pagina. Tuttavia, tutte le risorse che utilizzano una query multimediale per condizionale del relativo utilizzo vengono scaricate nel client. La media query determina semplicemente se la risorsa scaricata viene visualizzata.

Per risorse di grandi dimensioni, come le immagini, il download di tutte le risorse non è un uso efficiente della pipeline dei dati del client. Per scaricare selettivamente le risorse, utilizzate javascript per avviare la richiesta di risorse dopo che le media query avranno eseguito la selezione.

La strategia seguente carica una singola risorsa selezionata utilizzando le media query:

1. Aggiungete un elemento DIV per ciascuna versione della risorsa. Includete l’URI della risorsa come valore di un attributo. Il browser non interpreta l&#39;attributo come risorsa.
1. Aggiungete una query multimediale a ciascun elemento DIV appropriato per la risorsa.
1. Quando il documento viene caricato o la finestra viene ridimensionata, il codice JavaScript verifica la query multimediale di ciascun elemento DIV.
1. In base ai risultati delle query, determinare quale risorsa includere.
1. Inserite un elemento HTML nel DOM che fa riferimento alla risorsa.

### Valutazione delle query multimediali utilizzando Javascript {#evaluating-media-queries-using-javascript}

Le implementazioni dell&#39; [interfaccia MediaQueryList](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface) definita dal W3C consentono di valutare le query multimediali utilizzando javascript. È possibile applicare la logica ai risultati delle query multimediali ed eseguire script destinati alla finestra corrente:

* I browser che implementano l&#39;interfaccia MediaQueryList supportano la funzione `window.matchMedia()`. Questa funzione verifica le query multimediali rispetto a una stringa specificata. La funzione restituisce un oggetto `MediaQueryList` che fornisce l&#39;accesso ai risultati della query.

* Per i browser che non implementano l&#39;interfaccia, è possibile utilizzare un `matchMedia()` polifill, ad esempio [matchMedia.js](https://github.com/paulirish/matchMedia.js), una libreria javascript disponibile liberamente.

#### Selezione di risorse specifiche per i supporti {#selecting-media-specific-resources}

L&#39;elemento [picture](https://picture.responsiveimages.org/) proposto da W3C utilizza query multimediali per determinare l&#39;origine da utilizzare per gli elementi immagine. L’elemento picture utilizza gli attributi dell’elemento per associare le query multimediali ai percorsi immagine.

La libreria [picturefill.js disponibile liberamente fornisce funzionalità simili all&#39;elemento `picture` proposto e utilizza una strategia simile. ](https://github.com/scottjehl/picturefill) La libreria picturefill.js chiama `window.matchMedia` per valutare le media query definite per un set di elementi `div`. Ogni elemento `div` specifica anche una sorgente immagine. L&#39;origine viene utilizzata quando la query multimediale dell&#39;elemento `div` restituisce `true`.

La libreria `picturefill.js` richiede codice HTML simile al seguente esempio:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Quando viene eseguito il rendering della pagina, picturefull.js inserisce un elemento `img` come ultimo figlio dell&#39;elemento `<div data-picture>`:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

In una pagina AEM, il valore dell&#39;attributo `data-src` è il percorso di una risorsa nella directory archivio.

### Implementazione di immagini adattive in AEM {#implementing-adaptive-images-in-aem}

Per implementare le immagini adattive nell&#39;applicazione AEM, è necessario aggiungere le librerie javascript necessarie e includere nelle pagine il codice HTML richiesto.

**Librerie**

Ottenete le seguenti librerie JavaScript e includetele in una cartella libreria client:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js)  (per i browser che non implementano l&#39;interfaccia MediaQueryList)
* [pitturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponibile tramite la cartella della libreria client `/etc/clientlibs/granite/jquery` (categoria = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (evento jquery che si verifica una volta dopo il ridimensionamento della finestra)

**Suggerimento:** puoi concatenare automaticamente più cartelle libreria client  [incorporando](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Create un componente che generi gli elementi div richiesti dal codice picturefill.js. In una pagina AEM, il valore dell’attributo data-src è il percorso di una risorsa nell’archivio. Ad esempio, un componente di pagina può codificare le media query e i percorsi associati per le rappresentazioni di immagini in DAM. Oppure, create un componente Immagine personalizzato che consenta agli autori di selezionare le rappresentazioni delle immagini o di specificare le opzioni di rendering in fase di esecuzione.

L&#39;esempio seguente HTML seleziona da 2 rappresentazioni DAM della stessa immagine.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>Il componente Immagine adattiva foundation implementa le immagini adattive:
>
>* Cartella libreria client: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script che genera l’HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`

>
>
La sezione successiva fornisce dettagli su questo componente.


### Rendering delle immagini in AEM {#understanding-image-rendering-in-aem}

Per personalizzare il rendering delle immagini, è necessario comprendere l’implementazione predefinita AEM rendering delle immagini statiche. AEM fornisce il componente Immagine e un servlet per il rendering delle immagini che funzionano insieme per il rendering delle immagini per la pagina Web. La seguente sequenza di eventi si verifica quando il componente Immagine viene incluso nel sistema paragrafo della pagina:

1. Authoring: Gli autori possono modificare il componente Immagine per specificare il file immagine da includere in una pagina HTML. Il percorso del file è memorizzato come valore di proprietà del nodo del componente Immagine.
1. Richiesta pagina: Il JSP del componente pagina genera il codice HTML. La JSP del componente Immagine genera e aggiunge un elemento img alla pagina.
1. Richiesta immagine: Il browser Web carica la pagina e richiede l’immagine in base all’attributo src dell’elemento img.
1. Rendering delle immagini: Il servlet di rendering delle immagini restituisce l’immagine al browser Web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Ad esempio, la JSP del componente Immagine genera il seguente elemento HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Quando il browser carica la pagina, richiede l’immagine utilizzando il valore dell’attributo src come URL. Sling scompone l’URL:

* Risorsa: `/content/mywebsite/en/_jcr_content/par/image_0`
* Estensione nome file: `.jpg`
* Selettore: `img`
* Suffisso: `1358372073597.jpg`

Il nodo `image_0` ha un valore `jcr:resourceType` di `foundation/components/image`, che ha un valore `sling:resourceSuperType` di `foundation/components/parbase`. Il componente parbase include lo script img.GET.java che corrisponde al selettore e all’estensione del nome del file dell’URL della richiesta. CQ utilizza questo script (servlet) per eseguire il rendering dell’immagine.

Per visualizzare il codice sorgente dello script, utilizzare CRXDE Lite per aprire il `/libs/foundation/components/parbase/img.GET.java`
file.

## Ridimensionamento delle immagini per la dimensione della finestra corrente {#scaling-images-for-the-current-viewport-size}

Adatta le immagini in fase di esecuzione in base alle caratteristiche della finestra del client per fornire immagini conformi ai principi di responsive design. Usate lo stesso pattern di progettazione del rendering di immagini statiche, utilizzando un servlet e un componente di authoring.

Il componente deve eseguire le seguenti operazioni:

* Memorizzate il percorso e le dimensioni desiderate della risorsa immagine come valori delle proprietà.
* Generare elementi `div` che contengono selettori di supporti e chiamate di servizi per il rendering dell&#39;immagine.

>[!NOTE]
>
>Il client Web utilizza le librerie javascript matchMedia e Picturefill (o librerie simili) per valutare i selettori dei contenuti multimediali.


Il servlet che elabora la richiesta di immagine deve eseguire le seguenti operazioni:

* Recuperate il percorso e le dimensioni dell’immagine dalle proprietà del componente.
* Consente di ridimensionare l&#39;immagine in base alle proprietà e di restituire l&#39;immagine.

**Soluzioni disponibili**

AEM le seguenti implementazioni che potete utilizzare o estendere.

* Il componente Immagine adattiva che genera media query e le richieste HTTP al Servlet componente Immagine adattiva che ridimensiona le immagini.
* Il pacchetto Geometrixx Commons installa i servlet di esempio Image Reference Modification Servlet che modificano la risoluzione delle immagini.

### Informazioni sul componente Immagine adattiva {#understanding-the-adaptive-image-component}

Il componente Immagine adattiva genera chiamate al Servlet del componente Immagine adattiva per rappresentare un’immagine ridimensionata in base alla schermata del dispositivo. Il componente include le risorse seguenti:

* JSP: Aggiunge elementi div che associano le query multimediali alle chiamate al servlet componente immagine adattivo.
* Librerie client: La cartella clientlibs è una `cq:ClientLibraryFolder` che assembla la libreria javascript matchMedia Polyfill e una libreria javascript Picturefill modificata.
* Finestra di dialogo di modifica: Il nodo `cq:editConfig` sostituisce il componente immagine di base CQ in modo che la destinazione di rilascio crei un componente immagine adattiva anziché un componente immagine di base.

#### Aggiunta di elementi DIV {#adding-the-div-elements}

Lo script adaptive-image.jsp include il seguente codice che genera elementi div e media query:

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

La variabile `path` contiene il percorso della risorsa corrente (il nodo componente immagine adattiva). Il codice genera una serie di elementi `div` con la seguente struttura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

Il valore dell&#39;attributo `data-scr` è un URL che Sling risolve al Servlet componente immagine adattiva che esegue il rendering dell&#39;immagine. L&#39;attributo data-media contiene la query multimediale valutata in base alle proprietà client.

Il seguente codice HTML è un esempio degli elementi `div` generati dalla JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Modifica dei selettori delle dimensioni dell&#39;immagine {#changing-the-image-size-selectors}

Se personalizzate il componente Immagine adattiva e modificate i selettori di larghezza, dovete anche configurare il Servlet componente Immagine adattiva per supportare le larghezze.

### Il servlet componente immagine adattiva {#understanding-the-adaptive-image-component-servlet}

Il Servlet del componente Immagine adattiva ridimensiona un’immagine JPEG in base alla larghezza specificata e imposta la qualità JPEG.

#### Interfaccia del servlet componente immagine adattiva {#the-interface-of-the-adaptive-image-component-servlet}

Il Servlet componente immagine adattiva è associato al servlet Sling predefinito e supporta le estensioni di file .jpg, .jpeg, .gif e .png. Il selettore servlet è img.

>[!CAUTION]
>
>I file .gif animati non sono supportati in AEM per le rappresentazioni adattive.

Sling risolve quindi gli URL di richieste HTTP nel seguente formato a questo servlet:

`*path-to-node*.img.*extension*`

Ad esempio, Sling inoltra le richieste HTTP con l&#39;URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` al servlet componente immagine adattiva.

Due selettori aggiuntivi specificano la larghezza dell’immagine richiesta e la qualità JPEG. L’esempio seguente richiede un’immagine di larghezza di 480 pixel e qualità media:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Proprietà immagine supportate**

Il servlet accetta un numero limitato di larghezze e qualità delle immagini. Per impostazione predefinita, sono supportate le seguenti larghezze (in pixel):

* completo
* 320
* 480
* 476
* 620

Il valore intero non indica alcuna modifica in scala.

Sono supportati i seguenti valori per la qualità JPEG:

* BASSA
* MEDIO
* ALTO

I valori numerici sono rispettivamente 0,4, 0,82 e 1,0.

**Modifica delle larghezze supportate predefinite**

Utilizzate la console Web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) o un nodo sling:OsgiConfig per configurare le larghezze supportate dal  Servlet componente immagine adattivo Adobe CQ.

Per informazioni su come configurare AEM servizi, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Console Web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Nome servizio o nodo</th>
   <td>Il nome del servizio nella scheda Configurazione è  Servlet componente immagine adattiva Adobe CQ</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Proprietà</th>
   <td><p>Larghezze supportate</p>
    <ul>
     <li>Per aggiungere una larghezza supportata, fate clic su un pulsante + e immettete un numero intero positivo.</li>
     <li>Per rimuovere una larghezza supportata, fate clic sul pulsante associato -.</li>
     <li>Per modificare una larghezza supportata, modificare il valore del campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>La proprietà è un valore String multivalore.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Dettagli di implementazione {#implementation-details}

La classe `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` estende la classe [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). Il codice sorgente AdaptiveImageComponentServlet si trova nella cartella `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`.

La classe utilizza le annotazioni SCR Felix per configurare il tipo di risorsa e l&#39;estensione di file a cui è associato il servlet, nonché il nome del primo selettore.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

Il servlet utilizza l&#39;annotazione SCR di proprietà per impostare la qualità e le dimensioni dell&#39;immagine supportate predefinite.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

La classe `AbstractImageServlet` fornisce il metodo `doGet` che elabora la richiesta HTTP. Questo metodo determina la risorsa associata alla richiesta, recupera le proprietà della risorsa dall&#39;archivio e le restituisce in un oggetto [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

>[!NOTE]
>
>La classe [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) fornisce `getFileReference method`, che recupera il valore della proprietà `fileReference` della risorsa.

La classe `AdaptiveImageComponentServlet` sostituisce il metodo `createLayer`. Il metodo ottiene il percorso della risorsa immagine e la larghezza dell&#39;immagine richiesta dall&#39;oggetto `ImageContext`. Quindi, richiama i metodi della classe `info.geometrixx.commons.impl.AdaptiveImageHelper`, che esegue il ridimensionamento effettivo dell&#39;immagine.

Anche la classe AdaptiveImageComponentServlet sostituisce il metodo writeLayer. Questo metodo applica la qualità JPEG all’immagine.

### Servlet modifica riferimento immagine (Geometrixx comune) {#image-reference-modification-servlet-geometrixx-common}

Il servlet di modifica Riferimento immagine di esempio genera attributi di dimensione per l’elemento img per ridimensionare un’immagine sulla pagina Web.

#### Chiamata del servlet {#calling-the-servlet}

Il servlet è associato a `cq:page` risorse e supporta l&#39;estensione .jpg. Il selettore servlet è `image`. Sling risolve quindi gli URL di richieste HTTP nel seguente formato a questo servlet:

`path-to-page-node.image.jpg`

Ad esempio, Sling inoltra le richieste HTTP con l’URL `http://localhost:4502/content/geometrixx/en.image.jpg` a Image Reference Modification Servlet.

Tre selettori aggiuntivi specificano la larghezza, l’altezza e la qualità dell’immagine richiesta (facoltativamente). L’esempio seguente richiede un’immagine di larghezza 770 pixel, altezza 360 pixel e di qualità media.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Proprietà immagine supportate**

Il servlet accetta un numero finito di dimensioni immagine e valori di qualità.

I seguenti valori sono supportati per impostazione predefinita (widthheight):

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

Sono supportati i seguenti valori per la qualità delle immagini:

* Bassa
* Media
* Alta

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

#### Specifica della risorsa immagine {#specifying-the-image-resource}

Il percorso dell&#39;immagine, le dimensioni e i valori di qualità devono essere memorizzati come proprietà di un nodo nell&#39;archivio:

* Il nome del nodo è `image`.
* Il nodo principale è il nodo `jcr:content` di una risorsa `cq:page`.

* Il percorso dell&#39;immagine viene memorizzato come valore di una proprietà denominata `fileReference`.

Durante la creazione di una pagina, utilizzare la barra laterale **per specificare l&#39;immagine e aggiungere il nodo `image` alle proprietà della pagina:**

1. In **Barra laterale**, fare clic sulla scheda **Pagina**, quindi fare clic su **Proprietà pagina**.
1. Fare clic sulla scheda **Immagine** e specificare l&#39;immagine.
1. Fai clic su **OK**.

#### Dettagli di implementazione {#implementation-details-1}

La classe info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet estende la classe [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). Se avete installato il pacchetto cq-geometrixx-commons-pkg, il codice sorgente ImageReferenceModificationServlet si trova nella cartella `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`.

La classe utilizza le annotazioni SCR Felix per configurare il tipo di risorsa e l&#39;estensione di file a cui è associato il servlet, nonché il nome del primo selettore.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

Il servlet utilizza l&#39;annotazione SCR di proprietà per impostare la qualità e le dimensioni dell&#39;immagine supportate predefinite.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

La classe `AbstractImageServlet` fornisce il metodo `doGet` che elabora la richiesta HTTP. Questo metodo determina la risorsa associata alla chiamata, recupera le proprietà delle risorse dall&#39;archivio e le salva in un oggetto [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html).

La classe `ImageReferenceModificationServlet` sostituisce il metodo `createLayer` e implementa la logica che determina la risorsa immagine da eseguire. Il metodo recupera un nodo secondario del nodo `jcr:content` della pagina denominato `image`. Da questo nodo `image` viene creato un oggetto [Image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) e il metodo `getFileReference` restituisce il percorso del file di immagine dalla proprietà `fileReference` del nodo di immagine.

>[!NOTE]
>La classe [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) fornisce il metodo getFileReference.


## Sviluppo di una griglia fluida {#developing-a-fluid-grid}

AEM consente di implementare in modo efficiente ed efficace le griglie fluide. In questa pagina viene illustrato come integrare la griglia fluida o un&#39;implementazione esistente della griglia (ad esempio [Bootstrap](https://twitter.github.com/bootstrap/)) nell&#39;applicazione AEM.

Se non avete familiarità con le griglie fluide, consultate la sezione [Introduzione alle griglie fluide](/help/sites-developing/responsive.md#developing-a-fluid-grid) nella parte inferiore della pagina. Questa introduzione fornisce una panoramica delle griglie fluide e indicazioni per la loro progettazione.

### Definizione della griglia con un componente Pagina {#defining-the-grid-using-a-page-component}

Utilizzare i componenti pagina per generare gli elementi HTML che definiscono i blocchi di contenuto della pagina. ClientLibraryFolder a cui fa riferimento la pagina fornisce il CSS che controlla il layout dei blocchi di contenuto:

* Componente pagina: Aggiunge elementi div che rappresentano le righe dei blocchi di contenuto. Gli elementi div che rappresentano i blocchi di contenuto includono un componente parsys in cui gli autori aggiungono contenuto.
* Cartella libreria client: Fornisce il file CSS che include query multimediali e stili per gli elementi div.

Ad esempio, l’applicazione geometrixx-media di esempio contiene il componente media-home. Questo componente di pagina inserisce due script, che generano due elementi `div` della classe `row-fluid`:

* La prima riga contiene un elemento `div` della classe `span12` (il contenuto si estende su 12 colonne). L&#39;elemento `div` contiene il componente parsys.

* La seconda riga contiene due elementi `div`, uno della classe `span8` e l&#39;altro della classe `span4`. Ogni elemento `div` include il componente parsys.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>Quando un componente include più elementi `cq:include` che fanno riferimento al componente parsys, ogni attributo `path` deve avere un valore diverso.


#### Ridimensionamento della griglia del componente Pagina {#scaling-the-page-component-grid}

La struttura associata al componente pagina geometrixx-media (`/etc/designs/geometrixx-media`) contiene la cartella `clientlibs` ClientLibraryFolder. Questa ClientLibraryFolder definisce gli stili CSS per le classi `row-fluid`, `span*` e `span*` che sono elementi secondari di classi `row-fluid`. Le media query consentono di ridefinire gli stili per diverse dimensioni di visualizzazione.

Il seguente esempio di CSS è un sottoinsieme di tali stili. Questo sottoinsieme si concentra sulle classi `span12`, `span8` e `span4` e sulle query multimediali per due dimensioni di finestra. Osservate le seguenti caratteristiche del CSS:

* Gli stili `.span` definiscono le larghezze degli elementi utilizzando numeri assoluti.
* Gli stili `.row-fluid .span*` definiscono le larghezze degli elementi come percentuali del padre. Le percentuali sono calcolate a partire dalle larghezze assolute.
* Le query multimediali per le finestre più grandi assegnano larghezze assolute maggiori.

>[!NOTE]
>
>L&#39;esempio di Geometrixx Media integra il framework javascript [Bootstrap](https://twitter.github.com/bootstrap/javascript.html) nella relativa implementazione della griglia fluida. Il framework di Bootstrap fornisce il file bootstrap.css.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Riposizionamento del contenuto nella griglia dei componenti Pagina {#repositioning-content-in-the-page-component-grid}

Le pagine dell’applicazione Geometrixx Media di esempio distribuiscono le righe dei blocchi di contenuto orizzontalmente in viste ampie. Nelle finestre più piccole, gli stessi blocchi sono distribuiti in verticale. L&#39;esempio CSS seguente mostra gli stili che implementano questo comportamento per il codice HTML generato dal componente pagina media-home:

* Il CSS predefinito per la pagina di benvenuto multimediale assegna lo stile `float:left` per le classi `span*` che si trovano all&#39;interno di `row-fluid` classi.

* Le query multimediali per le finestre più piccole assegnano lo stile `float:none` per le stesse classi.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modulare i componenti della pagina {#tip-modularize-your-page-components}

Modularizzare i componenti per un utilizzo efficiente del codice. Probabilmente il sito utilizza diversi tipi di pagine, come una pagina di benvenuto, una pagina di articolo o una pagina di prodotto. Ogni tipo di pagina contiene diversi tipi di contenuto e probabilmente utilizza layout diversi. Tuttavia, quando alcuni elementi di ciascun layout sono comuni tra più pagine, potete riutilizzare il codice che implementa quella parte del layout.

**Utilizzare le sovrapposizioni di componenti pagina**

Creare un componente di pagina principale che fornisca script per la generazione delle varie parti di una pagina, come le sezioni `head` e `body`, `header`, `content` e `footer` all&#39;interno del corpo.

Create altri componenti di pagina che utilizzano il componente pagina principale come `cq:resourceSuperType`. Questi componenti includono script che ignorano gli script della pagina principale in base alle esigenze.

Ad esempio, l’applicazione goemetrixx-media include il componente pagina (il `sling:resourceSuperType` è il componente pagina di base). Diversi componenti secondari (come articolo, categoria e media-home) utilizzano questo componente di pagina come `sling:resourceSuperType`. Ogni componente secondario include un file content.jsp che sostituisce il file content.jsp del componente pagina.

**Riutilizzare gli script**

Creare più script JSP che generano combinazioni di righe e colonne comuni per più componenti di pagina. Ad esempio, lo script `content.jsp` dell&#39;articolo e i componenti Media-home fanno riferimento entrambi allo script `8x4col.jsp`.

**Organizzare gli stili CSS in base alle dimensioni della finestra di destinazione**

Includere stili CSS e query multimediali per diverse dimensioni di visualizzazione in file separati. Utilizzate le cartelle della libreria client per concatenarle.

### Inserimento di componenti nella griglia delle pagine {#inserting-components-into-the-page-grid}

Quando i componenti generano un singolo blocco di contenuto, in genere la griglia definita dal componente pagina controlla la posizione del contenuto.

Gli autori devono essere consapevoli del fatto che il blocco di contenuto può essere rappresentato in varie dimensioni e posizioni relative. Il testo del contenuto non deve utilizzare direzioni relative per fare riferimento ad altri blocchi di contenuto.

Se necessario, il componente deve fornire qualsiasi libreria CSS o javascript necessaria per il codice HTML generato. Usate una cartella libreria client all’interno del componente per generare i file CSS e JS. Per esporre i file, [creare una dipendenza o incorporare la libreria](/help/sites-developing/clientlibs.md#creating-client-library-folders) in un&#39;altra cartella della libreria client sotto la cartella /etc.

**Sottocartelle**

Se il componente contiene più blocchi di contenuto, aggiungete i blocchi di contenuto all’interno di una riga per creare una sottogriglia sulla pagina:

* Utilizzate gli stessi nomi di classe del componente di pagina contenitore per esprimere elementi div come righe e blocchi di contenuto.
* Per ignorare il comportamento che il CSS della progettazione di pagina implementa, utilizzate un nome di seconda classe per l&#39;elemento div della riga e fornite il CSS associato in una cartella libreria client.

Ad esempio, il componente `/apps/geometrixx-media/components/2-col-article-summary` genera due colonne di contenuto. L’HTML generato ha la struttura seguente:

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

I selettori `.row-fluid .span6` del CSS della pagina si applicano agli elementi `div` della stessa classe e struttura in questo HTML. Tuttavia, il componente include anche la cartella /apps/geometrixx-media/components/2-col-article-summary/clientlibs della libreria client:

* Il CSS utilizza le stesse query multimediali del componente pagina per stabilire le modifiche nel layout alle stesse larghezze di pagina discrete.
* I selettori utilizzano la classe `multi-col-article-summary` dell&#39;elemento riga `div` per ignorare il comportamento della classe `row-fluid` della pagina.

Ad esempio, nel file `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` sono inclusi i seguenti stili:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Introduzione alle griglie fluide {#introduction-to-fluid-grids}

Le griglie fluide consentono ai layout di pagina di adattarsi alle dimensioni della finestra del client. Le griglie sono costituite da colonne logiche e righe che posizionano i blocchi di contenuto sulla pagina.

* Le colonne determinano le posizioni orizzontali e le larghezze dei blocchi di contenuto.
* Le righe determinano le posizioni verticali relative dei blocchi di contenuto.

Con la tecnologia HTML5 potete implementare la griglia e manipolarla per adattare i layout di pagina a diverse dimensioni di visualizzazione:

* Gli elementi HTML `div` contengono blocchi di contenuto che si estendono su un certo numero di colonne.
* Uno o più di questi elementi div comprendono una riga quando condividono un elemento div padre comune.

### Utilizzo di larghezze discrete {#using-discrete-widths}

Per ogni intervallo di larghezze di visualizzazione di destinazione, utilizzate una larghezza di pagina statica e blocchi di contenuto con larghezza costante. Quando si ridimensiona manualmente una finestra del browser, le modifiche alla dimensione del contenuto vengono apportate a larghezze di finestre discrete (dette anche punti di interruzione). Di conseguenza, le progettazioni di pagina sono maggiormente rispettate, ottimizzando l&#39;esperienza dell&#39;utente.

#### Ridimensionamento della griglia {#scaling-the-grid}

Utilizzate le griglie per ridimensionare i blocchi di contenuto per adattarli a dimensioni di visualizzazione diverse. I blocchi di contenuto si estendono su un numero specifico di colonne. Poiché le larghezze delle colonne aumentano o diminuiscono per adattarsi a diverse dimensioni di visualizzazione, la larghezza dei blocchi di contenuto aumenta o diminuisce di conseguenza. Il ridimensionamento può supportare sia i visualizzatori di grandi e medie dimensioni sufficientemente larghi da adattarsi alla posizione affiancata dei blocchi di contenuto.

![](do-not-localize/chlimage_1-1a.png)

#### Riposizionamento del contenuto nella griglia {#repositioning-content-in-the-grid}

Le dimensioni dei blocchi di contenuto possono essere vincolate da una larghezza minima, oltre la quale il ridimensionamento non è più efficace. Per le finestre più piccole, la griglia può essere utilizzata per distribuire verticalmente blocchi di contenuto anziché orizzontalmente.

![](do-not-localize/chlimage_1-2a.png)

### Progettazione della griglia {#designing-the-grid}

Determinare le colonne e le righe necessarie per posizionare i blocchi di contenuto sulle pagine. I layout di pagina determinano il numero di colonne e righe che si estendono sulla griglia.

**Numero di colonne**

Includete un numero sufficiente di colonne per posizionare in orizzontale i blocchi di contenuto in tutti i layout, per tutte le dimensioni delle finestre. È consigliabile utilizzare più colonne di quelle attualmente necessarie per adattare le progettazioni di pagina future.

**Contenuto riga**

Utilizzare le righe per controllare il posizionamento verticale dei blocchi di contenuto. Determinare i blocchi di contenuto che condividono la stessa riga:

* I blocchi di contenuto che si trovano l&#39;uno accanto all&#39;altro in orizzontale in uno qualsiasi dei layout si trovano nella stessa riga.
* I blocchi di contenuto situati uno accanto all&#39;altro in orizzontale (finestre più ampie) e in verticale (finestre più piccole) si trovano nella stessa riga.

### Implementazioni griglia {#grid-implementations}

Creare classi e stili CSS per controllare il layout dei blocchi di contenuto su una pagina. Le strutture delle pagine sono spesso basate sulle dimensioni e la posizione relative dei blocchi di contenuto all&#39;interno della finestra della vista. La finestra di visualizzazione determina la dimensione effettiva dei blocchi di contenuto. Il CSS deve tenere conto delle dimensioni relative e assolute. Potete implementare una griglia fluida utilizzando tre tipi di classi CSS:

* Una classe per un elemento `div` che è un contenitore per tutte le righe. Questa classe imposta la larghezza assoluta della griglia.
* Una classe per gli elementi `div` che rappresentano una riga. Questa classe controlla il posizionamento orizzontale o verticale dei blocchi di contenuto in essa contenuti.
* Classi per gli elementi `div` che rappresentano blocchi di contenuto di diverse larghezze. Le larghezze sono espresse come percentuale della riga padre.

Le larghezze delle finestre di destinazione (e le relative query multimediali associate) delimitano le larghezze discrete utilizzate per un layout di pagina.

#### Larghezza dei blocchi di contenuto {#widths-of-content-blocks}

In genere, lo stile `width` delle classi di blocchi di contenuto si basa sulle seguenti caratteristiche della pagina e della griglia:

* Larghezza di pagina assoluta utilizzata per ogni dimensione di visualizzazione di destinazione. Si tratta di valori noti.
* Larghezza assoluta delle colonne della griglia per ogni larghezza di pagina. Questi valori vengono determinati.
* Larghezza relativa di ciascuna colonna come percentuale della larghezza totale della pagina. Potete calcolare questi valori.

Il CSS include una serie di media query che utilizzano la struttura seguente:

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

Utilizzate il seguente algoritmo come punto di partenza per lo sviluppo delle classi di elementi e degli stili CSS per le pagine.

1. Definire un nome di classe per l&#39;elemento div che contiene tutte le righe, ad esempio `content.`
1. Definire una classe CSS per gli elementi div che rappresentano le righe, ad esempio `row-fluid`.
1. Definire i nomi delle classi per gli elementi dei blocchi di contenuto. Una classe è necessaria per tutte le larghezze possibili, in termini di estensione di colonna. Ad esempio, utilizzare la classe `span3` per gli elementi `div` che si estendono su 3 colonne, utilizzare le classi `span4` per un&#39;estensione di 4 colonne. Definite tutte le classi quante colonne della griglia.

1. Per ogni dimensione di visualizzazione di destinazione, aggiungete la query multimediale corrispondente al file CSS. Aggiungete i seguenti elementi in ogni media query:

   * Un selettore per la classe `content`, ad esempio `.content{}`.
   * Selettori per ciascuna classe span, ad esempio `.span3{ }`.
   * Un selettore per la classe `row-fluid`, ad esempio `.row-fluid{ }`
   * Selettori per le classi span che si trovano all&#39;interno di classi fluide di righe, ad esempio `.row-fluid span3 { }`.

1. Aggiungete stili di larghezza per ciascun selettore:

   1. Impostare la larghezza dei selettori `content` sulla dimensione assoluta della pagina, ad esempio `width:480px`.
   1. Impostare la larghezza di tutti i selettori fluidi riga su 100%.
   1. Impostare la larghezza di tutti i selettori di estensione sulla larghezza assoluta del blocco di contenuto. Una griglia banale utilizza colonne distribuite in modo uniforme con la stessa larghezza: `(absolute width of page)/(number of columns)`.
   1. Impostare la larghezza dei selettori `.row-fluid .span` come percentuale della larghezza totale. Calcolare questa larghezza utilizzando la formula `(absolute span width)/(absolute page width)*100`.

#### Posizionamento dei blocchi di contenuto nelle righe {#positioning-content-blocks-in-rows}

Utilizzare lo stile mobile della classe `.row-fluid` per controllare se i blocchi di contenuto di una riga sono disposti in orizzontale o verticale.

* Lo stile `float:left` o `float:right` causa la distribuzione orizzontale degli elementi secondari (blocchi di contenuto).

* Lo stile `float:none` causa la distribuzione verticale degli elementi secondari.

Aggiungete lo stile al selettore `.row-fluid` all&#39;interno di ogni media query. Impostate il valore in base al layout di pagina utilizzato per la media query. Ad esempio, nel diagramma seguente è illustrata una riga che distribuisce il contenuto in orizzontale per le finestre grandi e in verticale per le finestre strette.

![](do-not-localize/chlimage_1-3a.png)

Il seguente CSS può implementare questo comportamento:

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Assegnazione di classi ai blocchi di contenuto {#assigning-classes-to-content-blocks}

Per il layout di pagina di ciascuna dimensione di visualizzazione di destinazione, stabilite il numero di colonne su cui si estende ciascun blocco di contenuto. Quindi, stabilite la classe da utilizzare per gli elementi div di tali blocchi di contenuto.

Una volta stabilite le classi div, è possibile implementare la griglia utilizzando l&#39;applicazione AEM.
