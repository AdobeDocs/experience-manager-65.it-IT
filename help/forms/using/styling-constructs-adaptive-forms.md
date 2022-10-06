---
title: Costruzioni di stile per i moduli adattivi
seo-title: Styling constructs for adaptive forms
description: Utilizza il framework LESS per personalizzare l’aspetto dei moduli adattivi.
seo-description: Use LESS framework to customize appearance of adaptive forms.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Adaptive Forms
exl-id: 691608a6-be82-4d81-b876-427de997e5be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 3%

---

# Costruzioni di stile per i moduli adattivi{#styling-constructs-for-adaptive-forms}

## Prerequisiti {#prerequisites}

Conoscenza del CSS e del framework LESS.

## Cosa può essere personalizzato {#what-can-be-customized}

L&#39;articolo elenca le classi css dei moduli adattivi disponibili al pubblico. È possibile sfruttare queste classi per assegnare uno stile a vari componenti di un modulo adattivo. Lo stile dei componenti di authoring, ad esempio finestre di dialogo e barre di stato contenenti avvisi, esula dall’ambito di questo articolo. Utilizzare questi costrutti di stile per creare stili (utilizzando CSS o Meno) solo quando non è possibile utilizzare i componenti di stile utilizzando [editor a tema](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## Personalizzazione degli stili nei moduli adattivi {#customizing-styles-in-adaptive-forms}

Il framework LESS semplifica il caso d’uso per personalizzare gli stili nei moduli adattivi. Il framework consente di definire gli stili utilizzando un set di variabili e funzioni (mixin). Il framework LESS aiuta a ridurre le dimensioni del codice bundle e ne aumenta la riutilizzabilità.

Puoi personalizzare gli stili dei moduli adattivi nei seguenti modi:

* Modificare il tema
* Modificare lo stile del componente

## Modifica del tema {#changing-theme}

È possibile modificare il tema di un modulo adattivo per assicurarne la coerenza con le pagine web in cui è incorporato il modulo adattivo.

Le modifiche nell’aspetto generale del modulo adattivo che utilizzano le proprietà CSS fanno generalmente parte di modifiche al tema. Le modifiche principali al &quot;ok&quot; del modulo adattivo, come le modifiche al layout e al posizionamento dei componenti, non sono considerate modifiche del tema.

In base al bootstrap, il seguente set di proprietà CSS definisce il tema di una pagina web:

* Colore sfondo
* Bordo (tipo, colore, spessore)
* Colore font
* Riempimento
* immagine
* Dimensione font
* AltezzaLinea

Attualmente, le variabili LESS sono definite solo per queste proprietà dei vari elementi in un modulo adattivo.

## Modifica dello stile del componente {#changing-component-style}

È possibile modificare l’aspetto, il layout, il posizionamento e la visibilità degli elementi. Per eseguire questa operazione, crea o aggiorna i file .css personalizzati per includere i costrutti di stile elencati in questo articolo.

Per applicare uno stile a un modulo adattivo, apri il modulo adattivo in per la modifica, apri le proprietà del contenitore di moduli adattivi, specifica il percorso del file CSS personalizzato nella scheda di base. costrutti di stile predefiniti del modulo adattivo e sostituiti con i costrutti elencati nel file .css personalizzato.

## Componenti {#components}

I componenti descritti in questo articolo hanno le loro classi CSS predefinite. Puoi modificare le variabili per modificare gli stili nelle classi CSS. In alternativa, è possibile riscrivere l&#39;intera classe. Questa sezione descrive le classi all’interno di componenti e stili che è possibile modificare utilizzando le variabili.

## Stile del contenitore {#container-styling}

Un contenitore è il componente di primo livello. Altri pannelli e campi si trovano sotto il componente contenitore .

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
   <td><p>Margine del contenitore</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>Colore font per il contenitore</p> </td>
  </tr>
 </tbody>
</table>

## Stile del campo {#field-styling}

I moduli adattivi includono vari tipi di campi. Ogni campo ha un nome di classe univoco, corrispondente al nome del campo. Il campo ha anche un nome di classe comune `guideFieldNode`.

I campi includono etichette, widget, descrizione della Guida (lunga e breve) e icone della Guida dei campi (punto interrogativo).

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
   <td><p>Colore del carattere del messaggio di errore del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>Dimensione del carattere del messaggio di errore del campo</p> </td>
  </tr>
 </tbody>
</table>

## Stile etichetta {#label-styling}

L’elemento HTML **etichetta** utilizzato per il campo include le classi **sinistra** o **top** a seconda che l’etichetta si trovi in alto o a sinistra.

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
   <td><p>Colore del font per l’etichetta del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>Dimensione del font per l’etichetta del campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>Proprietà di altezza riga CSS per l’etichetta del campo </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>Proprietà di spessore del font CSS per l’etichetta del campo </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Margine per l’etichetta del campo</p> </td>
  </tr>
 </tbody>
</table>

Le regole CSS per l’etichetta vengono applicate utilizzando il **guideFieldLabel** etichetta. Se sei un autore, sovrascrivi questa regola per rendere visibili le modifiche personalizzate.

## Stile dei Widget {#widgets-styling}

A seconda del tipo, i widget includono anche classi. Comunemente, i widget includono `guideFieldWidget` classe. I widget forniti con HTML normalmente utilizzano l’input standard dell’elemento HTML e selezionano. Lo stile viene eseguito di conseguenza. Non puoi assegnare uno stile a un widget personalizzato modificando le variabili.

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
   <td>Colore di sfondo per i widget (Non funziona per la casella di controllo e il pulsante di scelta)</td>
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
   <td><p>Colore del testo all'interno del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Dimensioni del testo all'interno del widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Proprietà CSS lineheight per il widget </td>
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
   <td><p>Colore di sfondo del widget quando il campo è disabilitato</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>Colore del carattere del widget quando il campo è disabilitato</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>Colore del bordo del widget quando il campo è disabilitato</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Altezza del widget (non funziona per le caselle di controllo e i pulsanti di scelta)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Altezza della casella di controllo e del pulsante di scelta.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Altezza massima per un menu a discesa con più selezioni</p> </td>
  </tr>
 </tbody>
</table>

### Limitazioni nello stile dei widget {#limitations-in-widget-styling}

Lo stile dei campi mirati, obbligatori e disabilitati è limitato utilizzando le variabili. Tuttavia, è possibile modificarlo ignorando gli stili. Le restrizioni che utilizzano le variabili sono fornite principalmente per mantenere il numero di variabili sotto controllo. La restrizione può essere attenuata se l&#39;aspetto di un campo cambia drasticamente perché si trova in uno degli stati discussi in precedenza.

## Descrizione dell’Aiuto {#help-description}

Un autore può specificare il contenuto della Guida nei campi utilizzando i componenti Descrizione breve e lunga. Entrambi i componenti hanno una classe comune `.guideHelpDescription` e un&#39;altra classe `.long`/ `.short`, a seconda del tipo di descrizione. Il contenuto della Guida è racchiuso in un elemento paragrafo per sostituire lo stile della descrizione. La descrizione della Guida (lunga e breve) viene modificata utilizzando le variabili che iniziano con widgetshelp, come indicato nella tabella seguente:

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
   <td><p>Colore bordo indicatore sinistro della Guida lunga dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Colore di sfondo della breve Guida dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Colore del carattere della breve Guida dei widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Colore di sfondo della breve descrizione dei widget Aiuto</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Colore del carattere della breve descrizione comandi dei widget Aiuto</p> </td>
  </tr>
 </tbody>
</table>

## Condizioni d’uso {#terms-and-conditions}

Termini e condizioni (TnC `` ``) consente di specificare termini e condizioni. Puoi personalizzare il widget utilizzando le variabili descritte nella tabella seguente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>Colore font del collegamento tnc non visitato.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>Colore font del collegamento tnc visitato.</td>
  </tr>
 </tbody>
</table>

## Pulsante {#button}

I pulsanti sono anche widget. Tuttavia, il loro stile è leggermente diverso dai widget. Nei moduli adattivi, uno dei seguenti costituisce un pulsante:

* input[type = text]
* pulsante
* elemento con classe .button

Codice HTML per il pulsante :

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
   <td><p>Dimensioni del bordo dei pulsanti</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>Tipo di bordo</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>Proprietà di spaziatura CSS per il pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>Dimensione del carattere del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>Colore di sfondo del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>Colore del carattere del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>Colore del bordo del pulsante</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>Spaziatura per i pulsanti di grandi dimensioni (pulsanti con classe .buttonlarge)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>Dimensione del carattere per i pulsanti di grandi dimensioni</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>Spaziatura per i piccoli pulsanti (pulsanti con classe .bottonsmall)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>Dimensione del carattere per i pulsanti di piccole dimensioni</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti informativi (pulsanti con classe .buttoninformative)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>Colore del carattere per i pulsanti informativi</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>Colore del bordo per i pulsanti informativi</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti con stili di avviso (pulsanti con classe .buttonwarning)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>Colore del carattere per i pulsanti con stile di avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>Colore del bordo per i pulsanti con stile avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti di avviso (pulsanti con classe .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Colore dei font per i pulsanti di avviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Colore del bordo dei pulsanti di avviso</p> </td>
  </tr>
 </tbody>
</table>

## Punto interrogativo {#question-mark}

Per i widget, viene visualizzato un punto interrogativoMark quando un autore aggiunge una lunga descrizione nel contenuto della Guida. Viene utilizzata l&#39;icona predefinita fornita in bootstrap. Per utilizzare un’icona personalizzata, puoi personalizzare le icone del bootstrap.

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
   <td><p>Colore dell’icona</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>Colore dell'icona quando il mouse passa sopra di essa</p> </td>
  </tr>
 </tbody>
</table>

## Tabella {#table}

È possibile modificare il tema del colore per le righe di intestazione e corpo di una tabella utilizzando le seguenti variabili.

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

Il widget File allegato di moduli adattivi consente di caricare file. Puoi anche personalizzare il widget utilizzando le variabili .

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
   <td><p>Colore di sfondo per l’elemento file</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Colore del bordo del bordo superiore</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Colore font per l’elemento file</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Colore dell’icona Anteprima (icona Bootstrap) nel widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Altezza del commento per l’elemento file</p> </td>
  </tr>
 </tbody>
</table>

## Stili navigazione {#navigator-styles}

Sono disponibili quattro tipi di schede di navigazione. Sono disponibili schede a sinistra, in alto, nella procedura guidata e a soffietto. Ogni navigatore ha una classe diversa.

<table>
 <tbody>
  <tr>
   <td><p><strong>Naviagatore</strong></p> </td>
   <td><p><strong>Classe CSS</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>navigatori a fisarmonica</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-verticali</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>navigatori</p> </td>
  </tr>
 </tbody>
</table>

Di seguito è riportato il codice HTML per l’elemento navigatore schede (simile alle schede bootstrap):

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

Puoi modificare lo stile del navigatore utilizzando le regole CSS che selezionano gli elementi utilizzando **discendente** selettori. Ad esempio, per aggiungere uno stile decorativo testo al tag di ancoraggio:

Navigatore a schede in alto:

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

Inoltre, esistono classi per i navigatori a schede di stile (sia a sinistra che in alto) in base al fatto che abbiano navigatori nidificati/secondari/secondari.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navigatori a schede (sinistra e superiore) con navigatori nidificati/secondari/secondari</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navigatori schede (sinistra e superiore) privi di navigatori nidificati/secondari/secondari</p> </td>
  </tr>
 </tbody>
</table>

La classe guideNavIcon fornisce un&#39;icona predefinita ai navigatori a schede (sia sinistro che superiore) e ai navigatori della procedura guidata.

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
>Puoi modificare l’icona di un particolare navigatore fornendo una classe CSS nel pannello in authoring, ad esempio &lt;class_name>. Aggiungi un **&lt;class_name>_nav** per l&#39;icona del navigatore.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigatori schede</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Colore di sfondo per l’intero navigatore schede</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>Colore font per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>Colore di sfondo per la scheda al passaggio del mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Colore del carattere per la scheda al passaggio del mouse</p> </td>
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
   <td><p>Colore di sfondo quando l’espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>Colore del carattere quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>Colore di sfondo quando il pannello è stato attivato una volta ma l'espressione di completamento restituisce falso </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Colore del carattere quando il pannello è stato attivato una volta ma l'espressione di completamento restituisce falso </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Colore del bordo della scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Dimensione del carattere della scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Spaziatura per la scheda</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Margine della scheda</p> </td>
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
   <td><p><strong>Navigatori della procedura guidata</strong></p> </td>
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
   <td><p>Colore del carattere quando il pannello è attivo (a fuoco)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>Colore di sfondo quando l’espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>Colore del carattere quando l'espressione di completamento del pannello restituisce true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>Colore di sfondo quando il pannello è stato messo a fuoco una volta ma l'espressione di completamento restituisce falso</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Colore del carattere quando il pannello è stato attivato una volta ma l'espressione di completamento restituisce falso</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Colore per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Dimensione del carattere per la procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>Aggiunta della creazione guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>Dimensioni del bordo della procedura guidata</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>Colore del bordo del punto elenco del navigatore della procedura guidata (predefinizione della didascalia/etichetta)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Colore di sfondo della barra di avanzamento del navigatore guidato</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Colore di riempimento per la barra di avanzamento</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigatori a soffietto</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Spaziatura per pannello a soffietto</p> </td>
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
   <td><p>Spaziatura all’interno del pannello</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>Dimensione del carattere della descrizione del pannello</p> </td>
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
   <td><p>Colore del bordo dell’indicatore per la guida del pannello</p> </td>
  </tr>
 </tbody>
</table>

Il nodo del pannello è diviso in navigatori e contenuti. Là `` `` non è un componente di stile separato per il contenuto. Le variabili descritte vengono applicate sia al navigatore che al contenuto.

La classe non è presente nel pannello principale (RootPanel).

## Stile mobile {#mobile-styling}

## Barra delle intestazioni {#header-bar}

Queste variabili influenzano la barra dell’intestazione visibile su un dispositivo mobile o su dispositivi a schermo piccolo che contengono il titolo del pannello e i navigatori successivi e posteriori.

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
   <td><p>Colore di sfondo per la barra dell’intestazione</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>Colore del carattere del testo all’interno della barra dell’intestazione</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Spaziatura per la barra dell’intestazione</p> </td>
  </tr>
 </tbody>
</table>

## Indicatore di scorrimento {#scroll-indicator}

Queste variabili influenzano l’indicatore di scorrimento, che è una freccia arancione visualizzata su un dispositivo mobile o su piccoli schermi. Un indicatore di scorrimento indica che il contenuto è presente oltre la parte visibile dello schermo. Puoi scorrere verso il basso per vederlo. Quando premi la fine del contenuto, la freccia scompare.

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
   <td><p>Altezza dello scrollindicatore</p> </td>
  </tr>
 </tbody>
</table>

## Variabili specifiche del layout della barra degli strumenti fissa mobile {#mobile-fixed-toolbar-layout-specific-variables}

Queste variabili nella tabella seguente influenzano il layout fisso della barra degli strumenti mobile.

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
   <td><p>Larghezza dell’icona dei pulsanti della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>Altezza dell’icona dei pulsanti della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>Colore di sfondo della barra degli strumenti sul dispositivo mobile</p> </td>
  </tr>
 </tbody>
</table>

## Variabile specifica per tema {#theme-specific-variable}

La **Registrazione semplice** Tema in /etc/clientlibs/fd/af/guidetheme/simpleEnrollment e la categoria `guide.theme.simpleEnrollment` introduce anche alcune variabili. Se si desidera creare un tema che incrementa la semplice iscrizione, è possibile utilizzare le seguenti &quot;variabili extra:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variabili </strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Colore di sfondo per pulsante attivo</p> </td>
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
   <td><p>Colore di sfondo per i pulsanti di navigazione (indietro/avanti)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Colore di sfondo per i pulsanti di navigazione (indietro/avanti) al passaggio del mouse</p> </td>
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
   <td><p>Colore di sfondo per i navigatori della procedura guidata e la barra di avanzamento corrispondente, visitati.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Contenitore biforcazione colore bordo in navigatori e pannelli</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Schede che separano i colori dei bordi inferiori delle schede a sinistra (navigatori schede).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Colore di sfondo per i navigatori nidificati/secondari/secondari del navigatore</p> </td>
  </tr>
 </tbody>
</table>
