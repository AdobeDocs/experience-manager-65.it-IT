---
title: '[!DNL Assets] guida al dimensionamento'
description: Best practice per determinare metriche efficienti per stimare l'infrastruttura e le risorse necessarie per distribuire [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architetto, amministratore
feature: Gestione risorse
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 0%

---


# [!DNL Assets] guida al dimensionamento  {#assets-sizing-guide}

Quando si esegue il dimensionamento dell&#39;ambiente per un&#39;implementazione [!DNL Adobe Experience Manager Assets], è importante assicurarsi che siano disponibili risorse sufficienti in termini di disco, CPU, memoria, IO e throughput di rete. Il dimensionamento di molte di queste risorse richiede una comprensione del numero di risorse caricate nel sistema. Se una metrica migliore non è disponibile, puoi dividere la dimensione della libreria esistente per l’età della libreria per trovare la velocità con cui vengono create le risorse.

## Disco {#disk}

### DataStore {#datastore}

Un errore comune durante il dimensionamento dello spazio su disco richiesto per un&#39;implementazione [!DNL Assets] consiste nel basare i calcoli sulle dimensioni delle immagini non elaborate da acquisire nel sistema. Per impostazione predefinita, [!DNL Experience Manager] crea tre rappresentazioni oltre all&#39;immagine originale da utilizzare nel rendering degli elementi dell&#39;interfaccia utente [!DNL Experience Manager]. Nelle implementazioni precedenti, queste rappresentazioni sono state osservate per assumere il doppio delle dimensioni delle risorse che vengono acquisite.

La maggior parte degli utenti definisce rappresentazioni personalizzate oltre alle rappresentazioni predefinite. Oltre ai rendering, [!DNL Assets] consente di estrarre risorse secondarie da tipi di file comuni, come [!DNL Adobe InDesign] e [!DNL Adobe Illustrator].

Infine, le funzionalità di controllo delle versioni di [!DNL Experience Manager] memorizzano duplicati delle risorse nella cronologia delle versioni. Puoi configurare le versioni da eliminare spesso. Tuttavia, molti utenti scelgono di mantenere le versioni nel sistema per un lungo periodo di tempo, che consuma ulteriore spazio di archiviazione.

Considerati questi fattori, è necessaria una metodologia per calcolare uno spazio di archiviazione accettabile e accurato per archiviare le risorse degli utenti.

1. Determina le dimensioni e il numero di risorse che verranno caricate nel sistema.
1. Ottieni un esempio rappresentativo delle risorse da caricare in [!DNL Experience Manager]. Ad esempio, se intendi caricare nel sistema file PSD, JPG, AI e PDF, è necessario disporre di più immagini di esempio di ciascun formato di file. Inoltre, questi campioni devono essere rappresentativi delle diverse dimensioni e complessità dei file delle immagini.
1. Definisci i rendering da utilizzare.
1. Crea le rappresentazioni in [!DNL Experience Manager] utilizzando le applicazioni [!DNL ImageMagick] o [!DNL Adobe Creative Cloud]. Oltre alle rappresentazioni specificate dagli utenti, crea rappresentazioni predefinite. Per gli utenti che implementano Dynamic Media, puoi utilizzare il binario IC per generare le rappresentazioni PTIFF da memorizzare in Experience Manager.
1. Se prevedi di utilizzare le risorse secondarie, generale per i tipi di file appropriati.
1. Confronta le dimensioni delle immagini, delle rappresentazioni e delle risorse secondarie di output con le immagini originali. Consente di generare un fattore di crescita previsto al caricamento del sistema. Ad esempio, se generi rappresentazioni e risorse secondarie con una dimensione combinata di 3 GB dopo aver elaborato 1 GB di risorse, il fattore di crescita del rendering è 3.
1. Determina il tempo massimo per il quale le versioni delle risorse devono essere mantenute nel sistema.
1. Determina la frequenza con cui le risorse esistenti vengono modificate nel sistema. Se [!DNL Experience Manager] viene utilizzato come hub di collaborazione nei flussi di lavoro creativi, la quantità di modifiche è elevata. Se nel sistema vengono caricate solo le risorse completate, questo numero è molto inferiore.
1. Determina quante risorse vengono caricate ogni mese nel sistema. Se non sei sicuro, verifica il numero di risorse attualmente disponibili e dividi il numero per l’età della risorsa più vecchia per calcolare un numero approssimativo.

L’esecuzione dei passaggi precedenti consente di determinare quanto segue:

* Dimensione non elaborata delle risorse da caricare.
* Numero di risorse da caricare.
* Fattore di crescita della rappresentazione.
* Numero di modifiche apportate alle risorse al mese.
* Numero di mesi per la gestione delle versioni delle risorse.
* Numero di nuove risorse caricate ogni mese.
* Anni di crescita per l&#39;allocazione dello spazio di archiviazione.

È possibile specificare questi numeri nel foglio di calcolo Ridimensionamento di rete per determinare lo spazio totale necessario per l’archivio dati. È anche uno strumento utile per determinare l’impatto della manutenzione delle versioni delle risorse o della modifica delle risorse in [!DNL Experience Manager] sulla crescita del disco.

I dati di esempio compilati nello strumento mostrano l’importanza di eseguire i passaggi indicati. Se si ridimensiona il datastore in base solo alle immagini non elaborate caricate (1 TB), è possibile che la dimensione del repository sia stata sottostimata di un fattore di 15.

[Ottieni file](assets/disk_sizing_tool.xlsx)

### Archiviazione dati condivisa {#shared-datastores}

Per i datastore di grandi dimensioni, è possibile implementare un datastore condiviso tramite un datastore di file condiviso su un&#39;unità di rete collegata o tramite un datastore Amazon S3. In questo caso, non è necessario mantenere una copia dei binari nelle singole istanze. Inoltre, un datastore condiviso facilita la replica senza binario e aiuta a ridurre la larghezza di banda utilizzata per replicare le risorse negli ambienti di pubblicazione.

#### Casi di utilizzo {#use-cases}

Il datastore può essere condiviso tra un’istanza di authoring primaria e standby per ridurre al minimo il tempo necessario per aggiornare l’istanza di standby con le modifiche apportate nell’istanza primaria. Puoi anche condividere l’archivio dati tra le istanze di authoring e pubblicazione per ridurre al minimo il traffico durante la replica.

#### Drawback {#drawbacks}

A causa di alcune insidie, la condivisione di un datastore non è consigliata in tutti i casi.

#### Singolo punto di errore {#single-point-of-failure}

Avere un datastore condiviso, introduce un singolo punto di errore in un&#39;infrastruttura. Considera uno scenario in cui il tuo sistema dispone di un autore e due istanze di pubblicazione, ciascuna con il proprio datastore. Se uno di questi si blocca, gli altri due possono ancora continuare a funzionare. Tuttavia, se il datastore viene condiviso, un singolo errore del disco può abbattere l&#39;intera infrastruttura. Di conseguenza, assicurati di mantenere un backup dell&#39;archivio dati condiviso da cui puoi ripristinare rapidamente l&#39;archivio dati.

È preferibile implementare il servizio AWS S3 per i datastore condivisi, in quanto riduce in modo significativo la probabilità di errore rispetto alle architetture normali del disco.

#### Maggiore complessità {#increased-complexity}

I datastore condivisi aumentano anche la complessità delle operazioni, come la raccolta degli oggetti inattivi. Normalmente, la raccolta degli oggetti inattivi per un datastore indipendente può essere avviata con un solo clic. Tuttavia, i datastore condivisi richiedono operazioni di sweep di contrassegno su ogni membro che utilizza il datastore, oltre a eseguire la raccolta effettiva su un singolo nodo.

Per le operazioni AWS, l&#39;implementazione di una singola posizione centrale (tramite Amazon S3), invece di costruire un array RAID di volumi EBS, può compensare in modo significativo la complessità e i rischi operativi del sistema.

#### Problemi di prestazioni {#performance-concerns}

Un datastore condiviso richiede che i binari siano memorizzati su un&#39;unità montata in rete condivisa tra tutte le istanze. Poiché questi binari sono accessibili tramite una rete, le prestazioni del sistema sono influenzate negativamente. È possibile attenuare parzialmente l&#39;impatto utilizzando una connessione di rete rapida a un array veloce di dischi. Tuttavia, questa è una proposta costosa. Nel caso di operazioni AWS, tutti i dischi sono remoti e richiedono connettività di rete. I volumi effimeri perdono i dati quando l&#39;istanza viene avviata o arrestata.

#### Latenza {#latency}

La latenza nelle implementazioni S3 viene introdotta dai thread di scrittura in background. Le procedure di backup devono tenere conto di questa latenza. Inoltre, gli indici Lucene possono rimanere incompleti durante la creazione di un backup. Si applica a qualsiasi file sensibile al tempo scritto nel datastore S3 e a cui si accede da un&#39;altra istanza.

### Archivio dei nodi o dei documenti {#node-store-document-store}

È difficile ottenere cifre precise di dimensionamento per un NodeStore o DocumentStore a causa delle risorse utilizzate da quanto segue:

* Metadati delle risorse
* Versioni delle risorse
* Registri di controllo
* Flussi di lavoro archiviati e attivi

Poiché i binari vengono memorizzati nel datastore, ogni binario occupa un po&#39; di spazio. La maggior parte degli archivi ha dimensioni inferiori a 100 GB. Tuttavia, ci possono essere archivi di dimensioni maggiori fino a 1 TB. Inoltre, per eseguire la compattazione offline, è necessario abbastanza spazio libero sul volume per riscrivere l&#39;archivio compattato insieme alla versione pre-compattata. Una buona regola è quella di ridimensionare il disco a 1,5 volte la dimensione prevista per l&#39;archivio.

Per l&#39;archivio, utilizzare SSD o dischi con un livello IOPS superiore a 3000. Per eliminare le possibilità che IOPS introduca i colli di bottiglia delle prestazioni, monitorare i livelli di attesa della CPU I/O per i primi segnali di problemi.

[Ottieni file](assets/aem_environment_sizingtool.xlsx)

## Rete {#network}

[!DNL Assets] ha una serie di casi d&#39;uso che rendono le prestazioni di rete più importanti rispetto a molti dei nostri  [!DNL Experience Manager] progetti. Un cliente può disporre di un server veloce, ma se la connessione di rete non è abbastanza grande per supportare il carico degli utenti che caricano e scaricano risorse dal sistema, allora apparirà comunque lento. Esiste una buona metodologia per determinare il punto di interruzione nella connessione di rete di un utente a [!DNL Experience Manager] in [Considerazioni sulle risorse per l&#39;esperienza utente, il dimensionamento dell&#39;istanza, la valutazione del flusso di lavoro e la topologia di rete](/help/assets/assets-network-considerations.md).

## Limitazioni  {#limitations}

Quando si dimensiona un&#39;implementazione, è importante tenere presenti le limitazioni di sistema. Se l’implementazione proposta supera tali limiti, utilizza strategie creative, ad esempio la suddivisione delle risorse tra più [!DNL Assets] implementazioni.

La dimensione del file non è l’unico fattore che contribuisce a problemi di memoria esaurita (OOM). Dipende anche dalle dimensioni dell&#39;immagine. È possibile evitare problemi di OOM fornendo una dimensione di heap maggiore all&#39;avvio di [!DNL Experience Manager].

Inoltre, è possibile modificare la proprietà Dimensione soglia del componente `com.day.cq.dam.commons.handler.StandardImageHandler` in Configuration Manager per utilizzare un file temporaneo intermedio maggiore di zero.

## Numero massimo di risorse {#maximum-number-of-assets}

Il limite al numero di file che possono esistere in un datastore può essere di 2,1 miliardi a causa di limitazioni del filesystem. È probabile che l’archivio incontri problemi a causa di un numero elevato di nodi molto lungo prima di raggiungere il limite del datastore.

Se le rappresentazioni non sono generate correttamente, utilizza la libreria Camera Raw. Tuttavia, in questo caso, il lato più lungo dell&#39;immagine non deve essere maggiore di 65000 pixel. Inoltre, l&#39;immagine non deve contenere più di 512 MP (512 x 1024 x 1024 pixel). La dimensione della risorsa non ha importanza.

È difficile stimare con precisione le dimensioni del file TIFF supportato come preconfigurato con un heap specifico per [!DNL Experience Manager] perché fattori aggiuntivi, come l’elaborazione dell’influenza delle dimensioni dei pixel. È possibile che [!DNL Experience Manager] possa elaborare un file di dimensioni pari a 255 MB out-of-the-box, ma non possa elaborare un file di dimensioni pari a 18 MB perché quest&#39;ultimo comprende un numero di pixel insolitamente più alto rispetto al primo.

## Dimensione delle risorse {#size-of-assets}

Per impostazione predefinita, [!DNL Experience Manager] consente di caricare risorse di dimensioni file fino a 2 GB. Per caricare risorse di grandi dimensioni in [!DNL Experience Manager], consulta [Configurazione per caricare risorse di grandi dimensioni](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
