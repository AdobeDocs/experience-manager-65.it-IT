---
title: Casi d'uso dell'indicizzazione Oak-run.jar
seo-title: Oak-run.jar Indexing Use Cases
description: Scopri i vari casi utente per l’esecuzione dell’indicizzazione con lo strumento Oak-run.
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Casi d&#39;uso dell&#39;indicizzazione Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run supporta i casi di utilizzo dell’indicizzazione sulla riga di comando senza dover orchestrare l’esecuzione di questi casi d’uso tramite AEM console JMX.

I vantaggi principali dell&#39;utilizzo dell&#39;approccio del comando oak-run.jar index per la gestione degli indici Oak sono i seguenti:

1. Il comando Oak-run index fornisce un nuovo set di strumenti di indicizzazione per AEM 6.4.
1. Oak-run diminuisce il time-to-reindex che riduce i tempi di reindicizzazione su archivi più grandi.
1. Oak-run riduce il consumo di risorse durante la reindicizzazione in AEM, ottenendo prestazioni del sistema complessivamente migliori.
1. Oak-run fornisce reindicizzazione fuori banda, situazioni di supporto in cui la produzione deve essere disponibile e non può tollerare manutenzione o tempi di inattività altrimenti necessari per reindicizzare.

Le sezioni seguenti forniscono comandi di esempio. Il comando oak-run index supporta tutte le impostazioni NodeStore e BlobStore. Gli esempi forniti di seguito sono intorno alle configurazioni con FileDataStore e SegmentNodeStore.

## Caso d’uso 1 - Controllo di coerenza dell’indice {#usercase1indexconsistencycheck}

Questo è un caso d&#39;uso relativo alla corruzione dell&#39;indice. In alcuni casi non è stato possibile determinare quale degli indici è corrotto. Pertanto, l’Adobe ha fornito strumenti che:

1. Esegue controlli di coerenza dell&#39;indice su tutti gli indici e fornisce un rapporto in cui gli indici sono validi e non sono validi;
1. La lavorazione è utilizzabile anche se AEM non è accessibile;
1. È facile da usare.

La verifica degli indici corrotti può essere eseguita tramite `--index-consistency-check` funzionamento:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Verrà generato un rapporto in `indexing-result/index-consistency-check-report.txt`. Di seguito è riportato un esempio di rapporto:

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

Il supporto e l&#39;amministratore di sistema possono ora utilizzare questo strumento per determinare rapidamente quali indici sono corrotti e quindi reindicizzarli.

## Caso d&#39;uso 2 - Statistiche dell&#39;indice {#usecase2indexstatistics}

Per diagnosticare alcuni dei casi relativi all&#39;Adobe delle prestazioni della query spesso richiedeva la definizione di indice esistente, le statistiche relative all&#39;indice dalla configurazione del cliente. Finora queste informazioni sono state sparse tra più risorse. Per semplificare la risoluzione dei problemi, Adobe ha creato strumenti che consentono di:

1. Eseguire il dump di tutta la definizione dell&#39;indice presente sul sistema in un unico file JSON;

1. elaborare statistiche importanti dagli indici esistenti;

1. Contenuto dell&#39;indice di dump per l&#39;analisi offline;

1. Sarà utilizzabile anche se AEM non è accessibile

Le operazioni di cui sopra possono ora essere eseguite tramite i seguenti comandi dell&#39;indice delle operazioni:

* `--index-info` - Raccoglie e scarica varie statistiche relative agli indici

* `--index-definitions` - Raccoglie e scarica le definizioni degli indici

* `--index-dump` - Contenuto dell&#39;indice dei dump

Di seguito è riportato un esempio di funzionamento pratico dei comandi:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

I rapporti vengono generati in `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Inoltre, gli stessi dettagli vengono forniti tramite la console Web e faranno parte dello zip di dump della configurazione. È possibile accedervi nel seguente percorso:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Vantaggi {#uc2benefits}

Questo strumento consente di raccogliere rapidamente tutti i dettagli richiesti relativi all’indicizzazione o ai problemi di query e di ridurre il tempo impiegato per l’estrazione di tali informazioni.

## Caso d&#39;uso 3 - Reindicizzazione {#usecase3reindexing}

A seconda del [scenari](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), in alcuni casi è necessario eseguire la reindicizzazione. Attualmente la reindicizzazione viene effettuata impostando il `reindex` flag to `true` nel nodo di definizione dell&#39;indice tramite CRXDE o tramite l&#39;interfaccia utente di Index Manager. Una volta impostato il flag, la reindicizzazione viene eseguita in modo asincrono.

Alcuni punti da notare sulla reindicizzazione:

* La reindicizzazione è molto più lenta su `DocumentNodeStore` impostazioni rispetto a `SegmentNodeStore` configurazioni in cui tutti i contenuti sono locali;

* Con la progettazione corrente, mentre la reindicizzazione avviene l&#39;indicizzatore asincrono è bloccato e tutti gli altri indici asincroni diventano obsoleti e non ricevono aggiornamenti per la durata dell&#39;indicizzazione. Per questo motivo, se il sistema è in uso, gli utenti potrebbero non vedere i risultati aggiornati;
* La reindicizzazione comporta l&#39;attraversamento dell&#39;intero archivio che può caricare un elevato carico sulla configurazione AEM e quindi influire sull&#39;esperienza dell&#39;utente finale;
* Per `DocumentNodeStore` installazione in cui la reindicizzazione potrebbe richiedere molto tempo, se la connessione al database Mongo non riesce nel mezzo dell&#39;operazione, l&#39;indicizzazione dovrebbe essere riavviata da zero;

* In alcuni casi la reindicizzazione può richiedere molto tempo a causa dell’estrazione del testo. Questo è specifico principalmente per le configurazioni con molti file PDF, dove il tempo trascorso sull’estrazione del testo può influire sul tempo di indicizzazione.

Per raggiungere questi obiettivi, gli strumenti dell&#39;indice oak-run supportano diverse modalità di reindicizzazione che possono essere utilizzate come richiesto. Il comando oak-run index fornisce i seguenti vantaggi:

* **reindicizzazione fuori banda** - la reindicizzazione oak-run può essere effettuata separatamente da una configurazione AEM in esecuzione e quindi riduce al minimo l&#39;impatto sull&#39;istanza AEM in uso;

* **reindicizzazione fuori corsia** - La reindicizzazione avviene senza influire sulle operazioni di indicizzazione. Ciò significa che l&#39;indicizzatore asincrono può continuare ad indicizzare altri indici;

* **Reindicizzazione semplificata per le installazioni di DocumentNodeStore** - Per `DocumentNodeStore` installazioni, reindicizzazione può essere effettuata con un unico comando che assicura che la reindicizzazione sia effettuata nel modo più ottimale;

* **Supporta l&#39;aggiornamento delle definizioni degli indici e l&#39;introduzione di nuove definizioni degli indici**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Per `DocumentNodeStore` le installazioni di reindicizzazione possono essere effettuate tramite un singolo comando oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Ciò offre i seguenti vantaggi

* Impatto minimo sull’esecuzione delle istanze AEM. La maggior parte delle letture può essere effettuata da server secondari e l&#39;esecuzione di cache AEM non è compromessa a causa di tutti gli attraversamenti necessari per la reindicizzazione;
* Gli utenti possono anche fornire un JSON di un indice nuovo o aggiornato tramite `--index-definitions-file` opzione .

### Reindicizzazione - SegmentNodeStore {#reindexsegmentnodestore}

Per `SegmentNodeStore` le installazioni di reindicizzazione possono essere eseguite in uno dei seguenti modi:

#### Reindicizzazione online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Seguire il modo stabilito in cui viene fatta la reindicizzazione tramite l&#39;impostazione `reindex` bandiera.

#### Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è in esecuzione {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Per `SegmentNodeStore` installa un solo processo che può accedere ai file dei segmenti in modalità di lettura-scrittura. A causa di questo alcune operazioni nell&#39;indicizzazione oak-run richiedono ulteriori passaggi manuali.

Ciò implica quanto segue:

1. Testo del passaggio
1. Collega `oak-run` allo stesso archivio utilizzato da AEM in modalità di sola lettura ed esegui l&#39;indicizzazione. Un esempio su come ottenere questo risultato:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Infine, importa i file di indice creati tramite il `IndexerMBean#importIndex` dal percorso in cui oak-run ha salvato i file di indicizzazione dopo aver eseguito il comando precedente.

In questo scenario non è necessario arrestare il server AEM o eseguire il provisioning di una nuova istanza. Tuttavia, poiché l’indicizzazione comporta l’attraversamento dell’intero archivio, aumenterebbe il carico di I/O sull’installazione, influendo negativamente sulle prestazioni di runtime.

#### Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è chiusa {#onlinereindexsegmentnodestoreaeminstanceisdown}

Per `SegmentNodeStore` le installazioni di reindicizzazione possono essere effettuate tramite un singolo comando oak-run. Tuttavia, l&#39;istanza AEM deve essere chiusa.

Puoi attivare la reindicizzazione con il seguente comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La differenza tra questo approccio e quello illustrato sopra è che la creazione di punti di controllo e l&#39;importazione di indici vengono eseguite automaticamente. Il rovescio della medaglia è che AEM essere fuori servizio durante il processo.

#### Reindice fuori banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

In questo caso d’uso, puoi eseguire la reindicizzazione su una configurazione clonata per ridurre al minimo l’impatto sull’istanza AEM in esecuzione:

1. Crea un checkpoint tramite un’operazione JMX. Per farlo, vai al [Console JMX](/help/sites-administering/jmx-console.md) e cerca `CheckpointManager`. Quindi, fai clic sul pulsante **createCheckpoint(long p1)** utilizzo di un valore elevato per la scadenza in secondi (ad esempio, **2592000**).
1. Copia il `crx-quickstart` cartella in un nuovo computer
1. Esegui reindicizzazione tramite il comando oak-run index

1. Copia i file di indice generati AEM server

1. Importa i file di indice tramite JMX.

In questo caso d’uso, si presume che l’archivio dati sia accessibile in un’altra istanza che potrebbe non essere possibile se `FileDataStore` è posizionato su una soluzione di storage basata su cloud come EBS. Questo esclude lo scenario in cui `FileDataStore` è anche clonato. Se la definizione dell&#39;indice non esegue l&#39;indicizzazione full-text, accedi a `DataStore` non è obbligatorio.

## Caso d&#39;uso 4 - Aggiornamento delle definizioni degli indici {#usecase4updatingindexdefinitions}

Attualmente, puoi inviare le modifiche alla definizione dell&#39;indice tramite [ACS Assicurare l&#39;indice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) pacchetto. Questo consente la spedizione delle definizioni dell&#39;indice tramite il pacchetto di contenuti che successivamente richiede la reindicizzazione tramite l&#39;impostazione del `reindex` flag to `true`.

Questo funziona bene per installazioni più piccole in cui la reindicizzazione non richiede molto tempo. Tuttavia, per archivi molto grandi, la reindicizzazione sarà fatta in un periodo di tempo molto più ampio. Per questi casi ora possiamo utilizzare gli strumenti dell&#39;indice oak-run.

Oak-run ora supporta la fornitura di definizioni di indice in formato JSON e la creazione di indici in modalità fuori banda in cui non vengono eseguite modifiche su un&#39;istanza live.

Il processo da considerare per questo caso d’uso è il seguente:

1. Uno sviluppatore aggiorna le definizioni dell’indice su un’istanza locale e quindi genera un file JSON di definizione dell’indice tramite il `--index-definitions` opzione

1. Il JSON aggiornato viene quindi consegnato all’amministratore di sistema
1. L&#39;amministratore di sistema segue l&#39;approccio fuori banda e prepara l&#39;indice in un&#39;installazione diversa
1. Una volta completato, i file di indice generati verranno importati in un&#39;installazione AEM in esecuzione.
