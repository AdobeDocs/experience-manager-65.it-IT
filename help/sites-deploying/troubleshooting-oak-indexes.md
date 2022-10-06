---
title: Risoluzione dei problemi degli indici Oak
seo-title: Troubleshooting Oak Indexes
description: Come rilevare e correggere la reindicizzazione lenta.
seo-description: How to detect and fix slow re-indexing.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# Risoluzione dei problemi degli indici Oak{#troubleshooting-oak-indexes}

## Re-indicizzazione lenta  {#slow-re-indexing}

AEM processo di reindicizzazione interna raccoglie i dati del repository e li memorizza negli indici Oak per supportare la query performante del contenuto. In circostanze eccezionali, il processo può diventare lento o addirittura bloccato. Questa pagina funge da guida alla risoluzione dei problemi per identificare se l’indicizzazione è lenta, trovare la causa e risolvere il problema.

È importante distinguere tra la reindicizzazione che richiede un tempo inappropriato e la reindicizzazione che richiede molto tempo perché sta indicizzando grandi quantità di contenuto. Ad esempio, il tempo necessario per indicizzare il contenuto viene ridimensionato in base alla quantità di contenuto, quindi la reindicizzazione degli archivi di produzione di grandi dimensioni richiederà più tempo rispetto ai piccoli archivi di sviluppo.

Consulta la sezione [Tecniche consigliate per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md) per ulteriori informazioni su quando e come reindicizzare il contenuto.

## Rilevamento iniziale {#initial-detection}

L&#39;indicizzazione lenta del rilevamento iniziale richiede la revisione `IndexStats` MBeans JMX. Nell’istanza AEM interessata, procedi come segue:

1. Apri la console Web e fai clic sulla scheda JMX oppure vai a https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Passa a `IndexStats` Fagioli.
1. Apri `IndexStats` MBeans for &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Per entrambi i MBeans, controlla se il **Fine** timestamp e **LastIndexTime** le marche temporali sono inferiori a 45 minuti dall’ora corrente.

1. Per MBean, se il valore del tempo (**Fine** o **LastIndexedTime**) è maggiore di 45 minuti dall&#39;ora corrente, quindi il processo di indicizzazione non riesce o richiede troppo tempo. Questo causa l’obsolescenza degli indici asincroni.

## L&#39;indicizzazione viene sospesa dopo un arresto forzato {#indexing-is-paused-after-a-forced-shutdown}

Un arresto forzato comporta AEM sospensione dell&#39;indicizzazione asincrona per un massimo di 30 minuti dopo il riavvio e in genere richiede altri 15 minuti per completare il primo passaggio di reindicizzazione, per un totale di circa 45 minuti (collegamento al [Rilevamento iniziale](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) arco temporale di 45 minuti). Nel caso in cui si sospetti che l&#39;indicizzazione venga sospesa dopo uno spegnimento forzato:

1. In primo luogo, determinare se l&#39;istanza AEM è stata chiusa in modo forzato (il processo di AEM è stato ucciso con la forza o si è verificato un guasto elettrico) e successivamente riavviata.

   * [Registrazione AEM](/help/sites-deploying/configure-logging.md) possono essere esaminati a tal fine.

1. Se l&#39;arresto forzato si è verificato, al riavvio, AEM automaticamente sospende la reindicizzazione per un massimo di 30 minuti.
1. Attendi circa 45 minuti per AEM riprendere le normali operazioni di indicizzazione asincrona.

## Pool di thread sovraccaricato {#thread-pool-overloaded}

>[!NOTE]
>
>Per AEM 6.1, assicurati che [AEM 6.1 PCP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) è installato.

In circostanze eccezionali, il pool di thread utilizzato per gestire l&#39;indicizzazione asincrona può diventare sovraccarico. Al fine di isolare il processo di indicizzazione, un pool di thread può essere configurato per evitare che altri lavori AEM interferiscano con la capacità di Oak di indicizzare il contenuto in modo tempestivo. A questo scopo, devi:

1. Definisci un nuovo pool di thread isolato per Apache Sling Scheduler da utilizzare per l&#39;indicizzazione asincrona:

   * Nell&#39;istanza AEM interessata, accedi AEM Console Web OSGi>OSGi>Configurazione>Modulo di pianificazione Apache Sling o vai su https://&lt;host>:&lt;port>/system/console/configMgr (ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Aggiungi una voce al campo &quot;Pool di thread consentiti&quot; con il valore di &quot;oak&quot;.
   * Fai clic su Salva in basso a destra per salvare le modifiche.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verifica che il nuovo pool di thread Apache Sling Scheduler sia registrato e visualizzato nella console web Apache Sling Scheduler Satus.

   * Passa alla console Web OSGi AEM>Stato>Utilità di pianificazione Sling oppure vai a https://&lt;host>:&lt;port>/system/console/status-slingscheduler (ad esempio, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verifica che siano presenti le seguenti voci del pool:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La coda di osservazione è piena {#observation-queue-is-full}

Se vengono apportate troppe modifiche e commit all&#39;archivio in un breve periodo di tempo, l&#39;indicizzazione può essere ritardata a causa di una coda di osservazione completa. In primo luogo, determinare se la coda di osservazione è piena:

1. Vai alla Console web e fai clic sulla scheda JMX o vai a https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Apri l&#39;MBean delle statistiche dell&#39;archivio Oak e stabilisci se esiste `ObservationQueueMaxLength` è maggiore di 10.000.

   * Nelle operazioni normali, questo valore massimo deve sempre ridursi a zero (in particolare `per second` in modo da verificare che `ObservationQueueMaxLength`Le metriche dei secondi sono 0.
   * Se i valori sono pari o superiori a 10.000 e aumentano costantemente, ciò indica che almeno una (possibilmente più) coda non può essere elaborata con la stessa velocità con cui si verificano nuove modifiche (commit).
   * Ogni coda di osservazione ha un limite (10.000 per impostazione predefinita) e, se la coda raggiunge tale limite, l’elaborazione diminuisce.
   * Quando si utilizza MongoMK, quando le lunghezze di coda aumentano, le prestazioni interne della cache Oak si riducono. Questa correlazione può essere vista in un `missRate` per `DocChildren` nella cache `Consolidated Cache` statistiche MBean.

1. Per evitare di superare i limiti accettabili della coda di osservazione, si raccomanda di:

   * Ridurre la frequenza costante di commit. I picchi brevi nei commit sono accettabili, ma il tasso costante dovrebbe essere ridotto.
   * Aumenta le dimensioni del `DiffCache` come descritto in [Suggerimenti per l&#39;ottimizzazione delle prestazioni > Ottimizzazione archiviazione Mongo > Dimensione della cache del documento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3).

## Identificazione e correzione di un processo di reindicizzazione bloccato {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindicizzazione può essere considerata &quot;completamente bloccata&quot; in due condizioni:

* La reindicizzazione è molto lenta, al punto in cui non viene riportato alcun progresso significativo nei file di log riguardo al numero di nodi attraversati.

   * Ad esempio, se non ci sono messaggi nel corso di un’ora o se il progresso è così lento che ci vorrà una settimana o più per terminare.

* La reindicizzazione è bloccata in un ciclo infinito se nei file di log vengono visualizzate eccezioni ripetute (ad esempio, `OutOfMemoryException`) nel thread di indicizzazione. La ripetizione delle stesse eccezioni nel registro indica che Oak tenta di indicizzare ripetutamente la stessa cosa, ma non riesce sullo stesso problema.

Per identificare e correggere un processo di reindicizzazione bloccato, procedi come segue:

1. Per identificare la causa dell’indicizzazione bloccata, è necessario raccogliere le seguenti informazioni:

   * Raccogliere 5 minuti di dump di thread, un dump di thread ogni 2 secondi.
   * [Imposta il livello DEBUG e i registri per gli appendici](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Raccogliere dati dall&#39;asincrono `IndexStats` MBean:

      * Passa a AEM Console web OSGi>Principale>JMX>IndexStat>async

         o vai a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Utilizzo [modalità console di oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) per raccogliere i dettagli di ciò che esiste sotto il * `/:async`* nodo.
   * Raccogli un elenco di punti di controllo del repository utilizzando `CheckpointManager` MBean:

      * Console Web OSGi AEM>Principale>JMX>CheckpointManager>listCheckpoints()

         o vai a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Dopo aver raccolto tutte le informazioni descritte nel passaggio 1, riavviare AEM.

   * Il riavvio del AEM può risolvere il problema nel caso di un carico concomitante elevato (overflow della coda di osservazione o qualcosa di simile).
   * Se un riavvio non risolve il problema, apri un problema con [Adobe Customer Care](https://helpx.adobe.com/it/marketing-cloud/contact-support.html) e fornire tutte le informazioni raccolte nel passaggio 1.

## Riindicizzazione asincrona interrotta in modo sicuro {#safely-aborting-asynchronous-re-indexing}

La reindicizzazione può essere interrotta in modo sicuro (interrotta prima del completamento) tramite il `async, async-reindex`e f `ulltext-async` corsie di indicizzazione ( `IndexStats` Mbean). Per ulteriori informazioni, consulta anche la documentazione di Apache Oak su [Come interrompere la reindicizzazione](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Inoltre, prendere in considerazione che:

* La reindicizzazione degli indici delle proprietà Lucene e Lucene può essere interrotta in quanto sono naturalmente asincroni.
* La reindicizzazione degli indici delle proprietà Oak può essere interrotta solo se la reindicizzazione è stata avviata tramite il `PropertyIndexAsyncReindexMBean`.

Per interrompere in modo sicuro la reindicizzazione, segui questi passaggi:

1. Identificare la MBean IndexStats che controlla la corsia di reindicizzazione che deve essere arrestata.

   * Passa alla MBean IndexStats appropriata tramite la console JMX andando alla console OSGi Web Console>Principale>JMX o https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Apri la MBean IndexStats in base alla corsia di reindicizzazione che desideri arrestare ( `async`, `async-reindex`oppure `fulltext-async`)

      * Per identificare la corsia appropriata e quindi l&#39;istanza MBean IndexStats, controlla la proprietà &quot;async&quot; degli indici Oak. La proprietà &quot;async&quot; conterrà il nome della corsia: `async`, `async-reindex`oppure `fulltext-async`.
      * La corsia è disponibile anche accedendo a AEM Index Manager nella colonna &quot;Async&quot;. Per accedere al Gestore indici, passa a Operazioni > Diagnosi>Gestione indici.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Richiama il `abortAndPause()` sul comando appropriato `IndexStats` MBean.
1. Contrassegna la definizione dell&#39;indice Oak in modo appropriato per impedire la ripresa della reindicizzazione quando la corsia di indicizzazione riprende.

   * Durante la reindicizzazione di un **esistente** index, imposta la proprietà reindex su false

      * `/oak:index/someExistingIndex@reindex=false`
   * Oppure, per un **nuovo** indice:

      * Imposta la proprietà type su disabled

         * `/oak:index/someNewIndex@type=disabled`
      * o rimuovere completamente la definizione dell&#39;indice

   Al termine, conferma le modifiche all’archivio.

1. Infine, riprendere l&#39;indicizzazione asincrona sulla corsia di indicizzazione interrotta.

   * In `IndexStats` MBean che ha emesso il `abortAndPause()` nel passaggio 2, richiamare il `resume()`comando.

## Impedire la reindicizzazione lenta {#preventing-slow-re-indexing}

È meglio reindicizzare durante i periodi di inattività (ad esempio, non durante un caricamento di contenuti di grandi dimensioni) e idealmente durante le finestre di manutenzione quando il caricamento AEM è noto e controllato. Inoltre, assicurati che la reindicizzazione non avvenga durante altre attività di manutenzione.
