---
title: Creazione di stili CSS per i moduli HTML5
description: Scopri come modificare l’aspetto dei moduli HTML5 modificando la classe CSS associata all’elemento modulo HTML.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms,Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 2%

---

# Creazione di stili CSS per i moduli HTML5 {#creating-css-styles-for-html-forms}

La rappresentazione HTML5 di un modello di modulo basato su XFA è costituita da diversi elementi HTML. Questi elementi sono disposti in ordine. Ogni elemento dispone di classi CSS ben definite. È possibile utilizzare queste classi CSS per selezionare e modificare l&#39;aspetto di un elemento.

>[!NOTE]
>
>Nelle classi CSS, non modificare il valore degli attributi width, height, border-thickness, top, left, right, bottom, padding, margin e altri attributi di posizione e dimensione. Qualsiasi modifica negli attributi di posizione e dimensione determina modifiche al layout del modulo.

## Classi CSS  per gli elementi  {#css-classes-nbsp-for-elements-nbsp}

Ogni elemento contiene classi CSS ben definite. È possibile modificare queste classi per modificare l&#39;aspetto di un elemento. Ogni elemento, ad eccezione degli elementi field e draw, dispone di due classi CSS: la classe Type e la classe Name.

* La **classe Type** rappresenta il tipo del campo XFA. È possibile sovrascrivere la classe `type` per modificare gli stili di tutti gli elementi di un determinato tipo.

* La **classe nome** corrisponde al nome del campo XFA. È possibile sovrascrivere la classe `name` per modificare e applicare uno stile personalizzato a un elemento.

>[!NOTE]
>
>Alcuni elementi XFA non hanno un nome. Per modificare gli stili di tali componenti, modificate tutti i componenti di quel particolare tipo.

Per le pagine non denominate in AEM Forms Designer, le pagine di un modulo HTML 5 vengono denominate in ordine crescente di numero. Nel caso di un modulo di HTML5 con due pagine, ad esempio, le pagine vengono denominate Pagina1, Pagina2.

## Elemento campo {#field-element}

L’elemento field contiene due elementi nidificati: widget e didascalia.

**Elemento widget**

L’elemento widget contiene l’elemento dell’interfaccia utente per l’interazione con gli utenti. Dispone di tre classi CSS:

* **Widget**: ogni widget ha questa classe.
* **name**: tutti i widget forniti con AEM contengono la classe nome widget. Per i widget personalizzati, lo sviluppatore fornisce la classe Nome widget.
* **tipo**: ogni widget ha un elemento dell&#39;interfaccia utente. Questa classe definisce il tipo dell’elemento dell’interfaccia utente.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Oltre alla classe type e name, il componente field contiene anche una classe CSS aggiuntiva denominata **subtype**. Un sottotipo identifica il tipo di campo, ad esempio NumericField, DateField, TextField. È possibile sovrascrivere la classe del sottotipo per modificare lo stile di tutti i campi di tipo, sottotipo.

## Classi CSS per componenti diversi {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome</strong></td>
  </tr>
  <tr>
   <td>Pagina</td>
   <td>pagina</td>
   <td>Nome definito dall'utente<br /> o<br /> Pagina&lt;numeroPagina&gt; (impostazione predefinita)</td>
  </tr>
  <tr>
   <td>Area contenuto</td>
   <td>contentarea</td>
   <td>Nome definito dall'utente</td>
  </tr>
  <tr>
   <td>Sottomodulo</td>
   <td>sottomodulo</td>
   <td>Nome definito dall'utente</td>
  </tr>
  <tr>
   <td>Gruppo di esclusione</td>
   <td>exclgroup</td>
   <td>Nome definito dall'utente</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>disegnare</td>
   <td>Nome definito dall'utente</td>
  </tr>
  <tr>
   <td>Campo</td>
   <td>campo</td>
   <td>Nome definito dall'utente</td>
  </tr>
  <tr>
   <td>Sottotitoli descrittivi</td>
   <td>didascalia</td>
   <td>ND</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>Lo sviluppatore del widget lo definisce (per i widget definiti dall'utente, vedere la tabella nella sezione seguente)</td>
  </tr>
 </tbody>
</table>

## Classi CSS per campi diversi {#css-classes-for-different-fields}

AEM Forms Designer supporta diversi tipi di campi in un modulo, ad esempio NumericField, DecimalField e DateField. Tutti questi campi in HTML contengono le classi CSS sopra menzionate. Contengono anche alcune classi aggiuntive a seconda del tipo di campo.

A ogni campo è associato un widget che rappresenta l’elemento dell’interfaccia utente. Di seguito sono elencate le classi di ciascun campo e i widget associati a ciascun campo.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo di campo</strong></td>
   <td><strong>Sottotipo</strong></td>
   <td><strong>Nome widget</strong></td>
   <td><strong>Tipo widget</strong></td>
   <td><strong>Tag interfaccia utente HTML</strong></td>
  </tr>
  <tr>
   <td>Pulsante<br type="_moz" /> </td>
   <td>ND</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkbox<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkbox fieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>campo di testo<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoDecimale<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>elenco scelte<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>seleziona</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>elenco scelte<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>CampoNumerico<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoPassword<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>campo radioattivo<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoTesto<br type="_moz" /> </td>
   <td>campo di testo<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CampoOra<br type="_moz" /> </td>
   <td>campo di testo<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classi CSS per diversi elementi di Draw {#css-classes-for-different-draw-elements}

È possibile inserire elementi di disegno statici come testo e immagini utilizzando AEM Forms Designer. Per ogni elemento di disegno, a tale elemento è associata una classe CSS separata. L’elenco delle classi CSS per gli elementi disegno è elencato di seguito. A ogni elemento di disegno è associata una classe di disegno.

| **Tipo Draw** | **Classe CSS** |
|---|---|
| Testo | text |
| Immagine | immagine |
| Rettangolo | rettangolo |
| Linea | linea |

## Applicazione di stili ad altre parti del modulo {#styling-other-parts-of-the-form}

Oltre all’aspetto dei componenti dell’interfaccia utente nel modulo HTML, puoi modificare lo stile di elementi come Errori in linea, Avvisi in linea e campi con errori di convalida.

`Styling Inline Errors`

Quando la convalida di un campo genera un errore, quando il campo è attivo viene visualizzato un errore in linea. Per modificare lo stile degli errori in linea, ignora l&#39;ID CSS **error-msg**.

`Styling Inline Warnings`

Quando la convalida di un campo genera un avviso, quando il campo è attivo viene visualizzato un avviso in linea. Per modificare lo stile di questi avvisi in linea, ignora l&#39;ID CSS **warning-msg**.

`Styling Fields with Validation Errors`

Quando la convalida di un campo non riesce, lo stile del widget cambia. Questa modifica di stile viene eseguita applicando una classe CSS **widgetError** al componente widget. Per modificare lo stile predefinito, sostituire la classe **widgetError**.
