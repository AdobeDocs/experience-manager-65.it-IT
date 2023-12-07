---
title: Utilizzo dei registri
description: Scopri come risolvere i problemi relativi all’AEM lavorando con i registri.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# Utilizzo dei registri{#working-with-logs}

Questa sezione include informazioni dettagliate sui registri disponibili per aiutarti a risolvere eventuali problemi.

>[!NOTE]
>
>Per ulteriori informazioni sui registri, consulta:
>
>* [Manutenzione del registro di controllo dell’AEM](/help/sites-administering/operations-audit-log.md)
>* [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

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

proprietà di debug. Non lasciare il registro a livello di registro DEBUG più tempo del necessario, in quanto genera numerosi registri.

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
