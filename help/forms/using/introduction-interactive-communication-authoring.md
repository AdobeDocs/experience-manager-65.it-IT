---
title: Introduzione all’interfaccia utente per l’authoring delle comunicazioni interattive
seo-title: Introduzione ai vari elementi dell'interfaccia utente che è possibile utilizzare per creare comunicazioni interattive
description: Introduzione ai vari elementi dell'interfaccia utente che è possibile utilizzare per creare comunicazioni interattive
seo-description: Introduzione ai vari elementi dell'interfaccia utente che è possibile utilizzare per creare comunicazioni interattive
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
translation-type: tm+mt
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# Introduzione all’interfaccia utente per l’authoring delle comunicazioni interattive{#introduction-to-interactive-communication-authoring-ui}

L&#39;interfaccia utente per la creazione di comunicazioni [](/help/forms/using/interactive-communications-overview.md) interattive è intuitiva e fornisce le seguenti informazioni per l&#39;authoring della stampa e del canale web della comunicazione interattiva:

* Editor di documenti con trascinamento WYSIWYG
* Archivio integrato per le risorse - le risorse caricate e create sul server sono disponibili nel browser Risorse dell’interfaccia di authoring per comunicazioni interattive

Quando [create una nuova comunicazione interattiva o modificate una comunicazione](../../forms/using/create-interactive-communication.md)interattiva esistente, utilizzate i seguenti elementi dell&#39;interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti Pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* Area contenuto

![interfaccia utente per la creazione di comunicazioni interattive](assets/form-editor.png)

******A. Barra laterale** B. Barra degli strumenti Pagina **C.** Area contenuto

## Barra laterale {#sidebar}

![Barra laterale](assets/sidebar-comps-2.png)

**************A. Browser canale** B. Browser dei contenuti **C.** Browser delle proprietà **D. Browser risorse** E. Browser componenti **F. Browser Origini dati - Modello dati** G. Browser Origini dati - Contenuto principale

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra laterale include quanto segue:

* **Browser canale**

Il browser Canale consente di passare dai canali di stampa a quelli Web della comunicazione interattiva. In base al canale selezionato nel browser del canale, i browser, come Contenuto e Componenti, visualizzano le opzioni.

* **Browser** Contenuto Nel browser del contenuto è possibile visualizzare la gerarchia degli oggetti del documento per il canale selezionato. L&#39;autore può passare a un componente specifico toccando tale elemento nella struttura ad albero oggetto documento. L&#39;autore può cercare gli oggetti nel canale Web e ridisporli da questa struttura ad albero.

* **Browser proprietà**

   Consente di modificare le proprietà di un componente. Le proprietà cambiano a seconda del componente. Ad esempio, per visualizzare le proprietà del contenitore documenti:
Selezionate un componente, quindi toccate il livello ![del](assets/field-level.png) campo > Contenitore **** documento, quindi toccate ![cmppr](assets/cmppr.png).

* **Browser** Risorse Consente di segmentare diversi tipi di contenuto, ad esempio frammenti di layout, immagini, documenti, pagine e video. L’autore può trascinare risorse nella comunicazione interattiva.

* **Browser** Componenti Include componenti che è possibile utilizzare per creare canali di stampa e Web di un documento. Puoi trascinare i componenti nella comunicazione interattiva per aggiungere elementi e configurare gli elementi aggiunti in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti per la stampa e i canali Web:

| **Componente** | **Stampa canale** | **Canale web** | **Funzionalità** |
|---|---|---|---|
| Grafico | ✓ | ✓ | Aggiunge un grafico che è possibile utilizzare in una comunicazione interattiva per la rappresentazione visiva dei dati bidimensionali recuperati da un elemento di raccolta dei dati del modulo. |
| Frammento di documento | ✓ | ✓ | Consente di aggiungere a una comunicazione interattiva un componente, un testo, un elenco o una condizione riutilizzabili. Il componente riutilizzabile aggiunto a una comunicazione interattiva potrebbe essere basato su un modello dati del modulo o non su un modello dati del modulo. |
| Immagine | ✓ | ✓ | Consente di inserire un’immagine. |
| Pannello | - | ✓ | Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla come un gruppo di componenti viene disposto in una comunicazione interattiva. Un componente pannello consente inoltre di rendere ripetibile un gruppo di componenti per l’utente finale, ad esempio in più voci richieste per compilare le credenziali educative. È inoltre buona norma utilizzare un pannello per ciascuna scheda di una comunicazione interattiva con più schede. |
| Tabella | * | ✓ | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
| Area di destinazione | ** | ✓ | Inserisce un’area di destinazione in un canale Web per organizzare i componenti specifici del canale Web. |
| Testo | - | ✓ | Aggiunge testo al canale Web di una comunicazione interattiva. Il testo può utilizzare oggetti del modello dati del modulo per rendere dinamico il contenuto. |

* Utilizzare i frammenti di layout nel canale di stampa per aggiungere tabelle.

** Nel canale di stampa, le aree di destinazione sono predefinite nel modello XDP/print. Non è possibile aggiungere nuove aree di destinazione utilizzando l&#39;interfaccia utente per l&#39;authoring delle comunicazioni interattive.

* **Origini dati Browser** Origini dati Browser visualizza le origini dati disponibili nel modello dati del modulo selezionato durante la creazione della comunicazione interattiva.

### Punti chiave per l’utilizzo dei componenti {#key-points-for-working-with-components}

I punti chiave per l’utilizzo dei componenti di comunicazione interattiva sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, toccate il componente e toccate ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente è identificato con il nome del relativo elemento. Toccando ![cmppr](assets/cmppr.png), potete modificare il nome del componente modificando il valore del campo Nome elemento nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e caratteri di sottolineatura (_). Non sono consentiti altri caratteri speciali e il nome dell&#39;elemento deve iniziare con una lettera.
* È possibile modificare la proprietà Titolo di un componente Comunicazione interattiva in linea nell’editor senza aprire il browser Proprietà, purché il titolo sia visibile nella comunicazione interattiva. A questo scopo:

   1. Toccate per selezionare un componente con una proprietà Titolo e la cui proprietà Nascondi titolo è disabilitata.
   1. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modificate il titolo e toccate il tasto Invio oppure toccate un punto qualsiasi all’esterno del componente per salvare le modifiche. Toccate il tasto Esc per annullare le modifiche.

## Component toolbar {#component-toolbar}

![Etichette della barra degli strumenti dei componenti](do-not-localize/component_toolbar_labels_new.png)

Quando selezionate un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configure**: Toccando **Configura**, le proprietà del componente sono visibili nella barra laterale.

B.**Modifica regole**: Quando si tocca Modifica regole, viene visualizzato Editor regole in cui è possibile modificare e creare le regole per il componente selezionato. Nell&#39;Editor regole è inoltre possibile selezionare altri oggetti modulo (componenti) e modificare o creare regole per tali oggetti modulo.

C.**Copia**: Potete usare l’opzione Copia per copiare un componente e incollarlo in altre aree della comunicazione interattiva.

D.**Taglia**: Potete usare l’opzione Taglia per spostare un componente da una posizione all’altra nella comunicazione interattiva.

E. **Elimina**: Consente di eliminare il componente dalla comunicazione interattiva.

F. **Inserisci componente**: Consente di inserire un componente sopra il componente selezionato.

G. **Incolla**: Consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte sopra.

H. **Gruppo**: Consente di selezionare più componenti per tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento padre**: Consente di selezionare l’elemento padre di un componente.

**J. Espressione** View SOM: Consente di visualizzare l&#39;espressione [](../../forms/using/using-som-expressions-adaptive-forms.md) SOM per il componente.

**K: Oggetti** gruppo nel pannello: Consente di raggruppare i componenti in un pannello per eseguire contemporaneamente operazioni su tali componenti. Per informazioni dettagliate, consultate [Raggruppare gli oggetti nel pannello](../../forms/using/create-interactive-communication.md#main-pars-header-1815149576).

L. **Aggiungi pannello** secondario (solo per i pannelli): Consente di aggiungere al pannello un pannello secondario.

M: Barra degli strumenti **del pannello** Aggiungi (solo per i pannelli):consente di aggiungere il componente Barra degli strumenti per il pannello. È quindi possibile eseguire ulteriori azioni sulla barra degli strumenti.

Inoltre, l’opzione **Sostituisci** nella barra degli strumenti consente di sostituire il componente esistente con un componente alternativo. L’opzione non è disponibile per il componente Pannello.

## Page toolbar {#page-toolbar}

La barra degli strumenti Pagina nella parte superiore contiene opzioni che consentono di visualizzare l’anteprima della comunicazione interattiva e di modificarne le proprietà. Potete visualizzare l’anteprima della comunicazione interattiva al momento della creazione e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili:

* Attiva/disattiva pannello laterale ![o pannello](assets/toggle-side-panel.png)laterale: Consente di mostrare o nascondere la barra laterale.
* Informazioni pagina, ![pageinformationad](assets/pageinformationad.png): Consente di visualizzare le proprietà della pagina.
* Emulatore ![righello](assets/ruler.png): Consente di emulare l’aspetto della comunicazione interattiva per diverse dimensioni di visualizzazione, ad esempio tablet e telefoni.
* Modifica: Consente di selezionare altre modalità, ad esempio: Modifica, Stile, Sviluppatore e Progettazione.

   * Modifica: Consente di modificare le proprietà della comunicazione interattiva e dei suoi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * Stile: Consente di definire l’aspetto dei componenti della comunicazione interattiva. Ad esempio, in modalità stile, potete selezionare un pannello e specificarne il colore di sfondo.
   * Sviluppatore: Consente a uno sviluppatore di:

      * Scopri di cosa si compone la comunicazione interattiva.
      * Eseguire il debug di quanto sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.
   * Target:Consente di abilitare o disabilitare componenti personalizzati, o componenti out-of-the-box non elencati nella barra laterale.


* Anteprima: Consente di visualizzare un&#39;anteprima dell&#39;aspetto della comunicazione interattiva al momento della pubblicazione.

