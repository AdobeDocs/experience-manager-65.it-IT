---
title: Indicizzazione tramite il Jar di esecuzione Oak
seo-title: Indicizzazione tramite il Jar di esecuzione Oak
description: Scoprite come eseguire l'indicizzazione tramite il Jar di esecuzione Oak.
seo-description: Scoprite come eseguire l'indicizzazione tramite il Jar di esecuzione Oak.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Indicizzazione tramite il Jar di esecuzione Oak {#indexing-via-the-oak-run-jar}

Oak-run supporta tutti i casi di utilizzo di indicizzazione sulla riga di comando senza dover operare dal livello JMX. I vantaggi dell&#39;approccio di rovere sono:

1. È un nuovo set di strumenti di indicizzazione per AEM 6.4
1. Diminuisce il tempo di reindicizzazione che influisce positivamente sui tempi di reindicizzazione sui repository più grandi
1. Durante la reindicizzazione in AEM, il consumo di risorse risulta ridotto e il sistema offre prestazioni migliori per altre attività AEM
1. Oak-run fornisce supporto fuori banda: Se le condizioni di produzione non consentono l&#39;esecuzione del reindicizzazione sulle istanze di produzione, è possibile utilizzare un ambiente clonato per reindicizzare per evitare un impatto critico sulle prestazioni.

Di seguito è riportato un elenco dei casi di utilizzo che è possibile utilizzare per eseguire operazioni di indicizzazione tramite `oak-run` lo strumento.

## Controlli di coerenza indice {#indexconsistencychecks}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, consultate Caso di [utilizzo 1 - Controllo](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)coerenza indice.

* `oak-run.jar`determina rapidamente se gli indici di quercia lucene sono danneggiati.
* È sicuro eseguire un’istanza di AEM in uso per verificare la coerenza dei livelli 1 e 2.

![screen_shot_2017-12-14at135758](assets/screen_shot_2017-12-14at135758.png)

## Statistiche indice {#indexstatistics}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedere Caso di [utilizzo 2 - Statistiche indice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` scarica tutte le definizioni di indice, gli stati di indice importanti e il contenuto dell&#39;indice per l&#39;analisi offline.
* Sicuro da eseguire su un’istanza AEM in uso.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Albero delle decisioni relative all&#39;approccio di reindicizzazione {#reindexingapproachdecisiontree}

Questo diagramma è una struttura decisionale che consente di utilizzare i vari approcci di reindicizzazione.

![oak_reindexingwith-oak run](assets/oak_-_reindexingwithoak-run.png)

## Re-indicizzazione MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Per ulteriori informazioni su questo scenario, vedere Caso di [utilizzo 3 - Reindicizzazione](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Pre-estrazione del testo per SegmentNodeStore e DocumentNodeStore {#textpre-extraction}

[La preestrazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) del testo (una funzione che esiste con AEM 6.3) può essere utilizzata per ridurre il tempo necessario per reindicizzare. La preestrazione del testo può essere utilizzata insieme a tutti gli approcci di reindicizzazione.

A seconda del metodo di `oak-run.jar` indicizzazione, ci saranno vari passaggi su entrambi i lati del passaggio Esegui reindicizzazione nel diagramma seguente.

![4](assets/4.png)

>[!NOTE]
>
>Arancione indica le attività in cui AEM deve trovarsi in una finestra di manutenzione.

### Reindicizzazione online per MongoMK o RDBMK tramite oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Per ulteriori informazioni su questo scenario, vedere [Reindex - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Questo è il metodo consigliato per reindicizzare le installazioni AEM di MongoMK (e RDBMK). Non utilizzare altri metodi.

Questo processo deve essere eseguito solo per una singola istanza di AEM nel cluster.

![5](assets/5.png)

## Re-indicizzazione TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Considerazioni sul Cold Standby (TarMK)**

   * Non vi è alcuna considerazione particolare per la Standby a freddo; le istanze Cold Standby sincronizzeranno le modifiche come al solito.

* **AEM Publish Farms (AEM Publish Farms dovrebbe sempre essere TarMK)**

   * Per la pubblicazione di farm, è necessario eseguire tutti i passaggi OPPURE su un&#39;unica pubblicazione, quindi duplicare la configurazione per altri utenti (eseguendo tutte le consuete procedure di duplicazione delle istanze AEM); sling.id - dovrebbe collegarsi a qualcosa qui)

### Riindicizzazione online per TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Per ulteriori informazioni su questo scenario, consulta Reindicizzazione [online - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Questo è il metodo utilizzato prima dell&#39;introduzione delle nuove funzionalità di indicizzazione di oak-run.jar. È possibile impostare la `reindex=true` proprietà sull&#39;indice Oak.

Questo approccio può essere utilizzato se gli effetti tempo e prestazioni da indicizzare sono accettabili per il cliente. Questo accade spesso per le installazioni AEM di piccole e medie dimensioni.

![6](assets/6.png)

### Riindicizzazione online di TarMK tramite oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per informazioni dettagliate su questo scenario, consultate Reindicizzazione [online - SegmentNodeStore - L’istanza AEM è in esecuzione](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

La reindicizzazione online di TarMK è più veloce della reindicizzazione TarkMK online descritta sopra. Tuttavia, richiede anche l&#39;esecuzione durante una finestra di manutenzione, con il metodo che la finestra sarà più breve, e sono necessari più passaggi per eseguire la reindicizzazione.

>[!NOTE]
>
>Arancione indica le operazioni in cui AEM deve essere eseguito in un periodo di manutenzione.

![7](assets/7.png)

### ReIndexing TarMK offline con oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per ulteriori informazioni su questo scenario, consulta Reindicizzazione [online - SegmentNodeStore - L’istanza di AEM è chiusa](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La reindicizzazione offline di TarMK è l&#39;approccio di reindicizzazione `oak-run.jar` basato più semplice per TarMK, in quanto richiede un solo `oak-run.jar` commento. Tuttavia, l’istanza di AEM deve essere chiusa.

>[!NOTE]
>
>Il rosso indica le operazioni in cui AEM deve essere chiuso.

![8](assets/8.png)

### Re-Indexing TarMK out-of-band utilizzando oak-run.jar {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Out of Band Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

Il reindicizzazione out-of-band riduce al minimo l’impatto del reindicizzazione sulle istanze AEM in uso.

>[!NOTE]
>
>Il rosso indica le operazioni in cui AEM potrebbe essere chiuso.

![9](assets/9.png)

## Aggiornamento delle definizioni di indicizzazione {#updatingindexingdefinitions}

>[!NOTE]
>
>Per ulteriori informazioni su questo scenario, vedere Caso [d&#39;uso 4 - Aggiornamento delle definizioni](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)di indice.

### Creazione e aggiornamento delle definizioni di indice su TarMK tramite ACS Verify Index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Verify Index è un progetto supportato dalla comunità e non è supportato dal supporto Adobe.

Questo consente di inviare la definizione dell&#39;indice tramite il pacchetto di contenuto, che in seguito si tradurrà in reindicizzazione impostando il flag di reindicizzazione su `true`. Questo funziona per le impostazioni più piccole in cui la reindicizzazione non richiede molto tempo.

Per ulteriori informazioni, consulta la documentazione [ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) Verify Index (Protezione dell&#39;indice ACS).

### Creazione e aggiornamento delle definizioni di indice su TarMK tramite oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Se l’impatto di tempo o prestazioni della reindicizzazione utilizzando `oak-run.jar` metodi non è troppo elevato, l’approccio `oak-run.jar` basato su indicato di seguito può essere utilizzato per importare e reindicizzare le definizioni dell’indice Lucene in un’installazione AEM basata su TarMK.

![10](assets/10.png)

### Creazione e aggiornamento delle definizioni di indice su MonogMK tramite oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Se l’impatto di tempo o prestazioni della reindicizzazione utilizzando `oak-run.jar` metodi non è troppo elevato, per importare e reindicizzare le definizioni dell’indice Lucene nelle installazioni AEM basate su MongoMK è possibile utilizzare il seguente approccio `oak-run.jar` basato su.

![11](assets/11.png)

