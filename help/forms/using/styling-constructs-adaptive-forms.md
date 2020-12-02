---
title: Stili di costruzione per i moduli adattivi
seo-title: Stili di costruzione per i moduli adattivi
description: Utilizzare il framework LESS per personalizzare l'aspetto dei moduli adattivi.
seo-description: Utilizzare il framework LESS per personalizzare l'aspetto dei moduli adattivi.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 3%

---


# Costruttori di stile per moduli adattivi{#styling-constructs-for-adaptive-forms}

## Prerequisiti {#prerequisites}

Conoscenza dei CSS e del framework LESS.

## Cosa è possibile personalizzare {#what-can-be-customized}

L&#39;articolo elenca le classi css dei moduli adattivi disponibili al pubblico. È possibile utilizzare queste classi per definire lo stile di vari componenti di un modulo adattivo. Lo stile dei componenti di authoring, ad esempio finestre di dialogo e barre di stato contenenti avvisi, non rientra nell’ambito di questo articolo. Utilizzate questi costrutti di stile per creare stili (utilizzando CSS o Less) solo quando non è possibile creare stili di componenti utilizzando l&#39;editor di temi [editor di temi](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## Personalizzazione degli stili nei moduli adattivi {#customizing-styles-in-adaptive-forms}

Il framework LESS semplifica l&#39;uso di maiuscole e minuscole per personalizzare gli stili nei moduli adattivi. Il framework consente di definire gli stili mediante un set di variabili e funzioni (mixin). Il framework LESS consente di ridurre le dimensioni del codice bundle e di aumentarne la riutilizzabilità.

È possibile personalizzare gli stili di modulo adattivi nei seguenti modi:

* Modificare il tema
* Modificare lo stile del componente

## Modifica del tema {#changing-theme}

È possibile modificare il tema di un modulo adattivo per assicurare che l&#39;aspetto sia coerente con le pagine Web in cui il modulo adattivo è incorporato.

Le modifiche nell&#39;aspetto generale del modulo adattivo che utilizzano le proprietà CSS in genere fanno parte di modifiche ai temi. Le modifiche principali allo &quot;ok&quot; e al funzionamento del modulo adattivo, come le modifiche nel layout e nella posizione dei componenti, non sono considerate modifiche ai temi.

In base al programma di avvio, il seguente set di proprietà CSS definisce il tema di una pagina Web:

* Colore sfondo
* Bordo (tipo, colore, spessore)
* Colore font
* Riempimento
* immagine
* Dimensione font
* LineHeight

Attualmente, le variabili LESS sono definite solo per queste proprietà dei vari elementi di un modulo adattivo.

## Modifica dello stile del componente {#changing-component-style}

Potete apportare modifiche all’aspetto, al layout, al posizionamento e alla visibilità degli elementi. Per eseguire questa operazione, create o aggiornate i file .css personalizzati in modo da includere i costrutti di stile elencati in questo articolo.

Per applicare uno stile a un modulo adattivo, aprire il modulo adattivo in per la modifica, aprire le proprietà del contenitore di modulo adattivo, specificare il percorso del file CSS personalizzato nella scheda di base. I costrutti di stile predefiniti del modulo adattivo vengono sostituiti con i costrutti elencati nel file .css personalizzato.

## Componenti {#components}

I componenti descritti in questo articolo dispongono di classi CSS predefinite. È possibile modificare le variabili per modificare gli stili nelle classi CSS. In alternativa, è possibile riscrivere l&#39;intera classe. Questa sezione descrive le classi all&#39;interno di componenti e stili che è possibile modificare utilizzando le variabili.

## Stile contenitore {#container-styling}

Un contenitore è il componente di primo livello. Altri pannelli e campi si trovano sotto il componente contenitore.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Descrizione variabili</strong></p> </td>
   <td><p><strong>Descrizione variabili</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>Colore di sfondo del contenitore</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>Spaziatura per il contenitore</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>Margine per il contenitore</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>Colore font per il contenitore</p> </td>
  </tr>
 </tbody>
</table>

## Stile del campo {#field-styling}

I moduli adattivi includono vari tipi di campi. Ogni campo ha un nome di classe univoco, che è il nome del campo. Il campo ha anche un nome di classe comune `guideFieldNode`.

I campi includono etichette, widget, descrizione dell’Aiuto (descrizione lunga e breve) e icone della Guida dei campi (punto interrogativo).

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>Spaziatura per il campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>Colore del font del messaggio di errore del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>Dimensione del font del messaggio di errore del campo</p> </td>
  </tr>
 </tbody>
</table>

## Stile etichetta {#label-styling}

L&#39;elemento HTML **label** utilizzato per il campo include le classi **left** o **top** a seconda che l&#39;etichetta sia in alto o in basso a sinistra.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>Colore del font per l'etichetta del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>Dimensione del font per l'etichetta del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>Proprietà di altezza riga CSS per l'etichetta del campo </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>Proprietà spessore font CSS per l'etichetta del campo </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Margine per l'etichetta del campo</p> </td>
  </tr>
 </tbody>
</table>

Le regole CSS per l&#39;etichetta vengono applicate utilizzando l&#39;etichetta **guideFieldLabel**. Se siete un autore, ignorate questa regola per rendere visibili le modifiche personalizzate.

## Stile dei widget {#widgets-styling}

A seconda del tipo, i widget includono anche classi. Comunemente, i widget includono la classe `guideFieldWidget`. I widget forniti con HTML normalmente utilizzano l&#39;input standard dell&#39;elemento HTML e selezionano. Lo stile viene applicato di conseguenza. Non è possibile formattare un widget personalizzato modificando le variabili.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili <code></code></strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>Colore di sfondo per i widget (Non funziona per le caselle di controllo e i pulsanti di scelta)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Colore del bordo per i widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Dimensione del bordo per i widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Raggio del bordo per i widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Tipo di bordo per i widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Tipo di messa a fuoco per i bordi dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Stile bordo consolidato dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>Colore del testo all’interno del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Dimensione del testo all’interno del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Proprietà lineheight CSS per il widget </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Proprietà di spaziatura CSS per il widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Colore del bordo quando il widget è attivo</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>Colore del bordo del widget per i campi obbligatori</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>Colore di sfondo del widget per i campi obbligatori</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>Colore di sfondo per il widget quando il campo è disattivato</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>Colore del font per il widget quando il campo è disabilitato</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>Colore del bordo del widget quando il campo è disattivato</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Altezza del widget (non funziona per casella di controllo e pulsante di scelta)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Altezza per la casella di controllo e il pulsante di scelta.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Altezza massima per un menu a discesa con più selezioni</p> </td>
  </tr>
 </tbody>
</table>

### Limitazioni nello stile del widget {#limitations-in-widget-styling}

Lo stile per i campi attivi, obbligatori e disattivati è limitato utilizzando le variabili. Tuttavia, potete modificarlo ignorando gli stili. L&#39;utilizzo di variabili è limitato principalmente per mantenere sotto controllo il numero di variabili. La limitazione può essere attenuata se l&#39;aspetto di un campo cambia drasticamente perché si trova in uno degli stati discussi in precedenza.

## Descrizione della Guida {#help-description}

Un autore può specificare il contenuto della Guida nei campi utilizzando i componenti Descrizione breve e lungo. Entrambi i componenti hanno una classe comune `.guideHelpDescription` e un&#39;altra classe `.long`/ `.short`, a seconda del tipo di descrizione. Il contenuto della Guida è racchiuso in un elemento paragrafo per sostituire lo stile della descrizione. La descrizione della Guida (lunga e breve) viene modificata utilizzando variabili che iniziano con widgetshelp, come indicato nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Colore di sfondo della Guida lunga dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Colore del bordo della Guida lunga dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Colore del bordo dell'indicatore sinistro della Guida lunga dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Colore di sfondo della breve Guida dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Colore dei font della breve Guida dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Colore di sfondo della breve descrizione dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Colore dei font della breve descrizione comandi dei widget</p> </td>
  </tr>
 </tbody>
</table>

## Condizioni d’uso {#terms-and-conditions}

Il widget Condizioni generali (TnC `` ``) consente di specificare termini e condizioni. Potete personalizzare il widget utilizzando le variabili descritte nella tabella seguente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>Colore del font del collegamento tnc non visitato.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>Colore del font del collegamento tnc visitato.</td>
  </tr>
 </tbody>
</table>

## Pulsante {#button}

I pulsanti sono anche widget. Tuttavia, il loro stile è leggermente diverso dai widget. Nei moduli adattivi, uno dei seguenti è un pulsante:

* input[type = text]
* pulsante
* element with class .button

Codice HTML per il pulsante:

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>Fornisce icone per il pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>Etichetta/didascalia pulsante Stili</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili <code></code></strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>Dimensione del bordo dei pulsanti</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>Tipo bordo</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>Proprietà di spaziatura CSS per il pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>Dimensione del font per il pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>Colore di sfondo per il pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>Colore del font del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>Colore del bordo del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>Spaziatura per i pulsanti grandi (pulsanti con classe .buttonlarge)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>Dimensione del font per i pulsanti di grandi dimensioni</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>Spaziatura per i pulsanti piccoli (pulsanti con classe .buttonsmall)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>Dimensione del font per i pulsanti di piccole dimensioni</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti informativi (pulsanti con classe .buttoninformative)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>Colore font per i pulsanti informativi</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>Colore del bordo per i pulsanti informativi</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti con lo stile dell'avviso (pulsanti con la classe .buttonwarning)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>Colore font per i pulsanti con lo stile dell'avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>Colore del bordo per i pulsanti con lo stile dell'avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti di avviso (pulsanti con classe .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Colore font per i pulsanti di avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Colore del bordo per i pulsanti di avviso</p> </td>
  </tr>
 </tbody>
</table>

## Punto interrogativo {#question-mark}

Per i widget, viene visualizzato un punto interrogativo quando un autore aggiunge una lunga descrizione al contenuto della Guida. Viene utilizzata l&#39;icona predefinita fornita in bootstrap. Per utilizzare un&#39;icona personalizzata, potete personalizzare le icone di avvio.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>Colore dell'icona</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>Colore dell’icona quando il mouse vi si trova sopra</p> </td>
  </tr>
 </tbody>
</table>

## Tabella {#table}

È possibile modificare il tema colore per le righe di intestazione e corpo di una tabella utilizzando le seguenti variabili.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la riga di intestazione. Il valore predefinito è <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la riga corpo dispari. Il valore predefinito è <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la riga corpo pari. Il valore predefinito è <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## Allegato file {#file-attachment}

Il widget Allegato file dei moduli adattivi consente di caricare i file. Potete inoltre personalizzare il widget utilizzando le variabili.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Spaziatura per i file visualizzati nel widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>Colore di sfondo per l’elemento del file</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Colore del bordo per il bordo superiore</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Colore del font per l’elemento del file</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Colore dell’icona Anteprima (icona Bootstrap) nel widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Altezza del commento per l’elemento del file</p> </td>
  </tr>
 </tbody>
</table>

## Stili di navigazione {#navigator-styles}

Esistono quattro tipi di schede di navigazione. Tra queste, le schede a sinistra, in alto, nella procedura guidata e nella fisarmonica. Ogni navigatore ha una classe diversa.

<table>
 <tbody>
  <tr>
   <td><p><strong>Naviagatore</strong></p> </td>
   <td><p><strong>Classe CSS</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.Accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.Wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

Di seguito è riportato il codice HTML per l&#39;elemento del navigatore tabulazione (simile alle schede di avvio):

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

Potete modificare lo stile del navigatore utilizzando le regole CSS che selezionano gli elementi utilizzando i selettori **discendenti**. Ad esempio, per aggiungere uno stile decorativo di testo al tag di ancoraggio:

Navigatore tabulazioni in alto:

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

Inoltre, esistono classi per assegnare uno stile ai navigatori tabulazione (sia a sinistra che in alto) in base al fatto che abbiano navigatori nidificati/secondari/secondari.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navigatori tabulazione (sinistra e superiore) con navigatori nidificati/secondari/secondari</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navigatori tabulazione (sinistra e superiore) senza navigatori nidificati/secondari/secondari</p> </td>
  </tr>
 </tbody>
</table>

La classe guideNavIcon fornisce un&#39;icona predefinita ai navigatori delle schede (sia sinistro che superiore) e ai navigatori della procedura guidata.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Potete modificare l&#39;icona di un particolare navigatore fornendo una classe CSS nel pannello in fase di creazione, ad esempio &lt;CLASS_NAME>. Per l&#39;icona del navigatore è possibile aggiungere un **&lt;CLASS_NAME>_nav**.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigatori tabulazione</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Colore di sfondo per l'intero navigatore tabulazione</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>Colore del font per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la scheda al passaggio del mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Colore font per la scheda al passaggio del mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>Colore di sfondo quando il pannello è attivo</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>Colore del font quando il pannello è attivo</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>Colore di sfondo quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>Colore del font quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>Colore di sfondo quando il pannello è stato attivo una volta ma l'espressione di completamento restituisce falso </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Colore del font quando il pannello è stato attivo una volta ma l'espressione di completamento restituisce falso </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Colore del bordo della scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Dimensione del font per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Spaziatura per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Margine per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>Margine per le schede verticali</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>Dimensione del bordo per le schede</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>Altezza minima delle schede</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>Rientro delle schede nidificate</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigatori procedura guidata</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>Colore di sfondo per l'intero navigatore della procedura guidata</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>Colore font per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>Colore di sfondo quando il pannello è attivo</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>Colore del font quando il pannello è attivo (attivo)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>Colore di sfondo quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>Colore del font quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>Colore di sfondo quando il pannello è stato attivo una volta ma l'espressione di completamento restituisce falso</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Colore del font quando il pannello è stato attivato una volta ma l'espressione di completamento restituisce falso</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Colore per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Dimensione font per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>Margine per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>Dimensione del bordo per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>Colore del bordo del punto elenco dello strumento di navigazione guidato (prefisso della didascalia/etichetta)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Colore di sfondo della barra di avanzamento della procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Colore di riempimento per la barra di avanzamento</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigatori Accordion</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Spaziatura per la struttura a soffietto</p> </td>
  </tr>
 </tbody>
</table>

## Stile del pannello {#panel-styling}

Un pannello include una barra degli strumenti opzionale e il relativo contenuto.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>Colore di sfondo per il pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>Dimensione del font per il testo del pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>Colore del font per il testo del pannello<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>Margine nel pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>Dimensione del font della descrizione del pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>Spaziatura della descrizione del pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la guida del pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>Colore del bordo indicatore per la guida del pannello</p> </td>
  </tr>
 </tbody>
</table>

Il nodo del pannello è diviso in navigatori e contenuti. `` `` non esiste un componente di stile separato per il contenuto. Le variabili descritte vengono applicate sia al navigatore che al contenuto.

Il pannello superiore (RootPanel) non dispone di questa classe.

## Stile mobile {#mobile-styling}

## Barra delle intestazioni {#header-bar}

Queste variabili influenzano la barra dell’intestazione visibile su un dispositivo mobile o su dispositivi con schermo piccolo che contengono il titolo del pannello e i navigatori successivi e posteriori.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>Colore di sfondo per la barra di intestazione</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>Colore del font per il testo all’interno della barra dell’intestazione</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Spaziatura per la barra dell’intestazione</p> </td>
  </tr>
 </tbody>
</table>

## Indicatore di scorrimento {#scroll-indicator}

Queste variabili influenzano l’indicatore di scorrimento, ossia una freccia arancione che viene visualizzata su un dispositivo mobile o su un dispositivo a schermo piccolo. Un indicatore di scorrimento indica che è presente del contenuto oltre la parte visibile dello schermo. Potete scorrere verso il basso per visualizzarlo. Quando si tocca la fine del contenuto, la freccia scompare.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>Posizione fissa dello scorrevole dal basso</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>Posizione fissa dello scorrevole da destra</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>Larghezza dello scorrevole</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>Altezza dello scorrevole</p> </td>
  </tr>
 </tbody>
</table>

## Variabili del layout fisso della barra degli strumenti mobile {#mobile-fixed-toolbar-layout-specific-variables}

Queste variabili nella tabella seguente influiscono sul layout della barra degli strumenti fissa per dispositivi mobili.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>Posizione fissa della barra degli strumenti, sul dispositivo mobile, dal basso</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>Posizione fissa della barra degli strumenti, sul dispositivo mobile, dall'alto</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>Posizione fissa della barra degli strumenti, sul dispositivo mobile, da sinistra</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>Posizione fissa della barra degli strumenti, sul dispositivo mobile, da destra</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>Posizione fissa dell'icona dei pulsanti della barra degli strumenti, dall'alto</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>Larghezza dell'icona dei pulsanti della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>Altezza dell'icona dei pulsanti della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>Colore di sfondo della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
 </tbody>
</table>

## Variabile specifica per il tema {#theme-specific-variable}

Anche il tema **Iscrizione semplice** in /etc/clientlibs/fd/af/guidetema/simpleEnrollment e la categoria `guide.theme.simpleEnrollment` presentano alcune variabili. Se desiderate creare un tema per migliorare la semplice iscrizione, potete utilizzare le seguenti &quot;variabili aggiuntive:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Colore di sfondo per il pulsante attivo</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>Colore di sfondo per il pulsante al passaggio del mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>Raggio del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti di navigazione (Indietro/Avanti)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti di navigazione (Indietro/Avanti) al passaggio del mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>Colore di sfondo per i navigatori della procedura guidata e la barra di avanzamento corrispondente, al primo rendering.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>Colore di sfondo per il navigatore della procedura guidata corrente/attiva e la barra di avanzamento corrispondente </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>Colore di sfondo per i navigatori della procedura guidata e la barra di avanzamento corrispondente visitata.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Bordo bipolazione del contenitore in navigatori e pannelli</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Colore del bordo inferiore che separa le schede per le schede a sinistra (navigatori tabulazione).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Colore di sfondo per i navigatori nidificati/secondari/secondari</p> </td>
  </tr>
 </tbody>
</table>

