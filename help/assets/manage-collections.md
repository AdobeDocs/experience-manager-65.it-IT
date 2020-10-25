---
title: Gestione delle raccolte di risorse digitali
description: Scoprite come gestire le raccolte di risorse, ad esempio creare, visualizzare, eliminare, modificare e scaricare le raccolte.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 11%

---


# Gestire le raccolte {#managing-collections}

Una raccolta è un insieme di risorse all&#39;interno [!DNL Adobe Experience Manager Assets]. Utilizzate le raccolte per condividere le risorse tra gli utenti. Il set può essere una raccolta statica o una raccolta dinamica basata sui risultati di ricerca.

A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Potete condividere le raccolte con vari utenti a cui sono stati assegnati diversi livelli di privilegi, inclusi la visualizzazione, la modifica e così via.

Potete condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L&#39;integrità referenziale delle risorse viene mantenuta tra le raccolte.

Le raccolte sono dei tipi seguenti, in base al modo in cui vengono raccolte le risorse:

* Una raccolta che contiene un elenco di riferimento statico di risorse, cartelle e altre raccolte.

* Una raccolta smart che include dinamicamente risorse basate su criteri di ricerca.

## Accedere alla console delle raccolte {#navigating-the-collections-console}

Per aprire le **[!UICONTROL raccolte]**, nell&#39; [!DNL Experience Manager] interfaccia passate a **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**.

## Creare una raccolta {#creating-a-collection}

Potete creare una raccolta con riferimenti [](#creating-a-collection-with-static-references) statici o in base a un filtro [basato su criteri di](#creating-a-smart-collection)ricerca. Potete anche creare una raccolta da una scatola luminosa.

### Creare una raccolta con riferimenti statici {#creating-a-collection-with-static-references}

Potete creare una raccolta con riferimenti statici, ad esempio una raccolta con riferimenti a risorse, cartelle, raccolte, set 360 gradi e set di immagini.

1. Passate alla console **[!UICONTROL Raccolte]** .
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea raccolta]** , immettete un titolo e una descrizione facoltativa per la raccolta.
1. Aggiungi i membri alla raccolta e assegna le autorizzazioni appropriate. In alternativa, per consentire a tutti gli utenti di accedere alla raccolta, seleziona **[!UICONTROL Raccolta pubblica]**.

   >[!NOTE]
   >
   >Per consentire ai membri di condividere le raccolte con altri utenti, fornite al `dam-users` gruppo le autorizzazioni di lettura nel percorso `home/users`. Consentite agli utenti di `/content/dam/collections` utilizzare la propria posizione per consentire loro di visualizzare le raccolte negli elenchi a comparsa. In alternativa, rendete l’utente parte del `dam-users` gruppo.

1. (Facoltativo) Aggiungete una miniatura per la raccolta.
1. Click **[!UICONTROL Create]**, and then click **[!UICONTROL OK]** to close the dialog. Una raccolta con il titolo e le proprietà specificati viene aperta nella console Raccolte.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] consente di creare attività di revisione per una raccolta in modo simile alle attività di revisione per una cartella di risorse.

   Per aggiungere risorse alla raccolta, passate all&#39;interfaccia [!DNL Assets] utente. Per informazioni dettagliate, consultate [Aggiungere risorse a una raccolta](#adding-assets-to-a-collection).

### Creazione di raccolte tramite dropzone {#create-collections-using-dropzone}

Potete trascinare le risorse dall&#39;interfaccia [!DNL Assets] utente a una raccolta. Potete anche creare una copia di una raccolta e trascinarvi le risorse.

1. Dall&#39;interfaccia [!DNL Assets] utente, selezionate le risorse che desiderate aggiungere a una raccolta.
1. Trascinate le risorse nell&#39;area **[!UICONTROL Rilascia nella raccolta]** . In alternativa, fare clic su **[!UICONTROL Alla raccolta]** dalla barra degli strumenti.

   ![drop_in_collection](assets/drop_in_collection.png)

1. In the **[!UICONTROL Add To Collection]** page, click **[!UICONTROL Create Collection]** from the toolbar.

   If you want to add the assets to an existing collection, select it from the page, and click **[!UICONTROL Add]**. Per impostazione predefinita, è selezionata la raccolta aggiornata più di recente.

1. Nella finestra di dialogo **[!UICONTROL Crea nuova raccolta]**, specifica un nome per la raccolta. Se vuoi che la raccolta sia accessibile a tutti gli utenti, seleziona **[!UICONTROL Raccolta pubblica]**.
1. Fate clic su **[!UICONTROL Continua]** per creare la raccolta.

### Creare una raccolta dinamica {#creating-a-smart-collection}

Una raccolta avanzata utilizza un criterio di ricerca per compilare in modo dinamico le risorse. Potete creare una raccolta avanzata utilizzando solo i file e non le cartelle o i file e le cartelle.

Per creare una raccolta dinamica, effettuate le seguenti operazioni:

1. Passate all’interfaccia [!DNL Assets] utente e fate clic su Cerca.

1. Digitate la parola chiave search nella casella corrispondente e premete `Enter`. Aprite il pannello Filtri e applicate un filtro di ricerca.

1. Dall’elenco **[!UICONTROL File e cartelle]** , selezionare **[!UICONTROL File]**.

   ![files_option](assets/files_option.png)

1. Fate clic su **[!UICONTROL Salva raccolta]** avanzata.

1. Specificate un nome per la raccolta. Selezionate **[!UICONTROL Pubblico]** per aggiungere il gruppo Utenti DAM con il ruolo Visualizzatore alla raccolta avanzata.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se selezionate **[!UICONTROL Pubblico]**, la raccolta smart diventa disponibile per tutti gli utenti con il ruolo di proprietario dopo averlo creato. Se deselezionate l&#39;opzione **[!UICONTROL Pubblica]** , il gruppo di utenti DAM non è più associato alla raccolta avanzata.

1. Click **[!UICONTROL Save]** to create the smart collection, and then close the message box to complete the process.

   The new smart collection is also added to the **[!UICONTROL Saved Searches]** list.

   ![collection_list](assets/collection_listing.png)

   The label of the **[!UICONTROL Create Smart Selection]** option changes to **[!UICONTROL Edit Smart Selection]**. Per modificare le impostazioni della raccolta avanzata, seleziona **[!UICONTROL File]** dall’elenco **[!UICONTROL File e cartelle]**. Fate clic sull&#39;opzione **[!UICONTROL Modifica selezione]** avanzata per ![modificare la raccolta](assets/do-not-localize/edit-smart-collection.png) dinamica.

## Aggiunta di risorse a una raccolta {#adding-assets-to-a-collection}

Potete aggiungere risorse a una raccolta contenente un elenco di risorse o cartelle a cui viene fatto riferimento. Le raccolte dinamiche utilizzano una query di ricerca per compilare le risorse. Pertanto, non è possibile applicare riferimenti statici a risorse e cartelle.

1. Nell&#39;interfaccia utente delle [!DNL A]risorse, selezionate la risorsa e fate clic su **[!UICONTROL Alla raccolta]** da ![aggiungere alla raccolta](assets/do-not-localize/add-to-collection.png) dalla barra degli strumenti.
In alternativa, puoi trascinare la risorsa nell&#39;area **[!UICONTROL Rilascia nella raccolta]** dell&#39;interfaccia. Aggiungete le risorse quando l&#39;etichetta della regione diventa **[!UICONTROL Rilascia in Aggiungi]**.

1. Nella pagina **[!UICONTROL Aggiungi alla raccolta]** , selezionate la raccolta alla quale desiderate aggiungere la risorsa.

1. Fate clic su **[!UICONTROL Aggiungi]**, quindi chiudete il messaggio di conferma. La risorsa viene aggiunta alla raccolta.

## Modificare una raccolta smart {#editing-a-smart-collection}

Le raccolte intelligenti vengono create salvando una ricerca in modo da modificarne il contenuto modificando i parametri di ricerca della ricerca [](#saved-searches)salvata.

1. Nell’interfaccia [!DNL Assets] utente, fare clic sull’opzione di ![ricerca nella barra degli strumenti](assets/do-not-localize/search_icon.png) .
1. Con il cursore nella casella Omnisearch, premere il tasto Invio.
1. Nell’ [!DNL Experience Manager] interfaccia, aprire il pannello Filtri.
1. Dall’elenco **[!UICONTROL Ricerche salvate]**, seleziona la raccolta avanzata da modificare. Nel pannello Ricerca sono visualizzati i filtri configurati per la ricerca salvata.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Dall’elenco **[!UICONTROL File e cartelle]** , selezionare **[!UICONTROL File]**.
1. Modificate uno o più filtri, a seconda delle necessità. Fate clic su **[!UICONTROL Modifica raccolta]** avanzata.

   Potete anche modificare il nome della raccolta dinamica.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. Fai clic su **[!UICONTROL Salva]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica raccolta]** avanzata.
1. Fate clic su **[!UICONTROL Sovrascrivi]** per sostituire la raccolta avanzata originale con la raccolta modificata. In alternativa, selezionate **[!UICONTROL Salva con nome]** per salvare separatamente la raccolta modificata.
1. Nella finestra di dialogo di conferma, fate clic su **[!UICONTROL Salva]** per completare il processo.

## Visualizzare e modificare i metadati della raccolta {#view-edit-collection-metadata}

I metadati della raccolta includono i dati sulla raccolta, compresi eventuali tag aggiunti.

1. Dalla console [!UICONTROL Raccolte] , selezionate una raccolta e fate clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, seleziona le schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]** per visualizzare i metadati della raccolta.
1. Modificate i metadati in base alle esigenze. Per salvare le modifiche, fate clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti.

## Modificare i metadati di più raccolte in blocco {#editing-collection-metadata-in-bulk}

Potete modificare i metadati di più raccolte contemporaneamente. Questa funzionalità consente di replicare rapidamente i metadati comuni in più raccolte.

1. Nella console Raccolte, selezionate due o più raccolte.
1. Dalla barra degli strumenti, fare clic su **[!UICONTROL Proprietà]**.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, modifica i metadati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, secondo necessità.
1. Per visualizzare le proprietà dei metadati per una raccolta specifica, deselezionate le raccolte rimanenti nell&#39;elenco delle raccolte. I campi dell&#39;editor di metadati vengono compilati con i metadati per la raccolta specifica.

   >[!NOTE]
   >
   >* Nella pagina [!UICONTROL Proprietà] , potete rimuovere le raccolte dall&#39;elenco delle raccolte deselezionandole. L&#39;elenco delle raccolte include tutte le raccolte selezionate per impostazione predefinita. [!DNL Experience Manager] non aggiorna i metadati delle raccolte che rimuovete.
   >* Nella parte superiore dell&#39;elenco, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle raccolte e la cancellazione dell&#39;elenco.


1. Fare clic su **[!UICONTROL Salva e chiudi]** nella barra degli strumenti, quindi chiudere la finestra di dialogo di conferma.
1. To append the new metadata with the existing metadata, select **[!UICONTROL Append mode]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Fate clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono i metadati precedenti per queste raccolte. Utilizzate la modalità  Aggiungi per aggiungere nuovi valori ai metadati esistenti nei campi che possono contenere più valori. I campi con valore singolo vengono sempre sovrascritti. Eventuali tag aggiunti nel campo [!UICONTROL Tag] vengono aggiunti all’elenco esistente di tag presenti nei metadati.

Per personalizzare la pagina [!UICONTROL Proprietà] metadati, compresa l&#39;aggiunta, la modifica, l&#39;eliminazione delle proprietà dei metadati, utilizzare l&#39;Editor schema.

>[!TIP]
>
>Il metodo di modifica collettiva funziona per le risorse disponibili in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è possibile aggiornare [in massa i metadati dopo la ricerca](/help/assets/search-assets.md#metadataupdates).

## Cerca raccolte {#searching-collections}

Potete cercare le raccolte dalla console Raccolte. Quando eseguite una ricerca con le parole chiave nella casella di ricerca Omnico, [!DNL Assets] cerca i nomi delle raccolte, i metadati e i tag aggiunti alle raccolte.

Se cercate raccolte dal livello principale, nei risultati della ricerca vengono restituite solo singole raccolte. [!DNL Assets] o le cartelle all&#39;interno delle raccolte sono escluse. In tutti gli altri casi (ad esempio, all&#39;interno di una singola raccolta o in una gerarchia di cartelle), vengono restituite tutte le risorse, le cartelle e le raccolte pertinenti.

## Cerca nelle raccolte {#searching-within-collections}

Nella console Raccolte, fate clic su una raccolta per aprirla.

All&#39;interno di una raccolta, la [!DNL Experience Manager] ricerca è limitata alle risorse (e ai relativi tag e metadati) all&#39;interno della raccolta che state visualizzando. Quando eseguite una ricerca all’interno di una cartella, vengono restituite tutte le risorse e le cartelle figlie corrispondenti all’interno della cartella corrente. Quando eseguite una ricerca all&#39;interno di una raccolta, vengono restituite solo le risorse, le cartelle e altre raccolte corrispondenti a membri diretti della raccolta.

## Modifica delle impostazioni della raccolta {#editing-collection-settings}

Potete modificare le impostazioni della raccolta, ad esempio titolo e descrizione, o aggiungere membri a una raccolta.

1. Selezionate una raccolta e fate clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti. In alternativa, utilizzate l&#39;azione rapida **[!UICONTROL Impostazioni]** dalla miniatura della raccolta.
1. Nella pagina **[!UICONTROL Impostazioni raccolta]**, puoi modificare le impostazioni della raccolta. For example, modify the collection title, descriptions, members, and permissions as discussed in [Adding Collections](#creating-a-collection).

1. Per salvare le modifiche, fate clic su **[!UICONTROL Salva]**.

## Eliminare una raccolta {#deleting-a-collection}

1. Dalla console Raccolte, selezionate una o più raccolte e fate clic su Elimina dalla barra degli strumenti.

1. Nella finestra di dialogo, fare clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione.

   >[!NOTE]
   >
   >Potete inoltre eliminare le raccolte avanzate [eliminando le ricerche](#saved-searches)salvate.

## Scaricare una raccolta {#downloading-a-collection}

Quando scaricate una raccolta, viene scaricata l&#39;intera gerarchia di risorse all&#39;interno della raccolta, comprese le cartelle e le raccolte figlie.

1. Dalla console Raccolte, selezionate una o più raccolte da scaricare.
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Scarica]**.
1. Nella finestra di dialogo **[!UICONTROL Scarica]** , fate clic su **[!UICONTROL Scarica]**. Se desiderate scaricare i rendering delle risorse all&#39;interno della raccolta, selezionate **[!UICONTROL Rendering]**. Selezionate l&#39;opzione **[!UICONTROL E-mail]** per inviare una notifica e-mail al proprietario della raccolta.

   Quando selezionate una raccolta da scaricare, viene scaricata l&#39;intera gerarchia di cartelle sotto la raccolta. Per includere ciascuna raccolta scaricata (comprese le risorse nelle raccolte figlie nidificate sotto la raccolta principale) in una singola cartella, selezionate **[!UICONTROL Crea cartella separata per ciascuna risorsa]**.

## Creare raccolte nidificate {#creating-nested-collections}

Potete aggiungere una raccolta a un&#39;altra raccolta, creando in tal modo una raccolta nidificata.

1. Dalla console Raccolte, selezionate la raccolta o il gruppo di raccolte desiderato, quindi fate clic su **[!UICONTROL Alla raccolta]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Aggiungi alla raccolta]** , selezionate la raccolta in cui aggiungere la raccolta.

   >[!NOTE]
   >
   >La raccolta aggiornata più di recente è selezionata per impostazione predefinita nella pagina **[!UICONTROL Aggiungi alla raccolta]** .

1. Fate clic su **[!UICONTROL Aggiungi]**. Un messaggio conferma che la raccolta viene aggiunta alla raccolta di destinazione nella pagina **[!UICONTROL Seleziona destinazione]** . Chiudi il messaggio per completare il processo.

>[!NOTE]
>
>Le raccolte avanzate non possono essere nidificate. In altre parole, le raccolte avanzate non possono contenere altre raccolte.

## Ricerche salvate {#saved-searches}

In the [!DNL Assets] user interface, you can search or filter assets based on certain rules, search criteria, or custom search facets. Se salvi queste ricerche come **[!UICONTROL Ricerche salvate]**, puoi accedervi in un secondo momento dall’elenco **[!UICONTROL Ricerche salvate]** nel pannello Filtro. La creazione di una ricerca salvata genera anche una raccolta avanzata.

![saved_Search_list](assets/saved_searches_list.png)

Le ricerche salvate vengono create quando generi una raccolta avanzata. Le raccolte avanzate vengono aggiunte automaticamente all’elenco **[!UICONTROL Ricerche salvate]**. The [!UICONTROL Saved Searches] query for the collection is saved in the `dam:query` property in CRXDE at the relative location `/content/dam/collections/`. Non ci sono limiti alle ricerche che puoi salvare e alle ricerche salvate visualizzate nell&#39;elenco.

>[!NOTE]
>
>Potete condividere le raccolte smart nello stesso modo in cui condividete le raccolte statiche.

La modifica delle ricerche salvate equivale alla modifica delle raccolte avanzate. Per informazioni dettagliate, consultate [Modificare una raccolta](#editing-a-smart-collection)dinamica.

Per eliminare le ricerche salvate, effettuate le seguenti operazioni:

1. Nell’interfaccia [!DNL Assets] utente, fate clic sull’opzione ![di](assets/do-not-localize/search_icon.png)ricerca.
1. Con il cursore nel campo Omnisearch, premere il tasto Invio.
1. Nell’ [!DNL Experience Manager] interfaccia, aprire il pannello Filtri.
1. From the **[!UICONTROL Saved Searches]** list, click **[!UICONTROL Delete]** next to the smart collection that you want to delete.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Nella finestra di dialogo, fate clic su **[!UICONTROL Elimina]** per eliminare la ricerca salvata.

## Esecuzione di un flusso di lavoro su una raccolta {#running-a-workflow-on-a-collection}

Potete eseguire un flusso di lavoro per le risorse all&#39;interno di una raccolta. Se la raccolta contiene raccolte nidificate, il flusso di lavoro viene eseguito anche sulle risorse all&#39;interno delle raccolte nidificate. Tuttavia, se la raccolta e la raccolta nidificata contengono risorse duplicate, il flusso di lavoro viene eseguito una sola volta per tali risorse.

1. Aprite **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**. Per eseguire un flusso di lavoro su una raccolta specifica, selezionatelo.
1. Open **[!UICONTROL Timeline]** rail. Fate clic ![sulla freccia verso l’alto](assets/do-not-localize/chevron-up-icon.png) e fate clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Nella sezione **[!UICONTROL Avvia flusso di lavoro]**, seleziona un modello di flusso di lavoro dall’elenco. Ad esempio, scegli il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Inserite un titolo per il flusso di lavoro e fate clic su **[!UICONTROL Avvia]**.
1. In the dialog, click **[!UICONTROL Proceed]**. Il flusso di lavoro elabora tutte le risorse nella raccolta selezionata.

>[!MORELIKETHIS]
>
>* [Configurare  notifiche e-mail di Risorse Experience Manager](/help/sites-administering/notification.md#assetsconfig)
>* [Creazione di un&#39;attività di revisione per le raccolte](bulk-approval.md)

