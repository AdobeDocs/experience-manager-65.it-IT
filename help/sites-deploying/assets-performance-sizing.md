---
title: Guida alle prestazioni di Assets
description: Scopri come determinare il dimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management (DAM) e come risolvere i problemi di prestazioni
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---

# Guida alle prestazioni di Assets{#assets-performance-guide}

Il Digital Asset Management (DAM) viene spesso utilizzato nei casi in cui le prestazioni sono importanti. Tuttavia, la tipica configurazione DAM contiene diversi componenti hardware e software che possono influire sulle prestazioni. Questo documento fornisce quanto segue:

* Informazioni per gli amministratori di sistema sulla determinazione del dimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management
* Informazioni per gli sviluppatori di software che desiderano risolvere i problemi relativi alle istanze DAM con problemi di prestazioni

## Problemi relativi alle prestazioni {#performance-issues}

Le scarse prestazioni nella gestione delle risorse digitali possono influire sull’esperienza utente in tre modi: prestazioni interattive, elaborazione delle risorse e velocità di download. Per migliorare le prestazioni, è importante misurare correttamente le prestazioni osservate e stabilire metriche target.

**1. Ricerca interattiva e navigazione** Gli utenti cercano le risorse o navigano nel Finder di DAM e si lamentano dei tempi di risposta lenti o del fatto che i risultati della ricerca non vengono visualizzati immediatamente. Si tratta di un problema di prestazioni interattivo.

Le prestazioni interattive sono misurate in termini di tempo di risposta della pagina. Questo è il tempo che trascorre tra la ricezione della richiesta HTTP e la chiusura della risposta HTTP, che può essere determinato dai file di registro delle richieste. Le prestazioni tipiche del target sono un tempo di risposta della pagina inferiore a due secondi.

**2. Elaborazione risorse** Un problema di elaborazione delle risorse si verifica quando gli utenti caricano le risorse e occorrono alcuni minuti prima che le risorse vengano prontamente convertite e acquisite in DAM Adobe Experience Manager (AEM).

Le prestazioni di elaborazione delle risorse vengono misurate in termini di tempo medio di completamento del processo del flusso di lavoro. Si tratta del tempo che trascorre tra il richiamo del processo del flusso di lavoro di aggiornamento delle risorse e il suo completamento, che può essere determinato dall’interfaccia utente dei rapporti del flusso di lavoro. Le prestazioni tipiche del target dipendono dalle dimensioni e dal tipo di risorse elaborate e dal numero di rappresentazioni. Di seguito sono riportati alcuni esempi di prestazioni del target:

* inferiore a dieci secondi per immagini di dimensioni inferiori a 1280x1280 pixel con rappresentazioni standard
* inferiore a un minuto per le immagini di dimensioni inferiori a 100 MB che utilizzano rappresentazioni standard
* inferiore a cinque minuti per video clip HD di durata inferiore a un minuto

**3. Velocità di download** Un problema di velocità effettiva si verifica quando il download da AEM DAM richiede molto tempo e le miniature non vengono visualizzate immediatamente durante la navigazione in DAM Admin o in DAM Finder.

Le prestazioni di throughput sono misurate in termini di velocità di download in kilobit al secondo. Le prestazioni tipiche del target sono di 300 Kbps per 100 download simultanei.

**4. Fattori che influiscono sulle prestazioni di elaborazione delle risorse**

Per poter stimare l&#39;hardware necessario per l&#39;elaborazione delle risorse, è necessario tenere conto dei seguenti aspetti:

* Risoluzione delle immagini in pixel
* L’heap assegnato al processo AEM

Il numero di pixel contenuti nell&#39;immagine determina il tempo di elaborazione, mentre il numero di pixel indica che l&#39;elaborazione richiede più tempo.
Il tipo di immagine, il tasso di compressione o le relative dimensioni del file in cui è memorizzata l&#39;immagine non influiscono in modo significativo sulle prestazioni complessive.

L’heap è stato identificato come il fattore limitante più importante. Ogni volta che la risorsa supera la memoria disponibile, le prestazioni di elaborazione si riducono rapidamente.

I processi DAM sono molto adatti per essere eseguiti in parallelo per grandi quantità. Il caricamento delle risorse in un batch e in processori multi-core accelera il tempo assoluto dedicato a ogni risorsa.

**5. Stima dei requisiti hardware per l&#39;elaborazione delle risorse**

L’elaborazione intensiva di risorse digitali richiede risorse hardware ottimizzate, i fattori più rilevanti sono le dimensioni delle immagini e il picco di trasmissione delle immagini elaborate.

Assegna almeno 16 GB di heap e configura l&#39;elemento [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro per utilizzare [pacchetto Camera Raw](/help/assets/camera-raw.md) per l’acquisizione di immagini non elaborate.

## Informazioni sul sistema {#understanding-the-system}

Una tipica configurazione DAM è costituita da utenti finali che accedono a DAM tramite un load balancer. L&#39;istanza DAM potrebbe far parte di un&#39;installazione cluster, in cui ogni istanza DAM viene eseguita in un processo di macchina virtuale Java™ su una macchina fisica o virtuale. Lo storage DAM viene fornito da un disco RAID se sono presenti impostazioni per un solo computer oppure da uno storage gestito collegato alla rete se sono presenti configurazioni cluster.

La legenda seguente descrive le possibili aree di insidia delle prestazioni con alcune soluzioni, a seconda delle necessità.

**Connessione di rete all&#39;utente finale** Una connessione di rete lenta può causare problemi di velocità effettiva e, in alcuni rari casi, anche problemi di latenza. A volte l’utente ha una connessione lenta dall’ISP, soprattutto nelle intranet. Segno di topologia di rete non corretta.

**File system temporaneo** Un file system locale lento può causare problemi di prestazioni interattive, soprattutto durante la ricerca, perché gli indici di ricerca sono memorizzati sul disco locale. Può inoltre causare problemi di elaborazione delle risorse se si utilizza il processo della riga di comando.

**Ricerca DAM AEM** I problemi di prestazioni interattive, spesso riscontrati nelle ricerche, sono causati da un elevato utilizzo della CPU dovuto a molti utenti simultanei o ad altri processi che utilizzano la CPU nella stessa istanza. Passare da macchine virtuali a macchine dedicate e assicurarsi che non vengano eseguiti altri servizi sulla macchina può contribuire a migliorare le prestazioni. Se a causa dell’elaborazione delle risorse e di molti utenti simultanei si verifica un carico elevato della CPU, Day consiglia di aggiungere ulteriori nodi cluster.

**Flusso di lavoro DAM AEM** I processi di flusso di lavoro a esecuzione prolungata durante l’inserimento delle risorse causano problemi di prestazioni nell’elaborazione delle risorse. A seconda del tipo di risorse da elaborare, questo può indicare un sovrautilizzo della CPU. Day consiglia di ridurre il numero di altri processi in esecuzione sul sistema e di aumentare il numero di CPU disponibili aggiungendo nodi cluster.

**Connettività NAS** La scarsa connettività di rete al NAS causa problemi di prestazioni interattive, perché l’accesso ai nuovi nodi durante l’elaborazione delle risorse è rallentato a causa della latenza della rete. Inoltre, una velocità effettiva di rete lenta influisce negativamente sulla velocità effettiva, ma anche sulle prestazioni di elaborazione delle risorse, perché il caricamento e il salvataggio delle rappresentazioni sono rallentati.

I motivi di latenza e throughput non validi in un NAS sono la topologia di rete o l&#39;utilizzo eccessivo del NAS da parte di altri servizi.

**Network Attached Storage** I sistemi di storage NAS sovrautilizzati possono causare una serie di problemi:

* Lo spazio su disco insufficiente è un problema che si verifica di frequente e che può essere evitato ridimensionando correttamente un progetto DAM.
* L&#39;elevata latenza del disco si propaga in tempi di accesso lenti per CRX e può causare problemi di prestazioni interattive.
* La bassa velocità di trasmissione del disco può comportare prestazioni ridotte per DAM CQ5.

## Test delle prestazioni {#testing-for-performance}

Per ogni progetto DAM, assicurati di stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. A tale scopo, considera i seguenti punti di controllo:

1. Test delle prestazioni end-to-end con JMeter: simula un esempio di sessione di ricerca e navigazione per rilevare problemi di prestazioni interattive.
1. Test della velocità effettiva e della latenza con JMeter: l&#39;esecuzione su un computer client assicura che non vi siano problemi relativi alla topologia.
1. Test di elaborazione delle risorse standardizzati: acquisisci alcune risorse di esempio e misura il tempo. Ciò dovrebbe includere l’integrazione del flusso di lavoro esterno.
1. Monitorare l&#39;utilizzo della CPU, del disco e della memoria di ciascun nodo del cluster.
1. Diagnostica delle prestazioni di lettura/scrittura di CRX per identificare i problemi correlati all&#39;elaborazione.
1. Monitorare la latenza e la velocità effettiva di rete dal cluster DAM al NAS.
1. Prestazioni di test, lettura e scrittura e latenza del disco direttamente sul NAS, se possibile.

## Modifica dei colli di bottiglia {#tweaking-bottlenecks}

Finora nei progetti sono state utilizzate le seguenti modifiche delle prestazioni:

* Generazione di rendering selettivo: genera solo le rappresentazioni necessarie aggiungendo condizioni al flusso di lavoro di elaborazione delle risorse, in modo che vengano generate rappresentazioni più costose solo per le risorse selezionate.
* Archivio dati condiviso tra istanze: quando lo spazio su disco è insufficiente, questo può ridurre notevolmente la quantità di spazio su disco necessario, a scapito di sforzi di configurazione più elevati e perdendo la pulizia automatica dell’archivio dati.

## Ulteriori informazioni {#further-reading}

* [Analisi dei processi lenti e bloccati](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
