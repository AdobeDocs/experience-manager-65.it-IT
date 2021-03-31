---
title: Gestire le raccolte di risorse digitali
description: Scopri le attività per gestire le raccolte di risorse, ad esempio creare, visualizzare, eliminare, modificare e scaricare le raccolte.
contentOwner: AG
mini-toc-levels: 1
role: Professionista
feature: Raccolte, Gestione risorse
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 11%

---


# Gestire le raccolte {#managing-collections}

Una raccolta è un set di risorse all’interno di [!DNL Adobe Experience Manager Assets]. Utilizza le raccolte per condividere le risorse tra gli utenti. Il set può essere una raccolta statica o una raccolta dinamica basata sui risultati della ricerca.

A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Puoi condividere raccolte con vari utenti a cui sono assegnati diversi livelli di privilegi, tra cui visualizzazione, modifica e così via.

Puoi condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L’integrità referenziale delle risorse viene mantenuta tra le raccolte.

Le raccolte sono dei tipi seguenti, in base alla modalità di raccolta delle risorse:

* Una raccolta contenente un elenco di riferimento statico di risorse, cartelle e altre raccolte.

* Una raccolta avanzata che include in modo dinamico le risorse in base a un criterio di ricerca.

## Accedi alla console Raccolte {#navigating-the-collections-console}

Per aprire le **[!UICONTROL Raccolte]**, nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**.

## Creare una raccolta {#creating-a-collection}

È possibile creare una raccolta con [riferimenti statici](#creating-a-collection-with-static-references) o in base a un [filtro basato su criteri di ricerca](#creating-a-smart-collection). Puoi anche creare una raccolta da una Lightbox.

### Creare una raccolta con riferimenti statici {#creating-a-collection-with-static-references}

Puoi creare una raccolta con riferimenti statici, ad esempio una raccolta con riferimenti a risorse, cartelle, raccolte, set 360 gradi e set di immagini.

1. Passa alla console **[!UICONTROL Raccolte]** .
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea raccolta]**, immetti un titolo e una descrizione facoltativa per la raccolta.
1. Aggiungi i membri alla raccolta e assegna le autorizzazioni appropriate. In alternativa, per consentire a tutti gli utenti di accedere alla raccolta, seleziona **[!UICONTROL Raccolta pubblica]**.

   >[!NOTE]
   >
   >Per consentire ai membri di condividere le raccolte con altri utenti, fornisci al gruppo `dam-users` le autorizzazioni di lettura nel percorso `home/users`. Concedi l&#39;autorizzazione agli utenti nella posizione `/content/dam/collections` per consentire agli utenti di visualizzare le raccolte negli elenchi a comparsa. In alternativa, imposta l’utente come parte del gruppo `dam-users` .

1. (Facoltativo) Aggiungi una miniatura per la raccolta.
1. Fai clic su **[!UICONTROL Crea]**, quindi fai clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Una raccolta con il titolo e le proprietà specificati viene aperta nella console Raccolte.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] consente di creare attività di revisione per una raccolta, in modo analogo a come si creano le attività di revisione per una cartella di risorse.

   Per aggiungere risorse alla raccolta, passa all’interfaccia utente [!DNL Assets] . Per informazioni dettagliate, consulta [Aggiungere risorse a una raccolta](#adding-assets-to-a-collection).

### Creare raccolte utilizzando la zona di rilascio {#create-collections-using-dropzone}

Puoi trascinare risorse dall’interfaccia utente [!DNL Assets] a una raccolta. Puoi anche creare una copia di una raccolta e trascinarvi le risorse.

1. Dall’interfaccia utente [!DNL Assets] , seleziona le risorse da aggiungere a una raccolta.
1. Trascina le risorse nella zona **[!UICONTROL Rilascia raccolta]** . In alternativa, fai clic su **[!UICONTROL Alla raccolta]** nella barra degli strumenti.

   ![drop_in_collection](assets/drop_in_collection.png)

1. Nella pagina **[!UICONTROL Aggiungi alla raccolta]**, fai clic su **[!UICONTROL Crea raccolta]** nella barra degli strumenti.

   Se desideri aggiungere le risorse a una raccolta esistente, selezionala dalla pagina e fai clic su **[!UICONTROL Aggiungi]**. Per impostazione predefinita, è selezionata la raccolta aggiornata più di recente.

1. Nella finestra di dialogo **[!UICONTROL Crea nuova raccolta]**, specifica un nome per la raccolta. Se vuoi che la raccolta sia accessibile a tutti gli utenti, seleziona **[!UICONTROL Raccolta pubblica]**.
1. Fai clic su **[!UICONTROL Continua]** per creare la raccolta.

### Creare una raccolta avanzata {#creating-a-smart-collection}

Una raccolta avanzata utilizza un criterio di ricerca per popolare dinamicamente le risorse. È possibile creare una raccolta avanzata utilizzando solo file e non cartelle o file e cartelle.

Per creare una raccolta avanzata, effettua le seguenti operazioni:

1. Passa all’ interfaccia utente [!DNL Assets] e fai clic su Cerca.

1. Digita la parola chiave di ricerca nella casella Omnisearch e seleziona `Enter`. Apri il pannello Filtri e applica un filtro di ricerca.

1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.

   ![files_option](assets/files_option.png)

1. Fai clic su **[!UICONTROL Salva raccolta avanzata]**.

1. Specifica un nome per la raccolta. Seleziona **[!UICONTROL Public]** per aggiungere il gruppo DAM Users con il ruolo Visualizzatore alla raccolta avanzata.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se selezioni **[!UICONTROL Public]**, la raccolta avanzata diventa disponibile a tutti coloro che dispongono del ruolo di proprietario dopo averlo creato. Se annulli l’opzione **[!UICONTROL Public]** , il gruppo di utenti DAM non è più associato alla raccolta avanzata.

1. Fai clic su **[!UICONTROL Salva]** per creare la raccolta avanzata, quindi chiudi la finestra messaggio per completare il processo.

   La nuova raccolta avanzata viene aggiunta anche all&#39;elenco **[!UICONTROL Ricerche salvate]**.

   ![collection_listing](assets/collection_listing.png)

   L&#39;etichetta dell&#39;opzione **[!UICONTROL Crea selezione avanzata]** diventa **[!UICONTROL Modifica selezione avanzata]**. Per modificare le impostazioni della raccolta avanzata, seleziona **[!UICONTROL File]** dall’elenco **[!UICONTROL File e cartelle]**. Fai clic sull&#39;opzione **[!UICONTROL Modifica selezione avanzata]** ![modifica raccolta avanzata](assets/do-not-localize/edit-smart-collection.png) .

## Aggiungere risorse a una raccolta {#adding-assets-to-a-collection}

Puoi aggiungere risorse a una raccolta contenente un elenco di risorse o cartelle a cui si fa riferimento. Le raccolte avanzate utilizzano una query di ricerca per popolare le risorse. Pertanto, i riferimenti statici a risorse e cartelle non sono applicabili a tali risorse.

1. Nell’interfaccia utente delle risorse [!DNL A]Assets, seleziona la risorsa e fai clic su **[!UICONTROL To Collection]** ![add to collection](assets/do-not-localize/add-to-collection.png) dalla barra degli strumenti.
In alternativa, puoi trascinare la risorsa nell’area **[!UICONTROL Rilascia raccolta]** sull’interfaccia. Aggiungi le risorse quando l&#39;etichetta della regione cambia in **[!UICONTROL Rilascia a Aggiungi]**.

1. Nella pagina **[!UICONTROL Aggiungi alla raccolta]** , seleziona la raccolta alla quale desideri aggiungere la risorsa.

1. Fai clic su **[!UICONTROL Aggiungi]**, quindi chiudi il messaggio di conferma. La risorsa viene aggiunta alla raccolta.

## Modificare una raccolta avanzata {#editing-a-smart-collection}

Le raccolte avanzate vengono create salvando una ricerca in modo da poter modificare il loro contenuto modificando i parametri di ricerca della [ricerca salvata](#saved-searches).

1. Nell&#39;interfaccia utente [!DNL Assets], fai clic sull&#39;opzione di ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png) nella barra degli strumenti.
1. Con il cursore nella casella Omnisearch, selezionare il tasto `Return`.
1. Nell’interfaccia [!DNL Experience Manager], apri il pannello Filtri .
1. Dall’elenco **[!UICONTROL Ricerche salvate]**, seleziona la raccolta avanzata da modificare. Nel pannello Ricerca sono visualizzati i filtri configurati per la ricerca salvata.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Dall&#39;elenco **[!UICONTROL File e cartelle]**, selezionare **[!UICONTROL File]**.
1. Se necessario, modifica uno o più filtri. Fai clic su **[!UICONTROL Modifica raccolta avanzata]**.

   Puoi anche modificare il nome della raccolta avanzata.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. Fai clic su **[!UICONTROL Salva]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica raccolta avanzata]**.
1. Fai clic su **[!UICONTROL Sovrascrivi]** per sostituire la raccolta avanzata originale con la raccolta modificata. In alternativa, selezionare **[!UICONTROL Salva con nome]** per salvare separatamente la raccolta modificata.
1. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Salva]** per completare il processo.

## Visualizzare e modificare i metadati della raccolta {#view-edit-collection-metadata}

I metadati della raccolta includono dati sulla raccolta, compresi eventuali tag aggiunti.

1. Dalla console [!UICONTROL Raccolte], seleziona una raccolta e fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, seleziona le schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]** per visualizzare i metadati della raccolta.
1. Se necessario, modifica i metadati. Per salvare le modifiche, fai clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti.

## Modifica metadati di più raccolte in blocco {#editing-collection-metadata-in-bulk}

Puoi modificare i metadati di più raccolte contemporaneamente. Questa funzionalità consente di replicare rapidamente i metadati comuni in più raccolte.

1. Nella console Raccolte , seleziona due o più raccolte.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Proprietà]**.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, modifica i metadati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, secondo necessità.
1. Per visualizzare le proprietà dei metadati per una raccolta specifica, annullare la selezione delle raccolte rimanenti nell&#39;elenco delle raccolte. I campi dell’editor di metadati sono compilati con i metadati per la raccolta specifica.

   >[!NOTE]
   >
   >* Nella pagina [!UICONTROL Proprietà], è possibile rimuovere le raccolte dall&#39;elenco delle raccolte annullando la selezione. Nell’elenco delle raccolte sono selezionate tutte le raccolte per impostazione predefinita. [!DNL Experience Manager] non aggiorna i metadati delle raccolte rimosse.
   >* Nella parte superiore dell’elenco, seleziona la casella di controllo accanto a **[!UICONTROL Titolo]** per passare dalla selezione delle raccolte alla cancellazione dell’elenco.


1. Fai clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti, quindi chiudi la finestra di dialogo di conferma.
1. Per aggiungere i nuovi metadati a quelli esistenti, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Fare clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono i metadati precedenti per queste raccolte. Utilizza la modalità [!UICONTROL Aggiungi] per aggiungere nuovi valori ai metadati esistenti nei campi che possono contenere più valori. I campi con valore singolo vengono sempre sovrascritti. Tutti i tag aggiunti nel campo [!UICONTROL Tag] vengono aggiunti all’elenco esistente di tag nei metadati.

Per personalizzare la pagina dei metadati [!UICONTROL Proprietà], inclusa l&#39;aggiunta, la modifica, l&#39;eliminazione delle proprietà dei metadati, utilizza l&#39;editor schema.

>[!TIP]
>
>Il metodo di modifica collettiva funziona per le risorse disponibili in una raccolta. Per le risorse disponibili nelle cartelle o che corrispondono a un criterio comune, è possibile [aggiornare in blocco i metadati dopo la ricerca](/help/assets/search-assets.md#metadataupdates).

## Raccolte di ricerca {#searching-collections}

Puoi cercare le raccolte dalla console Raccolte . Quando esegui una ricerca con parole chiave nella casella Omnisearch, [!DNL Assets] cerca i nomi delle raccolte, i metadati e i tag aggiunti alle raccolte.

Se cerchi raccolte dal livello principale, nei risultati della ricerca vengono restituite solo singole raccolte. [!DNL Assets] Le cartelle o all’interno delle raccolte sono escluse. In tutti gli altri casi (ad esempio, all’interno di una singola raccolta o in una gerarchia di cartelle), vengono restituite tutte le risorse, le cartelle e le raccolte pertinenti.

## Cerca nelle raccolte {#searching-within-collections}

Nella console Raccolte, fai clic su una raccolta per aprirla.

All&#39;interno di una raccolta, la ricerca [!DNL Experience Manager] è limitata alle risorse (e ai relativi tag e metadati) all&#39;interno della raccolta che stai visualizzando. Quando esegui una ricerca all’interno di una cartella, vengono restituite tutte le risorse e le cartelle secondarie corrispondenti all’interno della cartella corrente. Quando esegui una ricerca all’interno di una raccolta, vengono restituite solo le risorse, le cartelle e le altre raccolte corrispondenti ai membri diretti della raccolta.

## Modifica impostazioni raccolta {#editing-collection-settings}

È possibile modificare le impostazioni della raccolta, ad esempio titolo e descrizione, o aggiungere membri a una raccolta.

1. Seleziona una raccolta e fai clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti. In alternativa, utilizza l&#39;azione rapida **[!UICONTROL Impostazioni]** dalla miniatura della raccolta.
1. Nella pagina **[!UICONTROL Impostazioni raccolta]**, puoi modificare le impostazioni della raccolta. Ad esempio, modifica il titolo della raccolta, le descrizioni, i membri e le autorizzazioni, come descritto in [Aggiunta di raccolte](#creating-a-collection).

1. Per salvare le modifiche, fai clic su **[!UICONTROL Salva]**.

## Eliminare una raccolta {#deleting-a-collection}

1. Dalla console Raccolte, seleziona una o più raccolte e fai clic su Elimina nella barra degli strumenti.

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l’eliminazione.

   >[!NOTE]
   >
   >È inoltre possibile eliminare le raccolte avanzate eliminando le ricerche salvate](#saved-searches).[

## Scarica una raccolta {#downloading-a-collection}

Quando scarichi una raccolta, viene scaricata l’intera gerarchia delle risorse all’interno della raccolta, incluse le cartelle e le raccolte secondarie.

1. Dalla console Raccolte , seleziona una o più raccolte da scaricare.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.
1. Nella finestra di dialogo **[!UICONTROL Scarica]**, fai clic su **[!UICONTROL Scarica]**. Se desideri scaricare i rendering delle risorse all’interno della raccolta, seleziona **[!UICONTROL Rendering]**. Seleziona l’opzione **[!UICONTROL E-mail]** per inviare una notifica e-mail al proprietario della raccolta.

   Quando selezioni una raccolta da scaricare, viene scaricata la gerarchia completa delle cartelle sotto la raccolta. Per includere ogni raccolta scaricata (incluse le risorse nelle raccolte secondarie nidificate sotto la raccolta principale) in una singola cartella, seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Creare raccolte nidificate {#creating-nested-collections}

È possibile aggiungere una raccolta a un&#39;altra raccolta, creando in tal modo una raccolta nidificata.

1. Dalla console Raccolte, seleziona la raccolta o il gruppo di raccolte desiderato e fai clic su **[!UICONTROL To Collection]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Aggiungi alla raccolta]**, seleziona la raccolta in cui aggiungere la raccolta.

   >[!NOTE]
   >
   >La raccolta aggiornata più di recente è selezionata per impostazione predefinita nella pagina **[!UICONTROL Aggiungi alla raccolta]** .

1. Fate clic su **[!UICONTROL Aggiungi]**. Un messaggio conferma che la raccolta viene aggiunta alla raccolta di destinazione nella pagina **[!UICONTROL Seleziona destinazione]** . Chiudi il messaggio per completare il processo.

>[!NOTE]
>
>Le raccolte avanzate non possono essere nidificate. In altre parole, le raccolte avanzate non possono contenere altre raccolte.

## Ricerche salvate {#saved-searches}

Nell’interfaccia utente di [!DNL Assets] puoi cercare o filtrare le risorse in base a determinate regole, criteri di ricerca o facet di ricerca personalizzati. Se salvi queste ricerche come **[!UICONTROL Ricerche salvate]**, puoi accedervi in un secondo momento dall’elenco **[!UICONTROL Ricerche salvate]** nel pannello Filtro. La creazione di una ricerca salvata genera anche una raccolta avanzata.

![save_search_list](assets/saved_searches_list.png)

Le ricerche salvate vengono create quando generi una raccolta avanzata. Le raccolte avanzate vengono aggiunte automaticamente all’elenco **[!UICONTROL Ricerche salvate]**. La query [!UICONTROL Ricerche salvate] per la raccolta viene salvata nella proprietà `dam:query` in CRXDE nella posizione relativa `/content/dam/collections/`. Non ci sono limiti alle ricerche che puoi salvare e alle ricerche salvate visualizzate nell’elenco.

>[!NOTE]
>
>Puoi condividere le raccolte avanzate nello stesso modo in cui condividi le raccolte statiche.

La modifica delle ricerche salvate equivale alla modifica delle raccolte avanzate. Per informazioni dettagliate, consulta [modificare una raccolta avanzata](#editing-a-smart-collection).

Per eliminare le ricerche salvate, effettua le seguenti operazioni:

1. Nell&#39;interfaccia utente [!DNL Assets] fare clic su Cerca ![opzione di ricerca](assets/do-not-localize/search_icon.png).
1. Con il cursore nel campo Omnisearch , seleziona il tasto `Return` .
1. Nell’interfaccia [!DNL Experience Manager], apri il pannello Filtri .
1. Nell&#39;elenco **[!UICONTROL Ricerche salvate]**, fai clic su **[!UICONTROL Elimina]** accanto alla raccolta avanzata da eliminare.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per eliminare la ricerca salvata.

## Eseguire un flusso di lavoro su una raccolta {#running-a-workflow-on-a-collection}

Puoi eseguire un flusso di lavoro per le risorse all’interno di una raccolta. Se la raccolta contiene raccolte nidificate, il flusso di lavoro viene eseguito anche sulle risorse all’interno delle raccolte nidificate. Tuttavia, se la raccolta e la raccolta nidificata contengono risorse duplicate, il flusso di lavoro viene eseguito una sola volta per tali risorse.

1. Apri **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**. Per eseguire un flusso di lavoro su una raccolta specifica, selezionalo.
1. Apri la barra **[!UICONTROL Timeline]** . Fai clic su ![chevron su](assets/do-not-localize/chevron-up-icon.png) e fai clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Nella sezione **[!UICONTROL Avvia flusso di lavoro]**, seleziona un modello di flusso di lavoro dall’elenco. Ad esempio, scegli il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Immetti un titolo per il flusso di lavoro e fai clic su **[!UICONTROL Avvia]**.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Procedi]**. Il flusso di lavoro elabora tutte le risorse nella raccolta selezionata.

>[!MORELIKETHIS]
>
>* [Configurare le notifiche e-mail di Experience Manager Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Creare un&#39;attività di revisione per le raccolte](bulk-approval.md)

