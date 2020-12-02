---
title: AEM con MongoDB
seo-title: AEM con MongoDB
description: Scopri le attività e le considerazioni necessarie per un AEM di successo con la distribuzione MongoDB.
seo-description: Scopri le attività e le considerazioni necessarie per un AEM di successo con la distribuzione MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a
workflow-type: tm+mt
source-wordcount: '6513'
ht-degree: 0%

---


# AEM con MongoDB{#aem-with-mongodb}

Questo articolo mira a migliorare le conoscenze sulle attività e sulle considerazioni necessarie per distribuire con successo Adobe Experience Manager con MongoDB.

Per ulteriori informazioni sulla distribuzione, consultare la sezione [Implementazione e manutenzione](/help/sites-deploying/deploy.md) della documentazione.

## Quando utilizzare MongoDB con AEM {#when-to-use-mongodb-with-aem}

MongoDB viene in genere utilizzato per supportare AEM distribuzioni di autori in cui è soddisfatto uno dei seguenti criteri:

* più di 1000 utenti unici al giorno;
* Più di 100 utenti simultanei;
* elevati volumi di modifiche di pagina;
* Rollout o attivazioni di grandi dimensioni.

I criteri indicati sopra sono solo per le istanze di creazione e non per le istanze di pubblicazione basate su TarMK. Il numero di utenti si riferisce agli utenti autenticati, in quanto le istanze di autore non consentono l&#39;accesso non autenticato.

Se i criteri non sono soddisfatti, si consiglia di installare TarMK attivo/in standby per risolvere il problema della disponibilità. In generale, MongoDB dovrebbe essere considerato in situazioni in cui i requisiti di scala sono più di quanto si possa ottenere con un singolo elemento hardware.

>[!NOTE]
>
>Ulteriori informazioni sul ridimensionamento delle istanze dell&#39;autore e sulla definizione degli utenti simultanei sono disponibili nelle [Linee guida sul ridimensionamento hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Distribuzione MongoDB minima per AEM {#minimal-mongodb-deployment-for-aem}

Di seguito è riportata una distribuzione minima per AEM su MongoDB. Per semplicità, la terminazione SSL e i componenti proxy HTTP sono stati generalizzati. È costituito da un singolo set di repliche MongoDB, con un elemento primario e due secondari.

![chlimage_1-4](assets/chlimage_1-4.png)

Una distribuzione minima richiede 3 istanze `mongod` configurate come set di replica. Un&#39;istanza verrà selezionata come primaria, mentre le altre istanze saranno secondarie, mentre le elezioni saranno gestite da `mongod`. Associato a ogni istanza è un disco locale. Affinché il cluster supporti il carico, si consiglia una quantità minima di 12 MB/s con più di 3000 operazioni di I/O al secondo (IOPS).

Gli autori AEM sono connessi alle istanze `mongod`, con ogni AEM autore che si collega a tutte e tre le istanze `mongod`. Le scritture vengono inviate al modulo principale e le letture possono essere lette da una qualsiasi delle istanze. Il traffico viene distribuito in base al carico di un dispatcher a una delle istanze di creazione AEM attive. L&#39;archivio dati OAK è un `FileDataStore` e il monitoraggio MongoDB è fornito da MMS o da MongoDB Ops Manager a seconda della posizione della distribuzione. Il monitoraggio a livello di sistema operativo e di log è fornito da soluzioni di terze parti come Splunk o Ganglia.

In questa implementazione, tutti i componenti sono necessari per una corretta implementazione. Eventuali componenti mancanti non funzioneranno più.

### Sistemi operativi {#operating-systems}

Per un elenco dei sistemi operativi supportati per AEM 6, vedere la pagina [Requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Ambienti {#environments}

Gli ambienti virtualizzati sono supportati a condizione che vi sia una buona comunicazione tra i diversi team tecnici che eseguono il progetto. Ciò include il team che gestisce AEM, il team proprietario del sistema operativo e il team che gestisce l&#39;infrastruttura virtualizzata.

Esistono requisiti specifici relativi alla capacità di I/O delle istanze MongoDB che devono essere gestiti dal team che gestisce l&#39;ambiente virtualizzato. Se il progetto utilizza una distribuzione cloud, come  Amazon Web Services, sarà necessario eseguire il provisioning delle istanze con capacità di I/O e coerenza sufficienti per supportare le istanze MongoDB. In caso contrario, i processi MongoDB e l&#39;archivio Oak saranno eseguiti in modo inaffidabile e irregolare.

Negli ambienti virtualizzati MongoDB richiederà configurazioni di I/O e VM specifiche per garantire che il motore di storage di MongoDB non sia criptato dalle politiche di allocazione delle risorse VMWare. Un&#39;implementazione di successo garantirà che non ci siano barriere tra i vari team e che tutti siano registrati per fornire le prestazioni richieste.

## Considerazioni hardware {#hardware-considerations}

### Archiviazione {#storage}

Al fine di ottenere il throughput di lettura e scrittura per ottenere prestazioni migliori senza la necessità di scalare in orizzontale prematuro, MongoDB in genere richiede storage o SSD con prestazioni equivalenti a SSD.

### RAM {#ram}

Le versioni 2.6 e 3.0 di MongoDB che utilizzano il motore di storage MMAP richiedono che il set di lavoro del database e i relativi indici si inseriscano nella RAM.

Una quantità insufficiente di RAM ridurrà notevolmente le prestazioni. Le dimensioni del set di lavoro e del database dipendono fortemente dall&#39;applicazione. Sebbene sia possibile effettuare alcune stime, il modo più affidabile per determinare la quantità di RAM necessaria è la creazione dell&#39;applicazione AEM e il test del carico.

Per facilitare il processo di test del carico, si può ipotizzare il seguente rapporto tra il set di lavoro e la dimensione totale del database:

* 1:10 per lo storage SSD
* 1:3 per lo storage su disco rigido

Ciò significa che, nel caso delle installazioni SSD, per un database da 2 TB sarà necessario 200 GB di RAM.

Anche se le stesse limitazioni si applicano al motore di storage WiredTiger in MongoDB 3.0, la correlazione tra il set di lavoro, RAM e errori di pagina non è così forte come WiredTiger non utilizza la mappatura della memoria nello stesso modo in cui il motore di storage MMAP.

>[!NOTE]
>
> Adobe consiglia di utilizzare il motore di storage WiredTiger per le distribuzioni AEM 6.1 che utilizzano MongoDB 3.0.

### Archivio dati {#data-store}

A causa delle limitazioni del set di lavoro MongoDB, si consiglia vivamente di mantenere l&#39;archivio dati indipendente da MongoDB. Nella maggior parte degli ambienti è necessario utilizzare un `FileDataStore` che utilizza un NAS disponibile per tutte le istanze AEM. Per le situazioni in cui vengono utilizzati i servizi Web  Amazon, è presente anche un `S3 DataStore`. Se per qualsiasi motivo l&#39;archivio dati viene mantenuto all&#39;interno di MongoDB, la dimensione del datastore deve essere aggiunta alla dimensione totale del database e i calcoli del set di lavoro devono essere corretti in modo appropriato. Ciò può significare il provisioning di molta più RAM per mantenere le prestazioni senza errori di pagina.

## Monitoraggio {#monitoring}

Il monitoraggio è essenziale per la corretta attuazione del progetto. Sebbene con sufficiente conoscenza sia possibile eseguire AEM su MongoDB senza monitoraggio, tale conoscenza si trova normalmente in ingegneri specializzati per ogni sezione della distribuzione.

Questo richiede in genere un ingegnere R&amp;S che lavora su Apache Oak Core e uno specialista MongoDB.

Senza monitoraggio a tutti i livelli, per diagnosticare i problemi sarà necessario conoscere in modo dettagliato la base di codice. Grazie al monitoraggio e all&#39;adeguata guida sulle principali statistiche, i team di implementazione saranno in grado di reagire adeguatamente alle anomalie.

Anche se è possibile utilizzare gli strumenti della riga di comando per ottenere una rapida istantanea del funzionamento di un cluster, farlo in tempo reale su molti host è quasi impossibile. Gli strumenti della riga di comando forniscono raramente informazioni storiche oltre pochi minuti e non consentono mai la correlazione tra diversi tipi di metriche. Un breve periodo di lenta sincronizzazione in background `mongod` richiede un notevole sforzo manuale per correlarsi a un&#39;attesa di I/O o a livelli di scrittura eccessivi a una risorsa di memorizzazione condivisa da una macchina virtuale apparentemente non connessa.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager è un servizio gratuito offerto da MongoDB che consente il monitoraggio e la gestione delle istanze MongoDB. Fornisce una visualizzazione delle prestazioni e dello stato del cluster MongoDB in tempo reale. Gestisce sia le istanze cloud che quelle ospitate privatamente, a condizione che l&#39;istanza raggiunga il server di monitoraggio di Cloud Manager.

Richiede un agente installato nell&#39;istanza MongoDB che si connette al server di monitoraggio. Esistono 3 livelli di agente:

* Un agente di automazione in grado di automatizzare completamente tutto sul server MongoDB,
* Un agente di monitoraggio in grado di monitorare l&#39;istanza `mongod`,
* Agente di backup in grado di eseguire backup pianificati dei dati.

Anche se l&#39;utilizzo di Cloud Manager per l&#39;automazione della manutenzione di un cluster MongoDB semplifica molte delle attività di routine, non è richiesto e non lo è nemmeno per il backup. Quando si sceglie Cloud Manager per il monitoraggio, il monitoraggio è comunque necessario.

Per ulteriori informazioni su MongoDB Cloud Manager, consulta la [documentazione di MongoDB](https://docs.cloud.mongodb.com/).

### Gestione opzioni MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager è lo stesso software di MongoDB Cloud Manager. Una volta registrato, Ops Manager può essere scaricato e installato localmente in un centro dati privato o su qualsiasi altro computer portatile o desktop. Utilizza un database MongoDB locale per memorizzare i dati e comunicare esattamente come Cloud Manager con i server gestiti. Se si dispone di criteri di sicurezza che vietano l&#39;utilizzo di un agente di monitoraggio, è necessario utilizzare Gestione opzioni MongoDB.

### Monitoraggio del sistema operativo {#operating-system-monitoring}

Per eseguire un cluster MongoDB AEM è necessario il monitoraggio a livello di sistema operativo.

Ganglia è un buon esempio di tale sistema e fornisce un&#39;immagine sulla gamma e il dettaglio delle informazioni necessarie che va oltre le metriche di salute di base come CPU, media del carico e spazio libero su disco. Per diagnosticare i problemi, sono necessarie informazioni di livello inferiore, come i livelli del pool di entropia, l&#39;attesa I/O della CPU, i socket nello stato FIN_WAIT2.

### Aggregazione log {#log-aggregation}

Con un cluster di più server, l&#39;aggregazione centrale del registro è un requisito per un sistema di produzione. Software come Splunk supporta l&#39;aggregazione dei log e consente ai team di analizzare i pattern di comportamento dell&#39;applicazione senza dover raccogliere manualmente i log.

## Elenchi di controllo {#checklists}

Questa sezione descrive i vari passaggi da effettuare per garantire che le distribuzioni AEM e MongoDB siano configurate correttamente prima di implementare il progetto.

### Rete {#network}

1. Innanzitutto, accertatevi che tutti gli host dispongano di una voce DNS
1. Tutti gli host devono essere risolvibili dalla voce DNS di tutti gli altri host router
1. Tutti gli host MongoDB sono eseguibili in modo instradabile da tutti gli altri host MongoDB nello stesso cluster
1. Gli host MongoDB possono indirizzare i pacchetti a MongoDB Cloud Manager e agli altri server di monitoraggio
1. AEM server possono indirizzare i pacchetti a tutti i server MongoDB
1. La latenza del pacchetto tra qualsiasi server AEM e qualsiasi server MongoDB è inferiore a due millisecondi, senza perdita di pacchetti e con una distribuzione standard di almeno un millisecondo.
1. Assicuratevi che tra un AEM e un server MongoDB non siano presenti più di due hop
1. Non ci sono più di due hop tra due server MongoDB
1. Non esistono router superiori a OSI di livello 3 tra i server core (MongoDB o AEM o qualsiasi combinazione).
1. Se viene utilizzato il trunking VLAN o qualsiasi altro tipo di tunneling di rete, deve essere conforme ai controlli di latenza del pacchetto.

### Configurazione AEM {#aem-configuration}

#### Configurazione archivio nodi {#node-store-configuration}

Le istanze AEM devono essere configurate per utilizzare AEM con MongoMK. La base dell&#39;implementazione MongoMK in AEM è Document Node Store.

Per ulteriori informazioni su come configurare gli archivi dei nodi, vedere [Configurazione di archivi di nodi e di archivi dati in AEM](/help/sites-deploying/data-store-config.md).

Di seguito è riportato un esempio di configurazione dell&#39;archivio dei nodi del documento per una distribuzione MongoDB minima:

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
Questo è il server MongoDB a cui AEM connettersi. Vengono effettuate connessioni a tutti i membri noti del set di repliche predefinito. Se viene utilizzato MongoDB Cloud Manager, la protezione del server è abilitata. Di conseguenza, la stringa di connessione deve contenere un nome utente e una password appropriati. Le versioni non aziendali di MongoDB supportano solo l&#39;autenticazione tramite nome utente e password. Per ulteriori informazioni sulla sintassi della stringa di connessione, consultare la [documentazione](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Nome del database. Il valore predefinito per AEM è 
`aem-author`.

* `customBlobStore`
Se la distribuzione memorizza i file binari nel database, questi faranno parte del set di lavoro. Per questo motivo si consiglia di non memorizzare i file binari all&#39;interno di MongoDB, preferendo un datastore alternativo come un 
`FileSystem` datastore su un NAS.

* `cache`
Dimensione della cache in MB. Questo viene distribuito tra le diverse cache utilizzate nel pannello 
`DocumentNodeStore`. Il valore predefinito è 256 MB. Tuttavia, le prestazioni di lettura Oak trarranno vantaggio da una cache più grande.

* `blobCacheSize`
I BLOB utilizzati di frequente possono essere memorizzati nella cache da AEM per evitare di recuperarli dall&#39;archivio dati. Questo avrà un impatto maggiore sulle prestazioni, soprattutto quando si memorizzano i BLOB nel database MongoDB. Tutti gli archivi dati basati su file system trarranno vantaggio dalla cache del disco a livello di sistema operativo.

#### Configurazione archivio dati {#data-store-configuration}

L&#39;archivio dati viene utilizzato per archiviare file di dimensioni superiori a una soglia. Al di sotto di tale soglia, i file vengono memorizzati come proprietà nell&#39;archivio dei nodi del documento. Se si utilizza `MongoBlobStore`, viene creata una raccolta dedicata in MongoDB per memorizzare i BLOB. Questa raccolta contribuisce al set di lavoro dell&#39;istanza `mongod` e richiederà che `mongod` disponga di più RAM per evitare problemi di prestazioni. Per questo motivo, la configurazione consigliata è quella di evitare la `MongoBlobStore` per le distribuzioni di produzione e utilizzare `FileDataStore` con il backup di un NAS condiviso tra tutte le istanze AEM. Poiché la cache a livello di sistema operativo è efficiente nella gestione dei file, la dimensione minima di un file su disco deve essere impostata in modo che la dimensione del blocco del disco sia utilizzata in modo efficiente e che molti piccoli documenti non contribuiscano eccessivamente al set di lavoro dell&#39;istanza `mongod`.

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
Dimensioni in byte. I file binari di dimensioni inferiori o uguali a queste vengono memorizzati nell&#39;archivio dei nodi del documento. Invece di memorizzare l&#39;ID del BLOB, viene memorizzato il contenuto del file binario. Per i file binari di dimensioni maggiori di queste, l&#39;ID del binario viene memorizzato come proprietà del documento nell&#39;insieme di nodi e il corpo del binario viene memorizzato nella variabile 
`FileDataStore` su disco. 4096 byte è una dimensione di blocco tipica del file system.

* `path`
Percorso della directory principale dell&#39;archivio dati. Per una distribuzione MongoMK, questo deve essere un file system condiviso disponibile per tutte le istanze AEM. In genere viene utilizzato un server NAS (Network Attached Storage). Per distribuzioni cloud come  Amazon Web Services, la 
`S3DataFileStore` è disponibile anche.

* `cacheSizeInMB`
La dimensione totale della cache binaria in Megabyte. Viene utilizzato per memorizzare nella cache i file binari in un valore inferiore al 
`maxCacheBinarySize` impostazione.

* `maxCachedBinarySize`
La dimensione massima in byte di un binario memorizzato nella cache binaria. Se si utilizza un archivio dati basato su file system, si consiglia di non utilizzare valori elevati per la cache dell&#39;archivio dati in quanto i file binari sono già memorizzati nella cache dal sistema operativo.

#### Disattivazione del suggerimento query {#disabling-the-query-hint}

Si consiglia di disabilitare il suggerimento query inviato con tutte le query aggiungendo la proprietà

`-Doak.mongo.disableIndexHint=true`

all&#39;avvio AEM. In questo modo, MongoDB calcolerà sull&#39;indice più appropriato da utilizzare sulla base di statistiche interne.

Se l&#39;hint di query non è disabilitato, qualsiasi ottimizzazione delle prestazioni degli indici non avrà alcun impatto sulle prestazioni di AEM.

#### Abilita cache persistente per MongoMK {#enable-persistent-cache-for-mongomk}

Si consiglia di abilitare una configurazione cache persistente per le distribuzioni MongoDB, al fine di massimizzare la velocità per gli ambienti con elevate prestazioni di lettura I/O. Per ulteriori dettagli, consultare la [Documentazione Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Ottimizzazioni del sistema operativo MongoDB {#mongodb-operating-system-optimizations}

### Supporto del sistema operativo {#operating-system-support}

MongoDB 2.6 utilizza un motore di storage mappato sulla memoria che è sensibile ad alcuni aspetti della gestione a livello di sistema operativo tra RAM e disco. Le prestazioni di query e lettura dell&#39;istanza MongoDB si basano sull&#39;eliminazione o l&#39;eliminazione di operazioni di I/O lente, spesso denominate errori di pagina. Si tratta di errori di pagina che si applicano in particolare al processo `mongod`. Non devono essere confusi con errori di pagina a livello di sistema operativo.

Per un funzionamento veloce, il database MongoDB dovrebbe accedere solo ai dati già presenti nella RAM. I dati a cui deve accedere sono costituiti da indici e dati. Questa raccolta di indici e dati è denominata set di lavoro. Se il set di lavoro è più grande della RAM disponibile MongoDB deve inserire i dati da un disco con un costo di I/O, eliminando altri dati già in memoria. Se lo sfratto causa il ricaricamento dei dati da guasti della pagina del disco, le prestazioni risulteranno compromesse. Se il set di lavoro è dinamico e variabile, per supportare le operazioni vengono generati più errori di pagina.

MongoDB viene eseguito su un certo numero di sistemi operativi, tra cui un&#39;ampia varietà di versioni Linux, Windows e Mac OS. Per ulteriori informazioni, vedere [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms). A seconda della scelta del sistema operativo, MongoDB ha raccomandazioni a livello di sistema operativo diverse. Sono documentati all&#39;indirizzo [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) e qui riepilogati per comodità.

#### Linux {#linux}

* Disattivare gli hugepage trasparenti e sganciare. Per ulteriori informazioni, vedere [Impostazioni trasparenti delle pagine grandi.](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)
* [Regolare le ](https://docs.mongodb.com/manual/administration/production-notes/#readahead) impostazioni readahead sui dispositivi in cui sono memorizzati i file del database in base al caso d&#39;uso.

   * Per il motore di memorizzazione MMAPv1, se il set di lavoro è più grande della RAM disponibile e il pattern di accesso al documento è casuale, è consigliabile abbassare il valore di lettura a 32 o 16. Valutare diverse impostazioni per trovare un valore ottimale che massimizzi la memoria residente e riduca il numero di errori di pagina.
   * Per il motore di storage WiredTiger, impostare readahead su 0, indipendentemente dal tipo di supporto di storage (filatura, SSD, ecc.). In generale, utilizzare l&#39;impostazione di lettura consigliata a meno che i test non mostrino un vantaggio misurabile, ripetibile e affidabile con un valore di lettura superiore. [MongoDB Professional ](https://docs.mongodb.com/manual/administration/production-notes/#readahead) Support può fornire consigli e indicazioni sulle configurazioni di lettura non-zero.

* Se in un ambiente virtuale è in esecuzione RHEL 7/CentOS 7, disattivate lo strumento sintonizzato.
* Quando RHEL 7 / CentOS 7 viene eseguito in un ambiente virtuale, lo strumento sintonizzato richiama automaticamente un profilo di prestazioni derivato dal throughput delle prestazioni, che imposta automaticamente le impostazioni di lettura a 4 MB. Ciò può avere un impatto negativo sulle prestazioni.
* Utilizzare i programmi di pianificazione dei dischi noop o di scadenza per le unità SSD.
* Utilizzare il pianificatore di dischi noop per le unità virtualizzate nelle VM guest.
* Disabilitare NUMA o impostare vm.zone_reclamate_mode su 0 ed eseguire le istanze [mondio](https://docs.mongodb.com/manual/administration/production-notes/#readahead) con l&#39;interfoliazione dei nodi. Vedere: [MongoDB e NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) per ulteriori informazioni.

* Regolare i valori limite sull&#39;hardware in base alle esigenze d&#39;uso. Se più istanze [mondio](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) o [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) sono in esecuzione sotto lo stesso utente, ridimensionare i valori di limite di conseguenza. Vedere: [Impostazioni avanzate UNIX](https://docs.mongodb.com/manual/reference/ulimit/) per ulteriori informazioni.

* Utilizzare il tempo di attesa per il punto di montaggio [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath).
* Configurate handle di file sufficienti (fs.file-max), limite di kernel pid (kernel.pid_max) e massimo di thread per processo (kernel.thread-max) per la distribuzione. Per i sistemi di grandi dimensioni, i seguenti valori forniscono un buon punto di partenza:

   * fs.file-max valore di 98000,
   * kernel.pid_max valore di 64000,
   * andkernel.thread-max valore di 64000

* Verificate che nel sistema sia configurato lo spazio di scambio. Per informazioni sul ridimensionamento appropriato, consultate la documentazione del sistema operativo in uso.
* Verificare che il server TCP predefinito del sistema sia impostato correttamente. Un valore di 300 offre spesso prestazioni migliori per i set di repliche e i cluster condivisi. Vedere: [Il tempo di conservazione TCP influisce sulle installazioni MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) per ulteriori informazioni, consulta le Domande frequenti.

#### Windows {#windows}

* Considerate la possibilità di disattivare gli aggiornamenti NTFS dell&#39;&quot;ultima ora di accesso&quot;. Questo è analogo alla disattivazione del tempo su sistemi simili a Unix.

### WiredTiger {#wiredtiger}

A partire da MongoDB 3.2 il motore di storage predefinito per MongoDB è il motore di storage WiredTiger. Questo motore fornisce una serie di funzioni robuste e scalabili che lo rendono molto più adatto per tutti i carichi di lavoro generali del database. Le sezioni seguenti descrivono queste funzioni.

#### Condivisa a livello di documento {#document-level-concurrency}

WiredTiger utilizza il controllo della concorrenza a livello di documento per le operazioni di scrittura. Di conseguenza, più client possono modificare allo stesso tempo diversi documenti di una raccolta.

Per la maggior parte delle operazioni di lettura e scrittura, WiredTiger utilizza un controllo della concorrenza ottimistico. WiredTiger utilizza solo i blocchi di intento a livello globale, di database e di raccolta. Quando il motore di storage rileva i conflitti tra due operazioni, si verificherà un conflitto in scrittura che causerebbe un nuovo tentativo in modo trasparente da parte di MongoDB.Alcune operazioni globali, in genere di breve durata che coinvolgono più database, richiedono ancora un blocco globale &quot;a livello di istanza&quot;.

Alcune altre operazioni, come il rilascio di una raccolta, richiedono ancora un blocco esclusivo del database.

#### Snapshot e checkpoint {#snapshots-and-checkpoints}

WiredTiger utilizza MultiVersion Concurrency Control (MVCC). All’inizio di un’operazione, WiredTiger fornisce uno snapshot point-in-time dei dati alla transazione. Un&#39;istantanea presenta una visualizzazione coerente dei dati presenti nella memoria.

Durante la scrittura su disco, WiredTiger scrive su disco tutti i dati di un&#39;istantanea in modo coerente in tutti i file di dati. I dati ora [durevoli](https://docs.mongodb.com/manual/reference/glossary/#term-durable) fungono da punto di controllo nei file di dati. Il punto di controllo assicura che i file di dati siano coerenti fino all&#39;ultimo punto di controllo incluso; i checkpoint possono quindi fungere da punti di ripristino.

MongoDB configura WiredTiger per la creazione di checkpoint (ovvero per la scrittura dei dati dello snapshot su disco) a intervalli di 60 secondi o 2 gigabyte di dati del giornale.

Durante la scrittura di un nuovo checkpoint, il checkpoint precedente è ancora valido. Di conseguenza, anche se MongoDB termina o rileva un errore durante la scrittura di un nuovo checkpoint, al riavvio MongoDB può recuperare dall&#39;ultimo checkpoint valido.

Il nuovo punto di controllo diventa accessibile e permanente quando la tabella di metadati di WiredTiger viene aggiornata in modo atomico per fare riferimento al nuovo punto di controllo. Una volta accessibile il nuovo checkpoint, WiredTiger libera le pagine dai vecchi checkpoint.

Utilizzando WiredTiger, anche senza [giornalistica](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB può recuperare dall&#39;ultimo checkpoint; tuttavia, per recuperare le modifiche apportate dopo l&#39;ultimo checkpoint, eseguire con [journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diario {#journal}

WiredTiger utilizza un log delle transazioni di scrittura in combinazione con [checkpoint](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) per garantire la durata dei dati.

Il giornale WiredTiger persiste tutte le modifiche ai dati tra i checkpoint. Se MongoDB esce tra i checkpoint, utilizza il giornale di registrazione per riprodurre tutti i dati modificati dall&#39;ultimo checkpoint. Per informazioni sulla frequenza con cui MongoDB scrive i dati del giornale su disco, vedere [Processo di registrazione](https://docs.mongodb.com/manual/core/journaling/#journal-process).

Il giornale di registrazione WiredTiger viene compresso utilizzando la libreria di compressione [snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process). Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare l&#39;impostazione [storage.wiredTiger.EngineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor).

Per ulteriori informazioni, vedi: [Spostamento con WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>La dimensione minima del record del registro per WiredTiger è di 128 byte. Se un record di registro è pari o inferiore a 128 byte, WiredTiger non comprime tale record.
>
>È possibile disattivare la registrazione impostando [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) su false, il che può ridurre il sovraccarico di manutenzione della scrittura contabile.
>
>Per le istanze [standalone](https://docs.mongodb.com/manual/reference/glossary/#term-standalone), se non si utilizza il giornale di registrazione si perderanno alcune modifiche di dati quando MongoDB esce inaspettatamente tra i checkpoint. Per i membri di [set di repliche](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), il processo di replica può fornire sufficienti garanzie di durata.

#### Compressione {#compression}

Con WiredTiger, MongoDB supporta la compressione per tutte le raccolte e gli indici. La compressione riduce al minimo l&#39;utilizzo dello storage a scapito della CPU aggiuntiva.

Per impostazione predefinita, WiredTiger utilizza la compressione dei blocchi con la libreria di compressione [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) per tutte le raccolte e la [compressione dei prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) per tutti gli indici.

Per le raccolte, è disponibile anche la compressione a blocchi con [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib). Per specificare un algoritmo di compressione alternativo o nessuna compressione, utilizzare l&#39;impostazione [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib).

Per gli indici, per disabilitare la compressione [prefisso](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), utilizzare l&#39;impostazione [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression).

Le impostazioni di compressione sono configurabili anche per ogni raccolta e per indice durante la creazione di raccolte e indici. Vedere l&#39;opzione [Specificare le opzioni del motore di memorizzazione](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) e [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options).

Per la maggior parte dei carichi di lavoro, le impostazioni di compressione predefinite bilanciano l&#39;efficienza dello storage e i requisiti di elaborazione.

Anche il giornale di registrazione WiredTiger è compresso per impostazione predefinita. Per informazioni sulla compressione delle scritture contabili, vedere [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso memoria {#memory-use}

Con WiredTiger, MongoDB utilizza sia la cache interna WiredTiger che la cache del file system.

A partire dalla versione 3.4, la cache interna WiredTiger, per impostazione predefinita, utilizza la dimensione maggiore di:

* 50% di RAM meno 1 GB, o
* 256 MB

Per impostazione predefinita, WiredTiger utilizza la compressione Snappy block per tutte le raccolte e la compressione del prefisso per tutti gli indici. I valori predefiniti di compressione sono configurabili a livello globale e possono essere impostati anche a livello di raccolta e indice durante la creazione della raccolta e dell&#39;indice.

Diverse rappresentazioni vengono utilizzate per i dati nella cache interna di WiredTiger rispetto al formato su disco:

* I dati nella cache del file system sono gli stessi del formato su disco, inclusi i vantaggi di qualsiasi compressione per i file di dati. La cache del file system viene utilizzata dal sistema operativo per ridurre l&#39;I/O del disco.

Gli indici caricati nella cache interna di WiredTiger presentano una rappresentazione dati diversa rispetto al formato su disco, ma possono comunque sfruttare la compressione dei prefisso indice per ridurre l&#39;utilizzo della RAM.

La compressione del prefisso dell&#39;indice deduplica i prefissi comuni dai campi indicizzati.

I dati della raccolta nella cache interna di WiredTiger non sono compressi e utilizzano una rappresentazione diversa dal formato su disco. La compressione a blocchi consente di risparmiare notevolmente sullo storage su disco, ma i dati devono essere non compressi per essere manipolati dal server.

Tramite la cache del file system, MongoDB utilizza automaticamente tutta la memoria libera non utilizzata dalla cache WiredTiger o da altri processi.

Per regolare la dimensione della cache interna WiredTiger, vedere [storage.wiredTiger.EngineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evitare di aumentare la dimensione della cache interna WiredTiger al di sopra del valore predefinito.

### NUMA {#numa}

Accesso alla memoria non uniforme (NUMA) consente a un kernel di gestire la mappatura della memoria ai core del processore. Anche se questo tenta di rendere l&#39;accesso alla memoria più veloce per i core garantendo che siano in grado di accedere ai dati richiesti, NUMA interferisce con MMAP introducendo una latenza aggiuntiva, in quanto le letture non possono essere previste. Per questo motivo, NUMA deve essere disabilitato per il processo `mongod` su tutti i sistemi operativi che dispongono di tale funzionalità.

In sostanza, in un&#39;architettura NUMA la memoria è collegata alle CPU e le CPU sono collegate a un bus. In un&#39;architettura SMP o UMA, la memoria è collegata al bus e condivisa dalle CPU. Quando un thread alloca memoria su una CPU NUMA, lo assegna in base a un criterio. L&#39;impostazione predefinita prevede l&#39;allocazione di memoria collegata alla CPU locale del thread, a meno che non sia disponibile alcuna connessione, e a questo punto utilizza la memoria di una CPU gratuita a costi più elevati. Una volta allocata, la memoria non si sposta tra le CPU. L&#39;allocazione viene eseguita da un criterio ereditato dal thread padre, che in definitiva è il thread che ha avviato il processo.

In molti database che vedono la macchina come un&#39;architettura di memoria uniforme multi-core, questo porta alla CPU iniziale ottenere pieno prima e il riempimento della CPU secondaria più tardi, soprattutto se un thread centrale è responsabile per l&#39;allocazione dei buffer di memoria. La soluzione consiste nel modificare il criterio NUMA del thread principale utilizzato per avviare il processo `mongod`.

Questa operazione può essere eseguita eseguendo il comando seguente:

```shell
numactl --interleaved=all <mongod> -f config
```

Questo criterio consente di allocare la memoria in un round robin su tutti i nodi della CPU, garantendo una distribuzione uniforme su tutti i nodi. Non genera l&#39;accesso alla memoria con le prestazioni più elevate, come nei sistemi con più hardware CPU. Circa la metà delle operazioni di memoria sarà più lenta e oltre il bus, ma `mongod` non è stato scritto per raggiungere NUMA in modo ottimale, quindi è un compromesso ragionevole.

### Problemi NUMA {#numa-issues}

Se il processo `mongod` viene avviato da un percorso diverso dalla cartella `/etc/init.d`, è probabile che non venga avviato con il criterio NUMA corretto. A seconda del criterio predefinito, possono sorgere problemi. Questo perché i vari programmi di installazione di Linux Package Manager per MongoDB installano anche un servizio con file di configurazione che si trovano in `/etc/init.d` e che eseguono il passaggio descritto sopra. Se si installa ed esegue MongoDB direttamente da un archivio ( `.tar.gz`), sarà necessario eseguire manualmente mondio sotto il processo `numactl`.

>[!NOTE]
>
>Per ulteriori informazioni sui criteri NUMA disponibili, consultare la [documentazione numerica](https://linux.die.net/man/8/numactl).

Il processo MongoDB si comporterà in modo diverso in base ai diversi criteri di allocazione:

```

```

* `-membind=<nodes>`
Allocate solo sui nodi elencati. Mondio non allocerà memoria sui nodi elencati e potrebbe non utilizzare tutta la memoria disponibile.

* `-cpunodebind=<nodes>`
Viene eseguito solo sui nodi. Mondio verrà eseguito solo sui nodi specificati e utilizzerà solo la memoria disponibile su tali nodi.

* `-physcpubind=<nodes>`
Vengono eseguite solo su CPU (core) elencate. Mondio verrà eseguito solo sulle CPU elencate e utilizzerà solo la memoria disponibile su tali CPU.

* `--localalloc`
allocare sempre memoria sul nodo corrente, ma utilizzare tutti i nodi su cui viene eseguito il thread. Se un thread esegue l&#39;allocazione, verrà utilizzata solo la memoria disponibile per tale CPU.

* `--preferred=<node>`
Preferisce l&#39;allocazione a un nodo, ma torna ad altri se il nodo preferito è pieno. È possibile utilizzare una notazione relativa per definire un nodo. Inoltre, i thread vengono eseguiti su tutti i nodi.

Alcuni dei criteri potrebbero causare la perdita di tutta la RAM disponibile per il processo `mongod`. A differenza di MySQL, MongoDB evita attivamente il paging a livello di sistema operativo, e di conseguenza il processo `mongod` potrebbe ottenere meno memoria disponibile.

#### Scambio {#swapping}

A causa della natura intensiva di memoria dei database, lo scambio a livello di sistema operativo deve essere disattivato. Il processo MongoDB eviterà lo scambio per progettazione.

#### File system remoti {#remote-filesystems}

File system remoti come NFS non sono consigliati per i file di dati interni di MongoDB (i file di database di processo di mondio), perché introducono troppa latenza. Questo non deve essere confuso con il file system condiviso richiesto per l&#39;archiviazione di Oak Blob (FileDataStore), dove si consiglia NFS.

#### Leggi {#read-ahead}

La lettura deve essere regolata in modo che quando una pagina viene inserita in una pagina utilizzando una lettura casuale, i blocchi non necessari non vengono letti dal disco, con conseguente consumo non necessario di larghezza di banda I/O.

### Requisiti Linux {#linux-requirements}

#### Versioni minime del kernel {#minimum-kernel-versions}

* **2.6.23** per  `ext4` filesystem

* **2.6.25** per  `xfs` filesystem

#### Impostazioni consigliate per i dischi di database {#recommended-settings-for-database-disks}

**Disattiva ora**

Si consiglia di disattivare `atime` per i dischi che conterranno i database.

**Impostare il programma per dischi NOOP**

È possibile eseguire questa operazione tramite:

Innanzitutto, verificate l&#39;utilità di pianificazione I/O attualmente impostata. Questa operazione può essere eseguita eseguendo il comando seguente:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se la risposta è `noop`, non è necessario eseguire ulteriori operazioni.

Se NOOP non è il pianificatore di I/O configurato, potete modificarlo eseguendo:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Regola il valore di lettura in anticipo**

Si consiglia di utilizzare un valore 32 per i dischi da cui vengono eseguiti i database MongoDB. Ciò equivale a 16 kilobyte. Potete impostarlo eseguendo:

```shell
sudo blockdev --setra <value> <device>
```

#### Abilita NTP {#enable-ntp}

Verificare che nel computer in cui sono installati i database MongoDB sia installato e in esecuzione NTP. Ad esempio, potete installarlo utilizzando il gestore yum del pacchetto su un computer CentOS:

```shell
sudo yum install ntp
```

Dopo che il demone NTP è stato installato e ha avuto esito positivo, è possibile controllare il file di deriva per l&#39;offset temporale del server.

#### Disattiva pagine grandi trasparenti {#disable-transparent-huge-pages}

Red Hat Linux utilizza un algoritmo di gestione della memoria denominato Transparent Huge Pages (THP). Si consiglia di disattivarlo se si utilizza il sistema operativo per i carichi di lavoro del database.

Potete disattivarlo seguendo la procedura seguente:

1. Aprite il file `/etc/grub.conf` nell&#39;editor di testo desiderato.
1. Aggiungete la riga seguente al file grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Infine, verificare se l&#39;impostazione è entrata in vigore eseguendo:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l&#39;output del comando precedente deve essere:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Per ulteriori informazioni su Pagine grandi trasparenti, consultare questo [articolo](https://access.redhat.com/solutions/46111).

#### Disattiva NUMA {#disable-numa}

Nella maggior parte delle installazioni in cui è attivato NUMA, il demone MongoDB lo disattiverà automaticamente se viene eseguito come servizio dalla cartella `/etc/init.d`.

In caso contrario, è possibile disabilitare NUMA a livello di processo. Per disattivarlo, eseguite i seguenti comandi:

```shell
numactl --interleave=all <path_to_process>
```

Dove `<path_to_process>` è il percorso del processo di mondio.

Quindi, disattivate il recupero della zona eseguendo:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Regolare le impostazioni dell&#39;icona per il processo del mondio {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux consente il controllo configurabile sull&#39;allocazione delle risorse tramite il comando `ulimit`. Questa operazione può essere eseguita su un utente o su base di processo.

Si consiglia di configurare il limite massimo per il processo di mondio in base alle [Impostazioni di completamento consigliate MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Test prestazioni I/O MongoDB {#test-mongodb-i-o-performance}

MongoDB fornisce uno strumento denominato `mongoperf` progettato per testare le prestazioni di I/O. Si consiglia di utilizzarlo per testare le prestazioni di tutte le istanze MongoDB che costituiscono l&#39;infrastruttura.

Per informazioni sull&#39;utilizzo di `mongoperf`, vedere la [Documentazione MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>Tenere presente che `mongoperf` è progettato per essere un indicatore delle prestazioni di MongoDB sulla piattaforma su cui viene eseguito. Per questo motivo, i risultati non devono essere considerati definitivi per l&#39;esecuzione di un sistema di produzione.
>
>Per risultati di prestazioni più precisi, è possibile eseguire test complementari con lo strumento `fio` Linux.

**Verificare le prestazioni di lettura sulle macchine virtuali che compongono la distribuzione**

Dopo aver installato lo strumento, passate alla directory del database MongoDB per eseguire i test. Quindi, avviare il primo test eseguendo `mongoperf`con la configurazione seguente:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

L&#39;output desiderato dovrebbe raggiungere fino a due gigabyte al secondo (2 GB/s) e 500.000 IOPS in esecuzione a 32 thread per tutte le istanze MongoDB.

Eseguite un secondo test, questa volta utilizzando file mappati sulla memoria, impostando il parametro `mmf:true`:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

L&#39;output del secondo test dovrebbe essere notevolmente superiore al primo, indicando le prestazioni di trasferimento della memoria.

>[!NOTE]
>
>Durante l&#39;esecuzione dei test, controllare le statistiche sull&#39;uso dell&#39;I/O per le macchine virtuali in questione nel sistema di monitoraggio del sistema operativo in uso. Se indicano valori inferiori al 100% per le letture di I/O, potrebbe verificarsi un problema con la macchina virtuale.

**Verificare le prestazioni di scrittura dell&#39;istanza MongoDB primaria**

Quindi, controllare le prestazioni di scrittura I/O dell&#39;istanza MongoDB primaria eseguendo `mongoperf` dalla directory del database MongoDB con le stesse impostazioni:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

L&#39;output desiderato dovrebbe essere di 12 megabyte al secondo e raggiungere circa 3000 IOPS, con lieve variazione tra il numero di thread.

## Passaggi per gli ambienti virtualizzati {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se si utilizza WMWare ESX per gestire e implementare gli ambienti virtualizzati, assicurarsi di eseguire le seguenti impostazioni dalla console ESX per poter disporre del funzionamento MongoDB:

1. Disattivazione del bilanciamento della memoria
1. Preallocare e riservare memoria per le macchine virtuali che ospiteranno i database MongoDB
1. Utilizzare il controllo I/O dello storage per allocare un numero sufficiente di I/O al processo `mongod`.
1. Garantire le risorse CPU dei computer che ospitano MongoDB impostando [CPU Reservation](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Considerare l&#39;utilizzo di driver di I/O ParaVirtual. Per ulteriori informazioni su come eseguire questa operazione, consultate questo [articolo della knowledgebase](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

###  servizi Web Amazon {#amazon-web-services}

Per la documentazione su come configurare MongoDB con  Amazon Web Services, consultare l&#39;articolo [Configure AWS Integration](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) nel sito Web MongoDB.

## Protezione di MongoDB prima della distribuzione {#securing-mongodb-before-deployment}

Consulta questo post su [distribuzione sicura di MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) per informazioni su come proteggere la configurazione dei database prima della distribuzione.

## Dispatcher {#dispatcher}

### Scelta del sistema operativo per il dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Per distribuire correttamente la distribuzione MongoDB, il sistema operativo che ospita il dispatcher deve eseguire **Apache httpd** **versione 2.4 o successiva.**

Inoltre, accertatevi che tutte le librerie utilizzate nella build siano aggiornate al fine di ridurre al minimo le implicazioni di sicurezza.

### Configurazione del dispatcher {#dispatcher-configuration}

Una tipica configurazione del dispatcher consente una velocità di trasmissione di richieste da dieci a venti volte maggiore per una singola istanza AEM.

Poiché il dispatcher è principalmente senza stato, può essere ridimensionato orizzontalmente con facilità. In alcune distribuzioni, agli autori deve essere imposto un limite per l’accesso a determinate risorse. Per questo motivo, si consiglia vivamente di utilizzare un dispatcher con le istanze dell&#39;autore.

L&#39;esecuzione di AEM senza dispatcher richiede la terminazione SSL e il bilanciamento del carico da parte di un&#39;altra applicazione. Questo è richiesto perché le sessioni devono avere l&#39;affinità con l&#39;istanza AEM in cui hanno creato, un concetto noto come connessioni appiccicose. Lo scopo è garantire che gli aggiornamenti al contenuto presentino una latenza minima.

Per ulteriori informazioni sulla configurazione, consultare la [Documentazione del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

### Configurazione aggiuntiva {#additional-configuration}

#### Connessioni permanenti {#sticky-connections}

Le connessioni permanenti garantiscono che le pagine personalizzate e i dati delle sessioni per un utente siano tutti composti sulla stessa istanza di AEM. Questi dati vengono memorizzati nell&#39;istanza, pertanto le richieste successive dello stesso utente torneranno alla stessa istanza.

Si consiglia di abilitare le connessioni fissi per tutte le richieste di routing dei livelli interni alle istanze AEM, incoraggiando le richieste successive a raggiungere la stessa istanza AEM. Questo consente di ridurre la latenza che altrimenti risulta evidente quando il contenuto viene aggiornato tra le istanze.

#### Scadenza lunga {#long-expires}

Per impostazione predefinita, il contenuto inviato da un dispatcher AEM ha intestazioni Last-Modified ed Etag, senza alcuna indicazione della scadenza del contenuto. Anche se l’interfaccia utente ottiene sempre la versione più recente della risorsa, il browser esegue un’operazione di GET per verificare se la risorsa è cambiata. Ciò potrebbe causare più richieste alle quali la risposta HTTP è 304 (Non modificata), a seconda del caricamento della pagina. Per le risorse notoriamente non in scadenza, l’impostazione di un’intestazione Scadute e la rimozione delle intestazioni Last-Modified e ETag causeranno la memorizzazione del contenuto nella cache e non verranno effettuate ulteriori richieste di aggiornamento fino a quando non verrà soddisfatta la data nell’intestazione Expires.

Tuttavia, se si utilizza questo metodo non esiste alcun modo ragionevole per far scadere la risorsa nel browser prima della scadenza dell’intestazione Scade. Per ovviare a questo problema, è possibile configurare HtmlClientLibraryManager in modo da utilizzare URL immutabili per le librerie client.

Tali URL non verranno modificati. Quando il corpo della risorsa contenuta nell’URL cambia, le modifiche verranno automaticamente applicate all’URL, in modo che il browser richieda la versione corretta della risorsa.

La configurazione predefinita aggiunge un selettore a HtmlClientLibraryManager. Essendo un selettore, la risorsa viene memorizzata nella cache del dispatcher con il selettore intatto. Inoltre, questo selettore può essere utilizzato per garantire il corretto comportamento di scadenza. Il selettore predefinito segue il pattern `lc-.*?-lc`. Le seguenti direttive di configurazione Apache httpd garantiranno che tutte le richieste che corrispondono a tale pattern vengano servite con un tempo di scadenza adeguato.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Nessun sniff {#no-sniff}

Se il contenuto viene inviato senza alcun tipo di contenuto, molti browser tentano di indovinare il tipo di contenuto leggendo i primi byte del contenuto. Questo si chiama &quot;tirare su con il naso&quot;. La navigazione consente di aprire una vulnerabilità di sicurezza in quanto gli utenti in grado di scrivere nell’archivio possono caricare contenuti dannosi senza alcun tipo di contenuto.

Per questo motivo è consigliabile aggiungere un&#39;intestazione `no-sniff` alle risorse servite dal dispatcher. Tuttavia, il dispatcher non memorizza le intestazioni nella cache. Ciò significa che qualsiasi contenuto distribuito dal file system locale avrà il proprio tipo di contenuto determinato dall&#39;estensione, anziché utilizzare l&#39;intestazione del tipo di contenuto originale dal server di origine AEM.

Non è possibile abilitare alcun sniff se l&#39;applicazione Web non distribuisce mai risorse nella cache senza un tipo di file.

È possibile abilitare Nessuna stringa inclusiva:

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

Le impostazioni predefinite del dispatcher consentono l&#39;apertura dei criteri di protezione dei contenuti, noti anche come CSP. Questo consente a una pagina di caricare risorse da tutti i domini soggetti ai criteri predefiniti della sandbox del browser.

È consigliabile limitare la posizione in cui è possibile caricare le risorse per evitare di caricare il codice nel motore javascript da server esterni non attendibili o non verificati.

La CSP consente di regolare accuratamente le politiche. Tuttavia, in un&#39;applicazione complessa le intestazioni CSP devono essere sviluppate con cautela in quanto i criteri troppo restrittivi possono interrompere parti dell&#39;interfaccia utente.

>[!NOTE]
>
>Per ulteriori informazioni su come funziona, vedere la [pagina OWASP in Content Security Policy](https://www.owasp.org/index.php/Content_Security_Policy).

### Ridimensionamento {#sizing}

Per ulteriori informazioni sul ridimensionamento, vedere le [Linee guida sul ridimensionamento hardware](/help/managing/hardware-sizing-guidelines.md).

### Ottimizzazione delle prestazioni di MongoDB {#mongodb-performance-optimization}

Per informazioni generiche sulle prestazioni di MongoDB, vedere [Analisi delle prestazioni di MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitazioni note {#known-limitations}

### Installazioni simultanee {#concurrent-installations}

Anche se l&#39;uso simultaneo di più istanze AEM con un singolo database è supportato da MongoMK, le installazioni simultanee non lo sono.

Per risolvere il problema, accertatevi di eseguire prima l&#39;installazione con un singolo membro e di aggiungere gli altri al termine della prima installazione.

### Lunghezza nome pagina {#page-name-length}

Se AEM è in esecuzione su una distribuzione di gestione della persistenza MongoMK, i nomi di pagina [sono limitati a 150 caratteri.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Fare riferimento alla ](https://docs.mongodb.com/manual/reference/limits/) documentazione MongoDB per acquisire familiarità con i limiti e le soglie noti di MongoDB stesso.

