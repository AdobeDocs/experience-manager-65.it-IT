---
title: Stile in linea dei componenti di moduli adattivi
description: Sebbene sia possibile applicare stili personalizzati a un modulo adattivo, è anche possibile applicare proprietà CSS in linea ai singoli componenti di un modulo adattivo.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 4%

---

# Stile in linea dei componenti di moduli adattivi {#inline-styling-of-adaptive-form-components}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html) |
| AEM 6.5 | Questo articolo |

È possibile definire l’aspetto e lo stile generali di un modulo adattivo specificando gli stili utilizzando [editor temi](../../forms/using/themes.md). Inoltre, puoi applicare stili CSS in linea ai singoli componenti del modulo adattivo e visualizzare all’istante l’anteprima delle modifiche. Gli stili in linea sostituiscono gli stili forniti nel tema.

## Applicare le proprietà CSS in linea {#apply-inline-css-properties}

Per aggiungere stili in linea a un componente:

1. Apri il modulo nell’editor moduli e cambia la modalità in modalità di stile. Per cambiare la modalità in modalità stile, nella barra degli strumenti della pagina seleziona ![elenco a discesa area di lavoro](assets/canvas-drop-down.png) > **Stile**.
1. Seleziona un componente nella pagina e fai clic sul pulsante Modifica ![edit-button](assets/edit-button.png). Le proprietà di stile si aprono nella barra laterale.

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
1. Seleziona **Fine** per confermare le modifiche o **Annulla** per ignorare le modifiche.

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
   <td><p>100 px</p> </td>
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
