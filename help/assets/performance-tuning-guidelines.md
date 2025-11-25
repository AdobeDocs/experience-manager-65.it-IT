---
title: Ottimizzazione delle prestazioni [!DNL Assets]
description: Suggerimenti e indicazioni sulla configurazione di  [!DNL Experience Manager] e sulle modifiche a componenti hardware, software e di rete per rimuovere i colli di bottiglia e ottimizzare le prestazioni di [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Developer, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# Guida all’ottimizzazione delle prestazioni di [!DNL Adobe Experience Manager Assets] {#assets-performance-tuning-guide}

Un&#39;installazione di [!DNL Experience Manager Assets] contiene diversi componenti hardware, software e di rete. A seconda dello scenario di distribuzione, per rimuovere i colli di bottiglia delle prestazioni potrebbe essere necessario apportare modifiche specifiche alla configurazione di hardware, software e componenti di rete.

Inoltre, l&#39;identificazione e il rispetto di determinate linee guida per l&#39;ottimizzazione hardware e software consentono di creare una solida base che consente all&#39;implementazione di [!DNL Experience Manager Assets] di soddisfare le aspettative in termini di prestazioni, scalabilità e affidabilità.

Le prestazioni insoddisfacenti in [!DNL Experience Manager Assets] possono influire sull&#39;esperienza utente in termini di prestazioni interattive, elaborazione delle risorse, velocità di download e altre aree.

In effetti, l’ottimizzazione delle prestazioni è un’attività fondamentale che esegui prima di stabilire metriche target per qualsiasi progetto.

Di seguito sono elencate alcune aree chiave intorno alle quali individuare e risolvere i problemi di prestazioni prima che abbiano un impatto sugli utenti.

## Platform {#platform}

Anche se Experience Manager è supportato su diverse piattaforme, Adobe ha trovato il maggiore supporto per strumenti nativi su Linux® e Windows, il che contribuisce a prestazioni ottimali e alla facilità di implementazione. È consigliabile distribuire un sistema operativo a 64 bit per soddisfare i requisiti di memoria elevati di una distribuzione di [!DNL Experience Manager Assets]. Come per qualsiasi implementazione di Experience Manager, è necessario implementare TarMK laddove possibile. Anche se TarMK non può essere scalato oltre una singola istanza di authoring, ha prestazioni migliori di MongoMK. È possibile aggiungere istanze di offload TarMK per aumentare la potenza di elaborazione del flusso di lavoro della distribuzione di [!DNL Experience Manager Assets].

### Cartella temporanea {#temp-folder}

Per migliorare i tempi di caricamento delle risorse, utilizza uno storage ad alte prestazioni per la directory temporanea Java. Su Linux® e Windows, è possibile utilizzare un&#39;unità RAM o un&#39;unità SSD. Negli ambienti basati su cloud è possibile utilizzare un tipo di storage equivalente ad alta velocità. In Amazon EC2, ad esempio, è possibile utilizzare un&#39;[unità temporanea](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) per la cartella temporanea.

Se il server dispone di memoria sufficiente, configurare un&#39;unità RAM. Su Linux®, eseguire i comandi seguenti per creare un&#39;unità RAM da 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Nel sistema operativo Windows, utilizzare un driver di terze parti per creare un&#39;unità RAM o semplicemente utilizzare storage ad alte prestazioni come SSD.

Quando il volume temporaneo ad alte prestazioni è pronto, impostare il parametro JVM `-Djava.io.tmpdir`. Ad esempio, puoi aggiungere il parametro JVM seguente alla variabile `CQ_JVM_OPTS` nello script `bin/start` di [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configurazione Java {#java-configuration}

### Versione Java {#java-version}

Adobe consiglia di distribuire [!DNL Experience Manager Assets] in Java 8 per ottenere prestazioni ottimali.

<!-- TBD: Link to the latest official word around Java.
-->

### Parametri JVM {#jvm-parameters}

Imposta i seguenti parametri JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Archivio dati e configurazione della memoria {#data-store-and-memory-configuration}

### Configurazione archivio dati file {#file-data-store-configuration}

La separazione dell&#39;archivio dati dall&#39;archivio segmenti è consigliata per tutti gli utenti [!DNL Experience Manager Assets]. Inoltre, la configurazione dei parametri `maxCachedBinarySize` e `cacheSizeInMB` può aiutare a massimizzare le prestazioni. Impostare `maxCachedBinarySize` sulla dimensione file più piccola che può essere contenuta nella cache. Specificare la dimensione della cache in memoria da utilizzare per l&#39;archivio dati in `cacheSizeInMB`. Adobe consiglia di impostare questo valore tra il 2 e il 10% della dimensione heap totale. Tuttavia, il test di carico/prestazioni può aiutare a determinare l’impostazione ideale.

### Configurare la dimensione massima della cache immagine nel buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Quando si caricano grandi quantità di risorse in [!DNL Adobe Experience Manager], per consentire picchi imprevisti di consumo di memoria e impedire errori JVM con OutOfMemoryErrors, ridurre la dimensione massima configurata della cache immagine nel buffer. Si consideri ad esempio un sistema con un heap massimo (- `Xmx`param) di 5 GB, un Oak BlobCache impostato su 1 GB e una cache dei documenti impostata su 2 GB. In questo caso, la cache nel buffer richiederebbe un massimo di 1,25 GB e memoria, che lascerebbe solo 0,75 GB di memoria per picchi imprevisti.

Configura la dimensione della cache nel buffer nella console web OSGi. In `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, impostare la proprietà `cq.dam.image.cache.max.memory` in byte. Ad esempio, 1073741824 è 1 GB (1024 x 1024 x 1024 = 1 GB).

Da Experience Manager 6.1 SP1, se utilizzi un nodo `sling:osgiConfig` per configurare questa proprietà, assicurati di impostare il tipo di dati su Long.

### Archivi dati condivisi {#shared-data-stores}

L’implementazione di un archivio dati di file S3 o condiviso può contribuire a risparmiare spazio su disco e aumentare la velocità effettiva di rete nelle implementazioni su larga scala. Per ulteriori informazioni sui pro e i contro dell&#39;utilizzo di un datastore condiviso, consulta la [guida al dimensionamento di Assets](/help/assets/assets-sizing-guide.md).

### Archivio dati S3 {#s-data-store}

La seguente configurazione dell&#39;archivio dati S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ha aiutato Adobe a estrarre 12,8 TB di BLOB (Binary Large Object) da un archivio dati file esistente in un archivio dati S3 presso un sito del cliente:

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

Adobe consiglia di abilitare HTTPS, in quanto molte aziende dispongono di firewall che rilevano il traffico HTTP, il che influisce negativamente sui caricamenti e danneggia i file. Per i caricamenti di file di grandi dimensioni, accertati che gli utenti dispongano di connessioni cablate alla rete perché una rete WiFi si satura rapidamente. Per le linee guida sull&#39;identificazione dei colli di bottiglia di rete, vedere la [Guida al dimensionamento di Assets](/help/assets/assets-sizing-guide.md). Per valutare le prestazioni della rete analizzando la topologia di rete, vedere [Considerazioni sulla rete Assets](/help/assets/assets-network-considerations.md).

La strategia di ottimizzazione della rete dipende principalmente dalla quantità di larghezza di banda disponibile e dal carico dell&#39;istanza [!DNL Experience Manager]. Opzioni di configurazione comuni, inclusi firewall o proxy, possono contribuire a migliorare le prestazioni della rete. Di seguito sono riportati alcuni punti chiave da considerare:

* A seconda del tipo di istanza (piccola, moderata, grande), assicurati di disporre di una larghezza di banda di rete sufficiente per l’istanza Experience Manager. Un&#39;adeguata allocazione della larghezza di banda è particolarmente importante se [!DNL Experience Manager] è ospitato su AWS.
* Se l&#39;istanza di [!DNL Experience Manager] è ospitata su AWS, è possibile ottenere vantaggi grazie a criteri di scalabilità versatili. Se gli utenti prevedono un carico elevato, esegui l’upsize dell’istanza. Scaricala per un carico moderato/basso.
* HTTPS: la maggior parte degli utenti dispone di firewall che rilevano il traffico HTTP, che può influire negativamente sul caricamento di file o persino file danneggiati durante l’operazione di caricamento.
* Caricamenti di file di grandi dimensioni: verifica che gli utenti dispongano di connessioni cablate alla rete (le connessioni Wi-Fi si interrompono rapidamente).

## Flussi di lavoro {#workflows}

### Flussi di lavoro transitori {#transient-workflows}

Se possibile, imposta il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] su Transitorio. L&#39;impostazione consente di ridurre in modo significativo i costi generali necessari per l&#39;elaborazione dei flussi di lavoro, poiché in questo caso non è necessario che i flussi di lavoro passino attraverso i normali processi di tracciamento e archiviazione.

1. Passare a `/miscadmin` nella distribuzione di [!DNL Experience Manager] in `https://[aem_server]:[port]/miscadmin`.

1. Espandi **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL dam]**.

1. Apri **[!UICONTROL Risorsa di aggiornamento DAM]**. Dal pannello degli strumenti mobile, passare alla scheda **[!UICONTROL Pagina]** e quindi fare clic su **[!UICONTROL Proprietà pagina]**.

1. Seleziona **[!UICONTROL Flusso di lavoro transitorio]** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alcune funzioni non supportano flussi di lavoro transitori. Se la distribuzione di [!DNL Assets] richiede queste funzionalità, non configurare flussi di lavoro transitori.

Nei casi in cui non è possibile utilizzare flussi di lavoro transitori, esegui regolarmente la rimozione del flusso di lavoro per eliminare i flussi di lavoro [!UICONTROL Risorsa di aggiornamento DAM] archiviati per garantire che le prestazioni del sistema non diminuiscano.

In genere, l’eliminazione dei flussi di lavoro viene eseguita settimanalmente. Tuttavia, in scenari che richiedono molte risorse, ad esempio durante l’inserimento di risorse su vasta scala, puoi eseguirle con maggiore frequenza.

Per configurare l’eliminazione del flusso di lavoro, aggiungi una nuova configurazione di Adobe Granite Workflow Purge tramite la console OSGi. Quindi, configura e pianifica il flusso di lavoro come parte della finestra di manutenzione settimanale.

Se la rimozione dura troppo a lungo, si verifica un timeout. È quindi necessario assicurarsi che i processi di rimozione siano completati per evitare situazioni in cui la rimozione dei flussi di lavoro non riesce a completare a causa del numero elevato di flussi di lavoro.

Ad esempio, dopo aver eseguito numerosi flussi di lavoro non transitori (che creano i nodi dell&#39;istanza del flusso di lavoro), puoi eseguire [Rimozione flusso di lavoro ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) su base ad hoc. Rimuove immediatamente le istanze di flusso di lavoro completate e ridondanti anziché attendere l’esecuzione dello scheduler di eliminazione dei flussi di lavoro di Adobe Granite.

### Numero massimo processi paralleli {#maximum-parallel-jobs}

Per impostazione predefinita, [!DNL Experience Manager] esegue un numero massimo di processi paralleli pari al numero di processori sul server. Il problema con questa impostazione è che durante periodi di carico elevato, tutti i processori sono occupati da [!UICONTROL flussi di lavoro Aggiorna risorsa DAM], rallentando la reattività dell&#39;interfaccia utente e impedendo a [!DNL Experience Manager] di eseguire altri processi che salvaguardano le prestazioni e la stabilità del server. Come buona prassi, impostare questo valore su metà dei processori disponibili sul server eseguendo le operazioni seguenti:

1. All&#39;autore [!DNL Experience Manager], accedere a `https://[aem_server]:[port]/system/console/slingevent`.

1. Fai clic su **[!UICONTROL Modifica]** in ogni coda del flusso di lavoro rilevante per l&#39;implementazione, ad esempio **[!UICONTROL Coda del flusso di lavoro transitorio Granite]**.

1. Aggiorna il valore di **[!UICONTROL Numero massimo processi paralleli]** e fai clic su **[!UICONTROL Salva]**.

Se si imposta una coda su metà dei processori disponibili, è possibile iniziare da. Tuttavia, potrebbe essere necessario aumentare o diminuire questo numero per raggiungere la velocità effettiva massima e regolarla in base all’ambiente. Esistono code separate per i flussi di lavoro transitori e non transitori e per altri processi, ad esempio i flussi di lavoro esterni. Se più code impostate sul 50% dei processori sono attive contemporaneamente, il sistema può sovraccaricare rapidamente. Le code utilizzate con maggiore frequenza variano notevolmente da un utente all’altro. Di conseguenza, potrebbe essere necessario configurarli accuratamente per la massima efficienza senza sacrificare la stabilità del server.

### Configurazione risorsa di aggiornamento DAM {#dam-update-asset-configuration}

Il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] contiene una suite completa di passaggi configurati per le attività, ad esempio la generazione PTIFF di elementi multimediali dinamici e l&#39;integrazione di [!DNL Adobe InDesign Server]. Tuttavia, la maggior parte degli utenti potrebbe non richiedere diversi di questi passaggi. Adobe consiglia di creare una copia personalizzata del modello di flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] e di rimuovere tutti i passaggi non necessari. In questo caso, aggiorna i moduli di avvio per [!UICONTROL Risorsa di aggiornamento DAM] in modo che puntino al nuovo modello.

L&#39;esecuzione intensiva del flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] può aumentare notevolmente le dimensioni dell&#39;archivio dati dei file. I risultati di un esperimento eseguito da Adobe hanno mostrato che la dimensione dell’archivio dati può aumentare di circa 400 GB se vengono eseguiti circa 5500 flussi di lavoro entro 8 ore.

Si tratta di un aumento temporaneo e l&#39;archivio dati viene ripristinato alle dimensioni originali dopo l&#39;esecuzione dell&#39;attività di raccolta oggetti inattivi dell&#39;archivio dati.

In genere, l’attività di Garbage Collection dell’archivio dati viene eseguita settimanalmente insieme ad altre attività di manutenzione pianificate.

Se lo spazio su disco è limitato ed esegui intensamente i flussi di lavoro [!UICONTROL Risorsa di aggiornamento DAM], puoi pianificare l&#39;attività di Garbage Collection con maggiore frequenza.

#### Generazione rendering runtime {#runtime-rendition-generation}

I clienti utilizzano immagini di varie dimensioni e formati sul proprio sito web o per la distribuzione ai partner aziendali. Poiché ogni rappresentazione si aggiunge all’impronta della risorsa nell’archivio, Adobe consiglia di utilizzare questa funzione in modo giudizioso. Per ridurre la quantità di risorse necessarie per elaborare e archiviare le immagini, è possibile generarle in fase di esecuzione anziché come rappresentazioni durante l’acquisizione.

Molti clienti Sites implementano un servlet per le immagini che ridimensiona e ritaglia le immagini al momento in cui vengono richieste, imponendo un carico aggiuntivo all’istanza Publish. Tuttavia, se queste immagini possono essere memorizzate nella cache, il problema può essere attenuato.

Un approccio alternativo consiste nell’utilizzare la tecnologia Dynamic Media per gestire completamente la manipolazione delle immagini. Inoltre, è possibile distribuire un Brand Portal che si assuma non solo le responsabilità di generazione delle rappresentazioni dall&#39;infrastruttura [!DNL Experience Manager], ma anche l&#39;intero livello di pubblicazione.

#### ImageMagick {#imagemagick}

Se personalizzi il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] per generare rappresentazioni utilizzando ImageMagick, Adobe consiglia di modificare il file `policy.xml` in `/etc/ImageMagick/`. Per impostazione predefinita, ImageMagick utilizza l&#39;intero spazio su disco disponibile sul volume del sistema operativo e la memoria disponibile. Apportare le seguenti modifiche alla configurazione nella sezione `policymap` di `policy.xml` per limitare queste risorse.

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

Inoltre, impostare il percorso della cartella temporanea di ImageMagick nel file `configure.xml` (o impostando la variabile di ambiente `MAGICK_TEMPORARY_PATH`) su una partizione del disco con spazio sufficiente e IOPS.

>[!CAUTION]
>
>Se ImageMagick utilizza tutto lo spazio disponibile su disco, un errore di configurazione può rendere il server instabile. Le modifiche della policy necessarie per elaborare file di grandi dimensioni tramite ImageMagick potrebbero influire sulle prestazioni di [!DNL Experience Manager]. Per ulteriori informazioni, vedere [installare e configurare ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>I file ImageMagick `policy.xml` e `configure.xml` sono disponibili in `/usr/lib64/ImageMagick-&#42;/config/` anziché `/etc/ImageMagick/`. Per informazioni sul percorso dei file di configurazione, vedere la documentazione di ImageMagick (`https://www.imagemagick.org/script/resources.php` sito Web).

Se utilizzi [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l&#39;Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Collabora con un rappresentante dell’Assistenza clienti Adobe per implementare queste best practice per la tua implementazione di AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbe non elaborare file PSB ad alta risoluzione con più di 30000 x 23000 pixel.

### writeback di XMP {#xmp-writeback}

Il writeback di XMP aggiorna la risorsa originale ogni volta che i metadati vengono modificati in [!DNL Experience Manager], con il risultato seguente:

* La risorsa stessa viene modificata
* Viene creata una versione della risorsa
* [!UICONTROL Risorsa di aggiornamento DAM] eseguita per la risorsa

I risultati elencati consumano risorse considerevoli. Pertanto, Adobe consiglia di disabilitare il writeback di XMP se non è necessario. Per ulteriori informazioni, vedere [XMP writeback](/help/assets/xmp-writeback.md).

L&#39;importazione di una grande quantità di metadati può comportare un&#39;attività di writeback di XMP che richiede molte risorse se il flag Esegui flussi di lavoro è selezionato. Pianifica tale importazione durante l’utilizzo snello del server in modo che le prestazioni per altri utenti non siano influenzate.

## Replica {#replication}

Quando replichi le risorse in un numero elevato di istanze di pubblicazione, ad esempio in un’implementazione di Sites, Adobe consiglia di utilizzare la replica a catena. In questo caso, l’istanza di authoring viene replicata in una singola istanza di pubblicazione che a sua volta viene replicata nelle altre istanze di pubblicazione, liberando l’istanza di authoring.

### Configurare la replica a catena {#configure-chain-replication}

1. Scegli l’istanza di pubblicazione da utilizzare per il concatenamento delle repliche
1. In tale istanza di pubblicazione aggiungi agenti di replica che puntano alle altre istanze di pubblicazione
1. Su ciascuno di questi agenti di replica, abilita &quot;Alla ricezione&quot; nella scheda &quot;Triggers&quot;

>[!NOTE]
>
>Adobe consiglia di non attivare automaticamente le risorse. Tuttavia, se necessario, Adobe consiglia di eseguire questo passaggio come passaggio finale in un flusso di lavoro, in genere Aggiorna risorsa DAM.

## Cerca indici {#search-indexes}

Installa [i Service Pack più recenti](/help/release-notes/release-notes.md) e gli hotfix relativi alle prestazioni, in quanto spesso includono aggiornamenti agli indici di sistema. Consulta [suggerimenti per l&#39;ottimizzazione delle prestazioni](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/administer/performance-tuning-guidelines) per alcune ottimizzazioni dell&#39;indice.

Creare indici personalizzati per le query eseguite spesso. Per informazioni dettagliate, consulta la [metodologia per l&#39;analisi delle query lente](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [creazione di indici personalizzati](/help/sites-deploying/queries-and-indexing.md). Per ulteriori informazioni sulle best practice per query e indici, consulta [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurazioni dell’indice Lucene {#lucene-index-configurations}

È possibile eseguire alcune ottimizzazioni sulle configurazioni dell&#39;indice Oak per migliorare le prestazioni di [!DNL Experience Manager Assets]. Aggiorna le configurazioni dell’indice per migliorare il tempo di reindicizzazione:

1. Aprire CRXDe `/crx/de/index.jsp` e accedere come utente amministrativo.
1. Passare a `/oak:index/lucene`.
1. Aggiungere una proprietà `String[]` `excludedPaths` con valori `/var`, `/etc/workflow/instances` e `/etc/replication`.
1. Passare a `/oak:index/damAssetLucene`. Aggiungere una proprietà `String[]` `includedPaths` con valore `/content/dam`. Salva le modifiche.

Se gli utenti non devono eseguire ricerche full-text delle risorse, ad esempio cercare il testo nei documenti di PDF, disattivalo. È possibile migliorare le prestazioni dell&#39;indice disabilitando l&#39;indicizzazione full-text. Per disabilitare l&#39;estrazione del testo [!DNL Apache Lucene], eseguire la procedura seguente:

1. Nell&#39;interfaccia [!DNL Experience Manager], accedere a [!UICONTROL Gestione pacchetti].
1. Carica e installa il pacchetto disponibile in [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Totale stima {#guess-total}

Durante la creazione di query che generano set di risultati di grandi dimensioni, utilizzare il parametro `guessTotal` per evitare l&#39;utilizzo di memoria pesante durante l&#39;esecuzione.

## Problemi noti {#known-issues}

### File di grandi dimensioni {#large-files}

Esistono due importanti problemi noti relativi ai file di grandi dimensioni in [!DNL Experience Manager]. Quando le dimensioni dei file superano i 2 GB, la sincronizzazione in standby a freddo può esaurire la memoria. In alcuni casi, impedisce l&#39;esecuzione della sincronizzazione in standby. In altri casi, provoca l’arresto anomalo dell’istanza primaria. Questo scenario si applica a qualsiasi file in [!DNL Experience Manager] di dimensioni superiori a 2 GB, inclusi i pacchetti di contenuto.

Allo stesso modo, quando i file raggiungono le dimensioni di 2 GB durante l’utilizzo di un archivio dati S3 condiviso, potrebbe essere necessario un po’ di tempo per la completa persistenza del file dalla cache al file system. Di conseguenza, quando si utilizza la replica senza binario, è possibile che i dati binari non siano persistiti prima del completamento della replica. Questa situazione può causare problemi, soprattutto se la disponibilità dei dati è importante.

## Test delle prestazioni {#performance-testing}

Per ogni distribuzione di [!DNL Experience Manager], stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. Ecco alcune aree chiave su cui concentrarsi.

### Test di rete {#network-testing}

Per tutti i problemi relativi alle prestazioni della rete per il cliente, eseguire le operazioni seguenti:

* Verifica delle prestazioni di rete all&#39;interno della rete del cliente
* Verifica le prestazioni della rete dall’interno della rete Adobe. Per i clienti AMS, collabora con il tuo CSE per eseguire test dall’interno della rete Adobe.
* Verifica delle prestazioni di rete da un altro punto di accesso
* Utilizzando uno strumento di benchmark di rete
* Esegui il test rispetto al Dispatcher

### Test di distribuzione di [!DNL Experience Manager] {#aem-deployment-testing}

Per ridurre al minimo la latenza e ottenere un throughput elevato grazie all&#39;utilizzo efficiente di CPU e alla condivisione del carico, monitorare regolarmente le prestazioni dell&#39;implementazione di [!DNL Experience Manager]. In particolare:

* Eseguire i test di carico per la distribuzione [!DNL Experience Manager].
* Monitora le prestazioni di caricamento e la reattività dell’interfaccia utente.

## Elenco di controllo delle prestazioni di [!DNL Experience Manager Assets] e impatto delle attività di gestione risorse {#checklist}

* Abilita HTTPS per aggirare eventuali sniffer del traffico HTTP aziendale.
* Utilizza una connessione cablata per caricare risorse pesanti.
* Implementare su Java 8.
* Imposta i parametri JVM ottimali.
* Configurare un file system DataStore o un archivio dati S3.
* Disattiva la generazione di risorse secondarie. Se è abilitata, il flusso di lavoro di AEM crea una risorsa separata per ogni pagina in una risorsa multipagina. Ognuna di queste pagine è una singola risorsa che consuma ulteriore spazio su disco, richiede il controllo delle versioni e un’ulteriore elaborazione del flusso di lavoro. Se non hai bisogno di pagine separate, disabilita la generazione di risorse secondarie e le attività di estrazione delle pagine.
* Abilita flussi di lavoro transitori.
* Ottimizza le code del flusso di lavoro Granite per limitare i processi simultanei.
* Configura [!DNL ImageMagick] per limitare il consumo di risorse.
* Rimuovi i passaggi non necessari dal flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].
* Configura l’eliminazione del flusso di lavoro e della versione.
* Ottimizza gli indici con i Service Pack e gli hotfix più recenti. Rivolgiti all’Assistenza clienti di Adobe per ulteriori ottimizzazioni dell’indice eventualmente disponibili.
* Utilizza guessTotal per ottimizzare le prestazioni delle query.
* Se si configura [!DNL Experience Manager] per rilevare i tipi di file dal contenuto dei file (abilitando **[!UICONTROL Day CQ DAM Mime Type Service]** nella **[!UICONTROL console Web AEM]**), caricare in blocco molti file nelle ore non di punta, poiché la procedura è intensiva a livello di risorse.
