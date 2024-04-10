---
title: Adobe Experience Manager con MongoDB
description: Scopri le attività e le considerazioni necessarie per una corretta implementazione di Adobe Experience Manager con MongoDB.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 0%

---

# Adobe Experience Manager con MongoDB{#aem-with-mongodb}

Questo articolo ha lo scopo di migliorare le conoscenze sui compiti e sulle considerazioni necessarie per implementare correttamente l’AEM (Adobe Experience Manager) con MongoDB.

Per ulteriori informazioni relative alla distribuzione, consulta [Distribuzione e manutenzione](/help/sites-deploying/deploy.md) sezione della documentazione.

## Quando usare MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB viene generalmente utilizzato per supportare le distribuzioni di authoring AEM in cui è soddisfatto uno dei seguenti criteri:

* più di 1000 utenti unici al giorno;
* Più di 100 utenti simultanei;
* Volumi elevati di modifiche di pagina;
* Rollout o attivazioni di grandi dimensioni.

I criteri di cui sopra si applicano solo alle istanze di authoring e non alle istanze di pubblicazione che devono essere tutte basate su TarMK. Il numero di utenti si riferisce agli utenti autenticati, poiché le istanze di authoring non consentono l’accesso non autenticato.

Se i criteri non sono soddisfatti, si consiglia una distribuzione TarMK attiva/in standby per gestire la disponibilità. Generalmente, MongoDB deve essere considerato in situazioni in cui i requisiti di scalabilità sono più di quanto si possa ottenere con un singolo componente hardware.

>[!NOTE]
>
>Ulteriori informazioni sul dimensionamento delle istanze di authoring e sulla definizione di utenti simultanei sono disponibili nella sezione [Linee guida per il dimensionamento dell&#39;hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Distribuzione minima MongoDB per AEM {#minimal-mongodb-deployment-for-aem}

Di seguito è riportata una distribuzione minima per AEM su MongoDB. Per semplicità, sono stati generalizzati la terminazione SSL e i componenti proxy HTTP. È costituito da un singolo set di repliche MongoDB, con un primario e due secondari.

![chlimage_1-4](assets/chlimage_1-4.png)

Un&#39;installazione minima richiede tre `mongod` istanze configurate come set di repliche. Un’istanza è selezionata come primaria mentre le altre istanze sono secondarie, con la selezione gestita da `mongod`. A ogni istanza è associato un disco locale. Per supportare il carico, si consiglia un throughput minimo di 12 MB al secondo con più di 3000 operazioni di I/O al secondo (IOPS).

Gli autori dell’AEM sono collegati al `mongod` con ogni autore AEM che si connette a tutti e tre `mongod` istanze. Le scritture vengono inviate al primario e le letture possono essere lette da una qualsiasi delle istanze. Il traffico viene distribuito in base al carico da un Dispatcher a una qualsiasi delle istanze di authoring AEM attive. L’archivio dati Oak è un `FileDataStore`e il monitoraggio MongoDB viene fornito da MMS o MongoDB Ops Manager a seconda della posizione della distribuzione. Il monitoraggio del sistema operativo e dei registri è fornito da soluzioni di terze parti come Splunk o Ganglia.

In questa distribuzione, tutti i componenti sono necessari per una corretta implementazione. Qualsiasi componente mancante lascia l’implementazione non funzionante.

### Sistemi operativi {#operating-systems}

Per un elenco dei sistemi operativi supportati per l&#39;AEM 6, vedere [Pagina Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Ambienti {#environments}

Gli ambienti virtualizzati sono supportati a condizione che vi sia una buona comunicazione tra i diversi team tecnici che eseguono il progetto. Questo supporto include il team che esegue AEM, il team proprietario del sistema operativo e il team che gestisce l&#39;infrastruttura virtualizzata.

Esistono requisiti specifici relativi alla capacità di I/O delle istanze MongoDB che devono essere gestiti dal team che gestisce l’ambiente virtualizzato. Se il progetto utilizza una distribuzione cloud, come Amazon Web Services, le istanze devono essere fornite con capacità di I/O e coerenza sufficienti per supportare le istanze MongoDB. In caso contrario, i processi MongoDB e l’archivio Oak funzionano in modo inaffidabile ed errato.

Negli ambienti virtualizzati, MongoDB richiede specifiche configurazioni I/O e VM per garantire che il motore di storage di MongoDB non sia paralizzato da criteri di allocazione delle risorse VMWare. Un’implementazione di successo assicura che non vi siano barriere tra i vari team e che tutti siano iscritti per fornire le prestazioni richieste.

## Considerazioni sull&#39;hardware {#hardware-considerations}

### Archiviazione {#storage}

Per ottenere il throughput di lettura e scrittura per ottenere prestazioni ottimali senza la necessità di scalabilità orizzontale prematura, MongoDB richiede in genere storage SSD o storage con prestazioni equivalenti a SSD.

### RAM {#ram}

Le versioni 2.6 e 3.0 di MongoDB che utilizzano il motore di archiviazione MMAP richiedono che il working set del database e i relativi indici si inseriscano nella RAM.

Una RAM insufficiente determina una riduzione significativa delle prestazioni. Le dimensioni del working set e del database dipendono fortemente dall&#39;applicazione. Anche se alcune stime possono essere fatte, il modo più affidabile per determinare la quantità di RAM necessaria è quello di creare l&#39;applicazione AEM e testarla.

Per facilitare il processo di test di carico, è possibile supporre il seguente rapporto tra il working set e la dimensione totale del database:

* 1:10 per storage SSD
* 1:3 per l&#39;archiviazione su hard disk

Questi rapporti indicano che per le implementazioni SSD sono necessari 200 GB di RAM per un database da 2 TB.

Mentre le stesse limitazioni si applicano al motore di storage WiredTiger in MongoDB 3.0, la correlazione tra il working set, la RAM e gli errori di pagina non è così forte. WiredTiger non utilizza la mappatura della memoria allo stesso modo del motore di archiviazione MMAP.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare il motore di archiviazione WiredTiger per le distribuzioni AEM 6.1 che utilizzano MongoDB 3.0.

### Archivio dati {#data-store}

A causa delle limitazioni del working set MongoDB, si consiglia di mantenere l’archivio dati indipendente da MongoDB. Nella maggior parte degli ambienti, un `FileDataStore` utilizzare un NAS disponibile per tutte le istanze AEM. Nelle situazioni in cui viene utilizzato Amazon Web Services, è inoltre disponibile `S3 DataStore`. Se per qualsiasi motivo l’archivio dati viene mantenuto all’interno di MongoDB, la dimensione dell’archivio dati deve essere aggiunta alla dimensione totale del database e i calcoli del working set devono essere adeguati di conseguenza. Questo dimensionamento può significare il provisioning di più RAM per mantenere le prestazioni senza errori di pagina.

## Monitoraggio {#monitoring}

Il monitoraggio è essenziale per il successo dell&#39;attuazione del progetto. Con sufficienti conoscenze, è possibile eseguire AEM su MongoDB senza monitoraggio. Tuttavia, tale conoscenza si trova normalmente in ingegneri specializzati per ogni sezione della distribuzione.

Queste conoscenze specialistiche coinvolgono in genere un ingegnere R&amp;D che lavora su Apache Oak Core e uno specialista MongoDB.

Senza il monitoraggio a tutti i livelli, per diagnosticare i problemi è necessaria una conoscenza dettagliata della base di codice. Grazie al monitoraggio e a una guida adeguata sulle principali statistiche, i team addetti all’attuazione possono reagire in modo appropriato alle anomalie.

Sebbene sia possibile utilizzare strumenti della riga di comando per ottenere un&#39;istantanea rapida del funzionamento di un cluster, è quasi impossibile eseguire questa operazione in tempo reale su molti host. Gli strumenti della riga di comando raramente forniscono informazioni storiche oltre pochi minuti e non consentono mai correlazioni incrociate tra diversi tipi di metriche. Un breve periodo di background lento `mongod` La sincronizzazione richiede un notevole sforzo manuale per la correlazione con Attesa I/O o livelli di scrittura eccessivi in una risorsa di archiviazione condivisa da una macchina virtuale apparentemente non connessa.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager è un servizio gratuito offerto da MongoDB che consente il monitoraggio e la gestione delle istanze di MongoDB. Fornisce una panoramica delle prestazioni e dello stato del cluster MongoDB in tempo reale. Gestisce sia le istanze cloud che quelle ospitate privatamente, a condizione che l’istanza possa raggiungere il server di monitoraggio di Cloud Manager.

Richiede un agente installato sull’istanza di MongoDB che si connette al server di monitoraggio. Esistono tre livelli dell’agente:

* Un agente di automazione in grado di automatizzare completamente tutto ciò che si trova sul server MongoDB,
* Un agente di monitoraggio in grado di monitorare `mongod` istanza,
* Agente di backup in grado di eseguire backup pianificati dei dati.

Sebbene l’utilizzo di Cloud Manager per l’automazione della manutenzione di un cluster MongoDB semplifichi molte delle attività di routine, non è necessario e non viene utilizzato per il backup. Tuttavia, quando si sceglie Cloud Manager da monitorare, è necessario il monitoraggio.

Per ulteriori informazioni su MongoDB Cloud Manager, consulta [Documentazione di MongoDB](https://docs.cloud.mongodb.com/).

### Gestione operazioni MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager è lo stesso software di MongoDB Cloud Manager. Una volta registrato, Ops Manager può essere scaricato e installato localmente in un centro dati privato o su qualsiasi altro computer portatile o desktop. Utilizza un database MongoDB locale per memorizzare i dati e comunica allo stesso modo di Cloud Manager con i server gestiti. Se i criteri di sicurezza non consentono l&#39;utilizzo di un agente di monitoraggio, utilizzare MongoDB Ops Manager.

### Monitoraggio del sistema operativo {#operating-system-monitoring}

Per eseguire un cluster AEM MongoDB è necessario il monitoraggio a livello di sistema operativo.

Ganglia è un buon esempio di tale sistema e fornisce un&#39;immagine sulla gamma e sui dettagli delle informazioni richieste che vanno oltre le metriche di base sullo stato di salute come CPU, media di carico e spazio libero su disco. Per diagnosticare i problemi, sono necessarie informazioni di livello inferiore come i livelli del pool di entropia, l’attesa I/O della CPU e i socket nello stato FIN_WAIT2.

### Aggregazione registro {#log-aggregation}

Con un cluster di più server, l&#39;aggregazione centrale dei registri è un requisito per un sistema di produzione. Software come Splunk supporta l&#39;aggregazione dei registri e consente ai team di analizzare i modelli di comportamento dell&#39;applicazione senza dover raccogliere manualmente i registri.

## Elenchi di controllo {#checklists}

Questa sezione descrive i vari passaggi da seguire per garantire che le distribuzioni di AEM e MongoDB siano configurate correttamente prima di implementare il progetto.

### Rete {#network}

1. Innanzitutto, assicurati che tutti gli host abbiano una voce DNS
1. Tutti gli host devono essere risolvibili tramite la relativa voce DNS da tutti gli altri host instradabili
1. Tutti gli host MongoDB sono instradabili da tutti gli altri host MongoDB nello stesso cluster
1. Gli host MongoDB possono indirizzare i pacchetti a MongoDB Cloud Manager e agli altri server di monitoraggio
1. I server AEM possono indirizzare i pacchetti a tutti i server MongoDB
1. La latenza dei pacchetti tra qualsiasi server AEM e qualsiasi server MongoDB è inferiore a due millisecondi, senza perdita di pacchetti e con una distribuzione standard di un millisecondo o meno.
1. Assicurati che non vi siano più di due hop tra un server AEM e un server MongoDB
1. Non ci sono più di due hop tra due server MongoDB
1. Non esistono router di livello superiore a OSI livello 3 tra i server principali (MongoDB o AEM o qualsiasi combinazione).
1. Se si utilizza il trunking VLAN o una qualsiasi forma di tunneling di rete, questo deve essere conforme ai controlli di latenza dei pacchetti.

### Configurazione AEM {#aem-configuration}

#### Configurazione archivio nodi {#node-store-configuration}

Le istanze dell’AEM devono essere configurate per utilizzare l’AEM con MongoMK. La base dell’implementazione di MongoMK nell’AEM è l’archivio dei nodi dei documenti.

Per ulteriori informazioni su come configurare gli archivi nodi, vedi [Configurazione degli archivi di nodi e dei dati in AEM](/help/sites-deploying/data-store-config.md).

Di seguito è riportato un esempio di configurazione dell’archivio dei nodi di documento per una distribuzione minima di MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Dove:

* `mongodburi`
Il server MongoDB a cui AEM deve connettersi. Vengono stabilite connessioni a tutti i membri noti del set di repliche predefinito. Se si utilizza MongoDB Cloud Manager, la sicurezza del server è abilitata. Pertanto, la stringa di connessione deve contenere un nome utente e una password appropriati. Le versioni non aziendali di MongoDB supportano solo l’autenticazione tramite nome utente e password. Per ulteriori informazioni sulla sintassi della stringa di connessione, consultare [documentazione](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nome del database. Il valore predefinito per l’AEM è `aem-author`.

* `customBlobStore`
Se la distribuzione memorizza i file binari nel database, questi fanno parte del working set. Per questo motivo, si consiglia di non conservare dati binari all’interno di MongoDB, preferendo un archivio dati alternativo come un `FileSystem` archivio dati su un NAS.

* `cache`
Dimensione della cache in megabyte. Questo spazio viene distribuito tra le varie cache utilizzate in `DocumentNodeStore`. Il valore predefinito è 256 MB. Tuttavia, le prestazioni di lettura Oak traggono vantaggio da una cache più ampia.

* `blobCacheSize`
I BLOB utilizzati di frequente possono essere memorizzati nella cache dall’AEM per evitare di recuperarli dall’archivio dati. Questa operazione ha un impatto maggiore sulle prestazioni, in particolare quando si memorizzano i BLOB nel database MongoDB. Tutti gli archivi dati basati su file system usufruiscono della cache su disco a livello di sistema operativo.

#### Configurazione archivio dati {#data-store-configuration}

L’archivio dati viene utilizzato per memorizzare file di dimensioni superiori a una soglia. Al di sotto di tale soglia, i file vengono memorizzati come proprietà all&#39;interno dell&#39;archivio dei nodi dei documenti. Se il `MongoBlobStore` viene utilizzata, viene creata una raccolta dedicata in MongoDB per memorizzare i BLOB. Questa raccolta contribuisce al working set del `mongod` e richiede che `mongod` dispone di più RAM per evitare problemi di prestazioni. Per questo motivo, la configurazione consigliata consiste nell’evitare `MongoBlobStore` per le distribuzioni di produzione e l’utilizzo `FileDataStore` supportato da un NAS condiviso tra tutte le istanze AEM. Poiché la cache a livello di sistema operativo è efficiente nella gestione dei file, la dimensione minima di un file su disco deve essere impostata in prossimità della dimensione del blocco del disco. In questo modo il file system viene utilizzato in modo efficiente e molti documenti di piccole dimensioni non contribuiscono in modo eccessivo al working set del `mongod` dell&#39;istanza.

Di seguito è riportata una configurazione tipica dell’archivio dati per un’implementazione AEM minima con MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

Dove:

* `minRecordLength`
Dimensione in byte. I file binari di dimensioni inferiori o uguali a queste vengono memorizzati nell&#39;archivio nodi documento. Invece di memorizzare l’ID del BLOB, viene memorizzato il contenuto del binario. Se i file binari sono maggiori di queste dimensioni, l&#39;ID del file binario viene memorizzato come proprietà del documento nell&#39;insieme dei nodi. Il corpo del file binario viene memorizzato nel file `FileDataStore` su disco. 4096 byte è una dimensione tipica del blocco del file system.

* `path`
Percorso della directory principale dell’archivio dati. Per una distribuzione MongoMK, questo percorso deve essere un file system condiviso disponibile per tutte le istanze AEM. In genere viene utilizzato un server NAS (Network Attached Storage). Per implementazioni cloud come Amazon Web Services, il `S3DataFileStore` è disponibile anche.

* `cacheSizeInMB`
Dimensione totale della cache binaria in MB. Viene utilizzato per memorizzare in cache dati binari inferiori a `maxCacheBinarySize` impostazione.

* `maxCachedBinarySize`
Dimensione massima in byte di un file binario memorizzato nella cache binaria. Se si utilizza un archivio dati basato su file system, si sconsiglia di utilizzare valori elevati per la cache dell’archivio dati, in quanto i file binari sono già memorizzati nella cache dal sistema operativo.

#### Disattivazione del suggerimento query {#disabling-the-query-hint}

È consigliabile disattivare l’hint di query inviato con tutte le query aggiungendo la proprietà `-Doak.mongo.disableIndexHint=true` quando inizia l’AEM. In questo modo MongoDB calcola l’indice più appropriato da utilizzare in base alle statistiche interne.

Se l’hint query non è disabilitato, qualsiasi ottimizzazione delle prestazioni degli indici non ha alcun impatto sulle prestazioni dell’AEM.

#### Abilita cache persistente per MongoMK {#enable-persistent-cache-for-mongomk}

Si consiglia di abilitare una configurazione della cache persistente per le distribuzioni MongoDB, per massimizzare la velocità per gli ambienti con elevate prestazioni di lettura I/O. Per ulteriori dettagli, vedi [Documentazione di Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Ottimizzazioni del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Supporto del sistema operativo {#operating-system-support}

MongoDB 2.6 utilizza un motore di storage mappato alla memoria che è sensibile ad alcuni aspetti della gestione a livello di sistema operativo tra RAM e Disco. Le prestazioni di query e lettura dell’istanza MongoDB si basano sull’evitare o eliminare le operazioni di I/O lente, spesso denominate errori di pagina. Si tratta di errori di pagina che si applicano al `mongod` in particolare. Non confondere con gli errori di pagina del sistema operativo.

Per un funzionamento rapido, il database MongoDB dovrebbe accedere solo ai dati già presenti nella RAM. I dati a cui deve accedere sono costituiti da indici e dati. Questa raccolta di indici e dati è denominata working set. Se il working set è più grande della RAM disponibile, MongoDB deve inserire tali dati dal disco sostenendo un costo di I/O, eliminando altri dati già in memoria. Se lo sfratto causa il ricaricamento dei dati dal disco, dominano gli errori di pagina e le prestazioni peggiorano. Se il working set è dinamico e variabile, vengono generati più errori di pagina per supportare le operazioni.

MongoDB viene eseguito su diversi sistemi operativi, tra cui una vasta gamma di versioni Linux®, Windows e macOS. Consulta [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) per ulteriori dettagli. A seconda della scelta del sistema operativo, MongoDB ha diversi consigli a livello di sistema operativo. Sono documentati in [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) e riepilogati qui per comodità.

#### Linux® {#linux}

* Disattivare le coperture trasparenti e sfalsare. Consulta [Impostazioni pagine grandi trasparenti](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) per ulteriori informazioni.
* [Regolare le impostazioni di lettura anticipata](https://docs.mongodb.com/manual/administration/production-notes/#readahead) sui dispositivi che memorizzano i file del database in modo da adattarli al tuo caso d’uso.

   * Per il motore di storage MMAPv1, se il working set è più grande della RAM disponibile e il modello di accesso al documento è casuale, è consigliabile ridurre il valore di readahead a 32 o 16. Valutare diverse impostazioni per trovare un valore ottimale che massimizzi la memoria residente e riduca il numero di errori di pagina.
   * Per il motore di storage WiredTiger, impostare readahead su 0 indipendentemente dal tipo di supporto di storage (rotazione, SSD e così via). In generale, utilizza l’impostazione di lettura consigliata a meno che il test non mostri un vantaggio misurabile, ripetibile e affidabile in un valore di lettura più elevato. [Supporto professionale MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) può fornire consigli e indicazioni su configurazioni readahead diverse da zero.

* Disattivare lo strumento ottimizzato se si esegue RHEL 7/CentOS 7 in un ambiente virtuale.
* Quando RHEL 7/CentOS 7 viene eseguito in un ambiente virtuale, lo strumento ottimizzato richiama automaticamente un profilo di prestazioni derivato dal throughput delle prestazioni, che imposta automaticamente le impostazioni di lettura a 4 MB. Questa impostazione può avere un impatto negativo sulle prestazioni.
* Utilizzare le utilità di pianificazione disco noop o deadline per le unità SSD.
* Utilizzare il modulo di pianificazione dei dischi noop per le unità virtualizzate nelle VM guest.
* Disattiva NUMA o imposta `vm.zone_reclaim_mode` a 0 ed eseguire [mondio](https://docs.mongodb.com/manual/administration/production-notes/#readahead) istanze con interfoliazione dei nodi. Consulta: [MongoDB e NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) per ulteriori informazioni.

* Regola i valori massimi sull’hardware in modo che siano adatti al tuo caso d’uso. Se più [mondio](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) le istanze vengono eseguite con lo stesso utente, ridimensiona i valori limite di conseguenza. Consulta: [Impostazioni UNIX® ulimit](https://docs.mongodb.com/manual/reference/ulimit/) per ulteriori informazioni.

* Usa noatime per [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) punto di montaggio.
* Configurare un numero sufficiente di handle di file (fs.file-max), il limite pid del kernel (kernel.pid_max) e il numero massimo di thread per processo (kernel.threads-max) per la distribuzione. Per i sistemi di grandi dimensioni, i seguenti valori costituiscono un buon punto di partenza:

   * fs.file-max valore di 98000,
   * valore kernel.pid_max di 64000,
   * andkernel.threads-valore massimo di 64000

* Verificare che nel sistema sia configurato lo spazio di swap. Per informazioni dettagliate sul dimensionamento appropriato, consultare la documentazione del sistema operativo in uso.
* Verificare che il valore predefinito di sistema di TCP keepalive sia impostato correttamente. Un valore pari a 300 offre spesso prestazioni migliori per i set di repliche e i cluster condivisi. Consulta: [Il tempo di conservazione di TCP influisce sulle distribuzioni di MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) per ulteriori informazioni, vedere Domande frequenti.

#### Windows {#windows}

* È consigliabile disattivare gli aggiornamenti relativi all&#39;&quot;ora dell&#39;ultimo accesso&quot; NTFS. Questa impostazione è analoga alla disattivazione di atime su sistemi Unix-like.

### WiredTiger {#wiredtiger}

A partire da MongoDB 3.2 il motore di archiviazione predefinito per MongoDB è il motore di archiviazione WiredTiger. Questo motore offre alcune funzionalità solide e scalabili che lo rendono molto più adatto per tutti i carichi di lavoro generali del database. Le sezioni seguenti descrivono queste funzioni.

#### Concorrenza a livello di documento {#document-level-concurrency}

WiredTiger utilizza il controllo della concorrenza a livello di documento per le operazioni di scrittura. Di conseguenza, più client possono modificare contemporaneamente diversi documenti di una raccolta.

Per la maggior parte delle operazioni di lettura e scrittura, WiredTiger utilizza il controllo ottimistico della concorrenza. WiredTiger utilizza solo blocchi intento a livello globale, di database e di raccolta. Quando il motore di archiviazione rileva i conflitti tra due operazioni, una di esse genera un conflitto di scrittura che causa un nuovo tentativo trasparente di MongoDB di eseguire l’operazione. Alcune operazioni globali, in genere di breve durata che coinvolgono più database, richiedono ancora un blocco globale a livello di istanza.

Alcune altre operazioni, ad esempio l&#39;eliminazione di una raccolta, richiedono ancora un blocco esclusivo del database.

#### Snapshot e punti di controllo {#snapshots-and-checkpoints}

WiredTiger utilizza MultiVersion Concurrency Control (MVCC). All&#39;inizio di un&#39;operazione, WiredTiger fornisce un&#39;istantanea point-in-time dei dati della transazione. Uno snapshot presenta una visualizzazione coerente dei dati in memoria.

Durante la scrittura su disco, WiredTiger scrive tutti i dati di una copia istantanea su disco in modo coerente in tutti i file di dati. L&#39;ora- [durevole](https://docs.mongodb.com/manual/reference/glossary/#term-durable) I dati fungono da punto di controllo nei file di dati. Il punto di controllo assicura la coerenza dei file di dati fino all’ultimo punto di controllo incluso. In altre parole, i punti di controllo possono fungere da punti di ripristino.

MongoDB configura WiredTiger per creare punti di controllo (ovvero, scrivere i dati delle copie istantanee su disco) a intervalli di 60 secondi o 2 GB di dati del diario.

Durante la scrittura di un nuovo punto di controllo, il punto di controllo precedente è ancora valido. Di conseguenza, anche se MongoDB termina o riscontra un errore durante la scrittura di un nuovo punto di controllo, al riavvio MongoDB può ripristinarsi dall’ultimo punto di controllo valido.

Il nuovo punto di controllo diventa accessibile e permanente quando la tabella dei metadati di WiredTiger viene aggiornata atomicamente per fare riferimento al nuovo punto di controllo. Quando il nuovo punto di controllo è accessibile, WiredTiger libera le pagine dai punti di controllo precedenti.

Utilizzo di WiredTiger, anche senza [inserimento nel journal](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB può eseguire il ripristino dall’ultimo punto di controllo; tuttavia, per recuperare le modifiche apportate dopo l’ultimo punto di controllo, esegui con [inserimento nel journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger utilizza una combinazione di accesso alle transazioni write-ahead con [punti di controllo](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) per garantire la durata dei dati.

Il journal WiredTiger mantiene tutte le modifiche apportate ai dati tra i punti di controllo. Se MongoDB esce tra punti di controllo, utilizza il giornale di registrazione per riprodurre tutti i dati modificati dall’ultimo punto di controllo. Per informazioni sulla frequenza con cui MongoDB scrive i dati del giornale su disco, vedere [Processo di inserimento nel journal](https://docs.mongodb.com/manual/core/journaling/#journal-process).

Il giornale di registrazione WiredTiger è compresso utilizzando [accattivante](https://docs.mongodb.com/manual/core/journaling/#journal-process) libreria di compressione. Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) impostazione.

Consulta [Inserimento nel journal con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>La dimensione minima del record di registro per WiredTiger è di 128 byte. Se un record di registro è di almeno 128 byte, WiredTiger non comprime tale record.
>
>È possibile disattivare la registrazione impostando [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) su false, che può ridurre il sovraccarico di gestione del giornale.
>
>Per [standalone](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) Se non utilizzi il giornale di registrazione, alcune modifiche dati andranno perse quando MongoDB esce in modo imprevisto tra i punti di controllo. Per i membri di [set di repliche](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), il processo di replica può fornire sufficienti garanzie di durata.

#### Compressione {#compression}

Con WiredTiger, MongoDB supporta la compressione per tutte le raccolte e gli indici. La compressione riduce al minimo l&#39;utilizzo dello storage a scapito della CPU aggiuntiva.

Per impostazione predefinita, WiredTiger utilizza la compressione dei blocchi con [accattivante](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) libreria di compressione per tutte le raccolte e [compressione prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) per tutti gli indici.

Per le raccolte, blocca la compressione con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) è disponibile anche. Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) impostazione.

Per gli indici, per disattivare [compressione prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), utilizza [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) impostazione.

Le impostazioni di compressione sono configurabili anche per singola raccolta e per indice durante la creazione di raccolte e indici. Consulta [Specificare le opzioni del motore di archiviazione](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) e [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) opzione.

Per la maggior parte dei carichi di lavoro, le impostazioni di compressione predefinite bilanciano l&#39;efficienza dello storage e i requisiti di elaborazione.

Anche il journal WiredTiger è compresso per impostazione predefinita. Per informazioni sulla compressione del diario, vedere [Diario](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Utilizzo della memoria {#memory-use}

Con WiredTiger, MongoDB utilizza sia la cache interna di WiredTiger che la cache del file system.

A partire dalla versione 3.4, la cache interna di WiredTiger, per impostazione predefinita, utilizza il valore maggiore tra:

* 50% della RAM meno 1 GB o
* 256 MB

Per impostazione predefinita, WiredTiger utilizza la compressione dei blocchi Snappy per tutti gli insiemi e la compressione dei prefissi per tutti gli indici. I valori predefiniti di compressione sono configurabili a livello globale e possono essere impostati anche per singola raccolta e per singolo indice durante la creazione della raccolta e dell’indice.

Vengono utilizzate diverse rappresentazioni per i dati nella cache interna di WiredTiger rispetto al formato su disco:

* I dati nella cache del file system sono identici al formato su disco e includono i vantaggi di qualsiasi compressione per i file di dati. La cache del file system viene utilizzata dal sistema operativo per ridurre l&#39;I/O del disco.

Gli indici caricati nella cache interna di WiredTiger hanno una rappresentazione dei dati diversa rispetto al formato su disco, ma possono comunque sfruttare la compressione dei prefissi dell&#39;indice per ridurre l&#39;utilizzo della RAM.

La compressione dei prefissi di indice deduplica i prefissi comuni dai campi indicizzati.

I dati di raccolta nella cache interna di WiredTiger non sono compressi e utilizzano una rappresentazione diversa dal formato su disco. La compressione a blocchi può consentire un notevole risparmio di spazio su disco, ma i dati devono essere decompressi per poter essere manipolati dal server.

Tramite la cache del file system, MongoDB utilizza automaticamente tutta la memoria libera che non viene utilizzata dalla cache di WiredTiger o da altri processi.

Per regolare le dimensioni della cache interna di WiredTiger, vedere [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—cablatoTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evitare di aumentare le dimensioni della cache interna di WiredTiger oltre il valore predefinito.

### NUMA {#numa}

NUMA (Non-Uniform Memory Access) consente a un kernel di gestire il modo in cui la memoria viene mappata ai core del processore. Anche se questo processo tenta di rendere più veloce l&#39;accesso alla memoria per i core, garantendo che siano in grado di accedere ai dati richiesti, NUMA interferisce con MMAP introducendo una latenza aggiuntiva, in quanto non è possibile prevedere le letture. Di conseguenza, NUMA deve essere disabilitato per `mongod` su tutti i sistemi operativi compatibili.

In sostanza, in un&#39;architettura NUMA la memoria è connessa alle CPU e le CPU sono collegate a un bus. In un SMP o in un&#39;architettura UMA, la memoria è connessa al bus e condivisa dalle CPU. Quando un thread alloca memoria su una CPU NUMA, viene allocato in base a un criterio. L&#39;impostazione predefinita consiste nell&#39;allocare memoria collegata alla CPU locale del thread a meno che non vi sia spazio libero, nel qual caso utilizza memoria da una CPU libera a un costo maggiore. Una volta allocata, la memoria non si sposta tra le CPU. L’allocazione viene eseguita da un criterio ereditato dal thread padre, che in ultima analisi è il thread che ha avviato il processo.

In molti database che vedono il computer come un&#39;architettura di memoria uniforme e multicore, questo scenario fa sì che la CPU iniziale si riempia prima e la CPU secondaria si riempia in seguito. È particolarmente vero se un thread centrale è responsabile dell&#39;allocazione dei buffer di memoria. La soluzione consiste nel modificare il criterio NUMA del thread principale utilizzato per avviare `mongod` eseguire il comando seguente:

```shell
numactl --interleaved=all <mongod> -f config
```

Questo criterio consente di allocare la memoria in modo round robin su tutti i nodi della CPU, garantendo una distribuzione uniforme su tutti i nodi. Non genera l&#39;accesso alla memoria con le massime prestazioni come nei sistemi con più CPU hardware. Circa la metà delle operazioni di memoria sono più lente e sopra il bus, ma `mongod` non è stato scritto per raggiungere NUMA in modo ottimale, quindi è un compromesso ragionevole.

### Problemi NUMA {#numa-issues}

Se il `mongod` processo avviato da una posizione diversa da `/etc/init.d` cartella, è probabile che non sia stato avviato con il criterio NUMA corretto. A seconda del criterio predefinito, possono verificarsi problemi. Il motivo è che i vari programmi di installazione di Linux® Package Manager per MongoDB installano anche un servizio con i file di configurazione in `/etc/init.d` che eseguono il passaggio descritto sopra. Se installi ed esegui MongoDB direttamente da un archivio ( `.tar.gz`), è necessario eseguire manualmente monGod sotto il `numactl` processo.

>[!NOTE]
>
>Per ulteriori informazioni sui criteri NUMA disponibili, consulta [documentazione numactl](https://linux.die.net/man/8/numactl).

Il processo MongoDB si comporta in modo diverso in base a diversi criteri di allocazione:

```

```

* `-membind=<nodes>`
Alloca solo sui nodi elencati. MonGod non alloca memoria sui nodi elencati e potrebbe non utilizzare tutta la memoria disponibile.

* `-cpunodebind=<nodes>`
Esegui solo sui nodi. MonGod viene eseguito solo sui nodi specificati e utilizza solo la memoria disponibile su tali nodi.

* `-physcpubind=<nodes>`
Eseguire solo sulle CPU (core) elencate. MonGod viene eseguito solo sulle CPU elencate e utilizza solo la memoria disponibile su tali CPU.

* `--localalloc`
Alloca sempre memoria sul nodo corrente, ma utilizza tutti i nodi su cui viene eseguito il thread. Se un thread esegue l&#39;allocazione, viene utilizzata solo la memoria disponibile per tale CPU.

* `--preferred=<node>`
Preferisce l’allocazione a un nodo, ma torna ad altri se il nodo preferito è pieno. Per la definizione di un nodo può essere utilizzata la notazione relativa. Inoltre, i thread vengono eseguiti su tutti i nodi.

Alcuni criteri potrebbero causare l&#39;assegnazione di una quantità di RAM inferiore a quella disponibile `mongod` processo. A differenza di MySQL, MongoDB evita attivamente il paging a livello di sistema operativo, e quindi il `mongod` Il processo potrebbe ottenere una quantità inferiore di memoria che appare disponibile.

#### Scambio {#swapping}

A causa dell&#39;utilizzo intensivo della memoria dei database, è necessario disabilitare lo scambio a livello di sistema operativo. Il processo MongoDB evita lo scambio per progettazione.

#### File system remoti {#remote-filesystems}

I file system remoti come NFS non sono consigliati per i file di dati interni di MongoDB (i file di database di processo mongood) , perché introducono troppa latenza. Non confondere con il file system condiviso necessario per l’archiviazione di Oak Blob’s (FileDataStore), dove si consiglia NFS.

#### Leggi tutto {#read-ahead}

Sintonizza Leggi in avanti in modo che, quando si esegue il paging di una pagina utilizzando una lettura casuale, i blocchi non necessari non vengano letti dal disco. Ciò significa un consumo inutile di larghezza di banda di I/O.

### Requisiti Linux® {#linux-requirements}

#### Versioni minime del kernel {#minimum-kernel-versions}

* **2.6.23** per `ext4` file system

* **2.6.25** per `xfs` file system

#### Impostazioni consigliate per i dischi di database {#recommended-settings-for-database-disks}

**Disattiva tempo**

Si consiglia di: `atime` è disattivato per i dischi che contengono i database.

**Impostare l&#39;utilità di pianificazione dischi NOOP**

Effettua le seguenti operazioni:

Innanzitutto, controllare il modulo di pianificazione I/O impostato eseguendo il comando seguente:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se la risposta è `noop`, non c&#39;è altro da fare.

Se NOOP non è il modulo di pianificazione I/O configurato, è possibile modificarlo eseguendo:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Regola il valore di read-ahead**

È consigliabile utilizzare il valore 32 per i dischi in cui vengono eseguiti i database MongoDB. Questo valore ammonta a 16 KB. Puoi impostarlo eseguendo le seguenti operazioni:

```shell
sudo blockdev --setra <value> <device>
```

#### Abilita NTP {#enable-ntp}

Verificare che NTP sia installato e in esecuzione nel computer che ospita i database MongoDB. Ad esempio, puoi installarlo utilizzando Gestione pacchetti yum su un computer CentOS:

```shell
sudo yum install ntp
```

Dopo aver installato e avviato correttamente il daemon NTP, è possibile verificare la differenza di tempo del server nel file di deriva.

#### Disattiva pagine grandi trasparenti {#disable-transparent-huge-pages}

Red Hat® Linux® utilizza un algoritmo di gestione della memoria chiamato Transparent Huge Pages (THP). È consigliabile disattivarla se si utilizza il sistema operativo per i carichi di lavoro del database.

Puoi disattivarla seguendo la procedura seguente:

1. Apri `/etc/grub.conf` nell&#39;editor di testo desiderato.
1. Aggiungi la seguente riga al file grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Infine, verifica se l’impostazione è diventata effettiva eseguendo:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l’output del comando precedente deve essere:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Per ulteriori informazioni sulle pagine di grandi dimensioni trasparenti, consulta [articolo](https://access.redhat.com/solutions/46111).

#### Disattiva NUMA {#disable-numa}

Nella maggior parte delle installazioni in cui è abilitato NUMA, il daemon MongoDB lo disabilita automaticamente se viene eseguito come servizio dal `/etc/init.d` cartella.

In caso contrario, è possibile disattivare NUMA a livello di processo. Per disattivarla, eseguire i comandi seguenti:

```shell
numactl --interleave=all <path_to_process>
```

Dove `<path_to_process>` è la via del processo del mondio.

Quindi, disabilita il recupero delle zone eseguendo:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Modifica le impostazioni massime per il processo mondio {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® consente un controllo configurabile sull&#39;allocazione delle risorse tramite `ulimit` comando. Questa configurazione può essere eseguita su un utente o in base al singolo processo.

Si consiglia di configurare ulimit per il processo mondio in base al [Impostazioni limite consigliate MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Test prestazioni I/O MongoDB {#test-mongodb-i-o-performance}

MongoDB fornisce uno strumento denominato `mongoperf` progettato per testare le prestazioni di I/O. È consigliabile utilizzarlo per testare le prestazioni di tutte le istanze MongoDB che compongono la tua infrastruttura.

Per informazioni su come utilizzare `mongoperf`, visualizzare [Documentazione di MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>Il `mongoperf` è un indicatore delle prestazioni di MongoDB sulla piattaforma su cui viene eseguito. Di conseguenza, i risultati non dovrebbero essere considerati definitivi ai fini del funzionamento di un sistema di produzione.
>
>Per ottenere risultati più precisi, puoi eseguire test complementari con `fio` Strumento Linux®.

**Verifica delle prestazioni di lettura nelle macchine virtuali che compongono la distribuzione**

Dopo aver installato lo strumento, passa alla directory del database MongoDB per eseguire i test. Quindi, avvia il primo test eseguendo `mongoperf`con questa configurazione:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

L’output desiderato deve raggiungere un massimo di due gigabyte al secondo (2 GB/s) e 500.000 IOPS in esecuzione a 32 thread per tutte le istanze MongoDB.

Eseguire un secondo test, questa volta utilizzando file mappati in memoria, impostando `mmf:true` parametro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

L&#39;output del secondo test deve essere considerevolmente superiore al primo, indicando le prestazioni di trasferimento della memoria.

>[!NOTE]
>
>Durante l&#39;esecuzione dei test, controllare le statistiche sull&#39;utilizzo di I/O per le macchine virtuali in questione nel sistema di monitoraggio del sistema operativo. Se indicano valori inferiori al 100% per le letture I/O, potrebbe verificarsi un problema con la macchina virtuale.

**Verificare le prestazioni di scrittura dell’istanza MongoDB primaria**

Quindi, controlla le prestazioni di scrittura I/O dell’istanza MongoDB principale eseguendo il comando `mongoperf` dalla directory del database MongoDB con le stesse impostazioni:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

L’output desiderato dovrebbe essere di 12 megabyte al secondo e raggiungere circa 3000 IOPS, con poche variazioni tra il numero di thread.

## Passaggi per gli ambienti virtualizzati {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se si utilizza WMWare ESX per gestire e implementare gli ambienti virtualizzati, assicurarsi di eseguire le seguenti impostazioni dalla console ESX per supportare l&#39;operazione MongoDB:

1. Disattiva il fumetto della memoria
1. Preallocazione e riserva di memoria per le macchine virtuali che ospitano i database MongoDB
1. Utilizzare il controllo I/O dello storage per allocare un numero sufficiente di I/O al `mongod` processo.
1. Garantire le risorse della CPU dei computer che ospitano MongoDB impostando [Prenotazione CPU](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. Prendere in considerazione l&#39;utilizzo di driver di I/O ParaVirtual. Consulta [articolo della knowledgebase](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Per la documentazione sulla configurazione di MongoDB con Amazon Web Services, consulta [Configurare l’integrazione di AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) articolo sul sito web MongoDB.

## Protezione di MongoDB prima dell’implementazione {#securing-mongodb-before-deployment}

Vedi questo post su [distribuzione sicura di MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) per consigli su come proteggere la configurazione dei database prima della distribuzione.

## Dispatcher {#dispatcher}

### Scelta del sistema operativo per Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Per gestire correttamente l’implementazione di MongoDB, il sistema operativo che ospita Dispatcher deve essere in esecuzione **Apache httpd** **versione 2.4 o successiva.**

Inoltre, assicurati che tutte le librerie utilizzate nella build siano aggiornate per ridurre al minimo le implicazioni di sicurezza.

### Configurazione Dispatcher {#dispatcher-configuration}

Una tipica configurazione di Dispatcher fornisce da dieci a 20 volte di più il throughput delle richieste di una singola istanza AEM.

Poiché Dispatcher è senza stato, può scalare orizzontalmente con facilità. In alcune distribuzioni, agli autori deve essere limitato l’accesso a determinate risorse. È consigliabile utilizzare un’istanza di Dispatcher con le istanze di authoring.

L’esecuzione dell’AEM senza Dispatcher richiede la terminazione SSL e il bilanciamento del carico da parte di un’altra applicazione. È necessario perché le sessioni devono avere affinità con l’istanza AEM sulla quale vengono create, un concetto noto come connessioni permanenti. Il motivo è garantire che gli aggiornamenti al contenuto mostrino una latenza minima.

Controlla la [Documentazione di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per ulteriori informazioni su come configurarlo.

### Configurazione aggiuntiva {#additional-configuration}

#### Connessioni permanenti {#sticky-connections}

Le connessioni permanenti garantiscono che le pagine personalizzate e i dati di sessione di un utente siano tutti composti nella stessa istanza dell’AEM. Questi dati vengono memorizzati nell’istanza, quindi le richieste successive dello stesso utente tornano alla stessa istanza.

Si consiglia di abilitare le connessioni permanenti per tutti i livelli interni che instradano le richieste alle istanze AEM, incoraggiando le richieste successive a raggiungere la stessa istanza AEM. In questo modo è possibile ridurre al minimo la latenza, che in caso di aggiornamento del contenuto tra istanze si nota in altro modo.

#### Scadenza lunga {#long-expires}

Per impostazione predefinita, il contenuto inviato da un Dispatcher AEM ha le intestazioni Last-Modified ed Etag, senza indicazione della scadenza del contenuto. Questo flusso garantisce che l’interfaccia utente riceva sempre la versione più recente della risorsa. Significa anche che il browser esegue un’operazione di GET per verificare se la risorsa è stata modificata. Di conseguenza, può causare più richieste alle quali la risposta HTTP è 304 (Non modificata), a seconda del caricamento della pagina. Per le risorse che non scadono, l’impostazione di un’intestazione Scadenza e la rimozione delle intestazioni Last-Modified e ETag causano la memorizzazione in cache del contenuto. Inoltre, non vengono effettuate ulteriori richieste di aggiornamento fino alla data specificata nell’intestazione Scade.

Tuttavia, l’utilizzo di questo metodo significa che non esiste un modo ragionevole per causare la scadenza della risorsa nel browser prima della scadenza dell’intestazione Scade. Per attenuare questo flusso di lavoro, HtmlClientLibraryManager può essere configurato in modo da utilizzare URL immutabili per le librerie client.

Questi URL non subiranno modifiche. Quando il corpo della risorsa contenuta nell’URL cambia, le modifiche si riflettono nell’URL e garantiscono che il browser richieda la versione corretta della risorsa.

La configurazione predefinita aggiunge un selettore a HtmlClientLibraryManager. In quanto selettore, la risorsa viene memorizzata nella cache di Dispatcher, senza che il selettore sia intatto. Anche questo selettore può essere utilizzato per garantire il corretto comportamento di scadenza. Il selettore predefinito segue `lc-.*?-lc` pattern. Le seguenti direttive di configurazione di Apache httpd garantiscono che tutte le richieste che corrispondono a tale modello vengano soddisfatte con un tempo di scadenza appropriato.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Nessuna sniffatura {#no-sniff}

Se il contenuto viene inviato senza alcun tipo di contenuto, molti browser tentano di indovinare il tipo di contenuto leggendo i primi byte. Questo metodo è chiamato &quot;sniffing&quot;. Lo sniffing apre una vulnerabilità di sicurezza in quanto gli utenti in grado di scrivere nell’archivio potrebbero caricare contenuti dannosi senza alcun tipo di contenuto.

Per questo motivo, è consigliabile aggiungere una `no-sniff` nelle risorse gestite da Dispatcher. Tuttavia, Dispatcher non memorizza in cache le intestazioni. Di conseguenza, significa che qualsiasi contenuto fornito dal file system locale ha il suo tipo di contenuto determinato dalla sua estensione, piuttosto che utilizzare l’intestazione content-type originale dal suo server AEM di origine.

Nessun sniff può essere abilitato in modo sicuro se è noto che l’applicazione web non distribuisce mai le risorse memorizzate in cache senza un tipo di file.

È possibile abilitare No Sniff inclusivamente:

```xml
Header set X-Content-Type-Options "nosniff"
```

Può anche essere abilitato in modo selettivo:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Informativa sulla sicurezza dei contenuti {#content-security-policy}

Le impostazioni predefinite di Dispatcher consentono l’apertura di Criteri sulla sicurezza dei contenuti, noti anche come CSP. Queste impostazioni consentono a una pagina di caricare risorse da tutti i domini soggetti ai criteri predefiniti della sandbox del browser.

È opportuno limitare il luogo in cui le risorse possono essere caricate da per evitare di caricare il codice nel motore JavaScript da server esterni non attendibili o non verificati.

I CSP consentono di perfezionare i criteri. Tuttavia, in un’applicazione complessa, le intestazioni CSP devono essere sviluppate con cautela, in quanto i criteri troppo restrittivi possono interrompere parti dell’interfaccia utente.

>[!NOTE]
>
>Per ulteriori informazioni su come funziona, consulta [Pagina OWASP sull&#39;informativa sulla sicurezza dei contenuti](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Ridimensionamento {#sizing}

Per ulteriori informazioni sul dimensionamento, vedere [Linee guida per il dimensionamento dell&#39;hardware](/help/managing/hardware-sizing-guidelines.md).

### Ottimizzazione delle prestazioni di MongoDB {#mongodb-performance-optimization}

Per informazioni generiche sulle prestazioni di MongoDB, consulta [Analisi delle prestazioni di MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitazioni note {#known-limitations}

### Installazioni simultanee {#concurrent-installations}

Sebbene l’uso simultaneo di più istanze AEM con un singolo database sia supportato da MongoMK, le installazioni simultanee non lo sono.

Per risolvere il problema, assicurarsi di eseguire prima l&#39;installazione con un singolo membro e aggiungere gli altri dopo che l&#39;installazione del primo è stata completata.

### Lunghezza nome pagina {#page-name-length}

Se l’AEM è in esecuzione in un’implementazione di MongoMK persistence manager, [i nomi delle pagine non possono superare i 150 caratteri.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>Consulta la [Documentazione di MongoDB](https://docs.mongodb.com/manual/reference/limits/) così potrai acquisire familiarità con le limitazioni e le soglie note di MongoDB.
