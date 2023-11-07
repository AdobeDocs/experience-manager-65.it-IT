---
title: Panoramica dei rapporti sulle transazioni
seo-title: Transaction Reports Overview
description: Mantieni un conteggio di tutti i moduli inviati, comunicazione interattiva sottoposta a rendering, documenti convertiti in un formato e altro ancora
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Panoramica dei rapporti sulle transazioni{#transaction-reports-overview}

## Introduzione {#introduction}

I rapporti sulle transazioni in AEM Forms consentono di tenere traccia di tutte le transazioni eseguite a partire da una data specificata nella distribuzione AEM Forms. L’obiettivo è fornire informazioni sull’utilizzo dei prodotti e aiutare le parti interessate a comprendere i volumi di elaborazione digitale. Di seguito sono riportati alcuni esempi di transazioni:

* Invio di un modulo adattivo, di un modulo HTML5 o di un set di moduli
* Rappresentazione di una stampa o versione web di una comunicazione interattiva
* Conversione di un documento da un formato di file a un altro

Per ulteriori informazioni su quella che viene considerata una transazione, vedi [API fatturabili](../../forms/using/transaction-reports-billable-apis.md).

La registrazione delle transazioni è disabilitata per impostazione predefinita. È possibile [abilita registrazione transazioni](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) dalla console web dell’AEM. Puoi visualizzare i rapporti sulle transazioni nelle istanze di authoring, elaborazione o pubblicazione. Visualizzare i report delle transazioni sulle istanze di authoring o elaborazione per una somma aggregata di tutte le transazioni. Visualizzare i rapporti sulle transazioni nelle istanze di pubblicazione per un conteggio di tutte le transazioni che si verificano solo nell’istanza di pubblicazione da cui viene eseguito il rapporto.

Non creare contenuti (creare moduli adattivi, comunicazioni interattive, temi e altre attività di authoring) ed elaborare documenti (utilizzare flussi di lavoro, servizi documentali e altre attività di elaborazione) sulla stessa istanza AEM. Mantieni disabilitata la registrazione delle transazioni per i server AEM Forms utilizzati per l’authoring dei contenuti. Mantieni abilitata la registrazione delle transazioni per i server AEM Forms utilizzati per elaborare i documenti.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

Una transazione rimane nel buffer per un periodo specificato (tempo buffer di scaricamento + tempo replica inversa). Per impostazione predefinita, occorrono circa 90 secondi prima che il conteggio delle transazioni venga visualizzato nel rapporto sulle transazioni.

Azioni quali l’invio di un modulo PDF, l’utilizzo dell’interfaccia utente dell’agente per visualizzare in anteprima una comunicazione interattiva o l’utilizzo di metodi di invio di moduli non standard non vengono considerate transazioni. AEM Forms fornisce un’API per registrare tali transazioni. Chiama l’API dalle implementazioni personalizzate per registrare una transazione.

## Topologia supportata {#supported-topology}

I rapporti sulle transazioni sono disponibili solo in AEM Forms in ambiente OSGi. Supporta le topologie author-publish, author-processing-publish e only processing. Ad esempio, le topologie, vedi [Architettura e topologie di implementazione per AEM Forms](../../forms/using/transaction-reports-overview.md).

Il conteggio delle transazioni viene replicato in modo inverso dalle istanze di pubblicazione alle istanze di authoring o elaborazione. Di seguito è riportata una topologia indicativa autore-pubblicazione:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>I rapporti sulle transazioni di AEM Forms non supportano topologie che contengono solo istanze di pubblicazione.

### Linee guida per l’utilizzo dei report sulle transazioni {#guidelines-for-using-transaction-reports}

* Disattiva i rapporti sulle transazioni per tutte le istanze di authoring, poiché i rapporti sulle istanze di authoring includono le transazioni registrate durante le attività di authoring.
* Abilita **Mostra transazioni solo da pubblicazione** sull’istanza Autore per visualizzare le transazioni cumulative da tutte le istanze Publish. Puoi anche visualizzare i rapporti sulle transazioni su ogni istanza di pubblicazione per le transazioni effettive solo su quella particolare istanza di pubblicazione.
* Non utilizzare le istanze di authoring per eseguire flussi di lavoro ed elaborare documenti.
* Prima di utilizzare la generazione rapporti sulle transazioni, se disponi di una topologia con server di pubblicazione, assicurati che la replica inversa sia abilitata per tutte le istanze di pubblicazione.
* I dati delle transazioni vengono replicati in modo inverso da un’istanza Publish all’unica istanza di authoring o elaborazione corrispondente. L’istanza di authoring o elaborazione non può replicare ulteriormente i dati in un’altra istanza. Ad esempio, se disponi di una topologia di authoring-elaborazione-pubblicazione, i dati delle transazioni aggregati vengono replicati solo nell’istanza di elaborazione.

## Articoli correlati {#related-articles}

* [Visualizzazione e comprensione dei rapporti sulle transazioni](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Report transazioni API fatturabili](../../forms/using/transaction-reports-billable-apis.md)
* [Registrare una transazione per le implementazioni personalizzate](/help/forms/using/record-transaction-custom-implementation.md)
