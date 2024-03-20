---
title: Casi di utilizzo dell’indicizzazione Oak-run.jar
description: Scopri i vari casi d’uso per l’esecuzione dell’indicizzazione con lo strumento Oak-run.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Casi di utilizzo dell’indicizzazione Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run supporta l’indicizzazione dei casi d’uso sulla riga di comando senza dover orchestrare l’esecuzione di tali casi d’uso tramite la console JMX dell’AEM.

I vantaggi principali dell’utilizzo dell’approccio del comando dell’indice oak-run.jar per la gestione degli indici Oak sono:

1. Il comando Oak-run index fornisce un nuovo set di strumenti di indicizzazione per AEM 6.4.
1. Oak-run riduce il tempo di reindicizzazione, riducendo i tempi di reindicizzazione su archivi più grandi.
1. Oak-run riduce il consumo di risorse durante la reindicizzazione in AEM, con conseguente miglioramento generale delle prestazioni del sistema.
1. Oak-run fornisce reindicizzazione fuori banda, supportando situazioni in cui la produzione deve essere disponibile e non può tollerare la manutenzione o tempi di inattività altrimenti necessari per la reindicizzazione.

Le sezioni seguenti forniscono comandi di esempio. Il comando Oak-run index supporta tutte le impostazioni di NodeStore e BlobStore. Gli esempi forniti di seguito riguardano le impostazioni con FileDataStore e SegmentNodeStore.

## Caso d’uso 1: verifica di coerenza dell’indice {#usercase1indexconsistencycheck}

Questo è un caso d’uso relativo al danneggiamento dell’indice. A volte non era possibile determinare quali degli indici fossero danneggiati. Adobe ha pertanto fornito strumenti che:

1. Esegue controlli di coerenza dell’indice su tutti gli indici e fornisce una relazione sugli indici validi e non validi;
1. Gli strumenti sono utilizzabili anche se l’AEM non è accessibile;
1. È facile da usare.

La ricerca di indici danneggiati può essere eseguita tramite `--index-consistency-check` operazione:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Questo genera un rapporto in `indexing-result/index-consistency-check-report.txt`. Per un rapporto di esempio, consulta:

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Vantaggi {#uc1benefits}

Questo strumento può ora essere utilizzato dal supporto tecnico e dall&#39;amministratore di sistema per determinare rapidamente quali indici sono danneggiati e quindi reindicizzarli.

## Caso d’uso 2: statistiche dell’indice {#usecase2indexstatistics}

Per diagnosticare alcuni dei casi relativi all’Adobe delle prestazioni delle query, spesso era necessario disporre di una definizione di indice esistente e di statistiche relative all’indice provenienti dalla configurazione del cliente. Finora queste informazioni erano disseminate su più risorse. Per semplificare la risoluzione dei problemi, Adobe ha creato una serie di strumenti che:

1. Scarica tutte le definizioni di indice presenti sul sistema in un singolo file JSON;

1. Dump di importanti statistiche dagli indici esistenti;

1. Dump del contenuto dell’indice per l’analisi offline;

1. È utilizzabile anche se l’AEM non è accessibile

Le operazioni di cui sopra possono ora essere eseguite mediante i seguenti comandi di indice delle operazioni:

* `--index-info` - Raccoglie ed esegue il dump di varie statistiche relative agli indici

* `--index-definitions` - Raccoglie ed esegue il dump delle definizioni dell&#39;indice

* `--index-dump` - Dump del contenuto dell’indice

Di seguito è riportato un esempio di funzionamento pratico dei comandi:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

I rapporti vengono generati in `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Inoltre, gli stessi dettagli vengono forniti tramite la console web e farebbero parte del file zip del dump di configurazione. È possibile accedervi dal seguente percorso:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Vantaggi {#uc2benefits}

Questo strumento consente di raccogliere rapidamente tutti i dettagli richiesti relativi ai problemi di indicizzazione o query e di ridurre il tempo impiegato per estrarre tali informazioni.

## Caso d’uso 3: reindicizzazione {#usecase3reindexing}

A seconda della [scenari](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), a volte, è necessario eseguire la reindicizzazione. Attualmente, la reindicizzazione viene eseguita impostando `reindex` contrassegna per `true` nel nodo di definizione dell’indice tramite CRXDE o l’interfaccia utente di Index Manager. Una volta impostato il flag, la reindicizzazione viene eseguita in modo asincrono.

Alcuni punti da notare sulla reindicizzazione:

* Reindicizzazione molto più lenta `DocumentNodeStore` impostazioni confrontate con `SegmentNodeStore` impostazioni in cui tutto il contenuto è locale;

* Con la progettazione corrente, mentre si verifica la reindicizzazione, l’indicizzatore asincrono viene bloccato e tutti gli altri indici asincroni diventano obsoleti e non vengono aggiornati durante l’indicizzazione. Per questo motivo, se il sistema è in uso, gli utenti potrebbero non vedere risultati aggiornati;
* La reindicizzazione comporta la navigazione dell’intero archivio che può comportare un carico elevato sulla configurazione dell’AEM e quindi incidere sull’esperienza dell’utente finale;
* Per un `DocumentNodeStore` installazione in cui la reindicizzazione potrebbe richiedere molto tempo, se la connessione alla banca dati Mongo dovesse non riuscire nel mezzo dell’operazione, l’indicizzazione dovrebbe essere riavviata da zero;

* A volte, la reindicizzazione può richiedere molto tempo a causa dell’estrazione del testo. Questo è specifico per le configurazioni con molti file PDF, in cui il tempo impiegato per l’estrazione del testo può influire sul tempo di indicizzazione.

Per raggiungere questi obiettivi, la strumentazione dell&#39;indice oak-run supporta diverse modalità per la reindicizzazione che possono essere utilizzate secondo necessità. Il comando oak-run index offre i seguenti vantaggi:

* **reindicizzazione fuori banda** - la reindicizzazione oak-run può essere effettuata separatamente da una configurazione AEM in esecuzione e quindi riduce al minimo l&#39;impatto sull&#39;istanza AEM in uso;

* **reindicizzazione fuori corsia** - La reindicizzazione avviene senza influire sulle operazioni di indicizzazione. Ciò significa che l’indicizzatore asincrono può continuare a indicizzare altri indici;

* **Reindicizzazione semplificata per installazioni DocumentNodeStore** - Per `DocumentNodeStore` nelle installazioni, la reindicizzazione può essere effettuata con un unico comando che garantisce che la reindicizzazione sia effettuata nel modo più ottimale;

* **Supporta l’aggiornamento delle definizioni degli indici e l’introduzione di nuove definizioni degli indici**

### Reindicizza - DocumentNodeStore {#reindexdocumentnodestore}

Per `DocumentNodeStore` la reindicizzazione delle installazioni può essere eseguita mediante un singolo comando oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Questo offre i seguenti vantaggi

* Impatto minimo sull’esecuzione delle istanze AEM. La maggior parte delle letture può essere effettuata da server secondari e l’esecuzione di cache AEM non è influenzata negativamente a causa di tutte le traversali necessarie per la reindicizzazione;
* Gli utenti possono anche fornire un JSON di un indice nuovo o aggiornato tramite `--index-definitions-file` opzione.

### Reindicizza - SegmentNodeStore {#reindexsegmentnodestore}

Per `SegmentNodeStore` la reindicizzazione delle installazioni può essere eseguita in uno dei seguenti modi:

#### Reindicizzazione online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Seguire la modalità stabilita in cui la reindicizzazione viene eseguita impostando `reindex` flag.

#### Reindicizzazione online - SegmentNodeStore - L’istanza AEM è in esecuzione {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Per `SegmentNodeStore` installazioni, solo un processo può accedere ai file dei segmenti in modalità di lettura-scrittura. Per questo motivo, alcune operazioni nell’indicizzazione oak-run richiedono l’esecuzione di passaggi manuali aggiuntivi.

Ciò comporterebbe quanto segue:

1. Testo del passaggio
1. Connetti `oak-run` nello stesso archivio utilizzato dall’AEM in modalità di sola lettura ed eseguono l’indicizzazione. Un esempio di come ottenere questo risultato:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Infine, importa i file di indice creati tramite `IndexerMBean#importIndex` operazione dal percorso in cui oak-run ha salvato i file di indicizzazione dopo l’esecuzione del comando precedente.

In questo scenario, non è necessario arrestare il server AEM o eseguire il provisioning di una nuova istanza. Tuttavia, poiché l’indicizzazione comporta l’attraversamento dell’intero archivio, aumenta il carico di I/O sull’installazione, con un impatto negativo sulle prestazioni di runtime.

#### Reindicizzazione online - SegmentNodeStore - L’istanza AEM è chiusa {#onlinereindexsegmentnodestoreaeminstanceisdown}

Per `SegmentNodeStore` installazioni, la reindicizzazione può essere eseguita tramite un singolo comando oak-run. Tuttavia, l’istanza AEM deve essere chiusa.

Puoi attivare la reindicizzazione con il seguente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La differenza tra questo approccio e quello descritto in precedenza è che la creazione di punti di controllo e l’importazione degli indici vengono eseguite automaticamente. Il rovescio della medaglia è che l&#39;AEM deve essere abbassato durante il processo.

#### Reindicizzazione fuori banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

In questo caso d’uso, puoi eseguire la reindicizzazione su una configurazione clonata per ridurre al minimo l’impatto sull’istanza AEM in esecuzione:

1. Crea un punto di controllo tramite un’operazione JMX. Per eseguire questa operazione, vai al [Console JMX](/help/sites-administering/jmx-console.md) e cerca `CheckpointManager`. Quindi, fai clic su **createCheckpoint(long p1)** operazione che utilizza un valore elevato per la scadenza in secondi (ad esempio, **2592000**).
1. Copia il `crx-quickstart` cartella in un nuovo computer
1. Eseguire la reindicizzazione tramite il comando oak-run index

1. Copiare i file di indice generati nel server AEM

1. Importa i file di indice tramite JMX.

In questo caso d’uso, si presume che l’archivio dati sia accessibile in un’altra istanza, il che potrebbe non essere possibile se `FileDataStore` viene inserito in una soluzione di archiviazione basata su cloud come EBS. Questo esclude lo scenario in cui `FileDataStore` viene clonato anche. Se la definizione dell’indice non esegue l’indicizzazione full-text, puoi accedere a `DataStore` non è obbligatorio.

## Caso d&#39;uso 4: aggiornamento delle definizioni degli indici {#usecase4updatingindexdefinitions}

Attualmente, è possibile modificare la definizione dell’indice di spedizione tramite [ACS - Assicurati indice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) pacchetto. Questo consente la spedizione delle definizioni dell’indice tramite un pacchetto di contenuto che in seguito richiede che la reindicizzazione venga eseguita impostando `reindex` contrassegna per `true`.

Questo funziona bene per le installazioni più piccole in cui la reindicizzazione non richiede molto tempo. Tuttavia, per gli archivi di grandi dimensioni, la reindicizzazione viene eseguita in un periodo di tempo notevolmente più lungo. Per questi casi, ora possiamo utilizzare gli strumenti dell’indice oak-run.

Oak-run ora supporta la fornitura di definizioni di indice in formato JSON e la creazione di indice in modalità fuori banda, in cui non vengono eseguite modifiche su un’istanza live.

Il processo da considerare per questo caso d’uso è:

1. Uno sviluppatore aggiornerebbe le definizioni dell’indice in un’istanza locale e quindi genererebbe un file JSON di definizione dell’indice tramite `--index-definitions` opzione

1. Il JSON aggiornato viene quindi assegnato all’amministratore di sistema
1. L&#39;amministratore di sistema adotta l&#39;approccio out-of-band e prepara l&#39;indice su un&#39;installazione diversa
1. Al termine dell&#39;operazione, i file di indice generati vengono importati in un&#39;installazione AEM in esecuzione.
