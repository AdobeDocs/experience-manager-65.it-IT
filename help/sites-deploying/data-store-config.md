---
title: Configurazione degli archivi dei nodi e dei dati in AEM 6
description: Scopri come configurare archivi di nodi e archivi di dati e come eseguire la raccolta di rifiuti dell’archivio dati.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '3461'
ht-degree: 1%

---

# Configurazione degli archivi dei nodi e dei dati in AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introduzione {#introduction}

In Adobe Experience Manager (AEM), i dati binari possono essere memorizzati indipendentemente dai nodi di contenuto. I dati binari vengono memorizzati in un archivio dati, mentre i nodi di contenuto vengono memorizzati in un archivio nodi.

Utilizzando la configurazione OSGi è possibile configurare sia gli archivi dati che quelli dei nodi. Per ogni configurazione OSGi viene fatto riferimento utilizzando un identificatore persistente (PID).

## Passaggi di configurazione {#configuration-steps}

Per configurare sia l’archivio nodi che l’archivio dati, effettua le seguenti operazioni:

1. Copiare il file JAR quickstart dell&#39;AEM nella relativa directory di installazione.
1. Creare una cartella `crx-quickstart/install` nella directory di installazione.
1. Innanzitutto, configurare l&#39;archivio nodi creando un file di configurazione con il nome dell&#39;opzione dell&#39;archivio nodi che si desidera utilizzare nella directory `crx-quickstart/install`.

   Ad esempio, l&#39;archivio dei nodi Document (che è la base per l&#39;implementazione di MongoMK da parte dell&#39;AEM) utilizza il file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Modifica il file e imposta le opzioni di configurazione.
1. Crea un file di configurazione con il PID dell’archivio dati che desideri utilizzare. Modificate il file per impostare le opzioni di configurazione.

   >[!NOTE]
   >
   >Consulta [Configurazioni archivio nodi](#node-store-configurations) e [Configurazioni archivio dati](#data-store-configurations) per le opzioni di configurazione.

1. Avvia AEM.

## Configurazioni archivio nodi {#node-store-configurations}

>[!CAUTION]
>
>Le versioni più recenti di Oak utilizzano un nuovo schema di denominazione e un nuovo formato per i file di configurazione OSGi. Il nuovo schema di denominazione richiede che il file di configurazione sia denominato **.config** e che il nuovo formato richieda la digitazione dei valori. Per informazioni dettagliate, vedere [Modello di provisioning Apache Sling e Apache SlingStart - Formato configurazione predefinito](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Se esegui l&#39;aggiornamento da una versione precedente di Oak, accertati di eseguire prima un backup della cartella `crx-quickstart/install`. Dopo l&#39;aggiornamento, ripristinare il contenuto della cartella nell&#39;installazione aggiornata e modificare l&#39;estensione dei file di configurazione da **.cfg** a **.config**.

### Archivio nodi segmento {#segment-node-store}

L’archivio dei nodi di segmento è la base dell’implementazione TarMK di Adobe nell’AEM6. Utilizza il PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` per la configurazione.

>[!CAUTION]
>
>Il PID per l&#39;archivio dei nodi di segmento è cambiato da `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` di AEM 6 a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` nell&#39;AEM 6.3. Assicurati di apportare le regolazioni di configurazione necessarie per riflettere questa modifica.

Puoi configurare le seguenti opzioni:

* `repository.home`: percorso della home del repository in cui vengono archiviati i dati relativi al repository. Per impostazione predefinita, i file dei segmenti vengono memorizzati nella directory `crx-quickstart/segmentstore`.

* `tarmk.size`: dimensione massima di un segmento in MB. Il valore massimo predefinito è 256 MB.
* `customBlobStore`: valore booleano che indica l&#39;utilizzo di un archivio dati personalizzato. Il valore predefinito è true per AEM 6.3 e versioni successive. Prima di AEM 6.3 il valore predefinito era falso.

Di seguito è riportato un esempio di file `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Archivio nodi documento {#document-node-store}

L’archivio dei nodi di documenti è la base dell’implementazione MongoMK dell’AEM. Utilizza il PID `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`*. Sono disponibili le seguenti opzioni di configurazione:

* `mongouri`: [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessario per connettersi al database Mongo. Il valore predefinito è `mongodb://localhost:27017`

* `db`: nome del database Mongo. Il nome predefinito del database è **Oak** ``. However, new AEM 6 installations use **aem-author** ``.

* `cache`: dimensione della cache in MB. Viene distribuito tra le varie cache utilizzate in DocumentNodeStore. Il valore predefinito è `256`

* `changesSize`: dimensione in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output diff. Il valore predefinito è `256`

* `customBlobStore`: valore booleano che indica l&#39;utilizzo di un archivio dati personalizzato. Il valore predefinito è `false`.

Di seguito è riportato un esempio di file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurazioni archivio dati {#data-store-configurations}

Quando si tratta di un numero elevato di file binari, si consiglia di utilizzare un archivio dati esterno invece degli archivi nodi predefiniti per massimizzare le prestazioni.

Ad esempio, se il progetto richiede molte risorse multimediali, la loro memorizzazione nel file o nell’archivio dati S3 rende l’accesso più rapido rispetto alla loro memorizzazione direttamente in un MongoDB.

File Data Store offre prestazioni migliori rispetto a MongoDB e le operazioni di backup e ripristino di Mongo sono più lente con un numero elevato di risorse.

Di seguito sono descritti i dettagli relativi ai diversi archivi e configurazioni di dati.

>[!NOTE]
>
>Per abilitare gli archivi dati personalizzati, è necessario assicurarsi che `customBlobStore` sia impostato su `true` nel rispettivo file di configurazione dell&#39;archivio nodi ([archivio nodi segmenti](/help/sites-deploying/data-store-config.md#segment-node-store) o [archivio nodi documenti](/help/sites-deploying/data-store-config.md#document-node-store)).

### Archivio file di dati {#file-data-store}

Implementazione di [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) presente in Jackrabbit 2. Fornisce un modo per memorizzare i dati binari come file normali sul file system. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Sono disponibili le seguenti opzioni di configurazione:

* `repository.home`: percorso della home del repository in cui vengono archiviati i dati relativi a vari repository. Per impostazione predefinita, i file binari vengono memorizzati nella directory `crx-quickstart/repository/datastore`

* `path`: percorso della directory in cui archiviare i file. Se specificato, ha la precedenza sul valore `repository.home`

* `minRecordLength`: dimensione minima in byte di un file archiviato nell&#39;archivio dati. Il contenuto binario inferiore a questo valore viene allineato.

>[!NOTE]
>
>Quando si utilizza un NAS per archiviare i file data store condivisi, assicurarsi di utilizzare solo dispositivi ad alte prestazioni per evitare problemi di prestazioni.

## Archivio dati Amazon S3 {#amazon-s-data-store}

L’AEM può essere configurato per memorizzare i dati nel servizio di archiviazione semplice (S3) di Amazon. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` per la configurazione.

>[!NOTE]
>
>AEM 6.5 supporta la memorizzazione di dati in Amazon S3, tuttavia il supporto non è esteso alla memorizzazione di dati in altre piattaforme, i cui fornitori possono avere le proprie implementazioni delle API S3 di Amazon.

Per abilitare la funzionalità di archiviazione dati di S3, è necessario scaricare e installare un feature pack contenente il connettore S3 Datastore. Vai a [Archivio Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) e scarica la versione più recente dalle versioni 1.10.x del feature pack (ad esempio, com.adobe.granite.oak.s3connector-1.10.0.zip). Inoltre, devi scaricare e installare il service pack AEM più recente come elencato nella pagina [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md).

>[!NOTE]
>
>Quando si utilizza AEM con TarMK, i file binari verranno memorizzati per impostazione predefinita in `FileDataStore`. Per utilizzare TarMK con l&#39;archivio dati S3, è necessario avviare AEM utilizzando la modalità di esecuzione `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, puoi installare e configurare il connettore S3 come segue:

1. Estrai il contenuto del file zip del feature pack in una cartella temporanea.

1. Vai alla cartella temporanea e passa alla seguente posizione:

   ```xml
   jcr_root/libs/system/install
   ```

   Copia tutti i contenuti dalla posizione precedente in `<aem-install>/crx-quickstart/install.`

1. Se AEM è già configurato per funzionare con l&#39;archivio Tar o MongoDB, rimuovi eventuali file di configurazione esistenti dalla cartella ***&lt;aem-install>***/*crx-quickstart*/*install* prima di procedere. I file che devono essere rimossi sono:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Tornate alla posizione temporanea in cui è stato estratto il feature pack e copiate il contenuto della cartella seguente:

   * `jcr_root/libs/system/config`

   in

   * `<aem-install>/crx-quickstart/install`

   Assicurati di copiare solo i file di configurazione necessari per la configurazione corrente. Copiare il file `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` sia per un archivio dati dedicato che per una configurazione dell&#39;archivio dati condiviso.

   >[!NOTE]
   >
   >In una configurazione cluster, eseguire i passaggi precedenti su tutti i nodi del cluster uno alla volta. Inoltre, assicurati di utilizzare le stesse impostazioni S3 per tutti i nodi.

1. Modifica il file e aggiungi le opzioni di configurazione richieste dalla configurazione.
1. Avvia AEM.

## Aggiornamento a una nuova versione del connettore 1.10.x S3 {#upgrading-to-a-new-version-of-the-s-connector}

Per effettuare l’aggiornamento a una nuova versione del connettore 1.10.x S3 (ad esempio, da 1.10.0 a 1.10.4), effettua le seguenti operazioni:

1. Arresta l’istanza AEM.

1. Passare a `<aem-install>/crx-quickstart/install/15` nella cartella di installazione dell&#39;AEM e creare un backup del contenuto.
1. Dopo il backup, eliminare la versione precedente del connettore S3 e le relative dipendenze eliminando tutti i file jar nella cartella `<aem-install>/crx-quickstart/install/15`, ad esempio:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >I nomi di file sopra indicati sono utilizzati solo a scopo illustrativo.

1. Scarica la versione più recente del feature pack 1.10.x dall&#39;[archivio Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Decomprimere il contenuto in una cartella separata, quindi passare a `jcr_root/libs/system/install/15`.
1. Copia i file jar in **&lt;aem-install>**/crx-quickstart/install/15 nella cartella di installazione dell&#39;AEM.
1. Avviare AEM e verificare la funzionalità del connettore.

Puoi utilizzare il file di configurazione con le opzioni descritte di seguito.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Opzioni del file di configurazione del connettore S3 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>Il connettore S3 supporta sia l’autenticazione degli utenti IAM che l’autenticazione dei ruoli IAM. Per utilizzare l&#39;autenticazione del ruolo IAM, omettere i valori `accessKey` e `secretKey` dal file di configurazione. Il connettore S3 verrà quindi assegnato per impostazione predefinita al ruolo [IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) assegnato all&#39;istanza.

| Chiave | Descrizione | Predefiniti | Obbligatorio |
| --- | --- | --- | --- |
| accessKey | ID chiave di accesso per l’utente IAM con accesso al bucket. | | Sì, quando non si utilizzano i ruoli IAM. |
| secretKey | Chiave di accesso segreta per l’utente IAM con accesso al bucket. | | Sì, quando non si utilizzano i ruoli IAM. |
| cacheSize | Dimensione (in byte) della cache locale. | 64 GB | No. |
| connectionTimeout | Imposta il tempo di attesa (in millisecondi) prima del timeout durante la creazione iniziale di una connessione. | 10000 | No. |
| maxCachedBinarySize | I file binari con dimensione minore o uguale a questo valore (in byte) vengono memorizzati nella cache della memoria. | 17408 (17 KB) | No. |
| maxConnections | Imposta il numero massimo di connessioni HTTP aperte consentite. | 50 | No. |
| maxErrorRetry | Imposta il numero massimo di tentativi per le richieste non riuscite (recuperabili). | 3 | No. |
| minRecordLength | Dimensione minima (in byte) di un oggetto da archiviare nell&#39;archivio dati. | 16384 | No. |
| percorso | Percorso locale dell’archivio dati dell’AEM. | `crx-quickstart/repository/datastore` | No. |
| proxyHost | Impostare l&#39;host proxy opzionale tramite cui il client si connette. | | No. |
| proxyPort | Impostare la porta proxy opzionale attraverso la quale il client si connette. | | No. |
| s3Bucket | Nome del bucket S3. | | Sì |
| s3EndPoint | Endpoint API REST S3. | | No. |
| s3Region | Area in cui risiede il bucket. Vedi questa [pagina](https://docs.aws.amazon.com/general/latest/gr/s3.html) per ulteriori dettagli. | Area in cui è in esecuzione l’istanza di AWS. | No. |
| socketTimeout | Impostare la quantità di tempo di attesa (in millisecondi) per il trasferimento dei dati su una connessione aperta stabilita prima che la connessione venga interrotta per timeout e chiusa. | 50000 | No. |
| stagingPurgeInterval | Intervallo (in secondi) per la rimozione dei caricamenti completati dalla cache di staging. | 300 | No. |
| stagingRetryInterval | Intervallo (in secondi) tra i tentativi di caricamento non riusciti. | 600 | No. |
| stagingSplitPercentage | Percentuale di `cacheSize` da utilizzare per la gestione temporanea dei caricamenti asincroni. | 10 | No. |
| uploadThreads | Il numero di thread di caricamento utilizzati per i caricamenti asincroni. | 10 | No. |
| writeThreads | Numero di thread simultanei utilizzati per la scrittura tramite Gestione trasferimenti S3. | 10 | No. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### Memorizzazione in cache di DataStore {#data-store-caching}

>[!NOTE]
>
>Le implementazioni DataStore di `S3DataStore`, `CachingFileDataStore` e `AzureDataStore` supportano il caching del file system locale. L&#39;implementazione di `CachingFileDataStore` è utile quando l&#39;archivio dati è su NFS (Network File System).

Quando si esegue l’aggiornamento da un’implementazione della cache precedente (precedente a Oak 1.6), vi è una differenza nella struttura della directory della cache del file system locale. Nella vecchia struttura della cache, sia i file scaricati che quelli caricati venivano inseriti direttamente nel percorso della cache. La nuova struttura separa i download e i caricamenti e li memorizza in due directory denominate `upload` e `download` nel percorso della cache. Il processo di aggiornamento deve essere semplice e gli eventuali caricamenti in sospeso devono essere pianificati per il caricamento e tutti i file precedentemente scaricati nella cache vengono inseriti nella cache al momento dell’inizializzazione.

È inoltre possibile aggiornare la cache offline utilizzando il comando `datastorecacheupgrade` di oak-run. Per informazioni dettagliate su come eseguire il comando, controllare il file [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) per il modulo oak-run.

La cache ha un limite di dimensioni e può essere configurata utilizzando il parametro cacheSize.

#### Download {#downloads}

La cache locale viene controllata per il record del file o del BLOB richiesto prima di accedervi dall&#39;archivio dati. Quando la cache supera il limite configurato (vedere il parametro `cacheSize`) durante l&#39;aggiunta di un file nella cache, alcuni file vengono eliminati per recuperare spazio.

#### Caricamento asincrono {#async-upload}

La cache supporta i caricamenti asincroni nel DataStore. I file vengono posizionati nell’area intermedia localmente, nella cache (sul file system), e viene avviato un processo asincrono per caricare il file. Il numero di caricamenti asincroni è limitato dalla dimensione della cache di staging. La dimensione della cache di gestione temporanea è configurata utilizzando il parametro `stagingSplitPercentage`. Questo parametro definisce la percentuale di dimensione della cache da utilizzare per la cache di staging. Inoltre, la percentuale di cache disponibile per i download è calcolata come **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

I caricamenti asincroni sono multithread e il numero di thread è configurato utilizzando il parametro `uploadThreads`.

Al termine dei caricamenti, i file vengono spostati nella cache di download principale. Quando la dimensione della cache di gestione temporanea supera il limite, i file vengono caricati in modo sincrono nel DataStore fino al completamento dei caricamenti asincroni precedenti e fino a quando non viene nuovamente disponibile spazio nella cache di gestione temporanea. I file caricati vengono rimossi dall&#39;area di gestione temporanea da un processo periodico il cui intervallo è configurato dal parametro `stagingPurgeInterval`.

I caricamenti non riusciti (ad esempio, a causa di un’interruzione della rete) vengono inseriti in una coda di nuovi tentativi e ripetuti periodicamente. L&#39;intervallo tra i tentativi è configurato utilizzando `stagingRetryInterval parameter`.

#### Configurazione della replica senza binari con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Per configurare la replica senza binari con S3, sono necessari i seguenti passaggi:

1. Installa le istanze di authoring e pubblicazione e assicurati che vengano avviate correttamente.
1. Passare alle impostazioni dell&#39;agente di replica aprendo una pagina a *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Premi il pulsante **Modifica** nella sezione **Impostazioni**.
1. Cambia l&#39;opzione di tipo **Serializzazione** in **Binary less**.

1. Aggiungere il parametro &quot; `binaryless`= `true`&quot; nell&#39;URI di trasporto. Dopo la modifica, l’URI deve essere simile al seguente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Riavvia tutte le istanze di authoring e pubblicazione per rendere effettive le modifiche.

#### Creazione di un cluster tramite S3 e MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Decomprimi l’avvio rapido di CQ con il seguente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Dopo aver decompresso AEM, creare una cartella nella directory di installazione *crx-quickstart*/*install*.

1. Crea questi due file nella cartella `crx-quickstart`:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Dopo aver creato i file, aggiungi le opzioni di configurazione necessarie.

1. Installa i due bundle richiesti per l’archivio dati S3 come spiegato in precedenza.
1. Verificare che MongoDB sia installato e che un&#39;istanza di `mongod` sia in esecuzione.
1. Avvia AEM con il seguente comando:

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Ripetere i passaggi da 1 a 4 per la seconda istanza di AEM.
1. Avvia la seconda istanza di AEM.

#### Configurazione di un archivio dati condiviso {#configuring-a-shared-data-store}

1. Innanzitutto, crea il file di configurazione dell’archivio dati su ogni istanza necessaria per condividere l’archivio dati:

   * Se si utilizza un `FileDataStore`, creare un file denominato `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e inserirlo nella cartella `<aem-install>/crx-quickstart/install`.

   * Se si utilizza S3 come archivio dati, creare un file denominato o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` nella cartella `<aem-install>/crx-quickstart/install` come indicato sopra.

1. Modifica i file di configurazione dell’archivio dati in ogni istanza in modo che puntino allo stesso archivio dati. Per ulteriori informazioni, vedere [Configurazioni archivio dati](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Se l&#39;istanza è stata clonata da un server esistente, è necessario rimuovere `clusterId` della nuova istanza utilizzando l&#39;ultimo strumento oak-run mentre l&#39;archivio è offline. Il comando da eseguire è:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Se è configurato un archivio dei nodi di segmento, è necessario specificare il percorso dell’archivio. Per impostazione predefinita, il percorso è `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Se è configurato un archivio nodi Document, è possibile utilizzare un URI [stringa di connessione Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Lo strumento eseguito da Oak può essere scaricato da questa posizione:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >È necessario utilizzare versioni diverse dello strumento, a seconda della versione di Oak utilizzata con l’installazione dell’AEM. Prima di utilizzare lo strumento, controlla l’elenco dei requisiti delle versioni riportato di seguito:
   >
   >
   >
   >    * Per le versioni di Oak **1.2.x** utilizza l&#39;Oak-run **1.2.12 o successiva**
   >    * Per le versioni di Oak **più recenti di quelle precedenti**, utilizza la versione di Oak-run che corrisponde al core Oak dell&#39;installazione AEM.
   >
   >

1. Infine, convalida la configurazione. Per eseguire la convalida, cerca un file univoco aggiunto all’archivio dati da ogni archivio che lo condivide. Il formato dei file è `repository-[UUID]`, dove l&#39;UUID è un identificatore univoco di ogni singolo archivio.

   Pertanto, una configurazione corretta deve avere un numero di file univoci pari al numero di archivi che condividono l’archivio dati.

   I file vengono memorizzati in modo diverso, a seconda dell’archivio dati:

   * Per `FileDataStore` i file vengono creati nel percorso radice della cartella dell&#39;archivio dati.
   * Per `S3DataStore` i file vengono creati nel bucket S3 configurato nella cartella `META`.

## Archivio dati Azure {#azure-data-store}

L’AEM può essere configurato per archiviare i dati nel servizio di archiviazione Azure di Microsoft®. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` per la configurazione.

Per abilitare la funzionalità dell’archivio dati di Azure, è necessario scaricare e installare un feature pack contenente il connettore di Azure. Vai a [Archivio Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) e scarica la versione più recente dalle versioni 1.6.x del feature pack (ad esempio, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Quando si utilizza l’AEM con TarMK, i file binari vengono memorizzati per impostazione predefinita in FileDataStore. Per utilizzare TarMK con Azure DataStore, è necessario avviare AEM utilizzando la modalità di esecuzione `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, puoi installare e configurare il connettore Azure come segue:

1. Estrai il contenuto del file zip del feature pack in una cartella temporanea.

1. Passare alla cartella temporanea e copiare il contenuto di `jcr_root/libs/system/install` nella cartella `<aem-install>crx-quickstart/install`.
1. Se AEM è già configurato per l&#39;utilizzo con l&#39;archiviazione Tar o MongoDB, rimuovere tutti i file di configurazione esistenti dalla cartella `/crx-quickstart/install` prima di procedere. I file che devono essere rimossi sono:

   Per MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Per TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Tornare al percorso temporaneo in cui è stato estratto il feature pack e copiare il contenuto di `jcr_root/libs/system/config` nella cartella `<aem-install>/crx-quickstart/install`.
1. Modifica il file di configurazione e aggiungi le opzioni di configurazione richieste dalla configurazione.
1. Avvia AEM.

Puoi utilizzare il file di configurazione con le seguenti opzioni:

* azureSas=&quot;&quot;: nella versione 1.6.3 del connettore è stato aggiunto il supporto per la firma di accesso condiviso di Azure. **Se nel file di configurazione sono presenti sia le credenziali SAS che le credenziali di archiviazione, SAS ha la priorità.** Per ulteriori informazioni sulle associazioni di protezione, vedere la [documentazione ufficiale](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview). Assicurati che il carattere &#39;=&#39; sia di escape come &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: l&#39;endpoint BLOB di Azure. Ad esempio, https://&lt;account di archiviazione>.blob.core.windows.net.
* accessKey=&quot;&quot;: nome dell&#39;account di archiviazione. Per ulteriori dettagli sulle credenziali di autenticazione di Microsoft® Azure, vedere la [documentazione ufficiale](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: la chiave di accesso all’archiviazione. Assicurati che il carattere &#39;=&#39; sia di escape come &#39;\=&#39;.
* container=&quot;&quot;: nome del contenitore di archiviazione BLOB di Microsoft® Azure. Il contenitore è un raggruppamento di un insieme di BLOB. Per ulteriori dettagli, consulta la [documentazione ufficiale](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN).
* maxConnections=&quot;&quot;: il numero simultaneo di richieste simultanee per operazione. Il valore predefinito è 1.
* maxErrorRetry=&quot;&quot;: numero di tentativi per richiesta. Il valore predefinito è 3.
* socketTimeout=&quot;&quot;: intervallo di timeout, in millisecondi, utilizzato per la richiesta. Il valore predefinito è 5 minuti.

Oltre alle impostazioni precedenti, è possibile configurare anche le seguenti impostazioni:

* path: percorso dell’archivio dati. Il valore predefinito è `<aem-install>/repository/datastore.`
* RecordLength: dimensione minima di un oggetto che deve essere memorizzato nell&#39;archivio dati. Il valore predefinito è 16 KB.
* maxCachedBinarySize: i file binari con dimensioni inferiori o uguali a queste dimensioni vengono memorizzati nella cache della memoria. Dimensione in byte. Il valore predefinito è 17408 (17 KB).
* cacheSize: dimensione della cache. Il valore è specificato in byte. Il valore predefinito è 64 GB.
* secret: da utilizzare solo se si utilizza la replica senza dati binari per la configurazione dell’archivio dati condiviso.
* stagingSplitPercentage: percentuale della dimensione della cache configurata per l’utilizzo per la gestione temporanea di caricamenti asincroni. Il valore predefinito è 10.
* uploadThreads: il numero di thread di upload utilizzati per i caricamenti asincroni. Il valore predefinito è 10.
* stagingPurgeInterval: intervallo in secondi per la rimozione dei caricamenti completati dalla cache di staging. Il valore predefinito è 300 secondi (5 minuti).
* stagingRetryInterval: intervallo tra i tentativi in secondi per i caricamenti non riusciti. Il valore predefinito è 600 secondi (10 minuti).

>[!NOTE]
>
>Tutte le impostazioni devono essere inserite tra virgolette, ad esempio:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Raccolta oggetti inattivi dell’archivio dati {#data-store-garbage-collection}

Il processo di Garbage Collection dell’archivio dati viene utilizzato per rimuovere eventuali file inutilizzati nell’archivio dati, liberando così spazio su disco prezioso nel processo.

Per eseguire la raccolta di oggetti inattivi dell’archivio dati:

1. Vai alla console JMX all&#39;indirizzo *https://&lt;serveraddress:port>/system/console/jmx*
1. Ricerca di **RepositoryManagement.** Una volta trovato l&#39;MBean di Repository Manager, fare clic su di esso per visualizzare le opzioni disponibili.
1. Scorri fino alla fine della pagina e fai clic sul collegamento **startDataStoreGC(boolean markOnly)**.
1. Nella finestra di dialogo seguente, immetti `false` per il parametro `markOnly`, quindi fai clic su **Richiama**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >Il parametro `markOnly` indica se la fase di sweep della raccolta di oggetti inattivi è in esecuzione o meno.

## Raccolta oggetti inattivi dell’archivio dati per un archivio dati condiviso {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Quando si esegue la raccolta di oggetti inattivi in un archivio dati condiviso o in cluster, l’impostazione (con Mongo o Segment Tar) del registro potrebbe visualizzare avvisi sull’impossibilità di eliminare determinati ID BLOB. Agli ID BLOB eliminati in una precedente raccolta di oggetti inattivi viene fatto erroneamente riferimento da altri cluster o nodi condivisi che non dispongono di informazioni sulle eliminazioni degli ID. Di conseguenza, quando viene eseguita la raccolta di oggetti inattivi, registra un avviso quando tenta di eliminare un ID che è già stato eliminato nell’ultima esecuzione. Questo comportamento non influisce sulle prestazioni o sulle funzionalità.

>[!NOTE]
>
>Se utilizzi una configurazione dell’archivio dati condiviso e la raccolta di oggetti inattivi dell’archivio dati è disabilitata, l’esecuzione dell’attività di pulizia binaria di Lucene può improvvisamente aumentare lo spazio su disco utilizzato. Prova a disabilitare BlobTracker su tutte le istanze di authoring e pubblicazione effettuando le seguenti operazioni:
>
>1. Interrompi l’istanza AEM.
>2. Aggiungi il parametro `blobTrackSnapshotIntervalInSecs=L"0"` nel file `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`. Questo parametro richiede Oak 1.12.0, 1.10.2 o versione successiva.
>3. Riavvia l’istanza AEM.

Con le versioni più recenti di AEM, la raccolta di oggetti inattivi dell’archivio dati può essere eseguita anche sugli archivi dati condivisi da più di un archivio. Per poter eseguire la raccolta di oggetti inattivi dell’archivio dati in un archivio dati condiviso, effettua le seguenti operazioni:

1. Assicurati che tutte le attività di manutenzione configurate per la raccolta di oggetti inattivi dell’archivio dati siano disabilitate in tutte le istanze dell’archivio che condividono l’archivio dati.
1. Esegui i passaggi indicati in [Raccolta oggetti inattivi binari](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) singolarmente in **tutte** le istanze dell&#39;archivio che condividono l&#39;archivio dati. Tuttavia, assicurarsi di immettere `true` per il parametro `markOnly` prima di fare clic sul pulsante Richiama:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Dopo aver completato la procedura precedente in tutte le istanze, esegui nuovamente il garbage collect dell&#39;archivio dati da **qualsiasi** delle istanze:

   1. Vai alla console JMX e seleziona Repository Manager Mbean.
   1. Fai clic sul collegamento **Fai clic su startDataStoreGC(boolean markOnly)**.
   1. Nella finestra di dialogo seguente, immetti di nuovo `false` per il parametro `markOnly`.

   Tutti i file trovati vengono fascicolati utilizzando la fase contrassegno utilizzata in precedenza ed eliminano gli altri file non utilizzati dall&#39;archivio dati.
