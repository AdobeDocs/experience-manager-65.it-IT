---
title: Crea una pagina di esempio
description: Scopri come creare un modello per sito community contenente solo la funzione Pagina, che consente di creare un sito community semplice.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---

# Crea una pagina di esempio {#create-a-sample-page}

A partire da AEM 6.1 Communities, il modo più semplice per creare una pagina di esempio è quello di creare un sito community semplice, costituito semplicemente da una funzione Pagina.

Questo include un componente parsys che consente di: [abilita componenti per l’authoring](basics.md#accessing-communities-components).

Un&#39;altra opzione per l&#39;esplorazione con componenti di esempio consiste nell&#39;utilizzare le feature presentate nella [Guida ai componenti della community](components-guide.md).

## Creare un sito community {#create-a-community-site}

È simile alla creazione di un sito descritto in [Guida introduttiva ad AEM Communities](getting-started.md).

La differenza principale consiste nel fatto che questa esercitazione crea un modello di sito community contenente solo [Funzione pagina](functions.md#page-function) per creare un sito community semplice. Questa operazione è priva di altre funzioni (diverse dalle funzioni pre-cablate di base per tutti i siti della community).

### Crea nuovo modello sito {#create-new-site-template}

Per iniziare, crea un’ [modello per sito community](sites.md).

Dalla navigazione globale in un’istanza Autore, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Modelli del sito]**.

![create-site-template](assets/create-site-template1.png)

* Seleziona `Create button`
* INFORMAZIONI DI BASE

   * `Name`: modello a pagina singola
   * `Description`: modello costituito da una singola funzione Page.
   * Seleziona `Enabled`

![site-template-editor](assets/site-template-editor.png)

* STRUTTURA

   * Trascina un `Page` al Generatore di modelli
   * Per Dettagli funzione di configurazione, immetti

      * `Title`: Pagina singola
      * `URL`: pagina

![site-template-editor-structure](assets/site-template-editor1.png)

* Seleziona **`Save`** per configurazione
* Seleziona **`Save`** per il modello di sito

### Crea nuovo sito community {#create-new-community-site}

Ora crea un sito community basato sul modello di sito semplice.

Dopo aver creato il modello del sito, dalla navigazione globale seleziona **[!UICONTROL Community > Siti]**.

![create-community-site](assets/create-community-site1.png)

* Seleziona **`Create`** icona

* Passaggio `1 - Site Template`

   * `Title`: sito community semplice
   * `Description`: sito della community costituito da una singola pagina a scopo di sperimentazione.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: esempio

      * url = http://localhost:4502/content/sites/sample

      * `Template`: scegli `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* Seleziona `Next`
* Passaggio `2 - Design`

   * Seleziona qualsiasi design

* Seleziona `Next`
* Seleziona `Next`

  (Accetta tutte le impostazioni predefinite)

* Seleziona `Create`

  ![create-community-site](assets/create-community-site.png)

## Pubblicare il sito {#publish-the-site}

![publish-site](assets/publish-site.png)

Dalla sezione [console per siti community](sites-console.md), seleziona l’icona Pubblica per pubblicare il sito, per impostazione predefinita http://localhost:4503.

## Apri il sito su Author in modalità Modifica {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Selezionare l&#39;icona Apri sito per visualizzare il sito in modalità di modifica.

L’URL è [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Nella semplice home page è possibile vedere cosa è preconnesso tramite le funzioni e i modelli della community e giocare con l&#39;aggiunta e la configurazione di componenti della community.

## Visualizza sito alla pubblicazione {#view-site-on-publish}

Dopo aver pubblicato la pagina, apri la pagina in [istanza di pubblicazione](http://localhost:4503/content/sites/sample/en.html) per sperimentare le funzioni di visitatore anonimo del sito, membro connesso o amministratore. Il collegamento Amministrazione visibile nell’ambiente di authoring non viene visualizzato nell’ambiente di pubblicazione a meno che un amministratore non effettui l’accesso.
