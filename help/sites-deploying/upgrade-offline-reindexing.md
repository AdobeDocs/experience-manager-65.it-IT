---
title: Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento
description: Scopri come utilizzare la metodologia di reindicizzazione offline per ridurre i tempi di inattività del sistema durante l’esecuzione di un aggiornamento dell’AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introduzione {#introduction}

Una delle problematiche principali nell’aggiornamento di Adobe Experience Manager è il tempo di inattività associato all’ambiente di authoring quando viene eseguito un aggiornamento sul posto. Gli autori dei contenuti non potranno accedere all’ambiente durante un aggiornamento. È pertanto consigliabile ridurre al minimo il tempo necessario per eseguire l&#39;aggiornamento. Per gli archivi di grandi dimensioni, in particolare i progetti AEM Assets, che in genere hanno archivi di dati di grandi dimensioni e un elevato livello di caricamenti di risorse all’ora, la reindicizzazione degli indici Oak richiede una percentuale significativa del tempo di aggiornamento.

Questa sezione descrive come utilizzare lo strumento Oak-run per reindicizzare l&#39;archivio **prima** di eseguire l&#39;aggiornamento, riducendo in tal modo il tempo di inattività durante l&#39;aggiornamento effettivo. I passaggi presentati possono essere applicati agli indici [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) per le versioni AEM 6.4 e successive.

## Panoramica {#overview}

Le nuove versioni dell’AEM introducono modifiche alle definizioni dell’indice Oak man mano che il set di funzioni viene espanso. Le modifiche agli indici Oak forzano la reindicizzazione durante l’aggiornamento dell’istanza AEM. La reindicizzazione è costosa per le distribuzioni delle risorse in quanto il testo nelle risorse (ad esempio, il testo nel file PDF) viene estratto e indicizzato. Con gli archivi MongoMK, i dati vengono mantenuti sulla rete, aumentando ulteriormente il tempo necessario per la reindicizzazione.

Il problema che la maggior parte dei clienti si trova ad affrontare durante un aggiornamento è la riduzione della finestra di inattività. La soluzione consiste nel **saltare** l&#39;attività di reindicizzazione durante l&#39;aggiornamento. A tale scopo, crea i nuovi indici **prior** per eseguire l&#39;aggiornamento e importali semplicemente durante l&#39;aggiornamento.

## Approccio {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

L&#39;idea è quella di creare l&#39;indice prima dell&#39;aggiornamento, rispetto alle definizioni dell&#39;indice della versione AEM di destinazione utilizzando lo strumento [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). Il diagramma precedente mostra l’approccio alla reindicizzazione offline.

Inoltre, questo è l’ordine delle fasi descritto nell’approccio:

1. Il testo dai file binari viene estratto per primo
2. Vengono create le definizioni dell’indice di destinazione
3. Vengono creati indici offline
4. Gli indici vengono quindi importati durante il processo di aggiornamento

### Estrazione testo {#text-extraction}

Per abilitare l’indicizzazione completa in AEM, il testo da file binari come PDF viene estratto e aggiunto all’indice. In genere si tratta di un passaggio costoso nel processo di indicizzazione. L’estrazione del testo è un passaggio di ottimizzazione consigliato soprattutto per la reindicizzazione degli archivi di risorse in quanto archiviano un numero elevato di dati binari.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

Il testo dei file binari memorizzati nel sistema può essere estratto utilizzando lo strumento oak-run con la libreria tika. Un clone dei sistemi di produzione può essere acquisito prima dell’aggiornamento e utilizzato per questo processo di estrazione del testo. Questo processo crea quindi l’archivio di testo seguendo i passaggi seguenti:

**1. Attraversa l&#39;archivio e raccogli i dettagli dei file binari**

Questo passaggio genera un file CSV contenente una tupla di file binari, un percorso e un ID BLOB.

Esegui il comando seguente dalla directory da cui desideri creare l’indice. L’esempio seguente presuppone la home directory del repository.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Dove `nodestore path` è `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilizza il parametro `--fake-ds-path=temp` invece di `–fds-path` per velocizzare il processo.

**2. Riutilizzare l&#39;archivio di testo binario disponibile nell&#39;indice esistente**

Scaricare i dati di indice dal sistema esistente ed estrarre l&#39;archivio di testo.

Puoi scaricare i dati di indice esistenti utilizzando il seguente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Dove `nodestore path` è `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Quindi, utilizza l’immagine indice precedente per popolare l’archivio:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Dove `oak-index-name` è il nome dell&#39;indice full-text, ad esempio &quot;lucene&quot;.

**3. Esegui il processo di estrazione del testo utilizzando la libreria tika per i file binari non elaborati nel passaggio precedente**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Dove `datastore path` è il percorso dell&#39;archivio dati binario.

L’archivio di testo creato può essere aggiornato e riutilizzato per scenari futuri di reindicizzazione.

Per ulteriori dettagli sul processo di estrazione del testo, consulta la [documentazione eseguita da Oak](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindicizzazione offline {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Crea l’indice Lucene offline prima dell’aggiornamento. Se utilizzi MongoMK, si consiglia di eseguirlo direttamente su uno dei nodi MongoMk, in quanto questo evita il sovraccarico della rete.

Per creare l’indice offline, effettua le seguenti operazioni:

**1. Genera le definizioni dell&#39;indice Oak Lucene per la versione dell&#39;AEM di destinazione**

Effettua il dump delle definizioni di indice esistenti. Le definizioni degli indici che hanno subito modifiche sono state generate utilizzando il bundle dell’archivio Adobe Granite della versione dell’AEM di destinazione e oak-run.

Per eseguire il dump della definizione dell&#39;indice dall&#39;istanza AEM **source**, eseguire il comando seguente:

>[!NOTE]
>
>Per ulteriori dettagli sulle definizioni degli indici di dumping, consulta la [documentazione di Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Dove `datastore path` e `nodestore path` provengono dall&#39;istanza AEM **source**.

Quindi, genera le definizioni dell&#39;indice dalla versione dell&#39;AEM **target** utilizzando il bundle dell&#39;archivio Granite della versione di destinazione.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>Il processo di creazione della definizione dell&#39;indice precedente è supportato solo dalla versione `oak-run-1.12.0` in poi. Il targeting viene eseguito utilizzando il bundle dell&#39;archivio Granite `com.adobe.granite.repository-x.x.xx.jar`.

I passaggi precedenti creano un file JSON denominato `merge-index-definitions_target.json` che rappresenta la definizione dell&#39;indice.

**2. Crea un punto di controllo nel repository**

Crea un punto di controllo nell&#39;istanza AEM **source** di produzione con una durata prolungata. Questa operazione deve essere eseguita prima di clonare l’archivio.

Tramite la console JMX che si trova in `http://serveraddress:serverport/system/console/jmx`, vai a `CheckpointMBean` e crea un punto di controllo con una durata sufficiente (ad esempio, 200 giorni). Per questo, richiama `CheckpointMBean#createCheckpoint` con `17280000000` come argomento per la durata in millisecondi.

Al termine dell&#39;operazione, copiare l&#39;ID del punto di controllo appena creato e convalidarne la durata utilizzando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>Questo punto di controllo verrà eliminato quando l’indice verrà importato in un secondo momento.

Per ulteriori dettagli, consulta [creazione punto di controllo](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) dalla documentazione di Oak.

**Esegui indicizzazione offline per le definizioni dell&#39;indice generato**

La reindicizzazione Lucene può essere eseguita offline utilizzando oak-run. Questo processo crea i dati di indice nel disco in `indexing-result/indexes`. **not** scrive nel repository e pertanto non richiede l&#39;arresto dell&#39;istanza AEM in esecuzione. L&#39;archivio di testo creato viene inserito in questo processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

L&#39;utilizzo del parametro `--doc-traversal-mode` risulta utile con le installazioni di MongoMK in quanto migliora notevolmente il tempo di reindicizzazione tramite lo spooling del contenuto dell&#39;archivio in un file flat locale. Tuttavia, richiede spazio su disco aggiuntivo di dimensioni doppie rispetto a quelle dell’archivio.

Se è presente MongoMK, questo processo può essere accelerato se questo passaggio viene eseguito in un’istanza più vicina all’istanza MongoDB. Se viene eseguito sullo stesso computer, è possibile evitare il sovraccarico di rete.

Ulteriori dettagli tecnici sono disponibili nella [documentazione oak-run per l&#39;indicizzazione](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importazione degli indici {#importing-indexes}

Con AEM 6.4 e versioni più recenti, AEM ha la funzionalità incorporata di importare gli indici dal disco nella sequenza di avvio. La cartella `<repository>/indexing-result/indexes` viene controllata per verificare la presenza di dati di indice durante l&#39;avvio. È possibile copiare l&#39;indice precreato nella posizione precedente durante il [processo di aggiornamento](in-place-upgrade.md#performing-the-upgrade) prima di iniziare con la nuova versione del file jar dell&#39;AEM **target**. AEM lo importa nell’archivio e rimuove il punto di controllo corrispondente dal sistema. Pertanto, una reindicizzazione è completamente evitata.

## Ulteriori suggerimenti e risoluzione dei problemi {#troubleshooting}

Di seguito sono riportati alcuni suggerimenti utili e istruzioni per la risoluzione dei problemi.

### Ridurre l&#39;impatto sul sistema di produzione live {#reduce-the-impact-on-the-live-production-system}

Si consiglia di clonare il sistema di produzione e creare l’indice offline utilizzando il clone. Questo elimina qualsiasi potenziale impatto sul sistema di produzione. Tuttavia, il punto di controllo necessario per l’importazione dell’indice deve essere presente nel sistema di produzione. Pertanto, è fondamentale creare un punto di controllo prima di eseguire il clone.

### Preparare un Runbook e un’esecuzione di prova {#prepare-a-runbook-and-trial-run}

È consigliabile preparare un [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html?lang=it#building-the-upgrade-and-rollback-runbook) ed eseguire alcune prove prima di eseguire l&#39;aggiornamento in produzione.

### Modalità Di Trasferimento Dei Documenti Con Indicizzazione Offline {#doc-traversal-mode-with-offline-indexing}

L’indicizzazione offline richiede più attraversamenti dell’intero archivio. Con le installazioni MongoMK, l’accesso all’archivio avviene tramite la rete, con un impatto sulle prestazioni del processo di indicizzazione. Un&#39;opzione consiste nell&#39;eseguire il processo di indicizzazione offline sulla replica MongoDB stessa che eliminerà il sovraccarico di rete. Un’altra opzione è l’utilizzo della modalità di attraversamento documenti.

È possibile applicare la modalità di attraversamento dei documenti aggiungendo il parametro della riga di comando `—doc-traversal` al comando oak-run per l&#39;indicizzazione offline. Questa modalità effettua lo spool di una copia dell&#39;intero repository nel disco locale come file flat e la utilizza per eseguire l&#39;indicizzazione.
