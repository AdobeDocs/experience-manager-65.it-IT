---
title: Gestione dei banner
seo-title: Gestione dei banner
description: I banner rappresentano collegamenti promozionali tipicamente grafici. Segui questa pagina per saperne di più.
seo-description: I banner rappresentano collegamenti promozionali tipicamente grafici. Segui questa pagina per saperne di più.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# Gestione dei banner{#managing-banners}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire il contenuto all&#39;interno di un&#39;applicazione. Le azioni seguenti vengono eseguite sul contenuto all&#39;interno dell&#39;applicazione.

## Panoramica sui banner {#banners-overview}

I banner rappresentano collegamenti promozionali tipicamente grafici.

>[!NOTE]
>
>Consultate le seguenti risorse nella Guida in linea per informazioni sui seguenti argomenti nelle  app AEM Mobile:
>
>* [Considerazioni sulla progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Creazione di banner](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)

>



## Creazione di un banner {#creating-a-banner}

Il flusso di lavoro generale per la creazione di un articolo è il seguente:

1. Selezionare **Mobile** dalla barra laterale.
1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci banner**.
1. Per continuare a creare il nuovo banner, eseguite i vari passaggi della procedura guidata.
1. Quando è pronto, fare clic su **Crea**.
1. Il nuovo banner viene visualizzato nella sezione **Gestisci banner**.

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importazione di un nuovo banner {#importing-a-new-banner}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Questo consente la modifica e la visualizzazione locale dei contenuti.

>[!NOTE]
>
>L&#39;importazione non include immagini.

Flusso di lavoro per importare un nuovo articolo

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci banner** e selezionate Importa banner.
1. Fate clic su **Importa banner** nella finestra di dialogo, quindi su Chiudi.
1. Gli articoli Mobile On-Demand ora vengono visualizzati nella sezione **Gestisci banner**.

>[!CAUTION]
>
>È necessario associare prima una connessione Mobile On-Demand.

## Modifica di un banner {#editing-a-banner}

Utilizzate l&#39;editor incorporato AEM trascinamento per aggiungere o modificare un articolo. È possibile aggiungere o rimuovere componenti come testo e immagini. È possibile inserire immagini da Risorse DAM.

>[!CAUTION]
>
>Solo i banner creati in AEM possono essere aperti nell’editor.

Flusso di lavoro per modificare un articolo:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate un banner di origine AEM dalla sezione** Gestisci banner*.
1. Fate clic sul banner evidenziato dalla vista a elenco per aprirlo nell’editor del contenuto.
1. Usate l’editor dei contenuti per trascinare il contenuto del banner (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all&#39;interno di un banner {#viewing-and-editing-the-metadata-within-a-banner}

I banner hanno numerose proprietà quali titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Flusso di lavoro generale per visualizzare/modificare un articolo:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Scegliete un banner dalla sezione **Gestisci banner**.

1. Selezionare **Properties** dalla barra delle azioni.
1. Visualizzate tutti i metadati disponibili per l&#39;articolo.
1. Modificate i metadati, se necessario, e fate clic su **Salva** al termine.
1. Facoltativamente, caricate immediatamente le modifiche su Mobile On-Demand.

## Caricamento di un banner {#uploading-a-banner}

L&#39;azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand già esistente viene sostituito dalla nuova versione.

Flusso di lavoro generale per caricare un banner:

1. Da **Mobile**, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Nella sezione **Gestisci banner**, selezionate un banner da caricare su Mobile On-Demand.
1. Aggiungete altri banner se necessario dalla vista Elenco.
1. Selezionate **Carica** dalla barra delle azioni, quindi fate clic su Carica nella finestra di dialogo.
1. I banner ora vengono caricati su Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Eliminazione di un banner {#deleting-a-banner}

Questa operazione elimina il banner selezionato da Mobile On-Demand ed eventualmente dall&#39;istanza AEM locale.

Flusso di lavoro generale per eliminare un banner:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate il banner da eliminare nella sezione **Gestisci banner**.
1. Assicurarsi che sia selezionato nell&#39;elenco (selezionare altri da eliminare in base alle esigenze).
1. Fare clic su **Elimina** dalla barra delle azioni.
1. Verificate se desiderate eliminare sia da AEM che da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. Il banner ora viene rimosso dall&#39;elenco.

### Passaggi successivi {#the-next-steps}

Per informazioni sulla gestione dei banner, vedete

* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
