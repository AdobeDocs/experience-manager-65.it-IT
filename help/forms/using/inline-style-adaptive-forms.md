---
title: Stile in linea dei componenti di moduli adattivi
seo-title: Inline CSS properties for adaptive form components
description: Sebbene sia possibile applicare stili personalizzati a un modulo adattivo, è anche possibile applicare proprietà CSS in linea ai singoli componenti di un modulo adattivo.
seo-description: While you can apply custom styles on an adaptive form, you can also apply inline CSS properties on individual components of an adaptive form.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Adaptive Forms
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Stile in linea dei componenti di moduli adattivi {#inline-styling-of-adaptive-form-components}

È possibile definire l’aspetto e lo stile generali di un modulo adattivo specificando gli stili utilizzando [editor temi](../../forms/using/themes.md). Inoltre, puoi applicare stili CSS in linea ai singoli componenti del modulo adattivo e visualizzare all’istante l’anteprima delle modifiche. Gli stili in linea sostituiscono gli stili forniti nel tema.

## Applicare le proprietà CSS in linea {#apply-inline-css-properties}

Per aggiungere stili in linea a un componente:

1. Apri il modulo nell’editor moduli e cambia la modalità in modalità di stile. Per impostare la modalità stile, nella barra degli strumenti della pagina tocca ![elenco a discesa area di lavoro](assets/canvas-drop-down.png) > **Stile**.
1. Seleziona un componente nella pagina e tocca il pulsante Modifica ![edit-button](assets/edit-button.png). Le proprietà di stile si aprono nella barra laterale.

   Puoi anche selezionare i componenti dalla struttura gerarchica del modulo nella barra laterale. La struttura della gerarchia dei moduli è disponibile come Oggetti modulo nella barra laterale.

   Puoi anche selezionare un componente dalla barra laterale. Nella modalità Stile, è possibile visualizzare i componenti elencati in Oggetti modulo. Tuttavia, l’elenco Oggetti modulo nella barra laterale elenca componenti quali campi e pannelli. I campi e i pannelli sono componenti generici che possono contenere componenti quali caselle di testo e pulsanti di scelta.

   Quando selezioni un componente dalla barra laterale, vengono visualizzati tutti i sottocomponenti elencati e le proprietà del componente selezionato. Puoi selezionare un sottocomponente specifico e assegnargli uno stile.

1. Fai clic su una scheda nella barra laterale per specificare le proprietà CSS. Puoi specificare proprietà quali:

   * Dimension e posizione (impostazione di visualizzazione, spaziatura interna, altezza, larghezza, margine, posizione, indice z, mobile, deflusso)
   * Testo (famiglia di caratteri, peso, colore, dimensioni, altezza della linea e allineamento)
   * Sfondo (immagine e sfumatura, colore di sfondo)
   * Bordo (larghezza, stile, colore, raggio)
   * Effetti (Ombra, Opacità)
   * Avanzate (consente di scrivere CSS personalizzati per il componente)

1. Allo stesso modo, potete applicare stili ad altre parti di un componente, ad esempio Widget, Didascalia e Guida.
1. Tocca **Fine** per confermare le modifiche o **Annulla** per ignorare le modifiche.

## Esempio: stili in linea per un componente campo {#example-inline-styles-for-a-field-component}

Le immagini seguenti rappresentano un campo di testo prima e dopo l’applicazione di stili in linea.

![Componente casella di testo prima dell’applicazione dello stile in linea](assets/no-style.png)

Componente casella di testo prima di applicare proprietà di stile in linea

Osserva la modifica dello stile della casella di testo come mostrato nell’immagine seguente dopo l’applicazione delle seguenti proprietà CSS.

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
   <td><p>bordo</p> </td>
   <td><p>Larghezza bordo = 2 px</p> <p>Stile bordo=solido</p> <p>Colore bordo=#1111</p> </td>
   <td><p>Crea un bordo nero largo 2 px attorno al campo</p> </td>
  </tr>
  <tr>
   <td><p>Casella di testo</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia il colore di sfondo in blu fioreCornice (#6495ED)</p> <p>Nota: è possibile specificare un nome di colore o il relativo codice esadecimale nel campo valore.</p> </td>
  </tr>
  <tr>
   <td><p>Etichetta</p> </td>
   <td><p>Dimensioni e posizione &gt; larghezza</p> </td>
   <td><p>100px</p> </td>
   <td><p>Imposta la larghezza come 100 px per l'etichetta</p> </td>
  </tr>
  <tr>
   <td>Icona guida campo</td>
   <td>Testo &gt; Colore carattere</td>
   <td>#2ECC40</td>
   <td>Cambia il colore della faccia dell'icona della guida.</td>
  </tr>
  <tr>
   <td><p>Descrizione lunga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>centro</p> </td>
   <td><p>Allinea al centro la descrizione lunga della guida</p> </td>
  </tr>
 </tbody>
</table>

![Stile casella di testo dopo l&#39;applicazione dello stile in linea](assets/applied-style.png)

Componente casella di testo dopo l’applicazione delle proprietà di stile in linea

Seguendo i passaggi precedenti, è possibile selezionare e assegnare uno stile ad altri componenti, ad esempio pannelli, pulsanti di invio e pulsanti di scelta.

>[!NOTE]
>
>Le proprietà di stile variano in base al componente selezionato.
