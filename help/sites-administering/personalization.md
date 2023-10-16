---
title: Personalizzazione
seo-title: Personalization
description: Scopri la personalizzazione in Adobe Experience Manager per fornire all’utente un ambiente su misura con contenuti dinamici.
seo-description: Learn about personalization in AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 2%

---

# Personalizzazione {#personalization}

## Cos’è la personalizzazione? {#what-is-personalization}

Il volume dei contenuti attualmente disponibili è in continua crescita, sia su Internet che su siti Web di Extranet o Intranet.

La personalizzazione consiste nel fornire all’utente un ambiente personalizzato che mostri contenuti dinamici selezionati in base alle sue esigenze specifiche, sulla base di profili predefiniti, selezione degli utenti o comportamento interattivo degli utenti.

Nella personalizzazione sono coinvolti tre elementi principali:

### Utenti {#users}

* Hanno profili, sia individuali che di gruppo. Questi profili contengono caratteristiche (come la descrizione del lavoro, la posizione, gli interessi) che possono essere utilizzate per personalizzare il contenuto che possono vedere.
* Agisci. Questi possono quindi essere analizzati e confrontati con le regole di comportamento per adattare il contenuto visualizzato.

### Contenuto {#content}

* È ciò che l’utente vuole vedere. Preferibilmente il contenuto di interesse, e l&#39;uso, per loro per lo svolgimento dei loro compiti.
* Possono essere categorizzate e quindi rese disponibili agli utenti in base a regole predefinite.
* Deve essere dinamico.

In altre parole, il contenuto deve, in qualche modo, dipendere dall’utente. Se ogni utente visualizza lo stesso contenuto, la personalizzazione è ridondante.

### Regole {#rules}

* Definisci come avviene effettivamente la personalizzazione, quali contenuti può visualizzare l’utente e quando.

La personalizzazione può essere:

#### Esplicito {#explicit}

* Personalizzazione: in cui l’utente effettua selezioni da una scelta di origini di contenuto.

#### Implicito {#implicit}

* Basato su regole: i responsabili aziendali definiscono regole specifiche per le azioni in base a profili e/o comportamenti specifici.
* Filtro semplice: le selezioni vengono effettuate sulla base di profili predefiniti a livello di utente e/o di gruppo.
* Filtro collaborativo/per consigli: il comportamento dell’utente viene registrato in base a regole predefinite. Queste regole si basano sul comportamento osservato con individui che condividono la stessa opinione. Le informazioni raccolte vengono utilizzate per adattare le informazioni visualizzate all’utente, in particolare sotto forma di raccomandazioni.

## Come e quando può essere utilizzata la personalizzazione? {#how-and-when-can-personalization-be-used}

La personalizzazione può essere utilizzata in molti casi, ad esempio:

### Pagine Intranet {#intranet-pages}

* Il contenuto può essere fornito in base alla posizione, al reparto e/o al ruolo di un utente, già definito all’interno di una rete interna.
* A seconda della scelta disponibile, l’utente può effettuare ulteriori selezioni.

### Gruppi di utenti specifici, limitati e di destinazione - Extranet {#extranets}

* Gli utenti richiedono un accesso per l’autorizzazione; questo verrà collegato a un profilo che fornisce le informazioni necessarie per la personalizzazione; possibili dettagli come la loro posizione, la relazione con il prodotto, la cronologia dell’utilizzo, le responsabilità di budgeting, ecc.
* Tali istanze possono variare tra siti diversi, ad esempio:
* Aziende che forniscono siti web a una parte altamente specializzata del loro mercato, ad esempio, una società farmaceutica che fornisce un sito web specializzato per i medici.
* Aziende che forniscono siti Web che consentono ai clienti di visualizzare le informazioni relative al conto corrente e alla fatturazione, ad esempio i provider telefonici.

### Sito Web vendita e distribuzione {#sales-site}

* I siti web di vendita e distribuzione, come Amazon, possono combinare un profilo utente, la cronologia delle vendite dell’utente e la sua cronologia di navigazione per formulare suggerimenti su cosa potrebbe interessare all’utente successivo.

### Cerca siti Web {#search-site}

* Molti dei principali siti web dei motori di ricerca hanno strumenti analitici molto potenti che registrano il comportamento degli utenti, i termini di ricerca che usano e i siti web che visitano. Questo viene quindi utilizzato per personalizzare il contenuto fornito, in particolare per quanto riguarda la visualizzazione degli annunci pubblicitari.

### Punti di forza della personalizzazione e punti da considerare {#strengths-of-personalization-and-points-to-consider}

Di seguito sono riportati i motivi per cui la personalizzazione dovrebbe essere utilizzata:

* Un utente può sperimentare un sito web comodo e mirato.
* La personalizzazione può essere utilizzata per propagare automaticamente l’accesso all’ultima versione del contenuto.
* Le funzioni di collaborazione social sono disponibili per gli utenti per comunicare tra loro, in quanto possono essere identificati dai loro profili.
* A un utente può essere fornito il contenuto necessario per svolgere un’attività particolare. Nell&#39;intranet di un&#39;azienda, questo può rappresentare uno strumento prezioso per la diffusione delle informazioni.
* Gli utenti possono ricevere i contenuti desiderati o necessari, riducendo in tal modo il tempo necessario per eseguire le operazioni di ricerca.
* Il provider di contenuti può indirizzare il contenuto in modo che venga visualizzato da specifiche categorie di utenti.
* È possibile definire regole per distribuire contenuti in base a combinazioni di caratteristiche e comportamenti degli utenti. Questo fornisce un meccanismo sofisticato per personalizzare la loro esperienza web.

Quando utilizzi la personalizzazione, considera quanto segue:

#### Prestazioni {#performance}

* Naturalmente l&#39;analisi e la valutazione supplementari hanno un impatto sulle prestazioni. Tuttavia, i metodi utilizzati sono altamente sofisticati e possono essere ottimizzati per ridurre al minimo l&#39;impatto.

#### Autorizzazione {#authorization}

* La personalizzazione richiede un meccanismo di accesso in quanto il sito web deve essere in grado di identificare l’utente.

#### Memorizzazione in cache {#caching}

* La memorizzazione in cache è un aspetto che l’utente vedrà in termini di prestazioni e precisione: quanto rapidamente il sito web fornisce contenuti personalizzati e quanto è sempre attuale.
* La memorizzazione in cache è un fattore chiave durante la configurazione della personalizzazione e occorre quindi prendere in considerazione il tempo necessario per assicurarsi che venga utilizzata la corretta implementazione.

>[!TIP]
>
>L’effetto della personalizzazione sulle prestazioni e gli argomenti correlati al caching sono trattati più avanti nel documento [Ottimizzazione delle prestazioni.](/help/sites-deploying/configuring-performance.md)

#### Precisione delle regole {#accuracy}

* La personalizzazione realizzata tenendo traccia del comportamento dell’utente, o impostando regole in base al profilo dell’utente, deve essere precisa e logica.
* Non c’è niente di più frustrante per l’utente di avere contenuti forzati o negati a causa della logica inesatta di una regola.
* Pertanto, le regole devono essere ben ponderate, con i requisiti dell’utente in primo piano. Questo può richiedere molto lavoro, e non deve essere sottostimato; definire le regole di business spesso supera lo sforzo tecnico durante l’implementazione della personalizzazione.

#### Applicazione consigliata {#when-to-use}

* Come molte funzioni sul web, la personalizzazione deve essere utilizzata con cautela. L&#39;utilizzo di questa funzionalità apporterà vantaggi concreti all&#39;utente? dovrebbe sempre essere la prima considerazione - o se l&#39;obiettivo desiderato può essere raggiunto con meno sforzo con un altro metodo. La personalizzazione può correre il rischio di essere una funzione che gli utenti configurano una volta (per vedere come funziona) e una sola volta, in quanto non offre loro vantaggi reali.
* La personalizzazione ha senso solo quando il contenuto è dinamico, in qualche modo dipendente dall’utente. Se tutti gli utenti visualizzano lo stesso contenuto, la personalizzazione è ridondante.

#### Riservatezza {#confidentiality}

* Molti utenti sono preoccupati per la protezione dei dati e la sicurezza. In particolare per quanto riguarda i dati recuperati durante il tracciamento del loro comportamento durante la navigazione sul web.

## Personalizzazione e accesso {#personalization-and-access}

La personalizzazione deve essere considerata separatamente dal controllo degli accessi, ma si relazionano tra loro.

La personalizzazione di per sé non crea alcuna forma di controllo degli accessi. Si tratta semplicemente di un metodo per gestire ciò che l’utente vede; non limita l’accesso ad altri contenuti e come per qualsiasi contenuto, devono avere già assegnati i corretti controlli di accesso.

Tuttavia, il controllo degli accessi può essere utilizzato per creare una forma di personalizzazione. Se consenti o neghi a un utente l’accesso ai contenuti, questo inevitabilmente influisce sulla scelta dei contenuti che ha a disposizione, personalizzando così la sua esperienza web.

## Componenti disponibili per la personalizzazione {#components-available-for-personalization}

Vari componenti sono forniti con AEM per la personalizzazione. Alcuni consentono agli utenti di accedere e modificare i loro profili, altri (come I miei gadget) consentono agli utenti di configurare una pagina specifica:

| Titolo nel Sidekick | Scopo |
|---|---|
| Campo per password verificata | Richiede la password e la conferma della password. |
| Iscrizione all&#39;accesso combinato | Consente all&#39;utente di accedere a un account esistente o a un nuovo account. |
| Campo indirizzo Forms | Campo complesso che consente di inserire un indirizzo internazionale. |
| Inizio Forms | Avvia una definizione di modulo |
| Forms Captcha | Campo costituito da una parola alfanumerica che viene aggiornata automaticamente. Il componente captcha protegge i siti web dai bot. |
| Gruppo di caselle di controllo Forms | Più elementi organizzati in un elenco e preceduti da caselle di controllo. Gli utenti possono selezionare più caselle di controllo. |
| Elenco a discesa Forms | Più elementi organizzati in un elenco a discesa. Lo switch Multi Selectable specifica se è possibile selezionare più elementi dall&#39;elenco. |
| Fine Forms | Termina la definizione del modulo. |
| Caricamento file Forms | Elemento di caricamento che consente all’utente di caricare un file sul server. |
| Campo nascosto Forms | Questo campo non viene visualizzato all’utente. Può essere utilizzato per trasportare un valore al client e riportarlo al server. Questo campo non deve avere vincoli. |
| Pulsante immagine Forms | Pulsante di invio aggiuntivo per il modulo di cui è stato eseguito il rendering come immagine. |
| Campo password Forms | Come campo di testo, è consentita una sola riga e il testo immesso dall’utente non è visibile nel campo. |
| Gruppo pulsanti di scelta Forms | Più elementi organizzati in un elenco preceduto da un pulsante di opzione. Gli utenti devono selezionare un solo pulsante di scelta. |
| Pulsante Invia di Forms | Un pulsante di invio aggiuntivo per il modulo in cui il titolo viene visualizzato come testo sul pulsante. |
| Campo di testo Forms | Campo di testo che consente agli utenti di immettere informazioni. |
| Gadget personali | Consente di includere uno dei gadget disponibili selezionati. |
| Foto avatar profilo | Consente di inserire una foto avatar. |
| Nome completo profilo | Inserimento dei dettagli del nome, compresi elementi quali titolo, secondo nome e suffisso, se necessario. |
| Nome visualizzato profilo | Nome da visualizzare. |
| E-mail profilo | Inserimento di un indirizzo e-mail. |
| Genere profilo | Consente di immettere il genere. |
| Numero di telefono principale del profilo | Consente di immettere un numero di telefono. |
| URL principale profilo | Consente di inserire un URL. |
| Proprietà Testo generale profilo | Proprietà del profilo. |
| Accedi | Consente di inviare un nome utente e una password al momento dell&#39;accesso. |
| Esci | Indica l&#39;utente attualmente connesso e fornisce un collegamento per la disconnessione. |
| Tag cloud | Una nuvola di tag per mostrare una selezione di tag presentata graficamente all’interno del sito web |
| Teaser | Contenuto (in genere un’immagine) visualizzato in una pagina principale per &quot;prendere in giro&quot; gli utenti per accedere al contenuto sottostante. |

## Personalizzazione e contenuti della community {#personalization-and-community-content}

Le funzioni della community come blog, forum e calendari determinano la creazione di contenuti comunitari, comunemente denominati contenuti generati dagli utenti (UGC, User Generated Content). Quando UGC viene inserito in un ambiente di pubblicazione costituito da più istanze AEM (un [farm di pubblicazione](/help/communities/topologies.md)), un problema importante è stato come sincronizzare UGC tra tutte le istanze.

Con [AEM Communities 6.1](/help/communities/overview.md) , questo problema viene risolto utilizzando un [archivio comune per UGC](/help/communities/working-with-srp.md). Per quanto riguarda, la personalizzazione, Community include [Accesso social network](/help/communities/social-login.md) : possibilità per i visitatori del sito di accedere con Facebook e Twitter.

Senza l’estensione Communities, puoi esplorare diversi metodi per risolvere il problema della coerenza UGC:

* Sincronizzare più istanze di pubblicazione quando necessario
* Invia l’UGC dall’istanza di pubblicazione all’ambiente di authoring, da cui può essere pubblicato in modo simile alla pubblicazione del contenuto della pagina

Il metodo utilizzato per ottenere la coerenza UGC in un ambiente di pubblicazione costituito da più istanze di pubblicazione deve essere attentamente progettato e testato per verificarne le prestazioni e la coerenza.
