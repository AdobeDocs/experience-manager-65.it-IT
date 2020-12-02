---
title: Risoluzione dei problemi relativi agli indici Oak
seo-title: Risoluzione dei problemi relativi agli indici Oak
description: Come rilevare e correggere la reindicizzazione lenta.
seo-description: Come rilevare e correggere la reindicizzazione lenta.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---


# Risoluzione dei problemi relativi agli indici Oak{#troubleshooting-oak-indexes}

## Riindicizzazione lenta {#slow-re-indexing}

AEM processo interno di reindicizzazione raccoglie i dati del repository e li memorizza negli indici Oak per supportare la query del contenuto da parte degli esecutori. In circostanze eccezionali, il processo può diventare lento o addirittura bloccato. Questa pagina funge da guida alla risoluzione dei problemi per identificare se l’indicizzazione è lenta, individuare la causa e risolvere il problema.

È importante distinguere tra reindicizzazione che richiede un tempo eccessivamente lungo e reindicizzazione che richiede molto tempo, perché indicizza grandi quantità di contenuto. Ad esempio, il tempo necessario per indicizzare le dimensioni dei contenuti in base alla quantità di contenuto, pertanto i repository di produzione di grandi dimensioni richiederanno più tempo per reindicizzarsi rispetto ai repository di sviluppo di piccole dimensioni.

Per ulteriori informazioni su quando e come reindicizzare il contenuto, vedere le [Best Practices on Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Rilevamento iniziale {#initial-detection}

L&#39;indicizzazione lenta del rilevamento iniziale richiede la revisione dei MBean `IndexStats` JMX. Nell’istanza AEM interessata, effettuate le seguenti operazioni:

1. Aprite la console Web e fate clic sulla scheda JMX oppure andate a https://&lt;host>:&lt;porta>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Passare ai fagioli `IndexStats`.
1. Aprire i `IndexStats` MBeans per &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Per entrambi gli MBeans, verificare che la marca temporale **Done** e la marca temporale **LastIndexTime** siano inferiori a 45 minuti dall&#39;ora corrente.

1. Per MBean, se il valore di tempo (**Done** o **LastIndexedTime**) è maggiore di 45 minuti dall&#39;ora corrente, il processo di indice non riesce o richiede troppo tempo. Questo causa l&#39;insufficienza degli indici asincroni.

## L&#39;indicizzazione viene messa in pausa dopo una chiusura forzata {#indexing-is-paused-after-a-forced-shutdown}

Una chiusura forzata comporta AEM sospensione dell&#39;indicizzazione asincrona fino a 30 minuti dopo il riavvio e in genere richiede altri 15 minuti per completare la prima passata di reindicizzazione, per un totale di circa 45 minuti (collegando nuovamente la [Rilevamento iniziale](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) con un periodo di 45 minuti). Nel caso in cui sospettate che l&#39;indicizzazione venga messa in pausa dopo un arresto forzato:

1. In primo luogo, determinare se l&#39;istanza di AEM è stata chiusa in modo forzato (il processo di AEM è stato ucciso con la forza, o si è verificato un errore di alimentazione) e successivamente riavviata.

   * [AEM ](/help/sites-deploying/configure-logging.md) login può essere rivisto a tal fine.

1. Se l&#39;arresto forzato si è verificato, al riavvio AEM sospende automaticamente la reindicizzazione per un massimo di 30 minuti.
1. Attendete circa 45 minuti affinché AEM riprendere le normali operazioni di indicizzazione asincrona.

## Pool di thread sovraccarico {#thread-pool-overloaded}

>[!NOTE]
>
>Per AEM 6.1, assicurarsi che sia installato [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html).

In circostanze eccezionali, il pool di thread utilizzato per gestire l&#39;indicizzazione asycronica potrebbe venire sovraccaricato. Per isolare il processo di indicizzazione, è possibile configurare un pool di thread in modo da impedire ad altri AEM di interferire con la capacità di Oak di indicizzare i contenuti in modo tempestivo. A tal fine, è necessario:

1. Definite un nuovo pool di thread isolato per l&#39;Utilità di pianificazione Apache Sling da utilizzare per l&#39;indicizzazione asincrona:

   * Nell&#39;istanza AEM interessata, accedete AEM console Web OSGi>OSGi>Configuration>Apache Sling Scheduler oppure andate a https://&lt;host>:&lt;porta>/system/console/configMgr (ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Aggiungete una voce al campo &quot;Consentite Thread Pools&quot; con il valore &quot;Oak&quot;.
   * Fate clic su Salva in basso a destra per salvare le modifiche.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verificate che il nuovo pool di thread Apache Sling Scheduler sia registrato e venga visualizzato nella console Web Apache Sling Scheduler Satus.

   * Passate alla console Web OSGi AEM>Stato>Programmazione Sling oppure andate a https://&lt;host>:&lt;porta>/system/console/status-slingscheduler (ad esempio, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verificare che siano presenti le seguenti voci del pool:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La coda di osservazione è piena {#observation-queue-is-full}

Se in poco tempo vengono apportate troppe modifiche e impegni al repository, l&#39;indicizzazione può essere ritardata a causa di una coda di osservazione completa. In primo luogo, determinare se la coda di osservazione è piena:

1. Andate alla console Web e fate clic sulla scheda JMX oppure andate a https://&lt;host>:&lt;porta>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Aprite le statistiche dell&#39;archivio quercia MBean e stabilite se un qualsiasi valore `ObservationQueueMaxLength` è maggiore di 10.000.

   * Nelle operazioni normali, questo valore massimo deve sempre essere ridotto a zero (in particolare nella sezione `per second`), per verificare che le metriche dei secondi di `ObservationQueueMaxLength` siano pari a 0.
   * Se i valori sono 10.000 o più e aumentano costantemente, ciò indica che almeno una (possibilmente più) coda non può essere elaborata con la stessa velocità con cui si verificano nuove modifiche (commit).
   * Ogni coda di osservazione ha un limite (per impostazione predefinita, 10.000) e, se la coda raggiunge tale limite, l&#39;elaborazione diminuisce.
   * Quando si utilizza MongoMK, mentre le lunghezze delle code aumentano, le prestazioni della cache Oak interna diminuiscono. Questa correlazione è visibile in una `missRate` aumentata per la cache `DocChildren` nella `Consolidated Cache` statistica MBean.

1. Per evitare di superare i limiti accettabili della coda di osservazione, si raccomanda di:

   * Abbassa la velocità costante delle virgole. Picchi brevi in virgole sono accettabili, ma la velocità costante dovrebbe essere ridotta.
   * Aumentare le dimensioni della `DiffCache` come descritto in [Suggerimenti per l&#39;ottimizzazione delle prestazioni > Ottimizzazione dell&#39;archiviazione del Mongo > Dimensione della cache del documento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3).

## Identificazione e risoluzione di un processo di reindicizzazione bloccato {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindicizzazione può essere considerata &quot;completamente bloccata&quot; in due condizioni:

* Il reindicizzazione è molto lento, al punto in cui non viene segnalato alcun progresso significativo nei file di registro riguardo al numero di nodi attraversati.

   * Ad esempio, se non ci sono messaggi nel corso di un&#39;ora, o se l&#39;avanzamento è così lento che ci vorrà una settimana o più per terminare.

* La reindicizzazione viene bloccata in un ciclo infinito se nei file di registro (ad esempio, `OutOfMemoryException`) vengono visualizzate eccezioni ripetute nel thread di indicizzazione. La ripetizione delle stesse eccezioni nel registro indica che Oak tenta di indicizzare ripetutamente la stessa cosa, ma non riesce sullo stesso problema.

Per identificare e correggere un processo di reindicizzazione bloccato, effettuare le seguenti operazioni:

1. Per identificare la causa dell’indicizzazione bloccata, è necessario raccogliere le seguenti informazioni:

   * Raccogliere 5 minuti di dump del thread, un dump del thread ogni 2 secondi.
   * [Impostare il livello DEBUG e i registri per le appendici](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Raccogli dati da `IndexStats` MBean asincrono:

      * Passa a AEM console Web OSGi>Principale>JMX>IndexStat>asincrono

         oppure andate alla pagina [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Utilizzare la modalità console [oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) per raccogliere i dettagli di ciò che esiste sotto il nodo * `/:async`*.
   * Raccogli un elenco di checkpoint del repository utilizzando il file `CheckpointManager` MBean:

      * AEM console Web OSGi>Principale>JMX>CheckpointManager>listCheckpoint()

         oppure andate alla pagina [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Dopo aver raccolto tutte le informazioni descritte nel passaggio 1, riavviare AEM.

   * Il riavvio del AEM può risolvere il problema in caso di un carico concorrente elevato (overflow della coda di osservazione o qualcosa di simile).
   * Se il riavvio non risolve il problema, aprire un problema con l&#39;Assistenza clienti [ Adobe](https://helpx.adobe.com/it/marketing-cloud/contact-support.html) e fornire tutte le informazioni raccolte al passaggio 1.

## Riindicizzazione asincrona in modo sicuro {#safely-aborting-asynchronous-re-indexing}

È possibile interrompere la reindicizzazione in modo sicuro (interromperla prima del completamento) tramite le corsie di indicizzazione `async, async-reindex`e f `ulltext-async` ( `IndexStats` Mava). Per ulteriori informazioni, consulta anche la documentazione Apache Oak su [Come interrompere la reindicizzazione](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Inoltre, prendere in considerazione che:

* La reindicizzazione degli indici di proprietà Lucene e Lucene può essere interrotta in quanto sono naturalmente asycronici.
* Il reindicizzazione degli indici delle proprietà Oak può essere interrotto solo se il reindicizzazione è stato avviato tramite `PropertyIndexAsyncReindexMBean`.

Per interrompere la reindicizzazione in modo sicuro, procedere come segue:

1. Identificare l&#39;MBean IndexStats che controlla la corsia di reindicizzazione da arrestare.

   * Andate alla console JMX relativa a IndexStats MBean tramite AEM console OSGi Web Console>Principale>JMX o https://&lt;host>:&lt;porta>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Aprire l&#39;MBean IndexStats in base alla corsia di reindicizzazione che si desidera arrestare ( `async`, `async-reindex` o `fulltext-async`)

      * Per identificare la corsia appropriata e quindi l&#39;istanza MBean IndexStats, osservare la proprietà &quot;asincrona&quot; degli indici Oak. La proprietà &quot;asincrona&quot; conterrà il nome della corsia: `async`, `async-reindex` o `fulltext-async`.
      * La corsia è disponibile anche accedendo AEM Gestione indici nella colonna &quot;Async&quot;. Per accedere al gestore indice, passare a Operazioni>Diagnosi>Gestione indice.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Richiamate il comando `abortAndPause()` nel file `IndexStats` MBean appropriato.
1. Contrassegnate la definizione dell&#39;indice Oak in modo appropriato per impedire la ripresa della reindicizzazione quando la corsia di indicizzazione riprende.

   * Quando si reindicizza un indice **esistente**, impostare la proprietà reindex su false

      * `/oak:index/someExistingIndex@reindex=false`
   * Oppure, per un indice **new**:

      * Impostare la proprietà type su disabled

         * `/oak:index/someNewIndex@type=disabled`
      * o rimuovere completamente la definizione di indice

   Al termine, inviate le modifiche alla directory archivio.

1. Infine, riprendere l&#39;indicizzazione asycronica sulla corsia di indicizzazione interrotta.

   * In `IndexStats` MBean che ha emesso il comando `abortAndPause()` nel passaggio 2, richiamare il comando `resume()`.

## Impedire la reindicizzazione lenta {#preventing-slow-re-indexing}

È consigliabile reindicizzare durante i periodi di inattività (ad esempio, non durante un caricamento di contenuti di grandi dimensioni), e idealmente durante le finestre di manutenzione quando AEM carico è noto e controllato. Inoltre, accertarsi che la reindicizzazione non abbia luogo durante altre attività di manutenzione.
