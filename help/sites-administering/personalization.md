---
title: Personalizzazione
seo-title: Personalizzazione
description: Scopri la personalizzazione in AEM.
seo-description: Scopri la personalizzazione in AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 16%

---


# Personalizzazione{#personalization}

## Cos&#39;è la personalizzazione? {#what-is-personalization}

È disponibile un volume sempre crescente di contenuti, sia su siti Internet, extranet o intranet.

La personalizzazione si concentra sulla fornitura all&#39;utente di un ambiente su misura che mostri contenuti dinamici selezionati in base alle sue esigenze specifiche; in base a profili predefiniti, selezione degli utenti o comportamento interattivo degli utenti.

La personalizzazione è caratterizzata da tre elementi principali:

**Utenti**

* con profili, sia individuali che di gruppo. Questi profili contengono caratteristiche (come descrizione del lavoro, posizione, interessi) che possono essere utilizzate per personalizzare i contenuti che possono vedere.
* intraprendere azioni. Questi possono quindi essere analizzati e confrontati con le regole di comportamento per adattare i contenuti visualizzati.

**Contenuto**

* è ciò che l&#39;utente desidera vedere. Preferibilmente il contenuto di interesse e l&#39;utilizzo per l&#39;esecuzione dei propri compiti.
* può essere classificato e quindi messo a disposizione degli utenti in base a regole predefinite.deve essere dinamico; in altre parole, il contenuto
* In un certo senso, deve dipendere dall&#39;utente: se ogni utente visualizza lo stesso contenuto, la personalizzazione risulterebbe ridondante.

**Regole**

* definire in che modo si realizza effettivamente la personalizzazione, quali contenuti possono essere visualizzati dall&#39;utente e quando.

La personalizzazione può essere:

**Explicit**

* Personalizzazione: in base al quale l&#39;utente effettua le selezioni da una scelta di origini di contenuto.

**Implicato**

* Regole basate su: i manager aziendali definiscono regole specifiche per le azioni basate su profili e/o comportamenti specifici.
* Filtro semplice: le selezioni vengono effettuate sulla base di profili predefiniti a livello di utente e/o gruppo.
* Filtro collaborativo/raccomandazione: il comportamento utente è registrato in base a regole predefinite. Queste regole si basano sul comportamento osservato con persone che condividono la stessa opinione. Le informazioni raccolte vengono utilizzate per adattare le informazioni visualizzate all&#39;utente, in particolare sotto forma di raccomandazioni.

## Come e quando è possibile utilizzare la personalizzazione? {#how-and-when-can-personalization-be-used}

La personalizzazione può essere utilizzata in molti casi, ad esempio:

**Pagine Intranet**

* Il contenuto può essere fornito in base alla posizione, al dipartimento e/o al ruolo di un utente, già definito all&#39;interno di una rete interna.
* A seconda della scelta disponibile, l&#39;utente può effettuare ulteriori selezioni.

**Gruppi di utenti specifici, limitati e mirati (estranei)**

* Gli utenti richiedono un login per l&#39;autorizzazione; questo sarà collegato a un profilo che fornirà le informazioni necessarie per la personalizzazione; eventuali dettagli quali la loro posizione, la relazione con il prodotto, la cronologia di utilizzo, le responsabilità di budgeting, ecc.
* Tali istanze possono essere suddivise in siti quali:
* Aziende che forniscono siti web a una sezione altamente specializzata del loro mercato, ad esempio un&#39;azienda farmaceutica che fornisce un sito web specializzato per i medici.
* Aziende che forniscono siti web che consentono ai clienti di visualizzare le informazioni sul conto corrente e sulla fatturazione; ad esempio, fornitori telefonici.

**Sito Web di vendita e distribuzione**

* I siti Web di vendita e distribuzione, come  Amazon, possono combinare un profilo utente, la cronologia delle vendite dell&#39;utente e la cronologia delle loro ricerche per suggerire quali potrebbero interessare all&#39;utente successivo.

**Ricerca siti Web**

* Molti dei principali siti web dei motori di ricerca hanno strumenti analitici molto potenti che registrano il comportamento degli utenti, i termini di ricerca utilizzati e i siti web effettivamente visitati. Viene quindi utilizzato per personalizzare il contenuto fornito, in particolare per la visualizzazione di annunci pubblicitari.

### Punti di forza della personalizzazione e punti da considerare {#strengths-of-personalization-and-points-to-consider}

Di seguito sono riportati i motivi per cui la personalizzazione deve essere utilizzata:

* Un utente può sperimentare un sito Web comodo e mirato.
* La personalizzazione può essere utilizzata per estendere automaticamente l&#39;accesso alla versione più recente del contenuto.
* Le funzioni di collaborazione mediante social network sono disponibili per consentire agli utenti di comunicare tra loro, in base ai profili.
* A un utente può essere fornito il contenuto necessario per eseguire una particolare attività. All&#39;interno della Intranet aziendale, questo può costituire uno strumento prezioso per la diffusione delle informazioni.
* È possibile fornire all&#39;utente il contenuto di cui ha bisogno/desidera, riducendo così il tempo necessario per eseguire le operazioni di ricerca.
* Il fornitore di contenuti può indirizzare il contenuto da visualizzare per categorie specifiche di utenti.
* Le regole possono essere definite per distribuire contenuti basati su combinazioni sia di caratteristiche utente che di comportamento. Questo fornisce un sofisticato meccanismo per personalizzare la loro esperienza Web.

Quando si utilizza la personalizzazione, tenere presente quanto segue:

**Spettacolo**

* Naturalmente l&#39;analisi e la valutazione supplementari hanno un impatto sulle prestazioni. Tuttavia, i metodi utilizzati sono altamente sofisticati e possono essere ottimizzati per minimizzare l&#39;impatto.

**Autorizzazione**

* La personalizzazione richiede un meccanismo di login in quanto il sito Web deve essere in grado di identificare l’utente.

**Caching**

* La memorizzazione nella cache è un aspetto che l&#39;utente vedrà in termini di prestazioni e precisione: quanto velocemente il sito Web distribuisce contenuti personalizzati, ed è sempre attuale.
* La memorizzazione nella cache è un aspetto fondamentale per la configurazione della personalizzazione e occorre prendere il tempo necessario per garantire che venga utilizzata la corretta implementazione. Questo verrà discusso più dettagliatamente in seguito.

**Precisione delle regole**

* La personalizzazione realizzata monitorando il comportamento dell&#39;utente, o impostando regole basate sul profilo dell&#39;utente, deve essere accurata e logica.
* Non c&#39;è niente di più frustrante per l&#39;utente che avere contenuti forzati o negati a loro a causa della logica imprecisa di una regola.
* Pertanto, le regole devono essere ben concepite - con i requisiti dell&#39;utente in primo piano. Ciò può richiedere molto e non deve essere sottovalutato; definire le regole aziendali spesso supera lo sforzo tecnico nell&#39;implementazione della personalizzazione.

**Quando utilizzare**

* Come molte altre funzionalità sul web, la personalizzazione dovrebbe essere usata con attenzione. Il suo utilizzo andrà a vantaggio dell&#39;utente? dovrebbe sempre essere la prima considerazione - o se l&#39;obiettivo desiderato può essere raggiunto con meno sforzo con un altro metodo. La personalizzazione può correre il rischio di essere una funzione che gli utenti configurano una volta (per vedere come funziona) e solo una volta - in quanto non porta loro vantaggi reali.
* La personalizzazione è significativa solo quando il contenuto è dinamico, in qualche modo a seconda dell&#39;utente. Se tutti gli utenti visualizzano lo stesso contenuto, la personalizzazione è ridondante.

**Riservatezza**

* Molti utenti sono preoccupati per la protezione e la sicurezza dei dati. In particolare per quanto riguarda i dati recuperati durante il monitoraggio del loro comportamento durante la navigazione sul Web.

## Personalizzazione e accesso {#personalization-and-access}

La personalizzazione deve essere considerata separatamente dal controllo dell&#39;accesso, ma esse interagiscono.

La personalizzazione stessa non crea alcuna forma di controllo degli accessi. Si tratta semplicemente di un metodo di guida di ciò che l&#39;utente vede; non impedisce all&#39;utente di accedere ad altri contenuti e, come per qualsiasi contenuto, deve già essere assegnato il controllo di accesso corretto.

Tuttavia, il controllo degli accessi può essere utilizzato per creare una forma di personalizzazione. Se consentite o negate a un utente l&#39;accesso ai contenuti, ciò influisce inevitabilmente sulla scelta dei contenuti disponibili, personalizzando in tal modo la propria esperienza Web.

## Componenti disponibili per la personalizzazione {#components-available-for-personalization}

Sono disponibili diversi componenti con AEM per la personalizzazione. Alcuni consentono agli utenti di accedere e modificare i propri profili, altri (come I miei gadget) consentono agli utenti di configurare una pagina specifica:

| Titolo nella barra laterale | Scopo |
|---|---|
| Campo per password verificata | Richiede password e conferma della password. |
| Accesso combinato | Consente all&#39;utente di accedere a un account esistente o di registrarsi per un nuovo account. |
| Campo indirizzo Forms | Campo complesso per l’inserimento di un indirizzo internazionale. |
| Forms Begin | Avvia una definizione del modulo |
| Forms Captcha | Campo che consiste di un termine alfanumerico che viene aggiornato automaticamente. Il componente captcha viene usato per proteggere i siti Web dai bot. |
| Gruppo di caselle di controllo Forms | Più elementi organizzati in un elenco e preceduti da caselle di selezione. Gli utenti possono selezionare più caselle. |
| Elenco a discesa Forms | Più elementi organizzati in un elenco a discesa. Il controllo Per selezione multipla specifica se è possibile selezionare più elementi dell’elenco. |
| Fine Forms | Termina la definizione del modulo. |
| Caricamento file Forms | Elemento che consente all’utente di caricare un file nel server. |
| Campo nascosto Forms | Campo che non viene presentato all’utente. Può essere usato per trasferire un valore al client e di nuovo al server. Questo campo non deve presentare vincoli. |
| Pulsante immagine Forms | Pulsante di invio aggiuntivo per il modulo, rappresentato da un’immagine. |
| Campo password Forms | Come un campo testo, ma per l’inserimento di una sola riga di testo. Inoltre il testo inserito dall’utente non è visibile nel campo. |
| Forms Radio Group | Più elementi organizzati in un elenco e preceduti da un pulsante di scelta. Gli utenti possono selezionare un solo pulsante di scelta. |
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
| Esci | Indica l’utente che ha effettuato l’accesso e fornisce un collegamento per la disconnessione. |
| Tag cloud | Un tag cloud per mostrare una selezione grafica di tag all’interno del sito Web |
| Teaser | Contenuto (in genere un’immagine) visualizzato su una pagina principale per &quot;invitare&quot; gli utenti ad accedere ai contenuti sottostanti. |

## Personalizzazione e contenuto della community {#personalization-and-community-content}

Le funzioni della community Internet, quali blog, forum e calendari, consentono di creare contenuti per la community, comunemente denominati contenuti generati dall’utente (UGC). Quando UGC viene immesso in un ambiente di pubblicazione composto da più istanze di AEM (una [pubblicazione farm](/help/communities/topologies.md)), un problema principale è rappresentato dalla modalità di sincronizzazione UGC tra tutte le istanze.

Con l&#39;estensione [ AEM Communities 6.1](/help/communities/overview.md), questo problema viene risolto utilizzando un [store comune per UGC](/help/communities/working-with-srp.md). Per quanto riguarda la personalizzazione, Communities include [Social Login](/help/communities/social-login.md) - la possibilità di fornire ai visitatori del sito la possibilità di accedere con Facebook e Twitter.

Senza l&#39;estensione Community, vari metodi da esplorare per affrontare la questione della coerenza UGC sono:

* sincronizzate le istanze di pubblicazione multiple quando necessario
* inviate l’UGC dall’istanza di pubblicazione all’ambiente di authoring, da dove può essere pubblicato in modo simile al contenuto della pagina di pubblicazione

Il metodo utilizzato per ottenere la coerenza UGC in un ambiente di pubblicazione composto da più istanze di pubblicazione deve essere attentamente progettato e testato per garantire le prestazioni e la coerenza.
