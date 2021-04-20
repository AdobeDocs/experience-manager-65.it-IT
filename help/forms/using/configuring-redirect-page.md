---
title: Configurazione della pagina di reindirizzamento
seo-title: Configurazione della pagina di reindirizzamento
description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina web che gli autori del modulo possono configurare durante la creazione del modulo.
seo-description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina web che gli autori del modulo possono configurare durante la creazione del modulo.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Configurazione della pagina di reindirizzamento{#configuring-redirect-page}

Gli autori dei moduli possono configurare una pagina per ciascun modulo, a cui verranno reindirizzati gli utenti dopo l’invio.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi fai clic su ![cmppr](assets/cmppr.png).

1. Nella barra laterale fate clic su **Invio**.

1. Fornisci l’URL della pagina di reindirizzamento alla sezione Pagina di ringraziamento nella sezione Invio .
1. Facoltativamente, in Azione di invio per l’azione Invia a endpoint REST è possibile configurare il parametro da passare alla pagina di reindirizzamento.

![Reindirizza la configurazione della pagina](assets/thank-you-setting-1.png)

Reindirizza la configurazione della pagina

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, vengono passati i parametri `status` e `owner` . Oltre a questi due parametri, vengono passati alcuni parametri aggiuntivi per le seguenti azioni di invio:

* **Azione**  contenuto store (obsoleta) :  `contentPath`- viene passato il percorso del nodo nell&#39;archivio in cui sono archiviati i dati inviati.

* **Azione**  Store PDF (obsoleta) :  `contentPath`—dei dati inviati e del percorso del nodo che memorizza il file PDF nel repository—viene passato.

* **Invia al flusso di lavoro** Forms: I parametri di output restituiti dal flusso di lavoro dei moduli vengono trasmessi.

* **Invia all’endpoint** REST: I parametri aggiunti per la mappatura in-field ai parametri vengono passati. `status` e  `owner` i parametri non vengono passati in questa azione di invio. Per ulteriori informazioni, consulta [Configurazione dell’azione Invia all’endpoint REST](../../forms/using/configuring-submit-actions.md).

