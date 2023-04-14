---
title: Adobe Experience Manager con MongoDB
description: Scopri le attività e le considerazioni necessarie per una corretta implementazione di Adobe Experience Manager con MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 0%

---

# Adobe Experience Manager con MongoDB{#aem-with-mongodb}

Questo articolo mira a migliorare le conoscenze sulle attività e sulle considerazioni necessarie per implementare correttamente AEM (Adobe Experience Manager) con MongoDB.

Per ulteriori informazioni relative alla distribuzione, consulta la [Implementazione e manutenzione](/help/sites-deploying/deploy.md) sezione della documentazione.

## Quando utilizzare MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB viene in genere utilizzato per supportare AEM distribuzioni di authoring in cui è soddisfatto uno dei seguenti criteri:

* più di 1000 utenti unici al giorno;
* Più di 100 utenti simultanei;
* Elevati volumi di modifiche della pagina;
* Rollout o attivazioni di grandi dimensioni.

I criteri di cui sopra sono solo per le istanze dell’autore e non per eventuali istanze di pubblicazione basate su TarMK. Il numero di utenti si riferisce agli utenti autenticati, in quanto le istanze dell’autore non consentono l’accesso non autenticato.

Se i criteri non sono soddisfatti, si consiglia una distribuzione TarMK attiva/in standby per risolvere il problema della disponibilità. In genere, MongoDB dovrebbe essere considerato in situazioni in cui i requisiti di scalabilità sono più di quanto è possibile ottenere con un singolo elemento hardware.

>[!NOTE]
>
>Ulteriori informazioni sul dimensionamento delle istanze dell’autore e sulla definizione degli utenti simultanei sono disponibili nella sezione [Linee guida per il dimensionamento dell&#39;hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Distribuzione minima MongoDB per AEM {#minimal-mongodb-deployment-for-aem}

Di seguito è riportata una distribuzione minima per AEM su MongoDB. Per semplicità, i componenti terminazione SSL e proxy HTTP sono stati generalizzati. Si compone di un singolo set di repliche MongoDB, con uno primario e due secondari.

![chlimage_1-4](assets/chlimage_1-4.png)

Una distribuzione minima richiede tre `mongod` istanze configurate come set di replica. Un&#39;istanza viene eletta primaria con le altre istanze come secondari, con l&#39;elezione gestita da `mongod`. Ad ogni istanza è allegato un disco locale. Il cluster può quindi supportare il carico, si consiglia un throughput minimo di 12 MB al secondo con più di 3000 operazioni di I/O al secondo (IOPS).

Gli autori AEM sono collegati al `mongod` istanze, con ogni autore AEM che si connette a tutti e tre `mongod` istanze. Le scritture vengono inviate al principale e le letture possono essere lette da una qualsiasi delle istanze. Il traffico viene distribuito in base al caricamento di un’istanza di Dispatcher a una qualsiasi delle istanze di authoring AEM attive. L’archivio dati Oak è un `FileDataStore`, e il monitoraggio MongoDB viene fornito da MMS o MongoDB Ops Manager a seconda della posizione della distribuzione. Il livello del sistema operativo e il monitoraggio del registro sono forniti da soluzioni di terze parti come Splunk o Ganglia.

In questa implementazione, tutti i componenti sono necessari per una corretta implementazione. Qualsiasi componente mancante lascia l’implementazione non funzionante.

### Sistemi operativi {#operating-systems}

Per un elenco dei sistemi operativi supportati per AEM 6, consulta [Pagina Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Ambienti {#environments}

Sono supportati gli ambienti virtualizzati a condizione che vi sia una buona comunicazione tra i diversi team tecnici che eseguono il progetto. Questo supporto include il team che esegue AEM, il team proprietario del sistema operativo e il team che gestisce l&#39;infrastruttura virtualizzata.

Esistono requisiti specifici relativi alla capacità di I/O delle istanze MongoDB che devono essere gestiti dal team che gestisce l’ambiente virtualizzato. Se il progetto utilizza un’implementazione cloud, come Amazon Web Services, è necessario eseguire il provisioning delle istanze con capacità e coerenza di I/O sufficienti per supportare le istanze MongoDB. In caso contrario, i processi MongoDB e l&#39;archivio Oak si esibiscono in modo inaffidabile ed errato.

Negli ambienti virtualizzati, MongoDB richiede configurazioni di I/O e VM specifiche per garantire che il motore di storage di MongoDB non sia paralizzato dai criteri di allocazione delle risorse VMWare. Un’implementazione di successo garantisce che non ci siano barriere tra i vari team e che tutti siano registrati per fornire le prestazioni richieste.

## Considerazioni sull&#39;hardware {#hardware-considerations}

### Archiviazione {#storage}

Per ottenere il throughput di lettura e scrittura per le migliori prestazioni senza la necessità di scalabilità orizzontale prematura, MongoDB generalmente richiede lo storage SSD o lo storage con prestazioni equivalenti a SSD.

### RAM {#ram}

Le versioni 2.6 e 3.0 di MongoDB che utilizzano il motore di storage MAP richiedono che il set di lavoro del database e i relativi indici si inseriscano nella RAM.

Una quantità insufficiente di RAM riduce notevolmente le prestazioni. Le dimensioni del set di lavoro e del database dipendono fortemente dall&#39;applicazione. Mentre alcune stime possono essere fatte, il modo più affidabile per determinare la quantità di RAM richiesta è costruire l&#39;applicazione AEM e il carico di prova.

Per facilitare il processo di test del carico, è possibile ipotizzare il seguente rapporto tra il set di lavoro e la dimensione totale del database:

* 1:10 per lo storage SSD
* 1:3 per lo storage su hard disk

Questi rapporti indicano che per le distribuzioni SSD è necessario 200 GB di RAM per un database da 2 TB.

Mentre le stesse limitazioni si applicano al motore di storage WiredTiger in MongoDB 3.0, la correlazione tra il set di lavoro, la RAM e gli errori di pagina non è così forte. WiredTiger non utilizza la mappatura della memoria allo stesso modo del motore di storage MAP.

>[!NOTE]
>
>Adobe consiglia di utilizzare il motore di storage WiredTiger per le distribuzioni AEM 6.1 che utilizzano MongoDB 3.0.

### Archiviazione dati {#data-store}

A causa delle limitazioni del set di lavoro MongoDB, si consiglia di mantenere l&#39;archivio dati indipendente da MongoDB. Nella maggior parte degli ambienti, un `FileDataStore` utilizzare un NAS disponibile per tutte le istanze AEM. Nelle situazioni in cui viene utilizzato Amazon Web Services, è inoltre disponibile un `S3 DataStore`. Se per qualsiasi motivo l&#39;archivio dati viene mantenuto in MongoDB, la dimensione dell&#39;archivio dati deve essere aggiunta alla dimensione totale del database e i calcoli del set di lavoro devono essere adeguati in modo appropriato. Questo dimensionamento può significare il provisioning di più RAM per mantenere le prestazioni senza errori di pagina.

## Monitoraggio {#monitoring}

Il monitoraggio è essenziale per una corretta attuazione del progetto. Con sufficiente conoscenza, è possibile eseguire AEM su MongoDB senza monitoraggio. Tuttavia, tale conoscenza si trova normalmente in ingegneri specializzati per ogni sezione della distribuzione.

Questa conoscenza specializzata in genere coinvolge un ingegnere R&amp;S che lavora su Apache Oak Core e uno specialista MongoDB.

Senza monitoraggio a tutti i livelli, per diagnosticare i problemi è necessaria una conoscenza dettagliata della base di codice. Con il monitoraggio attivo e l&#39;orientamento appropriato sulle principali statistiche, i team di implementazione possono reagire in modo appropriato alle anomalie.

Mentre è possibile utilizzare strumenti della riga di comando per ottenere una rapida istantanea del funzionamento di un cluster, farlo in tempo reale su molti host è quasi impossibile. Gli strumenti della riga di comando raramente forniscono informazioni cronologiche oltre pochi minuti e non consentono mai la correlazione tra diversi tipi di metriche. Un breve periodo di background lento `mongod` La sincronizzazione richiede un notevole sforzo manuale per correlarsi a livelli di attesa di I/O o di scrittura eccessivi a una risorsa di archiviazione condivisa da una macchina virtuale apparentemente non connessa.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager è un servizio gratuito offerto da MongoDB che consente il monitoraggio e la gestione delle istanze MongoDB. Fornisce una visualizzazione delle prestazioni e dello stato del cluster MongoDB in tempo reale. Gestisce sia le istanze cloud che quelle ospitate privatamente, a condizione che l’istanza possa raggiungere il server di monitoraggio di Cloud Manager.

Richiede un agente installato sull&#39;istanza MongoDB che si connette al server di monitoraggio. Ci sono tre livelli dell&#39;agente:

* Un agente di automazione in grado di automatizzare completamente tutto sul server MongoDB,
* Un agente di monitoraggio in grado di monitorare `mongod` istanza,
* Agente di backup in grado di eseguire backup pianificati dei dati.

Anche se l&#39;utilizzo di Cloud Manager per la manutenzione automatizzata di un cluster MongoDB semplifica molte delle attività di routine, non è necessario e nemmeno lo utilizza per il backup. Quando si sceglie Cloud Manager per il monitoraggio, è comunque necessario effettuare il monitoraggio.

Per ulteriori informazioni su MongoDB Cloud Manager, consulta la [Documentazione MongoDB](https://docs.cloud.mongodb.com/).

### Gestione Ops MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager è lo stesso software di MongoDB Cloud Manager. Una volta registrato, Ops Manager può essere scaricato e installato localmente in un centro dati privato o su qualsiasi altro computer portatile o desktop. Utilizza un database MongoDB locale per memorizzare i dati e comunica allo stesso modo di Cloud Manager con i server gestiti. Se si dispone di criteri di sicurezza che vietano un agente di monitoraggio, MongoDB Ops Manager deve essere utilizzato.

### Monitoraggio del sistema operativo {#operating-system-monitoring}

È necessario il monitoraggio a livello di sistema operativo per eseguire un cluster MongoDB AEM.

Ganglia è un buon esempio di tale sistema e fornisce un&#39;immagine sulla gamma e sui dettagli delle informazioni necessarie che vanno oltre le metriche di integrità di base come la CPU, la media di carico e lo spazio libero su disco. Per diagnosticare i problemi, sono necessarie informazioni di livello inferiore come i livelli del pool entropia, l&#39;attesa I/O della CPU, prese nello stato FIN_WAIT2.

### Aggregazione del registro {#log-aggregation}

Con un cluster di più server, l&#39;aggregazione centrale dei log è un requisito per un sistema di produzione. Software come Splunk supporta l&#39;aggregazione dei log e consente ai team di analizzare i pattern di comportamento dell&#39;applicazione senza dover raccogliere manualmente i log.

## Elenchi di controllo {#checklists}

Questa sezione descrive vari passaggi da seguire per garantire che le distribuzioni AEM e MongoDB siano configurate correttamente prima di implementare il progetto.

### Rete {#network}

1. In primo luogo, assicurati che tutti gli host abbiano una voce DNS
1. Tutti gli host devono essere risolvibili dalla voce DNS da tutti gli altri host router
1. Tutti gli host MongoDB sono indirizzabili da tutti gli altri host MongoDB nello stesso cluster
1. Gli host MongoDB possono indirizzare i pacchetti a MongoDB Cloud Manager e agli altri server di monitoraggio
1. AEM server possono indirizzare i pacchetti a tutti i server MongoDB
1. La latenza del pacchetto tra qualsiasi server AEM e qualsiasi server MongoDB è inferiore a due millisecondi, senza perdita di pacchetti e con una distribuzione standard di un millisecondo o inferiore.
1. Assicurati che non ci siano più di due passaggi tra un AEM e un server MongoDB
1. Non ci sono più di due hop tra due server MongoDB
1. Non ci sono router superiori a OSI di livello 3 tra i server principali (MongoDB o AEM o qualsiasi combinazione).
1. Se viene utilizzato il trunking VLAN o qualsiasi forma di tunneling di rete, deve rispettare i controlli di latenza dei pacchetti.

### Configurazione AEM {#aem-configuration}

#### Configurazione archivio nodi {#node-store-configuration}

Le istanze AEM devono essere configurate per utilizzare AEM con MongoMK. La base dell&#39;implementazione MongoMK in AEM è Document Node Store.

Per ulteriori informazioni su come configurare gli archivi dei nodi, vedi [Configurazione di Node Stores e Data Store in AEM](/help/sites-deploying/data-store-config.md).

Di seguito è riportato un esempio di configurazione dell&#39;archivio dei nodi del documento per una distribuzione minima di MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Dove:

* `mongodburi`
È AEM connettersi al server MongoDB. Vengono effettuate connessioni a tutti i membri noti del set di repliche predefinito. Se viene utilizzato MongoDB Cloud Manager, la sicurezza del server è abilitata. Pertanto, la stringa di connessione deve contenere un nome utente e una password appropriati. Le versioni non aziendali di MongoDB supportano solo l’autenticazione tramite nome utente e password. Per ulteriori informazioni sulla sintassi della stringa di connessione, consulta la [documentazione](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nome del database. Il valore predefinito per AEM è 
`aem-author`.

* `customBlobStore`
Se la distribuzione memorizza i binari nel database, fanno parte del set di lavoro. Per questo motivo, si consiglia di non archiviare binari all&#39;interno di MongoDB, preferendo un datastore alternativo come un 
`FileSystem` archivio dati su un NAS.

* `cache`
Dimensione della cache in megabyte. Questo spazio è distribuito tra le varie cache utilizzate nel 
`DocumentNodeStore`. Il valore predefinito è 256 MB. Tuttavia, le prestazioni di lettura Oak traggono vantaggio da una cache più grande.

* `blobCacheSize`
I BLOB utilizzati di frequente possono essere memorizzati nella cache da AEM per evitare di recuperarli dall’archivio dati. Questo ha un maggiore impatto sulle prestazioni, soprattutto quando si memorizzano i BLOB nel database MongoDB. Tutti gli archivi dati basati su file system beneficiano della cache del disco a livello di sistema operativo.

#### Configurazione archivio dati {#data-store-configuration}

L&#39;archivio dati viene utilizzato per memorizzare file di dimensioni superiori a una soglia. Al di sotto di tale soglia, i file vengono memorizzati come proprietà all&#39;interno dell&#39;archivio dei nodi del documento. Se la `MongoBlobStore` viene utilizzata, viene creata una raccolta dedicata in MongoDB per memorizzare i BLOB. Questa collezione contribuisce al lavoro del `mongod` e richiede che `mongod` dispone di più RAM per evitare problemi di prestazioni. Per questo motivo, la configurazione consigliata è quella di evitare il `MongoBlobStore` per le distribuzioni di produzione e l&#39;utilizzo `FileDataStore` supportato da un NAS condiviso tra tutte le istanze AEM. Poiché la cache a livello di sistema operativo è efficiente nella gestione dei file, la dimensione minima di un file su disco deve essere impostata in prossimità della dimensione del blocco del disco. In questo modo si garantisce un uso efficiente del file system e molti piccoli documenti non contribuiscono eccessivamente al funzionamento del `mongod` istanza.

Di seguito è riportata una tipica configurazione dell&#39;archivio dati per una distribuzione AEM minima con MongoDB:

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
Dimensioni in byte. I binari di dimensioni inferiori o uguali a queste vengono memorizzati con l&#39;archivio dei nodi del documento. Invece di memorizzare l’ID del BLOB, viene memorizzato il contenuto del binario. Con binari di dimensioni maggiori di queste, l&#39;ID del binario viene memorizzato come proprietà del documento nell&#39;insieme nodes. E, il corpo del binario è memorizzato nel 
`FileDataStore` su disco. 4096 byte è una dimensione tipica del blocco del file system.

* `path`
Percorso della directory principale dell&#39;archivio dati. Per una distribuzione MongoMK, questo percorso deve essere un file system condiviso disponibile per tutte le istanze AEM. In genere viene utilizzato un server NAS (Network Attached Storage). Per implementazioni cloud come Amazon Web Services, la 
`S3DataFileStore` è disponibile anche.

* `cacheSizeInMB`
Dimensione totale della cache binaria in Megabyte. Viene utilizzato per memorizzare in cache i binari minori del 
`maxCacheBinarySize` impostazione.

* `maxCachedBinarySize`
Dimensione massima in byte di un binario memorizzato nella cache binaria. Se si utilizza un archivio dati basato su file system, si sconsiglia di utilizzare valori elevati per la cache del Data Store, in quanto i binari sono già memorizzati nella cache dal sistema operativo.

#### Disabilitazione dell’hint di query {#disabling-the-query-hint}

Si consiglia di disabilitare l’hint di query inviato con tutte le query aggiungendo la proprietà `-Doak.mongo.disableIndexHint=true` quando cominci AEM. In questo modo MongoDB calcola l&#39;indice più appropriato da utilizzare sulla base di statistiche interne.

Se l’hint di query non è disabilitato, qualsiasi ottimizzazione delle prestazioni degli indici non ha alcun impatto sulle prestazioni di AEM.

#### Abilita cache persistente per MongoMK {#enable-persistent-cache-for-mongomk}

Si consiglia di abilitare una configurazione della cache persistente per le distribuzioni MongoDB, per massimizzare la velocità per gli ambienti con elevate prestazioni di lettura I/O. Per ulteriori dettagli, consulta la sezione [Documentazione di Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Ottimizzazioni del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Supporto del sistema operativo {#operating-system-support}

MongoDB 2.6 utilizza un motore di storage mappato in memoria sensibile ad alcuni aspetti della gestione a livello di sistema operativo tra RAM e disco. La query e la lettura delle prestazioni dell&#39;istanza MongoDB si basano sull&#39;evitare o eliminare le operazioni di I/O lente spesso definite errori di pagina. Questi problemi sono errori di pagina che si applicano al `mongod` in particolare. Non confondere con errori di pagina a livello di sistema operativo.

Per un funzionamento rapido, il database MongoDB dovrebbe accedere solo ai dati già presenti nella RAM. I dati a cui deve accedere sono costituiti da indici e dati. Questa raccolta di indici e dati si chiama set di lavoro. Se il set di lavoro è più grande della RAM disponibile MongoDB deve inserire i dati in dal disco con un costo di I/O, eliminando altri dati già in memoria. Se lo sgombero causa il ricaricamento dei dati dal disco, gli errori di pagina dominano e le prestazioni si degradano. Se il set di lavoro è dinamico e variabile, vengono generati più errori di pagina per supportare le operazioni.

MongoDB funziona su diversi sistemi operativi, tra cui un&#39;ampia varietà di sapori Linux®, Windows e macOS. Vedi [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) per ulteriori dettagli. A seconda della scelta del sistema operativo, MongoDB ha diversi consigli a livello di sistema operativo. Sono documentati in [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) qui riassunto per comodità.

#### Linux® {#linux}

* Disattivare gli hugepage trasparenti e lo sbrinamento. Vedi [Impostazioni trasparenti per le pagine grandi](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) per ulteriori informazioni.
* [Regolare le impostazioni del readahead](https://docs.mongodb.com/manual/administration/production-notes/#readahead) sui dispositivi che memorizzano i file di database in modo da adattarli al caso d&#39;uso.

   * Per il motore di storage MMAPv1, se il set di lavoro è più grande della RAM disponibile e il modello di accesso al documento è casuale, è consigliabile abbassare il readahead a 32 o 16. Valuta diverse impostazioni in modo da trovare un valore ottimale che massimizza la memoria residente e abbassa il numero di errori di pagina.
   * Per il motore di storage WiredTiger, impostare readahead su 0 indipendentemente dal tipo di supporto di storage (filatura, SSD e così via). In generale, utilizza l’impostazione di lettura consigliata a meno che il test non mostri un vantaggio misurabile, ripetibile e affidabile con un valore di lettura più elevato. [Supporto professionale MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) può fornire consigli e indicazioni sulle configurazioni precedenti a zero readahead.

* Disattiva lo strumento sintonizzato se esegui RHEL 7 / CentOS 7 in un ambiente virtuale.
* Quando RHEL 7/CentOS 7 viene eseguito in un ambiente virtuale, lo strumento sintonizzato richiama automaticamente un profilo di prestazioni derivato dal throughput di prestazioni, che imposta automaticamente le impostazioni del programma readahead a 4 MB. Questa impostazione può influire negativamente sulle prestazioni.
* Utilizzare i programmatori di dischi noop o di scadenza per le unità SSD.
* Utilizzare lo strumento di pianificazione dei dischi noop per le unità virtualizzate nelle VM guest.
* Disattiva NUMA o imposta `vm.zone_reclaim_mode` a 0 ed esegui [mondio](https://docs.mongodb.com/manual/administration/production-notes/#readahead) istanze con interfoliazione dei nodi. Vedi: [Hardware MongoDB e NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) per ulteriori informazioni.

* Regolare i valori limite sull&#39;hardware in modo che siano adatti al tuo caso d&#39;uso. Se multipli [mondio](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongo](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) le istanze vengono eseguite con lo stesso utente, ridimensiona di conseguenza i valori di limite. Vedi: [Impostazioni di UNIX® ulimit](https://docs.mongodb.com/manual/reference/ulimit/) per ulteriori informazioni.

* Usa il tempo di attesa per il [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) punto di montaggio.
* Configura un numero sufficiente di handle di file (fs.file-max), un limite di kernel pid (kernel.pid_max) e un massimo di thread per processo (kernel.threads-max) per la distribuzione. Per i sistemi di grandi dimensioni, i seguenti valori forniscono un buon punto di partenza:

   * fs.file-max valore di 98000,
   * kernel.pid_max valore di 64000,
   * andkernel.threads-max valore di 64000

* Assicurati che nel sistema sia configurato lo spazio di scambio. Per ulteriori informazioni sulle dimensioni appropriate, consulta la documentazione del sistema operativo in uso.
* Assicurati che il blocco TCP predefinito del sistema sia impostato correttamente. Un valore di 300 fornisce spesso prestazioni migliori per i set di repliche e i cluster condivisi. Vedi: [Il tempo di mantenimento TCP influisce sulle implementazioni MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) nelle Domande frequenti per ulteriori informazioni.

#### Windows {#windows}

* Disabilitare gli aggiornamenti NTFS &quot;last access time&quot;. Questa impostazione è analoga alla disattivazione del tempo su sistemi simili a Unix.

### Tigre cablata {#wiredtiger}

A partire da MongoDB 3.2 il motore di storage predefinito per MongoDB è il motore di storage WiredTiger. Questo motore fornisce alcune funzioni robuste e scalabili che lo rendono molto più adatto per tutti i carichi di lavoro generali del database. Le sezioni seguenti descrivono queste funzioni.

#### Condivisa a livello di documento {#document-level-concurrency}

WiredTiger utilizza il controllo della concorrenza a livello di documento per le operazioni di scrittura. Di conseguenza, più client possono modificare contemporaneamente diversi documenti di una raccolta.

Per la maggior parte delle operazioni di lettura e scrittura, WiredTiger utilizza un controllo della concorrenza ottimistico. WiredTiger utilizza solo i blocchi intento a livello globale, di database e di raccolta. Quando il motore di archiviazione rileva i conflitti tra due operazioni, si verifica un conflitto di scrittura che causa la ripetizione trasparente di MongoDB dell&#39;operazione. Alcune operazioni globali, generalmente di breve durata che coinvolgono più database, richiedono ancora un blocco globale a livello di istanza.

Alcune altre operazioni, come il rilascio di una raccolta, richiedono ancora un blocco esclusivo del database.

#### Istantanee e checkpoint {#snapshots-and-checkpoints}

WiredTiger utilizza MultiVersion Concurrency Control (MVCC). All&#39;inizio di un&#39;operazione, WiredTiger fornisce un&#39;istantanea point-in-time dei dati relativi alla transazione. Un’istantanea presenta una visualizzazione coerente dei dati in memoria.

Durante la scrittura su disco, WiredTiger scrive su disco tutti i dati di un&#39;istantanea in modo coerente in tutti i file di dati. L&#39;ora [durevole](https://docs.mongodb.com/manual/reference/glossary/#term-durable) i dati fungono da punto di controllo nei file di dati. Il punto di controllo assicura che i file di dati siano coerenti fino all’ultimo punto di controllo incluso. In altre parole, i checkpoint possono fungere da punti di ripristino.

MongoDB configura WiredTiger per creare punti di controllo (vale a dire, scrivere i dati snapshot su disco) a intervalli di 60 secondi o 2 GB di dati del journal.

Durante la scrittura di un nuovo checkpoint, il checkpoint precedente è ancora valido. Di conseguenza, anche se MongoDB termina o rileva un errore durante la scrittura di un nuovo checkpoint, al riavvio MongoDB può recuperare dall&#39;ultimo checkpoint valido.

Il nuovo checkpoint diventa accessibile e permanente quando la tabella dei metadati di WiredTiger viene aggiornata in modo automatico per fare riferimento al nuovo checkpoint. Una volta che il nuovo checkpoint è accessibile, WiredTiger libera le pagine dai vecchi checkpoint.

Utilizzando WiredTiger, anche senza [inserimento nel journal](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB può recuperare dall&#39;ultimo checkpoint; tuttavia, per recuperare le modifiche apportate dopo l’ultimo checkpoint, esegui con [inserimento nel journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger utilizza una combinazione di accesso alle transazioni in scrittura con [checkpoint](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) per garantire la durabilità dei dati.

La rivista WiredTiger persiste tutte le modifiche ai dati tra i punti di controllo. Se MongoDB esce tra punti di controllo, utilizza il giornale di registrazione per riprodurre tutti i dati modificati dall&#39;ultimo punto di controllo. Per informazioni sulla frequenza con cui MongoDB scrive i dati del giornale su disco, vedere [Processo di registrazione](https://docs.mongodb.com/manual/core/journaling/#journal-process).

Il journal WiredTiger viene compresso utilizzando [schifoso](https://docs.mongodb.com/manual/core/journaling/#journal-process) libreria di compressione. Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare la [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) impostazione.

Vedi [Viaggio con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>La dimensione minima del record del registro per WiredTiger è di 128 byte. Se un record di log è pari o inferiore a 128 byte, WiredTiger non comprime tale record.
>
>È possibile disabilitare il journal impostando [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) su false, che può ridurre il sovraccarico della manutenzione del giornale di registrazione.
>
>Per [indipendente](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) Se non si utilizza il giornale di registrazione, si perdono alcune modifiche ai dati quando MongoDB esce in modo imprevisto tra i punti di controllo. Per i membri di [set di repliche](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), il processo di replica può fornire sufficienti garanzie di durata.

#### Compressione {#compression}

Con WiredTiger, MongoDB supporta la compressione per tutte le raccolte e gli indici. La compressione riduce al minimo l&#39;utilizzo dello storage a scapito della CPU aggiuntiva.

Per impostazione predefinita, WiredTiger utilizza la compressione dei blocchi con [schifoso](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) libreria di compressione per tutte le raccolte e [compressione prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) per tutti gli indici.

Per le raccolte, blocca la compressione con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) è disponibile anche. Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare la [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) impostazione.

Per gli indici, disabilitare [compressione prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), utilizza [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) impostazione.

Le impostazioni di compressione sono configurabili anche per raccolta e per indice durante la creazione di raccolte e indici. Vedi [Specificare le opzioni del motore di archiviazione](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) e [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) opzione .

Per la maggior parte dei carichi di lavoro, le impostazioni di compressione predefinite bilanciano l&#39;efficienza dello storage e i requisiti di elaborazione.

Anche il journal WiredTiger è compresso per impostazione predefinita. Per informazioni sulla compressione del journal, consulta [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Utilizzo della memoria {#memory-use}

Con WiredTiger, MongoDB utilizza sia la cache interna di WiredTiger che la cache del filesystem.

A partire dalla versione 3.4, la cache interna di WiredTiger, per impostazione predefinita, utilizza la dimensione maggiore di:

* 50% di RAM meno 1 GB, o
* 256 MB

Per impostazione predefinita, WiredTiger utilizza la compressione a blocchi Snappy per tutte le raccolte e la compressione a prefisso per tutti gli indici. I valori predefiniti di compressione sono configurabili a livello globale e possono essere impostati anche su base per raccolta e per indice durante la creazione di raccolte e indici.

Vengono utilizzate rappresentazioni diverse per i dati nella cache interna di WiredTiger rispetto al formato su disco:

* I dati nella cache del file system sono gli stessi del formato su disco, compresi i vantaggi di qualsiasi compressione per i file di dati. La cache del filesystem viene utilizzata dal sistema operativo per ridurre l&#39;I/O del disco.

Gli indici caricati nella cache interna WiredTiger hanno una rappresentazione dei dati diversa rispetto al formato su disco, ma possono comunque sfruttare la compressione dei prefisso dell&#39;indice per ridurre l&#39;utilizzo della RAM.

La compressione del prefisso dell’indice deduplica i prefissi comuni dai campi indicizzati.

I dati di raccolta nella cache interna di WiredTiger non sono compressi e utilizzano una rappresentazione diversa dal formato su disco. La compressione a blocchi può fornire un notevole risparmio di spazio su disco, ma i dati devono essere non compressi per essere manipolati dal server.

Tramite la cache del filesystem, MongoDB utilizza automaticamente tutta la memoria libera che non viene utilizzata dalla cache WiredTiger o da altri processi.

Per regolare le dimensioni della cache interna di WiredTiger, vedi [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evita di aumentare la dimensione della cache interna di WiredTiger al di sopra del valore predefinito.

### NUMA {#numa}

NUMA (Non-Uniform Memory Access) consente a un kernel di gestire il modo in cui la memoria viene mappata ai core del processore. Anche se questo processo tenta di rendere più veloce l&#39;accesso alla memoria per i core garantendo che siano in grado di accedere ai dati richiesti, NUMA interferisce con l&#39;introduzione di una latenza aggiuntiva, in quanto le letture non possono essere previste. Di conseguenza, NUMA deve essere disabilitato per `mongod` su tutti i sistemi operativi capaci.

In sostanza, in un&#39;architettura NUMA la memoria è connessa alle CPU e le CPU sono collegate a un bus. In un’architettura SMP o UMA, la memoria è connessa al bus e condivisa dalle CPU. Quando un thread alloca memoria su una CPU NUMA, alloca in base a un criterio. L&#39;impostazione predefinita consiste nell&#39;allocare la memoria collegata alla CPU locale del thread a meno che non vi sia spazio libero, a quel punto utilizza la memoria di una CPU gratuita a costi più elevati. Una volta allocata, la memoria non si sposta tra le CPU. L&#39;allocazione viene eseguita da un criterio ereditato dal thread padre, che in ultima analisi è il thread che ha avviato il processo.

In molti database che vedono il computer come un&#39;architettura di memoria multicore uniforme, questo scenario porta alla CPU iniziale piena prima e il riempimento secondario della CPU più tardi. È particolarmente vero se un thread centrale è responsabile dell&#39;allocazione dei buffer di memoria. La soluzione consiste nel modificare il criterio NUMA del thread principale utilizzato per avviare il `mongod` eseguire il comando seguente:

```shell
numactl --interleaved=all <mongod> -f config
```

Questo criterio assegna la memoria in modo approssimativo su tutti i nodi della CPU, garantendo una distribuzione uniforme su tutti i nodi. Non genera l&#39;accesso alla memoria con le prestazioni più elevate come in sistemi con più hardware della CPU. Circa la metà delle operazioni di memoria sono più lente e oltre il bus, ma `mongod` non è stato scritto per raggiungere NUMA in modo ottimale, quindi è un compromesso ragionevole.

### Problemi NUMA {#numa-issues}

Se la `mongod` il processo viene avviato da una posizione diversa da `/etc/init.d` cartella, è probabile che non sia stato avviato con il criterio NUMA corretto. A seconda del criterio predefinito, possono sorgere problemi. Il motivo è che i vari installatori di Linux® Package Manager per MongoDB installano anche un servizio con file di configurazione in `/etc/init.d` che eseguono il passaggio descritto sopra. Se installi ed esegui MongoDB direttamente da un archivio ( `.tar.gz`), è necessario eseguire manualmente mongod sotto il `numactl` processo.

>[!NOTE]
>
>Per ulteriori informazioni sui criteri NUMA disponibili, consultare la [documentazione numerica](https://linux.die.net/man/8/numactl).

Il processo MongoDB si comporta in modo diverso in base a diversi criteri di allocazione:

```

```

* `-membind=<nodes>`
Alloca solo sui nodi elencati. Mongod non alloca memoria sui nodi elencati e potrebbe non utilizzare tutta la memoria disponibile.

* `-cpunodebind=<nodes>`
Esegui solo sui nodi. Mongod viene eseguito solo sui nodi specificati e utilizza solo la memoria disponibile su tali nodi.

* `-physcpubind=<nodes>`
Esegui solo sulle CPU (core) elencate. Mongod viene eseguito solo sulle CPU elencate e utilizza solo la memoria disponibile su tali CPU.

* `--localalloc`
Alloca sempre la memoria sul nodo corrente, ma utilizza tutti i nodi su cui viene eseguito il thread. Se un thread esegue l&#39;allocazione, viene utilizzata solo la memoria disponibile per tale CPU.

* `--preferred=<node>`
Preferisce l&#39;allocazione a un nodo, ma torna ad altri se il nodo preferito è pieno. È possibile utilizzare una notazione relativa per definire un nodo. Inoltre, i thread vengono eseguiti su tutti i nodi.

Alcune delle politiche possono comportare una quantità inferiore a tutta la RAM disponibile assegnata al `mongod` processo. A differenza di MySQL, MongoDB evita attivamente il paging a livello di sistema operativo, e quindi il `mongod` Il processo potrebbe ottenere meno memoria disponibile.

#### Scambio {#swapping}

A causa della natura intensiva di memoria dei database, lo scambio a livello di sistema operativo deve essere disattivato. Il processo MongoDB evita lo scambio progettuale.

#### File system remoti {#remote-filesystems}

I file system remoti come NFS non sono consigliati per i file di dati interni di MongoDB (i file di database del processo mongod), perché introducono troppa latenza. Non confondere con il file system condiviso necessario per l&#39;archiviazione di Oak Blob (FileDataStore), dove è consigliato NFS.

#### Leggi tutto {#read-ahead}

Ottimizza la lettura in anticipo in modo che quando una pagina viene inserita tramite una lettura casuale, i blocchi non necessari non vengano letti dal disco. Tali risultati implicano un consumo non necessario della larghezza di banda I/O.

### Requisiti di Linux® {#linux-requirements}

#### Versioni minime del kernel {#minimum-kernel-versions}

* **2.6.23** per `ext4` filesystems

* **2.6.25** per `xfs` filesystems

#### Impostazioni consigliate per i dischi di database {#recommended-settings-for-database-disks}

**Disattiva tempo**

Si consiglia di: `atime` è disattivato per i dischi che contengono i database.

**Impostare lo scheduler del disco NOOP**

Effettua le seguenti operazioni:

Per prima cosa, controlla lo scheduler I/O impostato eseguendo il seguente comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se la risposta è `noop`Non c&#39;è altro da fare.

Se NOOP non è lo scheduler I/O configurato, puoi modificarlo eseguendo:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Regolare il valore letto avanti**

Si consiglia di utilizzare un valore di 32 per i dischi in cui vengono eseguiti i database MongoDB. Questo valore ammonta a 16 KB. Puoi impostarlo eseguendo le seguenti operazioni:

```shell
sudo blockdev --setra <value> <device>
```

#### Abilita NTP {#enable-ntp}

Assicurati di aver installato e eseguito NTP sul computer che ospita i database MongoDB. Ad esempio, puoi installarlo utilizzando Gestione pacchetti yum su un computer CentOS:

```shell
sudo yum install ntp
```

Dopo che il daemon NTP è stato installato e avviato correttamente, puoi controllare il file di deriva per l&#39;offset di tempo del server.

#### Disattiva pagine grandi trasparenti {#disable-transparent-huge-pages}

Red Hat® Linux® utilizza un algoritmo di gestione della memoria denominato Transparent Huge Pages (THP). Si consiglia di disattivarlo se si utilizza il sistema operativo per i carichi di lavoro del database.

È possibile disattivarlo seguendo la procedura seguente:

1. Apri `/etc/grub.conf` nell’editor di testo desiderato.
1. Aggiungi la seguente riga al file grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Infine, controlla se l&#39;impostazione è entrata in vigore eseguendo:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l&#39;output del comando precedente deve essere:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Per ulteriori informazioni sulle pagine grandi trasparenti, consulta questo articolo [articolo](https://access.redhat.com/solutions/46111).

#### Disattiva NUMA {#disable-numa}

Nella maggior parte delle installazioni in cui è abilitato NUMA, il daemon MongoDB lo disattiva automaticamente se viene eseguito come servizio da `/etc/init.d` cartella.

In caso contrario, è possibile disabilitare NUMA a livello di processo. Per disattivarlo, esegui i seguenti comandi:

```shell
numactl --interleave=all <path_to_process>
```

Dove `<path_to_process>` è la via del processo mondio.

Quindi, disattiva il recupero della zona eseguendo:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Regolare le impostazioni dell&#39;ulimit per il processo del mondio {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® consente un controllo configurabile sull&#39;allocazione delle risorse tramite `ulimit` comando. Questa configurazione può essere eseguita su un utente o su base di processo.

Si consiglia di configurare l&#39;ulimit per il processo mongod in base alla [Impostazioni di ottimizzazione consigliate MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Test delle prestazioni di I/O MongoDB {#test-mongodb-i-o-performance}

MongoDB fornisce uno strumento chiamato `mongoperf` progettato per testare le prestazioni di I/O. Si consiglia di utilizzarlo per testare le prestazioni di tutte le istanze MongoDB che compongono la tua infrastruttura.

Per informazioni su come utilizzare `mongoperf`, visualizza [Documentazione MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>La `mongoperf` è un indicatore delle prestazioni di MongoDB sulla piattaforma su cui viene eseguito. Di conseguenza, i risultati non dovrebbero essere considerati definitivi per l&#39;esecuzione di un sistema di produzione.
>
>Per risultati di prestazioni più precisi, è possibile eseguire test complementari con `fio` Strumento Linux®.

**Verificare le prestazioni di lettura sulle macchine virtuali che compongono la distribuzione**

Dopo aver installato lo strumento, passa alla directory del database MongoDB per eseguire i test. Quindi, avvia il primo test eseguendo `mongoperf`con questa configurazione:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

L&#39;output desiderato deve raggiungere fino a due gigabyte al secondo (2 GB/s) e 500.000 IOPS in esecuzione a 32 thread per tutte le istanze MongoDB.

Esegui un secondo test, questa volta utilizzando file mappati in memoria, impostando `mmf:true` parametro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

L&#39;output del secondo test deve essere notevolmente superiore al primo, indicando le prestazioni del trasferimento di memoria.

>[!NOTE]
Durante l&#39;esecuzione dei test, controllare le statistiche di utilizzo di I/O per le macchine virtuali in questione nel sistema di monitoraggio del sistema operativo in uso. Se indicano valori inferiori al 100% per le letture di I/O, potrebbe esserci un problema con la macchina virtuale.

**Verifica le prestazioni di scrittura dell&#39;istanza MongoDB primaria**

Quindi, controlla le prestazioni di scrittura I/O dell&#39;istanza MongoDB primaria eseguendo `mongoperf` dalla directory del database MongoDB con le stesse impostazioni:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

L&#39;uscita desiderata dovrebbe essere di 12 megabyte al secondo e raggiungere circa 3000 IOPS, con una minima variazione tra il numero di thread.

## Passaggi per gli ambienti virtualizzati {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se si utilizza WMWare ESX per gestire e distribuire gli ambienti virtualizzati, assicurarsi di eseguire le seguenti impostazioni dalla console ESX per consentire il funzionamento di MongoDB:

1. Disattivare la funzione di ballooning della memoria
1. Preallocare e riservare memoria per le macchine virtuali che ospitano i database MongoDB
1. Utilizzare il controllo I/O dello storage per allocare un numero sufficiente di I/O al `mongod` processo.
1. Garantire le risorse della CPU delle macchine che ospitano MongoDB impostando [Riserva CPU](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. Valutare l&#39;utilizzo dei driver di I/O ParaVirtual. Vedi [articolo della knowledgebase](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Per la documentazione su come configurare MongoDB con Amazon Web Services, controlla il [Configurare l’integrazione AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) articolo sul sito web MongoDB.

## Protezione di MongoDB prima della distribuzione {#securing-mongodb-before-deployment}

Vedi questo post su [distribuzione sicura di MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) per informazioni su come proteggere la configurazione dei database prima della distribuzione.

## Dispatcher {#dispatcher}

### Scelta del sistema operativo per il Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Per distribuire correttamente la distribuzione MongoDB, è necessario che il sistema operativo che ospita Dispatcher sia in esecuzione **Apache httpd** **versione 2.4 o successiva.**

Inoltre, assicurati che tutte le librerie utilizzate nella build siano aggiornate per ridurre al minimo le implicazioni in materia di sicurezza.

### Configurazione del Dispatcher {#dispatcher-configuration}

Una tipica configurazione del Dispatcher offre da dieci a venti volte di più la velocità effettiva della richiesta di una singola istanza AEM.

Poiché il Dispatcher è senza stato, può essere ridimensionato orizzontalmente con facilità. In alcune implementazioni, agli autori deve essere impedito l’accesso a determinate risorse. Si consiglia di utilizzare un’istanza di Dispatcher con le istanze dell’autore.

L’esecuzione di AEM senza Dispatcher richiede che la terminazione SSL e il bilanciamento del carico siano eseguiti da un’altra applicazione. È necessario perché le sessioni devono avere affinità con l&#39;istanza AEM in cui vengono create, un concetto noto come connessioni permanenti. Il motivo è garantire che gli aggiornamenti al contenuto presentino una latenza minima.

Controlla la [Documentazione di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per ulteriori informazioni su come configurarlo.

### Configurazione aggiuntiva {#additional-configuration}

#### Connessioni permanenti {#sticky-connections}

Le connessioni permanenti garantiscono che le pagine personalizzate e i dati di sessione per un utente siano tutti composti nella stessa istanza di AEM. Questi dati vengono memorizzati nell’istanza, quindi le richieste successive dello stesso utente ritornano alla stessa istanza.

Si consiglia di abilitare le connessioni permanenti per tutte le richieste di indirizzamento dei livelli interni alle istanze AEM, incoraggiando le richieste successive a raggiungere la stessa istanza AEM. In questo modo è possibile ridurre al minimo la latenza che si nota diversamente quando il contenuto viene aggiornato tra le istanze.

#### Scadenza lunga {#long-expires}

Per impostazione predefinita, il contenuto inviato da un’istanza di Dispatcher dispone di intestazioni Last-Modified ed Etag, senza alcuna indicazione della scadenza del contenuto. Questo flusso assicura che l’interfaccia utente ottenga sempre la versione più recente della risorsa. Significa anche che il browser esegue un’operazione di GET per vedere se la risorsa è cambiata. Di conseguenza, può causare più richieste a cui la risposta HTTP è 304 (non modificata), a seconda del caricamento della pagina. Per le risorse che non scadono, l’impostazione di un’intestazione Expires e la rimozione delle intestazioni Last-Modified e ETag causano la memorizzazione in cache del contenuto. Inoltre, non vengono più effettuate richieste di aggiornamento fino a quando non viene soddisfatta la data nell’intestazione Scadenza .

Tuttavia, l’utilizzo di questo metodo significa che non esiste alcun modo ragionevole per far scadere la risorsa nel browser prima della scadenza dell’intestazione Scade. Per attenuare questo problema, è possibile configurare HtmlClientLibraryManager in modo da utilizzare URL immutabili per le librerie client.

Questi URL non verranno modificati. Quando il corpo della risorsa contenuta nell’URL cambia, le modifiche si riflettono nell’URL e assicurano che il browser richieda la versione corretta della risorsa.

La configurazione predefinita aggiunge un selettore a HtmlClientLibraryManager. Essendo un selettore, la risorsa viene memorizzata nella cache in Dispatcher con il selettore intatto. Anche questo selettore può essere utilizzato per garantire il corretto comportamento di scadenza. Il selettore predefinito segue la `lc-.*?-lc` modello. Le seguenti direttive di configurazione Apache httpd assicurano che tutte le richieste che corrispondono a quel pattern vengano servite con un tempo di scadenza adeguato.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Nessun serpente {#no-sniff}

Se il contenuto viene inviato senza tipo di contenuto, molti browser tentano di indovinare il tipo di contenuto leggendo i primi byte del contenuto. Questo metodo si chiama &quot;sniffing&quot;. La navigazione apre una vulnerabilità di sicurezza in quanto gli utenti in grado di scrivere nell’archivio potrebbero caricare contenuti dannosi senza alcun tipo di contenuto.

Per questo motivo, è consigliabile aggiungere un `no-sniff` intestazione per le risorse gestite da Dispatcher. Tuttavia, Dispatcher non memorizza in cache le intestazioni. Di conseguenza, qualsiasi contenuto distribuito dal file system locale ha un tipo di contenuto determinato dall’estensione, anziché utilizzare l’intestazione del tipo di contenuto originale dal server di origine AEM.

Non è possibile abilitare alcun frammento in modo sicuro se l’applicazione web è nota per non distribuire mai risorse memorizzate nella cache senza un tipo di file.

È possibile abilitare No Siff inclusivo:

```xml
Header set X-Content-Type-Options "nosniff"
```

Può anche essere attivato selettivamente:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Informativa sulla sicurezza dei contenuti {#content-security-policy}

Le impostazioni predefinite di Dispatcher consentono l’apertura di Criteri di sicurezza del contenuto, noti anche come CSP. Queste impostazioni consentono a una pagina di caricare risorse da tutti i domini soggetti ai criteri predefiniti della sandbox del browser.

È opportuno limitare il luogo in cui è possibile caricare le risorse da per evitare di caricare il codice nel motore JavaScript da server esterni non attendibili o non verificati.

La CSP consente di ottimizzare le politiche. Tuttavia, in un&#39;applicazione complessa, le intestazioni CSP devono essere sviluppate con attenzione in quanto i criteri troppo restrittivi possono interrompere parti dell&#39;interfaccia utente.

>[!NOTE]
Per ulteriori informazioni su come funziona, consulta la sezione [Pagina OWASP sui criteri di sicurezza dei contenuti](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Ridimensionamento {#sizing}

Per ulteriori informazioni sul dimensionamento, consulta la sezione [Linee guida per il dimensionamento dell&#39;hardware](/help/managing/hardware-sizing-guidelines.md).

### Ottimizzazione delle prestazioni MongoDB {#mongodb-performance-optimization}

Per informazioni generiche sulle prestazioni di MongoDB, vedi [Analisi delle prestazioni di MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitazioni note {#known-limitations}

### Installazioni simultanee {#concurrent-installations}

Mentre l&#39;utilizzo simultaneo di più istanze AEM con un singolo database è supportato da MongoMK, le installazioni simultanee non lo sono.

Per risolvere questo problema, assicurati di eseguire prima l&#39;installazione con un singolo membro e di aggiungere gli altri al termine della prima installazione.

### Lunghezza nome pagina {#page-name-length}

Se AEM è in esecuzione su una distribuzione di gestione della persistenza MongoMK, [i nomi delle pagine non possono superare i 150 caratteri.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
Consulta la sezione [Documentazione MongoDB](https://docs.mongodb.com/manual/reference/limits/) in modo da acquisire familiarità con i limiti e le soglie noti di MongoDB.
