---
title: Tag avanzati migliorati
description: Tag avanzati migliorati
contentOwner: AG
translation-type: tm+mt
source-git-commit: 892237699a4027e7dab406fd620cac220aa8b88b
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 11%

---


# Tag avanzati migliorati {#enhanced-smart-tags}

## Panoramica dei tag avanzati avanzati {#overview-of-enhanced-smart-tags}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre di più il vocabolario controllato dalla tassonomia nei metadati delle risorse. Comprende in sostanza un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare risorse digitali di una determinata classe. L’assegnazione di tag alle risorse con un vocabolario controllato dalla tassonomia ne consente l’identificazione e il recupero tramite ricerche basate sui tag.

Rispetto ai vocabolari di lingua naturale, l’assegnazione di tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle al business di un’azienda e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche.

Ad esempio, un produttore di auto può assegnare tag alle immagini di un&#39;auto con nomi di modelli in modo che vengano visualizzate solo immagini rilevanti quando vengono ricercate immagini di vari modelli per progettare una campagna promozionale.

Affinché Smart Content Service possa applicare i tag giusti, è necessario addestrarlo per riconoscere la tassonomia. Per istruire il servizio, curate innanzitutto una serie di risorse e tag che meglio descrivano tali risorse. Applicate questi tag alle risorse ed eseguite un flusso di lavoro di formazione per facilitare l’apprendimento del servizio.

Una volta che un tag è stato preparato e pronto, il servizio ora può applicare questi tag alle risorse tramite un flusso di lavoro per l’assegnazione di tag.

In background, Smart Content Service utilizza  framework Adobe Sensei AI per formare il proprio algoritmo di riconoscimento delle immagini sulla struttura dei tag e la tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un altro set di risorse.

Smart Content Service è un servizio cloud ospitato su  I/O Adobe. Per utilizzarlo in [!DNL Adobe Experience Manager], l&#39;amministratore di sistema deve integrare la [!DNL Experience Manager] distribuzione con  I/O Adobe.

Di seguito sono riportati i passaggi principali per utilizzare Smart Content Service:

* Onboarding
* Verifica di risorse e tag (definizione tassonomia)
* Formazione di Smart Content Service
* Assegnazione tag automatica

![diagramma](assets/flowchart.gif)

## Prerequisiti {#prerequisites}

Prima di poter utilizzare il Servizio di contenuti avanzati, verifica quanto segue per creare un’integrazione su Adobe I/O:

* Disponi di un account Adobe ID con privilegi di amministratore dell’organizzazione.
* Il Servizio di contenuti avanzati è abilitato per la tua organizzazione.

## Onboarding {#onboarding}

Il Servizio di contenuti avanzati è acquistabile come componente aggiuntivo per [!DNL Experience Manager]. Dopo l’acquisto, viene inviata un’e-mail all’amministratore dell’organizzazione con un collegamento a  I/O Adobe.

L&#39;amministratore può seguire il collegamento per integrare Smart Content Service con [!DNL Experience Manager]. Per integrare il servizio con [!DNL Experience Manager Assets], consultate [Configurare i tag](config-smart-tagging.md)avanzati.

La procedura di registrazione è completa quando l’amministratore configura il servizio e aggiunge utenti in [!DNL Experience Manager].

>[!NOTE]
>
>Se utilizzate la versione [!DNL Experience Manager] 6.3 o precedente e necessitate di un servizio di tag per le risorse, consultate [Smart Tags](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). I tag avanzati non utilizzano le funzionalità AI più recenti e sono quindi meno precisi del servizio avanzato di smart tag.

## Rivedere risorse e tag {#reviewing-assets-and-tags}

Dopo essere stati caricati, la prima cosa da fare è identificare un set di tag che meglio descrivono queste immagini nel contesto della vostra attività.

Quindi, rivedete le immagini per identificare un set di immagini che meglio rappresentano il vostro prodotto per un particolare requisito aziendale. Assicurati che le risorse del set selezionato siano conformi alle linee guida [di formazione di](smart-tags-training-guidelines.md)Smart Content Service.

Aggiungete le risorse a una cartella e applicate i tag a ciascuna risorsa dalla pagina delle proprietà. Quindi, eseguite il flusso di lavoro di formazione su questa cartella. La serie di risorse selezionata consente a Smart Content Service di formare in modo efficace più risorse utilizzando le definizioni della tassonomia.

>[!NOTE]
>
>1. La formazione è un processo irrevocabile.  Adobe consiglia di rivedere i tag nel set di risorse curato prima di addestrare Smart Content Service sui tag.
>1. Prima di iniziare la formazione per un tag, consultate le linee guida [di formazione per](smart-tags-training-guidelines.md)Smart Content Service.
>1. Quando formate Smart Content Service per la prima volta,  Adobe consiglia di addestrarlo su almeno due tag distinti.


## Formazione del servizio Smart Content {#training-the-smart-content-service}

Affinché Smart Content Service riconosca la tassonomia aziendale, eseguitela su un set di risorse che già includono tag rilevanti per la vostra attività. Dopo la formazione, il servizio può applicare la stessa tassonomia a un set di risorse simile.

È possibile formare il servizio più volte per migliorarne la capacità di applicare tag rilevanti. Dopo ogni ciclo di formazione, eseguite un flusso di lavoro con tag e verificate che le risorse dispongano dei tag appropriati.

Potete addestrare Smart Content Service periodicamente o su richiesta.

>[!NOTE]
>
>Il flusso di lavoro di formazione viene eseguito solo sulle cartelle.

### Formazione periodica {#periodic-training}

Potete abilitare Smart Content Service per l&#39;addestramento periodico delle risorse e dei tag associati all&#39;interno di una cartella. Aprite la pagina [!UICONTROL Proprietà] della cartella di risorse, selezionate **[!UICONTROL Abilita tag]** avanzati nella scheda **[!UICONTROL Dettagli]** e salvate le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Quando questa opzione è selezionata per una cartella, [!DNL Experience Manager] esegue automaticamente un flusso di lavoro di formazione per formare Smart Content Service sulle risorse delle cartelle e i relativi tag. Per impostazione predefinita, il flusso di lavoro della formazione viene eseguito settimanalmente alle 12:30 del sabato.

### Formazione su richiesta {#on-demand-training}

Potete addestrare Smart Content Service quando necessario dalla console Flusso di lavoro.

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]** , individuate la cartella payload che include le risorse con tag per la formazione del servizio.
1. Specificate un titolo per il flusso di lavoro e un commento. Quindi fate clic su **[!UICONTROL Esegui]**. Le risorse e i tag vengono inviati per la formazione.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una volta che le risorse di una cartella vengono elaborate per la formazione, solo le risorse modificate vengono elaborate nei cicli di formazione successivi.

### Visualizzazione dei rapporti sulla formazione {#viewing-training-reports}

Per verificare se Smart Content Service è addestrato sui tag presenti nel set di risorse di formazione, controllate il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell’ [!DNL Experience Manager] interfaccia, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Then, click **[!UICONTROL Create]** from the toolbar.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Rivedete i dettagli del rapporto.

   Il rapporto mostra lo stato di formazione per i tag che hai appreso. La presenza del colore verde nella colonna **[!UICONTROL Training Status (Stato formazione)]** indica che per il tag è stato eseguito il training del servizio di contenuti avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag.

   Se non visualizzate i tag nel rapporto, eseguite nuovamente il flusso di lavoro di formazione per questi tag.

1. Per scaricare il rapporto, selezionatelo dall’elenco e fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo di Microsoft Excel.

## Assegnare automaticamente tag alle risorse {#tagging-assets-automatically}

Dopo aver creato Smart Content Service, potete attivare il flusso di lavoro dei tag per applicare automaticamente i tag appropriati a un altro set di risorse simili.

Potete eseguire il flusso di lavoro dei tag periodicamente o quando necessario.

>[!NOTE]
>
>Il flusso di lavoro dei tag viene eseguito sia sulle risorse che sulle cartelle.

### Assegnazione periodica di tag {#periodic-tagging}

Potete abilitare Smart Content Service per assegnare tag periodici alle risorse all’interno di una cartella. Aprite la pagina delle proprietà della cartella di risorse, selezionate **[!UICONTROL Abilita tag]** avanzati nella scheda **[!UICONTROL Dettagli]** e salvate le modifiche.

Quando questa opzione è selezionata per una cartella, Smart Content Service assegna automaticamente i tag alle risorse all’interno della cartella. Per impostazione predefinita, il flusso di lavoro dei tag viene eseguito ogni giorno alle 12:00.

### Assegnazione tag su richiesta {#on-demand-tagging}

Per assegnare tag istantanei alle risorse, potete attivare il flusso di lavoro dei tag:

* Console Flusso di lavoro
* Timeline 

>[!NOTE]
>
>Se eseguite il flusso di lavoro dei tag dalla timeline, potete applicare tag a un massimo di 15 risorse alla volta.

#### Assegnare tag alle risorse dalla console del flusso di lavoro {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]** , individuate la cartella payload contenente le risorse per le quali desiderate applicare automaticamente i tag.
1. Specificate un titolo per il flusso di lavoro e un commento facoltativo. Fate clic su **[!UICONTROL Esegui]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Andate alla cartella delle risorse e controllate i tag per verificare se Smart Content Service ha applicato correttamente i tag alle risorse. Per informazioni dettagliate, consultate [Gestione dei tag](managing-smart-tags.md)avanzati.

#### Applicare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Dall’interfaccia [!DNL Assets] utente, selezionate la cartella contenente le risorse o risorse specifiche a cui desiderate applicare gli smart tag.
1. Dall&#39;angolo superiore sinistro, aprite la **[!UICONTROL timeline]**.
1. Aprite le azioni nella parte inferiore della barra laterale sinistra e fate clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Selezionate il flusso di lavoro **[!UICONTROL DAM Smart Tag Assets]** e specificate un titolo per il flusso di lavoro.
1. Fate clic su **[!UICONTROL Avvia]**. Il flusso di lavoro applica i tag alle risorse. Andate alla cartella delle risorse e controllate i tag per verificare se Smart Content Service ha applicato correttamente i tag alle risorse. Per informazioni dettagliate, consultate [Gestione dei tag](managing-smart-tags.md)avanzati.

>[!NOTE]
>
>Nei cicli di assegnazione dei tag successivi, solo le risorse modificate dispongono di tag di nuova formazione. Tuttavia, vengono assegnati tag anche alle risorse inalterate se lo spazio tra l’ultimo ciclo di tag e quello corrente per il flusso di lavoro dei tag supera le 24 ore. Per i flussi di lavoro con tag periodici, le risorse inalterate vengono contrassegnate con tag quando l’intervallo di tempo supera i 6 mesi.
