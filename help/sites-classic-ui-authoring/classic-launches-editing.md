---
title: Modifica dei lanci
description: Quando è stato creato un lancio per una pagina (o un insieme di pagine) è possibile modificare il contenuto nella copia di lancio delle pagine.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 3%

---

# Modifica dei lanci{#editing-launches}

## Modifica delle pagine di lancio {#editing-launch-pages}

Quando è stato creato un lancio per una pagina (o un insieme di pagine) è possibile modificare il contenuto nella copia di lancio delle pagine.

1. Apri la pagina per la modifica.
1. Nella barra laterale, selezionate la **Controllo delle versioni** , quindi espandi la **Lanci** gruppo. Il titolo del lancio attualmente in corso di modifica utilizza un font in grassetto.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Seleziona il lancio su cui desideri lavorare, quindi fai clic su **Interruttore**.
1. Inizia a modificare.

   >[!NOTE]
   >
   >È possibile utilizzare **Pagina** scheda della barra laterale per eseguire azioni quali **Crea pagina figlia**, tra gli altri.

## Modifica di una configurazione di lancio {#editing-a-launch-configuration}

Dopo aver creato un lancio, puoi modificare il nome del lancio e la data del lancio. Puoi anche specificare un’immagine da associare al lancio.

1. Apri la pagina di amministrazione dei lanci ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Seleziona il lancio richiesto e fai clic su **Modifica** per aprire la finestra di dialogo:

   * In **Generale** è possibile modificare:

      * **Titolo**
      * **Data live**: equivale alla data del lancio
      * **Produzione pronta**

      Vedi [Lanci - Ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events) per informazioni sullo scopo e l&#39;interazione di questi campi.

   * In **Immagine** è possibile caricare un file di immagine.


1. Fai clic su **Salva**.

## Esplorazione dello stato di lancio di una pagina {#discovering-the-launch-status-of-a-page}

Quando modifichi un lancio di una pagina, le informazioni sul lancio vengono visualizzate nella parte inferiore della sezione **Controllo delle versioni** scheda della barra laterale:

* Nome del lancio.
* L&#39;ora dall&#39;ultima modifica.
* Utente che ha eseguito l’ultima modifica.
* Lo stato del **Produzione pronta** flag (arancione=non impostato; green=set).

![chlimage_1-186](assets/chlimage_1-186.png)
