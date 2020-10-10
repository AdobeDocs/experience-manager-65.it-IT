---
title: Note sulla versione del [!DNL Adobe Experience Manager Assets] 6.5.
description: The new capabilities and enhancements to [!DNL Adobe Experience Manager] 6.5 [!DNL Assets].
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 41%

---


# [!DNL Adobe Experience Manager Assets] note sulla versione {#aem-assets-release-notes}

Here are the key features and highlights of the [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] release.

## Integration with [!DNL Adobe Creative Cloud] and creative workflows {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] offre varie modalità di integrazione in e condivisione delle risorse da utilizzare nei flussi di lavoro che coinvolgono i team creativi e quelli di marketing o commerciali.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continua a sviluppare e semplificare l’integrazione per garantire maggiori opportunità e migliorare i metodi esistenti.

Read on to know the specific capabilities and integrations of [!DNL Experience Manager] 6.5 that you can leverage to best support your content velocity use cases.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] rafforza la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti. Creatives can access content stored in [!DNL Experience Manager Assets], without leaving the apps that they are most familiar with. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign] apps.

[!DNL Adobe Asset Link] è una parte della [Creative Cloud per l&#39;offerta enterprise](https://www.adobe.com/it/creativecloud/business/enterprise.html) . For more information about it, including necessary configuration of your [!DNL Experience Manager] deployment, see [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

![Cercare risorse in  Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] integration {#stock}

Your organization can use its [!DNL Adobe Stock] enterprise plan within [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for your creative and marketing projects. You can quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in Experience Manager, using the powerful DAM capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock]Il servizio offre a designer e aziende l’accesso a milioni di foto, immagini vettoriali, illustrazioni, video, modelli e risorse 3D di alta qualità, curate ed esenti da royalty, per qualsiasi progetto creativo.

For more info, see [Use Adobe Stock assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Anteprima  immagine e licenza Adobe Stock da  risorse Experience Manager](assets/stock_image_preview_license_options.png)

*Figura: Visualizza in anteprima[!DNL Adobe Stock]immagini e licenze dall&#39;interno[!DNL Experience Manager Assets].*

![Cercare e filtrare le immagini Adobe Stock  licenza in  Experience Manager](assets/aem-search-filters2.jpg)

*Figura: Cercate e filtrate le[!DNL Adobe Stock]immagini con licenza in[!DNL Experience Manager].*

### Dynamic references in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilizzati nei [!DNL Adobe InDesign] file sono dinamici. I riferimenti vengono aggiornati automaticamente se le risorse a cui si fa riferimento si spostano nella directory archivio. Per ulteriori informazioni, consultate [Gestione delle risorse](/help/assets/managing-linked-subassets.md)composte.

## Funzionalità di Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] consente di acquisire facilmente, controllare efficacemente e distribuire in modo sicuro le risorse approvate a fornitori/agenzie esterne e utenti aziendali interni su tutti i dispositivi. Consente di migliorare l’efficienza della condivisione delle risorse, accelera il time-to-market delle risorse ed elimina il rischio di utilizzo non conforme e di accesso non autorizzato.

Per ulteriori informazioni, consulta [Scopri le novità di Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Risorse collegate {#connectedassets}

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzioni di creazione di siti web e le risorse digitali richieste risiedono in silos diversi.

[!DNL Experience Manager Sites] offre la funzionalità di creazione di pagine web e è il sistema di gestione delle risorse digitali (DAM) che fornisce le risorse necessarie per i siti web. [!DNL Experience Manager Assets] [!DNL Experience Manager] supporta ora il caso d&#39;uso di cui sopra integrando [!DNL Sites] e [!DNL Assets]. Scopri [come configurare e utilizzare la funzione](/help/assets/use-assets-across-connected-assets-instances.md)Risorse connesse.

![Trascinamento di una risorsa da una [!DNL Experience Manager] distribuzione su una [!DNL Sites] pagina di un&#39;altra [!DNL Experience Manager] distribuzione](assets/connected-assets-drag-and-drop-only.gif)

*Figura: Trascinate una risorsa da una[!DNL Experience Manager]distribuzione su una[!DNL Sites]pagina in un’altra[!DNL Experience Manager]distribuzione.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] offre funzionalità avanzate di authoring e distribuzione di contenuti multimediali [!DNL Experience Manager Assets] per creare esperienze all&#39;avanguardia coinvolgenti e personalizzate. Caricando una singola risorsa principale di alta qualità e utilizzando il rendering cloud e i visualizzatori avanzati, potete distribuire al volo qualsiasi combinazione di rappresentazioni per supportare la strategia media aziendale.

For more details on new [!DNL Dynamic Media] features see [Dynamic Media Release Notes](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### 360 video support {#video-support}

Manage your 360-video files directly in [!DNL Experience Manager] using the cutting edge viewers to deliver VR-experiences to desktops, mobile and VR-headsets. Per ulteriori informazioni, consulta [Utilizzare i video a 360°](/help/assets/360-video.md).

### Custom video thumbnails {#custom-video-thumbnails}

È ora possibile personalizzare le miniature delle risorse video utilizzando fotogrammi dal video stesso o altri contenuti memorizzati nel sistema DAM. Per ulteriori istruzioni, consulta la sezione sulle [miniature video](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Miglioramenti dell’accessibilità {#accessibility-enhancements}

[!DNL Dynamic Media] i visualizzatori ora supportano funzioni di accessibilità avanzate come Aria-support, assistenti vocali e Alt-text. Per ulteriori dettagli, consulta le [note sulla versione per i visualizzatori di Dynamic Media](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html).

## Miglioramento dell’esperienza di ricerca {#experience-enhancement-for-searching}

[!DNL Experience Manager] A partire da 6.5, gli addetti al marketing possono individuare più rapidamente le risorse desiderate dalla pagina dei risultati della ricerca. I facet di ricerca vengono aggiornati con il numero di risorse anche prima di applicare il filtro di ricerca. La visualizzazione del conteggio previsto per il filtro consente agli utenti di navigare in modo efficiente tra i risultati della ricerca. Per ulteriori informazioni, consultate [Cercare risorse in  Experience Manager](../assets/search-assets.md).

![Visualizzazione del numero di risorse senza filtrare i risultati nei facet di ricerca](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figura: Visualizzate il numero di risorse senza filtrare i risultati di ricerca nei facet di ricerca.*

## Miglioramento dell’usabilità {#usability-enhancement}

Ora potete selezionare tutte le risorse caricate all’interno di una cartella o da un risultato di ricerca in una sola volta. Consente di gestire rapidamente più risorse. The check box selects all the assets that fits the scenario, say a search result and not just the assets that are visible in the [!DNL Experience Manager] interface.

![Utilizzate l&#39;opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.](assets/select-all-in-aem-assets.gif)

*Figura: Usate l’opzione Seleziona tutto per selezionare tutte le risorse caricate con un solo clic.*

## Miglioramenti dei metadati {#metadata-enhancements}

[!DNL Assets] consente di creare schemi di metadati per le cartelle delle risorse, che definiscono il layout e i metadati visualizzati nelle pagine di proprietà delle cartelle. È ora possibile assegnare uno schema di metadati di una cartella a una cartella esistente o quando si crea una nuova cartella. Per ulteriori informazioni, consulta [Schema metadati cartelle](/help/assets/metadata-config.md#folder-metadata-schema).

Quando si specificano i metadati a cascata, le selezioni possono essere caricate da un file JSON in fase di runtime, ad es. invece di digitare manualmente nel modulo. For more information, see [cascading metadata](/help/assets/metadata-schemas.md#cascading-metadata).

## Miglioramenti della creazione di rapporti {#reporting-enhancements}

I frammenti di contenuto e le condivisioni di collegamenti sono ora inclusi nel rapporto scaricato. Per ulteriori informazioni, consulta la sezione sui [rapporti sulle risorse](/help/assets/asset-reports.md).
