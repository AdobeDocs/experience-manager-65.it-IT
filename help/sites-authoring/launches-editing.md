---
title: Modifica dei lanci
seo-title: Editing Launches
description: Quando è stato creato un lancio per una pagina (o per un insieme di pagine), è possibile modificare il contenuto nella copia di lancio della pagina (o delle pagine).
seo-description: After creating a launch for your page (or set of pages) you can edit the content in the launch copy of the page(s).
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 99%

---

# Modifica dei lanci{#editing-launches}

## Modifica delle pagine di lancio {#editing-launch-pages}

Dopo aver creato un lancio per una pagina o un insieme di pagine, è possibile modificarne il contenuto nella copia di lancio.

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Vai a pagina** per aprire la pagina e modificarla.

>[!NOTE]
>
>Non puoi spostare una pagina all’interno di un lancio. Il tentativo di eseguire questa azione attiva un messaggio di avviso:
>
>* Attenzione: questa pagina è l’origine di un lancio. Lo spostamento della pagina non è consentito.


### Modifica delle pagine di lanci soggette a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Se il lancio si basa su una [Live Copy](/help/sites-administering/msm.md):

* saranno visibili simboli a forma di piccoli lucchetti quando si pubblica un componente (contenuto e/o proprietà);
* sarà visibile la scheda **Copia live** in **Proprietà pagina**.

Una Live Copy viene utilizzata per sincronizzare il contenuto *dal* ramo di origine *al* ramo lancio, al fine di mantenere aggiornato il lancio con le modifiche apportate nell’origine.

È possibile apportare modifiche allo stesso modo in cui si può modificare una Live Copy standard, ad esempio:

* Facendo clic su un lucchetto chiuso si interrompe la sincronizzazione e saranno possibili nuovi aggiornamenti del contenuto nel lancio. Una volta sbloccato (lucchetto aperto), le modifiche non verranno sovrascritte da nessuna modifica apportata alla stessa posizione all&#39;interno del ramo sorgente.
* **Sospendi** (e **Riprendi**) l’ereditarietà per una pagina specifica.

Per ulteriori informazioni, consulta [Modifica del contenuto per Live Copy](/help/sites-administering/msm-livecopy.md#changing-live-copy-content).

## Confronto tra una pagina di lancio e la relativa pagina sorgente {#comparing-a-launch-page-to-its-source-page}

Per tenere traccia delle modifiche apportate, puoi visualizzare il lancio in **Riferimenti** e confrontare la pagina del lancio con la relativa pagina di origine:

1. Nella console **Sites**, [spostati sulla pagina di origine del lancio e selezionala](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. Apri il pannello **[Riferimenti](/help/sites-authoring/basic-handling.md#references)** e seleziona **Lanci**.
1. Seleziona il tuo specifico lancio, quindi **Confronta con origine**:

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. Le due pagine (di lancio e di origine) verranno aperte una accanto all&#39;altra.

   Per informazioni complete sull&#39;utilizzo di questa funzionalità, consulta [Differenze tra pagine](/help/sites-authoring/page-diff.md).

## Modifica delle pagine di origine utilizzate {#changing-the-source-pages-used}

In qualsiasi momento è possibile aggiungere o rimuovere pagine da e verso la gamma di pagine di origine per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:

   * Dalla [console Lanci](/help/sites-authoring/launches.md#the-launches-console):

      * Seleziona **Modifica**.
   * Da [Riferimenti (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) per mostrare le azioni disponibili:

      * Seleziona **Modifica lancio**.

   Vengono visualizzate le pagine di origine.

1. Apporta le modifiche necessarie, quindi conferma con **Salva**.

   >[!NOTE]
   >
   >Per aggiungere pagine a un lancio, queste devono essere sotto una radice linguistica comune, cioè all&#39;interno di un singolo sito.

## Modifica di una configurazione di lancio {#editing-a-launch-configuration}

In qualsiasi momento è possibile modificare le proprietà per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:

   * Dalla [console Lanci](/help/sites-authoring/launches.md#the-launches-console):

      * Seleziona **Proprietà**.
   * Da [Riferimenti (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) per mostrare le azioni disponibili:

      * Seleziona **Modifica proprietà**.

   Verranno visualizzati i dettagli.

1. Apporta le modifiche necessarie, quindi conferma con **Salva**.

   Consulta la sezione [Lanci - Ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events) per informazioni sullo scopo e sull’interazione dei campi **Data lancio** e **Production Ready**.

## Rilevamento dello stato del lancio di una pagina {#discovering-the-launch-status-of-a-page}

Lo stato viene visualizzato quando si seleziona un lancio specifico dalla scheda Riferimenti (consulta [Avvia in Riferimenti (Console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console)).

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
