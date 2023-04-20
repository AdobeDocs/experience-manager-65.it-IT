---
title: Utilizzo di Lanci per sviluppare contenuti per una versione futura
description: Lanci consente di sviluppare in modo efficiente i contenuti per una versione futura. Consentono di preparare le modifiche per la pubblicazione futura, mantenendo le pagine correnti.
uuid: 4bbd9865-735d-4232-b69c-b64193ac5d83
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e145afd8-7391-47aa-b389-16fb303749d0
docset: aem65
exl-id: b25d3f8e-5687-49ab-95e1-19ec75c87f6e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 36%

---

# Lanci{#launches}

I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro.

Il lancio creato consente di preparare modifiche pronte alla pubblicazione futura (mantenendo le tue pagine correnti). Dopo aver modificato e aggiornato le pagine di lancio, le promuovi nuovamente all’origine e quindi attivi le pagine sorgente (livello superiore). La promozione duplica il contenuto del lancio nelle pagine sorgente e può essere eseguita manualmente o automaticamente (a seconda dei campi impostati durante la creazione e la modifica del lancio).

Ad esempio, le pagine dei prodotti stagionali del tuo negozio online vengono aggiornate trimestralmente in modo che i prodotti in evidenza si allineino alla stagione corrente. Per preparare il prossimo aggiornamento trimestrale, puoi creare un lancio delle pagine web appropriate. Nel corso del trimestre, le seguenti modifiche vengono accumulate nella copia del lancio:

* Modifiche apportate alle pagine sorgenti che si verificano in seguito alle consuete attività di manutenzione. Queste modifiche vengono duplicate automaticamente nelle pagine del lancio.
* Modifiche eseguite direttamente sulle pagine del lancio in preparazione del trimestre successivo.

Nel trimestre successivo, promuovi le pagine di lancio in modo da poter pubblicare le pagine sorgenti (mantenendo i contenuti aggiornati). Puoi promuovere tutte le pagine o solo quelle che hai modificato.

I lanci possono anche essere:

* Creato per più rami principali. Nonostante sia possibile creare il lancio per l&#39;intero sito (e apportare le modifiche desiderate), questa operazione potrebbe risultare poco pratica perché l&#39;intero sito dovrà essere copiato. Quando sono coinvolte centinaia o persino migliaia di pagine, i requisiti di sistema e le prestazioni sono influenzati sia dall&#39;azione di copia che, successivamente, dai confronti richiesti per le attività di promozione.
* Nidificato (un lancio all’interno di un lancio) per consentirti di creare un lancio da un lancio esistente in modo che gli autori possano sfruttare le modifiche già apportate, anziché dover apportare le stesse modifiche più volte per ogni lancio.

Questa sezione descrive come creare, modificare e promuovere (e se necessario [delete](/help/sites-authoring/launches-creating.md#deleting-a-launch)) avvia le pagine dall’interno della console Sites o [la console Lanci](#the-launches-console):

* [Creazione dei lanci](/help/sites-authoring/launches-creating.md)
* [Modifica dei lanci](/help/sites-authoring/launches-editing.md)
* [Promozione dei lanci](/help/sites-authoring/launches-promoting.md)

## Lanci - Ordine degli eventi {#launches-the-order-of-events}

I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura di una o più pagine web attivate.

I lanci consentono di:

* Crea una copia delle pagine sorgente:

   * La copia è il lancio.
   * Le pagine sorgente di primo livello sono note come **Produzione**.

      * Le pagine sorgenti possono essere prelevate da più rami (separati).

   ![chlimage_1-111](assets/chlimage_1-111.png)

* Modifica la configurazione del lancio:

   * Aggiungi o rimuovi pagine e/o rami dal lancio.
   * Modifica le proprietà di lancio, come **Titolo**, **Data lancio** e il flag **Production Ready**.

* Puoi promuovere e pubblicare il contenuto manualmente o automaticamente:

   * Manualmente:

      * Promuovi il contenuto del lancio verso **Target** (pagine di origine) quando è pronto per essere pubblicato.
      * Pubblica il contenuto dalle pagine sorgente (dopo la promozione).
      * Promuovi tutte le pagine o solo le pagine modificate.
   * Automaticamente - questo implica le seguenti attività:

      * Il campo **Data** **lancio**(**Live**): può essere impostato durante la creazione o la modifica di un lancio.

      * La **Produzione pronta** bandiera: può essere impostato solo durante la modifica di un lancio.
      * Se la **Produzione pronta** è impostato il flag , il lancio verrà promosso automaticamente alle pagine di produzione nel **Launch**(**Live**) **date**. Dopo la promozione, le pagine di produzione vengono pubblicate automaticamente.\
         Se la data non è stata impostata, il flag non ha alcun effetto.


* Aggiorna parallelamente la pagina sorgente e la pagina di lancio:

   * Le modifiche apportate alle pagine sorgenti vengono automaticamente implementate nella copia lancio (se impostate con ereditarietà; ovvero come Live Copy).
   * Le modifiche apportate alla copia di lancio possono essere effettuate senza interrompere gli aggiornamenti automatici o le pagine sorgenti.

   ![chlimage_1-112](assets/chlimage_1-112.png)

* [Creare un lancio nidificato](/help/sites-authoring/launches-creating.md#creating-a-nested-launch) - un lancio in un lancio:

   * L&#39;origine è un lancio esistente.
   * È possibile [promuovere un lancio nidificato](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch) a qualsiasi bersaglio; può trattarsi di un lancio padre o di pagine sorgente di primo livello (Produzione).

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!CAUTION]
   >
   >L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.

>[!NOTE]
>
>La creazione e la modifica dei lanci richiede diritti di accesso a `/content/launches`- come per il gruppo predefinito `content-authors`.
>
>Per qualsiasi problema riscontrato, contatta l&#39;amministratore del sistema.

>[!CAUTION]
>
>Il riordinamento dei componenti in una pagina Launch non è supportato.
>
>Quando la pagina viene promossa, eventuali modifiche al contenuto verranno applicate, ma le posizioni dei componenti non cambieranno.


### Console Lanci {#the-launches-console}

La console Lanci fornisce una panoramica dei lanci e consente di intervenire sui quelli elencati. Puoi accedere alla console da:

* La console **Strumenti**: **Strumenti**, **Sites**, **Lanci**.

* Oppure direttamente con [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## Lanci nei riferimenti (console Sites) {#launches-in-references-sites-console}

1. In **Sites** console, passa all’origine dei lanci.
1. Apri **Riferimenti** e seleziona la pagina sorgente.
1. Seleziona **Lanci**, verranno elencati i lanci esistenti:

   ![screen-shot_2019-03-05at121901-1](assets/screen-shot_2019-03-05at121901-1.png)

1. Tocca o fai clic sul lancio appropriato per visualizzare l&#39;elenco delle azioni possibili:

   ![screen-shot_2019-03-05at121952-1](assets/screen-shot_2019-03-05at121952-1.png)
