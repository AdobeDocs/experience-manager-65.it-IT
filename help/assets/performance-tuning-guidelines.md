---
title: Miglioramento delle prestazioni [!DNL Assets].
description: Suggerimenti e indicazioni su [!DNL Experience Manager] modifiche a componenti hardware, software e di rete per eliminare i colli di bottiglia e ottimizzare le prestazioni di [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2740'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guida all&#39;ottimizzazione delle prestazioni {#assets-performance-tuning-guide}

Un [!DNL Experience Manager Assets] la configurazione contiene diversi componenti hardware, software e di rete. A seconda dello scenario di distribuzione, per rimuovere i colli di bottiglia delle prestazioni potrebbe essere necessario apportare modifiche specifiche alla configurazione di hardware, software e componenti di rete.

Inoltre, l&#39;identificazione e il rispetto di determinate linee guida per l&#39;ottimizzazione hardware e software consentono di creare una solida base che consente [!DNL Experience Manager Assets] per soddisfare le aspettative in termini di prestazioni, scalabilità e affidabilità.

Prestazioni insoddisfacenti in [!DNL Experience Manager Assets] può influenzare l’esperienza utente in termini di prestazioni interattive, elaborazione delle risorse, velocità di download e altre aree.

In effetti, l’ottimizzazione delle prestazioni è un’attività fondamentale che esegui prima di stabilire metriche target per qualsiasi progetto.

Di seguito sono elencate alcune aree chiave intorno alle quali individuare e risolvere i problemi di prestazioni prima che abbiano un impatto sugli utenti.

## Platform {#platform}

Anche se Experience Manager è supportato su diverse piattaforme, Adobe ha trovato il massimo supporto per strumenti nativi su Linux e Windows, il che contribuisce a prestazioni ottimali e alla facilità di implementazione. È consigliabile implementare un sistema operativo a 64 bit per soddisfare i requisiti di memoria elevati di un [!DNL Experience Manager Assets] distribuzione. Come per qualsiasi implementazione di Experience Manager, è necessario implementare TarMK laddove possibile. Anche se TarMK non può essere scalato oltre una singola istanza di authoring, ha prestazioni migliori di MongoMK. Puoi aggiungere istanze di offload TarMK per aumentare la potenza di elaborazione del flusso di lavoro del tuo [!DNL Experience Manager Assets] distribuzione.

### Cartella temporanea {#temp-folder}

Per migliorare i tempi di caricamento delle risorse, utilizza uno storage ad alte prestazioni per la directory temporanea Java. Su Linux e Windows, è possibile utilizzare un&#39;unità RAM o un&#39;unità SSD. Negli ambienti basati su cloud è possibile utilizzare un tipo di storage equivalente ad alta velocità. Ad esempio, in Amazon EC2, un’ [trasmissione effimera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) può essere utilizzata per la cartella temporanea.

Se il server dispone di memoria sufficiente, configurare un&#39;unità RAM. Su Linux, eseguire i comandi seguenti per creare un&#39;unità RAM da 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Nel sistema operativo Windows, utilizzare un driver di terze parti per creare un&#39;unità RAM o semplicemente utilizzare storage ad alte prestazioni come SSD.

Quando il volume temporaneo ad alte prestazioni è pronto, impostare il parametro JVM `-Djava.io.tmpdir`. Ad esempio, puoi aggiungere il parametro JVM seguente al `CQ_JVM_OPTS` variabile in `bin/start` script di [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configurazione Java {#java-configuration}

### Versione Java {#java-version}

L’Adobe consiglia di distribuire [!DNL Experience Manager Assets] su Java 8 per prestazioni ottimali.

<!-- TBD: Link to the latest official word around Java.
-->

### Parametri JVM {#jvm-parameters}

Imposta i seguenti parametri JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=vero

## Archivio dati e configurazione della memoria {#data-store-and-memory-configuration}

### Configurazione archivio dati file {#file-data-store-configuration}

Si consiglia di separare l’archivio dati dall’archivio segmenti per tutti [!DNL Experience Manager Assets] utenti. Inoltre, la configurazione di `maxCachedBinarySize` e `cacheSizeInMB` I parametri possono aiutare a massimizzare le prestazioni. Imposta `maxCachedBinarySize` alle dimensioni di file più piccole che possono essere mantenute nella cache. Specifica la dimensione della cache in memoria da utilizzare per l’archivio dati in `cacheSizeInMB`. L’Adobe consiglia di impostare questo valore tra il 2 e il 10% della dimensione heap totale. Tuttavia, il test di carico/prestazioni può aiutare a determinare l’impostazione ideale.

### Configurare la dimensione massima della cache immagine nel buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Quando si caricano grandi quantità di risorse in [!DNL Adobe Experience Manager], per consentire picchi imprevisti nell’utilizzo della memoria e impedire errori JVM con OutOfMemoryErrors, riduci la dimensione massima configurata della cache immagine nel buffer. Prendi in considerazione un esempio di sistema con un heap massimo (- `Xmx`param) di 5 GB, un Oak BlobCache impostato su 1 GB e una cache dei documenti impostata su 2 GB. In questo caso, la cache nel buffer richiederebbe al massimo 1,25 GB e memoria, che lascerebbe solo 0,75 GB di memoria per picchi imprevisti.

Configura la dimensione della cache nel buffer nella console web OSGi. A `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, imposta la proprietà `cq.dam.image.cache.max.memory` in byte. Ad esempio, 1073741824 è 1 GB (1024 x 1024 x 1024 = 1 GB).

Dall&#39;Experience Manager 6.1 SP1, se si utilizza un `sling:osgiConfig` per configurare questa proprietà, assicurarsi di impostare il tipo di dati su Long. Per ulteriori dettagli, consulta [CQBufferedImageCache utilizza l’heap durante il caricamento delle risorse](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Archivi dati condivisi {#shared-data-stores}

L’implementazione di un archivio dati di file S3 o condiviso può contribuire a risparmiare spazio su disco e aumentare la velocità effettiva di rete nelle implementazioni su larga scala. Per ulteriori informazioni sui pro e i contro dell’utilizzo di un archivio dati condiviso, consulta [Guida al dimensionamento di Assets](/help/assets/assets-sizing-guide.md).

### Archivio dati S3 {#s-data-store}

La seguente configurazione dell’archivio dati S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ha aiutato Adobe a estrarre 12,8 TB di oggetti BLOB binari di grandi dimensioni da un archivio dati di file esistente in un archivio dati S3 presso un sito del cliente:

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Ottimizzazione della rete {#network-optimization}

L’Adobe consiglia di abilitare HTTPS, in quanto molte aziende dispongono di firewall che rilevano il traffico HTTP, con un conseguente impatto negativo sui caricamenti e sul danneggiamento dei file. Per i caricamenti di file di grandi dimensioni, accertati che gli utenti dispongano di connessioni cablate alla rete perché una rete WiFi si satura rapidamente. Per le linee guida sull&#39;identificazione dei colli di bottiglia della rete, vedere [Guida al dimensionamento di Assets](/help/assets/assets-sizing-guide.md). Per valutare le prestazioni della rete analizzando la topologia di rete, vedere [Considerazioni sulla rete delle risorse](/help/assets/assets-network-considerations.md).

La strategia di ottimizzazione della rete dipende principalmente dalla quantità di larghezza di banda disponibile e dal carico [!DNL Experience Manager] dell&#39;istanza. Opzioni di configurazione comuni, inclusi firewall o proxy, possono migliorare le prestazioni della rete. Di seguito sono riportati alcuni punti chiave da considerare:

* A seconda del tipo di istanza (piccola, moderata, grande), assicurati di disporre di una larghezza di banda di rete sufficiente per l’istanza di Experience Manager. Un&#39;adeguata allocazione della larghezza di banda è particolarmente importante se [!DNL Experience Manager] è in hosting su AWS.
* Se il [!DNL Experience Manager] L’istanza di è ospitata su AWS. Puoi trarne vantaggio disponendo di una policy di scalabilità versatile. Se gli utenti prevedono un carico elevato, esegui l’upsize dell’istanza. Scaricala per un carico moderato/basso.
* HTTPS: la maggior parte degli utenti dispone di firewall che rilevano il traffico HTTP, che può influire negativamente sul caricamento di file o persino file danneggiati durante l’operazione di caricamento.
* Caricamenti di file di grandi dimensioni: verifica che gli utenti dispongano di connessioni cablate alla rete (le connessioni Wi-Fi si interrompono rapidamente).

## Flussi di lavoro {#workflows}

### Flussi di lavoro transitori {#transient-workflows}

Se possibile, imposta [!UICONTROL Aggiorna risorsa DAM] del flusso di lavoro a Transient. L&#39;impostazione consente di ridurre in modo significativo i costi generali necessari per l&#39;elaborazione dei flussi di lavoro, poiché in questo caso non è necessario che i flussi di lavoro passino attraverso i normali processi di tracciamento e archiviazione.

1. Accedi a `/miscadmin` nel [!DNL Experience Manager] distribuzione in `https://[aem_server]:[port]/miscadmin`.

1. Espandi **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL dam]**.

1. Apri **[!UICONTROL Aggiorna risorsa DAM]**. Dal pannello strumenti mobile, passare alla **[!UICONTROL Pagina]** e quindi fare clic su **[!UICONTROL Proprietà pagina]**.

1. Seleziona **[!UICONTROL Flusso di lavoro transitorio]** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alcune funzioni non supportano flussi di lavoro transitori. Se il [!DNL Assets] La distribuzione richiede queste funzioni, non configurare flussi di lavoro transitori.

Nei casi in cui non è possibile utilizzare flussi di lavoro transitori, esegui regolarmente la rimozione del flusso di lavoro per eliminare quelli archiviati [!UICONTROL Aggiorna risorsa DAM] per garantire che le prestazioni del sistema non si deteriorino.

In genere, l’eliminazione dei flussi di lavoro viene eseguita settimanalmente. Tuttavia, in scenari che richiedono molte risorse, ad esempio durante l’inserimento di risorse su vasta scala, puoi eseguirle con maggiore frequenza.

Per configurare l’eliminazione del flusso di lavoro, aggiungi una nuova configurazione di eliminazione del flusso di lavoro Adobe Granite tramite la console OSGi. Quindi, configura e pianifica il flusso di lavoro come parte della finestra di manutenzione settimanale.

Se la rimozione dura troppo a lungo, si verifica un timeout. È quindi necessario assicurarsi che i processi di rimozione siano completati per evitare situazioni in cui la rimozione dei flussi di lavoro non riesce a completare a causa del numero elevato di flussi di lavoro.

Ad esempio, dopo l’esecuzione di numerosi flussi di lavoro non transitori (che creano nodi di istanze del flusso di lavoro), puoi eseguire [Rimozione flusso di lavoro ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) su base ad hoc. Rimuove immediatamente le istanze di flusso di lavoro completate e ridondanti anziché attendere l’esecuzione dello scheduler di eliminazione del flusso di lavoro Adobe Granite.

### Numero massimo processi paralleli {#maximum-parallel-jobs}

Per impostazione predefinita, [!DNL Experience Manager] esegue un numero massimo di processi paralleli uguale al numero di processori sul server. Il problema di questa impostazione è che durante i periodi di carico elevato, tutti i processori sono occupati da [!UICONTROL Aggiorna risorsa DAM] rallentamento dei tempi di risposta dell’interfaccia utente e prevenzione [!DNL Experience Manager] dall&#39;esecuzione di altri processi che salvaguardano le prestazioni e la stabilità del server. Come buona prassi, impostare questo valore su metà dei processori disponibili sul server eseguendo le operazioni seguenti:

1. On [!DNL Experience Manager] Autore, accesso `https://[aem_server]:[port]/system/console/slingevent`.

1. Clic **[!UICONTROL Modifica]** su ogni coda di flusso di lavoro rilevante per la tua implementazione, ad esempio, **[!UICONTROL Coda del flusso di lavoro transitorio Granite]**.

1. Aggiorna il valore di **[!UICONTROL Numero massimo processi paralleli]** e fai clic su **[!UICONTROL Salva]**.

Se si imposta una coda su metà dei processori disponibili, è possibile iniziare da. Tuttavia, potrebbe essere necessario aumentare o diminuire questo numero per raggiungere la velocità effettiva massima e regolarla in base all’ambiente. Esistono code separate per i flussi di lavoro transitori e non transitori e per altri processi, ad esempio i flussi di lavoro esterni. Se più code impostate sul 50% dei processori sono attive contemporaneamente, il sistema può sovraccaricare rapidamente. Le code utilizzate con maggiore frequenza variano notevolmente da un utente all’altro. Di conseguenza, potrebbe essere necessario configurarli accuratamente per la massima efficienza senza sacrificare la stabilità del server.

### Configurazione risorsa di aggiornamento DAM {#dam-update-asset-configuration}

Il [!UICONTROL Aggiorna risorsa DAM] Il flusso di lavoro contiene una suite completa di passaggi configurati per le attività, ad esempio la generazione di file PTIFF di Dynamic Medie e [!DNL Adobe InDesign Server] integrazione. Tuttavia, la maggior parte degli utenti potrebbe non richiedere diversi di questi passaggi. L’Adobe consiglia di creare una copia personalizzata del [!UICONTROL Aggiorna risorsa DAM] modello di flusso di lavoro e rimuovi eventuali passaggi non necessari. In questo caso, aggiorna i moduli di avvio per [!UICONTROL Aggiorna risorsa DAM] per puntare al nuovo modello.

Esecuzione di [!UICONTROL Aggiorna risorsa DAM] un flusso di lavoro intensivo può aumentare notevolmente le dimensioni dell’archivio dati dei file. I risultati di un esperimento condotto da Adobe hanno mostrato che la dimensione dell’archivio dati può aumentare di circa 400 GB se vengono eseguiti circa 5500 flussi di lavoro entro 8 ore.

Si tratta di un aumento temporaneo e l&#39;archivio dati viene ripristinato alle dimensioni originali dopo l&#39;esecuzione dell&#39;attività di raccolta oggetti inattivi dell&#39;archivio dati.

In genere, l’attività di Garbage Collection dell’archivio dati viene eseguita settimanalmente insieme ad altre attività di manutenzione pianificate.

Se lo spazio su disco è limitato ed è in esecuzione [!UICONTROL Aggiorna risorsa DAM] nei flussi di lavoro intensivi, è consigliabile pianificare l’attività di garbage collection con maggiore frequenza.

#### Generazione rendering runtime {#runtime-rendition-generation}

I clienti utilizzano immagini di varie dimensioni e formati sul proprio sito web o per la distribuzione ai partner aziendali. Poiché ogni rappresentazione si aggiunge all’impronta della risorsa nell’archivio, l’Adobe consiglia di utilizzare questa funzione in modo giudizioso. Per ridurre la quantità di risorse necessarie per elaborare e archiviare le immagini, è possibile generarle in fase di esecuzione anziché come rappresentazioni durante l’acquisizione.

Molti clienti Sites implementano un servlet per le immagini che ridimensiona e ritaglia le immagini al momento in cui vengono richieste, imponendo un carico aggiuntivo all’istanza Publish. Tuttavia, se queste immagini possono essere memorizzate nella cache, il problema può essere attenuato.

Un approccio alternativo consiste nell&#39;utilizzare la tecnologia Dynamic Medie per gestire completamente la manipolazione delle immagini. Inoltre, puoi implementare Brand Portal che non solo si assume le responsabilità di generazione delle rappresentazioni dal [!DNL Experience Manager] ma anche l&#39;intero livello di pubblicazione.

#### ImageMagick {#imagemagick}

Se si personalizza [!UICONTROL Aggiorna risorsa DAM] per generare le rappresentazioni utilizzando ImageMagick, l&#39;Adobe consiglia di modificare `policy.xml` file in `/etc/ImageMagick/`. Per impostazione predefinita, ImageMagick utilizza l&#39;intero spazio su disco disponibile sul volume del sistema operativo e la memoria disponibile. Apporta le seguenti modifiche alla configurazione all&#39;interno di `policymap` sezione di `policy.xml` per limitare queste risorse.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

Inoltre, impostare il percorso della cartella temporanea di ImageMagick in `configure.xml` file (o impostando la variabile di ambiente `MAGICK_TEMPORARY_PATH`) a una partizione del disco che disponga di spazio sufficiente e IOPS.

>[!CAUTION]
>
>Se ImageMagick utilizza tutto lo spazio disponibile su disco, un errore di configurazione può rendere il server instabile. Le modifiche alla policy necessarie per elaborare file di grandi dimensioni tramite ImageMagick possono influire sul [!DNL Experience Manager] prestazioni. Per ulteriori informazioni, consulta [installare e configurare ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` e `configure.xml` I file sono disponibili all&#39;indirizzo `/usr/lib64/ImageMagick-&#42;/config/` invece di `/etc/ImageMagick/`Vedere [Documentazione di ImageMagick](https://www.imagemagick.org/script/resources.php) per il percorso dei file di configurazione.

Se sta usando [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l’Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Collabora con il rappresentante dell’Assistenza clienti di Adobe per implementare queste best practice per la tua implementazione di AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbe non elaborare file PSB ad altissima risoluzione con una risoluzione superiore a 30000x23000 pixel.

### Write-back XMP {#xmp-writeback}

Il writeback dell&#39;XMP aggiorna la risorsa originale ogni volta che i metadati vengono modificati in [!DNL Experience Manager], che determina quanto segue:

* La risorsa stessa viene modificata
* Viene creata una versione della risorsa
* [!UICONTROL Aggiorna risorsa DAM] viene eseguito in base alla risorsa

I risultati elencati consumano risorse considerevoli. Pertanto, Adobe consiglia di disabilitare il writeback dell’XMP se non è necessario. Per ulteriori informazioni, consulta [Write-back XMP](/help/assets/xmp-writeback.md).

Se si seleziona il flag Esegui flussi di lavoro, l’importazione di una grande quantità di metadati può causare un’attività di writeback XMP che richiede molte risorse. Pianifica tale importazione durante l’utilizzo snello del server in modo che le prestazioni per altri utenti non siano influenzate.

## Replica {#replication}

Quando replichi le risorse in un numero elevato di istanze di pubblicazione, ad esempio in un’implementazione di Sites, l’Adobe consiglia di utilizzare la replica a catena. In questo caso, l’istanza di authoring viene replicata in una singola istanza di pubblicazione che a sua volta viene replicata nelle altre istanze di pubblicazione, liberando l’istanza di authoring.

### Configurare la replica a catena {#configure-chain-replication}

1. Scegli l’istanza di pubblicazione da utilizzare per il concatenamento delle repliche
1. In tale istanza di pubblicazione aggiungi agenti di replica che puntano alle altre istanze di pubblicazione
1. Su ciascuno di questi agenti di replica, abilita &quot;Alla ricezione&quot; nella scheda &quot;Triggers&quot;

>[!NOTE]
>
>L’Adobe non consiglia l’attivazione automatica delle risorse. Tuttavia, se necessario, Adobe consiglia di eseguire questo passaggio come passaggio finale in un flusso di lavoro, in genere Aggiorna risorsa DAM.

## Cerca indici {#search-indexes}

Installa [Service Pack più recenti](/help/release-notes/release-notes.md) e gli hotfix relativi alle prestazioni, in quanto spesso includono aggiornamenti agli indici di sistema. Consulta [suggerimenti per l&#39;ottimizzazione delle prestazioni](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) per alcune ottimizzazioni dell’indice.

Creare indici personalizzati per le query eseguite spesso. Per ulteriori informazioni, consulta [metodologia per l’analisi delle query lente](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [creazione di indici personalizzati](/help/sites-deploying/queries-and-indexing.md). Per ulteriori informazioni sulle best practice per query e indici, consulta [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurazioni dell’indice Lucene {#lucene-index-configurations}

È possibile eseguire alcune ottimizzazioni sulle configurazioni dell’indice Oak per migliorare [!DNL Experience Manager Assets] prestazioni. Aggiorna le configurazioni dell’indice per migliorare il tempo di reindicizzazione:

1. Apri CRXDe `/crx/de/index.jsp` e accedere come utente amministrativo.
1. Sfoglia per `/oak:index/lucene`.
1. Aggiungi un `String[]` proprietà `excludedPaths` con valori `/var`, `/etc/workflow/instances`, e `/etc/replication`.
1. Sfoglia per `/oak:index/damAssetLucene`. Aggiungi un `String[]` proprietà `includedPaths` con valore `/content/dam`. Salva le modifiche.

Se gli utenti non devono eseguire ricerche full-text delle risorse, ad esempio cercare il testo nei documenti PDF, disattivalo. È possibile migliorare le prestazioni dell&#39;indice disabilitando l&#39;indicizzazione full-text. Per disattivare [!DNL Apache Lucene] estrazione del testo, segui questi passaggi:

1. In entrata [!DNL Experience Manager] interfaccia, accesso [!UICONTROL Gestione pacchetti].
1. Carica e installa il pacchetto disponibile all’indirizzo [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Totale stima {#guess-total}

Quando si creano query che generano set di risultati di grandi dimensioni, utilizzare `guessTotal` per evitare l&#39;utilizzo intensivo della memoria durante l&#39;esecuzione.

## Problemi noti {#known-issues}

### File di grandi dimensioni {#large-files}

Esistono due importanti problemi noti relativi ai file di grandi dimensioni in [!DNL Experience Manager]. Quando le dimensioni dei file superano i 2 GB, la sincronizzazione in standby a freddo può esaurire la memoria. In alcuni casi, impedisce l&#39;esecuzione della sincronizzazione in standby. In altri casi, provoca l’arresto anomalo dell’istanza primaria. Questo scenario si applica a qualsiasi file in [!DNL Experience Manager] superiore a 2 GB, inclusi i pacchetti di contenuti.

Allo stesso modo, quando i file raggiungono le dimensioni di 2 GB durante l’utilizzo di un archivio dati S3 condiviso, potrebbe essere necessario un po’ di tempo per la completa persistenza del file dalla cache al file system. Di conseguenza, quando si utilizza la replica senza binario, è possibile che i dati binari non siano persistiti prima del completamento della replica. Questa situazione può causare problemi, soprattutto se la disponibilità dei dati è importante.

## Test delle prestazioni {#performance-testing}

Per ogni [!DNL Experience Manager] distribuzione, stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. Ecco alcune aree chiave su cui concentrarsi.

### Test di rete {#network-testing}

Per tutti i problemi relativi alle prestazioni di rete del cliente, eseguire le operazioni seguenti:

* Verifica delle prestazioni di rete all&#39;interno della rete del cliente
* Verifica le prestazioni della rete dall&#39;interno della rete Adobe. Per i clienti AMS, collabora con il tuo CSE per eseguire il test dall’interno della rete Adobe.
* Verifica delle prestazioni di rete da un altro punto di accesso
* Utilizzando uno strumento di benchmark di rete
* Esegui il test rispetto al dispatcher

### [!DNL Experience Manager] test di implementazione {#aem-deployment-testing}

Per ridurre al minimo la latenza e ottenere un throughput elevato grazie a un utilizzo efficiente della CPU e alla condivisione del carico, monitorare le prestazioni delle [!DNL Experience Manager] distribuzione regolare. In particolare:

* Eseguire test di carico su [!DNL Experience Manager] distribuzione.
* Monitora le prestazioni di caricamento e la reattività dell’interfaccia utente.

## [!DNL Experience Manager Assets] elenco di controllo delle prestazioni e impatto delle attività di gestione risorse {#checklist}

* Abilita HTTPS per aggirare eventuali sniffer del traffico HTTP aziendale.
* Utilizza una connessione cablata per caricare risorse pesanti.
* Implementare su Java 8.
* Imposta i parametri JVM ottimali.
* Configurare un file system DataStore o un archivio dati S3.
* Disattiva la generazione di risorse secondarie. Se è abilitata, il flusso di lavoro AEM crea una risorsa separata per ogni pagina in una risorsa multipagina. Ognuna di queste pagine è una singola risorsa che consuma ulteriore spazio su disco, richiede il controllo delle versioni e un’ulteriore elaborazione del flusso di lavoro. Se non hai bisogno di pagine separate, disabilita la generazione di risorse secondarie e le attività di estrazione delle pagine.
* Abilita flussi di lavoro transitori.
* Ottimizza le code del flusso di lavoro Granite per limitare i processi simultanei.
* Configura [!DNL ImageMagick] per limitare il consumo di risorse.
* Rimuovi i passaggi non necessari da [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro.
* Configura l’eliminazione del flusso di lavoro e della versione.
* Ottimizza gli indici con i Service Pack e gli hotfix più recenti. Rivolgiti all’Assistenza clienti Adobe per eventuali altre ottimizzazioni dell’indice disponibili.
* Utilizza guessTotal per ottimizzare le prestazioni delle query.
* Se configuri [!DNL Experience Manager] per rilevare i tipi di file dal contenuto dei file (abilitando **[!UICONTROL Servizio Day CQ DAM Mime Type]** nel **[!UICONTROL Console web AEM]**), carica molti file in blocco durante le ore non di picco, in quanto richiede molte risorse.
