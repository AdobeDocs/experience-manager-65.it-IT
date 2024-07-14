---
title: Indicizzazione tramite il file JAR eseguito da Oak
description: Scopri come eseguire l’indicizzazione tramite il Jar eseguito da Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Indicizzazione tramite il file JAR eseguito da Oak {#indexing-via-the-oak-run-jar}

Oak-run supporta tutti i casi di utilizzo dell’indicizzazione sulla riga di comando senza dover operare dal livello JMX. I vantaggi dell’approccio oak-run sono:

1. Si tratta di un nuovo set di strumenti di indicizzazione per AEM 6.4
1. Riduce il tempo di reindicizzazione, che influisce positivamente sui tempi di reindicizzazione su archivi più grandi
1. Sta riducendo il consumo di risorse durante la reindicizzazione nell&#39;AEM, il che si traduce in migliori prestazioni del sistema per altre attività dell&#39;AEM
1. Oak-run fornisce supporto out-of-band: se le condizioni di produzione non consentono di eseguire la reindicizzazione sulle istanze di produzione, è possibile utilizzare un ambiente clonato per la reindicizzazione al fine di evitare un impatto critico sulle prestazioni.

Di seguito è riportato un elenco di casi d&#39;uso che possono essere utilizzati durante l&#39;esecuzione di operazioni di indicizzazione tramite lo strumento `oak-run`.

## Controlli di coerenza indice {#indexconsistencychecks}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Caso d&#39;uso 1: verifica di coerenza indice](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`determina rapidamente se gli indici Lucene Oak sono danneggiati.
* È sicuro operare su un’istanza AEM in uso per i livelli di controllo di coerenza 1 e 2.

![Verifica coerenza indice](assets/screen_shot_2017-12-14at135758.png)

## Statistiche indice {#indexstatistics}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Caso d&#39;uso 2 - Statistiche indice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` esegue il dump di tutte le definizioni dell&#39;indice, delle statistiche importanti dell&#39;indice e del contenuto dell&#39;indice per l&#39;analisi offline.
* L’esecuzione è sicura su un’istanza AEM in uso.

![immagine2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Albero decisionale dell’approccio di reindicizzazione {#reindexingapproachdecisiontree}

Questo diagramma è un albero decisionale per quando utilizzare i vari approcci di reindicizzazione.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Reindicizzazione MongoMK/RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Caso d&#39;uso 3: reindicizzazione](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Pre-estrazione del testo per SegmentNodeStore e DocumentNodeStore {#textpre-extraction}

[È possibile utilizzare la funzione di pre-estrazione del testo](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (già disponibile con AEM 6.3) per ridurre il tempo di reindicizzazione. La pre-estrazione del testo può essere utilizzata con tutti gli approcci di reindicizzazione.

A seconda dell&#39;approccio di indicizzazione `oak-run.jar`, sono disponibili vari passaggi su entrambi i lati del passaggio Esegui reindicizzazione nel diagramma seguente.

![Pre-estrazione testo per SegmentNodeStore e DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>Arancione indica le attività in cui l’AEM deve trovarsi in una finestra di manutenzione.

### Reindicizzazione online per MongoMK o RDBMK tramite oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizza - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Questo è il metodo consigliato per la reindicizzazione delle installazioni di AEM MongoMK (e RDBMK). Non utilizzare altri metodi.

Eseguire questo processo solo su una singola istanza AEM nel cluster.

![Reindicizzazione online per MongoMK o RDBMK tramite oak-run.jar](assets/5.png)

## Reindicizzazione TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizza - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Considerazioni sullo standby a freddo (TarMK)**

   * Non vi sono considerazioni speciali per lo standby a freddo; le istanze dello standby a freddo sincronizzano le modifiche come di consueto.

* **Farm Publish AEM (le farm Publish AE devono essere sempre TarMK)**

   * Per la farm di pubblicazione, deve essere eseguito per tutti OPPURE eseguire i passaggi su una singola pubblicazione. Quindi, clona la configurazione per gli altri (adottando tutte le consuete precauzioni durante la clonazione delle istanze AEM; sling.id - dovrebbe essere collegato a qualcosa qui).

### Reindicizzazione online per TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizzazione online - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Questo è il metodo utilizzato prima dell’introduzione delle nuove funzionalità di indicizzazione di oak-run.jar. Questa operazione viene eseguita impostando la proprietà `reindex=true` sull&#39;indice Oak.

Questo approccio può essere utilizzato se gli effetti di indicizzazione in termini di tempo e prestazioni sono accettabili per il cliente. Questo è spesso il caso degli impianti AEM di piccole e medie dimensioni.

![Reindicizzazione online per TarMK](assets/6.png)

### Reindicizzazione online di TarMK tramite oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è in esecuzione](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

La reindicizzazione online di TarMK utilizzando oak-run.jar è più veloce della [reindicizzazione online per TarMK](#onlinere-indexingfortarmk) descritta sopra. Tuttavia, richiede anche l&#39;esecuzione durante una finestra di manutenzione; con la menzione che la finestra è più corta e sono necessari più passaggi per eseguire la reindicizzazione.

>[!NOTE]
>
>L&#39;arancione indica le operazioni in cui l&#39;AEM deve essere effettuato durante un periodo di mantenimento.

![Reindicizzazione online di TarMK tramite oak-run.jar](assets/7.png)

### Reindicizzazione offline di TarMK tramite oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizzazione online - SegmentNodeStore - L&#39;istanza AEM è chiusa](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La reindicizzazione offline di TarMK è l&#39;approccio più semplice basato su `oak-run.jar` per TarMK in quanto richiede un singolo commento `oak-run.jar`. Tuttavia, richiede la chiusura dell’istanza AEM.

>[!NOTE]
>
>Il rosso indica le operazioni in cui l&#39;AEM deve essere interrotto.

![Nuova indicizzazione offline di TarMK tramite oak-run.jar](assets/8.png)

### Reindicizzazione out-of-band di TarMK tramite oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedi [Reindicizzazione fuori banda - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

La reindicizzazione fuori banda riduce al minimo l’impatto della reindicizzazione sulle istanze di AEM in uso.

>[!NOTE]
>
>Il rosso indica le operazioni in cui l’AEM può essere interrotto.

![Nuova indicizzazione fuori banda di TarMK tramite oak-run.jar](assets/9.png)

## Aggiornamento delle definizioni di indicizzazione {#updatingindexingdefinitions}

>[!NOTE]
>
>Per informazioni più dettagliate su questo scenario, vedere [Caso d&#39;uso 4 - Aggiornamento delle definizioni dell&#39;indice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Creazione e aggiornamento delle definizioni degli indici in TarMK tramite ACS Ensure Index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index è un progetto supportato dalla community e non è supportato dal supporto Adobe.

Ciò consente la definizione dell&#39;indice di spedizione tramite il pacchetto di contenuto che in seguito determina la reindicizzazione impostando il flag di reindicizzazione su `true`. Questo funziona per le configurazioni più piccole in cui la reindicizzazione non richiede molto tempo.

Per ulteriori informazioni, consulta la [documentazione ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html).

### Creazione e aggiornamento delle definizioni degli indici in TarMK tramite oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Se il tempo o l&#39;impatto sulle prestazioni della reindicizzazione utilizzando metodi diversi da `oak-run.jar` è troppo elevato, è possibile utilizzare il seguente approccio basato su `oak-run.jar` per importare e reindicizzare le definizioni dell&#39;indice di Lucene in un&#39;installazione AEM basata su TarMK.

![Creazione e aggiornamento delle definizioni degli indici in TarMK tramite oak-run.jar](assets/10.png)

### Creazione e aggiornamento delle definizioni degli indici in MonogMK tramite oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Se il tempo o l&#39;impatto sulle prestazioni della reindicizzazione utilizzando metodi diversi da `oak-run.jar` è troppo elevato, è possibile utilizzare il seguente approccio basato su `oak-run.jar` per importare e reindicizzare le definizioni dell&#39;indice di Lucene nelle installazioni AEM basate su MongoMK.

![Creazione e aggiornamento delle definizioni degli indici in MonogMK tramite oak-run.jar](assets/11.png)
