---
title: Introduzione a [!DNL Adobe Experience Manager Assets]
description: Crea, gestisci, elabora e distribuisci le risorse digitali in Experience Manager. Queste guide descrivono le best practice, le funzioni di accessibilità e l’utilizzo delle risorse di AEM 6.5.
hide: true
feature: Asset Management
role: Leader, Developer, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 4%

---


# Informazioni su [!DNL Adobe Experience Manager Assets] come soluzione DAM {#administering-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/overview) |
| AEM 6.5 | Questo articolo |

AEM [!DNL Assets] è uno strumento di gestione delle risorse digitali (DAM) che fa parte della piattaforma [!DNL Experience Manager] e consente alla tua azienda di gestire e distribuire le risorse digitali. Gli utenti di un’organizzazione possono gestire, archiviare e accedere a molti tipi di risorse digitali, come immagini, video, documenti, clip audio, file 3D e rich media, per utilizzarli sul web, nella stampa e nella distribuzione digitale.

## Che cos’è Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets] consente la condivisione e la distribuzione a livello aziendale delle risorse digitali chiave di un&#39;organizzazione. Gli utenti di un’organizzazione possono archiviare, gestire e accedere a risorse digitali quali immagini, elementi grafici, audio, video e documenti tramite un’interfaccia web (o una cartella CIFS o WebDAV).

La funzionalità [!DNL Assets] di [!DNL Experience Manager] consente di effettuare le seguenti operazioni:

* Aggiungere e condividere immagini, documenti, file audio e file video in vari formati.
* Gestisci le risorse raggruppandole per tag, lightbox o stelle (i tuoi preferiti). Aggiungere annotazioni alle risorse.
* Per trovare le risorse, cercare i nomi dei file, il testo completo dei documenti, le date, il tipo di documento e i tag.
* Aggiungere o modificare le informazioni sui metadati per le risorse. Insieme alla risorsa corrispondente viene automaticamente creata una versione dei metadati. Puoi importare o esportare i metadati delle risorse.
* Eseguire le funzioni di modifica delle immagini, come il ridimensionamento e l&#39;aggiunta di filtri immagine. Importare ed esportare più risorse digitali contemporaneamente utilizzando una cartella WebDAV o CIFS.
* Utilizza i flussi di lavoro e le notifiche per consentire l’elaborazione e il download congiunti di qualsiasi insieme di risorse e gestire i diritti di accesso alle risorse.

### [!DNL Experience Manager Assets] è integrato con [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] si integra completamente con [!DNL Sites] e funziona senza problemi per tutti i casi d&#39;uso. Ad esempio, durante l&#39;authoring delle pagine Web, gli autori [!DNL Sites] possono trovare e utilizzare le risorse digitali tramite Content Finder. L&#39;interfaccia utente di [!DNL Assets] è uguale a quella di [!DNL Sites]. Per informazioni dettagliate, consulta la [panoramica di Sites](/help/sites-authoring/page-authoring.md).

L&#39;interfaccia utente di base è uguale a quella di [!DNL Sites]. Per informazioni dettagliate, vedere [Panoramica dei siti](/help/sites-authoring/page-authoring.md).

### Gestione delle risorse digitali e componente immagine {#digital-asset-management-versus-image-component}

Per determinare se inserire un’immagine nell’archivio DAM o utilizzare un componente immagine, considera il ciclo di vita dell’immagine:

* Se l’immagine ha lo stesso ciclo di vita della pagina, utilizza il componente Immagine.
* Se l&#39;immagine ha un ciclo di vita distinto, ad esempio se l&#39;immagine viene utilizzata due volte o al di fuori di WCM, utilizzare [!DNL Assets].

## Cosa sono le risorse digitali? {#what-are-digital-assets}

Una risorsa è un documento, un’immagine, un video o dell’audio digitale (o parte di essi) che può avere più rappresentazioni. Può anche contenere risorse secondarie, ad esempio livelli in un file Photoshop, slide in un file PowerPoint, pagine in un pdf e file in un file ZIP.

Una risorsa è essenzialmente un binario più metadati più rappresentazioni più risorse secondarie. Per informazioni dettagliate, vedere la [Guida alle prestazioni di DAM](/help/sites-deploying/assets-performance-sizing.md).

>[!CAUTION]
>
>Il caricamento e/o la modifica di un grande volume di risorse (in particolare immagini) può influire sulle prestazioni della distribuzione di [!DNL Experience Manager].

### Terminologia [!DNL Experience Manager Assets] {#aem-assets-terminology}

Quando si lavora con risorse digitali in [!DNL Experience Manager], è utile comprendere la seguente terminologia:

* **Raccolta**: una raccolta di risorse basata sulla posizione fisica (cartella), sulle proprietà comuni (cartella ricerche salvata) o sulla selezione dell&#39;utente (cartelle lightbox).

* **I metadati** [!DNL Assets] contengono metadati, ad esempio Autore, Data di scadenza e Informazioni DRM (Digital Rights Management). I metadati sono sotto controllo di accesso. [!DNL Assets] supporta i seguenti schemi di metadati comuni:

   * Dublin Core: include autore, descrizione, data, oggetto e così via.
   * IPTC: inclusi evento, modello, posizione e così via.
   * WCM: include le proprietà della pagina, [!UICONTROL Ora di attivazione] e [!UICONTROL Ora di disattivazione] e così via.

* **Assegnazione tag**: [!DNL Assets] può essere contrassegnato e classificato. Consulta [organizzazione delle risorse](/help/assets/organize-assets.md).

* **Rappresentazioni**: una rappresentazione è la rappresentazione binaria di una risorsa. [!DNL Assets] ha sempre una rappresentazione primaria, quella del file caricato. Possono disporre di un numero qualsiasi di rappresentazioni aggiuntive create, ad esempio, da passaggi di flusso di lavoro personalizzati o quando viene caricata una risorsa. Le rappresentazioni possono avere dimensioni diverse, una risoluzione diversa, una filigrana aggiunta o altre caratteristiche modificate.

* **Versioni**: il controllo delle versioni crea un&#39;istantanea delle risorse digitali in un momento specifico. Puoi ripristinare le risorse nelle versioni precedenti. Vedi [controllo delle versioni in [!DNL Assets]](manage-assets.md#asset-versioning).

* **Risorse secondarie**: le risorse secondarie sono risorse che compongono una risorsa, ad esempio livelli in un file [!DNL Adobe Photoshop] o pagine in un file PDF. In [!DNL Assets], puoi gestire le risorse secondarie come faresti con le risorse.

### Utilizzare le risorse digitali {#how-to-work-with-assets}

Esegui un’azione su una risorsa o su una raccolta. Le azioni possono creare o modificare risorse, raccolte e rappresentazioni. Molte delle azioni di base eseguite sulle risorse (caricamento, eliminazione, aggiornamento, salvataggio di risorse secondarie) attivano flussi di lavoro preconfigurati. Queste sono attivate automaticamente in [!DNL Assets] e sono descritte in dettaglio in [!DNL Assets] gestori di supporti.

Le attività che puoi eseguire con questi flussi di lavoro preconfigurati:

* Salva la risorsa nell’archivio o eliminala da tale archivio.
* Estrai e salva i metadati della risorsa; i singoli elementi di metadati vengono salvati come XMP.
* Genera rappresentazioni e miniature per la risorsa, compresi il ridimensionamento e il ritaglio automatici, se necessario.
* Se necessario, trascodifica la risorsa. Ad esempio, i video per l’utilizzo per dispositivi mobili e web vengono transcodificati con 24 fotogrammi al secondo, mentre i video da scaricare con 30 fotogrammi al secondo. L&#39;audio per l&#39;uso mobile e web viene transcodificato con 128 Kbps, l&#39;audio per il download con 192 Kbps.

Puoi anche applicare manualmente i flussi di lavoro. Per un elenco dei flussi di lavoro predefiniti, consulta [Assets Media Handlers](media-handlers.md).

## [!DNL Experience Manager Assets] e [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Per informazioni sulle differenze, vedere [Assets and Media Library](medialibrary.md).

>[!MORELIKETHIS]
>
>* [Video introduttivo - Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Comprendere i concetti relativi ai metadati](/help/assets/metadata-concepts.md)
