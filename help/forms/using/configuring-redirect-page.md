---
title: Configurazione della pagina di reindirizzamento
description: Dopo aver compilato un modulo adattivo, gli utenti possono essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: be1a774f-5681-443f-b195-28e89a020547
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 4%

---

# Configurazione della pagina di reindirizzamento{#configuring-redirect-page}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html?lang=it) |
| AEM 6.5 | Questo articolo |

Gli autori dei moduli possono configurare una pagina per ogni modulo, alla quale gli utenti vengono reindirizzati dopo l&#39;invio di un modulo.

1. In modalità di modifica, seleziona un componente, quindi fai clic su ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi fai clic su ![cmppr](assets/cmppr.png).

1. Nella barra laterale fare clic su **Invio**.

1. Immetti l’URL della pagina di reindirizzamento in Pagina di ringraziamento nella sezione Invio.
1. Facoltativamente, in Azione di invio, per l’azione Invia a endpoint REST, puoi configurare il parametro da passare alla pagina di reindirizzamento.

![Configurazione pagina di reindirizzamento](assets/thank-you-setting-1.png)

Configurazione pagina di reindirizzamento

Gli autori dei moduli possono utilizzare i seguenti parametri passati alla pagina di ringraziamento. Per tutte le azioni di invio disponibili, vengono passati `status` e `owner` parametri. Oltre a questi due parametri, vengono passati alcuni parametri aggiuntivi per le seguenti azioni di invio:

* **Azione contenuto archivio** (obsoleto): `contentPath`, il percorso del nodo nell&#39;archivio in cui sono archiviati i dati inviati, è passato.

* **Azione PDF archivio** (obsoleta): `contentPath` dei dati e del percorso inviati al nodo che memorizza il file PDF nell&#39;archivio è stato passato.

* **Invia a flusso di lavoro Forms**: i parametri di output restituiti dal flusso di lavoro dei moduli sono stati passati.

* **Invia all&#39;endpoint REST**: i parametri aggiunti per la mappatura interna al campo al parametro vengono passati. Parametri `status` e `owner` non passati in questa azione di invio. Per ulteriori informazioni, vedere [Configurazione dell&#39;azione di invio Invia all&#39;endpoint REST](../../forms/using/configuring-submit-actions.md).
