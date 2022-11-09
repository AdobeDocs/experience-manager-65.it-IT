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
ht-degree: 10%

---

# Sviluppo e differenze tra pagine{#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione di contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. Un autore desidera poter confrontare la pagina corrente con una versione precedente affiancata alle differenze evidenziate.

Le differenze tra pagine consentono a un utente di confrontare la pagina corrente con gli avvii, le versioni precedenti e così via. Per informazioni dettagliate su questa funzione utente, consulta [Differenze tra pagine](/help/sites-authoring/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata da AEM in background per facilitare le differenze. È necessario per poter eseguire il rendering del contenuto [per un confronto affiancato](/help/sites-developing/pagediff.md#operation-details).

Questa operazione di ricreazione viene eseguita da AEM internamente ed è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio in CRX DE Lite, vedrebbe queste versioni ricreati all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella posizione seguente:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Autorizzazioni {#permissions}

In precedenza, nell’interfaccia classica, era necessario prestare particolare attenzione allo sviluppo per facilitare la diffusione AEM (ad esempio l’utilizzo di `cq:text` libreria a tag, o personalizzata che integra `DiffService` servizio OSGi nei componenti). Questa funzione non è più necessaria per la nuova funzione di confronto delle differenze, in quanto si verifica sul lato client tramite il confronto DOM.

Tuttavia, lo sviluppatore deve tenere in considerazione una serie di limitazioni.

* Questa funzione utilizza classi CSS che non hanno nomi separati nel Prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione del confronto potrebbe essere interessata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la differenza è lato client ed è eseguita al caricamento della pagina, non verranno prese in considerazione eventuali modifiche al DOM dopo l’esecuzione del servizio di diff lato client. Ciò può influire

   * Componenti che utilizzano AJAX per includere i contenuti
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che manipolano il DOM in base all’interazione dell’utente.

>[!NOTE]
>
>Il confronto delle differenze tra pagine funziona solo per i componenti che hanno nodi cq:editConfig validi.
