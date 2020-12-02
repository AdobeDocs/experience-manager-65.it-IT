---
title: Configurazione di archivi di nodi e archivi di dati in AEM 6
seo-title: Configurazione di archivi di nodi e archivi di dati in AEM 6
description: Scopri come configurare archivi di nodi e archivi di dati e come eseguire la raccolta di oggetti per l'archivio dati.
seo-description: Scopri come configurare archivi di nodi e archivi di dati e come eseguire la raccolta di oggetti per l'archivio dati.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: 93cb84763cfd77b67a5dd1481caab79337f6e7c4
workflow-type: tm+mt
source-wordcount: '3423'
ht-degree: 1%

---


# Configurazione di archivi di nodi e archivi di dati in AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introduzione {#introduction}

In Adobe Experience Manager (AEM), i dati binari possono essere memorizzati indipendentemente dai nodi di contenuto. I dati binari sono memorizzati in un archivio dati, mentre i nodi di contenuto sono memorizzati in un archivio nodi.

Entrambi gli archivi di dati e gli archivi di nodi possono essere configurati utilizzando la configurazione OSGi. A ogni configurazione OSGi viene fatto riferimento tramite un identificatore permanente (PID).

## Passaggi di configurazione {#configuration-steps}

Per configurare sia l&#39;archivio nodi che l&#39;archivio dati, procedere come segue:

1. Copiate il file JAR AEM QuickStart nella directory di installazione.
1. Create una cartella `crx-quickstart/install` nella directory di installazione.
1. Innanzitutto, configurate l&#39;archivio nodi creando un file di configurazione con il nome dell&#39;opzione dell&#39;archivio nodi da utilizzare nella directory `crx-quickstart/install`.

   Ad esempio, l&#39;archivio dei nodi Documento (che è la base per AEM&#39;implementazione MongoMK) utilizza il file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Modificate il file e impostate le opzioni di configurazione.
1. Creare un file di configurazione con il PID dell&#39;archivio dati che si desidera utilizzare. Modificate il file per impostare le opzioni di configurazione.

   >[!NOTE]
   >
   >Per le opzioni di configurazione, vedere [Configurazioni archivio nodi](#node-store-configurations) e [Configurazioni archivio dati](#data-store-configurations).

1. Inizia AEM.

## Configurazioni archivio nodi {#node-store-configurations}

>[!CAUTION]
>
>Le versioni più recenti di Oak utilizzano un nuovo schema di denominazione e un nuovo formato per i file di configurazione OSGi. Il nuovo schema di denominazione richiede che il file di configurazione sia denominato **.config** e che il nuovo formato richieda la digitazione di valori ed è [documentato qui](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Se esegui l&#39;aggiornamento da una versione precedente di Oak, accertati di eseguire prima un backup della cartella `crx-quickstart/install`. Dopo l&#39;aggiornamento, ripristinare il contenuto della cartella all&#39;installazione aggiornata e modificare l&#39;estensione dei file di configurazione da **.cfg** a **.config**.
>
>Se state leggendo questo articolo in preparazione di un aggiornamento da un&#39;installazione **AEM 5.x**, accertatevi di consultare prima la documentazione [upgrade](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html).

### Archivio nodi segmento {#segment-node-store}

L&#39;archivio dei nodi del segmento è la base &#39;implementazione  TarMK di Adobe in AEM6. Utilizza il PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` per la configurazione.

>[!CAUTION]
>
>Il PID per l&#39;archivio dei nodi del segmento è cambiato da `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` di AEM 6 a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` in AEM 6.3. Accertatevi di apportare le modifiche necessarie alla configurazione per riflettere questa modifica.

Potete configurare le seguenti opzioni:

* `repository.home`: Percorso della home directory archivio in cui vengono memorizzati i dati relativi all&#39;archivio. Per impostazione predefinita, i file dei segmenti sono memorizzati nella directory `crx-quickstart/segmentstore`.

* `tarmk.size`: Dimensione massima di un segmento in MB. Il valore massimo predefinito è 256 MB.
* `customBlobStore`: Valore booleano che indica l&#39;utilizzo di un archivio dati personalizzato. Il valore predefinito è true per AEM 6.3 e versioni successive. Prima di AEM 6.3 il valore predefinito era false.

Esempio di file `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Archivio nodi del documento {#document-node-store}

L&#39;archivio dei nodi del documento è alla base dell&#39;implementazione AEM MongoMK. Utilizza il `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Sono disponibili le seguenti opzioni di configurazione:

* `mongouri`: Il  [](https://docs.mongodb.org/manual/reference/connection-string/) MongoURI richiesto per connettersi al database Mongo. Il valore predefinito è `mongodb://localhost:27017`

* `db`: Nome del database Mongo. Il valore predefinito è **Oak** ``. However, new AEM 6 installations use **aem-author** ``come nome predefinito del database.

* `cache`: Dimensione della cache in MB. Questo viene distribuito tra diverse cache utilizzate in DocumentNodeStore. Il valore predefinito è `256`

* `changesSize`: Dimensioni in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output delle diff. Il valore predefinito è `256`

* `customBlobStore`: Valore booleano che indica che verrà utilizzato un archivio dati personalizzato. Il valore predefinito è `false`.

Esempio di file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurazioni archivio dati {#data-store-configurations}

Per gestire un numero elevato di file binari, si consiglia di utilizzare un archivio dati esterno al posto degli archivi di nodi predefiniti, al fine di massimizzare le prestazioni.

Ad esempio, se il progetto richiede un numero elevato di risorse multimediali, memorizzarle nel file o nell&#39;archivio dati S3 consente di accedervi più rapidamente che archiviarle direttamente all&#39;interno di un MongoDB.

File Data Store offre prestazioni migliori rispetto a MongoDB, e le operazioni di backup e ripristino di Mongo sono anche più lente con un gran numero di risorse.

Di seguito sono descritti i dettagli relativi ai diversi data store e configurazioni.

>[!NOTE]
>
>Per abilitare gli archivi dati personalizzati, è necessario assicurarsi che `customBlobStore` sia impostato su `true` nel rispettivo file di configurazione Node Store ([store nodo di segmento](/help/sites-deploying/data-store-config.md#segment-node-store) o [document node store](/help/sites-deploying/data-store-config.md#document-node-store)).

### Archivio file di dati {#file-data-store}

Questa è l&#39;implementazione di [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) presente in Jackrabbit 2. Fornisce un modo per memorizzare i dati binari come file normali sul file system. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Sono disponibili le seguenti opzioni di configurazione:

* `repository.home`: Percorso della home directory archivio in cui vengono memorizzati i vari dati relativi al repository. Per impostazione predefinita, i file binari vengono memorizzati nella directory `crx-quickstart/repository/datastore`

* `path`: Percorso della directory in cui vengono memorizzati i file. Se specificato, ha precedenza rispetto al valore `repository.home`

* `minRecordLength`: La dimensione minima in byte di un file memorizzato nell&#39;archivio dati. Il contenuto binario inferiore a questo valore viene allineato.

>[!NOTE]
>
>Quando si utilizza un NAS per memorizzare gli archivi di dati dei file condivisi, assicurarsi di utilizzare solo dispositivi con prestazioni elevate per evitare problemi di prestazioni.

##  archivio dati Amazon S3 {#amazon-s-data-store}

AEM può essere configurato per memorizzare i dati in  Amazon Simple Storage Service (S3). Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` per la configurazione.

Per abilitare la funzionalità dell&#39;archivio dati S3, è necessario scaricare e installare un feature pack contenente il connettore S3 Datastore. Accedete al [ Repository di Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) e scaricate l&#39;ultima versione dalle versioni 1.10.x del feature pack (ad esempio, com.adobe.granite.oak.s3Connector-1.10.0.zip). Inoltre, è necessario scaricare e installare l&#39;ultimo service pack AEM come elencato nella pagina [AEM 6.5 Release Notes](/help/release-notes/sp-release-notes.md).

>[!NOTE]
>
>Se si utilizza AEM con TarMK, per impostazione predefinita i file binari vengono memorizzati in `FileDataStore`. Per utilizzare TarMK con il datastore S3, è necessario avviare AEM utilizzando la modalità di esecuzione `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, è possibile installare e configurare il connettore S3 come segue:

1. Estrarre il contenuto del file zip del pacchetto di funzioni in una cartella temporanea.

1. Passate alla cartella temporanea e individuate il percorso seguente:

   ```xml
   jcr_root/libs/system/install
   ```

   Copiate tutti i contenuti dalla posizione sopra indicata in `<aem-install>/crx-quickstart/install.`

1. Se AEM è già configurato per lavorare con l&#39;archivio Tar o MongoDB, rimuovere eventuali file di configurazione esistenti dalla cartella ***&lt;aem-install>***/*crx-quickstart*/*install* prima di continuare. I file da rimuovere sono:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Tornate nella posizione temporanea in cui è stato estratto il pacchetto di funzioni e copiate il contenuto della cartella seguente:

   * `jcr_root/libs/system/config`

   a

   * `<aem-install>/crx-quickstart/install`

   Accertatevi di copiare solo i file di configurazione richiesti dalla configurazione corrente. Per un archivio dati dedicato e una configurazione dell&#39;archivio dati condivisa, copiare il file `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >In una configurazione cluster, eseguite i passaggi sopra descritti su tutti i nodi del cluster uno per uno. Inoltre, accertatevi di utilizzare le stesse impostazioni S3 per tutti i nodi.

1. Modificate il file e aggiungete le opzioni di configurazione richieste dalla configurazione.
1. Inizia AEM.

### Aggiornamento a una nuova versione del connettore S3 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Per effettuare l&#39;aggiornamento a una nuova versione del connettore S3 1.10.x (ad esempio, da 1.10.0 a 1.10.4), procedere come segue:

1. Arrestate l&#39;istanza AEM.

1. Andate a `<aem-install>/crx-quickstart/install/15` nella cartella di installazione AEM ed effettuate un backup del relativo contenuto.
1. Dopo il backup, eliminare la vecchia versione del S3 Connector e le sue dipendenze eliminando tutti i file jar nella cartella `<aem-install>/crx-quickstart/install/15`, ad esempio:

   * **quercia-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >I nomi di file riportati sopra sono utilizzati solo a scopo illustrativo.

1. Scaricate l&#39;ultima versione del pacchetto di funzioni 1.8.x dal [ repository di Adobi](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Decomprimete il contenuto in una cartella separata, quindi andate a `jcr_root/libs/system/install/15`.
1. Copiate i file jar in **&lt;aem-install>**/crx-quickstart/install/15 nella cartella di installazione AEM.
1. Avviare AEM e controllare la funzionalità del connettore.

Potete utilizzare il file di configurazione con le seguenti opzioni:

* accessKey: La chiave di accesso AWS.
* secretKey: La chiave di accesso segreta AWS. **Nota:** in alternativa, per l&#39;autenticazione è possibile utilizzare i  [roletti ](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) IAM. Se si utilizzano i ruoli IAM, non è più necessario specificare `accessKey` e `secretKey`.

* s3Bucket: Il nome del bucket.
* s3Region: La regione del bucket.
* percorso: Percorso dell&#39;archivio dati. Il valore predefinito è **&lt;AEM cartella di installazione>/repository/datastore**
* minRecordLength: La dimensione minima di un oggetto che deve essere memorizzato nell&#39;archivio dati. Il valore minimo/predefinito è **16 KB.**
* maxCachedBinarySize: I file binari con dimensioni inferiori o uguali a queste dimensioni verranno memorizzati nella cache della memoria. La dimensione è espressa in byte. Il valore predefinito è **17408 **(17 KB).

* cacheSize: Dimensione della cache. Il valore è specificato in byte. Il valore predefinito è **64 GB**.
* secret: Da utilizzare solo se si utilizza la replica binaryless per l&#39;impostazione del datastore condiviso.
* stagingSplitPercentage: Percentuale della dimensione della cache configurata per l&#39;esecuzione di operazioni di caricamento asincrone. Il valore predefinito è **10**.
* uploadThread: Numero di thread di caricamento utilizzati per i caricamenti asincroni. Il valore predefinito è **10**.
* stagingPurgeInterval: L&#39;intervallo in secondi per l&#39;eliminazione dei caricamenti completati dalla cache di staging. Il valore predefinito è **300** secondi (5 minuti).
* stagingRetryInterval: L&#39;intervallo di tentativi in secondi per i caricamenti non riusciti. Il valore predefinito è **600** secondi (10 minuti).

### Opzioni regione intervalli {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>Standard USA</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>Stati Uniti</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (California del Nord)</td>
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

**Memorizzazione nella cache di DataStore**

>[!NOTE]
>
>Le implementazioni DataStore di `S3DataStore`, `CachingFileDataStore` e `AzureDataStore` supportano il caching dei file system locali. L&#39;implementazione `CachingFileDataStore` è utile quando DataStore è su NFS (Network File System).


Quando si esegue l&#39;aggiornamento da una precedente implementazione della cache (prima di Oak 1.6), si verifica una differenza nella struttura della directory della cache del file system locale. Nella vecchia struttura della cache, sia i file scaricati che quelli caricati venivano inseriti direttamente nel percorso della cache. La nuova struttura separa i download e i caricamenti e li memorizza in due directory denominate `upload` e `download` nel percorso della cache. Il processo di aggiornamento dovrebbe essere senza soluzione di continuità e tutti i caricamenti in sospeso dovrebbero essere pianificati per il caricamento e tutti i file scaricati in precedenza nella cache verranno inseriti nella cache al momento dell&#39;inizializzazione.

È inoltre possibile aggiornare la cache offline utilizzando il comando `datastorecacheupgrade` di esecuzione della quercia. Per informazioni dettagliate su come eseguire il comando, controllare il [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) per il modulo di esecuzione della quercia.

La cache ha un limite di dimensione e può essere configurata utilizzando il parametro cacheSize.

**Download**

La cache locale verrà controllata per verificare il record del file/BLOB richiesto prima di accedervi da DataStore. Quando la cache supera il limite configurato (vedere il parametro `cacheSize`) durante l&#39;aggiunta di un file nella cache, alcuni dei file verranno rimossi per recuperare spazio.

**Caricamento asincrono**

La cache supporta i caricamenti asincroni in DataStore. I file vengono memorizzati localmente, nella cache (del file system), e un processo asincrono inizia a caricare il file. Il numero di caricamenti asincroni è limitato dalla dimensione della cache di staging. La dimensione della cache di staging è configurata utilizzando il parametro `stagingSplitPercentage`. Questo parametro definisce la percentuale di dimensione della cache da utilizzare per la cache di staging. Inoltre, la percentuale di cache disponibile per i download è calcolata come **(100 - `stagingSplitPercentage`) *`cacheSize`**.

I caricamenti asincroni sono multithread e il numero di thread è configurato utilizzando il parametro `uploadThreads`.

Al termine dei caricamenti, i file vengono spostati nella cache di download principale. Quando la dimensione della cache di staging supera il limite, i file vengono caricati in modo sincrono in DataStore fino al completamento dei precedenti caricamenti asincroni e allo spazio disponibile nuovamente nella cache di staging. I file caricati vengono rimossi dall&#39;area di gestione temporanea tramite un processo periodico il cui intervallo è configurato dal parametro `stagingPurgeInterval`.

I caricamenti non riusciti (ad esempio a causa di un&#39;interruzione di rete) vengono messi in coda e riprovati periodicamente. L&#39;intervallo dei tentativi è configurato utilizzando il parametro `stagingRetryInterval parameter`.

#### Configurazione della replica binaryless con  Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Per configurare la replica binaryless con S3, sono necessari i seguenti passaggi:

1. Installate le istanze di creazione e pubblicazione e accertatevi che siano avviate correttamente.
1. Passate alle impostazioni dell&#39;agente di replica, aprendo una pagina su *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Premere il tasto **Edit** nella sezione **Settings**.
1. Cambia l&#39;opzione di tipo **Serialization** in **Binary less**.

1. Aggiungete il parametro &quot; `binaryless`= `true`&quot; nell&#39;uri di trasporto. Dopo la modifica, l&#39;URI deve essere simile al seguente:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Riavviate tutte le istanze di creazione e pubblicazione per rendere effettive le modifiche.

#### Creazione di un cluster con S3 e MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Scomprimete CQ QuickStart con il seguente comando:

   `java -jar cq-quickstart.jar -unpack`

1. Dopo aver decompresso AEM, create una cartella all&#39;interno della directory di installazione *crx-quickstart*/*install*.

1. Create questi due file all&#39;interno della cartella `crx-quickstart`:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Dopo aver creato i file, aggiungete le opzioni di configurazione necessarie.

1. Installare i due pacchetti richiesti per l&#39;archivio dati S3 come descritto sopra.
1. Assicurarsi che MongoDB sia installato e che sia in esecuzione un&#39;istanza di `mongod`.
1. Iniziate AEM con il seguente comando:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Ripetere i passaggi da 1 a 4 per la seconda istanza AEM.
1. Avviate la seconda istanza AEM.

#### Configurazione di un archivio dati condiviso {#configuring-a-shared-data-store}

1. Innanzitutto, creare il file di configurazione dell&#39;archivio dati su ogni istanza necessaria per condividere l&#39;archivio dati:

   * Se si utilizza un file `FileDataStore`, creare un file denominato `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e inserirlo nella cartella `<aem-install>/crx-quickstart/install`.

   * Se si utilizza S3 come archivio dati, creare un file denominato o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` nella cartella `<aem-install>/crx-quickstart/install` come sopra.

1. Modificare i file di configurazione dell&#39;archivio dati in ogni istanza in modo che puntino allo stesso archivio dati. Per ulteriori informazioni, vedere [questo articolo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Se l&#39;istanza è stata duplicata da un server esistente, è necessario rimuovere la `clusterId` della nuova istanza utilizzando lo strumento di esecuzione della quercia più recente mentre il repository è offline. Il comando da eseguire è:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Se è configurato un archivio nodi Segmento, è necessario specificare il percorso del repository. Per impostazione predefinita, il percorso è `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Se è configurato un archivio nodi documento, è possibile utilizzare un URI [Stringa di connessione Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Lo strumento di esecuzione Oak può essere scaricato da questo percorso:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >È necessario utilizzare diverse versioni dello strumento a seconda della versione Oak utilizzata con l&#39;installazione AEM. Prima di utilizzare lo strumento, controllare l&#39;elenco dei requisiti di versione riportato di seguito:
   >
   >
   >
   >    * Per le versioni di Oak **1.2.x** utilizzare il sistema di esecuzione Oak **1.2.12 o successivo**
   >    * Per le versioni di Oak **più recenti rispetto a quanto indicato sopra**, utilizzare la versione di esecuzione Oak che corrisponde al nucleo Oak dell&#39;installazione AEM.


1. Infine, convalidare la configurazione. A questo scopo, è necessario cercare un file univoco aggiunto all&#39;archivio dati da ogni repository che lo condivide. Il formato dei file è `repository-[UUID]`, dove l&#39;UUID è un identificatore univoco di ciascun repository.

   Di conseguenza, una configurazione corretta deve contenere tutti i file univoci presenti nei repository che condividono l&#39;archivio dati.

   I file vengono memorizzati in modo diverso, a seconda dell&#39;archivio dati:

   * Per `FileDataStore` i file vengono creati nel percorso principale della cartella dell&#39;archivio dati.
   * Per `S3DataStore` i file vengono creati nel bucket S3 configurato sotto la cartella `META`.

## Archivio dati Azure {#azure-data-store}

AEM è possibile configurare per la memorizzazione dei dati nel servizio di archiviazione di Microsoft Azure. Utilizza il PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` per la configurazione.

Per abilitare la funzionalità dell&#39;archivio dati di Azure, è necessario scaricare e installare un feature pack contenente il connettore di Azure. Accedete al [ Repository di Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) e scaricate l&#39;ultima versione dalle versioni 1.6.x del feature pack (ad esempio, com.adobe.granite.oak.azureblobConnector-1.6.3.zip).

>[!NOTE]
>
>Se si utilizza AEM con TarMK, per impostazione predefinita i file binari vengono memorizzati in FileDataStore. Per utilizzare TarMK con Azure DataStore, è necessario avviare AEM utilizzando la modalità di esecuzione `crx3tar-nofds`, ad esempio:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Una volta scaricato, è possibile installare e configurare il connettore Azure come segue:

1. Estrarre il contenuto del file zip del pacchetto di funzioni in una cartella temporanea.

1. Andate nella cartella temporanea e copiate il contenuto di `jcr_root/libs/system/install` nella cartella `<aem-install>crx-quickstart/install`.
1. Se AEM è già configurato per lavorare con l&#39;archivio Tar o MongoDB, rimuovere eventuali file di configurazione esistenti dalla cartella `/crx-quickstart/install` prima di continuare. I file da rimuovere sono:

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Per TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Tornate alla posizione temporanea in cui è stato estratto il pacchetto di funzioni e copiate il contenuto di `jcr_root/libs/system/config` nella cartella `<aem-install>/crx-quickstart/install`.
1. Modificate il file di configurazione e aggiungete le opzioni di configurazione richieste dalla configurazione.
1. Inizia AEM.

Potete utilizzare il file di configurazione con le seguenti opzioni:

* azureSas=&quot;&quot;: Nella versione 1.6.3 del connettore, è stato aggiunto il supporto SAS (Shared Access Signature) di Azure. **Se nel file di configurazione sono presenti sia le credenziali SAS che quelle di archiviazione, SAS ha priorità.** Per ulteriori informazioni su SAS vedere la documentazione [ ](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)ufficiale. Assicurarsi che il carattere &#39;=&#39; sia preceduto da un carattere con carattere di escape come &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: Endpoint BLOB di Azure. Ad esempio, https://&lt;account-archivio>.blob.core.windows.net.
* accessKey=&quot;&quot;: Nome account di archiviazione. Per ulteriori informazioni sulle credenziali di autenticazione di Microsoft Azure, vedere la [documentazione ufficiale](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;&quot;: La chiave di accesso allo storage. Assicurarsi che il carattere &#39;=&#39; sia preceduto da un carattere con carattere di escape come &#39;\=&#39;.
* container=&quot;&quot;: Nome del contenitore di archiviazione BLOB di Microsoft Azure. Il contenitore è un raggruppamento di un set di BLOB. Per ulteriori informazioni, consultare la [documentazione ufficiale](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;: Numero simultaneo di richieste simultanee per operazione. Il valore predefinito è 1.
* maxErrorRetry=&quot;&quot;: Numero di tentativi per richiesta. Il valore predefinito è 3.
* socketTimeout=&quot;&quot;: Intervallo di timeout, in millisecondi, utilizzato per la richiesta. Il valore predefinito è 5 minuti.

Oltre alle impostazioni precedenti, è possibile configurare anche le seguenti impostazioni:

* percorso: Percorso dell&#39;archivio dati. Il valore predefinito è `<aem-install>/repository/datastore.`
* LunghezzaRecord: La dimensione minima di un oggetto che deve essere memorizzato nell&#39;archivio dati. Il valore predefinito è 16 KB.
* maxCachedBinarySize: I file binari con dimensioni inferiori o uguali a queste dimensioni verranno memorizzati nella cache della memoria. La dimensione è espressa in byte. Il valore predefinito è 17408 (17 KB).
* cacheSize: Dimensione della cache. Il valore è specificato in byte. Il valore predefinito è 64 GB.
* secret: Da utilizzare solo se si utilizza la replica binaryless per l&#39;impostazione del datastore condiviso.
* stagingSplitPercentage: Percentuale della dimensione della cache configurata per l&#39;esecuzione di operazioni di caricamento asincrone. Il valore predefinito è 10.
* uploadThread: Numero di thread di caricamento utilizzati per i caricamenti asincroni. Il valore predefinito è 10.
* stagingPurgeInterval: L&#39;intervallo in secondi per l&#39;eliminazione dei caricamenti completati dalla cache di staging. Il valore predefinito è 300 secondi (5 minuti).
* stagingRetryInterval: L&#39;intervallo di tentativi in secondi per i caricamenti non riusciti. Il valore predefinito è 600 secondi (10 minuti).

>[!NOTE]
>
>Tutte le impostazioni devono essere inserite tra virgolette, ad esempio:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Raccolta rifiuti archivio dati {#data-store-garbage-collection}

Il processo di raccolta dei rifiuti dell&#39;archivio dati viene utilizzato per rimuovere eventuali file non utilizzati nell&#39;archivio dati, liberando così spazio prezioso su disco nel processo.

È possibile eseguire la raccolta dei rifiuti dell&#39;archivio dati tramite:

1. Passate alla console JMX che si trova in *https://&lt;serveraddress:port>/system/console/jmx*
1. Ricerca di **RepositoryManagement.** Una volta trovato il file MBean di Repository Manager, fare clic su di esso per visualizzare le opzioni disponibili.
1. Scorrete fino alla fine della pagina e fate clic sul collegamento **startDataStoreGC(boolean markOnly)**.
1. Nella finestra di dialogo seguente, immettere `false` per il parametro `markOnly`, quindi fare clic su **Invoke**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >Il parametro `markOnly` indica se la fase di sweep del processo di garbage collection verrà eseguita o meno.

## Raccolta di oggetti indesiderati nell&#39;archivio dati per un archivio dati condiviso {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Durante l&#39;esecuzione della raccolta dei dati in un&#39;impostazione dell&#39;archivio dati cluster o condiviso (con Mongo o Segment Tar), il registro potrebbe visualizzare avvisi sull&#39;impossibilità di eliminare alcuni ID BLOB. Ciò accade perché gli ID BLOB eliminati in una precedente raccolta di oggetti inattivi sono erroneamente citati da altri nodi cluster o condivisi che non dispongono di informazioni sulle eliminazioni ID. Di conseguenza, quando viene eseguita la raccolta di oggetti inattivi, viene registrato un avviso quando si tenta di eliminare un ID già eliminato nell&#39;ultima esecuzione. Questo comportamento non influisce sulle prestazioni o sulle funzionalità.

Con le versioni più recenti di AEM, è possibile eseguire la raccolta dei rifiuti dell&#39;archivio dati anche in archivi dati condivisi da più repository. Per poter eseguire la raccolta dei rifiuti dell&#39;archivio dati in un archivio dati condiviso, effettuare le seguenti operazioni:

1. Assicurarsi che tutte le attività di manutenzione configurate per la raccolta dei rifiuti dell&#39;archivio dati siano disattivate in tutte le istanze dell&#39;archivio che condividono l&#39;archivio dati.
1. Eseguire i passaggi indicati in [Binary Garbage Collection](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) singolarmente su **tutte le istanze del repository** che condividono l&#39;archivio dati. Tuttavia, prima di fare clic sul pulsante Richiama, assicurarsi di inserire `true` per il parametro `markOnly`:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Dopo aver completato la procedura sopra riportata su tutte le istanze, eseguire di nuovo il processo di garbage collection dell&#39;archivio dati da **qualsiasi** delle istanze:

   1. Accedete alla console JMX e selezionate Repository Manager Mbay.
   1. Fare clic sul collegamento **Click startDataStoreGC(boolean markOnly)**.
   1. Nella finestra di dialogo seguente, immettere di nuovo `false` per il parametro `markOnly`.

   In questo modo verranno raccolti tutti i file trovati utilizzando la fase di contrassegno utilizzata in precedenza ed eliminati gli altri file non utilizzati dall&#39;archivio dati.

