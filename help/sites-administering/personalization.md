---
title: Personalizzazione
seo-title: Personalization
description: Scopri la personalizzazione in AEM.
seo-description: Learn about personalization in AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
source-git-commit: d6b595b6b5477b5cad662e219f1abd483491897f
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 16%

---

# Personalizzazione {#personalization}

## Cos’è la personalizzazione? {#what-is-personalization}

Il volume di contenuti disponibili è in continuo aumento, sia su siti web Internet, extranet o intranet.

La personalizzazione si concentra sulla fornitura all&#39;utente di un ambiente su misura che mostri contenuti dinamici selezionati in base alle sue esigenze specifiche; in base a profili predefiniti, selezione degli utenti o comportamento interattivo degli utenti.

La personalizzazione è caratterizzata da tre elementi principali:

### Utenti {#users}

* Avere profili, sia individuali che di gruppo. Questi profili contengono caratteristiche (come descrizione del lavoro, posizione, interessi) che possono essere utilizzate per personalizzare il contenuto visibile.
* Prendete delle azioni. Questi possono quindi essere analizzati e confrontati con regole di comportamento per adattare il contenuto visualizzato.

### Contenuto {#content}

* È ciò che l&#39;utente vuole vedere. Preferibilmente contenuto di interesse e utilizzo per l&#39;esecuzione dei propri compiti.
* Può essere suddiviso in categorie e quindi reso disponibile agli utenti in base a regole predefinite.
* Deve essere dinamico.

In altre parole, il contenuto deve in qualche modo dipendere dall’utente. Se ogni utente visualizza lo stesso contenuto, la personalizzazione è ridondante.

### Regole {#rules}

* Definisci come avviene effettivamente la personalizzazione, quali contenuti l’utente può visualizzare e quando.

La personalizzazione può essere:

#### Explicit {#explicit}

* Personalizzazione: in cui l&#39;utente effettua le selezioni da una scelta di origini di contenuto.

#### Implicato {#implicit}

* Regole basate su: i manager aziendali definiscono regole specifiche per le azioni basate su profili e/o comportamenti specifici.
* Filtro semplice: le selezioni vengono effettuate sulla base di profili predefiniti a livello di utente e/o gruppo.
* Filtro collaborativo/consigliato: il comportamento dell’utente viene registrato in base a regole predefinite. Queste regole si basano sul comportamento osservato con persone dalla stessa mentalità. Le informazioni raccolte vengono utilizzate per adattare le informazioni visualizzate all’utente, in particolare sotto forma di raccomandazioni.

## Come e quando è possibile utilizzare la personalizzazione? {#how-and-when-can-personalization-be-used}

La personalizzazione può essere utilizzata in molti casi, ad esempio:

### Pagine Intranet {#intranet-pages}

* Il contenuto può essere archiviato in base alla posizione, al reparto e/o al ruolo di un utente, già definito all&#39;interno di una rete interna.
* A seconda della scelta disponibile, l&#39;utente può effettuare ulteriori selezioni.

### Gruppi di utenti specifici, limitati e di destinazione - Extranets {#extranets}

* Gli utenti richiedono un accesso per l&#39;autorizzazione; questo sarà collegato a un profilo che fornisce le informazioni necessarie per la personalizzazione; eventuali dettagli quali la loro posizione, la relazione con il prodotto, la cronologia di utilizzo, le responsabilità di budget, ecc.
* Tali istanze possono variare tra siti come:
* Aziende che forniscono siti web a una sezione altamente specializzata del loro mercato, ad esempio una società farmaceutica che fornisce un sito web specializzato per i medici.
* Aziende che forniscono siti web che consentono ai loro clienti di visualizzare le informazioni relative al conto corrente e alla fatturazione; ad esempio i fornitori telefonici.

### Sito web vendite e distribuzione {#sales-site}

* I siti web di vendita e distribuzione, come Amazon, possono combinare un profilo utente, la cronologia delle vendite dell&#39;utente e la cronologia delle loro ricerche per fornire suggerimenti su cosa potrebbe interessare all&#39;utente successivo.

### Cerca siti Web {#search-site}

* Molti dei principali siti web dei motori di ricerca hanno strumenti analitici molto potenti che registrano il comportamento degli utenti, i termini di ricerca che utilizzano e i siti web che effettivamente visitano. Viene quindi utilizzato per personalizzare il contenuto fornito, in particolare per quanto riguarda la visualizzazione di annunci pubblicitari.

### Punti di forza della personalizzazione e punti da considerare {#strengths-of-personalization-and-points-to-consider}

Di seguito sono riportati i motivi per cui la personalizzazione deve essere utilizzata:

* Un utente può sperimentare un sito web confortevole e mirato.
* La personalizzazione può essere utilizzata per propagare automaticamente l’accesso alla versione più recente del contenuto.
* Le funzioni di collaborazione social network sono disponibili per consentire agli utenti di comunicare tra loro, in quanto possono essere identificate dai loro profili.
* A un utente può essere fornito il contenuto necessario per eseguire una particolare attività. All&#39;interno dell&#39;intranet di un&#39;azienda questo può fornire uno strumento prezioso per la diffusione delle informazioni.
* È possibile fornire a un utente il contenuto di cui ha bisogno o desidera, riducendo così il tempo necessario per eseguire le operazioni di ricerca.
* Il provider di contenuti può gestire il contenuto che deve essere visualizzato da specifiche categorie di utenti.
* È possibile definire regole per fornire contenuti in base a combinazioni sia di caratteristiche che di comportamenti dell’utente. Questo fornisce un meccanismo sofisticato per personalizzare la loro esperienza web.

Quando utilizzi la personalizzazione, considera quanto segue:

#### Spettacolo {#performance}

* Naturalmente l&#39;analisi e la valutazione supplementari hanno un impatto sui risultati. Tuttavia, i metodi utilizzati sono altamente sofisticati e possono essere ottimizzati per minimizzare l&#39;impatto.

#### Autorizzazione {#authorization}

* La personalizzazione richiede un meccanismo di accesso in quanto il sito web deve essere in grado di identificare l’utente.

#### Memorizzazione in cache {#caching}

* La memorizzazione in cache è un aspetto che l’utente vedrà in termini di prestazioni e precisione: quanto rapidamente il sito web fornisce contenuti personalizzati ed è sempre attuale.
* La memorizzazione in cache è una considerazione chiave per la configurazione della personalizzazione e occorre prendere il tempo necessario per garantire che venga utilizzata l’implementazione corretta.

>[!TIP]
>
>Gli effetti della personalizzazione sulle prestazioni e i relativi argomenti di caching sono ulteriormente discussi nel documento [Ottimizzazione delle prestazioni.](/help/sites-deploying/configuring-performance.md)

#### Precisione delle regole {#accuracy}

* La personalizzazione realizzata mediante il tracciamento del comportamento dell’utente o l’impostazione di regole basate sul profilo dell’utente deve essere accurata e logica.
* Non c&#39;è niente di più frustrante per l&#39;utente che avere contenuti forzati o negati a loro a causa della logica imprecisa di una regola.
* Pertanto, le regole devono essere ben concepite - con i requisiti dell&#39;utente in primo piano. Questo può richiedere molto lavoro e non deve essere sottovalutato; definire le regole di business spesso supera lo sforzo tecnico durante l’implementazione della personalizzazione.

#### Applicazione consigliata {#when-to-use}

* Come molte funzioni sul web, la personalizzazione deve essere utilizzata con attenzione. Il suo utilizzo andrà a vantaggio dell&#39;utente? Dovrebbe sempre essere la prima considerazione - o se l&#39;obiettivo desiderato può essere raggiunto con meno sforzo con un altro metodo. La personalizzazione può correre il rischio di essere una funzione che gli utenti configurano una volta (per vedere come funziona) e una sola volta, in quanto non offre loro vantaggi reali.
* La personalizzazione ha un significato solo quando il contenuto è dinamico, in qualche modo dipende dall’utente. Se tutti gli utenti visualizzano lo stesso contenuto, la personalizzazione è ridondante.

#### Riservatezza {#confidentiality}

* Molti utenti sono preoccupati per la protezione e la sicurezza dei dati. In particolare per quanto riguarda i dati recuperati al momento del tracciamento del loro comportamento durante la navigazione sul web.

## Personalizzazione e accesso {#personalization-and-access}

La personalizzazione deve essere considerata separatamente dal controllo degli accessi, ma si interrelano.

La personalizzazione stessa non crea alcuna forma di controllo degli accessi. Si tratta semplicemente di un metodo per controllare ciò che l&#39;utente vede; non impedisce all’utente di accedere ad altri contenuti e, come per qualsiasi contenuto, deve disporre dei controlli di accesso corretti già assegnati.

Tuttavia, il controllo degli accessi può essere utilizzato per creare una forma di personalizzazione. Se consenti o neghi a un utente l’accesso ai contenuti, questo influisce inevitabilmente sulla scelta dei contenuti disponibili, personalizzando in tal modo la sua esperienza web.

## Componenti disponibili per Personalizzazione {#components-available-for-personalization}

Sono disponibili diversi componenti con AEM per la personalizzazione. Alcuni consentono agli utenti di accedere e modificare i loro profili, altri (come I miei gadget) consentono agli utenti di configurare una pagina specifica:

| Titolo nella barra laterale | Scopo |
|---|---|
| Campo per password verificata | Richiede password e conferma della password. |
| Accesso combinato | Consente all&#39;utente di accedere a un account esistente o di registrarsi per un nuovo account. |
| Campo indirizzo Forms | Campo complesso per l’inserimento di un indirizzo internazionale. |
| Forms Begin | Avvia una definizione del modulo |
| Forms Captcha | Campo che consiste di un termine alfanumerico che viene aggiornato automaticamente. Il componente captcha viene usato per proteggere i siti Web dai bot. |
| Gruppo di caselle di selezione Forms | Più elementi organizzati in un elenco e preceduti da caselle di selezione. Gli utenti possono selezionare più caselle. |
| Elenco a discesa Forms | Più elementi organizzati in un elenco a discesa. Il controllo Per selezione multipla specifica se è possibile selezionare più elementi dell’elenco. |
| Fine Forms | Termina la definizione del modulo. |
| Caricamento di file Forms | Elemento che consente all’utente di caricare un file nel server. |
| Campo nascosto Forms | Campo che non viene presentato all’utente. Può essere usato per trasferire un valore al client e di nuovo al server. Questo campo non deve presentare vincoli. |
| Pulsante immagine Forms | Pulsante di invio aggiuntivo per il modulo, rappresentato da un’immagine. |
| Campo password Forms | Come un campo testo, ma per l’inserimento di una sola riga di testo. Inoltre il testo inserito dall’utente non è visibile nel campo. |
| Gruppo pulsanti di scelta Forms | Più elementi organizzati in un elenco e preceduti da un pulsante di scelta. Gli utenti possono selezionare un solo pulsante di scelta. |
| Pulsante Invia Forms | Pulsante di invio aggiuntivo per il modulo. Il titolo rappresenta il testo visualizzato sul pulsante. |
| Campo di testo Forms | Campo di testo che consente agli utenti di inserire delle informazioni. |
| My Gadgets | Consente di includere una selezione di gadget disponibili. |
| Foto avatar profilo | Consente di inserire una foto avatar. |
| Nome completo profilo | Consente di inserire il nome, compreso eventuali elementi quali qualifica, secondo nome e suffisso. |
| Nome visualizzato profilo | Nome che verrà visualizzato. |
| E-mail profilo | Consente di inserire un indirizzo e-mail. |
| Genere profilo | Consente di specificare il genere. |
| Numero di telefono principale profilo | Consente di inserire un numero telefonico. |
| URL principale profilo | Consente di inserire un URL. |
| Proprietà testo generale profilo | Proprietà del profilo. |
| Accesso | Consente di inviare un nome utente e una password al momento dell&#39;accesso. |
| Esci | Indica l&#39;utente attualmente connesso e fornisce un collegamento per la disconnessione. |
| Tag cloud | Una nuvola di tag per mostrare graficamente una selezione di tag all’interno del sito web |
| Teaser | Contenuto (solitamente un’immagine) visualizzato su una pagina principale per &quot;invitare&quot; gli utenti ad accedere al contenuto sottostante. |

## Personalizzazione e contenuto della community {#personalization-and-community-content}

Le funzioni della community, quali blog, forum e calendari, determinano la creazione di contenuti della community, comunemente definiti contenuti generati dagli utenti (UGC, User-Generated Content, contenuti generati dagli utenti). Quando UGC viene immesso in un ambiente di pubblicazione composto da più istanze AEM (a [pubblica azienda](/help/communities/topologies.md)), un problema principale è stato come sincronizzare UGC tra tutte le istanze.

Con [AEM Communities 6.1](/help/communities/overview.md) estensione, questo problema viene risolto utilizzando un [archivio comune per UGC](/help/communities/working-with-srp.md). Per quanto riguarda la personalizzazione, le Comunità includono: [Accesso social](/help/communities/social-login.md) - la possibilità di fornire ai visitatori del sito l’opzione di accedere con Facebook e Twitter.

Senza l’estensione Communities, vari metodi da esplorare per affrontare il problema della coerenza UGC sono:

* Sincronizza le istanze di pubblicazione multiple quando necessario
* Invia l’UGC dall’istanza di pubblicazione all’ambiente di authoring, da cui può essere pubblicato in modo simile alla pubblicazione del contenuto della pagina

Il metodo utilizzato per ottenere la coerenza UGC in un ambiente di pubblicazione composto da più istanze di pubblicazione deve essere attentamente progettato e testato per le prestazioni e la coerenza.
