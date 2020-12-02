---
title: Linee guida per le dimensioni dell’hardware
seo-title: Linee guida per le dimensioni dell’hardware
description: Queste linee guida sul ridimensionamento offrono un'approssimazione delle risorse hardware necessarie per distribuire un progetto AEM.
seo-description: Queste linee guida sul ridimensionamento offrono un'approssimazione delle risorse hardware necessarie per distribuire un progetto AEM.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 1%

---


# Linee guida per le dimensioni dell’hardware{#hardware-sizing-guidelines}

Queste linee guida sul ridimensionamento offrono un&#39;approssimazione delle risorse hardware necessarie per distribuire un progetto AEM. Le stime di dimensionamento dipendono dall&#39;architettura del progetto, dalla complessità della soluzione, dal traffico previsto e dai requisiti del progetto. Questa guida consente di determinare le esigenze hardware di una soluzione specifica o di trovare una stima superiore e inferiore per i requisiti hardware.

I fattori di base da considerare sono (in questo ordine):

* **Velocità di rete**

   * Latenza della rete
   * Larghezza di banda disponibile

* **Velocità computazionale**

   * Efficienza della cache
   * Traffico previsto
   * Complessità di modelli, applicazioni e componenti
   * Autori simultanei
   * Complessità dell’operazione di authoring (semplice modifica dei contenuti, implementazione MSM ecc.)

* **Prestazioni I/O**

   * Prestazioni ed efficienza della memorizzazione del file o del database

* **Unità disco rigido**

   * almeno due o tre volte più grandi della dimensione del repository

* **Memoria**

   * Dimensione del sito Web (numero di oggetti-contenuto, pagine e utenti)
   * Numero di utenti/sessioni che sono attivi contemporaneamente

## Architettura {#architecture}

Una tipica configurazione AEM consiste in un ambiente di authoring e pubblicazione. Questi ambienti presentano requisiti diversi per quanto riguarda le dimensioni hardware e la configurazione del sistema sottostanti. Considerazioni dettagliate per entrambi gli ambienti sono descritte nelle sezioni [ambiente di authoring](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente di pubblicazione](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

In una configurazione di progetto tipica, sono disponibili diversi ambienti in cui è possibile organizzare le fasi di progetto:

* **Sviluppo**
dell&#39;ambienteSviluppare nuove funzioni o apportare modifiche significative. La best practice consiste nell&#39;utilizzare un ambiente di sviluppo per sviluppatore (in genere installazioni locali sui propri sistemi personali).

* **Ambiente di test dell&#39;autorePer verificare**
le modifiche. Il numero di ambienti di test può variare a seconda dei requisiti del progetto (ad esempio, separati per il controllo della qualità, il test di integrazione o il test di accettazione da parte dell&#39;utente).

* **Pubblica**
l’ambiente di provaPrincipalmente per testare i casi di utilizzo della collaborazione mediante social network e/o l’interazione tra l’autore e più istanze di pubblicazione.

* **Ambiente di produzione**
dell&#39;autoreConsente agli autori di modificare il contenuto.

* **Pubblica**
ambiente di produzionePer distribuire il contenuto pubblicato.

Inoltre, gli ambienti possono variare, da un sistema a server singolo che esegue AEM e un server applicazione, a un set di istanze cluster multi-server e multi-CPU. È consigliabile utilizzare un computer separato per ciascun sistema di produzione e non eseguire altre applicazioni su questi computer.

## Considerazioni generali sul ridimensionamento hardware {#generic-hardware-sizing-considerations}

Le sezioni seguenti forniscono indicazioni su come calcolare i requisiti hardware, tenendo conto di varie considerazioni. Per i sistemi di grandi dimensioni, consigliamo di eseguire una semplice serie di test di benchmark interni su una configurazione di riferimento.

L&#39;ottimizzazione delle prestazioni è un&#39;attività fondamentale che deve essere eseguita prima che sia possibile eseguire il benchmarking per un progetto specifico. Prima di eseguire qualsiasi test di benchmark e di utilizzare i relativi risultati per qualsiasi calcolo del ridimensionamento hardware, assicurarsi di applicare i consigli forniti nella [Documentazione sull&#39;ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

I requisiti di dimensionamento hardware per i casi di utilizzo avanzati devono essere basati su una valutazione dettagliata delle prestazioni del progetto. Le caratteristiche dei casi d&#39;uso avanzati che richiedono risorse hardware eccezionali includono combinazioni di:

* payload/throughput ad alto contenuto
* uso esteso di codice personalizzato, flussi di lavoro personalizzati o librerie software di terze parti
* integrazione con sistemi esterni non supportati

### Spazio su disco/Unità disco rigido {#disk-space-hard-drive}

Lo spazio su disco richiesto dipende in larga misura dal volume e dal tipo dell&#39;applicazione Web. I calcoli dovrebbero tener conto:

* la quantità e le dimensioni di pagine, risorse e altre entità memorizzate nel repository, come flussi di lavoro, profili ecc.
* la frequenza stimata delle modifiche dei contenuti e quindi la creazione di versioni dei contenuti
* il volume delle rappresentazioni delle risorse DAM che verranno generate
* la crescita complessiva del contenuto nel tempo

Lo spazio su disco viene monitorato continuamente durante la pulizia online e offline delle revisioni. Se lo spazio disponibile su disco scende al di sotto di un valore critico, il processo verrà annullato. Il valore critico è il 25% dell&#39;attuale spazio su disco del repository e non è configurabile. Si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione del repository, inclusa la crescita stimata.

È consigliabile configurare array ridondanti di dischi indipendenti (RAID, ad esempio RAID10) per la ridondanza dei dati.

>[!NOTE]
>
>La directory temporanea di un&#39;istanza di produzione deve avere almeno 6 GB di spazio disponibile.

#### Virtualizzazione {#virtualization}

AEM funziona bene in ambienti virtualizzati, ma ci possono essere fattori come CPU o I/O che non possono essere direttamente equiparati all&#39;hardware fisico. Una raccomandazione consiste nel scegliere una velocità di I/O più elevata (in generale), in quanto questo è un fattore critico nella maggior parte dei casi. Per comprendere con precisione quali risorse saranno necessarie, è necessario eseguire il benchmarking del proprio ambiente.

#### Parallelizzazione delle istanze AEM {#parallelization-of-aem-instances}

**Sicurezza non corretta**

Un sito Web sicuro per errore viene distribuito in almeno due sistemi separati. Se un sistema si rompe, un altro sistema può subentrare e quindi compensare il guasto del sistema.

**Scalabilità delle risorse di sistema**

Mentre tutti i sistemi sono in esecuzione, è disponibile un aumento delle prestazioni computazionali. che le prestazioni aggiuntive non sono necessariamente lineari con il numero di nodi del cluster, in quanto la relazione dipende fortemente dall&#39;ambiente tecnico; per ulteriori informazioni, consultare la [Documentazione cluster](/help/sites-deploying/recommended-deploys.md).

La stima del numero di nodi del cluster necessari si basa sui requisiti di base e sui casi di utilizzo specifici del progetto Web specifico:

* Dal punto di vista della sicurezza in caso di fallimento, è necessario determinare, per tutti gli ambienti, quanto sia critico il fallimento e il tempo di compensazione in caso di guasto in base al tempo necessario per il ripristino di un nodo del cluster.
* Per l&#39;aspetto della scalabilità, il numero di operazioni di scrittura è sostanzialmente il fattore più importante; consultate [Autori che lavorano in parallelo](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel) per l&#39;ambiente di authoring e [Social Collaboration](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations) per l&#39;ambiente di pubblicazione. Il bilanciamento del carico può essere stabilito per le operazioni che accedono al sistema esclusivamente per il processo di lettura; per ulteriori informazioni, vedere [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## Calcoli specifici dell&#39;ambiente di authoring {#author-environment-specific-calculations}

A scopo di benchmarking,  Adobe ha sviluppato alcuni test di benchmark per gli autori indipendenti.

* **Benchmark test 1**
Consente di calcolare il throughput massimo di un profilo di carico in cui gli utenti eseguono un semplice esercizio di creazione della pagina oltre a un carico di base di 300 pagine esistenti tutte di natura simile. I passaggi necessari erano l’accesso al sito, la creazione di una pagina con un file SWF e un file immagine/testo, l’aggiunta di un tag cloud e l’attivazione della pagina.

   * ****
Risultato: il throughput massimo per un semplice esercizio di creazione di pagine come sopra (considerato come una transazione) è stato rilevato come 1730 transazioni/ora.

* **Test Benchmark 2**
Consente di calcolare il throughput massimo quando il profilo di carico presenta una combinazione di creazione di nuove pagine (10%), modifica di una pagina esistente (80%) e creazione e successiva modifica di una pagina in successione (10%). La complessità delle pagine rimane la stessa del profilo del test di benchmark 1. La modifica di base della pagina viene eseguita aggiungendo un&#39;immagine e modificando il contenuto del testo. Anche in questo caso, l&#39;esercizio è stato eseguito su un carico di base di 300 pagine della stessa complessità definita nel test di riferimento 1.

   * **Il throughput**
ResultMaximum per uno scenario di operazione mix di questo tipo è risultato essere 3252 transazioni all&#39;ora.

>[!NOTE]
>
>La velocità effettiva non fa distinzione tra i tipi di transazione all&#39;interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput assicura che una percentuale fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

Le due prove di cui sopra evidenziano chiaramente che il throughput varia a seconda del tipo di operazione. Utilizzate le attività nell&#39;ambiente come base per il ridimensionamento del sistema. Potrai ottenere un throughput migliore con azioni meno complesse come la modifica (anch’essa più comune).

### Cache {#caching}

Nell’ambiente di authoring, l’efficienza di memorizzazione nella cache è in genere molto inferiore, perché le modifiche al sito Web sono più frequenti e anche il contenuto è altamente interattivo e personalizzato. Utilizzando il dispatcher, potete memorizzare nella cache AEM librerie, JavaScript, file CSS e immagini di layout. Questo consente di velocizzare alcuni aspetti del processo di authoring. La configurazione del server Web per impostare intestazioni aggiuntive per il caching dei browser su queste risorse riduce il numero di richieste HTTP e migliora quindi la capacità di risposta del sistema, come sperimentato dagli autori.

### Autori in parallelo {#authors-working-in-parallel}

Nell’ambiente di authoring, il numero di autori che lavorano in parallelo e il caricamento delle loro interazioni aggiungono al sistema sono i principali fattori di limitazione. Pertanto, consigliamo di ridimensionare il sistema in base al flusso condiviso di dati.

Per tali scenari  Adobe ha eseguito test di benchmark su un cluster di istanze dell&#39;autore con elementi condivisi a due nodi.

* **Test Benchmark 1**
aCon un cluster attivo-attivo shared-nothing di 2 istanze di autori, calcolare il throughput massimo con un profilo di carico in cui gli utenti eseguono un semplice esercizio di creazione di pagina oltre a un carico base di 300 pagine esistenti, il tutto di natura simile.

   * **Il throughput**
massimo per un semplice esercizio di creazione delle pagine, come sopra, (considerato come una transazione) è risultato essere 2016 transazioni/ora. Si tratta di un aumento di circa il 16% rispetto a un&#39;istanza di autore standalone per lo stesso test di benchmark.

* **Test Benchmark 2**
bCon un cluster attivo-attivo shared-nothing di 2 istanze di creazione, calcolare il throughput massimo quando il profilo di caricamento include una combinazione di creazione di nuove pagine (10%), modifica di pagine esistenti (80%) e creazione e modifica di una pagina in successione (10%). La complessità della pagina rimane la stessa del profilo del test di benchmark 1. La modifica di base della pagina viene eseguita aggiungendo un&#39;immagine e modificando il contenuto del testo. Anche in questo caso, l&#39;esercizio è stato eseguito su un carico di base di 300 pagine di complessità, come definito nel test di riferimento 1.

   * **Il throughput**
ResultMaximum per uno scenario di operazione mista è risultato essere 6288 transazioni/ora. Si tratta di un aumento di circa il 93% rispetto a un&#39;istanza di autore standalone per lo stesso test di benchmark.

>[!NOTE]
>
>La velocità effettiva non fa distinzione tra i tipi di transazione all&#39;interno di un profilo di carico. L&#39;approccio utilizzato per misurare il throughput assicura che una percentuale fissa di ciascun tipo di transazione sia inclusa nel carico di lavoro.

I due test di cui sopra evidenziano chiaramente che la AEM viene ridimensionata correttamente per gli autori che eseguono operazioni di modifica di base con AEM. In generale, AEM è più efficace nel ridimensionare le operazioni di lettura.

In un sito Web tipico, la maggior parte delle operazioni di authoring avviene durante la fase di progettazione. Dopo che il sito Web è attivo, il numero di autori che lavorano in parallelo passa solitamente a una media inferiore (modalità operativa).

Potete calcolare il numero di computer (o CPU) necessari per l’ambiente di authoring come segue:

`n = numberOfParallelAuthors / 30`

Questa formula può essere utilizzata come linea guida generale per ridimensionare le CPU quando gli autori eseguono operazioni di base con AEM. Si presuppone che il sistema e l&#39;applicazione siano ottimizzati. Tuttavia, la formula non rimarrà valida per le funzioni avanzate come MSM o Assets (vedere le sezioni seguenti).

Consultare anche i commenti aggiuntivi su [Parallelizzazione](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances) e [Ottimizzazione prestazioni](/help/sites-deploying/configuring-performance.md).

### Recommendations hardware {#hardware-recommendations}

In genere, per l’ambiente di authoring è possibile utilizzare lo stesso hardware consigliato per l’ambiente di pubblicazione. In genere, il traffico dei siti Web è molto inferiore nei sistemi di authoring, ma anche l’efficienza della cache è inferiore. Tuttavia, il fattore fondamentale in questo caso è il numero di autori che lavorano in parallelo, insieme al tipo di azioni che vengono intraprese per il sistema. In generale AEM cluster (dell&#39;ambiente di authoring) è più efficace nel scalare le operazioni di lettura; in altre parole, un cluster AEM può essere ridimensionato in modo ottimale con gli autori che eseguono operazioni di modifica di base.

I test di benchmark  Adobe sono stati eseguiti utilizzando il sistema operativo RedHat 5.5, eseguito su una piattaforma hardware Hewlett-Packard ProLiant DL380 G5 con la seguente configurazione:

* Due CPU Intel Xeon X5450 quad-core a 3,00 GHz
* 8 GB di RAM
* Broadcom NetXtreme II BCM5708 Gigabit Ethernet
* Controller RAID Smart Array HP, 256 MB di cache
* Due dischi SAS da 146 GB e 10.000 rpm configurati come set a strisce RAID0
* SPEC CINT2006 Il punteggio di riferimento del tasso è 110

AEM istanze venivano eseguite con una dimensione di heap minima di 256M, con una dimensione massima di 1024M.

## Calcoli specifici dell&#39;ambiente di pubblicazione {#publish-environment-specific-calculations}

### Efficienza della cache e traffico {#caching-efficiency-and-traffic}

L&#39;efficienza della cache è fondamentale per la velocità del sito Web. La tabella seguente mostra il numero di pagine al secondo che un sistema AEM ottimizzato può gestire utilizzando un proxy inverso, come il dispatcher:

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
>Dichiarazione di non responsabilità: I numeri si basano su una configurazione hardware predefinita e possono variare a seconda dell&#39;hardware utilizzato.

Il rapporto della cache è la percentuale di pagine che il dispatcher può restituire senza dover accedere AEM. 100% indica che il dispatcher risponde a tutte le richieste, 0% indica che AEM calcolare ogni singola pagina.

### Complessità di modelli e applicazioni {#complexity-of-templates-and-applications}

Se utilizzate modelli complessi AEM sarà necessario più tempo per eseguire il rendering di una pagina. Le pagine estratte dalla cache non sono interessate da questo problema, ma la dimensione della pagina è comunque pertinente quando si considera il tempo di risposta complessivo. Il rendering di una pagina complessa può richiedere dieci volte più tempo del rendering di una pagina semplice.

### Formula {#formula}

Utilizzando la seguente formula, potete calcolare una stima della complessità complessiva della soluzione AEM:

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

In base alla complessità, potete determinare il numero di server (o core CPU) necessari per l’ambiente di pubblicazione come segue:

`n = (traffic * complexity / 1000 ) * activations`

Le variabili dell&#39;equazione sono le seguenti:

<table>
 <tbody>
  <tr>
   <td>traffico</td>
   <td>Il traffico di picco previsto al secondo. Potete stimare questo numero come il numero di hit di pagina al giorno, diviso per 35.000.</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>Utilizzate 1 per un'applicazione semplice, 2 per un'applicazione complessa o un valore intermedio:</p>
    <ul>
     <li>1 - un sito completamente anonimo, orientato ai contenuti</li>
     <li>1.1 - un sito completamente anonimo orientato ai contenuti con personalizzazione lato client/Target</li>
     <li>1.5 - un sito orientato ai contenuti con sezioni anonime e con accesso, personalizzazione lato client/Target</li>
     <li>1.7 - per un sito orientato ai contenuti con sezioni anonime e con accesso, personalizzazione lato client/Target e alcuni contenuti generati dall'utente</li>
     <li>2 - dove l'intero sito richiede l'accesso, con un ampio utilizzo di contenuti generati dall'utente e una varietà di tecniche di personalizzazione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>Percentuale di pagine che escono dalla cache del dispatcher. Utilizzate 1 se tutte le pagine provengono dalla cache, o 0 se ogni pagina viene calcolata da AEM.</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>Usate un valore compreso tra 1 e 10 per indicare la complessità dei modelli. Numeri più alti indicano modelli più complessi, utilizzando il valore 1 per i siti con una media di 10 componenti per pagina, il valore 5 per una media di pagina di 40 componenti e 10 per una media di oltre 100 componenti.</td>
  </tr>
  <tr>
   <td>attivazioni</td>
   <td>Numero di attivazioni medie (replica di pagine di dimensioni medie e risorse dall’autore al livello di pubblicazione) per ora divise per x, dove x è il numero di attivazioni eseguite su un sistema senza effetti collaterali sulle prestazioni per altre attività elaborate dal sistema. È inoltre possibile preimpostare un valore iniziale pessimistico come x = 100.<br /> </td>
  </tr>
 </tbody>
</table>

Se disponete di un sito Web più complesso, avete anche bisogno di server Web più potenti in modo che AEM rispondere a una richiesta in un momento accettabile.

* Complessità inferiore a 4:
・ 1024 MB di RAM JVM*
・ CPU a prestazioni ridotte o medie

* Complessità tra 4 e 8:
・ 2048 MB di RAM JVM*
・ CPU mid-to high performance

* Complessità superiore a 8:
・ 4096 MB di RAM JVM*
CPU ad alte prestazioni

>[!NOTE]
>
>* Riservare una quantità sufficiente di RAM per il sistema operativo, oltre alla memoria necessaria per la JVM.

## Calcoli aggiuntivi specifici per casi d&#39;uso {#additional-use-case-specific-calculations}

Oltre al calcolo per un&#39;applicazione Web predefinita, potrebbe essere necessario considerare fattori specifici per i seguenti casi d&#39;uso. I valori calcolati devono essere aggiunti al calcolo predefinito.

### Considerazioni specifiche per le risorse {#assets-specific-considerations}

L&#39;ampia elaborazione delle risorse digitali richiede risorse hardware ottimizzate, i fattori più importanti sono la dimensione delle immagini e il volume di elaborazione delle immagini.

Assegnate almeno 16 GB di heap e configurate il flusso di lavoro [!UICONTROL DAM Update Asset] per utilizzare il [pacchetto Camera Raw](/help/assets/camera-raw.md) per l&#39;assimilazione di immagini non elaborate.

>[!NOTE]
Un maggiore throughput delle immagini significa che le risorse di elaborazione devono essere in grado di stare al passo con l&#39;I/O del sistema e viceversa. Ad esempio, se i flussi di lavoro vengono avviati dall’importazione di immagini, il caricamento di molte immagini tramite WebDAV potrebbe causare un backlog dei flussi di lavoro.
L&#39;utilizzo di dischi separati per TarPM, l&#39;archivio dati e l&#39;indice di ricerca può aiutare a ottimizzare il comportamento I/O del sistema (tuttavia, in genere ha senso mantenere localmente l&#39;indice di ricerca).

>[!NOTE]
Vedere anche la [Guida alle prestazioni delle risorse](/help/sites-deploying/assets-performance-sizing.md).

### Multi-Site Manager {#multi-site-manager}

Il consumo di risorse quando si utilizza AEM MSM in un ambiente di authoring dipende in larga misura dai casi di utilizzo specifici. I fattori di base sono:

* Numero di Live-Copy
* Periodicità dei rollout
* Dimensione della struttura del contenuto da distribuire
* Funzionalità collegata delle azioni di rollout

La verifica del caso di utilizzo pianificato con un estratto di contenuto rappresentativo può facilitare la comprensione del consumo delle risorse. Se si estrapolano i risultati con il throughput pianificato, è possibile valutare le risorse aggiuntive necessarie per l&#39;MSM AEM.

Si prega inoltre di tenere in considerazione che gli autori che lavorano in parallelo percepiranno effetti collaterali delle prestazioni se AEM casi d&#39;uso MSM consumano più risorse di quanto pianificato.

###  considerazioni sul ridimensionamento AEM Communities {#aem-communities-sizing-considerations}

AEM siti che includono  funzioni AEM Communities (siti community) sperimentano un elevato livello di interazione da parte dei visitatori (membri) del sito nell’ambiente di pubblicazione.

Le considerazioni relative al ridimensionamento di un sito community dipendono dall&#39;interazione prevista dai membri della community e dalla maggiore importanza che rivestono le prestazioni ottimali per il contenuto della pagina.

I membri inviati del contenuto generato dall&#39;utente (UGC) vengono memorizzati separatamente dal contenuto della pagina. Mentre la piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall&#39;autore alla pubblicazione,  AEM Communities utilizza un singolo archivio comune per UGC che non viene mai replicato.

Per lo store UGC, è necessario scegliere un provider di risorse di storage (SRP), che influenza la distribuzione scelta.
Consulta

* [Memorizzazione dei contenuti community](/help/communities/working-with-srp.md)
* [Topologie consigliate per community](/help/communities/topologies.md)

