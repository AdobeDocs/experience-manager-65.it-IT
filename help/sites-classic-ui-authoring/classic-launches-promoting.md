---
title: Promozione dei lanci
description: Con la promozione delle pagine di lancio si sposta il contenuto nell’origine (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# Promozione dei lanci{#promoting-launches}

Con la promozione delle pagine di lancio si sposta il contenuto nell’origine (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Quando promuovi una pagina di lancio sono disponibili le seguenti opzioni:

* Promuovere solo la pagina corrente o l’intero lancio.
* Promuovere le pagine figlie della pagina corrente.
* Promuovere il lancio completo o solo le pagine che sono state modificate.

## Promozione delle pagine di lancio {#promoting-launch-pages}

Per promuovere le pagine, effettua le seguenti operazioni durante la modifica della pagina di lancio che desideri promuovere:

1. Il giorno **Pagina** nel Sidekick, fare clic su **Promuovi lancio**.
1. Specifica le pagine da promuovere:

   * Impostazione predefinita. Per promuovere solo la pagina corrente, seleziona **Promuovi modifiche pagina a versione produzione**.
   * Per promuovere anche le pagine figlie della pagina corrente, seleziona **Includi sottopagine**.
   * Per promuovere tutte le pagine del lancio, seleziona **Promuovi Lancio Completo A Versione Produzione**.

1. Per aggiungere le pagine di produzione a un pacchetto del flusso di lavoro, seleziona **Aggiungi al pacchetto flusso di lavoro** e quindi selezionare il pacchetto del flusso di lavoro.
1. Clic **Promuovi**.

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

Utilizza i modelli di flusso di lavoro per eseguire l’elaborazione in blocco delle pagine di lanci promosse:

1. Crea un pacchetto flusso di lavoro.
1. Quando gli autori promuovono le pagine di lanci, queste vengono memorizzate nel pacchetto flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando le pagine vengono promosse, [configurare un modulo di avvio del flusso di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) per il nodo del pacchetto.

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un modulo di avvio del flusso di lavoro per avviare il flusso di lavoro Richiesta attivazione quando viene modificato il nodo del pacchetto.

![chlimage_1-136](assets/chlimage_1-136.png)
