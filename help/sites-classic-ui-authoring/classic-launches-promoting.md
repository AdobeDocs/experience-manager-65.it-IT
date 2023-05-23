---
title: Promozione dei lanci
description: È necessario promuovere le pagine di lancio per spostare nuovamente il contenuto nell’origine (produzione) prima di pubblicarlo. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 21%

---

# Promozione dei lanci{#promoting-launches}

È necessario promuovere le pagine di lancio per spostare nuovamente il contenuto nell’origine (produzione) prima di pubblicarlo. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Durante la promozione di una pagina di lancio sono disponibili le seguenti opzioni:

* Indica se promuovere solo la pagina corrente o l’intero lancio.
* Indica se promuovere le pagine figlie della pagina corrente.
* Indica se promuovere l’intero lancio o solo le pagine che sono state modificate.

## Promozione delle pagine di lancio {#promoting-launch-pages}

Per promuovere le pagine, effettua le seguenti operazioni durante la modifica della pagina di lancio che desideri promuovere:

1. Il giorno **Pagina** nella barra laterale, fai clic su **Promuovi lancio**.
1. Specifica le pagine da promuovere:

   * Impostazione predefinita. Per promuovere solo la pagina corrente, seleziona **Promuovi modifiche pagina a versione produzione**.
   * Per promuovere anche le pagine figlie della pagina corrente, seleziona **Includi sottopagine**.
   * Per promuovere tutte le pagine del lancio, seleziona **Promuovi Lancio Completo A Versione Produzione**.

1. Per aggiungere le pagine di produzione a un pacchetto del flusso di lavoro, seleziona **Aggiungi al pacchetto flusso di lavoro** e quindi selezionare il pacchetto del flusso di lavoro.
1. Clic **Promuovi**.

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

Utilizza i modelli di flusso di lavoro per eseguire l’elaborazione in blocco delle pagine dei lanci promossi:

1. Creare un pacchetto di flusso di lavoro.
1. Quando gli autori promuovono le pagine di Launch, le memorizzano nel pacchetto del flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando le pagine vengono promosse, [configurare un modulo di avvio del flusso di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) per il nodo del pacchetto.

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un modulo di avvio del flusso di lavoro per avviare il flusso di lavoro Attivazione richiesta quando viene modificato il nodo del pacchetto.

![chlimage_1-136](assets/chlimage_1-136.png)
