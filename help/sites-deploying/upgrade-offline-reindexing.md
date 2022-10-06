---
title: Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento
description: Scopri come utilizzare la metodologia di reindicizzazione offline per ridurre i tempi di inattività del sistema durante l'esecuzione di un aggiornamento AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introduzione {#introduction}

Una delle principali sfide nell’aggiornamento di Adobe Experience Manager è il downtime associato all’ambiente di authoring quando viene eseguito un aggiornamento sul posto. Gli autori dei contenuti non potranno accedere all’ambiente durante un aggiornamento. Pertanto, è consigliabile ridurre al minimo il tempo necessario per eseguire l’aggiornamento. Per gli archivi di grandi dimensioni, in particolare i progetti AEM Assets, che in genere dispongono di grandi archivi di dati e di un elevato livello di caricamenti di risorse all’ora, la reindicizzazione degli indici Oak richiede una percentuale significativa del tempo di aggiornamento.

Questa sezione descrive come utilizzare lo strumento Oak-run per reindicizzare l&#39;archivio **prima** l&#39;esecuzione dell&#39;aggiornamento, riducendo così la quantità di downtime durante l&#39;aggiornamento effettivo. Le fasi presentate possono essere applicate a [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) indici per le versioni AEM 6.4 e successive.

## Panoramica {#overview}

Le nuove versioni del AEM introducono modifiche alle definizioni degli indici Oak man mano che il set di funzioni viene espanso. Le modifiche agli indici Oak forzano la reindicizzazione quando si aggiorna l&#39;istanza AEM. La reindicizzazione è costosa per le distribuzioni di risorse in quanto il testo nelle risorse (ad esempio, il testo nel file pdf) viene estratto e indicizzato. Con gli archivi MongoMK, i dati vengono mantenuti attraverso la rete, aumentando ulteriormente la quantità di tempo necessario per la reindicizzazione.

Il problema che la maggior parte dei clienti deve affrontare durante un aggiornamento è la riduzione della finestra di inattività. La soluzione è **salta** l’attività di reindicizzazione durante l’aggiornamento. Ciò può essere ottenuto creando nuovi indici **precedente** per eseguire l&#39;aggiornamento, è sufficiente importarli durante l&#39;aggiornamento.

## Approccio {#approach}

![offline-reindicizzazione-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

L&#39;idea è quella di creare l&#39;indice prima dell&#39;aggiornamento, rispetto alle definizioni dell&#39;indice della versione AEM di destinazione utilizzando [corsa Oak](/help/sites-deploying/indexing-via-the-oak-run-jar.md) strumento. Il diagramma precedente mostra l&#39;approccio di reindicizzazione offline.

Inoltre, questo è l’ordine dei passaggi descritti nell’approccio:

1. Il testo dai binari viene estratto per primo
2. Vengono create le definizioni degli indici di Target
3. Gli indici offline vengono creati
4. Gli indici vengono quindi importati durante il processo di aggiornamento

### Estrazione testo {#text-extraction}

Per abilitare l’indicizzazione completa in AEM, il testo dei file binari come PDF viene estratto e aggiunto all’indice. Questo è solitamente un passo costoso nel processo di indicizzazione. L’estrazione del testo è una fase di ottimizzazione consigliata soprattutto per la reindicizzazione degli archivi di risorse in quanto memorizzano un gran numero di binari.

![offline-reindicizzazione-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

Il testo dei binari memorizzati nel sistema può essere estratto utilizzando lo strumento oak-run con la libreria tika. È possibile eseguire un clone dei sistemi di produzione prima dell’aggiornamento e utilizzarlo per questo processo di estrazione del testo. Questo processo crea quindi l&#39;archivio di testo, eseguendo i seguenti passaggi:

**1. Naviga nel repository e raccogli i dettagli dei binari**

Questo passaggio genera un file CSV contenente una tupla di binari, contenente un percorso e un ID BLOB.

Esegui il comando sottostante dalla directory da cui desideri creare l&#39;indice. L&#39;esempio seguente presuppone la directory home dell&#39;archivio.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Dove `nodestore path` è `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilizza la `--fake-ds-path=temp` invece di `–fds-path` per accelerare il processo.

**2. Riutilizzare l&#39;archivio di testo binario disponibile nell&#39;indice esistente**

Eseguire il dump dei dati dell&#39;indice dal sistema esistente ed estrarre l&#39;archivio di testo.

Puoi scaricare i dati di indice esistenti utilizzando il seguente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Dove `nodestore path` è `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Quindi, utilizza il dump dell&#39;indice di cui sopra per popolare l&#39;archivio:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Dove `oak-index-name` è il nome dell&#39;indice full text, ad esempio &quot;lucene&quot;.

**3. Esegui il processo di estrazione del testo utilizzando la libreria tika per i binari mancanti nel passaggio precedente**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Dove `datastore path` è il percorso dell&#39;archivio dati binario.

L’archivio di testo creato può essere aggiornato e riutilizzato in futuro per scenari di reindicizzazione.

Per ulteriori dettagli sul processo di estrazione del testo, consulta la sezione [Documentazione di Oak-run](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindicizzazione offline {#offline-reindexing}

![offline-reindicizzazione-aggiornamento-offline-reindicizzazione](assets/offline-reindexing-upgrade-offline-reindexing.png)

Crea l&#39;indice Lucene offline prima dell&#39;aggiornamento. Se si utilizza MongoMK, si consiglia di eseguirlo direttamente su uno dei nodi MongoMk, in quanto questo evita il sovraccarico di rete.

Per creare l&#39;indice offline, segui i passaggi seguenti:

**1. Generare le definizioni dell&#39;indice Oak Lucene per la versione AEM di destinazione**

Eseguire il dump delle definizioni di indice esistenti. Le definizioni degli indici oggetto di modifiche sono state generate utilizzando il bundle dell&#39;archivio Adobe Granite della versione AEM di destinazione e di oak-run.

Per scaricare la definizione dell&#39;indice dal **source** AEM&#39;istanza, esegui questo comando:

>[!NOTE]
>
>Per maggiori dettagli sulle definizioni degli indici di dumping, consultare il [Documentazione Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Dove `datastore path` e `nodestore path` sono del **source** AEM&#39;istanza.

Quindi, genera le definizioni degli indici dal **target** Versione AEM utilizzando il bundle dell’archivio Granite della versione di destinazione.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> Il processo di creazione della definizione dell&#39;indice di cui sopra è supportato solo da `oak-run-1.12.0` a partire dalla versione. Il targeting viene eseguito utilizzando il bundle dell&#39;archivio Granite `com.adobe.granite.repository-x.x.xx.jar`.

I passaggi precedenti creano un file JSON denominato `merge-index-definitions_target.json` che è la definizione dell&#39;indice.

**2. Creare un checkpoint nell’archivio**

Creare un checkpoint nella produzione **source** AEM&#39;istanza con una vita lunga. Questo deve essere fatto prima di clonare l’archivio.

Tramite la console JMX situata in `http://serveraddress:serverport/system/console/jmx`, vai a `CheckpointMBean` e crea un punto di controllo con una durata sufficiente (ad esempio, 200 giorni). Per questo, invoca `CheckpointMBean#createCheckpoint` con `17280000000` come argomento per la durata del ciclo di vita, in millisecondi.

Una volta fatto questo, copia il nuovo id del punto di controllo creato e convalida la durata utilizzando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Questo punto di controllo verrà eliminato quando l&#39;indice viene importato in un secondo momento.

Per maggiori dettagli, consulta [creazione di checkpoint](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) dalla documentazione Oak.

**Esegui indicizzazione offline per le definizioni di indice generate**

La reindicizzazione Lucene può essere fatta offline utilizzando oak-run. Questo processo crea i dati di indice nel disco sotto `indexing-result/indexes`. Lo fa **not** scrivi nell’archivio e quindi non richiede l’arresto dell’istanza AEM in esecuzione. L&#39;archivio di testo creato viene inserito in questo processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

Utilizzo del `--doc-traversal-mode` Il parametro è utile con le installazioni MongoMK in quanto migliora notevolmente il tempo di reindicizzazione spooling del contenuto dell&#39;archivio in un file flat locale. Tuttavia, richiede uno spazio su disco aggiuntivo pari al doppio delle dimensioni dell’archivio.

Nel caso di MongoMK, questo processo può essere accelerato se questo passaggio viene eseguito in un&#39;istanza più vicina all&#39;istanza MongoDB. Se eseguito sulla stessa macchina, è possibile evitare il sovraccarico di rete.

Ulteriori dettagli tecnici sono disponibili nella sezione [documentazione oak-run per l&#39;indicizzazione](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importazione degli indici {#importing-indexes}

Con AEM 6.4 e versioni più recenti, AEM ha la funzionalità integrata per importare gli indici dal disco nella sequenza di avvio. La cartella `<repository>/indexing-result/indexes` viene controllata la presenza di dati di indice durante l&#39;avvio. Puoi copiare l’indice pre-creato nella posizione precedente durante il [processo di aggiornamento](in-place-upgrade.md#performing-the-upgrade) prima di iniziare con la nuova versione di **target** AEM barattolo. AEM lo importa nell’archivio e rimuove il checkpoint corrispondente dal sistema. Così si evita completamente una reindicizzazione.

## Suggerimenti aggiuntivi e risoluzione dei problemi {#troubleshooting}

Di seguito sono riportati alcuni suggerimenti utili e istruzioni per la risoluzione dei problemi.

### Ridurre l&#39;impatto sul sistema di produzione live {#reduce-the-impact-on-the-live-production-system}

Si consiglia di clonare il sistema di produzione e creare l&#39;indice offline utilizzando il clone. Questo elimina ogni potenziale impatto sul sistema di produzione. Tuttavia, il checkpoint necessario per importare l&#39;indice deve essere presente nel sistema di produzione. Pertanto, è fondamentale creare un punto di controllo prima di eseguire il clone.

### Preparare un Runbook e un&#39;esecuzione di prova {#prepare-a-runbook-and-trial-run}

Si consiglia di preparare un [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) ed eseguire alcune prove prima di eseguire l&#39;aggiornamento in produzione.

### Modalità Traversal Doc Con Indicizzazione Offline {#doc-traversal-mode-with-offline-indexing}

L&#39;indicizzazione offline richiede più attraversamenti dell&#39;intero archivio. Con le installazioni MongoMK, l&#39;accesso all&#39;archivio avviene attraverso la rete che influisce sulle prestazioni del processo di indicizzazione. Un&#39;opzione consiste nell&#39;eseguire il processo di indicizzazione offline sulla replica MongoDB stessa, che eliminerà il sovraccarico di rete. Un&#39;altra opzione è l&#39;utilizzo della modalità traversal del documento.

La modalità traversal documento può essere applicata aggiungendo il parametro della riga di comando `—doc-traversal` al comando oak-run per l&#39;indicizzazione offline. Questa modalità spool una copia dell&#39;intero archivio nel disco locale come file flat e lo utilizza per eseguire l&#39;indicizzazione.
