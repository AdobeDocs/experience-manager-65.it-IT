---
title: Valutazione della complessità dell'aggiornamento con il rilevamento dei pattern
seo-title: Valutazione della complessità dell'aggiornamento con il rilevamento dei pattern
description: Scopri come utilizzare il Rilevatore di pattern per valutare la complessità dell'aggiornamento.
seo-description: Scopri come utilizzare il Rilevatore di pattern per valutare la complessità dell'aggiornamento.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Valutazione della complessità dell&#39;aggiornamento con il rilevamento dei pattern{#assessing-the-upgrade-complexity-with-the-pattern-detector}

## Panoramica {#overview}

Questa funzione consente di controllare le istanze AEM esistenti per verificarne la aggiornabilità rilevando i pattern in uso che:

1. Violare determinate regole e vengono eseguite in aree che saranno interessate o sovrascritte dall&#39;aggiornamento
1. Utilizzate una funzione AEM 6.x o un&#39;API che non sia compatibile con le versioni precedenti di AEM 6.5 e che possa interrompersi dopo l&#39;aggiornamento.

Questo potrebbe servire come valutazione dello sforzo di sviluppo coinvolto nell’aggiornamento ad AEM 6.5.

## Come impostare {#how-to-set-up}

Il rilevamento dei pattern viene rilasciato separatamente come [un pacchetto](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65) che funziona su qualsiasi versione sorgente di AEM dalla versione 6.1 alla 6.5, con targeting dell’aggiornamento di AEM 6.5. Può essere installato utilizzando [Package Manager](/help/sites-administering/package-manager.md).

## Guida all’uso {#how-to-use}

>[!NOTE]
>
>Il rilevamento dei pattern può essere eseguito in qualsiasi ambiente, comprese le istanze di sviluppo locale. Tuttavia, al fine di:
>
>* aumentare la velocità di rilevamento
>* evitare rallentamenti in casi business critical


>allo stesso tempo, si consiglia di eseguirlo **in ambienti** di pre-produzione il più vicino possibile a quelli di produzione nelle aree delle applicazioni utente, dei contenuti e delle configurazioni.
>
È possibile utilizzare diversi metodi per controllare l&#39;output di Rilevamento pattern:

* **Tramite la console di Felix Inventory:**

1. Andate alla console Web di AEM visitando *https://serveraddress:serverport/system/console/configMgr*
1. Seleziona **stato - Rilevamento** pattern come illustrato nell&#39;immagine seguente:

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **Tramite un&#39;interfaccia JSON reattiva basata su testo o normale**

* **Tramite un&#39;interfaccia di linee JSON reattive, **che genera un documento JSON separato in ogni riga.

Entrambi i metodi sono descritti di seguito:

## Interfaccia reattiva {#reactive-interface}

L&#39;interfaccia reattiva consente l&#39;elaborazione della segnalazione di violazione non appena viene rilevato un sospetto.

L’output è attualmente disponibile in 2 URL:

1. Interfaccia testo semplice
1. Interfaccia JSON

## Gestione dell’interfaccia di testo semplice {#handling-the-plain-text-interface}

Le informazioni nell&#39;output sono formattate come una serie di voci dell&#39;evento. Esistono due canali: uno per pubblicare le violazioni e l’altro per pubblicare i progressi correnti.

Possono essere ottenuti utilizzando i seguenti comandi:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

L&#39;output sarà simile al seguente:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

L&#39;avanzamento può essere filtrato utilizzando il `grep` comando:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

che genera il seguente output:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Gestione dell’interfaccia JSON {#handling-the-json-interface}

Allo stesso modo, JSON può essere elaborato utilizzando lo strumento [](https://stedolan.github.io/jq/) jq non appena viene pubblicato.

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

L&#39;avanzamento viene segnalato ogni 5 secondi e può essere ottenuto escludendo altri messaggi oltre a quelli contrassegnati come sospetti:

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
L&#39;approccio consigliato consiste nel salvare l&#39;intero output dall&#39;archivio e quindi elaborarlo tramite `jq` o `grep` filtrare il tipo di informazioni.

## Ambito di rilevamento {#scope}

Al momento il rilevamento dei pattern consente di controllare:

* Mancata corrispondenza tra esportazioni e importazioni di bundle OSGi
* Sovrapposizioni per tipi di risorse Sling e super-tipi (con sovrapposizioni di contenuti per percorsi di ricerca)
* definizioni di indici di quercia (compatibilità)
* Pacchetti VLT (overuse)
* rep:compatibilità dei nodi utente (nel contesto della configurazione OAuth)

>[!NOTE]
Tenere presente che il Rilevatore pattern tenta di prevedere con precisione gli avvisi relativi all&#39;aggiornamento. Tuttavia, in alcuni scenari potrebbe generare falsi positivi.

