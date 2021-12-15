---
title: Informazioni sull’utilizzo dei riferimenti nei frammenti di contenuto
description: Scopri come utilizzare i riferimenti in Frammenti di contenuto, per contenuti, altri frammenti e altre risorse (file multimediali). Introdurre la necessità e la meccanica dei frammenti nidificati per l’authoring CMS headless.
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# Informazioni sull’utilizzo dei riferimenti nei frammenti di contenuto {#author-headless-references}

## La storia finora {#story-so-far}

All&#39;inizio del [AEM Percorso di authoring dei contenuti headless](overview.md) la [Introduzione](introduction.md) ha trattato i concetti e la terminologia di base relativi all&#39;authoring per headless.

Hai appreso le nozioni di base sull’authoring di CMS headless, con un’introduzione all’authoring con AEMaaCS e, in particolare, l’authoring di frammenti di contenuto.

Questo articolo si basa su questi elementi per comprendere come utilizzare i riferimenti per creare contenuti personalizzati per il progetto headless AEM.

## Obiettivo {#objective}

* **Pubblico**: Avanzate
* **Obiettivo**: Introdurre l&#39;uso di riferimenti per l&#39;authoring CMS headless. Quali tipi di riferimenti sono disponibili e quali sono i loro scopi:

   * Riferimenti contenuto
   * Riferimenti a risorse/file multimediali
   * Riferimenti ai frammenti
   * Riferimenti ad hoc all&#39;interno di un blocco di testo

## Riferimenti {#what-are-references}

I riferimenti sono semplicemente un meccanismo per collegare le risorse, siano esse altro contenuto, risorse (come nelle immagini) o altri frammenti. Anche se molto simile, ci sono alcune differenze.

Alcuni riferimenti dispongono di tipi di dati dedicati (ad esempio, Riferimenti al contenuto e Riferimenti ai frammenti), mentre altri sono semplicemente aggiunti come riferimento all’interno di un blocco di testo (riferimenti alle risorse e riferimenti ad hoc).

![Frammenti di contenuto - Riferimenti](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Riferimenti contenuto {#content-references}

I riferimenti al contenuto fanno proprio questo: ti consentono di fare riferimento a qualsiasi altro contenuto. Viene aperto un browser che consente di selezionare l’elemento di contenuto.

## Riferimenti a risorse/file multimediali {#assets-media-references}

È possibile fare riferimento alle risorse (ad esempio, immagini o file multimediali) all’interno di un blocco di testo utilizzando **Inserisci risorsa** opzione . Viene aperto un browser che consente di selezionare la risorsa.

![Frammenti di contenuto - Inserire una risorsa](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Riferimenti ai frammenti {#fragment-references}

Anche in questo caso, i riferimenti a frammenti consentono di fare riferimento a un altro frammento. Perché questo è significativo ha bisogno di un po&#39; più di spiegazione.

Ad esempio, è possibile che siano definiti i seguenti modelli di frammento di contenuto:

* Città
* Azienda
* Person
* Premi

Sembra abbastanza semplice, ma ovviamente un&#39;Azienda ha sia un amministratore delegato che dei dipendenti....e queste sono tutte persone, ognuna definita come Persona.

E una Persona può avere un Premio (o forse due).

* La mia azienda - Azienda
   * Amministratore delegato - Persona
   * Dipendente/i - Persona
      * Premio(i) personale(i) - Premio(i)

Ed è solo per cominciare. A seconda della complessità, un premio potrebbe essere specifico per l&#39;Azienda o un&#39;Azienda potrebbe avere la sua sede principale in una città specifica.

La rappresentazione di queste interrelazioni può essere ottenuta con i Riferimenti ai frammenti, in quanto sono compresi sia dall’utente (l’autore) che dalle applicazioni headless.

In qualità di autore, non sei responsabile della definizione di queste relazioni (come viene fatto dall’architetto di contenuti durante la creazione del modello di frammento di contenuto), ma devi sapere come riconoscere e modificare i riferimenti.

### Creazione di frammenti nidificati {#author-nested-fragment}

Authoring I riferimenti ai frammenti sono abbastanza semplici (anche se in genere il campo non viene etichettato come **Riferimento frammento**). È possibile digitare direttamente il riferimento oppure selezionare l’icona della cartella per aprire un browser che consente di spostarsi e selezionare il frammento desiderato.

![Frammenti di contenuto - Riferimenti](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La definizione del modello di frammento di contenuto controlla:

* se è possibile selezionare per aggiungere più riferimenti
* i tipi di modelli di frammenti di contenuto selezionabili; il modello frammento di contenuto definisce i modelli di frammento consentiti per il riferimento, pertanto AEM solo i frammenti basati su tali modelli.

### Navigazione tra i frammenti nidificati {#navigate-nested-fragment}

Utilizzo della **Struttura ad albero** La scheda dell’Editor frammento di contenuto consente di spostarsi tra i frammenti a cui fa riferimento il frammento e quindi tra eventuali riferimenti contenuti. Quando si seleziona un riferimento, il frammento viene aperto per la modifica.

>[!NOTE]
>
>Utilizzando le breadcrumb nel pannello principale è possibile tornare al punto iniziale.

![Struttura ad albero dei frammenti di contenuto](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Riferimenti ad hoc {#adhoc-references}

I riferimenti ad hoc possono essere aggiunti come semplice collegamento all’interno di un blocco di testo:

![Frammenti di contenuto - Riferimenti ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Novità {#whats-next}

Ora che hai imparato i riferimenti e la struttura nei frammenti di contenuto, il passaggio successivo è [Informazioni su metadati e tag](metadata-tagging.md). In questo modo verrà illustrato come definire metadati e tag per i frammenti di contenuto.

## Risorse aggiuntive {#additional-resources}

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)

      * [Applica la configurazione alla cartella delle risorse](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creazione di un frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Varianti - Authoring di frammenti di contenuto](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelli per frammenti di contenuto - Tipi di dati](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelli per frammenti di contenuto - Proprietà](/help/assets/content-fragments/content-fragments-models.md#properties)


* Guide introduttive
   * [Guida rapida alla creazione di una cartella Assets Headless](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [percorso di architetti di contenuti headless AEM](/help/journey-headless/architect/overview.md)

* [AEM Percorso di traduzione headless](/help/journey-headless/translation/overview.md)
