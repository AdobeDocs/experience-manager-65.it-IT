---
title: Configurazione e amministrazione della funzionalità metadati.
description: Configurazione e amministrazione di [!DNL Experience Manager Assets] funzionalità relative all'aggiunta e alla gestione dei metadati.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 4%

---

# Configurazione e amministrazione della funzionalità metadati in [!DNL Assets] {#config-metadata}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | Questo articolo |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] conserva i metadati per ogni risorsa. Consente di categorizzare e organizzare più facilmente le risorse e aiuta le persone alla ricerca di una risorsa specifica. Grazie alla possibilità di conservare e gestire i metadati con le risorse, è possibile organizzare ed elaborare automaticamente le risorse in base ai relativi metadati. [!DNL Adobe Experience Manager Assets] consente agli amministratori di configurare e personalizzare la funzionalità dei metadati per modificare l’offerta Adobe predefinita.

## Modifica schema metadati {#metadata-schema}

Per ulteriori informazioni, consulta [modifica moduli schema metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registrare uno spazio dei nomi personalizzato in [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puoi aggiungere spazi dei nomi personalizzati in [!DNL Experience Manager]. Così come sono presenti spazi dei nomi predefiniti, ad esempio `cq`, `jcr`, e `sling`, è possibile disporre di uno spazio dei nomi per i metadati del repository e l&#39;elaborazione XML.

1. Accedere alla pagina di amministrazione del tipo di nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Per accedere alla pagina di amministrazione dello spazio dei nomi, fai clic su **[!UICONTROL Namespace]** nella parte superiore della pagina.
1. Per aggiungere uno spazio dei nomi, fai clic su **[!UICONTROL Nuovo]** nella parte inferiore della pagina.
1. Specificare uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML. Specifica l’ID sotto forma di URI e di un prefisso associato per l’ID. Fai clic su **[!UICONTROL Salva]**.

## Configurare i limiti per l’aggiornamento in blocco dei metadati {#bulk-metadata-update-limit}

Per evitare una situazione di tipo Denial of Service (DOS), [!DNL Enterprise Manager] limita il numero di parametri supportati in una richiesta Sling. Quando aggiorni contemporaneamente i metadati di molte risorse, potresti raggiungere il limite e i metadati non vengono aggiornati per altre risorse. Enterprise Manager genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Per modificare il limite, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]** e modificare il valore di **[!UICONTROL Parametri POST massimi]** in **[!UICONTROL Gestione dei parametri delle richieste Apache Sling]** Configurazione OSGi.

## Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo di metadati e applicalo a una cartella. Qualsiasi risorsa caricata successivamente nella cartella eredita i metadati predefiniti configurati nel profilo di metadati.

### Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili metadati]** e fai clic su **[!UICONTROL Crea]**.
1. Inserisci un titolo per il profilo, ad esempio `Sample Metadata`e fai clic su **[!UICONTROL Crea]**. Il [!UICONTROL Modifica modulo] per il profilo di metadati.

   ![Modificare un modulo di metadati](assets/metadata-edit-form.png)

1. Fai clic su un componente e configurane le proprietà nella sezione **[!UICONTROL Impostazioni]** scheda. Ad esempio, fai clic su **[!UICONTROL Descrizione]** e modificarne le proprietà.

   ![Impostazione di un componente nel profilo metadati](assets/metadata-profile-component-setting.png)

   Modifica le seguenti proprietà per **[!UICONTROL Descrizione]** componente:

   * **[!UICONTROL Etichetta campo]**: nome visualizzato della proprietà dei metadati. È solo per riferimento utente.

   * **[!UICONTROL Mappa su proprietà]**: il valore di questa proprietà fornisce il percorso o il nome relativo del nodo della risorsa in cui viene salvato nell’archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

   ![Mappa su impostazione proprietà nel profilo metadati](assets/metadata-profile-setting-map-property.png)

   Il valore specificato per **[!UICONTROL Mappa su proprietà]** viene memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se specifichi `./jcr:content/metadata/dc:desc` come nome di **[!UICONTROL Mappa su proprietà]**, [!DNL Assets] memorizza il valore `dc:desc` nel nodo dei metadati della risorsa. L’Adobe consiglia di mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona l’ultimo campo aggiunto mappato alla proprietà.

   * **[!UICONTROL Valore predefinito]**: utilizza questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;Descrizione&quot; questo valore viene assegnato alla proprietà `dc:desc` nel nodo dei metadati della risorsa.

   ![Imposta descrizione predefinita nel profilo metadati](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste in `/jcr:content/metadata` ) non visualizza la proprietà e il relativo valore sul [!UICONTROL Proprietà] pagina per impostazione predefinita. Per visualizzare la nuova proprietà sulle risorse [!UICONTROL Proprietà] , modificare il modulo schema corrispondente.

1. (Facoltativo) In **[!UICONTROL Genera modulo]** , aggiungere altri componenti a [!UICONTROL Modifica modulo]e configurarne le proprietà in **[!UICONTROL Impostazioni]** scheda. Le seguenti proprietà sono disponibili nel **[!UICONTROL Genera modulo]** scheda:

| Componente | Proprietà |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Etichetta campo, <br> Descrizione |
| [!UICONTROL Testo su riga singola] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Testo con più valori] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Numero] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Data] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito |
| [!UICONTROL Tag standard] | Etichetta campo, <br> Mappa su proprietà, <br> Valore predefinito, <br> Descrizione |

1. Clic **[!UICONTROL Fine]**. Il profilo metadati viene aggiunto all’elenco dei profili nel **[!UICONTROL Profili metadati]** pagina.<br>

   ![Profilo metadati aggiunto nella pagina Profili metadati](assets/MetadataProfiles-page.png)

### Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla sezione **[!UICONTROL Profili metadati]** , seleziona un profilo di metadati per crearne una copia.

   ![Copiare un profilo di metadati](assets/metadata-profile-edit-copy-option.png)

1. Clic **[!UICONTROL Copia]** dalla barra degli strumenti.
1. In **[!UICONTROL Copia profilo metadati]** immetti un titolo per la nuova copia del profilo metadati.
1. Clic **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

   ![Una copia del profilo di metadati aggiunto nella pagina Profili metadati](assets/copy-metadata-profile.png)

### Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Dalla sezione **[!UICONTROL Profili metadati]** , selezionare un profilo da eliminare.

1. Clic **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l&#39;operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

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

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle di risorse, che definiscono il layout e i metadati visualizzati nelle pagine delle proprietà delle cartelle.

### Aggiungere un modulo schema metadati cartelle {#add-a-folder-metadata-schema-form}

Utilizza l’editor di Forms per lo schema metadati delle cartelle per creare e modificare gli schemi di metadati per le cartelle.

1. In entrata [!DNL Experience Manager] , vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Il giorno [!UICONTROL Forms schema metadati cartelle] pagina, fai clic su **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo e fare clic su **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato in [!UICONTROL Schema Forms] pagina.

### Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

Puoi modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema metadati.

1. Nella pagina Schema Forms selezionare il modulo creato, quindi selezionare **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle, fai clic su `+` per aggiungere una scheda al modulo. Per rinominare la scheda, fate clic sul nome di default e specificate il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![custom_tab](assets/custom_tab.png)

   Per aggiungere altre schede, fai clic su `+`. Per eliminare, fai clic su `X` su una scheda.

1. Nella scheda attiva, aggiungi uno o più componenti della **[!UICONTROL Genera modulo]** scheda.

   ![add_components](assets/adding_components.png)

   Se si creano più schede, fare clic su una scheda specifica per aggiungere componenti.

1. Per configurare un componente, selezionalo e modificane le proprietà in **[!UICONTROL Impostazioni]** scheda.

   Se necessario, elimina un componente dal **[!UICONTROL Impostazioni]** scheda.

   ![configure_properties](assets/configure_properties.png)

1. Per salvare le modifiche, seleziona **[!UICONTROL Salva]** dalla barra degli strumenti.

#### Componenti per la creazione di moduli {#components-to-build-forms}

Il **[!UICONTROL Genera modulo]** scheda elenca gli elementi del modulo utilizzati nel modulo schema metadati cartelle. Il **[!UICONTROL Impostazioni]** nella scheda vengono visualizzati gli attributi di ogni elemento selezionato nel **[!UICONTROL Genera modulo]** scheda. Di seguito è riportato un elenco degli elementi modulo disponibili nel **[!UICONTROL Genera modulo]** scheda:

| Nome componente | Descrizione |
|---|---|
| [!UICONTROL Intestazione sezione] | Aggiungi un’intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungi un componente numero. |
| [!UICONTROL Data] | Aggiungi un componente data. |
| [!UICONTROL A discesa] | Aggiungi un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Campo nascosto] | Aggiungi un campo nascosto. Viene inviato come parametro POST al salvataggio della risorsa. |

#### Modifica di elementi modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, fai clic sul componente e modifica tutte o un sottoinsieme delle seguenti proprietà in **[!UICONTROL Impostazioni]** scheda.

**[!UICONTROL Etichetta campo]**: nome della proprietà dei metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: questa proprietà specifica il percorso relativo del nodo della cartella nell’archivio CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova sotto il nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore come proprietà nel nodo di metadati della cartella `dc:title`.

* `./jcr:created`: visualizza la proprietà JCR nel nodo della cartella. Se configuri queste proprietà in CRXDE, l’Adobe consiglia di contrassegnarle come Disattiva modifica, in quanto sono protette. In caso contrario, l’errore &quot; `Asset(s) failed to modify`&quot; si verifica quando si salvano le proprietà della risorsa.

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso JSON]**: utilizzalo per specificare il percorso del file JSON in cui specificare le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: utilizza questa proprietà per specificare il testo segnaposto rilevante relativo alla proprietà dei metadati.

**[!UICONTROL Scelte]**: utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: utilizza questa proprietà per aggiungere una breve descrizione del componente metadati.

**[!UICONTROL Classe]**: classe oggetto a cui è associata la proprietà.

### Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

Puoi eliminare i moduli schema metadati cartelle dalla pagina Forms dello schema metadati cartelle. Per eliminare un modulo, selezionalo e fai clic sull’opzione Elimina nella barra degli strumenti.

![delete_form](assets/delete_form.png)

### Assegnare uno schema di metadati per le cartelle {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati di cartella a una cartella dalla pagina Forms dello schema metadati cartelle o durante la creazione di una cartella.

Se configuri uno schema di metadati per una cartella, il percorso del modulo schema viene memorizzato in `folderMetadataSchema` proprietà del nodo della cartella in `./jcr:content`.

#### Assegnare a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. In entrata [!DNL Experience Manager] , vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Dalla pagina Forms schema metadati cartelle, seleziona il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Applica a cartelle]**.

1. Seleziona la cartella in cui applicare lo schema, quindi fai clic su **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema metadati, un messaggio di avviso informa che stai per sovrascrivere lo schema metadati esistente. Clic **[!UICONTROL Sovrascrivere]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![folder_properties](assets/folder_properties.png)

   Per visualizzare i campi di metadati della cartella, fai clic su **[!UICONTROL Metadati cartella]** scheda.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Puoi assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema è presente almeno uno schema di metadati di cartella, viene visualizzato un elenco aggiuntivo nel **[!UICONTROL Crea cartella]** . Puoi selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcuno schema.

1. Dalla sezione [!DNL Experience Manager Assets] interfaccia utente, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, seleziona lo schema desiderato. Quindi, fai clic su **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi di metadati della cartella, fai clic su **[!UICONTROL Metadati cartella]** scheda.

### Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. A **[!UICONTROL Metadati cartella]** nella cartella [!UICONTROL Proprietà] pagina. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immetti i valori dei metadati nei vari campi e fai clic su **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell’archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Suggerimenti e limitazioni {#best-practices-limitations}

* Per importare metadati su spazi dei nomi personalizzati, registra innanzitutto gli spazi dei nomi.
* Il selettore proprietà visualizza le proprietà utilizzate negli editor di schema e nei moduli di ricerca. Il selettore proprietà non seleziona le proprietà dei metadati da una risorsa.
* Potresti avere profili di metadati preesistenti da prima dell&#39;aggiornamento a [!DNL Experience Manager] 6.5. Dopo l’aggiornamento, se applichi tale profilo nella cartella [!UICONTROL Proprietà] in [!UICONTROL Profili metadati] , i campi del modulo metadati non vengono visualizzati. Tuttavia, se applichi un profilo di metadati appena creato, i campi del modulo vengono visualizzati ma non sono disponibili come previsto. Non si verifica alcuna perdita di funzionalità, ma se desideri visualizzare i campi modulo (non disponibili) modifica e salva i profili di metadati esistenti.

>[!MORELIKETHIS]
>
>* [Concetti e informazioni sui metadati](metadata-concepts.md).
>* [Modificare le proprietà dei metadati di più raccolte](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importazione ed esportazione di metadati in Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Best practice per organizzare le risorse digitali per utilizzare i profili di elaborazione](/help/assets/organize-assets.md).
>* [Write-back XMP](/help/assets/xmp-writeback.md).

