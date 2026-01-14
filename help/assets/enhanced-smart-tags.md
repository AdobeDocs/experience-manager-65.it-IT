---
title: Tag avanzati migliorati
description: Tag avanzati migliorati
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7c1aeec18f35b019a63d0385ada248b26a0df9de
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 2%

---

# Comprendere, applicare e curare tag avanzati {#enhanced-smart-tags}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=it) |
| AEM 6.5 | Questo articolo |

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più spesso il vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare risorse digitali di una particolare classe. L’assegnazione dei tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificarle e recuperarle facilmente.

Rispetto ai vocabolari del linguaggio naturale, assegnare tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle alle attività aziendali e assicura che le risorse più rilevanti vengano visualizzate nelle ricerche.

Ad esempio, un produttore di automobili può taggare le immagini dell’auto con i nomi dei modelli, in modo che vengano visualizzate solo le immagini pertinenti quando si cercano immagini di vari modelli per progettare una campagna promozionale.

Affinché il Servizio di contenuti avanzati possa applicare i tag giusti, addestralo a riconoscere la tua tassonomia. Per addestrare il servizio, crea innanzitutto una serie di risorse e tag che descrivono al meglio tali risorse. Per aiutare il servizio ad apprendere, applica questi tag alle risorse ed esegui un flusso di lavoro di formazione.

Una volta che un tag è stato preparato e pronto, il servizio può ora applicarlo alle risorse tramite un flusso di lavoro sui tag.

In background, il Servizio di contenuti avanzati utilizza il framework di intelligenza artificiale di Adobe per addestrare il suo algoritmo di riconoscimento delle immagini in base alla struttura dei tag e alla tassonomia aziendale. Questa content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse.

Servizio di contenuti avanzati è un servizio cloud ospitato su [!DNL Adobe Developer Console]. Per utilizzarlo in [!DNL Adobe Experience Manager], l&#39;amministratore di sistema deve integrare la distribuzione di [!DNL Experience Manager] con [!DNL Adobe Developer Console].

In sintesi, ecco i passaggi principali per utilizzare il Servizio di contenuti avanzati:

* Onboarding
* Esame di risorse e tag (definizione della tassonomia)
* Formazione del Servizio di contenuti avanzati
* Assegnazione tag automatica

![Diagramma di flusso](assets/flowchart.gif)

## Prerequisiti e formati supportati {#prerequisites}

Prima di poter utilizzare il Servizio di contenuti avanzati, verificare quanto segue per creare un&#39;integrazione in [!DNL Adobe Developer Console]:

* Un account Adobe ID con privilegi di amministratore dell’organizzazione.
* Abilita il servizio di contenuti avanzati per la tua organizzazione.
* Per aggiungere il pacchetto base di Smart Content Services a una distribuzione, concedere la licenza al pacchetto base [!DNL Adobe Experience Manager Sites] e al componente aggiuntivo [!DNL Assets].

Il servizio applica tag avanzati alle risorse dei seguenti tipi MIME:

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

Il servizio applica tag avanzati alle rappresentazioni delle risorse dei seguenti tipi MIME:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Onboarding {#onboarding}

Il Servizio di contenuti avanzati è acquistabile come componente aggiuntivo per [!DNL Experience Manager]. Dopo l&#39;acquisto, viene inviata un&#39;e-mail all&#39;amministratore dell&#39;organizzazione con un collegamento a [!DNL Adobe I/O].

L&#39;amministratore può seguire il collegamento per integrare Smart Content Service con [!DNL Experience Manager]. Per integrare il servizio con [!DNL Experience Manager Assets], vedere [Configurare tag avanzati](config-smart-tagging.md).

Il processo di onboarding è stato completato quando l&#39;amministratore configura il servizio e aggiunge utenti in [!DNL Experience Manager].

## Esaminare risorse e tag {#reviewing-assets-and-tags}

Dopo l’onboarding, la prima cosa da fare è identificare un set di tag che descrivano al meglio queste immagini nel contesto della tua attività.

Quindi, rivedi le immagini per identificare un set di immagini che rappresentano al meglio il tuo prodotto per un particolare requisito aziendale. Assicurati che le risorse del set curato siano conformi alle [linee guida per la formazione sul Servizio di contenuti avanzati](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Aggiungi le risorse a una cartella e applica i tag a ciascuna risorsa dalla pagina delle proprietà. Quindi, esegui il flusso di lavoro di formazione su questa cartella. Il set curato di risorse consente al Servizio di contenuti avanzati di addestrare in modo efficace più risorse utilizzando le definizioni della tassonomia.

>[!NOTE]
>
>1. La formazione è un processo irrevocabile. Adobe consiglia di rivedere i tag nel set curato di risorse ben prima di addestrare il Servizio di contenuti avanzati sui tag.
>1. Prima della formazione per un tag, consulta [Linee guida per la formazione sul Servizio di contenuti avanzati](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Quando si addestra il Servizio di contenuti avanzati per la prima volta, Adobe consiglia di addestrarlo su almeno due tag distinti.

## Comprendere i risultati della ricerca di [!DNL Experience Manager] con tag avanzati {#understandsearch}

Per impostazione predefinita, la ricerca [!DNL Experience Manager] combina i termini di ricerca con una clausola `AND`. L’utilizzo di smart tag non modifica questo comportamento predefinito. L&#39;utilizzo di smart tag aggiunge una clausola `OR` aggiuntiva per trovare i termini di ricerca correlati agli smart tag. Ad esempio, provare a cercare `woman running`. Assets con solo `woman` o solo `running` parola chiave nei metadati non viene visualizzata nei risultati della ricerca per impostazione predefinita. Tuttavia, una risorsa con tag `woman` o `running` tramite tag avanzati viene visualizzata in tale query di ricerca. I risultati della ricerca sono quindi una combinazione di:

* Assets con `woman` e `running` parole chiave nei metadati.

* Smart tag di Assets con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca nei tag avanzati. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde a `woman running` nei vari campi di metadati.
1. Corrisponde a `woman running` negli smart tag.
1. Corrisponde a `woman` o `running` negli smart tag.

>[!CAUTION]
>
>Se l&#39;indicizzazione Lucene viene eseguita su [!DNL Adobe Experience Manager], la ricerca basata su smart tag non funziona come previsto.

## Assegna tag automatici alle risorse {#tagging-assets-automatically}

Dopo aver addestrato il Servizio di contenuti avanzati, puoi attivare il flusso di lavoro sui tag per applicare automaticamente i tag appropriati a un diverso set di risorse simili.

Puoi eseguire il flusso di lavoro sui tag periodicamente o quando necessario.

>[!NOTE]
>
>Il flusso di lavoro sui tag viene eseguito sia sulle risorse che sulle cartelle.

### Assegnazione tag periodica {#periodic-tagging}

Puoi abilitare il Servizio di contenuti avanzati per assegnare periodicamente tag alle risorse all’interno di una cartella. Apri la pagina delle proprietà della cartella di risorse, seleziona **[!UICONTROL Abilita tag avanzati]** nella scheda **[!UICONTROL Dettagli]** e salva le modifiche.

Una volta selezionata questa opzione per una cartella, il Servizio di contenuti avanzati assegna automaticamente i tag alle risorse all’interno della cartella. Per impostazione predefinita, il flusso di lavoro sui tag viene eseguito ogni giorno alle ore 00:00.:00

### Assegnazione di tag su richiesta {#on-demand-tagging}

Puoi attivare il flusso di lavoro sui tag dalla console del flusso di lavoro o dalla timeline per assegnare immediatamente i tag alle risorse.

>[!NOTE]
>
>Se esegui il flusso di lavoro sui tag dalla timeline, puoi applicare tag a un massimo di 15 risorse alla volta.

#### Assegnare tag alle risorse dalla console del flusso di lavoro {#tagging-assets-from-the-workflow-console}

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL DAM Smart Tags Assets]** e quindi fai clic su **[!UICONTROL Avvia flusso di lavoro]** nella barra degli strumenti.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]**, individua la cartella del payload contenente le risorse alle quali desideri applicare automaticamente i tag.
1. Specifica un titolo per il flusso di lavoro e un commento facoltativo. Fare clic su **[!UICONTROL Esegui]**.

   ![finestra di dialogo per assegnazione tag](assets/tagging_dialog.png)

   Per verificare se il Servizio di contenuti avanzati ha applicato i tag appropriati alle risorse, passa alla cartella delle risorse e controlla i tag.

#### Assegnare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Dall&#39;interfaccia utente [!DNL Assets], selezionare la cartella contenente le risorse o le risorse specifiche a cui si desidera applicare gli smart tag.
1. Dall&#39;angolo superiore sinistro, apri la **[!UICONTROL Timeline]**.
1. Apri le azioni dalla parte inferiore della barra laterale a sinistra e fai clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Selezionare il flusso di lavoro **[!UICONTROL Tag avanzati DAM Assets]** e specificare un titolo per il flusso di lavoro.
1. Fare clic su **[!UICONTROL Inizio]**. Il flusso di lavoro applica i tag alle risorse. per verificare se il Servizio di contenuti avanzati ha applicato i tag appropriati alle risorse, passa alla cartella delle risorse e controlla i tag.

>[!NOTE]
>
>Nei cicli di assegnazione tag successivi, solo le risorse modificate vengono nuovamente taggate con tag nuovi. Tuttavia, anche le risorse non modificate vengono contrassegnate se il gap tra l’ultimo e l’attuale ciclo di assegnazione tag per il flusso di lavoro di assegnazione tag supera le 24 ore. Per i flussi di lavoro di assegnazione tag periodici, alle risorse non modificate vengono assegnati tag quando il periodo di tempo supera i sei mesi.

## Cura o modera gli smart tag applicati {#manage-smart-tags}

È possibile curare i tag avanzati per rimuovere eventuali tag non accurati assegnati alle immagini del marchio in modo che vengano visualizzati solo i tag più rilevanti.

La moderazione dei tag avanzati consente inoltre di perfezionare le ricerche di immagini basate su tag, garantendo che l’immagine venga visualizzata nei risultati di ricerca dei tag più rilevanti. In sostanza, elimina la possibilità che immagini non correlate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare una classificazione più alta a un tag per aumentarne la rilevanza per un’immagine. La promozione di un tag per un’immagine aumenta le possibilità che l’immagine appaia nei risultati di ricerca quando viene eseguita la ricerca nel tag specifico.

1. Nella casella di ricerca, cerca le risorse in base a un tag come parola chiave.
1. Per identificare un&#39;immagine che non è rilevante per la ricerca, esaminare i risultati della ricerca.
1. Seleziona l&#39;immagine e fai clic su **[!UICONTROL Gestisci tag]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Gestisci tag]**, controlla i tag. Se non si desidera cercare l&#39;immagine in base a un tag specifico, selezionare il tag e fare clic su **[!UICONTROL Elimina]** nella barra degli strumenti. In alternativa, fare clic sul simbolo `x` visualizzato accanto a un tag.
1. Facoltativamente, per assegnare una classificazione superiore a un tag, selezionare il tag e fare clic su **[!UICONTROL Promuovi]** nella barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]**.
1. Fai clic su **[!UICONTROL Salva]** e quindi su **[!UICONTROL OK]**
1. Passare alla pagina **[!UICONTROL Proprietà]** per l&#39;immagine. Osserva che al tag promosso è stata assegnata maggiore rilevanza e viene visualizzato prima nei risultati di ricerca.

## Suggerimenti e limitazioni {#tips-best-practices-limitations}

* Per addestrare il modello, utilizzate le immagini più appropriate. Non è possibile ripristinare l’addestramento o rimuovere il modello di addestramento. La precisione dei tag dipende dall&#39;addestramento corrente, quindi esegui questa operazione con attenzione.
* L’utilizzo di Smart Content Services è limitato a un massimo di 2 milioni di immagini con tag all’anno. Tutte le immagini duplicate che vengono elaborate e taggate vengono conteggiate come immagini taggate.
* Se esegui il flusso di lavoro sui tag dalla timeline, puoi applicare tag a un massimo di 15 risorse alla volta.
* I tag avanzati funzionano solo per i formati immagine PNG e JPG. Pertanto, le risorse supportate con rappresentazioni create in questi due formati vengono contrassegnate con tag avanzati.

>[!MORELIKETHIS]
>
>* [Panoramica e formazione dei tag avanzati](enhanced-smart-tags.md)
>* [Configura assegnazione tag avanzati](config-smart-tagging.md)
>* [Risoluzione dei problemi relativi agli smart tag per le credenziali OAuth](config-oauth.md)
>* [Esercitazione video sugli smart tag](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=it)
