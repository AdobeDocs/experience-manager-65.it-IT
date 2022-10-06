---
title: Modifica dei lanci
seo-title: Editing Launches
description: Dopo aver creato un lancio per una pagina o un insieme di pagine, è possibile modificarne il contenuto nella copia di lancio.
seo-description: When a launch has been created for a page (or set of pages) you can edit the content in the launch copy of the page(s).
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 100%

---

# Modifica dei lanci{#editing-launches}

## Modifica delle pagine di lancio {#editing-launch-pages}

Dopo aver creato un lancio per una pagina o un insieme di pagine, è possibile modificarne il contenuto nella copia di lancio.

1. Apri la pagina da modificare.
1. Nella barra laterale, seleziona la scheda **Gestione versioni** ed espandi il gruppo **Lanci**. Il titolo del lancio attualmente in fase di modifica mostra un font in grassetto.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Seleziona il lancio su cui lavorare, poi fai clic su **Cambia**.
1. Inizia a modificare.

   >[!NOTE]
   >
   >È possibile utilizzare la scheda **Pagina** della barra laterale per eseguire azioni quali, tra le altre, **Crea pagina figlia**.

## Modifica di una configurazione di lancio {#editing-a-launch-configuration}

Dopo aver creato un lancio è possibile modificarne il nome e la data. È inoltre possibile specificare un’immagine da associare al lancio.

1. Apri la pagina di amministrazione dei lanci ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)). 

1. Seleziona il lancio richiesto e fai clic su **Modifica** per aprire la finestra di dialogo:

   * Nella scheda **Generale**, puoi modificare:

      * **Titolo**
      * **Data attivazione**: è equivalente alla data di lancio
      * **Produzione pronta**

      Consulta [Lanci - Ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events) per informazioni sullo scopo e l&#39;interazione con questi campi.

   * Nella scheda **Immagini, è possibile caricare un file di immagine.**


1. Fai clic su **Salva**.

## Rilevamento dello stato del lancio di una pagina {#discovering-the-launch-status-of-a-page}

Quando si modifica il lancio di una pagina, le informazioni sul lancio vengono visualizzate nella parte inferiore della scheda **Gestione versioni** nella barra laterale:

* Il nome del lancio.
* Ora dell’ultima modifica.
* L&#39;utente che ha apportato l’ultima modifica.
* Lo stato del flag **Produzione pronta** (arancione = non impostato; verde = impostato).

![chlimage_1-186](assets/chlimage_1-186.png)
