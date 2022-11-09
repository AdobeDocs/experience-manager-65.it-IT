---
title: Applicazione dei flussi di lavoro alle pagine
seo-title: Applying Workflows to Pages
description: Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro..
seo-description: When authoring, you can invoke workflows to take action on your pages; it is also possible to apply more than one workflow..
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 99%

---

# Applicazione dei flussi di lavoro alle pagine{#applying-workflows-to-pages}

Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro.

Quando si applica il flusso di lavoro, è necessario specificare le seguenti informazioni:

* Flusso di lavoro da applicare.
Puoi utilizzare qualsiasi flusso di lavoro a cui hai accesso, secondo quanto assegnato dall’amministratore AEM.
* Facoltativamente, un titolo che aiuti a identificare l&#39;istanza di flusso di lavoro nella casella in entrata di un utente.
* Il payload del flusso di lavoro; può trattarsi di una o più pagine.

Puoi avviare i flussi di lavoro a partire da:

* [La console Sites](#starting-a-workflow-from-the-sites-console);
* [durante la modifica di una pagina, da Informazioni pagina](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Consulta anche:
>
>* [Come applicare i flussi di lavoro alle risorse DAM](/help/assets/assets-workflow.md).
>* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-authoring/projects-with-workflows.md).
>


>[!NOTE]
>
>Gli amministratori AEM possono [avviare i flussi di lavoro attraverso molti altri metodi](/help/sites-administering/workflows-starting.md).

## Avviare un flusso di lavoro dalla console Sites {#starting-a-workflow-from-the-sites-console}

Puoi avviare un flusso di lavoro in uno dei due modi seguenti:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

In entrambi i casi, è necessario:

* [Specificare i Dettagli del flusso di lavoro nella Procedura guidata Crea flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avviare un flusso di lavoro dalla barra degli strumenti di Sites {#starting-a-workflow-from-the-sites-toolbar}

Puoi avviare un flusso di lavoro dalla barra degli strumenti della console **Sites**:

1. Vai alla pagina richiesta e selezionala.

1. Dall’opzione **Crea** nella barra degli strumenti è ora possibile selezionare **Flusso di lavoro**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. La procedura guidata **Crea flusso di lavoro** consente di [specificare i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avviare un flusso di lavoro dalla Timeline {#starting-a-workflow-from-the-timeline}

Puoi avviare un flusso di lavoro da applicare alla risorsa selezionata dalla **Timeline** 

1. [Seleziona la risorsa](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) e apri [Timeline](/help/sites-authoring/basic-handling.md#timeline) (o apri Timeline, quindi seleziona la risorsa).
1. Puoi utilizzare la freccia dal campo commento per visualizzare **Avvia flusso di lavoro**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. La procedura guidata **Crea flusso di lavoro** consente di [specificare i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Specificazione dei Dettagli del flusso di lavoro nella procedura guidata Crea flusso di lavoro {#specifying-workflow-details-in-the-create-workflow-wizard}

La procedura guidata **Crea flusso di lavoro** consente di selezionare il flusso di lavoro e specificare i dettagli necessari.

Dopo aver aperto la procedura guidata **Crea flusso di lavoro** in uno dei due modi seguenti:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

Puoi specificare i dettagli:

1. Nel passaggio **Proprietà**, che definisce le opzioni di base del flusso di lavoro:

   * **modello flusso di lavoro**;
   * **titolo flusso di lavoro**.

      * Per questa istanza, puoi specificare un titolo che aiuti a identificarla in una fase successiva.

   A seconda del modello di flusso di lavoro, sono disponibili anche le seguenti opzioni. Queste consentono di conservare il pacchetto creato come payload, dopo il completamento del flusso di lavoro.

   * **Mantieni pacchetto flusso di lavoro**
   * **Titolo pacchetto**

      * Puoi specificare un titolo da attribuire al pacchetto, per facilitarne l&#39;identificazione.
   >[!NOTE]
   >
   >L’opzione **Mantieni pacchetto flusso di lavoro** è disponibile quando il flusso di lavoro è stato configurato per Supporto risorse multiple e sono state selezionate più risorse.[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   Una volta completato, premere su **Successivo** per continuare.

   ![wf-52](assets/wf-52.png)

1. Al passaggio **Ambito** puoi selezionare:

   * **Aggiungi contenuto**, per aprire il [browser percorsi](/help/sites-authoring/author-environment-tools.md#path-browser) e selezionare altre risorse; una volta nel browser, tocca o fai clic su **Seleziona** per aggiungere contenuti all’istanza di flusso di lavoro.

   * Una risorsa esistente per visualizzare le seguenti azioni:

      * **Includi elementi figlio** per specificare gli elementi secondari di tale risorsa che verranno inclusi nel flusso di lavoro.
Una finestra di dialogo si apre per permettere di perfezionare la selezione includendo:

         * Solo gli elementi figli di primo livello.
         * Solo pagine modificate.
         * Solo pagine già pubblicate.

         Tutti gli elementi secondari specificati vengono aggiunti all&#39;elenco di risorse al quale verrà applicato il flusso di lavoro.

      * **Rimuovi selezione** per rimuovere una determinata risorsa dal flusso di lavoro.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Se aggiungi ulteriori risorse, puoi selezionare **Indietro** per regolare l’impostazione di **Mantieni pacchetto flusso di lavoro** nel passaggio **Proprietà**.

1. Usa **Crea** per chiudere la procedura guidata e creare l’istanza di flusso di lavoro. Una notifica appare nella console Sites.

## Avviare un flusso di lavoro dall&#39;editor pagina {#starting-a-workflow-from-the-page-editor}

Quando modifichi una pagina, puoi selezionare **Informazioni pagina** nella barra degli strumenti. Il menu a discesa contiene l&#39;opzione **Avvia nel flusso di lavoro**. Questa apre una finestra di dialogo nella quale puoi specificare il flusso di lavoro obbligatorio, insieme a un titolo richiesto:

![wf-54](assets/wf-54.png)
