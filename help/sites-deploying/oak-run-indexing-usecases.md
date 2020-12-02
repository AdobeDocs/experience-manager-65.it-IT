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
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---


# Indicizzazione Oak-run.jar Casi di utilizzo{#oak-run-jar-indexing-use-cases}

Oak-run supporta l&#39;indicizzazione di casi di utilizzo sulla riga di comando senza dover orchestrare l&#39;esecuzione di questi casi di utilizzo tramite AEM console JMX.

I vantaggi generali dell’utilizzo del metodo di comando oak-run.jar index per la gestione degli indici Oak sono:

1. Il comando indice di esecuzione Oak fornisce un nuovo set di strumenti di indicizzazione per AEM 6.4.
1. Il funzionamento dell&#39;Oak riduce il tempo di reindicizzazione, riducendo i tempi di reindicizzazione nei repository più grandi.
1. L&#39;esecuzione Oak riduce il consumo di risorse durante la reindicizzazione in AEM, migliorando nel complesso le prestazioni del sistema.
1. L&#39;esecuzione di Oak fornisce reindicizzazione fuori banda, situazioni di supporto in cui la produzione deve essere disponibile e non può tollerare la manutenzione o i tempi di inattività altrimenti necessari per la reindicizzazione.

Le sezioni seguenti forniscono comandi di esempio. Il comando indice di esecuzione del quercia supporta tutte le impostazioni NodeStore e BlobStore. Gli esempi forniti di seguito indicano le impostazioni con FileDataStore e SegmentNodeStore.

## Caso d&#39;uso 1 - Controllo di coerenza indice {#usercase1indexconsistencycheck}

Questo è un caso d&#39;uso correlato al danneggiamento dell&#39;indice. In alcuni casi non è stato possibile determinare quali indici sono danneggiati. Pertanto,  Adobe ha fornito strumenti che:

1. esegue controlli di coerenza dell&#39;indice su tutti gli indici e fornisce un rapporto su cui gli indici sono validi e che non sono validi;
1. L&#39;utensile è utilizzabile anche se AEM non è accessibile;
1. È facile da usare.

La verifica degli indici danneggiati può essere eseguita tramite l&#39;operazione `--index-consistency-check`:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Questo genererà un report in `indexing-result/index-consistency-check-report.txt`. Per un rapporto campione, vedi sotto:

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

## Caso d&#39;uso 2 - Statistiche indice {#usecase2indexstatistics}

Per diagnosticare alcuni dei casi relativi alle prestazioni della query  Adobe spesso richiedeva la definizione di indice esistente, le statistiche relative all&#39;indice dalla configurazione del cliente. Finora queste informazioni erano sparse su più risorse. Per semplificare la risoluzione dei problemi,  Adobe ha creato strumenti che consentiranno di:

1. Eseguire il dump di tutte le definizioni di indice presenti nel sistema in un unico file JSON;

1. elaborare statistiche importanti dagli indici esistenti;

1. Discarica il contenuto dell&#39;indice per l&#39;analisi offline;

1. Sarà utilizzabile anche se AEM non è accessibile

Le operazioni di cui sopra possono ora essere eseguite tramite i seguenti comandi di indice delle operazioni:

* `--index-info` - Raccoglie e scarica varie statistiche relative agli indici

* `--index-definitions` - Raccoglie e scarica le definizioni degli indici

* `--index-dump` - Contenuto indice Dumps

Di seguito è riportato un esempio di funzionamento pratico dei comandi:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

I report verranno generati in `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Inoltre, gli stessi dettagli vengono forniti tramite la console Web e fanno parte del file ZIP del dump di configurazione. È possibile accedervi nel seguente percorso:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Vantaggi {#uc2benefits}

Questo strumento consente di raccogliere rapidamente tutti i dettagli necessari relativi a problemi di indicizzazione o query e di ridurre il tempo impiegato per estrarre tali informazioni.

## Caso d&#39;uso 3 - Reindicizzazione {#usecase3reindexing}

In base agli [scenari](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), in alcuni casi è necessario eseguire la reindicizzazione. Attualmente la reindicizzazione viene eseguita impostando il flag `reindex` su `true` nel nodo di definizione dell&#39;indice tramite CRXDE o tramite l&#39;interfaccia utente di Gestione indici. Una volta impostato il flag, la reindicizzazione viene eseguita in modo asincrono.

Alcuni punti da notare sulla reindicizzazione:

* La reindicizzazione è molto più lenta nelle impostazioni `DocumentNodeStore` rispetto alle impostazioni `SegmentNodeStore` in cui tutto il contenuto è locale;

* Con la progettazione corrente, mentre viene eseguita la reindicizzazione, l&#39;indicizzatore asincrono viene bloccato e tutti gli altri indici asincrono diventano obsoleti e non ricevono aggiornamenti per la durata dell&#39;indicizzazione. Per questo motivo, se il sistema è in uso, gli utenti potrebbero non visualizzare i risultati aggiornati;
* La reindicizzazione comporta l&#39;attraversamento dell&#39;intero repository, che può comportare un carico elevato sulla configurazione del AEM e quindi avere un impatto sull&#39;esperienza dell&#39;utente finale;
* Per un&#39;installazione `DocumentNodeStore` in cui la reindicizzazione potrebbe richiedere molto tempo, se la connessione al database Mongo non riesce a metà dell&#39;operazione, l&#39;indicizzazione dovrebbe essere riavviata da zero;

* In alcuni casi, l’estrazione del testo può richiedere molto tempo. Questo è specifico per le impostazioni con molti file PDF, dove il tempo impiegato per l’estrazione del testo può influire sui tempi di indicizzazione.

Per raggiungere questi obiettivi, la struttura dell&#39;indice di rovere supporta diverse modalità di reindicizzazione che possono essere utilizzate come necessario. Il comando indice di esecuzione della quercia offre i seguenti vantaggi:

* **reindicizzazione**  fuori banda: la reindicizzazione in rovere può essere effettuata separatamente da una configurazione AEM in esecuzione e, quindi, minimizza l&#39;impatto sull&#39;istanza AEM in uso;

* **reindicizzazione**  out-of-lane - La reindicizzazione avviene senza che si verifichino effetti sulle operazioni di indicizzazione. Ciò significa che l&#39;indicizzatore asincrono può continuare ad indicizzare altri indici;

* **reindicizzazione semplificata per le installazioni**  di DocumentNodeStore - Per  `DocumentNodeStore` le installazioni è possibile eseguire la reindicizzazione con un singolo comando che assicura che la reindicizzazione venga effettuata nel modo migliore;

* **Supporta l&#39;aggiornamento delle definizioni di indice e l&#39;introduzione di nuove definizioni di indice**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Per le installazioni di `DocumentNodeStore` la reindicizzazione può essere effettuata tramite un singolo comando di esecuzione della quercia:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Questo offre i seguenti vantaggi

* Impatto minimo sull&#39;esecuzione delle istanze AEM. La maggior parte delle letture può essere effettuata da server secondari e l&#39;esecuzione AEM cache non viene compromessa a causa di tutta la traversata necessaria per la reindicizzazione;
* Gli utenti possono inoltre fornire un JSON di un indice nuovo o aggiornato tramite l&#39;opzione `--index-definitions-file`.

### Reindex - SegmentNodeStore {#reindexsegmentnodestore}

Per le installazioni `SegmentNodeStore` la reindicizzazione può essere effettuata in uno dei modi seguenti:

#### Reindicizzazione online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Seguire il modo stabilito in cui viene fatta la reindicizzazione tramite l&#39;impostazione del flag `reindex`.

#### Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è in esecuzione {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Per le installazioni di `SegmentNodeStore` solo un processo può accedere ai file dei segmenti in modalità di lettura/scrittura. A causa di ciò, alcune operazioni di indicizzazione delle rovere richiedono ulteriori passaggi manuali.

Ciò implicherebbe quanto segue:

1. Testo del passaggio
1. Collegare l&#39;elemento `oak-run` allo stesso repository utilizzato da AEM in modalità di sola lettura ed eseguire l&#39;indicizzazione. Esempio di come ottenere questo risultato:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Infine, importate i file di indice creati tramite l&#39;operazione `IndexerMBean#importIndex` dal percorso in cui la corsa ha salvato i file di indicizzazione dopo l&#39;esecuzione del comando precedente.

In questo scenario non è necessario arrestare il server AEM o eseguire il provisioning di alcuna nuova istanza. Tuttavia, poiché l&#39;indicizzazione comporta l&#39;attraversamento dell&#39;intero repository, aumenterebbe il carico di I/O sull&#39;installazione, con un impatto negativo sulle prestazioni del runtime.

#### Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è chiusa {#onlinereindexsegmentnodestoreaeminstanceisdown}

Per le installazioni `SegmentNodeStore` è possibile eseguire la reindicizzazione tramite un singolo comando di esecuzione della quercia. Tuttavia, l&#39;istanza AEM deve essere chiusa.

È possibile attivare la reindicizzazione con il comando seguente:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La differenza tra questo approccio e quello descritto sopra è che la creazione di checkpoint e l&#39;importazione di indice vengono eseguite automaticamente. Il lato negativo è che AEM essere giù durante il processo.

#### Reindice fuori banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

In questo caso di utilizzo, potete eseguire la reindicizzazione su una configurazione clonata per ridurre al minimo l&#39;impatto sull&#39;istanza di AEM in esecuzione:

1. Creare un checkpoint tramite un&#39;operazione JMX. A tal fine, accedete alla [console JMX](/help/sites-administering/jmx-console.md) e cercate `CheckpointManager`. Quindi, fare clic sull&#39;operazione **createCheckpoint(long p1)** utilizzando un valore elevato per la scadenza in secondi (ad esempio, **2592000**).
1. Copiare la cartella `crx-quickstart` in un nuovo computer
1. Esegui reindicizzazione tramite il comando indice di esecuzione della quercia

1. Copiare i file di indice generati AEM server

1. Importa i file di indice tramite JMX.

In questo caso d&#39;uso, si presume che l&#39;archivio dati sia accessibile in un&#39;altra istanza che potrebbe non essere possibile se `FileDataStore` è collocato in una soluzione di archiviazione basata su cloud come EBS. Ciò esclude lo scenario in cui viene clonato anche `FileDataStore`. Se la definizione dell&#39;indice non esegue l&#39;indicizzazione full-text, non è necessario accedere a `DataStore`.

## Caso d&#39;uso 4 - Aggiornamento delle definizioni degli indici {#usecase4updatingindexdefinitions}

Attualmente, è possibile inviare le modifiche alla definizione dell&#39;indice tramite il pacchetto [ACS Verify Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Questo consente la spedizione delle definizioni di indice tramite il pacchetto di contenuto, che successivamente richiede l&#39;esecuzione di reindicizzazione impostando il flag `reindex` su `true`.

Questo funziona bene per le installazioni più piccole in cui la reindicizzazione non richiede molto tempo. Tuttavia, per i depositi molto grandi, la reindicizzazione sarà effettuata in un periodo di tempo molto più ampio. Per questi casi ora è possibile utilizzare gli strumenti indice di esecuzione della quercia.

Oak-run ora supporta la definizione dell&#39;indice in formato JSON e la creazione dell&#39;indice in modalità fuori banda, dove non viene eseguita alcuna modifica su un&#39;istanza live.

Il processo da considerare per questo caso di utilizzo è:

1. Uno sviluppatore aggiorna le definizioni di indice in un&#39;istanza locale e quindi genera un file JSON di definizione indice tramite l&#39;opzione `--index-definitions`

1. Il JSON aggiornato viene quindi fornito all&#39;amministratore di sistema
1. L&#39;amministratore di sistema segue l&#39;approccio fuori banda e prepara l&#39;indice in una diversa installazione
1. Una volta completato, i file di indice generati verranno importati in un&#39;installazione AEM in esecuzione.

