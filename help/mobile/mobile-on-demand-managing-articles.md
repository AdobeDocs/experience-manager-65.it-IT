---
title: Gestione degli articoli
seo-title: Gestione degli articoli
description: Seguite questa pagina per informazioni sulla creazione e la gestione degli articoli.
seo-description: Seguite questa pagina per informazioni sulla creazione e la gestione degli articoli.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---


# Gestione degli articoli{#managing-articles}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire gli articoli all&#39;interno di un&#39;applicazione. Le azioni seguenti vengono eseguite sugli articoli all&#39;interno dell&#39;applicazione.

## Panoramica degli articoli {#articles-overview}

Gli articoli rappresentano il testo basato sulla grafica per trasmettere le informazioni.

>[!NOTE]
>
>Consultate le seguenti risorse nella Guida in linea per informazioni sui seguenti argomenti nelle  app AEM Mobile:
>
>* [Considerazioni sulla progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gestione degli articoli](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)

>



## Creazione di un articolo {#creating-an-article}

Il flusso di lavoro generale per la creazione di un articolo è il seguente:

1. Selezionare **Mobile** dalla barra laterale.
1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci articoli**.
1. Scegliete un modello di articolo e fate clic su **Avanti**.
1. Per continuare a creare il nuovo articolo, eseguite i vari passaggi della procedura guidata.
1. Quando è pronto, fare clic su **Crea**.
1. Il nuovo articolo viene visualizzato nella sezione **Gestisci articoli**.

## Importazione di un nuovo articolo {#importing-a-new-article}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Questo consente la modifica e la visualizzazione locale dei contenuti.

>[!NOTE]
>
>L&#39;importazione non include immagini.

Flusso di lavoro per importare un nuovo articolo

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci articoli** e selezionate Importa articoli.
1. Fare clic su **Importa articoli** nella finestra di dialogo, quindi su Chiudi.
1. Gli articoli Mobile On-Demand ora vengono visualizzati nella sezione **Gestisci articoli**.

>[!CAUTION]
>
>È necessario associare prima una connessione Mobile On-Demand.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Modifica di un articolo {#editing-an-article}

Utilizzate l&#39;editor incorporato AEM trascinamento per aggiungere o modificare un articolo. È possibile aggiungere o rimuovere componenti come testo e immagini. È possibile inserire immagini da Risorse DAM.

>[!CAUTION]
>
>Solo gli articoli creati in AEM possono essere aperti nell&#39;editor.

Flusso di lavoro per modificare un articolo:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate un articolo di origine AEM dalla sezione **Gestisci articoli**.
1. Fate clic sull&#39;articolo evidenziato dalla vista a elenco per aprirlo nell&#39;editor del contenuto.
1. Usate l’editor di contenuti per trascinare il contenuto dell’articolo (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all&#39;interno di un articolo {#viewing-and-editing-the-metadata-within-an-article}

I contenuti come articoli, banner, ecc. hanno numerose proprietà come titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Flusso di lavoro generale per visualizzare/modificare un articolo:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Scegliete un articolo dalla sezione **Gestisci articoli**.

1. Selezionare **Visualizza proprietà** dalla barra delle azioni.
1. Visualizzate tutti i metadati disponibili per l&#39;articolo.
1. Modificate i metadati, se necessario, e fate clic su **Salva** al termine.
1. Facoltativamente, caricate immediatamente le modifiche su Mobile On-Demand.

## Caricamento di un articolo {#uploading-an-article}

L&#39;azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand già esistente viene sostituito dalla nuova versione.

Flusso di lavoro generale per caricare un articolo:

1. Da **Mobile**, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Nella sezione **Gestisci articoli**, selezionate un articolo da caricare su Mobile On-Demand.
1. Se necessario, aggiungete altri articoli dalla vista Elenco.
1. Selezionate **Carica** dalla barra delle azioni, quindi fate clic su Carica nella finestra di dialogo.
1. Gli articoli vengono ora caricati su Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Eliminazione di un articolo {#deleting-an-article}

Questa operazione elimina il contenuto selezionato da Mobile On-Demand ed eventualmente dall&#39;istanza AEM locale.

Flusso di lavoro generale per eliminare un articolo:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionare l&#39;articolo da eliminare nella sezione **Gestisci articoli**.
1. Assicurarsi che sia selezionato nell&#39;elenco (selezionare altri da eliminare in base alle esigenze).
1. Fare clic su **Elimina** dalla barra delle azioni.
1. Verificate se desiderate eliminare sia da AEM che da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. L&#39;articolo ora viene rimosso dall&#39;elenco.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Passaggi successivi {#the-next-steps}

Per informazioni sulla gestione degli articoli, consultate

* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione delle raccolte](/help/mobile/mobile-on-demand-managing-collections.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
