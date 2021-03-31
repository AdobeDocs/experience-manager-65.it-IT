---
title: Creare progetti di traduzione
description: Scopri come creare progetti di traduzione in [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architetto, amministratore
feature: Traduzione
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 18%

---


# Creare progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attiva uno dei seguenti flussi di lavoro di copia per lingua disponibili nella barra Riferimenti nell’ interfaccia utente [!DNL Experience Manager] .

* **Crea e traduce**: In questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. Inoltre, a seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti . A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

* **Aggiorna copie** della lingua: Esegui questo flusso di lavoro per tradurre un gruppo aggiuntivo di risorse e includerlo in una copia per lingua per una specifica impostazione internazionale. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza.

>[!PREREQUISITES]
>
>* Gli utenti che creano progetti di traduzione sono membri del gruppo `projects-administrators`.
>* Il provider di servizi di traduzione supporta la traduzione di file binari.


## Creare e tradurre un flusso di lavoro {#create-and-translate-workflow}

Utilizza il flusso di lavoro Crea e traduci per generare copie per lingua per una particolare lingua per la prima volta. Il flusso di lavoro fornisce le seguenti opzioni:

* Crea solo struttura.
* Crea un nuovo progetto di traduzione.
* Aggiungi a progetto di traduzione esistente.

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **[!UICONTROL Crea solo struttura]** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell&#39;interfaccia [!DNL Assets], selezionare la cartella di origine per la quale si desidera creare una struttura nella directory principale della lingua di destinazione.

1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.

   ![Copie per lingua](assets/translation-language-copies.png)

1. Fai clic su **[!UICONTROL Crea e traduci]**. Dall’elenco **[!UICONTROL Lingue di destinazione]**, seleziona la lingua per la quale vuoi creare una struttura di cartelle.

1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.

1. Fai clic su **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in **[!UICONTROL Copie per lingua]**.

   ![copie per lingua](assets/lang-copy2.png)

1. Fai clic sulla struttura dall’elenco, quindi fai clic su **[!UICONTROL Mostra in Assets]** per accedere alla struttura delle cartelle nella lingua di destinazione.

   ![rivelare le risorse](assets/reveal-in-assets.png)

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project}

Se utilizzi questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. A seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti . A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o viene eseguito automaticamente non appena viene creato il progetto di traduzione.

1. Nell&#39;interfaccia utente [!DNL Assets], selezionare la cartella di origine per la quale si desidera creare una copia in lingua.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Fai clic su **[!UICONTROL Crea e traduci]** in basso.

1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Crea un nuovo progetto di traduzione]**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Fai clic su **[!UICONTROL Crea]**. [!DNL Assets] dalla cartella di origine vengono copiati nelle cartelle di destinazione per le impostazioni internazionali selezionate al passaggio 4.

   ![copie per lingua](assets/lang-copy2.png)

1. Per passare alla cartella, seleziona la copia per lingua e fai clic su **[!UICONTROL Mostra in Assets]**.

   ![rivelare le risorse](assets/reveal-in-assets.png)

1. Passa alla console Progetti . La cartella di traduzione viene copiata nella console Progetti .

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Apri la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Fai clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Per visualizzare lo stato del lavoro di traduzione, fai clic sull&#39;ellissi nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** .

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Per ulteriori dettagli sugli stati dei processi, consulta [Monitoraggio dello stato di un processo di traduzione](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Passa all’interfaccia utente [!DNL Assets] e apri la pagina [!UICONTROL Proprietà] per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

   ![visualizzare i metadati tradotti nella pagina Proprietà della risorsa](assets/translated-metadata-asset-properties.png)

   *Figura: Metadati tradotti nella pagina delle proprietà della risorsa.*

   >[!NOTE]
   >
   >Questa funzione è disponibile sia per le risorse che per le cartelle. Quando una risorsa viene selezionata al posto di una cartella, l’intera gerarchia di cartelle fino alla directory principale lingua viene copiata per creare una copia per la lingua della risorsa.

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project}

Se utilizzi questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo aver eseguito un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell’interfaccia utente di [!DNL Assets] , accedi alla cartella di origine contenente le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Fai clic su **[!UICONTROL Crea e traduci]** in basso.

1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.

1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.

   >[!NOTE]
   >
   >Se scegli l’opzione **[!UICONTROL Aggiungi al progetto di traduzione esistente]**, il progetto di traduzione viene aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente alle impostazioni del progetto preesistente. In caso contrario, viene creato un nuovo progetto.

1. Dall’elenco **[!UICONTROL Progetto di traduzione esistente]** , seleziona un progetto per aggiungere la risorsa da tradurre.

1. Fai clic su **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Passa alla console Progetti e apri il progetto di traduzione esistente a cui hai aggiunto.
1. Fai clic sulla pagina dei dettagli del progetto di traduzione.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Fai clic sull’ellissi nella parte inferiore della sezione **Processo di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >Se elimini la voce per tag o metadati, non vengono tradotti tag o metadati per nessuna delle risorse.

   >[!NOTE]
   >
   >Se la risorsa aggiunta al processo di traduzione include le risorse secondarie, selezionale e rimuoverle affinché la traduzione prosegua senza problemi.

1. Per avviare la traduzione delle risorse, fai clic sulla freccia nel riquadro **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Avvia]** dall’elenco.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un messaggio notifica l’inizio del processo di traduzione.

1. Per visualizzare lo stato del lavoro di traduzione, fai clic sull&#39;ellissi nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** .

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Per ulteriori dettagli, consulta [Monitoraggio dello stato di un lavoro di traduzione](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Passa all’ interfaccia utente [!DNL Assets] e apri la pagina Proprietà per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

## Aggiorna copie per lingua {#update-language-copies}

Esegui questo flusso di lavoro per tradurre qualsiasi set aggiuntivo di risorse e includerlo in una copia per lingua per una particolare impostazione internazionale. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza. A seconda della scelta delle opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro per la copia in lingua di aggiornamento include le seguenti opzioni:

* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project-1}

Se utilizzi questa opzione, viene creato un progetto di traduzione per il set di risorse per il quale desideri aggiornare una copia per lingua.

1. Dall’interfaccia utente di [!DNL Assets], seleziona la cartella di origine in cui hai aggiunto una risorsa.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare l&#39;elenco delle copie per lingua.
1. Seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**, quindi fai clic sulla cartella di destinazione che corrisponde alle impostazioni internazionali appropriate.

   ![seleziona copia per lingua](assets/lang-copy1.png)

1. Fare clic su **[!UICONTROL Aggiorna copie della lingua]** in basso.

1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea un nuovo progetto di traduzione]**.

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

1. Fare clic su **[!UICONTROL Start]**.
1. Passa alla console Progetti . La cartella di traduzione viene copiata nella console Progetti .

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Apri la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Fai clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Per avviare la traduzione delle risorse, fai clic sulla freccia nel riquadro **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Avvia]** dall’elenco.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un messaggio notifica l’inizio del processo di traduzione.

1. Per visualizzare lo stato del lavoro di traduzione, fai clic sull&#39;ellissi nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** .

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Per ulteriori dettagli sugli stati dei processi, consulta [Monitoraggio dello stato di un processo di traduzione](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Passa all’ interfaccia utente [!DNL Assets] e apri la pagina Proprietà per ciascuna risorsa tradotta per visualizzare i metadati tradotti.

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project-1}

Se utilizzi questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia per lingua relativa alle impostazioni internazionali selezionate.

1. Dall’interfaccia utente [!DNL Assets], seleziona la cartella di origine in cui hai aggiunto una cartella di risorse.
1. Apri il **[!UICONTROL riquadro Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare l&#39;elenco delle copie per lingua.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per lingua corrispondente alle impostazioni internazionali verso cui vuoi tradurre.

   ![seleziona copia per lingua](assets/lang-copy1.png)

1. Fare clic su **[!UICONTROL Aggiorna copie della lingua]** in basso.

1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Aggiungi al progetto di traduzione esistente]**.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Dall’elenco **[!UICONTROL Progetto di traduzione esistente]** , seleziona un progetto per aggiungere la risorsa da tradurre.

1. Fare clic su **[!UICONTROL Start]**.
1. Per completare il resto della procedura, vedi i passaggi 9-14 di [Aggiungi al progetto di traduzione esistente](translation-projects.md#add-to-existing-translation-project) .

## Crea copie in lingua temporanea {#creating-temporary-language-copies}

Quando esegui un flusso di lavoro di traduzione per aggiornare una copia in lingua con le versioni modificate delle risorse originali, la copia in lingua esistente viene conservata fino all’approvazione delle risorse tradotte. [!DNL Adobe Experience Manager Assets] memorizza le risorse appena tradotte in una posizione temporanea e aggiorna la copia in lingua esistente dopo l’approvazione esplicita delle risorse. Se si rifiutano le risorse, la copia in lingua rimane invariata.

1. Fai clic sulla cartella principale di origine in **[!UICONTROL Copie per lingua]** per la quale hai già creato una copia per lingua, quindi fai clic su **[!UICONTROL Mostra in Assets]** per aprire la cartella in [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Dall’interfaccia [!DNL Assets], seleziona una risorsa già tradotta e fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modifica la risorsa e salva le modifiche.
1. Esegui i passaggi 2-14 della procedura [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) per aggiornare la copia per lingua.
1. Fai clic sull&#39;ellissi nella parte inferiore della sezione **[!UICONTROL Processo di traduzione]** . Dall’elenco delle risorse nella pagina **[!UICONTROL Processo di traduzione]**, puoi visualizzare chiaramente la posizione temporanea in cui è memorizzata la versione tradotta della risorsa.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Seleziona la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Accetta traduzione]** ![accetta traduzione](assets/do-not-localize/thumb-up.png), quindi fai clic su **[!UICONTROL Accetta]** nella finestra di dialogo per sovrascrivere la risorsa tradotta nella cartella di destinazione con la versione tradotta della risorsa modificata.

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accetta sia la risorsa che i metadati.

   Fai clic su **[!UICONTROL Rifiuta traduzione]** ![Rifiuta traduzione](assets/do-not-localize/thumb-down.png) per conservare la versione tradotta originariamente nella directory principale delle impostazioni internazionali di destinazione e rifiutare la versione modificata.

1. Per visualizzare i metadati tradotti, passa alla console [!DNL Assets] e apri la pagina [!UICONTROL Proprietà] per ciascuna risorsa tradotta.

## Suggerimenti e limitazioni {#tips-limitations}

* Se avvii un flusso di lavoro di traduzione per risorse complesse, come file PDF e [!DNL Adobe InDesign], le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.
* Se utilizzi la traduzione automatica, i binari delle risorse non vengono tradotti.
