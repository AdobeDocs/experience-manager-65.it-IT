---
title: Guida alle prestazioni di Assets
seo-title: Assets Performance Guide
description: Scopri come determinare il dimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management (DAM) e come risolvere i problemi di prestazioni
seo-description: Learn how to determine the optimal hardware sizing for a new Digital Asset Management (DAM) setup and how to troubleshoot performance issues
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---

# Guida alle prestazioni di Assets{#assets-performance-guide}

La gestione delle risorse digitali è spesso utilizzata nei casi in cui le prestazioni contano; tuttavia, la tipica configurazione DAM contiene una serie di componenti hardware e software che possono influire sulle prestazioni. Questo documento fornisce quanto segue:

* Informazioni per gli amministratori di sistema su come determinare il dimensionamento hardware ottimale per una nuova configurazione di Digital Asset Management
* Informazioni per gli sviluppatori di software che desiderano risolvere i problemi relativi alle istanze DAM con problemi di prestazioni

## Problemi di prestazioni {#performance-issues}

Le scarse prestazioni nella gestione delle risorse digitali possono influenzare l’esperienza utente in tre modi: prestazioni interattive, elaborazione delle risorse e velocità di download. Per migliorare le prestazioni, è importante misurare correttamente le prestazioni osservate e stabilire le metriche target.

**1. Ricerca e navigazione interattive** Gli utenti cercano le risorse o navigano nel DAM Finder e si lamentano dei tempi di risposta lenti o che i risultati della ricerca non vengono visualizzati immediatamente. Questo è un problema di prestazioni interattive.

Le prestazioni interattive vengono misurate in termini di tempo di risposta della pagina. Questo è il tempo necessario dalla ricezione della richiesta HTTP alla chiusura della risposta HTTP, che può essere determinata dai file di log della richiesta. Le prestazioni di destinazione tipiche sono un tempo di risposta della pagina inferiore a due secondi.

**2. Elaborazione delle risorse** Un problema di elaborazione delle risorse si verifica quando gli utenti caricano le risorse e ci vogliono minuti finché le risorse non vengono rapidamente convertite e acquisite in AEM DAM.

Le prestazioni di elaborazione delle risorse vengono misurate in termini di tempo medio di completamento del processo del flusso di lavoro. Questo è il tempo necessario per richiamare il processo del flusso di lavoro di aggiornamento delle risorse al suo completamento, che può essere determinato dall’interfaccia utente dei rapporti del flusso di lavoro. Le prestazioni di destinazione tipiche dipendono dalle dimensioni e dal tipo di risorse elaborate e dal numero di rappresentazioni. Esempi di prestazioni target possono essere i seguenti:

* meno di dieci secondi per immagini di dimensioni inferiori a 1280x1280 pixel utilizzando rappresentazioni standard
* inferiore a un minuto per immagini di dimensioni inferiori a 100 MB che utilizzano rappresentazioni standard
* inferiore a cinque minuti per clip video HD di meno di un minuto

**3. Velocità di download** Un problema di throughput si verifica quando il download da AEM DAM richiede molto tempo e le miniature non vengono visualizzate immediatamente quando si naviga nell’amministratore DAM o nel Finder DAM.

Le prestazioni della velocità effettiva sono misurate in termini di velocità di download in kilobit al secondo. Le prestazioni target tipiche sono 300 kilobit al secondo per 100 download simultanei.

**4. Fattori che influenzano le prestazioni di elaborazione delle risorse**

Per poter stimare l’hardware necessario per elaborare le risorse, è necessario tenere conto dei seguenti aspetti:

* La risoluzione delle immagini in quantità di pixel
* heap assegnato al processo AEM

La quantità di pixel contenuti nell&#39;immagine determina il tempo di elaborazione. Più pixel significa che l&#39;elaborazione richiede un tempo più lungo.
Il tipo di immagine, il tasso di compressione o le dimensioni correlate del file in cui viene memorizzata l&#39;immagine non influenzano in modo significativo le prestazioni complessive.

L&#39;heap è stato identificato come il fattore limitante più importante. Ogni volta che la risorsa supera la memoria disponibile, le prestazioni di elaborazione diminuiscono rapidamente.

I processi DAM sono ben adatti per essere eseguiti in parallelo per grandi quantità. Il caricamento delle risorse in un processore batch e multi-core velocizza il tempo assoluto trascorso per risorsa.

**5. Stima dei requisiti hardware per l’esecuzione dell’elaborazione delle risorse**

L&#39;elaborazione estensiva delle risorse digitali richiede risorse hardware ottimizzate, i fattori più importanti sono le dimensioni delle immagini e il throughput di picco delle immagini elaborate.

Alloca almeno 16 GB di heap e configura il [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro per utilizzare [pacchetto Camera Raw](/help/assets/camera-raw.md) per l’acquisizione di immagini crude.

## Informazioni sul sistema {#understanding-the-system}

Una tipica configurazione DAM consiste nell’accedere a DAM tramite un load balancer. L&#39;istanza DAM potrebbe far parte di una configurazione cluster, in cui ogni istanza DAM viene eseguita in un processo Java Virtual Machine su una macchina fisica o una macchina virtuale. Lo storage DAM è fornito da un disco RAID in caso di configurazione di un singolo computer o da un sistema di storage collegato di rete gestito in caso di configurazione di cluster.

La legenda seguente descrive le possibili aree di insidia delle prestazioni con alcune soluzioni, a seconda dei casi.

**Connessione di rete all&#39;utente finale** Una connessione di rete lenta può causare problemi di velocità effettiva, in alcuni rari casi anche problemi di latenza. A volte l&#39;utente ha una connessione lenta da parte dell&#39;ISP, soprattutto nelle intranets. Questo è un segno di topologia di rete non corretta.

**File system temporaneo** Un file system locale lento può causare problemi di prestazioni interattive, soprattutto quando si tratta di ricerca, perché gli indici di ricerca sono memorizzati sul disco locale. Inoltre, se si utilizza il processo della riga di comando, può causare problemi di elaborazione delle risorse.

**AEM DAM Finder** Problemi di prestazioni interattive, spesso riscontrati nelle ricerche, sono causati da un elevato utilizzo della CPU dovuto a molti utenti simultanei o ad altri processi che consumano CPU nella stessa istanza. Il passaggio dalle macchine virtuali alle macchine dedicate e l&#39;assicurazione che nessun altro servizio eseguito sulla macchina possa aiutare a migliorare le prestazioni. Se l’elevato carico della CPU è causato dall’elaborazione delle risorse e da molti utenti simultanei, Day consiglia di aggiungere altri nodi cluster.

**Flusso di lavoro AEM DAM** I processi del flusso di lavoro a lungo termine durante l’inserimento delle risorse causano problemi di prestazioni nell’elaborazione delle risorse. A seconda del tipo di risorse da elaborare, questo può indicare un eccessivo utilizzo della CPU. Day consiglia di ridurre il numero di altri processi in esecuzione sul sistema e di aumentare il numero di CPU disponibili aggiungendo nodi cluster.

**Connettività NAS** Una scarsa connettività di rete al NAS causa problemi di prestazioni interattive, perché l’accesso ai nuovi nodi durante l’elaborazione delle risorse è rallentato a causa della latenza di rete. Inoltre, la velocità di trasmissione lenta della rete influisce negativamente sul throughput, ma anche sulle prestazioni di elaborazione delle risorse, poiché il caricamento e il salvataggio dei rendering sono rallentati.

I motivi per una latenza e un throughput errati in un NAS sono solitamente topologia di rete o sovrautilizzo del NAS da parte di altri servizi.

**Storage collegato alla rete** I sistemi di storage collegati alla rete utilizzati in modo eccessivo possono causare una serie di problemi:

* Lo spazio su disco insufficiente è un problema che si verifica di frequente e che può essere impedito tramite il dimensionamento corretto di un progetto DAM.
* La latenza elevata del disco si propaga in tempi di accesso lenti per CRX e può causare problemi di prestazioni interattive.
* Una bassa velocità del disco può causare prestazioni basse per CQ5 DAM.

## Test delle prestazioni {#testing-for-performance}

Per ogni progetto DAM, assicurati di stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. A questo scopo, considera i seguenti punti di controllo:

1. Test delle prestazioni end-to-end tramite JMeter - Simula una sessione di ricerca e navigazione di esempio per rilevare problemi di prestazioni interattive.
1. I test di Throughput e latenza con JMeter - L&#39;esecuzione su un computer client assicura che non ci siano problemi relativi alla topologia.
1. Test di elaborazione delle risorse standardizzati: consente di acquisire un numero limitato di risorse di esempio e di misurare il tempo. Questo dovrebbe includere l’integrazione con flussi di lavoro esterni.
1. Monitora l&#39;utilizzo della CPU, del disco e della memoria di ogni nodo del cluster.
1. Diagnostica delle prestazioni di lettura/scrittura CRX per identificare i problemi relativi alla non elaborazione.
1. Monitorare la latenza e il throughput di rete dal cluster DAM al NAS.
1. Verificare le prestazioni di lettura e scrittura e la latenza del disco direttamente sul NAS, se possibile.

## Colori di bottiglia {#tweaking-bottlenecks}

Finora nei progetti sono state utilizzate le seguenti modifiche delle prestazioni:

* Generazione selettiva dei rendering: genera solo i rendering necessari aggiungendo condizioni al flusso di lavoro di elaborazione delle risorse, in modo che i rendering più costosi vengano generati solo per le risorse selezionate.
* Archiviazione dati condivisi tra le istanze: quando lo spazio su disco è insufficiente, questo può ridurre notevolmente la quantità di spazio su disco necessaria a costi maggiori sforzi di configurazione e perdere la pulizia automatica del datastore.

## Ulteriori informazioni {#further-reading}

* [Analisi dei processi lenti e bloccati](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
