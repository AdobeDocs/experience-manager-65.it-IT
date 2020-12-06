---
title: Ottimizzazione delle prestazioni [!DNL Assets].
description: Suggerimenti e indicazioni sulla configurazione  [!DNL Experience Manager] modifiche a hardware, software e componenti di rete per rimuovere i colli di bottiglia e ottimizzare le prestazioni di [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '2744'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guida per l&#39;ottimizzazione delle prestazioni  {#assets-performance-tuning-guide}

Un&#39;installazione [!DNL Experience Manager Assets] contiene una serie di componenti hardware, software e di rete. A seconda dello scenario di distribuzione, potrebbe essere necessario apportare modifiche specifiche alla configurazione di hardware, software e componenti di rete per rimuovere i colli di bottiglia delle prestazioni.

Inoltre, l&#39;identificazione e il rispetto di alcune linee guida per l&#39;ottimizzazione hardware e software consente di creare solide basi per la distribuzione [!DNL Experience Manager Assets] in grado di soddisfare le aspettative in termini di prestazioni, scalabilità e affidabilità.

Le prestazioni scadenti in [!DNL Experience Manager Assets] possono influire sulle prestazioni interattive, l&#39;elaborazione delle risorse, la velocità di download e altre aree.

In realtà, l&#39;ottimizzazione delle prestazioni è un&#39;attività fondamentale che esegui prima di stabilire le metriche di destinazione per qualsiasi progetto.

Di seguito sono riportate alcune aree di interesse principali intorno alle quali è possibile individuare e risolvere problemi di prestazioni prima che abbiano un impatto sugli utenti.

## Platform {#platform}

Sebbene  Experience Manager sia supportato su diverse piattaforme,  Adobe ha trovato il maggiore supporto per gli strumenti nativi su Linux e Windows, che contribuisce a migliorare le prestazioni e la facilità di implementazione. È consigliabile implementare un sistema operativo a 64 bit in grado di soddisfare i requisiti di memoria elevati di una distribuzione [!DNL Experience Manager Assets]. Come per ogni implementazione  Experience Manager, è necessario implementare TarMK laddove possibile. Mentre TarMK non può essere ridimensionato oltre una singola istanza di creazione, si è scoperto che funziona meglio di MongoMK. Potete aggiungere istanze di offload TarMK per aumentare la potenza di elaborazione del flusso di lavoro della distribuzione [!DNL Experience Manager Assets].

### Cartella temporanea {#temp-folder}

Per migliorare i tempi di caricamento delle risorse, utilizzate lo storage ad alte prestazioni per la directory temporanea Java. In Linux e Windows, è possibile utilizzare un&#39;unità RAM o SSD. In ambienti basati su cloud, è possibile utilizzare un tipo di storage ad alta velocità equivalente. Ad esempio in  Amazon EC2, per la cartella temporanea è possibile utilizzare un&#39;unità [effimera](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html).

Presupponendo che il server disponga di memoria sufficiente, configurare un’unità RAM. In Linux, eseguite questi comandi per creare un&#39;unità RAM da 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

In Windows OS, utilizzare un driver di terze parti per creare un&#39;unità RAM o semplicemente utilizzare storage ad alte prestazioni come SSD.

Una volta pronto il volume temporaneo ad alte prestazioni, impostare il parametro JVM `-Djava.io.tmpdir`. Ad esempio, è possibile aggiungere il parametro JVM di seguito alla variabile `CQ_JVM_OPTS` nello script `bin/start` di [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configurazione Java {#java-configuration}

### Versione Java {#java-version}

 Adobe consiglia di distribuire [!DNL Experience Manager Assets] su Java 8 per ottenere prestazioni ottimali.

<!-- TBD: Link to the latest official word around Java.
-->

### Parametri JVM {#jvm-parameters}

Impostate i seguenti parametri JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=vero

## Configurazione dell&#39;archivio dati e della memoria {#data-store-and-memory-configuration}

### Configurazione archivio dati file {#file-data-store-configuration}

La separazione dell&#39;archivio dati dall&#39;archivio segmenti è consigliata per tutti gli utenti [!DNL Experience Manager Assets]. Inoltre, la configurazione dei parametri `maxCachedBinarySize` e `cacheSizeInMB` può contribuire a ottimizzare le prestazioni. Impostare `maxCachedBinarySize` sulla dimensione file più piccola che può essere mantenuta nella cache. Specificate la dimensione della cache in memoria da utilizzare per il datastore all&#39;interno di `cacheSizeInMB`.  Adobe consiglia di impostare questo valore tra il 2 e il 10% della dimensione totale dell&#39;heap. Tuttavia, il test di carico/prestazioni può aiutare a determinare l&#39;impostazione ideale.

### Configurare la dimensione massima della cache delle immagini nel buffer {#configure-the-maximum-size-of-the-buffered-image-cache}

Quando si caricano grandi quantità di risorse su [!DNL Adobe Experience Manager], per consentire picchi imprevisti nel consumo di memoria e per evitare errori JVM con OutOfMemoryErrors, ridurre la dimensione massima configurata della cache delle immagini nel buffer. Si consideri un esempio di sistema con un heap massimo (- `Xmx`param) di 5 GB, un Oak BlobCache impostato su 1 GB e una cache del documento impostata su 2 GB. In questo caso, la cache nel buffer richiederebbe al massimo 1,25 GB di memoria, lasciando solo 0,75 GB di memoria per picchi imprevisti.

Configurare la dimensione della cache nel buffer nella console Web OSGi. In `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, impostare la proprietà `cq.dam.image.cache.max.memory` in byte. Ad esempio, 1073741824 è 1 GB (1024 x 1024 x 1024 = 1 GB).

 Experience Manager 6.1 SP1, se si utilizza un nodo `sling:osgiConfig` per configurare questa proprietà, assicurarsi di impostare il tipo di dati su Long. Per ulteriori informazioni, consultate [CQBufferedImageCache consuma un heap durante il caricamento delle risorse](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Memorizzazione dati condivisa {#shared-data-stores}

L&#39;implementazione di un archivio dati file S3 o condiviso può contribuire a risparmiare spazio su disco e ad aumentare il throughput di rete nelle implementazioni su larga scala. Per ulteriori informazioni sui pro e i contro dell&#39;utilizzo di un datastore condiviso, vedere [Guida al ridimensionamento delle risorse](/help/assets/assets-sizing-guide.md).

### Archivio dati S3 {#s-data-store}

La seguente configurazione dell&#39;archivio dati S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ha aiutato  Adobe a estrarre 12,8 TB di oggetti binari di grandi dimensioni (BLOB) da un archivio dati di file esistente in un archivio dati S3 presso un sito cliente:

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

 Adobe consiglia di abilitare HTTPS perché molte aziende dispongono di firewall che troncano il traffico HTTP, il che influisce negativamente sui caricamenti e corrompe i file. Per caricamenti di file di grandi dimensioni, accertatevi che gli utenti dispongano di connessioni cablate alla rete perché una rete WiFi diventa rapidamente saturata. Per linee guida sull&#39;identificazione dei colli di bottiglia della rete, consultate [Guida al ridimensionamento delle risorse](/help/assets/assets-sizing-guide.md). Per valutare le prestazioni della rete analizzando la topologia di rete, vedere [Considerazioni sulla rete delle risorse](/help/assets/assets-network-considerations.md).

In primo luogo, la strategia di ottimizzazione della rete dipende dalla quantità di larghezza di banda disponibile e dal carico sull&#39;istanza [!DNL Experience Manager]. Le comuni opzioni di configurazione, inclusi firewall o proxy, possono migliorare le prestazioni della rete. Ecco alcuni punti chiave da tenere a mente:

* A seconda del tipo di istanza (piccolo, moderato, grande), accertatevi di disporre di una larghezza di banda di rete sufficiente per l’istanza del Experience Manager . Un&#39;adeguata allocazione della larghezza di banda è particolarmente importante se [!DNL Experience Manager] è in hosting su AWS.
* Se l&#39;istanza [!DNL Experience Manager] è ospitata su AWS, è possibile trarre vantaggio da un criterio di ridimensionamento versatile. Aggiornate l&#39;istanza se gli utenti prevedono un carico elevato. Sgrandisci per un carico moderato o basso.
* HTTPS: La maggior parte degli utenti dispone di firewall che troncano il traffico HTTP, il che può avere un impatto negativo sul caricamento di file o persino di file danneggiati durante l’operazione di caricamento.
* Caricamenti di file di grandi dimensioni: Verificate che gli utenti dispongano di connessioni cablate alla rete (le connessioni WiFi si saturano rapidamente).

## Flussi di lavoro {#workflows}

### Flussi di lavoro transitori {#transient-workflows}

Se possibile, impostate il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] su Temporaneo. L&#39;impostazione riduce notevolmente i costi generali necessari per l&#39;elaborazione dei flussi di lavoro perché, in questo caso, i flussi di lavoro non devono passare attraverso i normali processi di monitoraggio e archiviazione.

1. Passare a `/miscadmin` nella distribuzione [!DNL Experience Manager] in `https://[aem_server]:[port]/miscadmin`.

1. Espandete **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL dam]**.

1. Aprire **[!UICONTROL DAM Update Asset]**. Dal pannello degli strumenti mobile, passare alla scheda **[!UICONTROL Pagina]**, quindi fare clic su **[!UICONTROL Proprietà pagina]**.

1. Selezionare **[!UICONTROL Flusso di lavoro transitorio]** e fare clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alcune funzioni non supportano flussi di lavoro transitori. Se la distribuzione [!DNL Assets] richiede queste funzionalità, non configurate flussi di lavoro transitori.

Nei casi in cui non è possibile utilizzare flussi di lavoro transitori, esegui regolarmente la rimozione del flusso di lavoro per eliminare i flussi di lavoro [!UICONTROL DAM Update Asset] archiviati, in modo da garantire che le prestazioni del sistema non subiscano rallentamenti.

In genere, i flussi di lavoro di eliminazione vengono eseguiti settimanalmente. Tuttavia, negli scenari che richiedono risorse, ad esempio durante l’assimilazione di risorse su larga scala, potete eseguirle con maggiore frequenza.

Per configurare la rimozione del flusso di lavoro, aggiungete una nuova configurazione di rimozione del flusso di lavoro granito  Adobe tramite la console OSGi. Quindi, configurate e pianificate il flusso di lavoro come parte della finestra di manutenzione settimanale.

Se l&#39;eliminazione dura troppo, si verifica un timeout. È quindi necessario assicurarsi che i processi di eliminazione siano completati in modo da evitare situazioni in cui i flussi di lavoro di eliminazione non vengono completati a causa dell’elevato numero di flussi di lavoro.

Ad esempio, dopo aver eseguito numerosi flussi di lavoro non transitori (che crea nodi di istanza del flusso di lavoro), puoi eseguire [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) su base ad hoc. Rimuove immediatamente le istanze del flusso di lavoro ridondanti e completate, anziché attendere l&#39;esecuzione del programma di svuotamento del flusso di lavoro Granite del Adobe .

### Numero massimo di processi paralleli {#maximum-parallel-jobs}

Per impostazione predefinita, [!DNL Experience Manager] esegue un numero massimo di processi paralleli pari al numero di processori presenti sul server. Il problema di questa impostazione è che durante i periodi di carico eccessivo, tutti i processori sono occupati da flussi di lavoro [!UICONTROL DAM Update Asset], rallentando la reattività dell&#39;interfaccia utente e impedendo a [!DNL Experience Manager] di eseguire altri processi che salvaguardano le prestazioni e la stabilità del server. Come procedura corretta, impostare questo valore su metà dei processori disponibili sul server eseguendo la procedura seguente:

1. In [!DNL Experience Manager] Autore, accedere a `https://[aem_server]:[port]/system/console/slingevent`.

1. Fare clic su **[!UICONTROL Modifica]** in ogni coda di workflow rilevante per l&#39;implementazione, ad esempio **[!UICONTROL Granite Transient Workflow Queue]**.

1. Aggiornate il valore di **[!UICONTROL Processi paralleli massimi]** e fate clic su **[!UICONTROL Salva]**.

L&#39;impostazione di una coda a metà dei processori disponibili è una soluzione praticabile con cui iniziare. Tuttavia, potrebbe essere necessario aumentare o diminuire questo numero per ottenere il massimo throughput e ottimizzarlo in base all&#39;ambiente. Sono presenti code separate per flussi di lavoro transitori e non transitori, nonché per altri processi, come i flussi di lavoro esterni. Se diverse code impostate al 50% dei processori sono attivi contemporaneamente, il sistema può sovraccaricare rapidamente. Le code che vengono utilizzate in modo molto diffuso variano notevolmente tra le implementazioni degli utenti. Di conseguenza, potrebbe essere necessario configurarli con attenzione per la massima efficienza senza compromettere la stabilità del server.

### Configurazione risorsa aggiornamento DAM {#dam-update-asset-configuration}

Il flusso di lavoro [!UICONTROL DAM Update Asset] contiene una suite completa di passaggi configurati per attività, ad esempio per la generazione Dynamic Media PTIFF e l&#39;integrazione con [!DNL Adobe InDesign Server]. Tuttavia, la maggior parte degli utenti potrebbe non richiedere diversi di questi passaggi.  Adobe consiglia di creare una copia personalizzata del modello di flusso di lavoro [!UICONTROL DAM Update Asset] e di rimuovere eventuali passaggi superflui. In questo caso, aggiornate i programmi di avvio per [!UICONTROL DAM Update Asset] in modo che puntino al nuovo modello.

L&#39;esecuzione intensiva del flusso di lavoro [!UICONTROL DAM Update Asset] può aumentare notevolmente la dimensione del datatastore del file. I risultati di un esperimento eseguito da  Adobe hanno dimostrato che la dimensione del datastore può aumentare di circa 400 GB se vengono eseguiti circa 5500 flussi di lavoro entro 8 ore.

Si tratta di un aumento temporaneo e il datastore viene ripristinato alle dimensioni originali dopo l&#39;esecuzione dell&#39;attività di raccolta dei rifiuti del datastore.

In genere, l&#39;attività di raccolta rifiuti del datastore viene eseguita settimanalmente insieme ad altre attività di manutenzione pianificate.

Se disponete di uno spazio su disco limitato ed eseguite intensamente i flussi di lavoro [!UICONTROL DAM Update Asset], prendete in considerazione la pianificazione dell&#39;attività di raccolta dei rifiuti con maggiore frequenza.

#### Generazione di rappresentazioni runtime {#runtime-rendition-generation}

I clienti utilizzano immagini di varie dimensioni e formati all&#39;interno del sito Web o per la distribuzione ai partner commerciali. Poiché ogni rappresentazione aggiunge un’impronta alla risorsa nella directory archivio,  Adobe consiglia di usare questa funzione con cautela. Per ridurre la quantità di risorse necessarie per elaborare e archiviare le immagini, potete generare queste immagini in fase di esecuzione anziché come rappresentazioni durante l’assimilazione.

Molti clienti di Sites implementano un servlet di immagini che ridimensiona e ritaglia le immagini al momento della richiesta, il che impone un carico aggiuntivo sull’istanza di pubblicazione. Tuttavia, finché queste immagini possono essere memorizzate nella cache, la sfida può essere attenuata.

Un approccio alternativo consiste nell’utilizzare la tecnologia Dynamic Media per distribuire completamente la manipolazione delle immagini. Inoltre, potete implementare Brand Portal che non solo prende in consegna le responsabilità di generazione delle rappresentazioni dall&#39;infrastruttura [!DNL Experience Manager], ma anche l&#39;intero livello di pubblicazione.

#### ImageMagick {#imagemagick}

Se personalizzate il flusso di lavoro [!UICONTROL DAM Update Asset] per generare rappresentazioni utilizzando ImageMagick,  Adobe consiglia di modificare il file `policy.xml` in `/etc/ImageMagick/`. Per impostazione predefinita, ImageMagick utilizza l’intero spazio disponibile sul volume del sistema operativo e la memoria disponibile. Apportate le seguenti modifiche alla configurazione all&#39;interno della sezione `policymap` di `policy.xml` per limitare tali risorse.

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

Inoltre, impostare il percorso della cartella temporanea di ImageMagick nel file `configure.xml` (o impostando la variabile di ambiente `MAGIC_TEMPORARY_PATH`) su una partizione del disco con spazio sufficiente e IOPS.

>[!CAUTION]
>
>Una configurazione errata può rendere instabile il server se ImageMagick utilizza tutto lo spazio disponibile su disco. Le modifiche dei criteri necessarie per elaborare file di grandi dimensioni con ImageMagick possono influire sulle prestazioni di [!DNL Experience Manager]. Per ulteriori informazioni, vedere [installare e configurare ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>I file ImageMagick `policy.xml` e `configure.xml` sono disponibili in `/usr/lib64/ImageMagick-&#42;/config/` invece di `/etc/ImageMagick/`.Per informazioni sulla posizione dei file di configurazione, vedere [Documentazione ImageMagick](https://www.imagemagick.org/script/resources.php).

Se utilizzi [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l&#39;Assistenza clienti  Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Consultate  rappresentante dell&#39;Assistenza clienti di Adobe per implementare queste best practice per l&#39;implementazione di AMS e scegliere i migliori strumenti e modelli possibili per  formati proprietari  Adobe. [!DNL Experience Manager] potrebbero non essere in grado di elaborare file PSB ad alta risoluzione con oltre 30000 x 23000 pixel.

### XMP di riscrittura {#xmp-writeback}

XMP writeback aggiorna la risorsa originale ogni volta che i metadati vengono modificati in [!DNL Experience Manager], con le seguenti conseguenze:

* La risorsa stessa viene modificata
* Viene creata una versione della risorsa
* [!UICONTROL Risorse di aggiornamento DAM ] eseguite sulla risorsa

I risultati elencati richiedono notevoli risorse. Pertanto,  Adobe consiglia di [disattivare XMP WriteBack](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html), se non è richiesto.

Se è selezionato il flag di esecuzione dei flussi di lavoro, l&#39;importazione di una grande quantità di metadati può comportare un&#39;attività di XMP di riscrittura delle risorse. Pianificate tale importazione durante l&#39;utilizzo di un server snello in modo che le prestazioni per altri utenti non vengano compromesse.

## Replica {#replication}

Quando si replicano le risorse in un numero elevato di istanze pubblicate, ad esempio in un&#39;implementazione di Sites,  Adobe consiglia di utilizzare la replica a catena. In questo caso, l’istanza di creazione si replica in una singola istanza di pubblicazione che a sua volta viene replicata nelle altre istanze di pubblicazione, liberando l’istanza di creazione.

### Configurare la replica della catena {#configure-chain-replication}

1. Scegliere l&#39;istanza di pubblicazione da utilizzare per concatenare le repliche
1. In tale istanza di pubblicazione aggiungere agenti di replica che puntano alle altre istanze di pubblicazione
1. Per ciascuno di questi agenti di replica, abilitare &quot;Su ricezione&quot; nella scheda &quot;Triggers&quot;

>[!NOTE]
>
> Adobe non consiglia di attivare automaticamente le risorse. Tuttavia, se necessario,  Adobe consiglia di eseguire questa operazione come passo finale in un flusso di lavoro, in genere DAM Update Asset (Aggiorna risorsa).

## Indice di ricerca {#search-indexes}

Assicuratevi di implementare i Service Pack più recenti e gli hotfix correlati alle prestazioni, in quanto spesso includono aggiornamenti agli indici di sistema. Per alcune ottimizzazioni di indice, vedere [Suggerimenti per l&#39;ottimizzazione delle prestazioni](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).

Creare indici personalizzati per le query eseguite spesso. Per informazioni dettagliate, vedere [metodologia per l&#39;analisi delle query lente](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [creazione di indici personalizzati](/help/sites-deploying/queries-and-indexing.md). Per ulteriori informazioni sulle best practice relative alle query e agli indici, vedere [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md) (Tecniche consigliate per query e indicizzazione).

### Configurazioni indice Lucene {#lucene-index-configurations}

Alcune ottimizzazioni possono essere eseguite sulle configurazioni dell&#39;indice Oak che possono contribuire a migliorare le prestazioni di [!DNL Experience Manager Assets]. Aggiornare le configurazioni dell&#39;indice per migliorare il tempo di reindicizzazione:

1. Aprite CRXDe `/crx/de/index.jsp` ed effettuate l&#39;accesso come utente amministrativo.
1. Passare a `/oak:index/lucene`.
1. Aggiungere una proprietà `String[]` `excludedPaths` con valori `/var`, `/etc/workflow/instances` e `/etc/replication`.
1. Passare a `/oak:index/damAssetLucene`. Aggiungete una proprietà `String[]` `includedPaths` con il valore `/content/dam`. Salvare le modifiche.

Se gli utenti non devono effettuare la ricerca full-text delle risorse, ad esempio, eseguendo ricerche nel testo di documenti PDF, disattivate questa opzione. È possibile migliorare le prestazioni dell&#39;indice disattivando l&#39;indicizzazione full-text. Per disabilitare l&#39;estrazione del testo [!DNL Apache Lucene], procedere come segue:

1. Nell&#39;interfaccia [!DNL Experience Manager], accedere a [!UICONTROL Gestione pacchetti].
1. Caricate e installate il pacchetto disponibile in [disable_indexingbinarytextestrazione-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Indovina totale {#guess-total}

Quando create query che generano set di risultati di grandi dimensioni, utilizzate il parametro `guessTotal` per evitare un utilizzo eccessivo della memoria durante l&#39;esecuzione.

## Problemi noti {#known-issues}

### File di grandi dimensioni {#large-files}

Esistono due problemi noti principali relativi ai file di grandi dimensioni in [!DNL Experience Manager]. Quando i file raggiungono dimensioni superiori a 2 GB, la sincronizzazione in standby a freddo può trovarsi in una situazione di memoria insufficiente. In alcuni casi, impedisce l&#39;esecuzione della sincronizzazione in standby. In altri casi, causa l&#39;arresto anomalo dell&#39;istanza principale. Questo scenario si applica a qualsiasi file in [!DNL Experience Manager] maggiore di 2 GB, inclusi i pacchetti di contenuto.

Allo stesso modo, quando i file raggiungono le dimensioni di 2 GB durante l&#39;utilizzo di un archivio dati S3 condiviso, potrebbe essere necessario del tempo per mantenere il file completamente persistente dalla cache al file system. Di conseguenza, quando si utilizza la replica senza binario, è possibile che i dati binari non siano stati persistenti prima del completamento della replica. Questa situazione può causare problemi, soprattutto se la disponibilità dei dati è importante.

## Test delle prestazioni {#performance-testing}

Per ogni [!DNL Experience Manager] implementazione, è necessario stabilire un sistema di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. Ecco alcune aree chiave su cui concentrarsi.

### Test di rete {#network-testing}

Per tutti i problemi di prestazioni della rete da parte del cliente, eseguire le seguenti operazioni:

* Verificare le prestazioni della rete dall&#39;interno della rete del cliente
* Verificare le prestazioni di rete dall&#39;interno  rete del Adobe. Per i clienti AMS, utilizza il tuo CSE per eseguire il test dall&#39;interno della rete del Adobe .
* Verificare le prestazioni di rete da un altro punto di accesso
* Utilizzando uno strumento di benchmark di rete
* Prova contro lo speditore

### [!DNL Experience Manager] test di distribuzione  {#aem-deployment-testing}

Per ridurre al minimo la latenza e ottenere un throughput elevato grazie all&#39;utilizzo efficiente della CPU e alla condivisione del carico, controlla regolarmente le prestazioni della distribuzione [!DNL Experience Manager]. In particolare:

* Eseguire test di carico sulla distribuzione [!DNL Experience Manager].
* Monitorare le prestazioni di caricamento e la capacità di risposta dell’interfaccia utente.

## [!DNL Experience Manager Assets] elenco di controllo delle prestazioni e impatto delle attività di gestione delle risorse  {#checklist}

* Abilitate HTTPS per aggirare eventuali misuratori di traffico HTTP aziendali.
* Usate una connessione cablata per il caricamento di risorse pesanti.
* Implementare in Java 8.
* Impostare parametri JVM ottimali.
* Configurare un archivio dati del file system o un archivio dati S3.
* Disattiva la generazione delle risorse secondarie. Se è attivato, AEM flusso di lavoro viene creata una risorsa separata per ogni pagina di una risorsa con più pagine. Ciascuna di queste pagine è una singola risorsa che consuma ulteriore spazio su disco, richiede il controllo delle versioni e un&#39;ulteriore elaborazione del flusso di lavoro. Se non sono necessarie pagine separate, disattivate la generazione di risorse secondarie e le attività di estrazione della pagina.
* Abilita flussi di lavoro transitori.
* Regola le code del flusso di lavoro Granite per limitare i processi simultanei.
* Configurare [!DNL ImageMagick] per limitare il consumo di risorse.
* Rimuovete i passaggi non necessari dal flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].
* Configurare l&#39;eliminazione del flusso di lavoro e delle versioni.
* Ottimizzate gli indici con i service pack e gli hotfix più recenti. Consulta &#39;Assistenza clienti di Adobe per eventuali ottimizzazioni di indice aggiuntive disponibili.
* Utilizzare EstimateTotal per ottimizzare le prestazioni della query.
* Se si configura [!DNL Experience Manager] per rilevare i tipi di file dal contenuto dei file (abilitando **[!UICONTROL Day CQ DAM Mime Type Service]** in **[!UICONTROL AEM Web Console]**), è possibile caricare molti file in massa durante le ore non di picco, poiché richiede molte risorse.
