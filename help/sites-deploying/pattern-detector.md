---
title: Valutazione della complessità dell’aggiornamento con il rilevatore pattern
description: Scopri come utilizzare il rilevatore pattern per valutare la complessità dell’aggiornamento.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Valutazione della complessità dell’aggiornamento con il rilevatore pattern

## Panoramica {#overview}

Questa funzione consente di verificare le istanze AEM esistenti per la loro aggiornabilità rilevando i pattern in uso che:

1. Violano alcune regole e vengono eseguiti in aree che saranno interessate o sovrascritte dall’aggiornamento
1. Utilizza una funzione AEM 6.x o un’API che non è compatibile con le versioni precedenti di AEM 6.5 e può potenzialmente interrompersi dopo l’aggiornamento.

Ciò potrebbe servire come valutazione dello sforzo di sviluppo che è coinvolto nell&#39;aggiornamento all&#39;AEM 6.5.

## Configurazione {#how-to-set-up}

Il rilevatore pattern viene rilasciato separatamente come [un pacchetto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) che funziona su qualsiasi versione AEM di origine dalla 6.1 alla 6.5 e ha come destinazione l&#39;aggiornamento AEM 6.5. Può essere installato utilizzando [Gestione pacchetti](/help/sites-administering/package-manager.md).

## Guida all’uso {#how-to-use}

>[!NOTE]
>
>Il rilevatore pattern può essere eseguito in qualsiasi ambiente, incluse le istanze di sviluppo locali. Tuttavia, per:
>
>* aumentare il tasso di rilevamento
>* evitare rallentamenti nelle istanze business critical
>
>entrambi allo stesso tempo si consiglia di eseguirlo **in ambienti di staging** che siano il più possibile simili a quelli di produzione nelle aree di applicazioni utente, contenuto e configurazioni.

È possibile utilizzare diversi metodi per controllare l&#39;output del rilevatore pattern:

* **Tramite la console Inventario Felix:**

1. Passa alla console Web AEM navigando su *https://serveraddress:serverport/system/console/configMgr*
1. Selezionare **Stato - Rilevatore pattern** come illustrato nell&#39;immagine seguente:

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **Tramite un&#39;interfaccia JSON normale o basata su testo reattivo**
* **Tramite un’interfaccia per righe JSON reattive, **che genera un documento JSON separato in ogni riga.

Entrambi i metodi sono descritti di seguito:

## Interfaccia reattiva {#reactive-interface}

L’interfaccia reattiva consente l’elaborazione della segnalazione della violazione non appena viene rilevato un sospetto.

L’output è attualmente disponibile in 2 URL:

1. Interfaccia testo normale
1. Interfaccia JSON

## Gestione dell’interfaccia testo normale {#handling-the-plain-text-interface}

Le informazioni nell’output vengono formattate come una serie di voci evento. Sono disponibili due canali: uno per le violazioni di pubblicazione e il secondo per la pubblicazione dell’avanzamento corrente.

È possibile ottenerli utilizzando i seguenti comandi:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

L’output sarà simile al seguente:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

L&#39;avanzamento può essere filtrato utilizzando il comando `grep`:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

Il che si traduce nel seguente output:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Gestione dell’interfaccia JSON {#handling-the-json-interface}

Analogamente, JSON può essere elaborato utilizzando lo strumento [jq](https://stedolan.github.io/jq/) non appena viene pubblicato.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Con l&#39;output:

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

L’avanzamento viene segnalato ogni 5 secondi e può essere recuperato escludendo messaggi diversi da quelli contrassegnati come sospetti:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Con l&#39;output:

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>L&#39;approccio consigliato consiste nel salvare l&#39;intero output da curl nel file e quindi elaborarlo tramite `jq` o `grep` per filtrare il tipo di informazioni.

## Ambito di rilevamento {#scope}

Al momento il rilevatore pattern consente di controllare quanto segue:

* Bundle OSGi con esportazioni e importazioni non corrispondenti
* Sovrautilizzi di tipi di risorse e super tipi Sling (con sovrapposizioni di contenuto del percorso di ricerca)
* definizioni degli indici di Oak (compatibilità)
* Pacchetti VLT (uso eccessivo)
* rep:Compatibilità dei nodi utente (nel contesto della configurazione OAuth)

>[!NOTE]
>
>Il rilevatore pattern tenta di prevedere con precisione gli avvisi per l’aggiornamento. Tuttavia, in alcuni scenari potrebbe generare falsi positivi.
