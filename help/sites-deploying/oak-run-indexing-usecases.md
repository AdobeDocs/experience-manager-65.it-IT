---
title: Indicizzazione Oak-run.jar - Casi di utilizzo
seo-title: Indicizzazione Oak-run.jar - Casi di utilizzo
description: Scoprite i diversi casi di utilizzo per l’indicizzazione con lo strumento di esecuzione Oak.
seo-description: Scoprite i diversi casi di utilizzo per l’indicizzazione con lo strumento di esecuzione Oak.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Indicizzazione Oak-run.jar - Casi di utilizzo{#oak-run-jar-indexing-use-cases}

Oak-run supporta l’indicizzazione dei casi di utilizzo sulla riga di comando senza dover orchestrare l’esecuzione di questi casi tramite la console JMX di AEM.

I vantaggi generali dell’utilizzo del metodo di comando oak-run.jar index per la gestione degli indici Oak sono:

1. Il comando indice di esecuzione Oak fornisce un nuovo set di strumenti di indicizzazione per AEM 6.4.
1. La corsa Oak diminuisce il tempo di reindicizzazione, riducendo i tempi di reindicizzazione sui repository più grandi.
1. L’esecuzione Oak riduce il consumo di risorse durante il reindicizzazione in AEM, migliorando nel complesso le prestazioni del sistema.
1. L&#39;esecuzione di Oak fornisce reindicizzazione fuori banda, situazioni di supporto in cui la produzione deve essere disponibile e non può tollerare la manutenzione o i tempi di inattività altrimenti necessari per la reindicizzazione.

Le sezioni seguenti forniscono comandi di esempio. Il comando indice di esecuzione del quercia supporta tutte le impostazioni NodeStore e BlobStore. Gli esempi forniti di seguito indicano le impostazioni con FileDataStore e SegmentNodeStore.

## Caso d’uso 1 - Controllo di coerenza indice {#usercase1indexconsistencycheck}

Questo è un caso d&#39;uso correlato al danneggiamento dell&#39;indice. In alcuni casi non è stato possibile determinare quali indici sono danneggiati. Adobe ha pertanto fornito strumenti che:

1. esegue controlli di coerenza dell&#39;indice su tutti gli indici e fornisce un rapporto su cui gli indici sono validi e che non sono validi;
1. La strumentazione è utilizzabile anche se AEM non è accessibile;
1. È facile da usare.

La verifica degli indici danneggiati può essere eseguita tramite `--index-consistency-check` operazione:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

In questo modo verrà generato un rapporto in `indexing-result/index-consistency-check-report.txt`. Per un rapporto campione, vedi sotto:

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

Questo strumento può ora essere utilizzato da Supporto e Amministratore di sistema per determinare rapidamente quali indici sono danneggiati e quindi reindicizzarli.

## Caso d’uso 2 - Statistiche indice {#usecase2indexstatistics}

Per diagnosticare alcuni dei casi relativi alle prestazioni della query, spesso Adobe ha richiesto la definizione di indice esistente, statistiche relative all&#39;indice dalla configurazione del cliente. Finora queste informazioni erano sparse su più risorse. Per semplificare la risoluzione dei problemi, Adobe ha creato strumenti che consentiranno di:

1. Eseguire il dump di tutte le definizioni di indice presenti nel sistema in un unico file JSON;

1. elaborare statistiche importanti dagli indici esistenti;

1. Dump il contenuto dell&#39;indice per l&#39;analisi offline;

1. Sarà utilizzabile anche se AEM non è accessibile

Le operazioni di cui sopra possono essere eseguite tramite i seguenti comandi di indice delle operazioni:

* `--index-info` - Raccoglie e scarica varie statistiche relative agli indici

* `--index-definitions` - Raccoglie e scarica le definizioni degli indici

* `--index-dump` - Contenuto indice Dumps

Di seguito è riportato un esempio di funzionamento pratico dei comandi:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

I rapporti vengono generati in `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Inoltre, gli stessi dettagli vengono forniti tramite la console Web e fanno parte del file ZIP del dump di configurazione. È possibile accedervi nel seguente percorso:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Vantaggi {#uc2benefits}

Questo strumento consente di raccogliere rapidamente tutti i dettagli necessari relativi a problemi di indicizzazione o query e di ridurre il tempo impiegato per estrarre tali informazioni.

## Caso d’uso 3 - Riindicizzazione {#usecase3reindexing}

In base agli [scenari](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), in alcuni casi è necessario eseguire la reindicizzazione. Attualmente la reindicizzazione viene eseguita impostando il `reindex` flag `true` nel nodo di definizione dell&#39;indice tramite CRXDE o tramite l&#39;interfaccia utente di Gestione indici. Una volta impostato il flag, la reindicizzazione viene eseguita in modo asincrono.

Alcuni punti da notare sulla reindicizzazione:

* La reindicizzazione è molto più lenta nelle `DocumentNodeStore` impostazioni rispetto alle `SegmentNodeStore` impostazioni locali;

* Con la progettazione corrente, mentre viene eseguita la reindicizzazione, l&#39;indicizzatore asincrono viene bloccato e tutti gli altri indici asincrono diventano obsoleti e non ricevono aggiornamenti per la durata dell&#39;indicizzazione. Per questo motivo, se il sistema è in uso, gli utenti potrebbero non visualizzare i risultati aggiornati;
* La reindicizzazione comporta l’attraversamento dell’intero repository, che può comportare un carico elevato sulla configurazione di AEM e quindi avere un impatto sull’esperienza dell’utente finale;
* Per un&#39; `DocumentNodeStore` installazione in cui la reindicizzazione potrebbe richiedere molto tempo, se la connessione al database Mongo non riesce nel mezzo dell&#39;operazione, l&#39;indicizzazione dovrebbe essere riavviata da zero;

* In alcuni casi, l’estrazione del testo può richiedere molto tempo. Questo è specifico per le impostazioni con molti file PDF, dove il tempo impiegato per l’estrazione del testo può influire sui tempi di indicizzazione.

Per raggiungere questi obiettivi, la struttura dell&#39;indice di rovere supporta diverse modalità di reindicizzazione che possono essere utilizzate come necessario. Il comando indice di esecuzione della quercia offre i seguenti vantaggi:

* **reindicizzazione fuori banda** : la reindicizzazione in rovere può essere effettuata separatamente da una configurazione di AEM in esecuzione, riducendo così l&#39;impatto sull&#39;istanza di AEM in uso;

* **reindicizzazione** out-of-lane - La reindicizzazione avviene senza che si verifichino effetti sulle operazioni di indicizzazione. Ciò significa che l&#39;indicizzatore asincrono può continuare ad indicizzare altri indici;

* **Reindicizzazione semplificata per le installazioni** DocumentNodeStore - Per `DocumentNodeStore` le installazioni è possibile eseguire la reindicizzazione con un singolo comando che assicura che la reindicizzazione venga effettuata nel modo migliore;

* **Supporta l&#39;aggiornamento delle definizioni di indice e l&#39;introduzione di nuove definizioni di indice**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Per `DocumentNodeStore` le installazioni è possibile eseguire la reindicizzazione tramite un singolo comando di esecuzione della quercia:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Questo offre i seguenti vantaggi

* Impatto minimo sull’esecuzione di istanze AEM. La maggior parte delle letture può essere effettuata da server secondari e l&#39;esecuzione delle cache AEM non ha un impatto negativo a causa di tutta la traversata necessaria per la reindicizzazione;
* Gli utenti possono anche fornire un JSON di un indice nuovo o aggiornato tramite l&#39; `--index-definitions-file` opzione.

### Reindex - SegmentNodeStore {#reindexsegmentnodestore}

Per `SegmentNodeStore` le installazioni è possibile eseguire la reindicizzazione in uno dei seguenti modi:

#### Reindicizzazione online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Seguire il modo stabilito in cui la reindicizzazione viene fatta tramite `reindex` flag di impostazione.

#### Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è in esecuzione {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Per `SegmentNodeStore` le installazioni, un solo processo può accedere ai file dei segmenti in modalità di lettura/scrittura. A causa di ciò, alcune operazioni di indicizzazione delle rovere richiedono ulteriori passaggi manuali.

Ciò implica quanto segue:

1. Testo del passaggio
1. Collegate lo `oak-run` stesso repository utilizzato da AEM in modalità di sola lettura ed eseguite l&#39;indicizzazione. Esempio di come ottenere questo risultato:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Infine, importare i file di indice creati tramite l&#39; `IndexerMBean#importIndex` operazione dal percorso in cui la corsa ha salvato i file di indicizzazione dopo l&#39;esecuzione del comando precedente.

In questo scenario non è necessario arrestare il server AEM o eseguire il provisioning di alcuna nuova istanza. Tuttavia, poiché l&#39;indicizzazione comporta l&#39;attraversamento dell&#39;intero repository, aumenterebbe il carico di I/O sull&#39;installazione, con un impatto negativo sulle prestazioni del runtime.

#### Reindicizzazione online - SegmentNodeStore - Istanza AEM chiusa {#onlinereindexsegmentnodestoreaeminstanceisdown}

Per `SegmentNodeStore` le installazioni è possibile eseguire la reindicizzazione tramite un singolo comando di esecuzione della quercia. Tuttavia, l’istanza di AEM deve essere chiusa.

È possibile attivare la reindicizzazione con il comando seguente:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La differenza tra questo approccio e quello descritto sopra è che la creazione di checkpoint e l&#39;importazione di indice vengono eseguite automaticamente. Il lato negativo è che AEM deve essere disattivato durante il processo.

#### Reindice fuori banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

In questo caso d’uso, potete eseguire la reindicizzazione su una configurazione clonata per ridurre al minimo l’impatto sull’istanza AEM in esecuzione:

1. Creare un checkpoint tramite un&#39;operazione JMX. A tal fine, accedete alla console [](/help/sites-administering/jmx-console.md) JMX e cercate `CheckpointManager`. Quindi, fate clic sull&#39;operazione **createCheckpoint(long p1)** con un valore elevato per la scadenza in secondi (ad esempio, **2592000**).
1. Copiare la `crx-quickstart` cartella in un nuovo computer
1. Esegui reindicizzazione tramite il comando indice di esecuzione della quercia

1. Copiare i file di indice generati nel server AEM

1. Importa i file di indice tramite JMX.

In questo caso di utilizzo, si presume che l&#39;archivio dati sia accessibile in un&#39;altra istanza che potrebbe non essere possibile se `FileDataStore` viene collocato in una soluzione di archiviazione basata su cloud come EBS. Questo esclude lo scenario in cui `FileDataStore` viene clonata. Se la definizione dell&#39;indice non esegue l&#39;indicizzazione full-text, non `DataStore` è necessario accedere a.

## Caso d’uso 4 - Aggiornamento delle definizioni degli indici {#usecase4updatingindexdefinitions}

Al momento, è possibile inviare le modifiche alla definizione dell&#39;indice tramite il pacchetto [ACS Verify Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) . Questo consente la spedizione delle definizioni di indice tramite il pacchetto di contenuto, che successivamente richiede l&#39;esecuzione di una reindicizzazione impostando il `reindex` flag su `true`.

Questo funziona bene per le installazioni più piccole dove la reindicizzazione non richiede molto tempo. Tuttavia, per i depositi molto grandi, la reindicizzazione sarà effettuata in un periodo di tempo molto più ampio. Per questi casi ora è possibile utilizzare gli strumenti indice di esecuzione della quercia.

Oak-run ora supporta la definizione dell&#39;indice in formato JSON e la creazione dell&#39;indice in modalità fuori banda, dove non viene eseguita alcuna modifica su un&#39;istanza live.

Il processo da considerare per questo caso di utilizzo è:

1. Uno sviluppatore aggiorna le definizioni di indice in un&#39;istanza locale e genera quindi un file JSON di definizione indice tramite l&#39; `--index-definitions` opzione

1. Il JSON aggiornato viene quindi fornito all&#39;amministratore di sistema
1. L&#39;amministratore di sistema segue l&#39;approccio fuori banda e prepara l&#39;indice in una diversa installazione
1. Al termine, i file di indice generati verranno importati in un’installazione AEM in esecuzione.

