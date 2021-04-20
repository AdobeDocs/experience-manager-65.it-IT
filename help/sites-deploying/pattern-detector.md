---
title: Valutazione della complessità dell’aggiornamento con il rilevatore pattern
seo-title: Valutazione della complessità dell’aggiornamento con il rilevatore pattern
description: Scopri come utilizzare il rilevatore pattern per valutare la complessità dell’aggiornamento.
seo-description: Scopri come utilizzare il rilevatore pattern per valutare la complessità dell’aggiornamento.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---


# Valutazione della complessità dell’aggiornamento con il rilevatore pattern

## Panoramica {#overview}

Questa funzione consente di controllare le istanze di AEM esistenti per la loro aggiornabilità rilevando i pattern utilizzati che:

1. Violano determinate regole e vengono eseguite in aree che saranno influenzate o sovrascritte dall&#39;aggiornamento
1. Utilizza una funzionalità AEM 6.x o un&#39;API che non è compatibile con le versioni precedenti in AEM 6.5 e che può potenzialmente interrompersi dopo l&#39;aggiornamento.

Ciò potrebbe servire da valutazione dello sforzo di sviluppo che comporta l&#39;aggiornamento al AEM 6.5.

## Configurazione {#how-to-set-up}

Il rilevatore pattern viene rilasciato separatamente come [un pacchetto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) che funziona su qualsiasi versione di AEM di origine dalla versione 6.1 alla versione 6.5 per il targeting AEM aggiornamento 6.5. Può essere installato utilizzando il [Package Manager](/help/sites-administering/package-manager.md).

## Guida all’uso {#how-to-use}

>[!NOTE]
>
>Il rilevatore pattern può essere eseguito in qualsiasi ambiente, incluse le istanze di sviluppo locali. Tuttavia, al fine di:
>
>* aumentare il tasso di rilevamento
>* evitare rallentamenti nelle istanze business critical

>
>
allo stesso tempo, si consiglia di eseguirlo **negli ambienti di staging** che sono il più vicini possibile a quelli di produzione nelle aree delle applicazioni utente, dei contenuti e delle configurazioni.

È possibile utilizzare diversi metodi per controllare l’output del rilevatore pattern:

* **Tramite la console Inventario Felix:**

1. Vai alla Console Web AEM sfogliando *https://serveraddress:serverport/system/console/configMgr*
1. Seleziona **Stato - Rilevatore pattern** come mostrato nell’immagine seguente:

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **Tramite un’interfaccia JSON reattiva basata su testo o normale**
* **Tramite un’interfaccia di linee JSON reattive, **genera un documento JSON separato in ogni riga.

Entrambi i metodi sono descritti di seguito:

## Interfaccia reattiva {#reactive-interface}

L&#39;interfaccia reattiva consente l&#39;elaborazione della segnalazione di violazione non appena viene rilevato un sospetto.

L’output è attualmente disponibile sotto 2 URL:

1. Interfaccia di testo normale
1. Interfaccia JSON

## Gestione dell&#39;interfaccia di testo normale {#handling-the-plain-text-interface}

Le informazioni nell&#39;output vengono formattate come una serie di voci evento. Esistono due canali: uno per la pubblicazione delle violazioni e l’altro per la pubblicazione dell’avanzamento corrente.

Possono essere ottenuti utilizzando i seguenti comandi:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

L&#39;output sarà simile al seguente:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

L&#39;avanzamento può essere filtrato utilizzando il comando `grep` :

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

che produce il seguente output:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Gestione dell’interfaccia JSON {#handling-the-json-interface}

Allo stesso modo, JSON può essere elaborato utilizzando lo strumento [jq](https://stedolan.github.io/jq/) non appena viene pubblicato.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Con l&#39;uscita:

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

I progressi vengono segnalati ogni 5 secondi e possono essere recuperati escludendo messaggi diversi da quelli contrassegnati come sospetti:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Con l&#39;uscita:

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
>L&#39;approccio consigliato è quello di salvare l&#39;intero output da curl nel file e quindi elaborarlo tramite `jq` o `grep` per filtrare il tipo di informazioni.

## Ambito di rilevamento {#scope}

Attualmente il rilevatore pattern consente di controllare:

* Esportazioni e importazioni dei bundle OSGi non corrispondenti
* Sovrapusi per tipi di risorse Sling e super type (con sovrapposizioni di contenuto del percorso di ricerca)
* definizioni degli indici Oak (compatibilità)
* Pacchetti VLT (utilizzo eccessivo)
* rep:Compatibilità dei nodi utente (nel contesto della configurazione OAuth)

>[!NOTE]
>
>Tieni presente che il rilevatore pattern cerca di prevedere con precisione gli avvisi relativi all’aggiornamento. Tuttavia, potrebbe generare falsi positivi in alcuni scenari.
