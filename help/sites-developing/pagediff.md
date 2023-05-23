---
title: Sviluppo e differenze tra pagine
seo-title: Developing and Page Diff
description: Sviluppo e differenze tra pagine
seo-description: null
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 85895215904b8706830d20f7714de5512b2c3ec2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%

---

# Sviluppo e differenze tra pagine{#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. Visualizzare una versione di pagina e l’altra è inefficiente e soggetto a errori. L’autore vuole poter confrontare la pagina corrente con una versione precedente, evidenziando le differenze.

La differenza di pagina consente a un utente di confrontare la pagina corrente con lanci, versioni precedenti, ecc. Per informazioni dettagliate su questa funzione utente, consulta [Differenza di pagina](/help/sites-authoring/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata dall’AEM in background per facilitare la differenza. Questo è necessario per poter eseguire il rendering del contenuto [per il confronto affiancato](/help/sites-developing/pagediff.md#operation-details).

Questa operazione di ricreazione viene eseguita internamente dall&#39;AEM, è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio in CRX DE Lite, vedrebbe queste versioni ricreate all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella seguente posizione:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Autorizzazioni {#permissions}

Precedentemente, nell’interfaccia classica, era necessario prestare particolare attenzione allo sviluppo per facilitare la differenziazione dell’AEM (ad esempio utilizzando `cq:text` libreria di tag o integrazione personalizzata `DiffService` servizio OSGi nei componenti). Questa funzione non è più necessaria per la nuova funzione di differenze, poiché la differenza si verifica lato client tramite il confronto DOM.

Tuttavia, esistono alcune limitazioni che devono essere prese in considerazione dallo sviluppatore.

* Questa funzione utilizza classi CSS senza spazio tra nomi e prodotti AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione delle differenze potrebbe esserne influenzata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la differenze è lato client ed viene eseguita al caricamento della pagina, eventuali modifiche apportate al DOM dopo l’esecuzione del servizio differenze lato client non verranno contabilizzate. Questo può influire

   * Componenti che utilizzano l’AJAX per includere i contenuti
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che manipolano il DOM in seguito all’interazione dell’utente.

>[!NOTE]
>
>Il confronto delle differenze di pagina funziona solo per i componenti che hanno nodi cq:editConfig validi.
