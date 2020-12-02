---
title: Estensione e configurazione di Importazione progettazione per le pagine di destinazione
seo-title: Estensione e configurazione di Importazione progettazione per le pagine di destinazione
description: Scoprite come configurare Importazione progettazione per le pagine di destinazione.
seo-description: Scoprite come configurare Importazione progettazione per le pagine di destinazione.
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 63%

---


# Estensione e configurazione di Importazione progettazione per pagine di destinazione{#extending-and-configuring-the-design-importer-for-landing-pages}

Questa sezione descrive come configurare ed eventualmente estendere la funzione Importazione progettazione per le pagine di destinazione. L&#39;utilizzo delle pagine di destinazione dopo l&#39;importazione è trattato in [Pagine di destinazione.](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**Estrazione di un componente personalizzato tramite Importazione progettazione**

Passaggi logici per il riconoscimento di un componente personalizzato da parte di Importazione progettazione

1. Creare un gestore di tag

   * Un gestore di tag è un elemento POJO che gestisce i tag HTML di un particolare tipo. Il “tipo” di tag HTML che può essere gestito viene definito dalla proprietà TagHandlerFactory OSGi “tagpattern.name”. Questa proprietà OSGi è essenzialmente un regex che deve corrispondere al tag HTML in input che si intende gestire. Tutti i tag nidificati vengono quindi inviati al gestore di tag. Se, ad esempio, vi registrate per un elemento div che contiene un tag nidificato &lt;p>, anche il tag &lt;p> viene inviato al gestore di tag e dipende da come intendete gestirlo.
   * L’interfaccia del gestore di tag è simile a quella di un gestore di contenuti SAX. Riceve eventi SAX per ciascun tag HTML. Come fornitore del gestore di tag, è necessario implementare alcuni metodi lifecycle che vengono automaticamente chiamati dal framework di Importazione progettazione.

1. Create il tagHandlerFactory corrispondente.

   * L’elemento TagHandlerFactory è un componente OSGi (singleton) responsabile per la generazione di istanze del gestore di tag.
   * L’elemento TagHandlerFactory deve esporre la proprietà OSGi “tagpattern.name”, il cui valore corrisponde al tag HTML in input.
   * Se esistono diversi gestori di tag che corrispondono al tag HTML di input, viene scelto quello con classificazione maggiore. La classificazione stessa è esposta come proprietà OSGi **service.ranking**.
   * L’elemento TagHandlerFactory è un componente OSGi. Eventuali riferimenti che desiderate fornire al gestore di tag devono essere gestiti da questo componente factory.

1. Accertatevi che TagHandlerFactory disponga di una classificazione migliore se desiderate ignorare il valore predefinito.

>[!CAUTION]
>
>L’importazione di progettazione, usata per importare le pagine di destinazione, [è diventata obsoleta in AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features).

## Preparazione dell’HTML per l’Importazione {#preparing-the-html-for-import}

Dopo aver creato una pagina di importazione, potete importare la pagina di destinazione HTML completa. Per importare la pagina di destinazione HTML, occorre innanzitutto creare un pacchetto di progettazione, ossia un file .zip del suo contenuto. Il pacchetto di progettazione contiene la pagina di destinazione HTML e tutti i contenuti a cui si fa riferimento (immagini, css, icone, script e così via).

Esempio di come preparare la pagina HTML da importare:

Pagina di destinazione

[Ottieni file](assets/cheatsheet.zip)

### Layout e requisiti del file .zip {#zip-file-layout-and-requirements}

>[!NOTE]
>
>A questo punto, i file ZIP possono solo contenere una pagina HTML o una parte di una pagina.

Esempio di layout del file ZIP:

* /index.html -> file HTML della pagina di destinazione
* /css -> da aggiungere a clientlib CSS
* /img -> tutte le immagini e le risorse
* /js -> da aggiungere alla clientlib JS

Il layout si basa sulle best practice HTML5 Boilerplate. Ulteriori informazioni su [https://html5boilerplate.com/](https://html5boilerplate.com/)

>[!NOTE]
>
>Come minimo, il pacchetto di progettazione **deve contenere un file** index.html **a livello principale.** Se anche la pagina di destinazione da importare dispone di una versione mobile, il file ZIP deve contenere **mobile.index.html** insieme a **index.html** a livello principale.

### Preparazione della pagina di destinazione HTML {#preparing-the-landing-page-html}

Per poter importare il file HTML, occorre aggiungere un elemento canvas div alla pagina di destinazione HTML.

L&#39;elemento canvas div è un elemento HTML **div** con `id="cqcanvas"` che deve essere inserito nel tag HTML `<body>` e deve racchiudere il contenuto destinato alla conversione.

Snippet di esempio della pagina di destinazione HTML dopo l’aggiunta dell’elemento canvas div:

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

### Preparazione del file HTML per l’inclusione di componenti AEM modificabili {#preparing-the-html-to-include-editable-aem-components}

Quando importate una pagina di destinazione, potete scegliere se importare la pagina così com’è. In questo caso, una volta importata la pagina di destinazione non sarà più possibile modificare gli elementi importati in AEM. Tuttavia sarà possibile aggiungere alla pagina altri componenti AEM.

Prima di importare la pagina di destinazione, potete eventualmente convertire alcune sue parti in modo da ottenere componenti AEM modificabili. Questo consente di modificare rapidamente alcune parti della pagina di destinazione anche dopo l’importazione.

A questo scopo occorre aggiungere l’attributo `data-cq-component` al componente appropriato nel file HTML da importare.

Di seguito viene descritto come modificare il file HTML al fine di convertire alcune parti della pagina di destinazione in diversi componenti AEM modificabili. I componenti sono descritti in dettaglio in [Componenti delle pagine di destinazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md).

>[!NOTE]
>
>La marcatura HTML per convertire parti della pagina di destinazione in componenti AEM dispone di una forma estesa e di una dichiarazione di tag con abbreviazioni. Per ciascun componente vengono descritte entrambe queste forme.

### Limitazioni   {#limitations}

Prima di procedere all’importazione, considerate i seguenti limiti:

### Eventuali attributi come class o id applicati al &amp;lt;body> tag non viene mantenuto{#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

Se un attributo come id o class viene applicato al tag body, ad esempio `<body id="container">`, dopo l&#39;importazione non viene mantenuto. Pertanto, la progettazione importata non deve avere dipendenze dagli attributi applicati al tag `<body>`.

### Caricamento del file ZIP tramite trascinamento {#drag-and-drop-zip}

Il caricamento del file ZIP tramite trascinamento non è supportato per Internet Explorer e Firefox versione 3.6 e precedenti. Per caricare una progettazione con uno di questi browser, fate clic sulla zone di rilascio del file per aprire una finestra di dialogo che consente di caricare la progettazione.

I browser che supportano il &quot;trascinamento&quot; del file ZIP della progettazione sono Chrome, Safari5.x, Firefox 4 e versioni successive.

### Modernizr non è supportato {#modernizr-is-not-supported}

`Modernizr.js` è uno strumento basato su javascript che rileva le funzionalità native dei browser e se queste sono o meno adatte per elementi html5. Le progettazioni che utilizzano Modernizr per estendere il supporto delle versioni precedenti di vari browser possono provocare problemi di importazione nella soluzione della pagina di destinazione. Gli script `Modernizr.js` non sono supportati da Importazione progettazione.

### Le proprietà pagina non vengono mantenute al momento dell’importazione del pacchetto di progettazione {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

Eventuali proprietà pagina (ad esempio Dominio personalizzato, Applicazione HTTPS ecc.) impostate per una pagina (che utilizza il modello Pagina di destinazione vuota) prima dell’importazione del pacchetto di progettazione vengono perdute dopo l’importazione. Si consiglia quindi di impostare le proprietà pagina dopo l’importazione del pacchetto di progettazione.

### Marcatura solo HTML considerata {#html-only-markup-assumed}

Durante l’importazione il codice viene bonificato per motivi di sicurezza e per evitare di importare e pubblicare un codice non valido. Ciò presuppone che solo il codice HTML e tutte le altre forme di elementi, ad esempio i componenti web o SVG in linea, saranno esclusi dal filtro.

### Testo {#text}

Marcatura HTML per inserire un componente testo (`foundation/components/text`) nel codice HTML in un pacchetto di progettazione:

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

Risultato dell’inclusione nell’HTML della marcatura riportata qui sopra:

* Crea un componente AEM testo modificabile ( `sling:resourceType=foundation/components/text`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Viene impostata la proprietà `text` del componente di testo creato nell’HTML racchiuso nell’elemento `div`.

**Dichiarazione abbreviata del tag del componente**:

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**Testo con elenco**

Per aggiungere un testo con un elenco:

* 1°
* 2°

che possa essere modificato nell’editor RTE:

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**Testo con colore**

Per aggiungere un testo con colore (rosa) che possa essere modificato nell’editor RTE:

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### Titolo {#title}

Marcatura HTML per inserire un componente titolo ( `wcm/landingpage/components/title`) nel codice HTML all’interno del pacchetto di progettazione:

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

Risultato dell’inclusione nell’HTML della marcatura riportata qui sopra:

* Crea un componente titolo AEM modificabile ( `sling:resourceType=wcm/landingpage/components/title`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Imposta la proprietà `jcr:title` del componente titolo creato sul testo all’interno del tag del titolo racchiuso in un elemento div.
* Imposta la proprietà `type` sul tag del titolo, in questo caso `h1`.

Il componente titolo supporta 7 tipi: `h1, h2, h3, h4, h5, h6` e `default`.

**Dichiarazione abbreviata del tag del componente**:

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### Immagine {#image}

Marcatura HTML per inserire un componente immagine (foundation/components/image) nel codice HTML in un pacchetto di progettazione:

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

Risultato dell’inclusione nell’HTML della marcatura riportata qui sopra:

* Crea un componente immagine AEM modificabile ( `sling:resourceType=foundation/components/image`) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Imposta la proprietà `fileReference` del componente immagine creato sul percorso nel quale viene importata l’immagine specificata dall’attributo src.
* Imposta la proprietà `alt` sul valore dell&#39;attributo alt nel tag img.
* Imposta la proprietà `title` sul valore dell’attributo title nel tag img.
* Imposta la proprietà `width` sul valore dell’attributo width nel tag img.
* Imposta la proprietà `height` sul valore dell&#39;attributo height nel tag img.

**Dichiarazione abbreviata del tag del componente**:

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### Nell’elemento div del componente immagine non è supportato img src con URL assoluto {#absolute-url-img-src-not-supported-within-image-component-div}

Se per la conversione di un componente viene tentato un tag `<img>` con src con un URL assoluto, viene generato un tag **UnsupportedTagContentException** appropriato. Esempio di riferimento non supportato:

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

Fatta eccezione di questo caso, immagini con URL assoluto sono supportate per i tag img che non sono parte dell’elemento div di un componente immagine.

### Componenti di invito all’azione  {#call-to-action-components}

È possibile contrassegnare una parte della pagina di destinazione da importare come &quot;componente Invito all’azione modificabile&quot;, che potrà essere modificato dopo l’importazione della pagina di destinazione. AEM include i seguenti componenti CTA (Call To Action, invito all’azione):

* Collegamento ClickThrough: consente di aggiungere un collegamento testuale su cui il visitatore può fare clic per passare all’URL di destinazione.
* Collegamento grafico: consente di aggiungere un’immagine su cui il visitatore può fare clic per passare all’URL di destinazione.

#### Collegamento ClickThrough  {#click-through-link}

Questo componente CTA può essere usato per aggiungere un testo con collegamento sulla pagina di destinazione.

Proprietà supportate

* Etichetta, con opzioni per grassetto, corsivo e sottolineato
* URL di destinazione, supporta URL di terze parti e di AEM
* Opzioni per il rendering della pagina (stessa finestra, nuova finestra, ecc.)

Tag HTML per includere un componente collegamento ClickThrough nel file ZIP importato. Qui href viene mappato sull’URL di destinazione, &quot;Visualizza dettagli prodotto&quot; viene mappato sull’etichetta e così via.

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

Questo componente può essere usato in qualsiasi applicazione indipendente oppure può essere importato da un pacchetto ZIP.

**Dichiarazione abbreviata del tag del componente**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### Collegamento grafico {#graphical-link}

Questo componente Invito all&#39;azione può essere usato per aggiungere un’immagine come collegamento sulla pagina di destinazione. L’immagine può essere un semplice pulsante o un’immagine grafica di sfondo. Quando un visitatore fa clic sull’immagine, viene portato all’URL di destinazione specificato nelle proprietà del componente. Fa parte del gruppo “Invito all’Azione”.

Proprietà supportate

* Ritaglio e rotazione immagine
* Testo che compare al passaggio del mouse, descrizione, dimensione in px
* URL di destinazione, supporta URL di terze parti e di AEM
* Opzioni per il rendering della pagina (stessa finestra, nuova finestra, ecc.)

Tag HTML per includere un componente collegamento grafico nel file ZIP importato. Qui href viene mappato sull’URL di destinazione, img src è l’immagine di rendering, &quot;title&quot; viene preso come testo al passaggio del mouse e così via.

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**Dichiarazione abbreviata del tag del componente**:

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>Per creare un collegamento grafico, occorre racchiudere un tag di ancoraggio e il tag immagine all’interno di un elemento div con l’attributo `data-cq-component="clickthroughgraphicallink"`.
>
>Esempio: `<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>Non sono supportati altri metodi per associare un’image con un tag di ancoraggio utilizzando CSS, ad esempio la marcatura seguente non funziona:
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>associato a `css .hasbackground { background-image: pathtoimage }`


### Modulo lead {#lead-form}

I moduli lead vengono utilizzati per raccogliere le informazioni profilo di un visitatore o lead. Tali informazioni vengono memorizzate e usate più tardi per attività di marketing basate su informazioni. Le informazioni comprendono in genere qualifica, nome, indirizzo e-mail, data di nascita, interessi e così via. Fa parte del gruppo &quot;Modulo lead CTA&quot;.

**Funzioni supportate**

* Campi per lead predefiniti: nome, cognome, indirizzo, data di nascita, genere, informazioni, ID utente, ID e-mail, pulsante Invia sono disponibili nella barra laterale. È sufficiente trascinare il componente richiesto nel modulo per lead.
* Inserendo questi componenti è possibile creare moduli per lead indipendenti, con campi per moduli lead. In applicazioni ZIP indipendenti o importate, gli utenti possono aggiungere altri campi utilizzando i campi per modulo cq:form o di invito all’azione, assegnare loro un nome e progettarli in base alle proprie esigenze.
* Mappare i campi per i moduli lead utilizzando nomi predefiniti specifici per i moduli lead CTA, ad esempio firstName per il nome nel modulo lead e così via.
* I campi che non vengono mappati sul modulo lead vengono mappati su componenti cq:form: testo, pulsante di scelta, casella di selezione, menu a comparsa, nascosto e password.
* L’utente può fornire il titolo con il tag “label” e la formattazione con l’attributo di stile “class” (disponibile solo per i componenti per modulo lead CTA).
* La pagina di ringraziamento e l’elenco di iscrizione possono essere forniti come parametro nascosto del modulo (presente nel file index.htm) oppure possono essere aggiunti o modificati dalla barra di modifica di &quot;Inizio del modulo lead&quot;

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot; />

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot; />

* Vincoli come - possono essere forniti dalla configurazione di modifica di ciascun componente.

Tag HTML per includere un componente collegamento grafico nel file ZIP importato. Qui &quot;firstName&quot; è mappato su firstName del modulo lead e così via, tranne che per le caselle di controllo - queste due caselle di controllo vengono mappate sul componente a discesa cq:form.

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

Il componente AEM parsys è un contenitore per altri componenti AEM. È possibile aggiungere un componente parsys nell’HTML importato. Questo consente di aggiungere o eliminare componenti AEM modificabili nella pagina di destinazione anche dopo l’importazione.

Il sistema paragrafo offre agli utenti la possibilità di aggiungere componenti mediante la barra laterale.

Marcatura HTML per inserire un componente parsys (`foundation/components/parsys`) nel codice HTML in un pacchetto di progettazione:

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

Risultato dell’inclusione nell’HTML della marcatura riportata qui sopra:

* Inserisce un componente AEM parsys (foundation/components/parsys) nella pagina di destinazione creata dopo l’importazione del pacchetto di progettazione.
* Inizializza la barra laterale con componenti predefiniti. Per aggiungere nuovi componenti alla pagina di destinazione, trascinateli dalla barra laterale al componente parsys.
* Due piccoli componenti appartengono a parsys.

### Destinazione  {#target}

Il componente Destinazione mostra i contenuti di un’esperienza sulla pagina. È possibile creare numerose esperienze in una campagna e il componente Destinazione può mostrare in modo dinamico i contenuti da diverse esperienze per i diversi visitatori della pagina.

Marcatura HTML per inserire un componente Destinazione e creare diverse esperienze in una campagna:

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

Oltre a specificare se i componenti importati sono componenti AEM modificabili, potete anche configurare quanto segue prima di importare il pacchetto di progettazione:

* Impostazione delle proprietà pagina mediante l’estrazione dei metadati definiti nell’HTML importato.
* Specifica della codifica charset nell’HTML.
* Sovrapposizione del modello di pagina di importazione.

### Impostazione delle proprietà pagina mediante l’estrazione dei metadati definiti nell’HTML importato {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

I seguenti metadati dichiarati nell’intestazione dell’HTML importato vengono estratti e mantenuti da Importazione progettazione come proprietà &quot;jcr:description&quot;:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

L&#39;attributo Lang impostato nel tag HTML viene estratto e mantenuto da Importazione progettazione come proprietà &quot;jcr:language&quot;

* &lt;html lang=&quot;en&quot;>

### Specifica della codifica charset nell’HTML {#specifying-the-charset-encoding-in-the-html}

Importazione progettazione legge la codifica specificata nell’HTML importato. La codifica può essere specificata come segue:

`<meta charset="UTF-8">`

*OPPURE*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

Se non si specifica alcuna codifica nell’HTML importato, Importazione progettazione imposta la codifica predefinita UTF-8.

### Sovrapposizione del modello  {#overlaying-template}

Per sovrapporre il modello Pagina di destinazione vuota, createne uno nuovo in: `/apps/<appName>/designimporter/templates/<templateName>`

I passaggi per la creazione di un nuovo modello in AEM sono descritti [qui](/help/sites-developing/templates.md).

### Riferimento a un componente dalla pagina di destinazione {#referring-a-component-from-landing-page}

Supponiamo che vogliate fare riferimento a un componente nell’HTML utilizzando l’attributo data-cq-component in modo che Importazione progettazione effettui il rendering del componente. Ad esempio, è necessario fare riferimento al componente Tabella ( `resourceType = /libs/foundation/components/table`). è necessario aggiungere quanto segue all’HTML:

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

Il percorso in data-cq-component deve corrispondere al resourceType del componente.

### Best practice    {#best-practices}

Non è consigliato usare selettori CSS simili ai seguenti con elementi contrassegnati per la conversione del componente durante l’importazione.

| E > F | un elemento F figlio di un elemento E | [Combinatore di bambini](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E &amp;gt; F | un elemento F immediatamente preceduto da un elemento E | [Combinatore di pari livello adiacente](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | un elemento F preceduto da un elemento E | [Combinazione generale di pari livello](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | un elemento E, radice del documento | [pseudoclassi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | un elemento E, n-esimo figlio del proprio elemento padre | [pseudoclassi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | un elemento E, n-esimo figlio del proprio elemento padre, a partire dall’ultimo | [pseudoclassi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | un elemento E, n-esimo elemento di pari livello del proprio tipo | [pseudoclassi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | un elemento E, n-esimo elemento di pari livello del proprio tipo, a partire dall’ultimo | [pseudoclassi strutturali](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

Ciò è dovuto al fatto che elementi HTML aggiuntivi come il tag &lt;div> vengono aggiunti all’HTML generato dopo l’importazione.

* Si consiglia inoltre di non utilizzare script che si basano su una struttura simile a quella riportata qui sopra con elementi contrassegnati per la conversione in componenti AEM.
* Si consiglia di non utilizzare stili sui tag di marcatura per la conversione di componenti come &lt;div data-cq-component=&quot;&amp;ast;&quot;>.
* Il layout di progettazione deve seguire le best practice di HTML5 Boilerplate. Ulteriori informazioni su: [https://html5boilerplate.com/](https://html5boilerplate.com/).

## Configurazione di moduli OSGI {#configuring-osgi-modules}

I componenti con proprietà configurabili tramite la console OSGI sono i seguenti:

* Importazione progettazione per pagina di destinazione
* Generazione pagina di destinazione
* Generazione pagina di destinazione per dispositivi mobili
* Pre-elaborazione pagina di destinazione

Le proprietà sono riassunte nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Descrizione proprietà </strong></td>
  </tr>
  <tr>
   <td>Importazione progettazione per pagina di destinazione</td>
   <td>Filtro estrazione</td>
   <td>Elenco di espressioni regolari da usare per filtrare i file dall’estrazione. <br /> Gli elementi ZIP che corrispondono a qualsiasi dei pattern specificati vengono esclusi dall’estrazione</td>
  </tr>
  <tr>
   <td>Generazione pagina di destinazione</td>
   <td>Pattern file</td>
   <td>Il Generatore di pagine di destinazione può essere configurato per gestire i file HTML che corrispondono a un'espressione regolare definita dal pattern di file.</td>
  </tr>
  <tr>
   <td>Generazione pagina di destinazione per dispositivi mobili</td>
   <td>Pattern file</td>
   <td>Il Generatore di pagine di destinazione può essere configurato per gestire i file HTML che corrispondono a un'espressione regolare definita dal pattern di file.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Gruppi dispositivo</td>
   <td>Elenco dei gruppi di dispositivi da supportare.</td>
  </tr>
  <tr>
   <td>Pre-elaborazione pagina di destinazione</td>
   <td>Pattern di ricerca </td>
   <td>Pattern da cercare, nei contenuti dell’archivio. A questa espressione regolare corrisponde il contenuto della voce riga per riga. Alla corrispondenza, il testo corrispondente viene sostituito con il pattern di sostituzione specificato.<br /> <br /> Vedere la nota di seguito sui limiti attuali della pre-elaborazione della pagina di destinazione.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Pattern di sostituzione</td>
   <td>Pattern con cui sostituire la corrispondenza trovata. Potete utilizzare riferimenti di gruppo regex come $1, $2. Inoltre, questo pattern supporta parole chiave come {designPath} che vengono risolte con il valore effettivo durante l'importazione.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**Limite attuale della pre-elaborazione della pagina di destinazione:**
>Se dovete apportare delle modifiche al pattern di ricerca, quando aprite l’editor di proprietà Felix dovete aggiungere manualmente i caratteri di barra rovesciata per effettuare l’escape dei metacaratteri regex. In caso contrario, il regex viene considerato non valido e non potrà sostituire il precedente.
>
>Ad esempio, se la configurazione predefinita è
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>E devi sostituire >`CQ_DESIGN_PATH` con `VIPURL` nel pattern di ricerca, il pattern di ricerca deve essere simile al seguente:
`/\* *VIPURL *\*/ *(['"])`

## Risoluzione dei problemi {#troubleshooting}

Quando si importa il pacchetto di progettazione, si potrebbero riscontrare alcuni errori, descritti in questa sezione.

### Inizializzazione della barra laterale con componenti relativi alla pagina di destinazione  {#initialization-of-sidekick-with-landing-page-relevant-components}

Se il pacchetto di progettazione contiene una marcatura di componente parsys, dopo l’importazione la barra laterale inizia a mostrare componenti relativi alla pagina di destinazione. Potete rilasciare nuovi componenti sul componente parsys nella pagina di destinazione. Potete inoltre passare alla modalità di progettazione e aggiungere nuovi componenti alla barra laterale.

### Messaggi di errore visualizzati durante l’importazione {#error-messages-displayed-during-import}

In caso di errori (ad es. se il pacchetto importato non è un file ZIP valido), Importazione progettazione non importa il pacchetto e visualizza un messaggio di errore sulla pagina appena sopra la casella di rilascio e di trascinamento. Seguono alcuni esempi di scenari di errore. Una volta corretto l’errore, potete importare nuovamente il file ZIP aggiornato nella stessa pagina di destinazione vuota. Diversi scenari in cui si verifica un errore:

* Il pacchetto di progettazione importato non è un archivio ZIP valido.
* Il pacchetto di progettazione importato non contiene un file index.html al livello principale.

### Avvertenze visualizzate dopo l’importazione {#warnings-displayed-after-import}

In caso di avvisi (ad esempio, se l&#39;HTML fa riferimento a immagini che non esistono nel pacchetto), Importazione progettazione importa il file ZIP e visualizza un elenco di problemi/avvisi nel riquadro dei risultati. Facendo clic sul collegamento dei problemi, verrà visualizzato un elenco di avvisi che segnalano eventuali problemi nel pacchetto di progettazione. Alcuni scenari di avvertenze rilevate e visualizzate da Importazione progettazione:

* L’HTML fa riferimento a immagini che non esistono nel pacchetto.
* L&#39;HTML fa riferimento a script che non esistono nel pacchetto.
* L’HTML fa riferimento a stili che non esistono nel pacchetto.

### Dove vengono memorizzati in AEM i file dell’archivio ZIP? {#where-are-the-files-of-the-zip-file-being-stored-in-aem}

Dopo l’importazione di una pagina di destinazione, i file (immagini, css, js, ecc.) nel pacchetto di progettazione sono memorizzati nel seguente percorso in AEM:

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

Supponiamo che la pagina di destinazione venga creata nella campagna We.Retail e che il nome della pagina di destinazione sia **myBlankLandingPage**, quindi la posizione in cui i file ZIP vengono memorizzati è la seguente:

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### Formattazione non mantenuta {#formatting-not-preserved}

Quando create il CSS, tenete presenti i seguenti limiti:

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

Quindi `box img` viene utilizzato in Importazione progettazione, la pagina di destinazione risultante non ha mantenuto la formattazione. Per ovviare a questo problema, tenete presente che AEM aggiunge i tag div nel CSS e riscrive di conseguenza il codice. In caso contrario alcune regole CSS risulterebbero non valide.

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
Inoltre, i designer devono essere consapevoli del fatto che solo il codice all&#39;interno del tag **id=cqcanvas** è riconosciuto dal modulo di importazione, altrimenti la progettazione non viene mantenuta.

