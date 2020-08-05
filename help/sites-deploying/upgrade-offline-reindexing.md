---
title: Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento
description: Scoprite come utilizzare la metodologia di reindicizzazione offline per ridurre i tempi di inattività del sistema durante l'esecuzione di un AEM aggiornamento.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: d3a69bbbc9c3707538be74fd05f94f20a688d860
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introduzione {#introduction}

Uno dei problemi principali nell&#39;aggiornamento di Adobe Experience Manager è rappresentato dai tempi di inattività associati all&#39;ambiente di authoring durante l&#39;esecuzione di un aggiornamento locale. Gli autori dei contenuti non potranno accedere all&#39;ambiente durante un aggiornamento. Pertanto, è consigliabile ridurre al minimo il tempo necessario per eseguire l&#39;aggiornamento. Per i repository di grandi dimensioni, specialmente  progetti AEM Assets, che in genere dispongono di grandi archivi dati e di un elevato livello di caricamenti di risorse all’ora, la reindicizzazione degli indici Oak richiede una percentuale significativa del tempo di aggiornamento.

Questa sezione descrive come utilizzare lo strumento di esecuzione Oak per reindicizzare il repository **prima** di eseguire l&#39;aggiornamento, riducendo così la quantità di tempi di inattività durante l&#39;aggiornamento effettivo. Le fasi presentate possono essere applicate agli indici [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) per le versioni AEM 6.4 e successive.

## Panoramica {#overview}

Nuove versioni del AEM introducono modifiche alle definizioni dell&#39;indice Oak mano a mano che il set di funzioni viene espanso. Le modifiche agli indici Oak forzano la reindicizzazione durante l&#39;aggiornamento dell&#39;istanza AEM. La reindicizzazione è costosa per le distribuzioni di risorse, in quanto il testo presente nelle risorse (ad esempio, testo contenuto in file pdf) viene estratto e indicizzato. Con i repository MongoMK, i dati sono persistenti sulla rete, aumentando ulteriormente la quantità di tempo di reindicizzazione richiede.

Il problema che la maggior parte dei clienti si trova ad affrontare durante un aggiornamento è la riduzione del tempo di inattività. La soluzione consiste nel **saltare** l&#39;attività di reindicizzazione durante l&#39;aggiornamento. Questo può essere ottenuto creando nuovi indici **prima** di eseguire l&#39;aggiornamento, quindi semplicemente importandoli durante l&#39;aggiornamento.

## Approccio {#approach}

![offline-reindexing-upgrade-text-estrazione](assets/offline-reindexing-upgrade-process.png)

L&#39;idea è quella di creare l&#39;indice prima dell&#39;aggiornamento, rispetto alle definizioni di indice della versione AEM di destinazione utilizzando lo strumento [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) . Il diagramma precedente mostra l&#39;approccio di reindicizzazione offline.

Inoltre, questo è l&#39;ordine dei passaggi descritti nell&#39;approccio:

1. Testo dai binari viene estratto per primo
2. Definizione dell&#39;indice di destinazione
3. Gli indici offline vengono creati
4. Gli indici vengono quindi importati durante il processo di aggiornamento

### Estrazione testo {#text-extraction}

Per abilitare l&#39;indicizzazione completa in AEM, il testo dei file binari, come il PDF, viene estratto e aggiunto all&#39;indice. In genere si tratta di un passo costoso nel processo di indicizzazione. L&#39;estrazione del testo è una fase di ottimizzazione consigliata soprattutto per reindicizzare i repository di risorse in quanto contengono un gran numero di file binari.

![offline-reindexing-upgrade-text-estrazione](assets/offline-reindexing-upgrade-text-extraction.png)

Il testo dei file binari memorizzati nel sistema può essere estratto utilizzando lo strumento di esecuzione della quercia con la libreria tika. Un clone dei sistemi di produzione può essere fatto prima dell&#39;aggiornamento e può essere utilizzato per questo processo di estrazione del testo. Questo processo crea quindi l&#39;archivio di testo eseguendo i passaggi seguenti:

**1. Naviga nella directory archivio e raccoglie i dettagli dei file binari**

Questo passaggio genera un file CSV contenente un tuple di file binari, contenente un percorso e un ID BLOB.

Eseguire il comando seguente dalla directory da cui si desidera creare l&#39;indice. L&#39;esempio seguente presuppone la directory principale del repository.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Dove `nodestore path` si trova il `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Utilizzate il `--fake-ds-path=temp` parametro invece di `–fds-path` velocizzare il processo.

**2. Riutilizzare l&#39;archivio di testo binario disponibile nell&#39;indice esistente**

Eseguire il dump dei dati di indice dal sistema esistente ed estrarre l&#39;archivio di testo.

È possibile scaricare i dati di indice esistenti utilizzando il seguente comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Dove `nodestore path` si trova il `mongo_ur` o `crx-quickstart/repository/segmentstore/`

Quindi, utilizzate il dump dell&#39;indice riportato sopra per compilare lo store:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Dove `oak-index-name` è il nome dell&#39;indice di testo completo, ad esempio &quot;lucene&quot;.

**3. Eseguire il processo di estrazione del testo utilizzando la libreria tika per i file binari mancanti nel passaggio precedente**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Dove `datastore path` è il percorso dell&#39;archivio dati binario.

L&#39;archivio di testo creato può essere aggiornato e riutilizzato in futuro per gli scenari di reindicizzazione.

Per ulteriori dettagli sul processo di estrazione del testo, consulta la documentazione [di](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)esecuzione Oak.

### Riindicizzazione offline {#offline-reindexing}

![offline-reindicxing-upgrade-offline-reindicizzazione](assets/offline-reindexing-upgrade-offline-reindexing.png)

Creare l&#39;indice Lucene offline prima dell&#39;aggiornamento. Se si utilizza MongoMK, si consiglia di eseguirlo direttamente su uno dei nodi MongoMk, in quanto questo evita il sovraccarico di rete.

Per creare l&#39;indice offline, attenetevi alla procedura seguente:

**1. Genera definizioni dell&#39;indice Oak Lucene per la versione AEM di destinazione**

Eseguire il dump delle definizioni di indice esistenti. Le definizioni degli indici oggetto di modifiche sono state generate utilizzando il pacchetto dell&#39;archivio Granite  Adobe della versione AEM di destinazione e dell&#39;esecuzione della quercia.

Per eliminare la definizione dell&#39;indice dall&#39;istanza di AEM **di origine** , eseguire il comando seguente:

>[!NOTE]
>
>Per maggiori dettagli sulle definizioni dell&#39;indice di dumping, consulta la documentazione [](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)Oak.

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Posizione `datastore path` e `nodestore path` dell’istanza di AEM **origine** .

Quindi, generate le definizioni di indice dalla versione di **destinazione** AEM utilizzando il bundle del repository Granite della versione di destinazione.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> Il processo di creazione della definizione di indice riportato sopra è supportato solo a partire dalla `oak-run-1.12.0` versione. Il targeting viene eseguito utilizzando il bundle del repository Granite `com.adobe.granite.repository-x.x.xx.jar`.

I passaggi precedenti creano un file JSON denominato `merge-index-definitions_target.json` che è la definizione di indice.

**2. Creare un checkpoint nell&#39;archivio**

Crea un punto di controllo nell’istanza di AEM **origine** di produzione con una durata prolungata. Questa operazione deve essere eseguita prima della duplicazione del repository.

Tramite console JMX ubicata in `http://serveraddress:serverport/system/console/jmx`, andate a `CheckpointMBean` creare un checkpoint con una durata sufficiente (ad esempio, 200 giorni). Per questo, invocate `CheckpointMBean#createCheckpoint` con `17280000000` come argomento la durata del ciclo di vita, in millisecondi.

Al termine, copiate l’ID del checkpoint appena creato e convalidate la durata utilizzando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Questo punto di controllo verrà eliminato quando l&#39;indice verrà importato in un secondo momento.

Per ulteriori informazioni, consulta la sezione dedicata alla creazione [dei punti di](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) controllo nella documentazione Oak.

**Eseguire l&#39;indicizzazione offline per le definizioni di indice generate**

La reindicizzazione Lucene può essere fatta offline utilizzando la rovere. Questo processo crea i dati di indice nel disco sotto `indexing-result/indices`. Non **scrive** nella directory archivio e non richiede pertanto l&#39;arresto dell&#39;istanza AEM in esecuzione. L&#39;archivio di testo creato viene incluso in questo processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indices in this file will be re-indexed.
```

L&#39;utilizzo del `--doc-traversal-mode` parametro è molto pratico con le installazioni MongoMK, in quanto migliora notevolmente il tempo di reindicizzazione spooling del contenuto del repository in un file flat locale. Tuttavia, richiede uno spazio su disco aggiuntivo pari al doppio delle dimensioni del repository.

Nel caso di MongoMK, questo processo può essere accelerato se questo passaggio viene eseguito in un&#39;istanza più vicina all&#39;istanza MongoDB. Se eseguito sullo stesso computer, è possibile evitare il sovraccarico di rete.

Ulteriori dettagli tecnici si trovano nella documentazione [di esecuzione della quercia per l&#39;indicizzazione](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importazione di indici {#importing-indices}

Con AEM 6.4 e versioni successive, AEM ha la capacità integrata di importare indici da disco sulla sequenza di avvio. La cartella `<repository>/indexing-result/indices` viene controllata per verificare la presenza dei dati di indice durante l&#39;avvio. Potete copiare l&#39;indice pre-creato nella posizione sopra durante il processo [di](in-place-upgrade.md#performing-the-upgrade) aggiornamento prima di iniziare con la nuova versione del AEM di **destinazione** . AEM lo importa nel repository e rimuove il checkpoint corrispondente dal sistema. Così un reindice è completamente evitato.

## Suggerimenti aggiuntivi e risoluzione dei problemi {#troubleshooting}

Di seguito sono riportati alcuni utili suggerimenti e istruzioni per la risoluzione di problemi.

### Ridurre l&#39;impatto sul sistema di produzione live {#reduce-the-impact-on-the-live-production-system}

Si consiglia di duplicare il sistema di produzione e creare l&#39;indice offline utilizzando il clone. Ciò elimina ogni potenziale impatto sul sistema di produzione. Tuttavia, il checkpoint richiesto per l&#39;importazione dell&#39;indice deve essere presente nel sistema di produzione. Pertanto, è fondamentale creare un punto di controllo prima di eseguire il clone.

### Preparare un Runbook e un&#39;esecuzione di prova {#prepare-a-runbook-and-trial-run}

Si consiglia di preparare un [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) ed eseguire alcune prove prima di eseguire l&#39;aggiornamento in produzione.

### Modalità Traversal Doc Con Indicizzazione Offline {#doc-traversal-mode-with-offline-indexing}

L&#39;indicizzazione offline richiede più passaggi dell&#39;intero repository. Con le installazioni MongoMK, l&#39;accesso al repository è effettuato attraverso la rete che influisce sulle prestazioni del processo di indicizzazione. Un&#39;opzione consiste nell&#39;eseguire il processo di indicizzazione offline sulla replica MongoDB stessa, che eliminerà il sovraccarico di rete. Un&#39;altra opzione è l&#39;utilizzo della modalità traversal del documento.

La modalità traversal Doc può essere applicata aggiungendo il parametro della riga di comando `—doc-traversal` al comando di esecuzione della quercia per l&#39;indicizzazione offline. Questa modalità mette in comune una copia dell&#39;intero repository nel disco locale come file semplice e la utilizza per eseguire l&#39;indicizzazione.
