---
title: Progettazione reattiva per le pagine web
seo-title: Responsive design for web pages
description: Con il design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi con più orientamenti
seo-description: With responsive design, the same pages can be effectively displayed on multiple devices in multiple orientations
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5317'
ht-degree: 1%

---

# Progettazione reattiva per le pagine web{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio _Reagire_). [Per saperne di più](/help/sites-developing/spa-overview.md).

Progetta le pagine web in modo che si adattino al riquadro di visualizzazione client in cui sono visualizzate. Con il design reattivo, le stesse pagine possono essere visualizzate in modo efficace su più dispositivi in entrambi gli orientamenti. L&#39;immagine seguente illustra alcuni modi in cui una pagina può rispondere ai cambiamenti nelle dimensioni del riquadro di visualizzazione:

* Layout: Utilizza layout a colonne singola per riquadri di visualizzazione più piccoli e layout a più colonne per riquadri di visualizzazione più grandi.
* Dimensioni testo: Utilizzare dimensioni di testo più grandi (se appropriato, ad esempio titoli) nei riquadri di visualizzazione più grandi.
* Contenuto: Includi solo il contenuto più importante quando viene visualizzato su dispositivi più piccoli.
* Navigazione: Sono disponibili strumenti specifici per il dispositivo per accedere ad altre pagine.
* Immagini: Distribuzione di rappresentazioni di immagini appropriate per il riquadro di visualizzazione client. in base alle dimensioni della finestra.

![chlimage_1-4](assets/chlimage_1-4a.png)

Sviluppa applicazioni Adobe Experience Manager (AEM) che generano pagine HTML5 adattabili a diverse dimensioni e orientamenti delle finestre. Ad esempio, i seguenti intervalli di larghezze di visualizzazione corrispondono a vari tipi di dispositivi e orientamenti

* Larghezza massima di 480 pixel (telefono, verticale)
* Larghezza massima di 767 pixel (telefono, orizzontale)
* Larghezza tra 768 pixel e 979 pixel (tablet, ritratto)
* Larghezza tra 980 pixel e 1199 pixel (tablet, orizzontale)
* Larghezza uguale o superiore a 1200 px (desktop)

Per informazioni sull’implementazione di un comportamento di progettazione reattiva, consulta i seguenti argomenti:

* [Query multimediali](/help/sites-developing/responsive.md#using-media-queries)
* [Griglie fluide](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Immagini adattive](/help/sites-developing/responsive.md#using-adaptive-images)

Durante la progettazione, utilizza **[!UICONTROL Barra laterale]** per visualizzare in anteprima le pagine per diverse dimensioni dello schermo.

## Prima di sviluppare {#before-you-develop}

Prima di sviluppare l’applicazione AEM che supporta le pagine web, è necessario prendere diverse decisioni di progettazione. Ad esempio, è necessario disporre delle seguenti informazioni:

* I dispositivi di destinazione.
* Dimensioni del riquadro di visualizzazione di destinazione.
* Layout di pagina per ciascuna dimensione del riquadro di visualizzazione di destinazione.

### Struttura dell&#39;applicazione {#application-structure}

La tipica struttura dell&#39;applicazione AEM supporta tutte le implementazioni di progettazione reattiva:

* I componenti della pagina si trovano sotto /apps/*nome_applicazione*/components
* I modelli si trovano sotto /apps/*nome_applicazione*/templates
* I progetti risiedono sotto /etc/designs

## Utilizzo di query multimediali {#using-media-queries}

Le query multimediali abilitano l’uso selettivo degli stili CSS per il rendering della pagina. Gli strumenti e le funzioni di sviluppo AEM consentono di implementare in modo efficace ed efficiente le query multimediali nelle applicazioni.

Il gruppo W3C fornisce [Query multimediali](https://www.w3.org/TR/css3-mediaqueries/) consiglio che descrive questa funzione CSS3 e la sintassi.

### Creazione del file CSS {#creating-the-css-file}

Nel file CSS, definisci le query multimediali in base alle proprietà dei dispositivi di destinazione. La seguente strategia di implementazione è efficace per gestire gli stili per ogni query multimediale:

* Utilizza una ClientLibraryFolder per definire il CSS che viene assemblato quando la pagina viene sottoposta a rendering.
* Definisci ogni query multimediale e gli stili associati in file CSS separati. È utile utilizzare nomi di file che rappresentano le caratteristiche del dispositivo della query multimediale.
* Definisci gli stili comuni a tutti i dispositivi in un file CSS separato.
* Nel file css.txt del ClientLibraryFolder, ordinare i file CSS dell&#39;elenco come richiesto nel file CSS assemblato.

L’esempio di file multimediali We.Retail utilizza questa strategia per definire gli stili nella progettazione del sito. Il file CSS utilizzato da We.Retail si trova in `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

Nella tabella seguente sono elencati i file presenti nella cartella figlio css.

<table>
 <tbody>
  <tr>
   <th>Nome file</th>
   <th>Descrizione</th>
   <th>Query multimediale</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Stili comuni.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Stili comuni, definiti da Twitter Bootstrap.</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Stili per tutti i contenuti multimediali con una larghezza o una larghezza di 1200 pixel.</td>
   <td><p>@media (larghezza minima: 1200 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Stili per contenuti multimediali di larghezza compresa tra 980 e 1199 pixel.</td>
   <td><p>@media (larghezza minima: 980 px) e (larghezza max: 1199px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Stili per contenuti multimediali di larghezza compresa tra 768 e 979 pixel. </td>
   <td><p>@media (larghezza minima: 768 px) e (larghezza max: 979px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Stili per tutti i file multimediali con larghezza inferiore a 768 pixel.</td>
   <td><p>@media (larghezza massima: 767 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Stili per tutti i file multimediali con larghezza inferiore a 481 pixel.</td>
   <td>@media (larghezza massima: 480) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

Il file css.txt nel `/etc/designs/weretail/clientlibs` elenca i file CSS inclusi nella cartella della libreria client. L&#39;ordine dei file implementa la precedenza di stile. Gli stili sono più specifici quando le dimensioni del dispositivo diminuiscono.

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

**Suggerimento**: I nomi descrittivi dei file consentono di identificare facilmente la dimensione del riquadro di visualizzazione di destinazione.

### Utilizzo di query multimediali con pagine AEM {#using-media-queries-with-aem-pages}

Includi la cartella della libreria client nello script JSP del componente pagina per generare il file CSS che include le query multimediali e per fare riferimento al file.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>La `apps.weretail.all` la cartella libreria client incorpora la libreria clientlibs.

Lo script JSP genera il seguente codice HTML che fa riferimento ai fogli di stile:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Anteprima per dispositivi specifici {#previewing-for-specific-devices}

Per verificare il comportamento del design reattivo, consulta le anteprime delle pagine in diverse dimensioni del riquadro di visualizzazione. In **[!UICONTROL Anteprima]** modalità, **[!UICONTROL Barra laterale]** include **[!UICONTROL Dispositivi]** menu a discesa utilizzato per selezionare un dispositivo. Quando si seleziona un dispositivo, la pagina cambia per adattarsi alle dimensioni del riquadro di visualizzazione.

![chlimage_1-5](assets/chlimage_1-5a.png)

Per abilitare l’anteprima del dispositivo in **[!UICONTROL Barra laterale]**, devi configurare la pagina e la **[!UICONTROL MobileEmulatorProvider]** servizio. Un&#39;altra configurazione di pagina controlla l&#39;elenco dei dispositivi che appare nella **[!UICONTROL Dispositivi]** elenco.

### Aggiunta dell’elenco dei dispositivi {#adding-the-devices-list}

La **[!UICONTROL Dispositivi]** elenco visualizzato in **[!UICONTROL Barra laterale]** quando la pagina include lo script JSP che esegue il rendering del **[!UICONTROL Dispositivi]** elenco. Per aggiungere la **[!UICONTROL Dispositivi]** elenco a **[!UICONTROL Barra laterale]**, include `/libs/wcm/mobile/components/simulator/simulator.jsp` nel `head` della pagina.

Include il seguente codice nel JSP che definisce il `head` sezione:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Per visualizzare un esempio, apri la `/apps/weretail/components/page/head.jsp` in CRXDE Lite.

### Registrazione dei componenti della pagina per la simulazione {#registering-page-components-for-simulation}

Per abilitare il simulatore dispositivo per supportare le pagine, registra i componenti pagina con il servizio di fabbrica MobileEmulatorProvider e definisci il `mobile.resourceTypes` proprietà.

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete.

Ad esempio, per creare un ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` nodo nell&#39;applicazione:

* Cartella padre: `/apps/application_name/config`
* Nome: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   - `*alias*` suffisso necessario perché il servizio MobileEmulatorProvider è un servizio di fabbrica. Utilizzare qualsiasi alias univoco per questa fabbrica.

* jcr:primaryType: `sling:OsgiConfig`

Aggiungi la seguente proprietà del nodo:

* Nome: `mobile.resourceTypes`
* Tipo: `String[]`
* Valore: I percorsi dei componenti della pagina che eseguono il rendering delle pagine web. Ad esempio, l’app geometrixx-media utilizza i seguenti valori:

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### Specifica dei gruppi di dispositivi {#specifying-the-device-groups}

Per specificare i gruppi di dispositivi visualizzati nell’elenco Dispositivi , aggiungi un `cq:deviceGroups` della proprietà `jcr:content` nodo della pagina principale del sito. Il valore della proprietà è una matrice di percorsi ai nodi del gruppo di dispositivi.

I nodi del gruppo di dispositivi si trovano nella `/etc/mobile/groups` cartella.

Ad esempio, la pagina principale del sito Geometrixx Media è `/content/geometrixx-media`. La `/content/geometrixx-media/jcr:content` node include la seguente proprietà:

* Nome: `cq:deviceGroups`
* Tipo: `String[]`
* Valore: `/etc/mobile/groups/responsive`

Utilizzare la console Strumenti per [creare e modificare gruppi di dispositivi](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>Per i gruppi di dispositivi utilizzati per la progettazione reattiva, modificare il gruppo di dispositivi e nella scheda Generale selezionare Disabilita emulatore. Questa opzione impedisce la visualizzazione del carosello dell’emulatore, che non è pertinente alla progettazione reattiva.

## Utilizzo di immagini adattive {#using-adaptive-images}

È possibile utilizzare query multimediali per selezionare una risorsa immagine da visualizzare nella pagina. Tuttavia, ogni risorsa che utilizza una query multimediale per condizionale del suo utilizzo viene scaricata sul client. La query multimediale determina semplicemente se la risorsa scaricata viene visualizzata.

Per risorse di grandi dimensioni, come le immagini, scaricare tutte le risorse non è un uso efficiente della pipeline dei dati del client. Per scaricare in modo selettivo le risorse, utilizza javascript per avviare la richiesta di risorsa dopo che le query multimediali hanno eseguito la selezione.

La strategia seguente carica una singola risorsa selezionata utilizzando le query multimediali:

1. Aggiungi un elemento DIV per ogni versione della risorsa. Includi l’URI della risorsa come valore di un valore di attributo. Il browser non interpreta l’attributo come risorsa.
1. Aggiungi una query multimediale a ogni elemento DIV appropriato per la risorsa.
1. Quando il documento viene caricato o la finestra viene ridimensionata, il codice javascript verifica la query multimediale di ciascun elemento DIV.
1. In base ai risultati delle query, determina quale risorsa includere.
1. Inserisci un elemento HTML nel DOM che fa riferimento alla risorsa.

### Valutazione delle query multimediali utilizzando Javascript {#evaluating-media-queries-using-javascript}

Attuazioni della [Interfaccia MediaQueryList](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface) che il W3C definisce consente di valutare le query multimediali utilizzando javascript. È possibile applicare la logica ai risultati della query multimediale ed eseguire gli script di destinazione per la finestra corrente:

* I browser che implementano l’interfaccia MediaQueryList supportano i `window.matchMedia()` funzione . Questa funzione esegue il test delle query multimediali rispetto a una stringa specificata. La funzione restituisce un `MediaQueryList` oggetto che consente di accedere ai risultati della query.

* Per i browser che non implementano l’interfaccia, puoi utilizzare un `matchMedia()` il polyfill, come [matchMedia.js](https://github.com/paulirish/matchMedia.js), una libreria javascript disponibile liberamente.

#### Selezione di risorse specifiche per i file multimediali {#selecting-media-specific-resources}

Il W3C proposto [elemento dell&#39;immagine](https://picture.responsiveimages.org/) utilizza le query multimediali per determinare l&#39;origine da utilizzare per gli elementi immagine. L’elemento immagine utilizza gli attributi degli elementi per associare le query multimediali con i percorsi immagine.

Libero accesso [libreria picturefill.js](https://github.com/scottjehl/picturefill) fornisce funzionalità simili a quelle proposte `picture` e utilizza una strategia simile. Chiamate alla libreria picturefill.js `window.matchMedia` per valutare le query multimediali definite per un set di `div` elementi. Ogni `div` specifica anche un&#39;origine immagine. L&#39;origine viene utilizzata quando la query multimediale del `div` restituisce un elemento `true`.

La `picturefill.js` La libreria richiede un codice HTML simile al seguente esempio:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

Durante il rendering della pagina, picturefull.js inserisce un `img` come ultimo elemento secondario di `<div data-picture>` elemento:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

In una pagina AEM, il valore della `data-src` attribute è il percorso di una risorsa nell’archivio.

### Implementazione di immagini adattive in AEM {#implementing-adaptive-images-in-aem}

Per implementare immagini adattive nell’applicazione AEM, è necessario aggiungere le librerie javascript richieste e includere nelle pagine il markup HTML richiesto.

**Librerie**

Ottieni le seguenti librerie javascript e includile in una cartella della libreria client:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (per i browser che non implementano l’interfaccia MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (disponibile tramite `/etc/clientlibs/granite/jquery` cartella libreria client (category = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (un evento jquery che si verifica una volta dopo il ridimensionamento della finestra)

**Suggerimento:** Puoi concatenare automaticamente più cartelle della libreria client in base a [incorporazione](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Crea un componente che genera gli elementi div richiesti dal codice picturefill.js. In una pagina AEM, il valore dell’attributo data-src è il percorso di una risorsa nell’archivio. Ad esempio, un componente pagina può codificare le query multimediali e i percorsi associati per le rappresentazioni di immagini in DAM. Oppure, crea un componente Immagine personalizzato che consente agli autori di selezionare rappresentazioni di immagini o specificare opzioni di rendering in fase di esecuzione.

Nell’esempio seguente HTML seleziona da 2 rappresentazioni DAM della stessa immagine.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>Il componente Immagine adattiva foundation implementa immagini adattive:
>
>* Cartella libreria client: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Script che genera HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>La sezione successiva fornisce dettagli su questo componente.

### Informazioni sul rendering delle immagini in AEM {#understanding-image-rendering-in-aem}

Per personalizzare il rendering delle immagini, è necessario comprendere l’implementazione predefinita AEM rendering delle immagini statiche. AEM fornisce il componente Immagine e un servlet di rendering delle immagini che lavorano insieme per il rendering delle immagini per la pagina web. La seguente sequenza di eventi si verifica quando il componente Immagine viene incluso nel sistema paragrafo della pagina:

1. Authoring: Gli autori possono modificare il componente Immagine per specificare il file immagine da includere in una pagina di HTML. Il percorso del file viene memorizzato come valore di proprietà del nodo del componente Immagine.
1. Richiesta pagina: Il JSP del componente pagina genera il codice HTML. Il JSP del componente Immagine genera e aggiunge un elemento img alla pagina.
1. Richiesta immagine: Il browser web carica la pagina e richiede l’immagine in base all’attributo src dell’elemento img.
1. Rendering immagine: Il servlet di rendering delle immagini restituisce l’immagine al browser web.

![chlimage_1-6](assets/chlimage_1-6a.png)

Ad esempio, il JSP del componente Immagine genera il seguente elemento HTML:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

Quando il browser carica la pagina, richiede l’immagine utilizzando il valore dell’attributo src come URL. Sling decompone l&#39;URL:

* Risorsa: `/content/mywebsite/en/_jcr_content/par/image_0`
* Estensione del nome file: `.jpg`
* Selettore: `img`
* Suffisso: `1358372073597.jpg`

La `image_0` il nodo ha `jcr:resourceType` valore `foundation/components/image`che ha `sling:resourceSuperType` valore `foundation/components/parbase`. Il componente parbase include lo script img.GET.java che corrisponde al selettore e all’estensione del nome file dell’URL della richiesta. CQ utilizza questo script (servlet) per eseguire il rendering dell’immagine.

Per visualizzare il codice sorgente dello script, utilizzare CRXDE Lite per aprire `/libs/foundation/components/parbase/img.GET.java`
file.

## Ridimensionamento delle immagini per la dimensione del riquadro di visualizzazione corrente {#scaling-images-for-the-current-viewport-size}

Scala le immagini in fase di runtime in base alle caratteristiche del riquadro di visualizzazione client per fornire immagini conformi ai principi di design reattivo. Utilizza lo stesso pattern di progettazione del rendering di immagini statiche utilizzando un servlet e un componente di authoring.

Il componente deve eseguire le seguenti attività:

* Memorizza il percorso e le dimensioni desiderate della risorsa immagine come valori di proprietà.
* Genera `div` elementi che contengono selettori di contenuti multimediali e chiamate di servizio per il rendering dell&#39;immagine.

>[!NOTE]
>
>Il client web utilizza le librerie javascript matchMedia e Picturefill (o librerie simili) per valutare i selettori multimediali.

Il servlet che elabora la richiesta di immagine deve eseguire le seguenti attività:

* Recupera il percorso e le dimensioni dell’immagine dalle proprietà del componente.
* Ridimensiona l’immagine in base alle proprietà e restituisce l’immagine.

**Soluzioni disponibili**

AEM installa le seguenti implementazioni che puoi utilizzare o estendere.

* Componente di base Immagine adattiva che genera query multimediali e richieste HTTP al Servlet del componente Immagine adattiva che ridimensiona le immagini.
* Il pacchetto Geometrixx Commons installa i servlet di esempio Image Reference Modification Servlet che alterano la risoluzione delle immagini.

### Informazioni sul componente Immagine adattiva {#understanding-the-adaptive-image-component}

Il componente Immagine adattiva genera chiamate al servlet del componente Immagine adattiva per eseguire il rendering di un’immagine che viene ridimensionata in base alla schermata del dispositivo. Il componente include le risorse seguenti:

* JSP: Aggiunge elementi div che associano le query multimediali alle chiamate al servlet del componente immagine adattivo.
* Librerie client: La cartella clientlibs è una `cq:ClientLibraryFolder` che assembla la libreria javascript matchMedia polyfill e una libreria javascript Picturefill modificata.
* Finestra di dialogo Modifica: La `cq:editConfig` Il nodo sostituisce il componente immagine di base CQ in modo che il target di rilascio crei un componente immagine adattiva anziché un componente immagine di base.

#### Aggiunta di elementi DIV {#adding-the-div-elements}

Lo script adaptive-image.jsp include il seguente codice che genera elementi div e query multimediali:

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

La `path` contiene il percorso della risorsa corrente (il nodo del componente immagine adattiva). Il codice genera una serie di `div` elementi con la seguente struttura:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

Il valore del `data-scr` attributo è un URL che Sling risolve nel Servlet del componente immagine adattivo che esegue il rendering dell&#39;immagine. L&#39;attributo data-media contiene la query multimediale valutata in base alle proprietà del client.

Il seguente codice HTML è un esempio di `div` elementi generati da JSP:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Modifica dei selettori delle dimensioni dell’immagine {#changing-the-image-size-selectors}

Se personalizzi il componente Immagine adattiva e modifichi i selettori di larghezza, devi anche configurare il servlet del componente Immagine adattiva per supportare le larghezze.

### Informazioni sul servlet del componente immagine adattivo {#understanding-the-adaptive-image-component-servlet}

Il servlet del componente immagine adattivo ridimensiona un’immagine JPEG in base a una larghezza specificata e imposta la qualità JPEG.

#### Interfaccia del servlet del componente immagine adattivo {#the-interface-of-the-adaptive-image-component-servlet}

Il Servlet del componente immagine adattivo è associato al servlet Sling predefinito e supporta le estensioni di file .jpg, .jpeg, .gif e .png. Il selettore del servlet è img.

>[!CAUTION]
>
>I file .gif animati non sono supportati in AEM per le rappresentazioni adattive.

Pertanto, Sling risolve in questo servlet gli URL di richiesta HTTP del seguente formato:

`*path-to-node*.img.*extension*`

Ad esempio, Sling inoltra le richieste HTTP con l’URL `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` al servlet del componente immagine adattivo.

Due selettori aggiuntivi specificano la larghezza dell’immagine richiesta e la qualità di JPEG. L’esempio seguente richiede un’immagine di larghezza di 480 pixel e di qualità media:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Proprietà immagine supportate**

Il servlet accetta un numero finito di larghezze e qualità delle immagini. Le seguenti larghezze sono supportate per impostazione predefinita (in pixel):

* completo
* 320
* 480
* 476
* 620

Il valore completo non indica alcuna scala.

Sono supportati i seguenti valori per la qualità di JPEG:

* BASSO
* MEDIO
* ALTO

I valori numerici sono rispettivamente 0,4, 0,82 e 1,0.

**Modifica delle larghezze supportate predefinite**

Utilizzare la console Web ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) o un nodo sling:OsgiConfig per configurare le larghezze supportate del servlet del componente immagine adattiva di Adobe CQ.

Per informazioni su come configurare i servizi AEM, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Console web</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Nome del servizio o del nodo</th>
   <td>Il nome del servizio nella scheda Configurazione è Servlet del componente immagine adattiva di Adobe CQ</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>Proprietà</th>
   <td><p>Larghezze supportate</p>
    <ul>
     <li>Per aggiungere una larghezza supportata, fare clic su un pulsante + e immettere un numero intero positivo.</li>
     <li>Per rimuovere una larghezza supportata, fai clic sul pulsante associato - .</li>
     <li>Per modificare una larghezza supportata, modifica il valore del campo.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>La proprietà è un valore String multivalore.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Dettagli di implementazione {#implementation-details}

La `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` la classe estende [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe. Il codice sorgente AdaptiveImageComponentServlet si trova nella `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` cartella.

La classe utilizza le annotazioni Felix SCR per configurare il tipo di risorsa e l’estensione di file a cui è associato il servlet e il nome del primo selettore.

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

Il servlet utilizza l’annotazione SCR di proprietà per impostare la qualità e le dimensioni dell’immagine supportate predefinite.

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

La `AbstractImageServlet` la classe fornisce `doGet` che elabora la richiesta HTTP. Questo metodo determina la risorsa associata alla richiesta, recupera le proprietà della risorsa dall’archivio e le restituisce in un [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) oggetto.

>[!NOTE]
>
>La [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) la classe fornisce `getFileReference method`, che recupera il valore della risorsa `fileReference` proprietà.

La `AdaptiveImageComponentServlet` sostituisce la classe `createLayer` metodo . Il metodo ottiene il percorso della risorsa immagine e la larghezza dell&#39;immagine richiesta dalla `ImageContext` oggetto. Chiama quindi i metodi del `info.geometrixx.commons.impl.AdaptiveImageHelper` , che esegue il ridimensionamento effettivo dell&#39;immagine.

Anche la classe AdaptiveImageComponentServlet sostituisce il metodo writeLayer. Questo metodo applica la qualità JPEG all&#39;immagine.

### Servlet di modifica del riferimento immagine (Geometrixx Common) {#image-reference-modification-servlet-geometrixx-common}

Il servlet di modifica Riferimento immagine di esempio genera attributi di dimensione per l’elemento img per ridimensionare un’immagine sulla pagina web.

#### Chiamata del servlet {#calling-the-servlet}

Il servlet è associato a `cq:page` e supporta l’estensione del file .jpg. Il selettore del servlet è `image`. Pertanto, Sling risolve in questo servlet gli URL di richiesta HTTP del seguente formato:

`path-to-page-node.image.jpg`

Ad esempio, Sling inoltra le richieste HTTP con l’URL `http://localhost:4502/content/geometrixx/en.image.jpg` al servlet di modifica dei riferimenti alle immagini.

Tre selettori aggiuntivi specificano la larghezza, l’altezza e la qualità dell’immagine richieste (facoltativamente). L’esempio seguente richiede un’immagine di larghezza 770 pixel, altezza 360 pixel e di qualità media.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Proprietà immagine supportate**

Il servlet accetta un numero finito di dimensioni immagine e valori di qualità.

I seguenti valori sono supportati per impostazione predefinita (larghezza/altezza):

* 256 x 192
* 370 x 150
* 480 x 200
* 127x127
* 770 x 360
* 620 x 290
* 480 x 225
* 320 x 150
* 375x175
* 303x142
* 1170 x 400
* 940 x 340
* 770 x 300
* 480 x 190

Sono supportati i seguenti valori per la qualità delle immagini:

* Bassa
* Media
* Alta

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete.

#### Specifica della risorsa immagine {#specifying-the-image-resource}

Il percorso dell&#39;immagine, le dimensioni e i valori di qualità devono essere memorizzati come proprietà di un nodo nell&#39;archivio:

* Il nome del nodo è `image`.
* Il nodo principale è il `jcr:content` nodo di un `cq:page` risorsa.

* Il percorso immagine viene memorizzato come valore di una proprietà denominata `fileReference`.

Durante la creazione di una pagina, utilizza **Barra laterale** per specificare l’immagine e aggiungere il `image` alle proprietà della pagina:

1. In **Barra laterale**, fai clic su **Pagina** , quindi fai clic su **Proprietà pagina**.
1. Fai clic sul pulsante **Immagine** e specifica l’immagine.
1. Fai clic su **OK**.

#### Dettagli di implementazione {#implementation-details-1}

La classe info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet estende [AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) classe. Se hai installato il pacchetto cq-geometrixx-commons-pkg, il codice sorgente ImageReferenceModificationServlet si trova in `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` cartella.

La classe utilizza le annotazioni Felix SCR per configurare il tipo di risorsa e l’estensione di file a cui è associato il servlet e il nome del primo selettore.

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

Il servlet utilizza l’annotazione SCR di proprietà per impostare la qualità e le dimensioni dell’immagine supportate predefinite.

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

La `AbstractImageServlet` la classe fornisce `doGet` che elabora la richiesta HTTP. Questo metodo determina la risorsa associata alla chiamata , recupera le proprietà della risorsa dall’archivio e le salva in un [ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) oggetto.

La `ImageReferenceModificationServlet` sostituisce la classe `createLayer` e implementa la logica che determina la risorsa immagine da riprodurre. Il metodo recupera un nodo figlio della pagina `jcr:content` nodo denominato `image`. Un [Immagine](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html) oggetto creato da questo `image` e `getFileReference` restituisce il percorso del file di immagine dal `fileReference` del nodo immagine.

>[!NOTE]
>La [com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html) La classe fornisce il metodo getFileReference.

## Sviluppo di una griglia fluida {#developing-a-fluid-grid}

AEM consente di implementare in modo efficiente ed efficace le griglie fluide. Questa pagina spiega come integrare la griglia fluida o un’implementazione della griglia esistente (ad esempio [Bootstrap](https://twitter.github.com/bootstrap/)) nell&#39;applicazione AEM.

Se non hai familiarità con le griglie fluide, consulta la [Introduzione alle griglie fluide](/help/sites-developing/responsive.md#developing-a-fluid-grid) in fondo a questa pagina. Questa introduzione fornisce una panoramica delle griglie fluide e indicazioni per la loro progettazione.

### Definizione della griglia utilizzando un componente Pagina {#defining-the-grid-using-a-page-component}

Utilizza i componenti pagina per generare gli elementi HTML che definiscono i blocchi di contenuto della pagina. La classe ClientLibraryFolder a cui fa riferimento la pagina fornisce il CSS che controlla il layout dei blocchi di contenuto:

* Componente pagina: Aggiunge elementi div che rappresentano righe di blocchi di contenuto. Gli elementi div che rappresentano i blocchi di contenuto includono un componente parsys in cui gli autori aggiungono contenuto.
* Cartella libreria client: Fornisce il file CSS che include query multimediali e stili per gli elementi div.

Ad esempio, l&#39;applicazione geometrixx-media di esempio contiene il componente media-home. Questo componente pagina inserisce due script, che generano due `div` elementi di classe `row-fluid`:

* La prima riga contiene un `div` elemento della classe `span12` (il contenuto si estende su 12 colonne). La `div` l&#39;elemento contiene il componente parsys.

* La seconda riga contiene due `div` elementi, uno di classe `span8` e l&#39;altro di classe `span4`. Ogni `div` include il componente parsys.

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
>Quando un componente include più `cq:include` elementi che fanno riferimento al componente parsys, ciascuno `path` l&#39;attributo deve avere un valore diverso.

#### Ridimensionamento della griglia dei componenti Pagina {#scaling-the-page-component-grid}

Progettazione associata al componente pagina geometrixx-media (`/etc/designs/geometrixx-media`) contiene `clientlibs` ClientLibraryFolder. Questa ClientLibraryFolder definisce gli stili CSS per `row-fluid` classi, `span*` classi e `span*` classi di cui sono figli `row-fluid` classi. Le query multimediali consentono di ridefinire gli stili per diverse dimensioni di visualizzazione.

Il seguente esempio CSS è un sottoinsieme di tali stili. Questo sottoinsieme si concentra su `span12`, `span8`e `span4` classi e query multimediali per due dimensioni di visualizzazione. Osserva le seguenti caratteristiche del CSS:

* La `.span` gli stili definiscono le larghezze degli elementi utilizzando numeri assoluti.
* La `.row-fluid .span*` gli stili definiscono le larghezze degli elementi come percentuali del padre. Le percentuali sono calcolate in base alle larghezze assolute.
* Le query multimediali per riquadri di visualizzazione più grandi assegnano larghezze assolute più grandi.

>[!NOTE]
>
>L’esempio di Geometrixx Media integra il [Bootstrap](https://twitter.github.com/bootstrap/javascript.html) framework javascript nella sua implementazione a griglia fluida. Il framework Bootstrap fornisce il file bootstrap.css .

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

#### Riposizionamento del contenuto nella griglia del componente Pagina {#repositioning-content-in-the-page-component-grid}

Le pagine dell’applicazione Geometrixx Media di esempio distribuiscono le righe dei blocchi di contenuto orizzontalmente in riquadri di visualizzazione ampi. Nei riquadri di visualizzazione più piccoli, gli stessi blocchi sono distribuiti verticalmente. L’esempio CSS seguente mostra gli stili che implementano questo comportamento per il codice HTML generato dal componente Media-home page:

* Il CSS predefinito per la pagina di benvenuto del contenuto multimediale assegna il `float:left` stile per `span*` classi interne `row-fluid` classi.

* Le query multimediali per riquadri di visualizzazione più piccoli assegnano `float:none` stile per le stesse classi.

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

Modularizza i componenti per utilizzare in modo efficiente il codice. È probabile che il sito utilizzi diversi tipi di pagine, ad esempio una pagina di benvenuto, una pagina di articolo o una pagina di prodotto. Ogni tipo di pagina contiene diversi tipi di contenuto e probabilmente utilizza layout diversi. Tuttavia, quando alcuni elementi di ciascun layout sono comuni su più pagine, puoi riutilizzare il codice che implementa tale parte del layout.

**Utilizzare le sovrapposizioni dei componenti pagina**

Creare un componente pagina principale che fornisce script per la generazione delle varie parti di una pagina, ad esempio `head` e `body` sezioni e `header`, `content`e `footer` sezioni all&#39;interno del corpo.

Crea altri componenti della pagina che utilizzano il componente pagina principale come `cq:resourceSuperType`. Questi componenti includono script che ignorano gli script della pagina principale in base alle esigenze.

Ad esempio, l’applicazione goemetrixx-media include il componente pagina (il `sling:resourceSuperType` è il componente pagina di base). Diversi componenti secondari (come articolo, categoria e media-home) utilizzano questo componente pagina come `sling:resourceSuperType`. Ogni componente figlio include un file content.jsp che si sovrappone al file content.jsp del componente pagina.

**Riutilizzare gli script**

Crea più script JSP che generano combinazioni di righe e colonne comuni per più componenti pagina. Ad esempio, il `content.jsp` lo script dell&#39;articolo e i componenti media-home fanno riferimento entrambi al `8x4col.jsp` script.

**Organizzare gli stili CSS in base alle dimensioni del riquadro di visualizzazione di destinazione**

Includere stili CSS e query multimediali per diverse dimensioni di riquadri di visualizzazione in file separati. Utilizza le cartelle della libreria client per concatenarle.

### Inserimento di componenti nella griglia della pagina {#inserting-components-into-the-page-grid}

Quando i componenti generano un singolo blocco di contenuto, in genere la griglia stabilita dal componente pagina controlla il posizionamento del contenuto.

Gli autori devono tenere presente che il blocco di contenuto può essere rappresentato in varie dimensioni e posizioni relative. Il testo di contenuto non deve utilizzare indicazioni relative per fare riferimento ad altri blocchi di contenuto.

Se necessario, il componente deve fornire tutte le librerie CSS o javascript necessarie per il codice HTML generato. Utilizza una cartella della libreria client all’interno del componente per generare i file CSS e JS. Per esporre i file, [creare una dipendenza o incorporare la libreria](/help/sites-developing/clientlibs.md#creating-client-library-folders) in un&#39;altra cartella della libreria client sotto la cartella /etc.

**Griglie secondarie**

Se il componente contiene più blocchi di contenuto, aggiungi i blocchi di contenuto all’interno di una riga per stabilire una griglia secondaria sulla pagina:

* Utilizza gli stessi nomi di classe del componente pagina contenitore per esprimere elementi div come righe e blocchi di contenuto.
* Per ignorare il comportamento che il CSS della progettazione di pagina implementa, utilizza un nome di seconda classe per l’elemento div della riga e fornisci il CSS associato in una cartella della libreria client.

Ad esempio, il `/apps/geometrixx-media/components/2-col-article-summary` Il componente genera due colonne di contenuto. Il HTML generato ha la seguente struttura:

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

La `.row-fluid .span6` i selettori del CSS della pagina si applicano al `div` elementi della stessa classe e struttura in questo HTML. Tuttavia, il componente include anche la cartella della libreria client /apps/geometrixx-media/components/2-col-article-summary/clientlibs :

* Il CSS utilizza le stesse query multimediali del componente pagina per stabilire le modifiche nel layout alle stesse larghezze di pagina discrete.
* I selettori utilizzano `multi-col-article-summary` classe della riga `div` per ignorare il comportamento della pagina `row-fluid` classe.

Ad esempio, i seguenti stili sono inclusi nel `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` file:

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

Le griglie fluide consentono ai layout di pagina di adattarsi alle dimensioni del riquadro di visualizzazione client. Le griglie sono costituite da colonne logiche e righe che posizionano i blocchi di contenuto nella pagina.

* Le colonne determinano le posizioni orizzontali e le larghezze dei blocchi di contenuto.
* Le righe determinano le posizioni verticali relative dei blocchi di contenuto.

Utilizzando la tecnologia HTML5 è possibile implementare la griglia e manipolarla per adattare i layout di pagina alle diverse dimensioni dei riquadri di visualizzazione:

* HTML `div` gli elementi contengono blocchi di contenuto che si estendono su un certo numero di colonne.
* Uno o più di questi elementi div comprendono una riga quando condividono un subelemento padre comune.

### Utilizzo di larghezze discrete {#using-discrete-widths}

Per ogni intervallo di larghezze di visualizzazione di destinazione, utilizza una larghezza di pagina statica e blocchi di contenuto di larghezza costante. Quando si ridimensiona manualmente una finestra del browser, le modifiche alle dimensioni del contenuto vengono apportate a larghezze di finestre discrete (note anche come punti di interruzione). Di conseguenza, le progettazioni delle pagine sono più fedeli, ottimizzando l’esperienza utente.

#### Ridimensionamento della griglia {#scaling-the-grid}

Utilizza le griglie per scalare i blocchi di contenuto per adattarli a diverse dimensioni di visualizzazione. I blocchi di contenuto si estendono su un numero specifico di colonne. Man mano che le larghezze delle colonne aumentano o diminuiscono per adattarsi a diverse dimensioni delle finestre, la larghezza dei blocchi di contenuto aumenta o diminuisce di conseguenza. La scalabilità supporta sia riquadri di grandi e medie dimensioni che sono sufficientemente ampi per adattarsi al posizionamento affiancato dei blocchi di contenuto.

![](do-not-localize/chlimage_1-1a.png)

#### Riposizionamento del contenuto nella griglia {#repositioning-content-in-the-grid}

La dimensione dei blocchi di contenuto può essere vincolata da una larghezza minima, oltre la quale la scala non è più efficace. Per i riquadri di visualizzazione più piccoli, la griglia può essere utilizzata per distribuire verticalmente blocchi di contenuto anziché orizzontalmente.

![](do-not-localize/chlimage_1-2a.png)

### Progettazione della griglia {#designing-the-grid}

Determina le colonne e le righe necessarie per posizionare i blocchi di contenuto sulle pagine. I layout di pagina determinano il numero di colonne e righe che si estendono sulla griglia.

**Numero di colonne**

Includi un numero sufficiente di colonne per posizionare in orizzontale i blocchi di contenuto in tutti i layout, per tutte le dimensioni dei riquadri di visualizzazione. È consigliabile utilizzare più colonne di quante siano attualmente necessarie per adattare le progettazioni di pagina future.

**Contenuto riga**

Utilizza le righe per controllare il posizionamento verticale dei blocchi di contenuto. Determina i blocchi di contenuto che condividono la stessa riga:

* I blocchi di contenuto posizionati uno accanto all’altro orizzontalmente in uno qualsiasi dei layout si trovano nella stessa riga.
* I blocchi di contenuto posizionati uno accanto all’altro orizzontalmente (riquadri di visualizzazione più ampi) e verticalmente (riquadri di visualizzazione più piccoli) si trovano nella stessa riga.

### Implementazioni a griglia {#grid-implementations}

Crea classi e stili CSS per controllare il layout dei blocchi di contenuto in una pagina. Le progettazioni di pagina sono spesso basate sulle dimensioni e la posizione relative dei blocchi di contenuto all’interno del riquadro di visualizzazione. La finestra di visualizzazione determina la dimensione effettiva dei blocchi di contenuto. Il CSS deve tenere conto delle dimensioni relative e assolute. Puoi implementare una griglia fluida utilizzando tre tipi di classi CSS:

* Una classe per un `div` che è un contenitore per tutte le righe. Questa classe imposta la larghezza assoluta della griglia.
* Una classe per `div` elementi che rappresentano una riga. Questa classe controlla il posizionamento orizzontale o verticale dei blocchi di contenuto in essa contenuti.
* Classi per `div` elementi che rappresentano blocchi di contenuto di diverse larghezze. Le larghezze sono espresse come percentuale della riga padre.

Larghezze di visualizzazione di destinazione (e relative query multimediali associate) delimitano larghezze discrete utilizzate per un layout di pagina.

#### Larghezza dei blocchi di contenuto {#widths-of-content-blocks}

In generale, il `width` lo stile delle classi di blocchi di contenuto si basa sulle seguenti caratteristiche della pagina e della griglia:

* Larghezza assoluta della pagina utilizzata per ogni dimensione di visualizzazione mirata. Si tratta di valori noti.
* Larghezza assoluta delle colonne della griglia per ogni larghezza di pagina. Questi valori vengono determinati.
* Larghezza relativa di ciascuna colonna come percentuale della larghezza totale della pagina. Questi valori vengono calcolati.

Il CSS include una serie di query multimediali che utilizzano la seguente struttura:

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

Utilizza il seguente algoritmo come punto di partenza per sviluppare le classi di elementi e gli stili CSS per le pagine.

1. Definire un nome di classe per l’elemento div che contiene tutte le righe, ad esempio `content.`
1. Definire una classe CSS per gli elementi div che rappresentano le righe, ad esempio `row-fluid`.
1. Definire i nomi delle classi per gli elementi dei blocchi di contenuto. È necessaria una classe per tutte le larghezze possibili, in termini di intervalli di colonne. Ad esempio, utilizza `span3` classe per `div` elementi che si estendono su 3 colonne, utilizza `span4` classi per intervalli di 4 colonne. Definisci tutte le classi quante sono le colonne presenti nella griglia.

1. Per ogni dimensione del riquadro di visualizzazione di destinazione, aggiungi la query multimediale corrispondente al file CSS. Aggiungi i seguenti elementi in ogni query multimediale:

   * Un selettore per il `content` Classe, ad esempio `.content{}`.
   * Selettori per ogni classe span, ad esempio `.span3{ }`.
   * Un selettore per il `row-fluid` Classe, ad esempio `.row-fluid{ }`
   * Selettori per le classi span che si trovano all’interno di classi di file fluidi, ad esempio `.row-fluid span3 { }`.

1. Aggiungi stili di larghezza per ciascun selettore:

   1. Imposta la larghezza di `content` seleziona in base alle dimensioni assolute della pagina, ad esempio `width:480px`.
   1. Imposta la larghezza di tutti i selettori a fluido di riga su 100%.
   1. Imposta la larghezza di tutti i selettori di estensione sulla larghezza assoluta del blocco di contenuto. Una griglia banale utilizza colonne distribuite in modo uniforme della stessa larghezza: `(absolute width of page)/(number of columns)`.
   1. Imposta la larghezza del `.row-fluid .span` selettori come percentuale della larghezza totale. Calcola questa larghezza utilizzando la variabile `(absolute span width)/(absolute page width)*100` formula.

#### Posizionamento di blocchi di contenuto nelle righe {#positioning-content-blocks-in-rows}

Utilizza lo stile mobile del `.row-fluid` per controllare se i blocchi di contenuto di una riga sono disposti orizzontalmente o verticalmente.

* La `float:left` o `float:right` lo stile causa la distribuzione orizzontale degli elementi secondari (blocchi di contenuto).

* La `float:none` lo stile causa la distribuzione verticale degli elementi figlio.

Aggiungi lo stile al `.row-fluid` selettore all’interno di ogni query multimediale. Imposta il valore in base al layout di pagina utilizzato per tale query multimediale. Ad esempio, il diagramma seguente illustra una riga che distribuisce il contenuto in orizzontale per riquadri di visualizzazione ampi e in verticale per riquadri di visualizzazione ristretti.

![](do-not-localize/chlimage_1-3a.png)

Il CSS seguente potrebbe implementare questo comportamento:

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

Per il layout di pagina di ogni dimensione del riquadro di visualizzazione di destinazione, determinare il numero di colonne su cui si estende ogni blocco di contenuto. Quindi, determina quale classe utilizzare per gli elementi div di tali blocchi di contenuto.

Una volta stabilite le classi div, è possibile implementare la griglia utilizzando l’applicazione AEM.
