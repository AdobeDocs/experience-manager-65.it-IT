---
title: Linee guida per il dimensionamento dell'hardware
description: Queste linee guida sul dimensionamento offrono un'approssimazione delle risorse hardware necessarie per implementare un progetto AEM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
solution: Experience Manager, Experience Manager 6.5
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '2833'
ht-degree: 0%

---

# Linee guida per il dimensionamento dell&#39;hardware{#hardware-sizing-guidelines}

Queste linee guida sul dimensionamento offrono un&#39;approssimazione delle risorse hardware necessarie per implementare un progetto AEM. Le stime di dimensionamento dipendono dall’architettura del progetto, dalla complessità della soluzione, dal traffico previsto e dai requisiti del progetto. Questa guida consente di determinare le esigenze hardware per una soluzione specifica o di trovare una stima superiore e inferiore per i requisiti hardware.

I fattori di base da considerare sono (in questo ordine):

* **Velocità di rete**

   * Latenza di rete
   * Larghezza di banda disponibile

* **Velocità di calcolo**

   * Efficienza della memorizzazione in cache
   * Traffico previsto
   * Complessità di modelli, applicazioni e componenti
   * Autori simultanei
   * Complessità dell’operazione di authoring (modifica semplice dei contenuti, rollout MSM e così via)

* **Prestazioni I/O**

   * Prestazioni ed efficienza dello storage di file o database

* **Disco rigido**

   * almeno due o tre volte più grande della dimensione dell’archivio

* **Memoria**

   * Dimensioni del sito Web (numero di oggetti contenuto, pagine e utenti)
   * Numero di utenti/sessioni attivi contemporaneamente

## Architettura {#architecture}

Una tipica configurazione AEM è costituita da un ambiente di authoring e uno di pubblicazione. Questi ambienti presentano requisiti diversi per quanto riguarda le dimensioni dell&#39;hardware e la configurazione del sistema. Considerazioni dettagliate su entrambi gli ambienti sono descritte nella [ambiente di authoring](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente di pubblicazione](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations) sezioni.

In una tipica configurazione di progetto, sono disponibili diversi ambienti in cui suddividere le fasi del progetto:

* **Ambiente di sviluppo**
Sviluppare nuove funzioni o apportare modifiche significative. Si consiglia di utilizzare un ambiente di sviluppo per sviluppatore (installazioni locali sui propri sistemi personali).

* **Ambiente di test di authoring**
Per verificare le modifiche. Il numero di ambienti di test può variare a seconda dei requisiti del progetto (ad esempio, separati per QA, test di integrazione o test di accettazione da parte dell’utente).

* **Pubblica ambiente di test**
Principalmente per testare casi di utilizzo di collaborazione social e/o l’interazione tra l’istanza di authoring e più istanze di pubblicazione.

* **Ambiente di produzione dell’autore**
Consentire agli autori di modificare il contenuto.

* **Pubblica ambiente di produzione**
Distribuire il contenuto pubblicato.

Inoltre, gli ambienti possono variare, da un sistema a server singolo con AEM e un server applicazioni, fino a un set altamente scalabile di istanze cluster multi-server e multi-CPU. L&#39;Adobe consiglia di utilizzare un computer separato per ogni sistema di produzione e di non eseguire altre applicazioni su tali computer.

## Considerazioni generiche sul dimensionamento dell&#39;hardware {#generic-hardware-sizing-considerations}

Le sezioni seguenti forniscono indicazioni su come calcolare i requisiti hardware, tenendo conto di varie considerazioni. Per i sistemi di grandi dimensioni, ad Adobe, si consiglia di eseguire un semplice set di test di benchmark interni su una configurazione di riferimento.

L’ottimizzazione delle prestazioni è un’attività fondamentale che deve essere eseguita prima di poter eseguire qualsiasi benchmark per un progetto specifico. Assicurati di applicare i consigli forniti nella [Documentazione sull’ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) prima di eseguire test di benchmark e di utilizzare i risultati per i calcoli di dimensionamento hardware.

I requisiti di dimensionamento dell&#39;hardware per i casi d&#39;uso avanzati devono essere basati su una valutazione dettagliata delle prestazioni del progetto. Le caratteristiche dei casi d&#39;uso avanzati che richiedono risorse hardware eccezionali includono:

* payload/throughput di contenuti elevati
* utilizzo esteso di codice personalizzato, flussi di lavoro personalizzati o librerie software di terze parti
* integrazione con sistemi esterni non supportati

### Spazio su disco/Disco rigido {#disk-space-hard-drive}

Lo spazio su disco necessario dipende in larga misura dal volume e dal tipo dell&#39;applicazione Web. I calcoli devono tenere conto dei seguenti elementi:

* la quantità e le dimensioni di pagine, risorse e altre entità memorizzate nell’archivio, ad esempio flussi di lavoro, profili e così via.
* la frequenza stimata delle modifiche ai contenuti e quindi la creazione di versioni dei contenuti
* volume delle rappresentazioni delle risorse DAM che verranno generate
* la crescita complessiva dei contenuti nel tempo

Lo spazio su disco viene costantemente monitorato durante la pulizia delle revisioni online e offline. Se lo spazio su disco disponibile scende al di sotto di un valore critico, il processo viene annullato. Il valore critico è pari al 25% dell&#39;attuale spazio su disco dell&#39;archivio e non è configurabile. L&#39;Adobe consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione dell&#39;archivio, inclusa la crescita stimata.

Considerare la configurazione di array ridondanti di dischi indipendenti (RAID, ad esempio, RAID10) per la ridondanza dei dati.

>[!NOTE]
>
>La directory temporanea di un’istanza di produzione deve disporre di almeno 6 GB di spazio disponibile.

#### Virtualizzazione {#virtualization}

L&#39;AEM funziona bene negli ambienti virtualizzati, ma ci possono essere fattori come CPU o I/O che non possono essere direttamente equiparati all&#39;hardware fisico. Si consiglia di scegliere una velocità di I/O più elevata (in generale), in quanto si tratta solitamente di un fattore critico. Per comprendere con precisione quali risorse sono necessarie, è necessario eseguire un benchmarking dell’ambiente.

#### Parallelizzazione delle istanze AEM {#parallelization-of-aem-instances}

**Sicurezza degli errori**

Un sito Web a prova di errore viene distribuito su almeno due sistemi separati. In caso di guasto di un sistema, un altro sistema può sostituire il sistema e quindi compensare il guasto.

**Scalabilità delle risorse di sistema**

Mentre tutti i sistemi sono in esecuzione, è disponibile un aumento delle prestazioni di elaborazione. Tali prestazioni aggiuntive non sono necessariamente lineari con il numero di nodi cluster, in quanto la relazione dipende in larga misura dall’ambiente tecnico. Consulta [Documentazione del cluster](/help/sites-deploying/recommended-deploys.md) per ulteriori informazioni.

La stima del numero di nodi cluster necessari si basa sui requisiti di base e sui casi d’uso specifici del particolare progetto web:

* Dal punto di vista della sicurezza in caso di guasto, è necessario determinare, per tutti gli ambienti, il livello di criticità del guasto e il tempo di compensazione del guasto in base al tempo necessario per il ripristino di un nodo cluster.
* Per l&#39;aspetto della scalabilità, il numero di operazioni di scrittura è fondamentalmente il fattore più importante; vedere [Autori in parallelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) per l’ambiente di authoring e [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) per l’ambiente di pubblicazione. Il bilanciamento del carico può essere stabilito per le operazioni che accedono al sistema solo per elaborare operazioni di lettura; vedere [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per i dettagli.

## Creare calcoli specifici per l’ambiente {#author-environment-specific-calculations}

A scopo di benchmarking, Adobe ha sviluppato alcuni test di benchmark per le istanze di authoring autonome.

* **Prova di riferimento 1**
Calcola la velocità effettiva massima di un profilo di caricamento in cui gli utenti eseguono un semplice esercizio di creazione pagina sopra un carico di base di 300 pagine esistenti tutte di natura simile. I passaggi necessari consistevano nell’accedere al sito, creare una pagina con un SWF e un’immagine o un testo, aggiungere un tag cloud e attivare la pagina.

   * **Risultato**
La velocità effettiva massima per un semplice esercizio di creazione delle pagine come quello precedente, considerato come una transazione, è di 1730 transazioni/ora.

* **Prova di riferimento 2**
Calcola la velocità effettiva massima quando il profilo di caricamento presenta un mix di creazione di nuove pagine (10%), modifica di una pagina esistente (80%) e creazione, quindi modifica di una pagina in successione (10%). La complessità delle pagine rimane la stessa del profilo del test di riferimento 1. La modifica di base della pagina viene eseguita aggiungendo un’immagine e modificando il contenuto del testo. Anche in questo caso, l’esercizio è stato eseguito in aggiunta a un carico di base di 300 pagine della stessa complessità definita nel test di riferimento 1.

   * **Risultato**
Il throughput massimo per questo scenario di operazioni mix è risultato pari a 3252 transazioni all&#39;ora.

>[!NOTE]
>
>La velocità effettiva non distingue tra i tipi di transazione all’interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput garantisce che una proporzione fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

Le due prove di cui sopra evidenziano chiaramente che il throughput varia a seconda del tipo di operazione. Utilizza le attività del tuo ambiente come base per ridimensionare il sistema. Il throughput è migliore con azioni meno intensive, come la modifica (anche più comune).

### Memorizzazione in cache {#caching}

Nell’ambiente di authoring l’efficienza della memorizzazione in cache è in genere molto inferiore, perché le modifiche al sito web sono più frequenti e il contenuto è altamente interattivo e personalizzato. Utilizzando Dispatcher, puoi memorizzare in cache librerie AEM, JavaScript, file CSS e immagini di layout. Ciò accelera alcuni aspetti del processo di authoring. Configurando il server web per impostare anche le intestazioni per la memorizzazione nella cache del browser su queste risorse, riduce il numero di richieste HTTP e quindi migliora la reattività del sistema in base all’esperienza degli autori.

### Autori in parallelo {#authors-working-in-parallel}

Nell’ambiente di authoring i principali fattori di limitazione sono il numero di autori che lavorano in parallelo e il carico delle loro interazioni aggiunto al sistema. Pertanto, Adobe consiglia di ridimensionare il sistema in base alla velocità effettiva condivisa dei dati.

Per tali scenari, Adobe ha eseguito test di benchmark su un cluster a due nodi condiviso-niente di istanze di authoring.

* **Test comparativo 1a**
Con un cluster active-active shared-Nothing di 2 istanze di authoring, calcola la velocità effettiva massima con un profilo di caricamento in cui gli utenti eseguono un semplice esercizio di creazione pagina sopra un carico di base di 300 pagine esistenti, tutte di natura simile.

   * **Risultato**
La velocità effettiva massima per un semplice esercizio di creazione delle pagine, come quello di cui sopra, considerato come una transazione, è pari a 2016 transazioni/ora. Si tratta di un aumento di circa il 16% rispetto a un’istanza Autore indipendente per lo stesso test di benchmark.

* **Prova comparativa 2b**
Con un cluster active-active shared-Nothing di 2 istanze di authoring, calcola la velocità effettiva massima quando il profilo di caricamento presenta un mix di creazione di pagine nuove (10%), modifica di pagine esistenti (80%) e creazione e modifica di una pagina in successione (10%). La complessità della pagina rimane la stessa del profilo del test benchmark 1. La modifica di base della pagina viene eseguita aggiungendo un’immagine e modificando il contenuto del testo. Anche in questo caso, l’esercizio è stato eseguito in aggiunta a un carico di base di 300 pagine di complessità, come definito nel test di riferimento 1.

   * **Risultato**
Il throughput massimo per questo scenario di operazioni miste è risultato pari a 6288 transazioni/ora. Si tratta di un aumento di circa il 93% rispetto a un’istanza Autore indipendente per lo stesso test di benchmark.

>[!NOTE]
>
>La velocità effettiva non distingue tra i tipi di transazione all’interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput garantisce che una proporzione fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

I due test precedenti evidenziano chiaramente che l&#39;AEM ha una buona scalabilità per gli autori che eseguono operazioni di editing di base con l&#39;AEM. In generale, l&#39;AEM è più efficace nel ridimensionare le operazioni di lettura.

In un sito web tipico, la maggior parte delle operazioni di authoring si svolge durante la fase di progetto. Dopo che il sito web è stato reso disponibile, il numero di autori che lavorano in parallelo solitamente diminuisce fino a raggiungere una media più bassa (modalità operativa).

È possibile calcolare il numero di computer (o CPU) necessari per l&#39;ambiente di authoring nel modo seguente:

`n = numberOfParallelAuthors / 30`

Questa formula può fungere da linea guida generale per il ridimensionamento delle CPU quando gli autori eseguono operazioni di base con AEM. Si presuppone che il sistema e l&#39;applicazione siano ottimizzati. Tuttavia, la formula non sarà true per le funzioni avanzate come MSM o Assets (vedi le sezioni seguenti).

Vedi anche [Parallelizzazione](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

### Recommendations hardware {#hardware-recommendations}

In genere, per l’ambiente di authoring è possibile utilizzare lo stesso hardware consigliato per l’ambiente di pubblicazione. In genere, il traffico del sito web è inferiore nei sistemi di authoring, ma anche l’efficienza della cache è inferiore. Tuttavia, il fattore fondamentale in questo caso è il numero di autori che lavorano in parallelo, insieme al tipo di azioni che vengono effettuate al sistema. In generale, il clustering dell’AEM (dell’ambiente di authoring) è più efficace per ridimensionare le operazioni di lettura; in altre parole, un cluster AEM si adatta bene agli autori che eseguono operazioni di modifica di base.

I test di benchmark Adobe sono stati eseguiti utilizzando il sistema operativo Red Hat® 5.5, eseguito su una piattaforma hardware Hewlett-Packard ProLiant DL380 G5 con la seguente configurazione:

* Due CPU Intel Xeon® X5450 quad-core a 3,00 GHz
* 8 GB di RAM
* Broadcom NetXtreme II BCM5708 Gigabit Ethernet
* Controller RAID HP Smart Array, cache da 256 MB
* Due dischi SAS da 146 GB a 10.000 rpm configurati come set di stripe RAID0
* SPEC CINT2006 Il punteggio del benchmark del tasso è 110

Le istanze AEM erano in esecuzione con una dimensione heap minima di 256 M, una dimensione heap massima di 1024 M.

## Pubblicare calcoli specifici per l’ambiente {#publish-environment-specific-calculations}

### Efficienza e traffico della memorizzazione in cache {#caching-efficiency-and-traffic}

L’efficienza della cache è fondamentale per la velocità del sito web. La tabella seguente mostra quante pagine al secondo un sistema AEM ottimizzato può gestire utilizzando un proxy inverso, come Dispatcher:

| Proporzione cache | Pagine/e (picco) | Milioni di pagine/giorno (media) |
|---|---|---|
| 100% | 1000 — 2000 | 35 - 70 |
| 99% | 910 | 32 |
| 95% | 690 | 25 |
| 90% | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3,5 |

>[!CAUTION]
>
>Esclusione di responsabilità: i numeri si basano su una configurazione hardware predefinita e possono variare a seconda dell&#39;hardware specifico utilizzato.

Il rapporto cache è la percentuale di pagine che Dispatcher può restituire senza dover accedere all’AEM. 100% indica che Dispatcher risponde a tutte le richieste, 0% significa che AEM calcola ogni pagina.

### Complessità di modelli e applicazioni {#complexity-of-templates-and-applications}

Se utilizzi modelli complessi, AEM ha bisogno di più tempo per eseguire il rendering di una pagina. Le pagine prese dalla cache non sono interessate da questo problema, ma la dimensione della pagina è ancora rilevante quando si considera il tempo di risposta complessivo. Il rendering di una pagina complessa può facilmente richiedere dieci volte più tempo rispetto al rendering di una pagina semplice.

### Formula {#formula}

Utilizzando la formula seguente, puoi calcolare una stima della complessità complessiva della soluzione AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

In base alla complessità, è possibile determinare il numero di server (o core CPU) necessari per l’ambiente di pubblicazione nel modo seguente:

`n = (traffic * complexity / 1000 ) * activations`

Le variabili nell&#39;equazione sono le seguenti:

<table>
 <tbody>
  <tr>
   <td>traffico</td>
   <td>Traffico di picco previsto al secondo. Puoi stimare questo dato come il numero di hit di pagina al giorno, diviso per 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilizzare 1 per un'applicazione semplice, 2 per un'applicazione complessa o un valore intermedio:</p>
    <ul>
     <li>1 - un sito completamente anonimo e orientato ai contenuti</li>
     <li>1.1 - Un sito completamente anonimo, orientato ai contenuti con personalizzazione lato client/Target</li>
     <li>1.5 - Un sito orientato ai contenuti con sezioni anonime e connesse, personalizzazione lato client/Target</li>
     <li>1.7 - Per un sito orientato ai contenuti con sezioni anonime e connesse, personalizzazione lato client/Target e alcuni contenuti generati dagli utenti</li>
     <li>2 - laddove l’intero sito richiede l’accesso, con un ampio utilizzo di contenuti generati dagli utenti e varie tecniche di personalizzazione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>La percentuale di pagine che fuoriescono dalla cache di Dispatcher. Usa 1 se tutte le pagine provengono dalla cache, oppure 0 se ogni pagina è calcolata dall’AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Utilizzare un valore compreso tra 1 e 10 per indicare la complessità dei modelli. I numeri più alti indicano modelli più complessi, utilizzando il valore 1 per i siti con una media di 10 componenti per pagina, il valore 5 per una media di 40 componenti e 10 per una media di oltre 100 componenti.</td>
  </tr>
  <tr>
   <td>attivazioni</td>
   <td>Numero medio di attivazioni (replica di pagine e risorse di dimensioni medie dal livello di authoring a quello di pubblicazione) per ora diviso per x, dove x è il numero di attivazioni eseguite su un sistema senza effetti collaterali sulle prestazioni per altre attività elaborate dal sistema. Puoi anche predefinire un valore iniziale pessimistico come x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se si dispone di un sito Web più complesso, è inoltre necessario disporre di server Web più potenti in modo che l&#39;AEM possa rispondere a una richiesta in un tempo accettabile.

* Complessità inferiore a 4:
   * RAM JVM 1024 MB&#42;
   * CPU a prestazioni medio-basse

* Complessità da 4 a 8:
   * RAM JVM DA 2048 MB&#42;
   * CPU a prestazioni medio-elevate

* Complessità superiore a 8:
   * RAM JVM 4096 MB&#42;
   * CPU ad alte prestazioni

>[!NOTE]
>
>&#42; Riserva una quantità di RAM sufficiente per il sistema operativo, oltre alla memoria necessaria per la JVM.

## Calcoli aggiuntivi specifici per casi d’uso {#additional-use-case-specific-calculations}

Oltre al calcolo per un’applicazione web predefinita, considera fattori specifici per i seguenti casi d’uso. I valori calcolati devono essere aggiunti al calcolo predefinito.

### Considerazioni specifiche sulle risorse {#assets-specific-considerations}

L’elaborazione intensiva di risorse digitali richiede risorse hardware ottimizzate, i fattori più rilevanti sono le dimensioni delle immagini e il picco di trasmissione delle immagini elaborate.

Assegna almeno 16 GB di heap e configura l&#39;elemento [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro per utilizzare [pacchetto Camera Raw](/help/assets/camera-raw.md) per l’acquisizione di immagini non elaborate.

>[!NOTE]
>
Un throughput più elevato delle immagini significa che le risorse informatiche devono essere in grado di tenere il passo con l&#39;I/O del sistema e viceversa. Ad esempio, se i flussi di lavoro vengono avviati mediante l’importazione di immagini, il caricamento di molte immagini tramite WebDAV potrebbe causare un backlog di flussi di lavoro.
>
L&#39;utilizzo di dischi separati per TarPM, data store e indice di ricerca può aiutare a ottimizzare il comportamento di I/O del sistema (tuttavia, in genere ha senso mantenere localmente l&#39;indice di ricerca).

>[!NOTE]
>
Consulta anche [Guida alle prestazioni di Assets](/help/sites-deploying/assets-performance-sizing.md).

### Gestione multisito {#multi-site-manager}

Il consumo di risorse quando si utilizza AEM MSM in un ambiente di authoring dipende in larga misura dai casi d’uso specifici. I fattori di base sono:

* Numero di Live Copy
* Periodicità dei rollout
* Dimensioni della struttura contenuto da distribuire
* Funzionalità connessa delle azioni di rollout

Testare il caso d’uso pianificato con un estratto di contenuto rappresentativo può aiutarti a comprendere meglio il consumo delle risorse. Se estrapoli i risultati con la velocità effettiva pianificata, puoi valutare le risorse aggiuntive necessarie per MSM AEM.

Inoltre, sono responsabili degli autori che lavorano in parallelo. Essi percepiranno gli effetti collaterali delle prestazioni se i casi d’uso di AEM MSM consumano più risorse di quanto pianificato.

### Considerazioni sul dimensionamento di AEM Communities {#aem-communities-sizing-considerations}

I siti AEM che includono funzioni di AEM Communities (siti community) presentano un elevato livello di interazione da parte dei visitatori del sito (membri) nell’ambiente di pubblicazione.

Le considerazioni sul dimensionamento di un sito community dipendono dall’interazione prevista dai membri della community e dall’importanza di prestazioni ottimali per il contenuto della pagina.

I membri inviati tramite contenuti generati dagli utenti (UGC, User-generated content) vengono memorizzati separatamente dal contenuto della pagina. Mentre la piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall’ambiente di authoring a quello di pubblicazione, AEM Communities utilizza un singolo archivio comune per i contenuti generati dagli utenti che non vengono mai replicati.

Per l&#39;archivio UGC, è necessario scegliere un provider di risorse di archiviazione (SRP) che influisca sulla distribuzione scelta.
Consulta

* [Archiviazione contenuti community](/help/communities/working-with-srp.md)
* [Topologie consigliate per le community](/help/communities/topologies.md)
