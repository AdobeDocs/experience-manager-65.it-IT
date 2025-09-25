---
title: Linee guida per le dimensioni dell’hardware
description: Queste linee guida sul dimensionamento offrono un’approssimazione delle risorse hardware necessarie per implementare un progetto AEM.
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader
source-git-commit: 658e1f6e07fb1219ba186137eb8403bf85383723
workflow-type: ht
source-wordcount: '1351'
ht-degree: 100%

---

# Linee guida per le dimensioni dell’hardware{#hardware-sizing-guidelines}

Queste linee guida sul dimensionamento offrono un’approssimazione delle risorse hardware necessarie per implementare un progetto AEM. Le stime di dimensionamento dipendono dall’architettura del progetto, dalla complessità della soluzione, dal traffico previsto e dai requisiti del progetto. Questa guida consente di determinare le esigenze hardware per una soluzione specifica o di trovare una stima superiore e inferiore per i requisiti hardware.

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

   * Prestazioni ed efficienza dell’archiviazione di file o database

* **Disco rigido**

   * almeno due o tre volte più grande della dimensione dell’archivio

* **Memoria**

   * Dimensioni del sito Web (numero di oggetti contenuto, pagine e utenti)
   * Numero di utenti/sessioni attivi contemporaneamente

## Architettura {#architecture}

Una tipica configurazione di AEM è costituita da un ambiente di authoring e uno di pubblicazione. Questi ambienti presentano requisiti diversi per quanto riguarda le dimensioni dell’hardware e la configurazione del sistema. Considerazioni dettagliate su entrambi gli ambienti sono descritte nelle sezioni [ambiente di authoring](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) e [ambiente di pubblicazione](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

In una tipica configurazione di progetto, sono disponibili diversi ambienti in cui suddividere le fasi del progetto:

* **Ambiente di sviluppo**
Per sviluppare nuove funzioni o apportare modifiche significative. Si consiglia di lavorare utilizzando un ambiente di sviluppo per sviluppatore (installazioni locali sui propri sistemi personali).

* **Ambiente di test dell’autore**
Per verificare le modifiche. Il numero di ambienti di test può variare a seconda dei requisiti del progetto (ad esempio, separati per QA, test di integrazione o test di accettazione da parte dell’utente).

* **Ambiente di test di pubblicazione**
Principalmente per testare casi di utilizzo di collaborazione social e/o l’interazione tra l’istanza di authoring e più istanze di pubblicazione.

* **Ambiente di produzione di authoring**
Per consentire agli autori di modificare il contenuto.

* **Ambiente di produzione di pubblicazione**
Per distribuire il contenuto pubblicato.

Inoltre, gli ambienti possono variare, da un sistema a server singolo eseguito con AEM e un server applicazioni, a un set altamente scalabile di istanze cluster multi-server e multi-CPU. Adobe consiglia di utilizzare un computer separato per ogni sistema di produzione e di non eseguire altre applicazioni su tali computer.

## Considerazioni generiche sul dimensionamento dell’hardware {#generic-hardware-sizing-considerations}

Le sezioni seguenti forniscono indicazioni su come calcolare i requisiti hardware, tenendo conto di varie considerazioni. Per i sistemi di grandi dimensioni, Adobe consiglia di eseguire un semplice set di test di benchmark interni su una configurazione di riferimento.

L’ottimizzazione delle prestazioni è un’attività fondamentale che deve essere eseguita prima di poter eseguire eventuali benchmark per un progetto specifico. Prima di eseguire test di benchmark e di utilizzare i risultati per i calcoli di dimensionamento hardware, assicurati di applicare i suggerimenti forniti nella [documentazione sull’ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).

I requisiti di dimensionamento dell’hardware per i casi d’uso avanzati devono essere basati su una valutazione dettagliata delle prestazioni del progetto. Le caratteristiche dei casi d’uso avanzati che richiedono risorse hardware eccezionali includono:

* payload/throughput di contenuti elevati
* utilizzo esteso di codice personalizzato, flussi di lavoro personalizzati o librerie software di terze parti
* integrazione con sistemi esterni non supportati

## Spazio su disco/Disco rigido {#disk-space-hard-drive}

Lo spazio su disco necessario dipende in larga misura dal volume e dal tipo di applicazione web. I calcoli devono tenere conto dei seguenti elementi:

* la quantità e le dimensioni di pagine, risorse e altre entità memorizzate nell’archivio, ad esempio flussi di lavoro, profili e così via.
* la frequenza stimata delle modifiche ai contenuti e quindi la creazione di versioni dei contenuti
* il volume delle rappresentazioni delle risorse DAM che verranno generate
* la crescita complessiva dei contenuti nel tempo

Lo spazio su disco viene costantemente monitorato durante la pulizia delle revisioni online e offline. Se lo spazio su disco disponibile scende al di sotto di un valore critico, il processo viene annullato. Il valore critico è pari al 25% dell’attuale spazio su disco dell’archivio e non è configurabile. Adobe consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione dell’archivio, inclusa la crescita stimata.

### Virtualizzazione {#virtualization}

AEM funziona bene in ambienti virtualizzati, ma ci possono essere fattori come CPU o I/O che non possono essere direttamente equiparati all’hardware fisico. Si consiglia di scegliere una velocità di I/O più elevata (in generale), in quanto si tratta solitamente di un fattore critico. Per comprendere con precisione quali risorse sono necessarie, è necessario eseguire un benchmarking dell’ambiente.

### Parallelizzazione delle istanze di AEM {#parallelization-of-aem-instances}

**Sicurezza non riuscita**

Un sito Web a prova di errore viene distribuito su almeno due sistemi separati. In caso di guasto di un sistema, un altro sistema può sostituirlo e quindi compensare il guasto.

**Scalabilità risorse di sistema**

Mentre tutti i sistemi sono in esecuzione, è disponibile un aumento delle prestazioni di elaborazione. Tali prestazioni aggiuntive non sono necessariamente lineari con il numero di nodi cluster, in quanto la relazione dipende in larga misura dall’ambiente tecnico. Per ulteriori informazioni, consulta la [documentazione cluster](/help/sites-deploying/recommended-deploys.md).

La stima del numero di nodi cluster necessari si basa sui requisiti di base e sui casi d’uso specifici del particolare progetto web:

* Dal punto di vista della sicurezza in caso di guasto, è necessario determinare, per tutti gli ambienti, il livello di criticità del guasto e il tempo di compensazione dello stesso in base al tempo necessario per il ripristino di un nodo cluster.
* Per l’aspetto della scalabilità, il numero di operazioni di scrittura è fondamentalmente il fattore più importante. È possibile stabilire il bilanciamento del carico per le operazioni che accedono al sistema solo per elaborare operazioni di lettura. Per ulteriori informazioni, consulta [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it).

### Consigli hardware {#hardware-recommendations}

In genere, per l’ambiente di authoring è possibile utilizzare lo stesso hardware consigliato per l’ambiente di pubblicazione. In genere, il traffico del sito web è inferiore nei sistemi di authoring, ma anche l’efficienza della cache è inferiore. Tuttavia, il fattore fondamentale in questo caso è il numero di autori che lavorano in parallelo, insieme al tipo di azioni che vengono effettuate nel sistema. In generale, il clustering di AEM (dell’ambiente di authoring) è più efficace per ridimensionare le operazioni di lettura; in altre parole, un cluster di AEM viene ridimensionato in modo ottimale con gli autori che eseguono operazioni di modifica di base.

## Calcoli aggiuntivi specifici per il caso d’uso {#additional-use-case-specific-calculations}

Oltre al calcolo per un’applicazione web predefinita, tieni presente fattori specifici per i seguenti casi d’uso. I valori calcolati devono essere aggiunti al calcolo predefinito.

### Considerazioni specifiche per risorse {#assets-specific-considerations}

L’elaborazione intensiva di risorse digitali richiede risorse hardware ottimizzate, i fattori più rilevanti sono le dimensioni delle immagini e il picco di trasmissione delle immagini elaborate.

Alloca almeno 16 GB di memoria heap e configura il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] per utilizzare il [pacchetto Camera Raw](/help/assets/camera-raw.md) per l’acquisizione di immagini non elaborate.

>[!NOTE]
>
>Un throughput più elevato delle immagini significa che le risorse informatiche devono essere in grado di tenere il passo con l’I/O del sistema e viceversa. Ad esempio, se i flussi di lavoro vengono avviati mediante l’importazione di immagini, il caricamento di molte immagini tramite WebDAV potrebbe causare un backlog di flussi di lavoro.
>
>L’utilizzo di dischi separati per TarPM, archivio dati e indice di ricerca può aiutare a ottimizzare il comportamento di I/O del sistema (tuttavia, in genere ha senso mantenere l’ndice di ricerca in locale).

>[!NOTE]
>
>Consulta anche la [Guida alle prestazioni delle risorse](/help/sites-deploying/assets-performance-sizing.md).

### Gestione multi-sito {#multi-site-manager}

Il consumo di risorse quando si utilizza AEM MSM in un ambiente di authoring dipende in larga misura dai casi d’uso specifici. I fattori di base sono:

* Numero di copie live
* Periodicità dei rollout
* Dimensioni della struttura contenuto da distribuire
* Funzionalità connessa delle azioni di rollout

Testare il caso d’uso pianificato con un estratto di contenuto rappresentativo può aiutarti a comprendere meglio il consumo delle risorse. Se estrapoli i risultati con la velocità effettiva pianificata, puoi valutare le risorse aggiuntive necessarie per AEM MSM.

Inoltre, sono responsabili per gli autori che lavorano in parallelo. Percepiranno gli effetti collaterali delle prestazioni se i casi d’uso di AEM MSM consumano più risorse di quanto pianificato.

### Considerazioni sul dimensionamento di AEM Communities {#aem-communities-sizing-considerations}

I siti AEM che includono funzioni di AEM Communities (siti community) presentano un elevato livello di interazione da parte dei visitatori del sito (membri) nell’ambiente di pubblicazione.

Le considerazioni sul dimensionamento di un sito community dipendono dall’interazione prevista dai membri della community e dall’eventuale maggiore importanza di prestazioni ottimali per il contenuto della pagina.

I membri inviati tramite contenuto generato dall’utente (UGC) vengono archiviati separatamente dal contenuto della pagina. Anche se la piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall’ambiente di authoring a quello di pubblicazione, AEM Communities utilizza un singolo archivio comune per il contenuto generato dall’utente che non viene mai replicato.

Per l’archivio UGC, è necessario scegliere un provider di risorse di archiviazione (SRP) che influisca sulla distribuzione scelta.
Consulta

* [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md)
* [Topologie consigliate per le community](/help/communities/topologies.md)
