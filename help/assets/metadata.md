---
title: Consente di gestire i metadati delle risorse digitali in [!DNL Adobe Experience Manager].
description: Scoprite i tipi di metadati e [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] come organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c3f85314740c4e9ca8ed0c9a724b49ff4276616a
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 11%

---


# Gestione dei metadati delle risorse digitali {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantiene i metadati per ogni risorsa. Consente una classificazione e un’organizzazione più semplici delle risorse e aiuta le persone che cercano una risorsa specifica. Grazie alla possibilità di estrarre i metadati dai file caricati in [!DNL Experience Manager Assets], la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di conservare e gestire i metadati insieme alle risorse, potete organizzare ed elaborare automaticamente le risorse in base ai metadati.

## Metadati e relativa origine {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. e viene aggiunto alle risorse e [!DNL Experience Manager] viene elaborato al momento del caricamento di una risorsa. Potete modificare i metadati esistenti e aggiungere nuove proprietà di metadati ai campi esistenti. Le organizzazioni hanno bisogno di vocabolari di metadati controllati e affidabili. Pertanto [!DNL Experience Manager Assets] non è possibile aggiungere su richiesta nuove proprietà di metadati. Solo gli amministratori e gli sviluppatori possono aggiungere nuove proprietà o campi che contengono metadati. Gli utenti possono compilare i campi esistenti con i metadati.

Per aggiungere metadati alle risorse digitali potete usare i metodi seguenti:

* Per iniziare, le applicazioni native che creano le risorse vi aggiungono alcuni metadati. Ad esempio, [Acrobat aggiunge alcuni metadati](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) ai file PDF o una fotocamera aggiunge alcuni metadati di base alle fotografie. Durante la generazione delle risorse, potete aggiungere i metadati direttamente nelle applicazioni native. Ad esempio, potete [aggiungere metadati IPTC in  Adobe Lightroom](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* Prima di caricare una risorsa in [!DNL Experience Manager], potete modificare i metadati utilizzando l’applicazione nativa utilizzata per creare una risorsa o altre applicazioni di modifica dei metadati. Quando caricate una risorsa in  Experience Manager, i metadati vengono elaborati. Ad esempio, vedere come [lavorare con i metadati [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) e vedere il pannello [tag per [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) in [!DNL Adobe Exchange].

* In [!DNL Experience Manager Assets], potete aggiungere o modificare manualmente i metadati delle risorse nella pagina [!UICONTROL Proprietà] .

* Potete sfruttare la funzionalità dei profili [di](/help/assets/metadata-config.md#metadata-profiles) metadati [!DNL Experience Manager Assets] per aggiungere automaticamente i metadati quando le risorse vengono caricate in DAM.

## Aggiungere o modificare i metadati in [!DNL Experience Manager Assets] {#add-edit-metadata}

Per modificare i metadati di una risorsa nell’interfaccia [!DNL Assets] utente, effettuate le seguenti operazioni:

1. Effettua una delle operazioni seguenti:

   * Dall’ [!DNL Assets] interfaccia, selezionate la risorsa e fate clic su **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
   * Dalla miniatura della risorsa, selezionate l’azione rapida **[!UICONTROL Visualizza proprietà]** .
   * Dalla pagina della risorsa, fai clic sull’icona **[!UICONTROL Visualizza proprietà]** ![](assets/do-not-localize/info-circle-icon.png) Risorse nella barra degli strumenti.

   Nella pagina della risorsa vengono visualizzati tutti i metadati della risorsa. I metadati vengono estratti quando la risorsa viene caricata (assimilata) in [!DNL Experience Manager].

   ![Selezionate Proprietà di una risorsa per visualizzarne i metadati](assets/asset-metadata.png)

   *Figura: Modificate o aggiungete i metadati nella pagina[!UICONTROL Proprietà]risorsa.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non esiste alcun set di metadati. Potete immettere un valore nel campo e salvarlo per aggiungere la proprietà dei metadati.

Qualsiasi modifica ai metadati di una risorsa viene riscritta nel binario originale come parte dei dati XMP. Il flusso di lavoro per la riscrittura dei metadati aggiunge i metadati al binario originale. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le nuove proprietà (incluse quelle personalizzate come `cq:tags`) vengono aggiunte allo schema.

XMP riscrittura è supportata e abilitata per le piattaforme e i formati di file descritti nei requisiti [tecnici.](/help/sites-deploying/technical-requirements.md)

## Modificare le proprietà dei metadati di più risorse {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] consente di modificare simultaneamente i metadati di più risorse, in modo da poter rapidamente estendere le comuni modifiche ai metadati alle risorse in gruppo. Potete anche modificare i metadati per più raccolte in blocco. Utilizzate la pagina delle proprietà per eseguire modifiche ai metadati su più risorse o raccolte:

* Cambiare le proprietà dei metadati impostando un valore comune
* Aggiunta o modifica di tag

Per personalizzare la pagina delle proprietà dei metadati, incluse l’aggiunta, la modifica, l’eliminazione delle proprietà dei metadati, utilizzate l’editor dello schema.

>[!NOTE]
>
>I metodi di modifica collettiva funzionano per le risorse disponibili in una cartella o in una raccolta. Per le risorse disponibili in più cartelle o che corrispondono a criteri comuni, è possibile aggiornare [in massa i metadati dopo la ricerca](search-assets.md#metadataupdates).

1. Nell’interfaccia [!DNL Assets] utente, individuate la posizione delle risorse da modificare.
1. Selezionate le risorse per le quali desiderate modificare le proprietà comuni.
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Proprietà]** per aprire la pagina delle proprietà relativa alle risorse selezionate.

   >[!NOTE]
   >
   >Quando selezionate più risorse, per le risorse viene selezionato il modulo padre più basso comune. In altre parole, nella pagina delle proprietà vengono visualizzati solo i campi di metadati comuni nelle pagine delle proprietà di tutte le singole risorse.

1. Modificate le proprietà dei metadati per le risorse selezionate nelle varie schede.
1. Per visualizzare l’editor di metadati per una risorsa specifica, deselezionate le risorse rimanenti nell’elenco. I campi dell’editor di metadati vengono compilati con i metadati della risorsa in questione.

   >[!NOTE]
   >
   >* Nella pagina delle proprietà potete rimuovere le risorse dall’elenco delle risorse deselezionandole. Per impostazione predefinita, nell’elenco delle risorse sono selezionate tutte le risorse. I metadati delle risorse rimosse dall’elenco non vengono aggiornati.
   >* Nella parte superiore dell’elenco delle risorse, selezionate la casella di controllo accanto a **[!UICONTROL Titolo]** per alternare tra la selezione delle risorse e la cancellazione dell’elenco.


1. Per selezionare uno schema di metadati diverso per le risorse, fate clic su **[!UICONTROL Impostazioni]** nella barra degli strumenti, quindi selezionate lo schema desiderato.
1. Salva le modifiche.
1. Per aggiungere i nuovi metadati a quelli esistenti nei campi che contengono più valori, seleziona **[!UICONTROL Modalità di aggiunta]**. Se non selezioni questa opzione, i nuovi metadati sostituiranno quelli già esistenti nei campi. Fate clic su **[!UICONTROL Invia]**.

   >[!CAUTION]
   >
   >Per i campi con valore singolo, i nuovi metadati non vengono aggiunti al valore esistente nel campo, nemmeno se selezioni **[!UICONTROL Modalità di aggiunta]**.

## Importare i metadati {#import-metadata}

[!DNL Assets] consente di importare in massa i metadati delle risorse mediante un file CSV. Potete eseguire aggiornamenti in blocco per le risorse caricate di recente o per le risorse esistenti importando un file CSV. Potete anche assimilare i metadati delle risorse in massa da sistemi di terze parti in formato CSV.

L&#39;importazione dei metadati è asincrona e non ostacola le prestazioni del sistema. L’aggiornamento simultaneo dei metadati per più risorse può richiedere molte risorse, a causa XMP’attività di reinserimento se è selezionato il flag del flusso di lavoro. Pianificate tale importazione durante l&#39;utilizzo di un server snello in modo che le prestazioni per altri utenti non vengano compromesse.

>[!NOTE]
>
>Per importare i metadati negli spazi dei nomi personalizzati, registrate prima gli spazi dei nomi.

1. Passate all’interfaccia [!DNL Assets] utente e fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dal menu, selezionate **[!UICONTROL Metadati]**.
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. Scegli il file CSV con i metadati.
1. Specificate i seguenti parametri. Consultate un file CSV di esempio in [metadata-import-sample-file.csv](assets/metadata-import-sample-file.csv).

   | Parametri di importazione metadati | Descrizione |
   |:---|:---|
   | [!UICONTROL Dimensione batch] | Numero di risorse in un batch per cui importare i metadati. Il valore predefinito è 50. Il valore massimo è 100. |
   | [!UICONTROL Separatore di campi] | Il valore predefinito è `,` (una virgola). È possibile specificare qualsiasi altro carattere. |
   | [!UICONTROL Delimitatore valori multipli] | Separatore per i valori dei metadati. Il valore predefinito è `|`. |
   | [!UICONTROL Avvia flussi di lavoro] | False per impostazione predefinita. Quando è impostata su `true` e le impostazioni predefinite di Launcher sono attive per il flusso di lavoro WriteBack [!UICONTROL metadati] DAM (che scrive i metadati nei dati XMP binari). L&#39;attivazione dei flussi di lavoro di avvio rallenta il sistema. |
   | [!UICONTROL Nome colonna percorso risorsa] | Definisce il nome della colonna per il file CSV con le risorse. |

1. Click **[!UICONTROL Import]** from the toolbar. Una volta importati i metadati, nella inbox delle [!UICONTROL notifiche] viene visualizzata una notifica.

1. Per verificare la corretta importazione, andate alla pagina [!UICONTROL Proprietà] di una risorsa e verificate i valori nei campi.

Per aggiungere data e marca temporale al momento dell’importazione dei metadati, utilizzate `YYYY-MM-DDThh:mm:ss.fff-00:00` il formato per la data e l’ora. Data e ora sono separate da `T`, `hh` è ore in formato 24 ore, `fff` è nanosecondi e `-00:00` è l’offset del fuso orario. Ad esempio, `2020-03-26T11:26:00.000-07:00` è il 26 marzo 2020 alle 11:26:00.000 ora di ora precedente.

>[!CAUTION]
>
>Se il formato della data non corrisponde, `YYYY-MM-DDThh:mm:ss.fff-00:00`i valori della data non vengono impostati. I formati data del file CSV dei metadati esportati sono nel formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desiderate importarlo, convertitelo nel formato accettabile aggiungendo il valore nanosecondi indicato da `fff`.

## Export metadata {#export-metadata}

Potete esportare i metadati per più risorse in formato CSV. I metadati vengono esportati in modo asincrono e non influiscono sulle prestazioni del sistema. Per esportare i metadati, [!DNL Experience Manager] scorrono le proprietà del nodo della risorsa `jcr:content/metadata` e dei relativi nodi secondari ed esportano le proprietà dei metadati in un file CSV.

Alcuni esempi di utilizzo per l’esportazione di metadati in massa sono:

* Importate i metadati in un sistema di terze parti durante la migrazione delle risorse.
* Condividete i metadati delle risorse con un team di progetto più ampio.
* Verificate o verificate la conformità dei metadati.
* Esternalizzate i metadati per localizzarli separatamente.

1. Selezionate la cartella di risorse che contiene le risorse per le quali desiderate esportare i metadati. Dalla barra degli strumenti, selezionate **[!UICONTROL Esporta metadati]**.

1. Nella finestra di dialogo Esportazione  metadati, specificate un nome per il file CSV. Per esportare i metadati delle risorse nelle sottocartelle, selezionate **[!UICONTROL Includi risorse nelle sottocartelle]**.

   ![Interfaccia e opzioni per l’esportazione dei metadati di tutte le risorse di una](assets/export_metadata_page.png "cartellaInterfaccia e opzioni per l’esportazione dei metadati di tutte le risorse di una cartella")

1. Selezionate le opzioni desiderate. Specificare un nome di file e, se necessario, una data.

1. Nel campo **[!UICONTROL Proprietà da esportare]** , specificate se esportare tutte le proprietà o solo proprietà specifiche. Se scegliete le proprietà selettive da esportare, aggiungete le proprietà desiderate.

1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Esporta]**. Viene visualizzato un messaggio di conferma dell’esportazione dei metadati. Chiudi il messaggio.

1. Apri la notifica della casella in entrata del processo di esportazione. Seleziona il processo e fai clic su **[!UICONTROL Apri]** nella barra degli strumenti. To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. Fai clic su **[!UICONTROL Chiudi]**.

   ![Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa](assets/csv_download.png)

   *Figura: Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa.*

## Modifica dei metadati delle raccolte {#collections-metadata}

Per informazioni dettagliate, consultate [visualizzare e modificare i metadati](/help/assets/managing-collections-touch-ui.md#view-edit-collection-metadata) della raccolta e [modificare i metadati di più raccolte in blocco](/help/assets/managing-collections-touch-ui.md#editing-collection-metadata-in-bulk).

## Applicazione di un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

Quando assegnate un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. Questo significa che potete assegnare un solo profilo di metadati a una cartella. Considerate quindi attentamente la struttura delle cartelle in cui caricare, memorizzare, usare e archiviare le risorse.

Se avete assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse di cartella esistenti in precedenza restano invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

![Nella vista a schede viene visualizzato il profilo di metadati applicato a una cartella](assets/metadata-profile-card-view-display.png)

Potete applicare i profili di metadati a cartelle specifiche o globalmente a tutte le risorse.

Potete rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Potete rielaborare le risorse in una cartella che dispone già di un profilo video esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

### Applicazione dei profili di metadati alle cartelle dall&#39;interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Seguite i passaggi per applicare il profilo di metadati:

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selezionate il profilo di metadati da applicare a una o più cartelle.
1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicazione dei profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, fate clic su **[!UICONTROL Risorse]** , quindi individuate la cartella a cui desiderate applicare un profilo di metadati.
1. Nella cartella, fare clic sul segno di spunta per selezionarlo, quindi fare clic su **[!UICONTROL Proprietà]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the popup menu and click **[!UICONTROL Save]**.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicazione del profilo di metadati a livello globale {#metadata-profile-global}

Per informazioni dettagliate, consultate [Configurazione per applicare il profilo di metadati a livello globale](/help/assets/metadata-config.md#apply-a-metadata-profile-globally).

### Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovete un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla cartella principale. Tuttavia, l&#39;elaborazione dei file che si è verificata all&#39;interno delle cartelle rimane intatta.

Potete rimuovere un profilo di metadati da una cartella dal menu **[!UICONTROL Strumenti]** o dalle **[!UICONTROL Proprietà]** dall’interno della cartella.

#### Rimozione di profili di metadati dalle cartelle tramite l&#39;interfaccia utente Profili {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selezionate il profilo di metadati da rimuovere da una o più cartelle.
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   Potete confermare che il profilo di metadati non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

#### Rimozione di profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Fate clic sul [!DNL Experience Manager] logo, individuate **[!UICONTROL Risorse]** e quindi la cartella da cui desiderate rimuovere un profilo di metadati.
1. Nella cartella, fare clic sul segno di spunta per selezionarlo, quindi fare clic su **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

## Suggerimenti e limitazioni {#best-practices-limitations}

* Gli aggiornamenti dei metadati tramite l&#39;interfaccia utente modificano le proprietà dei metadati nello `dc` spazio dei nomi. Eventuali aggiornamenti effettuati tramite l’API HTTP modificano le proprietà dei metadati nello `jcr` spazio nomi. Scoprite [come aggiornare i metadati mediante l&#39;API](/help/assets/mac-api-assets.md#update-asset-metadata)HTTP.

* Il file CSV per l’importazione dei metadati delle risorse è in un formato molto specifico. Per risparmiare tempo e sforzi ed evitare errori non intenzionali, potete iniziare a creare il CSV utilizzando il formato di un file CSV esportato.

* Quando importate dei metadati utilizzando un file CSV, il formato di data richiesto è `YYYY-MM-DDThh:mm:ss.fff-00:00`. Se viene utilizzato un altro formato, i valori data non vengono impostati. I formati data del file CSV dei metadati esportati sono nel formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desiderate importarlo, convertitelo nel formato accettabile aggiungendo il valore nanosecondi indicato da `fff`.

>[!MORELIKETHIS]
>
>* [Concetti di metadati e comprensione](metadata-concepts.md).
>* [Modifica delle proprietà dei metadati di più raccolte](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [Importazione ed esportazione di metadati in  risorse Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
