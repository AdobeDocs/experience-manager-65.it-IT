---
title: Elaborazione delle risorse tramite flussi di lavoro
description: Elaborazione delle risorse per convertire i formati, creare rappresentazioni, gestire le risorse, convalidare le risorse ed eseguire flussi di lavoro.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---


# Elabora risorse digitali {#process-assets}

[!DNL Adobe Experience Manager Assets] consente di lavorare sulle risorse digitali in molti modi per consentire una solida elaborazione delle risorse. Puoi utilizzare i metodi di elaborazione predefiniti o personalizzati per garantire il completamento completo dei processi aziendali, la conformità e i controlli, l&#39;individuazione e la distribuzione nonché l&#39;integrità di base delle risorse digitali. Potete eseguire le attività di gestione delle risorse ottenendo le dimensioni e la personalizzazione richieste.

## Comprendere i flussi di lavoro {#understand-workflows}

Per l’elaborazione delle risorse, [!DNL Experience Manager] utilizza i flussi di lavoro. I flussi di lavoro consentono di automatizzare la logica o le attività aziendali. Per impostazione predefinita vengono forniti passaggi granulari per eseguire attività specifiche e gli sviluppatori possono creare i propri passi personalizzati. Questi passaggi possono essere combinati in un ordine logico per creare flussi di lavoro. Ad esempio, un flusso di lavoro può applicare una filigrana alle immagini caricate in base a criteri specifici, ad esempio la cartella in cui viene caricata, la risoluzione dell’immagine e così via. Un altro esempio è rappresentato da un flusso di lavoro configurato per inserire filigrane e aggiungere contemporaneamente metadati, creare rappresentazioni, aggiungere tag avanzati e pubblicare contenuti in un archivio dati.

## Flussi di lavoro predefiniti disponibili in [!DNL Experience Manager] {#default-workflows}

Per impostazione predefinita, tutte le risorse caricate vengono elaborate utilizzando il flusso di lavoro Aggiorna risorsa  DAM. Il flusso di lavoro viene eseguito per ciascuna risorsa caricata ed esegue attività di base per la gestione delle risorse, come generazione di rappresentazioni, remix di metadati, estrazione di pagina, estrazione di contenuti multimediali e transcodifica.

Per visualizzare i vari modelli di workflow disponibili per impostazione predefinita, vedi **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]** in [!DNL Experience Manager].

![Alcuni dei flussi di lavoro predefiniti](assets/aem-default-workflows.png)

*Figura: Alcuni dei flussi di lavoro predefiniti disponibili in [!DNL Experience Manager].*

## Applicazione di flussi di lavoro per elaborare le risorse {#applying-workflows-to-assets}

L’applicazione dei flussi di lavoro alle risorse digitali è la stessa utilizzata per le pagine di siti Web. Per una guida completa su come creare e utilizzare i flussi di lavoro, consulta Flussi di lavoro [iniziali](/help/sites-authoring/workflows-participating.md).

Usate i flussi di lavoro nelle risorse digitali per attivare la risorsa o creare filigrane. Molti dei flussi di lavoro per le risorse vengono automaticamente attivati. Ad esempio, il flusso di lavoro che crea automaticamente una rappresentazione dopo la modifica di un’immagine viene automaticamente attivato.

>[!NOTE]
>
>Se un flusso di lavoro disponibile nell’interfaccia classica non è disponibile nell’interfaccia touch, ad esempio [!UICONTROL Richiesta di attivazione] e [!UICONTROL Richiesta di disattivazione], consultate [Realizzare modelli](/help/sites-developing/workflows-models.md#classic2touchui)di flusso di lavoro.

## Applicazione di un flusso di lavoro a una risorsa {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Per applicare un flusso di lavoro a una risorsa, effettuate le seguenti operazioni:

1. Andate alla posizione della risorsa per la quale desiderate avviare un flusso di lavoro e fate clic sulla risorsa per aprire la pagina della risorsa. Selezionate **[!UICONTROL Timeline]** dal menu per visualizzare la timeline.

   ![timeline-1](assets/timeline.png)

1. Fate clic su **[!UICONTROL Azioni]** in basso per aprire l’elenco delle azioni disponibili per la risorsa.

1. Fare clic su **[!UICONTROL Avvia flusso di lavoro]** dall&#39;elenco.

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

1. (Facoltativo) Specificate un titolo per il flusso di lavoro che può essere utilizzato per fare riferimento all&#39;istanza del flusso di lavoro.

   ![selezionate il flusso di lavoro, fornite un titolo e fate clic su Avvia](assets/start-workflow.png)

1. Fate clic su **[!UICONTROL Avvia]** , quindi fate clic su **[!UICONTROL Procedi]**. Ciascun passaggio del flusso di lavoro viene visualizzato nella timeline come un evento.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Applicazione di un flusso di lavoro a più risorse {#applying-a-workflow-to-multiple-assets}

1. Dalla [!DNL Assets] console, individuate la posizione delle risorse per le quali desiderate avviare un flusso di lavoro e selezionate le risorse. Selezionate **[!UICONTROL Timeline]** dal menu per visualizzare la timeline.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Fate clic su **[!UICONTROL Azioni]** ![con la freccia verso l’alto](assets/do-not-localize/chevron-up-icon.png) in basso.
1. Fate clic su **[!UICONTROL Avvia flusso di lavoro]**. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![avvia flusso di lavoro](assets/start-workflow.png)

1. (Facoltativo) Specificate un titolo per il flusso di lavoro, che può essere utilizzato per fare riferimento all’istanza del flusso di lavoro.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Avvia]**, quindi su **[!UICONTROL Conferma]**. Il flusso di lavoro viene eseguito su tutte le risorse selezionate.

## Applicazione di un flusso di lavoro a più cartelle {#applying-a-workflow-to-multiple-folders}

La procedura per applicare un flusso di lavoro a più cartelle è simile a quella per applicare un flusso di lavoro a più risorse. Selezionate le cartelle nell’ [!DNL Assets] interfaccia ed eseguite i passaggi da 2 a 7 della procedura per [applicare un flusso di lavoro a più risorse](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Applicazione di un flusso di lavoro a una raccolta {#applying-a-workflow-to-a-collection}

Consultate [Applicare un flusso di lavoro a una raccolta](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Avvio automatico di un flusso di lavoro per elaborare le risorse in modo condizionale {#auto-execute-workflow-on-some-assets}

Gli amministratori possono configurare il flusso di lavoro per eseguire ed elaborare automaticamente le risorse in base a condizioni predefinite. Questa funzionalità è utile per utenti e addetti al marketing della linea di business, ad esempio per creare flussi di lavoro personalizzati per cartelle specifiche. Supponiamo che tutte le risorse del servizio fotografico di un&#39;agenzia possano essere filigrane o che tutte le risorse caricate da un freelancer possano essere elaborate per creare rappresentazioni specifiche.

Per un modello di workflow, gli utenti possono creare un modulo di avvio che lo esegua. Un avvio di workflow monitora le modifiche nell&#39;archivio dei contenuti ed esegue il flusso di lavoro quando vengono soddisfatte le condizioni predefinite. Gli amministratori possono fornire l&#39;accesso agli addetti al marketing per creare i flussi di lavoro e configurare il programma di avvio. Gli utenti possono modificare il flusso di lavoro predefinito [!UICONTROL DAM Update Asset] per aggiungere i passaggi aggiuntivi necessari per elaborare risorse specifiche. Il flusso di lavoro viene eseguito su tutte le risorse appena caricate. Utilizzate uno dei seguenti metodi per limitare l&#39;esecuzione dei passaggi aggiuntivi su risorse specifiche:

* Effettuate una copia del flusso di lavoro Aggiorna risorsa  DAM e modificatelo per l&#39;esecuzione in una gerarchia di cartelle specifica. Questo approccio è utile per alcune cartelle.
* I passaggi di elaborazione aggiuntivi possono essere aggiunti utilizzando un [OR diviso](/help/sites-developing/workflows-step-ref.md#or-split) in base alle condizioni applicabili a tutte le cartelle richieste.

## Best practice e limitazioni {#best-practices-limitations-tips}

* Considerate le vostre esigenze per tutti i tipi di rappresentazioni durante la progettazione di flussi di lavoro. Se non prevedete la necessità di una rappresentazione in futuro, rimuovete il passaggio di creazione dal flusso di lavoro. Le rappresentazioni non possono essere eliminate in blocco in seguito. Le rappresentazioni indesiderate possono occupare molto spazio di archiviazione dopo un uso prolungato di [!DNL Experience Manager]. Per le singole risorse, potete rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, potete personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche oppure eliminare le risorse e caricarle di nuovo.
* Per impostazione predefinita, il flusso di lavoro Aggiorna risorsa  DAM include alcuni passaggi per creare miniature e rappresentazioni Web. Se dal flusso di lavoro vengono rimosse delle rappresentazioni predefinite, il rendering dell&#39;interfaccia utente di [!DNL Assets] non viene eseguito correttamente.

>[!MORELIKETHIS]
>
>* [Applicazione e partecipazione ai flussi di lavoro](/help/sites-authoring/workflows.md)
>* [Creare modelli di workflow ed estendere le funzionalità dei flussi di lavoro](/help/sites-developing/workflows.md)
>* [Metodi per eseguire i flussi di lavoro](/help/sites-administering/workflows-starting.md)
>* [Best practice per i flussi di lavoro](/help/sites-developing/workflows-best-practices.md)
>* [Articolo della community sulla modifica delle risorse mediante il flusso di lavoro](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

