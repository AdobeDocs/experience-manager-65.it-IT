---
title: Elementi di storage in AEM 6.5
seo-title: Storage Elements in AEM 6.5
description: Scopri le implementazioni di archiviazione dei nodi disponibili in AEM 6.5 e come mantenere l’archivio.
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# Elementi di storage in AEM 6.5{#storage-elements-in-aem}

In questo articolo tratteremo:

* [Panoramica dello storage in AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Manutenzione dell’archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Panoramica dello storage in AEM 6 {#overview-of-storage-in-aem}

Una delle modifiche più importanti nel AEM 6 sono le innovazioni a livello di archivio.

Al momento sono disponibili due implementazioni di archiviazione nodi in AEM6: Archiviazione Tar e archiviazione MongoDB.

### Archiviazione Tar {#tar-storage}

#### Esecuzione di un&#39;istanza AEM appena installata con Tar Storage {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>Il PID per l’archivio dei nodi del segmento è cambiato da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService nelle versioni precedenti di AEM 6 su org.apache.jackrabbit.oak.segment.SegmentNodeStoreService in AEM 6.3. Assicurati di effettuare le regolazioni di configurazione necessarie per riflettere questa modifica.

Per impostazione predefinita, AEM 6 utilizza l’archiviazione Tar per memorizzare nodi e binari, utilizzando le opzioni di configurazione predefinite. Per configurare manualmente le impostazioni di archiviazione, segui la procedura seguente:

1. Scarica il jar AEM 6 quickstart e inseriscilo in una nuova cartella.
1. Scompattare AEM eseguendo:

   `java -jar cq-quickstart-6.jar -unpack`

1. Crea una cartella denominata `crx-quickstart\install` nella directory di installazione.

1. Crea un file denominato `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` nella cartella appena creata.

1. Modifica il file e imposta le opzioni di configurazione. Le seguenti opzioni sono disponibili per Segment Node Store, che è la base dell&#39;implementazione AEM archiviazione Tar:

   * `repository.home`: Percorso della home dell&#39;archivio in cui vengono archiviati vari dati relativi all&#39;archivio. Per impostazione predefinita, i file dei segmenti vengono memorizzati nella directory crx-quickstart/segmentstore .
   * `tarmk.size`: Dimensione massima di un segmento in MB. Il valore predefinito è 256 MB.

1. Inizia AEM.

### Archiviazione Mongo {#mongo-storage}

#### Esecuzione di un&#39;istanza AEM appena installata con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 può essere configurato per l&#39;esecuzione con l&#39;archiviazione MongoDB seguendo la procedura seguente:

1. Scarica il jar AEM 6 quickstart e inseriscilo in una nuova cartella.
1. Estrai AEM eseguendo il seguente comando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Assicurati che MongoDB sia installato e che sia presente un&#39;istanza di `mongod` è in esecuzione. Per ulteriori informazioni, consulta [Installazione di MongoDB](https://docs.mongodb.org/manual/installation/).
1. Crea una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configura l&#39;archivio nodi creando un file di configurazione con il nome della configurazione che desideri utilizzare nel `crx-quickstart\install` directory.

   Document Node Store (che è la base per AEM&#39;implementazione dell&#39;archiviazione MongoDB) utilizza un file chiamato `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Modifica il file e imposta le opzioni di configurazione. Sono disponibili le seguenti opzioni:

   * `mongouri`: La [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) richiesto per la connessione al database Mongo. Il valore predefinito è `mongodb://localhost:27017`
   * `db`: Nome del database Mongo. Per impostazione predefinita, le nuove installazioni AEM 6 utilizzano **autore di aem** come nome del database.
   * `cache`: Dimensione della cache in MB. Questa viene distribuita tra le varie cache utilizzate in DocumentNodeStore. Il valore predefinito è 256.
   * `changesSize`: Dimensioni in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output diff. Il valore predefinito è 256.
   * `customBlobStore`: Valore booleano che indica che verrà utilizzato un archivio dati personalizzato. Il valore predefinito è false.

1. Crea un file di configurazione con il PID dell’archivio dati che desideri utilizzare e modifica il file per impostare le opzioni di configurazione. Per ulteriori informazioni, consulta [Configurazione di archivi di nodi e archivi dati](/help/sites-deploying/data-store-config.md).

1. Avvia AEM 6 jar con un backend di archiviazione MongoDB eseguendo:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Dove **`-r`** è la modalità di esecuzione back-end. In questo esempio, inizierà con il supporto MongoDB.

#### Disabilitazione delle pagine grandi trasparenti {#disabling-transparent-huge-pages}

Red Hat Linux utilizza un algoritmo di gestione della memoria chiamato Transparent Huge Pages (THP). Mentre AEM le letture e le scritture a grana fine, THP è ottimizzato per le operazioni di grandi dimensioni. Per questo motivo, si consiglia di disabilitare THP sia su archiviazione Tar che Mongo. Per disabilitare l’algoritmo, effettua le seguenti operazioni:

1. Apri `/etc/grub.conf` nell’editor di testo desiderato.
1. Aggiungi la seguente riga al **grub.conf** file:

   ```
   transparent_hugepage=never
   ```

1. Infine, controlla se l&#39;impostazione è entrata in vigore eseguendo:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l&#39;output del comando precedente deve essere:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>È inoltre possibile consultare le seguenti risorse:
>
>* Per ulteriori informazioni su Transparent Huge Pages su Red Hat Linux, vedi questo [articolo](https://access.redhat.com/solutions/46111).
>* Per suggerimenti per l&#39;ottimizzazione di Linux, consulta questo [articolo](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>


## Manutenzione dell’archivio {#maintaining-the-repository}

Ogni aggiornamento del repository crea una nuova revisione del contenuto. Di conseguenza, con ogni aggiornamento le dimensioni dell&#39;archivio crescono. Per evitare una crescita incontrollata dell&#39;archivio, è necessario ripulire le vecchie revisioni per liberare le risorse del disco. Questa funzionalità di manutenzione è denominata Revision Cleanup (Pulizia delle revisioni). Il meccanismo Revision Cleanup recupererà lo spazio su disco rimuovendo i dati obsoleti dall&#39;archivio. Per ulteriori dettagli sul cleanup delle revisioni, leggere il [Pagina Pulizia revisioni](/help/sites-deploying/revision-cleanup.md).
