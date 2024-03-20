---
title: Gestire le raccolte di risorse digitali
description: Scopri le attività per gestire le raccolte di risorse, ad esempio creare, visualizzare, eliminare, modificare e scaricare le raccolte.
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 14%

---

# Gestire le raccolte {#managing-collections}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=en) |
| AEM 6.5 | Questo articolo |

Una raccolta è un set di risorse all’interno di [!DNL Adobe Experience Manager Assets]. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti. Il set può essere una raccolta statica o dinamica basata sui risultati della ricerca.

A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse. Puoi condividere raccolte con vari utenti a cui sono assegnati livelli diversi di privilegi, tra cui visualizzazione, modifica e così via.

Puoi condividere più raccolte con un utente. Ogni raccolta contiene riferimenti alle risorse. L’integrità dei riferimenti alle risorse viene mantenuta tra le varie raccolte.

Le raccolte sono dei seguenti tipi, in base al modo in cui raccolgono le risorse:

* Una raccolta che contiene un elenco di riferimento statico di risorse, cartelle e altre raccolte.

* Una raccolta avanzata che include dinamicamente le risorse in base a un criterio di ricerca.

## Accedere alla console delle raccolte {#navigating-the-collections-console}

Per aprire **[!UICONTROL Raccolte]**, nella [!DNL Experience Manager] , vai a **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**.

## Creare una raccolta {#creating-a-collection}

Puoi creare una raccolta con [riferimenti statici](#creating-a-collection-with-static-references) o in base a [filtro basato su criteri di ricerca](#creating-a-smart-collection). Puoi anche creare una raccolta da un lightbox.

### Creare una raccolta con riferimenti statici {#creating-a-collection-with-static-references}

Puoi creare una raccolta con riferimenti statici, ad esempio una raccolta con riferimenti a risorse, cartelle, raccolte, set 360 gradi e set di immagini.

1. Accedi a **[!UICONTROL Raccolte]** console.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea raccolta]** , immetti un titolo e una descrizione facoltativa per la raccolta.
1. Aggiungi i membri alla raccolta e assegna le autorizzazioni appropriate. In alternativa, per consentire a tutti gli utenti di accedere alla raccolta, seleziona **[!UICONTROL Raccolta pubblica]**.

   >[!NOTE]
   >
   >Per consentire ai membri di condividere raccolte con altri utenti, specificare `dam-users` autorizzazioni di lettura di gruppo nel percorso `home/users`. Concedi l’autorizzazione agli utenti in `/content/dam/collections` per consentire agli utenti di visualizzare le raccolte negli elenchi a comparsa. In alternativa, rendi l’utente parte di `dam-users` gruppo.

1. (Facoltativo) Aggiungi una miniatura per la raccolta.
1. Clic **[!UICONTROL Crea]** e quindi fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo Una raccolta con il titolo e le proprietà specificati viene aperta nella console Raccolte.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] consente di creare attività di revisione per una raccolta in modo analogo a come si creano le attività di revisione per una cartella risorse.

   Per aggiungere risorse alla raccolta, passa alla [!DNL Assets] dell&#39;utente. Per ulteriori informazioni, consulta [Aggiungere risorse a una raccolta](#adding-assets-to-a-collection).

### Creare raccolte tramite dropzone {#create-collections-using-dropzone}

Puoi trascinare le risorse da [!DNL Assets] interfaccia utente di una raccolta. Puoi anche creare una copia di una raccolta e trascinarvi le risorse.

1. Dalla sezione [!DNL Assets] nell&#39;interfaccia utente, seleziona le risorse da aggiungere a una raccolta.
1. Trascina le risorse in **[!UICONTROL Rilascia in raccolta]** zona. In alternativa, fare clic su **[!UICONTROL Alla raccolta]** dalla barra degli strumenti.

   ![drop_in_collection](assets/drop_in_collection.png)

1. In **[!UICONTROL Aggiungi a raccolta]** pagina, fai clic su **[!UICONTROL Crea raccolta]** dalla barra degli strumenti.

   Se desideri aggiungere le risorse a una raccolta esistente, selezionala dalla pagina e fai clic su **[!UICONTROL Aggiungi]**. Per impostazione predefinita, è selezionata la raccolta aggiornata più di recente.

1. Nella finestra di dialogo **[!UICONTROL Crea nuova raccolta]**, specifica un nome per la raccolta. Se vuoi che la raccolta sia accessibile a tutti gli utenti, seleziona **[!UICONTROL Raccolta pubblica]**.
1. Clic **[!UICONTROL Continua]** per creare la raccolta.

### Creare una raccolta avanzata {#creating-a-smart-collection}

Una raccolta avanzata utilizza un criterio di ricerca per popolare dinamicamente le risorse. Puoi creare una raccolta avanzata utilizzando solo file e non cartelle o file e cartelle.

Per creare una raccolta avanzata, effettua le seguenti operazioni:

1. Accedi a [!DNL Assets] e fare clic su cerca.

1. Digita la parola chiave di ricerca nella casella Omnisearch e seleziona `Enter`. Apri il pannello Filtri e applica un filtro di ricerca.

1. Dalla sezione **[!UICONTROL File e cartelle]** elenco, seleziona **[!UICONTROL File]**.

   ![files_option](assets/files_option.png)

1. Clic **[!UICONTROL Salva raccolta avanzata]**.

1. Specifica un nome per la raccolta. Seleziona **[!UICONTROL Pubblico]** per aggiungere il gruppo Utenti DAM con il ruolo Visualizzatore alla raccolta avanzata.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se si seleziona **[!UICONTROL Pubblico]**, la raccolta avanzata diventa disponibile per tutti coloro che hanno il ruolo di proprietario dopo che è stata creata. Se si annulla la **[!UICONTROL Pubblico]** , il gruppo utenti DAM non è più associato alla raccolta avanzata.

1. Clic **[!UICONTROL Salva]** per creare la raccolta avanzata, quindi chiudere la finestra di messaggio per completare il processo.

   La nuova raccolta avanzata viene aggiunta anche al **[!UICONTROL Ricerche salvate]** elenco.

   ![elenco_raccolte](assets/collection_listing.png)

   Etichetta del **[!UICONTROL Crea selezione avanzata]** l’opzione diventa **[!UICONTROL Modifica selezione avanzata]**. Per modificare le impostazioni della raccolta avanzata, seleziona **[!UICONTROL File]** dall’elenco **[!UICONTROL File e cartelle]**. Fai clic su **[!UICONTROL Modifica selezione avanzata]** ![modifica raccolta avanzata](assets/do-not-localize/edit-smart-collection.png) opzione.

## Aggiungere risorse a una raccolta {#adding-assets-to-a-collection}

Puoi aggiungere risorse a una raccolta che contiene un elenco di risorse o cartelle a cui si fa riferimento. Le raccolte avanzate utilizzano una query di ricerca per compilare le risorse. Pertanto, i riferimenti statici a risorse e cartelle non sono ad esse applicabili.

1. In [!DNL A]interfaccia utente di Assets, seleziona la risorsa e fai clic su **[!UICONTROL Alla raccolta]** ![aggiungi a raccolta](assets/do-not-localize/add-to-collection.png) dalla barra degli strumenti.
In alternativa, puoi trascinare la risorsa sul **[!UICONTROL Rilascia in raccolta]** nell&#39;interfaccia. Aggiungi le risorse quando l’etichetta dell’area cambia in **[!UICONTROL Rilascia per aggiungere]**.

1. In **[!UICONTROL Aggiungi a raccolta]** , seleziona la raccolta a cui desideri aggiungere la risorsa.

1. Clic **[!UICONTROL Aggiungi]**, quindi chiudere il messaggio di conferma. La risorsa viene aggiunta alla raccolta.

## Modificare una raccolta avanzata {#editing-a-smart-collection}

Le raccolte avanzate vengono create salvando una ricerca in modo da poterne modificare il contenuto modificando i parametri di ricerca della [ricerca salvata](#saved-searches).

1. In [!DNL Assets] interfaccia utente, fai clic sull’opzione di ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png) dalla barra degli strumenti.
1. Con il cursore nella casella Omnisearch, selezionate la `Return` chiave.
1. In [!DNL Experience Manager] , aprire il pannello Filtri.
1. Dall’elenco **[!UICONTROL Ricerche salvate]**, seleziona la raccolta avanzata da modificare. Nel pannello Ricerca sono visualizzati i filtri configurati per la ricerca salvata.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Dalla sezione **[!UICONTROL File e cartelle]** elenco, seleziona **[!UICONTROL File]**.
1. Modifica uno o più filtri, a seconda delle necessità. Fai clic su **[!UICONTROL Modifica raccolta avanzata]**.

   Puoi anche modificare il nome della raccolta avanzata.

   ![finestra di dialogo edit_smart_collection](assets/edit_smart_collectiondialog.png)

1. Fai clic su **[!UICONTROL Salva]**. Il **[!UICONTROL Modifica raccolta avanzata]** viene visualizzata.
1. Clic **[!UICONTROL Sovrascrivere]** per sostituire la raccolta avanzata originale con la raccolta modificata. In alternativa, seleziona **[!UICONTROL Salva con nome]** per salvare separatamente la raccolta modificata.
1. Nella finestra di conferma, fai clic su **[!UICONTROL Salva]** per completare il processo.

## Visualizzare e modificare i metadati di una raccolta {#view-edit-collection-metadata}

I metadati della raccolta includono i dati sulla raccolta, inclusi eventuali tag aggiunti.

1. Dalla sezione [!UICONTROL Raccolte] , seleziona una raccolta e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, seleziona le schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]** per visualizzare i metadati della raccolta.
1. Se necessario, modifica i metadati. Per salvare le modifiche, fai clic su **[!UICONTROL Salva e chiudi]** dalla barra degli strumenti.

## Modificare in blocco i metadati di più raccolte {#editing-collection-metadata-in-bulk}

Puoi modificare i metadati di più raccolte contemporaneamente. Questa funzionalità consente di replicare rapidamente i metadati comuni in più raccolte.

1. Nella console Raccolte, seleziona due o più raccolte.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Proprietà]**.
1. Nella pagina **[!UICONTROL Metadati raccolta]**, modifica i metadati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, secondo necessità.
1. Per visualizzare le proprietà dei metadati per una raccolta specifica, annulla la selezione delle raccolte rimanenti nell’elenco delle raccolte. I campi dell’editor di metadati vengono compilati con i metadati di una determinata raccolta.

   >[!NOTE]
   >
   >* In [!UICONTROL Proprietà] pagina, puoi rimuovere le raccolte dall’elenco annullando la selezione. Per impostazione predefinita, nell&#39;elenco delle raccolte sono selezionate tutte le raccolte. [!DNL Experience Manager] non aggiorna i metadati delle raccolte rimosse.
   >* Nella parte superiore dell&#39;elenco selezionare la casella di controllo accanto a **[!UICONTROL Titolo]** per passare dalla selezione delle raccolte alla cancellazione dell’elenco.

1. Clic **[!UICONTROL Salva e chiudi]** dalla barra degli strumenti, quindi chiudi la finestra di dialogo di conferma.
1. Per aggiungere i nuovi metadati a quelli esistenti, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Fai clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >I metadati aggiunti per le raccolte selezionate sovrascrivono quelli precedenti per queste raccolte. Utilizza il [!UICONTROL Modalità di aggiunta] per aggiungere nuovi valori ai metadati esistenti nei campi che possono contenere più valori. I campi con valore singolo vengono sempre sovrascritti. Tutti i tag aggiunti in [!UICONTROL Tag] , sono aggiunti all&#39;elenco esistente di tag nei metadati.

Per personalizzare i metadati [!UICONTROL Proprietà] , incluse l’aggiunta, la modifica e l’eliminazione delle proprietà dei metadati, utilizza l’editor di schema.

>[!TIP]
>
>Il metodo di modifica in blocco funziona per le risorse disponibili in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a un criterio comune, è possibile: [aggiorna in blocco i metadati dopo la ricerca](/help/assets/search-assets.md#metadataupdates).

## Cerca raccolte {#searching-collections}

Puoi cercare le raccolte dalla console Raccolte. Quando si esegue una ricerca con parole chiave nella casella Omnisearch, [!DNL Assets] cerca i nomi delle raccolte, i metadati e i tag aggiunti alle raccolte.

Se cerchi raccolte dal livello principale, nei risultati della ricerca vengono restituite solo singole raccolte. [!DNL Assets] Le cartelle o all’interno delle raccolte sono escluse. In tutti gli altri casi (ad esempio, all’interno di una singola raccolta o di una gerarchia di cartelle), vengono restituite tutte le risorse, le cartelle e le raccolte pertinenti.

## Cerca nelle raccolte {#searching-within-collections}

Nella console Raccolte, fai clic su una raccolta per aprirla.

All’interno di una raccolta, [!DNL Experience Manager] la ricerca è limitata alle risorse (con i relativi tag e metadati) all’interno della raccolta che stai visualizzando. Quando esegui una ricerca all’interno di una cartella, vengono restituite tutte le risorse e le cartelle secondarie corrispondenti nella cartella corrente. Quando esegui una ricerca all’interno di una raccolta, vengono restituite solo le risorse, le cartelle e le altre raccolte corrispondenti che sono membri diretti della raccolta.

## Modifica impostazioni raccolta {#editing-collection-settings}

È possibile modificare le impostazioni della raccolta, ad esempio titolo e descrizione, oppure aggiungere membri a una raccolta.

1. Seleziona una raccolta e fai clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti. In alternativa, utilizza **[!UICONTROL Impostazioni]** azione rapida dalla miniatura della raccolta.
1. Nella pagina **[!UICONTROL Impostazioni raccolta]**, puoi modificare le impostazioni della raccolta. Ad esempio, modifica il titolo della raccolta, le descrizioni, i membri e le autorizzazioni, come descritto in [Aggiunta di raccolte](#creating-a-collection).

1. Per salvare le modifiche, fai clic su **[!UICONTROL Salva]**.

## Eliminare una raccolta {#deleting-a-collection}

1. Dalla console Raccolte, seleziona una o più raccolte e fai clic su Elimina nella barra degli strumenti.

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l’azione elimina.

   >[!NOTE]
   >
   >Puoi anche eliminare le raccolte avanzate con [eliminazione di ricerche salvate](#saved-searches).

## Scaricare una raccolta {#downloading-a-collection}

Quando si scarica una raccolta, viene scaricata l’intera gerarchia di risorse all’interno della raccolta, incluse le cartelle e le raccolte secondarie.

1. Dalla console Raccolte, seleziona una o più raccolte da scaricare.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.
1. In **[!UICONTROL Scarica]** , fai clic su **[!UICONTROL Scarica]**. Per scaricare le rappresentazioni delle risorse all’interno della raccolta, seleziona **[!UICONTROL Rappresentazioni]**. Seleziona la **[!UICONTROL E-mail]** opzione per inviare una notifica e-mail al proprietario della raccolta.

   Quando selezioni una raccolta da scaricare, viene scaricata l’intera gerarchia di cartelle sotto la raccolta. Per includere in una singola cartella ogni raccolta scaricata (comprese le risorse nelle raccolte secondarie nidificate nella raccolta principale), seleziona **[!UICONTROL Crea una cartella separata per ogni risorsa]**.

## Creare raccolte nidificate {#creating-nested-collections}

È possibile aggiungere una raccolta a un&#39;altra raccolta per creare una raccolta nidificata.

1. Dalla console Raccolte, seleziona la raccolta o il gruppo di raccolte desiderato e fai clic su **[!UICONTROL Alla raccolta]** nella barra degli strumenti.

1. Dalla sezione **[!UICONTROL Aggiungi a raccolta]** , seleziona la raccolta in cui aggiungere la raccolta.

   >[!NOTE]
   >
   >La raccolta aggiornata più di recente è selezionata per impostazione predefinita nel **[!UICONTROL Aggiungi a raccolta]** pagina.

1. Clic **[!UICONTROL Aggiungi]**. Un messaggio conferma che la raccolta viene aggiunta alla raccolta di destinazione nel **[!UICONTROL Seleziona destinazione]** pagina. Chiudi il messaggio per completare il processo.

>[!NOTE]
>
>Le raccolte avanzate non possono essere nidificate. In altre parole, le raccolte avanzate non possono contenere altri insiemi.

## Ricerche salvate {#saved-searches}

In [!DNL Assets] interfaccia utente, puoi cercare o filtrare le risorse in base a determinate regole, criteri di ricerca o facet di ricerca personalizzata. Se salvi queste ricerche come **[!UICONTROL Ricerche salvate]**, puoi accedervi in un secondo momento dall’elenco **[!UICONTROL Ricerche salvate]** nel pannello Filtro. La creazione di una ricerca salvata genera anche una raccolta avanzata.

![elenco_ricerche_salvate](assets/saved_searches_list.png)

Le ricerche salvate vengono create quando generi una raccolta avanzata. Le raccolte avanzate vengono aggiunte automaticamente all’elenco **[!UICONTROL Ricerche salvate]**. Il [!UICONTROL Ricerche salvate] la query per la raccolta viene salvata in `dam:query` proprietà in CRXDE nella posizione relativa `/content/dam/collections/`. Non esistono limiti alle ricerche che è possibile salvare e alle ricerche salvate visualizzate nell&#39;elenco.

>[!NOTE]
>
>Puoi condividere le raccolte avanzate nello stesso modo in cui condividi le raccolte statiche.

La modifica delle ricerche salvate equivale alla modifica delle raccolte avanzate. Per ulteriori informazioni, consulta [modificare una raccolta avanzata](#editing-a-smart-collection).

Per eliminare le ricerche salvate, eseguire la procedura seguente:

1. In [!DNL Assets] interfaccia utente, fare clic su ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png).
1. Con il cursore nel campo Omnisearch, seleziona la `Return` chiave.
1. In [!DNL Experience Manager] , aprire il pannello Filtri.
1. Dalla sezione **[!UICONTROL Ricerche salvate]** , fare clic su **[!UICONTROL Elimina]** accanto alla raccolta avanzata da eliminare.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per eliminare la ricerca salvata.

## Eseguire un flusso di lavoro su una raccolta {#running-a-workflow-on-a-collection}

Puoi eseguire un flusso di lavoro per le risorse all’interno di una raccolta. Se la raccolta contiene raccolte nidificate, il flusso di lavoro viene eseguito anche sulle risorse all’interno delle raccolte nidificate. Tuttavia, se la raccolta e la raccolta nidificata contengono risorse duplicate, il flusso di lavoro viene eseguito una sola volta per tali risorse.

1. Apri **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**. Per eseguire un flusso di lavoro su una raccolta specifica, selezionala.
1. Apri **[!UICONTROL Timeline]** barra. Clic ![freccia su](assets/do-not-localize/chevron-up-icon.png) e fai clic su **[!UICONTROL Avvia flusso di lavoro]**.
1. Nella sezione **[!UICONTROL Avvia flusso di lavoro]**, seleziona un modello di flusso di lavoro dall’elenco. Ad esempio, scegli il modello **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Inserisci un titolo per il flusso di lavoro e fai clic su **[!UICONTROL Inizio]**.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Procedi]**. Il flusso di lavoro elabora tutte le risorse nella raccolta selezionata.

>[!MORELIKETHIS]
>
>* [Configurare le notifiche e-mail di Experience Manager Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Creare un&#39;attività di revisione per le raccolte](bulk-approval.md)
