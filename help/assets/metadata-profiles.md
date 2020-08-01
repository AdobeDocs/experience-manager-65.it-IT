---
title: Profili di metadati per personalizzare i requisiti di metadati delle risorse
description: Informazioni sui profili di metadati per le risorse. Scoprite come creare un profilo di metadati e applicarlo alle risorse delle cartelle.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 21%

---


# Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare i metadati predefiniti alle risorse all’interno di una cartella. Create un profilo di metadati e applicatelo a una cartella. Le risorse che successivamente caricate nella cartella ereditano i metadati predefiniti configurati nel profilo di metadati.

## Aggiunta di un profilo di metadati {#adding-a-metadata-profile}

1. Andate su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Profili **** metadati e fate clic su **[!UICONTROL Crea]**.
1. Immettete un titolo per il profilo di metadati, ad esempio Metadati di esempio, e fate clic su **[!UICONTROL Crea]**. Viene visualizzato [!UICONTROL Modifica modulo] per il profilo di metadati.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Fate clic su un componente e configuratene le proprietà nella scheda **[!UICONTROL Impostazioni]** . Ad esempio, fare clic sul componente **[!UICONTROL Descrizione]** e modificarne le proprietà.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Modificate le seguenti proprietà per il componente **[!UICONTROL Descrizione]** :

   * **[!UICONTROL Etichetta]** campo: Nome visualizzato della proprietà metadata. È solo per il riferimento utente.

   * **[!UICONTROL Mappa su proprietà]**: Il valore di questa proprietà fornisce il percorso/nome relativo al nodo della risorsa in cui viene salvata nella directory archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

   ![chlimage_1-199](assets/chlimage_1-482.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Ad esempio, se specifichi: `/jcr:content/metadata/dc:desc` come nome della proprietà **** Mappa, [!DNL Assets] memorizza il valore `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore]** predefinito: Utilizzare questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specificate &quot;Descrizione personale&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste già in . `/jcr:content/metadata` node) per impostazione predefinita, la proprietà e il relativo valore non vengono visualizzati nella pagina Proprietà della risorsa. Per visualizzare la nuova proprietà nella pagina [!UICONTROL Proprietà] delle risorse, modificare il modulo schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Etichetta campo, <br> Descrizione |
| [!UICONTROL Testo su riga singola] | Etichetta campo, <br> Mappa su proprietà, Valore <br> predefinito |
| [!UICONTROL Testo con più valori] | Etichetta campo, <br> Mappa su proprietà, Valore <br> predefinito |
| [!UICONTROL Numero] | Etichetta campo, <br> Mappa su proprietà, Valore <br> predefinito |
| [!UICONTROL Data] | Etichetta campo, <br> Mappa su proprietà, Valore <br> predefinito |
| [!UICONTROL Tag standard] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito, <br> Descrizione |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Fate clic su **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nella pagina **[!UICONTROL Profili]** metadati.<br>

   ![Profilo metadati aggiunto nella pagina Profili metadati](assets/MetadataProfiles-page.png)

## Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili]** metadati, selezionate un profilo di metadati per copiarlo.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo]** metadati, inserite un titolo per la nuova copia del profilo metadati.
1. Fate clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

   ![Una copia del profilo di metadati aggiunto nella pagina Profili metadati](assets/copy-metadata-profile.png)

## Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Nella pagina **[!UICONTROL Profili]** metadati, selezionate un profilo da eliminare.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Toccate[] **[!UICONTROL Elimina profili]** metadati nella barra degli strumenti.
1. Nella finestra di dialogo, fare clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo di metadati viene eliminato dall’elenco.

## Applicazione di un profilo di metadati alle cartelle {#applying-a-metadata-profile-to-folders}

Quando assegnate un profilo di metadati a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. Questo significa che potete assegnare un solo profilo di metadati a una cartella. Considerate quindi attentamente la struttura delle cartelle in cui caricare, memorizzare, usare e archiviare le risorse.

Se avete assegnato un profilo di metadati diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse di cartella esistenti in precedenza restano invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

![chlimage_1-206](assets/chlimage_1-489.png)

Potete applicare i profili di metadati a cartelle specifiche o globalmente a tutte le risorse.

Potete rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

### Applicazione di profili di metadati a cartelle specifiche {#applying-metadata-profiles-to-specific-folders}

Puoi applicare un profilo di metadati a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili di metadati alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Potete rielaborare le risorse in una cartella che dispone già di un profilo video esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

#### Applicazione dei profili di metadati alle cartelle dall&#39;interfaccia utente Profili {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Seguite i passaggi per applicare il profilo di metadati:

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selezionate il profilo di metadati da applicare a una o più cartelle.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

#### Applicazione dei profili di metadati alle cartelle da Proprietà {#applying-metadata-profiles-to-folders-from-properties}

1. Nella barra a sinistra, fate clic su **[!UICONTROL Risorse]** , quindi individuate la cartella a cui desiderate applicare un profilo di metadati.
1. Nella cartella, fare clic sul segno di spunta per selezionarlo, quindi fare clic su **[!UICONTROL Proprietà]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and click **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

### Applicare un profilo di metadati a livello globale {#applying-a-metadata-profile-globally}

Oltre ad applicare un profilo a una cartella, potete anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato nelle [!DNL Experience Manager] risorse di qualsiasi cartella sia applicato il profilo selezionato.

Potete rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

Per applicare un profilo di metadati a livello globale, effettuate le seguenti operazioni:

* Individuate `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e applicate il profilo appropriato e fate clic su **[!UICONTROL Salva]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* In CRXDE Lite , andate al seguente nodo: `/content/dam/jcr:content`. Aggiungete la proprietà `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` e fate clic su **[!UICONTROL Salva tutto]**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Rimozione di un profilo di metadati dalle cartelle {#removing-a-metadata-profile-from-folders}

Quando rimuovete un profilo di metadati da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla cartella principale. Tuttavia, l&#39;elaborazione dei file che si è verificata all&#39;interno delle cartelle rimane intatta.

Puoi rimuovere un profilo di metadati da una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come rimuovere i profili di metadati dalle cartelle con entrambe le soluzioni.

### Rimozione di profili di metadati dalle cartelle tramite l&#39;interfaccia utente Profili {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selezionate il profilo di metadati da rimuovere da una o più cartelle.
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   Potete confermare che il profilo di metadati non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione di profili di metadati dalle cartelle tramite Proprietà {#removing-metadata-profiles-from-folders-via-properties}

1. Fate clic sul [!DNL Experience Manager] logo, individuate **[!UICONTROL Risorse]** e quindi la cartella da cui desiderate rimuovere un profilo di metadati.
1. Nella cartella, fare clic sul segno di spunta per selezionarlo, quindi fare clic su **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili metadati]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

## Limitations and best practices {#limitations-best-practices-tips}

* È possibile che siano già presenti profili di metadati preesistenti prima dell’aggiornamento alla versione [!DNL Experience Manager] 6.5. Dopo l’aggiornamento, se applicate un profilo simile in [!UICONTROL Proprietà] cartella nella scheda Profili  metadati, i campi dei moduli di metadati non vengono visualizzati. Tuttavia, se applicate un profilo di metadati appena creato, i campi del modulo vengono visualizzati ma non sono disponibili come previsto. Non si verificano perdite di funzionalità, ma se si desidera visualizzare i campi modulo (non disponibili), è necessario modificare e salvare i profili di metadati esistenti.

>[!MORELIKETHIS]
>
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md)
>* [Best practice per organizzare le risorse digitali in modo da utilizzare i profili di elaborazione](/help/assets/organize-assets.md)

