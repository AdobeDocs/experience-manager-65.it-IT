---
title: Introduzione all’interfaccia utente di authoring delle comunicazioni interattive
seo-title: An introduction to the various user interface elements you can use to author Interactive Communication
description: Introduzione ai vari elementi dell’interfaccia utente che è possibile utilizzare per creare la comunicazione interattiva
seo-description: An introduction to the various user interface elements you can use to author Interactive Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 14%

---

# Introduzione all’interfaccia utente di authoring delle comunicazioni interattive{#introduction-to-interactive-communication-authoring-ui}

Interfaccia utente per l’authoring [Comunicazione interattiva](/help/forms/using/interactive-communications-overview.md) è intuitivo e fornisce quanto segue per l’authoring di stampe e canali web della comunicazione interattiva:

* Editor di documenti con trascinamento della selezione WYSIWYG
* Archivio integrato per le risorse: le risorse caricate e create sul server sono disponibili nel browser Risorse dell’interfaccia di authoring di comunicazioni interattive

Quando [creare o modificare una comunicazione interattiva esistente](../../forms/using/create-interactive-communication.md), utilizza i seguenti elementi dell’interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* Area contenuto

![interfaccia utente per l’authoring di comunicazioni interattive](assets/form-editor.png)

**R.** Barra laterale **B.** Barra degli strumenti Pagina **C.** Area contenuto

## Barra laterale {#sidebar}

![Barra laterale](assets/sidebar-comps-2.png)

**R.** Browser canali **B.** Browser contenuti **C.** Browser delle proprietà **D.** Browser risorse **E.** Browser Componenti **F.** Browser Origini dati - Modello dati **G.** Browser Origini dati - Contenuto principale

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra laterale include quanto segue:

* **Browser canali**

Il browser Canale consente di passare dalla stampa ai canali web della comunicazione interattiva e viceversa. In base al canale selezionato nel browser Canali, le opzioni sono visualizzate nei browser, ad esempio Contenuto e Componenti.

* **Browser contenuti**
Nel browser del contenuto è possibile visualizzare la gerarchia degli oggetti del documento per il canale selezionato. L’autore può passare a un componente specifico toccando tale elemento nella struttura ad oggetti del documento. L’autore può cercare oggetti nel canale web e ridisporli da questa struttura.

* **Browser proprietà**

  Consente di modificare le proprietà di un componente. Le proprietà cambiano in base al componente. Ad esempio, per visualizzare le proprietà del contenitore di documenti: seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **Contenitore documento**, quindi tocca ![cmppr](assets/cmppr.png).

* **Browser risorse**
Segrega diversi tipi di contenuto, ad esempio frammenti di layout, immagini, documenti, pagine e video. L’autore può trascinare le risorse nella comunicazione interattiva.

* **Browser Componenti**
Include componenti che è possibile utilizzare per creare i canali di stampa e web di un documento. Puoi trascinare i componenti nella comunicazione interattiva per aggiungere elementi e configurare un elemento aggiunto in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti per i canali di stampa e web:

| **Component** | **Canale di stampa** | **Canale web** | **Funzionalità** |
|---|---|---|---|
| Grafico | ✓ | ✓ | Aggiunge un grafico che è possibile utilizzare in una comunicazione interattiva per la rappresentazione visiva di dati bidimensionali recuperati da un elemento di raccolta di modelli di dati modulo. |
| Frammento di documento | ✓ | ✓ | Consente di aggiungere un componente, testo, elenco o condizione riutilizzabile a una comunicazione interattiva. Il componente riutilizzabile aggiunto a una comunicazione interattiva potrebbe essere basato su un modello di dati modulo o senza un modello di dati modulo. |
| Immagine | ✓ | ✓ | Consente di inserire un&#39;immagine. |
| Pannello | - | ✓ | Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla il layout di un gruppo di componenti in una comunicazione interattiva. Un componente pannello consente inoltre di rendere un gruppo di componenti ripetibili per l’utente finale, ad esempio in più voci necessarie per compilare le credenziali educative. È inoltre consigliabile utilizzare un pannello ciascuno per una scheda di una comunicazione interattiva con più schede. |
| Tabella | &#42; | ✓ | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
| Area di destinazione | &#42;&#42; | ✓ | Inserisce un&#39;area di destinazione in un canale web per organizzare i componenti specifici del canale web. |
| Testo | - | ✓ | Aggiunge testo al canale web di una comunicazione interattiva. Il testo può utilizzare oggetti modello dati modulo per rendere dinamico il contenuto. |

&#42; Utilizza Frammenti layout nel canale Stampa per aggiungere tabelle.

&#42;&#42; Nel canale di stampa, le aree di destinazione sono predefinite nel modello XDP/print. Non è possibile aggiungere nuove aree di destinazione utilizzando l’interfaccia utente di creazione della comunicazione interattiva.

* **Browser origini dati**
Il browser Origini dati visualizza le origini dati disponibili nel modello dati del modulo selezionato durante la creazione della comunicazione interattiva.

### Punti chiave per l’utilizzo dei componenti {#key-points-for-working-with-components}

I punti chiave quando si lavora con i componenti di comunicazione interattiva sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, tocca il componente e tocca ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente è identificato dal relativo nome elemento. Quando tocchi ![cmppr](assets/cmppr.png), è possibile modificare il nome del componente modificando il valore del campo Nome elemento nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e trattini bassi (_). Non sono consentiti altri caratteri speciali e il nome dell’elemento deve iniziare con una lettera.
* Puoi modificare la proprietà Titolo di un componente Comunicazione interattiva in linea nell’editor senza aprire il browser Proprietà, purché il titolo sia visibile nella Comunicazione interattiva. Per eseguire questa operazione:

   1. Tocca per selezionare un componente con la proprietà Titolo e la cui proprietà Nascondi titolo è disabilitata.
   1. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modifica il titolo e tocca Ritorna o tocca un punto qualsiasi all’esterno del componente per salvare le modifiche. Toccare il tasto Esc per ignorare le modifiche.

## Barra degli strumenti del componente {#component-toolbar}

![Etichette della barra degli strumenti del componente](do-not-localize/component_toolbar_labels_new.png)

Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configura**: quando tocchi **Configura**, le proprietà dei componenti sono visibili nella barra laterale.

B.**Modifica regole**: quando tocchi Modifica regole, viene visualizzato l’Editor regole in cui puoi modificare e creare regole per il componente selezionato. Nell’Editor regole è inoltre possibile selezionare altri oggetti modulo (componenti) e modificare/creare regole per tali oggetti modulo.

C.**Copia**: puoi utilizzare l’opzione Copia per copiare un componente e incollarlo in altre posizioni nella comunicazione interattiva.

D.**Taglia**: puoi utilizzare l’opzione Taglia per spostare un componente da una posizione all’altra nella comunicazione interattiva.

E. **Elimina**: consente di eliminare il componente dalla comunicazione interattiva.

F. **Inserisci componente**: consente di inserire un componente sopra il componente selezionato.

G. **Incolla**: consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.

H. **Gruppo**: consente di selezionare più componenti se si desidera tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento principale**: consente di selezionare l’elemento principale di un componente.

J. **Visualizza espressione SOM:** Consente di visualizzare [Espressione SOM](../../forms/using/using-som-expressions-adaptive-forms.md) per il componente.

K: **Raggruppa oggetti nel pannello:** Consente di raggruppare i componenti in un pannello per poter eseguire operazioni su tali componenti contemporaneamente. Per ulteriori informazioni, consulta [Raggruppa oggetti nel pannello](create-interactive-communication.md#groupobjectspanel).

L. **Aggiungi pannello secondario** (solo per i pannelli): consente di aggiungere un pannello figlio al pannello.

M: **Barra degli strumenti Aggiungi pannello** (solo per i pannelli): consente di aggiungere la barra degli strumenti per il componente Pannello. È quindi possibile eseguire ulteriori azioni sulla barra degli strumenti.

Inoltre, la **Sostituisci** sulla barra degli strumenti consente di sostituire il componente esistente con un componente alternativo. L’opzione non è disponibile per il componente Pannello.

## Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti Pagina nella parte superiore fornisce opzioni che consentono di visualizzare in anteprima la comunicazione interattiva e modificarne le proprietà. Puoi visualizzare in anteprima la comunicazione interattiva quando la crei e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili le seguenti opzioni:

* Attiva/Disattiva pannello laterale![ attiva/disattiva pannello laterale](assets/toggle-side-panel.png): consente di mostrare o nascondere la barra laterale.
* Informazioni pagina ![pageinformationad](assets/pageinformationad.png): consente di visualizzare le proprietà della pagina.
* Emulatore ![righello](assets/ruler.png): consente di simulare l’aspetto della comunicazione interattiva per diverse dimensioni di display, ad esempio tablet e telefoni.
* Modifica: consente di selezionare altre modalità, ad esempio: Modifica, Stile, Sviluppatore e Progettazione.

   * Modifica: consente di modificare le proprietà della comunicazione interattiva e dei relativi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * Stile: consente di applicare uno stile all’aspetto dei componenti della comunicazione interattiva. Ad esempio, in modalità stile è possibile selezionare un pannello e specificarne il colore di sfondo.
   * Sviluppatore: consente a uno sviluppatore di:

      * Scopri di cosa è composta la comunicazione interattiva.
      * Eseguire il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.

   * Target: consente di abilitare o disabilitare i componenti personalizzati o i componenti predefiniti non elencati nella barra laterale.

* Anteprima: consente di visualizzare in anteprima come si presenterà la comunicazione interattiva quando verrà pubblicata.
