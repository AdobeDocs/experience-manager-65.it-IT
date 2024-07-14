---
title: Introduzione all’interfaccia utente di authoring delle comunicazioni interattive
description: Introduzione ai vari elementi dell’interfaccia utente che è possibile utilizzare per creare la comunicazione interattiva
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 3d15a723-df6c-4b4a-992e-a6636f4cf3dc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 10%

---

# Introduzione all’interfaccia utente di authoring delle comunicazioni interattive{#introduction-to-interactive-communication-authoring-ui}

L&#39;interfaccia utente per l&#39;authoring di [comunicazione interattiva](/help/forms/using/interactive-communications-overview.md) è intuitiva e fornisce le seguenti informazioni per l&#39;authoring di stampa e canale Web della comunicazione interattiva:

* Editor di documenti con trascinamento della selezione WYSIWYG
* Archivio integrato per le risorse: le risorse caricate e create sul server sono disponibili nel browser Risorse dell’interfaccia di authoring di comunicazioni interattive

Quando [crei o modifichi una comunicazione interattiva esistente](../../forms/using/create-interactive-communication.md), utilizzi i seguenti elementi dell&#39;interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* Area contenuto

![interfaccia utente per l&#39;authoring di comunicazioni interattive](assets/form-editor.png)

**A.** Barra laterale **B.** Barra degli strumenti delle pagine **C.** Area contenuto

## Barra laterale {#sidebar}

![Barra laterale](assets/sidebar-comps-2.png)

**A.** Browser canali **B.** Browser contenuti **C.** Browser proprietà **D.** Browser risorse **E.** Browser componenti **F.** Browser origini dati - Modello dati **G.** Browser origini dati - Contenuto principale

<!-- Click to enlarge

![sidebar-comps-3](assets/sidebar-comps-3.png)-->

La barra laterale include quanto segue:

* **Browser canali**

Il browser Canale consente di passare dalla stampa ai canali web della comunicazione interattiva e viceversa. In base al canale selezionato nel browser Canali, le opzioni sono visualizzate nei browser, ad esempio Contenuto e Componenti.

* **Browser contenuti**
Nel browser del contenuto è possibile visualizzare la gerarchia degli oggetti del documento per il canale selezionato. L’autore può passare a un componente specifico toccando tale elemento nella struttura ad oggetti del documento. L’autore può cercare oggetti nel canale web e ridisporli da questa struttura.

* **Browser proprietà**

  Consente di modificare le proprietà di un componente. Le proprietà cambiano in base al componente. Ad esempio, per visualizzare le proprietà del contenitore di documenti:
Seleziona un componente, quindi seleziona ![livello campo](assets/field-level.png) > **Contenitore documenti**, quindi seleziona ![cmppr](assets/cmppr.png).

* **Browser Assets**
Segrega diversi tipi di contenuto, ad esempio frammenti di layout, immagini, documenti, pagine e video. L’autore può trascinare le risorse nella comunicazione interattiva.

* **Browser componenti**
Include componenti che è possibile utilizzare per creare i canali di stampa e web di un documento. Puoi trascinare i componenti nella comunicazione interattiva per aggiungere elementi e configurare un elemento aggiunto in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti per i canali di stampa e web:

| **Component** | **Canale di stampa** | **Canale Web** | **Funzionalità** |
|---|---|---|---|
| Grafico | ✓ | ✓ | Aggiunge un grafico che è possibile utilizzare in una comunicazione interattiva per la rappresentazione visiva di dati bidimensionali recuperati da un elemento di raccolta di modelli di dati modulo. |
| Frammento di documento | ✓ | ✓ | Consente di aggiungere un componente, testo, elenco o condizione riutilizzabile a una comunicazione interattiva. Il componente riutilizzabile aggiunto a una comunicazione interattiva potrebbe essere basato su un modello di dati modulo o senza un modello di dati modulo. |
| Immagine | ✓ | ✓ | Consente di inserire un&#39;immagine. |
| Pannello | - | ✓ | Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla il layout di un gruppo di componenti in una comunicazione interattiva. Un componente pannello consente inoltre di rendere un gruppo di componenti ripetibili per l’utente finale, ad esempio in più voci necessarie per compilare le credenziali educative. È inoltre consigliabile utilizzare un pannello ciascuno per una scheda di una comunicazione interattiva con più schede. |
| Tabella | &#42; | ✓ | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
| Area di destinazione | &#42;&#42; | ✓ | Inserisce un&#39;area di destinazione in un canale web per organizzare i componenti specifici del canale web. |
| Testo | - | ✓ | Aggiunge testo al canale web di una comunicazione interattiva. Il testo può utilizzare oggetti modello dati modulo per rendere dinamico il contenuto. |

&#42; Utilizzare i frammenti di layout nel canale di stampa per aggiungere tabelle.

&#42;&#42; Nel canale di stampa, le aree di destinazione sono predefinite nel modello XDP/print. Non è possibile aggiungere nuove aree di destinazione utilizzando l’interfaccia utente di creazione della comunicazione interattiva.

* **Browser Origini Dati**
Il browser Origini dati visualizza le origini dati disponibili nel modello dati del modulo selezionato durante la creazione della comunicazione interattiva.

### Punti chiave per l’utilizzo dei componenti {#key-points-for-working-with-components}

I punti chiave quando si lavora con i componenti di comunicazione interattiva sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, selezionarlo e selezionare ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente è identificato dal relativo nome elemento. Quando si seleziona ![cmppr](assets/cmppr.png), è possibile modificare il nome del componente modificando il valore del campo Nome elemento nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e trattini bassi (_). Non sono consentiti altri caratteri speciali e il nome dell’elemento deve iniziare con una lettera.
* Puoi modificare la proprietà Titolo di un componente Comunicazione interattiva in linea nell’editor senza aprire il browser Proprietà, purché il titolo sia visibile nella Comunicazione interattiva. Per eseguire questa operazione:

   1. Seleziona per selezionare un componente con la proprietà Titolo e la cui proprietà Nascondi titolo è disabilitata.
   1. Seleziona ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modifica il titolo e seleziona il tasto Invio o seleziona un punto qualsiasi all’esterno del componente per salvare le modifiche. Selezionare la chiave Esc per ignorare le modifiche.

## Barra degli strumenti del componente {#component-toolbar}

![Etichette barra degli strumenti componente](do-not-localize/component_toolbar_labels_new.png)

Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configura**: quando selezioni **Configura**, le proprietà del componente sono visibili nella barra laterale.

B.**Modifica regole**: quando si seleziona Modifica regole, viene visualizzato l&#39;Editor regole in cui è possibile modificare e creare regole per il componente selezionato. Nell’Editor regole è inoltre possibile selezionare altri oggetti modulo (componenti) e modificare/creare regole per tali oggetti modulo.

C.**Copia**: è possibile utilizzare l&#39;opzione Copia per copiare un componente e incollarlo in altre posizioni nella comunicazione interattiva.

D.**Taglia**: è possibile utilizzare l&#39;opzione Taglia per spostare un componente da una posizione all&#39;altra nella comunicazione interattiva.

E. **Elimina**: consente di eliminare il componente dalla comunicazione interattiva.

F. **Inserisci componente**: consente di inserire un componente sopra il componente selezionato.

G. **Incolla**: consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.

H. **Gruppo**: consente di selezionare più componenti se si desidera tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento padre**: consente di selezionare il padre di un componente.

J. **Visualizza espressione SOM:** Consente di visualizzare [espressione SOM](../../forms/using/using-som-expressions-adaptive-forms.md) per il componente.

K: **Raggruppa oggetti nel pannello:** Consente di raggruppare i componenti in un pannello per poter eseguire operazioni su tali componenti contemporaneamente. Per ulteriori dettagli, vedere [Raggruppa oggetti nel pannello](create-interactive-communication.md#groupobjectspanel).

L. **Aggiungi pannello figlio** (solo per i pannelli): consente di aggiungere un pannello figlio al pannello.

M: **Barra degli strumenti Aggiungi pannello** (solo per i pannelli):Consente di aggiungere la barra degli strumenti per il componente Pannello. È quindi possibile eseguire ulteriori azioni sulla barra degli strumenti.

Inoltre, l&#39;opzione **Sostituisci** nella barra degli strumenti consente di sostituire il componente esistente con un componente alternativo. L’opzione non è disponibile per il componente Pannello.

## Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti Pagina nella parte superiore fornisce opzioni che consentono di visualizzare in anteprima la comunicazione interattiva e modificarne le proprietà. Puoi visualizzare in anteprima la comunicazione interattiva quando la crei e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili le seguenti opzioni:

* Attiva/disattiva pannello laterale ![attiva pannello laterale](assets/toggle-side-panel.png): consente di mostrare o nascondere la barra laterale.
* Informazioni pagina ![pageinformationad](assets/pageinformationad.png): consente di visualizzare le proprietà della pagina.
* Emulatore ![righello](assets/ruler.png): consente di emulare l&#39;aspetto della comunicazione interattiva per diverse dimensioni di visualizzazione, ad esempio tablet e telefoni.
* Modifica: consente di selezionare altre modalità, ad esempio Modifica, Stile, Sviluppatore e Progettazione.

   * Modifica: consente di modificare le proprietà della comunicazione interattiva e dei relativi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * Stile: consente di applicare uno stile all’aspetto dei componenti della comunicazione interattiva. Ad esempio, in modalità stile è possibile selezionare un pannello e specificarne il colore di sfondo.
   * Sviluppatore: consente agli sviluppatori di:

      * Scopri di cosa è composta la comunicazione interattiva.
      * Eseguire il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.

   * Target: consente di abilitare o disabilitare i componenti personalizzati o i componenti predefiniti non elencati nella barra laterale.

* Anteprima: consente di visualizzare in anteprima come si presenterà la comunicazione interattiva quando verrà pubblicata.
