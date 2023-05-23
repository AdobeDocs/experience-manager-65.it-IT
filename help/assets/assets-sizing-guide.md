---
title: "[!DNL Assets] guida al dimensionamento"
description: Best practice per determinare metriche efficienti per stimare l’infrastruttura e le risorse necessarie per l’implementazione [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Management
exl-id: fd58ead9-5e18-4f55-8d20-1cf4402fad97
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# [!DNL Assets] guida al dimensionamento {#assets-sizing-guide}

Quando si ridimensiona l’ambiente per un [!DNL Adobe Experience Manager Assets] è importante garantire che siano disponibili risorse sufficienti in termini di disco, CPU, memoria, I/O e velocità effettiva di rete. Il dimensionamento di molte di queste risorse richiede la comprensione del numero di risorse caricate nel sistema. Se non è disponibile una metrica migliore, puoi dividere la dimensione della libreria esistente per la durata della libreria, per trovare la velocità di creazione delle risorse.

## Disco {#disk}

### Archivio dati {#datastore}

Errore comune durante il dimensionamento dello spazio su disco richiesto per un [!DNL Assets] L’implementazione consiste nel basare i calcoli sulle dimensioni delle immagini non elaborate da acquisire nel sistema. Per impostazione predefinita, [!DNL Experience Manager] crea tre rappresentazioni oltre all’immagine originale da utilizzare per il rendering del [!DNL Experience Manager] elementi dell’interfaccia utente. Nelle implementazioni precedenti, si è osservato che queste rappresentazioni presumevano dimensioni doppie rispetto alle risorse acquisite.

La maggior parte degli utenti definisce le rappresentazioni personalizzate oltre a quelle predefinite. Oltre alle rappresentazioni, [!DNL Assets] consente di estrarre risorse secondarie da tipi di file comuni, ad esempio [!DNL Adobe InDesign] e [!DNL Adobe Illustrator].

Infine, le funzionalità di controllo delle versioni di [!DNL Experience Manager] archivia i duplicati delle risorse nella cronologia delle versioni. Puoi configurare le versioni da eliminare spesso. Tuttavia, molti utenti scelgono di conservare le versioni nel sistema per un periodo di tempo prolungato, che richiede ulteriore spazio di archiviazione.

Tenendo conto di questi fattori, è necessario utilizzare una metodologia per calcolare uno spazio di archiviazione sufficientemente accurato per l&#39;archiviazione delle risorse utente.

1. Determina la dimensione e il numero di risorse che verranno caricate nel sistema.
1. Ottieni un esempio rappresentativo delle risorse da caricare in [!DNL Experience Manager]. Ad esempio, se si prevede di caricare nel sistema file PSD, JPG, AI e PDF, è necessario disporre di più immagini di esempio per ciascun formato di file. Inoltre, questi campioni devono essere rappresentativi delle diverse dimensioni e complessità delle immagini.
1. Definisci le rappresentazioni da utilizzare.
1. Creare le rappresentazioni in [!DNL Experience Manager] utilizzo [!DNL ImageMagick] o [!DNL Adobe Creative Cloud] applicazioni. Oltre alle rappresentazioni specificate dagli utenti, crea rappresentazioni pronte all’uso. Per gli utenti che implementano Dynamic Media, puoi utilizzare il binario IC per generare le rappresentazioni PTIFF da memorizzare in Experience Manager.
1. Se prevedi di utilizzare risorse secondarie, generale per i tipi di file appropriati.
1. Confronta le dimensioni delle immagini di output, delle rappresentazioni e delle risorse secondarie con le immagini originali. Consente di generare un fattore di crescita previsto al caricamento del sistema. Ad esempio, se generi copie trasformate e risorse secondarie con una dimensione combinata di 3 GB dopo l’elaborazione di 1 GB di risorse, il fattore di crescita della copia trasformata è 3.
1. Determina il tempo massimo per il quale le versioni delle risorse devono essere mantenute nel sistema.
1. Determinare la frequenza con cui le risorse esistenti vengono modificate nel sistema. Se [!DNL Experience Manager] viene utilizzato come hub di collaborazione nei flussi di lavoro creativi; la quantità di modifiche è elevata. Se nel sistema vengono caricate solo le risorse finite, questo numero è molto inferiore.
1. Determina quante risorse vengono caricate nel sistema ogni mese. In caso di dubbi, verifica il numero di risorse attualmente disponibili e, per calcolare un numero approssimativo, lo divide per l’età della risorsa più vecchia.

L’esecuzione dei passaggi precedenti consente di determinare quanto segue:

* Dimensione non elaborata delle risorse da caricare.
* Numero di risorse da caricare.
* Fattore di crescita della rappresentazione.
* Numero di modifiche apportate alle risorse al mese.
* Numero di mesi per la gestione delle versioni delle risorse.
* Numero di nuove risorse caricate ogni mese.
* Anni di crescita per l&#39;allocazione dello spazio di storage.

È possibile specificare questi numeri nel foglio di calcolo Ridimensionamento rete per determinare lo spazio totale necessario per l&#39;archivio dati. È anche uno strumento utile per determinare l’impatto della gestione delle versioni delle risorse o della modifica delle risorse in [!DNL Experience Manager] sulla crescita del disco.

I dati di esempio inseriti nello strumento mostrano quanto sia importante eseguire i passaggi indicati. Se imposti l’archivio dati esclusivamente in base alle immagini non elaborate caricate (1 TB), potresti aver sottovalutato la dimensione dell’archivio di un fattore di 15.

[Ottieni file](assets/disk_sizing_tool.xlsx)

### Archivi dati condivisi {#shared-datastores}

Per i datastore di grandi dimensioni, puoi implementare un datastore condiviso sia tramite un datastore di file condiviso su un’unità collegata in rete sia tramite un datastore Amazon S3. In questo caso, non è necessario che le singole istanze conservino una copia dei binari. Inoltre, un datastore condiviso facilita la replica senza binari e contribuisce a ridurre la larghezza di banda utilizzata per replicare le risorse negli ambienti di pubblicazione.

#### Casi d’uso {#use-cases}

L’archivio dati può essere condiviso tra un’istanza di authoring primaria e in standby per ridurre al minimo il tempo necessario per aggiornare l’istanza in standby con le modifiche apportate nell’istanza principale. Puoi anche condividere l’archivio dati tra le istanze di authoring e pubblicazione per ridurre al minimo il traffico durante la replica.

#### Svantaggi {#drawbacks}

A causa di alcune insidie, la condivisione di un archivio dati non è consigliata in tutti i casi.

#### Singolo punto di errore {#single-point-of-failure}

L&#39;utilizzo di un datastore condiviso introduce un singolo punto di errore in un&#39;infrastruttura. Considera uno scenario in cui il sistema ha un’istanza Author e due istanze Publish, ciascuna con il proprio archivio dati. Se uno di questi si blocca, gli altri due possono continuare a correre. Tuttavia, se l’archivio dati è condiviso, un singolo guasto del disco può causare il guasto dell’intera infrastruttura. Assicurati quindi di mantenere un backup dell’archivio dati condiviso da cui puoi ripristinarlo rapidamente.

È preferibile implementare il servizio AWS S3 per gli archivi dati condivisi, in quanto riduce in modo significativo la probabilità di errore rispetto alle normali architetture disco.

#### Maggiore complessità {#increased-complexity}

Gli archivi dati condivisi aumentano inoltre la complessità delle operazioni, ad esempio la raccolta di oggetti inattivi. Normalmente, la raccolta di oggetti inattivi per un datastore indipendente può essere avviata con un solo clic. Tuttavia, gli archivi dati condivisi richiedono operazioni di spostamento dei contrassegni per ogni membro che utilizza l&#39;archivio dati, oltre all&#39;esecuzione della raccolta effettiva su un singolo nodo.

Per le operazioni AWS, l&#39;implementazione di un&#39;unica posizione centrale (tramite Amazon S3), anziché la creazione di un array RAID di volumi EBS, può compensare in modo significativo la complessità e i rischi operativi del sistema.

#### Problemi di prestazioni {#performance-concerns}

Un datastore condiviso richiede che i file binari siano archiviati in un&#39;unità di rete condivisa tra tutte le istanze. L&#39;accesso a questi file binari in rete influisce negativamente sulle prestazioni del sistema. È possibile mitigare parzialmente l&#39;impatto utilizzando una connessione di rete veloce a un array veloce di dischi. Tuttavia, si tratta di una proposta costosa. Nel caso delle operazioni AWS, tutti i dischi sono remoti e richiedono la connettività di rete. I volumi temporanei perdono i dati quando l&#39;istanza viene avviata o arrestata.

#### Latenza {#latency}

La latenza nelle implementazioni S3 è introdotta dai thread di scrittura in background. Le procedure di backup devono tenere conto di questa latenza. Inoltre, gli indici Lucene possono rimanere incompleti durante la creazione di un backup. Si applica a qualsiasi file sensibile al tempo scritto nell’archivio dati S3 e a cui si accede da un’altra istanza.

### Archivio nodi o archivio documenti {#node-store-document-store}

È difficile ottenere cifre di dimensionamento precise per un NodeStore o DocumentStore a causa delle risorse utilizzate da:

* Metadati risorsa
* Versioni risorsa
* Registri di audit
* Flussi di lavoro attivi e archiviati

Poiché i file binari vengono archiviati nell&#39;archivio dati, ogni file binario occupa spazio. La maggior parte degli archivi ha dimensioni inferiori a 100 GB. Tuttavia, potrebbero essere presenti archivi di dimensioni fino a 1 TB. Inoltre, per eseguire la compattazione offline, è necessario spazio libero sufficiente sul volume per riscrivere l&#39;archivio compattato insieme alla versione precompattata. Una buona regola consiste nel ridimensionare il disco a 1,5 volte le dimensioni previste per l’archivio.

Per l&#39;archivio, utilizzare unità SSD o dischi con un livello IOPS superiore a 3000. Per eliminare la possibilità che IOPS introduca colli di bottiglia delle prestazioni, monitorare i livelli di attesa I/O della CPU per rilevare i primi segnali di problemi.

[Ottieni file](assets/aem_environment_sizingtool.xlsx)

## Rete {#network}

[!DNL Assets] presenta una serie di casi d’uso che rendono le prestazioni di rete più importanti che in molti dei nostri [!DNL Experience Manager] progetti. Un cliente può avere un server veloce, ma se la connessione di rete non è abbastanza grande da supportare il carico degli utenti che caricano e scaricano le risorse dal sistema, allora apparirà ancora lenta. Esiste una buona metodologia per determinare il punto di interruzione nella connessione di rete di un utente a [!DNL Experience Manager] a [Considerazioni sulle risorse per l’esperienza utente, il dimensionamento delle istanze, la valutazione del flusso di lavoro e la topologia di rete](/help/assets/assets-network-considerations.md).

## Limitazioni {#limitations}

Durante il dimensionamento di un’implementazione, è importante tenere presenti i limiti del sistema. Se l’implementazione proposta supera tali limiti, utilizza strategie creative, ad esempio suddividere le risorse in più [!DNL Assets] implementazioni.

La dimensione del file non è l&#39;unico fattore che contribuisce ai problemi di memoria insufficiente. Dipende anche dalle dimensioni dell’immagine. È possibile evitare i problemi OOM fornendo una dimensione heap più elevata all&#39;avvio [!DNL Experience Manager].

Inoltre, puoi modificare la proprietà di dimensione della soglia del `com.day.cq.dam.commons.handler.StandardImageHandler` in Configuration Manager per utilizzare un file temporaneo intermedio maggiore di zero.

## Numero massimo di risorse {#maximum-number-of-assets}

Il limite al numero di file che possono esistere in un archivio dati può essere di 2,1 miliardi a causa di limitazioni del file system. È probabile che l’archivio riscontri problemi a causa del numero elevato di nodi che precedono il raggiungimento del limite dell’archivio dati.

Se le rappresentazioni non vengono generate correttamente, utilizza la libreria Camera Raw. Tuttavia, in questo caso, il lato più lungo dell&#39;immagine non deve essere maggiore di 65000 pixel. Inoltre, l&#39;immagine non deve contenere più di 512 MP (512 x 1024 x 1024 pixel). La dimensione della risorsa non ha importanza.

È difficile stimare con precisione le dimensioni del file TIFF supportato come standard con un heap specifico per [!DNL Experience Manager] perché fattori aggiuntivi, come la dimensione dei pixel, influenzano l’elaborazione. È possibile che [!DNL Experience Manager] è in grado di elaborare un file di dimensioni pari a 255 MB, ma non può elaborare un file di dimensioni pari a 18 MB perché quest&#39;ultimo include un numero insolitamente più elevato di pixel rispetto al primo.

## Dimensioni delle risorse {#size-of-assets}

Per impostazione predefinita, [!DNL Experience Manager] consente di caricare risorse di dimensioni file fino a 2 GB. Per caricare risorse di grandi dimensioni in [!DNL Experience Manager], vedi [Configurazione per caricare risorse molto grandi](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
