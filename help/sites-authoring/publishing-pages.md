---
title: Pubblicazione delle pagine
seo-title: Publishing Pages
description: Pubblicazione delle pagine
seo-description: null
uuid: 57795e4a-e528-4e74-ad9c-e13f868daebb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1f5eb646-acc7-49d5-b839-e451e68ada9e
docset: aem65
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
source-git-commit: 9946bfd3c2701a37d13e6eb6b4c19562ef77d24c
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 85%

---

# Pubblicazione delle pagine {#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, [devi renderli disponibili nel sito Web pubblico](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Quando si pubblica e si annulla la pubblicazione di una pagina, quest’ultima rimane disponibile nell’ambiente di authoring per ulteriori modifiche, finché non decidi di eliminarla.

Puoi pubblicare o annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

>[!NOTE]
>
>Alcuni termini correlati alla pubblicazione possono creare confusione:
>
>* **Pubblicare/Annullare la pubblicazione**
   >  Termini principali per le azioni che consentono di rendere o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
>
>* **Attivare/Disattivare**
   >  Sinonimi di pubblicare/annullare la pubblicazione.
>
>* **Replicare/Replica**
   >  Si tratta dei termini tecnici che descrivono lo spostamento di dati (ad esempio contenuto di pagina, file, codice, commenti degli utenti) da un ambiente all’altro, ad esempio per la pubblicazione o la replica inversa dei commenti degli utenti.
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

* [Dall’editor di pagine](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [Dalla console Sites](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### Pubblicazione dall’editor {#publishing-from-the-editor}

Se stai modificando una pagina, puoi pubblicarla direttamente dall’editor.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu, quindi l’opzione **Pubblica pagina**.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. A seconda che la pagina includa o meno riferimenti che devono essere pubblicati:

   * La pagina verrà pubblicata direttamente, se non sono presenti riferimenti da pubblicare.
   * Se la pagina include riferimenti da pubblicare, questi saranno elencati nella procedura guidata di **Pubblicazione**, dove è possibile:

      * Specifica le risorse, i tag ecc. da pubblicare insieme alla pagina, quindi seleziona **Pubblica** per completare il processo.

      * Seleziona **Annulla** per annullare l’azione.

   ![chlimage_1](assets/chlimage_1.png)

1. Se selezioni l’opzione **Pubblica**, la pagina verrà replicata nell’ambiente di pubblicazione. Nell’editor di pagine verrà visualizzato un banner informativo che conferma l’azione di pubblicazione.

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   Quando visualizzi la stessa pagina nella console, lo stato aggiornato della pubblicazione è visibile.

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>La pubblicazione dall’editor è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

>[!NOTE]
>
>Non è possibile pubblicare le pagine accessibili da [alias](/help/sites-authoring/editing-page-properties.md#advanced) nell’editor. Le opzioni di pubblicazione nell’editor sono disponibili solo per le pagine accessibili tramite i percorsi effettivi.

### Pubblicazione dalla console {#publishing-from-the-console}

Nella console Sites vi sono due opzioni di modifica:

* [Pubblicazione rapida ](/help/sites-authoring/publishing-pages.md#quick-publish)
* [Gestisci pubblicazione ](/help/sites-authoring/publishing-pages.md#manage-publication)

#### Pubblicazione rapida  {#quick-publish}

**Pubblicazione rapida** si usa in casi semplici; le pagine selezionate vengono pubblicate immediatamente senza ulteriore interazione. Anche eventuali riferimenti non pubblicati verranno pubblicati automaticamente.

Per pubblicare una pagina con Pubblicazione rapida:

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Pubblicazione rapida**.

   ![pp-02](assets/pp-02.png)

1. Nella finestra di dialogo Pubblicazione rapida, conferma la pubblicazione facendo clic su **Pubblica** o annulla la pubblicazione facendo clic su **Annulla**. Tieni presente che verranno pubblicati automaticamente anche eventuali riferimenti non pubblicati.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Quando la pagina viene pubblicata, viene visualizzato un avviso di conferma della pubblicazione.

>[!NOTE]
>
>La pubblicazione rapida è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

#### Gestisci pubblicazione  {#manage-publication}

**Gestisci pubblicazione** offre più opzioni rispetto alla pubblicazione rapida e consente di includere pagine figlie, personalizzare i riferimenti e avviare tutti i flussi di lavoro applicabili; consente inoltre di pubblicare la pagina in un secondo momento.

Per pubblicare una pagina o annullarne la pubblicazione tramite Gestisci pubblicazione:

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**.

   ![pp-02-1](assets/pp-02-1.png)

1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Il primo passaggio, **Opzioni**, consente di:

   * Scegliere di pubblicare le pagine selezionate o annullarne la pubblicazione.
   * Scegliere di eseguire l’azione immediatamente o in un secondo momento.

   Con Pubblica più tardi viene avviato un flusso di lavoro per attivare le pagine selezionate alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per disattivare le pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-administering/workflows.md) e interrompete il flusso di lavoro corrispondente.

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Fai clic su **Avanti** per continuare.

1. Nel passaggio successivo della procedura guidata Gestisci pubblicazione, **Ambito**, puoi definire l&#39;ambito della pubblicazione o dell&#39;annullamento della pubblicazione, ad esempio per includere pagine figlie e/o riferimenti.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   Puoi usare il pulsante **Aggiungi contenuto** per aggiungere ulteriori pagine all’elenco delle pagine da pubblicare, nel caso in cui ti sia dimenticato di selezionarne una prima di avviare la procedura guidata Gestisci pubblicazione.

   Facendo clic sul pulsante Aggiungi contenuto si avvia il [browser percorsi](/help/sites-authoring/author-environment-tools.md#path-browser), che consente di selezionare contenuti.

   Seleziona le pagine desiderate e fai clic su **Seleziona** per aggiungere contenuti alla procedura guidata o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   Nella procedura guidata puoi selezionare un elemento nell’elenco per configurare ulteriori opzioni, come:

   * Includere gli elementi figlio.
   * Rimuoverlo dalla selezione.
   * Gestire i relativi riferimenti pubblicati.

   ![pp-03](assets/pp-03.png)

   Facendo clic su **Includi elementi figlio** viene visualizzata una finestra di dialogo che consente di includere:

   * Solo gli elementi figli di primo livello.
   * Solo pagine modificate.
   * Solo pagine già pubblicate.

   Fai clic su **Aggiungi** per aggiungere le pagine figlio nell’elenco delle pagine da pubblicare o di cui annullare la pubblicazione, in base alle opzioni selezionate. Fai clic su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   ![chlimage_1-3](assets/chlimage_1-3.png)

   Tornando alla procedura guidata vengono visualizzate le pagine aggiunte in base alle opzioni selezionate nella finestra di dialogo Includi elementi figlio.

   Puoi visualizzare e modificare i riferimenti da pubblicare o di cui annullare la pubblicazione per una pagina selezionandola e facendo clic sul pulsante **Riferimenti pubblicati**.

   ![pp-04](assets/pp-04.png)

   La finestra di dialogo **Riferimenti pubblicati** visualizza i riferimenti per il contenuto selezionato. Per impostazione predefinita sono tutti selezionati e verranno pubblicati o ne verrà annullata la pubblicazione, ma puoi deselezionarli in modo da non includerli nell’azione.

   Fai clic su **Fine** per salvare le modifiche o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   Nella procedura guidata, la colonna **Riferimenti** verrà aggiornata per riflettere la selezione dei riferimenti da pubblicare o di cui annullare la pubblicazione.

   ![pp-05](assets/pp-05.png)

1. Fai clic su **Pubblica** per completare l’azione.

   Nella console Sites, un messaggio di notifica confermerà la pubblicazione.

1. Se le pagine pubblicate sono associate a flussi di lavoro, potrebbero essere visualizzati in un passaggio finale **Flussi di lavoro** della procedura guidata di pubblicazione.

   >[!NOTE]
   >
   >Il passaggio **Flussi di lavoro** verrà visualizzato in base ai diritti di cui dispone l’utente. Per ulteriori informazioni, consulta la [nota precedente su questa pagina](/help/sites-authoring/publishing-pages.md#main-pars-note-0-ejsjqg-refd) relativa ai privilegi di pubblicazione, nonché [Gestione dell’accesso ai flussi di lavoro](/help/sites-administering/workflows-managing.md) e [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd) .

   Le risorse vengono raggruppate in base ai flussi di lavoro attivati e per ognuna sono disponibili opzioni per:

   * Definire il titolo del flusso di lavoro.
   * Mantenere il pacchetto del flusso di lavoro, a condizione che il flusso di lavoro sia dotato di [supporto per più risorse](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * Definire un titolo del pacchetto del flusso di lavoro se è stata selezionata l’opzione per mantenere il pacchetto del flusso di lavoro.

   Fai clic su **Pubblica** o **Pubblica più tardi** per completare la pubblicazione.

   ![chlimage_1-4](assets/chlimage_1-4.png)

## Annullamento della pubblicazione delle pagine {#unpublishing-pages}

L’annullamento della pubblicazione di una pagina ne effettua la rimozione dall’ambiente di pubblicazione e la pagina non sarà più disponibile per i lettori.

Con una procedura [simile alla pubblicazione](/help/sites-authoring/publishing-pages.md#publishing-pages), è possibile annullare la pubblicazione di una o più pagine:

* [Dall’editor di pagine](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [Dalla console Sites](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### Annullamento della pubblicazione dall’editor  {#unpublishing-from-the-editor}

Durante la modifica di una pagina, se desideri annullarne la pubblicazione seleziona **Annulla pubblicazione pagina** nel menu **Informazioni pagina**. La procedura è simile a quella di [pubblicazione della pagina](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>Le pagine a cui si accede da [alias](/help/sites-authoring/editing-page-properties.md#advanced) nell&#39;editor non possono essere annullate. Le opzioni di pubblicazione nell’editor sono disponibili solo per le pagine accessibili tramite i percorsi effettivi.

### Annullamento della pubblicazione dalla console  {#unpublishing-from-the-console}

Puoi utilizzare [l’opzione Gestisci pubblicazione per eseguire la pubblicazione](/help/sites-authoring/publishing-pages.md#manage-publication), ma anche per annullarla.

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Nel primo passaggio, **Opzioni**, seleziona **Annulla pubblicazione** anziché l’opzione predefinita **Pubblica**.

   ![chlimage_1-5](assets/chlimage_1-5.png)

   Con Pubblica più tardi viene avviato un flusso di lavoro per pubblicare tale versione della pagina alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per annullare la pubblicazione delle pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-administering/workflows.md) e interrompete il flusso di lavoro corrispondente.

1. Per completare l’annullamento della pubblicazione, continua a seguire la procedura guidata come faresti per [pubblicare la pagina](/help/sites-authoring/publishing-pages.md#manage-publication).

## Pubblicazione e annullamento della pubblicazione di una struttura {#publishing-and-unpublishing-a-tree}

Se hai inserito o aggiornato un numero considerevole di pagine di contenuto, tutte residenti sotto la stessa pagina principale, può essere più semplice pubblicare l’intera struttura con una singola azione.

Puoi utilizzare l’opzione [Gestisci pubblicazione](/help/sites-authoring/publishing-pages.md#manage-publication) sulla console Sites per eseguire questa operazione.

1. Nella console Sites, seleziona la pagina principale della struttura che desideri pubblicare o di cui desideri annullare la pubblicazione e seleziona **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Scegli se e quando eseguire o annullare la pubblicazione, quindi seleziona **Avanti** per continuare.
1. Nel passaggio **Ambito**, seleziona la pagina principale e seleziona **Includi elementi figlio**.

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. Nella finestra di dialogo **Includi elementi figlio**, deseleziona le opzioni:

   * Solo gli elementi figli di primo livello
   * Solo pagine già pubblicate

   Queste opzioni sono selezionate per impostazione predefinita, pertanto dovrai ricordarti di deselezionarle. Fai clic su **Aggiungi** per confermare e aggiungere il contenuto alla pubblicazione o all’annullamento della pubblicazione.

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. La procedura guidata **Gestisci pubblicazione** elenca il contenuto della struttura a scopi di revisione. Puoi personalizzare ulteriormente la selezione aggiungendo ulteriori pagine o rimuovendo quelle selezionate.

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   Non dimenticare che è anche possibile esaminare i riferimenti da pubblicare tramite l’opzione **Riferimenti pubblicati**.

1. [Continua a seguire la procedura guidata Gestisci pubblicazione come ](#manage-publication) normale per completare la pubblicazione o annullare la pubblicazione della struttura.

## Determinazione dello stato di pubblicazione {#determining-publication-status}

Puoi determinare lo stato di pubblicazione di una pagina:

* Nelle [informazioni generali sulla risorsa nella console Sites](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

   Lo stato di pubblicazione è indicato nelle viste [a schede](/help/sites-authoring/basic-handling.md#card-view), [a colonne](/help/sites-authoring/basic-handling.md#column-view) e [a elenco](/help/sites-authoring/basic-handling.md#list-view) nella console Sites.

* Nella [timeline](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* Nel menu [Informazioni pagina](/help/sites-authoring/author-environment-tools.md#page-information) durante la modifica di una pagina

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
