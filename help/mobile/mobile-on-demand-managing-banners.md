---
title: Gestione dei banner
seo-title: Managing Banners
description: I banner rappresentano in genere collegamenti promozionali grafici. Per ulteriori informazioni, segui questa pagina.
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# Gestione dei banner{#managing-banners}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire i contenuti all’interno di un’applicazione. Le azioni seguenti vengono eseguite sul contenuto all’interno dell’applicazione.

## Panoramica banner {#banners-overview}

I banner rappresentano in genere collegamenti promozionali grafici.

>[!NOTE]
>
>Consulta le seguenti risorse nella Guida in linea per scoprire i seguenti argomenti nelle app AEM Mobile:
>
>* [Considerazioni di progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Creazione di banner](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## Creazione di un banner {#creating-a-banner}

Il flusso di lavoro generale per la creazione di un articolo è il seguente:

1. Seleziona **Dispositivi mobili** dalla barra laterale.
1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Fare clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della **Gestisci banner** affiancare.
1. Segui i passaggi della procedura guidata per continuare a creare il nuovo banner.
1. Quando è pronto, fai clic su **Crea**.
1. Il nuovo banner verrà visualizzato nel **Gestisci banner** affiancare.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importazione di un nuovo banner {#importing-a-new-banner}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Ciò consente di modificare e visualizzare contenuti locali.

>[!NOTE]
>
>L&#39;importazione non include immagini.

Flusso di lavoro per importare un nuovo articolo

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Fare clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della **Gestisci banner** affiancare e selezionare Importa banner.
1. Clic **Importa banner** nella finestra di dialogo, quindi Chiudi.
1. Gli articoli Mobile On-Demand vengono ora visualizzati nel **Gestisci banner** affiancare.

>[!CAUTION]
>
>È innanzitutto necessario associare una connessione Mobile On-Demand.

## Modifica di un banner {#editing-a-banner}

Utilizza l’editor integrato di trascinamento AEM per aggiungere o modificare un articolo. È possibile aggiungere/rimuovere componenti quali testo e immagini. È possibile inserire immagini da Risorse DAM.

>[!CAUTION]
>
>Solo i banner creati nell&#39;AEM possono essere aperti nell&#39;editor.

Flusso di lavoro per modificare un articolo:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Seleziona un banner di origine AEM dal riquadro** Gestisci banner**.
1. Fai clic sul banner evidenziato nella vista a elenco per aprirlo nell’editor di contenuti.
1. Utilizza l’editor di contenuti per trascinare il contenuto del banner (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all’interno di un banner {#viewing-and-editing-the-metadata-within-a-banner}

I banner hanno numerose proprietà come titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Il flusso di lavoro generale per visualizzare/modificare un articolo:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Scegli un banner da **Gestisci banner** affiancare.

1. Seleziona **Proprietà** dalla barra delle azioni.
1. Visualizza tutti i metadati disponibili per tale articolo.
1. Se necessario, modifica i metadati e fai clic su **Salva** al termine.
1. Se necessario, carica le modifiche immediatamente in Mobile On-Demand.

## Caricamento di un banner {#uploading-a-banner}

L’azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand esistente viene sostituito dalla nuova versione.

Il flusso di lavoro generale per caricare un banner:

1. Da **Dispositivi mobili**, scegli la tua app Mobile On-Demand dal catalogo.
1. In **Gestisci banner** , seleziona un banner da caricare su Mobile On-Demand.
1. Se necessario, aggiungi altri banner dalla vista a elenco.
1. Seleziona **Carica** dalla barra delle azioni, fai clic su Carica nella finestra di dialogo.
1. I banner ora sono caricati su Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Eliminazione di un banner {#deleting-a-banner}

Questa operazione elimina il banner selezionato da Mobile On-Demand e, facoltativamente, dall’istanza AEM locale.

Flusso di lavoro generale per eliminare un banner:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Selezionare il banner da eliminare nel **Gestisci banner** affiancare.
1. Assicurati che sia selezionato nell’elenco (seleziona gli altri da eliminare in base alle esigenze).
1. Clic **Elimina** dalla barra delle azioni.
1. Seleziona se desideri eliminare dall’AEM e da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. Il banner è stato rimosso dall&#39;elenco.

### Passaggi successivi {#the-next-steps}

Per informazioni sulla gestione dei banner, consulta

* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
