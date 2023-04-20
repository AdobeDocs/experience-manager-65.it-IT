---
title: Applicare flussi di lavoro alle pagine di contenuto
description: Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro.
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 53%

---

# Applicazione dei flussi di lavoro alle pagine{#applying-workflows-to-pages}

Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro.

Quando applichi il flusso di lavoro, specifica le seguenti informazioni:

* Flusso di lavoro da applicare.
Puoi utilizzare qualsiasi flusso di lavoro a cui hai accesso, secondo quanto assegnato dall’amministratore AEM.
* Facoltativamente, un titolo che aiuta a identificare l’istanza del flusso di lavoro nella casella in entrata di un utente.
* Il payload del flusso di lavoro; può essere una o più pagine.

I flussi di lavoro possono essere avviati da:

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
>AEM amministratori possono [avvia flussi di lavoro utilizzando diversi altri metodi](/help/sites-administering/workflows-starting.md).

## Avvio di un flusso di lavoro dalla console Sites {#starting-a-workflow-from-the-sites-console}

Puoi avviare un flusso di lavoro da:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

In entrambi i casi è necessario:

* [Specificare i dettagli del flusso di lavoro nella Creazione guidata flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avvio di un flusso di lavoro dalla barra degli strumenti Sites {#starting-a-workflow-from-the-sites-toolbar}

Puoi avviare un flusso di lavoro dalla barra degli strumenti della console **Sites**:

1. Vai alla pagina richiesta e selezionala.

1. Dall’opzione **Crea** nella barra degli strumenti è ora possibile selezionare **Flusso di lavoro**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. La **Crea flusso di lavoro** la procedura guidata ti aiuterà [specifica i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avvio di un flusso di lavoro dalla timeline {#starting-a-workflow-from-the-timeline}

Da **Timeline** puoi avviare un flusso di lavoro da applicare alla risorsa selezionata.

1. [Seleziona la risorsa](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) e apri [Timeline](/help/sites-authoring/basic-handling.md#timeline) (o apri Timeline, quindi seleziona la risorsa).
1. Puoi utilizzare la freccia dal campo commento per visualizzare **Avvia flusso di lavoro**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. La **Crea flusso di lavoro** la procedura guidata ti aiuterà [specifica i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Specifica dei dettagli del flusso di lavoro nella Creazione guidata flusso di lavoro {#specifying-workflow-details-in-the-create-workflow-wizard}

La **Crea flusso di lavoro** la procedura guidata consente di selezionare il flusso di lavoro e specificare i dettagli richiesti.

Dopo aver aperto la **Crea flusso di lavoro** procedura guidata da:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

Puoi specificare i dettagli:

1. In **Proprietà** le opzioni di base del flusso di lavoro sono definite:

   * **Modello flusso di lavoro**
   * **Titolo flusso di lavoro**

      * Puoi specificare un titolo per questa istanza, in modo da identificarla in un secondo momento.

   A seconda del modello di flusso di lavoro, sono disponibili anche le seguenti opzioni. Questi consentono di mantenere il pacchetto creato come payload al termine del flusso di lavoro.

   * **Mantieni pacchetto flusso di lavoro**
   * **Titolo pacchetto**

      * Puoi specificare un titolo per il pacchetto, per facilitarne l’identificazione.
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

         Tutti gli elementi secondari specificati vengono aggiunti all’elenco delle risorse a cui verrà applicato il flusso di lavoro.

      * **Rimuovi selezione** per rimuovere la risorsa dal flusso di lavoro.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Se aggiungi ulteriori risorse, puoi selezionare **Indietro** per regolare l’impostazione di **Mantieni pacchetto flusso di lavoro** nel passaggio **Proprietà**.

1. Usa **Crea** per chiudere la procedura guidata e creare l’istanza di flusso di lavoro. Nella console Sites viene visualizzata una notifica.

## Avvio di un flusso di lavoro dall’Editor pagina {#starting-a-workflow-from-the-page-editor}

Durante la modifica di una pagina è possibile selezionare **Informazioni pagina** dalla barra degli strumenti. L’opzione del menu a discesa **Avvia nel flusso di lavoro**. Questa apre una finestra di dialogo nella quale puoi specificare il flusso di lavoro obbligatorio, insieme a un titolo richiesto:

![wf-54](assets/wf-54.png)
