---
title: Introduzione a [!DNL Adobe Experience Manager Assets]
description: Scopri cosa sono la gestione delle risorse digitali, i relativi casi d’uso e [!DNL Adobe Experience Manager Asset] offerta.
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 33%

---

# Informazioni [!DNL Adobe Experience Manager Assets] come soluzione DAM {#administering-assets}

[!DNL Assets] è uno strumento di gestione delle risorse digitali (DAM) che è parte integrante del [!DNL Experience Manager] e consente alle aziende di gestire e distribuire le risorse digitali. Gli utenti di un’organizzazione possono gestire, archiviare e accedere a numerosi tipi di risorse digitali quali immagini, video, documenti, clip audio, file 3D e contenuti multimediali avanzati da utilizzare sul web, nella stampa e per la distribuzione digitale.

## Che cos’è Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets] consente di condividere e distribuire le risorse digitali chiave di un’organizzazione in tutta l’azienda. Gli utenti di un’organizzazione possono archiviare, gestire e accedere a risorse digitali quali immagini, elementi grafici, audio, video e documenti tramite un’interfaccia Web (o una cartella CIFS o WebDAV).

[!DNL Assets] capacità [!DNL Experience Manager] consente di effettuare le seguenti operazioni:

* Aggiungere e condividere immagini, documenti, file audio e video in diversi formati.
* Gestisci le risorse raggruppandole per tag, lightbox o stelle (i tuoi preferiti). Aggiungere note alle risorse.
* Trovare risorse cercando il nome dei file, l’intero testo dei documenti in base a data, tipo di documento e tag.
* Aggiungere o modificare le informazioni sui metadati per le risorse. La versione dei metadati viene adeguata automaticamente alla relativa risorsa. È possibile importare o esportare i metadati delle risorse.
* Utilizzare funzioni di modifica delle immagini come il ridimensionamento e l’aggiunta di filtri. È possibile importare ed esportare contemporaneamente più risorse digitali utilizzando una cartella WebDAV o CIFS.
* Utilizzare flussi di lavoro e notifiche per consentire l’elaborazione e il download simultanei di qualsiasi insieme di risorse e gestire i diritti di accesso alle risorse.

### [!DNL Experience Manager Assets] è integrato con [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] si integra completamente con [!DNL Sites] e funziona senza problemi per tutti i casi d&#39;uso. Ad esempio, durante la creazione di pagine web, il [!DNL Sites] Gli autori possono trovare e utilizzare le risorse digitali tramite Content Finder. Interfaccia utente di [!DNL Assets] è uguale a quello di [!DNL Sites]. Vedi [panoramica di Sites](/help/sites-authoring/page-authoring.md) per informazioni complete.

L’interfaccia utente di base è la stessa di [!DNL Sites]. Vedi [Panoramica dei siti](/help/sites-authoring/page-authoring.md) per informazioni complete.

### Digital Asset Management e componente immagine {#digital-asset-management-versus-image-component}

Per determinare se inserire un’immagine nell’archivio DAM o utilizzare un componente immagine, considera il ciclo di vita dell’immagine:

* Se l&#39;immagine ha lo stesso ciclo di vita della pagina, utilizza il componente Immagine .
* Se l’immagine presenta un ciclo di vita separato, ad esempio se devi utilizzare l’immagine due volte o all’esterno di WCM, utilizza [!DNL Assets].

## Cosa sono le risorse digitali? {#what-are-digital-assets}

Una risorsa è un documento, un’immagine, un video o dell’audio digitale (o parte di essi) che può avere più rappresentazioni e risorse secondarie (ad esempio, livelli in un file Photoshop, slide in un file PowerPoint, pagine in un file pdf, file in un file ZIP).

Una risorsa, in pratica, è composta da un file binario, da metadati, da rappresentazioni e da risorse secondarie. Consulta la [Guida alle prestazioni di DAM](/help/sites-deploying/assets-performance-sizing.md) per informazioni dettagliate.

>[!CAUTION]
>
>Il caricamento e/o la modifica di un grande volume di risorse (in particolare di immagini) può influire sulle prestazioni del [!DNL Experience Manager] distribuzione.

### [!DNL Experience Manager Assets] terminologia {#aem-assets-terminology}

Quando si lavora con risorse digitali in [!DNL Experience Manager], è necessario comprendere la seguente terminologia:

* **Raccolta**: Una raccolta di risorse in base alla posizione fisica (cartella), alle proprietà comuni (cartella di ricerca salvata) o alla selezione dell’utente (cartelle lightbox).

* **Metadati** [!DNL Assets] avere metadati; ad esempio autore, data di scadenza, informazioni DRM (Digital Rights Management) e così via. I metadati disponibili dipendono dalle autorizzazioni di accesso. [!DNL Assets] offre e supporta i seguenti schemi di metadati di uso comune:

   * Dublin Core: comprende autore, descrizione, data, oggetto e così via.
   * IPTC: comprende evento, modello, luogo e così via.
   * WCM: comprese le proprietà della pagina, [!UICONTROL Ora di attivazione] e [!UICONTROL Ora di disattivazione]e così via.

* **Assegnazione tag**: [!DNL Assets] possono essere contrassegnati e classificati. Vedi [organizzazione delle risorse](/help/assets/organize-assets.md).

* **Rendering**: Un rendering è la rappresentazione binaria di una risorsa. [!DNL Assets] hanno sempre una rappresentazione principale, quella del file caricato. Possono disporre di diverse rappresentazioni aggiuntive create, ad esempio, dai passaggi personalizzati del flusso di lavoro o durante il caricamento di una risorsa. Le rappresentazioni possono essere di dimensioni diverse, con diverse risoluzioni, con filigrana aggiunta o altre caratteristiche modificate.

* **Versioni**: Il controllo delle versioni crea un’istantanea delle risorse digitali in un momento specifico. Se necessario, puoi ripristinare le risorse alle versioni precedenti. Vedi [versione in [!DNL Assets]](manage-assets.md#asset-versioning).

* **Risorse secondarie**: Le risorse secondarie sono risorse che costituiscono una risorsa, ad esempio i livelli in una [!DNL Adobe Photoshop] in un file PDF. In [!DNL Assets], puoi gestire le risorse secondarie in modo analogo alle risorse.

### Come lavorare con le risorse digitali {#how-to-work-with-assets}

È possibile intervenire su una risorsa o una raccolta eseguendo specifiche azioni per creare o modificare risorse, raccolte e rappresentazioni. Molte delle azioni di base eseguite sulle risorse (caricamento, eliminazione, aggiornamento, salvataggio di risorse secondarie) attivano flussi di lavoro preconfigurati. che vengono attivate automaticamente [!DNL Assets] e sono descritti in dettaglio in [!DNL Assets] gestori di contenuti multimediali.

Le attività eseguibili con questi flussi di lavoro preconfigurati:

* Salva la risorsa nell’archivio o eliminala.
* Estrarre e salvare i metadati della risorsa; i singoli elementi di metadati vengono salvati come XMP.
* Genera rappresentazioni e miniature della risorsa; compreso, se necessario, il ridimensionamento e il ritaglio automatici.
* Se necessario, transcodifica la risorsa. Ad esempio, i video per dispositivi mobili e web vengono codificati con 24 fotogrammi al secondo, quelli per il download con 30 fotogrammi al secondo. L&#39;audio per dispositivi mobili e web viene codificato a 128 Kbps, quello per il download a 192 Kbps.

Ovviamente, puoi applicare i flussi di lavoro anche manualmente. Per un elenco dei flussi di lavoro predefiniti, consulta [Gestori di contenuti multimediali di Assets ](media-handlers.md).

## [!DNL Experience Manager Assets] e [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Vedi [Risorse e Media Library](medialibrary.md) per informazioni sulle differenze.

>[!MORELIKETHIS]
>
>* [Video introduttivo - Experience Manager Assets come DAM moderno](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Concetti di metadati](/help/assets/metadata-concepts.md)

