---
title: Creazione e gestione delle offerte
description: Usa la console Offerte per creare offerte da utilizzare nelle esperienze Attività.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: 34293432-cfdc-466b-96bd-2c43b566a420
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 74%

---

# Creazione e gestione delle offerte{#creating-and-managing-offers}

Usa la console Offerte per creare offerte da [utilizzare in più esperienze](/help/sites-authoring/content-targeting-touch.md). La creazione di offerte nella console Offerte consente di risparmiare tempo quando più esperienze richiedono la stessa offerta:

* Crea l’offerta una volta nella libreria e utilizzala in più esperienze per le attività del tuo marchio.
* Modifica l’offerta nella libreria e la modifica influisce su tutte le esperienze che la utilizzano.

Nella console Offerte, le offerte sono organizzate per marchio. Ogni marchio contiene una libreria di offerte che possono essere utilizzate nelle diverse esperienze del marchio. Utilizza le cartelle per definire una struttura gerarchica per organizzare le offerte in ogni libreria. Una struttura logica delle cartelle consente agli autori di trovare facilmente le offerte navigando nella libreria. Gli strumenti di assegnazione tag e ricerca consentono inoltre agli autori di trovare le offerte.

## Aggiunta di un marchio utilizzando la console Offerte {#add-a-brand-using-the-offers-console}

Crea un marchio a cui sono associate le offerte. Apri un marchio nella console Offerte per accedere alla libreria delle offerte, dove puoi creare cartelle e offerte.

Quando crei un marchio utilizzando la console Offerte, questo viene visualizzato anche nella [Console Attività](/help/sites-authoring/activitylib.md) dove puoi aggiungere e amministrare attività per il marchio.

1. Nella console Navigazione, fai clic su **Personalizzazione** > **Offerte**.

   ![screen-shot_2019-03-05at124139-1](assets/screen-shot_2019-03-05at124139-1.png)

1. Clic **Crea** e poi **Crea** **Marchio**.
1. Seleziona il modello del brand e fai clic su **Successivo**.
1. Digita un titolo per il marchio in base a come desideri che appaia nelle console Offerte e Attività. Facoltativamente, digita o seleziona uno o più tag da associare al marchio.
1. Fai clic su **Crea**.

## Aggiunta di una cartella a una libreria di offerte {#add-a-folder-to-an-offer-library}

Aggiungi una cartella alla libreria di offerte di un marchio per organizzare e archiviare le offerte. Puoi creare una cartella sotto il marchio o sotto altre cartelle.

1. Nella console Offerte, apri il percorso in cui desideri creare la cartella. Ad esempio, apri il marchio per creare una cartella di livello superiore o apri un’altra cartella nella libreria.
1. Clic **Crea** > **Crea cartella o offerta**.

   ![schermata_2019-03-05at124557](assets/screen-shot_2019-03-05at124557.png)

1. Seleziona **Cartella** e fai clic su **Avanti**.
1. Digita un titolo per la cartella come desideri che appaia nella libreria dell&#39;offerta e digita o seleziona i tag.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Fai clic su **Crea**.

## Aggiungere un’offerta a una libreria di offerte {#add-an-offer-to-an-offer-library}

Aggiungi un’offerta alla libreria di offerte di un marchio in modo che possa essere aggiunta alle esperienze del marchio. Quando aggiungi un’offerta, fornisci un titolo. Puoi anche associare l’offerta a uno o più tag per migliorare la ricerca.

Dopo aver creato l’offerta, puoi aprirla per eseguire l’authoring del contenuto.

1. Nella console Offerte, apri la posizione in cui desideri creare l’offerta. Ad esempio, apri il marchio per creare un’offerta di livello superiore o apri una cartella nella libreria.
1. Clic **Crea** > **Crea cartella o offerta**.

   ![screen-shot_2019-03-05at124557-1](assets/screen-shot_2019-03-05at124557-1.png)

1. Seleziona la **Pagina offerta** e quindi fare clic su **Successivo**.
1. Digita un titolo per l’offerta e facoltativamente seleziona o digita uno o più tag da associare all’offerta, quindi fai clic su **Crea**.
1. Nella finestra di dialogo di conferma, per aprire l’offerta da modificare fai clic su **Apri pagina**.

## Modifica di un’offerta {#editing-an-offer}

Apri un’offerta e modifica il contenuto in base a come desideri che appaia nelle esperienze che la utilizzano. Quando modifichi un’offerta utilizzata in una qualsiasi esperienza, le modifiche vengono visualizzate nelle esperienze.

Puoi aprire un’offerta da una cartella in una libreria di offerte o dai risultati della ricerca. Puoi anche aprire un’offerta da un’esperienza che utilizza l’offerta.

1. Nella console Offerte, fai clic sull’icona accanto all’offerta e fai clic su **Modifica**.
1. Aggiungi componenti all’offerta e modifica normalmente il contenuto dei componenti.

## Eliminazione di un’offerta {#deleting-an-offer}

Elimina un’offerta quando non è più necessaria. Quando tenti di eliminare un’offerta utilizzata in un’esperienza, ti viene richiesto di confermare l’eliminazione. La conferma comporta l’eliminazione dell’offerta e la sua rimozione dalle esperienze.

Puoi eliminare un’offerta quando visualizzi il contenuto di una cartella in una libreria di offerte o nei risultati della ricerca.

1. Nella console Offerte, fai clic sull’icona accanto all’offerta e fai clic su **Elimina**.

   Seleziona l’offerta e fai clic su **Elimina**.

1. Nella finestra di dialogo visualizzata, fai clic su **Elimina** per confermare l’eliminazione.
1. Se l’offerta viene utilizzata in una o più esperienze, viene visualizzata una finestra di dialogo per indicare che si fa riferimento all’offerta:

   * Per eliminare l’offerta e rimuoverla dalle esperienze, fai clic su **Forza eliminazione**.
   * Per mantenere l’offerta, fai clic su **Annulla**.

## Ricerca di offerte {#searching-for-offers}

Cerca le offerte di qualsiasi marchio utilizzando parole chiave che corrispondano al titolo.

![schermata_2019-03-05at124731](assets/screen-shot_2019-03-05at124731.png)

I criteri di ricerca correnti vengono visualizzati accanto ai risultati della ricerca. Puoi anche ordinare i risultati per colonna in ordine crescente o decrescente. Puoi eseguire una ricerca in qualsiasi cartella di qualsiasi libreria di offerte. I risultati della ricerca sono gli stessi, indipendentemente dalla cartella corrente.

Per cercare le offerte:

1. Nella parte superiore della console Offerte, fai clic sull’icona della lente di ingrandimento. Per impostazione predefinita, la ricerca è limitata alle offerte.
1. Immetti la parola chiave per cercare le offerte. Seleziona un elemento dai risultati di ricerca.
