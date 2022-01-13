---
title: Ottimizzazione delle prestazioni [!DNL Assets].
description: Suggerimenti e indicazioni [!DNL Experience Manager] configurazione, modifiche a hardware, software e componenti di rete per rimuovere i colli di bottiglia e ottimizzare le prestazioni [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '2741'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guida all’ottimizzazione delle prestazioni {#assets-performance-tuning-guide}

Un [!DNL Experience Manager Assets] La configurazione contiene diversi componenti hardware, software e di rete. A seconda dello scenario di distribuzione, potrebbe essere necessario apportare modifiche specifiche alla configurazione di hardware, software e componenti di rete per rimuovere i colli di bottiglia delle prestazioni.

Inoltre, l&#39;identificazione e l&#39;aderenza a determinate linee guida per l&#39;ottimizzazione di hardware e software aiuta a creare una base audio che consenta al tuo [!DNL Experience Manager Assets] implementazione per soddisfare le aspettative su prestazioni, scalabilità e affidabilità.

Scarse prestazioni in [!DNL Experience Manager Assets] può influenzare l’esperienza degli utenti in relazione a prestazioni interattive, elaborazione delle risorse, velocità di download e altre aree.

L’ottimizzazione delle prestazioni è infatti un’attività fondamentale da eseguire prima di stabilire le metriche di destinazione per qualsiasi progetto.

Di seguito sono elencate alcune aree principali intorno alle quali puoi individuare e risolvere i problemi di prestazioni prima che abbiano un impatto sugli utenti.

## Platform {#platform}

Anche se Experience Manager è supportato su diverse piattaforme, Adobe ha trovato il supporto più grande per gli strumenti nativi su Linux e Windows, che contribuisce a prestazioni ottimali e alla facilità di implementazione. Idealmente, è necessario implementare un sistema operativo a 64 bit per soddisfare i requisiti di memoria elevati di un [!DNL Experience Manager Assets] distribuzione. Come per qualsiasi implementazione di Experience Manager, è necessario implementare TarMK laddove possibile. Mentre TarMK non può scalare oltre una singola istanza di authoring, si scopre che funziona meglio di MongoMK. Puoi aggiungere istanze di offload TarMK per aumentare la potenza di elaborazione del flusso di lavoro del tuo [!DNL Experience Manager Assets] distribuzione.

### Cartella temporanea {#temp-folder}

Per migliorare i tempi di caricamento delle risorse, utilizza l’archiviazione ad alte prestazioni per la directory temporanea Java. Su Linux e Windows, è possibile utilizzare un&#39;unità RAM o SSD. In ambienti basati su cloud, è possibile utilizzare un tipo di storage ad alta velocità equivalente. Ad esempio in Amazon EC2, un [azionamento effimero](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) unità può essere utilizzata per la cartella temporanea.

Supponendo che il server disponga di una memoria ampia, configura un&#39;unità RAM. Su Linux, esegui questi comandi per creare un&#39;unità RAM da 8 GB:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

In Windows OS, utilizzare un driver di terze parti per creare un&#39;unità RAM o semplicemente utilizzare un&#39;unità di storage ad alte prestazioni come SSD.

Una volta pronto il volume temporaneo ad alte prestazioni, imposta il parametro JVM `-Djava.io.tmpdir`. Ad esempio, puoi aggiungere il parametro JVM qui sotto al `CQ_JVM_OPTS` nella variabile `bin/start` copione [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configurazione Java {#java-configuration}

### Versione Java {#java-version}

Adobe consiglia di implementare [!DNL Experience Manager Assets] su Java 8 per prestazioni ottimali.

<!-- TBD: Link to the latest official word around Java.
-->

### Parametri JVM {#jvm-parameters}

Imposta i seguenti parametri JVM:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=vero

## Configurazione dell&#39;archivio dati e della memoria {#data-store-and-memory-configuration}

### Configurazione archivio dati file {#file-data-store-configuration}

È consigliabile separare l’archivio dati dall’archivio segmenti per tutti [!DNL Experience Manager Assets] utenti. Inoltre, configura la `maxCachedBinarySize` e `cacheSizeInMB` i parametri possono contribuire a massimizzare le prestazioni. Imposta `maxCachedBinarySize` alla dimensione più piccola del file che può essere mantenuta nella cache. Specifica la dimensione della cache in memoria da utilizzare per l’archivio dati in `cacheSizeInMB`. Adobe consiglia di impostare questo valore tra il 2 e il 10% della dimensione totale dell&#39;heap. Tuttavia, il test di carico/prestazioni può aiutare a determinare l&#39;impostazione ideale.

### Configura la dimensione massima della cache delle immagini bufferizzate {#configure-the-maximum-size-of-the-buffered-image-cache}

Quando si caricano grandi quantità di risorse in [!DNL Adobe Experience Manager], per consentire picchi imprevisti nel consumo di memoria e per evitare errori JVM con OutOfMemoryErrors, riduci la dimensione massima configurata della cache delle immagini bufferizzate. Considera un esempio di sistema con un heap massimo (- `Xmx`param) di 5 GB, un Oak BlobCache impostato a 1 GB, e la cache del documento impostata a 2 GB. In questo caso, la cache bufferizzata richiederebbe un massimo di 1,25 GB e memoria, lasciando solo 0,75 GB di memoria per picchi imprevisti.

Configura la dimensione della cache bufferizzata nella console Web OSGi. A `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, imposta la proprietà `cq.dam.image.cache.max.memory` in byte. Ad esempio, 1073741824 è 1 GB (1024 x 1024 x 1024 = 1 GB).

Da Experience Manager 6.1 SP1, se utilizzi un `sling:osgiConfig` nodo per la configurazione di questa proprietà, assicurarsi di impostare il tipo di dati su Long. Per ulteriori dettagli, consulta [CQBufferedImageCache consuma heap durante il caricamento delle risorse](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Archiviazione dati condivisa {#shared-data-stores}

L&#39;implementazione di un S3 o Shared File Datastore può aiutare a risparmiare spazio su disco e ad aumentare il throughput di rete nelle implementazioni su larga scala. Per ulteriori informazioni sui pro e i contro dell’utilizzo di un datastore condiviso, consulta [Guida al dimensionamento delle risorse](/help/assets/assets-sizing-guide.md).

### Archiviazione dati S3 {#s-data-store}

La seguente configurazione dell’archivio dati S3 ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) ha aiutato Adobe ad estrarre 12,8 TB di oggetti BLOB (binari di grandi dimensioni) da un archivio dati di file esistente in un archivio dati S3 in un sito cliente:

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

L’Adobe consiglia di abilitare HTTPS perché molte aziende dispongono di firewall per l’attivazione del traffico HTTP, il che influisce negativamente sui caricamenti e corrompe i file. Per caricamenti di file di grandi dimensioni, assicurati che gli utenti abbiano connessioni cablate alla rete perché una rete WiFi diventa rapidamente saturata. Per le linee guida sull&#39;identificazione delle strozzature di rete, vedi [Guida al dimensionamento delle risorse](/help/assets/assets-sizing-guide.md). Per valutare le prestazioni della rete analizzando la topologia di rete, vedi [Considerazioni sulla rete Assets](/help/assets/assets-network-considerations.md).

In primo luogo, la strategia di ottimizzazione della rete dipende dalla quantità di larghezza di banda disponibile e dal carico sul [!DNL Experience Manager] istanza. Opzioni di configurazione comuni, inclusi firewall o proxy, possono contribuire a migliorare le prestazioni di rete. Ecco alcuni punti chiave da tenere a mente:

* A seconda del tipo di istanza (piccolo, moderato, grande), assicurati di disporre di una larghezza di banda di rete sufficiente per l’istanza di Experience Manager. Un&#39;adeguata allocazione della larghezza di banda è particolarmente importante se [!DNL Experience Manager] è ospitato su AWS.
* Se [!DNL Experience Manager] L&#39;istanza è ospitata su AWS, è possibile beneficiare di una policy di scalabilità versatile. Aggiorna l&#39;istanza se gli utenti prevedono un carico elevato. Ridimensionarla per un carico moderato/basso.
* HTTPS: La maggior parte degli utenti dispone di firewall che annusano il traffico HTTP, che può avere un impatto negativo sul caricamento di file o persino di file corrotti durante l’operazione di caricamento.
* Caricamenti di file di grandi dimensioni: Assicurati che gli utenti abbiano connessioni cablate alla rete (le connessioni WiFi saturano rapidamente).

## Flussi di lavoro {#workflows}

### Flussi di lavoro transitori {#transient-workflows}

Se possibile, imposta la [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro a transitorio. L’impostazione riduce notevolmente i costi generali necessari per elaborare i flussi di lavoro perché, in questo caso, i flussi di lavoro non devono passare attraverso i normali processi di tracciamento e archiviazione.

1. Passa a `/miscadmin` in [!DNL Experience Manager] implementazione in `https://[aem_server]:[port]/miscadmin`.

1. Espandi **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL diga]**.

1. Apri **[!UICONTROL Risorsa di aggiornamento DAM]**. Dal pannello degli strumenti mobili, passa alla **[!UICONTROL Pagina]** , quindi fai clic su **[!UICONTROL Proprietà pagina]**.

1. Seleziona **[!UICONTROL Flusso di lavoro transitorio]** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Alcune funzionalità non supportano flussi di lavoro transitori. Se [!DNL Assets] la distribuzione richiede queste funzionalità, non configurare flussi di lavoro transitori.

Nei casi in cui non è possibile utilizzare flussi di lavoro transitori, esegui regolarmente l’eliminazione del flusso di lavoro per eliminare quelli archiviati [!UICONTROL Risorsa di aggiornamento DAM] flussi di lavoro per garantire che le prestazioni del sistema non peggiorino.

In genere, eseguire i flussi di lavoro di eliminazione settimanalmente. Tuttavia, in scenari ad uso intensivo di risorse, ad esempio durante l’assimilazione di risorse su larga scala, puoi eseguirli più frequentemente.

Per configurare l’eliminazione del flusso di lavoro, aggiungi una nuova configurazione Adobe Granite Workflow Purge tramite la console OSGi. Quindi, configura e pianifica il flusso di lavoro come parte della finestra di manutenzione settimanale.

Se la pulizia viene eseguita per troppo tempo, si verifica un timeout. Pertanto, assicurati che i processi di eliminazione siano completi per evitare situazioni in cui l’eliminazione dei flussi di lavoro non riesce a essere completata a causa dell’elevato numero di flussi di lavoro.

Ad esempio, dopo aver eseguito numerosi flussi di lavoro non transitori (che creano nodi di istanza del flusso di lavoro), puoi eseguire [Ripristino dei flussi di lavoro ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) su base ad hoc. Rimuove immediatamente le istanze del flusso di lavoro ridondanti e completate anziché attendere l’esecuzione della pianificazione di eliminazione del flusso di lavoro di Adobe Granite.

### Processi paralleli massimi {#maximum-parallel-jobs}

Per impostazione predefinita, [!DNL Experience Manager] esegue un numero massimo di processi paralleli uguale al numero di processori sul server. Il problema di questa impostazione è che durante i periodi di carico pesante, tutti i processori sono occupati da [!UICONTROL Risorsa di aggiornamento DAM] flussi di lavoro, rallentamento della reattività dell’interfaccia utente e prevenzione [!DNL Experience Manager] dall&#39;esecuzione di altri processi che salvaguardano le prestazioni e la stabilità del server. Come buona pratica, imposta questo valore a metà dei processori disponibili sul server eseguendo i seguenti passaggi:

1. On [!DNL Experience Manager] Autore, accesso `https://[aem_server]:[port]/system/console/slingevent`.

1. Fai clic su **[!UICONTROL Modifica]** in ogni coda di flusso di lavoro pertinente all’implementazione, ad esempio **[!UICONTROL Coda flusso di lavoro transitorio di Granite]**.

1. Aggiorna il valore di **[!UICONTROL Processi paralleli massimi]** e fai clic su **[!UICONTROL Salva]**.

Impostare una coda a metà dei processori disponibili è una soluzione praticabile con cui iniziare. Tuttavia, potrebbe essere necessario aumentare o diminuire questo numero per ottenere il massimo throughput e regolarlo in base all&#39;ambiente. Sono presenti code separate per i flussi di lavoro transitori e non transitori e per altri processi, ad esempio quelli esterni. Se diverse code impostate al 50% dei processori sono attive contemporaneamente, il sistema può essere sovraccaricato rapidamente. Le code utilizzate in modo massiccio variano notevolmente a seconda delle implementazioni degli utenti. Pertanto, potrebbe essere necessario configurarli con attenzione per la massima efficienza senza sacrificare la stabilità del server.

### Configurazione risorsa di aggiornamento DAM {#dam-update-asset-configuration}

La [!UICONTROL Risorsa di aggiornamento DAM] il flusso di lavoro contiene una suite completa di passaggi configurati per attività quali la generazione di PTIFF Dynamic Media e [!DNL Adobe InDesign Server] integrazione. Tuttavia, la maggior parte degli utenti potrebbe non richiedere diversi di questi passaggi. Adobe consiglia di creare una copia personalizzata del [!UICONTROL Risorsa di aggiornamento DAM] modello di flusso di lavoro e rimuovi eventuali passaggi superflui. In questo caso, aggiorna i moduli di avvio per [!UICONTROL Risorsa di aggiornamento DAM] per puntare al nuovo modello.

Esecuzione del [!UICONTROL Risorsa di aggiornamento DAM] un flusso di lavoro intensivo può aumentare notevolmente le dimensioni del datatastore dei file. I risultati di un esperimento eseguito da Adobe hanno dimostrato che la dimensione del datastore può aumentare di circa 400 GB se vengono eseguiti circa 5500 flussi di lavoro in 8 ore.

Si tratta di un aumento temporaneo e il datastore viene ripristinato alle dimensioni originali dopo aver eseguito l&#39;attività di raccolta rifiuti del datastore.

In genere, l&#39;attività di raccolta oggetti inattivi del datastore viene eseguita settimanalmente insieme ad altre attività di manutenzione pianificate.

Se lo spazio su disco è limitato ed è in esecuzione [!UICONTROL Risorsa di aggiornamento DAM] flussi di lavoro intensivi, considera la pianificazione dell’attività di raccolta degli oggetti inattivi più frequentemente.

#### Generazione rendering runtime {#runtime-rendition-generation}

I clienti utilizzano immagini di varie dimensioni e formati sul proprio sito web o per la distribuzione ai partner commerciali. Poiché ogni rendering viene aggiunto all’impronta della risorsa nell’archivio, Adobe consiglia di utilizzare questa funzione in modo giudizioso. Per ridurre la quantità di risorse necessarie per elaborare e archiviare le immagini, puoi generarle in fase di esecuzione anziché come rappresentazioni durante l’acquisizione.

Molti clienti di Sites implementano un servlet immagine che ridimensiona e ritaglia le immagini al momento della richiesta, il che impone un carico aggiuntivo sull’istanza di pubblicazione. Tuttavia, finché queste immagini possono essere memorizzate nella cache, la sfida può essere attenuata.

Un approccio alternativo è quello di utilizzare la tecnologia Dynamic Media per distribuire completamente la manipolazione delle immagini. Inoltre, puoi distribuire Brand Portal che non solo assume le responsabilità di generazione del rendering dal [!DNL Experience Manager] infrastruttura, ma anche l&#39;intero livello di pubblicazione.

#### ImageMagick {#imagemagick}

Se si personalizza la [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro per generare rappresentazioni utilizzando ImageMagick, Adobe consiglia di modificare il `policy.xml` file a `/etc/ImageMagick/`. Per impostazione predefinita, ImageMagick utilizza l&#39;intero spazio su disco disponibile sul volume del sistema operativo e la memoria disponibile. Apporta le seguenti modifiche alla configurazione all’interno della `policymap` sezione `policy.xml` per limitare tali risorse.

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

Inoltre, imposta il percorso della cartella temporanea di ImageMagick nel `configure.xml` o impostando la variabile di ambiente `MAGIC_TEMPORARY_PATH`) in una partizione disco con spazio sufficiente e IOPS.

>[!CAUTION]
>
>Una configurazione errata può rendere instabile il server se ImageMagick utilizza tutto lo spazio su disco disponibile. Le modifiche dei criteri necessarie per elaborare file di grandi dimensioni utilizzando ImageMagick possono influire sul [!DNL Experience Manager] prestazioni. Per ulteriori informazioni, consulta [installa e configura ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` e `configure.xml` i file sono disponibili in `/usr/lib64/ImageMagick-&#42;/config/` anziché `/etc/ImageMagick/`.See [Documentazione di ImageMagick](https://www.imagemagick.org/script/resources.php) per la posizione dei file di configurazione.

Se utilizzi [!DNL Experience Manager] in Adobe Managed Services (AMS), contatta l’Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Collabora con il rappresentante di Assistenza clienti Adobe per implementare queste best practice per la distribuzione AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbero non essere in grado di elaborare file PSB ad alta risoluzione con più di 3000 x 23000 pixel.

### XMP {#xmp-writeback}

XMP writeback aggiorna la risorsa originale ogni volta che i metadati vengono modificati in [!DNL Experience Manager], che si traduce in quanto segue:

* La risorsa stessa viene modificata
* Viene creata una versione della risorsa
* [!UICONTROL Risorsa di aggiornamento DAM] viene eseguito sulla risorsa

I risultati elencati consumano notevoli risorse. Pertanto, l&#39;Adobe raccomanda [disabilitazione XMP Writeback](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html), se non è obbligatorio.

Se è selezionato il flag di esecuzione dei flussi di lavoro, l’importazione di una grande quantità di metadati può comportare un’attività di XMP write-back ad uso intensivo di risorse. Pianifica un&#39;importazione di questo tipo durante l&#39;utilizzo snello del server in modo che le prestazioni per altri utenti non siano influenzate.

## Replica {#replication}

Quando si replicano le risorse in un numero elevato di istanze di pubblicazione, ad esempio in un’implementazione di Sites, Adobe consiglia di utilizzare la replica a catena. In questo caso, l&#39;istanza dell&#39;autore si replica in una singola istanza di pubblicazione che a sua volta si replica alle altre istanze di pubblicazione, liberando l&#39;istanza dell&#39;autore.

### Configurare la replica a catena {#configure-chain-replication}

1. Scegliere l&#39;istanza di pubblicazione da utilizzare per concatenare le replicazioni
1. In quell&#39;istanza di pubblicazione aggiungi agenti di replica che puntano alle altre istanze di pubblicazione
1. Su ciascuno di questi agenti di replica, abilita &quot;Al ricevimento&quot; sulla scheda &quot;Triggers&quot;

>[!NOTE]
>
>Ad Adobe, non è consigliabile attivare automaticamente le risorse. Tuttavia, se necessario, Adobe consiglia di eseguire questo come passaggio finale in un flusso di lavoro, in genere DAM Update Asset.

## Cerca indici {#search-indexes}

Installa [i Service Pack più recenti](/help/release-notes/release-notes.md) e hotfix relativi alle prestazioni, in quanto spesso includono aggiornamenti agli indici di sistema. Vedi [suggerimenti per l&#39;ottimizzazione delle prestazioni](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) per alcune ottimizzazioni dell&#39;indice.

Crea indici personalizzati per le query che esegui spesso. Per maggiori dettagli, vedi [metodologia per l’analisi delle query lente](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) e [creazione di indici personalizzati](/help/sites-deploying/queries-and-indexing.md). Per ulteriori informazioni sulle best practice relative a query e indice, consulta [Tecniche consigliate per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurazioni dell&#39;indice Lucene {#lucene-index-configurations}

Alcune ottimizzazioni possono essere fatte sulle configurazioni dell&#39;indice Oak che possono aiutare a migliorare [!DNL Experience Manager Assets] prestazioni. Aggiorna le configurazioni dell&#39;indice per migliorare il tempo di reindicizzazione:

1. Apri CRXDe `/crx/de/index.jsp` e accedi come utente amministrativo.
1. Sfoglia per `/oak:index/lucene`.
1. Aggiungi un `String[]` property `excludedPaths` con valori `/var`, `/etc/workflow/instances`e `/etc/replication`.
1. Sfoglia per `/oak:index/damAssetLucene`. Aggiungi un `String[]` property `includedPaths` con valore `/content/dam`. Salva le modifiche.

Se gli utenti non devono eseguire la ricerca full-text delle risorse, ad esempio, eseguendo una ricerca nel testo dei documenti di PDF, disabilitala. Migliori le prestazioni dell&#39;indice disattivando l&#39;indicizzazione full-text. Per disabilitare [!DNL Apache Lucene] estrazione del testo, effettua le seguenti operazioni:

1. In [!DNL Experience Manager] interfaccia, accesso [!UICONTROL Gestione pacchetti].
1. Carica e installa il pacchetto disponibile in [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Totale Indovini {#guess-total}

Quando crei query che generano set di risultati di grandi dimensioni, utilizza la variabile `guessTotal` per evitare l&#39;utilizzo di memoria pesante quando vengono eseguiti.

## Problemi noti {#known-issues}

### File di grandi dimensioni {#large-files}

Ci sono due importanti problemi noti relativi ai file di grandi dimensioni in [!DNL Experience Manager]. Quando i file raggiungono dimensioni superiori a 2 GB, la sincronizzazione standby a freddo può trovarsi in una situazione di esaurimento della memoria. In alcuni casi, impedisce l’esecuzione della sincronizzazione in standby. In altri casi, causa l’arresto anomalo dell’istanza primaria. Questo scenario si applica a qualsiasi file in [!DNL Experience Manager] superiore a 2 GB, inclusi i pacchetti di contenuti.

Allo stesso modo, quando i file raggiungono le dimensioni di 2 GB durante l&#39;utilizzo di un archivio dati S3 condiviso, potrebbe essere necessario un po&#39; di tempo perché il file venga mantenuto completamente dalla cache al file system. Di conseguenza, quando si utilizza la replica senza binario, è possibile che i dati binari non siano stati persistenti prima del completamento della replica. Questa situazione può causare problemi, soprattutto se la disponibilità dei dati è importante.

## Test delle prestazioni {#performance-testing}

Per ogni [!DNL Experience Manager] implementazione, stabilire un regime di test delle prestazioni in grado di identificare e risolvere rapidamente i colli di bottiglia. Ecco alcune aree chiave su cui concentrarsi.

### Test di rete {#network-testing}

Per tutti i problemi di prestazioni della rete da parte del cliente, eseguire le seguenti operazioni:

* Verificare le prestazioni di rete dalla rete del cliente
* Verificare le prestazioni di rete dalla rete Adobe. Per i clienti AMS, collabora con il tuo CSE per eseguire il test dall’interno della rete Adobe.
* Verificare le prestazioni di rete da un altro punto di accesso
* Utilizzando uno strumento di benchmark della rete
* Test contro il dispatcher

### [!DNL Experience Manager] test di distribuzione {#aem-deployment-testing}

Per ridurre al minimo la latenza e ottenere un throughput elevato grazie all&#39;utilizzo efficiente della CPU e alla condivisione del carico, controlla le prestazioni del tuo [!DNL Experience Manager] distribuzione regolare. In particolare:

* Eseguire test di carico contro [!DNL Experience Manager] distribuzione.
* Monitora le prestazioni di caricamento e la reattività dell&#39;interfaccia utente.

## [!DNL Experience Manager Assets] elenco di controllo delle prestazioni e impatto delle attività di gestione delle risorse {#checklist}

* Abilita HTTPS per aggirare qualsiasi sniffer di traffico HTTP aziendale.
* Utilizza una connessione cablata per il caricamento di risorse pesanti.
* Distribuisci su Java 8.
* Imposta parametri JVM ottimali.
* Configura un archivio dati del sistema di file o un archivio dati S3.
* Disattiva la generazione di risorse secondarie. Se è abilitata, AEM flusso di lavoro crea una risorsa separata per ogni pagina di una risorsa multipagina. Ciascuna di queste pagine è una singola risorsa che consuma ulteriore spazio su disco, richiede il controllo delle versioni e ulteriore elaborazione del flusso di lavoro. Se non richiedi pagine separate, disattiva la generazione di risorse secondarie e le attività di estrazione della pagina.
* Abilita flussi di lavoro transitori.
* Ottimizza le code del flusso di lavoro Granite per limitare i processi simultanei.
* Configura [!DNL ImageMagick] per limitare il consumo di risorse.
* Rimuovi i passaggi non necessari dal [!UICONTROL Risorsa di aggiornamento DAM] workflow.
* Configura la pulizia del flusso di lavoro e delle versioni.
* Ottimizza gli indici con i Service Pack e gli hotfix più recenti. Consulta Adobe Customer Support per eventuali ottimizzazioni aggiuntive dell&#39;indice disponibili.
* Utilizza guessTotal per ottimizzare le prestazioni della query.
* Se si configura [!DNL Experience Manager] per rilevare i tipi di file dal contenuto dei file (abilitando **[!UICONTROL Servizio Day CQ DAM Mime Type]** in **[!UICONTROL Console Web AEM]**), carica molti file in blocco nelle ore non di picco, in quanto richiede molte risorse.
