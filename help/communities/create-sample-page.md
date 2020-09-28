---
title: Creare una pagina di esempio
seo-title: Creare una pagina di esempio
description: Creare un sito della community di esempi
seo-description: Creare un sito della community di esempi
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 824ddd48e4680eed1d4612c6ad450a8f1bc68e7c
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---


# Creare una pagina di esempio {#create-a-sample-page}

A partire da AEM Community 6.1, il modo più semplice per creare una pagina di esempio è creare un sito community semplice, costituito semplicemente da una funzione Pagina.

Questo includerà un componente parsys in modo da poter [abilitare i componenti per l’authoring](basics.md#accessing-communities-components).

Un&#39;altra opzione per l&#39;esplorazione con componenti campione consiste nell&#39;utilizzare le funzioni presentate nella Guida [ai componenti](components-guide.md)comunitari.

## Creazione di un sito community {#create-a-community-site}

È molto simile alla creazione di un nuovo sito descritto in [Guida introduttiva  AEM Communities](getting-started.md).

La differenza principale è che questa esercitazione creerà un nuovo modello di sito community che contiene solo la funzione [](functions.md#page-function) Pagina per creare un sito community semplice privo di altre funzioni (diverse dalle funzioni precablate di base per tutti i siti community).

### Crea nuovo modello del sito {#create-new-site-template}

Per iniziare, create un semplice modello [di sito per](sites.md)community.

Per la navigazione globale in un’istanza di creazione, selezionate **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > Modelli **** sito.

![create-site-template](assets/create-site-template1.png)

* Seleziona `Create button`
* INFORMAZIONI DI BASE

   * `Name`: Modello per pagina singola
   * `Description`: Un modello composto da una funzione Pagina singola.
   * Seleziona `Enabled`

![site-template-editor](assets/site-template-editor.png)

* STRUTTURA

   * Trascinate una `Page` funzione nel generatore di modelli
   * Per i dettagli della funzione di configurazione, immettere

      * `Title`: Pagina singola
      * `URL`: page

![site-template-editor-structure](assets/site-template-editor1.png)

* Seleziona **`Save`** per la configurazione
* Selezionare **`Save`** per il modello di sito

### Crea nuovo sito community {#create-new-community-site}

Ora create un nuovo sito community basato sul modello di sito semplice.

Dopo aver creato il modello di sito, nella navigazione globale selezionate **[!UICONTROL Community > Siti]**.

![create-community-site](assets/create-community-site1.png)

* Seleziona **`Create`** icona

* Incremento `1 - Site Template`

   * `Title`: Sito community semplice
   * `Description`: Un sito community composto da una singola pagina di sperimentazione.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: esempio

      * url = http://localhost:4502/content/sites/sample

      * `Template`: scegli `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* Seleziona `Next`
* Incremento `2 - Design`

   * Selezionare una progettazione

* Seleziona `Next`
* Seleziona `Next`

   (Accetta tutte le impostazioni predefinite)

* Seleziona `Create`

   ![create-community-site](assets/create-community-site.png)

## Pubblicare il sito {#publish-the-site}

![sito di pubblicazione](assets/publish-site.png)

Dalla console [Siti](sites-console.md)community, selezionate l’icona Pubblica per pubblicare il sito, per impostazione predefinita, su http://localhost:4503.

## Aprire il sito in modalità di modifica {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Selezionate l’icona del sito aperto per visualizzare il sito in modalità di modifica.

L’URL sarà [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Nella semplice home page è possibile vedere cosa è preconnesso attraverso le funzioni e i modelli della community, e giocare con l&#39;aggiunta e la configurazione di componenti della community.

## Visualizza sito su Pubblica {#view-site-on-publish}

Dopo aver pubblicato la pagina, aprite la pagina nell’istanza [di](http://localhost:4503/content/sites/sample/en.html) pubblicazione per sperimentare le funzioni di visitatore anonimo del sito, membro firmato o amministratore. Il collegamento Amministrazione visibile nell’ambiente di authoring non viene visualizzato nell’ambiente di pubblicazione a meno che un amministratore non effettui l’accesso.
