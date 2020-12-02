---
title: Configurazione della pagina di reindirizzamento
seo-title: Configurazione della pagina di reindirizzamento
description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina Web che gli autori del modulo possono configurare durante la creazione del modulo.
seo-description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina Web che gli autori del modulo possono configurare durante la creazione del modulo.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Configurazione della pagina di reindirizzamento{#configuring-redirect-page}

Gli autori dei moduli possono configurare una pagina per ciascun modulo, alla quale verranno reindirizzati gli utenti dopo l&#39;invio del modulo.

1. In modalità di modifica, selezionare un componente, quindi fare clic su ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi fare clic su ![cmppr](assets/cmppr.png).

1. Nella barra laterale, fare clic su **Invio**.

1. Fornite l’URL della pagina di reindirizzamento nella sezione Pagina di ringraziamento della sezione Invio.
1. Facoltativamente, in Invia azione, per l’azione Invia a endpoint REST è possibile configurare il parametro da passare alla pagina di reindirizzamento.

![Reindirizza configurazione pagina](assets/thank-you-setting-1.png)

Reindirizza configurazione pagina

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, vengono passati i parametri `status` e `owner`. Oltre a questi due parametri, alcuni parametri aggiuntivi vengono passati per le seguenti azioni di invio:

* **Azione**  contenuto store (obsoleto):  `contentPath`— il percorso del nodo nell&#39;archivio in cui sono memorizzati i dati inviati.

* **Azione**  Store PDF (obsoleto):  `contentPath`—dei dati inviati e del percorso del nodo in cui è memorizzato il file PDF nella directory archivio—viene passato.

* **Invia al flusso di lavoro** Forms: I parametri di output restituiti dal flusso di lavoro dei moduli vengono passati.

* **Invia a endpoint** REST: I parametri aggiunti per la mappatura in-field ai parametri vengono passati. `status` e  `owner` i parametri non vengono passati in questa azione di invio. Per ulteriori informazioni, vedere [Configurazione dell&#39;azione Invia a endpoint REST](../../forms/using/configuring-submit-actions.md).

