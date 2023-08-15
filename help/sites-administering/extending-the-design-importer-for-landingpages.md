---
title: Estensione e configurazione di Importazione progettazione per le pagine di destinazione
description: Scopri come configurare l’Importazione progettazione per le pagine di destinazione.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b8c6075-13c6-4277-b726-8dea7991efec
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3501'
ht-degree: 0%

---

# Estensione e configurazione di Importazione progettazione per le pagine di destinazione{#extending-and-configuring-the-design-importer-for-landing-pages}

Questa sezione descrive come configurare e, se necessario, estendere l’importazione progettazione per le pagine di destinazione. Utilizzo delle pagine di destinazione dopo l’importazione è trattato in [Landing Pages.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Come fare in modo che l’importazione progettazione estragga il componente personalizzato**

Di seguito sono riportati i passaggi logici per fare in modo che Importazione progettazione riconosca il componente personalizzato

1. Creare un TagHandler

   * Un gestore di tag è un POJO che gestisce tag HTML di un tipo specifico. Il &quot;tipo&quot; di tag HTML che TagHandler può gestire è definito tramite la proprietà OSGi di TagHandlerFactory &quot;tagpattern.name&quot;. Questa proprietà OSGi è essenzialmente un regex che deve corrispondere al tag HTML di input che desideri gestire. Tutti i tag nidificati vengono inviati al gestore di tag per la gestione. Ad esempio, se ti registri per un div che contiene un &lt;p> , il tag &lt;p> Il tag verrà anche inviato al tuo TagHandler e spetta a te decidere come gestirlo.
   * L’interfaccia del gestore di tag è simile a quella del gestore di contenuti SAX. Riceve eventi SAX per ogni tag html. In qualità di provider di gestori di tag, devi implementare alcuni metodi del ciclo di vita che vengono automaticamente chiamati dal framework di importazione progettazione.

1. Creare il TagHandlerFactory corrispondente.

   * La factory del gestore di tag è un componente OSGi (singleton) responsabile della generazione di istanze del gestore di tag.
   * il factory del gestore di tag deve esporre una proprietà OSGi denominata &quot;tagpattern.name&quot; il cui valore corrisponde al tag html di input.
   * Se esistono più gestori di tag che corrispondono al tag HTML di input, viene scelto quello con una classificazione più elevata. La classificazione stessa viene esposta come proprietà OSGi **service.ranking**.
   * TagHandlerFactory è un componente OSGi. Tutti i riferimenti che desideri fornire al tuo TagHandler devono essere forniti tramite questa factory.

1. Se si desidera ignorare l&#39;impostazione predefinita, assicurarsi che TagHandlerFactory disponga di una classificazione migliore.

>[!CAUTION]
>
>Importazione progettazione, utilizzato per importare pagine di destinazione, [è stato dichiarato obsoleto con AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparazione di HTML per l&#39;importazione {#preparing-the-html-for-import}

Dopo aver creato una pagina di importazione, puoi importare la pagina di destinazione completa di HTML. Per importare la pagina di destinazione di HTML, devi prima comprimerne il contenuto in un pacchetto di progettazione. Il pacchetto progettazione contiene la pagina di destinazione di HTML e le risorse di riferimento (immagini, CSS, icone, script e così via).

La seguente scheda di riferimento rapido fornisce un esempio di come preparare il HTML per l’importazione:

Scheda di riferimento rapido della pagina di destinazione

[Ottieni file](assets/cheatsheet.zip)

### Layout e requisiti dei file ZIP {#zip-file-layout-and-requirements}

>[!NOTE]
>
>A questo punto, i file ZIP possono contenere solo una pagina HTML o una parte di una pagina.

Di seguito è riportato un esempio di layout dello zip:

* /index.html -> file HTML della pagina di destinazione
* /css -> da aggiungere alla libreria client CSS
* /img -> tutte le immagini e le risorse
* /js -> da aggiungere alla libreria client JS

Il layout si basa sul layout delle best practice per le boilerplate di HTML5. Ulteriori informazioni all&#39;indirizzo [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>Come minimo, il pacchetto di progettazione **deve** contiene un **index.html** a livello di radice. Se la pagina di destinazione da importare ha anche una versione per dispositivi mobili, il file ZIP deve contenere **mobile.index.html** insieme a **index.html** a livello principale.

### Preparazione di Landing Page HTML {#preparing-the-landing-page-html}

Per importare il HTML, devi aggiungere un div canvas al HTML della pagina di destinazione.

Il div canvas è un html **div** con `id="cqcanvas"` che deve essere inserito all’interno del HTML `<body>` e deve racchiudere il contenuto destinato alla conversione.

Di seguito è riportato un frammento di esempio di HTML della pagina di destinazione dopo l’aggiunta dell’area di lavoro:

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### Preparazione delle HTML per includere componenti AEM modificabili {#preparing-the-html-to-include-editable-aem-components}

Quando importi una pagina di destinazione, puoi scegliere di importarla così com’è, il che significa che dopo l’importazione della pagina di destinazione non puoi modificare nessuno degli elementi importati in AEM (puoi comunque aggiungere altri componenti AEM nella pagina).

Prima di importare la pagina di destinazione, potrebbe essere utile convertire alcune parti della pagina in modo che risultino componenti AEM modificabili. Questo consente di modificare rapidamente parti della pagina di destinazione anche dopo l’importazione della progettazione.

Per farlo, aggiungi il `data-cq-component` al componente appropriato nel file HTML importato.

La sezione seguente descrive come modificare il file HTML in modo da convertire alcune parti delle pagine di destinazione in diversi componenti AEM modificabili. I componenti sono descritti in dettaglio all’indirizzo [Componenti delle pagine di destinazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>Il markup HTML per convertire parti della pagina di destinazione in componenti AEM ha sia una forma lunga che una dichiarazione di tag abbreviata. Entrambi sono descritti per ogni componente.

### Limitazioni {#limitations}

Prima di importare, tieni presente le seguenti limitazioni:

### Qualsiasi attributo come classe o ID applicato al tag &amp;lt;body> non viene mantenuto {#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Ad esempio, se al tag body viene applicato un attributo come id o classe `<body id="container">` dopo l’importazione, non viene conservato. Pertanto, la progettazione in fase di importazione non deve avere alcuna dipendenza dagli attributi applicati al `<body>` tag.

### Trascina e rilascia zip {#drag-and-drop-zip}

Il caricamento tramite trascinamento della selezione zip non è supportato per Internet Explorer e Firefox versioni 3.6 e precedenti. Per caricare un progetto quando si utilizzano questi browser, fare clic sull&#39;area di rilascio dei file per aprire una finestra di dialogo di caricamento dei file e caricare il progetto utilizzando tale finestra di dialogo.

I browser che supportano il &quot;trascinamento&quot; dello zip di progettazione sono Chrome, Safari5.x, Firefox 4 e versioni successive.

### Modernizzatore non supportato {#modernizr-is-not-supported}

`Modernizr.js` è uno strumento basato su JavaScript che rileva le funzionalità native dei browser e rileva se sono adatte o meno agli elementi html5. Le progettazioni che utilizzano Modernizzatore per migliorare il supporto nelle versioni precedenti di browser diversi possono causare problemi di importazione nella soluzione della pagina di destinazione. `Modernizr.js` Gli script non sono supportati con Importazione progettazione.

### Le proprietà di pagina non vengono conservate al momento dell&#39;importazione del pacchetto di progettazione {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Qualsiasi proprietà di pagina (ad esempio, Dominio personalizzato, Applicazione di HTTPS e così via) impostata per una pagina (che utilizza il modello Pagina di destinazione vuota) prima dell’importazione del pacchetto di progettazione viene persa dopo l’importazione della progettazione. Pertanto, si consiglia di impostare le proprietà della pagina dopo l’importazione del pacchetto di progettazione.

### Presunto markup solo HTML {#html-only-markup-assumed}

Durante l’importazione, il markup viene bonificato per motivi di sicurezza e per evitare di importare e pubblicare markup non validi. Ciò presuppone che il markup solo HTML e tutti gli altri tipi di elementi, ad esempio SVG in linea o Componenti Web, vengano esclusi.

### Testo {#text}

Markup HTML per inserire un componente testo ( `foundation/components/text`) nel pacchetto di progettazione HTML:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Includendo il markup sopra riportato nel HTML, si verifica quanto segue:

* Crea un componente testo AEM modificabile ( `sling:resourceType=foundation/components/text`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Imposta il `text` del componente testo creato al HTML racchiuso all’interno del `div`.

**Dichiarazione tag componente breve**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Testo con un elenco**

Per aggiungere un testo con un elenco:

* 1st
* 2nd

che possono essere modificate nell’editor Rich Text:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Testo con colore**

Per aggiungere un testo con un colore (rosa) modificabile nell’editor Rich Text:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Titolo {#title}

Markup HTML per inserire un componente titolo ( `wcm/landingpage/components/title`) nel pacchetto di progettazione HTML:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Includendo il markup sopra riportato nel HTML, si verifica quanto segue:

* Crea un componente titolo AEM modificabile ( `sling:resourceType=wcm/landingpage/components/title`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Imposta il `jcr:title` del componente titolo creato al testo all’interno del tag titolo racchiuso in div.
* Imposta il `type` al tag titolo, in questo caso `h1`.

Il componente Titolo supporta sette tipi: `h1, h2, h3, h4, h5, h6` e `default`.

**Dichiarazione tag componente breve**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Immagine {#image}

Markup HTML per inserire un componente immagine (foundation/components/image) nel pacchetto progettazione di HTML:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

Includendo il markup sopra riportato nel HTML, si verifica quanto segue:

* Crea un componente immagine AEM modificabile ( `sling:resourceType=foundation/components/image`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Imposta il `fileReference` proprietà del componente immagine creato nel percorso in cui viene importata l’immagine specificata nell’attributo src.
* Imposta il `alt` al valore dell’attributo alt nel tag img.
* Imposta il `title` proprietà al valore dell’attributo title nel tag img.
* Imposta il `width` al valore dell’attributo width nel tag img.
* Imposta il `height` proprietà al valore dell&#39;attributo height nel tag img.

**Dichiarazione tag componente breve:**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### URL assoluto img src non supportato in Image Component Div {#absolute-url-img-src-not-supported-within-image-component-div}

Se un `<img>` viene tentato un tag con un url src assoluto per la conversione del componente, un **UnsupportedTagContentException** è sollevato. Ad esempio, quanto segue non è supportato:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

In caso contrario, sono supportate le immagini URL assolute per i tag immagine che non fanno parte dell’elemento div del componente Immagine.

### Componenti dell’invito all’azione {#call-to-action-components}

È possibile contrassegnare una parte della pagina di destinazione per l’importazione come &quot;componente di invito all’azione modificabile&quot;: tali componenti di invito all’azione importati possono essere modificati dopo l’importazione della pagina di destinazione. L’AEM include le seguenti componenti del CTA:

* Collegamento Click-through: consente di aggiungere un collegamento di testo che, se selezionato, porta il visitatore a un URL di destinazione.
* Collegamento grafico: consente di aggiungere un’immagine che, se selezionata, porta il visitatore a un URL di destinazione.

#### Collegamento Click-through {#click-through-link}

Questo componente CTA può essere utilizzato per aggiungere un collegamento di testo alla pagina di destinazione.

Proprietà supportate

* Etichetta con opzioni grassetto, corsivo e sottolineato
* URL di Target, supporta URL di terze parti e AEM
* Opzioni di rendering della pagina (stessa finestra, nuova finestra e così via)

Tag HTML per includere il componente click-through nel file zip importato. Qui href corrisponde all’URL di destinazione, &quot;Visualizza dettagli prodotto&quot; corrisponde all’etichetta e così via.

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

Questo componente può essere utilizzato in qualsiasi applicazione autonoma o può essere importato da zip.

**Dichiarazione tag componente breve**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Collegamento grafico {#graphical-link}

Questo componente CTA può essere utilizzato per aggiungere qualsiasi immagine grafica con collegamento nella pagina di destinazione. L&#39;immagine può essere un semplice pulsante o qualsiasi immagine grafica come sfondo. Quando si fa clic sull’immagine, l’utente viene indirizzato all’URL di destinazione specificato nelle proprietà del componente. Fa parte del gruppo &quot;Invito all&#39;azione&quot;.

Proprietà supportate

* Ritaglio immagine, rotazione
* Testo al passaggio del mouse, descrizione, dimensione in pixel
* URL di Target, supporta URL di terze parti e AEM
* Opzioni di rendering della pagina (stessa finestra, nuova finestra e così via)

Tag HTML per includere il componente collegamento grafico nello zip importato. Qui href corrisponde all’URL di destinazione, img src corrisponde all’immagine di rendering, &quot;title&quot; viene preso come testo al passaggio del mouse e così via.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Dichiarazione tag componente breve**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Per creare un collegamento grafico clickthrough, devi racchiudere un tag di ancoraggio e il tag immagine in un div con `data-cq-component="clickthroughgraphicallink"` attributo.
>
>Ad esempio `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Non sono supportati altri modi per associare un’immagine a un tag di ancoraggio utilizzando gli stili CSS. Ad esempio, il markup seguente non funziona:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>con un associato `css .hasbackground { background-image: pathtoimage }`
>

### Modulo lead {#lead-form}

Un modulo lead è un modulo utilizzato per raccogliere le informazioni sul profilo di un visitatore/lead. Queste informazioni possono essere memorizzate e utilizzate in un secondo momento per effettuare un marketing efficace basato sulle informazioni. Queste informazioni generalmente includono titolo, nome, e-mail, data di nascita, indirizzo, interesse e così via. Fa parte del gruppo &quot;Modulo lead CTA&quot;.

**Funzioni supportate**

* Campi lead predefiniti: nome, cognome, indirizzo, dominio, genere, informazioni, ID utente, ID e-mail, pulsante di invio sono disponibili nella barra laterale. È sufficiente trascinare il componente richiesto nel modulo del lead.
* Con l’aiuto di questi componenti, l’autore può progettare un modulo lead indipendente; questi campi corrispondono ai campi del modulo lead. In un’applicazione zip indipendente o importata, l’utente può aggiungere campi aggiuntivi utilizzando i campi del modulo cq:form o cta lead, il nome e progettarli in base ai requisiti.
* Mappa i campi del modulo lead utilizzando nomi predefiniti specifici del modulo lead CTA, ad esempio: firstName per nome nel modulo lead e così via.
* I campi non mappati ai componenti modulo lead vengono mappati su cq:form: testo, radio, casella di controllo, menu a discesa, nascosto, password.
* L’utente può fornire il titolo utilizzando il tag &quot;label&quot; e lo stile utilizzando l’attributo di stile &quot;class&quot; (disponibile solo per i componenti del modulo lead CTA).
* La pagina di ringraziamento e l’elenco delle iscrizioni possono essere forniti come parametro nascosto del modulo (presente nel file index.htm) oppure possono essere aggiunti/modificati dalla barra di modifica di &quot;Inizio del modulo lead&quot;

  &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot;/>

  &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot;/>

* I vincoli come - obbligatorio possono essere forniti dalla configurazione di modifica di ciascun componente.

Tag HTML per includere il componente collegamento grafico nello zip importato. Qui &quot;firstName&quot; è mappato al firstName del modulo lead e così via, tranne che per le caselle di controllo: queste due caselle di controllo sono mappate al componente a discesa cq:form.

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

Il componente parsys dell’AEM è un componente contenitore che può contenere altri componenti dell’AEM. È possibile aggiungere un componente parsys nel HTML importato. Questo consente all’utente di aggiungere/eliminare componenti AEM modificabili nella pagina di destinazione anche dopo l’importazione.

Il sistema paragrafo consente agli utenti di aggiungere componenti utilizzando la barra laterale.

Markup HTML per inserire un componente parsys ( `foundation/components/parsys`) nel pacchetto di progettazione HTML:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

L’inclusione del markup sopra riportato nel HTML comporta le seguenti operazioni:

* Inserisce un componente parsys AEM (foundation/components/parsys) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Inizializza la barra laterale con i componenti predefiniti. È possibile aggiungere nuovi componenti alla pagina di destinazione trascinandoli dalla barra laterale al componente parsys.
* Anche due componenti titolo fanno parte del parsys.

### Destinazione {#target}

Il componente Target mostra il contenuto di un’esperienza sulla pagina. È possibile creare più esperienze in una campagna e il componente Target può mostrare in modo dinamico il contenuto di esperienze diverse ai vari utenti che visitano la pagina.

Il markup html per inserire un componente target e creare anche esperienze diverse in una campagna:

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## Opzioni di importazione aggiuntive {#additional-importing-options}

Oltre a specificare se i componenti importati sono componenti AEM modificabili, è possibile configurare quanto segue prima di importare il pacchetto di progettazione:

* Impostazione delle proprietà di pagina mediante l&#39;estrazione dei metadati definiti nelle HTML importate.
* Specifica della codifica charset nel HTML.
* Sovrapposizione del modello della pagina di importazione.

### Impostazione delle proprietà di pagina mediante l&#39;estrazione dei metadati definiti nelle HTML importate {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

I seguenti metadati dichiarati nel capo del HTML importato sono estratti e conservati dall’importatore di progettazione come proprietà &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

L’attributo della lingua impostato nel tag HTML viene estratto e mantenuto dall’importazione di progetti come proprietà &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Specifica della codifica charset nel codice HTML {#specifying-the-charset-encoding-in-the-html}

L&#39;utilità di importazione della progettazione legge la codifica specificata nel HTML importato. La codifica può essere specificata come segue:

`<meta charset="UTF-8">`

*OPPURE*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Se nel HTML importato non è specificata alcuna codifica, la codifica predefinita impostata dall&#39;utilità di importazione progettazione è UTF-8.

### Sovrapposizione modello {#overlaying-template}

Il modello Pagina di destinazione vuota può essere sovrapposto creando un nuovo modello in: `/apps/<appName>/designimporter/templates/<templateName>`

Scopri come creare un nuovo modello in AEM [qui](/help/sites-developing/templates.md).

### Riferimento a un componente dalla pagina di destinazione {#referring-a-component-from-landing-page}

Supponiamo di avere un componente a cui desideri fare riferimento nel HTML utilizzando l’attributo data-cq-component in modo che l’importazione progettazione esegua il rendering di un componente che includi in questa posizione. Ad esempio, si desidera fare riferimento al componente tabella ( `resourceType = /libs/foundation/components/table`). È necessario aggiungere quanto segue in HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

Il percorso nel componente data-cq-component deve essere il resourceType del componente.

### Best practice {#best-practices}

L’utilizzo di selettori CSS simili a quelli seguenti non è consigliato con elementi contrassegnati per la conversione dei componenti durante l’importazione.

| E > F | un elemento F figlio di un elemento E | [Combinatore figlio](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | un elemento F immediatamente preceduto da un elemento E | [Combinatore di pari livello adiacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un elemento F preceduto da un elemento E | [Combinatore di pari livello generale](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:radice | un elemento E, radice del documento | [Pseudo-classi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:n-esimo figlio/i | un elemento E, l’n-esimo elemento figlio del relativo elemento padre | [Pseudo-classi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un elemento E, l’n-esimo figlio del padre, a partire dall’ultimo | [Pseudo-classi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un elemento E, l’n-esimo elemento di pari livello del suo tipo | [Pseudo-classi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un elemento E, l’n-esimo pari livello del suo tipo, a partire dall’ultimo | [Pseudo-classi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Questo perché elementi HTML aggiuntivi come &lt;div> vengono aggiunti al codice Html generato dopo l’importazione.

* Anche gli script che si basano su una struttura simile a quella descritta sopra non sono consigliati per l’uso con elementi contrassegnati per la conversione in componenti AEM.
* Utilizzo degli stili nei tag di markup per la conversione dei componenti, ad esempio &lt;div data-cq-component=&quot;&amp;ast;&quot;> non è consigliato.
* Il layout del progetto deve seguire le best practice di HTML5 Boilerplate. Ulteriori informazioni su: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configurazione dei moduli OSGI {#configuring-osgi-modules}

I componenti che espongono le proprietà configurabili tramite la console OSGI sono i seguenti:

* Importazione progettazione pagina di destinazione
* Landing Page Builder
* Generatore di pagine di destinazione mobile
* Preprocessore di ingresso pagina di destinazione

La tabella seguente descrive brevemente le proprietà:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Descrizione proprietà </strong></td>
  </tr>
  <tr>
   <td>Importazione progettazione pagina di destinazione</td>
   <td>Extract Filter</td>
   <td>L’elenco delle espressioni regolari da utilizzare per filtrare i file dall’estrazione. <br /> Le voci ZIP che corrispondono a uno dei pattern specificati sono escluse dall’estrazione</td>
  </tr>
  <tr>
   <td>Landing Page Builder</td>
   <td>Pattern file</td>
   <td>Il Generatore di pagine di destinazione può essere configurato per gestire i file HTML che corrispondono a un’espressione regolare definita dal modello di file.</td>
  </tr>
  <tr>
   <td>Generatore di pagine di destinazione mobile</td>
   <td>Pattern file</td>
   <td>Il Generatore di pagine di destinazione può essere configurato per gestire i file HTML che corrispondono a un’espressione regolare definita dal modello di file.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Gruppi dispositivo</td>
   <td>Elenco dei gruppi di dispositivi da supportare.</td>
  </tr>
  <tr>
   <td>Preprocessore di ingresso pagina di destinazione</td>
   <td>Pattern di ricerca </td>
   <td>Pattern da cercare, nei contenuti della voce archivio. Questa espressione regolare viene associata alla voce contenuto riga per riga. In caso di corrispondenza, il testo corrispondente viene sostituito con il pattern di sostituzione specificato.<br /> <br /> Consulta la nota seguente sulle limitazioni attuali del preprocessore di accesso alla pagina di destinazione.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Sostituisci pattern</td>
   <td>Pattern che sostituisce le corrispondenze trovate. Puoi utilizzare riferimenti a gruppi regex come $1, $2. Inoltre, questo modello supporta parole chiave come {designPath} che vengono risolti con il valore effettivo durante l’importazione.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limitazione corrente del preprocessore di accesso alla pagina di destinazione:**
>Se devi apportare delle modifiche al pattern di ricerca, quando apri l’editor delle proprietà felix, devi aggiungere manualmente i caratteri barra rovesciata per evitare i metacaratteri regex. Se non aggiungi manualmente i caratteri barra rovesciata, il regex non è considerato valido e non sostituirà quello precedente.
>
>Ad esempio, se la configurazione predefinita è
>
>>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>E devi sostituire `CQ_DESIGN_PATH` con `VIPURL` nel modello di ricerca, il modello di ricerca deve essere simile al seguente:
>
>`/\* *VIPURL *\*/ *(['"])`

## Risoluzione dei problemi {#troubleshooting}

Durante l&#39;importazione del pacchetto di progettazione, è possibile che si verifichino diversi errori, descritti in questa sezione.

### Inizializzazione della barra laterale con i componenti rilevanti per la pagina di destinazione {#initialization-of-sidekick-with-landing-page-relevant-components}

Se il pacchetto di progettazione contiene un markup di componente parsys, dopo l’importazione la barra laterale inizia a mostrare i componenti rilevanti per la pagina di destinazione. Puoi trascinare i nuovi componenti sul componente parsys all’interno della pagina di destinazione. Potete anche passare alla modalità progettazione e aggiungere nuovi componenti alla barra laterale.

### Messaggi di errore visualizzati durante l’importazione {#error-messages-displayed-during-import}

In caso di errori, ad esempio se il pacchetto importato non è un file ZIP valido, l&#39;importazione del progetto non importa il pacchetto. Nella parte superiore della pagina viene invece visualizzato un messaggio di errore sopra la casella di trascinamento. Di seguito sono riportati alcuni esempi di scenari di errore. Dopo aver corretto l’errore, puoi reimportare lo zip aggiornato nella stessa pagina di destinazione vuota. Di seguito sono riportati i diversi scenari in cui vengono generati errori:

* Il pacchetto di progettazione importato non è un archivio zip valido.
* Il pacchetto di progettazione importato non contiene un index.html al livello superiore.

### Avvisi visualizzati dopo l’importazione {#warnings-displayed-after-import}

Se sono presenti avvertenze (ad esempio, HTML fa riferimento a immagini che non esistono nel pacchetto), l’importazione di progetti importa lo zip ma allo stesso tempo visualizza un elenco di problemi/avvertenze nel riquadro dei risultati. Facendo clic sul collegamento dei problemi, viene visualizzato un elenco di avvertenze che segnalano eventuali problemi all’interno del pacchetto di progettazione. Di seguito sono riportati i diversi scenari in cui gli avvisi vengono rilevati e visualizzati dall&#39;utilità di importazione della progettazione:

* HTML fa riferimento a immagini che non esistono all’interno del pacchetto.
* HTML fa riferimento a script che non esistono nel pacchetto.
* HTML fa riferimento a stili che non esistono nel pacchetto.

### Dove vengono memorizzati i file del file ZIP in AEM? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Dopo l’importazione della pagina di destinazione, i file (immagini, css, js e così via) all’interno del pacchetto di progettazione vengono memorizzati nel seguente percorso in AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supponiamo che la pagina di destinazione sia creata in We.Retail della campagna e che il nome della pagina di destinazione sia **myBlankLandingPage** quindi la posizione in cui vengono memorizzati i file ZIP è la seguente:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Formattazione non mantenuta {#formatting-not-preserved}

Quando crei un file CSS, tieni presente le seguenti limitazioni:

Se un testo e un’immagine (modificabile) sono simili ai seguenti:

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

con un CSS applicato alla classe `box` come segue:

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

Then `box img` viene utilizzato in importazione progettazione, la formattazione della pagina di destinazione risultante non sembra essere stata mantenuta. Per ovviare a questo problema, l’AEM aggiunge tag div nel CSS e riscrive il codice di conseguenza. In caso contrario, alcune regole CSS non saranno valide.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
>
>Inoltre, i designer devono essere consapevoli del fatto che solo il codice all’interno del **id=cqcanvas** il tag viene riconosciuto dall’importazione, altrimenti la progettazione non viene mantenuta.
