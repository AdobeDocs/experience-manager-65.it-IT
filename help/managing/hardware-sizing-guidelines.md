---
title: Linee guida per le dimensioni dell’hardware
seo-title: Hardware Sizing Guidelines
description: Queste linee guida offrono un’approssimazione delle risorse hardware necessarie per implementare un progetto AEM.
seo-description: These sizing guidelines offer an approximation of the hardware resources required to deploy an AEM project.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2816'
ht-degree: 0%

---

# Linee guida per le dimensioni dell’hardware{#hardware-sizing-guidelines}

Queste linee guida offrono un’approssimazione delle risorse hardware necessarie per implementare un progetto AEM. Le stime delle dimensioni dipendono dall’architettura del progetto, dalla complessità della soluzione, dal traffico previsto e dai requisiti del progetto. Questa guida consente di determinare le esigenze hardware di una soluzione specifica o di trovare una stima superiore e inferiore per i requisiti hardware.

I fattori di base da considerare sono (in questo ordine):

* **Velocità di rete**

   * Latenza di rete
   * Larghezza di banda disponibile

* **Velocità computazionale**

   * Efficienza della memorizzazione in cache
   * Traffico previsto
   * Complessità di modelli, applicazioni e componenti
   * Autori simultanei
   * Complessità dell’operazione di authoring (semplice modifica dei contenuti, rollout MSM, ecc.)

* **Prestazioni I/O**

   * Prestazioni ed efficienza dello storage dei file o dei database

* **Disco rigido**

   * almeno due o tre volte più grandi della dimensione del repository

* **Memoria**

   * Dimensione del sito web (numero di oggetti-contenuto, pagine e utenti)
   * Numero di utenti/sessioni che sono attivi contemporaneamente

## Architettura {#architecture}

Una tipica configurazione AEM consiste in un ambiente di authoring e di pubblicazione. Questi ambienti presentano requisiti diversi per quanto riguarda le dimensioni hardware e la configurazione del sistema sottostanti. Considerazioni dettagliate per entrambi gli ambienti sono descritte nella sezione [ambiente di authoring](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente di pubblicazione](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) sezioni.

In una tipica configurazione di progetto sono disponibili diversi ambienti in cui eseguire l’esecuzione delle fasi di progetto:

* **Ambiente di sviluppo**
Sviluppare nuove funzionalità o apportare modifiche significative. Si consiglia di utilizzare un ambiente di sviluppo per sviluppatore (in genere installazioni locali sui propri sistemi personali).

* **Ambiente di test dell’autore**
Verificare le modifiche. Il numero di ambienti di test può variare a seconda dei requisiti del progetto (ad esempio, separati per QA, test di integrazione o test di accettazione da parte dell’utente).

* **Pubblica ambiente di test**
Principalmente per testare i casi d’uso di collaborazione social e/o l’interazione tra l’autore e più istanze di pubblicazione.

* **Ambiente di produzione di authoring**
Per consentire agli autori di modificare il contenuto.

* **Ambiente di produzione di pubblicazione**
Per distribuire il contenuto pubblicato.

Inoltre, gli ambienti possono variare, da un sistema a server singolo che esegue AEM e un server applicativo, a un set altamente scalato di istanze a cluster multi-server e multi-CPU. Si consiglia di utilizzare un computer separato per ogni sistema di produzione e di non eseguire altre applicazioni su questi computer.

## Considerazioni sul dimensionamento dell&#39;hardware generico {#generic-hardware-sizing-considerations}

Le sezioni seguenti forniscono indicazioni su come calcolare i requisiti hardware, tenendo conto di varie considerazioni. Per i sistemi di grandi dimensioni si consiglia di eseguire un semplice set di test di benchmark interni su una configurazione di riferimento.

L&#39;ottimizzazione delle prestazioni è un compito fondamentale che deve essere svolto prima che sia possibile eseguire un benchmarking per un progetto specifico. Assicurati di applicare il consiglio fornito nella [Documentazione di Performance Optimization](/help/sites-deploying/configuring-performance.md) prima di eseguire qualsiasi test di benchmark e utilizzando i relativi risultati per qualsiasi calcolo di dimensionamento dell&#39;hardware.

I requisiti di dimensionamento dell&#39;hardware per i casi d&#39;uso avanzati devono essere basati su una valutazione dettagliata delle prestazioni del progetto. Le caratteristiche dei casi d’uso avanzati che richiedono risorse hardware eccezionali includono combinazioni di:

* payload/throughput di contenuti elevati
* utilizzo esteso di codice personalizzato, flussi di lavoro personalizzati o librerie software di terze parti
* integrazione con sistemi esterni non supportati

### Spazio su disco/disco rigido {#disk-space-hard-drive}

Lo spazio su disco richiesto dipende in larga misura dal volume e dal tipo dell&#39;applicazione Web. I calcoli dovrebbero tener conto:

* la quantità e le dimensioni di pagine, risorse e altre entità archiviate nell’archivio, come flussi di lavoro, profili, ecc.
* la frequenza stimata delle modifiche dei contenuti e quindi la creazione di versioni dei contenuti
* il volume dei rendering delle risorse DAM che verranno generati
* la crescita complessiva dei contenuti nel tempo

Lo spazio su disco viene monitorato continuamente durante il cleanup delle revisioni online e offline. Se lo spazio su disco disponibile scende al di sotto di un valore critico, il processo verrà annullato. Il valore critico è pari al 25% dell&#39;attuale spazio su disco dell&#39;archivio e non è configurabile. Si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione dell&#39;archivio, inclusa la crescita stimata.

È consigliabile configurare array ridondanti di dischi indipendenti (RAID, ad esempio RAID10) per la ridondanza dei dati.

>[!NOTE]
>
>La directory temporanea di un&#39;istanza di produzione deve avere almeno 6 GB di spazio disponibile.

#### Virtualizzazione {#virtualization}

AEM funziona bene in ambienti virtualizzati, ma ci possono essere fattori come la CPU o l&#39;I/O che non possono essere equati direttamente all&#39;hardware fisico. Si consiglia di scegliere una velocità di I/O più elevata (in generale) in quanto questo è un fattore critico nella maggior parte dei casi. Il benchmarking del tuo ambiente è necessario per capire con precisione quali risorse saranno necessarie.

#### Parallelizzazione delle istanze AEM {#parallelization-of-aem-instances}

**Sicurezza non riuscita**

Un sito web non sicuro per errore viene distribuito su almeno due sistemi separati. Se un sistema si rompe, un altro sistema può assumere il controllo e quindi compensare il guasto del sistema.

**Scalabilità delle risorse di sistema**

Mentre tutti i sistemi sono in esecuzione, è disponibile un aumento delle prestazioni computazionali. che le prestazioni aggiuntive non sono necessariamente lineari con il numero di nodi del cluster in quanto la relazione dipende fortemente dall&#39;ambiente tecnico; per favore, vedi [Documentazione del cluster](/help/sites-deploying/recommended-deploys.md) per ulteriori informazioni.

La stima del numero di nodi cluster necessari si basa sui requisiti di base e sui casi d’uso specifici del particolare progetto web:

* Dal punto di vista della sicurezza in caso di errore è necessario determinare, per tutti gli ambienti, quanto sia critico l&#39;errore e il tempo di compensazione in caso di guasto in base al tempo necessario al ripristino di un nodo cluster.
* Per quanto riguarda l&#39;aspetto della scalabilità, il numero di operazioni di scrittura è fondamentalmente il fattore più importante; vedere [Autori in parallelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) per l’ambiente di authoring e [Collaborazione](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) per l’ambiente di pubblicazione. Il bilanciamento del carico può essere stabilito per le operazioni che accedono al sistema unicamente per elaborare le operazioni di lettura; vedere [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) per i dettagli.

## Calcoli specifici dell’ambiente di authoring {#author-environment-specific-calculations}

A fini di benchmarking, l&#39;Adobe ha sviluppato alcuni test di benchmark per istanze autrici autonome.

* **Prova di riferimento 1**
Calcola la velocità effettiva massima di un profilo di carico in cui gli utenti eseguono un semplice esercizio di creazione pagina su un carico base di 300 pagine esistenti tutte di natura simile. I passaggi necessari erano l’accesso al sito, la creazione di una pagina con un SWF e un’immagine/testo, l’aggiunta di un tag cloud e l’attivazione della pagina.

   * **Risultato**
Il throughput massimo per un semplice esercizio di creazione della pagina come sopra (considerato come una transazione) è stato rilevato come 1730 transazioni/ora.

* **Prova di riferimento 2**
Calcola la velocità effettiva massima quando il profilo di caricamento presenta una combinazione di nuova creazione di pagine (10%), modifica di una pagina esistente (80%) e creazione e successiva modifica di una pagina in successione (10%). La complessità delle pagine rimane la stessa del profilo del test di riferimento 1. La modifica di base della pagina viene eseguita aggiungendo un’immagine e modificando il contenuto del testo. Anche in questo caso, l&#39;esercizio è stato eseguito su un carico base di 300 pagine della stessa complessità definita nel test di riferimento 1.

   * **Risultato**
Il throughput massimo per questo scenario operativo misto è risultato essere 3252 transazioni all&#39;ora.

>[!NOTE]
>
>La velocità effettiva non distingue tra i tipi di transazione all’interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput assicura che una percentuale fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

Le due prove di cui sopra evidenziano chiaramente che la velocità effettiva varia a seconda del tipo di funzionamento. Utilizza le attività nell’ambiente come base per il dimensionamento del sistema. Sarà possibile ottenere un throughput migliore con azioni meno intensive, come la modifica (che è anche più comune).

### Memorizzazione in cache {#caching}

Nell’ambiente di authoring l’efficienza di memorizzazione in cache è in genere molto inferiore, perché le modifiche al sito web sono più frequenti e il contenuto è altamente interattivo e personalizzato. Utilizzando il dispatcher, puoi memorizzare nella cache AEM librerie, JavaScript, file CSS e immagini di layout. Questo velocizza alcuni aspetti del processo di authoring. La configurazione del server web per impostare anche le intestazioni per il caching del browser su queste risorse, ridurrà il numero di richieste HTTP e migliorerà quindi la reattività del sistema come sperimentato dagli autori.

### Autori in parallelo {#authors-working-in-parallel}

Nell’ambiente di authoring il numero di autori che lavorano in parallelo e il caricamento delle loro interazioni aggiunge al sistema sono i principali fattori limitanti. Pertanto, ti consigliamo di ridimensionare il sistema in base al throughput condiviso dei dati.

Per tali scenari, ad Adobe, sono stati eseguiti test di benchmark su un cluster di istanze dell&#39;autore a due nodi shared-nothing.

* **Test di riferimento 1a**
Con un cluster attivo-attivo shared-nothing di 2 istanze di authoring, calcola il throughput massimo con un profilo di caricamento in cui gli utenti eseguono un semplice esercizio di creazione di pagina oltre a un carico base di 300 pagine esistenti, il tutto di natura simile.

   * **Risultato**
Il throughput massimo per un semplice esercizio di creazione di pagine, come indicato sopra, (considerato come una transazione) è risultato essere transazioni 2016/ora. Si tratta di un aumento di circa il 16% rispetto a un’istanza di authoring indipendente per lo stesso test di benchmark.

* **Prova di riferimento 2b**
Con un cluster attivo-attivo shared-nothing di 2 istanze di authoring, calcola il throughput massimo quando il profilo di caricamento presenta una combinazione di nuova creazione di pagine (10%), modifica di una pagina esistente (80%) e creazione e modifica di una pagina in successione (10%). La complessità della pagina rimane la stessa del profilo del test di benchmark 1. La modifica di base della pagina viene eseguita aggiungendo un’immagine e modificando il contenuto del testo. Anche in questo caso, l&#39;esercizio è stato eseguito su un carico base di 300 pagine di complessità, come definito nel test di riferimento 1.

   * **Risultato**
Il throughput massimo per questo scenario di operazioni miste è risultato essere 6288 transazioni/ora. Si tratta di un aumento di circa il 93% rispetto a un’istanza di authoring indipendente per lo stesso test di benchmark.

>[!NOTE]
>
>La velocità effettiva non distingue tra i tipi di transazione all’interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput assicura che una percentuale fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

I due test di cui sopra evidenziano chiaramente che la AEM è ben scalata per gli autori che eseguono operazioni di modifica di base con AEM. In generale, AEM è più efficace nel scalare le operazioni di lettura.

In un tipico sito web, la maggior parte delle operazioni di authoring avviene durante la fase del progetto. Una volta che il sito web è attivo, il numero di autori che lavorano in parallelo di solito scende a una media inferiore (modalità operativa).

Puoi calcolare il numero di computer (o CPU) necessari per l’ambiente di authoring come segue:

`n = numberOfParallelAuthors / 30`

Questa formula può fungere da linea guida generale per il ridimensionamento delle CPU quando gli autori eseguono operazioni di base con AEM. Si parte dal presupposto che il sistema e l&#39;applicazione siano ottimizzati. Tuttavia, la formula non sarà valida per le funzioni avanzate come MSM o Assets (vedi le sezioni seguenti).

Si prega di consultare anche i commenti aggiuntivi su [Parallelizzazione](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

### Recommendations hardware {#hardware-recommendations}

In genere è possibile utilizzare per l’ambiente di authoring lo stesso hardware consigliato per l’ambiente di pubblicazione. In genere, il traffico del sito web è molto più basso nei sistemi di authoring, ma anche l’efficienza della cache è più bassa. Tuttavia, il fattore fondamentale in questo caso è il numero di autori che lavorano in parallelo, insieme al tipo di azioni che vengono effettuate al sistema. In generale AEM clustering (dell&#39;ambiente di authoring) è più efficace per scalare le operazioni di lettura; in altre parole, un cluster AEM si adatta bene agli autori che eseguono operazioni di modifica di base.

I test di benchmark in Adobe sono stati eseguiti utilizzando il sistema operativo RedHat 5.5, in esecuzione su una piattaforma hardware Hewlett-Packard ProLiant DL380 G5 con la seguente configurazione:

* Due CPU Intel Xeon quad-core X5450 a 3,00 GHz
* 8 GB di RAM
* Broadcom NetXtreme II BCM5708 Gigabit Ethernet
* Controller RAID Smart Array HP, 256 MB di cache
* Due dischi SAS da 146 GB a 10.000 rpm configurati come set a strisce RAID0
* SPEC CINT2006 Il punteggio di benchmark del tasso è 110

Le istanze AEM erano in esecuzione con una dimensione di heap minima di 256M, una dimensione massima di heap di 1024M.

## Calcoli specifici dell’ambiente di pubblicazione {#publish-environment-specific-calculations}

### Efficienza della memorizzazione in cache e traffico {#caching-efficiency-and-traffic}

L&#39;efficienza della cache è fondamentale per la velocità del sito web. La tabella seguente mostra quante pagine al secondo un sistema AEM ottimizzato può gestire utilizzando un proxy inverso, come il dispatcher:

| Rapporto cache | Pagine/s (picco) | Milioni di pagine al giorno (media) |
|---|---|---|
| 100% | 1000-2000 | 35-70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>Disclaimer: I numeri si basano su una configurazione hardware predefinita e possono variare a seconda dell&#39;hardware specifico utilizzato.

Il rapporto cache è la percentuale di pagine che il dispatcher può restituire senza dover accedere a AEM. Il 100% indica che il dispatcher risponde a tutte le richieste; lo 0% indica che AEM calcola ogni singola pagina.

### Complessità di modelli e applicazioni {#complexity-of-templates-and-applications}

Se utilizzi modelli complessi, AEM bisogno di più tempo per eseguire il rendering di una pagina. Le pagine prelevate dalla cache non sono influenzate da questo, ma la dimensione della pagina è ancora rilevante quando si considera il tempo di risposta complessivo. Il rendering di una pagina complessa può richiedere facilmente dieci volte più tempo del rendering di una pagina semplice.

### Formula {#formula}

Utilizzando la seguente formula, puoi calcolare una stima della complessità complessiva della soluzione AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

In base alla complessità, puoi determinare il numero di server (o core della CPU) necessari per l’ambiente di pubblicazione come segue:

`n = (traffic * complexity / 1000 ) * activations`

Le variabili nell&#39;equazione sono le seguenti:

<table>
 <tbody>
  <tr>
   <td>traffico</td>
   <td>Il traffico di picco previsto al secondo. Puoi stimare questo come il numero di hit di pagina al giorno, diviso per 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilizza 1 per un'applicazione semplice, 2 per un'applicazione complessa o un valore intermedio:</p>
    <ul>
     <li>1 - un sito completamente anonimo, orientato ai contenuti</li>
     <li>1.1 - un sito completamente anonimo e orientato ai contenuti con personalizzazione lato client/Target</li>
     <li>1.5 - un sito orientato ai contenuti con sezioni anonime e registrate, personalizzazione lato client/Target</li>
     <li>1.7 - per un sito orientato ai contenuti con sezioni anonime e registrate, personalizzazione lato client/Target e alcuni contenuti generati dall'utente</li>
     <li>2 - dove l’intero sito richiede l’accesso, con un ampio utilizzo di contenuti generati dall’utente e una varietà di tecniche di personalizzazione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>La percentuale di pagine che provengono dalla cache del dispatcher. Utilizza 1 se tutte le pagine provengono dalla cache o 0 se ogni pagina viene calcolata da AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilizza un valore compreso tra 1 e 10 per indicare la complessità dei modelli. I numeri più alti indicano modelli più complessi; in base al valore 1 per i siti con una media di 10 componenti per pagina, 5 per una media di pagina di 40 componenti e 10 per una media di oltre 100 componenti.</td>
  </tr>
  <tr>
   <td>attivazioni</td>
   <td>Numero di attivazioni medie (replica di pagine e risorse di dimensioni medie dal livello di authoring al livello di pubblicazione) per ora diviso per x, dove x è il numero di attivazioni eseguite su un sistema senza effetti collaterali sulle prestazioni per altre attività elaborate dal sistema. È inoltre possibile predefinire un valore iniziale pessimistico come x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se disponi di un sito web più complesso, hai anche bisogno di server web più potenti in modo che AEM rispondere a una richiesta in un momento accettabile.

* Complessità inferiore a 4: ・ RAM JVM da 1024 MB&#42;
・ CPU dalle prestazioni basse a quelle medie

* Complessità tra 4 e 8: ・ 2048 MB di RAM JVM&#42;
・ CPU media ad alte prestazioni

* Complessità superiore a 8: ・ 4096 MB di RAM JVM&#42;
CPU high-end

>[!NOTE]
>
>&#42; Riserva RAM sufficiente per il tuo sistema operativo oltre alla memoria necessaria per la tua JVM.

## Calcoli aggiuntivi specifici del caso d’uso {#additional-use-case-specific-calculations}

Oltre al calcolo per un&#39;applicazione Web predefinita, potrebbe essere necessario tenere in considerazione fattori specifici per i seguenti casi d&#39;uso. I valori calcolati devono essere aggiunti al calcolo predefinito.

### Considerazioni specifiche sulle risorse {#assets-specific-considerations}

L&#39;elaborazione estensiva delle risorse digitali richiede risorse hardware ottimizzate, i fattori più importanti sono le dimensioni delle immagini e il throughput di picco delle immagini elaborate.

Alloca almeno 16 GB di heap e configura il [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro per utilizzare [pacchetto Camera Raw](/help/assets/camera-raw.md) per l’acquisizione di immagini crude.

>[!NOTE]
>
>Un maggiore throughput delle immagini significa che le risorse informatiche devono essere in grado di tenere il passo con i sistemi I/O e viceversa. Ad esempio, se i flussi di lavoro vengono avviati tramite l’importazione di immagini, il caricamento di molte immagini tramite WebDAV potrebbe causare un backlog dei flussi di lavoro.
>
>L&#39;utilizzo di dischi separati per TarPM, l&#39;archivio dati e l&#39;indice di ricerca può aiutare a ottimizzare il comportamento I/O del sistema (tuttavia, di solito ha senso mantenere l&#39;indice di ricerca localmente).

>[!NOTE]
>
>Vedi anche [Guida alle prestazioni di Assets](/help/sites-deploying/assets-performance-sizing.md).

### Gestione multisito {#multi-site-manager}

Il consumo di risorse quando si utilizza AEM MSM su un ambiente di authoring dipende in larga misura dai casi d’uso specifici. I fattori di base sono:

* Numero di Live Copy
* Periodicità dei rollout
* Dimensioni della struttura del contenuto da distribuire
* Funzionalità collegate delle azioni di rollout

Il test del caso d’uso pianificato con un estratto di contenuto rappresentativo può aiutarti a comprendere meglio il consumo di risorse. Se estrapoli i risultati con il throughput pianificato, puoi valutare le risorse aggiuntive necessarie per l’MSM AEM.

Inoltre, tieni presente che gli autori che lavorano in parallelo percepiranno gli effetti collaterali delle prestazioni se AEM casi di utilizzo di MSM utilizzano più risorse del previsto.

### Considerazioni sul dimensionamento di AEM Communities {#aem-communities-sizing-considerations}

AEM siti che includono funzioni di AEM Communities (siti community) sperimentano un elevato livello di interazione dei visitatori del sito (membri) nell’ambiente di pubblicazione.

Le considerazioni relative alle dimensioni di un sito community dipendono dall’interazione prevista dai membri della community e dall’importanza maggiore o meno che le prestazioni ottimali per il contenuto della pagina rivestano un’importanza maggiore.

I membri inviati al contenuto generato dall’utente (UGC) vengono memorizzati separatamente dal contenuto della pagina. Mentre la piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall’autore alla pubblicazione, AEM Communities utilizza un singolo archivio comune per UGC che non viene mai replicato.

Per l&#39;archivio UGC, è necessario scegliere un provider di risorse di archiviazione (SRP), che influenza la distribuzione scelta.
Consulta

* [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md)
* [Topologie consigliate per community](/help/communities/topologies.md)
