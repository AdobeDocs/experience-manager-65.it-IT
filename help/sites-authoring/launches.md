---
title: Lanci
seo-title: Lanci
description: I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro. Consentono di preparare le modifiche per una pubblicazione futura, mantenendo le pagine correnti
seo-description: I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro. Consentono di preparare le modifiche per una pubblicazione futura, mantenendo le pagine correnti
uuid: 4bbd9865-735d-4232-b69c-b64193ac5d83
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e145afd8-7391-47aa-b389-16fb303749d0
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Lanci{#launches}

I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro.

Il lancio creato consente di preparare modifiche pronte alla pubblicazione futura (mantenendo le tue pagine correnti). Dopo aver modificato e aggiornato le pagine di lancio, le promuovi di nuovo a sorgente e quindi attivi le pagine sorgente (livello superiore). Con la promozione il contenuto del lancio viene duplicato sulle pagine sorgente. La promozione può essere effettuata manualmente o automaticamente (a seconda dei campi impostati durante la creazione e la modifica del lancio).

Ad esempio, le pagine dei prodotti stagionali del tuo negozio online vengono aggiornate ogni tre mesi in modo da evidenziare i prodotti per la stagione corrente. Per preparare il prossimo aggiornamento trimestrale, puoi creare un lancio delle pagine web appropriate Nel corso del trimestre, le seguenti modifiche vengono accumulate nella copia del lancio:

* Modifiche apportate alle pagine sorgenti che si verificano in seguito alle consuete attività di manutenzione. Queste modifiche vengono automaticamente duplicate nelle pagine del lancio.
* Modifiche eseguite direttamente sulle pagine di lancio in preparazione del trimestre successivo.

Nel trimestre successivo, promuovi le pagine di lancio in modo da poter pubblicare le pagine sorgenti (mantenendo i contenuti aggiornati). Puoi promuovere tutte le pagine o solo quelle che hai modificato.

I lanci possono anche essere:

* Creati per rami principali multipli. Nonostante sia possibile creare il lancio per l&#39;intero sito (e apportare le modifiche desiderate), questa operazione potrebbe risultare poco pratica perché l&#39;intero sito dovrà essere copiato. Quando vengono coinvolte centinaia o persino migliaia di pagine, i requisiti e le prestazioni di sistema sono influenzate sia dall&#39;azione di copia che, in un secondo momento, dai confronti richiesti per le attività di promozione.
* Nidificato (un lancio all&#39;interno di un lancio), permette di creare un lancio da un lancio esistente, in modo che gli autori possano sfruttare le modifiche già apportate, senza dover eseguire le stesse modifiche più volte per ogni lancio.

Questa sezione spiega come creare, modificare e promuovere (e, se necessario, [eliminare](/help/sites-authoring/launches-creating.md#deleting-a-launch)) le pagine di lancio dall&#39;interno della console Sites o [della console dei lanci](#the-launches-console):

* [Creazione di lanci](/help/sites-authoring/launches-creating.md)
* [Modifica dei lanci](/help/sites-authoring/launches-editing.md)
* [Promozione del lancio](/help/sites-authoring/launches-promoting.md)

## Lanci - Ordine degli eventi {#launches-the-order-of-events}

La funzione Lanci consente di sviluppare i contenuti per il rilascio futuro di una o più pagine web attivate.

I lanci permettono di:

* Creare una copia delle pagine sorgenti:

   * La copia corrisponde al lancio.
   * Le pagine sorgenti di primo livello sono dette **Produzione**.

      * Le pagine sorgenti possono essere prelevate dai rami multipli (separati).
   ![chlimage_1-111](assets/chlimage_1-111.png)

* Modifica la configurazione di lancio:

   * Aggiungi o rimuovi pagine e/o rami al/dal lancio.
   * Modifica le proprietà di lancio; ad esempio, **Titolo lancio**, **Data lancio**, **Flag pronto** per la produzione.

* Puoi promuovere e pubblicare i contenuti manualmente o automaticamente:

   * Manualmente:

      * Promuovi il contenuto del lancio fino al **Target** (pagine sorgenti) quando è pronto per essere pubblicato.
      * Modifica il contenuto dalle pagine sorgenti (dopo la promozione).
      * Promuovi tutte le pagine o solo le pagine modificate.
   * Automaticamente - questo implica le seguenti attività:

      * Il campo **Data** **lancio**(**Live**): può essere impostato durante la creazione o la modifica di un lancio.

      * Il flag **pronto per la produzione**: può essere impostato solo quando si modifica un lancio.
      * Se il flag **pronto per la produzione** è impostato, il lancio verrà promosso automaticamente sulla pagine di produzione alla **data** **lancio**(**Live**) specificata. Dopo la promozione, le pagine di produzione sono pubblicate automaticamente.\
         Se la data non è stata impostata, il flag non ha alcun effetto.


* Aggiorna parallelamente la pagina sorgente e la pagina di lancio:

   * Le modifiche apportate alle pagine sorgenti vengono automaticamente implementate nella copia lancio (se impostate con ereditarietà; ovvero come Live Copy).
   * Le modifiche apportate alla copia di lancio possono essere effettuate senza interrompere gli aggiornamenti automatici o le pagine sorgenti.
   ![chlimage_1-112](assets/chlimage_1-112.png)

* [Crea un lancio nidificato](/help/sites-authoring/launches-creating.md#creating-a-nested-launch) - un lancio all&#39;interno di un lancio:

   * L’origine è un lancio esistente.
   * Puoi [promuovere un lancio nidificato](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch) per qualsiasi target; può trattarsi di un lancio padre o di pagine sorgenti di primo livello (Produzione).
   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!CAUTION]
   >
   >L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.

>[!NOTE]
>
>Creating and editing launches requires access rights to `/content/launches` - as with the default group `content-authors`.
>
>Per qualsiasi problema riscontrato, contatta l&#39;amministratore del sistema.

### La console dei lanci {#the-launches-console}

La console dei lanci fornisce una panoramica dei tuoi lanci e consente di intraprendere azioni su quelli elencati. Puoi accedere alla console da:

* La console **Strumenti**: **Strumenti**, **Sites**, **Lanci**.

* Or directly with [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## Lanci nei Riferimenti (console Sites) {#launches-in-references-sites-console}

1. Nella console **Sites**, vai all’origine dei lanci.
1. Apri la barra **Riferimenti** e seleziona la pagina sorgente.
1. Seleziona **Lanci** per visualizzare l’elenco dei lanci esistenti:

   ![screen-shot_2019-03-05at121901-1](assets/screen-shot_2019-03-05at121901-1.png)

1. Tocca o fai clic sul lancio appropriato per visualizzare l&#39;elenco delle azioni possibili :

   ![screen-shot_2019-03-05at121952-1](assets/screen-shot_2019-03-05at121952-1.png)
