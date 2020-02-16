---
title: Elementi di archiviazione in AEM 6.5
seo-title: Elementi di archiviazione in AEM 6.5
description: Scopri le implementazioni per l’archiviazione nodi disponibili in AEM 6.5 e come mantenere l’archivio.
seo-description: Scopri le implementazioni per l’archiviazione nodi disponibili in AEM 6.5 e come mantenere l’archivio.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Elementi di archiviazione in AEM 6.5{#storage-elements-in-aem}

In questo articolo verranno trattati:

* [Panoramica sullo storage in AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Gestione del repository](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Panoramica sullo storage in AEM 6 {#overview-of-storage-in-aem}

Una delle modifiche più importanti in AEM 6 riguarda le innovazioni a livello di repository.

In AEM6 sono attualmente disponibili due implementazioni di storage a nodi: Archiviazione Tar e storage MongoDB.

### Archiviazione Tar {#tar-storage}

#### Esecuzione di un’istanza AEM appena installata con Tar Storage {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>Il PID per l&#39;archivio nodi Segmento è cambiato da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService nelle versioni precedenti di AEM 6 a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService in AEM 6.3. Accertatevi di apportare le modifiche necessarie alla configurazione per riflettere questa modifica.

Per impostazione predefinita, AEM 6 utilizza l’archiviazione Tar per memorizzare nodi e file binari, utilizzando le opzioni di configurazione predefinite. Per configurare manualmente le impostazioni di memorizzazione, attenersi alla procedura seguente:

1. Scaricate l’avvio rapido di AEM 6 e inseritelo in una nuova cartella.
1. Scomprimi AEM eseguendo:

   `java -jar cq-quickstart-6.jar -unpack`

1. Create una cartella denominata `crx-quickstart\install` nella directory di installazione.

1. Create un file chiamato `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` nella cartella appena creata.

1. Modificate il file e impostate le opzioni di configurazione. Le seguenti opzioni sono disponibili per Segment Node Store, che è la base dell’implementazione di AEM per l’archiviazione Tar:

   * `repository.home`: Percorso della home directory archivio in cui vengono memorizzati i vari dati relativi al repository. Per impostazione predefinita, i file dei segmenti vengono memorizzati nella directory crx-quickstart/segmentstore.
   * `tarmk.size`: Dimensione massima di un segmento in MB. Il valore predefinito è 256 MB.

1. Avviate AEM.

### Mongo Storage {#mongo-storage}

#### Esecuzione di un’istanza AEM appena installata con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 può essere configurato per l’esecuzione con l’archiviazione MongoDB seguendo la procedura seguente:

1. Scaricate l’avvio rapido di AEM 6 e inseritelo in una nuova cartella.
1. Scomprimi AEM eseguendo il comando seguente:

   `java -jar cq-quickstart-6.jar -unpack`

1. Accertatevi che MongoDB sia installato e che un&#39;istanza di `mongod` sia in esecuzione. Per ulteriori informazioni, vedere [Installazione di MongoDB](https://docs.mongodb.org/manual/installation/).
1. Create una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configurate l&#39;archivio nodi creando un file di configurazione con il nome della configurazione che desiderate utilizzare nella `crx-quickstart\install` directory.

   Document Node Store (che è la base per l&#39;implementazione dell&#39;archivio MongoDB di AEM) utilizza un file denominato `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Modificate il file e impostate le opzioni di configurazione. Sono disponibili le seguenti opzioni:

   * `mongouri`: Il [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) richiesto per connettersi al database Mongo. Il valore predefinito è `mongodb://localhost:27017`
   * `db`: Nome del database Mongo. Per impostazione predefinita, le nuove installazioni di AEM 6 utilizzano l’autore **** AEM come nome del database.
   * `cache`: Dimensione della cache in MB. Questo viene distribuito tra diverse cache utilizzate in DocumentNodeStore. Il valore predefinito è 256.
   * `changesSize`: Dimensioni in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output delle diff. Il valore predefinito è 256.
   * `customBlobStore`: Valore booleano che indica che verrà utilizzato un archivio dati personalizzato. Il valore predefinito è false.

1. Creare un file di configurazione con il PID dell&#39;archivio dati che si desidera utilizzare e modificare il file per impostare le opzioni di configurazione. Per ulteriori informazioni, consulta [Configurazione di archivi di nodi e archivi](/help/sites-deploying/data-store-config.md)dati.

1. Avviate il JAR di AEM 6 con un backend di archiviazione MongoDB eseguendo:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Dov&#39; **`-r`** è la modalità di esecuzione back-end. In questo esempio, inizierà con il supporto MongoDB.

#### Disattivazione di pagine grandi trasparenti {#disabling-transparent-huge-pages}

Red Hat Linux utilizza un algoritmo di gestione della memoria denominato Transparent Huge Pages (THP). Mentre AEM esegue letture e scrittura con granulosità ridotta, THP è ottimizzato per le operazioni di grandi dimensioni. Per questo motivo, si consiglia di disabilitare THP sia su storage Tar che Mongo. Per disattivare l’algoritmo, procedere come segue:

1. Aprite il `/etc/grub.conf` file nell’editor di testo desiderato.
1. Aggiungi la riga seguente al file **grub.conf** :

   ```
   transparent_hugepage=never
   ```

1. Infine, verificare se l&#39;impostazione ha avuto effetto eseguendo:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l&#39;output del comando precedente deve essere:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>È inoltre possibile consultare le risorse seguenti:
>
>* Per ulteriori informazioni sulle Pagine Enormi Trasparenti su Red Hat Linux, consulta questo [articolo](https://access.redhat.com/solutions/46111).
>* Per suggerimenti di ottimizzazione per Linux, consultate questo [articolo](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>



## Gestione del repository {#maintaining-the-repository}

Ogni aggiornamento al repository crea una nuova revisione del contenuto. Di conseguenza, con ogni aggiornamento le dimensioni del repository aumentano. Per evitare una crescita incontrollata del repository, le vecchie revisioni devono essere pulite per liberare risorse su disco. Questa funzionalità di manutenzione è denominata Revision Cleanup (Pulizia revisioni). Il meccanismo Revision Cleanup recupererà spazio su disco rimuovendo i dati obsoleti dall&#39;archivio. Per ulteriori dettagli sulla pulizia della revisione, consultate la pagina [Pulizia](/help/sites-deploying/revision-cleanup.md)revisione.
