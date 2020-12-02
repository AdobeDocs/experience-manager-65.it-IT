---
title: Creazione di stili CSS per i moduli HTML5
seo-title: Creazione di stili CSS per i moduli HTML5
description: Scoprite come modificare l'aspetto dei moduli HTML5 modificando la classe CSS associata all'elemento modulo HTML.
seo-description: Scoprite come modificare l'aspetto dei moduli HTML5 modificando la classe CSS associata all'elemento modulo HTML.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 3%

---


# Creazione di stili CSS per moduli HTML5 {#creating-css-styles-for-html-forms}

La rappresentazione HTML5 di un modello di modulo basato su XFA è costituita da diversi elementi HTML. Questi elementi sono disposti in ordine. Ogni elemento ha classi CSS ben definite. Potete utilizzare questa classe CSS per selezionare e modificare l&#39;aspetto di un elemento.

>[!NOTE]
>
>Nelle classi CSS, non modificate il valore di larghezza, altezza, spessore del bordo, in alto, a sinistra, a destra, in basso, spaziatura, margini e altri attributi di posizione e dimensione. Qualsiasi modifica negli attributi posizione e dimensione comporta modifiche al layout del modulo.

## Classi CSS  per gli elementi  {#css-classes-nbsp-for-elements-nbsp}

Ogni elemento contiene classi CSS ben definite. È possibile modificare queste classi per modificare l&#39;aspetto di un elemento. Ogni elemento, ad eccezione del campo e degli elementi di disegno, ha due classi CSS - Classe Type e Classe Name.

* La **classe Type** rappresenta il tipo del campo XFA. È possibile ignorare la classe `type` per modificare gli stili di tutti gli elementi di un particolare tipo.

* La **classe Name** corrisponde al nome del campo XFA. È possibile ignorare la classe `name` per modificare e applicare lo stile personalizzato a un elemento.

>[!NOTE]
>
>Alcuni elementi XFA non hanno un nome. Per modificare gli stili di tali componenti, modificate tutti i componenti di quel particolare tipo.

Per le pagine senza nome in  AEM Forms Designer, le pagine in un modulo HTML5 vengono denominate in ordine crescente rispetto al numero corrispondente. Ad esempio, per un modulo HTML5 con due pagine le pagine sono denominate Pagina1, Pagina2.

## Elemento del campo {#field-element}

L&#39;elemento campo contiene due elementi nidificati: widget e didascalia.

**Widget, elemento**

L&#39;elemento widget contiene l&#39;elemento dell&#39;interfaccia utente per l&#39;interazione con gli utenti. Sono disponibili tre classi CSS:

* **Widget**: Ogni widget ha questa classe.
* **name**: Tutti i widget forniti con AEM contengono la classe del nome del widget. Per i widget personalizzati, lo sviluppatore di widget fornisce la classe Widget name.
* **type**: Ogni widget ha un elemento interfaccia utente. Questa classe definisce il tipo dell&#39;elemento dell&#39;interfaccia utente.

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

Oltre alla classe tipo e nome, il componente campo contiene anche una classe CSS aggiuntiva denominata **subtype**. Un sottotipo identifica il tipo di campo, ad esempio NumericField, DateField, TextField. È possibile ignorare la classe di sottotipo per modificare lo stile di tutti i campi di tipo, sottotipo.

## Classi CSS per diversi componenti {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome</strong></td>
  </tr>
  <tr>
   <td>Pagina</td>
   <td>page</td>
   <td>Nome definito dall'utente<br /> o<br /> Page&lt;pageNumber&gt; (predefinito)</td>
  </tr>
  <tr>
   <td>Area contenuto</td>
   <td>contentarea</td>
   <td>Nome definito dall’utente</td>
  </tr>
  <tr>
   <td>Sottomodulo</td>
   <td>sottomodulo</td>
   <td>Nome definito dall’utente</td>
  </tr>
  <tr>
   <td>Gruppo di esclusione</td>
   <td>exclgroup</td>
   <td>Nome definito dall’utente</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>Nome definito dall’utente</td>
  </tr>
  <tr>
   <td>Campo</td>
   <td>o in un altro campo</td>
   <td>Nome definito dall’utente</td>
  </tr>
  <tr>
   <td>Didascalia</td>
   <td>caption</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>Lo sviluppatore di widget lo definisce (per i widget definiti dall’utente, consultate la tabella nella sezione seguente)</td>
  </tr>
 </tbody>
</table>

## Classi CSS per diversi campi {#css-classes-for-different-fields}

 AEM Forms Designer supporta diversi tipi di campi in un modulo come NumericField, DecimalField e Date Field. Tutti questi campi in HTML contengono le suddette classi CSS. Contiene inoltre alcune classi aggiuntive a seconda del tipo di campo.

A ogni campo è associato un widget che rappresenta l’elemento dell’interfaccia utente. Le classi di ciascun campo e i widget associati a ciascun campo sono elencati di seguito.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo campo</strong></td>
   <td><strong>Sottotipo</strong></td>
   <td><strong>Nome widget</strong></td>
   <td><strong>Tipo di widget</strong></td>
   <td><strong>Tag HTML UI</strong></td>
  </tr>
  <tr>
   <td>Pulsante<br type="_moz" /> </td>
   <td>NA</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>tipo di input=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>tipo di input=casella di controllo<br type="_moz" /> </td>
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
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radifield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>tipo di input=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classi CSS per diversi elementi di disegno {#css-classes-for-different-draw-elements}

È possibile inserire elementi di disegno statici come testo e immagini utilizzando  AEM Forms Designer. Per ciascun elemento draw, è associata a tale elemento una classe CSS separata. L&#39;elenco delle classi CSS per gli elementi di disegno è riportato di seguito. A ogni elemento draw è associata una classe draw.

| **Tipo di disegno** | **Classe CSS** |
|---|---|
| Testo | testo |
| Immagine | immagine |
| Rettangolo | rectangle |
| Linea | line |

## Attribuzione dello stile ad altre parti del modulo {#styling-other-parts-of-the-form}

Oltre all&#39;aspetto dei componenti dell&#39;interfaccia utente nel modulo HTML, è possibile modificare lo stile di elementi quali Errori in linea, Avvisi in linea e campi con errori di convalida.

`Styling Inline Errors`

Quando la convalida di un campo genera un errore, quando il campo è attivo viene visualizzato un errore in linea. Per modificare lo stile degli errori in linea, ignorate l&#39;ID CSS **error-msg**.

`Styling Inline Warnings`

Quando la convalida di un campo genera un avviso, quando il campo è attivo viene visualizzato un avviso in linea. Per modificare lo stile di questi avvisi in linea, ignorare l&#39;ID CSS **warning-msg**.

`Styling Fields with Validation Errors`

Quando la convalida di un campo ha esito negativo, lo stile del widget cambia. Questa modifica dello stile viene eseguita applicando una classe CSS **widgetError** sul componente widget. Per modificare lo stile predefinito, ignorate la classe **widgetError**.
