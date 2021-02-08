---
title: Markdown
seo-title: Markdown
description: Durante la fase di creazione, l'editor dei frammenti di contenuto utilizza la sintassi di marketing per consentire di scrivere facilmente il contenuto.
seo-description: Durante la fase di creazione, l'editor dei frammenti di contenuto utilizza la sintassi di marketing per consentire di scrivere facilmente il contenuto.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
translation-type: tm+mt
source-git-commit: 08bf8f42898446f2e5cca1fde55ceb84710a1e30
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 4%

---


# Markdown{#markdown}

Quando si crea [authoring](content-fragments-variations.md#authoring-your-content), l&#39;editor di frammenti di contenuto utilizza la sintassi *markdown* per consentire di scrivere facilmente i contenuti:

![editor marketing](/help/assets/content-fragments/assets/cfm-6420-08.png)

È possibile definire:

* [Notazione titolo](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Paragrafi e interruzioni di riga](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Collegamenti](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Immagini](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Virgolette a blocchi](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Elenchi](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Enfasi](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocchi di codice](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Backslash](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notazione titolo {#heading-notation}

Per creare un&#39;intestazione, posizionate un tag hash (#) davanti all&#39;intestazione. Un tag hash (#) viene usato per un H1, due tag hash (##) per un H2 e così via. È possibile utilizzare fino a 6 hashtag. Esempio:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Facoltativamente, potete creare un H1 evidenziando il testo in segni uguali e creando un H2 evidenziando il testo con segni meno. Esempio:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Paragrafi e interruzioni di riga {#paragraphs-and-line-breaks}

Un paragrafo è costituito semplicemente da una o più righe di testo consecutive, separate da una o più righe vuote. Una linea vuota è una linea che non contiene altro che spazi o tabulazioni. I paragrafi normali non devono essere rientrati con spazi o tabulazioni.

Un&#39;interruzione di riga viene creata terminando una linea con due o più spazi e quindi un ritorno.

## Collegamenti {#links}

Potete creare collegamenti in linea e collegamenti di riferimento.

In entrambi gli stili, il testo del collegamento è delimitato da parentesi quadre `[]`.

Di seguito sono riportati alcuni esempi di collegamenti in linea:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Un collegamento di riferimento ha la sintassi seguente:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Immagini {#images}

La sintassi delle immagini è simile a quella dei collegamenti. Potete creare immagini in linea e di riferimento.

Ad esempio, un&#39;immagine in linea ha la sintassi seguente:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

La sintassi include:

* Un punto esclamativo: !;
* seguita da un set di parentesi quadre, contenente il testo dell’attributo alt per l’immagine;
* seguita da una serie di parentesi, contenente l’URL o il percorso dell’immagine, e da un attributo titolo facoltativo racchiuso tra virgolette singole o doppie.

Un’immagine in stile Riferimento ha la sintassi seguente:

    `![Alt text][id]`

Dove &quot;id&quot; è il nome di un riferimento immagine definito. I riferimenti alle immagini sono definiti utilizzando una sintassi identica ai riferimenti ai collegamenti:

    `[id]: url/to/image "Optional title attribute"`

## Virgolette a blocchi {#block-quotes}

Potete citare il testo aggiungendo il simbolo > prima del testo. Esempio:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

È possibile inserire virgolette di blocco nidificate. Esempio:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Elenchi {#lists}

Potete creare elenchi ordinati e non ordinati.

Per creare un elenco non ordinato, utilizzare &amp;ast; prima degli elementi dell&#39;elenco. Esempio:

    `* item in list`

    `* item in list`

    `* item in list`

Per creare un elenco ordinato, aggiungere i numeri, seguiti da un punto, prima di ogni elemento dell&#39;elenco. Esempio:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Enfasi {#emphasis}

Potete aggiungere al testo uno stile corsivo o grassetto.

Per aggiungere il corsivo, procedere come segue:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Potete applicare il grassetto al testo nel modo seguente:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Per indicare un&#39;estensione di codice, racchiudetela con virgolette (`). A differenza di un blocco di codice preformattato, un&#39;estensione di codice indica il codice all&#39;interno di un normale paragrafo.

Esempio:

    ``Use the `printf()` function.``

## Blocchi di codice {#code-blocks}

I blocchi di codice vengono generalmente utilizzati per illustrare il codice sorgente. È possibile creare blocchi di codice applicando un rientro al codice utilizzando una scheda o almeno 4 spazi. Esempio:

    `This is a normal paragraph.`

        `This is a code block.`

## Backslash escape {#backslash-escapes}

È possibile utilizzare gli escape barra rovesciata per generare caratteri letterali con un significato speciale nella sintassi di formattazione. Ad esempio, se desiderate racchiudere una parola con asterischi letterali (invece di un tag HTML &lt;em>), potete utilizzare le barre rovesciate prima degli asterischi, come segue:

    `\\*literal asterisks\\*`

Gli escape barra rovesciata sono disponibili per i seguenti caratteri:

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

