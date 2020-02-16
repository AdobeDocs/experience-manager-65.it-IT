---
title: Pubblicazione delle pagine
seo-title: Pubblicazione delle pagine
description: 'null'
seo-description: 'null'
uuid: 57795e4a-e528-4e74-ad9c-e13f868daebb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1f5eb646-acc7-49d5-b839-e451e68ada9e
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Pubblicazione delle pagine {#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, [devi renderli disponibili nel sito Web pubblico](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Quando si pubblica e si annulla la pubblicazione di una pagina, quest’ultima rimane disponibile nell’ambiente di authoring per ulteriori modifiche, finché non decidi di eliminarla.

Puoi pubblicare o annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

>[!NOTE]
>
>Alcuni termini correlati alla pubblicazione possono creare confusione:
>
>* **Pubblicare / Annullare la pubblicazione**
   >  Termini principali per le azioni che rendono o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
   >
   >
* **Attiva/Disattiva**
   >  Sinonimi di pubblicare/annullare la pubblicazione.
   >
   >
* **Replicare / Replica**
   >  Si tratta dei termini tecnici che descrivono lo spostamento di dati (ad esempio contenuto di una pagina, file, codice, commenti degli utenti) da un ambiente all&#39;altro, ad esempio per la pubblicazione o la replica inversa dei commenti degli utenti.
>



>[!NOTE]
>
>Se non disponi delle autorizzazioni necessarie per pubblicare una specifica pagina:
>
>* Viene avviato un flusso di lavoro per comunicare al soggetto adeguato la tua richiesta di pubblicazione.
>* Questo [flusso di lavoro potrebbe essere stato personalizzato](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) dal team di sviluppo.
>* Verrà visualizzato brevemente un messaggio che informa che il flusso di lavoro è stato attivato.
>



## Pubblicazione delle pagine {#publishing-pages-1}

A seconda della tua posizione, puoi pubblicare:

* [Dall’Editor pagina](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [Dalla console Sites](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### Pubblicazione dall’editor {#publishing-from-the-editor}

Se stai modificando una pagina, puoi pubblicarla direttamente dall’editor.

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. A seconda che la pagina includa o meno riferimenti che devono essere pubblicati:

   * La pagina verrà pubblicata direttamente, se non sono presenti riferimenti da pubblicare.
   * Se la pagina include riferimenti da pubblicare, questi saranno elencati nella procedura guidata di **Pubblicazione**, dove è possibile:

      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.

      * utilizzare **Annulla** per annullare l’azione.
   ![chlimage_1](assets/chlimage_1.png)

1. Selecting **Publish** will replicate the page to the publish environment. Nell’editor pagina verrà visualizzato un banner informativo che conferma l’azione di pubblicazione.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Quando visualizzi la stessa pagina nella console, lo stato aggiornato della pubblicazione è visibile.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>La pubblicazione dall’editor è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

### Pubblicazione dalla console {#publishing-from-the-console}

Nella console Sites vi sono due opzioni di modifica:

* [Pubblicazione rapida](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gestisci pubblicazione](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Pubblicazione rapida {#quick-publish}

**Pubblicazione** rapida si riferisce a casi semplici e pubblica immediatamente le pagine selezionate senza ulteriore interazione. Anche eventuali riferimenti non pubblicati verranno pubblicati automaticamente.

Per pubblicare una pagina con Pubblicazione rapida:

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![pp-02](assets/pp-02.png)

1. In the Quick Publish dialogue, confirm the publication by clicking on **Publish** or cancel by clicking on **Cancel**. Tieni presente che verranno pubblicati automaticamente anche eventuali riferimenti non pubblicati.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Quando la pagina viene pubblicata, viene visualizzato un avviso di conferma della pubblicazione.

>[!NOTE]
>
>La pubblicazione rapida è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

#### Gestisci pubblicazione {#manage-publication}

**Gestisci pubblicazione** offre più opzioni rispetto alla pubblicazione rapida, consentendo l’inclusione di pagine figlie, la personalizzazione dei riferimenti e l’avvio di eventuali flussi di lavoro applicabili, nonché l’opzione di pubblicazione in un secondo momento.

Per pubblicare una pagina o annullarne la pubblicazione tramite Gestisci pubblicazione:

1. Select the page or pages in the sites console and click on the **Manage Publication** button.

   ![pp-02-1](assets/pp-02-1.png)

1. The **Manage Publication** wizard starts. The first step, **Options**, allows you to:

   * Scegliere di pubblicare le pagine selezionate o annullarne la pubblicazione.
   * Scegliere di eseguire l’azione immediatamente o in un secondo momento.
   Con Pubblica più tardi viene avviato un flusso di lavoro per attivare le pagine selezionate alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per disattivare le pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-administering/workflows.md) e interrompete il flusso di lavoro corrispondente.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Fai clic su **Avanti** per continuare.

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/unpublication such as including to include child pages and/or including references.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   You can use the **Add Content** button to add additional pages to the list of pages to be published in case you neglected to select one before starting the Manage Publication wizard.

   Facendo clic sul pulsante Aggiungi contenuto si avvia il [browser percorsi](/help/sites-authoring/author-environment-tools.md#path-browser), che consente di selezionare contenuti.

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   Nella procedura guidata puoi selezionare un elemento nell’elenco per configurare ulteriori opzioni, come:

   * Includere gli elementi figlio.
   * Rimuoverlo dalla selezione.
   * Gestire i relativi riferimenti pubblicati.
   ![pp-03](assets/pp-03.png)

   Clicking **Include Children** opens a dialogue allowing you to:

   * Solo gli elementi figli di primo livello.
   * Solo pagine modificate.
   * Solo pagine già pubblicate.
   Click **Add** to add the children pages to the list of pages to be published or unpublished based on the selection options. Click **Cancel** to cancel the selection and return to the wizard.

   ![chlimage_1-3](assets/chlimage_1-3.png)

   Tornando alla procedura guidata vengono visualizzate le pagine aggiunte in base alle opzioni selezionate nella finestra di dialogo Includi elementi figlio.

   You can view and modify the references to be published or unpublished for a page by selecting it and then clicking the **Published References** button.

   ![pp-04](assets/pp-04.png)

   The **Published References** dialogue displayes the references for the selected content. Per impostazione predefinita sono tutti selezionati e verranno pubblicati o ne verrà annullata la pubblicazione, ma puoi deselezionarli in modo da non includerli nell’azione.

   Click **Done** to save your changes or **Cancel** to cancel the selction and return to the wizard.

   Nella procedura guidata, la colonna **Riferimenti** verrà aggiornata per riflettere la selezione dei riferimenti da pubblicare o di cui annullare la pubblicazione.

   ![pp-05](assets/pp-05.png)

1. Click **Publish** to complete.

   Nella console Sites, un messaggio di notifica confermerà la pubblicazione.

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the [previous note on this page](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) for details.

   Le risorse vengono raggruppate in base ai flussi di lavoro attivati e per ognuna sono disponibili opzioni per:

   * Definire il titolo del flusso di lavoro.
   * Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * Definire un titolo del pacchetto del flusso di lavoro se è stata selezionata l’opzione per mantenere il pacchetto del flusso di lavoro.
   Click **Publish** or **Publish Later** to complete the publication.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Annullamento della pubblicazione delle pagine {#unpublishing-pages}

L’annullamento della pubblicazione di una pagina ne effettua la rimozione dall’ambiente di pubblicazione e la pagina non sarà più disponibile per i lettori.

In a [manner similar to publishing](/help/sites-authoring/publishing-pages.md#publishing-pages), one or more pages can be unpublished:

* [Dall’Editor pagina](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [Dalla console Sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Annullamento della pubblicazione dall’editor {#unpublishing-from-the-editor}

Durante la modifica di una pagina, se desideri annullarne la pubblicazione seleziona **Annulla pubblicazione pagina** nel menu **Informazioni pagina**. La procedura è simile a quella di [pubblicazione della pagina](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

### Annullamento della pubblicazione dalla console {#unpublishing-from-the-console}

Puoi utilizzare [l’opzione Gestisci pubblicazione per eseguire la pubblicazione](/help/sites-authoring/publishing-pages.md#manage-publication), ma anche per annullarla.

1. Select the page or pages in the sites console and click on the **Manage Publication** button.
1. The **Manage Publication** wizard starts. In the first step, **Options**, select to **Unpublish** instead of the default option of **Publish**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   Con Pubblica più tardi viene avviato un flusso di lavoro per pubblicare tale versione della pagina alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per annullare la pubblicazione delle pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-administering/workflows.md) e interrompete il flusso di lavoro corrispondente.

1. Per completare l’annullamento della pubblicazione, continua a seguire la procedura guidata come faresti per [pubblicare la pagina](/help/sites-authoring/publishing-pages.md#manage-publication).

## Pubblicazione e annullamento della pubblicazione di una struttura {#publishing-and-unpublishing-a-tree}

Se hai inserito o aggiornato un numero considerevole di pagine di contenuto, tutte residenti sotto la stessa pagina principale, può essere più semplice pubblicare l’intera struttura con una singola azione.

Puoi utilizzare l’opzione [Gestisci pubblicazione](/help/sites-authoring/publishing-pages.md#manage-publication) sulla console Sites per eseguire questa operazione.

1. Nella console Sites, seleziona la pagina principale della struttura che desideri pubblicare o di cui desideri annullare la pubblicazione e seleziona **Gestisci pubblicazione**.
1. The **Manage Publication** wizard starts. Scegli se e quando eseguire o annullare la pubblicazione, quindi seleziona **Avanti** per continuare.
1. Nel passaggio **Ambito**, seleziona la pagina principale e seleziona **Includi elementi figlio**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Nella finestra di dialogo **Includi elementi figlio**, deseleziona le opzioni:

   * Solo gli elementi figli di primo livello
   * Solo pagine già pubblicate
   Queste opzioni sono selezionate per impostazione predefinita, pertanto dovrai ricordarti di deselezionarle. Fai clic su **Aggiungi** per confermare e aggiungere il contenuto alla pubblicazione o all’annullamento della pubblicazione.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. La procedura guidata **Gestisci pubblicazione** elenca il contenuto della struttura a scopi di revisione. Puoi personalizzare ulteriormente la selezione aggiungendo ulteriori pagine o rimuovendo quelle selezionate.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [Continua a seguire normalmente](#manage-publication) la procedura guidata Gestisci pubblicazione per completare la pubblicazione o annullare la pubblicazione della struttura.

## Determinazione dello stato di pubblicazione {#determining-publication-status}

Puoi determinare lo stato di pubblicazione di una pagina:

* Nelle [informazioni generali sulla risorsa nella console Sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) 

   ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

   Lo stato di pubblicazione è indicato nelle viste [a schede](/help/sites-authoring/basic-handling.md#card-view), [a colonne](/help/sites-authoring/basic-handling.md#column-view) e [a elenco](/help/sites-authoring/basic-handling.md#list-view) nella console Sites.

* In the [timeline](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* In the [Page Information menu](/help/sites-authoring/author-environment-tools.md#page-information) when editing a page

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
