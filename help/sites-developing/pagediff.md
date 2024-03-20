---
title: Sviluppo e differenze tra pagine
description: Scopri come sviluppare e utilizzare la funzione di differenze tra pagine in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# Sviluppo e differenze tra pagine{#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore vuole poter confrontare la pagina corrente con una versione precedente evidenziando le differenze.

La differenza di pagina consente a un utente di confrontare la pagina corrente con lanci, versioni precedenti e così via. Per informazioni dettagliate su questa funzione utente, consulta [Differenza di pagina](/help/sites-authoring/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata dall’AEM in background per facilitare la differenza. Questo è necessario per poter eseguire il rendering del contenuto [per il confronto affiancato](/help/sites-developing/pagediff.md#operation-details).

Questa operazione di ricreazione viene eseguita internamente dall&#39;AEM, è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio, in CRXDE Liti vedrebbe queste versioni ricreato all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella seguente posizione:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Autorizzazioni {#permissions}

Precedentemente, nell’interfaccia classica, era necessario prestare particolare attenzione allo sviluppo per facilitare la differenziazione dell’AEM (ad esempio utilizzando `cq:text` libreria di tag o integrazione personalizzata `DiffService` servizio OSGi nei componenti). Questa funzione non è più necessaria per la nuova funzione di differenze, poiché la differenza si verifica lato client tramite il confronto DOM.

Tuttavia, ci sono alcune limitazioni che devono essere considerate dallo sviluppatore.

* Questa funzione utilizza classi CSS che non fanno parte del namespace del prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione delle differenze potrebbe esserne influenzata.

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
