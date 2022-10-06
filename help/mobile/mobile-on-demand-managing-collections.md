---
title: Gestione delle raccolte
seo-title: Managing Collections
description: Le raccolte rappresentano un secchio ben definito con contenuti quali articoli o banner adatti al tema della copertina. Segui questa pagina per ulteriori informazioni.
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---

# Gestione delle raccolte{#managing-collections}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire contenuti all’interno di un’applicazione. Le azioni seguenti vengono eseguite sul contenuto all’interno dell’applicazione.

## Panoramica delle raccolte {#collections-overview}

Le raccolte rappresentano un *secchio* ripieni di contenuti come articoli o banner che si adattano al tema della copertina.

>[!NOTE]
>
>Consulta le seguenti risorse nella Guida in linea per scoprire i seguenti argomenti nelle app AEM Mobile:
>
>* [Considerazioni sulla progettazione](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Gestione delle raccolte](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>


## Creazione di una raccolta {#creating-a-collection}

Il flusso di lavoro generale per creare una raccolta è il seguente:

1. Seleziona **Mobile** dalla barra laterale.
1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Fai clic sulla freccia giù nell’angolo in alto a destra del **Gestire le raccolte** piastrelle.
1. Segui ogni passaggio della procedura guidata per continuare a creare il nuovo articolo.
1. Quando è pronto, fai clic su **Crea**.
1. Il nuovo articolo viene visualizzato nella sezione **Gestire le raccolte** piastrelle.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importazione di una nuova raccolta {#importing-a-new-collection}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Consente la modifica e la visualizzazione dei contenuti locali.

>[!NOTE]
>
>L’importazione non include immagini.

Flusso di lavoro per importare una nuova raccolta

1. Da Mobile, scegli l’app mobile on-demand dal catalogo.
1. Fai clic sulla freccia giù nell’angolo in alto a destra del **Gestire le raccolte** e selezionare Importa raccolte.
1. Fai clic su **Importare raccolte** nella finestra di dialogo, quindi Chiudi.
1. Le raccolte Mobile On-Demand vengono ora visualizzate nella sezione **Gestire le raccolte** piastrelle.

>[!CAUTION]
>
>È innanzitutto necessario associare una connessione Mobile On-Demand.

## Modifica di una raccolta {#editing-a-collection}

Utilizza l’editor integrato AEM trascinamento per aggiungere o modificare un articolo. È possibile aggiungere o rimuovere componenti quali testo e immagini. È possibile inserire immagini da DAM Assets.

Flusso di lavoro per modificare una raccolta:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Seleziona un articolo di origine AEM dal **Gestire le raccolte** piastrelle.
1. Fai clic sulla raccolta evidenziata dalla vista a elenco per aprirla nell’editor dei contenuti.
1. Utilizza l’editor dei contenuti per trascinare il contenuto della raccolta (manoscritti, immagini, testo, ecc.).

### Visualizzazione e modifica dei metadati all’interno di una raccolta {#viewing-and-editing-the-metadata-within-a-collection}

Le raccolte hanno numerose proprietà come titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Flusso di lavoro generale per visualizzare/modificare una raccolta:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Scegli una raccolta dal **Gestire le raccolte** piastrelle.

1. Seleziona **Proprietà** dalla barra delle azioni.
1. Visualizza tutti i metadati disponibili per l&#39;articolo.
1. Modifica i metadati, se desiderato, e fai clic su **Salva** al termine.
1. Facoltativamente, carica immediatamente le modifiche su Mobile On-Demand.

## Caricamento di una raccolta {#uploading-a-collection}

L’azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand già esistente viene sostituito dalla nuova versione.

Flusso di lavoro generale per caricare una raccolta:

1. Da **Mobile**, scegli l’app Mobile On-Demand dal catalogo.
1. In **Gestire le raccolte** seleziona un articolo da caricare su Mobile On-Demand.
1. Aggiungi altre raccolte se necessario dalla vista a elenco.
1. Seleziona **Carica** dalla barra delle azioni, fai clic su Carica nella finestra di dialogo.
1. Le raccolte sono ora caricate su Mobile On-Demand.

## Eliminazione di una raccolta {#deleting-a-collection}

Questa operazione elimina la raccolta selezionata da Mobile On-Demand ed eventualmente dall&#39;istanza AEM locale.

Flusso di lavoro generale per eliminare una raccolta:

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Seleziona l’articolo da eliminare nella **Gestire le raccolte** piastrelle.
1. Accertati che sia selezionato nell’elenco (seleziona altri da eliminare in base alle esigenze).
1. Fai clic su **Elimina** dalla barra delle azioni.
1. Controlla se desideri eliminare da AEM e da Mobile On-Demand.
1. Fai clic su **Elimina**.
1. La raccolta viene ora rimossa dall’elenco.

## Aggiunta di contenuto alle raccolte {#adding-content-to-collections}

Le raccolte sono essenzialmente una categoria di contenuto correlato. Raccolgono contenuti quali articoli, banner insieme in pacchetti che definiscono la struttura di navigazione dell’applicazione. Le raccolte possono essere nidificate.

>[!NOTE]
>
>Il contenuto deve essere caricato su Mobile On-Demand prima di poter essere aggiunto a una raccolta.

Le raccolte sono essenzialmente una categoria di contenuti correlati: Raccolgono contenuti quali articoli, banner insieme in pacchetti che definiscono la struttura di navigazione dell’applicazione. Le raccolte possono essere nidificate.

1. Da Mobile, scegli l’app Mobile On-Demand dal catalogo.
1. Seleziona un articolo caricato in precedenza (o banner/raccolta)
1. Scegli Aggiungi a dalla barra delle azioni.
1. Seleziona una raccolta caricata in precedenza dalla finestra di dialogo.
1. Fai clic su **Aggiorna** per aggiungere contenuto alla raccolta.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Passaggi successivi {#the-next-steps}

Per informazioni sulla gestione delle raccolte, consulta

* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
