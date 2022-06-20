---
title: Sono stati migliorati i tag avanzati
description: Sono stati migliorati i tag avanzati
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
source-git-commit: dd1e08bee03a6c7b07b32b0fb929d02dad467744
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 4%

---

# Comprendere, applicare e curare tag avanzati {#enhanced-smart-tags}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | Questo articolo |
| AEM 6.4 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/enhanced-smart-tags.html?lang=en) |

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave a cui i dipendenti, i partner e i clienti utilizzano comunemente per fare riferimento e cercare risorse digitali di una particolare classe. L’assegnazione di tag alle risorse tramite un vocabolario controllato dalla tassonomia garantisce che le risorse vengano identificate e recuperate facilmente.

Rispetto ai vocabolari linguistici naturali, l’assegnazione di tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle con il business di un’azienda e assicura che le risorse più rilevanti vengano visualizzate nelle ricerche.

Ad esempio, un produttore di auto può assegnare tag alle immagini di un&#39;auto con nomi di modello in modo che vengano visualizzate solo immagini rilevanti quando vengono ricercate immagini di vari modelli per progettare una campagna promozionale.

Affinché il Servizio di contenuti avanzati applichi i tag giusti, addestralo a riconoscere la tassonomia. Per addestrare il servizio, cura innanzitutto un insieme di risorse e tag che descrivono al meglio queste risorse. Per facilitare l’apprendimento del servizio, applica questi tag alle risorse ed esegui un flusso di lavoro di formazione.

Una volta che un tag è stato addestrato e pronto, il servizio può ora applicare questi tag alle risorse tramite un flusso di lavoro di assegnazione tag.

In background, il Servizio di contenuti avanzati utilizza il framework Adobe Sensei AI per addestrare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e sulla tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un diverso set di risorse.

Il Servizio di contenuti avanzati è un servizio cloud ospitato su [!DNL Adobe Developer Console]. Per utilizzarlo in [!DNL Adobe Experience Manager], l’amministratore di sistema deve integrare [!DNL Experience Manager] implementazione con [!DNL Adobe Developer Console].

In sintesi, ecco i passaggi principali per l’utilizzo del Servizio di contenuti avanzati:

* Onboarding
* Verifica di risorse e tag (definizione della tassonomia)
* Formazione del Servizio di contenuti avanzati
* Assegnazione tag automatica

![Grafico a flusso](assets/flowchart.gif)

## Prerequisiti e formati supportati {#prerequisites}

Prima di poter utilizzare il Servizio di contenuti avanzati, verifica quanto segue per creare un’integrazione su [!DNL Adobe Developer Console]:

* Un account Adobe ID con privilegi di amministratore per l’organizzazione.
* Abilita il servizio Servizio di contenuti avanzati per la tua organizzazione.
* Per aggiungere il pacchetto di base Smart Content Services a una distribuzione, concedere una licenza [!DNL Adobe Experience Manager Sites] Pacchetto di base e [!DNL Assets] add-on.

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

Il servizio applica tag avanzati alle rappresentazioni di risorse dei seguenti tipi MIME:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Onboarding {#onboarding}

Il Servizio di contenuti avanzati è acquistabile come componente aggiuntivo per [!DNL Experience Manager]. Dopo l’acquisto, viene inviata un’e-mail all’amministratore dell’organizzazione con un collegamento ad [!DNL Adobe I/O].

L’amministratore può seguire il collegamento per integrare il Servizio di contenuti avanzati con [!DNL Experience Manager]. Per integrare il servizio con [!DNL Experience Manager Assets], vedi [Configurare tag avanzati](config-smart-tagging.md).

Il processo di onboarding è completo quando l’amministratore configura il servizio e aggiunge gli utenti in [!DNL Experience Manager].

## Esaminare risorse e tag {#reviewing-assets-and-tags}

Una volta a bordo, la prima cosa che si desidera fare è identificare un set di tag che descrivono al meglio queste immagini nel contesto della propria attività.

Quindi, rivedi le immagini per identificare un set di immagini che meglio rappresentano il tuo prodotto per un particolare requisito aziendale. Assicurati che le risorse nel set curato siano conformi a [Linee guida per la formazione sul Servizio di contenuti avanzati](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Aggiungi le risorse a una cartella e applica i tag a ciascuna risorsa dalla pagina delle proprietà. Quindi, esegui il flusso di lavoro di formazione su questa cartella. Il set di risorse curato consente al Servizio di contenuti avanzati di addestrare in modo efficace più risorse utilizzando le definizioni di tassonomia.

>[!NOTE]
>
>1. La formazione è un processo irrevocabile. Adobe consiglia di rivedere i tag nel set di risorse curato molto prima di addestrare il Servizio di contenuti avanzati sui tag.
>1. Prima di addestrare un tag, consulta [Linee guida per la formazione sul Servizio di contenuti avanzati](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Quando si prepara il Servizio di contenuti avanzati per la prima volta, Adobe consiglia di addestrarlo su almeno due tag distinti.


## Comprendere [!DNL Experience Manager] risultati di ricerca con tag avanzati {#understandsearch}

Per impostazione predefinita, [!DNL Experience Manager] la ricerca combina i termini di ricerca con un `AND` clausola . L’utilizzo di smart tag non modifica questo comportamento predefinito. L’utilizzo di tag avanzati aggiunge un ulteriore `OR` per trovare i termini di ricerca correlati agli smart tag. Ad esempio, considera la ricerca `woman running`. Risorse con `woman` o semplicemente `running` nei metadati non vengono visualizzate nei risultati della ricerca per impostazione predefinita. Tuttavia, una risorsa è taggata con `woman` o `running` l’utilizzo di smart tag viene visualizzato in una query di ricerca di questo tipo. Quindi i risultati della ricerca sono una combinazione di:

* Risorse con `woman` e `running` parole chiave nei metadati.

* Risorse con tag avanzati con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. Corrisponde a `woman running` nei vari campi di metadati.
1. Corrisponde a `woman running` in smart tag.
1. Corrisponde a `woman` o `running` in smart tag.

>[!CAUTION]
>
>Se l&#39;indicizzazione di Lucene è fatta a partire da [!DNL Adobe Experience Manager], la ricerca basata sugli smart tag non funziona come previsto.

## Assegnare automaticamente tag alle risorse {#tagging-assets-automatically}

Dopo aver completato il training del Servizio di contenuti avanzati, puoi attivare il flusso di lavoro di assegnazione tag per applicare automaticamente i tag appropriati a un set diverso di risorse simili.

Puoi eseguire il flusso di lavoro dei tag periodicamente o quando necessario.

>[!NOTE]
>
>Il flusso di lavoro di assegnazione tag viene eseguito sia sulle risorse che sulle cartelle.

### Assegnazione periodica di tag {#periodic-tagging}

È possibile abilitare il Servizio di contenuti avanzati per assegnare periodicamente tag alle risorse all’interno di una cartella. Apri la pagina delle proprietà della cartella di risorse e seleziona **[!UICONTROL Abilita tag avanzati]** in **[!UICONTROL Dettagli]** e salva le modifiche.

Una volta selezionata questa opzione per una cartella, il Servizio di contenuti avanzati assegna automaticamente i tag alle risorse all’interno della cartella. Per impostazione predefinita, il flusso di lavoro di assegnazione tag viene eseguito ogni giorno alle 12:00.

### Assegnazione tag su richiesta {#on-demand-tagging}

Puoi attivare il flusso di lavoro di assegnazione tag dalla console del flusso di lavoro o dalla timeline per assegnare tag istantanei alle risorse.

>[!NOTE]
>
>Se esegui il flusso di lavoro di assegnazione tag dalla timeline, puoi applicare tag a un massimo di 15 risorse alla volta.

#### Assegnare tag alle risorse dalla console del flusso di lavoro {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interfaccia, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Da **[!UICONTROL Modelli di flusso di lavoro]** , seleziona la **[!UICONTROL Risorse per tag avanzati DAM]** , quindi fai clic su **[!UICONTROL Avvia flusso di lavoro]** dalla barra degli strumenti.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In **[!UICONTROL Esegui flusso di lavoro]** , individua la cartella payload contenente le risorse sulle quali desideri applicare automaticamente i tag.
1. Specifica un titolo per il flusso di lavoro e un commento facoltativo. Fai clic su **[!UICONTROL Esegui]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Per verificare se il Servizio di contenuti avanzati ha applicato correttamente i tag alle risorse, passa alla cartella delle risorse e controlla i tag.

#### Assegnare tag alle risorse dalla timeline {#tagging-assets-from-the-timeline}

1. Da [!DNL Assets] interfaccia utente, seleziona la cartella contenente le risorse o risorse specifiche a cui desideri applicare gli smart tag.
1. Dall’angolo in alto a sinistra, apri le **[!UICONTROL Timeline]**.
1. Apri le azioni dalla parte inferiore della barra laterale sinistra e fai clic su **[!UICONTROL Avvia flusso di lavoro]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleziona la **[!UICONTROL Risorse per tag avanzati DAM]** e specifica un titolo per il flusso di lavoro.
1. Fai clic su **[!UICONTROL Inizio]**. Il flusso di lavoro applica tag alle risorse. per verificare se il Servizio di contenuti avanzati ha applicato correttamente i tag alle risorse, passa alla cartella delle risorse e controlla i tag.

>[!NOTE]
>
>Nei cicli di assegnazione tag successivi, solo le risorse modificate vengono nuovamente taggate con tag appena addestrati. Tuttavia, anche le risorse non modificate vengono contrassegnate se il divario tra l’ultimo ciclo di assegnazione tag e quello corrente per il flusso di lavoro di assegnazione tag supera le 24 ore. Per i flussi di lavoro con tag periodici, le risorse non modificate vengono taggate quando il tempo gap supera i sei mesi.

## Cura o modera gli smart tag applicati {#manage-smart-tags}

Puoi curare i tag avanzati per rimuovere eventuali tag non accurati assegnati alle immagini del tuo marchio in modo che vengano visualizzati solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche basate sui tag per le immagini, garantendo che l’immagine venga visualizzata nei risultati della ricerca per i tag più rilevanti. In sostanza, aiuta ad eliminare le possibilità che immagini non collegate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare un rango più alto a un tag per aumentarne la pertinenza per un’immagine. La promozione di un tag per un’immagine aumenta le possibilità che l’immagine appaia nei risultati della ricerca quando viene ricercato un particolare tag.

1. Nella casella di ricerca, cerca le risorse basate su un tag come parola chiave.
1. Per identificare un’immagine che non è pertinente alla ricerca, controlla i risultati della ricerca.
1. Seleziona l’immagine e fai clic su **[!UICONTROL Gestire i tag]** dalla barra degli strumenti.
1. Da **[!UICONTROL Gestire i tag]** , controlla i tag. Se non desideri che la ricerca dell’immagine sia basata su un tag specifico, selezionalo e fai clic su **[!UICONTROL Elimina]** dalla barra degli strumenti. In alternativa, fai clic su `x` simbolo visualizzato accanto a un tag.
1. Facoltativamente, per assegnare un rango più alto a un tag, selezionalo e fai clic su **[!UICONTROL Promuovi]** dalla barra degli strumenti. Il tag promosso viene spostato in **[!UICONTROL Tag]** sezione .
1. Fai clic su **[!UICONTROL Salva]** quindi fai clic su **[!UICONTROL OK]**
1. Passa a **[!UICONTROL Proprietà]** per l’immagine. Osserva che al tag promosso viene assegnata una maggiore rilevanza e viene visualizzato in precedenza nei risultati della ricerca.

## Suggerimenti e limitazioni {#tips-best-practices-limitations}

* Per addestrare il modello, utilizzare le immagini più appropriate. Non è possibile ripristinare l’addestramento o rimuovere il modello di formazione. La precisione dell’assegnazione tag dipende dall’addestramento corrente, quindi è necessario eseguirlo con attenzione.
* L’utilizzo di Smart Content Services è limitato a 2 milioni di immagini con tag all’anno. Tutte le immagini duplicate elaborate e con tag vengono conteggiate come immagini con tag.
* Se esegui il flusso di lavoro di assegnazione tag dalla timeline, puoi applicare tag a un massimo di 15 risorse alla volta.
* I tag avanzati funzionano solo per i formati immagine PNG e JPG. Le risorse supportate con rappresentazioni create in questi due formati ricevono i tag di Tag avanzati.
