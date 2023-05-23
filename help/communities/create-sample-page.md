---
title: Crea una pagina di esempio
seo-title: Create a Sample Page
description: Creare un sito community di esempio
seo-description: Create a Sample community site
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# Crea una pagina di esempio {#create-a-sample-page}

A partire da AEM 6.1 Communities, il modo più semplice per creare una pagina di esempio è quello di creare un sito community semplice, costituito semplicemente da una funzione Pagina.

Questo includerà un componente parsys in modo che tu possa [abilita componenti per l’authoring](basics.md#accessing-communities-components).

Un&#39;altra opzione per l&#39;esplorazione con componenti di esempio consiste nell&#39;utilizzare le feature presentate nella [Guida ai componenti della community](components-guide.md).

## Creare un sito community {#create-a-community-site}

È molto simile alla creazione di un nuovo sito descritto in [Guida introduttiva ad AEM Communities](getting-started.md).

La differenza principale è che questa esercitazione creerà un nuovo modello di sito community che contiene solo [Funzione pagina](functions.md#page-function) per creare un semplice sito community privo di altre funzioni (diverse dalle funzioni precollegate di base per tutti i siti community).

### Crea nuovo modello sito {#create-new-site-template}

Per iniziare, crea un’ [modello per sito community](sites.md).

Dalla navigazione globale su un’istanza Autore, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Modelli del sito]**.

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

Ora crea un nuovo sito community basato sul modello di sito semplice.

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

L’URL sarà [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Nella semplice home page è possibile vedere cosa è preconnesso attraverso le funzioni e i modelli della community e giocare con l&#39;aggiunta e la configurazione di componenti della community.

## Visualizza sito alla pubblicazione {#view-site-on-publish}

Dopo aver pubblicato la pagina, apri la pagina in [istanza di pubblicazione](http://localhost:4503/content/sites/sample/en.html) per sperimentare le funzioni di visitatore anonimo del sito, membro connesso o amministratore. Il collegamento Amministrazione visibile nell’ambiente di authoring non viene visualizzato nell’ambiente di pubblicazione a meno che un amministratore non effettui l’accesso.
