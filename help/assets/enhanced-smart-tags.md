---
title: Smart tag migliorati
description: Smart tag migliorati
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Smart tag migliorati {#enhanced-smart-tags}

## Panoramica dei tag avanzati avanzati {#overview-of-enhanced-smart-tags}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più vocabolario controllato dalla tassonomia nei metadati delle risorse. Comprende in sostanza un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare risorse digitali di una determinata classe. L’assegnazione di tag alle risorse con un vocabolario controllato dalla tassonomia ne consente l’identificazione e il recupero tramite ricerche basate sui tag.

Rispetto ai vocabolari di lingua naturale, l’assegnazione di tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle al business di un’azienda e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche.

Ad esempio, un produttore di auto può assegnare tag alle immagini di un&#39;auto con nomi di modelli in modo che vengano visualizzate solo immagini rilevanti quando vengono ricercate immagini di vari modelli per progettare una campagna promozionale.

Affinché Smart Content Service possa applicare i tag giusti, è necessario addestrarlo per riconoscere la tassonomia. Per istruire il servizio, curate innanzitutto una serie di risorse e tag che meglio descrivano tali risorse. Applicate questi tag alle risorse ed eseguite un flusso di lavoro di formazione per facilitare l’apprendimento del servizio.

Una volta che un tag è stato preparato e pronto, il servizio ora può applicare questi tag alle risorse tramite un flusso di lavoro per l’assegnazione di tag.

In background, Smart Content Service utilizza il framework AI di Adobe Sensei per formare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e la tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un altro set di risorse.

Smart Content Service è un servizio cloud ospitato su Adobe I/O. Per utilizzarlo in Adobe Experience Manager (AEM), l’amministratore di sistema deve integrare l’istanza AEM con Adobe IO.

Di seguito sono riportati i passaggi principali per utilizzare Smart Content Service:

* Onboarding
* Verifica di risorse e tag (definizione tassonomia)
* Formazione di Smart Content Service
* Assegnazione tag automatica

![diagramma](assets/flowchart.gif)

## Prerequisiti {#prerequisites}

Prima di poter utilizzare Smart Content Service, accertatevi quanto segue per creare un&#39;integrazione su Adobe I/O:

* Un account Adobe ID con privilegi di amministratore per l’organizzazione.
* Il servizio Smart Content Service è abilitato per la vostra azienda.

## Onboarding {#onboarding}

Smart Content Service è disponibile per l&#39;acquisto come componente aggiuntivo per AEM. Dopo l&#39;acquisto, viene inviata un&#39;e-mail all&#39;amministratore dell&#39;organizzazione con un collegamento ad Adobe IO.

L’amministratore può seguire il collegamento per integrare Smart Content Service con AEM. Per integrare il servizio con AEM Assets, consulta [Configurare i tag](config-smart-tagging.md)avanzati.

La procedura di registrazione è completa quando l’amministratore configura il servizio e aggiunge utenti in AEM.

>[!NOTE]
>
>Se utilizzi AEM 6.3 o versione precedente e necessiti di un servizio di tag per le risorse, consulta [Tag](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)avanzati. I tag avanzati non utilizzano le funzionalità AI più recenti e sono quindi meno precisi del servizio avanzato di smart tag.

## Rivedere risorse e tag {#reviewing-assets-and-tags}

Dopo essere stati caricati, la prima cosa da fare è identificare un set di tag che meglio descrivono queste immagini nel contesto della vostra attività.

Quindi, rivedete le immagini per identificare un set di immagini che meglio rappresentano il vostro prodotto per un particolare requisito aziendale. Assicurati che le risorse del set selezionato siano conformi alle linee guida [di formazione di](smart-tags-training-guidelines.md)Smart Content Service.

Aggiungete le risorse a una cartella e applicate i tag a ciascuna risorsa dalla pagina delle proprietà. Quindi, eseguite il flusso di lavoro di formazione su questa cartella. La serie di risorse selezionata consente a Smart Content Service di formare in modo efficace più risorse utilizzando le definizioni della tassonomia.

>[!NOTE]
>
>1. La formazione è un processo irrevocabile. Adobe consiglia di rivedere i tag nel set di risorse curato prima di addestrare Smart Content Service sui tag.
>1. Prima di iniziare la formazione per qualsiasi tag, leggete le linee guida [per la formazione su](smart-tags-training-guidelines.md) Smart Content Service.
>1. Quando formate Smart Content Service per la prima volta, Adobe consiglia di addestrarlo su almeno due tag distinti.


## Formazione del servizio Smart Content {#training-the-smart-content-service}

Affinché Smart Content Service riconosca la tassonomia aziendale, eseguitela su un set di risorse che già includono tag rilevanti per la vostra attività. Dopo la formazione, il servizio può applicare la stessa tassonomia a un set di risorse simile.

È possibile formare il servizio più volte per migliorarne la capacità di applicare tag rilevanti. Dopo ogni ciclo di formazione, eseguite un flusso di lavoro con tag e verificate che le risorse dispongano dei tag appropriati.

Potete addestrare Smart Content Service periodicamente o su richiesta.

>[!NOTE]
>
>Il flusso di lavoro di formazione viene eseguito solo sulle cartelle.

### Formazione periodica {#periodic-training}

Potete abilitare Smart Content Service per l&#39;addestramento periodico delle risorse e dei tag associati all&#39;interno di una cartella. Aprite la pagina delle proprietà della cartella di risorse, selezionate **[!UICONTROL Abilita tag]** avanzati nella scheda **[!UICONTROL Dettagli]** e salvate le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Quando questa opzione è selezionata per una cartella, AEM esegue automaticamente un flusso di lavoro di formazione per formare Smart Content Service sulle risorse delle cartelle e i relativi tag. Per impostazione predefinita, il flusso di lavoro della formazione viene eseguito settimanalmente alle 12:30 del sabato.

### Formazione su richiesta {#on-demand-training}

Potete addestrare Smart Content Service quando necessario dalla console Flusso di lavoro.

1. Toccate o fate clic sul logo AEM, quindi andate a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Dalla pagina Modelli **[!UICONTROL di]** flusso di lavoro, selezionate il flusso di lavoro Formazione **[!UICONTROL tag]** avanzati, quindi toccate o fate clic su **[!UICONTROL Avvia flusso di lavoro]** dalla barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]** , individuate la cartella payload che include le risorse con tag per la formazione del servizio.
1. Specificate un titolo per il flusso di lavoro e un commento. Quindi toccate o fate clic su **[!UICONTROL Esegui]**. Le risorse e i tag vengono inviati per la formazione.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una volta che le risorse di una cartella vengono elaborate per la formazione, solo le risorse modificate vengono elaborate nei cicli di formazione successivi.

### Visualizzazione dei rapporti sulla formazione {#viewing-training-reports}

Per verificare se Smart Content Service è addestrato sui tag presenti nel set di risorse di formazione, controllate il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Toccate/fate clic sul logo AEM, quindi andate a **[!UICONTROL Strumenti > Risorse > Rapporti]**.
1. Nella pagina Rapporti **** risorse, toccate o fate clic su **[!UICONTROL Crea]**.
1. Selezionate il rapporto Formazione **** tag avanzati, quindi toccate o fate clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In Rapporto **** pianificazione, lasciate selezionata l&#39;opzione **[!UICONTROL Ora]** . Se desiderate pianificare il rapporto per un momento successivo, selezionate **[!UICONTROL Più tardi]** e specificate una data e un&#39;ora. Quindi toccate o fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Nella pagina Rapporti **** risorse, selezionate il rapporto generato. Per visualizzare il rapporto, toccate **[!UICONTROL Visualizza]** dalla barra degli strumenti.
1. Rivedete i dettagli del rapporto.

   Il rapporto mostra lo stato di formazione per i tag che hai imparato. Il colore verde nella colonna Stato **** formazione indica che il servizio Smart Content è stato addestrato per il tag. Il colore giallo indica che il servizio non è completamente addestrato per un particolare tag. In questo caso, aggiungete altre immagini con il tag specifico ed eseguite il flusso di lavoro di formazione per addestrare completamente il servizio sul tag .

   Se non visualizzate i tag nel rapporto, eseguite nuovamente il flusso di lavoro di formazione per questi tag.

1. Per scaricare il rapporto, selezionatelo dall’elenco e toccate **[!UICONTROL Scarica]** dalla barra degli strumenti. Il rapporto viene scaricato come file Excel.

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

1. Toccate o fate clic sul logo AEM, quindi andate a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Dalla pagina Modelli **[!UICONTROL di]** workflow, seleziona il flusso di lavoro Risorse **[!UICONTROL tag avanzati]** DAM e tocca o fai clic su **[!UICONTROL Avvia flusso di lavoro]** dalla barra degli strumenti.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]** , individuate la cartella payload contenente le risorse per le quali desiderate applicare automaticamente i tag.
1. Specificate un titolo per il flusso di lavoro e un commento facoltativo. Quindi toccate o fate clic su **[!UICONTROL Esegui]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Andate alla cartella delle risorse e controllate i tag per verificare se Smart Content Service ha applicato correttamente i tag alle risorse. Per informazioni dettagliate, consultate [Gestione dei tag](managing-smart-tags.md)avanzati.

#### Applicare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Dall’interfaccia utente di Risorse, selezionate la cartella contenente le risorse o risorse specifiche a cui desiderate applicare gli smart tag.
1. Toccate il logo Experience Manager e aprite la timeline.
1. Toccate la freccia in basso, quindi toccate o fate clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Selezionate il flusso di lavoro **[!UICONTROL DAM Smart Tag Assets]** e specificate un titolo per il flusso di lavoro.
1. Toccate o fate clic su **[!UICONTROL Avvia]**. Il flusso di lavoro applica i tag alle risorse. Andate alla cartella delle risorse e controllate i tag per verificare se Smart Content Service ha applicato correttamente i tag alle risorse. Per informazioni dettagliate, consultate [Gestione dei tag](managing-smart-tags.md)avanzati.

>[!NOTE]
>
>Nei successivi cicli di assegnazione dei tag, solo le risorse modificate vengono nuovamente etichettate con tag di nuova formazione.
>
>Tuttavia, vengono assegnati tag anche alle risorse inalterate se lo spazio tra l’ultimo ciclo di tag e quello corrente per il flusso di lavoro dei tag supera le 24 ore.
>
>Per flussi di lavoro con tag periodici, le risorse inalterate vengono contrassegnate con tag quando il gap supera i 6 mesi.
