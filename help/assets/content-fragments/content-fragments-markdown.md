---
title: Markdown
description: Scopri in che modo l’editor Frammento di contenuto utilizza la sintassi markdown per consentire di creare facilmente contenuti headless.
feature: Content Fragments
role: User
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# Markdown {#markdown}

Quando sei [autore](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content), l’editor dei frammenti di contenuto utilizza la sintassi *markdown* per consentire di scrivere facilmente contenuti headless:

![editor markdown](/help/assets/content-fragments/assets/cfm-markdown-01.png)

Puoi definire:

* [Notazione titolo](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Paragrafi e interruzioni di riga](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Collegamenti](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Immagini](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Virgolette a blocchi](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Elenchi](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Enfasi](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocchi di codice](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Backslash escape](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notazione titolo {#heading-notation}

Per creare un’intestazione inserendo un tag hash (#) davanti all’intestazione. Un tag hash (#) viene utilizzato per un valore H1, due tag hash (##) per un valore H2, ecc. Puoi utilizzare fino a 6 hashtag. Esempio:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Facoltativamente, è possibile creare un H1 evidenziando il testo in segni uguali e creando un H2 evidenziando il testo sotto i segni meno. Esempio:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Paragrafi e interruzioni di riga {#paragraphs-and-line-breaks}

Un paragrafo è costituito semplicemente da una o più righe di testo consecutive, separate da una o più righe vuote. Una riga vuota è una riga contenente solo spazi o tabulazioni. I paragrafi normali non devono presentare un rientro con spazi o tabulazioni.

Un’interruzione di riga viene creata terminando una riga con due o più spazi e quindi un ritorno.

## Collegamenti {#links}

Puoi creare collegamenti in linea e di riferimento.

In entrambi gli stili, il testo del collegamento è delimitato da parentesi quadre `[]`.

Di seguito sono riportati alcuni esempi di collegamenti in linea:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Un collegamento di riferimento ha la seguente sintassi:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Immagini {#images}

La sintassi per le immagini è simile a quella dei collegamenti. Puoi creare immagini in linea e a cui fare riferimento.

Ad esempio, un&#39;immagine in linea ha la seguente sintassi:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

La sintassi include:

* Punto esclamativo: !;
* seguita da un set di parentesi quadre, contenente il testo dell’attributo alt per l’immagine;
* seguita da un set di parentesi, contenente l’URL o il percorso dell’immagine, e da un attributo titolo facoltativo racchiuso tra virgolette doppie o singole.

Un’immagine in stile Riferimento ha la seguente sintassi:

    `![Alt text][id]`

Dove &quot;id&quot; è il nome di un riferimento immagine definito. I riferimenti alle immagini sono definiti utilizzando una sintassi identica ai riferimenti di collegamento:

    `[id]: url/to/image "Optional title attribute"`

## Virgolette a blocchi {#block-quotes}

È possibile citare il testo aggiungendo il simbolo > prima del testo. Esempio:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

È possibile disporre di virgolette di blocco nidificate. Esempio:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Elenchi {#lists}

È possibile creare elenchi ordinati e non ordinati.

Per creare un elenco non ordinato, utilizzare &amp;ast; prima degli elementi dell’elenco. Esempio:

    `* item in list`

    `* item in list`

    `* item in list`

Per creare un elenco ordinato, aggiungere i numeri, seguiti da un punto, prima di ogni elemento dell’elenco. Esempio:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Enfasi {#emphasis}

È possibile aggiungere al testo uno stile corsivo o grassetto.

Per aggiungere il corsivo, procedere come segue:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Il testo in grassetto può essere visualizzato come segue:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Per indicare un intervallo di codice, inseriscilo con virgolette di backtick (&amp;grave;). A differenza di un blocco di codice preformattato, un intervallo di codice indica il codice all’interno di un paragrafo normale.

Esempio:

    ``Use the `printf()` function.``

## Blocchi di codice {#code-blocks}

I blocchi di codice vengono generalmente utilizzati per illustrare il codice sorgente. Puoi creare blocchi di codice applicando un rientro al codice utilizzando una scheda o un minimo di 4 spazi. Esempio:

    `This is a normal paragraph.`

        `This is a code block.`

## Backslash escape {#backslash-escapes}

È possibile utilizzare gli escape barra rovesciata per generare caratteri letterali che hanno un significato speciale nella sintassi di formattazione. Ad esempio, se desideri circondare una parola con asterischi letterali (invece di un tag HTML &lt;em> ), puoi utilizzare le barre rovesciate prima degli asterischi, come segue:

    `\\*literal asterisks\\*`

Gli escape delle barre rovesciate sono disponibili per i seguenti caratteri:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
