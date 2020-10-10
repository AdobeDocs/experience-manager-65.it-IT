---
title: Configurazione e amministrazione della funzionalità dei metadati.
description: Funzionalità di configurazione e amministrazione [!DNL Experience Manager Assets] relative all'aggiunta e alla gestione dei metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c3f85314740c4e9ca8ed0c9a724b49ff4276616a
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 6%

---


# Configurazione e amministrazione della funzionalità dei metadati [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantiene i metadati per ogni risorsa. Consente una classificazione e un’organizzazione più semplici delle risorse e aiuta le persone che cercano una risorsa specifica. Grazie alla possibilità di conservare e gestire i metadati insieme alle risorse, potete organizzare ed elaborare automaticamente le risorse in base ai metadati. [!DNL Adobe Experience Manager Assets] consente agli amministratori di configurare e personalizzare la funzionalità dei metadati per modificare l&#39;offerta di Adobe  predefinito.

## Modifica schema metadati {#metadata-schema}

Per informazioni dettagliate, vedere [Modificare i moduli](metadata-schemas.md#edit-metadata-schema-forms)degli schemi di metadati.

## Registra uno spazio nomi personalizzato all&#39;interno di [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Potete aggiungere spazi dei nomi personalizzati all&#39;interno [!DNL Experience Manager]. Allo stesso modo in cui esistono spazi dei nomi predefiniti come `cq`, `jcr`e `sling`, potete avere uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione XML.

1. Accedere alla pagina di amministrazione del tipo di nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Per accedere alla pagina di amministrazione dello spazio dei nomi, fare clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina.
1. Per aggiungere uno spazio nomi, fate clic su **[!UICONTROL Nuovo]** nella parte inferiore della pagina.
1. Specificate uno spazio nomi personalizzato nella convenzione spazio nomi XML. Specificate l’ID sotto forma di URI e il prefisso associato per l’ID. Fai clic su **[!UICONTROL Salva]**.

## Configurare i limiti per l&#39;aggiornamento in massa dei metadati {#bulk-metadata-update-limit}

Per evitare una situazione di negazione del servizio (DOS), [!DNL Enterprise Manager] limita il numero di parametri supportati in una richiesta Sling. Quando aggiornate i metadati di molte risorse in una sola volta, potete raggiungere il limite massimo e i metadati non vengono aggiornati per altre risorse. Enterprise Manager genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

## Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare i metadati predefiniti alle risorse all’interno di una cartella. Create un profilo di metadati e applicatelo a una cartella. Le risorse che successivamente caricate nella cartella ereditano i metadati predefiniti configurati nel profilo di metadati.

### Aggiunta di un profilo di metadati {#adding-a-metadata-profile}

1. Andate su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Profili **** metadati e fate clic su **[!UICONTROL Crea]**.
1. Inserite un titolo per il profilo, ad esempio `Sample Metadata`, e fate clic su **[!UICONTROL Crea]**. Viene visualizzato [!UICONTROL Modifica modulo] per il profilo di metadati.

   ![Modificare un modulo di metadati](assets/metadata-edit-form.png)

1. Fate clic su un componente e configuratene le proprietà nella scheda **[!UICONTROL Impostazioni]** . Ad esempio, fare clic sul componente **[!UICONTROL Descrizione]** e modificarne le proprietà.

   ![Impostazione di un componente nel profilo di metadati](assets/metadata-profile-component-setting.png)

   Modificate le seguenti proprietà per il componente **[!UICONTROL Descrizione]** :

   * **[!UICONTROL Etichetta]** campo: Nome visualizzato della proprietà metadata. È solo per il riferimento utente.

   * **[!UICONTROL Mappa su proprietà]**: Il valore di questa proprietà fornisce il percorso o il nome relativo al nodo della risorsa in cui viene salvata nella directory archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

   ![Mappa su impostazione proprietà nel profilo di metadati](assets/metadata-profile-setting-map-property.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Ad esempio, se specificate `./jcr:content/metadata/dc:desc` come nome della proprietà **** Mappa su, [!DNL Assets] memorizza il valore `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore]** predefinito: Utilizzare questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specificate &quot;Descrizione personale&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

   ![Impostazione della descrizione predefinita nel profilo di metadati](assets/metadata-profile-setting-default-value.png)

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

1. Fate clic su **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nella pagina **[!UICONTROL Profili]** metadati.<br>

   ![Profilo metadati aggiunto nella pagina Profili metadati](assets/MetadataProfiles-page.png)

### Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili]** metadati, selezionate un profilo di metadati per copiarlo.

   ![Copiare un profilo di metadati](assets/metadata-profile-edit-copy-option.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo]** metadati, inserite un titolo per la nuova copia del profilo metadati.
1. Fate clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

   ![Una copia del profilo di metadati aggiunto nella pagina Profili metadati](assets/copy-metadata-profile.png)

### Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Nella pagina **[!UICONTROL Profili]** metadati, selezionate un profilo da eliminare.

1. Fate clic su **[!UICONTROL Elimina profili]** metadati nella barra degli strumenti.
1. Nella finestra di dialogo, fare clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo di metadati viene eliminato dall’elenco.

<!-- TBD: Revisit to find out the correct config. and update these steps.
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## Schema metadati per una cartella {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle delle risorse, che definiscono il layout e i metadati visualizzati nelle pagine di proprietà delle cartelle.

### Aggiunta di uno schema di metadati di una cartella {#add-a-folder-metadata-schema-form}

Usate l’editor Forms Schema metadati cartella per creare e modificare gli schemi di metadati per le cartelle.

1. Nell’ [!DNL Experience Manager] interfaccia, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di metadati **[!UICONTROL della cartella]**.
1. Nella pagina Forms [!UICONTROL Schema metadati] cartella, fate clic su **[!UICONTROL Crea]**.
1. Specify a name for the form, and click **[!UICONTROL Create]**. Il nuovo modulo schema è elencato nella pagina Forms  schema.

### Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

È possibile modificare un modulo di schema di metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi del modulo all&#39;interno delle schede.

È possibile mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema di metadati.

1. Nella pagina Schema Forms, selezionare il modulo creato, quindi selezionare l&#39;opzione **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartella, fare clic su `+` per aggiungere una scheda al modulo. Per rinominare la scheda, fare clic sul nome predefinito e specificare il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, fare clic su `+`. Fare clic `X` su una scheda per eliminarla.

1. Nella scheda attiva, aggiungere uno o più componenti dalla scheda **[!UICONTROL Genera modulo]** .

   ![adding_components](assets/adding_components.png)

   Se create più schede, fate clic su una scheda specifica per aggiungere i componenti.

1. Per configurare un componente, selezionatelo e modificatene le proprietà nella scheda **[!UICONTROL Impostazioni]** .

   Se necessario, eliminate un componente dalla scheda **[!UICONTROL Impostazioni]** .

   ![configure_properties](assets/configure_properties.png)

1. Fate clic su **[!UICONTROL Salva]** dalla barra degli strumenti per salvare le modifiche.

#### Componenti per la creazione di moduli {#components-to-build-forms}

Nella scheda **[!UICONTROL Genera modulo]** sono elencati gli elementi del modulo utilizzati nel modulo schema di metadati della cartella. Nella scheda **[!UICONTROL Impostazioni]** sono visualizzati gli attributi per ogni elemento selezionato nella scheda **[!UICONTROL Modulo]** di creazione. Elenco degli elementi del modulo disponibili nella scheda **[!UICONTROL Genera modulo]** :

| Nome componente | Descrizione |
|---|---|
| [!UICONTROL Intestazione sezione] | Aggiungere un&#39;intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungere una proprietà di testo su una sola riga. È memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungete una proprietà di testo con più valori. È memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungere un componente numero. |
| [!UICONTROL Data] | Aggiungere un componente data. |
| [!UICONTROL A discesa] | Aggiungere un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Campo nascosto] | Aggiungere un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa. |

#### Modifica degli elementi del modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, fare clic sul componente e modificare tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]** .

**[!UICONTROL Etichetta]** campo: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: Questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio CRX in cui viene salvato. Comincia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: Memorizza il valore nel nodo di metadati della cartella come proprietà `dc:title`.

* `./jcr:created`: Visualizza la proprietà JCR nel nodo della cartella. Se configurate queste proprietà in CRXDE,  Adobe consiglia di contrassegnarle come Disattiva modifica, perché sono protette. In caso contrario, l&#39;errore `Asset(s) failed to modify`&#39; si verifica quando si salvano le proprietà della risorsa.

Per garantire che il componente venga visualizzato correttamente nel modulo dello schema di metadati, non includete uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso]** JSON: Utilizzatelo per specificare il percorso del file JSON in cui specificate le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: Utilizzare questa proprietà per specificare il testo segnaposto relativo alla proprietà metadata.

**[!UICONTROL Scelte]**: Utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: Utilizzate questa proprietà per aggiungere una breve descrizione per il componente di metadati.

**[!UICONTROL Classe]**: Classe oggetto a cui è associata la proprietà.

### Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

È possibile eliminare i moduli dello schema di metadati della cartella dalla pagina Forms Schema metadati cartella. Per eliminare un modulo, selezionarlo e fare clic sull&#39;opzione Elimina dalla barra degli strumenti.

![delete_form](assets/delete_form.png)

### Assegnazione di uno schema di metadati di una cartella {#assign-a-folder-metadata-schema}

Potete assegnare uno schema di metadati a una cartella dalla pagina Forms Schema metadati cartella o durante la creazione di una cartella.

Se si configura uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato nella `folderMetadataSchema` proprietà del nodo della cartella in `./jcr:content`.

#### Assegnazione a uno schema dalla pagina Schema metadati cartella {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Nell’ [!DNL Experience Manager] interfaccia, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di metadati **[!UICONTROL della cartella]**.
1. Nella pagina Forms Schema metadati cartella, selezionate il modulo dello schema da applicare a una cartella.
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Applica alle cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi fare clic su **[!UICONTROL Applica]**. Se uno schema di metadati è già applicato alla cartella, un messaggio di avviso informa che lo schema di metadati esistente sta per essere sovrascritto. Fate clic su **[!UICONTROL Sovrascrivi]**.
1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Assegnazione di uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Quando create una cartella, potete assegnare uno schema di metadati a una cartella. Se nel sistema è presente almeno uno schema di metadati della cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** viene visualizzato un elenco aggiuntivo. È possibile selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcun schema.

1. Dall’interfaccia [!DNL Experience Manager Assets] utente, fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specificate un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartella, selezionate lo schema desiderato. Quindi fate clic su **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

### Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immettete i valori dei metadati nei vari campi e fate clic su **[!UICONTROL Salva]** per memorizzarli. I valori specificati vengono memorizzati nel nodo cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Suggerimenti e limitazioni {#best-practices-limitations}

* Per importare i metadati negli spazi dei nomi personalizzati, registrate prima gli spazi dei nomi.
* Il selettore proprietà visualizza le proprietà utilizzate negli editor di schemi e nei moduli di ricerca. Il selettore proprietà non seleziona le proprietà dei metadati da una risorsa.
* È possibile che siano già presenti profili di metadati preesistenti prima dell’aggiornamento alla versione [!DNL Experience Manager] 6.5. Dopo l’aggiornamento, se applicate un profilo simile in [!UICONTROL Proprietà] cartella nella scheda Profili  metadati, i campi dei moduli di metadati non vengono visualizzati. Tuttavia, se applicate un profilo di metadati appena creato, i campi del modulo vengono visualizzati ma non sono disponibili come previsto. Non si verificano perdite di funzionalità, ma se si desidera visualizzare i campi modulo (non disponibili), è necessario modificare e salvare i profili di metadati esistenti.

>[!MORELIKETHIS]
>
>* [Concetti di metadati e comprensione](metadata-concepts.md).
>* [Modificate le proprietà dei metadati di più raccolte](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk).
>* [Modificate le proprietà dei metadati di più raccolte](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk).
>* [Importazione ed esportazione di metadati in  risorse](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)Experience Manager.
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Best practice per organizzare le risorse digitali in modo da utilizzare i profili](/help/assets/organize-assets.md)di elaborazione.
>* [XMP riscritto](/help/assets/xmp-writeback.md).

