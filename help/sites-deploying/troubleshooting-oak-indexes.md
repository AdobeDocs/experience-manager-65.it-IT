---
title: Risoluzione dei problemi degli indici Oak
seo-title: Troubleshooting Oak Indexes
description: Come rilevare e correggere la reindicizzazione lenta.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 2%

---

# Risoluzione dei problemi degli indici Oak{#troubleshooting-oak-indexes}

## Reindicizzazione lenta  {#slow-re-indexing}

Il processo di reindicizzazione interno dell’AEM raccoglie i dati dell’archivio e li memorizza negli indici Oak per supportare l’esecuzione di query sui contenuti. In circostanze eccezionali, il processo può diventare lento o addirittura bloccato. Questa pagina funge da guida alla risoluzione dei problemi per identificare se l’indicizzazione è lenta, individuare la causa e risolvere il problema.

È importante distinguere tra la reindicizzazione che richiede una quantità di tempo inappropriatamente lunga e la reindicizzazione che richiede una quantità di tempo molto lunga perché si tratta di indicizzare grandi quantità di contenuto. Ad esempio, il tempo necessario per indicizzare il contenuto corrisponde alla quantità di contenuto, pertanto la reindicizzazione dei grandi archivi di produzione richiede più tempo rispetto alla reindicizzazione dei piccoli archivi di sviluppo.

Consulta la [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md) per ulteriori informazioni su quando e come reindicizzare il contenuto.

## Rilevamento iniziale {#initial-detection}

L’indicizzazione lenta del rilevamento iniziale richiede la revisione del `IndexStats` Media JMX. Nell’istanza AEM interessata, effettua le seguenti operazioni:

1. Apri la console Web e fai clic sulla scheda JMX o vai a https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Accedi a `IndexStats` Mbeans.
1. Apri `IndexStats` MBean per &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Per entrambi gli MBean, verifica se **Fine** timestamp e **LastIndexTime** i timestamp sono a meno di 45 minuti dall’ora corrente.

1. Per MBean, se il valore di ora (**Fine** o **LastIndexedTime**) è a più di 45 minuti dall&#39;ora corrente, quindi il processo di indicizzazione non riesce o richiede troppo tempo. Questo problema fa sì che gli indici asincroni non siano aggiornati.

## Indicizzazione sospesa dopo un arresto forzato {#indexing-is-paused-after-a-forced-shutdown}

Un arresto forzato comporta la sospensione dell’indicizzazione asincrona da parte dell’AEM per un massimo di 30 minuti dopo il riavvio. E, in genere, sono necessari altri 15 minuti per completare la prima fase di reindicizzazione, per un totale di circa 45 minuti (rilegandosi al [Rilevamento iniziale](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45 minuti). Se l&#39;indicizzazione viene sospesa dopo un arresto forzato:

1. In primo luogo, stabilire se l&#39;istanza AEM è stata chiusa in modo forzato (il processo AEM è stato interrotto con la forza o si è verificato un guasto di corrente) e successivamente riavviata.

   * [Registrazione AEM](/help/sites-deploying/configure-logging.md) possono essere rivisti a questo scopo.

1. Se si è verificata la chiusura forzata, al riavvio l’AEM sospende automaticamente la reindicizzazione per un massimo di 30 minuti.
1. Attendere circa 45 minuti affinché l’AEM riprenda le normali operazioni di indicizzazione asincrona.

## Pool di thread sovraccaricato {#thread-pool-overloaded}

>[!NOTE]
>
>Per l’AEM 6.1, assicurare che [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it) è installato.

In circostanze eccezionali, il pool di thread utilizzato per gestire l’indicizzazione asincrona potrebbe subire un sovraccarico. Per isolare il processo di indicizzazione, è possibile configurare un pool di thread per evitare che altri processi AEM interferiscano con la capacità di Oak di indicizzare il contenuto in modo tempestivo. In questi casi, effettuare le seguenti operazioni:

1. Definisci un nuovo pool di thread isolati per Apache Sling Scheduler da utilizzare per l’indicizzazione asincrona:

   * Nell’istanza AEM interessata, passa a AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler oppure vai a https://&lt;host>:&lt;port>/system/console/configMgr (ad esempio, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Aggiungi una voce al campo &quot;Pool di thread consentiti&quot; con il valore &quot;oak&quot;.
   * Per salvare le modifiche, fai clic su **Salva** in basso a destra.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verifica che il nuovo pool di thread di Apache Sling Scheduler sia registrato e visualizzato nella console web Stato Apache Sling Scheduler.

   * Passa a AEM OSGi Web Console>Stato>Sling Scheduler oppure vai su https://&lt;host>:&lt;port>/system/console/status-slingscheduler (ad esempio, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verificare che siano presenti le seguenti voci del pool:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## La coda di osservazione è piena {#observation-queue-is-full}

Se vengono apportate troppe modifiche e commit all’archivio in un breve periodo di tempo, l’indicizzazione può essere ritardata a causa di una coda di osservazione completa. Innanzitutto, verifica se la coda di osservazione è piena:

1. Passa alla console Web e fai clic sulla scheda JMX o vai a https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Apri l’MBean delle statistiche dell’archivio Oak e determina se `ObservationQueueMaxLength` è maggiore di 10.000.

   * Nelle operazioni normali, questo valore massimo deve sempre alla fine ridursi a zero (in particolare nel `per second` sezione ), in modo da verificare che `ObservationQueueMaxLength`Le metriche dei secondi di sono 0.
   * Se i valori sono 10.000 o più e aumentano costantemente, indica che almeno una coda (possibilmente più code) non può essere elaborata con la stessa rapidità con cui si verificano nuove modifiche (commit).
   * Ogni coda di osservazione ha un limite (10.000 per impostazione predefinita) e se la coda raggiunge tale limite, la sua elaborazione si deteriora.
   * Quando si utilizza MongoMK, con l’aumentare delle lunghezze delle code, le prestazioni della cache Oak interna si riducono. Questa correlazione può essere vista in un aumento `missRate` per `DocChildren` cache in `Consolidated Cache` Statistiche MBean.

1. Per evitare di superare i limiti accettabili della coda di osservazione, si raccomanda di:

   * Abbassa la percentuale costante di commit. Picchi brevi nei commit sono accettabili, ma la velocità costante deve essere ridotta.
   * Aumentare le dimensioni del `DiffCache` come descritto in [Suggerimenti per l&#39;ottimizzazione delle prestazioni > Ottimizzazione archiviazione Mongo > Dimensione cache documenti](/help/sites-deploying/configuring-performance.md).

## Identificazione e correzione di un processo di reindicizzazione bloccato {#identifying-and-remediating-a-stuck-re-indexing-process}

La reindicizzazione può essere considerata &quot;completamente bloccata&quot; in due condizioni:

* La reindicizzazione è lenta, al punto che nei file di registro non viene segnalato alcun progresso significativo per quanto riguarda il numero di nodi attraversati.

   * Ad esempio, se non ci sono messaggi nel corso di un’ora o se l’avanzamento è così lento che il completamento richiede una settimana o più.

* La reindicizzazione è bloccata in un ciclo infinito se nei file di registro vengono visualizzate eccezioni ripetute (ad esempio, `OutOfMemoryException`) nel thread di indicizzazione. La ripetizione di una o più stesse eccezioni nel registro indica che Oak tenta di indicizzare ripetutamente la stessa cosa, ma non riesce per lo stesso problema.

Per identificare e correggere un processo di reindicizzazione bloccato, effettuare le seguenti operazioni:

1. Per identificare la causa del blocco dell’indicizzazione, è necessario raccogliere le seguenti informazioni:

   * Raccogli 5 minuti di immagine thread, un’immagine thread ogni 2 secondi.
   * [Imposta livello DEBUG e registri per le appendici](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Raccogliere dati da asincrono `IndexStats` MBean:

      * Passa a AEM OSGi Web Console>Principale>JMX>IndexStat>asincrono

         o vai a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Utilizzare [modalità console di oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) per raccogliere i dettagli di ciò che esiste sotto il * `/:async`* nodo.
   * Raccogliere un elenco di punti di controllo dell’archivio utilizzando `CheckpointManager` MBean:

      * Console Web OSGi AEM>Principale>JMX>Gestione punti di controllo>listCheckpoints()

         o vai a [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Dopo aver raccolto tutte le informazioni descritte nel passaggio 1, riavviare l&#39;AEM.

   * Il riavvio dell’AEM può risolvere il problema in presenza di un carico concorrente elevato (overflow della coda di osservazione o simile).
   * Se il riavvio non risolve il problema, apri un problema con [Assistenza clienti Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=homehome?lang=it#support) e fornire tutte le informazioni raccolte nel passaggio 1.

## Interruzione sicura della reindicizzazione asincrona {#safely-aborting-asynchronous-re-indexing}

La reindicizzazione può essere interrotta in modo sicuro (interrotta prima del completamento) tramite `async, async-reindex`e f `ulltext-async` corsie di indicizzazione ( `IndexStats` Mbean). Per ulteriori informazioni, consulta anche la documentazione di Apache Oak su [Interrompere la reindicizzazione](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Inoltre, considera quanto segue:

* La reindicizzazione degli indici di proprietà Lucene e Lucene può essere interrotta in quanto sono naturalmente asincroni.
* La reindicizzazione degli indici di proprietà Oak può essere interrotta solo se è stata avviata tramite `PropertyIndexAsyncReindexMBean`.

Per interrompere in modo sicuro la reindicizzazione, segui questi passaggi:

1. Identificare la voce MBean IndexStats che controlla la corsia di reindicizzazione che deve essere interrotta.

   * Passa all’MBean IndexStats appropriato tramite la console JMX, da AEM OSGi Web Console>Principale>JMX o https://&lt;host>:&lt;port>/system/console/jmx (ad esempio, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Aprire la voce MBean IndexStats in base alla corsia di reindicizzazione che si desidera interrompere ( `async`, `async-reindex`, o `fulltext-async`)

      * Per identificare la corsia appropriata e quindi l’istanza MBean IndexStats, controlla la proprietà &quot;async&quot; degli indici Oak. La proprietà &quot;async&quot; contiene il nome della corsia: `async`, `async-reindex`, o `fulltext-async`.
      * La corsia è disponibile anche accedendo a Gestione indice AEM nella colonna &quot;Asincrono&quot;. Per accedere a Gestione indice, passare a Operazioni>Diagnosi>Gestione indice.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Richiama `abortAndPause()` comando sulla scheda appropriata `IndexStats` MBean.
1. Contrassegna la definizione dell’indice Oak in modo appropriato per impedire la ripresa della reindicizzazione quando la corsia di indicizzazione riprende.

   * Durante la reindicizzazione di un **esistente** , impostare la proprietà reindex su false

      * `/oak:index/someExistingIndex@reindex=false`
   * Oppure, per un **nuovo** indice, ovvero:

      * Impostare la proprietà type su disabled

         * `/oak:index/someNewIndex@type=disabled`
      * o rimuovere completamente la definizione dell’indice

   Al termine, esegui il commit delle modifiche nell’archivio.

1. Infine, riprendere l&#39;indicizzazione asincrona sulla corsia di indicizzazione interrotta.

   * In `IndexStats` MBean che ha emesso `abortAndPause()` nel passaggio 2, richiama il comando `resume()`comando.

## Prevenzione della reindicizzazione lenta {#preventing-slow-re-indexing}

È meglio reindicizzare durante i periodi di silenzio (ad esempio, non durante un caricamento di contenuti di grandi dimensioni) e idealmente durante le finestre di manutenzione quando il caricamento dell’AEM è noto e controllato. Inoltre, assicurati che la reindicizzazione non avvenga durante altre attività di manutenzione.
