---
title: Stile in linea dei componenti per moduli adattivi
seo-title: Proprietà CSS in linea per componenti modulo adattivi
description: Sebbene sia possibile applicare stili personalizzati a un modulo adattivo, è anche possibile applicare proprietà CSS in linea ai singoli componenti di un modulo adattivo.
seo-description: Sebbene sia possibile applicare stili personalizzati a un modulo adattivo, è anche possibile applicare proprietà CSS in linea ai singoli componenti di un modulo adattivo.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Stile in linea dei componenti per modulo adattivo {#inline-styling-of-adaptive-form-components}

È possibile definire l&#39;aspetto e lo stile generali di un modulo adattivo specificando gli stili utilizzando l&#39;editor di temi [editor di temi](../../forms/using/themes.md). Inoltre, potete applicare stili CSS in linea a singoli componenti di moduli adattivi e visualizzare rapidamente l&#39;anteprima delle modifiche. Gli stili in linea sostituiscono lo stile fornito nel tema.

## Applica proprietà CSS in linea {#apply-inline-css-properties}

Per aggiungere stili in linea a un componente:

1. Aprire il modulo nell&#39;editor del modulo e passare alla modalità di stile. Per modificare la modalità di formattazione, nella barra degli strumenti della pagina, toccate ![canvas-drop-down](assets/canvas-drop-down.png) > **Style**.
1. Selezionate un componente nella pagina e toccate il pulsante di modifica ![pulsante di modifica](assets/edit-button.png). Le proprietà di stile vengono aperte nella barra laterale.

   È inoltre possibile selezionare componenti dalla struttura gerarchica del modulo nella barra laterale. La struttura gerarchica del modulo è disponibile come oggetti modulo nella barra laterale.

   Potete anche selezionare un componente dalla barra laterale. In modalità Stile è possibile visualizzare i componenti elencati in Oggetti modulo. Tuttavia, gli oggetti modulo elencati nella barra laterale elencano componenti quali campi e pannelli. I campi e i pannelli sono componenti generici che possono contenere componenti quali caselle di testo e pulsanti di scelta.

   Quando selezionate un componente dalla barra laterale, vengono elencati tutti i componenti secondari e le proprietà del componente selezionato. È possibile selezionare uno specifico sottocomponente e formattarlo.

1. Fate clic su una scheda nella barra laterale per specificare le proprietà CSS. È possibile specificare proprietà quali:

   * Dimension e posizione (impostazione visualizzazione, spaziatura, altezza, larghezza, margine, posizione, indice z, float, cancellazione, overflow)
   * Testo (famiglia di font, spessore, colore, dimensione, altezza e allineamento)
   * Sfondo (immagine e sfumatura, colore di sfondo)
   * Bordo (larghezza, stile, colore, raggio)
   * Effetti (Ombra, Opacità)
   * Avanzate (consente di scrivere CSS personalizzato per il componente)

1. Allo stesso modo, potete applicare stili ad altre parti di un componente, ad esempio Widget, Didascalia e Aiuto.
1. Toccate **Fine** per confermare le modifiche oppure **Annulla** per annullare le modifiche.

## Esempio: stili in linea per un componente campo {#example-inline-styles-for-a-field-component}

Le immagini seguenti rappresentano un campo di testo prima e dopo l’applicazione degli stili in linea.

![Componente casella di testo prima dell&#39;applicazione dello stile in linea](assets/no-style.png)

Componente casella di testo prima dell&#39;applicazione delle proprietà di stile in linea

Osservate la modifica nello stile della casella di testo come illustrato nell&#39;immagine seguente dopo l&#39;applicazione delle seguenti proprietà CSS.

<table>
 <tbody>
  <tr>
   <td><p>Selettore</p> </td>
   <td><p>Proprietà CSS</p> </td>
   <td><p>Valore</p> </td>
   <td><p>Effetto</p> </td>
  </tr>
  <tr>
   <td><p>Campo</p> </td>
   <td><p>border</p> </td>
   <td><p>Larghezza bordo = 2px</p> <p>Stile bordo=Uniforme</p> <p>Colore del bordo=#1111</p> </td>
   <td><p>Crea un bordo largo 2 px nero intorno al campo.</p> </td>
  </tr>
  <tr>
   <td><p>Casella di testo</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia il colore di sfondo in CornflowerBlue (#6495ED)</p> <p>Nota: È possibile specificare un nome di colore o il relativo codice esadecimale nel campo del valore.</p> </td>
  </tr>
  <tr>
   <td><p>Etichetta</p> </td>
   <td><p>Dimensioni e posizione &gt; larghezza</p> </td>
   <td><p>100 px</p> </td>
   <td><p>Corregge la larghezza di 100 px per l'etichetta</p> </td>
  </tr>
  <tr>
   <td>Icona guida campo</td>
   <td>Testo &gt; Colore font</td>
   <td>#2ECC40</td>
   <td>Cambia il colore della faccia dell’icona Aiuto.</td>
  </tr>
  <tr>
   <td><p>Descrizione lunga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Allinea la descrizione lunga per l’Aiuto al centro</p> </td>
  </tr>
 </tbody>
</table>

![Stile casella di testo dopo l&#39;applicazione dello stile in linea](assets/applied-style.png)

Componente casella di testo dopo l&#39;applicazione delle proprietà di stile in linea

Seguendo i passaggi descritti qui sopra, è possibile selezionare e formattare altri componenti, ad esempio pannelli, pulsanti di invio e pulsanti di scelta.

>[!NOTE]
>
>Le proprietà di stile variano in base al componente selezionato.

