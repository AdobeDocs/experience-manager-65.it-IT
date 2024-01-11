---
title: Elenco di controllo - Ulteriori riferimenti
description: Scopri ulteriori dettagli che approfondiscono e/o arricchiscono i documenti e i principi coperti dalla checklist Gestione dei progetti - Best practice.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist
content-type: reference
exl-id: 36620e3e-ecdf-4062-bbef-65513362d691
source-git-commit: d2c0dea636280c28e1d5a76d1c5375f21b6eb111
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---

# Elenco di controllo - Ulteriori riferimenti{#the-checklist-further-reference}

Questa pagina fornisce ulteriori dettagli per elaborare e/o integrare i documenti e i principi coperti dal [Gestione dei progetti - Elenco di controllo delle best practice](/help/managing/best-practices.md).

## AEM - Che cosa userai? {#aem-what-will-you-be-using}

>[!CAUTION]
>
>Gli elenchi di questa sottosezione non sono esaustivi, ma intesi come introduzione.

### Caratteristiche all’interno dell’AEM {#features-within-aem}

Quando si implementa l’AEM (in particolare per la prima volta), rivedere [capacità e flussi di lavoro dell’AEM](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html) per essere sicuri di quali aree desiderate o di cui avete bisogno.

Considera le funzioni dell’AEM in uso e l’impatto sulla progettazione, ad esempio:

* [Commerce](/help/commerce/cif-classic/administering/ecommerce.md)
* [Schermi](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it)
* [Risorse](/help/assets/assets.md)
* [Tag](/help/sites-administering/tags.md)
* [Gestione multisito e traduzione](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/using/introduction-aem-forms.md)
* [Communities](/help/communities/deploy-communities.md)

Inoltre, controlla [Note sulla versione](/help/release-notes/release-notes.md), per le varie versioni dell’AEM, per vedere quando sono state aggiunte nuove funzioni.

### Integrazioni {#integrations}

L’AEM può essere integrato con altri prodotti Adobi, con servizi di terze parti o con entrambi. Questi flussi di lavoro possono aumentare la potenza e le funzionalità a tua disposizione.

Consulta [Integrazione delle soluzioni](/help/sites-administering/integration.md) per informazioni complete.

## Eseguire la migrazione o l&#39;aggiornamento? {#migrate-or-upgrade}

Un aspetto importante da considerare è se desideri:

* Aggiornare l&#39;installazione esistente.
* Migrare il contenuto dal sistema corrente a una nuova installazione.

Quando si passa da una versione precedente alla versione corrente, sono disponibili due opzioni:

* Utilizza il [Gestione pacchetti](/help/sites-administering/package-manager.md) per esportare tutto il contenuto e il codice dell&#39;applicazione dal vecchio sistema a quello nuovo.
* [Aggiorna](/help/sites-deploying/upgrade.md) il vecchio sistema sul posto. Questo metodo è in genere la scelta consigliata.

## Regole di base {#basic-ground-rules}

Come per qualsiasi progetto, è fondamentale stabilire regole di base il prima possibile. Tali regole includono:

>[!NOTE]
>
>Questi punti sono generici, [Elenco di controllo delle best practice](/help/managing/best-practices.md) tratta aspetti specifici in relazione all’AEM.

* **Ruoli**

  I ruoli dovrebbero essere chiaramente definiti e resi noti a tutti coloro che sono coinvolti nel progetto. Inoltre, è opportuno evidenziare:

   * Responsabili decisionali
   * Punti di contatto

* **Responsabilità**

   * Per ogni ruolo, una chiara definizione delle responsabilità correlate al progetto aiuta a evitare confusione.

* **Coinvolgimento**

  Coinvolgendo al più presto le parti interessate, puoi incoraggiarle a diventare *stakeholder* nel progetto. Così facendo aumenta il loro impegno per il suo successo.

   * Per quanto riguarda il cliente, questo ruolo include gli autori che lavorano quotidianamente con il sistema
   * All’interno del team del progetto, questo coinvolgimento include anche le persone responsabili del controllo qualità. Più capiscono le esigenze del cliente, meglio possono pianificare i test.

* **Percorsi di comunicazione**

   * Anche se i percorsi di comunicazione non dovrebbero essere formalizzati eccessivamente, definizioni specifiche dovrebbero garantire che le persone chiave siano sempre informate e quindi tenute aggiornate. Particolare attenzione dovrebbe essere prestata alla comunicazione con le parti esterne.

* **Processi**

  I processi definiti dipendono dal singolo progetto. Di nuovo, prova a mantenere questi processi semplici, tenendo in considerazione:

   * Definizione di processi (e percorsi di comunicazione) per interagire con terze parti; ad esempio, agenzie di progettazione e fornitori di software di terze parti, tra gli altri.
   * Spesso il cliente dispone di procedure e strumenti propri per la gestione dei progetti e la generazione dei rapporti.

* **Strumenti di tracciamento**

  Sono disponibili molti strumenti per il tracciamento di informazioni su bug, attività e altri aspetti del progetto - vedi [Panoramica dei potenziali strumenti](#overview-of-potential-tools) per ulteriori dettagli.

   * In questo caso, è importante conservare una sola copia delle informazioni e condividerle (e quindi accedere allo strumento utilizzato). Questo flusso di lavoro semplifica la manutenzione e aiuta a evitare discrepanze.

* **Ambito**

  Definire con chiarezza gli elementi che devono essere coperti dal progetto ai vari livelli:

   * le singole versioni (se viene utilizzato un processo di rilascio iterativo e indipendentemente dal fatto che vengano consegnate ai clienti o al team di test interno).
   * il progetto AEM.
   * l’intero progetto, incluso qualsiasi software di terze parti, il loro impatto sui test, sui problemi organizzativi e molti altri.
   * Per alcuni aspetti, può essere utile anche indicare che cosa è *non* nell&#39;ambito del progetto. Questa idea può aiutare a evitare confusione e presupposti errati, anche se dovrebbe essere limitata a questioni essenziali.

* **Reporting**

  Definisci chiaramente quali informazioni desideri segnalare, in quale forma, con quale frequenza e a chi.

* **Terminologia**

   * Definisci eventuali abbreviazioni e/o terminologia specifica per il cliente da utilizzare.

* **Presupposti**

   * Definisci le ipotesi da effettuare.

Queste informazioni possono essere definite all&#39;interno di un manuale di progetto; l&#39;uso di un Wiki può anche contribuire a garantire che le modifiche in corso siano gestite in modo efficiente. Ovunque siano definite tali ipotesi, i fattori chiave sono i seguenti:

* Le informazioni sono definite e gestite
* Le informazioni vengono comunicate chiaramente a tutte le persone coinvolte. Sebbene la gestione dei progetti sia una pratica standard, non è possibile ripetere abbastanza spesso che una chiara definizione dei ruoli e una buona comunicazione possano creare o interrompere un progetto.
* Per ogni informazione tracciata viene mantenuta una sola versione, ad esempio il tracciamento dei bug e dei problemi.

## Indicatori di prestazioni chiave e metriche di destinazione {#key-performance-indicators-and-target-metrics}

Le organizzazioni utilizzano gli indicatori prestazioni chiave (KPI, Key Performance Indicators) per valutare il successo nel raggiungimento degli obiettivi. Questi indicatori sono valori misurabili che possono essere utilizzati per dimostrare l&#39;efficacia con cui vengono raggiunti gli obiettivi specifici.

Tali indicatori possono essere:

* Aziende:

   * Utilizzato per misurare gli obiettivi aziendali chiave.
   * È importante scegliere i KPI appropriati alla tua azienda/scenario con definizioni chiare di cosa sono, come sono misurati, come vengono utilizzati e da chi.

* Prestazioni:

   * Definire come misurare le prestazioni del sistema.
   * Alcuni esempi includono il tempo di caricamento delle pagine, il tempo di risposta del server e le prestazioni delle query sul database.

Alcuni indicatori, ma non tutti, possono essere basati sulle metriche di destinazione che identifichi e definisci.

### Metriche di Target {#target-metrics}

Le metriche vengono utilizzate per definire misurazioni quantitative per la qualità del sito web. Si tratta fondamentalmente di una definizione degli obiettivi di prestazioni che desideri raggiungere e che possono essere utilizzati per definire [KPI (indicatori chiave di prestazioni)](#key-performance-indicators-and-target-metrics).

È possibile definire molte metriche, ma spesso quelle definite coprono gli obiettivi in termini di prestazioni e concorrenza. In particolare, fattori che possono essere difficili da quantificare e che sono spesso soggetti a *emotivo* valutazione:

* &quot;il sito web è *troppo lento* oggi&quot; - quando fa *lento* qualificato?

* &quot;tutto *si ferma* &quot;quando il mio collega effettua l’accesso&quot; - quanti utenti simultanei può supportare il sistema?
* &quot;quando eseguo una ricerca, il sistema *si ferma* &quot; - quali richieste di ricerca influiscono sul sistema?
* &quot;è necessario *età* per scaricare il file&quot; - quali sono i tempi di download accettabili (in condizioni di rete normali)?

Le metriche di destinazione sono definite all’inizio di un progetto per:

* indica le dimensioni previste del sito web che puoi offrire
* indicare la qualità minima che si desidera ottenere
* definisci come vengono misurati questi fattori
* essere utilizzati come base per [Indicatori prestazioni chiave](#key-performance-indicators-and-target-metrics)

Come sempre, fai molta attenzione quando definisci le metriche di destinazione:

* se impostati su un valore troppo alto, potrebbero non essere raggiungibili
* se impostato, le fluttuazioni troppo basse potrebbero non essere evidenziate
* per garantire che possano essere misurati ripetutamente e in modo coerente
* fornire un equilibrio tra i diversi fattori misurati
* alcune metriche si riferiscono a un ambiente di test, ma alcune dovrebbero riflettere scenari reali in quanto devono essere misurabili e riproducibili sul sito web di produzione
* assegnare la priorità alle metriche in base al loro significato per il sito web
* limitare le metriche a un set che può essere monitorato

Durante lo sviluppo del progetto, possono essere aggiornati e regolati in modo appropriato. Una volta implementato correttamente il progetto, è possibile utilizzarlo per controllare l&#39;installazione e monitorare/mantenere i livelli di servizio richiesti per il funzionamento continuo.

Se utilizzate correttamente, queste metriche possono fornire uno strumento utile; se utilizzate in modo irresponsabile, possono causare una distrazione che comporta una perdita di tempo. Come sempre, capisci cosa stai misurando, come lo stai misurando e perché.

>[!NOTE]
>
>Questa sezione descrive i principi di base e le questioni da considerare. Ogni installazione è diversa, quindi i valori effettivi da misurare tendono a differire.

### Tutto si basa sulla progettazione del progetto {#everything-rests-on-your-project-design}

Tutte le metriche misurate sono influenzate dalla progettazione del progetto. Al contrario, molti problemi possono essere risolti meglio con modifiche alla progettazione.

Pertanto, definisci le metriche target *prima di* decidi il tuo progetto. In questo modo è possibile ottimizzare la progettazione in base a questi fattori. Dopo aver sviluppato il progetto, è difficile rispettare i principi di progettazione di base.

Quando crei la struttura del sito web, segui la struttura consigliata per i siti web AEM. Assicurati di comprendere i seguenti problemi e/o principi:

* Come strutturare il contenuto del sito web.
* Funzionamento di modelli e componenti.
* Come funziona il caching?
* L’impatto dei contenuti personalizzati.
* Funzionamento della funzione di ricerca.
* Come utilizzare i CSS e le tecnologie correlate per creare un codice HTML compatto e non ridondante.

Se ritieni che la tua progettazione non segua le linee guida o se non sei sicuro di alcune delle implicazioni, chiarisci questi problemi. Esegui questa operazione prima di avviare la fase di programmazione o di compilare il contenuto.

### Infrastruttura {#infrastructure}

Per definire o valutare l’infrastruttura, è utile definire valori target quali:

* visitatori/giorno; sia media che picco
* hit/giorno; sia media che picco
* numero di pagine web rese disponibili
* volume di contenuti web

A seconda della situazione e dell&#39;importanza strategica del sito Web, la definizione dell&#39;infrastruttura può essere utile per valutare e scegliere l&#39;infrastruttura:

* numero di server
* numero di istanze AEM (authoring e pubblicazione)

### Prestazioni {#performance}

È possibile valutare diversi fattori di prestazione:

* tempi di risposta per singole pagine, tenendo conto di:

   * tempi di risposta in un ambiente di authoring
   * tempi di risposta nell’ambiente di pubblicazione

* tempi di risposta per le richieste di ricerca

Questa sezione può essere letta con [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) che amplia i dettagli tecnici per misurare davvero le prestazioni.

#### Tempi di risposta per singole pagine {#response-times-for-individual-pages}

Un problema chiave è il tempo impiegato dal sito web per rispondere alle richieste dei visitatori.

Anche se questo valore varia per ogni richiesta, è possibile definire un valore target medio. Una volta dimostrato che questo valore è sia realizzabile che gestibile, può essere utilizzato per monitorare le prestazioni del sito web e indicare lo sviluppo di potenziali problemi

Destinazioni diverse per ambienti di authoring e pubblicazione

I tempi di risposta desiderati sono diversi per gli ambienti di authoring e pubblicazione, a seconda del pubblico di destinazione:

* **Ambiente di authoring**

  Questo ambiente viene utilizzato dagli autori che inseriscono e aggiornano il contenuto, pertanto deve:

   * considera alcuni utenti che generano un numero elevato di richieste durante l’aggiornamento delle pagine di contenuto e dei singoli elementi in tali pagine
   * essere il più veloce possibile per massimizzare la loro produttività per ottenere i contenuti sul tuo sito web

* **Ambiente di pubblicazione**

  Questo ambiente contiene contenuti che rendi disponibili agli utenti:

   * la velocità è ancora fondamentale, ma è spesso più lenta di un ambiente di authoring
   * spesso vengono applicati meccanismi aggiuntivi per migliorare le prestazioni:

      * il contenuto è memorizzato in cache
      * viene applicato il bilanciamento del carico

#### Impostazione dei tempi di risposta del target {#setting-target-response-times}

Come puoi decidere i tempi di risposta (medi) ottenibili? La domanda e la risposta sono spesso una questione di esperienza:

* esperienza sul sito web
* esperienza con AEM
* riconoscimento di pagine complesse con tempi di risposta superiori alla media (se possibile, queste pagine devono essere ottimizzate singolarmente)

Tuttavia, in circostanze controllate, possono essere applicate le seguenti linee guida:

* Il 70% delle richieste di pagine dovrebbe rispondere in meno di 100 ms.
* Il 25% delle richieste di pagine dovrebbe rispondere in meno di 100-300 ms.
* Il 4% delle richieste di pagine dovrebbe rispondere in meno di 300-500 ms.
* L’1% delle richieste di pagine dovrebbe rispondere in meno di 500-1000 ms.
* Nessuna pagina deve rispondere a un tempo inferiore a 1 secondo.

I numeri di cui sopra presuppongono le seguenti condizioni:

* misurato al momento della pubblicazione (nessun ambiente di authoring e/o sovraccarico CFC)
* misurata sul server (nessun sovraccarico di rete)
* non memorizzato in cache (nessuna cache di output AEM, nessuna cache di Dispatcher)
* solo per gli elementi complessi con molte dipendenze (HTML, JS, PDF, ...)
* nessun altro carico sul sistema

Esistono diversi meccanismi che è possibile utilizzare per monitorare i tempi di risposta:

* **Monitoraggio dei tempi di risposta con il registro delle richieste AEM**

  Un buon punto di partenza per l’analisi delle prestazioni è il registro delle richieste. Tra le altre informazioni, puoi vedere i tempi di risposta delle singole richieste. Consulta [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) per ulteriori dettagli.

* **Monitoraggio dei tempi di risposta con i commenti di HTML**

  I commenti di HTML possono essere utilizzati per includere informazioni sui tempi di risposta all’interno dell’origine di ogni pagina:

  `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### Richieste di ricerca {#search-requests}

Le richieste di ricerca possono avere un impatto significativo sul sito web, in termini sia di:

* Tempo di risposta della ricerca effettiva

   * Una funzione di ricerca rapida è un obiettivo di qualità per il tuo sito web

* Impatto sulle prestazioni generali

   * Poiché una funzione di ricerca deve scansionare sezioni (potenzialmente grandi) del contenuto o un indice estratto in modo speciale, questa capacità può influire sulle prestazioni dell’intero sistema, se non ottimizzata

L’impostazione dei target per le richieste di ricerca è, ancora una volta, una questione di esperienza che dipende da:

* esperienza dell’AEM
* una valutazione della frequenza con cui la ricerca viene utilizzata rispetto ad altri obiettivi
* gestione della persistenza
* indice di ricerca
* la complessità della funzione di ricerca; una funzione di ricerca di base che consente di inserire un termine di ricerca è più rapida di una ricerca avanzata che consente all’utente di creare istruzioni di ricerca complesse utilizzando AND/OR/NOT.

Queste richieste di ricerca devono essere pianificate e integrate fin dall’inizio del progetto. I meccanismi di monitoraggio disponibili comprendono:

* **Monitoraggio dei tempi di risposta delle ricerche con il registro delle richieste AEM**

  Anche in questo caso request.log può essere utilizzato per monitorare i tempi di risposta per le richieste di ricerca; vedi [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) per ulteriori dettagli.

* **Meccanismi programmati per la misurazione dei tempi di risposta alle ricerche**

  Per personalizzare le informazioni raccolte sulle richieste di ricerca e sulle relative prestazioni, è consigliabile includere la raccolta di informazioni nel codice sorgente del progetto; vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) per ulteriori dettagli.

### Concorrenza {#concurrency}

Rendi il tuo sito web disponibile ad alcuni utenti e visitatori, sia nell’ambiente di authoring che in quello di pubblicazione. I numeri sono spesso più numerosi di quelli utilizzati durante i test, ma anche fluttuanti e difficili da prevedere. Progetta il tuo sito web per un numero medio di utenti e visitatori simultanei senza notare un impatto negativo sulle prestazioni. Di nuovo, utilizza `request.log` per eseguire test di concorrenza. Consulta [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) per ulteriori dettagli.

Gli obiettivi per il numero di utenti simultanei dipendono dal tipo di ambiente:

* **Ambiente di authoring**

   * Di solito è possibile stimare con precisione il numero di utenti simultanei. Puoi sapere quanti autori hai in totale, anche se (probabilmente) non tutti sono attivi contemporaneamente.

* **Ambiente di pubblicazione**

   * L’ambiente di pubblicazione è più difficile da prevedere, pertanto devi selezionare un valore target. Anche in questo caso, dovrebbe basarsi sull’esperienza del tuo sito web attuale insieme alle aspettative realistiche del nuovo sito web.
   * Eventi speciali (ad esempio, quando pubblichi nuovi contenuti popolari) possono superare le aspettative o persino le funzionalità (come talvolta riportato dalla stampa quando i biglietti per determinati eventi sono resi disponibili per la vendita).

### Capacità e volume {#capacity-and-volume}

Prima di illustrare le metriche correlate, fornisci una rapida definizione dei termini:

* **Volume**

   * Quantità di output elaborata e consegnata dal sistema.

* **Capacità**

   * La capacità del sistema di erogare il volume.
   * Ad ogni passaggio, la capacità e il volume vengono misurati in modo diverso, come illustrato nella tabella seguente. Per ottenere prestazioni ottimali, verificare che la capacità corrisponda al volume in ogni passaggio e che sia la capacità che il volume siano condivisi in tutti i passaggi. Ad esempio, è possibile calcolare la navigazione nel computer client o inserirla nella cache, invece di calcolarla sul server per ogni richiesta.

* **Capacità e volume**

  | Cosa/Dove | Capacità | Volume |
  |---|---|---|
  | Client | Potenza di calcolo del computer dell&#39;utente. | Complessità del layout della pagina. |
  | Rete | Larghezza di banda di rete. | Dimensione della pagina (codice, immagini e così via). |
  | Cache del Dispatcher | Memoria del server Web (memoria principale e disco rigido). | Server web (memoria principale e disco rigido). Numero e dimensioni delle pagine memorizzate in cache. |
  | Cache di output | Memoria del server AEM (memoria principale e disco rigido). | Numero e dimensioni delle pagine nella cache di output, numero di dipendenze per pagina. La cache di Dispatcher riduce questo volume. |
  | Server web | Potenza di elaborazione del server web. | Numero di richieste. La memorizzazione in cache abbassa questo volume. |
  | Modello | Potenza di elaborazione del server web. | Complessità dei modelli. |
  | Archivio | Prestazioni dell’archivio. | Numero di pagine caricate dall’archivio. |

### Altre metriche {#other-metrics}

Le sezioni precedenti descrivono nel dettaglio le metriche principali da definire.

A seconda delle esigenze specifiche, potrebbe essere utile definire metriche aggiuntive, sia singolarmente che tenendo conto delle classificazioni di cui sopra.

Tuttavia, è preferibile disporre di un piccolo insieme di metriche accurate e fondamentali che funzionano in modo semplice e affidabile, piuttosto che cercare di misurare e definire ogni aspetto del sito web. Per sua stessa natura, il tuo sito web inizia a cambiare ed evolversi quando viene consegnato ai tuoi utenti.

## Sicurezza {#security}

La sicurezza è fondamentale e una sfida in continua crescita. It ***deve*** essere considerato e pianificato fin dalle prime fasi del progetto.

Il [Elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md) descrive i passaggi da seguire per garantire la sicurezza dell’installazione dell’AEM durante l’installazione. Altri aspetti di sicurezza sono trattati nell&#39;ambito [Sicurezza (durante lo sviluppo)](/help/sites-developing/security.md) e [Amministrazione utenti e sicurezza](/help/sites-administering/security.md).

## Attività parallele e iterative {#parallel-and-iterative-tasks}

>[!NOTE]
>
>I seguenti elementi:
>
>* Offre una panoramica relativa al *primo* attuazione di un progetto AEM.
>* è intesa come panoramica astratta; consulta la sezione [Elenco di controllo progetto](/help/managing/best-practices.md) per fasi/attività cardine/attività specifiche.
>* Qualsiasi scala temporale è teorica.
>

Per una nuova implementazione di un progetto AEM standard, considera attività quali:

* Consegna dal processo di vendita.
* Implementazione dell&#39;applicazione per il cliente (**Sviluppo**).
* Installazione e configurazione dell&#39;infrastruttura (e dei processi correlati) sul sito del cliente (**Infrastruttura**).
* Creazione (o migrazione) del contenuto (**Contenuto**).
* Consegna alle operazioni (**Manutenzione/Supporto**).
* Versioni di follow-up.

![chlimage_1-2](assets/chlimage_1-2.png)

Per tutti gli aspetti si raccomanda di utilizzare un approccio iterativo:

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>Per consentire la messa a punto, l’ottimizzazione e la formazione degli utenti in condizioni realistiche sull’ambiente di produzione, suddivide il lancio del progetto in **Lancio morbido** (disponibilità ridotta, più iterazioni) e **Lancio rigido** (disponibilità completa - Live).

>[!NOTE]
>
>Consulta la [Elenco di controllo progetto](/help/managing/best-practices.md) per esempi di attività da eseguire (o valutare) durante il ciclo di vita del progetto.

Alcuni punti da notare per ogni categoria sono:

* **Sviluppo**

   * Definisci prima l’architettura di base.
   * Utilizza diverse iterazioni (sprint) per lo sviluppo:

      * Primo sprint equivale al primo ciclo di sviluppo completo.
      * Il primo sprint determina la prima distribuzione nell’ambiente di test.
      * Ogni sprint ha un risultato eseguibile.
      * Ogni sprint ottiene una conclusione del cliente (minimo di test strutturati con feedback).

   * Pianifica l’eventualità di un aggiornamento della versione AEM disponibile durante il progetto.
   * Pianifica i test e l’ottimizzazione durante gli sprint.
   * Pianificare le fasi di stabilizzazione e ottimizzazione.
   * Crea un registro di elementi da pianificare per le prossime versioni.
   * Pianifica il coinvolgimento e il passaggio di consegne dei partner.

* **Infrastruttura**

   * Definire prima l&#39;architettura di base:

      * Definire i requisiti di prestazioni.
      * Definire gli obiettivi di prestazioni (ovvero, definire chiaramente le aspettative).
      * Definizione dell&#39;architettura hardware e dell&#39;infrastruttura, incluse le dimensioni.
      * Definire la distribuzione.

   * Utilizza diverse iterazioni; per il primo sprint e la configurazione iniziale, prepara:

      * Ambiente di sviluppo.
      * Processo di sviluppo.
      * Ambiente di test.
      * Processo di distribuzione (inclusa la gestione della configurazione).

   * Pianificare diversi test di carico.
   * Pianifica i test e l’ottimizzazione durante gli sprint.
   * Pianificare una fase di stabilizzazione e ottimizzazione.
   * Distribuisci all’ambiente di produzione il prima possibile (fai in modo che il team operativo configuri il sistema per acquisire esperienza).
   * Utilizza il prima possibile utenti denominati e ruoli definiti.
   * Pianifica la formazione (ad esempio la formazione degli amministratori).
   * Pianifica il passaggio alle operazioni.

* **Contenuto**

   * Architettura di base:
      * Guida la gerarchia dei contenuti.
      * Consente di definire il concetto di contenuto.
      * Definisce l’utilizzo e il layout di MSM.
      * Definisce ruoli, gruppi, flussi di lavoro e autorizzazioni.
   * Valuta se è utile la creazione di pagine offline.
   * Pianifica la creazione anticipata di prime pagine e contenuti (da utilizzare nei test e nei feedback).
   * Pianifica la migrazione dei contenuti esistenti.
   * Pianifica la &quot;migrazione in-sprint&quot; dopo il refactoring.
   * Pianifica il &quot;burn-down dei contenuti&quot; (mappa del sito per i contenuti live).

## Stima di tempo e impegno {#estimating-time-and-effort}

A seconda dell&#39;elenco di attività risultante, è quindi possibile effettuare una stima iniziale del tempo e dell&#39;impegno necessari per le definizioni di attività (di alto livello). Queste stime devono includere un’indicazione di chi (cliente o partner) fa cosa e quando.

L&#39;elenco seguente mostra approssimazioni standard e interrelazioni di sforzo coinvolte, e quindi costi:

>[!CAUTION]
>
>Questi dati possono essere utilizzati solo per stime iniziali. Un sviluppatore di AEM esperto deve effettuare l&#39;analisi dettagliata.

| Fase | Impegno |
|---|---|
| Ambiente di sviluppo | Una stima approssimativa di 2-4 ore per ciascun nodo componente che copre tutti i requisiti di sviluppo. |
| Test per sviluppatori | 15% dello sviluppo |
| Follow-up | 10% dello sviluppo |
| Documentazione | 15% dello sviluppo |
| Documentazione JavaDoc | 10% dello sviluppo |
| Correzione di bug | 15% dello sviluppo |
| Gestione progetto | 20% dei costi del progetto per la gestione e la governance del progetto |

Una pianificazione dettagliata può quindi mettere in relazione le risorse disponibili o necessarie con le scadenze e i costi.

## Architettura di riferimento {#reference-architecture}

L’architettura di riferimento è fornita per fornire un modello di soluzione per l’architettura dell’AEM. L&#39;architettura di riferimento risolve i problemi più comuni dei sistemi aziendali, tra cui scalabilità, affidabilità e sicurezza.

È necessario definire le metriche del sito seguenti:

| Classificazione | Definizione |
|---|---|
| Numero di siti Internet |  |
| Numero di siti Intranet |  |
| Numero di basi di codice (ad esempio, se Internet e Intranet sono diversi) |  |
| Numero di singole pagine |  |
| Numero di visite al sito/giorno |  |
| Numero di visualizzazioni di pagina/giorno |  |
| Volume (in GB) di trasferimento dati/giorno |  |
| Numero di utenti simultanei (gruppo utenti chiuso) |  |
| Numero di visitatori simultanei (pubblicazione) |  |
| Numero di autori simultanei |  |
| Numero di autori registrati |  |
| Numero di attivazioni pagina/giorno lavorativo |  |
| Numero di attivazioni di pagina durante la distribuzione |  |

## Panoramica dei potenziali strumenti {#overview-of-potential-tools}

Il seguente elenco fornisce informazioni sugli strumenti che possono essere utilizzati. Si tratta di un’introduzione, non di un elenco completo di consigli, e non dovrebbe scoraggiarti dall’utilizzare altri strumenti.

<table>
 <tbody>
  <tr>
   <td><strong>Prodotto</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>L'AEM offre una serie di meccanismi per il monitoraggio, il test, l'analisi e il debug dell'applicazione, tra cui:</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">Modalità Sviluppatore</a></li>
     <li>Il <a href="/help/sites-developing/hobbes.md">Console di test</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">Dashboard operazioni</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">Approfondimenti contenuto</a></li>
     <li>Il <a href="/help/sites-authoring/author-environment-tools.md#content-tree">Struttura contenuto</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selenio</td>
   <td><a href="https://www.selenium.dev/">Selenio</a> è uno strumento di test Open Source. I test vengono eseguiti direttamente nel browser, emulando il funzionamento degli utenti.</td>
  </tr>
  <tr>
   <td>Progetto Microsoft®</td>
   <td>Strumento di gestione dei progetti di uso comune.</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> è uno strumento open source per il tracciamento e la gestione dei dettagli dei bug software. I flussi di lavoro possono essere imposti sui dettagli del bug in base alle esigenze.</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> è un software di controllo della revisione.</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse è un IDE open source, composto da vari progetti. Si concentra sulla creazione di una piattaforma di sviluppo aperta composta da framework estensibili, strumenti e runtime per la creazione, l’implementazione e la gestione del software durante l’intero ciclo di vita.</p> <p>Consulta <a href="/help/sites-developing/howto-projects-eclipse.md">Come sviluppare progetti AEM utilizzando Eclipse</a> per ulteriori informazioni.</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>Un IDE professionale (e quindi soggetto a costi di licenza) che offre una gamma completa di funzioni. </p> <p>Consulta <a href="/help/sites-developing/ht-intellij.md">Come sviluppare progetti AEM utilizzando IntelliJ IDEA</a> per ulteriori informazioni.</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> è uno strumento per la gestione e la comprensione dei progetti software in grado di gestire il processo di creazione di un progetto (software e documentazione).</td>
  </tr>
 </tbody>
</table>

## Ulteriori informazioni {#further-reading}

Sono inoltre di particolare interesse le seguenti sezioni:

* [Guida introduttiva](/help/sites-deploying/deploy.md#getting-started)
* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Monitoraggio e manutenzione dell’istanza](/help/sites-deploying/monitoring-and-maintaining.md)

### Best practice {#best-practices}

Adobe fornisce ulteriori best practice per tutte le fasi e i tipi di pubblico:

* [Distribuzione](/help/sites-deploying/best-practices.md)
* [Authoring](/help/sites-authoring/best-practices.md)
* [Amministrazione](/help/sites-administering/administer-best-practices.md)
* [Sviluppo](/help/sites-developing/best-practices.md)
* [Gestione progetto](/help/managing/best-practices.md)
