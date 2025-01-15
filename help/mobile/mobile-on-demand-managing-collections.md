---
title: Gestione delle raccolte
description: Le raccolte rappresentano un bucket ben definito pieno di contenuti quali articoli o banner adatti al tema della copertina. Per ulteriori informazioni, segui questa pagina.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Gestione delle raccolte{#managing-collections}

{{ue-over-mobile}}

Le azioni di gestione dei contenuti sono gli elementi costitutivi che consentono di creare e gestire i contenuti all’interno di un’applicazione. Le azioni seguenti vengono eseguite sul contenuto all’interno dell’applicazione.

## Panoramica raccolte {#collections-overview}

Le raccolte rappresentano un *bucket* ben definito e pieno di contenuti quali articoli o banner adatti al tema della copertina.

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
1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Fai clic sulla freccia in giù nell&#39;angolo in alto a destra del riquadro **Gestisci raccolte**.
1. Segui i passaggi della procedura guidata per continuare a creare il nuovo articolo.
1. Al termine, fare clic su **Crea**.
1. Il nuovo articolo verrà visualizzato nel riquadro **Gestisci raccolte**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importazione di una nuova raccolta {#importing-a-new-collection}

Il contenuto Mobile On-Demand esistente può essere scaricato (importato) da Mobile On-Demand a AEM. Ciò consente di modificare e visualizzare contenuti locali.

>[!NOTE]
>
>L&#39;importazione non include immagini.

Flusso di lavoro per importare una nuova raccolta

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Fare clic sulla freccia rivolta verso il basso nell&#39;angolo superiore destro del riquadro **Gestisci raccolte** e selezionare Importa raccolte.
1. Fai clic su **Importa raccolte** nella finestra di dialogo, quindi su Chiudi.
1. Le raccolte Mobile On-Demand vengono ora visualizzate nel riquadro **Gestisci raccolte**.

>[!CAUTION]
>
>Associate prima una connessione Mobile On-Demand.

## Modifica di una raccolta {#editing-a-collection}

Utilizza l’editor integrato di trascinamento AEM per aggiungere o modificare un articolo. È possibile aggiungere/rimuovere componenti quali testo e immagini. È possibile inserire immagini da DAM Assets.

Flusso di lavoro per modificare una raccolta:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Seleziona un articolo originato da AEM dal riquadro **Gestisci raccolte**.
1. Fai clic sulla raccolta evidenziata dalla vista a elenco per aprirla nell’editor di contenuti.
1. Utilizza l’editor di contenuti per trascinare il contenuto della raccolta (manoscritti, immagini, testo e così via).

### Visualizzazione e modifica dei metadati all’interno di una raccolta {#viewing-and-editing-the-metadata-within-a-collection}

Le raccolte hanno numerose proprietà come titoli, descrizioni, immagini. Questa azione viene utilizzata per visualizzare e modificare tali proprietà. Facoltativamente, queste modifiche possono essere caricate su Mobile On-Demand al momento del salvataggio.

Il flusso di lavoro generale per visualizzare/modificare una raccolta:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Scegli una raccolta dal riquadro **Gestisci raccolte**.

1. Seleziona **Proprietà** dalla barra delle azioni.
1. Visualizza tutti i metadati disponibili per tale articolo.
1. Modificare i metadati, se necessario, e al termine fare clic su **Salva**.
1. Se necessario, carica le modifiche immediatamente in Mobile On-Demand.

## Caricamento di una raccolta {#uploading-a-collection}

L’azione di caricamento copia il contenuto selezionato e lo aggiunge a un progetto Mobile On-Demand. Il contenuto Mobile On-Demand esistente viene sostituito dalla nuova versione.

Il flusso di lavoro generale per caricare una raccolta:

1. Da **Mobile**, scegli la tua app Mobile On-Demand dal catalogo.
1. Nel riquadro **Gestisci raccolte**, seleziona un articolo da caricare su Mobile On-Demand.
1. Se necessario, aggiungi altre raccolte dalla vista a elenco.
1. Seleziona **Carica** dalla barra delle azioni, quindi fai clic su Carica nella finestra di dialogo.
1. Le raccolte sono ora caricate su Mobile On-Demand.

## Eliminazione di una raccolta {#deleting-a-collection}

Questa operazione elimina la raccolta selezionata da Mobile On-Demand e, facoltativamente, dall’istanza AEM locale.

Flusso di lavoro generale per eliminare una raccolta:

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Selezionare l&#39;articolo da eliminare nel riquadro **Gestisci raccolte**.
1. Assicurati che sia selezionato nell’elenco; seleziona gli altri da eliminare in base alle esigenze.
1. Fai clic su **Elimina** nella barra delle azioni.
1. Seleziona questa opzione se desideri eliminarla da AEM e Mobile On-Demand.
1. Fai clic su **Elimina**.
1. La tua raccolta è stata rimossa dall&#39;elenco.

## Aggiunta di contenuto alle raccolte {#adding-content-to-collections}

Le raccolte sono essenzialmente una categoria di contenuti correlati. Raccolgono contenuti come articoli, banner in pacchetti che definiscono la struttura di navigazione dell’applicazione. Le raccolte possono essere nidificate.

>[!NOTE]
>
>Il contenuto deve essere caricato su Mobile On-Demand prima di poter essere aggiunto a una raccolta.

Le raccolte sono essenzialmente una categoria di contenuti correlati: raccolgono contenuti come articoli, banner e pacchetti che definiscono la struttura di navigazione dell’applicazione. Le raccolte possono essere nidificate.

1. In Mobile, scegli la tua app Mobile On-Demand dal catalogo.
1. Seleziona un articolo (o banner/raccolta) caricato in precedenza
1. Dalla barra delle azioni, seleziona Aggiungi a.
1. Seleziona una raccolta caricata in precedenza dalla finestra di dialogo.
1. Fai clic su **Aggiorna** per aggiungere contenuto alla raccolta.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Passaggi successivi {#the-next-steps}

Dopo aver appreso come gestire le raccolte, consulta

* [Gestione dei banner](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestione degli articoli](/help/mobile/mobile-on-demand-managing-articles.md)
* [Caricamento delle risorse condivise](/help/mobile/mobile-on-demand-shared-resources.md)
* [Pubblicazione/annullamento della pubblicazione del contenuto](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
