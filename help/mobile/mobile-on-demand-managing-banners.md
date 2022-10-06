---
title: Gestione dei banner
seo-title: Managing Banners
description: I banner rappresentano in genere collegamenti promozionali grafici. Segui questa pagina per ulteriori informazioni.
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Gestione dei banner{#managing-banners}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire contenuti all’interno di un’applicazione. Le azioni seguenti vengono eseguite sul contenuto all’interno dell’applicazione.

## Panoramica dei banner {#banners-overview}

I banner rappresentano in genere collegamenti promozionali grafici.

>[!NOTE]
>
>Consulta le seguenti risorse nella Guida in linea per scoprire i seguenti argomenti nelle app AEM Mobile:
>
>* [Considerazioni sulla progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Creazione di banner](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>


## Creazione di un banner {#creating-a-banner}

Il flusso di lavoro generale per creare un articolo è il seguente:

1. Seleziona **Mobile** dalla barra laterale.
1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Fai clic sulla freccia giù nell’angolo in alto a destra del **Gestire i banner** piastrelle.
1. Segui ogni passaggio della procedura guidata per continuare a creare il nuovo banner.
1. Quando è pronto, fai clic su **Crea**.
1. Il nuovo banner viene visualizzato nel **Gestire i banner** piastrelle.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importazione di un nuovo banner {#importing-a-new-banner}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Consente la modifica e la visualizzazione dei contenuti locali.

>[!NOTE]
>
>L’importazione non include immagini.

Flusso di lavoro per importare un nuovo articolo

1. Da Mobile, scegli l’app mobile on-demand dal catalogo.
1. Fai clic sulla freccia giù nell’angolo in alto a destra del **Gestire i banner** e selezionare Importa banner.
1. Fai clic su **Banner di importazione** nella finestra di dialogo, quindi Chiudi.
1. Gli articoli on-demand per dispositivi mobili vengono ora visualizzati nella sezione **Gestire i banner** piastrelle.

>[!CAUTION]
>
>È innanzitutto necessario associare una connessione Mobile On-Demand.

## Modifica di un banner {#editing-a-banner}

Utilizza l’editor integrato AEM trascinamento per aggiungere o modificare un articolo. È possibile aggiungere o rimuovere componenti quali testo e immagini. È possibile inserire immagini da DAM Assets.

>[!CAUTION]
>
>Solo i banner creati in AEM possono essere aperti nell’editor.

Flusso di lavoro per modificare un articolo:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Seleziona un banner sorgente AEM dal riquadro** Manage Banner**.
1. Fai clic sul banner evidenziato nella vista a elenco per aprirlo nell’editor dei contenuti.
1. Utilizza l’editor dei contenuti per trascinare il contenuto del banner (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all’interno di un banner {#viewing-and-editing-the-metadata-within-a-banner}

I banner hanno numerose proprietà come titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Flusso di lavoro generale per visualizzare/modificare un articolo:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Scegli un banner dal **Gestire i banner** piastrelle.

1. Seleziona **Proprietà** dalla barra delle azioni.
1. Visualizza tutti i metadati disponibili per l&#39;articolo.
1. Modifica i metadati, se desiderato, e fai clic su **Salva** al termine.
1. Facoltativamente, carica immediatamente le modifiche su Mobile On-Demand.

## Caricamento di un banner {#uploading-a-banner}

L’azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand già esistente viene sostituito dalla nuova versione.

Flusso di lavoro generale per caricare un banner:

1. Da **Mobile**, scegli l’app Mobile On-Demand dal catalogo.
1. In **Gestire i banner** seleziona un banner da caricare su Mobile On-Demand.
1. Aggiungi altri banner se necessario dalla vista a elenco.
1. Seleziona **Carica** dalla barra delle azioni, fai clic su Carica nella finestra di dialogo.
1. I banner sono ora caricati su Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Eliminazione di un banner {#deleting-a-banner}

Questa operazione elimina il banner selezionato da Mobile On-Demand ed eventualmente dall’istanza AEM locale.

Flusso di lavoro generale per eliminare un banner:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Seleziona il banner da eliminare nella **Gestire i banner** piastrelle.
1. Accertati che sia selezionato nell’elenco (seleziona altri da eliminare in base alle esigenze).
1. Fai clic su **Elimina** dalla barra delle azioni.
1. Controlla se desideri eliminare da AEM e da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. Il banner viene ora rimosso dall’elenco.

### Passaggi successivi {#the-next-steps}

Una volta appresa la gestione dei banner, vedi

* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
