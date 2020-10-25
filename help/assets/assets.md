---
title: Introduzione a [!DNL Adobe Experience Manager Assets].
description: Scopri cos’è la gestione delle risorse digitali, i relativi casi di utilizzo e [!DNL Adobe Experience Manager Asset] il offerta.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 35%

---


# Informazioni [!DNL Adobe Experience Manager Assets] come soluzione DAM {#administering-assets}

[!DNL Assets] è uno strumento Digital Asset Management (DAM) che è parte integrante della [!DNL Experience Manager] piattaforma e consente alla vostra azienda di gestire e distribuire risorse digitali. Gli utenti di un’organizzazione possono gestire, archiviare e accedere a numerosi tipi di risorse digitali, come immagini, video, documenti, clip audio, file 3D e contenuti multimediali da usare sul Web, nella stampa e per la distribuzione digitale.

## Che cos’è Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets] consente di condividere e distribuire le risorse digitali chiave di un’organizzazione in tutta l’azienda. Gli utenti di un’organizzazione possono archiviare, gestire e accedere a risorse digitali come immagini, elementi grafici, audio, video e documenti tramite un’interfaccia Web (o una cartella CIFS o WebDAV).

[!DNL Assets] consente di [!DNL Experience Manager] effettuare le seguenti operazioni:

* Aggiungere e condividere immagini, documenti, file audio e video in diversi formati.
* Gestire le risorse raggruppandole in base a tag, lightbox o stelle (preferiti). Aggiungere note alle risorse.
* Trovare risorse cercando il nome dei file, l’intero testo dei documenti in base a data, tipo di documento e tag.
* Aggiungere o modificare le informazioni sui metadati per le risorse. La versione dei metadati viene adeguata automaticamente alla relativa risorsa. È possibile importare o esportare i metadati delle risorse.
* Utilizzare funzioni di modifica delle immagini come il ridimensionamento e l’aggiunta di filtri. È possibile importare ed esportare contemporaneamente più risorse digitali utilizzando una cartella WebDAV o CIFS.
* Utilizzare flussi di lavoro e notifiche per consentire l’elaborazione e il download simultanei di qualsiasi insieme di risorse e gestire i diritti di accesso alle risorse.

### [!DNL Experience Manager Assets] è integrato con [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] si integra completamente con [!DNL Sites] e funziona perfettamente per tutti i casi di utilizzo. Ad esempio, durante la creazione di pagine Web, gli [!DNL Sites] autori possono trovare e utilizzare le risorse digitali tramite Content Finder. L&#39;interfaccia utente di [!DNL Assets] è uguale a quella di [!DNL Sites]. Per informazioni dettagliate, consultate [la panoramica dei siti](/help/sites-authoring/page-authoring.md) .

L&#39;interfaccia utente di base è la stessa di [!DNL Sites]. Per informazioni dettagliate, consulta [Panoramica dei siti](/help/sites-authoring/page-authoring.md) .

### Digital Asset Management e componente immagine {#digital-asset-management-versus-image-component}

Per determinare se inserire un’immagine nell’archivio DAM o utilizzare un componente immagine, considera il ciclo di vita dell’immagine:

* Se l’immagine ha lo stesso ciclo di vita della pagina, utilizza il componente immagine.
* Se l’immagine presenta un ciclo di vita separato, ad esempio se devi utilizzare l’immagine due volte o all’esterno di WCM, utilizza [!DNL Assets].

## Cosa sono le risorse digitali? {#what-are-digital-assets}

Una risorsa è un documento digitale, un’immagine, un video o un file audio (o parte di esso) che può avere più rappresentazioni e risorse secondarie (ad esempio, livelli in un file Photoshop, diapositive in un file PowerPoint, pagine in un pdf, file in un file ZIP).

Una risorsa, in pratica, è composta da un file binario, da metadati, da rappresentazioni e da risorse secondarie. Consulta la [Guida alle prestazioni di DAM](/help/sites-deploying/assets-performance-sizing.md) per informazioni dettagliate.

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] deployment.

### [!DNL Experience Manager Assets] terminologia {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], you need to understand the following terminology:

* **Raccolta**: Una raccolta di risorse, basata sulla posizione fisica (cartella), sulle proprietà comuni (cartella di ricerca salvata) o sulla selezione dell’utente (cartelle lightbox).

* **I metadati** sono [!DNL Assets] metadati; ad esempio autore, data di scadenza, informazioni DRM (Digital Rights Management) e così via. I metadati disponibili dipendono dalle autorizzazioni di accesso. [!DNL Assets] offre e supporta i seguenti schemi di metadati di uso comune:

   * Dublin Core: comprende autore, descrizione, data, oggetto e così via.
   * IPTC: comprende evento, modello, luogo e così via.
   * WCM: incluse le proprietà della pagina, [!UICONTROL Ora] di attivazione e [!UICONTROL Ora]di disattivazione e così via.

* **Assegnazione tag**: [!DNL Assets] può essere contrassegnato e classificato. Consultate [Organizzazione delle risorse](/help/assets/organize-assets.md).

* **Rappresentazioni**: Una rappresentazione è la rappresentazione binaria di una risorsa. [!DNL Assets] hanno sempre una rappresentazione principale, quella del file caricato. Possono disporre di diverse rappresentazioni aggiuntive create, ad esempio, dai passaggi personalizzati del flusso di lavoro o durante il caricamento di una risorsa. Le rappresentazioni possono essere di dimensioni diverse, con diverse risoluzioni, con filigrana aggiunta o altre caratteristiche modificate.

* **Versioni**: Quando si crea una versione, viene creata un&#39;istantanea delle risorse digitali in un momento specifico. Se necessario, puoi ripristinare le risorse alle versioni precedenti. See [versioning in Assets](manage-assets.md#asset-versioning).

* **Risorse secondarie**: Le risorse secondarie sono risorse che costituiscono una risorsa, ad esempio i livelli di un [!DNL Adobe Photoshop] file o le pagine di un file PDF. In [!DNL Assets], you can manage sub-assets as you would assets.

### How to work with assets {#how-to-work-with-assets}

È possibile intervenire su una risorsa o una raccolta eseguendo specifiche azioni per creare o modificare risorse, raccolte e rappresentazioni. Molte delle azioni di base eseguite sulle risorse (caricamento, eliminazione, aggiornamento, salvataggio di risorse secondarie) attivano flussi di lavoro preconfigurati. These are automatically turned on in [!DNL Assets] and are described in detail in [!DNL Assets] media handlers.

Le attività che puoi eseguire con questi flussi di lavoro preconfigurati:

* Salvate la risorsa nella directory archivio o eliminatela.
* Estrarre e salvare i metadati della risorsa; i singoli elementi di metadati vengono salvati come XMP.
* Generazione di rappresentazioni e miniature per la risorsa; compresi, se necessario, il ridimensionamento e il ritaglio automatici.
* Se necessario, transcodificate la risorsa. Ad esempio, i video per dispositivi mobili e Web sono codificati con 24 fotogrammi al secondo, quelli per il download con 30 fotogrammi al secondo. L&#39;audio per dispositivi mobili e Web viene transcodificato con 128 Kbps, quello per il download con 192 Kbps.

Ovviamente, puoi applicare i flussi di lavoro anche manualmente. Per un elenco dei flussi di lavoro predefiniti, consulta [Gestori di contenuti multimediali di Assets ](/help/assets/media-handlers.md).

## [!DNL Experience Manager Assets] e [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

Consulta [Risorse e MediaLibrary](/help/assets/medialibrary.md) per informazioni sulle differenze.
