---
title: Tag di decorazione
description: Quando viene eseguito il rendering di un componente in una pagina web, è possibile generare un elemento HTML che racchiude all’interno il componente renderizzato. AEM offre agli sviluppatori una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti.
exl-id: d049ebf1-7fa6-4d2c-86f9-b18e107092ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 10%

---

# Tag di decorazione{#decoration-tag}

Quando viene eseguito il rendering di un componente in una pagina web, è possibile generare un elemento HTML che racchiude all’interno il componente renderizzato. Ciò ha principalmente due finalità:

* È possibile modificare un componente solo se è racchiuso con un elemento HTML.
* L’elemento wrapping viene utilizzato per applicare le classi HTML che forniscono:

   * informazioni sul layout
   * informazioni sullo stile

AEM offre agli sviluppatori una logica chiara e semplice che controlla i tag di decorazione che racchiudono i componenti. Se e come viene eseguito il rendering del tag di decorazione è definito dalla combinazione di due fattori, in cui questa pagina si immergerà:

* Il componente stesso può configurare il tag di decorazione con un set di proprietà.
* Gli script che includono componenti (HTL, JSP, dispatcher, ecc.) possono definire gli aspetti del tag di decorazione con parametri di inclusione.

## Consigli {#recommendations}

Di seguito sono riportati alcuni consigli generali su quando includere l’elemento wrapper che dovrebbero contribuire a evitare problemi imprevisti:

* La presenza dell’elemento wrapper non deve differire tra i WCMModes (modalità di modifica o anteprima), le istanze (authoring o pubblicazione) o l’ambiente (staging o produzione), in modo che i CSS e JavaScript della pagina funzionino in modo identico in tutti i casi.
* L’elemento wrapper deve essere aggiunto a tutti i componenti modificabili, in modo che l’editor pagina possa inizializzarli e aggiornarli correttamente.
* Per i componenti non modificabili, l’elemento wrapper può essere evitato se non svolge alcuna funzione particolare, in modo che il markup risultante non sia gonfiato inutilmente.

## Controlli dei componenti {#component-controls}

I seguenti nodi e proprietà possono essere applicati ai componenti per controllare il comportamento del tag di decorazione:

* **`cq:noDecoration {boolean}`:** Questa proprietà può essere aggiunta a un componente e un valore vero costringe AEM non generare alcun elemento wrapper sul componente.

* **`cq:htmlTag`nodo :** Questo nodo può essere aggiunto sotto un componente e può avere le seguenti proprietà:

   * **`cq:tagName {String}`:** Può essere utilizzato per specificare un tag HTML personalizzato da utilizzare per il wrapping dei componenti invece dell’elemento DIV predefinito.
   * **`class {String}`:** Può essere utilizzato per specificare i nomi delle classi css da aggiungere al wrapper.
   * Altri nomi di proprietà verranno aggiunti come attributi di HTML con lo stesso valore String fornito.

## Controlli script {#script-controls}

Il comportamento del wrapper varia tuttavia a seconda di se [HTL](/help/sites-developing/decoration-tag.md#htl) o [JSP](/help/sites-developing/decoration-tag.md#jsp) viene utilizzato per includere l’elemento .

### HTL {#htl}

In generale, il comportamento del wrapper in HTL può essere riassunto come segue:

* Per impostazione predefinita non viene eseguito il rendering di alcun wrapper DIV (solo durante l’esecuzione `data-sly-resource="foo"`).
* Tutte le modalità wcm (disabilitate, visualizzate in anteprima, modificate sia sull’autore che sulla pubblicazione) vengono eseguite il rendering in modo identico.

Il comportamento del wrapper può anche essere completamente controllato.

* Lo script HTL ha pieno controllo sul comportamento risultante del tag wrapper.
* Proprietà dei componenti (come `cq:noDecoration` e `cq:tagName`) può anche definire il tag wrapper .

È possibile controllare completamente il comportamento dei tag wrapper dagli script HTL e la logica associata.

Per ulteriori informazioni sullo sviluppo in HTL, consulta la sezione [Documentazione di HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html).

#### Albero decisionale {#decision-tree}

Questa struttura decisionale riepiloga la logica che determina il comportamento dei tag wrapper.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### Casi d&#39;uso {#use-cases}

I tre casi d’uso seguenti forniscono esempi di gestione dei tag wrapper e illustrano anche la semplicità del controllo del comportamento desiderato dei tag wrapper.

Tutti gli esempi seguenti si basano sulla seguente struttura del contenuto e componenti:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Caso d&#39;uso 1: Includi un componente per il riutilizzo del codice {#use-case-include-a-component-for-code-reuse}

Il caso d’uso più tipico si verifica quando un componente include un altro componente per motivi di riutilizzo del codice. In questo caso, il componente incluso non è modificabile con la propria barra degli strumenti e la propria finestra di dialogo, quindi non è necessario alcun wrapper e il componente è `cq:htmlTag` verranno ignorati. Questo può essere considerato il comportamento predefinito.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`Hello World!`**

Un esempio è un componente che include un componente immagine di base per visualizzare un’immagine, in genere utilizzando una risorsa sintetica, che consiste nell’includere un componente figlio virtuale passando alla risorsa sly data un oggetto Map che rappresenta tutte le proprietà del componente.

#### Caso d&#39;uso 2: Includi un componente modificabile {#use-case-include-an-editable-component}

Un altro caso d’uso comune si verifica quando i componenti contenitore includono componenti figlio modificabili, come un Contenitore di layout. In questo caso, ogni bambino incluso ha bisogno di un wrapper per il funzionamento dell&#39;editor (a meno che non sia esplicitamente disabilitato con il `cq:noDecoration` proprietà).

Poiché in questo caso il componente incluso è un componente indipendente, per il funzionamento dell’editor è necessario un elemento wrapper e per definirne il layout e lo stile da applicare. Per attivare questo comportamento, è possibile `decoration=true` opzione .

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Output risultante su `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso d&#39;uso 3: Comportamento personalizzato {#use-case-custom-behavior}

Ci può essere un certo numero di casi complessi, che possono essere facilmente raggiunti dalla possibilità di HTL di fornire esplicitamente:

* **`decorationTagName='ELEMENT_NAME'`** Per definire il nome dell’elemento del wrapper.
* **`cssClassName='CLASS_NAME'`** Per definire i nomi delle classi CSS da impostarvi.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Output risultante `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

Quando includi un componente utilizzando `cq:includ`e o `sling:include`, il comportamento predefinito in AEM consiste nell’utilizzare un DIV per racchiudere l’elemento. Tuttavia, questo avvolgimento può essere personalizzato in due modi:

* Comunicare esplicitamente AEM non avvolgere il componente utilizzando `cq:noDecoration`.
* Utilizza un tag HTML personalizzato per racchiudere il componente utilizzando `cq:htmlTag`/ `cq:tagName` o `decorationTagName`.

### Albero decisionale {#decision-tree-1}

Il seguente albero decisionale illustra come `cq:noDecoration`, `cq:htmlTag`, `cq:tagName`e `decorationTagName` influisce sul comportamento del wrapper.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
