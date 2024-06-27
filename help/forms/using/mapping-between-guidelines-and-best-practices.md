---
title: Linee guida e best practice per l’accessibilità per la creazione di moduli in Forms Designer
description: Best practice e linee guida per l’accessibilità durante lo sviluppo di moduli in Forms Designer.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 082a705e25c8c9f17428daadb017d5ab55784994
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 1%

---

# Mappatura tra linee guida e best practice

Nelle sezioni seguenti vengono associate le linee guida della sezione 508 e delle linee guida WCAG alle best practice descritte in questa guida.

## § 1194.21 Linee guida Descrizione e best practice

### Sezione 508 §1194.21: Applicazioni software e sistemi operativi

| § 1194.21 Linee guida | Descrizione linea guida | Best practice LiveCycle Designer per la conformità | Note |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| a) IT | Se il software è progettato per essere eseguito su un sistema dotato di tastiera, le funzioni del prodotto devono poter essere eseguite da una tastiera in cui la funzione stessa o il risultato dell’esecuzione di una funzione possono essere individuati testualmente. | <li> 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera </li><li> 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto</li> | |
| b) IT | Le applicazioni non interrompono né disattivano le funzioni attivate di altri prodotti identificati come funzioni di accessibilità, se tali funzioni sono sviluppate e documentate conformemente agli standard del settore. Le applicazioni non devono inoltre interrompere o disattivare le funzioni attivate di sistemi operativi identificate come funzioni di accessibilità, se l’interfaccia di programmazione dell’applicazione per tali funzioni di accessibilità è stata documentata dal fabbricante del sistema operativo ed è disponibile per lo sviluppatore del prodotto. | Nessuna tecnica specifica di LiveCycle per Designer: questa linea guida è gestita da Adobe Reader per i PDF forms. | |
| c) IT | Deve essere fornita sullo schermo un’indicazione precisa della messa a fuoco in corso, che si sposta tra gli elementi dell’interfaccia interattivi quando cambia la messa a fuoco dell’input. La messa a fuoco deve essere esposta a livello di programmazione in modo che la tecnologia assistiva possa tenere traccia dei cambiamenti di messa a fuoco e messa a fuoco. | 2.3 Scegliere i controlli giusti Per garantire che lo stato attivo sia esposto a livello di programmazione e di visualizzazione, utilizzare sempre i controlli standard. | |
| d) | La tecnologia assistiva deve disporre di informazioni sufficienti su un elemento dell’interfaccia utente, tra cui l’identità, il funzionamento e lo stato dell’elemento. Quando un’immagine rappresenta un elemento del programma, anche le informazioni trasmesse dall’immagine devono essere disponibili nel testo. | <ul><li>2.1 Moduli semplici e facili da usare</li> <li>2.1.1 Evitare di spostare, lampeggiare o lampeggiare i contenuti</li> <li>2.2 Configurare le proprietà del modulo per generare le informazioni di accessibilità</li> <li>2.5 Fornire etichette appropriate per i controlli dei moduli</li></ul> | |
| e) | Quando si utilizzano immagini bitmap per identificare controlli, indicatori di stato o altri elementi programmatici, il significato assegnato a tali immagini deve essere coerente per l&#39;intera durata delle prestazioni di un&#39;applicazione. | <ul><li>2.4 Fornire equivalenti testuali per le immagini</li><li> 2.5 Fornire etichette appropriate per i controlli modulo Questo standard si applica solo se si utilizza la stessa immagine in più punti di un modulo. Non è consigliabile utilizzare controlli personalizzati basati su immagini. In alternativa, utilizzare solo i controlli standard forniti da LiveCycle Designer. Se si utilizzano immagini nei controlli, assicurarsi sempre che vengano utilizzate in modo coerente.</li> | |
| f) | Le informazioni testuali devono essere fornite attraverso le funzioni del sistema operativo per la visualizzazione del testo. Le informazioni minime da rendere disponibili sono il contenuto del testo, la posizione del punto di inserimento del testo e gli attributi del testo. | 2.3 Scegliere i controlli appropriati Evitare di utilizzare immagini per trasmettere informazioni testuali. Anziché utilizzare componenti di input personalizzati che potrebbero non esporre correttamente le proprietà del testo al sistema operativo, utilizzare sempre i controlli standard. | |
| g) | Le applicazioni non devono sostituire le selezioni del contrasto e del colore e altri attributi di visualizzazione selezionati dall’utente. | Nessun LiveCycle di tecniche specifiche per Designer | Se possibile, utilizzate i colori di sistema predefiniti di base. |
| h) | Quando è visualizzata un&#39;animazione, le informazioni devono poter essere visualizzate in almeno una modalità di presentazione non animata a scelta dell&#39;utente. | 2.1 Mantenere i moduli semplici e facili da usare Evitare di utilizzare animazioni nei moduli o fornire versioni separate in cui le animazioni vengono sostituite da immagini statiche. | |
| i) IT | La codifica a colori non deve essere utilizzata come unico mezzo per trasmettere informazioni, indicare un’azione, sollecitare una risposta o distinguere un elemento visivo. | 2.8 Usare il colore in modo responsabile | |
| j) | Quando un prodotto consente all&#39;utente di regolare le impostazioni di colore e contrasto, è disponibile una varietà di selezioni di colore in grado di produrre una gamma di livelli di contrasto. | Non applicabile | Questa funzionalità è generalmente fornita da Adobe Reader, non dallo sviluppatore del modulo. |
| k) | Il software non deve utilizzare testo lampeggiante o lampeggiante, oggetti o altri elementi con una frequenza di lampeggiamento o lampeggiamento superiore a 2 Hz e inferiore a 55 Hz. | 2.1.1 Evitare di spostare, lampeggiare o lampeggiare i contenuti | |
| l) | Quando si utilizzano moduli elettronici, il modulo consente alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità necessarie per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti. | 2.5 Fornire etichette appropriate per i controlli dei moduli | |

### Sezione 508 §11942: Intranet basata sul web e informazioni e applicazioni Internet

| §11942 linea guida | Descrizione linea guida | Best practice LiveCycle Designer per la conformità | Note |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| a) IT | Deve essere fornito un equivalente testuale per ogni elemento non testuale (ad esempio tramite &quot;alt&quot;, &quot;longdesc&quot; o nel contenuto dell’elemento). | 2.4 Fornire equivalenti testuali per le immagini | |
| b) IT | Le alternative equivalenti per qualsiasi presentazione multimediale devono essere sincronizzate con la presentazione. | 2.12 Garantire l&#39;accessibilità di tutti i contenuti multimediali | |
| c) IT | Le pagine web sono concepite in modo che tutte le informazioni trasmesse a colori siano disponibili anche senza colore, ad esempio dal contesto o dal markup. | 2.8 Usare il colore in modo responsabile | |
| d) | I documenti sono organizzati in modo da essere leggibili senza richiedere un foglio di stile associato. | Non applicabile | |
| e) | Per ogni area attiva di una mappa immagine lato server sono forniti collegamenti di testo ridondanti. | Non applicabile | |
| f) | Al posto delle mappe immagine sul lato server, devono essere fornite mappe immagine sul lato client, salvo nei casi in cui non sia possibile definire le regioni con una forma geometrica disponibile. | Non applicabile | |
| g) | Le intestazioni di riga e di colonna sono identificate per le tabelle di dati. | 2.9 Fornire celle di intestazione per le tabelle | |
| h) | Il markup è utilizzato per associare le celle di dati e le celle di intestazione delle tabelle di dati che presentano due o più livelli logici di intestazioni di riga o di colonna. | 2.9 Fornire celle di intestazione per le tabelle | |
| i) IT | Le cornici sono denominate con un testo che facilita l&#39;identificazione e la navigazione delle cornici. | Non applicabile | |
| j) | Le pagine devono essere progettate in modo da evitare che lo schermo sfarfallii con una frequenza superiore a 2 Hz e inferiore a 55 Hz. | 2.1 Moduli semplici e facili da usare | |
| k) | Qualora non sia possibile ottenere la conformità in altro modo, è necessario fornire una pagina di solo testo con informazioni o funzionalità equivalenti per rendere un sito web conforme alle disposizioni della presente parte. Il contenuto della pagina di solo testo viene aggiornato ogni volta che cambia la pagina principale. | Non applicabile | |
| l) | Quando le pagine utilizzano linguaggi di scripting per visualizzare il contenuto o per creare elementi dell’interfaccia, le informazioni fornite dallo script devono essere identificate con testo funzionale leggibile con la tecnologia per l’accessibilità. | 2.11 Evitare l’interruzione degli script | |
| m) | Quando una pagina web richiede che un’applet, un plug-in o un’altra applicazione sia presente sul sistema client per interpretare il contenuto della pagina, la pagina deve fornire un collegamento a un plug-in o a un’applet conforme alla norma §1194.21, lettere da a) a l). | Non applicabile | Le pagine web che si collegano ai PDF forms devono fornire un collegamento ad Adobe Reader. |
| n) | Quando i moduli elettronici sono progettati per essere compilati on line, il modulo deve consentire alle persone che utilizzano tecnologie per l’accessibilità di accedere alle informazioni, agli elementi del campo e alle funzionalità necessarie per la compilazione e la presentazione del modulo, compresi tutti gli orientamenti e i suggerimenti. | 2.5 Fornire etichette appropriate per i controlli dei moduli | |
| o) | Deve essere fornito un metodo che consenta agli utenti di saltare i collegamenti di navigazione ripetitivi. | 2.10 Fornire una struttura di modulo navigabile | |
| (e) | Quando è richiesta una risposta a tempo, l’utente è avvisato e dispone di tempo sufficiente per indicare che è necessario più tempo. | 2.11 Evitare l’interruzione degli script | |

### Punti di controllo WCAG 1.0 con priorità 1

| Checkpoint | Descrizione checkpoint | Best practice LiveCycle Designer per la conformità | Note |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | Fornisci un equivalente testuale per ogni elemento non testuale (ad esempio, tramite &quot;alt&quot;, &quot;longdesc&quot; o nel contenuto dell’elemento). Ciò include: immagini, rappresentazioni grafiche di testo (compresi i simboli), aree delle mappe immagine, animazioni (ad esempio, GIF animati), applet e oggetti programmatici, ASCII art, fotogrammi, script, immagini utilizzate come punti elenco, distanziatori, pulsanti grafici, suoni (riprodotti con o senza l’interazione dell’utente), file audio autonomi, tracce audio di video e video. | <ul><li>2.4 Fornire equivalenti testuali per le immagini</li> <li>2.12 Garantire l&#39;accessibilità di tutti i contenuti multimediali</li> | |
| [1,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | Fornisci collegamenti di testo ridondanti per ogni area attiva di una mappa immagine lato server. | Non applicabile | |
| [1,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | Fino a quando gli agenti utente non sono in grado di leggere automaticamente ad alta voce l&#39;equivalente testuale di una traccia visiva, fornire una descrizione uditiva delle informazioni importanti della traccia visiva di una presentazione multimediale. | 2.12 Garantire l&#39;accessibilità di tutti i contenuti multimediali | |
| [1,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | Per qualsiasi presentazione multimediale basata sul tempo (ad esempio, un filmato o un&#39;animazione), sincronizzare alternative equivalenti (ad esempio, didascalie o descrizioni acustiche della traccia visiva) con la presentazione. | 2.12 Garantire l&#39;accessibilità di tutti i contenuti multimediali | |
| [2,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | Assicurati che tutte le informazioni trasmesse con il colore siano disponibili anche senza colore, ad esempio dal contesto o dal markup. | 2.8 Usare il colore in modo responsabile | |
| [4,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | Identificare chiaramente le modifiche nel linguaggio naturale del testo di un documento ed eventuali equivalenti testuali (ad esempio, didascalie). | 2.13 Identificare i cambiamenti linguistici | |
| [5,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | Per le tabelle di dati, identifica le intestazioni di riga e di colonna. | 2.9 Fornire celle di intestazione per le tabelle | |
| [5,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | Per le tabelle di dati con due o più livelli logici di intestazioni di riga o di colonna, utilizzare il markup per associare celle di dati e celle di intestazione. | 2.9 Fornire celle di intestazione per le tabelle | |
| [6,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | Organizzare i documenti in modo che possano essere letti senza fogli di stile. Quando, ad esempio, viene eseguito il rendering di un documento HTML senza i fogli di stile associati, deve essere comunque possibile leggere il documento. | Non applicabile | |
| [6,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | Assicurati che gli equivalenti per il contenuto dinamico vengano aggiornati quando il contenuto dinamico cambia. | 2.11 Evitare l’interruzione degli script | |
| [6.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | Assicurati che le pagine siano utilizzabili quando gli script, le applet o altri oggetti programmatici sono disattivati o non supportati. Se ciò non fosse possibile, fornisci informazioni equivalenti su una pagina alternativa accessibile. | 2.11 Evitare l’interruzione degli script | |
| [7,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | Fino a quando gli agenti utente non consentono agli utenti di controllare lo sfarfallio, evita di causare lo sfarfallio dello schermo. | 2.1 Moduli semplici e facili da usare | |
| [9,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | Fornisci mappe immagine lato client invece di mappe immagine lato server, a meno che non sia possibile definire le aree con una forma geometrica disponibile. | Non applicabile | |
| [11,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | Se, dopo ogni tentativo, non è possibile creare una pagina accessibile, fornire un collegamento a una pagina alternativa che utilizza tecnologie W3C, è accessibile, dispone di informazioni (o funzionalità) equivalenti e viene aggiornata con la stessa frequenza della pagina inaccessibile (originale). | Non applicabile | |
| [12,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | Assegnate un titolo a ciascun frame per facilitarne l&#39;identificazione e la navigazione. | Non applicabile | |
| [14,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | Utilizza il linguaggio più chiaro e semplice appropriato per il contenuto di un sito. | 2.1 Moduli semplici e facili da usare | |

### Punti di controllo WCAG 1.0 Priority 2

| Checkpoint priorità 2 | Descrizione checkpoint | Best practice di LiveCycle richieste per la conformità | Note |
|------------|------------------------|-------------------------------------------------|-------|
| [2,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | Assicurati che le combinazioni di colori di primo piano e di sfondo forniscano un contrasto sufficiente quando vengono visualizzate da persone con deficit di colore o su uno schermo in bianco e nero. [Priorità 2 per le immagini, priorità 3 per il testo]. | 2.8 Usare il colore in modo responsabile | |
| [3,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | Se esiste un linguaggio di markup appropriato, utilizzare il markup anziché le immagini per trasmettere le informazioni. | <ul><li>2.1 Moduli semplici e facili da usare</li><li> 2.1.1 Evitare di spostare, lampeggiare o lampeggiare i contenuti</li> <li>2.2 Configurare le proprietà del modulo per generare informazioni di accessibilità Utilizzare sempre testo effettivo anziché immagini di testo.</li> | |
| [3,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | Creare documenti convalidati in grammatiche formali pubblicate. | | Per eseguire il rendering in Adobe Reader, i PDF forms devono corrispondere alla specifica dei PDF pubblicata. |
| [3,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | Utilizzare i fogli di stile per controllare layout e presentazione. | Non applicabile | |
| [3,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | Utilizzare unità relative anziché assolute nei valori degli attributi del linguaggio di markup e delle proprietà del foglio di stile. | Non applicabile | |
| [3,5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | Utilizza gli elementi intestazione per trasmettere la struttura del documento e utilizzarli in base alle specifiche. | 2.10 Fornire una struttura di modulo navigabile | |
| [3,6](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | Contrassegnare gli elenchi e le voci di elenco in modo corretto. | 2.10.3 Contrassegni elenchi Contrassegna il contenuto basato su elenco come elenchi utilizzando i ruoli Elenco ed Elemento elenco. | |
| [3,7](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | Contrassegna le offerte. Non utilizzare le virgolette per formattare effetti quali i rientri. | Non applicabile | |
| [5,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | Non utilizzare le tabelle per il layout a meno che la tabella non abbia senso quando viene linearizzata. In caso contrario, se la tabella non ha senso, fornisci un equivalente alternativo (che può essere una versione linearizzata). | Nessuna tecnica di LiveCycle specifica | Non è necessario utilizzare tabelle per il layout nei moduli di LiveCycle. Utilizzare invece la tavolozza Layout per posizionare i campi modulo in un motivo a griglia. Utilizza una tabella solo quando utilizzi funzioni specifiche della tabella, come le intestazioni della tabella. |
| [5,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | Se per il layout viene utilizzata una tabella, non utilizzare markup strutturali ai fini della formattazione visiva. | Nessuna tecnica di LiveCycle specifica | |
| [6.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | Per gli script e le applet, verificare che i gestori eventi siano indipendenti dal dispositivo di input. | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| [6.5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | Assicurati che il contenuto dinamico sia accessibile o fornisci una presentazione o una pagina alternativa. | 2.11 Evitare l’interruzione degli script | |
| [7,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | Fino a quando gli agenti utente non consentono agli utenti di controllare la visualizzazione lampeggiante, evita che il contenuto lampeggi (ad esempio, modifica la presentazione a una velocità regolare, come l’attivazione e lo spegnimento). | 2.1 Moduli semplici e facili da usare | |
| [7,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | Fino a quando gli agenti utente non consentono agli utenti di bloccare i contenuti in movimento, evita lo spostamento nelle pagine. | 2.1 Moduli semplici e facili da usare | |
| [7,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | Fino a quando gli agenti utente non forniscono la possibilità di interrompere l’aggiornamento, non creare pagine con aggiornamento automatico periodico. | Non applicabile | |
| [7,5](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | Fino a quando gli agenti utente non forniscono la possibilità di interrompere il reindirizzamento automatico, non utilizzare il markup per reindirizzare le pagine automaticamente. Al contrario, configura il server per eseguire i reindirizzamenti. | Non applicabile | |
| [8,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | Rendere gli elementi programmatici come script e applet direttamente accessibili o compatibili con le tecnologie per l’accessibilità [Priorità 1 se la funzionalità è importante e non viene presentata altrove, altrimenti Priorità 2.] | 2.11 Evitare l’interruzione degli script | |
| [9,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | Assicurati che qualsiasi elemento con una propria interfaccia possa essere utilizzato in modo indipendente dal dispositivo. | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| [9,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | Per gli script, specificare gestori di eventi logici anziché gestori di eventi dipendenti dal dispositivo. | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| [10,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | Fino a quando gli agenti utente non consentono agli utenti di disattivare le finestre generate, non far apparire finestre pop-up o di altro tipo e non modificare la finestra corrente senza informare l&#39;utente. | 2.11 Evitare l’interruzione degli script | |
| [10,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | Fino a quando gli agenti utente non supportano associazioni esplicite tra etichette e controlli modulo, per tutti i controlli modulo con etichette associate in modo implicito, verificare che l&#39;etichetta sia posizionata correttamente. | 2.5 Fornire etichette appropriate per i controlli dei moduli | |
| [11,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | Utilizza le tecnologie W3C quando sono disponibili e appropriate per un’attività e, se supportate, utilizza le versioni più recenti. | Non applicabile | |
| [11,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | Evita funzioni obsolete delle tecnologie W3C. | Non applicabile | |
| [12,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | Descrivere lo scopo dei fotogrammi e il modo in cui i fotogrammi si relazionano tra loro se non è evidente dai soli titoli dei fotogrammi. | Non applicabile | |
| [12,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | Dividere grandi blocchi di informazioni in gruppi più gestibili in modo naturale e appropriato. | 2.10 Fornire una struttura di modulo navigabile | |
| [12,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | Associare esplicitamente le etichette ai relativi controlli. | 2.5 Fornire etichette appropriate per i controlli dei moduli | |
| [13,1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | Identifica chiaramente il target di ogni collegamento. | 2.5 Fornire etichette appropriate per i controlli dei moduli 2.5.6 Fornire testo di collegamento | |
| [13,2](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | Fornisci metadati per aggiungere informazioni semantiche a pagine e siti. | Non applicabile | |
| [13,3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | Fornire informazioni sul layout generale di un sito, ad esempio una mappa del sito o un sommario. | 2.10 Fornire una struttura di modulo navigabile | |
| [13,4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | Utilizza i meccanismi di navigazione in modo coerente. | 2.10 Fornire una struttura di modulo navigabile | Utilizza le pagine master per creare contenuti di navigazione coerenti. |

### Criteri di successo WCAG 2.0

| Priorità 1 Punti Di Controllo G 2 | Best practice di LiveCycle richieste per la conformità | Note |
| --- | --- | --- |
| 1,1 [Alternative testuali](http://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1. [Contenuto non testuale](http://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 Fornire equivalenti testuali per le immagini | |
| | 2.5 Fornire etichette appropriate per i controlli dei moduli | |
| 1,2 [Contenuti multimediali temporizzati](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1. [Solo audio e solo video (preregistrati)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.2. [Sottotitoli (preregistrati)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.3. [Audiodescrizione o tipo di media alternativo (preregistrato)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.4. [Sottotitoli (dal vivo)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.5. [Audiodescrizione (preregistrata)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.6. [Lingua del segno (preregistrata)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.7. [Descrizione audio estesa (preregistrata)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.8. [Media Alternative (Preregistrate)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1.2.9. [Solo audio (dal vivo)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 Garantire che tutti i contenuti audio e video siano accessibili | |
| 1,3 [Adattabile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1. [Informazioni e relazioni](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 Fornire celle di intestazione per le tabelle | |
| 1.3.2. [Sequenza significativa](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto | |
| | 2.10 Fornire una struttura di modulo navigabile | |
| 1.3.3. [Caratteristiche sensoriali](http://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 Usare il colore in modo responsabile | |
| 1,4 [Distinguibile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1. [Uso del colore](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 Usare il colore in modo responsabile | |
| 1.4.2. [Controllo audio](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | Nessuna tecnica di LiveCycle specifica | |
| 1.4.3. [Contrasto (minimo)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 Usare il colore in modo responsabile | |
| 1.4.4. [Ridimensiona testo](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | Nessuna tecnica di LiveCycle specifica | |
| 1.4.5. [Immagini di testo](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | Nessuna tecnica di LiveCycle specifica | |
| 1.4.6. [Contrasto (ottimizzato)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 Usare il colore in modo responsabile | |
| 1.4.7. [Audio di sfondo basso o assente](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | Nessuna tecnica di LiveCycle specifica | |
| 1.4.9. [Immagini di testo (nessuna eccezione)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | Nessuna tecnica di LiveCycle specifica | |
| 2,1 [Accessibile da tastiera](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1. [Tastiera](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto | |
| | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| 2.1.2. [Nessun impedimento all’uso della tastiera](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| 2.1.3. [Tastiera (nessuna eccezione)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto | |
| | 2.7 Assicurarsi che i controlli del modulo siano accessibili da tastiera | |
| 2,2 [Tempo sufficiente](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1. [Regolazione tempi di esecuzione](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | Nessuna tecnica di LiveCycle specifica | |
| 2.2.2. [Pausa, stop, nascondi](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 Moduli semplici e facili da usare | |
| 2.2.3. [Nessuna tempistica](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | Nessuna tecnica di LiveCycle specifica | |
| 2.2.4. [Interruzioni](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | Nessuna tecnica di LiveCycle specifica | |
| 2.2.5. [Nuova autenticazione](http://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | Nessuna tecnica di LiveCycle specifica | |
| 2,3 [Convulsioni] | | |
| 2.3.1. [Tre Flash o inferiore alla soglia](http://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 Moduli semplici e facili da usare | |
| 2.3.2. [Tre Flash](http://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 Moduli semplici e facili da usare | |
| 2,4 [Navigabile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1. [Ignora blocchi](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 Fornire una struttura di modulo navigabile | |
| 2.4.2. [Pagina con titolo](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | Nessuna tecnica di LiveCycle specifica | |
| 2.4.3. [Ordine del focus](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 Verificare che l&#39;ordine di lettura e di tabulazione sia corretto | |
| 2.4.4. [Scopo del collegamento (nel contesto)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | Nessuna tecnica di LiveCycle specifica | Lo scopo del collegamento dipende dalla scelta da parte degli autori di testo significativo per gli elementi collegati. |
| 2.4.5. [Differenti modalità](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 Fornire una struttura di modulo navigabile | |
| 2.4.6. [Intestazioni ed etichette](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 Fornire etichette appropriate per i controlli dei moduli</li><li>2.10 Fornire una struttura di modulo navigabile</li> | |
| 2.4.7. [Focus visibile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | Nessuna tecnica di LiveCycle specifica | Lo stato attivo predefinito nei moduli di LiveCycle è visibile. |
| 2.4.8. [Posizione](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | Nessuna tecnica di LiveCycle specifica | Non applicabile: i moduli di LiveCycle non richiedono sistemi di navigazione. |
| 2.4.9. [Scopo collegamento (solo collegamento)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | Nessuna tecnica di LiveCycle specifica | Lo scopo del collegamento dipende dalla scelta da parte degli autori di testo significativo per gli elementi collegati. |
| 2.4.10 [Intestazioni di sezione](http://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 Fornire una struttura di modulo navigabile | |
| 3,1 [Leggibile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1. [Lingua della pagina](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 Identificare il linguaggio naturale ed eventuali modifiche del linguaggio | |
| 3.1.2. [Lingua delle parti](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 Identificare il linguaggio naturale ed eventuali modifiche del linguaggio | |
| 3.1.3. [Parole insolite](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | Nessuna tecnica di LiveCycle specifica | |
| 3.1.4. [Abbreviazioni](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | Nessuna tecnica di LiveCycle specifica | |
| 3.1.5. [Livello di lettura](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | Nessuna tecnica di LiveCycle specifica | |
| 3.1.6. [Pronuncia](http://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | Nessuna tecnica di LiveCycle specifica | |
| 3,2 [Prevedibile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1. [Al focus](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 Evitare l’interruzione degli script | |
| 3.2.2. [All’input](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 Evitare l’interruzione degli script | |
| 3.2.3. [Navigazione coerente](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 Fornire una struttura di modulo navigabile | |
| 3.2.4. [Identificazione coerente](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 Scegliere i controlli giusti</li><li>2.5 Fornire etichette appropriate per i controlli dei moduli</li> | |
| 3.2.5. [Modifica su richiesta](http://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 Evitare l’interruzione degli script | |
| 3,3 [Assistenza nell’inserimento](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1. [Identificazione di errori](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycle Designer fornisce gli strumenti necessari per contrassegnare i campi modulo e per eseguire la convalida dell&#39;input del modulo. |
| 3.3.2. [Etichette o istruzioni](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 Fornire etichette appropriate per i controlli dei moduli | |
| 3.3.3. [Suggerimenti per gli errori](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycle Designer fornisce gli strumenti necessari per contrassegnare i campi modulo e per eseguire la convalida dell&#39;input del modulo. |
| 3.3.4. [Prevenzione degli errori (legali, finanziari, dati)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | Nessuna tecnica di LiveCycle specifica | |
| 3.3.5. [Aiuto](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | Nessuna tecnica di LiveCycle specifica | |
| 3.3.6. [Prevenzione degli errori (tutti)](http://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | Nessuna tecnica di LiveCycle specifica | |
| 4,1 [Compatibile](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1. [Analisi](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | Nessuna tecnica di LiveCycle specifica | |
| 4.1.2. [Nome, ruolo, valore](http://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 Scegliere i controlli giusti</li> <li>2.5 Fornire etichette appropriate per i controlli dei moduli</li> | |



