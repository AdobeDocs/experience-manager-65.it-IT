---
title: Integrazione Progetto creativo e PIM
seo-title: Integrazione Progetto creativo e PIM
description: La funzionalità Progetto creativo migliora l’intero flusso di lavoro per servizio fotografico inclusa la generazione della richiesta di servizio fotografico, il caricamento di un servizio fotografico, la collaborazione su un servizio fotografico e la creazione di pacchetti per le risorse approvate.
seo-description: La funzionalità Progetto creativo migliora l’intero flusso di lavoro per servizio fotografico inclusa la generazione della richiesta di servizio fotografico, il caricamento di un servizio fotografico, la collaborazione su un servizio fotografico e la creazione di pacchetti per le risorse approvate.
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '3013'
ht-degree: 69%

---


# Integrazione Progetto creativo e PIM{#creative-project-and-pim-integration}

Gli esperti di marketing o i professionisti del settore creativo possono usare gli strumenti Creative Project in Adobe Experience Manager (AEM) per gestire la fotografia dei prodotti eCommerce e i relativi processi creativi all’interno dell’organizzazione.

In particolare, puoi utilizzare la funzionalità Progetto creativo per semplificare le seguenti attività nel flusso di lavoro per il servizio fotografico:

* Generazione di una richiesta di servizio fotografico
* Caricamento di un servizio fotografico
* Collaborazione su un servizio fotografico
* Creazione di pacchetti di risorse approvate

>[!NOTE]
>
>Consulta [Ruoli utente del progetto](/help/sites-authoring/projects.md#user-roles-in-a-project) per informazioni sull’assegnazione di ruoli utenti e flussi di lavoro a determinati tipi di utenti.

## Flussi di lavoro per servizio fotografico per prodotti  {#exploring-product-photo-shoot-workflows}

La funzionalità Progetto creativo offre vari modelli di progetto per soddisfare vari requisiti di progetto. Il modello di **Progetto servizio fotografico per prodotto** è disponibile pronto all’uso. Questo modello offre flussi di lavoro per il servizio fotografico che consentono di avviare e gestire le richieste di servizio fotografico per i prodotti. Include anche una serie di attività che consentono di ottenere le immagini digitali per i prodotti tramite processi di revisione e approvazione appropriati.

Il modello include i seguenti flussi di lavoro:

* **Servizio fotografico per prodotto (integrazione Commerce)**: questo flusso di lavoro sfrutta l’integrazione Commerce con il sistema di gestione delle informazioni dei prodotti (PIM) per generare automaticamente un elenco di foto per i prodotti selezionati (gerarchia). Puoi visualizzare i dati dei prodotti come parte dei metadati della risorsa al completamento del flusso di lavoro.
* **Servizio fotografico per prodotto**: questo flusso di lavoro consente di fornire un elenco di foto invece di dipendere dall’integrazione Commerce. Associa le immagini caricate a un file CSV nella cartella delle risorse del progetto.

>[!NOTE]
>
>Il file CSV che viene caricato in Carica attività elenco di foto del flusso di lavoro Servizio fotografico per prodotto deve avere il nome shotlist.csv.

## Creare un progetto Servizio fotografico per prodotto {#create-a-product-photo-shoot-project}

1. In the **Projects** console, tap/click **Create** and then choose **Create Project** from the list.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. Nella pagina **Crea progetto**, seleziona il modello del progetto di servizio fotografico e tocca o fai clic su **Avanti**.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Inserisci i dettagli del progetto, quali il titolo, la descrizione e la data di scadenza. Aggiungi utenti e assegna loro i vari ruoli. Puoi anche aggiungere una miniatura per il progetto.

   ![chlimage_1-134](assets/chlimage_1-134a.png)

1. Tocca o fai clic su **Crea**. La creazione del progetto è indicata da un messaggio di conferma.
1. Tap/click **Done** to return to the **Projects** console. Alternatively, tap/click **Open** to view the assets within the photoshoot project.

## Avviare il lavoro di ripresa in un progetto Servizio fotografico per prodotto {#starting-work-in-a-product-photo-shoot-project}

Per avviare una richiesta di servizio fotografico, tocca o fai clic su un progetto, poi tocca o fai clic su **Aggiungi lavoro** nella pagina dei dettagli del progetto per avviare un flusso di lavoro.

![chlimage_1-135](assets/chlimage_1-135a.png)

Un progetto Servizio fotografico per prodotto include i seguenti flussi di lavoro preconfigurati:

* Flusso di lavoro Servizio fotografico per prodotto (integrazione Commerce)
* Flusso di lavoro Servizio fotografico per prodotto

Utilizza il flusso di lavoro Servizio fotografico per prodotto (integrazione Commerce) per associare le risorse immagini con i prodotti in AEM. Questo flusso di lavoro, sfrutta l’Integrazione Commerce per collegare le immagini approvate ai dati di prodotto esistenti in */etc/commerce*.

Il flusso di lavoro Product Photo Shoot (Integrazione Commerce) include le seguenti attività:

* Crea elenco di foto
* Carica servizio fotografico
* Ritocca servizio fotografico
* Rivedi e approva
* Sposta ad attività produzione

Se le informazioni sul prodotto non sono disponibili in AEM, utilizza il flusso di lavoro Servizio fotografico per prodotto per associare le risorse immagini ai prodotti in base ai dettagli caricati nel file CSV. Il file CSV deve contenere le informazioni di base sul prodotto, ad esempio ID, categoria e descrizione. Il flusso di lavoro recupera le risorse approvate per i prodotti.

Questo flusso di lavoro comprende le seguenti attività:

* Carica elenco di foto
* Carica servizio fotografico
* Ritocca servizio fotografico
* Rivedi e approva
* Sposta ad attività produzione

Puoi personalizzare questo flusso di lavoro utilizzando l’opzione di configurazione del flusso di lavoro.

Entrambi questi flussi di lavoro includono i passaggi per collegare i prodotti con le rispettive risorse approvate. Ogni flusso di lavoro comprende i seguenti passaggi:

* Configurazione flusso di lavoro: descrive le opzioni per personalizzare il flusso di lavoro
* Avvio di un flusso di lavoro del progetto: illustra come avviare un Servizio fotografico per prodotto
* Dettagli attività del flusso di lavoro: fornisce i dettagli delle attività disponibili nel flusso di lavoro

## Monitoraggio dello stato di avanzamento del progetto {#tracking-project-progress}

Puoi controllare lo stato di un progetto selezionando le attività attive o completate di un progetto.

Utilizza quanto segue per controllare l’avanzamento di un progetto:

* **Scheda Attività**

* **Elenco delle attività**

La scheda Attività mostra l&#39;avanzamento generale del progetto. Viene mostrata nella pagina Dettagli del progetto solo se il progetto contiene attività correlate. La scheda Attività mostra lo stato di completamento corrente del progetto in base al numero di attività completate. Non include le attività future.

La scheda Attività offre i seguenti dettagli:

* Percentuale di attività in corso
* Percentuale di attività completate

![chlimage_1-136](assets/chlimage_1-136a.png)

L’elenco delle attività attualmente fornisce informazioni dettagliate sull’attività attiva del flusso di lavoro per il progetto. Per visualizzare l’elenco, tocca o fai clic sulla scheda Attività. L’elenco delle attività visualizza anche i metadati, quali data iniziale, data di scadenza, assegnatario, priorità e stato dell’attività.

![chlimage_1-137](assets/chlimage_1-137a.png)

## Configurazione del flusso di lavoro {#workflow-configuration}

Questa attività include l’assegnazione di passaggi del flusso di lavoro agli utenti in base ai relativi ruoli.

Per configurare il flusso di lavoro **Servizio fotografico per prodotto**:

1. Navigate to **Tools** > **Workflows**, and then tap the **Models** tile to open the **Workflow Models** page.
1. Select the **Product Photo Shoot** workflow, and the tap the **Edit** icon from the toolbar to open it in edit mode.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

1. In the **Product Photo Shoot Workflow** page, open a project task. Ad esempio, apri **Carica elenco di foto**.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

1. Fai clic sulla scheda **Attività** per configurare le seguenti opzioni:

   * Nome dell’attività
   * Utente predefinito (ruolo) che riceve l’attività
   * Priorità predefinita dell’attività, che verrà visualizzata nell’elenco delle attività dell’utente
   * Descrizione da visualizzare quando il relativo assegnatario apre l’attività
   * Data di scadenza per l’attività, calcolata dal momento in cui si avvia l’attività

1. Fai clic su **OK** per salvare le impostazioni.

   Analogamente, puoi configurare le seguenti attività per il flusso di lavoro **Servizio fotografico per prodotto**:

   * Carica servizio fotografico
   * Ritocca servizio fotografico
   * Revisiona servizio fotografico
   * Sposta a produzione

   Perform a similar procedure to configure the tasks in the **Product Photo Shoot (Commerce Integration) workflow**.

Questa sezione descrive come integrare la gestione delle informazioni sul prodotto con il progetto creativo.

## Avviare un flusso di lavoro di progetto {#starting-a-project-workflow}

1. Navigate to a Product Photo Shoot project, and tap/click the **Add Work** icon on the **Workflows** card.
1. Seleziona la scheda del flusso di lavoro **Servizio fotografico per prodotto (integrazione Commerce)** per avviare il flusso di lavoro Servizio fotografico per prodotto (integrazione Commerce). If the product information isn&#39;t available under /etc/commerce, select the **Product Photo Shoot** workflow and start the Product Photo Shoot workflow.

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Tocca o fai clic su **Avanti** per avviare il flusso di lavoro nel progetto.
1. Immetti i dettagli del flusso di lavoro nella pagina successiva.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   Fai clic su **Invia** per avviare il flusso di lavoro del servizio fotografico. Viene visualizzata la pagina dei dettagli per il progetto del servizio fotografico.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

### Dettagli delle attività del flusso di lavoro {#workflow-tasks-details}

Il flusso di lavoro per il servizio fotografico include diverse attività. Ogni attività viene assegnata a un gruppo utente in base alla configurazione definita per l’attività.

#### Crea attività elenco di foto {#create-shot-list-task}

L’attività **Crea elenco di foto** consente al proprietario del progetto di selezionare i prodotti per i quali sono necessarie le immagini. In base all’opzione selezionata dall’utente, viene generato un file CSV contenente le informazioni di base sul prodotto.

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the task item in the workflow.

   ![chlimage_1-143](assets/chlimage_1-143a.png)

1. Select the **Create Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. Esamina i dettagli dell’attività e quindi tocca o fai clic sul pulsante **Crea elenco di foto**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Seleziona i prodotti per i quali esistono dati di prodotto senza immagini associate.

   ![chlimage_1-146](assets/chlimage_1-146a.png)

1. Tap/click the **Add To Shotlist** icon to create a CSV file that contains a list of all such products. Un messaggio conferma che l’elenco di foto è stato creato per i prodotti selezionati. Fai clic su **Chiudi** per completare il flusso di lavoro.
1. Dopo aver creato un elenco di foto, compare il collegamento **Visualizza elenco di foto**. To add more products to the shot list, tap/click **Add to Shot List**. In questo caso, i dati vengono associati all’elenco di foto inizialmente creato.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

1. Tocca o fai clic su **Visualizza elenco di foto** per visualizzare il nuovo elenco di foto.

   ![chlimage_1-148](assets/chlimage_1-148a.png)

   Per modificare i dati esistenti o aggiungere nuovi dati, tocca o fai clic su **Modifica** sulla barra degli strumenti. Only the **Product **and **Description** fields are editable.

   ![chlimage_1-149](assets/chlimage_1-149a.png)

   After you update the file, tap/click **Save** on toolbar to save the file.

1. After adding the products, tap/click the **Complete** icon on the **Create Shot List **task details page to mark the task as completed. Puoi aggiungere un commento opzionale.

   Il completamento dell’attività introduce le seguenti modifiche all’interno del progetto:

   * Le risorse corrispondenti alla gerarchia del prodotto vengono create in una cartella con lo stesso nome del titolo del flusso di lavoro.
   * I metadati per le risorse diventano modificabili mediante la console delle risorse, anche prima che il fotografo inserisca le immagini.
   * Viene creata una cartella Servizio fotografico dove vengono memorizzate le immagini che fornisce il fotografo. La cartella Servizio fotografico contiene delle sottocartelle per ogni voce di prodotto nell’Elenco di foto.

   Per il flusso di lavoro del Servizio fotografico per prodotto (senza l’integrazione Commerce), la prima attività è Carica elenco di foto. Tocca o fai clic su **Carica elenco di foto** per caricare un file **shotlist.csv**. Il file CSV deve contenere l’ID del prodotto. Gli altri campi sono facoltativi. Puoi utilizzarli per associare le risorse ai prodotti.

### Carica attività elenco di foto {#upload-shot-list-task}

Questa attività è parte del flusso di lavoro Servizio fotografico per prodotto. Esegui l’attività se in AEM non sono disponibili le informazioni sui prodotti. In questo caso carichi un elenco di prodotti in un file CSV per i cui sono richieste le risorse immagini. In base ai dettagli nel file CSV, potete mappare le risorse di immagine con i prodotti.

Scarica un file CSV di esempio, tramite il collegamento **Visualizza elenco di foto** sotto la scheda del progetto nella procedura precedente. Esamina il file di esempio per conoscere il contenuto tipico di un file CSV.

L’elenco dei prodotti o il file CSV possono contenere campi come **Categoria, Prodotto, ID, Descrizione** e **Percorso**. Il campo **ID** è obbligatorio e contiene l’ID del prodotto. Gli altri campi sono facoltativi.

Un prodotto può appartenere a una particolare categoria. La categoria del prodotto può essere elencata nel CSV nella colonna **Categoria**. Il campo **Prodotto** contiene il nome del prodotto. Nel campo **Descrizione** immetti la descrizione o istruzioni per il fotografo.

>[!NOTE]
>
>The name of images to be uploaded should start with &quot;**&lt;ProductId>_&quot;** where Product ID is referenced from the **Id** field in the *shotlist.csv* file. For example, for a product in the shot list with **Id 397122**, you can upload files with names **397122_highcontrast.jpg**, **397122_lowlight.png**, and so on.

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the list of tasks in the workflow.
1. Select the **Upload Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-150](assets/chlimage_1-150a.png)

1. Review the task details and then tap/click the **Upload Shot List** button.

   ![chlimage_1-151](assets/chlimage_1-151a.png)

1. Tap/click the **Upload Shot List** button to upload the CSV file with filename shotlist.csv. Il flusso di lavoro riconosce questo file come sorgente da utilizzare per estrarre i dati dei prodotti per l’attività successiva.
1. Carica un file CSV contenente le informazioni sui prodotti nel formato corretto. The **View Uploaded Assets** link appears under the card after the CSV file is uploaded.

   ![chlimage_1-152](assets/chlimage_1-152a.png)

   Click the **Complete** icon to complete the task.

1. Tap/click the **Complete** icon to complete the task.

### Attività Carica servizio fotografico {#upload-photo-shoot-task}

If you are an Editor, you can upload shots for the products listed in the **shotlist.csv** file that is created or uploaded in the previous task.

The name of images to be uploaded should begin with **&quot;&lt;productId>_&quot;** where Product ID is referenced from the **Id** field in the **shotlist.csv** file. Ad esempio, per un prodotto con **ID 397122** nell’elenco di foto, puoi caricare i file **397122_highcontrast.jpg**,**397122_lowlight.png** e così via.

Puoi caricare direttamente le immagini o caricare un file zip contenente le immagini. Sulla base dei loro nomi, le immagini vengono inserite nelle rispettive cartelle dei prodotti all’interno della cartella **Servizio fotografico**.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Upload Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-153](assets/chlimage_1-153a.png)

1. Tap/click **Upload Photo Shoot** and upload the photo shoot images.
1. Tocca o fai clic sull’icona **Completato** sulla barra degli strumenti per completare l’attività.

### Attività Ritocca servizio fotografico {#retouch-photo-shoot-task}

Se disponi delle autorizzazioni di modifica, esegui l’attività Ritocca servizio fotografico per modificare le immagini caricate nella cartella Servizio fotografico.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Retouch Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-154](assets/chlimage_1-154a.png)

1. Tap/click the **View Uploaded Assets** link in the **Retouch Photo Shoot** page to browse the uploaded images.

   ![chlimage_1-155](assets/chlimage_1-155a.png)

   Se necessario, modifica le immagini con l’ausilio di un’applicazione Adobe Creative Cloud.

   ![chlimage_1-156](assets/chlimage_1-156a.png)

1. Tocca o fai clic sull’icona **Completato** sulla barra degli strumenti per completare l’attività.

### Attività Rivedi e approva {#review-and-approve-task}

In questa attività, esamina le immagini del servizio fotografico caricate da un fotografo e contrassegnale come approvate per l’uso.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Review &amp; Approve** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-157](assets/chlimage_1-157a.png)

1. In the **Review &amp; Approve** page, assign the review task to role, for example Reviewers, and then tap/click **Review **to start reviewing the uploaded product images.

   ![chlimage_1-158](assets/chlimage_1-158a.png)

1. Seleziona un’immagine del prodotto e tocca o fai clic sull’icona Approvato nella barra degli strumenti per contrassegnarlo come approvato.

   ![chlimage_1-159](assets/chlimage_1-159a.png)

   Una volta approvata un’immagine, viene visualizzato un banner di approvazione.

   >[!NOTE]
   È possibile omettere alcuni prodotti senza alcuna immagine. In seguito, puoi rivisitare l’attività e contrassegnarla come completata.

1. Tocca o fai clic su **Completato**. Le immagini approvate sono collegate alle risorse vuote che sono state create.

Puoi accedere alle risorse del progetto tramite l’interfaccia utente di Assets e verificare le immagini approvate.

Tocca o fai clic sul livello successivo per visualizzare i prodotti in base alla gerarchia di dati di prodotto.

I collaboratori del progetto creativo approvano le risorse con il prodotto a cui si fa riferimento. I metadati delle risorse vengono aggiornati con il riferimento del prodotto e le informazioni di base nella scheda **Dati prodotto** per le proprietà delle risorse vengono visualizzate nella sezione Metadati delle risorse di AEM.

>[!NOTE]
Nel flusso di lavoro per il servizio fotografico per prodotto (senza l’integrazione Commerce), le immagini non approvate non sono associate ai prodotti.

### Sposta ad attività produzione {#move-to-production-task}

Questa attività consente di spostare le risorse approvate nella cartella per la produzione per renderle disponibili per l’uso.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Move to Production** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-160](assets/chlimage_1-160a.png)

1. Per visualizzare le risorse approvate per il servizio fotografico prima di spostarle nella cartella per la produzione, fai clic sul collegamento **Visualizza risorse approvate** sotto la miniatura del progetto sulla pagina dell’attività **Sposta a produzione**.

   ![chlimage_1-161](assets/chlimage_1-161a.png)

1. Enter the path of the production-ready folder in the **Move To** field.

   ![chlimage_1-162](assets/chlimage_1-162a.png)

   Tap/click **Move to Production**. Chiudi il messaggio di conferma. Le risorse vengono spostate nel percorso indicato e viene creato automaticamente un Set 360 gradi per le risorse approvate per ogni prodotto in base alla gerarchia delle cartelle.

1. Tocca o fai clic sull’icona **Completato** sulla barra degli strumenti. Il flusso di lavoro è completo quando l’ultimo passaggio è indicato come “completato”.

## Visualizzazione dei metadati risorsa DAM {#viewing-dam-asset-metadata}

Dopo che avrai approvato, le risorse vengono collegate ai prodotti corrispondenti. La [pagina delle proprietà](/help/assets/manage-assets.md#editing-properties) delle risorse approvate ora dispone di una scheda aggiuntiva, **Dati prodotto** (collegata alle informazioni sul prodotto). Questa scheda consente di visualizzare i dettagli del prodotto, il numero SKU e altri dettagli relativi ai prodotti che collegano la risorsa. Tocca o fa clic sull’icona **Modifica** per aggiornare una proprietà di risorsa. Le informazioni relative al prodotto restano di sola lettura.

Tocca o fai clic sul collegamento che appare per passare alla relativa pagina di dettagli del prodotto nella console del prodotto al quale la risorsa è associato.

## Personalizzare i flussi di lavoro Servizio fotografico di un progetto {#customizing-the-project-photo-shoot-workflows}

Puoi personalizzare i flussi di lavoro Servizio fotografico per il progetto in base ai requisiti. È un’attività facoltativa basata sui ruoli, che consente di impostare il valore di una variabile all’interno del progetto. Successivamente, puoi utilizzare il valore configurato per arrivare a una decisione.

1. Click/tap the AEM logo, and then navigate to **Tools** > **Workflow** > **Models** to open the Workflow Models page.
1. Seleziona il flusso di lavoro **Servizio fotografico per prodotto (integrazione Commerce)** o **Servizio fotografico per prodotto** e fai clic su **Modifica** sulla barra degli strumenti per aprire il flusso di lavoro in modalità di modifica.
1. Apri le attività **Progetti** nella barra laterale e trascina il passaggio **Crea attività progetto basata su ruolo** nel flusso di lavoro.

   ![chlimage_1-163](assets/chlimage_1-163a.png)

1. Open the **Role Based Task** step.
1. Nella scheda **Attività**, immetti un nome per l’attività da visualizzare nell’elenco delle **Attività**. È inoltre possibile assegnare l&#39;attività a un ruolo, impostare la priorità predefinita, fornire una descrizione e specificare l&#39;ora in cui l&#39;attività è scaduta.

   ![chlimage_1-164](assets/chlimage_1-164a.png)

1. Nella scheda **Indirizzamento**, specifica le azioni per l’attività. Per aggiungere più azioni, toccate o fate clic sul collegamento **Add Item **link.

   ![chlimage_1-165](assets/chlimage_1-165a.png)

1. After adding the options click **OK** to add the changes to the step.

   >[!NOTE]
   Tapping/clicking **OK** does not save the changes in the workflow. To save changes in the workflow, tap/click **Save**.

1. Open the **Workflow** tasks from side kick, and add a **Goto** task.
1. Apri l’attività **Passaggio** e tocca o fai clic sulla scheda **Processo**.
1. Specifica il codice seguente nel riquadro **Script**:

```
   function check() {

   if (workflowData.getMetaDataMap().get("lastTaskAction","") == "Reject All") {

   return true

   }

   // set copywriter user in metadata

   var previousId = workflowData.getMetaDataMap().get("lastTaskCompletedBy", "");

   workflowData.getMetaDataMap().put("copywriter", previousId);

   return false;

   }
```

>[!NOTE]
For details around scripting in workflow steps, see [Defining a Rule for an OR Split](/help/sites-developing/workflows-models.md).

![chlimage_1-166](assets/chlimage_1-166a.png)

1. Tap/click **OK**.

1. Tap/click **Save** to save the workflow.

   ![chlimage_1-167](assets/chlimage_1-167a.png)

1. A new Project owner acceptance task now comes up after the [Move to Production task](#move-to-production-task) is completed and is assigned to the owner.

   L’utente con il ruolo di Proprietario può completare l’attività e selezionare un’azione (dall’elenco delle azioni aggiunte nelle configurazioni delle fasi del flusso di lavoro) dall’elenco nel popup dei commenti.

   ![chlimage_1-168](assets/chlimage_1-168a.png)

   Seleziona l’opzione appropriata e fai clic su **Completato** per eseguire il **Passaggio** nel flusso di lavoro.

>[!NOTE]
When you start a server, the Project task list servlet caches the mappings between task types and URLs defined under `/libs/cq/core/content/projects/tasktypes`. You can then perform the usual overlay and add custom task types by placing them under `/apps/cq/core/content/projects/tasktypes`.

