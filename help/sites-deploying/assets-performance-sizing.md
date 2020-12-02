---
title: Guida alle prestazioni di Risorse
seo-title: Guida alle prestazioni di Risorse
description: Scoprite come determinare il ridimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management (DAM) e come risolvere i problemi di prestazioni
seo-description: Scoprite come determinare il ridimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management (DAM) e come risolvere i problemi di prestazioni
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---


# Guida alle prestazioni delle risorse{#assets-performance-guide}

La gestione delle risorse digitali è spesso utilizzata nei casi in cui le prestazioni contano; tuttavia, la tipica configurazione di DAM contiene una serie di componenti hardware e software che possono influire sulle prestazioni. Questo documento contiene le seguenti informazioni:

* Informazioni per gli amministratori di sistema sulla determinazione del ridimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management
* Informazioni per gli sviluppatori di software che cercano di risolvere i problemi relativi alle istanze DAM con problemi di prestazioni

## Problemi di prestazioni {#performance-issues}

Le scarse prestazioni nella gestione delle risorse digitali possono avere un impatto sull&#39;esperienza dell&#39;utente in tre modi: prestazioni interattive, elaborazione delle risorse e velocità di download. Per migliorare le prestazioni, è importante misurare correttamente le prestazioni osservate e stabilire metriche target.

**1. Ricerca e navigazione interattive** Gli utenti stanno cercando le risorse o sfogliando il Finder di DAM e lamentano tempi di risposta lenti o che i risultati della ricerca non vengono visualizzati immediatamente. Si tratta di un problema di prestazioni interattive.

Le prestazioni interattive sono misurate in termini di tempo di risposta della pagina. Questo è il tempo che trascorre dalla ricezione della richiesta HTTP alla chiusura della risposta HTTP, che può essere determinata dai file di registro della richiesta. Le prestazioni di destinazione tipiche sono tempi di risposta della pagina inferiori a due secondi.

**2. Elaborazione delle risorse** Un problema di elaborazione delle risorse è rappresentato dal momento in cui gli utenti caricano le risorse e restano in pochi minuti finché le risorse non vengono convertite e assimilate AEM DAM.

Le prestazioni di elaborazione delle risorse vengono misurate in termini di tempo medio di completamento del processo del flusso di lavoro. Questo è il tempo necessario per richiamare il processo del flusso di lavoro di aggiornamento delle risorse al suo completamento, che può essere determinato dall’interfaccia utente dei rapporti sul flusso di lavoro. Le prestazioni di destinazione tipiche dipendono dalle dimensioni e dal tipo di risorse elaborate e dal numero di rappresentazioni. Esempi di prestazioni target possono essere i seguenti:

* meno di dieci secondi per le immagini di dimensioni inferiori a 1280x1280 pixel con rappresentazioni standard
* inferiore a un minuto per le immagini di dimensioni inferiori a 100 MB che utilizzano rappresentazioni standard
* inferiore a cinque minuti per le clip video HD più brevi di un minuto

**3. Velocità di download** Un problema di throughput si verifica quando il download da AEM DAM richiede molto tempo e le miniature non vengono visualizzate immediatamente quando si sfoglia l&#39;amministratore DAM o il Finder DAM.

Le prestazioni della potenza vengono misurate in termini di velocità di download in kilobit al secondo. Le prestazioni target tipiche sono 300 kilobit al secondo per i download simultanei a 100.

**4. Fattori che influiscono sulle prestazioni di elaborazione delle risorse**

Per poter stimare l’hardware necessario per elaborare le risorse, è necessario tenere conto dei seguenti aspetti:

* La risoluzione delle immagini in pixel
* L&#39;heap assegnato al processo AEM

La quantità di pixel contenuti nell’immagine determina il tempo di elaborazione. Più pixel significa che l’elaborazione richiede più tempo.
Il tipo di immagine, la frequenza di compressione o la dimensione correlata del file in cui è memorizzata l&#39;immagine non influenza in modo significativo le prestazioni complessive.

L&#39;heap è stato identificato come il fattore limitante più importante. Ogni volta che la risorsa supera la memoria disponibile, le prestazioni di elaborazione diminuiscono rapidamente.

I processi DAM sono ben adatti per essere eseguiti in paralell per grandi quantità. Il caricamento delle risorse in un processore batch e multi-core velocizza il tempo assoluto trascorso per risorsa.

**5. Stima dei requisiti hardware per l&#39;esecuzione dell&#39;elaborazione delle risorse**

L&#39;ampia elaborazione delle risorse digitali richiede risorse hardware ottimizzate, i fattori più importanti sono la dimensione delle immagini e il volume di elaborazione delle immagini.

Assegnate almeno 16 GB di heap e configurate il flusso di lavoro [!UICONTROL DAM Update Asset] per utilizzare il [pacchetto Camera Raw](/help/assets/camera-raw.md) per l&#39;assimilazione di immagini non elaborate.

## Informazioni sul sistema {#understanding-the-system}

Una tipica configurazione DAM consiste nell’accedere a DAM da parte degli utenti finali tramite un sistema di bilanciamento del carico. L&#39;istanza DAM potrebbe far parte di un&#39;installazione cluster, in cui ogni istanza DAM viene eseguita in un processo Java Virtual Machine su una macchina fisica o su una macchina virtuale. Lo storage DAM è fornito da un disco RAID in caso di configurazione a macchina singola o da uno storage collegato in rete gestito in caso di configurazione cluster.

La legenda seguente descrive le possibili aree di limite delle prestazioni con alcune soluzioni, a seconda dei casi.

**Connessione di rete all&#39;** utente finaleUna connessione di rete lenta può causare problemi di throughput, in alcuni rari casi anche problemi di latenza. A volte l&#39;utente ha una connessione lenta dal provider di servizi Internet, soprattutto nelle Intranet. Questo è un segno di topologia di rete non corretta.

**File** system temporaneoUn file system locale lento può causare problemi di prestazioni interattivi, soprattutto quando si tratta di ricerca, perché gli indici di ricerca sono memorizzati sul disco locale. Inoltre, se si utilizza il processo della riga di comando, può causare problemi di elaborazione delle risorse.

**AEM DAM** FinderProblemi di prestazioni interattivi, spesso riscontrati nelle ricerche sono causati da un elevato utilizzo della CPU dovuto a molti utenti simultanei o altri processi che utilizzano la CPU nella stessa istanza. Passare dalle macchine virtuali alle macchine dedicate e assicurarsi che nessun altro servizio venga eseguito sulla macchina può aiutare a migliorare le prestazioni. Se l’elevato carico della CPU è dovuto all’elaborazione delle risorse e a molti utenti simultanei, Day consiglia di aggiungere altri nodi del cluster.

**AEM** Flusso di lavoro DAMI processi del flusso di lavoro con esecuzione prolungata durante l’assimilazione delle risorse causano problemi di prestazioni nell’elaborazione delle risorse. A seconda del tipo di risorse elaborate, questo può indicare un utilizzo eccessivo della CPU. Day consiglia di ridurre il numero di altri processi in esecuzione sul sistema e di aumentare il numero di CPU disponibili aggiungendo i nodi del cluster.

**NAS** ConnectivityLa scarsa connettività di rete al NAS causa problemi di prestazioni interattive, perché l&#39;accesso ai nuovi nodi durante l&#39;elaborazione delle risorse è rallentato a causa della latenza della rete. Inoltre, la lentezza del throughput di rete influisce negativamente sul throughput, ma anche sulle prestazioni di elaborazione delle risorse, poiché il caricamento e il salvataggio delle rappresentazioni sono rallentati.

I motivi per una latenza e un throughput errati in un NAS sono in genere topologia di rete o sovrautilizzo del NAS da parte di altri servizi.

**Network Attached** StorageI sistemi di storage collegati alla rete utilizzati in eccesso possono causare una serie di problemi:

* Lo spazio su disco insufficiente è un problema che si verifica di frequente e che può essere impedito mediante il ridimensionamento corretto di un progetto DAM.
* La latenza elevata del disco si propaga in tempi di accesso lenti per i CRX e può causare problemi di prestazioni interattive.
* Un basso throughput del disco potrebbe causare prestazioni ridotte per CQ5 DAM.

## Verifica delle prestazioni {#testing-for-performance}

Per ogni progetto DAM, accertatevi di stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. A tal fine, prendere in considerazione i seguenti punti di controllo:

1. Test delle prestazioni end-to-end con JMeter - Simulare una sessione di ricerca e ricerca di esempio per rilevare problemi di prestazioni interattive.
1. Test di throughput e latency con JMeter - L&#39;esecuzione su un computer client assicura che non ci siano problemi relativi alla topologia.
1. Test standardizzati per l’elaborazione delle risorse: per acquisire un numero limitato di risorse di esempio e misurare il tempo. Deve includere l&#39;integrazione con flussi di lavoro esterni.
1. Monitorare l&#39;utilizzo di CPU, disco e memoria di ciascun nodo del cluster.
1. Diagnostica delle prestazioni in lettura/scrittura CRX per identificare problemi relativi alla non elaborazione.
1. Monitorare la latenza e il throughput della rete dal cluster DAM al NAS.
1. Verificare le prestazioni di lettura e scrittura e la latenza del disco direttamente sul NAS, se possibile.

## Tweaking Bottiglia {#tweaking-bottlenecks}

Finora nei progetti sono state utilizzate le seguenti modifiche delle prestazioni:

* Generazione di rappresentazioni selettive: genera solo le rappresentazioni necessarie aggiungendo condizioni al flusso di lavoro di elaborazione delle risorse, in modo che vengano generate rappresentazioni più costose solo per determinate risorse.
* Memorizzazione dei dati condivisi tra le istanze: quando si utilizza poco spazio su disco, questo può ridurre notevolmente la quantità di spazio su disco necessaria a costi maggiori per la configurazione e perdere la pulizia automatica del datastore.

## Lettura successiva {#further-reading}

* [Analisi dei processi lenti e bloccati](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

