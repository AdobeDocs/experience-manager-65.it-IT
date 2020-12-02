---
title: Gestione delle raccolte
seo-title: Gestione delle raccolte
description: Le raccolte rappresentano un bucket ben definito con contenuto, ad esempio articoli o banner, adatto al tema della copertina. Segui questa pagina per saperne di più.
seo-description: Le raccolte rappresentano un bucket ben definito con contenuto, ad esempio articoli o banner, adatto al tema della copertina. Segui questa pagina per saperne di più.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Gestione delle raccolte{#managing-collections}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire il contenuto all&#39;interno di un&#39;applicazione. Le azioni seguenti vengono eseguite sul contenuto all&#39;interno dell&#39;applicazione.

## Panoramica delle raccolte {#collections-overview}

Le raccolte rappresentano un *bucket* ben definito, riempito con contenuti quali articoli o banner che si adattano al tema della copertina.

>[!NOTE]
>
>Consultate le seguenti risorse nella Guida in linea per informazioni sui seguenti argomenti nelle  app AEM Mobile:
>
>* [Considerazioni sulla progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gestione delle raccolte](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)

>



## Creazione di una raccolta {#creating-a-collection}

Il flusso di lavoro generale per creare una raccolta è il seguente:

1. Selezionare **Mobile** dalla barra laterale.
1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci raccolte**.
1. Per continuare a creare il nuovo articolo, eseguite i vari passaggi della procedura guidata.
1. Quando è pronto, fare clic su **Crea**.
1. Il nuovo articolo viene visualizzato nella sezione **Gestisci raccolte**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importazione di una nuova raccolta {#importing-a-new-collection}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Questo consente la modifica e la visualizzazione locale dei contenuti.

>[!NOTE]
>
>L&#39;importazione non include immagini.

Flusso di lavoro per l&#39;importazione di una nuova raccolta

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Fate clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro della sezione **Gestisci raccolte** e selezionate Importa raccolte.
1. Fare clic su **Importa raccolte** nella finestra di dialogo, quindi su Chiudi.
1. Le raccolte Mobile On-Demand ora vengono visualizzate nella sezione **Gestisci raccolte**.

>[!CAUTION]
>
>È necessario associare prima una connessione Mobile On-Demand.

## Modifica di una raccolta {#editing-a-collection}

Utilizzate l&#39;editor incorporato AEM trascinamento per aggiungere o modificare un articolo. È possibile aggiungere o rimuovere componenti come testo e immagini. È possibile inserire immagini da Risorse DAM.

Flusso di lavoro per la modifica di una raccolta:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate un articolo di origine AEM dalla sezione **Gestisci raccolte**.
1. Fate clic sulla raccolta evidenziata dalla vista a elenco per aprirla nell&#39;editor del contenuto.
1. Usate l&#39;editor dei contenuti per trascinare il contenuto della raccolta (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all&#39;interno di una raccolta {#viewing-and-editing-the-metadata-within-a-collection}

Le raccolte presentano numerose proprietà quali titoli, descrizioni e immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Flusso di lavoro generale per visualizzare/modificare una raccolta:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Scegliete una raccolta dalla sezione **Gestisci raccolte**.

1. Selezionare **Properties** dalla barra delle azioni.
1. Visualizzate tutti i metadati disponibili per l&#39;articolo.
1. Modificate i metadati, se necessario, e fate clic su **Salva** al termine.
1. Facoltativamente, caricate immediatamente le modifiche su Mobile On-Demand.

## Caricamento di una raccolta {#uploading-a-collection}

L&#39;azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand già esistente viene sostituito dalla nuova versione.

Flusso di lavoro generale per caricare una raccolta:

1. Da **Mobile**, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Nella sezione **Gestisci raccolte**, selezionate un articolo da caricare su Mobile On-Demand.
1. Se necessario, aggiungete altre raccolte dalla vista a elenco.
1. Selezionate **Carica** dalla barra delle azioni, quindi fate clic su Carica nella finestra di dialogo.
1. Le raccolte ora vengono caricate su Mobile On-Demand.

## Eliminazione di una raccolta {#deleting-a-collection}

Questa operazione elimina la raccolta selezionata da Mobile On-Demand ed eventualmente dall&#39;istanza AEM locale.

Flusso di lavoro generale per eliminare una raccolta:

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate l&#39;articolo da eliminare nella sezione **Gestisci raccolte**.
1. Assicurarsi che sia selezionato nell&#39;elenco (selezionare altri da eliminare in base alle esigenze).
1. Fare clic su **Elimina** dalla barra delle azioni.
1. Verificate se desiderate eliminare sia da AEM che da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. La raccolta viene ora rimossa dall&#39;elenco.

## Aggiunta di contenuto alle raccolte {#adding-content-to-collections}

Le raccolte sono essenzialmente una categoria di contenuto correlato. Raccolgono contenuti come articoli, banner insieme in pacchetti che definiscono la struttura di navigazione dell&#39;applicazione. Le raccolte possono essere nidificate.

>[!NOTE]
>
>Il contenuto deve essere caricato su Mobile On-Demand prima di poter essere aggiunto a una raccolta.

Le raccolte sono essenzialmente una categoria di contenuto correlato: Raccolgono contenuti come articoli, banner insieme in pacchetti che definiscono la struttura di navigazione dell&#39;applicazione. Le raccolte possono essere nidificate.

1. Da Mobile, scegliete l&#39;app Mobile On-Demand dal catalogo.
1. Selezionate un articolo precedentemente caricato (o banner/raccolta)
1. Scegliete Aggiungi a dalla barra delle azioni.
1. Selezionate una raccolta caricata in precedenza dalla finestra di dialogo.
1. Fate clic su **Aggiorna** per aggiungere contenuto alla raccolta.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Passaggi successivi {#the-next-steps}

Una volta appresa la gestione delle raccolte, vedete

* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
