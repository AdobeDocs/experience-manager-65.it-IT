---
title: Elementi di conservazione in AEM 6.5
description: Scopri le implementazioni di archiviazione dei nodi disponibili in AEM 6.5 e come gestire l’archivio.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Elementi di conservazione in AEM 6.5{#storage-elements-in-aem}

Il presente articolo riguarda:

* [Panoramica sulla conservazione nell’AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Gestione dell’archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Panoramica sulla conservazione nell’AEM 6 {#overview-of-storage-in-aem}

Una delle modifiche più importanti dell’AEM 6 sono le innovazioni a livello di deposito.

Attualmente, nell’AEM6 sono disponibili due implementazioni di storage dei nodi: storage Tar e storage MongoDB.

### Archiviazione Tar {#tar-storage}

#### Esecuzione di un’istanza AEM appena installata con archiviazione Tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>Il PID per l’archivio dei nodi di segmento è stato modificato da org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService nelle versioni precedenti di AEM 6 in org.apache.jackrabbit.oak.segment.SegmentNodeStoreService nell&#39;AEM 6.3. Assicurati che vengano apportate le necessarie regolazioni di configurazione in modo che le modifiche vengano applicate.

Per impostazione predefinita, AEM 6 utilizza l’archiviazione Tar per memorizzare nodi e binari, utilizzando le opzioni di configurazione predefinite. È possibile configurare manualmente le impostazioni di archiviazione eseguendo le operazioni seguenti:

1. Scarica il file jar quickstart di AEM 6 e inseriscilo in una nuova cartella.
1. Decomprimere l’AEM eseguendo:

   `java -jar cq-quickstart-6.jar -unpack`

1. Creare una cartella denominata `crx-quickstart\install` nella directory di installazione.

1. Creare un file denominato `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` nella cartella appena creata.

1. Modifica il file e imposta le opzioni di configurazione. Per Segment Node Store, che è la base dell’implementazione dell’archiviazione Tar dell’AEM, sono disponibili le seguenti opzioni:

   * `repository.home`: percorso della home del repository in cui vengono archiviati vari dati relativi al repository. Per impostazione predefinita, i file dei segmenti vengono memorizzati nella directory crx-quickstart/segmentstore.
   * `tarmk.size`: dimensione massima di un segmento in MB. Il valore predefinito è 256 MB.

1. Avvia AEM.

### Archiviazione Mongo {#mongo-storage}

#### Esecuzione di un’istanza AEM appena installata con Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

L’AEM 6 può essere configurato per funzionare con lo storage MongoDB seguendo la procedura seguente:

1. Scarica il file jar quickstart di AEM 6 e inseriscilo in una nuova cartella.
1. Decomprimi AEM eseguendo il comando seguente:

   `java -jar cq-quickstart-6.jar -unpack`

1. Verificare che MongoDB sia installato e che un&#39;istanza di `mongod` sia in esecuzione. Per ulteriori informazioni, vedere [Installazione di MongoDB](https://docs.mongodb.org/manual/installation/).
1. Creare una cartella denominata `crx-quickstart\install` nella directory di installazione.
1. Configurare l&#39;archivio nodi creando un file di configurazione con il nome della configurazione da utilizzare nella directory `crx-quickstart\install`.

   L&#39;archivio dei nodi dei documenti (che è la base per l&#39;implementazione dell&#39;archiviazione MongoDB dell&#39;AEM) utilizza un file denominato `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Modifica il file e imposta le opzioni di configurazione. Sono disponibili le seguenti opzioni:

   * `mongouri`: [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessario per connettersi al database Mongo. Il valore predefinito è `mongodb://localhost:27017`
   * `db`: nome del database Mongo. Per impostazione predefinita, le nuove installazioni di AEM 6 utilizzano **aem-author** come nome del database.
   * `cache`: dimensione della cache in megabyte. Questa dimensione della cache viene distribuita tra le varie cache utilizzate in DocumentNodeStore. Il valore predefinito è 256.
   * `changesSize`: dimensione in MB della raccolta limitata utilizzata in Mongo per memorizzare nella cache l&#39;output diff. Il valore predefinito è 256.
   * `customBlobStore`: valore booleano che indica l&#39;utilizzo di un archivio dati personalizzato. Il valore predefinito è false.

1. Crea un file di configurazione con il PID dell’archivio dati che desideri utilizzare e modifica il file per impostare le opzioni di configurazione. Per ulteriori informazioni, vedere [Configurazione degli archivi nodi e degli archivi dati](/help/sites-deploying/data-store-config.md).

1. Avvia il file jar dell’AEM 6 con un back-end di archiviazione MongoDB eseguendo:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Se la modalità di esecuzione del back-end è **`-r`**, l&#39;esempio inizia con il supporto MongoDB.

#### Disabilitazione delle pagine di grandi dimensioni trasparenti {#disabling-transparent-huge-pages}

Red Hat® Linux® utilizza un algoritmo di gestione della memoria chiamato Transparent Huge Pages (THP). Mentre l&#39;AEM esegue operazioni di lettura e scrittura dettagliate, il THP è ottimizzato per operazioni di grandi dimensioni. Pertanto, si consiglia di disabilitare THP sia nella memoria di Tar che in quella di Mongo. Per disattivare l’algoritmo, effettua le seguenti operazioni:

1. Aprire il file `/etc/grub.conf` nell&#39;editor di testo desiderato.
1. Aggiungi la seguente riga al file **grub.conf**:

   ```
   transparent_hugepage=never
   ```

1. Infine, verifica se l’impostazione è diventata effettiva eseguendo:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP è disattivato, l’output del comando precedente deve essere:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Consulta le seguenti risorse:
>
>* Per ulteriori informazioni su Transparent Huge Pages su Red Hat® Linux®, consultare il seguente articolo dal portale clienti Red Hat®: [Come utilizzare, monitorare e disabilitare gli hugepage trasparenti in Red Hat Enterprise Linux 6,7 e 8?](https://access.redhat.com/solutions/46111)
>* Per suggerimenti per l&#39;ottimizzazione di Linux®, vedere [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md).
>

## Gestione dell’archivio {#maintaining-the-repository}

Ogni aggiornamento del repository crea una revisione del contenuto. Di conseguenza, con ogni aggiornamento aumenta la dimensione dell’archivio. Per evitare una crescita incontrollata dell&#39;archivio, è necessario ripulire le vecchie revisioni per liberare le risorse su disco. Questa funzionalità di manutenzione è denominata Pulizia revisioni. Il meccanismo di pulizia delle revisioni recupera spazio su disco rimuovendo i dati obsoleti dall&#39;archivio. Per ulteriori dettagli sulla pulizia delle revisioni, leggere la [pagina pulizia revisioni](/help/sites-deploying/revision-cleanup.md).
