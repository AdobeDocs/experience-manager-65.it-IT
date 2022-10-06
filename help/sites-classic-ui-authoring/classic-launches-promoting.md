---
title: Promozione dei lanci
seo-title: Promoting Launches
description: Con la promozione delle pagine di lancio si sposta il contenuto nella sorgente (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa.
seo-description: You need to promote launch pages to move the content back into the source (production) before publishing. When a launch page is promoted, the corresponding page of the source pages is replaced with the content of the promoted page.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 91%

---

# Promozione dei lanci{#promoting-launches}

Con la promozione delle pagine di lancio si sposta il contenuto nella sorgente (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Quando si promuove una pagina di lancio, sono disponibili le seguenti opzioni:

* Promuovere solo la pagina corrente o l’intero lancio.
* Promuovere le pagine figlie della pagina corrente.
* Promuovere il lancio completo o solo le pagine che sono state modificate.

## Promozione delle pagine di lancio {#promoting-launch-pages}

Per promuovere le pagine, esegui le seguenti operazioni durante la modifica della pagina di lancio da promuovere:

1. Nella scheda **Pagina** nella barra laterale, fai clic su **Promuovi lancio**.
1. Specifica le pagine da promuovere:

   * (Impostazione predefinita) Per promuovere solo la pagina corrente, seleziona **Promuovi modifiche pagina a versione produzione**.
   * Per promuovere anche le pagine figlie della pagina corrente, seleziona **Includi sottopagine**.
   * Per promuovere tutte le pagine del lancio, seleziona **Promuovi lancio completo alla versione in produzione**.

1. Per aggiungere le pagine di produzione a un pacchetto flusso di lavoro, seleziona **Aggiungi al pacchetto flusso di lavoro**, quindi selezionalo.
1. Fai clic su **Promuovi**.

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

I modelli di flusso di lavoro consentono di eseguire operazioni di elaborazione collettive sulle pagine di lancio promosse:

1. Crea un pacchetto di flusso di lavoro.
1. Quando gli autori promuovono le pagine di lanci, queste vengono memorizzate nel pacchetto di flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando vengono promosse le pagine, [configura un programma di avvio del flusso di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) per il nodo del pacchetto.

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un programma di avvio per avviare il flusso di lavoro Attivazione richiesta quando viene modificato il nodo del pacchetto.

![chlimage_1-136](assets/chlimage_1-136.png)
