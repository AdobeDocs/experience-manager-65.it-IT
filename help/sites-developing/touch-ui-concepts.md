---
title: Concetti dell’interfaccia utente di AEM Touch
seo-title: Concetti dell’interfaccia utente di AEM Touch
description: Con AEM 5.6 Adobe ha introdotto una nuova interfaccia touch con design reattivo per l’ambiente di authoring
seo-description: Con AEM 5.6 Adobe ha introdotto una nuova interfaccia touch con design reattivo per l’ambiente di authoring
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Concetti dell’interfaccia utente di AEM Touch{#concepts-of-the-aem-touch-enabled-ui}

AEM offre un’interfaccia touch con design [](/help/sites-authoring/responsive-layout.md) reattivo per l’ambiente di authoring, progettato per funzionare sia sui dispositivi touch che sui dispositivi desktop.

>[!NOTE]
>
>L’interfaccia touch è l’interfaccia standard di AEM. L’interfaccia classica era obsoleta con AEM 6.4.

L’interfaccia touch include:

* L&#39;intestazione della suite che:
   * Mostra il logo
   * Fornisce un collegamento alla navigazione globale
   * Fornisce un collegamento ad altre azioni generiche; come Cerca, Aiuto, Soluzioni Marketing Cloud, Notifiche e Impostazioni utente.
* La barra a sinistra (visualizzata quando necessario e nascosta), che può mostrare:
   * Timeline
   * Riferimenti
   * Filtri
* L’intestazione di navigazione, anch’essa sensibile al contesto, può mostrare:
   * Indica la console in uso e/o la posizione all’interno della console
   * Selezione per la barra a sinistra
   * Breadcrumb
   * Accesso alle azioni **Create** appropriate
   * Visualizzare le selezioni
* L&#39;area contenuto che:
   * Elenca gli elementi di contenuto (siano essi pagine, risorse, post di forum, ecc.)
   * Può essere formattato come richiesto, ad esempio colonna, scheda o elenco
   * Utilizza un design reattivo (il display si ridimensiona automaticamente in base al dispositivo e/o alle dimensioni della finestra)
   * Utilizza lo scorrimento infinito (nessuna impaginazione più impaginazione; tutti gli elementi sono elencati in una finestra)

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>Quasi tutte le funzionalità di AEM sono state portate nell’interfaccia touch. Tuttavia, in alcuni casi limitati, le funzionalità torneranno all’interfaccia classica. Per ulteriori informazioni, consulta Stato [delle funzioni dell’interfaccia](/help/release-notes/touch-ui-features-status.md) touch.

L’interfaccia touch è stata progettata da Adobe per garantire coerenza nell’esperienza utente tra più prodotti. Si basa su:

* **Interfaccia** utente Coral (CUI) un’implementazione dello stile visivo di Adobe per l’interfaccia touch. L&#39;interfaccia utente Coral fornisce tutto il prodotto/progetto/applicazione Web necessario per adottare lo stile visivo dell&#39;interfaccia utente.
* **I componenti dell’interfaccia** Granite sono creati con l’interfaccia utente Coral.

I principi di base dell’interfaccia touch sono:

* Prima di tutto per dispositivi mobili (tenendo presente il desktop)
* Design reattivo
* Visualizzazione contestuale
* Riutilizzabile
* Includi documentazione di riferimento incorporata
* Includi test incorporati
* Progettazione dal basso verso l’alto per garantire che questi principi vengano applicati a ogni elemento e componente

Per un&#39;ulteriore panoramica della struttura dell&#39;interfaccia touch, consultate l&#39;articolo [Struttura dell&#39;interfaccia utente](/help/sites-developing/touch-ui-structure.md)AEM Touch.

## Stack di tecnologia AEM {#aem-technology-stack}

AEM utilizza la piattaforma Granite come base e la piattaforma Granite include, tra le altre cose, il repository di contenuti Java.

![chlimage_1-80](assets/chlimage_1-80.png)

## GRANITE {#granite}

Granite è lo stack Web aperto di Adobe, che fornisce vari componenti tra cui:

* Avvio di un&#39;applicazione
* Un framework OSGi in cui tutto è distribuito
* Numerosi servizi di compendio OSGi per supportare le applicazioni di creazione
* Un framework di registrazione completo che fornisce diverse API di registrazione
* Implementazione del repository CRX della specifica API JCR
* Apache Sling Web Framework
* Parti aggiuntive dell&#39;attuale prodotto CRX

>[!NOTE]
>
>Granite viene eseguito come progetto di sviluppo aperto in Adobe: i contributi al codice, le discussioni e le questioni vengono effettuati da tutta l&#39;azienda.
>
>Tuttavia, Granite **non** è un progetto open source. È fortemente basato su diversi progetti open source (Apache Sling, Felix, Jackrabbit e Lucene in particolare), ma Adobe disegna una linea chiara tra ciò che è pubblico e ciò che è interno.

## Interfaccia Granite {#granite-ui}

La piattaforma di progettazione Granite fornisce anche un framework di interfaccia utente di base. I principali obiettivi di tale iniziativa sono:

* Fornisci widget di interfaccia utente granulare
* Implementate i concetti dell’interfaccia utente e illustrate le procedure ottimali (rendering di elenchi lunghi, filtro di elenchi, creazione di oggetti CRUD, procedure guidate CUD).
* Fornire un&#39;interfaccia utente di amministrazione estensibile e basata su plug-in

Tali requisiti sono conformi:

* Rispetto di &quot;mobile first&quot;
* Essere estensibile
* Semplice da ignorare

![chlimage_1-81](assets/chlimage_1-81.png)GraniteUI.pdf

[Ottieni file](assets/graniteui.pdf)dall’interfaccia utente Granite:

* Utilizza l&#39;architettura RESTful di Sling
* Implementa le librerie di componenti destinate alla creazione di applicazioni Web incentrate sui contenuti
* Fornisce widget di interfaccia utente granulare
* Offre un’interfaccia utente standard predefinita
* È estensibile
* È progettato sia per dispositivi mobili che per desktop (rispetta innanzitutto i dispositivi mobili)
* può essere utilizzato in qualsiasi piattaforma/prodotto/progetto basato su Granite; ad esempio AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI Foundation Components](#granite-ui-foundation-components)Questa libreria di componenti di base può essere utilizzata o estesa da altre librerie.
* [Componenti per l’amministrazione dell’interfaccia utente Granite](#granite-ui-administration-components)

### Lato client e lato server {#client-side-vs-server-side}

La comunicazione client-server nell&#39;interfaccia utente Granite è costituita da ipertesto, non da oggetti, quindi non è necessario che il client comprenda la logica di business

* Il server arricchisce l’HTML con dati semantici
* Il client arricchisce l&#39;ipertesto con l&#39;ipermedia (interazione)

![chlimage_1-83](assets/chlimage_1-83.png)

#### Client-Side {#client-side}

Viene utilizzata un&#39;estensione del vocabolario HTML, purché l&#39;autore possa esprimere l&#39;intenzione di creare un&#39;app Web interattiva. Questo è un approccio simile a [WAI-ARIA](https://www.w3.org/TR/wai-aria/) e [microformati](https://microformats.org/).

Consiste principalmente in una raccolta di pattern di interazione (ad esempio, l&#39;invio asincrono di un modulo) interpretati dai codici JS e CSS, eseguiti sul lato client. Il ruolo del lato client è quello di migliorare il markup (dato come l&#39;ipermedia conveniente dal server) per l&#39;interattività.

Il lato client è indipendente da qualsiasi tecnologia server. Fintanto che il server fornisce la marcatura appropriata, il lato client può svolgere il proprio ruolo.

Attualmente i codici JS e CSS sono forniti come [clientlibs](/help/sites-developing/clientlibs.md) Granite nella categoria:

`granite.ui.foundation and granite.ui.foundation.admin`

Questi vengono forniti come parte del pacchetto di contenuti:

`granite.ui.content`

#### Lato server {#server-side}

Questo è costituito da una raccolta di componenti Sling che consentono all&#39;autore di *comporre* rapidamente un&#39;app Web. Lo sviluppatore sviluppa i componenti, l’autore assembla i componenti come un’app Web. Il ruolo del lato server consiste nel fornire al client i costi (markup) dell&#39;ipermedia.

Attualmente i componenti si trovano nel repository di Granite all&#39;indirizzo:

`/libs/granite/ui/components/foundation`

Viene distribuito come parte del pacchetto di contenuti:

`granite.ui.content`

### Differenze con l’interfaccia classica {#differences-with-the-classic-ui}

Sono interessanti anche le differenze tra l’interfaccia Granite e ExtJS (utilizzata per l’interfaccia classica):

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Interfaccia Granite</strong></td>
  </tr>
  <tr>
   <td>Chiamata a procedura remota<br /> </td>
   <td>Transistenze Stato</td>
  </tr>
  <tr>
   <td>Oggetti di trasferimento dati</td>
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>Il client conosce gli interni del server</td>
   <td>Il client non conosce gli interni</td>
  </tr>
  <tr>
   <td>"Fat client"</td>
   <td>"Thin client"</td>
  </tr>
  <tr>
   <td>Librerie client specializzate</td>
   <td>Librerie client universali</td>
  </tr>
 </tbody>
</table>

### Componenti Granite UI Foundation {#granite-ui-foundation-components}

I componenti [di base per l’interfaccia utente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) Granite forniscono gli elementi di base necessari per la creazione di qualsiasi interfaccia utente. Esse comprendono, tra l&#39;altro:

* Pulsante
* Collegamento ipertestuale
* Avatar utente

I componenti di base si trovano in:

`/libs/granite/ui/components/foundation`

Questa libreria contiene un componente dell’interfaccia Granite per ogni elemento Coral. Un componente è basato sul contenuto e la sua configurazione risiede nella directory archivio. Questo consente di comporre un’applicazione di interfaccia Granite senza scrivere tag HTML a mano.

Scopo:

* Modello di componente per elementi HTML
* Composizione componente
* Test automatico di unità e funzionalità

Implementazione:

* Composizione e configurazione basate su repository
* Sfruttare gli impianti di prova forniti dalla piattaforma Granite
* Modello JSP

Questa libreria di componenti di base può essere utilizzata o estesa da altre librerie.

### ExtJS e componenti dell&#39;interfaccia Granite corrispondenti {#extjs-and-corresponding-granite-ui-components}

Quando si aggiorna il codice ExtJS per l&#39;utilizzo dell&#39;interfaccia utente Granite, l&#39;elenco seguente fornisce una panoramica pratica degli xtype e dei tipi di nodo ExtJS con i tipi di risorse equivalenti dell&#39;interfaccia Granite.

| **ExtJS xtype** | **Tipo di risorsa dell’interfaccia utente Granite** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **Tipo nodo** | **Tipo di risorsa dell’interfaccia utente Granite** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Componenti per l’amministrazione dell’interfaccia utente Granite {#granite-ui-administration-components}

I componenti [di amministrazione dell’interfaccia utente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) Granite si basano sui componenti di base per fornire blocchi di base generici che qualsiasi applicazione di amministrazione può implementare. Tra questi figurano, tra l&#39;altro:

* Barra di navigazione globale
* Barra (scheletro)
* Pannello di ricerca

Scopo:

* Aspetto unificato per le applicazioni di amministrazione
* RAD per applicazioni amministrative

Implementazione:

* Componenti predefiniti che utilizzano i componenti di base
* I componenti possono essere personalizzati

## Interfaccia utente Coral {#coral-ui}

CoralUI.pdf

[L’interfaccia utente &quot;Get File](assets/coralui.pdf)Coral UI&quot; (CUI) è un’implementazione dello stile visivo di Adobe per l’interfaccia touch, progettata per garantire coerenza nell’esperienza utente tra più prodotti. L’interfaccia utente Coral offre tutto il necessario per adottare lo stile visivo utilizzato nell’ambiente di authoring.

>[!CAUTION]
>
>L’interfaccia utente Coral è una libreria di interfaccia utente accessibile ai clienti AEM per la creazione di applicazioni e interfacce Web entro i limiti dell’utilizzo concesso in licenza del prodotto.
>
>L’utilizzo dell’interfaccia utente Coral è consentito solo:
>
>
>* Una volta spedito e fornito in bundle con AEM.
>* Da utilizzare per estendere l’interfaccia esistente dell’ambiente Authoring.
>* Materiale collaterale aziendale Adobe, annunci pubblicitari e presentazioni.
>* Interfaccia delle applicazioni Adobe (il font non deve essere facilmente disponibile per altri usi).
>* Con personalizzazioni minori.
>
>
È consigliabile evitare l’utilizzo dell’interfaccia utente Coral in:
>
>* Documenti e altri elementi non correlati ad Adobe.
>* Ambienti per la creazione di contenuti (in cui gli elementi precedenti potrebbero essere generati da altri).
>* Applicazioni/componenti/pagine Web che non sono chiaramente collegate ad Adobe.
>



L’interfaccia utente Coral è una raccolta di elementi di base per lo sviluppo di applicazioni Web.

![chlimage_1-84](assets/chlimage_1-84.png)

Progettato per essere modulare fin dall&#39;inizio, ciascun modulo forma un livello distinto in base al suo ruolo primario. Sebbene i livelli siano stati progettati per supportare l’uno con l’altro, possono essere utilizzati anche in modo indipendente se necessario. Questo consente di implementare l’esperienza utente di Coral in qualsiasi ambiente compatibile con HTML.

Con l’interfaccia utente Coral non è obbligatorio utilizzare un particolare modello di sviluppo e/o piattaforma. L’obiettivo principale di Coral è quello di fornire tag HTML5 unificati e puliti, indipendentemente dal metodo utilizzato per emettere tale marcatura. Questo può essere utilizzato per il rendering lato client o server, modelli, JSP, PHP o anche applicazioni Adobe Flash RIA, per citarne solo alcuni.

### Elementi HTML - Livello di marcatura {#html-elements-the-markup-layer}

Gli elementi HTML offrono un aspetto comune a tutti gli elementi dell&#39;interfaccia utente di base (tra cui barra di navigazione, pulsante, menu, barra laterale, ecc.).

Al livello più basilare, un elemento HTML è un tag HTML con un nome di classe dedicato. Gli elementi più complessi possono essere composti da più tag, nidificati l&#39;uno all&#39;altro (in un modo specifico).

Il CSS viene utilizzato per fornire l&#39;aspetto e il comportamento effettivi. Per rendere possibile la personalizzazione dei valori di stile effettivi (ad es. per il marchio) dell&#39;aspetto e dell&#39;aspetto (ad es. per il marchio), vengono dichiarati come variabili espanse dal preprocessore [LESS](https://lesscss.org/) durante il runtime.

Scopo:

* Elementi di base dell’interfaccia utente con un aspetto comune
* Fornire il sistema griglia predefinito

Implementazione:

* Tag HTML con stili ispirati a [bootstrap](https://twitter.github.com/bootstrap/)
* Le classi sono definite nei file LESS
* Le icone sono definite come sprite di font

Ad esempio, la marcatura:

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

Viene visualizzato come:

![chlimage_1-85](assets/chlimage_1-85.png)

L&#39;aspetto è definito in LESS, legato a un elemento per nome di classe dedicato (l&#39;estratto seguente è stato abbreviato per ragioni di brevità):

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

I valori effettivi sono definiti in un file variabile LESS (il seguente estratto è stato abbreviato per ragioni di brevità):

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### Plugin elemento {#element-plugins}

Molti degli elementi HTML dovranno mostrare una specie di comportamento dinamico, come l&#39;apertura e la chiusura dei menu a comparsa. Questo è il ruolo dei plug-in di elementi, che eseguono tali attività manipolando il DOM utilizzando JavaScript.

Un plug-in è:

* Progettato per funzionare su un elemento DOM specifico. Ad esempio, un plug-in di dialogo prevede di trovare `DIV class=dialog`
* Generico in natura. Ad esempio, un gestore di layout fornisce il layout per qualsiasi elenco `DIV` o `LI` elemento

Il comportamento del plug-in può essere personalizzato con parametri, tramite:

* Passaggio dei parametri tramite una chiamata javascript
* Utilizzo di attributi dedicati `data-*` associati alla marcatura HTML

Anche se lo sviluppatore può selezionare l&#39;approccio migliore per qualsiasi plug-in, la regola del pollice è di utilizzare:

* `data-*` attributi per le opzioni relative al layout HTML. Ad esempio, per specificare il numero di colonne
* Opzioni/classi API per funzionalità correlate ai dati. Ad esempio, creazione dell&#39;elenco di elementi da visualizzare

Lo stesso concetto viene utilizzato per implementare la convalida del modulo. Per un elemento da convalidare, è necessario specificare il modulo di input richiesto come `data-*` attributo personalizzato. Questo attributo viene quindi utilizzato come opzione per un plug-in di convalida.

>[!NOTE]
>
>La convalida del modulo nativo per HTML5 deve essere utilizzata ogni volta che è possibile e/o estesa.

Scopo:

* Fornire un comportamento dinamico per gli elementi HTML
* Non è possibile fornire layout personalizzati con CSS puro
* Eseguire la convalida del modulo
* Esegui manipolazione DOM avanzata

Implementazione:

* Plug-in jQuery, associato a specifici elementi DOM
* Utilizzo di `data-*` attributi per personalizzare il comportamento

Un estratto del codice di esempio (notare le opzioni specificate come attributi data-*):

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

La chiamata al plug-in jQuery:

```
$(‘.cards’).cardlayout ();
```

Verrà visualizzato come:

![chlimage_1-86](assets/chlimage_1-86.png)

Il `cardLayout` plug-in riproduce gli elementi inclusi `UL` in base alle rispettive altezze e tenendo conto anche della larghezza del padre.

### Widget per elementi HTML {#html-elements-widgets}

Un widget combina uno o più elementi di base con un plug-in javascript per creare elementi dell’interfaccia utente di livello superiore. Questi possono implementare un comportamento più complesso e anche un aspetto e un aspetto più complessi di quanto un singolo elemento possa offrire. Esempi validi sono il selettore di tag o i widget della barra.

Un widget può attivare e ascoltare eventi personalizzati per collaborare con altri widget sulla pagina. Alcuni widget sono in realtà widget jQuery nativi che utilizzano gli elementi HTML Coral.

Scopo:

* Implementare elementi dell&#39;interfaccia utente di livello superiore che mostrano un comportamento complesso
* Attivazione e gestione degli eventi

Implementazione:

* plugin jQuery + markup HTML
* Può utilizzare modelli lato client/server

Esempio di markup:

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

La chiamata al plug-in jQuery (con opzioni):

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

Il plug-in emette tag HTML (questa marcatura utilizza elementi di base, che possono utilizzare altri plug-in internamente):

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

Verrà visualizzato come:

![chlimage_1-87](assets/chlimage_1-87.png)

### Libreria di utilità {#utility-library}

Questa libreria è una raccolta di plug-in e/o funzioni helper JavaScript:

* Interfaccia indipendente
* Tuttavia, è fondamentale creare applicazioni Web complete

Questi includono la gestione XSS e il bus dell&#39;evento.

Sebbene i plug-in e i widget degli elementi HTML possano basarsi sulle funzionalità fornite dalla libreria dell&#39;utilità, la libreria dell&#39;utilità non può avere alcuna dipendenza dagli elementi o dai widget stessi.

Scopo:

* Fornire funzionalità comuni
* Implementazione bus evento
* Modelli lato client
* XSS

Implementazione:

* Plug-in jQuery o moduli JavaScript conformi con AMD
