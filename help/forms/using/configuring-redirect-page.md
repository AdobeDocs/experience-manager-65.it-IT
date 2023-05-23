---
title: Configurazione della pagina di reindirizzamento
seo-title: Configuring redirect page
description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configurazione della pagina di reindirizzamento{#configuring-redirect-page}

Gli autori dei moduli possono configurare una pagina per ogni modulo, alla quale gli utenti vengono reindirizzati dopo l&#39;invio di un modulo.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![a livello di campo](assets/field-level.png) > **Contenitore modulo adattivo** e quindi fare clic su ![cmppr](assets/cmppr.png).

1. Nella barra laterale, fai clic su **Invio**.

1. Immetti l’URL della pagina di reindirizzamento in Pagina di ringraziamento nella sezione Invio.
1. Facoltativamente, in Azione di invio, per l’azione Invia a endpoint REST, puoi configurare il parametro da passare alla pagina di reindirizzamento.

![Configurazione pagina di reindirizzamento](assets/thank-you-setting-1.png)

Configurazione pagina di reindirizzamento

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, `status` e `owner` i parametri vengono passati. Oltre a questi due parametri, vengono passati alcuni parametri aggiuntivi per le seguenti azioni di invio:

* **Azione contenuto store** (obsoleto) : `contentPath`: viene passato il percorso del nodo nell’archivio in cui sono memorizzati i dati inviati.

* **Azione Store PDF** (obsoleto) : `contentPath`: dei dati inviati e del percorso del nodo in cui è memorizzato il file PDF nell’archivio.

* **Invia a flusso di lavoro Forms**: vengono passati i parametri di output restituiti dal flusso di lavoro dei moduli.

* **Invia all’endpoint REST**: vengono passati i parametri aggiunti per la mappatura in-field ai parametri. `status` e `owner` I parametri non vengono passati in questa azione di invio. Per ulteriori informazioni, consulta [Configurazione dell’azione di invio Invia all’endpoint REST](../../forms/using/configuring-submit-actions.md).
