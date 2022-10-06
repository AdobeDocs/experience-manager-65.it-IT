---
title: Introduzione all’interfaccia utente per l’authoring delle comunicazioni interattive
seo-title: An introduction to the various user interface elements you can use to author Interactive Communication
description: Introduzione ai vari elementi dell’interfaccia utente utilizzabili per la creazione di comunicazioni interattive
seo-description: An introduction to the various user interface elements you can use to author Interactive Communication
uuid: e8c5b1e8-b2bb-46b4-b42e-1f343192641a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 5855d21b-340c-4139-aabe-c3a534cedb98
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 3%

---

# Introduzione all’interfaccia utente per l’authoring delle comunicazioni interattive{#introduction-to-interactive-communication-authoring-ui}

Interfaccia utente per l’authoring [Comunicazione interattiva](/help/forms/using/interactive-communications-overview.md) è intuitivo e fornisce quanto segue per l’authoring di canali web e di stampa della comunicazione interattiva:

* Editor di documenti con trascinamento WYSIWYG
* Archivio integrato per le risorse: le risorse caricate e create sul server sono disponibili nel browser Risorse dell’interfaccia di authoring delle comunicazioni interattive

Quando [creare una nuova comunicazione interattiva o modificarne una esistente](../../forms/using/create-interactive-communication.md), utilizza i seguenti elementi dell’interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* Area contenuto

![interfaccia utente per l’authoring delle comunicazioni interattive](assets/form-editor.png)

**A.** Barra laterale **B.** Barra degli strumenti della pagina **C.** Area contenuto

## Barra laterale {#sidebar}

![Barra laterale](assets/sidebar-comps-2.png)

**A.** Browser del canale **B.** Browser dei contenuti **C.** Browser proprietà **D.** Browser risorse **E.** Browser Componenti **F.** Browser Origini dati - Modello dati **G.** Browser Origini dati - Contenuto principale

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra laterale include i seguenti elementi:

* **Browser del canale**

Il browser Canale consente di passare dai canali di stampa a quelli web della comunicazione interattiva. In base al canale selezionato nel browser del canale, i browser, ad esempio Contenuto e Componenti , visualizzano le opzioni .

* **Browser dei contenuti**
Nel browser del contenuto è possibile visualizzare la gerarchia degli oggetti del documento per il canale selezionato. Per passare a un componente specifico, l’autore può toccarlo nella struttura ad albero degli oggetti documento. L’autore può cercare gli oggetti nel canale web e riorganizzarli da questo albero.

* **Browser proprietà**

   Consente di modificare le proprietà di un componente. Le proprietà cambiano in base al componente. Ad esempio, per visualizzare le proprietà del contenitore documento: Seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **Contenitore documento**, quindi tocca ![cmppr](assets/cmppr.png).

* **Browser risorse**
Segrega diversi tipi di contenuto, ad esempio frammenti di layout, immagini, documenti, pagine, video. L’autore può trascinare le risorse nella comunicazione interattiva.

* **Browser Componenti**
Include i componenti che è possibile utilizzare per creare i canali web e di stampa di un documento. Puoi trascinare i componenti nella comunicazione interattiva per aggiungere elementi e configurare gli elementi aggiunti in base ai requisiti. Nella tabella seguente sono descritti i componenti elencati nel browser Componenti per la stampa e i canali web:

| **Component** | **Canale di stampa** | **Canale web** | **Funzionalità** |
|---|---|---|---|
| Grafico | ✓ | ✓ | Aggiunge un grafico che è possibile utilizzare in una comunicazione interattiva per la rappresentazione visiva dei dati bidimensionali recuperati da un elemento di raccolta dati del modulo. |
| Frammento di documento | ✓ | ✓ | Consente di aggiungere un componente, un testo, un elenco o una condizione riutilizzabili a una comunicazione interattiva. Il componente riutilizzabile aggiunto a una comunicazione interattiva può essere basato su un modello di dati del modulo o senza un modello di dati del modulo. |
| Immagine | ✓ | ✓ | Consente di inserire un’immagine. |
| Pannello | - | ✓ | Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla come un gruppo di componenti viene disposto in una comunicazione interattiva. Un componente pannello consente inoltre di rendere ripetibile un gruppo di componenti per l’utente finale, ad esempio in più voci richieste per il riempimento delle credenziali educative. È inoltre buona prassi utilizzare un pannello ciascuno per una scheda di una comunicazione interattiva con più schede. |
| Tabella | &#42; | ✓ | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
| Area di destinazione | &#42;&#42; | ✓ | Inserisce un’area di destinazione in un canale web per organizzare i componenti specifici del canale web. |
| Testo | - | ✓ | Aggiunge testo al canale web di una comunicazione interattiva. Il testo può utilizzare gli oggetti del modello dati del modulo per rendere dinamico il contenuto. |

&#42; Utilizzare i frammenti di layout nel canale Stampa per aggiungere tabelle.

&#42;&#42; Nel canale di stampa, le aree di destinazione sono predefinite nel modello XDP/print. Non è possibile aggiungere nuove aree di destinazione utilizzando l’interfaccia utente per la creazione di comunicazioni interattive.

* **Browser Origini dati**
Origini dati Browser visualizza le origini dati disponibili nel modello dati del modulo selezionato durante la creazione della comunicazione interattiva.

### Punti chiave per l’utilizzo dei componenti {#key-points-for-working-with-components}

I punti chiave per l’utilizzo dei componenti di comunicazione interattivi sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, tocca il componente e tocca ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente viene identificato con il suo nome elemento. Quando tocchi ![cmppr](assets/cmppr.png), puoi modificare il nome del componente modificando il valore del campo Nome elemento nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e caratteri di sottolineatura (_). Altri caratteri speciali non sono consentiti e il nome dell’elemento deve iniziare con una lettera.
* È possibile modificare la proprietà Titolo di un componente Comunicazione interattiva in linea nell’editor senza aprire il browser Proprietà, purché il titolo sia visibile nella comunicazione interattiva. Per eseguire questa operazione:

   1. Tocca per selezionare un componente con una proprietà Titolo e la cui proprietà Nascondi titolo è disabilitata.
   1. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modifica il titolo e tocca il tasto Invio oppure tocca un punto qualsiasi all’esterno del componente per salvare le modifiche. Tocca il tasto Esc per eliminare le modifiche.

## Barra degli strumenti del componente {#component-toolbar}

![Etichette per la barra degli strumenti del componente](do-not-localize/component_toolbar_labels_new.png)

Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configura**: Quando tocchi **Configura**, le proprietà dei componenti sono visibili nella barra laterale.

B.**Modifica regole**: Quando tocchi Modifica regole, viene visualizzato Editor regole in cui puoi modificare e creare regole per il componente selezionato. Nell’Editor regole è inoltre possibile selezionare altri oggetti modulo (componenti) e modificare/creare regole per tali oggetti modulo.

C.**Copia**: È possibile utilizzare l’opzione Copia per copiare un componente e incollarlo in altre posizioni nella comunicazione interattiva.

D.**Taglia**: È possibile utilizzare l’opzione Taglia per spostare un componente da una posizione all’altra nella comunicazione interattiva.

E. **Elimina**: Consente di eliminare il componente dalla comunicazione interattiva.

F. **Inserisci componente**: Consente di inserire un componente sopra il componente selezionato.

G. **Incolla**: Consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.

H. **Gruppo**: Consente di selezionare più componenti se si desidera tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento padre**: Consente di selezionare l’elemento padre di un componente.

J. **Visualizza espressione SOM:** Consente di visualizzare il [Espressione SOM](../../forms/using/using-som-expressions-adaptive-forms.md) per il componente.

K: **Raggruppa gli oggetti nel pannello:** Consente di raggruppare i componenti in un pannello per eseguire le operazioni su tali componenti simultaneamente. Per maggiori dettagli, vedi [Raggruppare gli oggetti nel pannello](create-interactive-communication.md#groupobjectspanel).

L. **Aggiungi pannello figlio** (solo per i pannelli): Consente di aggiungere un pannello figlio al pannello.

M: **Aggiungi barra degli strumenti del pannello** (solo per i pannelli):consente di aggiungere il componente Barra degli strumenti per il pannello. È quindi possibile eseguire ulteriori azioni sulla barra degli strumenti.

Inoltre, il **Sostituisci** nella barra degli strumenti puoi sostituire il componente esistente con un componente alternativo. L’opzione non è disponibile per il componente Pannello.

## Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti Pagina nella parte superiore fornisce opzioni che consentono di visualizzare in anteprima la comunicazione interattiva e di modificarne le proprietà. Puoi visualizzare in anteprima la comunicazione interattiva quando la crei e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili le seguenti opzioni:

* Attiva/Disattiva pannello laterale ![pannello laterale di attivazione](assets/toggle-side-panel.png): Consente di mostrare o nascondere Sidebar.
* Informazioni sulla pagina ![pageinformationad](assets/pageinformationad.png): Consente di visualizzare le proprietà della pagina.
* Emulatore ![righello](assets/ruler.png): Consente di emulare l’aspetto della comunicazione interattiva per diverse dimensioni di visualizzazione, come tablet e telefoni.
* Modifica: Consente di selezionare altre modalità, ad esempio: Modifica, Stile, Sviluppatore e Progettazione.

   * Modifica: Consente di modificare le proprietà della comunicazione interattiva e dei relativi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * Stile: Consente di definire lo stile dei componenti della comunicazione interattiva. Ad esempio, in modalità stile è possibile selezionare un pannello e specificarne il colore di sfondo.
   * Sviluppatore: Consente a uno sviluppatore di:

      * Scopri la composizione della comunicazione interattiva.
      * Esegui il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.
   * Target: Consente di abilitare o disabilitare i componenti personalizzati o i componenti predefiniti non elencati nella barra laterale.


* Anteprima: Ti consente di visualizzare un’anteprima dell’aspetto della comunicazione interattiva quando la pubblichi.
