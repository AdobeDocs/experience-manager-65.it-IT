---
title: Frammenti di documenti in AEM
description: I frammenti di documento, ad esempio Testo, elenchi, condizioni e frammenti di layout, in Gestione corrispondenza consentono di formare i componenti statici, dinamici e ripetibili della corrispondenza con i clienti.
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
exl-id: 71754e41-45d7-4cc5-ba49-0748bd51c0cf
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '6905'
ht-degree: 0%

---

# Frammenti del documento{#document-fragments}

## Frammenti del documento {#document-fragments-1}

I frammenti di documento sono parti/componenti riutilizzabili di una corrispondenza mediante le quali è possibile comporre lettere/corrispondenza. I frammenti di documento sono dei seguenti tipi:

* **Testo**: una risorsa di testo è un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico.
* **Elenco**: l&#39;elenco è un gruppo di frammenti di documenti, inclusi testo, elenchi, condizioni e immagini. L’ordine degli elementi dell’elenco può essere fisso o modificabile. Durante la creazione di una lettera, potete utilizzare alcuni o tutti gli elementi dell&#39;elenco per replicare un pattern di elementi riutilizzabile.
* **Condizione**: le condizioni ti consentono di definire quale contenuto viene incluso al momento della creazione della corrispondenza, in base ai dati forniti. La condizione è descritta in termini di variabili di controllo. Una variabile di controllo può essere un elemento del dizionario dati o un segnaposto.
* **Frammento layout**: un frammento layout è un layout che può essere utilizzato con una o più lettere. Un frammento di layout viene utilizzato per creare pattern ripetibili, in particolare tabelle dinamiche. Il layout può contenere campi modulo tipici come &quot;Indirizzo&quot; e &quot;Numero di riferimento&quot;. Contiene anche sottomoduli vuoti che denotano le aree di destinazione. I layout (XDP) vengono creati in Designer e quindi caricati in AEM Forms.

## Testo {#text}

Una risorsa di testo è un contenuto costituito da uno o più paragrafi di testo. Un paragrafo può essere statico o dinamico. Un paragrafo dinamico contiene riferimenti a elementi dati, i cui valori vengono forniti in fase di esecuzione. Ad esempio, il nome del cliente nella formula di apertura di una lettera potrebbe essere un elemento dati dinamico, con il relativo valore reso disponibile in fase di esecuzione. Modificando questi valori, lo stesso modello di lettera può essere utilizzato per generare lettere per clienti diversi.

La soluzione di gestione della corrispondenza supporta due tipi di elementi di dati dinamici (dati variabili):

* **Elementi del dizionario dati**: questi elementi sono associati al dizionario dati e ottengono i loro valori dall&#39;origine dati fornita. Una variabile del dizionario dati può essere protetta o non protetta. Durante la creazione di corrispondenza, l’utente può modificare il valore predefinito delle variabili del dizionario dati non protette, ma non può modificare quelle protette.
* **Segnaposto**: si tratta di variabili non associate a un&#39;origine dati back-end. Richiedono all’utente di compilare un valore durante la creazione di corrispondenza. Per impostazione predefinita, i segnaposto non sono protetti.

>[!NOTE]
>
>I modelli di Gestione della corrispondenza non forzano la creazione di nomi univoci durante la creazione di segnaposto. Se si creano due segnaposto con lo stesso nome, ad esempio un testo e una condizione, e li si utilizzano entrambi in un modello di lettera, i valori dell&#39;ultimo segnaposto inserito vengono utilizzati per entrambi i segnaposto. Se due segnaposto hanno lo stesso nome, i relativi tipi vengono confrontati. Se i tipi sono diversi, il relativo tipo diventa String. All’interno di un modulo, tuttavia, non è possibile creare più segnaposto con lo stesso nome.

### Crea testo {#create-text}

1. Seleziona **Forms** > **Frammenti di documento**.
1. Seleziona **Crea** > **Testo** oppure seleziona una risorsa di testo e seleziona **Modifica**.
1. Specificare le seguenti informazioni per il testo:

   * **Titolo: (facoltativo)** Inserisci il titolo della risorsa di testo. I titoli non devono necessariamente essere univoci e possono contenere caratteri speciali e non inglesi. I testi sono indicati dai rispettivi titoli (se disponibili), ad esempio nelle miniature e nelle proprietà della risorsa.
   * **Nome:** il nome univoco della risorsa di testo. Non possono esistere due risorse (testo, condizione o elenco) in nessuno stato con lo stesso nome. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini in lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti da trattini nel campo Nome. Anche se il valore nel campo Titolo viene copiato automaticamente nel Nome, è possibile modificarlo.
   * **Descrizione**: digita una descrizione della risorsa.
   * **Dizionario dati**: è possibile selezionare il dizionario dati in cui eseguire il mapping. Questo attributo consente di aggiungere riferimenti agli elementi del dizionario dati nella risorsa di testo.
   * **Tag**: facoltativamente, per creare un tag personalizzato immettere il valore nel campo di testo e premere Invio. Puoi visualizzare il tag sotto il campo di testo dei tag. Quando salvi questo testo, vengono creati anche i nuovi tag aggiunti.

1. Seleziona **Avanti**. Gestione corrispondenza visualizza la pagina Editor in cui è possibile aggiungere paragrafi di testo ed elementi dati al testo.

   Il correttore ortografico predefinito nel browser controlla l&#39;ortografia nell&#39;editor di testo. Per gestire il controllo ortografico e grammaticale, è possibile modificare le impostazioni del correttore ortografico del browser oppure installare i plug-in e gli add-on del browser per il controllo ortografico e grammaticale.

   È inoltre possibile utilizzare le varie scelte rapide da tastiera disponibili nell&#39;editor di testo per gestire, modificare e formattare il testo. Per ulteriori informazioni sulle scelte rapide da tastiera dell&#39;[Editor di testo](/help/forms/using/keyboard-shortcuts.md#p-formatting-p) in Scelte rapide da tastiera per Gestione corrispondenza.

1. Viene aperto un editor di testo, immettete il testo. Utilizza la barra degli strumenti nella parte superiore della pagina per formattare il testo, inserire condizioni, collegamenti e interruzioni di pagina.

   ![Barra degli strumenti](assets/advancedediting.png)

   * **Collegamento**: inserire il collegamento [ipertesto](#insert-hyperlink) nel testo.
   * **Ripeti**: ripeti stampa l&#39;elemento della raccolta nel dizionario dati utilizzando un delimitatore.
   * **Condizione**: selezionare per inserire una condizione. Inserisce testo in base alla condizione. Se la condizione è true, il testo è visibile nella lettera, altrimenti no.
   * **Aggiungi descrizione**: aggiungi un&#39;annotazione a un testo. Si tratta di metadati visibili all’autore, ma che non fanno parte della lettera creata.
   * **Interruzione di pagina**: se si imposta l&#39;attributo di interruzione di pagina di un modulo di testo su false, il modulo di testo non si interrompe tra le pagine.

   Viene aperto un editor di testo. Immettere il testo. La barra degli strumenti cambia a seconda del tipo di modifiche che si sceglie di apportare: Paragrafo, Allineamento o Elenco:

   ![Seleziona tipo di barra degli strumenti](assets/toolbarselection.png)

   Seleziona il tipo di barra degli strumenti: Paragrafo, Allineamento o Elenco

   ![Barra degli strumenti paragrafo](assets/fonteditingtoolbar.png)

   Barra degli strumenti Paragrafo
   [![Barra degli strumenti di allineamento](assets/paragrapheditingtoolbar.png)](assets/paragrapheditingtoolbar-1.png)Barra degli strumenti di allineamento

   ![Barra degli strumenti delle inserzioni](assets/bulleteditingtoolbar.png)

   Barra degli strumenti dell’inserzione (fai clic per aprire un’immagine di dimensioni reali)

1. Per riutilizzare uno o più paragrafi di testo esistenti in un&#39;altra applicazione, ad esempio da pagine di MS Word o HTML, copiare e incollare il testo nell&#39;editor di testo. La formattazione del testo copiato viene mantenuta nell’editor di testo.

   È possibile copiare e incollare uno o più paragrafi di testo in un modulo di testo modificabile. Ad esempio, è possibile disporre di un documento di MS Word con un elenco puntato di prove di residenza accettabili come:

   ![pastetextmsword-1](assets/pastetextmsword-1.png)

   È possibile copiare e incollare direttamente il testo dal documento di MS Word in un modulo di testo modificabile. Nel modulo di testo viene mantenuta la formattazione come elenco puntato, carattere e colore del testo.

   ![pastetexttextmodule](assets/pastetexttextmodule.png)

   >[!NOTE]
   >
   >La formattazione del testo incollato presenta tuttavia alcune [limitazioni](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

1. Se necessario, inserisci caratteri speciali nel frammento del documento. Ad esempio, è possibile utilizzare la tavolozza Caratteri speciali per inserire:

   * Simboli di valuta come €,¥ e £
   * Simboli matematici come ∑, √, ∂ e ^
   * Simboli di punteggiatura come ‟ e &quot;

   ![caratteri speciali-1](assets/specialcharacters-1.png)

   Gestione della corrispondenza supporta 210 caratteri speciali. L&#39;amministratore può [aggiungere il supporto di caratteri speciali aggiuntivi/personalizzati tramite personalizzazione](/help/forms/using/custom-special-characters.md).

1. Per evidenziare/enfatizzare parti di testo in un modulo inline modificabile, selezionate il testo e selezionate Colore evidenziazione.

   ![textbackgroundcolorapply](assets/textbackgroundcolorapplied.png)

   È possibile selezionare direttamente un colore di base `**[A]**` presente nella tavolozza Colori di base oppure selezionare **Seleziona** dopo aver utilizzato il cursore `**[B]**` per scegliere la tonalità appropriata del colore.

   Se necessario, è anche possibile passare alla scheda Avanzate per selezionare la tonalità, la luminosità e la saturazione `**[C]**` appropriate per creare il colore preciso, quindi selezionare Seleziona `**[D]**` per applicare il colore per evidenziare il testo.

   ![textbackgroundcolor-1](assets/textbackgroundcolor-1.png)

1. Dal pannello dati, trascina gli elementi del dizionario dati e gli elementi segnaposto nel testo.

   A:

   * Aggiungere un elemento del dizionario dati nel testo, selezionare un elemento dati dall&#39;elenco, quindi selezionare Inserisci ( ![inserisci](assets/insert.png)). Se selezioni Protetto, l’elemento del dizionario dati è di sola lettura e viene visualizzato nell’editor di lettere, ma non nell’interfaccia utente Crea corrispondenza o Creatore corrispondenza.
   * Aggiungi un elemento segnaposto nel testo. Nel pannello Elementi dati, seleziona Crea nuovo, immetti i dettagli per il nuovo elemento dati e seleziona Crea per aggiungere il nuovo elemento all’elenco. Il nuovo segnaposto può essere inserito nel testo allo stesso modo dell’elemento del dizionario dati. Per modificare un segnaposto, selezionare un segnaposto e selezionare Modifica.

   ![Elementi segnaposto](assets/placeholder_elements_in_xmldata.png)

   Elementi segnaposto specificati nel file di dati di esempio di un dizionario dati

   ![Elementi segnaposto nella lettera](assets/placeholder_elements_in_text.png)

   Valori degli elementi segnaposto nella vista CCR compilati dalle variabili del dizionario dati come specificato nel file di dati di esempio

   Puoi anche utilizzare il simbolo @ per cercare e aggiungere elementi del dizionario dati e segnaposto all’editor di testo. Posizionare il cursore nel punto in cui si desidera inserire l&#39;elemento. Digita @ seguito dalla stringa di ricerca. L’editor di testo esegue l’operazione di ricerca su tutti gli elementi del dizionario dati e segnaposto disponibili nel frammento del documento di testo. L’operazione di ricerca recupera e visualizza gli elementi contenenti la stringa di ricerca come elenco a discesa. Spostarsi tra i risultati della ricerca e fare clic sull&#39;elemento che si desidera inserire nella posizione del cursore. Premere ESC per nascondere i risultati della ricerca.

1. È possibile utilizzare condizioni in linea e ripetere per rendere la lettera altamente contestuale e ben strutturata. Per ulteriori informazioni sulla condizione in linea e la ripetizione, vedere [Condizioni in linea e ripetizione in lettere](/help/forms/using/cm-inline-condition.md).
1. Seleziona **Salva**.

#### Inserire un collegamento ipertestuale in un testo {#insert-hyperlink}

Per creare un collegamento ipertestuale in una risorsa di testo, effettua le seguenti operazioni:

1. Seleziona il testo o l’oggetto modello dati nell’editor di testo.

2. Seleziona **[!UICONTROL Collegamento]**. Selezionare il campo **[!UICONTROL Testo alternativo]** per rimuovere il testo o il nome dell&#39;oggetto modello dati esistente.

3. Specifica l&#39;URL e seleziona ![Salva](assets/save_icon.svg).

![Crea collegamento ipertestuale nella risorsa di testo](assets/text-create-hyperlink.png)

#### Ricerca e sostituzione di testo {#searching-and-replacing-text}

Quando si utilizzano elementi di testo contenenti un corpo di testo di grandi dimensioni, è necessario cercare una stringa di testo specifica. Potrebbe inoltre essere necessario sostituire una stringa di testo specifica con una stringa alternativa.

La funzione Trova e sostituisci consente di cercare (e sostituire) qualsiasi stringa di testo in un elemento di testo. La funzione include anche una potente ricerca di espressioni regolari.

#### Per cercare testo in un modulo di testo {#to-search-text-in-a-text-module}

1. Apri il modulo di testo nell’editor di testo.

1. Selezionare Trova e sostituisci.
1. Immettere il testo da cercare nella casella di testo Trova e premere Trova. Il testo da cercare viene evidenziato nel modulo di testo.
1. Per cercare l&#39;istanza successiva del testo, premere nuovamente Trova.

   Se si continua a premere il pulsante Trova, la ricerca continua lungo la pagina. Dopo aver trovato l&#39;ultima istanza del testo, il messaggio **Raggiunta la fine del modulo** indica che non sono stati trovati altri risultati di ricerca.

   Tuttavia, se nel modulo di testo non viene trovata alcuna istanza del testo di ricerca, viene visualizzato il messaggio: **Corrispondenza non trovata**.

1. Se si preme di nuovo Trova, la ricerca continua nella parte superiore della pagina.

#### Opzioni di ricerca {#search-options}

**Rispetta maiuscole/minuscole:** La ricerca restituisce solo risultati con le stesse maiuscole/minuscole.

**Parola intera:** La ricerca restituisce solo parole intere.

>[!NOTE]
>
>Se si immettono caratteri speciali nella casella di testo Trova, l&#39;opzione Parola intera è disattivata.

**Reg ex:** Eseguire ricerche utilizzando espressioni regolari. Ad esempio, la seguente espressione regolare cerca gli indirizzi e-mail in un modulo di testo:

`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}`

#### Per cercare e sostituire il testo in un modulo di testo {#to-search-and-replace-text-in-a-text-module}

1. Apri il modulo di testo nell’editor di testo.
1. Selezionare Trova e sostituisci.
1. Immettere il testo da cercare nella casella Trova e il testo con cui sostituire il testo da cercare e premere Sostituisci.
1. Se viene trovato il testo da cercare, il testo viene sostituito dal testo Sostituisci.

   * Se viene trovata un’altra istanza del testo di ricerca, tale istanza viene evidenziata nel modulo di testo. Se si preme nuovamente Sostituisci, l&#39;istanza evidenziata viene sostituita e il cursore si sposta in avanti, se viene individuata una terza istanza.
   * Se non viene trovata un&#39;altra istanza, il cursore si arresta in corrispondenza dell&#39;ultima istanza sostituita.

1. Se si preme di nuovo Trova, la ricerca continua nella parte superiore della pagina.

   Utilizzare l&#39;opzione Sostituisci tutto per sostituire tutte le istanze di un testo nel modulo di testo. Quando si utilizza &quot;, il numero di sostituzioni viene visualizzato come messaggio nella finestra di dialogo Trova e sostituisci.

#### Best practice/suggerimenti per i moduli di testo {#best-practices-tips-and-tricks-for-text-modules}

* Utilizza una convenzione di denominazione coerente per evitare duplicazioni.
* Utilizza l’associazione appropriata del dizionario dati nei moduli di testo.
* Quando si utilizza l’Editor di testo quando si modifica una risorsa di testo, si applicano le seguenti regole:

   * **Aggiunta della variabile:** consentita
   * **Rimozione della variabile:** consentita
   * **Aggiornamento delle proprietà:** consentito
   * **Modifica del dizionario dati:** consentita fino a quando l&#39;elemento del dizionario dati non viene utilizzato. Non è possibile modificare il dizionario dati durante l&#39;aggiornamento.

## Elenco {#list}

Un elenco è un gruppo di frammenti di documenti, inclusi testo o altri elenchi, condizioni e immagini. L’ordine degli elementi dell’elenco può essere fisso o modificabile. Durante la creazione di una lettera, potete utilizzare alcuni o tutti gli elementi dell&#39;elenco per replicare un pattern di elementi riutilizzabile. Gli elenchi si comportano fondamentalmente come destinazioni che possono essere nidificate all’interno di altre destinazioni.

### Implementazione degli elenchi {#implementing-lists}

Gli elenchi di implementazione sono costituiti da due passaggi:

1. Definizione delle proprietà di base come nome, descrizione e dizionario dati.
1. Sezione di contenuto inclusa nell&#39;elenco e quindi impostazione di proprietà quali l&#39;ordine di blocco e l&#39;accesso alla raccolta per l&#39;elenco.

### Creare un elenco {#create-a-list}

Un elenco è un gruppo di contenuti correlati che è possibile utilizzare in un modello di lettera come singola unità. Qualsiasi tipo di contenuto può essere aggiunto a un elenco. È inoltre possibile nidificare gli elenchi. I moduli elenco possono essere specificati come:

* **ORDINATO**: impossibile modificare l&#39;ordine nel runtime di creazione corrispondenza.
* **Accesso libreria**: gli utenti possono aggiungere moduli all&#39;elenco. Questo flag specifica se l&#39;accesso alla libreria è abilitato. Se attivato (aperto), l’utente può aggiungere moduli all’elenco durante l’anteprima della lettera.
* Durante la creazione di un elenco, è possibile specificare un tipo, ad esempio:
* **Normale**: nessuna formattazione di stile aggiuntiva applicata all&#39;elenco.
* **Puntato**: elenco formattato con un punto elenco semplice.
* **Numerato**: un elenco numerico con la scelta delle cifre Standard (1,2,...), Upper Roman (I, II, ...) e Lower Roman (i, ii,...).
* **Lettered**: un elenco alfabetico con la scelta di lettere minuscole (a,b,...) e maiuscole (A,B,...).
* **Personalizzato**: puoi creare qualsiasi tipo numerato/lettera e valori di prefisso e suffisso a tua scelta.

1. Seleziona **Forms** > **Frammenti di documento**.

1. Selezionare **Crea** > **Elenco**.

1. Specificare le seguenti informazioni per l&#39;elenco:

   * **Titolo (facoltativo): immetti** il titolo dell&#39;elenco. Il titolo non deve necessariamente essere univoco e può contenere caratteri speciali e non inglesi. Gli elenchi sono indicati dai relativi titoli (se disponibili), ad esempio nelle miniature e nelle proprietà della risorsa.
   * **Nome:** Il nome univoco dell&#39;elenco. Non possono esistere due risorse (testo, condizione o elenco) in nessuno stato con lo stesso nome. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini in lingua inglese. Nel campo Nome viene inserito automaticamente il valore specificato nel campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti da trattini nel campo Nome. Anche se il valore nel campo Titolo viene copiato automaticamente nel Nome, è possibile modificarlo.
   * **Descrizione (facoltativo)**: digitare una descrizione della risorsa.
   * **Dizionario dati (facoltativo)**: è possibile selezionare il dizionario dati a cui connettersi. È possibile aggiungere all’elenco solo le risorse che utilizzano lo stesso dizionario dati dell’elenco, oppure le risorse a cui non è assegnato alcun dizionario dati. L’assegnazione di un dizionario dati a un elenco semplifica la ricerca dell’elenco appropriato da parte di chi crea un modello di lettera.
   * **Tag (facoltativo)**: selezionare i tag da applicare. Puoi anche digitare il nome di un nuovo tag e crearlo. Il nuovo tag viene creato quando si seleziona **Salva**.

1. Seleziona **Avanti**.
1. Seleziona **Aggiungi risorsa**.
1. Per aggiungere risorse all&#39;elenco, selezionale nella pagina Seleziona Assets e seleziona **Fine**.

   ![Selezionare le risorse da aggiungere all&#39;elenco](assets/selectassets.png)

1. Le risorse vengono aggiunte alla pagina Elementi di elenco.
Per modificare l&#39;ordine delle risorse all&#39;interno dell&#39;elenco, seleziona e tieni premuto l&#39;icona delle frecce ( ![trascinamento](assets/dragndrop.png) ) e trascina. Quando l’utente apre un modello di lettera nell’interfaccia utente Crea corrispondenza, il contenuto viene assemblato nell’ordine definito qui.

   ![Riordinare e configurare le risorse in un elenco](assets/listitems.png)

1. Per specificare il comportamento dell’elenco nell’interfaccia utente di CCR, puoi selezionare le seguenti opzioni:

   * **Accesso alla libreria**: per abilitare l&#39;accesso alla libreria per l&#39;aggiunta di risorse, selezionare Accesso alla libreria. Quando Accesso libreria è abilitato, il perito di verifica delle attestazioni può aggiungere più contenuto all&#39;elenco. In caso contrario, l&#39;Adattatore richieste di rimborso è limitato al contenuto definito per l&#39;elenco.
   * **Blocca ordine**: per bloccare l&#39;ordine delle risorse nell&#39;elenco in modo che l&#39;Aggiustatore richieste di rimborso non possa modificarlo, selezionare Blocca ordine. Se non si seleziona questa opzione, l&#39;Aggiustatore richieste di rimborso può modificare l&#39;ordine delle voci di elenco.

   * **Aggiungi punti elenco**: utilizza questa opzione per applicare al modulo uno stile di punto elenco o di numerazione. È possibile utilizzare uno stile di elenco predefinito o personalizzato. È inoltre possibile specificare il testo da visualizzare prima e dopo ogni voce dell&#39;elenco.
   * **Interruzione di pagina**: selezionare questa opzione ( ![interruzione](assets/break.png)) per aggiungere un&#39;interruzione di pagina tra i contenuti dell&#39;elenco. Se questa opzione non è selezionata ( ![nobreak](assets/nobreak.png)), se il contenuto dell&#39;elenco viene riportato alla pagina successiva, l&#39;intero elenco viene spostato alla pagina successiva invece di essere interrotto nella pagina tra le due.

   * **Configurazione assegnazione**: utilizzare questa opzione per specificare il numero minimo e massimo di risorse che è possibile aggiungere all&#39;elenco.

1. Per specificare il comportamento di ciascuna risorsa nell’elenco in fase di esecuzione, puoi selezionare le seguenti opzioni:

   * **Modificabile:** Quando questa opzione è selezionata, il contenuto può essere modificato nell&#39;interfaccia utente Crea corrispondenza. Questa opzione non è disponibile per i moduli Elenco e Immagine.
   * **Obbligatorio:** Quando questa opzione è selezionata, il contenuto è richiesto nell&#39;interfaccia utente Crea corrispondenza.
   * **Selezionato:** Quando questa opzione è selezionata, il contenuto viene preselezionato nell&#39;interfaccia utente Crea corrispondenza.
   * **Ignora stile:** Quando questa opzione è selezionata, il contenuto ignora i punti elenco e la numerazione nell&#39;interfaccia utente Crea corrispondenza. Questa opzione non è disponibile per i moduli Immagine. Inoltre, tra Skip Style (Ignora stile), Compound (Composto) e Ignore List Style (Ignora stile elenco), a un modulo è possibile applicare solo una delle opzioni. È possibile utilizzare una di queste opzioni per un modulo selezionando Aggiungi punti elenco per un modulo.)
   * **Rientro:** È possibile modificare il livello di rientro di ogni modulo/contenuto selezionato come parte dell&#39;elenco. Il rientro è specificato in termini di livelli (a partire da zero), in modo che ogni livello di rientro corrisponda a una spaziatura di 36 punti.
   * **Composto:** Se selezionata, la numerazione composta viene applicata come combinazione dello stile dell&#39;elenco esterno (padre) e del relativo stile. La numerazione composta di questo elenco nidificato si basa sull&#39;ordine in cui l&#39;elenco nidificato viene visualizzato nell&#39;elenco esterno.
   * **Ignora stile elenco:** Se l&#39;opzione Numerazione composta è deselezionata, l&#39;opzione Ignora stile elenco è abilitata. Questa selezione ignora lo stile dell&#39;elenco nidificato e la numerazione continua dall&#39;elenco esterno. Pertanto, i moduli dell’elenco nidificato vengono trattati come parte dell’elenco esterno stesso, indipendentemente dagli stili specificati nell’elenco nidificato. Se l&#39;opzione Ignora stile elenco è deselezionata per un elenco nidificato, i moduli che fanno parte di tale elenco nidificato hanno il proprio stile di numerazione.
   * **Mantieni con successivo:** Imposta l&#39;interruzione di pagina per le risorse contenute in un elenco. Se imposti la proprietà Mantieni con successivo di una risorsa di un elenco su **Il**, la risorsa e quella successiva rimarranno sulla stessa pagina. Ciò significa che il contenuto della risorsa selezionata e della risorsa successiva non si suddivide tra le pagine.

1. Seleziona **Salva**.

### Best practice/suggerimenti {#best-practices-tips-and-tricks}

* Utilizza una convenzione di denominazione coerente per evitare duplicazioni.
* Utilizza associazione dizionario dati appropriata
* Quando si utilizza l’Editor elenco per modificare un elenco, si applicano le seguenti regole:

   * Aggiornamento delle proprietà: consentito
   * **Modifica del dizionario dati:** Consentita fino a quando non viene associato alcun elemento che utilizza il dizionario dati. Non è possibile modificare il dizionario dati durante l&#39;aggiornamento.

## Condizioni {#conditions}

Le condizioni ti consentono di definire quale contenuto viene incluso al momento della creazione di corrispondenza e lettere, in base ai dati forniti. La condizione è descritta in termini di variabili di controllo. Quando aggiungi una condizione, puoi scegliere di includere una risorsa in base al valore di cui dispone la variabile di controllo.

In base alle opzioni scelte, viene valutata solo la prima espressione che risulta true, in base alla variabile di condizione corrente, oppure tutte le condizioni. Quando si riempie la lettera in Create Correspondence (CCR), le condizioni si comportano come &quot;scatole bianche&quot;. Se una condizione genera un elenco, vengono generati tutti gli elementi obbligatori e preselezionati dell’elenco. Se uno di questi elementi è costituito da condizioni o elenchi, anche il contenuto risultante viene visualizzato in ordine di profondità, dall’alto verso il basso, come elenco semplice di contenuti di testo e immagini. I risultati della condizione possono essere di qualsiasi tipo (testo, elenco, condizione o immagine).

### Condizioni di attuazione {#implementing-conditions}

L&#39;editor delle condizioni include un&#39;interfaccia utente di [Generatore di espressioni](/help/forms/using/expression-builder.md) che supporta la creazione di espressioni utilizzando più segnaposto ed elementi del dizionario dati. In tali espressioni è possibile utilizzare operandi comuni e funzioni locali/globali. Ogni espressione può essere associata ad alcuni contenuti e, facoltativamente, potrebbe essere presente una sezione predefinita se nessuna delle espressioni restituisce true. Tutte le espressioni vengono valutate nella sequenza in cui sono definite e vengono selezionate le prime espressioni che restituiscono true e il relativo contenuto associato viene restituito da tale modulo condizionale.

Ad esempio, se il testo dei termini e delle condizioni in una lettera varia a seconda dello stato in cui si trova il cliente e il dizionario dati contiene un elemento denominato &quot;state&quot;, puoi aggiungere la condizione come segue:
* state = NY, selezionate il paragrafo di testo T&amp;C_NY
* state = NC, selezionate il paragrafo di testo T&amp;C_NC

L’editor delle condizioni consente di specificare una condizione predefinita. Se il valore delle variabili di controllo non corrisponde a nessuna delle condizioni, viene utilizzato il contenuto associato alla condizione predefinita. Seguendo l’esempio precedente, puoi aggiungere questa riga di condizione:
* Predefinito, seleziona T&amp;C_Rest

### Creare una condizione {#create-a-condition}

1. Seleziona **Forms** > **Frammenti di documento**.
1. Selezionare **Crea > Condizione**.
1. Specificare le seguenti informazioni per l&#39;elenco:

   * **Titolo (facoltativo):** Immettere il titolo per la condizione. Il titolo non deve necessariamente essere univoco e può contenere caratteri speciali e non inglesi. Le condizioni sono indicate dai relativi titoli (se disponibili), ad esempio nelle miniature e nelle proprietà della risorsa.
   * **Nome:** Il nome univoco della condizione. Non possono esistere due risorse (testo, condizione o elenco) in nessuno stato con lo stesso nome. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini in lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti da trattini nel campo Nome. Anche se il valore nel campo Titolo viene copiato automaticamente nel Nome, è possibile modificarlo.
   * **Descrizione (facoltativo)** Digitare una descrizione della condizione.
   * **Dizionario dati (facoltativo)**: è possibile selezionare il dizionario dati a cui connettersi. È possibile aggiungere all’elenco solo le risorse che utilizzano lo stesso dizionario dati della condizione, o le risorse a cui non è assegnato alcun dizionario dati. L’assegnazione di un dizionario dati a un elenco semplifica la ricerca della condizione appropriata da parte di chi crea un modello di lettera.
   * **Tag (facoltativo)**: è possibile selezionare i tag da applicare. Puoi anche digitare il nome di un nuovo tag e crearlo. Il nuovo tag viene creato quando si seleziona **Salva**.

1. Seleziona **Avanti**.
1. Seleziona **Aggiungi risorsa**.
1. Per aggiungere una risorsa alla condizione, selezionala nella pagina Seleziona Assets e seleziona **Fine**. Le risorse vengono aggiunte al riquadro Espressione.
1. Per specificare il comportamento della condizione in fase di esecuzione, è possibile selezionare le opzioni seguenti:

   * **Disabilita valutazione risultati multipli\Abilita valutazione risultati multipli**: quando questa opzione è abilitata (appare come &quot;Abilita più...&quot;), tutte le condizioni vengono valutate e il risultato è la somma di tutte le condizioni vere. Se questa opzione è disabilitata (appare come &quot;Disable Multiple...&quot;), solo la prima condizione che risulta essere true viene valutata e diventa l&#39;output della condizione.
   * **Interruzione di pagina**: seleziona questa opzione ( ![interruzione](assets/break.png)) per aggiungere un&#39;interruzione di pagina tra i moduli delle condizioni. Se questa opzione non è selezionata ( ![nobreak](assets/nobreak.png)), se una condizione sta per essere riportata alla pagina successiva, l&#39;intera condizione viene spostata alla pagina successiva invece di interrompere la pagina tra le condizioni.

1. Per modificare l&#39;ordine delle risorse all&#39;interno della condizione, seleziona e tieni premuto l&#39;icona delle frecce ( ![trascinamento](assets/dragndrop.png) ) e trascina. Quando l’utente apre un modello di lettera nell’interfaccia utente Crea corrispondenza, il contenuto viene assemblato nell’ordine definito qui.
1. Selezionare **Elimina** per eliminare la riga. Se selezioni Elimina per la riga predefinita, cancella solo le informazioni sulla risorsa.
1. Seleziona **Copia** per duplicare una riga.
1. Seleziona **Modifica** per modificare la risorsa o l&#39;espressione.

   Ulteriori informazioni:

   * Per aggiornare la risorsa, seleziona l’icona della cartella nella colonna Risorsa.
   * Per aprire il Generatore di espressioni e inserire un’espressione, seleziona l’icona della cartella nella colonna Espressione. Per ulteriori informazioni su Expression Builder, vedere [Expression Builder](/help/forms/using/expression-builder.md).

### Best practice/suggerimenti {#best-practices-tips-and-tricks-1}

* Utilizza una convenzione di denominazione coerente per semplificare la ricerca ed evitare duplicazioni.
* Le condizioni si comportano come le istruzioni di caso, pertanto l’ordine delle condizioni è importante. Viene restituita la prima corrispondenza.
* Utilizza associazione dizionario dati appropriata
* Quando si utilizza l’Editor condizioni per modificare una condizione, vengono applicate le seguenti regole:

   * **Aggiunta della variabile:** consentita
   * **Rimozione della variabile:** consentita
   * **Aggiornamento delle proprietà:** consentito
   * **Modifica del dizionario dati:** consentita fino a quando l&#39;elemento del dizionario dati non viene utilizzato.

## Frammenti di layout {#layoutfragments}

Un frammento di layout si basa su XDP creati in Designer. Per creare frammenti di layout, devi creare gli XDP e [caricarli in AEM Forms](/help/forms/using/import-export-forms-templates.md).

Uno o più frammenti di layout possono formare parti di una lettera e definire il layout grafico di tali parti. Un frammento di layout può contenere campi modulo tipici, come Indirizzo e Numero di riferimento, e sottomoduli vuoti che denotano aree di destinazione. I frammenti di layout consentono inoltre di creare tabelle e inserirle in lettere.

Un caso d’uso comune consiste nell’individuare pattern di layout riutilizzabili nelle lettere e creare frammenti di layout per tali pattern. Ad esempio, la formula di apertura, l&#39;indirizzo e la parte oggetto della lettera, che vengono visualizzate nello stesso ordine più lettere. Un altro esempio potrebbe essere una tabella con un numero simile di righe e colonne utilizzate in più lettere.

Puoi creare un frammento di layout basato su un XDP esistente. Un frammento di layout può essere costituito da campi e aree di destinazione o da una o più tabelle. Le tabelle di un layout possono essere statiche o dinamiche. Viene creato un XDP in Designer e [caricato in AEM Forms](/help/forms/using/import-export-forms-templates.md). Un XDP può formare la struttura di un frammento di layout o di una lettera. Ulteriori informazioni su [Progettazione layout](/help/forms/using/layout-design-details.md).

L’utilizzo di frammenti associati ad aree di destinazione consente di modificare la lettera al momento dell’authoring. È possibile creare un frammento di layout con dimensioni diverse e associare il frammento appropriato all’area di destinazione. I frammenti di layout consentono inoltre di personalizzare alcune delle proprietà della tabella:

1. Puoi aumentare il numero di righe e colonne.
1. È possibile specificare il testo di intestazione e piè di pagina per più righe e colonne.
1. Puoi definire il rapporto tra la larghezza delle colonne della tabella. In fase di runtime, le colonne della tabella vengono ridimensionate in base al rapporto definito e allo spazio disponibile. La somma del rapporto di larghezza deve essere 100. In caso contrario non è applicabile.
1. Se una tabella è un segnaposto (contiene una sola cella vuota), è possibile definire il tipo (area/campo di destinazione) delle nuove colonne.
1. È possibile nascondere le righe di intestazione e piè di pagina.

Prima di eseguire questa procedura, crea un frammento XFA utilizzando Designer. Il frammento può contenere tabelle per organizzare campi e aree di destinazione. Designer consente la creazione di due tipi di tabelle: statiche e dinamiche. Le tabelle statiche contengono un numero fisso di righe. Le tabelle statiche possono contenere aree e campi di destinazione. Questi campi e aree di destinazione non possono essere associati a DDE ripetute. Una tabella dinamica può avere anche una singola riga. I dati associati alle celle di tabella determinano il numero di righe per le tabelle dinamiche. Una tabella dinamica può contenere solo campi. I DDE possono essere ripetuti o non ripetuti.

Durante la progettazione delle tabelle, tenere presenti le considerazioni riportate di seguito.

1. Le tabelle possono essere personalizzate al momento della creazione del frammento di layout. Tuttavia, l&#39;opzione di personalizzazione è abilitata solo quando viene eseguito il flusso della sottomaschera padre della tabella.
1. Per le tabelle dinamiche tutti i campi, le righe e le tabelle ripetibili utilizzano l’associazione &quot;use name&quot; per unire correttamente i dati.
1. Per le tabelle dinamiche, tutti i DDE ripetuti associati ai campi della tabella fanno parte della stessa gerarchia. Per i DDE non ripetuti tale restrizione non esiste.
1. Al momento dell’unione del frammento di layout nelle tabelle dell’area di destinazione principale, questo viene ridimensionato in base allo spazio disponibile. Tuttavia, il ridimensionamento viene eseguito solo se il frammento di layout non contiene alcuna area di destinazione o campo direttamente all’interno della sottomaschera di livello superiore. L’area di destinazione e i campi all’interno della tabella sono consentiti.
1. È possibile creare tabelle segnaposto. Le tabelle segnaposto hanno una sola cella vuota.

* Per le tabelle segnaposto, è possibile personalizzare le seguenti proprietà al momento della creazione del frammento.

   * conteggio righe
   * numero colonne
   * intestazione e piè di pagina per ogni colonna
   * tipo (area/campo di destinazione) di ciascuna colonna
   * rapporto larghezza per ogni colonna

* Per una tabella non segnaposto, è possibile personalizzare le proprietà seguenti:

   * conteggio righe
   * numero colonne
   * intestazione e piè di pagina per colonna aggiuntiva
   * rapporto larghezza per ogni colonna

È possibile nidificare i frammenti in una lettera. Ciò implica che è possibile aggiungere un frammento all’interno di un frammento. La soluzione Gestione corrispondenza supporta fino a quattro livelli di nidificazione all&#39;interno di una lettera: **Lettera *>*Frammento *>*Frammento *>*Frammento *>*Frammento.**

Per un esempio dettagliato dell&#39;utilizzo di tabelle statiche e dinamiche nei frammenti di layout, vedere [Esempio con file di esempio: utilizzo di tabelle statiche e dinamiche in una lettera](#examplewithsamplefiles).

### Creazione di un frammento di layout {#creating-a-layout-fragment}

1. Seleziona **Crea** > **Frammento layout**.
1. Gestione corrispondenza visualizza gli XDP disponibili. Seleziona l&#39;XDP su cui vuoi basare il frammento di layout e seleziona **Successivo**.
1. Specificare le seguenti informazioni per il layout:

   * **Titolo (facoltativo):** Immettere il titolo per il frammento di layout. Il titolo non deve necessariamente essere univoco e può contenere caratteri speciali e non inglesi. I frammenti di layout sono indicati dai relativi titoli (se disponibili), ad esempio nelle miniature e nelle proprietà della risorsa.
   * **Nome:** Il nome univoco per il frammento di layout. Non possono esistere due risorse (testo, condizione o elenco) in nessuno stato con lo stesso nome. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini in lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti da trattini nel campo Nome. Anche se il valore nel campo Titolo viene copiato automaticamente nel Nome, è possibile modificarlo. Questo nome viene visualizzato nell’elenco dell’interfaccia utente Gestisci Assets.
   * **Descrizione (facoltativo)**: descrizione visualizzata nell&#39;elenco dell&#39;interfaccia utente Gestisci Assets.
   * **Tag (facoltativo)**: è possibile selezionare i tag da applicare alla condizione. Puoi anche digitare il nome di un nuovo tag e crearlo.

1. Selezionare la scheda **Tabella** e specificare le informazioni seguenti per il layout:

   * **Configurazione per**: selezionare la tabella da configurare.Come suffisso al nome della tabella nel menu a discesa è (Statico) se la tabella è statica oppure (Dinamico) se la tabella è dinamica. Le tabelle statiche contengono un numero fisso di righe. Le tabelle statiche possono contenere aree e campi di destinazione. Questi campi e aree di destinazione non possono essere associati a DDE ripetute. I dati associati alle celle di tabella determinano il numero di righe per le tabelle dinamiche.

   * **Righe**: selezionare il numero di righe per il layout. Il numero di righe configurato deve essere maggiore o uguale al numero di righe originale.
   * **Colonne**: selezionare il numero di colonne per il layout. Il numero di colonne configurato deve essere maggiore o uguale al numero di colonne originale.

   Per ogni colonna sono richiesti i seguenti dettagli:

   * **Intestazione**: testo da visualizzare per l&#39;intestazione
   * **Piè di pagina**: testo da visualizzare per il piè di pagina
   * **Tipo**: tipo di colonna aggiuntiva. Campo o area di destinazione. Tipo abilitato per tabelle segnaposto statiche. Il tipo può essere definito a livello di colonna e non a livello di cella. Tutte le celle di una colonna estesa sono dello stesso tipo. Per una tabella dinamica, tutte le colonne sono di tipo Campo. Per le tabelle non segnaposto non è possibile definire il tipo di colonne aggiuntive. In questo caso, il tipo di celle aggiuntive nella colonna estesa è uguale al tipo dell&#39;ultima colonna della riga e il tipo di cella nella riga aggiuntiva è uguale al tipo dell&#39;ultima cella della colonna.
   * **Proporzione larghezza:** proporzione delle larghezze delle colonne della tabella.

   Per un esempio dettagliato dell&#39;utilizzo di tabelle statiche e dinamiche nei frammenti di layout, vedere [Esempio con file di esempio: utilizzo di tabelle statiche e dinamiche in una lettera](#examplewithsamplefiles).

1. Seleziona **Salva**.

### Caricare un XDP in Gestione corrispondenza {#upload-an-xdp-to-correspondence-management}

Per istruzioni su come caricare/importare un XDP in Gestione corrispondenza, vedere [Importazione ed esportazione di risorse in AEM Forms](/help/forms/using/import-export-forms-templates.md).

### Best practice/suggerimenti {#best-practices-tips-and-tricks-2}

#### Impostare l&#39;associazione sottomaschera predefinita {#set-the-default-subform-binding}

Quando si creano aree di destinazione in Designer, è utile impostare su &quot;none&quot; l’associazione predefinita per tutti i nuovi sottomascheri.

Per impostare l&#39;associazione predefinita:

1. In Designer, selezionare **Strumenti** > **Opzioni** > **Associazioni dati** > **Associazione sottomodulo**.

1. Nell&#39;elenco Associazione predefinita per nuovi sottomoduli selezionare **Nessuna associazione dati**.

In questo modo, per impostazione predefinita, le sottomaschere inserite utilizzando il comando Inserisci > Sottomaschera o mediante trascinamento della selezione dalla tavolozza degli oggetti hanno un&#39;associazione &quot;none&quot;. Ciò significa che, per impostazione predefinita, qualsiasi nuova sottomaschera è un&#39;area di destinazione a meno che non si aggiunga contenuto, non si modifichi l&#39;impostazione di associazione o non si denomini la sottomaschera con un suffisso &quot;_int&quot;.

#### Conformità alla sezione 508 {#section-compliance}

Se la lettera completata creata nell’interfaccia utente Crea corrispondenza viene utilizzata per compilare un flusso di lavoro successivo. Segui queste raccomandazioni relative alla Sezione 508 durante la creazione del layout. In caso contrario, il PDF della lettera verrà visualizzato e sarà possibile ignorare i seguenti consigli:

* Tutte le sottomaschere dell&#39;area di destinazione e tutti i campi in un layout hanno un ordine di tabulazione.
* Per impostazione predefinita, i campi con didascalie sono conformi allo standard 508. L’attributo /field/assist/speak@priority del campo è impostato su &quot;custom&quot; per impostazione predefinita, il che significa che, a meno che non venga fornito un testo personalizzato per la lettura dello schermo, questa legge la didascalia del campo.
* I campi senza didascalia specificano una descrizione e indicano che gli assistenti vocali leggono la descrizione impostando

`/field/assist/speak@priority="toolTip"` e specificazione del testo della descrizione in `/field/assist/toolTip`.

#### Formati delle date in Designer e Asset Configuration Manager {#date-formats-in-designer-and-asset-configuration-manager}

Durante la progettazione di un layout in Designer, accertati che i formati per i campi data corrispondano ai formati data specificati in Formati visualizzazione dati nelle [Proprietà di configurazione di Gestione corrispondenza](/help/forms/using/cm-configuration-properties.md). Per ulteriori informazioni, vedere &quot;Formattazione dei valori dei campi e utilizzo dei modelli&quot; nella Guida di Designer.

#### Acquisizione di intervalli di date {#capturing-date-ranges}

Quando si tratta di una combinazione di date, ad esempio startDate - endDate, utilizzare un&#39;unica sottomaschera per garantire il corretto allineamento della lettera finita e ridurre al minimo il numero di campi.

#### Impostazione dell&#39;associazione a livello di modulo {#setting-form-level-binding}

Quando un layout contiene molti campi e aree di destinazione mappati a singoli elementi XML, utilizzare l&#39;associazione a livello di modulo e creare un nodo separato per ogni elemento. I campi associati a livello di modulo vengono ignorati durante la mappatura dei dati in Gestione corrispondenza.

#### Non utilizzare aree di destinazione sottomaschera in una pagina master {#do-not-use-subform-target-areas-in-a-master-page}

Le aree di destinazione dei sottomoduli in una pagina master non sono visibili nell’interfaccia utente Gestisci Assets e non è possibile mappare i dati su di esse.

#### Scelta di posizioni e tipi appropriati per le aree di destinazione {#choosing-appropriate-positions-and-types-for-target-areas}

Durante la progettazione del layout, prestare attenzione nella scelta delle sottomaschere. Se il layout contiene una singola sottomaschera, può essere un tipo di flusso. Dopo aver posizionato i campi nella sottomaschera, è possibile racchiuderla in un&#39;altra sottomaschera in modo che anche la sottomaschera a capo scorra e il layout non venga disturbato.

#### Inserimento di campi nelle pagine master {#placing-fields-on-master-pages}

Quando si inserisce un campo in una pagina master, tenere presente quanto segue:

* Impostare l&#39;associazione dei campi della pagina master per utilizzare i dati globali
* Non posizionare il campo direttamente sotto la PageArea principale della pagina master.
* Racchiudi il campo in una sottomaschera denominata e assicurati che l’associazione della sottomaschera denominata sia impostata su Usa nome.

## Creazione di tabelle tramite frammenti di layout {#creating-tables-using-layout-fragments}

Molti modelli di lettere contengono tabelle. Le tabelle possono essere statiche, ad esempio una tabella di termini e condizioni, in cui ogni riga rappresenta una condizione e ogni parte viene visualizzata in una colonna separata. Le tabelle possono anche essere dinamiche, ad esempio le informazioni sul conto, che contengono informazioni quali il nome del cliente, l&#39;ID conto, il numero della transazione e l&#39;importo della transazione.

* **Tabelle statiche**: a volte le tabelle vengono create con righe con un numero diverso di colonne, ad esempio per una tabella di termini e condizioni. Dove ogni riga rappresenta una condizione e ogni condizione può avere diverse parti secondarie. Ogni parte viene visualizzata in una colonna separata.
* **Tabelle dinamiche**: i frammenti di layout consentono di associare i campi di una tabella dinamica ai DDE della raccolta. Al momento della generazione della lettera, le righe della tabella vengono generate in base alle dimensioni dei DDE della raccolta.

L&#39;elemento DD dispone di un elemento Nominee_details che dispone di un elemento composito con tre elementi primitivi: Nominee_name, Nominee_address e Nominee_gender.
Anche l’XDP dinamico ha le stesse intestazioni. Puoi mappare i campi XDP dinamici con i campi DD sopra menzionati.

### Esempio con file di esempio: utilizzo di tabelle statiche e dinamiche in una lettera {#examplewithsamplefiles}

In questo esempio viene illustrato come creare una tabella dinamica e una tabella statica, associare la tabella dinamica ai DDE e quindi creare una lettera che includa queste due tabelle. Quando si utilizza questo esempio, è possibile creare file da zero o utilizzare i file di input forniti nei passaggi.

1. Creare un dizionario dati (DD) che si desidera utilizzare nell&#39;esempio, come rappresentato nell&#39;immagine.

   Quindi selezionare DD ed esportare i dati di esempio. Il file XML ottenuto contiene i dati relativi ai dipendenti e tre istanze per Nominee_details (per impostazione predefinita vengono scaricate 3 istanze. Puoi aggiungere o eliminare in base alle tue esigenze). Aggiorna i valori e importa i dati di test in DD. Il file CMP è il pacchetto e contiene il DD. Importa quindi DD in Gestione corrispondenza.

   Per ulteriori informazioni sull&#39;utilizzo del dizionario dati e dei dati di prova, vedere [Dizionario dati](/help/forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Struttura dizionario dati](assets/dd.jpeg)

[Ottieni file](assets/exportpackage_1431709897770.cmp.zip)

1. In Designer, crea due XDP (frammenti di layout): una tabella dinamica e una tabella statica. Per entrambi i layout:

   * Aggiungere una sottomaschera alla colonna della tabella. Assicurarsi di modificare il layout della sottomaschera padre della tabella in fluito e rimuovere le associazioni della sottomaschera nella tabella.
   * Aggiungere una sottomaschera alla cella della tabella. Assicurarsi di modificare il layout della sottomaschera padre della tabella in fluito e rimuovere le associazioni della sottomaschera nella tabella.

   In alternativa, utilizzare gli XDP statici e dinamici associati a questo passaggio.

   Per ulteriori informazioni sull&#39;utilizzo dei frammenti di layout, vedere [Frammenti di layout](#layoutfragments).
Per ulteriori informazioni sulla progettazione dei layout, vedere la [Guida di Designer](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/).

[Ottieni file](assets/static.xdp.zip)

[Ottieni file](assets/dynamic.xdp.zip)

1. Carica gli XDP in AEM Forms.
1. Crea un frammento di layout basato su XDP dinamico. Nella scheda Tabella delle proprietà viene visualizzato che la tabella è dinamica (campo Configurazione per ). Il numero di righe (1) e colonne (3) è derivato dal frammento XDP/Layout.

   I campi di questo layout sono successivamente associati al DD importato e nella lettera il numero di righe viene creato in modo dinamico in base al numero di record nel file di dati di prova (il file di dati XML allegato al DD).

   ![Crea una schermata frammento layout](assets/dynamictableproperties.png)

   Fai clic per aprire un&#39;immagine di dimensioni intere

1. Crea un frammento di layout basato su XDP statico. Nella scheda Tabella delle proprietà viene visualizzato che la tabella è statica (campo Configurazione per ). Il numero di righe (1) e colonne (3) è derivato dal frammento XDP/Layout.

   Puoi modificare il numero di colonne e righe qui. In base alla scelta effettuata in questa schermata, il numero di righe e colonne di una tabella statica rimane fisso nella lettera creata con questo layout.
   [![Crea una schermata frammento layout](assets/statictableproperties.png)](assets/statictableproperties-1.png)

1. Crea una lettera utilizzando entrambi i frammenti di layout. Quando inserisci l’XDP dinamico nella lettera, imposta l’associazione dei suoi campi agli elementi di raccolta del dizionario dati.

   Per ulteriori informazioni sulla creazione di modelli di lettere e lettere, vedere [Crea lettera](/help/forms/using/create-letter.md).

1. Salva la lettera e visualizzala in anteprima. Quando si visualizza l’anteprima della lettera, i valori del dizionario dati vengono visualizzati nella lettera. Per la tabella dinamica sono disponibili tre righe. Questo perché i dati del test hanno tre record per queste righe.

   Per la tabella statica, sono presenti tutte le righe e colonne specificate durante la creazione del frammento di layout.

   ![Tabella statica nella lettera](assets/statictableletter.png)

   Per la tabella dinamica, le tre righe vengono visualizzate in base al numero di record nel file di dati di test. Ciò si è verificato perché durante l’aggiunta del layout alla lettera è stata creata un’associazione tra i campi della tabella dinamica e gli elementi di raccolta del dizionario dati. I valori Nome, Indirizzo e Genere vengono compilati dal file di dati di test utilizzato.

   ![Tabella dinamica nella lettera](assets/dynamictableletter.png)

## Creare una copia di un frammento di documento {#create-a-copy-of-a-document-fragment}

Per creare rapidamente un frammento di documento con proprietà e contenuto simili a quelli di un frammento di documento esistente, è possibile copiarlo e incollarlo.

1. Dall’elenco dei frammenti di documento, seleziona uno o più frammenti di documento. Nell’interfaccia utente viene visualizzata l’icona Copia.
1. Seleziona Copia. Nell’interfaccia viene visualizzata l’icona Incolla. Puoi anche scegliere di entrare in una cartella prima di incollarla. Cartelle diverse possono contenere risorse con gli stessi nomi. Per ulteriori informazioni sulle cartelle, consulta [Cartelle e organizzazione delle risorse](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Seleziona Incolla. Viene visualizzata la finestra di dialogo Incolla. Se i frammenti di documento vengono copiati e incollati nello stesso punto, il sistema assegna automaticamente nomi e titoli alle nuove copie di lettere, ma è possibile modificare i titoli e i nomi delle lettere.
1. Se necessario, modifica il Titolo e il Nome con cui vuoi salvare la copia del frammento di documento.
1. Seleziona Incolla. Viene creata la copia del frammento di documento.
