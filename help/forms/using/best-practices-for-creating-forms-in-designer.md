---
title: Procedure consigliate per la creazione di moduli in Forms Designer
description: Scopri le best practice per l’accessibilità nella creazione di moduli in Forms Designer
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 3a9d7943-2c34-4e0a-9803-7ce1ef40f676
source-git-commit: 0d491be4fb2605220b1558c8c877151ab4405978
workflow-type: tm+mt
source-wordcount: '11687'
ht-degree: 0%

---

# Procedure consigliate per la creazione di moduli in Forms Designer

LiveCycle Designer consente di creare contenuti avanzati e di rispettare le linee guida della Sezione 508. Questa guida contiene una panoramica delle best practice per la creazione di un modulo accessibile e le linee guida per l’implementazione di queste best practice tramite LiveCycle Designer. Sono trattate le seguenti best practice:

1. [Moduli semplici e facili da usare](#keep-simple)
1. [Configura le proprietà del modulo per generare le informazioni di accessibilità](#configure-form-properties)
1. [Scegli i controlli giusti](#choose-right-controls)
1. [Fornisci equivalenti di testo per le immagini](#provide-text-equivalents)
1. [Fornire etichette appropriate per i controlli modulo](#provide-proper-labels)
1. [Verificare che l&#39;ordine di lettura e di tabulazione sia corretto](#ensure-reading-tab-order)
1. [Assicurarsi che i controlli del modulo siano accessibili da tastiera](#ensure-keyboard-accessible)
1. [Usa il colore in modo responsabile](#use-color-responsibly)
1. [Fornire celle di intestazione per le tabelle](#provide-heading-cells)
1. [Fornire una struttura di moduli navigabile](#provide-navigable-form)
1. [Evitare l&#39;interruzione degli script](#avoid-disruptive-scripting)
1. [Assicurati che tutti i contenuti audio e video siano accessibili](#ensure-audio-video-accessible)
1. [Identificare il linguaggio naturale ed eventuali modifiche nel linguaggio](#identify-natural-language)

## Moduli semplici e facili da usare {#keep-simple}

Un modulo non è accessibile se non è facile da utilizzare. È consigliabile progettare moduli semplici e utilizzabili. Un layout semplice di controlli e campi con didascalie e descrizioni degli strumenti chiare e significative semplificherà notevolmente l&#39;utilizzo del modulo da parte di tutti gli utenti.
La progettazione di moduli ordinati e disposti in modo logico e che forniscano istruzioni chiare e semplici aiuterà tutti gli utenti a compilare i moduli nel modo più semplice possibile. Le funzionalità di spostamento, ad esempio l&#39;ordine di tabulazione e le scelte rapide da tastiera, devono supportare l&#39;ordine logico degli oggetti nel modulo.

### Evita di spostare, lampeggiare o lampeggiare i contenuti

Alcuni soggetti con epilessia fotosensibile possono avere una crisi scatenata da un movimento in frequenze superiori a 2 Hz (1 Hz, o Hertz, uguale a uno al secondo) e inferiori a 55 Hz (55 al secondo).

Il movimento a meno di 2 Hz è considerato abbastanza lento da essere sicuro per gli individui con epilessia fotosensibile. Il movimento a più di 55 Hz è considerato impercettibile.

Gli sviluppatori devono essere a conoscenza di questi parametri quando utilizzano qualsiasi movimento nei contenuti web.

Altri utenti possono avere disabilità cognitive che rendono difficile concentrarsi quando è presente contenuto animato o lampeggiante nel modulo.

In genere, si consiglia di evitare di utilizzare effetti ottici inseriti da script, ad esempio testo lampeggiante o animazione, nei moduli interattivi. Tali effetti riducono l’usabilità dei moduli per alcuni utenti.

Punti di controllo correlati
* Sezione 508 §11934.21

   * (h) Quando è visualizzata un&#39;animazione, le informazioni devono poter essere visualizzate in almeno una modalità di presentazione non animata a scelta dell&#39;utente.
   * (k) Il software non deve utilizzare testo lampeggiante o lampeggiante, oggetti o altri elementi con una frequenza di lampeggiamento o lampeggiamento superiore a 2 Hz e inferiore a 55 Hz.
* Sezione 508 §11934.22
   * (j) Le pagine devono essere progettate in modo da evitare che lo schermo sfarfallii con una frequenza superiore a 2 Hz e inferiore a 55 Hz.
* WCAG 1.0
   * 7.1 Fino a quando gli agenti utente non consentono agli utenti di controllare lo sfarfallio, evita di causare lo sfarfallio dello schermo. P1)
   * 7.2 Fino a quando gli user agent non consentono agli utenti di controllare la lampeggiatura, evitare di causare la lampeggiamento del contenuto (ad esempio, cambiare la presentazione a una velocità regolare, come accendere e spegnere) (P2).
   * 7.3 Fino a quando gli agenti utente non consentono agli utenti di bloccare i contenuti in movimento, evita lo spostamento nelle pagine.
   * 14.1 Utilizza il linguaggio più chiaro e semplice appropriato per il contenuto di un sito.
* WCAG 2.0
   * 2.2.2 Pausa, stop, nascondi: per le informazioni in movimento, lampeggianti, scorrevoli o con aggiornamento automatico, vale quanto segue: (Livello A)
   * 2.3.1 Tre Flash o inferiore alla soglia: le pagine web non contengono elementi che lampeggiano più di tre volte al secondo, oppure il lampeggiamento è inferiore alle soglie di lampeggiamento generale e rosso. (Livello A)
   * 2.3.2 Tre Flash: le pagine web non contengono elementi che lampeggiano più di tre volte al secondo. (livello AAA)


## Configura le proprietà del modulo per generare le informazioni di accessibilità {#configure-form-properties}

Affinché un modulo sia accessibile, deve essere [percepibile](https://www.w3.org/TR/WCAG20/#perceivable) dalla tecnologia per l&#39;accessibilità. La maggior parte degli assistenti vocali, ad esempio, non considera il layout visivo del modulo, ma la struttura sottostante.

Per implementare questa struttura sottostante utilizzando LiveCycle Designer, è necessario creare un modulo PDF con informazioni di accessibilità (a volte denominate tag) incluse, in modo che l’assistente vocale o un’altra tecnologia possa leggere il testo e i componenti del modulo. In un modulo con informazioni sull&#39;accessibilità, ogni elemento contiene informazioni sulla propria struttura, oltre a informazioni su come è correlato o dipendente da altri elementi. Solo nei file PDF con le informazioni di accessibilità incluse è possibile identificare e descrivere con precisione il contenuto di un documento.

Per creare un modulo accessibile, è necessario configurare le proprietà del modulo in modo che Designer di LiveCycle generi informazioni di accessibilità quando si salva la struttura del modulo come file PDF:
1. Scegliete File > Proprietà modulo.
1. Fai clic sulla scheda Opzioni di salvataggio e, nell’area PDF, accertati che sia selezionata l’opzione Genera informazioni sull’accessibilità (tag) per Acrobat.
1. Fare clic su OK.

In LiveCycle Designer, questa opzione è selezionata per impostazione predefinita.

>[!NOTE]
> Queste opzioni sono valide solo quando si salva la struttura del modulo come file PDF. Non si applicano ai file PDF creati con LiveCycle Forms che dispongono di opzioni di configurazione indipendenti da questa opzione in LiveCycle Designer.

**Punti di controllo correlati**

* Sezione 508 §1194.21
   * (d) Le tecnologie per l&#39;accessibilità devono disporre di informazioni sufficienti su un elemento dell&#39;interfaccia utente, compresa l&#39;identità, il funzionamento e lo stato dell&#39;elemento. Quando un’immagine rappresenta un elemento del programma, anche le informazioni trasmesse dall’immagine devono essere disponibili nel testo.
   * (l) Quando si utilizzano moduli elettronici, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità richieste per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.
* Sezione 508 §1194.22
   * (n) Se i moduli elettronici sono concepiti per essere compilati in linea, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità necessarie per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.


## Scegli i controlli giusti {#choose-right-controls}

Quando si progettano i moduli, utilizzare gli oggetti di sviluppo delle schede disponibili nella Libreria oggetti di LiveCycle Designer. Potete visualizzare questo pannello scegliendo Finestra > Libreria oggetti o premendo Maiusc+F12 (vedere Figura 1).

![Pannello Libreria oggetti](/help/forms/using/assets/image-1.png)

Figura 1: **Pannello Libreria oggetti**

Se utilizzi altri oggetti, questi potrebbero essere ignorati dalle tecnologie per l’accessibilità. L&#39;utilizzo dei soli oggetti standard consente inoltre di definire le proprietà di Accesso facilitato per gli oggetti creati personalmente. Se si creano e si utilizzano oggetti personalizzati, assicurarsi di utilizzare la tavolozza Accessibilità per impostare le proprietà di accessibilità, ad esempio Ruolo, Descrizione comando, Precedenza Reader schermo e Testo Reader schermo personalizzato. Per visualizzare la tavolozza Accessibilità, scegliete Finestra > Accessibilità.

**Punti di controllo correlati**
* Sezione 508 §1194.21
   * (c) Deve essere fornita un’indicazione su schermo precisa della messa a fuoco in corso, che si sposta tra gli elementi interattivi dell’interfaccia man mano che cambia la messa a fuoco dell’input. La messa a fuoco deve essere esposta a livello di programmazione in modo che la tecnologia assistiva possa tenere traccia dei cambiamenti di messa a fuoco e messa a fuoco.
   * (d) Le tecnologie per l&#39;accessibilità devono disporre di informazioni sufficienti su un elemento dell&#39;interfaccia utente, compresa l&#39;identità, il funzionamento e lo stato dell&#39;elemento. Quando un’immagine rappresenta un elemento del programma, anche le informazioni trasmesse dall’immagine devono essere disponibili nel testo.
   * (l) Quando si utilizzano moduli elettronici, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità richieste per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.
* Sezione 508 §1194.22
   * (n) Se i moduli elettronici sono concepiti per essere compilati in linea, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità necessarie per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.

* WCAG 2.0
   * 3.2.4 Identificazione coerente: i componenti che hanno la stessa funzionalità all’interno di un insieme di pagine web sono identificati in modo coerente. (livello AA).
   * 4.1.2 Nome, ruolo, valore: per tutti i componenti dell’interfaccia utente (inclusi ma non limitati a: elementi di un modulo, collegamenti e componenti generati da script), il nome e il ruolo possono essere determinati programmaticamente; stati, proprietà e valori che possono essere impostati dall’utente possono essere impostati programmaticamente; e la notifica delle modifiche a questi elementi è disponibile per gli agenti utente, incluse le tecnologie per l’accessibilità. (Livello A)


## Fornisci equivalenti di testo per le immagini {#provide-text-equivalents}

Le immagini possono aiutare a migliorare la comprensione per gli utenti con alcuni tipi di disabilità. Tuttavia, per gli utenti di utilità di lettura dello schermo, le immagini diminuiranno l’accessibilità del modulo se non si fornisce un’alternativa testuale.

Se scegli di utilizzare le immagini, fornisci descrizioni testuali per tutti gli oggetti campo immagine e immagine. Verificare che il testo descriva l&#39;oggetto e il relativo scopo nel modulo. Quando si definisce un&#39;alternativa testuale, l&#39;assistente vocale legge tale alternativa quando incontra l&#39;immagine. Per questo motivo, un&#39;immagine contenente informazioni deve sempre avere un testo alternativo specificato.

Le descrizioni di testo vengono fornite utilizzando le proprietà Descrizione comando o Testo Reader schermo personalizzato nella tavolozza Accessibilità oppure tramite campi di testo, didascalie e nomi di oggetto, come specificato nell&#39;opzione Nome della scheda Associazione. La Figura 2 mostra ad esempio un esempio di immagine contenente il testo &quot;Ottieni Adobe Reader&quot;. Poiché un assistente vocale non è in grado di leggere il testo che fa parte di un’immagine, è necessario includere un testo alternativo nel campo Testo Reader schermo personalizzato della tavolozza Accessibilità per questo oggetto. Nella maggior parte dei casi, il testo alternativo deve essere uguale al testo visibile nell’immagine (vedi Figura 2).

![Specifica di testo alternativo per un&#39;immagine mediante la tavolozza Accesso facilitato](/help/forms/using/assets/image-2.png)

Figura 2: **Specifica di testo alternativo per un&#39;immagine tramite la tavolozza Accessibilità**

Quando specificate il testo alternativo, tenete presente quanto segue:
* Se l&#39;oggetto immagine o l&#39;immagine digitalizzata include informazioni importanti per il modulo, creare testo per l&#39;immagine nel riquadro Accessibilità che descrive l&#39;oggetto e il relativo scopo. Il testo del logo di una società, ad esempio, può essere costituito dalle parole &quot;logo della società&quot; e dal nome della società.
* Se l&#39;oggetto immagine contiene informazioni sui colori semantici, includerle anche nella descrizione. Una descrizione di un semaforo verde, ad esempio, potrebbe essere &quot;Trasmissione riuscita&quot; e la descrizione di un semaforo rosso potrebbe essere &quot;Trasmissione non riuscita&quot;.
* Se si utilizzano elementi grafici complessi, ad esempio grafici a barre, fornire le informazioni in una versione accessibile alternativa, ad esempio una tabella o una descrizione testuale più lunga.
* Non creare descrizioni testuali per le immagini statiche utilizzate solo a scopo di decorazione.
* Non utilizzare dati digitalizzati come informazioni di background. Ciò può verificarsi quando una finestra di progettazione analizza un modulo di stampa e utilizza Adobe LiveCycle Designer per aggiungere nuovi campi al modulo. Gli assistenti vocali non sono in grado di rilevare i dati digitalizzati in questo stato.

Quando si includono contenuti grafici puramente decorativi nei moduli, è necessario assicurarsi che gli assistenti vocali non annuncino la presenza dell&#39;immagine. Per la maggior parte degli assistenti vocali, questo può essere ottenuto impostando la proprietà Testo Reader su Nessuno nella tavolozza Accessibilità. In caso contrario, alcuni assistenti vocali potrebbero annunciare la presenza di un&#39;immagine, senza indicare ciò che l&#39;immagine rappresenta. Per le immagini dinamiche, come gli oggetti campo immagine, assicurati che le alternative di testo vengano aggiornate correttamente quando l’immagine viene modificata. Non creare descrizioni testuali per gli oggetti campo immagine utilizzati solo a scopo di decorazione. È possibile utilizzare il linguaggio di script FormCalc per assegnare descrizioni di testo a un oggetto campo immagine in modo dinamico. FormCalc è il linguaggio di script standard di Adobe LiveCycle Designer. Si consideri ad esempio un modulo con un campo immagine denominato ImageField1 e testo associato nel nodo imagetext dei dati di runtime. È possibile utilizzare gli script per passare questo testo in un evento appropriato, ad esempio `form:ready`, nel modo seguente:

`ImageField1.assist.toolTip = $record.imagetext.value`

Punti di controllo correlati
* Sezione 508 §1194.22
   * (a) Deve essere fornito un equivalente testuale per ogni elemento non testuale (ad esempio tramite &quot;alt&quot;, &quot;longdesc&quot; o nel contenuto dell’elemento).
* WCAG 1.0
   * 1.1 Fornisci un equivalente testuale per ogni elemento non testuale (ad esempio, tramite &quot;alt&quot;, &quot;longdesc&quot; o nel contenuto dell’elemento). Ciò include: immagini, rappresentazioni grafiche di testo (compresi i simboli), aree delle mappe immagine, animazioni (ad esempio, GIF animati), applet e oggetti programmatici, arte ascii, fotogrammi, script, immagini utilizzate come punti elenco, distanziatori, pulsanti grafici, suoni (riprodotti con o senza interazione dell’utente), file audio autonomi, tracce audio di video e video (P1).
* WCAG 2.0
   * 1.1.1 Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito. (Livello A)


## Fornire etichette appropriate per i controlli modulo{#provide-proper-labels}

L&#39;etichetta o la didascalia di un controllo modulo identifica ciò che il controllo deve rappresentare. Ad esempio, il testo &quot;Nome&quot; indica agli utenti che devono immettere il proprio nome in un campo di testo. Per essere accessibile agli assistenti vocali, l&#39;etichetta deve essere associata a livello di programmazione al controllo modulo oppure il controllo modulo deve essere configurato con informazioni aggiuntive sull&#39;accessibilità utilizzando la tavolozza Accessibilità. Non è sufficiente posizionare un oggetto di testo accanto al controllo. Per gli utenti non vedenti o ipovedenti è importante che l’etichetta sia posizionata correttamente accanto al controllo. Entrambe le tecniche saranno discusse nelle sezioni seguenti.

### Specifica del testo dell&#39;etichetta accessibile mediante la tavolozza Accessibilità

L’etichetta percepita dagli utenti di utilità di lettura dello schermo non deve necessariamente essere la stessa della didascalia visiva. In alcuni casi può essere necessario specificare meglio lo scopo del controllo.
Per ogni oggetto campo di un modulo, è possibile utilizzare la tavolozza Accessibilità (vedere la Figura 3) per specificare l&#39;annuncio che verrà visualizzato dall&#39;assistente vocale per identificare il campo modulo specifico.

Per utilizzare la tavolozza Accessibilità, effettuare le seguenti operazioni:

1. Visualizzare la tavolozza Accessibilità scegliendo Finestra > Accessibilità o premendo Maiusc+F6.
1. Selezionare un oggetto nel modulo. La palette mostra le proprietà di accessibilità dell’oggetto.

![Tavolozza Accesso facilitato](/help/forms/using/assets/image-3.png)

Figura 3: **Tavolozza Accessibilità**

Quando il modulo viene salvato come PDF, Designer di LiveCycle cerca nel modulo le proprietà Testo personalizzato, Descrizione, Didascalia e Nome, nell&#39;ordine indicato, per trovare il testo che deve essere letto dagli assistenti vocali. È possibile ignorare questo ordine predefinito utilizzando l&#39;opzione Precedenza Reader schermo nella tavolozza Accessibilità:

1. Selezionare l&#39;oggetto nella struttura del modulo.
1. Fare clic sulla tavolozza Accessibilità.
1. Selezionare un&#39;opzione di precedenza del Reader di schermate diversa da Nessuno.

Sono disponibili le seguenti opzioni:

* **Testo personalizzato**, impostato nel campo Testo Reader schermo personalizzato della tavolozza Accessibilità. Questa opzione consente di specificare il testo che si desidera utilizzare con la tecnologia per l’accessibilità, ad esempio le utilità per la lettura dello schermo. L’impostazione Didascalia è la soluzione ottimale per la maggior parte delle situazioni: la creazione di Testo per Reader con schermo personalizzato deve essere considerata un’opzione solo quando non è possibile utilizzare la Didascalia o una descrizione comando.
* **Descrizione**, impostata nel campo Descrizione comando della tavolozza Accessibilità. Per la maggior parte degli oggetti, le descrizioni comandi vengono visualizzate in fase di esecuzione quando l&#39;utente passa il puntatore sull&#39;oggetto. Le descrizioni comandi vengono visualizzate per alcuni oggetti di sola lettura, ad esempio l&#39;oggetto codice a barre di un modulo cartaceo, solo quando è in uso un assistente vocale.
* **Didascalia**, che farà in modo che Designer di LiveCycle utilizzi l&#39;etichetta (visiva) associata al campo modulo come testo per la lettura dello schermo.
* **Nome**, impostato nel campo Nome della scheda Associazione. Questo nome non può contenere spazi.
* **Nessuno**. L&#39;oggetto non avrà un nome. Questa opzione non è mai consigliata per i controlli modulo.

Quando si utilizza la tavolozza Accessibilità per l&#39;etichettatura del controllo modulo, tenere presente quanto segue:

* Se la didascalia del controllo modulo descrive correttamente il controllo, sarà accessibile agli assistenti vocali. In questo caso, lasciare vuoti i campi Testo personalizzato e Descrizione comando nella tavolozza Accessibilità oppure impostare Priorità Reader su Didascalia.
* Quando si esegue il targeting degli assistenti vocali, non ha senso specificare descrizioni di testo diverse per lo stesso controllo modulo, in quanto ne verrà utilizzato solo uno: il primo campo non vuoto nell’ordine di precedenza del Reader Schermo. Ad esempio, non c’è motivo di specificare sia Testo personalizzato che Testo descrizione comando per un assistente vocale.
* Per impostazione predefinita, l&#39;utilità di lettura dello schermo legge la didascalia se non viene specificato nulla nella casella Descrizione comando o nella casella Testo Reader schermo personalizzato.
* Non utilizzare la tavolozza Accessibilità per creare descrizioni per campi o aree invisibili.
* Se è necessario creare una descrizione utilizzando le opzioni Descrizione comando o Testo Reader schermo personalizzato, includere sempre la didascalia visibile nel modulo, tranne quando la didascalia visibile non è significativa, ad esempio quando la didascalia stessa viene abbreviata. Questo consente agli utenti di utilità di lettura dello schermo di comunicare in modo efficace con altri utenti in merito agli elementi dell’interfaccia utente. Questi diversi gruppi di utenti hanno difficoltà a identificare lo stesso elemento dell’interfaccia utente se il testo della didascalia è diverso dalla descrizione comando o dal testo del Reader di schermate personalizzate.
* Per le caselle di controllo e i controlli degli elenchi a discesa nelle celle di tabella, l&#39;assistente vocale annuncerà il testo specificato per l&#39;oggetto in termini di didascalia, descrizione comando o utilità di lettura dello schermo. Se si desidera utilizzare l&#39;intestazione di colonna per il testo alternativo per questi oggetti quando si posiziona in una tabella, non fornire didascalia, descrizione comando o testo personalizzato per la lettura dello schermo.
* Se il controllo richiede istruzioni aggiuntive, assicurarsi che siano incluse anche nel testo alternativo. Includi informazioni vocali sufficienti per consentire agli utenti di sapere quale input è previsto e come completare correttamente il campo, ma non sopraffare gli utenti con informazioni ridondanti.
* Non fornire informazioni non necessarie che descrivono come utilizzare i controlli; lascia che siano le tecnologie per l’accessibilità dell’utente a gestirli. Gli utenti possono configurare il livello di dettaglio in base al proprio livello di comfort.

La Figura 4 mostra un esempio di campo di testo con una didascalia visiva che potrebbe non essere chiara per alcuni utenti di utilità per la lettura dello schermo. In questo esempio, l&#39;opzione Testo Reader schermo personalizzato è impostata su &quot;Numero di pagine&quot; e l&#39;opzione Precedenza Reader schermo è impostata su Testo personalizzato. Di conseguenza, il testo della didascalia effettiva (visiva) (&quot;# pagine&quot;) non verrà utilizzato dall’assistente vocale. In alternativa, è possibile specificare una descrizione comandi.

![Specifica del testo di Reader per lo schermo personalizzato quando l&#39;etichetta visibile non è adeguata](/help/forms/using/assets/image-4.png)

Figura 4: **Specifica del testo di Reader dello schermo personalizzato quando l&#39;etichetta visibile è inadeguata**

### Pulsanti di scelta Etichettatura

Quando un utente con problemi di vista preme un tasto di scelta, l’assistente vocale deve leggere due cose:
* Indicazione della funzione del gruppo di pulsanti di scelta
* Etichetta significativa per ogni pulsante di opzione
Per rendere accessibili i pulsanti di scelta utilizzando le didascalie dei pulsanti:
   1. Nella tavolozza Gerarchia, selezionare il gruppo di esclusione.
   1. Fare clic sulla tavolozza Accesso facilitato e nella casella Testo Reader schermo personalizzato digitare il testo da leggere per il gruppo. Ad esempio, per un gruppo di esclusione che indica le opzioni di pagamento per varie carte di credito, digita Selezionare un metodo di pagamento.
   1. Se le didascalie di ciascun pulsante di opzione forniscono testo significativo se pronunciato da un assistente vocale, nella palette Oggetto selezionare la scheda Associazione e deselezionare Specifica valore elemento.

  Per rendere accessibili i pulsanti di scelta utilizzando un valore di elemento specificato:
   1. Nella tavolozza Gerarchia, selezionare il gruppo di esclusione.
   1. Fare clic sulla tavolozza Accesso facilitato e nella casella Testo Reader schermo personalizzato digitare il testo da leggere per il gruppo. Ad esempio, per un gruppo di esclusione che indica le opzioni di pagamento per varie carte di credito, digita Selezionare un metodo di pagamento.
   1. Nella tavolozza Gerarchia selezionare il primo pulsante di opzione del gruppo.
   1. Nella tavolozza Oggetto fare clic sulla scheda Campo. Nell&#39;area Elemento fare doppio clic sull&#39;elemento e digitare un valore significativo per il pulsante di opzione selezionato. Ad esempio, per il primo pulsante di un gruppo di metodi di pagamento, è possibile digitare Contanti.
   1. Ripeti i passaggi 3 e 4 per ogni pulsante di opzione nel gruppo di esclusione.

### Etichettatura dei controlli personalizzati

Si consiglia vivamente di utilizzare componenti standard invece di componenti personalizzati, in quanto forniranno alla tecnologia per l’accessibilità i segnali e le informazioni corretti per impostazione predefinita. Tuttavia, se vengono utilizzati controlli personalizzati, considera quanto segue:
* Annunciare lo stato delle caselle di controllo e dei pulsanti di scelta.
* Nelle caselle di riepilogo e negli elenchi a discesa, annunciare l&#39;elemento predefinito selezionato nell&#39;elenco. Assicurarsi che l&#39;utente sappia utilizzare i tasti Freccia su e Freccia giù per spostarsi tra le voci dell&#39;elenco. Tieni presente che premendo il tasto TAB o INVIO o INVIO verrà selezionata la voce nell’elenco. Utilizzando gli script, è possibile impostare l&#39;evento Change dell&#39;oggetto per annunciare l&#39;elemento selezionato dall&#39;elenco.
* Annunciare agli utenti le sequenze di tasti speciali necessarie per eseguire una funzione, ad esempio premendo la barra spaziatrice per selezionare un pulsante o il tasto Freccia giù per selezionare un elemento da una casella di riepilogo.

### Posizionamento corretto della didascalia di un controllo

Il posizionamento di una didascalia è importante perché gli utenti si aspettano che si trovi accanto al controllo. Per gli utenti che utilizzano l’ingrandimento dello schermo questo è ancora più importante, in quanto potrebbero non essere in grado di visualizzare contemporaneamente sia il controllo che la didascalia se sono troppo distanti tra loro.

Quando si crea un oggetto, LiveCycle Designer posiziona automaticamente la didascalia come specificato dal tipo di oggetto. Le didascalie dei pulsanti di scelta, ad esempio, vengono posizionate a destra. Questo posizionamento predefinito è sempre la posizione migliore per una didascalia accessibile. Se è necessario modificare la posizione del testo della didascalia, attenersi alla seguente procedura:
1. Selezionare l&#39;oggetto spostando lo stato attivo su di esso.
1. Nella tavolozza Layout, selezionare la posizione della didascalia dell&#39;oggetto dall&#39;opzione Posizione nella sezione Didascalia, nella parte inferiore della tavolozza.

L&#39;esempio riportato nella Figura 5 mostra una casella di testo con una didascalia sopra di essa. L&#39;opzione Posizione nella tavolozza Layout è impostata su Superiore. La posizione predefinita della didascalia si trova a sinistra della casella di testo.

![Modifica del posizionamento dei sottotitoli mediante la tavolozza Layout](/help/forms/using/assets/image-5.png)

Figura 5: **Modifica del posizionamento dei sottotitoli mediante la tavolozza Layout**

Nella tabella seguente viene fornita una panoramica delle regole di posizionamento delle etichette per i controlli di uso comune.

| Tipo di controllo | Regole di posizionamento |
|--------------|-----------------|
| Input di testo (inclusi i campi di data, ora e password) | Posizionare la didascalia a sinistra del controllo (impostazione predefinita). Se ciò non fosse possibile, posizionarlo immediatamente sopra o sotto di esso. Le etichette devono essere posizionate vicino al controllo per gli utenti con ingrandimento maggiore, in modo che l’etichetta e il controllo abbiano più probabilità di essere visualizzati insieme nella vista ingrandita. |
| Casella di controllo | Posiziona la didascalia a destra della casella di controllo (impostazione predefinita). Per i controlli casella di controllo nelle celle di tabella, l&#39;utilità di lettura dello schermo annuncerà qualsiasi didascalia, descrizione comando o testo personalizzato specificato per l&#39;oggetto. Se desideri utilizzare l’intestazione di colonna come testo alternativo per una casella di controllo in una tabella, non fornire didascalia, descrizione comando o testo personalizzato per la lettura dello schermo. |
| Gruppo pulsanti di scelta | Creare un titolo visibile per il gruppo di pulsanti di scelta creando un elemento di testo statico e posizionandolo a sinistra o sopra il gruppo. Per ogni singolo pulsante di scelta, posizionare l&#39;etichetta a destra (impostazione predefinita). |
| Elenco a discesa | Posizionare la didascalia a sinistra dell&#39;oggetto (impostazione predefinita). Se ciò non è possibile, posizionarlo immediatamente sopra di esso. Per i controlli elenco a discesa nelle celle di tabella, l&#39;utilità di lettura dello schermo annuncia qualsiasi didascalia, descrizione comando o testo personalizzato specificato per l&#39;oggetto. Se si desidera utilizzare l&#39;intestazione di colonna come testo alternativo per questi oggetti in una tabella, non fornire didascalia, descrizione o testo personalizzato per la lettura dello schermo. |
| Casella di riepilogo | La didascalia viene posizionata sopra la casella di riepilogo per impostazione predefinita al momento della creazione. |
| Pulsante | La didascalia viene automaticamente posizionata sul pulsante e non deve essere posizionata manualmente. Assicurati che lo scopo del pulsante sia descritto correttamente dal testo della didascalia. |


### Compilazione dinamica di una descrizione comando o di un testo del Reader di schermate personalizzato

È inoltre possibile popolare dinamicamente un&#39;alternativa testuale di un controllo modulo, ad esempio la descrizione comando, con un valore proveniente da un&#39;origine dati. Ad esempio, è possibile visualizzare una descrizione personalizzata per un oggetto in francese.
Per una descrizione comandi dello schema a cui ci si connette è possibile definire quanto segue:


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


Nel file di dati a cui si fa riferimento, per una descrizione comando potrebbe essere definito quanto segue:

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. Nella tavolozza Libreria oggetti fare clic sulla categoria Standard e trascinare un oggetto nella struttura del modulo. Inserire ad esempio un oggetto Campo di testo.
1. (Facoltativo) Nella tavolozza Oggetto, fare clic sulla scheda Campo e digitare una didascalia per l&#39;oggetto nella casella Didascalia. Ad esempio, digitare Quantité.
1. Nella tavolozza Accessibilità fare clic sull&#39;etichetta attiva Descrizione comando.
1. Seleziona la connessione dati.
1. Fare clic sul triangolo accanto alla casella Associazione e selezionare un&#39;associazione. Ad esempio, seleziona descrizione > @dp_tt.

Nella casella Associazione viene visualizzata la stringa seguente: $record.tooltip.dp_tt Suggerimento: è possibile digitare questa stringa nella casella Elementi anziché selezionarla.
1. Fare clic su OK.
1. Visualizzare il modulo nella scheda Anteprima PDF.

### Inserimento di testo di collegamento

Gli utenti delle tecnologie per l’accessibilità possono utilizzare metodi diversi per la lettura del testo collegato. Ad esempio, gli utenti di utilità di lettura dello schermo spesso utilizzano un elenco di collegamenti come quello mostrato nella Figura 6 per analizzare rapidamente i collegamenti disponibili in una pagina.

![Finestra di dialogo Elenco collegamenti JAWS](/help/forms/using/assets/image-6.png)

Figura 6: **Finestra di dialogo Elenco collegamenti JAWS**

Per questo motivo i collegamenti devono essere auto-descrittivi; questo è il loro significato non dovrebbe dipendere dal loro contesto (il testo circostante). Ad esempio, l’elemento collegamento potrebbe essere costituito dalle parole &quot;fai clic qui&quot; nella frase &quot;fai clic qui per scaricare il modulo di richiesta&quot;. Un collegamento di questo tipo risulterebbe di difficile comprensione quando si legge in un elenco di collegamenti, in particolare quando sono presenti più collegamenti contenenti lo stesso testo.

Quando si utilizzano i collegamenti nel modulo, assicurarsi che ogni collegamento descriva correttamente lo scopo, senza dipendere dal testo circostante o dalla posizione nella pagina. Ad esempio, invece di utilizzare una frase come &quot;Fai clic qui&quot; come testo di collegamento, utilizza &quot;Scarica modulo dell’applicazione&quot; come testo di collegamento.

**Punti di controllo correlati**

* Sezione 508 §1194.21
   * (d) Le tecnologie per l&#39;accessibilità devono disporre di informazioni sufficienti su un elemento dell&#39;interfaccia utente, compresa l&#39;identità, il funzionamento e lo stato dell&#39;elemento. Quando un’immagine rappresenta un elemento del programma, anche le informazioni trasmesse dall’immagine devono essere disponibili nel testo.
   * (l) Quando si utilizzano moduli elettronici, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità richieste per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.
* Sezione 508 §1194.22
   * (n) Se i moduli elettronici sono concepiti per essere compilati in linea, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità necessarie per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti.
* WCAG 1.0
   * 12.4 Associare esplicitamente le etichette ai relativi controlli (P2).
   * 13.1 Identificare chiaramente il target di ciascun collegamento (P2).
* WCAG 2.0
   * 1.1.1 Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito. (Livello A)
   * 2.4.6 Intestazioni ed etichette: le intestazioni e le etichette descrivono l’argomento o la finalità. (livello AA)
   * 3.2.4 Identificazione coerente: i componenti che hanno la stessa funzionalità all’interno di un insieme di pagine web sono identificati in modo coerente. (livello AA)
   * 3.3.2 Etichette o istruzioni: quando il contenuto richiede l’intervento dell’utente, vengono fornite etichette o istruzioni. (Livello A)
   * 4.1.2 Nome, ruolo, valore: per tutti i componenti dell’interfaccia utente (inclusi ma non limitati a: elementi di un modulo, collegamenti e componenti generati da script), il nome e il ruolo possono essere determinati programmaticamente; stati, proprietà e valori che possono essere impostati dall’utente possono essere impostati programmaticamente; e la notifica delle modifiche a questi elementi è disponibile per gli agenti utente, incluse le tecnologie per l’accessibilità. (Livello A)


## Verificare che l&#39;ordine di lettura e di tabulazione sia corretto {#ensure-reading-tab-order}

È molto importante garantire un ordine di lettura significativo durante la progettazione di moduli accessibili agli utenti con problemi di vista o altre disabilità. Questi utenti in genere non utilizzano il mouse per spostarsi all’interno di un modulo, quindi dipendono dalla tastiera. L&#39;ordine di lettura determina la sequenza utilizzata dagli utenti di utilità di lettura dello schermo durante la lettura del modulo. Inoltre, l&#39;ordine di tabulazione consente agli utenti di passare rapidamente da un controllo modulo interattivo al successivo utilizzando i tasti TAB o MAIUSC+TAB. Un ordine di tabulazione logico garantisce l&#39;accesso a tutti i campi del modulo e la possibilità di spostarsi all&#39;interno del modulo in modo intelligente ed efficiente.

L&#39;ordine di lettura del modulo include tutti gli oggetti statici, ad esempio testo e immagini, e gli oggetti campo, ma solo i controlli del modulo interattivi fanno parte dell&#39;ordine di tabulazione.

>[!NOTE]
> In molti casi, l&#39;ordine di tabulazione è strettamente correlato all&#39;ordine di lettura. Per semplicità, in questa guida verrà utilizzato il termine &quot;ordine di tabulazione&quot; al posto di &quot;ordine di tabulazione o di lettura&quot;.

### Ordine di tabulazione predefinito nei moduli Designer di LiveCycle

L&#39;ordine di tabulazione predefinito viene creato automaticamente quando si salva il modulo come PDF con tag. Inizialmente, l&#39;ordine di tabulazione in un modulo viene determinato in base alla posizione locale degli oggetti utilizzando le regole riportate di seguito.

* Tutti gli oggetti vengono ordinati da sinistra a destra e dall&#39;alto verso il basso (ordine locale), a partire dall&#39;angolo superiore sinistro della maschera.
* Tutte le sottomaschere create vengono trattate come unità autonome e vengono spostate da sinistra a destra e dall&#39;alto verso il basso. Se due sottomaschere sono posizionate una accanto all&#39;altra, entrambe contenenti oggetti, l&#39;ordine di lettura passa a tutti gli oggetti della prima sottomaschera prima di passare alla sottomaschera successiva.

Per i moduli semplici, ovvero i moduli con un layout da sinistra a destra e dall&#39;alto al basso, l&#39;ordine di tabulazione predefinito è in genere corretto. Per verificare questo aspetto, è necessario esaminare l&#39;ordine di tabulazione predefinito prima di pubblicare il modulo. È possibile rendere visibile l&#39;ordine di tabulazione utilizzando uno dei metodi seguenti:

* Scegliete Visualizza > Mostra ordine tabulazioni.
* Fare clic su Mostra ordine nella tavolozza Ordine schede.

Tutti gli oggetti vengono visualizzati con un numero nell&#39;angolo superiore destro, che indica la posizione dell&#39;oggetto nell&#39;ordine di tabulazione predefinito. Gli oggetti interattivi in questa sequenza formano l&#39;ordine di tabulazione. La Figura 7 mostra la visualizzazione dell’ordine di lettura di un modulo di base.

![Visualizzazione dell&#39;ordine di lettura predefinito per un modulo d&#39;ordine tipico](/help/forms/using/assets/image-7.png)

Figura 7: **Visualizzazione dell&#39;ordine di lettura predefinito per un modulo ordine tipico**

Ogni numero di ordine di tabulazione viene visualizzato in una forma colorata. Le forme hanno il seguente significato:
* I cerchi grigi (#1 e #4) vengono utilizzati per gli oggetti nell&#39;area del contenuto.
* I cerchi verdi (#6 e #7) vengono utilizzati per gli oggetti della pagina master.
* I quadrati di lavanda (#2 e #3) vengono utilizzati per gli oggetti all’interno di un frammento.

È possibile scegliere di visualizzare solo i controlli modulo interattivi (che costituiscono l&#39;ordine di tabulazione) o tutti gli oggetti nell&#39;ordine di lettura (che include anche oggetti statici come testo e immagini). Per modificare questa preferenza, scegliere Strumenti > Opzioni > Ordine schede e selezionare Mostra solo ordine schede per campi.

In un modulo complesso, può essere difficile vedere come la tabulazione scorre da un oggetto all’altro. È possibile utilizzare gli strumenti visivi per visualizzare il flusso di tabulazione nel modulo. Con gli strumenti visivi attivati, quando si posiziona il puntatore sull&#39;oggetto, le frecce blu mostrano il flusso di tabulazione per i due oggetti precedenti e seguenti nell&#39;ordine di tabulazione (vedere Figura 8).

![Gli strumenti visivi evidenziano l&#39;ordine di tabulazione](/help/forms/using/assets/image-8.png)

Figura 8: **Gli strumenti visivi evidenziano l&#39;ordine di tabulazione**

Per attivare gli strumenti visivi, utilizzare i metodi seguenti:
* Scegliete Strumenti > Opzioni > Ordine schede e, nel pannello Ordine schede, selezionate Visualizza altri strumenti visivi per ordine schede.
* Nel menu della tavolozza Ordine schede, selezionare Mostra strumenti visivi.

### Utilizzo della posizione per influenzare l&#39;ordine di tabulazione predefinito

Per modificare l&#39;ordine di tabulazione predefinito, è possibile modificare le coordinate di un oggetto spostandolo in una posizione diversa. Ad esempio, nella Figura 9, il campo Nome prodotto viene visualizzato nell&#39;ordine di tabulazione prima del campo Quantità. Per modificare questo ordine, è possibile spostare il campo Nome prodotto in modo che venga posizionato sotto o a destra del campo Quantità.

![L&#39;ordine di tabulazione predefinito è da sinistra a destra](/help/forms/using/assets/image-9.png)

Figura 9: **L&#39;ordine di tabulazione predefinito è da sinistra a destra**

È possibile modificare la posizione di un oggetto effettuando una delle seguenti operazioni:
* Trascinarlo con il mouse
* Selezionala e spostala utilizzando i tasti freccia della tastiera.

>[!NOTE]
> Può essere utile mantenere l&#39;allineamento degli oggetti scegliendo Visualizza > Blocca sulla griglia.

Potete modificare le coordinate di un oggetto in modo più preciso utilizzando la tavolozza Layout (mostrata nella Figura 10). Questa tavolozza consente di specificare le coordinate X e Y, nonché la larghezza e l&#39;altezza dell&#39;oggetto.

![Utilizzo delle coordinate per posizionare con precisione un oggetto con la tavolozza Layout](/help/forms/using/assets/image-10.png)

Figura 10: **Utilizzo di coordinate per posizionare con precisione un oggetto con la tavolozza Layout**

>[!NOTE]
> Quando la didascalia e il controllo non vengono uniti, la posizione della didascalia di un controllo modulo è indipendente dall&#39;ordine in cui gli assistenti vocali leggono l&#39;oggetto e i relativi elementi. Per ulteriori informazioni sui sottotitoli, vedere la sezione 2.5 Fornire etichette appropriate per i controlli modulo in questa guida.

### Utilizzo delle sottomaschere per influenzare l&#39;ordine di tabulazione predefinito

Come accennato in precedenza, le sottomaschere consentono di inserire gruppi di oggetti con un proprio ordine di tabulazione. È possibile creare una sottomaschera eseguendo una delle operazioni seguenti:
* Scegliere Inserisci > Standard > Sottomaschera.
* Selezionare gli oggetti nella tavolozza Gerarchia e raggrupparli in una sottomaschera scegliendo Inserisci > Racchiudi in sottomaschera.
* Selezionare gli oggetti nella maschera effettiva, fare clic con il pulsante destro del mouse sulla selezione e scegliere Racchiudi nella sottomaschera

Quando due sottomaschere contenenti oggetti campo vengono posizionate una accanto all&#39;altra, la sequenza di tabulazione passa attraverso i campi della prima sottomaschera prima di passare a quella successiva. Questo è illustrato nella Figura 11, in cui due sottomaschere vengono utilizzate per creare un ordine di tabulazione predefinito basato su colonne.

![Ordine di tabulazione predefinito tramite sottomaschere](/help/forms/using/assets/image-11.png)

Figura 11: **Ordine di tabulazione predefinito tramite sottomaschere**

Le sottomaschere, i pulsanti di scelta e le aree contenuto, insieme alla posizione verticale degli oggetti su una pagina e sulla relativa pagina master, influenzano tutti l&#39;ordine di tabulazione.

### Creazione di un ordine di tabulazione personalizzato mediante la tavolozza Ordine di tabulazione

È possibile modificare l&#39;ordine di tabulazione predefinito quando è necessaria una sequenza diversa nel modulo e la modifica non può essere eseguita con il posizionamento o il raggruppamento nelle sottomaschere. Per modificare l&#39;ordine di tabulazione predefinito è possibile creare un ordine di tabulazione personalizzato utilizzando la tavolozza Ordine di tabulazione.
La tavolozza Ordine di tabulazione (vedere Figura 12) consente di verificare e modificare l&#39;ordine in cui gli oggetti del modulo vengono letti dalla tecnologia di accesso facilitato e spostati mediante il tasto TAB dell&#39;utente.

![Tavolozza Ordine schede](/help/forms/using/assets/image-12.png)

Figura 12: **Tavolozza Ordine schede**

La tavolozza Ordine tabulazioni fornisce una visualizzazione alternativa dell&#39;ordine di tabulazione nel modulo. Vengono visualizzati tutti gli oggetti del modulo sotto forma di elenco numerato, in cui ogni numero rappresenta la posizione dell&#39;oggetto nel flusso di tabulazione.
Per aprire la tavolozza Ordine schede, scegliete Finestra > Ordine schede.


La tavolozza Ordine tabulazioni fornisce i seguenti marcatori visivi:
* Una barra grigia contrassegna ogni pagina del modulo. L&#39;ordine di tabulazione in ogni pagina inizia con il numero 1.
* La lettera M all&#39;interno di un cerchio verde indica gli oggetti della pagina master (visibili solo quando si visualizza la maschera nella scheda Visualizzazione Struttura).
* Un intervallo di numeri indica gli oggetti all’interno di un frammento.
* Uno sfondo giallo indica l&#39;elemento attualmente selezionato.
* Un&#39;icona di blocco accanto al primo oggetto della pagina indica che l&#39;oggetto non può essere spostato nell&#39;ordine di tabulazione (visibile solo quando si visualizza il modulo nella scheda Pagine master).

Nell&#39;elenco vengono visualizzati gli stessi numeri di ordine di tabulazione dei numeri visualizzati nella maschera quando si sceglie Visualizza > Mostra ordine di tabulazione. Per modificare la posizione di un oggetto nell&#39;ordine di tabulazione, spostare l&#39;oggetto verso l&#39;alto o verso il basso nell&#39;elenco della tavolozza Ordine tabulazioni. È possibile spostare un singolo oggetto o un gruppo di oggetti. Tale obiettivo può essere conseguito mediante uno dei seguenti metodi:

* Trascinare l&#39;oggetto selezionato in alto o in basso nell&#39;elenco e posizionarlo nella posizione desiderata. Una maniglia nera contrassegna la posizione corrente all&#39;interno dell&#39;elenco prima di posizionare l&#39;oggetto.
* Nella tavolozza Ordine tabulazioni fare clic sui pulsanti freccia su o freccia giù fino a quando l&#39;oggetto selezionato non viene posizionato nella posizione corretta. In alternativa, premere CTRL+freccia SU o CTRL+freccia GIÙ.
* Nel menu della tavolozza Ordine tabulazioni, selezionare Sposta su o Sposta giù.
* Nell&#39;elenco della tavolozza Ordine tabulazioni fare clic sull&#39;oggetto selezionato oppure selezionarlo e premere F2 per rendere modificabile il numero visualizzato accanto al nome dell&#39;oggetto. Digitare quindi il numero che indica la nuova posizione dell&#39;oggetto nell&#39;ordine di tabulazione e premere Invio.
* Selezionate Copia (Copy) dal menu della tavolozza Ordine tabulazioni (Tab Order) e, nell&#39;elenco, selezionate l&#39;oggetto sopra il quale posizionare l&#39;oggetto che state spostando, quindi selezionate Incolla (Paste) dal menu.

Quando si sposta l&#39;oggetto in una nuova posizione nell&#39;ordine, LiveCycle Designer riassegna i numeri di ordine di tabulazione. Sebbene l&#39;ordine di tabulazione per gli oggetti che si trovano in una pagina master sia visualizzato nella scheda Visualizzazione Struttura, è possibile modificare l&#39;ordine di questi oggetti solo nella scheda Pagine master. Se nel modulo si utilizzano i riferimenti ai frammenti, l’ordine di tabulazione all’interno di un frammento è visibile quando si visualizza l’ordine del modulo. Per modificare l’ordine di tabulazione all’interno di un frammento, è necessario aprire il file di origine del frammento per la modifica, apportare la modifica e salvare il file. Questa modifica interessa tutti i moduli che utilizzano questo frammento.

Se si decide di non utilizzare l&#39;ordine di tabulazione personalizzato nel modulo, è possibile tornare rapidamente all&#39;ordine di tabulazione automatico (predefinito) eseguendo le operazioni riportate di seguito. Qualsiasi modifica apportata all&#39;ordine di tabulazione andrà persa:
1. Nella tavolozza Ordine schede, selezionare Automatico.
1. Nella finestra di messaggio visualizzata, fare clic su Sì per confermare la rimozione dell&#39;ordine di tabulazione personalizzato.

**Punti di controllo correlati**
* Sezione 508 §1194.21
   * (a) Quando il software è progettato per essere eseguito su un sistema dotato di tastiera, le funzioni del prodotto devono essere eseguibili da una tastiera in cui la funzione stessa o il risultato dell&#39;esecuzione di una funzione possono essere individuati testualmente.
* WCAG 1.0
   * 9.2 Assicurarsi che qualsiasi elemento con una propria interfaccia possa essere utilizzato in modo indipendente dal dispositivo.
* WCAG 2.0
   * 1.3.2 Sequenza significativa: quando la sequenza in cui il contenuto è presentato influisce sul suo significato, si può determinare programmaticamente una sequenza di lettura corretta. (Livello A)
   * 2.1.1 Tastiera: tutte le funzionalità del contenuto sono utilizzabili tramite un&#39;interfaccia di tastiera senza richiedere tempi specifici per la pressione dei singoli tasti, salvo il caso in cui la funzione di base richieda un input che dipende dal percorso del movimento dell&#39;utente e non solo dagli endpoint. (Livello A)
   * 2.1.3 Tastiera (nessuna eccezione): tutte le funzionalità del contenuto sono utilizzabili tramite un&#39;interfaccia di tastiera senza richiedere tempi specifici per la pressione dei singoli tasti. (livello AAA)
   * 2.4.3 Ordine del focus: se è possibile navigare in una pagina web in modo sequenziale e le sequenze di navigazione influiscono sul suo significato o sul suo funzionamento, i componenti attivabili ricevono lo stato attivo in un ordine che ne mantenga il significato e l’operabilità. (Livello A)


## Assicurarsi che i controlli del modulo siano accessibili da tastiera{#ensure-keyboard-accessible}

Gli utenti devono essere in grado di compilare completamente il modulo utilizzando solo la tastiera o un dispositivo di input alternativo equivalente. Gli utenti con mobilità ridotta o problemi di vista potrebbero non avere altra scelta se non quella di utilizzare la tastiera, e molti utenti che possono utilizzare un mouse preferiscono semplicemente l&#39;input da tastiera. Consentendo l&#39;utilizzo di diversi metodi di input, non solo si creano moduli accessibili, ma si creano anche moduli più adatti alle preferenze di tutti gli utenti.

In Designer di LiveCycle, il modo più semplice per garantire l&#39;accesso da tastiera ai controlli consiste nell&#39;utilizzare i controlli elencati nella scheda Comune della tavolozza Libreria oggetti. Per impostazione predefinita, questi controlli rispondono sia all&#39;input del mouse che a quello della tastiera. Per ulteriori informazioni, vedere la sezione 2.3 Scegliere i controlli appropriati in questa guida.

Un altro aspetto importante dell&#39;accessibilità della tastiera è garantire che ogni elemento interattivo sia incluso nell&#39;ordine di tabulazione del modulo. In questo modo l&#39;utente può spostare il cursore avanti e indietro nel modulo utilizzando i tasti TAB e MAIUSC+TAB. Assicurarsi di impostare un ordine di tabulazione logico che includa tutti i campi e i pulsanti. Per ulteriori informazioni, vedere la sezione 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto in questa guida.

Infine, è importante garantire che anche il comportamento basato su script sia accessibile da tastiera e non dipenda da eventi specifici del dispositivo. L&#39;evento mouse MouseEnter, ad esempio, non può essere eseguito utilizzando la tastiera. Inoltre, tali gestori di eventi non devono interferire con l’accessibilità della tastiera. Ad esempio, assicurati che gli eventi di modifica utilizzati negli elenchi a discesa o nelle caselle di riepilogo non attivino azioni impreviste.

**Punti di controllo correlati**
* Sezione 508 §1194.21
   * (a) Quando il software è progettato per essere eseguito su un sistema dotato di tastiera, le funzioni del prodotto devono essere eseguibili da una tastiera in cui la funzione stessa o il risultato dell&#39;esecuzione di una funzione possono essere individuati testualmente.
* WCAG 1.0
   * 6.4 Per script e applet, assicurarsi che i gestori eventi siano indipendenti dal dispositivo di input (P2).
   * 9.2 Accertarsi che qualsiasi elemento con una propria interfaccia possa essere utilizzato in modo indipendente dal dispositivo (P2).
   * 9.3 Per gli script, specificare gestori di eventi logici anziché gestori di eventi dipendenti dal dispositivo (P2).
* WCAG 2.0
   * 2.1.1 Tastiera: tutte le funzionalità del contenuto sono utilizzabili tramite un&#39;interfaccia di tastiera senza richiedere tempi specifici per la pressione dei singoli tasti, salvo il caso in cui la funzione di base richieda un input che dipende dal percorso del movimento dell&#39;utente e non solo dagli endpoint. (Livello A)
   * 2.1.2 Nessun impedimento all’uso della tastiera: se è possibile spostare lo stato attivo su un componente della pagina utilizzando un’interfaccia di tastiera, lo stato attivo può essere spostato da tale componente utilizzando solo un’interfaccia di tastiera e, se non sono necessari tasti freccia o tasto TAB non modificati o altri metodi di uscita standard, l’utente è informato del metodo per spostare lo stato attivo. (Livello A)
   * 2.1.3 Tastiera (nessuna eccezione): tutte le funzionalità del contenuto sono utilizzabili tramite un&#39;interfaccia di tastiera senza richiedere tempi specifici per la pressione dei singoli tasti. (livello AAA)


## Usa il colore in modo responsabile{#use-color-responsibly}

La progettazione di moduli per l&#39;accessibilità comporta l&#39;analisi di alcune linee guida aggiuntive per l&#39;utilizzo dei colori. I progettisti utilizzano i colori per migliorare l&#39;aspetto delle maschere evidenziandone i vari componenti. L&#39;uso improprio del colore, tuttavia, può rendere le informazioni nel modulo difficili o impossibili da leggere da parte di persone con disabilità.

### Non trasmettere informazioni utilizzando solo il colore

I colori possono enfatizzare e migliorare alcune parti del modulo, ma non è consigliabile trasmettere le informazioni in base al solo colore.

Qualsiasi informazione trasmessa esclusivamente a colori (con significato semantico) non è accessibile agli utenti non vedenti. Lo stesso vale per gli utenti con problemi di percezione dei colori o per gli utenti che utilizzano combinazioni di colori diverse, ad esempio uno schermo a colori ad alto contrasto con testo bianco o in primo piano su sfondo nero. È inoltre necessario tenere presente che gli assistenti vocali non sono in grado di rilevare automaticamente le informazioni sui colori.

La Figura 13 mostra ad esempio un campo modulo con una didascalia rossa (specificata utilizzando la tavolozza Carattere) per indicare che il campo modulo è obbligatorio. In questo esempio, il colore è l&#39;unico a significare la differenza tra i campi di input obbligatori e quelli facoltativi, rendendo impossibile per gli utenti non vedenti o con determinati tipi di cecità del colore distinguerli.

![Utilizzo del solo colore per trasmettere le informazioni](/help/forms/using/assets/image-13.png)

Figura 13: **Utilizzo del solo colore per trasmettere informazioni**

Per risolvere questo problema, indicare anche lo stato obbligatorio del modulo nel testo alternativo del controllo modulo (come descritto nella sezione 2.5 Fornire etichette appropriate per i controlli modulo). Ad esempio, puoi impostare il testo dell’assistente vocale su &quot;Codice postale (obbligatorio)&quot;. Per gli utenti che hanno difficoltà a visualizzare il colore in determinate combinazioni, si consiglia di impostare il tipo di campo di testo su Inserito dall&#39;utente - Obbligatorio nella palette Oggetto, oltre al testo alternativo che indica che il campo è obbligatorio. In alternativa, è possibile utilizzare indicazioni diverse dal colore, ad esempio testo visivo, stili di testo e stili di bordo. Tuttavia, gli utenti di utilità di lettura dello schermo dovranno comunque trasmettere le informazioni richieste utilizzando la palette Accessibilità.

Inoltre, quando fornisci descrizioni o istruzioni all’utente del modulo, tieni presente che le istruzioni basate sul solo colore non sono sufficienti per gli utenti con disabilità visive. Ad esempio, invece di un&#39;istruzione come, &quot;Fai clic sul pulsante verde per continuare&quot;, utilizza una descrizione testuale per le azioni, come &quot;Fai clic sul pulsante Successivo per continuare&quot;.

>[!NOTE]
> Questa best practice non vieta l’uso del colore. Vieta l&#39;uso del colore come unico mezzo per trasmettere informazioni importanti. Se per questo tipo di informazioni è ancora necessaria un&#39;indicazione visiva, il progettista potrebbe utilizzare un asterisco o un indicatore visivo simile per contrassegnare i campi obbligatori.

### Fornire un contrasto del colore sufficiente

Molti utenti con problemi di vista si affidano a un contrasto elevato tra testo e sfondo per leggere i moduli. Quando il contrasto tra i colori di sfondo e di primo piano non è sufficiente, un modulo può diventare difficile, se non impossibile, da leggere per alcuni utenti. La figura 14 mostra un esempio di modulo con contrasto insufficiente.

![Modulo con contrasto colore insufficiente](/help/forms/using/assets/image-14.png)

Figura 14: **Modulo con contrasto cromatico insufficiente**

Si consiglia vivamente di utilizzare il carattere e i colori di sfondo predefiniti: il nero su sfondo bianco. Se è necessario modificare questi colori predefiniti, assicurarsi di scegliere una combinazione appropriata di colori ad alto contrasto; utilizzare un colore di primo piano scuro su uno sfondo chiaro o viceversa. Per essere certi, usate uno strumento (come WAT-C Color Contrast Analyzer) per verificare che il contrasto sia sufficiente.

Adobe Reader e Adobe Acrobat consentono agli utenti di specificare se i colori devono essere sostituiti per soddisfare le loro esigenze visive. Gli utenti possono specificare il proprio schema di contrasto o scegliere di utilizzare uno schema fornito dal sistema operativo. Inoltre, Adobe Reader e Adobe Acrobat dispongono di uno schema di contrasto elevato che può essere abilitato. Affinché queste opzioni abbiano successo, l&#39;approccio migliore è quello di utilizzare sempre i colori predefiniti.

Durante la progettazione del modulo, verificarlo frequentemente utilizzando una combinazione di colori simile a quella utilizzata da molti utenti con problemi di vista per completare il modulo. Questa procedura consente di individuare e correggere i problemi nelle prime fasi del processo di progettazione.

Recommendations per l&#39;utilizzo dei colori:
* Assicurati che non vadano perse informazioni se il colore semantico non è visibile.
* Se non è possibile utilizzare i colori predefiniti, verificare che i colori siano a contrasto elevato, ad esempio il nero su uno sfondo chiaro (bianco). Gli utenti ipovedenti in genere richiedono un elevato contrasto tra il testo e il relativo sfondo per poterlo leggere.
* Verificare la leggibilità dei moduli passando a uno schermo a contrasto elevato, sia in Windows che in Adobe Reader o Adobe Acrobat. Mac OSX offre solo un filtro semplice in scala di grigi per un contrasto elevato, quindi non è sufficiente per il test.
* Non trasmettere informazioni esclusivamente in base al colore. Ad esempio, non utilizzare solo il colore per evidenziare parti di testo importanti. Utilizzare anche altri metodi di evidenziazione e descrizioni testuali.
* Non utilizzare troppi colori, in quanto ciò può rendere difficile la lettura delle informazioni effettive nel contenuto. Quando si decide quali colori utilizzare, è sempre necessario mantenere la leggibilità delle informazioni come priorità principale.

**Punti di controllo correlati**
* Sezione 508 §1194.21
   * (i) La codifica a colori non deve essere utilizzata come unico mezzo per trasmettere informazioni, indicare un’azione, sollecitare una risposta o distinguere un elemento visivo.
* WCAG 1.0
   * 2.1 Accertatevi che tutte le informazioni trasmesse con il colore siano disponibili anche senza colore, ad esempio dal contesto o dal markup.
   * 2.2 Assicurati che le combinazioni di colori di primo piano e di sfondo forniscano un contrasto sufficiente quando vengono visualizzate da persone con deficit di colore o su uno schermo in bianco e nero. [Priorità 2 per le immagini, Priorità 3 per il testo] (P2).
* WCAG 2.0
   * 1.4.1 Uso del colore: il colore non è utilizzato come unico mezzo visivo per trasmettere informazioni, indicare un&#39;azione, richiedere una risposta o distinguere un elemento visivo. (Livello A)
   * 1.4.3 Contrasto (minimo): la presentazione visiva di testo e immagini di testo ha un rapporto di contrasto di almeno 4,5:1, con le seguenti eccezioni: (livello AA)
   * 1.4.6 Contrasto (ottimizzato): la presentazione visiva di testo e immagini di testo ha un rapporto di contrasto di almeno 7:1, con le seguenti eccezioni: (Livello AAA)


## Fornire celle di intestazione per le tabelle{#provide-heading-cells}

Le tabelle sono un modo efficace per organizzare e presentare il contenuto in moduli accessibili. Se utilizzate in modo appropriato, le righe e le colonne di una tabella forniscono una struttura prevedibile e coerente per il contenuto del modulo. Ad esempio, quando un utente di utilità di lettura dello schermo passa a una cella della riga del corpo, l’utilità di lettura dello schermo specifica la posizione della cella e quindi legge il contenuto della cella. L&#39;assistente vocale specifica la posizione della cella utilizzando una combinazione di intestazioni di riga e di colonna o numeri di riga e di colonna. Poiché gli assistenti vocali forniscono informazioni che orientano l’utente alla posizione del contenuto nella tabella, il suo layout influisce direttamente sull’accessibilità della tabella.

Durante la creazione delle tabelle è possibile specificare i seguenti ruoli per gli elementi di tabella. Questi ruoli consentono agli assistenti vocali di navigare nella struttura della tabella utilizzando scelte rapide speciali e trasmettono all’utente la relazione tra le celle della tabella e le celle di intestazione corrispondenti.
* Tabella
Assegna il ruolo di una tabella alla sottomaschera selezionata. Quando l’utente passa a questa sottomaschera, la maggior parte degli assistenti vocali la identifica come tabella e indica il numero di righe e colonne.
* Riga intestazione
Assegna il ruolo di una riga di intestazione alla sottomaschera o alla riga di tabella selezionata. Quando si parla del contenuto di una cella della riga del corpo, la maggior parte degli assistenti vocali identifica innanzitutto il contenuto della cella corrispondente nella riga dell’intestazione.
* Riga corpo
Assegna il ruolo di una riga corpo alla sottomaschera o alla riga tabella selezionata. Se una cella contiene una sottomaschera, gli assistenti vocali in genere parlano il contenuto della cella corrispondente nella riga di intestazione, seguito dai campi nella sottomaschera.
* Riga piè di pagina
Assegna il ruolo di una riga di piè di pagina alla sottomaschera o alla riga di tabella selezionata.
* (Nessuno)
Specifica una riga che trasmette informazioni sulla tabella o sul relativo contenuto. La riga non è considerata parte della tabella; tuttavia, l’assistente vocale ne legge il contenuto.

Se utilizzate correttamente, le tabelle sono un modo efficace per organizzare e presentare le informazioni tabulari. Evita tabelle troppo complesse, ad esempio quelle con tabelle e sezioni nidificate.

### Rendere accessibili tabelle semplici

Si consiglia di utilizzare tabelle con layout semplici. Le tabelle semplici iniziano con una singola riga di intestazione seguita dalle righe del corpo.

Durante la progettazione di tabelle semplici per l&#39;accessibilità, tenere presenti le seguenti linee guida:

* L&#39;ordine di tabulazione di una tabella è l&#39;ordine geografico, che è lo stesso della maschera stessa. Assicurati che il contenuto della tabella sia organizzato in modo appropriato quando letto da sinistra a destra e dall’alto al basso.
* La maggior parte degli assistenti vocali interpreta la prima riga di una tabella come riga di intestazione. Durante la lettura del contenuto di una cella della riga del corpo, questi assistenti vocali leggono innanzitutto il contenuto della cella della riga dell’intestazione associata. Assicurati che il contenuto di ogni cella della riga di intestazione descriva in modo significativo il contenuto della colonna.
* Evitare le celle che si estendono su due o più colonne, tabelle nidificate o sezioni di tabella. Alcuni assistenti vocali hanno difficoltà a interpretare correttamente queste funzioni o potrebbero non utilizzarle. Ad esempio, se una cella in una riga del corpo si estende su due colonne, gli assistenti vocali potrebbero non fare riferimento al contenuto corretto della cella nella riga di intestazione durante la lettura della cella successiva nella riga.

### Rendere accessibili tabelle complesse

Durante la progettazione di tabelle per l’accessibilità, cerca di mantenere semplice il layout della tabella, con una riga di intestazione seguita da righe del corpo. Naturalmente, alcuni contenuti potrebbero richiedere un layout di tabella più complesso. Ad esempio, potrebbe essere necessario utilizzare l’estensione delle celle o più intestazioni per trasmettere efficacemente il contenuto.

È possibile creare tabelle complesse utilizzando l&#39;oggetto tabella o combinando oggetti sottomaschera. L&#39;oggetto table consente di utilizzare caratteristiche che facilitano il processo di progettazione, ad esempio le opzioni per l&#39;inserimento e il ridimensionamento di colonne e righe.

Tramite la tavolozza Accessibilità è possibile specificare ruoli correlati alle tabelle nelle sottomaschere per creare una tabella complessa accessibile. A seconda dell&#39;esperienza di progettazione e delle preferenze, è possibile scegliere di creare tabelle complesse combinando oggetti sottomaschera. È ad esempio possibile creare una sottomaschera che includa due righe e specificare questa sottomaschera come intestazione per la tabella e specificare un&#39;altra sottomaschera per le righe del corpo della tabella.

Quando si utilizzano oggetti sottomaschera invece di oggetti tabella per creare tabelle, sono necessari i seguenti passaggi aggiuntivi:
* Nella scheda Sottomaschera impostare il tipo di ogni sottomaschera su Posizionato.
* Nella tavolozza Accessibilità impostare il ruolo di sottomaschera appropriato per ogni sottomaschera che costituisce la tabella. Ad esempio, assegnare il ruolo di riga intestazione alla sottomaschera utilizzata come intestazione della tabella.
* Per le righe che contengono informazioni sulla tabella o sul relativo contenuto ma che non sono considerate parte della tabella, assegnare il ruolo Sottomaschera Nessuno. L’assistente vocale legge il contenuto della riga.

Le funzioni supportate dall&#39;utilità di lettura dello schermo determinano le informazioni lette per una tabella complessa. Si consideri ad esempio una tabella che include una riga di intestazione e una sezione con una riga di intestazione. Quando l’utente passa a una cella della riga del corpo nella sezione della tabella, gli assistenti vocali in genere leggono il seguente contenuto, nell’ordine in cui:
* Contenuto della cella appropriata nella riga di intestazione per la tabella
* Contenuto della cella appropriata nella riga di intestazione della sezione
* Contenuto della cella selezionata
Alcuni assistenti vocali, tuttavia, potrebbero non leggere il contenuto da entrambe le righe di intestazione.

Creare nomi o titoli visibili significativi per le tabelle. È possibile creare un nome di tabella come testo statico in Adobe LiveCycle Designer e posizionarlo davanti alla tabella. È possibile raggruppare una tabella e il relativo nome in una sottomaschera. Le sottomaschere sono particolarmente utili quando si desidera combinare oggetti associati in un layout.

Per i controlli nelle celle di tabella, l&#39;utilità di lettura dello schermo annuncia il testo della didascalia, della descrizione comando o dell&#39;utilità di lettura dello schermo personalizzata specificato per l&#39;oggetto. Se si desidera utilizzare l&#39;intestazione di colonna come testo alternativo per un controllo in una tabella, non fornire didascalia, descrizione comando o testo personalizzato per la lettura dello schermo. Si noti, tuttavia, che questa strategia non è sempre così chiara per gli utenti di utilità per la lettura dello schermo, in quanto gli assistenti vocali possono associare l’intestazione di colonna al controllo solo quando l’utente non è nella modalità di interazione del lettore.

**Punti di controllo correlati**
* Sezione 508 §1194.22
   * (g) Le intestazioni di riga e di colonna sono identificate per le tabelle di dati.
   * (h) Il markup è utilizzato per associare le celle di dati e le celle di intestazione delle tabelle di dati che presentano due o più livelli logici di intestazioni di riga o di colonna.
* WCAG 1.0
   * 5.1 Per le tabelle di dati, identificare le intestazioni di riga e di colonna (P1).
   * 5.2 Per le tabelle dati con due o più livelli logici di intestazioni di riga o di colonna, utilizzare il markup per associare le celle dati e le celle intestazione (P1)
* WCAG 2.0
   * 1.3.1 Informazioni e relazioni: le informazioni, la struttura e le relazioni trasmesse attraverso la presentazione possono essere determinate a livello di programmazione o sono disponibili nel testo. (Livello A)


## Fornire una struttura di moduli navigabile{#provide-navigable-form}

Quando una forma diventa lunga e complessa, la sua facilità d’uso sarà notevolmente influenzata dal modo in cui è strutturata. Così come un libro diventa più facile da comprendere quando è diviso in capitoli e sezioni, un modulo diventa più facile da utilizzare quando è diviso in titoli e sottotitoli. Questo partizionamento è particolarmente utile per gli utenti di utilità per la lettura dello schermo, per i seguenti motivi:
* Ogni intestazione indica all’utente di utilità di lettura dello schermo cosa ci si può aspettare dalla sezione che segue l’intestazione.
* Le utilità per la lettura dello schermo consentono di spostarsi rapidamente da un titolo all&#39;altro del modulo e di accedere a un elenco di titoli che fornisce una panoramica della struttura del documento e consente una navigazione rapida.

La disponibilità di meccanismi che consentono agli utenti di passare ad altre aree del modulo può rendere il modulo più pratico. È possibile aggiungere una struttura di intestazione al modulo utilizzando la tavolozza Accessibilità di LiveCycle Designer.

### Meccanismi di salto

Gli utenti vedenti possono scansionare una pagina in qualsiasi ordine. Possono iniziare guardando l’angolo in basso a destra della pagina e scorrere all’indietro il contenuto. Questa opzione non è disponibile per l’utente di utilità di lettura dello schermo, perché l’assistente vocale inizierà a leggere la pagina in alto a sinistra (come indicato nel codice sorgente) e si sposterà in ordine lineare. Inoltre, l’utente vedente può scansionare la pagina alla ricerca di collegamenti interessanti e attivarli con il mouse. L’utente che usa un’utilità di lettura dello schermo deve spostarsi nella pagina in sequenza.

Il modo più semplice ed efficace per rendere disponibile una struttura di modulo navigabile consiste nell&#39;utilizzare intestazioni strutturali ed elenchi definiti in modo appropriato nel modulo.
È inoltre possibile fornire meccanismi che consentano all&#39;utente di passare ad altre aree del modulo, ad esempio aggiungendo pulsanti di spostamento nella parte superiore e inferiore del modulo. Nella parte superiore di un modulo è possibile includere pulsanti quali Apri file di dati, Pagina precedente e Pagina successiva. Nella parte inferiore del modulo è possibile includere pulsanti quali Salva dati, Dati e-mail, Vai all&#39;inizio della pagina e Stampa.

I campi avanzati possono essere un modo efficace per semplificare la compilazione di alcuni moduli. Ad esempio, un modulo di richiesta di viaggio può avere diverse righe e colonne di campi. Se una riga specifica è vuota, premendo il tasto TAB sull&#39;ultimo elemento della riga si passa alla sezione successiva del modulo anziché continuare a scorrere i campi che rimangono vuoti.

### Aggiunta di titoli mediante la tavolozza Accessibilità

È possibile utilizzare la tavolozza Accesso facilitato per assegnare ruoli agli oggetti in base allo scopo per cui l&#39;oggetto viene utilizzato. Questi ruoli possono essere applicati per creare titoli a livelli diversi.

![Specifica di un ruolo di intestazione nella tavolozza Accesso facilitato](/help/forms/using/assets/image-15.png)
Figura 15: **Specificare un ruolo di intestazione nella tavolozza Accessibilità**

Per creare un’intestazione nel modulo, effettua le seguenti operazioni:

1. Identificare l&#39;inizio di ogni segmento logico del modulo utilizzando etichette di testo statiche,
1. Per ogni etichetta e selezionare una delle opzioni di intestazione come Ruolo nella tavolozza Accessibilità. I diversi livelli di titolo (da 1 a 6) consentono di creare una struttura di titolo nel modulo. Iniziare con il livello 1, quindi utilizzare il livello 2 e così via per le sottosezioni nidificate.

La maggior parte degli assistenti vocali consente agli utenti di navigare rapidamente tra gli elementi dell’intestazione in base al loro livello. La Figura 16 mostra una maschera divisa in segmenti più piccoli utilizzando le intestazioni. In questo esempio, viene utilizzata la seguente struttura di intestazione:

* Livello titolo 1: richiesta prodotto
   * Livello intestazione 2: dettagli ordine
      * Livello intestazione 3: opzioni di consegna
* Livello intestazione 2: informazioni aggiuntive
   * Livello intestazione 3: Dati personali
   * Livello intestazione 3: Indirizzo

![Strutturazione di un modulo tramite intestazioni](/help/forms/using/assets/image-16.png)

Figura 16: **Strutturazione di un modulo tramite intestazioni**

Queste intestazioni sono solo elementi di testo statico a cui sono state assegnate una dimensione di carattere specifica e un ruolo di intestazione con il livello appropriato.

>[!NOTE]
> La semplice modifica dell&#39;aspetto visivo di un&#39;etichetta di testo in modo che sembri un&#39;intestazione non consente agli assistenti vocali di riconoscerla come intestazione. È necessario applicare un ruolo di intestazione.

Assicurati sempre che l’ordine dei livelli di intestazione sia logico. Ad esempio, una sottosezione di un&#39;intestazione di livello 2 deve essere sempre un&#39;intestazione di livello 3. Non è necessario saltare i livelli quando si contrassegnano le sottosezioni. Gli utenti di utilità di lettura dello schermo utilizzano i diversi livelli per comprendere meglio la struttura del modulo. Ad esempio, dopo aver incontrato un’intestazione di livello 2, l’utente può utilizzare un collegamento per cercare le intestazioni di livello 3 e determinare se sono presenti sottosezioni. Se salti i livelli, l’utente avrà difficoltà a identificare queste sottosezioni.

### Marcatura di elenchi

A volte può essere utile aggiungere il contenuto dell’elenco al modulo. Gli elenchi sono utili per raggruppare gli elementi correlati e consentono agli utenti di utilità di lettura dello schermo di sapere quanti elementi sono presenti in un elenco e di spostarsi rapidamente oltre tale elenco. La corretta marcatura degli elenchi rende più chiara la struttura del modulo agli utenti di utilità di lettura dello schermo.

In LiveCycle Designer è possibile creare elenchi utilizzando sottomaschere con i seguenti passaggi:

1. Selezionare un sottomodulo contenente il contenuto da contrassegnare come voci di elenco.
1. Nella tavolozza Accessibilità selezionare Elenco come Ruolo.
1. Selezionare ogni sottomaschera nidificata all&#39;interno della sottomaschera Elenco e impostare il relativo ruolo su Voce elenco.

>[!NOTE]
> Un ruolo Voce di elenco può essere assegnato solo a una sottomaschera contenuta in una sottomaschera per la quale è stato specificato un ruolo Elenco. Non è possibile definire una tabella o una riga di tabella come un elenco o una voce di elenco. Una voce di elenco può tuttavia contenere una tabella.

**Punti di controllo correlati**
* Sezione 508 §11934.22
   * (o) Deve essere fornito un metodo che consenta agli utenti di saltare i collegamenti di navigazione ripetitivi.
* WCAG 1.0
   * 3.5 Utilizzare gli elementi intestazione per trasmettere la struttura del documento e utilizzarli in base alle specifiche (P2).
   * 3.6 Contrassegnare correttamente elenchi e voci di elenco. (P2).
   * 12.3 Dividere grandi blocchi di informazioni in gruppi più gestibili, se ciò è naturale e appropriato. (P2).
   * 13.3 Fornire informazioni sul layout generale di un sito, ad esempio una mappa del sito o un sommario.
   * 13.4 Utilizzare i meccanismi di navigazione in modo coerente (P2).
* WCAG 2.0
   * 1.3.2 Sequenza significativa: quando la sequenza in cui il contenuto è presentato influisce sul suo significato, si può determinare programmaticamente una sequenza di lettura corretta. (Livello A)
   * 2.4.1 Salto di blocchi: è disponibile un meccanismo per saltare blocchi di contenuto che si ripetono su più pagine web. (Livello A)
   * 2.4.5 Differenti modalità: sono disponibili più modalità per individuare una pagina web all’interno di un insieme di pagine web, salvo il caso in cui la pagina web sia il risultato o un passaggio di un processo. (livello AA)
   * 2.4.6 Intestazioni ed etichette: le intestazioni e le etichette descrivono l’argomento o la finalità. (livello AA)
   * 2.4.10 Intestazioni di sezione: i titoli di sezione vengono utilizzati per organizzare il contenuto. (livello AAA)
   * 3.2.3 Navigazione coerente: i meccanismi di navigazione che si ripetono su più pagine web all’interno di un insieme di pagine web si verificano nello stesso ordine relativo ogni volta che si ripetono, a meno che l’utente non avvii una modifica. (livello AA)


## Evitare l&#39;interruzione degli script{#avoid-disruptive-scripting}

Come parte del processo di progettazione del modulo, gli sviluppatori possono utilizzare gli script per fornire un’esperienza utente più ricca. È possibile aggiungere script alla maggior parte dei campi modulo e degli oggetti. Ad esempio, puoi creare script semplici per aggiornare dinamicamente i valori in un modulo interattivo in risposta all’input dell’utente.

Durante la progettazione di script per l&#39;accessibilità, tenere presenti le seguenti linee guida generali:

* Mantenere il contenuto del modulo esente da interruzioni visive. Ad esempio, evita le funzioni che causano sfarfallio, sfarfallio o spostamento del contenuto.
* Assicurarsi che le finestre popup vengano visualizzate solo come risultato delle azioni avviate dall&#39;utente. Analogamente, non consentire la modifica dello stato attivo corrente del modulo (la visualizzazione corrente dell&#39;utente) o la visualizzazione del contenuto, a meno che non sia stato avviato dall&#39;utente. Ad esempio, se l’utente compila dei campi nella metà inferiore del modulo, non consentire lo stato attivo nell’angolo superiore sinistro del modulo, a meno che l’utente non scelga di passare a questa posizione.
* Gli utenti con disabilità possono richiedere più tempo per fornire input nei campi. Non specificare risposte basate sul tempo per i campi di input.
* Tieni presente che gli script lato client possono interferire con gli assistenti vocali e le tastiere se lo script cambia lo stato attivo dell’applicazione client. Ad esempio, gli eventi change e mouseEnter, se utilizzati con elenchi a discesa o caselle di riepilogo, possono causare azioni impreviste. Verifica che gli script lato client non introducano problemi per gli utenti di utilità di lettura dello schermo e per gli utenti solo tastiera.
* Gli utenti delle tecnologie per l’accessibilità a volte avranno bisogno di più tempo per completare le attività. In tutti i casi in cui una routine temporizzata sta per scadere, visualizza un messaggio accessibile per consentire l’estensione. Le caselle di avviso create tramite JavaScript sono utilizzabili con la tecnologia per l&#39;accessibilità. È inoltre possibile distribuire una nuova finestra con un messaggio che avvisa l’utente di un timeout imminente.

**Punti di controllo correlati**:
* Sezione 508 §1194.22
   * (l) Quando le pagine utilizzano linguaggi di scripting per visualizzare il contenuto o per creare elementi di interfaccia, le informazioni fornite dallo script devono essere identificate con testo funzionale leggibile con la tecnologia per l’accessibilità.
   * (p) Quando è richiesta una risposta a tempo, l’utente deve essere avvisato e deve disporre di tempo sufficiente per indicare che è necessario più tempo.
* WCAG 1.0
   * 1.4 Per qualsiasi presentazione multimediale basata sul tempo (ad esempio, un filmato o un&#39;animazione), sincronizzare alternative equivalenti (ad esempio, didascalie o descrizioni acustiche della traccia visiva) con la presentazione (P1).
   * 6.2 Assicurati che gli equivalenti per il contenuto dinamico vengano aggiornati quando il contenuto dinamico cambia.
   * 6.3 Assicurarsi che le pagine siano utilizzabili quando script, applet o altri oggetti programmatici sono disattivati o non supportati. Se ciò non fosse possibile, fornisci informazioni equivalenti su una pagina alternativa accessibile.
   * 6.5 Assicurarsi che il contenuto dinamico sia accessibile o fornire una presentazione o una pagina alternativa (P2).
   * 8.1 Rendere gli elementi programmatici come script e applet direttamente accessibili o compatibili con le tecnologie per l&#39;accessibilità [Priorità 1 se la funzionalità è importante e non viene presentata altrove], altrimenti (P2).
   * 9.3 Per gli script, specificare gestori di eventi logici anziché gestori di eventi dipendenti dal dispositivo (P2).
   * 10.1 Fino a quando gli agenti utente non consentono agli utenti di disattivare le finestre generate, non far apparire finestre pop-up o altre finestre e non modificare la finestra corrente senza informare l&#39;utente.
* WCAG 2.0
   * 3.2.1 Al focus: quando un componente diventa attivo, non inizia un cambiamento del contesto. (Livello A)
   * 3.2.2 All’input: la modifica dell’impostazione di un componente nell’interfaccia non provoca automaticamente un cambiamento di contesto, a meno che l’utente non sia stato informato del comportamento prima di utilizzare il componente. (Livello A)
   * 3.2.5 Modifica su richiesta: i cambiamenti di contesto vengono avviati solo su richiesta dell&#39;utente oppure è disponibile un meccanismo per disattivare tali cambiamenti. (livello AAA)

## Assicurati che tutti i contenuti audio e video siano accessibili{#ensure-audio-video-accessible}

Se i moduli includono contenuto audio o video, inclusi clip audio e video, è necessario assicurarsi che tale contenuto sia accessibile. In particolare, assicurarsi che i video clip incorporati nei moduli contengano didascalie (a volte denominate sottotitoli) per utenti non udenti e ipoudenti e descrizioni video per utenti non vedenti. Per i file audio non sincronizzati con il contenuto video, è sufficiente una trascrizione semplice.
Per i file multimediali basati su Flash, consultare [link](/help/forms/using/best-practices-for-creating-forms-in-designer.md) per informazioni su come specificare i sottotitoli.

**Punti di controllo correlati**:
* Sezione 508 §1194.22
   * (b) Le alternative equivalenti per qualsiasi presentazione multimediale sono sincronizzate con la presentazione.
* WCAG 1.0
   * 1.1 Fornisci un equivalente testuale per ogni elemento non testuale (ad esempio, tramite &quot;alt&quot;, &quot;longdesc&quot; o nel contenuto dell’elemento). Ciò include: immagini, rappresentazioni grafiche di testo (compresi i simboli), aree delle mappe immagine, animazioni (ad esempio, GIF animati), applet e oggetti programmatici, arte ascii, fotogrammi, script, immagini utilizzate come punti elenco, distanziatori, pulsanti grafici, suoni (riprodotti con o senza interazione dell’utente), file audio autonomi, tracce audio di video e video (P1).
   * 1.3 Fino a quando gli agenti utente non possono leggere automaticamente ad alta voce l&#39;equivalente testuale di una traccia visiva, fornire una descrizione uditiva delle informazioni importanti della traccia visiva di una presentazione multimediale (P1).
   * 1.4 Per qualsiasi presentazione multimediale basata sul tempo (ad esempio, un filmato o un&#39;animazione), sincronizzare alternative equivalenti (ad esempio, didascalie o descrizioni acustiche della traccia visiva) con la presentazione (P1).
* WCAG 2.0
   * 1.2.1 Solo audio e solo video (preregistrati): per gli elementi solo video e solo audio preregistrati vale quanto segue, tranne quando l’audio o il video sia un elemento alternativo per il testo, chiaramente indicato come tale: (Livello A)
   * 1.2.2 Sottotitoli (preregistrati): i sottotitoli vengono forniti per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati, tranne quando l’elemento multimediale è alternativo al testo ed è chiaramente indicato come tale. (Livello A)
   * 1.2.3 Audiodescrizione o tipo di media alternativo (preregistrato): viene fornita un’alternativa per gli elementi multimediali temporizzati o una descrizione audio dei contenuti video preregistrati per gli elementi multimediali sincronizzati, tranne quando l’elemento multimediale è alternativo al testo ed è chiaramente indicato come tale. (Livello A)
   * 1.2.4 Sottotitoli (dal vivo): i sottotitoli vengono forniti per tutti i contenuti audio dal vivo negli elementi multimediali sincronizzati. (livello AA)
   * 1.2.5 Audiodescrizione (preregistrata): per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati viene fornita una descrizione audio. (livello AA)
   * 1.2.6 Lingua dei segni (preregistrata): l’interpretazione della lingua dei segni è fornita per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati. (livello AAA)
   * 1.2.7 Descrizione audio estesa (preregistrata): se le pause nell’audio in primo piano non sono sufficienti per consentire alle descrizioni audio di trasmettere il senso del video, viene fornita una descrizione audio estesa per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati. (livello AAA)
   * 1.2.8 Media Alternative (preregistrate): viene fornita un’alternativa per gli elementi multimediali temporizzati per tutti gli elementi multimediali sincronizzati preregistrati e per tutti gli elementi multimediali solo video preregistrati. (livello AAA)
   * 1.2.9 Solo audio (dal vivo): viene fornita un’alternativa per gli elementi multimediali temporizzati che presentano informazioni equivalenti per i contenuti solo audio dal vivo. (livello AAA)

## Identificare il linguaggio naturale ed eventuali modifiche nel linguaggio{#identify-natural-language}

Il contenuto del modulo verrà letto da tecnologie per l’accessibilità che utilizzano sintetizzatori vocali specifici per il linguaggio, pertanto è importante identificare correttamente la lingua principale del modulo per garantire che i moduli vengano letti nella lingua desiderata.

Se il testo (o testo alternativo) nei moduli viene presentato in più lingue, è necessario identificare le aree del modulo in cui viene effettuato un passaggio da una lingua all&#39;altra.

In Designer di LiveCycle, l&#39;impostazione della lingua primaria viene eseguita impostando la proprietà Locale della maschera e la proprietà Locale della sottomaschera di livello superiore. Per identificare le modifiche apportate alla lingua principale, modificare la proprietà Locale per qualsiasi oggetto che utilizza una lingua diversa dalla lingua del modulo.

Per impostare la proprietà Locale di una maschera:
1. Scegliete File > Proprietà modulo e selezionate la scheda Default
2. Selezionare la lingua appropriata per le impostazioni internazionali del modulo (vedere Figura 17)
3. Fare clic su OK

![Modifica delle impostazioni internazionali del modulo nella finestra di dialogo Proprietà modulo](/help/forms/using/assets/image-17.png)

Figura 17: **Modifica delle impostazioni internazionali del modulo nella finestra di dialogo Proprietà modulo**

Per impostare la proprietà Local della sottomaschera di primo livello o di un oggetto che richiede una lingua diversa:
1. Selezionare la sottomaschera o l&#39;oggetto di primo livello nella visualizzazione Struttura
1. Visualizzare la tavolozza Oggetto scegliendo Finestra > Oggetto
1. Nella tavolozza Oggetto selezionare la scheda Campo e nell&#39;elenco Impostazioni internazionali selezionare la lingua da utilizzare per l&#39;oggetto (vedere Figura 18). Quando si applicano opzioni di impostazioni internazionali diverse a singoli oggetti, tenere presente che gli oggetti inclusi nelle tabelle e nelle sottomaschere ricevono automaticamente la stessa impostazione di impostazioni internazionali dell&#39;oggetto tabella e sottomaschera.

![Modifica delle impostazioni locali di un oggetto](/help/forms/using/assets/image-18.png)

Figura 18: **Modifica delle impostazioni locali di un oggetto**

**Punti di controllo correlati**:
* WCAG 1.0
   * 4.1 Identificare chiaramente le modifiche nel linguaggio naturale del testo di un documento e qualsiasi equivalente testuale (ad esempio, didascalie).
* WCAG 2.0
   * 3.1.1 Language of Page (Lingua della pagina): la lingua umana predefinita di ogni pagina web può essere determinata programmaticamente. (Livello A)
   * 3.1.2 Parti in lingua: il linguaggio umano di ogni passaggio o frase del contenuto può essere determinato a livello di programmazione, ad eccezione dei nomi propri, dei termini tecnici, delle parole in lingua indeterminata e delle parole o frasi che sono diventate parte del gergo del testo immediatamente circostante. (livello AA)
