---
title: Configurazione degli archivi di nodi e degli archivi di dati nel AEM 6
seo-title: Configurazione degli archivi di nodi e degli archivi di dati nel AEM 6
description: Scopri come configurare gli archivi di nodi e gli archivi di dati e come eseguire la raccolta degli oggetti inattivi dell’archivio dati.
seo-description: Scopri come configurare gli archivi di nodi e gli archivi di dati e come eseguire la raccolta degli oggetti inattivi dell’archivio dati.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 1%

---


# Configurazione degli archivi dei nodi e degli archivi di dati in AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introduzione {#introduction}

In Adobe Experience Manager (AEM), i dati binari possono essere memorizzati indipendentemente dai nodi di contenuto. I dati binari vengono memorizzati in un archivio dati, mentre i nodi di contenuto sono memorizzati in un archivio nodi.

È possibile configurare sia gli archivi di dati che gli archivi dei nodi utilizzando la configurazione OSGi. A ogni configurazione OSGi viene fatto riferimento utilizzando un identificatore permanente (PID).

## Passaggi di configurazione {#configuration-steps}

Per configurare sia l&#39;archivio nodi che l&#39;archivio dati, esegui questi passaggi:

1. Copia il file JAR AEM quickstart nella relativa directory di installazione.
1. Crea una cartella `crx-quickstart/install` nella directory di installazione.
1. Per prima cosa, configura l&#39;archivio nodi creando un file di configurazione con il nome dell&#39;opzione dell&#39;archivio nodi che desideri utilizzare nella directory `crx-quickstart/install`.

   Ad esempio, l&#39;archivio dei nodi Document (che è la base per AEM&#39;implementazione MongoMK) utilizza il file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Modifica il file e imposta le opzioni di configurazione.
1. Crea un file di configurazione con il PID dell’archivio dati che desideri utilizzare. Modifica il file per impostare le opzioni di configurazione.

   >[!NOTE]
   >
   >Per le opzioni di configurazione, consulta [Configurazioni archivio nodi](#node-store-configurations) e [Configurazioni archivio dati](#data-store-configurations) .

1. Inizia AEM.

## Configurazioni dell&#39;archivio nodi {#node-store-configurations}

>[!CAUTION]
>
>Le versioni più recenti di Oak utilizzano un nuovo schema e formato di denominazione per i file di configurazione OSGi. Il nuovo schema di denominazione richiede che il file di configurazione sia denominato **.config** e che il nuovo formato richieda la digitazione di valori ed è [documentato qui](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Se esegui l’aggiornamento da una versione precedente di Oak, assicurati di eseguire prima un backup della cartella `crx-quickstart/install`. Dopo l&#39;aggiornamento, ripristina il contenuto della cartella nell&#39;installazione aggiornata e modifica l&#39;estensione dei file di configurazione da **.cfg** a **.config**.
>
>Se leggi questo articolo in preparazione di un aggiornamento da un&#39;installazione di **AEM 5.x**, assicurati di consultare prima la documentazione [upgrade](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) .

### Archivio dei nodi del segmento {#segment-node-store}

L’archivio dei nodi del segmento è la base dell’implementazione TarMK di Adobe in AEM6. Utilizza il `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID per la configurazione.

>[!CAUTION]
>
>Il PID per l’archivio dei nodi di segmento è stato modificato da `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` di AEM 6 a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` in AEM 6.3. Assicurati di effettuare le regolazioni di configurazione necessarie per riflettere questa modifica.

Puoi configurare le seguenti opzioni:

* `repository.home`: Percorso della home del repository in cui vengono archiviati i dati relativi al repository. Per impostazione predefinita, i file dei segmenti sono memorizzati nella directory `crx-quickstart/segmentstore` .

* `tarmk.size`: Dimensione massima di un segmento in MB. Il massimo predefinito è 256 MB.
* `customBlobStore`: Valore booleano che indica l&#39;utilizzo di un archivio dati personalizzato. Il valore predefinito è true per AEM 6.3 e versioni successive. Prima di AEM 6.3, il valore predefinito era false.

Di seguito è riportato un file di esempio `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` :

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Archiviazione dei nodi del documento {#document-node-store}

L&#39;archivio dei nodi del documento è la base dell&#39;implementazione AEM MongoMK. Utilizza il `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Sono disponibili le seguenti opzioni di configurazione:

* `mongouri`: Il  [](https://docs.mongodb.org/manual/reference/connection-string/) MongoURIrichiesto per connettersi al database Mongo. Il valore predefinito è `mongodb://localhost:27017`

* `db`: Nome del database Mongo. Il valore predefinito è **Oak** ``. However, new AEM 6 installations use **aem-author** ``come nome predefinito del database.

* `cache`: Dimensione della cache in MB. Questa viene distribuita tra le varie cache utilizzate in DocumentNodeStore. Il valore predefinito è `256`

* `changesSize`: Dimensioni in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output diff. Il valore predefinito è `256`

* `customBlobStore`: Valore booleano che indica che verrà utilizzato un archivio dati personalizzato. Il valore predefinito è `false`.

Di seguito è riportato un file di esempio `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` :

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurazioni archivio dati {#data-store-configurations}

Quando si gestisce un numero elevato di binari, si consiglia di utilizzare un archivio dati esterno al posto degli archivi nodi predefiniti per massimizzare le prestazioni.

Ad esempio, se il progetto richiede un numero elevato di risorse multimediali, memorizzarle nel File o nell’archivio dati S3 consente di accedervi più rapidamente che archiviarle direttamente all’interno di un MongoDB.

Il File Data Store offre prestazioni migliori rispetto a MongoDB, e le operazioni di backup e ripristino Mongo sono anche più lente con un gran numero di risorse.

Di seguito sono descritti i dettagli sui diversi archivi di dati e configurazioni.

>[!NOTE]
>
>Per abilitare gli archivi dati personalizzati, è necessario assicurarsi che `customBlobStore` sia impostato su `true` nel rispettivo file di configurazione Node Store ([archivio nodi segmento](/help/sites-deploying/data-store-config.md#segment-node-store) o [archivio nodi documento](/help/sites-deploying/data-store-config.md#document-node-store)).

### Archivio file di dati {#file-data-store}

Implementazione di [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) presente in Jackrabbit 2. Fornisce un modo per memorizzare i dati binari come file normali sul file system. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Sono disponibili le seguenti opzioni di configurazione:

* `repository.home`: Percorso della home dell&#39;archivio in cui vengono archiviati vari dati relativi all&#39;archivio. Per impostazione predefinita, i file binari vengono memorizzati nella directory `crx-quickstart/repository/datastore`

* `path`: Percorso della directory in cui vengono archiviati i file. Se specificato, ha la precedenza sul valore `repository.home`

* `minRecordLength`: Dimensione minima in byte di un file archiviato nell&#39;archivio dati. Il contenuto binario inferiore a questo valore viene allineato.

>[!NOTE]
>
>Quando si utilizza un NAS per memorizzare gli archivi di dati dei file condivisi, assicurarsi di utilizzare solo dispositivi con prestazioni elevate per evitare problemi di prestazioni.

## Archivio dati Amazon S3 {#amazon-s-data-store}

AEM può essere configurato per memorizzare i dati in Amazon Simple Storage Service (S3). Utilizza il `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID per la configurazione.

Per abilitare la funzionalità dell&#39;archivio dati S3, è necessario scaricare e installare un feature pack contenente il connettore S3 Datastore. Vai al [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) e scarica l&#39;ultima versione dalle versioni 1.10.x del feature pack (ad esempio, com.adobe.granite.oak.s3connector-1.10.0.zip). Inoltre, devi scaricare e installare l&#39;ultimo service pack AEM come elencato nella pagina [AEM Note sulla versione 6.5](/help/release-notes/sp-release-notes.md) .

>[!NOTE]
>
>Quando si utilizza AEM con TarMK, i binari vengono memorizzati per impostazione predefinita in `FileDataStore`. Per utilizzare TarMK con il Datastore S3, è necessario avviare AEM utilizzando la modalità runmode `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, è possibile installare e configurare il S3 Connector come segue:

1. Estrarre il contenuto del file zip del feature pack in una cartella temporanea.

1. Passa alla cartella temporanea e passa al seguente percorso:

   ```xml
   jcr_root/libs/system/install
   ```

   Copia tutti i contenuti dalla posizione precedente in `<aem-install>/crx-quickstart/install.`

1. Se AEM è già configurato per lavorare con l&#39;archivio Tar o MongoDB, rimuovi eventuali file di configurazione esistenti dalla cartella ***&lt;aem-install>**/*crx-quickstart*/*install* prima di procedere. I file da rimuovere sono:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Torna alla posizione temporanea in cui è stato estratto il pacchetto di funzionalità e copia il contenuto della cartella seguente:

   * `jcr_root/libs/system/config`

   a

   * `<aem-install>/crx-quickstart/install`

   Assicurati di copiare solo i file di configurazione necessari per la configurazione corrente. Per un archivio dati dedicato e una configurazione dell&#39;archivio dati condivisa, copia il file `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >In una configurazione cluster, esegui i passaggi sopra descritti su tutti i nodi del cluster uno per uno. Inoltre, assicurati di utilizzare le stesse impostazioni S3 per tutti i nodi.

1. Modifica il file e aggiungi le opzioni di configurazione richieste dalla configurazione.
1. Inizia AEM.

### Aggiornamento a una nuova versione del connettore S3 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Per effettuare l’aggiornamento a una nuova versione del connettore S3 1.10.x (ad esempio, da 1.10.0 a 1.10.4), effettua le seguenti operazioni:

1. Interrompi l&#39;istanza AEM.

1. Passa a `<aem-install>/crx-quickstart/install/15` nella cartella di installazione di AEM ed effettua un backup del relativo contenuto.
1. Dopo il backup, elimina la vecchia versione del S3 Connector e le sue dipendenze eliminando tutti i file jar nella cartella `<aem-install>/crx-quickstart/install/15`, ad esempio:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >I nomi di file sopra riportati sono utilizzati solo a scopo illustrativo.

1. Scarica la versione più recente del pacchetto di funzioni 1.8.x dal [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Decomprimi il contenuto in una cartella separata, quindi passa a `jcr_root/libs/system/install/15`.
1. Copia i file jar in **&lt;aem-install>**/crx-quickstart/install/15 nella cartella di installazione AEM.
1. Avvia AEM e controlla la funzionalità del connettore.

Puoi utilizzare il file di configurazione con le seguenti opzioni:

* accessKey: Chiave di accesso AWS.
* secretKey: Chiave di accesso segreto AWS. **Nota:** in alternativa, i  [ruoli IAM ](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) possono essere utilizzati per l&#39;autenticazione. Se utilizzi i ruoli IAM, non è più necessario specificare i valori `accessKey` e `secretKey`.

* s3Bucket: Nome del bucket.
* s3Region: La regione del bucket.
* percorso: Percorso dell&#39;archivio dati. Il valore predefinito è **&lt;AEM cartella di installazione>/repository/datastore**
* minRecordLength: Dimensione minima di un oggetto che deve essere memorizzato nell&#39;archivio dati. Il valore minimo/predefinito è **16 KB.**
* maxCachedBinarySize: I binari con dimensioni inferiori o uguali a queste dimensioni verranno memorizzati nella cache di memoria. La dimensione è espressa in byte. Il valore predefinito è **17408 **(17 KB).

* cacheSize: Dimensione della cache. Il valore è specificato in byte. Il valore predefinito è **64 GB**.
* segreto: Da utilizzare solo se si utilizza la replica binaryless per l&#39;impostazione di un archivio dati condiviso.
* stagingSplitPercentage: Percentuale di dimensioni della cache configurate da utilizzare per i caricamenti asincroni di staging. Il valore predefinito è **10**.
* uploadThreads: Il numero di thread di caricamento utilizzati per i caricamenti asincroni. Il valore predefinito è **10**.
* stagingPurgeInterval: Intervallo in secondi per lo svuotamento dei caricamenti completati dalla cache di staging. Il valore predefinito è **300** secondi (5 minuti).
* stagingRetryInterval: Intervallo dei tentativi in secondi per caricamenti non riusciti. Il valore predefinito è **600** secondi (10 minuti).

### Opzioni dell&#39;area a blocchi {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>Standard USA</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>Stati Uniti d'America</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (California del nord)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>UE (Irlanda)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacifico (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacifico (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacifico (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>Sud America (San Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**Memorizzazione in cache del DataStore**

>[!NOTE]
>
>Le implementazioni di DataStore di `S3DataStore`, `CachingFileDataStore` e `AzureDataStore` supportano il caching dei file system locali. L&#39;implementazione `CachingFileDataStore` è utile quando DataStore è su NFS (Network File System).


Quando si esegue l’aggiornamento da un’implementazione precedente della cache (prima di Oak 1.6), c’è una differenza nella struttura della directory della cache del file system locale. Nella vecchia struttura della cache sia i file scaricati che quelli caricati sono stati messi direttamente sotto il percorso della cache. La nuova struttura separa i download e i caricamenti e li memorizza in due directory denominate `upload` e `download` nel percorso della cache. Il processo di aggiornamento dovrebbe essere senza soluzione di continuità e tutti i caricamenti in sospeso dovrebbero essere pianificati per il caricamento e tutti i file precedentemente scaricati nella cache verranno inseriti nella cache al momento dell&#39;inizializzazione.

Puoi anche aggiornare la cache offline utilizzando il comando `datastorecacheupgrade` di oak-run. Per informazioni dettagliate su come eseguire il comando, controllare [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) per il modulo oak-run.

La cache ha un limite di dimensioni e può essere configurata utilizzando il parametro cacheSize.

**Download**

La cache locale verrà controllata per individuare il record del file/BLOB richiesto prima di accedervi dal DataStore. Quando la cache supera il limite configurato (vedi il parametro `cacheSize` ) durante l’aggiunta di un file nella cache, alcuni dei file verranno sfrattati per recuperare spazio.

**Caricamento asincrono**

La cache supporta caricamenti asincroni in DataStore. I file vengono memorizzati localmente, nella cache (nel file system) e inizia un processo asincrono per caricare il file. Il numero di caricamenti asincroni è limitato dalle dimensioni della cache di staging. La dimensione della cache di staging viene configurata utilizzando il parametro `stagingSplitPercentage` . Questo parametro definisce la percentuale di dimensione della cache da utilizzare per la cache di staging. Inoltre, la percentuale di cache disponibile per i download è calcolata come **(100 - `stagingSplitPercentage`) *`cacheSize`**.

I caricamenti asincroni sono multithread e il numero di thread è configurato utilizzando il parametro `uploadThreads` .

I file vengono spostati nella cache di download principale al termine dei caricamenti. Quando la dimensione della cache di staging supera il limite, i file vengono caricati in modo sincrono nel DataStore fino a quando i caricamenti asincroni precedenti non sono completi e lo spazio è nuovamente disponibile nella cache di staging. I file caricati vengono rimossi dall’area di gestione temporanea da un processo periodico il cui intervallo è configurato dal parametro `stagingPurgeInterval` .

I caricamenti non riusciti (ad esempio a causa di un’interruzione della rete) vengono messi in una coda di nuovi tentativi e riprovati periodicamente. L&#39;intervallo di tentativi è configurato utilizzando il parametro `stagingRetryInterval parameter`.

#### Configurazione della replica binaryless con Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Per configurare la replica binaryless con S3, sono necessari i seguenti passaggi:

1. Installa le istanze di authoring e pubblicazione e assicurati che siano avviate correttamente.
1. Vai alle impostazioni dell&#39;agente di replica, aprendo una pagina su *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Premere il pulsante **Modifica** nella sezione **Impostazioni**.
1. Cambia l&#39;opzione del tipo **Serialization** in **Binary less**.

1. Aggiungi il parametro &quot; `binaryless`= `true`&quot; nell&#39;URI di trasporto. Dopo la modifica, l’uri deve essere simile al seguente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Riavvia tutte le istanze di authoring e pubblicazione per rendere effettive le modifiche.

#### Creazione di un cluster utilizzando S3 e MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Estrai CQ quickstart utilizzando il seguente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Dopo AEM scompattato, crea una cartella all&#39;interno della directory di installazione *crx-quickstart*/*install*.

1. Crea questi due file all&#39;interno della cartella `crx-quickstart` :

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Dopo aver creato i file, aggiungi le opzioni di configurazione necessarie.

1. Installa i due bundle necessari per l&#39;archivio dati S3 come spiegato sopra.
1. Assicurati che MongoDB sia installato e che sia in esecuzione un&#39;istanza di `mongod`.
1. Inizia AEM con il seguente comando:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Ripetere i passaggi da 1 a 4 per la seconda istanza AEM.
1. Avvia la seconda istanza AEM.

#### Configurazione di un archivio dati condiviso {#configuring-a-shared-data-store}

1. Innanzitutto, crea il file di configurazione dell’archivio dati su ogni istanza necessaria per condividere l’archivio dati:

   * Se utilizzi un file `FileDataStore`, crea un file denominato `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e inseriscilo nella cartella `<aem-install>/crx-quickstart/install`.

   * Se utilizzi S3 come archivio dati, crea un file denominato o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` nella cartella `<aem-install>/crx-quickstart/install` come indicato sopra.

1. Modifica i file di configurazione dell&#39;archivio dati in ogni istanza in modo che puntino allo stesso archivio dati. Per ulteriori informazioni, consulta [questo articolo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Se l’istanza è stata clonata da un server esistente, devi rimuovere la `clusterId` della nuova istanza utilizzando lo strumento oak-run più recente mentre l’archivio è offline. Il comando da eseguire è:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Se è configurato un archivio dei nodi di segmento, è necessario specificare il percorso del repository. Per impostazione predefinita, il percorso è `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Se è configurato un archivio dei nodi del documento, è possibile utilizzare un [URI della stringa di connessione Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Lo strumento Oak-run può essere scaricato da questo percorso:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Tieni presente che è necessario utilizzare diverse versioni dello strumento a seconda della versione Oak utilizzata con l’installazione di AEM. Prima di utilizzare lo strumento, controlla l’elenco dei requisiti di versione riportato di seguito:
   >
   >
   >
   >    * Per le versioni Oak **1.2.x** utilizza l&#39;esecuzione Oak **1.2.12 o successive**
   >    * Per le versioni Oak **più recenti rispetto a quanto indicato sopra**, utilizza la versione di Oak-run che corrisponde al nucleo Oak dell&#39;installazione AEM.


1. Infine, convalida la configurazione. A questo scopo, è necessario cercare un file univoco aggiunto all’archivio dati da ogni archivio che lo condivide. Il formato dei file è `repository-[UUID]`, dove l’UUID è un identificatore univoco di ciascun archivio.

   Pertanto, una configurazione corretta deve contenere tutti i file univoci quanti sono gli archivi che condividono l&#39;archivio dati.

   I file vengono memorizzati in modo diverso, a seconda dell&#39;archivio dati:

   * Per `FileDataStore` i file vengono creati nel percorso principale della cartella dell&#39;archivio dati.
   * Per `S3DataStore` i file vengono creati nel bucket S3 configurato sotto la cartella `META` .

## Archivio dati Azure {#azure-data-store}

AEM può essere configurato per memorizzare i dati nel servizio di archiviazione di Microsoft Azure. Utilizza il `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID per la configurazione.

Per abilitare la funzionalità dell’archivio dati di Azure, è necessario scaricare e installare un pacchetto di funzioni contenente il connettore di Azure. Vai al [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) e scarica l&#39;ultima versione dalle versioni 1.6.x del feature pack (ad esempio, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Quando si utilizza AEM con TarMK, i binari verranno memorizzati per impostazione predefinita nel FileDataStore. Per utilizzare TarMK con Azure DataStore, è necessario avviare AEM utilizzando la modalità di esecuzione `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, puoi installare e configurare il connettore di Azure come segue:

1. Estrarre il contenuto del file zip del feature pack in una cartella temporanea.

1. Vai alla cartella temporanea e copia il contenuto di `jcr_root/libs/system/install` nella cartella `<aem-install>crx-quickstart/install`.
1. Se AEM è già configurato per lavorare con l&#39;archivio Tar o MongoDB, rimuovi eventuali file di configurazione esistenti dalla cartella `/crx-quickstart/install` prima di procedere. I file da rimuovere sono:

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Per TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Torna alla posizione temporanea in cui è stato estratto il feature pack e copia il contenuto di `jcr_root/libs/system/config` nella cartella `<aem-install>/crx-quickstart/install`.
1. Modifica il file di configurazione e aggiungi le opzioni di configurazione richieste dalla configurazione.
1. Inizia AEM.

Puoi utilizzare il file di configurazione con le seguenti opzioni:

* azureSas=&quot;&quot;: Nella versione 1.6.3 del connettore è stato aggiunto il supporto per la firma di accesso condiviso (SAS) di Azure. **Se nel file di configurazione sono presenti sia le credenziali SAS che di archiviazione, SAS ha priorità.** Per ulteriori informazioni su SAS, consultare la documentazione  [ufficiale](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). Assicurati che il carattere &#39;=&#39; sia preceduto da &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: Endpoint BLOB di Azure. Ad esempio, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: Nome dell&#39;account di archiviazione. Per ulteriori dettagli sulle credenziali di autenticazione di Microsoft Azure, consulta la [documentazione ufficiale](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: Chiave di accesso allo storage. Assicurati che il carattere &#39;=&#39; sia preceduto da &#39;\=&#39;.
* container=&quot;&quot;: Nome del contenitore di archiviazione BLOB di Microsoft Azure. Il contenitore è un raggruppamento di un set di BLOB. Per ulteriori informazioni, consulta la [documentazione ufficiale](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;: Numero simultaneo di richieste simultanee per operazione. Il valore predefinito è 1.
* maxErrorRetry=&quot;&quot;: Numero di tentativi per richiesta. Il valore predefinito è 3.
* socketTimeout=&quot;&quot;: Intervallo di timeout, in millisecondi, utilizzato per la richiesta. Il valore predefinito è 5 minuti.

Oltre alle impostazioni di cui sopra, è possibile configurare anche le seguenti impostazioni:

* percorso: Percorso dell&#39;archivio dati. Il valore predefinito è `<aem-install>/repository/datastore.`
* RecordLength: Dimensione minima di un oggetto che deve essere memorizzato nell&#39;archivio dati. Il valore predefinito è 16 KB.
* maxCachedBinarySize: I binari con dimensioni inferiori o uguali a queste dimensioni verranno memorizzati nella cache di memoria. La dimensione è espressa in byte. Il valore predefinito è 17408 (17 KB).
* cacheSize: Dimensione della cache. Il valore è specificato in byte. Il valore predefinito è 64 GB.
* segreto: Da utilizzare solo se si utilizza la replica binaryless per l&#39;impostazione di un archivio dati condiviso.
* stagingSplitPercentage: Percentuale di dimensioni della cache configurate da utilizzare per i caricamenti asincroni di staging. Il valore predefinito è 10.
* uploadThreads: Il numero di thread di caricamento utilizzati per i caricamenti asincroni. Il valore predefinito è 10.
* stagingPurgeInterval: Intervallo in secondi per lo svuotamento dei caricamenti completati dalla cache di staging. Il valore predefinito è 300 secondi (5 minuti).
* stagingRetryInterval: Intervallo dei tentativi in secondi per caricamenti non riusciti. Il valore predefinito è 600 secondi (10 minuti).

>[!NOTE]
>
>Tutte le impostazioni devono essere inserite tra virgolette, ad esempio:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Raccolta rifiuti dell&#39;archivio dati {#data-store-garbage-collection}

Il processo di raccolta degli oggetti inattivi dell&#39;archivio dati viene utilizzato per rimuovere tutti i file non utilizzati nell&#39;archivio dati, liberando così spazio prezioso sul disco nel processo.

Puoi eseguire la raccolta degli oggetti inattivi dell&#39;archivio dati:

1. Andando alla console JMX all&#39;indirizzo *https://&lt;serveraddress:port>/system/console/jmx*
1. Ricerca di **RepositoryManagement.** Una volta trovato il MBean di Repository Manager, fai clic su di esso per visualizzare le opzioni disponibili.
1. Scorri fino alla fine della pagina e fai clic sul collegamento **startDataStoreGC(boolean markOnly)** .
1. Nella finestra di dialogo seguente, immetti `false` per il parametro `markOnly`, quindi fai clic su **Invoke**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >Il parametro `markOnly` indica se la fase di sweep della raccolta degli oggetti inattivi verrà eseguita o meno.

## Raccolta rifiuti dell&#39;archivio dati per un archivio dati condiviso {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Quando si esegue la raccolta oggetti inattivi in una configurazione dell’archivio dati in cluster o condiviso (con Mongo o Segment Tar), il registro potrebbe visualizzare avvisi sull’impossibilità di eliminare determinati ID BLOB. Questo accade perché gli ID BLOB eliminati in una precedente raccolta oggetti inattivi vengono erroneamente referenziati da altri nodi cluster o condivisi che non hanno informazioni sulle eliminazioni degli ID. Di conseguenza, quando si esegue la raccolta oggetti inattivi, viene registrato un avviso quando si tenta di eliminare un ID già eliminato nell’ultima esecuzione. Questo comportamento non influisce sulle prestazioni o sulle funzionalità.

Con le versioni più recenti di AEM, la raccolta degli oggetti inattivi dell&#39;archivio dati può essere eseguita anche sugli archivi di dati condivisi da più di un archivio. Per poter eseguire la raccolta degli oggetti inattivi dell&#39;archivio dati in un archivio dati condiviso, procedi come segue:

1. Assicurati che tutte le attività di manutenzione configurate per la raccolta oggetti inattivi dell&#39;archivio dati siano disabilitate su tutte le istanze dell&#39;archivio che condividono l&#39;archivio dati.
1. Esegui i passaggi indicati in [Raccolta rifiuti binari](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) singolarmente su **tutte le istanze dell&#39;archivio** che condividono l&#39;archivio dati. Tuttavia, assicurati di inserire `true` per il parametro `markOnly` prima di fare clic sul pulsante Invoke :

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Dopo aver completato la procedura di cui sopra su tutte le istanze, esegui di nuovo la raccolta oggetti inattivi dell&#39;archivio dati da **any** delle istanze:

   1. Vai alla console JMX e seleziona il Mbean di Repository Manager.
   1. Fai clic sul collegamento **Click startDataStoreGC(boolean markOnly)** .
   1. Nella finestra di dialogo seguente, immetti di nuovo `false` per il parametro `markOnly` .

   In questo modo verranno raccolti tutti i file trovati utilizzando la fase di contrassegno utilizzata in precedenza ed eliminati gli altri file non utilizzati dall&#39;archivio dati.

