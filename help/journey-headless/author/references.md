---
title: Informazioni sull’utilizzo dei riferimenti nei frammenti di contenuto
description: Imparare a utilizzare i riferimenti in Frammenti di contenuto, per i contenuti, altri frammenti e altre risorse (file multimediali). Introdurre la necessità e la meccanica dei frammenti nidificati per l’authoring CMS headless.
exl-id: d54a0a40-a8af-456a-9bf5-219d84540c97
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 98%

---

# Informazioni sull’utilizzo dei riferimenti nei frammenti di contenuto {#author-headless-references}

## Percorso affrontato finora {#story-so-far}

All’inizio del [Percorso di authoring dei contenuti headless in AEM](overview.md), nell’[Introduzione](introduction.md) sono stati trattati i concetti e la terminologia di base relativi all’authoring per headless.

Hai appreso le nozioni di base sull’authoring di CMS headless, con un’introduzione all’authoring con AEMaaCS e, in particolare, all’authoring di frammenti di contenuto.

Questo articolo si basa su questi elementi e spiega come utilizzare i riferimenti per creare contenuti personalizzati per il progetto headless in AEM.

## Obiettivo {#objective}

* **Pubblico**: avanzato
* **Obiettivo**: introdurre l’uso di riferimenti per l’authoring CMS headless. Quali tipi di riferimenti sono disponibili e quali sono i loro scopi:

   * Riferimenti al contenuto
   * Riferimenti a risorse/file multimediali
   * Riferimenti ai frammenti
   * Riferimenti ad hoc dall’interno di un blocco di testo

## Cosa sono i riferimenti {#what-are-references}

I riferimenti sono semplicemente un meccanismo per collegare le risorse, sia che si tratti di altro contenuto, di risorse (come nelle immagini) o di altri frammenti. Anche se molto simili, ci sono alcune differenze.

Alcuni riferimenti sono costituiti da tipi di dati dedicati (ad esempio, Riferimenti al contenuto e Riferimenti ai frammenti), mentre altri sono semplicemente aggiunti come riferimento all’interno di un blocco di testo (riferimenti alle risorse e riferimenti ad hoc).

![Frammenti di contenuto - Riferimenti](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Riferimenti al contenuto {#content-references}

I riferimenti al contenuto fanno proprio questo: ti consentono di fare riferimento a qualsiasi altro contenuto. Questo apre un browser che consente di selezionare l’elemento di contenuto.

## Riferimenti a risorse/file multimediali {#assets-media-references}

È possibile fare riferimento alle risorse (ad esempio, immagini o file multimediali) all’interno di un blocco di testo utilizzando l’opzione **Inserisci risorsa**. Questa apre un browser che consente di selezionare la risorsa.

![Frammenti di contenuto - Inserisci risorsa](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Riferimenti ai frammenti {#fragment-references}

Anche in questo caso, i riferimenti ai frammenti fanno solo questo: consentono di fare riferimento a un altro frammento. Per comprendere perché questo è significativo, è necessaria una spiegazione più completa.

Ad esempio, è possibile che siano definiti i seguenti modelli di frammento di contenuto:

* Città
* Azienda
* Persona
* Premi

Sembra abbastanza semplice, ma ovviamente un’Azienda ha sia un amministratore delegato che dei dipendenti....e queste sono tutte persone, ognuna definita come Persona.

E una Persona può ricevere un Premio (o forse due).

* La mia azienda - Azienda
   * Amministratore delegato - Persona
   * Dipendente/i - Persona
      * Premio(i) personale(i) - Premio

E siamo solo all’inizio. A seconda della complessità, un premio potrebbe essere specifico per l’Azienda o un’Azienda potrebbe avere la sua sede principale in una città specifica.

La rappresentazione di queste interrelazioni può essere effettuata con i Riferimenti ai frammenti, in quanto sono compresi sia da te (l’autore) che dalle applicazioni headless.

In qualità di autore, non sei responsabile della definizione di queste relazioni (attività svolta dall’architetto di contenuti durante la creazione del modello di frammento di contenuto), ma devi sapere come riconoscere e modificare i riferimenti.

### Come creare i frammenti nidificati {#author-nested-fragment}

L’authoring dei riferimenti ai frammenti è abbastanza semplice (anche se in genere il campo non sarà etichettato come **Riferimento a frammento**). È possibile digitare direttamente il riferimento oppure (più probabilmente) selezionare l’icona della cartella per aprire un browser che consente di sfogliare e selezionare il frammento desiderato.

![Frammenti di contenuto - Riferimenti](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La definizione del modello di frammento di contenuto controlla:

* se è possibile selezionare per aggiungere più riferimenti
* i tipi di modelli di frammenti di contenuto selezionabili; il modello frammento di contenuto definisce i modelli di frammento consentiti per il riferimento, pertanto AEM presenta solo i frammenti basati su tali modelli.

### Come accedere ai frammenti nidificati {#navigate-nested-fragment}

Utilizzando la scheda **Struttura ad albero** dell’Editor frammento di contenuto, ci si può spostare tra i frammenti a cui fa riferimento il tuo frammento e, quindi, tra eventuali riferimenti che i frammenti possono contenere. Quando si seleziona un riferimento, il frammento viene aperto per la modifica.

>[!NOTE]
>
>Utilizzando le breadcrumb nel pannello principale, puoi tornare indietro fino al punto iniziale.

![Struttura del frammento di contenuto](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Riferimenti ad hoc {#adhoc-references}

I riferimenti ad hoc possono essere aggiunti come semplice collegamento all’interno di un blocco di testo:

![Frammenti di contenuto - Riferimenti ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Passaggio successivo {#whats-next}

Ora che hai imparato i riferimenti e la struttura nei frammenti di contenuto, il passaggio successivo è [Informazioni su metadati e assegnazione tag](metadata-tagging.md). In questo modo verrà introdotto e illustrato come definire metadati e tag per i frammenti di contenuto.

## Risorse aggiuntive {#additional-resources}

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)

      * [Applica la configurazione alla cartella Risorse](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creazione di un frammento di contenuto](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Varianti - Authoring di frammenti di contenuto](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelli per frammenti di contenuto - Tipi di dati](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelli per frammenti di contenuto - Proprietà](/help/assets/content-fragments/content-fragments-models.md#properties)


* Guide introduttive
   * [Guida rapida alla creazione di una cartella Assets Headless](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Percorso Architect di contenuti AEM headless](/help/journey-headless/architect/overview.md)

* [Percorso di traduzione headless di AEM](/help/journey-headless/translation/overview.md)
