---
title: Creazione di progetti di traduzione
description: Scopri come creare progetti di traduzione in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 16%

---


# Creazione di progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attivare uno dei seguenti flussi di lavoro di copia per lingua disponibili nella barra laterale Riferimenti nell’interfaccia [!DNL Experience Manager] utente.

* **Crea e traduci**: In questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desiderate tradurre. Inoltre, a seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

* **Aggiorna copie** della lingua: Eseguite questo flusso di lavoro per tradurre un altro gruppo di risorse e includerlo in una copia per lingua per una lingua specifica. In questo caso, le risorse convertite vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza.

>[!NOTE]
>
>I file binari di risorse vengono tradotti solo se il provider di servizi di traduzione supporta la traduzione dei file binari.

>[!NOTE]
>
>Se avviate un flusso di lavoro di traduzione per risorse complesse, come file PDF e InDesign, le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.

## Crea e traduci flusso di lavoro {#create-and-translate-workflow}

È possibile utilizzare il flusso di lavoro di creazione e traduzione per generare per la prima volta copie della lingua per una lingua particolare. Il flusso di lavoro offre le seguenti opzioni:

* Crea solo struttura.
* Crea un nuovo progetto di traduzione.
* Aggiungi a progetto di traduzione esistente.

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **[!UICONTROL Crea solo struttura]** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell&#39; [!DNL Assets] interfaccia, selezionate la cartella di origine per la quale desiderate creare una struttura nella directory principale della lingua di destinazione.
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Fate clic su **[!UICONTROL Crea e traduci]** in basso.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. From the **[!UICONTROL Target Languages]** list, select the language for which you want to create a folder structure.

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. Fai clic su **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in Copie **[!UICONTROL lingua]**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Fai clic sulla struttura dall’elenco, quindi fai clic su **[!UICONTROL Mostra in risorse]** per passare alla struttura di cartelle nella lingua di destinazione.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project}

Se utilizzate questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desiderate tradurre. A seconda delle opzioni selezionate, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o eseguito automaticamente non appena viene creato il progetto di traduzione.

1. Nell’interfaccia utente Risorse, seleziona la cartella di origine per la quale vuoi creare una copia per la lingua.
1. Open the **[!UICONTROL References]** pane and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Fate clic su **[!UICONTROL Crea e traduci]** in basso.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Dall’elenco **[!UICONTROL Progetto]** , selezionate **[!UICONTROL Crea un nuovo progetto]** di traduzione.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Fai clic su **[!UICONTROL Crea]**. Le risorse della cartella di origine vengono copiate nelle cartelle di destinazione per le impostazioni internazionali selezionate al punto 4.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Per passare alla cartella, selezionate la copia della lingua e fate clic su **[!UICONTROL Mostra nelle risorse]**.

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. Passate alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Aprite la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Fate clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Per visualizzare lo stato del processo di traduzione, fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Per ulteriori dettagli sugli stati dei processi, vedere [Monitoraggio dello stato di un processo](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)di traduzione.

1. Andate all’interfaccia utente delle risorse e aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati tradotti.

   ![visualizzare i metadati convertiti nella pagina Proprietà della risorsa](assets/translated-metadata-asset-properties.png)

   *Figura: Metadati tradotti nella pagina delle proprietà della risorsa.*


   >[!NOTE]
   >
   >Questa funzione è disponibile sia per le risorse che per le cartelle. Quando una risorsa viene selezionata al posto di una cartella, viene copiata l’intera gerarchia di cartelle fino alla radice della lingua per creare una copia della lingua per la risorsa.

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project}

Se utilizzate questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo aver eseguito un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell’interfaccia utente Risorse, passa alla cartella di origine contenente le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Fate clic su **[!UICONTROL Crea e traduci]** in basso.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Nell’elenco **[!UICONTROL Lingue di destinazione]**, seleziona le lingue per le quali vuoi creare una struttura di cartelle.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Se scegliete l’opzione **[!UICONTROL Aggiungi al progetto]** di traduzione esistente, il progetto di traduzione viene aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente alle impostazioni del progetto preesistente. In caso contrario, viene creato un nuovo progetto.

1. Dall’elenco Progetto **[!UICONTROL di traduzione]** esistente, selezionate un progetto per aggiungere la risorsa per la traduzione.

   ![chlimage_1-70](assets/chlimage_1-78.png)

1. Fai clic su **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Passate alla console Progetti e aprite il progetto di traduzione esistente a cui avete aggiunto.
1. Fate clic sulla pagina dei dettagli del progetto di traduzione.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Click the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >Se eliminate la voce relativa a tag o metadati, non vengono convertiti tag o metadati per nessuna risorsa.

   >[!NOTE]
   >
   >Se utilizzate Traduzione automatica, i file binari delle risorse non vengono tradotti.

   >[!NOTE]
   >
   >Se la risorsa aggiunta al processo di conversione include risorse secondarie, selezionate le risorse secondarie e rimuoverle affinché la conversione possa proseguire senza problemi.

1. Per avviare la conversione delle risorse, fate clic sulla freccia nella sezione Processo **[!UICONTROL di]** traduzione e selezionate **[!UICONTROL Avvia]** dall’elenco.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un messaggio notifica l’inizio del processo di traduzione.

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. Per visualizzare lo stato del processo di traduzione, fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Per ulteriori dettagli, consultate [Monitoraggio dello stato di un processo](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)di traduzione.

1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Andate all’interfaccia utente delle risorse e aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati tradotti.

## Aggiorna copie per lingua {#update-language-copies}

Eseguite questo flusso di lavoro per tradurre qualsiasi altro set di risorse e includerlo in una copia della lingua per una lingua specifica. In questo caso, le risorse convertite vengono aggiunte alla cartella di destinazione che contiene già risorse tradotte in precedenza. A seconda della scelta delle opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro Copia lingua aggiornamento include le seguenti opzioni:

* Crea un nuovo progetto di traduzione
* Aggiungi a progetto di traduzione esistente

### Crea un nuovo progetto di traduzione {#create-a-new-translation-project-1}

Se utilizzate questa opzione, viene creato un progetto di traduzione per il set di risorse per il quale desiderate aggiornare una copia in lingua.

1. Nell’interfaccia utente Risorse, seleziona la cartella di origine in cui hai aggiunto una risorsa.
1. Open the **[!UICONTROL References]** pane, and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.
1. Seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**, quindi fai clic sulla cartella di destinazione che corrisponde alle impostazioni internazionali appropriate.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Fate clic su **[!UICONTROL Aggiorna copie]** della lingua in basso.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Dall’elenco **[!UICONTROL Progetto]** , scegliete **[!UICONTROL Crea un nuovo progetto]** di traduzione.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Fate clic su **[!UICONTROL Avvia]**.
1. Passate alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Aprite la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Fate clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Per avviare la conversione delle risorse, fate clic sulla freccia nella sezione Processo **[!UICONTROL di]** traduzione e selezionate **[!UICONTROL Avvia]** dall’elenco.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un messaggio notifica l’inizio del processo di traduzione.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Per visualizzare lo stato del processo di traduzione, fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Per ulteriori dettagli sugli stati dei processi, vedere [Monitoraggio dello stato di un processo](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job)di traduzione.

1. Andate all’interfaccia utente delle risorse e aprite la pagina Proprietà per ciascuna risorsa convertita per visualizzare i metadati tradotti.

### Aggiungi a progetto di traduzione esistente {#add-to-existing-translation-project-1}

Se utilizzate questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia della lingua per le impostazioni internazionali scelte.

1. Dall’interfaccia utente Risorse, selezionate la cartella di origine in cui avete aggiunto una cartella di risorse.
1. Open the **[!UICONTROL References pane]**, and click **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per lingua corrispondente alle impostazioni internazionali verso cui vuoi tradurre.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Fate clic su **[!UICONTROL Aggiorna copie]** della lingua in basso.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. Dall’elenco **[!UICONTROL Progetto]** , scegliete **[!UICONTROL Aggiungi al progetto]** di traduzione esistente.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Dall’elenco Progetto **[!UICONTROL di traduzione]** esistente, selezionate un progetto per aggiungere la risorsa per la traduzione.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Fate clic su **[!UICONTROL Avvia]**.
1. Per completare il resto della procedura, consulta i passaggi da 9 a 14 di [Aggiungi al progetto](translation-projects.md#add-to-existing-translation-project) di traduzione esistente.

## Creare copie in lingua temporanea {#creating-temporary-language-copies}

Quando eseguite un flusso di lavoro di traduzione per aggiornare una copia per lingua con versioni modificate di risorse originali, la copia per lingua esistente viene mantenuta fino all’approvazione delle risorse tradotte. [!DNL Adobe Experience Manager Assets] memorizza le risorse appena tradotte in una posizione temporanea e aggiorna la copia della lingua esistente dopo l’approvazione esplicita delle risorse. Se rifiutate le risorse, la copia nella lingua rimane invariata.

1. Click the source root folder under **[!UICONTROL Language Copies]** for which you already created a language copy, and then click **[!UICONTROL Reveal in Assets]** to open the folder in [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Dall’ [!DNL Assets] interfaccia, selezionate una risorsa già tradotta e fate clic sull’icona **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modificate la risorsa e salvate le modifiche.
1. Per aggiornare la copia della lingua, eseguite i passaggi da 2 a 14 della procedura [Aggiungi al progetto](#add-to-existing-translation-project) di traduzione esistente.
1. Fate clic sui puntini di sospensione nella parte inferiore della sezione Processo **[!UICONTROL di]** traduzione. Dall’elenco delle risorse nella pagina Processo **[!UICONTROL di]** traduzione, potete visualizzare chiaramente la posizione temporanea in cui è memorizzata la versione convertita della risorsa.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Selezionate la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. From the toolbar, click **[!UICONTROL Accept Translation]** and then click **[!UICONTROL Accept]** in the dialog to overwrite the translated asset in the target folder with the translated version of the edited asset.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accettate sia la risorsa che i metadati.

   Fate clic su **[!UICONTROL Rifiuta traduzione]** per mantenere la versione tradotta originariamente nella directory principale delle impostazioni internazionali di destinazione e rifiutare la versione modificata.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Per visualizzare i metadati convertiti, andate alla [!DNL Assets] console e aprite la pagina [!UICONTROL Proprietà] per ciascuna risorsa convertita.

>[!MORELIKETHIS]
>
>* [Suggerimenti per tradurre in modo efficiente i metadati](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/).

