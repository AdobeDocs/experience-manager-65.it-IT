---
title: Testi nelle comunicazioni interattive
description: 'Creazione e modifica di frammenti di documenti di testo da utilizzare nelle comunicazioni interattive: il testo è uno dei quattro tipi di frammenti di documenti utilizzati per creare le comunicazioni interattive. Gli altri tre sono condizioni, elenchi e frammenti di layout.  '
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: b8e84c5d-2ec8-4575-9eed-6b37b04e5d66
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2474'
ht-degree: 1%

---

# Testi nelle comunicazioni interattive{#texts-in-interactive-communications}

## Panoramica {#overview}

Un frammento di documento di testo è costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico. Un paragrafo dinamico può contenere proprietà e variabili del modello di dati del modulo. È inoltre possibile applicare regole e ripetere all’interno di un frammento di documento di testo. Ad esempio, il nome del cliente in una formula di apertura potrebbe essere una proprietà FDM (Form Data Model) con il relativo valore reso disponibile in fase di esecuzione. Modificando questi valori, la stessa comunicazione interattiva può essere utilizzata per preparare la comunicazione interattiva per clienti diversi utilizzando l’interfaccia utente dell’agente.

Il frammento di documento di testo nella comunicazione interattiva supporta il seguente tipo di dati dinamici:

* **Oggetti modello dati**: le proprietà dei dati utilizzano un’origine dati back-end.
* **Contenuto basato su regole**: parti di contenuto in un testo che vengono visualizzate o nascoste in base a una regola. Una regola può anche essere basata sulle proprietà e le variabili del modello di dati del modulo.
* **Variabili**: nel frammento di documento di testo, le variabili non sono associate a un’origine dati back-end. L’agente inserisce/seleziona i valori nelle variabili o associa le variabili alle origini dati durante la preparazione della comunicazione interattiva per l’invio a un processo post.
* **Ripeti**: nella comunicazione interattiva potrebbero essere presenti informazioni dinamiche, ad esempio transazioni in un estratto conto relativo a una carta di credito, il cui numero di occorrenze potrebbe continuare a cambiare con ogni comunicazione interattiva generata. Utilizzando la funzione di ripetizione è possibile formattare e strutturare tali informazioni dinamiche. Per ulteriori informazioni, consulta [Condizione in linea e ripetizione](https://helpx.adobe.com/experience-manager/6-3/forms/using/cm-inline-condition.html).

## Crea testo {#createtext}

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.
1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Testo]**.
1. Specifica le seguenti informazioni:

   * **[!UICONTROL Titolo]**: (Facoltativo) immetti il titolo del frammento di documento di testo. I titoli non devono necessariamente essere univoci e possono contenere caratteri speciali e non inglesi. I testi sono indicati dai rispettivi titoli (se disponibili), ad esempio nelle miniature e nelle proprietà.
   * **[!UICONTROL Nome]**: nome univoco del testo all’interno di una cartella. In una cartella non possono esistere due frammenti di documento (testo, condizione o elenco) con lo stesso nome. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini in lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti da trattini nel campo Nome. Anche se il valore nel campo Titolo viene copiato automaticamente nel Nome, è possibile modificarlo.

   * **[!UICONTROL Descrizione]**: digita una descrizione del testo.
   * **[!UICONTROL Modello dati modulo]**: se necessario, seleziona il pulsante di opzione Modello dati modulo per creare il testo basato su un modello dati modulo. Quando selezioni il pulsante di opzione Modello dati modulo, **[!UICONTROL Modello dati modulo]** viene visualizzato. Sfoglia e seleziona un modello di dati del modulo. Durante la creazione di testo e condizione per una comunicazione interattiva, accertati di utilizzare lo stesso modello di dati che intendi utilizzare nella comunicazione interattiva. Per ulteriori informazioni sul modello dati modulo, consulta [Integrazione dei dati](/help/forms/using/data-integration.md).

   * **[!UICONTROL Tag]**: facoltativamente, per creare un tag personalizzato, immetti il valore nel campo di testo e premi Invio. Quando salvi questo testo, vengono creati i nuovi tag aggiunti.

1. Seleziona **[!UICONTROL Avanti]**.

   Viene visualizzata la pagina Crea testo. Se si è scelto di creare un testo basato su modello di dati modulo, le proprietà del modello di dati modulo vengono visualizzate nel riquadro sinistro.

1. Digita il testo e utilizza le seguenti opzioni per formattare, condizionare e inserire nel testo le proprietà e le variabili del modello dati del modulo:

   * [Modello dati modulo](#formdatamodel)
   * [Variabili](#variables)
   * [Editor regole](#rules)
   * [Opzioni di formattazione](#formatting)

      * [Copia e incolla testo formattato da altre applicazioni](#paste)

      * [Evidenzia parti di testo](#highlight)

   * [Ripeti](/help/forms/using/cm-inline-condition.md)
   * [Caratteri speciali](#special)
   * [Ricerca e sostituzione di testo](#searching)
   * [Scelte rapide da tastiera](/help/forms/using/keyboard-shortcuts.md)

   >[!NOTE]
   >
   >Puoi aggiungere elementi del modello dati modulo, elementi del dizionario dati e variabili utilizzando il simbolo @ nell’editor di testo. Quando immetti una stringa preceduta da @ nell’editor di testo, vengono cercati tutti gli elementi del modello dati, gli elementi e le variabili del dizionario dati e vengono visualizzati gli elementi o le variabili contenenti la stringa cercata. Puoi spostarti tra i risultati della ricerca e selezionare un elemento o una variabile. Se non viene restituito alcun risultato corrispondente, la *Nessun risultato corrispondente trovato* viene visualizzato il messaggio.

1. Seleziona **[!UICONTROL Salva]**.

   Il testo viene creato. Ora puoi utilizzare il testo come blocco predefinito durante la creazione di una comunicazione interattiva.

## Modifica testo {#edittext}

Per modificare un frammento di documento di testo esistente, segui la procedura riportata di seguito. Puoi anche scegliere di modificare un frammento di documento di testo dall’interno di un editor di comunicazione interattiva.

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti di documenti]**.
1. Passa a un frammento di documento di testo e selezionalo.
1. Seleziona **[!UICONTROL Modifica]**.
1. Apporta le modifiche necessarie. Per ulteriori informazioni sulle opzioni di testo, consulta [Crea testo](#createtext).
1. Seleziona **[!UICONTROL Salva]** e quindi seleziona **[!UICONTROL Chiudi]**.

## Personalizzazione di un frammento di documento di testo utilizzando le proprietà del modello di dati del modulo {#formdatamodel}

È possibile personalizzare frammenti di documenti di testo inserendo le proprietà del modello di dati del modulo. Inserendo le proprietà del modello dati modulo nel testo, è possibile recuperare e popolare dati specifici del destinatario dall’origine dati associata durante l’anteprima di una comunicazione interattiva. Per ulteriori informazioni sul modello dati del modulo, consulta [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

Se è stato specificato un modello dati modulo durante la creazione di un testo, le proprietà nel modello dati modulo vengono visualizzate nel riquadro sinistro dell&#39;editor di testo. Il modello dati del modulo specificato deve essere lo stesso per il frammento del documento di testo e la comunicazione interattiva che lo include.

![insertfdmelementtext](assets/insertfdmelementtext.png)

* Per inserire una proprietà del modello dati del modulo nel testo, posiziona il cursore nel punto in cui desideri inserire la proprietà, quindi seleziona la **[A]** nel riquadro a sinistra toccandolo e selezionando **[!UICONTROL [B] Aggiungi selezionati]**. Puoi anche selezionare due volte la proprietà per inserirla nella **[C]** posizione del cursore. Le proprietà del modello dati modulo vengono evidenziate con un colore di sfondo bruno.

In alternativa, è possibile cercare e aggiungere la proprietà del modello dati del modulo utilizzando il simbolo @ nell’editor di testo. Posizionare il cursore nel punto in cui si desidera inserire la proprietà. Digita @ seguito dalla stringa di ricerca. L’operazione di ricerca viene eseguita su tutte le proprietà e le variabili del modello dati del modulo disponibili nel frammento di documento. Le proprietà o le variabili contenenti la stringa di ricerca vengono recuperate e visualizzate come elenco a discesa. Spostarsi tra i risultati della ricerca e fare clic sulla proprietà che si desidera inserire nella posizione del cursore. Premere ESC per nascondere i risultati della ricerca.

* Per consentire agli agenti di modificare il valore della proprietà del modello dati di un modulo nell’interfaccia utente dell’agente durante [Prepara e invia comunicazione interattiva](/help/forms/using/prepare-send-interactive-communication.md) utilizzando l’interfaccia utente dell’agente, seleziona **[D]** blocca l’icona per quella proprietà e assicurati che sia in stato sbloccato. Lo stato predefinito della proprietà è bloccato e un agente non può modificare la proprietà nell’interfaccia utente agente.

È inoltre possibile utilizzare le proprietà del modello dati modulo per creare regole per visualizzare o nascondere parti del contenuto. Per ulteriori informazioni, consulta [Creare regole nel testo](#rules).

## Creazione e utilizzo di variabili in un frammento di documento di testo {#variables}

Le variabili sono segnaposto che possono essere associati durante la creazione di una comunicazione interattiva. Le variabili possono essere associate a una proprietà del modello di dati del modulo o a un frammento di testo. È inoltre possibile lasciare variabili da compilare per l’agente.

È possibile utilizzare le variabili al posto delle proprietà del modello dati del modulo quando:

* Un frammento di documento di testo deve essere utilizzato in più comunicazioni interattive in cui l’associazione deve essere diversa per le diverse comunicazioni interattive.
* Il frammento di documento di testo non dispone di un modello dati modulo al momento della creazione. È possibile inserire variabili e successivamente associarle alle proprietà del modello di dati del modulo al momento della creazione della comunicazione interattiva.
* È necessario associare e recuperare il testo da un frammento di documento di testo. Solo i frammenti di documenti di testo che possono essere associati a variabili non devono avere variabili in.

Durante la creazione o la modifica di un frammento di documento di testo, è possibile creare e inserire variabili. Le variabili create vengono visualizzate nella scheda Dati dell’interfaccia utente dell’agente. L&#39;agente specifica i valori per le variabili mentre [Preparare e inviare comunicazioni interattive tramite l’interfaccia utente dell’agente](/help/forms/using/prepare-send-interactive-communication.md).

### Creare le variabili {#createvariables}

1. Nel riquadro a sinistra, seleziona **[!UICONTROL Variabili]**.

   Viene visualizzato il riquadro Variabili.

   ![variablespane](assets/variablespane.png)

1. Seleziona **[!UICONTROL Crea]**.

   Viene visualizzato il riquadro Crea variabili.

1. Immetti le seguenti informazioni e seleziona **[!UICONTROL Crea]**:

   * **[!UICONTROL Nome]** : nome della variabile.
   * **[!UICONTROL Descrizione]** : facoltativamente, inserisci una descrizione della variabile.
   * **[!UICONTROL Tipo]** : seleziona un tipo di variabile: String, Number, Boolean o Date.
   * **[!UICONTROL Consenti solo valori specifici]** : per le variabili String e Number, puoi fare in modo che l’agente scelga uno specifico set di valori per un segnaposto nell’interfaccia utente dell’agente. Per specificare il set di valori, seleziona questa opzione e quindi specifica i valori separati da virgola consentiti nella **[!UICONTROL Valori]** campo.

1. Seleziona **[!UICONTROL Crea]**.

   La variabile viene creata ed elencata nel riquadro Variabili.

1. Per inserire una variabile nel testo, posiziona il cursore nella posizione appropriata, seleziona la variabile e seleziona **[!UICONTROL Aggiungi selezionati]**.

   ![variableinserted](assets/variableinserted.png)

   Le variabili vengono evidenziate con un colore di sfondo blu chiaro, mentre le proprietà del modello di dati del modulo vengono evidenziate con un colore bruno.

   In alternativa, è possibile cercare e aggiungere variabili utilizzando il simbolo @ nell’editor di testo. Posizionare il cursore nel punto in cui si desidera inserire la variabile. Digita @ seguito dalla stringa di ricerca. L’operazione di ricerca viene eseguita su tutte le proprietà e le variabili del modello dati del modulo disponibili nel frammento di documento. Le proprietà e le variabili contenenti la stringa di ricerca vengono recuperate e visualizzate come elenco a discesa. Spostarsi tra i risultati della ricerca e fare clic sulla variabile che si desidera inserire nella posizione del cursore. Premere ESC per nascondere i risultati della ricerca.

1. Seleziona **[!UICONTROL Salva]**.

## Creare regole nel testo {#rules}

Utilizzando l’editor di regole in un testo, puoi creare regole per visualizzare o nascondere stringhe di testo o parti di contenuto in base a **condizioni preimpostate**. Queste condizioni possono essere costruite in base a:

* Stringhe
* Numeri
* Espressione matematica
* Date
* Proprietà del modello dati modulo associato
* Eventuali variabili create nel testo

### Creare regole nel testo {#create-rules-in-text}

1. Durante la creazione o la modifica di un testo, seleziona la stringa di testo, il paragrafo o il contenuto che desideri rendere condizionale utilizzando la regola.

   ![selectcontentapplyrule](assets/selectcontentapplyrule.png)

1. Seleziona **[!UICONTROL Crea regola]**.

   Viene visualizzata la finestra di dialogo Crea regola. Oltre a stringa, numero, espressione matematica e data, nell’Editor regole sono disponibili anche le seguenti opzioni per la creazione di istruzioni delle regole:

   * Proprietà del modello dati modulo associato
   * Eventuali variabili create

   Seleziona l’opzione appropriata da valutare.

   ![editor di regole](assets/ruleeditor.png) ![ruleeditorfdm](assets/ruleeditorfdm.png)

   >[!NOTE]
   >
   >La proprietà Collection non è supportata per la creazione di regole per la condizionalizzazione e la visualizzazione del testo.

1. Selezionare l&#39;operatore appropriato per valutare la regola, ad esempio È uguale a, Contiene e Inizia con.

   ![ruleeditorfdm-1](assets/ruleeditorfdm-1.png)

1. Inserisci l’espressione di valutazione, il valore, la proprietà del modello dati o la variabile.

   ![Regola per visualizzare il testo selezionato se la posizione del destinatario è US in base ai dati di origine di FDM](assets/ruleeditorfdm-1-1.png)

   Regola per visualizzare il testo selezionato se la posizione del destinatario è US in base ai dati di origine di FDM

   * Durante la creazione o la modifica di una regola, puoi anche selezionare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola/Modifica regola. La finestra di dialogo espansa a finestra intera consente di trascinare e rilasciare le proprietà e le variabili del modello di dati del modulo per creare regole. Seleziona Ridimensiona di nuovo per tornare alla finestra di dialogo Crea regola.
   * Puoi anche creare più condizioni in una regola.
   * Puoi anche creare regole di sovrapposizione, in cui una regola viene applicata a una parte di un contenuto a cui è già stata applicata una regola.

1. Seleziona **[!UICONTROL Fine]**.

   La regola viene applicata. Il testo o il contenuto a cui viene applicata la regola viene evidenziato in verde. Quando passi il cursore del mouse sulla maniglia sinistra dell’evidenziazione, viene visualizzata la regola applicata.

   ![appliedruletext](assets/appliedruletext.png)

   Facendo clic sul quadratino di ridimensionamento sinistro della regola applicata, si ottengono le opzioni per modificare o rimuovere la regola.

## Formattazione del testo {#formatting}

Durante la creazione o la modifica del testo, la barra degli strumenti cambia a seconda del tipo di modifiche che si sceglie di apportare: Paragrafo, Allineamento o Elenco:

![Seleziona tipo di barra degli strumenti](do-not-localize/toolbarselection.png)

Seleziona il tipo di barra degli strumenti: Paragrafo, Allineamento o Elenco

![Barra degli strumenti di modifica dei caratteri](do-not-localize/paragraphtoolbar.png)

Barra degli strumenti di modifica dei caratteri

![Barra degli strumenti Allineamento](assets/alignmenttoolbar.png)

Barra degli strumenti Allineamento

![Barra degli strumenti Elenco](do-not-localize/listingtoolbar.png)

Barra degli strumenti Elenco

### Evidenzia/evidenzia parti di testo {#highlight}

Per evidenziare/enfatizzare parti di testo in un frammento di documento modificabile, selezionate il testo e selezionate Colore evidenziazione.

![textbackgroundcolorapply-1](assets/textbackgroundcolorapplied-1.png)

È possibile selezionare direttamente un colore di base `**[A]**` presente nella palette Colori di base o selezionare **Seleziona** dopo aver utilizzato il dispositivo di scorrimento `**[B]**` per scegliere la tonalità appropriata del colore.

Se necessario, è anche possibile passare alla scheda Avanzate per selezionare la tonalità, la luminosità e la saturazione appropriate `**[C]**` per creare il colore preciso e selezionare Seleziona `**[D]**` per applicare il colore per evidenziare il testo.

![textbackgroundcolor-2](assets/textbackgroundcolor-2.png)

### Incolla testo formattato {#paste}

Per riutilizzare uno o più paragrafi di testo esistenti in un&#39;altra applicazione, ad esempio da pagine Microsoft® Word o HTML, copiare e incollare il testo nell&#39;editor di testo. La formattazione del testo copiato viene mantenuta nell’editor di testo.

È possibile copiare e incollare uno o più paragrafi di testo in un frammento di documento di testo modificabile. È possibile, ad esempio, disporre di un documento di Microsoft® Word con un elenco puntato di prove di residenza accettabili, ad esempio:

![pastetextmsword-2](assets/pastetextmsword-2.png)

È possibile copiare e incollare direttamente il testo dal documento di Microsoft® Word in un frammento di documento di testo modificabile. La formattazione, ad esempio elenco puntato, carattere e colore del testo, viene mantenuta nel frammento del documento di testo.

![pastetexteditablemodule-1](assets/pastetexteditablemodule-1.png)

>[!NOTE]
>
>La formattazione del testo incollato, tuttavia, presenta alcune [limitazioni](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

## Inserisci caratteri speciali nel testo {#special}

Se necessario, inserisci caratteri speciali nel frammento del documento. Ad esempio, è possibile utilizzare la tavolozza Caratteri speciali per inserire:

* Simboli di valuta come €,¥ e £
* Simboli matematici come ∑, √, ∂ e ^
* Simboli di punteggiatura come ‟ e &quot;

![caratteri speciali-2](assets/specialcharacters-2.png)

L’editor di testo supporta 210 caratteri speciali. L’amministratore può [aggiungi supporto per caratteri speciali aggiuntivi/personalizzati tramite personalizzazione](/help/forms/using/custom-special-characters.md).

## Ricerca e sostituzione di testo {#searching}

Quando si utilizzano frammenti di documenti di testo contenenti una grande quantità di testo, è necessario cercare una stringa di testo specifica. Potrebbe inoltre essere necessario sostituire una stringa di testo specifica con una stringa alternativa.

La funzione Trova e sostituisci consente di cercare (e sostituire) qualsiasi stringa di testo in un frammento di documento di testo. La funzione include anche una potente ricerca di espressioni regolari.

1. Apri un frammento di documento di testo per [modifica](#edittext).
1. Seleziona **[!UICONTROL Trova e sostituisci]**.

1. Immettere il testo da cercare in **[!UICONTROL Trova]** e il nuovo testo (testo sostitutivo) nella **[!UICONTROL Sostituisci]** e selezionare **[!UICONTROL Sostituisci]**.

1. Se viene trovato il testo cercato, il testo viene sostituito dal testo sostitutivo.

   * Se viene trovata un’altra istanza del testo di ricerca, tale istanza viene evidenziata nel frammento del documento di testo. Se si seleziona **[!UICONTROL Sostituisci]** di nuovo, l&#39;istanza evidenziata viene sostituita e il cursore si sposta in avanti, se viene trovata una terza istanza.
   * Se non viene trovata un’altra istanza, nella finestra di dialogo Trova e sostituisci viene visualizzato il messaggio Fine del modulo.

   Puoi anche selezionare Sostituisci tutto per sostituire tutte le corrispondenze in una sola volta.

   La funzione Trova e sostituisci include anche una ricerca avanzata delle espressioni regolari. Per usare regex nella ricerca, seleziona **[!UICONTROL Reg eseg]** e quindi seleziona **[!UICONTROL Trova]** o **[!UICONTROL Sostituisci]**.
