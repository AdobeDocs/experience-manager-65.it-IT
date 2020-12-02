---
title: Elenco di controllo - Ulteriore riferimento
seo-title: Elenco di controllo - Ulteriore riferimento
description: Ulteriori informazioni su dettagli che approfondiscono e/o aumentano i documenti e i principi coperti dall'elenco di controllo Gestione progetti - Best Practices.
seo-description: Ulteriori informazioni su dettagli che approfondiscono e/o aumentano i documenti e i principi coperti dall'elenco di controllo Gestione progetti - Best Practices.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
translation-type: tm+mt
source-git-commit: 37ec3d8ce779ba392e6a92c828efb5fad749abec
workflow-type: tm+mt
source-wordcount: '3783'
ht-degree: 1%

---


# Elenco di controllo - Ulteriore riferimento{#the-checklist-further-reference}

Questa pagina fornisce ulteriori dettagli per approfondire e/o completare i documenti e i principi coperti dalla [Lista di controllo Gestione progetti - Best Practices](/help/managing/best-practices.md).

## AEM - Cosa userete? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>Gli elenchi di cui alla presente sottosezione non sono esaustivi, ma sono intesi come introduzione.

### Funzioni all&#39;interno di AEM {#features-within-aem}

Durante l&#39;implementazione di AEM (in particolare per la prima volta) sarà necessario rivedere le [funzionalità e flussi di lavoro di AEM](https://www.adobe.com/it/marketing/experience-manager.html) per essere certi delle aree desiderate e necessarie.

Considerare le caratteristiche di AEM che si intende utilizzare e l&#39;impatto sulla progettazione; ad esempio:

* [Commerce](/help/sites-administering/ecommerce.md)
* [Schermi](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Assets](/help/assets/assets.md)
* [Tag](/help/sites-administering/tags.md)
* [Gestione multisito e traduzione](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [Community](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

Inoltre, controllare le [Note sulla versione](/help/release-notes/release-notes.md), per le diverse versioni di AEM, per vedere quando sono state aggiunte nuove funzioni.

### Integrations (Integrazioni){#integrations}

AEM può essere integrato con altri prodotti  Adobe e/o servizi di terze parti. Questi possono aumentare la potenza e le funzionalità a vostra disposizione.

Per ulteriori informazioni, vedere [Integrazione delle soluzioni](/help/sites-administering/integration.md).

## Migrare o aggiornare? {#migrate-or-upgrade}

Una considerazione importante è se si desidera:

* Aggiornate l&#39;installazione esistente.
* Migrate il contenuto dal sistema corrente a una nuova installazione.

Per passare da una versione precedente a quella corrente, sono disponibili due opzioni:

* Utilizzate [Package Manager](/help/sites-administering/package-manager.md) per esportare tutto il contenuto e il codice dell&#39;applicazione dal vecchio sistema al nuovo.
* [Il vecchio ](/help/sites-deploying/upgrade.md) sistema è stato aggiornato. Questa è la scelta consigliata nella maggior parte dei casi.

## Regole di base del terreno {#basic-ground-rules}

Come per qualsiasi progetto, è fondamentale stabilire regole di base il prima possibile. Comprendono:

>[!NOTE]
>
>Questi punti sono generici, la [lista di controllo delle best practice](/help/managing/best-practices.md) contiene informazioni specifiche relative alle AEM.

* **Ruoli**

   Questi devono essere chiaramente definiti e resi noti a tutti coloro che partecipano al progetto. Inoltre, è opportuno evidenziare:

   * Decisori
   * Punti di contatto

* **Responsabilità**

   * Per ciascun ruolo, una chiara definizione delle responsabilità relative al progetto contribuisce a evitare confusione.

* **Partecipazione**

   Coinvolgendo al più presto le parti interessate è possibile incoraggiarle a diventare *parti interessate* nel progetto, aumentando così il loro impegno per il suo successo.

   * Dal punto di vista del cliente, questo include gli autori che dovranno collaborare con il sistema giorno per giorno.
   * All&#39;interno del team di progetto, questo includerà anche i responsabili della garanzia della qualità. Più comprendono le esigenze del cliente e meglio possono pianificare i test.

* **Percorsi di comunicazione**

   * Anche se non devono essere formalizzate eccessivamente, le definizioni specifiche dovrebbero garantire che le persone chiave siano sempre informate e quindi aggiornate. Occorre prestare particolare attenzione alla comunicazione con le parti esterne.

* **Processi**

   I processi da definire dipenderanno dal singolo progetto. Tentate di mantenere questi semplici, tenendo conto di:

   * definizione di processi (e percorsi di comunicazione) per interagire con terzi; ad esempio agenzie di progettazione e fornitori di software di terze parti.
   * Spesso il cliente avrà le proprie procedure e strumenti per la gestione dei progetti e la segnalazione.

* **Strumenti di tracciamento**

   Sono disponibili molti strumenti per il tracciamento delle informazioni su bug, attività e altri aspetti del progetto. Per ulteriori informazioni, vedere [Panoramica sugli strumenti potenziali](#overview-of-potential-tools).

   * Il punto chiave da notare qui è di mantenere una sola copia delle informazioni e condividere le informazioni (e quindi l&#39;accesso allo strumento in uso). Questo faciliterà la manutenzione e aiuterà a prevenire le discrepanze.

* **Ambito**

   Definisce chiaramente i settori che devono essere coperti dal progetto a vari livelli:

   * le singole versioni (se viene utilizzato un processo di rilascio iterativo, e indipendentemente dal fatto che siano consegnate ai clienti o al team di test interno).
   * il progetto AEM.
   * l&#39;intero progetto; compresi eventuali software di terze parti, il loro impatto sui test, i problemi organizzativi e molti altri.
   * Per alcuni aspetti può anche essere utile indicare che cosa è *non* nell&#39;ambito del progetto. Ciò può aiutare a prevenire confusione e ipotesi errate, anche se dovrebbe essere limitato a questioni essenziali.

* **Generazione rapporti**

   Definite chiaramente quali informazioni segnalerete, in quale forma, con quale frequenza e a chi.

* **Terminologia**

   * Definire eventuali abbreviazioni e/o termini specifici per il cliente da utilizzare.

* **Ipotesi**

   * Definire eventuali ipotesi in corso.

Tali informazioni possono essere definite all&#39;interno di un manuale del progetto; l&#39;utilizzo di un wiki può anche garantire che le modifiche in corso vengano gestite in modo efficiente. In ogni caso, i fattori chiave sono i seguenti:

* Le informazioni sono definite e mantenute
* Le informazioni sono comunicate chiaramente a tutte le persone interessate. Anche se la prassi standard di gestione dei progetti non può essere ripetuta abbastanza spesso da consentire una chiara definizione del ruolo e una buona comunicazione per realizzare o interrompere un progetto.
* È mantenuta una sola versione di tutte le informazioni oggetto di monitoraggio; ad esempio, tracciamento dei bug, tracciamento dei problemi, ecc.

## Indicatori prestazioni chiave e metriche di destinazione {#key-performance-indicators-and-target-metrics}

Le organizzazioni utilizzano indicatori prestazioni chiave (KPI, Key Performance Indicators) per valutare il loro successo nel raggiungimento dei target. Questi indicatori sono valori misurabili che possono essere utilizzati per dimostrare l&#39;efficacia del conseguimento di obiettivi specifici.

Questi indicatori possono essere:

* Business:

   * Utilizzato per misurare i principali obiettivi aziendali.
   * È importante scegliere KPI appropriati per la vostra attività/scenario con chiare definizioni di cosa sono, come verranno misurati, come verranno utilizzati e da chi.

* Spettacolo:

   * Definire come misurare le prestazioni del sistema.
   * Alcuni esempi includono il tempo di caricamento della pagina, il tempo di risposta del server e le prestazioni delle query del database.

Alcuni indicatori, ma non tutti, possono essere basati sulle metriche di destinazione identificate e definite.

### Metriche di destinazione {#target-metrics}

Le metriche vengono utilizzate per definire le misurazioni quantitative per la qualità del sito Web, ovvero una definizione degli obiettivi prestazionali che si desidera raggiungere e che può essere utilizzata per definire i [KPI (Key Performance Indicators)](#key-performance-indicators-and-target-metrics).

È possibile definire molte metriche, ma spesso quelle definite coprono gli obiettivi per prestazioni e concorrenza. In particolare, fattori che possono essere difficili da quantificare e che sono spesso soggetti a *valutazione emotiva*:

* &quot;il nostro sito Web è *troppo lento* oggi&quot; - quando *lento* è qualificato?

* &quot;tutto *si arresta* quando il mio collega effettua l&#39;accesso&quot; - quanti utenti simultanei possono supportare il sistema?
* &quot;quando si esegue una ricerca, il sistema *si chiude in un blocco* &quot; - quali richieste di ricerca influiscono sul sistema?
* &quot;il download del file richiede *ages*&quot; - quali sono i tempi di download accettabili (in condizioni di rete normali)?

Le metriche di destinazione sono definite all&#39;inizio di un progetto per:

* indicare le dimensioni previste del sito Web che verrà offerto
* indicare la qualità minima che si desidera ottenere
* definire il modo in cui tali fattori saranno effettivamente misurati
* essere utilizzato come base per [Indicatori prestazioni chiave](#key-performance-indicators-and-target-metrics)

Quando si definiscono le metriche di destinazione, occorre sempre prestare attenzione:

* se sono troppo alti, possono essere completamente irraggiungibili
* se impostato su fluttuazioni troppo basse non può essere evidenziato
* per garantire che possano essere misurati ripetutamente e in modo coerente
* per fornire un saldo tra i diversi fattori misurati
* determinate metriche si riferiscono a un ambiente di test, ma alcune dovrebbero riflettere gli scenari reali, in quanto devono essere misurabili e riproducibili nel sito Web di produzione
* priorità delle metriche in base alla loro importanza per il sito Web
* limitare le metriche a un set che può essere monitorato in modo realistico

Durante lo sviluppo del progetto possono essere aggiornati e sintonizzati secondo necessità. Dopo che il progetto è stato implementato correttamente, possono essere utilizzati per controllare l&#39;installazione e monitorare/mantenere i livelli di servizio richiesti per il funzionamento in corso.

Se utilizzate correttamente, queste metriche possono fornire uno strumento utile; se usati in modo irresponsabile, possono essere una distrazione che perde tempo. Come sempre, è necessario capire cosa si sta misurando, come lo si misura e perché.

>[!NOTE]
>
>La presente sezione si occuperà dei principi e delle questioni fondamentali da esaminare. Ogni installazione è diversa, quindi i valori effettivi da misurare saranno diversi.

### Tutto dipende dalla progettazione del progetto {#everything-rests-on-your-project-design}

Tutte le metriche da misurare saranno in qualche modo influenzate dalla progettazione del progetto. Al contrario, molti problemi saranno risolti al meglio con le modifiche alla progettazione.

Pertanto, è necessario definire le metriche di destinazione *prima di* decidere in merito alla progettazione. Questo consente di ottimizzare la progettazione in base a questi fattori. Una volta sviluppato il progetto, sarà difficile apportare modifiche ai principi di progettazione di base.

Quando create la struttura per il sito Web, seguite la struttura consigliata per AEM siti Web. Assicuratevi di comprendere i seguenti problemi e/o principi:

* Come strutturare il contenuto del sito Web.
* Funzionamento di modelli e componenti.
* Come funziona la memorizzazione nella cache.
* L&#39;impatto dei contenuti personalizzati.
* Funzionamento della funzione di ricerca.
* Come utilizzare CSS e tecnologie correlate per creare codice HTML compatto e non ridondante.

Se ritenete che la progettazione non segua le linee guida, o se non siete sicuri di alcune delle implicazioni, chiarite questi problemi prima di iniziare la fase di programmazione o riempire il contenuto.

### Infrastruttura {#infrastructure}

Per definire o valutare l&#39;infrastruttura, sarà utile definire valori target quali:

* visitatori/giorno; media e picco
* hit/day; media e picco
* numero di pagine Web rese disponibili
* volume di contenuti Web

A seconda della situazione e del significato strategico del sito Web, questo vi aiuterà a valutare e scegliere l&#39;infrastruttura:

* numero di server
* numero di istanze AEM (autore e pubblicazione)

### Spettacolo {#performance}

Esistono diversi fattori di prestazione che possono essere valutati:

* tempi di risposta per le singole pagine, tenendo conto:

   * tempi di risposta in un ambiente di authoring
   * tempi di risposta nell’ambiente di pubblicazione

* tempi di risposta per le richieste di ricerca

Questa sezione può essere letta insieme a [Performance Optimization](/help/sites-deploying/configuring-performance.md) che amplia i dettagli tecnici della misurazione effettiva delle prestazioni.

#### Tempi di risposta per le singole pagine {#response-times-for-individual-pages}

Un problema chiave è rappresentato dal tempo impiegato dal sito Web per rispondere alle richieste dei visitatori.

Anche se questo valore varia per ogni richiesta, è possibile definire un valore target medio. Una volta dimostrato che questo valore è sia raggiungibile che gestibile, può essere utilizzato per monitorare le prestazioni del sito web e indicare lo sviluppo di potenziali problemi

Oggetti diversi negli ambienti di creazione e pubblicazione

I tempi di risposta desiderati saranno diversi negli ambienti di creazione e pubblicazione, in base al pubblico di destinazione:

* **Ambiente di authoring**

   Questo ambiente viene utilizzato dagli autori che immettono e aggiornano il contenuto, pertanto deve:

   * per un numero limitato di utenti che generano un numero elevato di richieste durante l’aggiornamento delle pagine di contenuto e dei singoli elementi di tali pagine
   * essere il più veloce possibile per massimizzare la produttività e inserire i contenuti nel sito Web

* **Ambiente di pubblicazione**

   Questo ambiente contiene il contenuto che potete rendere disponibile agli utenti:

   * la velocità è ancora vitale, ma è spesso più lenta rispetto all’ambiente di authoring
   * vengono spesso applicati ulteriori meccanismi di miglioramento delle prestazioni:

      * il contenuto è memorizzato nella cache
      * è applicato il bilanciamento del carico

#### Impostazione dei tempi di risposta della destinazione {#setting-target-response-times}

Come si può decidere sui tempi di risposta raggiungibili (medi)? Spesso si tratta di una questione di esperienza:

* esperienza passata sul sito Web
* esperienza con AEM
* riconoscimento di pagine complesse con tempi di risposta superiori alla media (se possibile, queste devono essere ottimizzate singolarmente)

Tuttavia, in circostanze controllate, si possono applicare le seguenti linee guida:

* Il 70% delle richieste di pagine deve rispondere in meno di 100 ms.
* Il 25% delle richieste di pagine deve rispondere in meno di 100 ms-300 ms.
* Il 4% delle richieste di pagine deve rispondere in meno di 300 ms-500 ms.
* L&#39;1% delle richieste di pagine deve rispondere in meno di 500 ms-1000 ms.
* Nessuna pagina deve rispondere più lentamente di 1 secondo.

I numeri sopra riportati si basano sulle seguenti condizioni:

* misurati al momento della pubblicazione (nessun ambiente di authoring e/o sovraccarico CFC)
* misurati sul server (nessun sovraccarico di rete)
* non memorizzato nella cache (nessuna cache di output AEM, nessuna cache del dispatcher)
* solo per elementi complessi con molte dipendenze (HTML, JS, PDF, ...)
* nessun altro carico sul sistema

Sono disponibili diversi meccanismi per monitorare i tempi di risposta:

* **Monitoraggio dei tempi di risposta con AEM request.log**

   Un buon punto di partenza per l&#39;analisi delle prestazioni è il registro delle richieste. Tra le altre informazioni, potete utilizzarlo per visualizzare i tempi di risposta delle singole richieste. Per ulteriori informazioni, vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

* **Monitoraggio dei tempi di risposta con commenti HTML**

   I commenti HTML possono essere utilizzati per includere informazioni sui tempi di risposta all&#39;interno dell&#39;origine di ciascuna pagina:

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Richieste di ricerca {#search-requests}

Le richieste di ricerca possono avere un impatto significativo sul sito Web, in termini di:

* Tempo di risposta della ricerca effettiva

   * Una funzione di ricerca rapida è un obiettivo di qualità per il sito Web

* Impatto sulle prestazioni generali

   * Poiché una funzione di ricerca deve analizzare (potenzialmente grandi) sezioni del contenuto, o un indice appositamente estratto, ciò può influenzare le prestazioni dell&#39;intero sistema se non ottimizzato

L&#39;impostazione dei target per le richieste di ricerca è, ancora una volta, una questione di esperienza a seconda:

* esperienza di AEM
* una valutazione della frequenza con cui la ricerca sarà utilizzata rispetto ad altri obiettivi
* il responsabile della persistenza
* indice di ricerca
* la complessità della funzione di ricerca; una funzione di ricerca di base che consente solo 1 termine di ricerca di essere inserito sarà più rapida di una ricerca avanzata che consente all&#39;utente di creare istruzioni di ricerca complesse utilizzando AND/OR/NOT.

Questi devono essere pianificati e integrati fin dall&#39;inizio del progetto. I meccanismi disponibili per il monitoraggio comprendono:

* **Monitoraggio dei tempi di risposta della ricerca con AEM request.log**

   Anche in questo caso, request.log può essere utilizzato per monitorare i tempi di risposta per le richieste di ricerca; per ulteriori informazioni, vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

* **Meccanismi programmati per misurare i tempi di risposta delle ricerche**

   Per personalizzare le informazioni raccolte sulle richieste di ricerca e le relative prestazioni, si consiglia di includere la raccolta di informazioni nel codice sorgente del progetto; per ulteriori informazioni, vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

### Convaluta {#concurrency}

Il sito Web verrà reso disponibile a diversi utenti/visitatori, sia nell’ambiente di creazione che nell’ambiente di pubblicazione. I numeri sono spesso più numerosi di quelli utilizzati per i test, ma anche fluttuanti e difficili da prevedere. Il sito Web dovrà essere progettato per un numero medio di utenti/visitatori simultanei, senza che si noti un impatto negativo sulle prestazioni. Anche in questo caso, la `request.log` può essere utilizzata per effettuare test di concorrenza; per ulteriori informazioni, vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

Le destinazioni per il numero di utenti simultanei dipendono dal tipo di ambiente:

* **Ambiente di authoring**

   * In genere, il numero di utenti simultanei può essere stimato con precisione. Saprete quanti autori avete in totale, anche se (probabilmente) non tutti saranno attivi contemporaneamente.

* **Ambiente di pubblicazione**

   * Questo è più difficile da prevedere, quindi è necessario selezionare un valore di destinazione. Anche in questo caso si dovrebbe basare sull&#39;esperienza del sito Web corrente e sulle aspettative realistiche del nuovo sito Web.
   * Eventi speciali (ad esempio quando pubblicate nuovi contenuti molto popolari) possono superare le aspettative - o addirittura le capacità (come talvolta riportato dalla stampa quando i biglietti per alcuni eventi sono messi in vendita).

### Capacità e volume {#capacity-and-volume}

Prima di discutere delle metriche correlate, una rapida definizione dei termini:

* **Volume**

   * La quantità di output elaborata e consegnata dal sistema.

* **Capacità**

   * La capacità del sistema di fornire il volume.
   * In ogni fase, la capacità e il volume vengono misurati in modo diverso, come illustrato nella tabella seguente. Per ottenere prestazioni ottimali, accertatevi che la capacità corrisponda al volume in ogni fase e che sia la capacità che il volume siano condivisi in tutti i passaggi. Ad esempio, potete calcolare la navigazione sul computer client, o inserirla nella cache, invece di elaborarla sul server per ogni richiesta.

* **Capacità e volume**

   | What / Where | Capacità | Volume |
   |---|---|---|
   | Client | Potenza computazionale del computer dell&#39;utente. | Complessità del layout della pagina. |
   | Rete | Larghezza di banda della rete. | Dimensioni della pagina (codice, immagini e così via). |
   | Cache del dispatcher | Memoria server del server Web (memoria principale e disco rigido). | Server Web (memoria principale e disco rigido). Numero e dimensione delle pagine memorizzate nella cache. |
   | Cache di output | Memoria server del server AEM (memoria principale e disco rigido). | Numero e dimensione delle pagine nella cache di output, numero di dipendenze per pagina. La cache del dispatcher riduce questo volume. |
   | Server web | Potenza computazionale del server Web. | Quantità di richieste. La cache abbassa questo volume. |
   | Modello | Potenza computazionale del server Web. | Complessità dei modelli. |
   | Archivio | Prestazioni del repository. | Numero di pagine caricate dalla directory archivio. |

### Altre metriche {#other-metrics}

Le sezioni precedenti descrivono le metriche principali da definire.

A seconda dei requisiti specifici, potrebbe essere utile definire metriche aggiuntive, isolatamente o tenendo conto delle classificazioni di cui sopra.

Tuttavia, è preferibile disporre di un set limitato di metriche di base precise che funzionino in modo facile e affidabile, anziché cercare di misurare e definire ogni aspetto del sito Web. Per sua stessa natura, il tuo sito web inizierà a cambiare ed evolvere non appena viene consegnato ai tuoi utenti.

## Sicurezza {#security}

La sicurezza è fondamentale e una sfida in continua crescita. ***deve*** essere considerato e pianificato fin dalle prime fasi del progetto.

La [lista di controllo di sicurezza](/help/sites-administering/security-checklist.md) procedura dettagliata da eseguire per garantire che l&#39;installazione AEM sia sicura quando distribuita. Altri aspetti di sicurezza sono trattati in [Sicurezza (durante lo sviluppo)](/help/sites-developing/security.md) e [Amministrazione utente e sicurezza](/help/sites-administering/security.md).

## Attività parallele e iterative {#parallel-and-iterative-tasks}

>[!NOTE]
>
>Seguono:
>
>* Offre una panoramica relativa alla *prima* implementazione di un progetto AEM.
>* è intesa come una panoramica astratta; vedere la [lista di controllo del progetto](/help/managing/best-practices.md) per le fasi/tappe/attività specifiche.
>* Ogni scala temporale è teorica.

>



Per una nuova implementazione di un progetto AEM standard è necessario considerare attività quali:

* Consegna dal processo di vendita.
* Implementazione dell&#39;applicazione del cliente (**Sviluppo**).
* Installazione e configurazione dell&#39;infrastruttura (e dei processi correlati) sul sito del cliente (**Infrastruttura**).
* Creazione (o migrazione) del contenuto (**Content**).
* Consegna alle operazioni (**Manutenzione/Assistenza**).
* Seguite i rilasci.

![chlimage_1-2](assets/chlimage_1-2.png)

Per tutti gli aspetti si raccomanda di utilizzare un approccio iterativo:

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Suddividere il lancio del progetto in **Lanci morbidi** (disponibilità ridotta, iterazioni multiple) e **Lancio rigido** (disponibilità completa - Dal vivo) per consentire l&#39;ottimizzazione, l&#39;ottimizzazione e la formazione degli utenti in condizioni realistiche nell&#39;ambiente di produzione.

>[!NOTE]
>
>Per esempi di attività da eseguire (o valutare) durante il ciclo di vita del progetto, vedere [Project Checklist](/help/managing/best-practices.md).

Alcuni punti da sottolineare per ciascuna categoria sono:

* **Sviluppo**

   * Definire innanzitutto l&#39;architettura di base.
   * Utilizzare diverse iterazioni (sprint) per lo sviluppo:

      * La prima fase corrisponde al primo ciclo di sviluppo completo.
      * Il primo risultato di sprint è la prima distribuzione nell&#39;ambiente di test.
      * Ogni sprint ha un risultato scorrevole.
      * Ogni sprint riceve una conclusione da parte del cliente (minimo di test strutturato con feedback).
   * Pianificare l&#39;eventuale aggiornamento della versione AEM disponibile durante il progetto.
   * Pianificare i test e l&#39;ottimizzazione durante gli spruzzi.
   * Pianificare le fasi di stabilizzazione e ottimizzazione.
   * Crea un registro di elementi da pianificare per ulteriori rilasci.
   * Pianificare il coinvolgimento e la consegna dei partner.


* **Infrastruttura**

   * Definire innanzitutto l&#39;architettura di base:

      * Definizione dei requisiti di prestazioni.
      * Definire obiettivi di prestazioni (ad esempio definire chiaramente le aspettative).
      * Definire l&#39;architettura dell&#39;hardware e dell&#39;infrastruttura; incluso il ridimensionamento.
      * Definire la distribuzione.
   * Utilizzare diverse iterazioni; per la prima fase di preparazione e la configurazione iniziale:

      * Ambiente di sviluppo.
      * Processo di sviluppo.
      * Ambiente di prova.
      * Processo di distribuzione (compresa la gestione della configurazione).
   * Pianificare diversi test di carico.
   * Pianificare i test e l&#39;ottimizzazione durante gli spruzzi.
   * Pianificare una fase di stabilizzazione e ottimizzazione.
   * Implementare l&#39;ambiente di produzione il prima possibile (lasciare che il team operativo configuri il sistema per acquisire esperienza).
   * Utilizzate gli utenti denominati e i ruoli definiti il prima possibile.
   * Pianificare la formazione (ad esempio, formazione di amministratore).
   * Piano per il passaggio alle operazioni.



* **Contenuto**

   * L&#39;architettura di base:
      * Gestisce la gerarchia del contenuto.
      * Consente di definire il concetto di contenuto.
      * Definisce l&#39;utilizzo e il layout di MSM.
      * Definisce ruoli, gruppi, flussi di lavoro e autorizzazioni.
   * Considerate l&#39;utilità della creazione offline delle pagine.
   * Pianificate la creazione anticipata di prime pagine e contenuti (da utilizzare nei test e nei feedback).
   * Pianificare la migrazione dei contenuti esistenti.
   * Pianificare la &quot;migrazione in-sprint&quot; dopo il refactoring.
   * Pianificate la &quot;suddivisione del contenuto&quot; (sitemap per il contenuto live).

## Stima del tempo e dello sforzo {#estimating-time-and-effort}

A seconda dell&#39;elenco di attività risultante, è quindi possibile effettuare stime iniziali del tempo e del lavoro necessari per le definizioni di attività (di alto livello). Devono includere un&#39;indicazione di chi (cliente o partner) farà cosa e quando.

L&#39;elenco seguente mostra approssimazioni standard e interrelazioni di sforzo, e quindi costi:

>[!CAUTION]
>
>Tali cifre possono essere utilizzate solo per le stime iniziali. Uno sviluppatore AEM esperto deve eseguire un&#39;analisi dettagliata.

| Fase | Sforzo |
|---|---|
| Sviluppo | Una stima approssimativa di 2-4 ore per ciascun nodo di componente coprirà tutti i requisiti di sviluppo. |
| Test per sviluppatori | 15% di sviluppo |
| Seguito | 10% di sviluppo |
| Documentazione | 15% di sviluppo |
| Documentazione JavaDoc | 10% di sviluppo |
| Correzione dei bug | 15% di sviluppo |
| Gestione progetto | 20% dei costi del progetto per la gestione e la governance dei progetti in corso |

Una pianificazione dettagliata può quindi collegare le risorse disponibili o necessarie a scadenze e costi.

## Architettura di riferimento {#reference-architecture}

L&#39;architettura di riferimento è data per fornire una soluzione modello per l&#39;architettura AEM. L&#39;architettura di riferimento risolve i problemi più comuni riscontrati per i sistemi aziendali, tra cui il ridimensionamento, l&#39;affidabilità e la sicurezza.

È necessario definire le metriche del sito seguenti:

| Classificazione | Definizione |
|---|---|
| Numero di siti Internet |  |
| Numero di siti Intranet |  |
| Numero di basi di codice (ad esempio se Internet e Intranet sono diversi) |  |
| Numero di singole pagine |  |
| Numero di visite al sito / giorno |  |
| Numero di visualizzazioni pagina/giorno |  |
| Volume (in GB) di trasferimento dati/giorno |  |
| Numero di utenti simultanei (gruppo utenti chiuso) |  |
| Numero di visitatori simultanei (pubblicazione) |  |
| Numero di autori simultanei |  |
| Numero di autori registrati |  |
| Numero di attivazioni di pagina/giorno lavorativo |  |
| Numero di attivazioni di pagina durante la distribuzione |  |

## Panoramica degli strumenti potenziali {#overview-of-potential-tools}

Viene fornito l’elenco seguente per informarvi sugli strumenti che possono essere utilizzati. Si tratta di un&#39;introduzione, non di un elenco esteso di raccomandazioni, e certamente non dovrebbe dissuadervi dall&#39;utilizzare altri strumenti che preferite.

<table>
 <tbody>
  <tr>
   <td><strong>Prodotto</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM fornisce una serie di meccanismi che consentono di monitorare, testare, esaminare ed eseguire il debug dell'applicazione; compresi:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modalità Sviluppatore</a></li>
     <li>La <a href="/help/sites-developing/hobbes.md">console di test</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Dashboard operazioni</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Approfondimenti contenuto</a></li>
     <li><a href="/help/sites-authoring/author-environment-tools.md#content-tree">Struttura contenuto</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selenio</td>
   <td><a href="https://docs.seleniumhq.org/"></a> Seleniumis uno strumento di test Open Source. I test vengono eseguiti direttamente nel browser, emulando il funzionamento degli utenti.</td>
  </tr>
  <tr>
   <td>Microsoft Project</td>
   <td>Uno strumento di gestione del progetto di uso comune.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira"></a> Jirais uno strumento Open Source per tenere traccia e gestire i dettagli dei bug software. I flussi di lavoro possono essere imposti sui dettagli del bug come richiesto.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/"></a> Gite un software di controllo revisione.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse è un IDE open source, composto da vari progetti. Si tratta della creazione di una piattaforma di sviluppo aperta, composta da framework estensibili, strumenti e tempi di esecuzione per la creazione, l'implementazione e la gestione del software nel corso del ciclo di vita.</p> <p>Per ulteriori informazioni, vedere <a href="/help/sites-developing/howto-projects-eclipse.md">Come sviluppare AEM progetti con Eclipse</a>.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Un IDE professionale (e quindi soggetto a costi di licenza) che offre una vasta gamma di funzioni. </p> <p>Per ulteriori informazioni, vedere <a href="/help/sites-developing/ht-intellij.md">Come sviluppare AEM progetti con IntelliJ IDEA</a>.</p> </td>
  </tr>
  <tr>
   <td>Paradiso</td>
   <td><a href="https://maven.apache.org/"></a> Mavenis è uno strumento di gestione e comprensione del progetto software che può gestire il processo di creazione di un progetto (software e documentazione).</td>
  </tr>
 </tbody>
</table>

## Lettura successiva {#further-reading}

Inoltre, sono di particolare interesse le seguenti sezioni:

* [Guida introduttiva](/help/sites-deploying/deploy.md#getting-started)
* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Monitoraggio e manutenzione dell’istanza](/help/sites-deploying/monitoring-and-maintaining.md)

### Best practice   {#best-practices}

 Adobe offre ulteriori Best practice per tutte le fasi e per il pubblico:

* [Distribuzione](/help/sites-deploying/best-practices.md)
* [Authoring  ](/help/sites-authoring/best-practices.md)
* [Amministrazione](/help/sites-administering/administer-best-practices.md)
* [Sviluppo](/help/sites-developing/best-practices.md)
* [Gestione progetto](/help/managing/best-practices.md)