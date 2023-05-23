---
title: Utilizzo dei registri
seo-title: Working with Logs
description: Scopri come risolvere i problemi relativi all’AEM lavorando con i registri.
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 3%

---

# Utilizzo dei registri{#working-with-logs}

Questa sezione include informazioni dettagliate sui registri disponibili per aiutarti a risolvere eventuali problemi.

CRX registra i registri dettagliati. Dopo aver decompresso e avviato Quickstart, i registri sono disponibili nelle seguenti posizioni:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Attivazione del livello di registro DEBUG {#activating-the-debug-log-level}

Il livello di registro predefinito è INFO, ovvero i messaggi DEBUG non vengono registrati.

Per attivare il livello di registro DEBUG, utilizzare l&#39;Explorer CRX per impostare

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

proprietà di debug. Non lasciare il registro a livello di registro DEBUG più tempo del necessario, in quanto genera molti registri.

Una riga nel file di debug in genere inizia con DEBUG e quindi fornisce il livello di registro, l&#39;azione del programma di installazione e il messaggio di registro. Ad esempio:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

I livelli del registro sono i seguenti:

| 0 | Errore irreversibile | Azione non riuscita. Impossibile continuare l&#39;installazione. |
|---|---|---|
| 1 | Errore | Azione non riuscita. L&#39;installazione procede, ma una parte di CRX non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è stata completata ma si sono verificati problemi. CRX potrebbe funzionare correttamente o meno. |
| 3 | Informazioni | Azione completata. |

## Opzione dettagliata utilizzata per la risoluzione dei problemi {#verbose-option-used-for-troubleshooting}

Quando si avvia CRX, è possibile aggiungere l&#39;opzione -v (verbose) alla riga di comando come in:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilizza l’opzione dettagliata per la risoluzione dei problemi, in quanto questa opzione mostra parte dell’output del registro quickstart sulla console.
