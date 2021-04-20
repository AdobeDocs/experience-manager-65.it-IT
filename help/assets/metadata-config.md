---
title: Configurazione e amministrazione della funzionalità dei metadati.
description: Configurazione e amministrazione della funzionalità  [!DNL Experience Manager Assets] relativa all'aggiunta e alla gestione dei metadati.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Metadata
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 6%

---


# Configurazione e amministrazione della funzionalità dei metadati in [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] conserva i metadati per ogni risorsa. Consente di organizzare e classificare più facilmente le risorse e aiuta le persone che cercano una specifica risorsa. Grazie alla possibilità di mantenere e gestire i metadati con le risorse, puoi organizzare ed elaborare automaticamente le risorse in base ai relativi metadati. [!DNL Adobe Experience Manager Assets] consente agli amministratori di configurare e personalizzare la funzionalità dei metadati per modificare l’offerta di Adobe predefinita.

## Modifica schema metadati {#metadata-schema}

Per informazioni dettagliate, vedere [modificare i moduli dello schema metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registra uno spazio dei nomi personalizzato in [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puoi aggiungere i tuoi namespace all’interno di [!DNL Experience Manager]. Come sono disponibili spazi dei nomi predefiniti, ad esempio `cq`, `jcr` e `sling`, puoi disporre di uno spazio dei nomi per i metadati dell’archivio e l’elaborazione XML.

1. Accedi alla pagina di amministrazione del tipo di nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Per accedere alla pagina di amministrazione dello spazio dei nomi, fai clic su **[!UICONTROL Namespace]** nella parte superiore della pagina.
1. Per aggiungere uno spazio dei nomi, fai clic su **[!UICONTROL Nuovo]** nella parte inferiore della pagina.
1. Specifica uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML. Specifica l’ID sotto forma di URI e un prefisso associato per l’ID. Fai clic su **[!UICONTROL Salva]**.

## Configura i limiti per l&#39;aggiornamento in massa dei metadati {#bulk-metadata-update-limit}

Per evitare una situazione di rifiuto del servizio (DOS) come , [!DNL Enterprise Manager] limita il numero di parametri supportati in una richiesta Sling. Quando aggiorni i metadati di molte risorse in una sola volta, potresti raggiungere il limite e i metadati non vengono aggiornati per altre risorse. Enterprise Manager genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Per modificare il limite, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]** e modifica il valore di **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** Configurazione OSGi.

## Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo di metadati e applicalo a una cartella. Tutte le risorse successivamente caricate nella cartella ereditano i metadati predefiniti configurati nel profilo di metadati.

### Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]** e fai clic su **[!UICONTROL Crea]**.
1. Immetti un titolo per il profilo, ad esempio `Sample Metadata`, e fai clic su **[!UICONTROL Crea]**. Viene visualizzato il [!UICONTROL Modifica modulo] per il profilo di metadati.

   ![Modificare un modulo di metadati](assets/metadata-edit-form.png)

1. Fai clic su un componente e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]** . Ad esempio, fai clic sul componente **[!UICONTROL Descrizione]** e modificane le proprietà.

   ![Impostazione di un componente nel profilo metadati](assets/metadata-profile-component-setting.png)

   Modifica le seguenti proprietà per il componente **[!UICONTROL Descrizione]** :

   * **[!UICONTROL Etichetta]** campo: Nome visualizzato della proprietà metadati. È solo per il riferimento utente.

   * **[!UICONTROL Mappa su proprietà]**: Il valore di questa proprietà fornisce il percorso o il nome relativo al nodo della risorsa in cui viene salvata nell’archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

   ![Mappare all’impostazione della proprietà nel profilo metadati](assets/metadata-profile-setting-map-property.png)

   Il valore specificato per **[!UICONTROL Mappa su proprietà]** viene memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se specifichi `./jcr:content/metadata/dc:desc` come nome di **[!UICONTROL Mappa su proprietà]**, [!DNL Assets] memorizza il valore `dc:desc` nel nodo di metadati della risorsa.

   * **[!UICONTROL Valore]** predefinito: Utilizzare questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;La mia descrizione&quot;, questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

   ![Impostare la descrizione predefinita nel profilo metadati](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste già in . `/jcr:content/metadata` node) non visualizza la proprietà e il relativo valore nella pagina Proprietà della risorsa per impostazione predefinita. Per visualizzare la nuova proprietà nella pagina [!UICONTROL Proprietà] delle risorse, modifica il modulo schema corrispondente.

1. (Facoltativo) Aggiungi altri componenti alla scheda Modifica modulo dalla scheda **[!UICONTROL Genera modulo]** e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili dalla scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Etichetta campo, <br> descrizione |
| [!UICONTROL Testo su riga singola] | Etichetta campo <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Testo con più valori] | Etichetta campo <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Numero] | Etichetta campo <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Data] | Etichetta campo <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Tag standard] | Etichetta campo <br> Mappa su proprietà, <br> Valore predefinito, <br> Descrizione |

1. Fare clic su **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all&#39;elenco dei profili nella pagina **[!UICONTROL Profili metadati]**.<br>

   ![Profilo metadati aggiunto nella pagina Profili metadati](assets/MetadataProfiles-page.png)

### Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]** , seleziona un profilo di metadati per crearne una copia.

   ![Copiare un profilo di metadati](assets/metadata-profile-edit-copy-option.png)

1. Fai clic su **[!UICONTROL Copia]** nella barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo metadati]**, immetti un titolo per la nuova copia del profilo metadati.
1. Fate clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

   ![Una copia del profilo metadati aggiunto nella pagina Profili metadati](assets/copy-metadata-profile.png)

### Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]** , seleziona un profilo da eliminare.

1. Fai clic su **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l’operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
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

### Aggiungi un modulo schema metadati cartella {#add-a-folder-metadata-schema-form}

Utilizza l’editor Forms per Schema metadati cartelle per creare e modificare schemi di metadati per le cartelle.

1. Nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cartella Schemi di metadati]**.
1. Nella pagina [!UICONTROL Schema metadati cartelle Forms], fai clic su **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo e fare clic su **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina [!UICONTROL Forms schema].

### Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

È possibile modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o nuovi elementi modulo al modulo schema metadati.

1. Nella pagina Forms schema, seleziona il modulo creato, quindi seleziona l’opzione **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle, fare clic su `+` per aggiungere una scheda al modulo. Per rinominare la scheda, fai clic sul nome predefinito e specifica il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, fai clic su `+`. Fai clic su `X` in una scheda per eliminarla.

1. Nella scheda attiva, aggiungi uno o più componenti dalla scheda **[!UICONTROL Genera modulo]** .

   ![add_components](assets/adding_components.png)

   Se crei più schede, fai clic su una scheda specifica per aggiungere componenti.

1. Per configurare un componente, selezionalo e modificane le proprietà nella scheda **[!UICONTROL Impostazioni]** .

   Se necessario, elimina un componente dalla scheda **[!UICONTROL Impostazioni]** .

   ![configure_properties](assets/configure_properties.png)

1. Fai clic su **[!UICONTROL Salva]** nella barra degli strumenti per salvare le modifiche.

#### Componenti per creare moduli {#components-to-build-forms}

La scheda **[!UICONTROL Genera modulo]** elenca gli elementi del modulo utilizzati nel modulo schema metadati della cartella. La scheda **[!UICONTROL Impostazioni]** visualizza gli attributi per ogni elemento selezionato nella scheda **[!UICONTROL Genera modulo]** . Elenco degli elementi del modulo disponibili nella scheda **[!UICONTROL Genera modulo]** :

| Nome componente | Descrizione |
|---|---|
| [!UICONTROL Intestazione sezione] | Aggiungi un’intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungi un componente numerico. |
| [!UICONTROL Data] | Aggiungi un componente data . |
| [!UICONTROL A discesa] | Aggiungi un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Campo nascosto] | Aggiungi un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa. |

#### Modifica degli elementi del modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, fare clic sul componente e modificare tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]** .

**[!UICONTROL Etichetta]** campo: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: Questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: Memorizza il valore nel nodo di metadati della cartella come proprietà  `dc:title`.

* `./jcr:created`: Visualizza la proprietà JCR nel nodo della cartella. Se configuri queste proprietà in CRXDE, Adobe consiglia di contrassegnarle come Disabilita modifica, perché sono protette. In caso contrario, l’errore &#39; `Asset(s) failed to modify`&#39; si verifica quando salvi le proprietà della risorsa.

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso]** JSON: Usarlo per specificare il percorso del file JSON in cui specificare coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: Utilizzare questa proprietà per specificare il testo segnaposto pertinente relativo alla proprietà metadati.

**[!UICONTROL Scelte]**: Utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: Utilizza questa proprietà per aggiungere una breve descrizione per il componente metadati.

**[!UICONTROL Classe]**: Classe oggetto a cui è associata la proprietà.

### Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

È possibile eliminare i moduli schema metadati cartelle dalla pagina Forms Schema metadati cartelle. Per eliminare un modulo, selezionarlo e fare clic sull’opzione Elimina sulla barra degli strumenti.

![delete_form](assets/delete_form.png)

### Assegnare uno schema di metadati della cartella {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati a una cartella dalla pagina Forms Schema metadati cartelle o durante la creazione di una cartella.

Se si configura uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato nella proprietà `folderMetadataSchema` del nodo della cartella in `./jcr:content`.

#### Assegna a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Nell&#39;interfaccia [!DNL Experience Manager] vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Cartella Schemi di metadati]**.
1. Nella pagina Forms Schema metadati cartelle selezionare il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Applica a cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi fare clic su **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema di metadati, un messaggio di avviso segnala che lo schema di metadati esistente sta per essere sovrascritto. Fare clic su **[!UICONTROL Sovrascrivi]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![folder_properties](assets/folder_properties.png)

   Per visualizzare i campi di metadati della cartella, fai clic sulla scheda **[!UICONTROL Folder Metadata]** (Metadati cartella).

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

È possibile assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema esiste almeno uno schema di metadati della cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** viene visualizzato un elenco aggiuntivo. È possibile selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcun schema.

1. Dall&#39;interfaccia utente [!DNL Experience Manager Assets], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, selezionare lo schema desiderato. Quindi, fai clic su **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi di metadati della cartella, fai clic sulla scheda **[!UICONTROL Folder Metadata]** (Metadati cartella).

### Utilizza lo schema metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina della cartella [!UICONTROL Proprietà] viene visualizzata una scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immetti i valori dei metadati nei vari campi e fai clic su **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Suggerimenti e limitazioni {#best-practices-limitations}

* Per importare i metadati negli spazi dei nomi personalizzati, registra innanzitutto gli spazi dei nomi.
* Selettore proprietà visualizza le proprietà utilizzate negli editor dello schema e nei moduli di ricerca. Il selettore proprietà non seleziona le proprietà dei metadati da una risorsa.
* È possibile che siano presenti profili di metadati preesistenti prima dell&#39;aggiornamento a [!DNL Experience Manager] 6.5. Dopo l&#39;aggiornamento, se si applica tale profilo nella cartella [!UICONTROL Proprietà] nella scheda [!UICONTROL Profili metadati], i campi del modulo metadati non vengono visualizzati. Tuttavia, se si applica un profilo di metadati appena creato, i campi del modulo vengono visualizzati ma non sono disponibili come previsto. Non si verifica alcuna perdita di funzionalità, ma se desideri visualizzare i campi del modulo (non disponibili), modifica e salva i profili di metadati esistenti.

>[!MORELIKETHIS]
>
>* [Concetti di metadati e comprensione](metadata-concepts.md).
>* [Modifica le proprietà dei metadati di più raccolte](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importazione ed esportazione di metadati in Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html).
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Best practice per organizzare le risorse digitali in modo da utilizzare i profili](/help/assets/organize-assets.md) di elaborazione.
>* [XMP di nuovo](/help/assets/xmp-writeback.md).

