---
title: Configurazione e amministrazione della funzionalità metadati.
description: Configurazione e amministrazione della funzionalità  [!DNL Experience Manager Assets]  relativa all'aggiunta e alla gestione dei metadati.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 3%

---

# Configurazione e amministrazione della funzionalità metadati in [!DNL Assets] {#config-metadata}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=it) |
| AEM 6.5 | Questo articolo |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantiene i metadati per ogni risorsa. Consente di categorizzare e organizzare più facilmente le risorse e aiuta le persone alla ricerca di una risorsa specifica. Grazie alla possibilità di conservare e gestire i metadati con le risorse, è possibile organizzare ed elaborare automaticamente le risorse in base ai relativi metadati. [!DNL Adobe Experience Manager Assets] consente agli amministratori di configurare e personalizzare la funzionalità dei metadati per modificare l&#39;offerta Adobe predefinita.

## Modifica schema metadati {#metadata-schema}

Per ulteriori dettagli, vedere [modificare i moduli schema metadati](metadata-schemas.md#edit-metadata-schema-forms).

## Registra uno spazio dei nomi personalizzato in [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

È possibile aggiungere spazi dei nomi personalizzati in [!DNL Experience Manager]. Poiché sono presenti spazi dei nomi predefiniti come `cq`, `jcr` e `sling`, è possibile disporre di uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione XML.

1. Accedere alla pagina di amministrazione del tipo di nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Per accedere alla pagina di amministrazione dello spazio dei nomi, fai clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina.
1. Per aggiungere uno spazio dei nomi, fai clic su **[!UICONTROL Nuovo]** nella parte inferiore della pagina.
1. Specificare uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML. Specifica l’ID sotto forma di URI e di un prefisso associato per l’ID. Fai clic su **[!UICONTROL Salva]**.

## Configurare i limiti per l’aggiornamento in blocco dei metadati {#bulk-metadata-update-limit}

Per evitare una situazione di tipo Denial of Service (DOS), [!DNL Enterprise Manager] limita il numero di parametri supportati in una richiesta Sling. Quando aggiorni contemporaneamente i metadati di molte risorse, potresti raggiungere il limite e i metadati non vengono aggiornati per altre risorse. Enterprise Manager genera il seguente avviso nei registri:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Per modificare il limite, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]** e modifica il valore di **[!UICONTROL Parametri POST massimi]** nella **[!UICONTROL Gestione parametri richiesta Apache Sling]** configurazione OSGi.

## Profili metadati {#metadata-profiles}

Un profilo di metadati consente di applicare metadati predefiniti alle risorse all’interno di una cartella. Crea un profilo di metadati e applicalo a una cartella. Qualsiasi risorsa caricata successivamente nella cartella eredita i metadati predefiniti configurati nel profilo di metadati.

### Aggiungere un profilo di metadati {#adding-a-metadata-profile}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Profili metadati]** e fai clic su **[!UICONTROL Crea]**.
1. Immettere un titolo per il profilo, ad esempio `Sample Metadata`, e fare clic su **[!UICONTROL Crea]**. Viene visualizzato [!UICONTROL Modifica modulo] per il profilo metadati.

   ![Modifica modulo metadati](assets/metadata-edit-form.png)

1. Fai clic su un componente e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Ad esempio, fai clic sul componente **[!UICONTROL Descrizione]** e modificane le proprietà.

   ![Impostazione di un componente nel profilo metadati](assets/metadata-profile-component-setting.png)

   Modifica le seguenti proprietà per il componente **[!UICONTROL Descrizione]**:

   * **[!UICONTROL Etichetta campo]**: nome visualizzato della proprietà dei metadati. È solo per riferimento utente.

   * **[!UICONTROL Mappa su proprietà]**: il valore di questa proprietà fornisce il percorso relativo o il nome del nodo della risorsa in cui viene salvato nell&#39;archivio. Il valore deve sempre iniziare con `./` perché indica che il percorso si trova sotto il nodo della risorsa.

   ![Mappa su impostazione proprietà nel profilo metadati](assets/metadata-profile-setting-map-property.png)

   Il valore specificato per **[!UICONTROL Mappa su proprietà]** è memorizzato come proprietà sotto il nodo di metadati della risorsa. Ad esempio, se si specifica `./jcr:content/metadata/dc:desc` come nome di **[!UICONTROL Mappa sulla proprietà]**, [!DNL Assets] memorizza il valore `dc:desc` nel nodo di metadati della risorsa. L’Adobe consiglia di mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona l’ultimo campo aggiunto mappato alla proprietà.

   * **[!UICONTROL Valore predefinito]**: utilizzare questa proprietà per aggiungere un valore predefinito per il componente metadati. Ad esempio, se specifichi &quot;Descrizione&quot; questo valore viene assegnato alla proprietà `dc:desc` nel nodo di metadati della risorsa.

   ![Imposta la descrizione predefinita nel profilo metadati](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >L&#39;aggiunta di un valore predefinito a una nuova proprietà di metadati (che non esiste nel nodo `/jcr:content/metadata`) non visualizza la proprietà e il relativo valore nella pagina [!UICONTROL Proprietà] della risorsa per impostazione predefinita. Per visualizzare la nuova proprietà nella pagina [!UICONTROL Proprietà] delle risorse, modifica il modulo schema corrispondente.

1. (Facoltativo) Nella scheda **[!UICONTROL Genera modulo]**, aggiungi altri componenti a [!UICONTROL Modifica modulo] e configurane le proprietà nella scheda **[!UICONTROL Impostazioni]**. Le seguenti proprietà sono disponibili nella scheda **[!UICONTROL Genera modulo]**:

| Componente | Proprietà |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Etichetta Campo, Descrizione <br> |
| [!UICONTROL Testo su riga singola] | Etichetta campo, <br> Mappa sulla proprietà, <br> Valore predefinito |
| [!UICONTROL Testo con più valori] | Etichetta campo, <br> Mappa sulla proprietà, <br> Valore predefinito |
| [!UICONTROL Numero] | Etichetta campo, <br> Mappa sulla proprietà, <br> Valore predefinito |
| [!UICONTROL Data] | Etichetta campo, <br> Mappa sulla proprietà, <br> Valore predefinito |
| [!UICONTROL Tag standard] | Etichetta campo, <br> Mappa sulla proprietà, <br> Valore predefinito, <br> Descrizione |

1. Fai clic su **[!UICONTROL Fine]**. Il profilo metadati è stato aggiunto all&#39;elenco dei profili nella pagina **[!UICONTROL Profili metadati]**.<br>

   ![Profilo metadati aggiunto nella pagina Profili metadati](assets/MetadataProfiles-page.png)

### Copiare un profilo di metadati {#copying-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]**, seleziona un profilo metadati per crearne una copia.

   ![Copia un profilo metadati](assets/metadata-profile-edit-copy-option.png)

1. Fai clic su **[!UICONTROL Copia]** nella barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Copia profilo metadati]** immettere un titolo per la nuova copia del profilo metadati.
1. Fai clic su **[!UICONTROL Copia]**. La copia del profilo metadati viene visualizzata nell’elenco apposito della pagina **[!UICONTROL Profili metadati]**.

   ![Una copia del profilo metadati aggiunto nella pagina Profili metadati](assets/copy-metadata-profile.png)

### Eliminare un profilo di metadati {#deleting-a-metadata-profile}

1. Dalla pagina **[!UICONTROL Profili metadati]**, selezionare un profilo da eliminare.

1. Fare clic su **[!UICONTROL Elimina profili metadati]** nella barra degli strumenti.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Elimina]** per confermare l&#39;operazione di eliminazione. Il profilo metadati viene eliminato dall’elenco.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/it/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

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

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Nella pagina [!UICONTROL Schema metadati cartelle Forms] fare clic su **[!UICONTROL Crea]**.
1. Specificare un nome per il modulo e fare clic su **[!UICONTROL Crea]**. Il nuovo modulo schema è elencato nella pagina [!UICONTROL Schema Forms].

### Modifica moduli schema metadati cartelle {#edit-folder-metadata-schema-forms}

Puoi modificare un modulo schema metadati appena aggiunto o esistente, che include quanto segue:

* Schede
* Elementi modulo all’interno di schede.

Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere nuove schede o elementi del modulo al modulo schema metadati.

1. Nella pagina Forms schema selezionare il modulo creato, quindi selezionare l&#39;opzione **[!UICONTROL Modifica]** dalla barra degli strumenti.
1. Nella pagina Editor schema metadati cartelle fare clic su `+` per aggiungere una scheda al modulo. Per rinominare la scheda, fare clic sul nome predefinito e specificare il nuovo nome in **[!UICONTROL Impostazioni]**.

   ![scheda_personalizzata](assets/custom_tab.png)

   Per aggiungere altre schede, fare clic su `+`. Per eliminare, fare clic su `X` in una scheda.

1. Nella scheda attiva, aggiungi uno o più componenti dalla scheda **[!UICONTROL Genera modulo]**.

   ![aggiunta_componenti](assets/adding_components.png)

   Se si creano più schede, fare clic su una scheda specifica per aggiungere componenti.

1. Per configurare un componente, selezionarlo e modificarne le proprietà nella scheda **[!UICONTROL Impostazioni]**.

   Se necessario, eliminare un componente dalla scheda **[!UICONTROL Impostazioni]**.

   ![configure_properties](assets/configure_properties.png)

1. Per salvare le modifiche, seleziona **[!UICONTROL Salva]** nella barra degli strumenti.

#### Componenti per la creazione di moduli {#components-to-build-forms}

Nella scheda **[!UICONTROL Genera modulo]** sono elencati gli elementi del modulo utilizzati nel modulo schema metadati cartelle. Nella scheda **[!UICONTROL Impostazioni]** vengono visualizzati gli attributi di ogni elemento selezionato nella scheda **[!UICONTROL Genera modulo]**. Elenco degli elementi modulo disponibili nella scheda **[!UICONTROL Genera modulo]**:

| Nome componente | Descrizione |
|---|---|
| [!UICONTROL Intestazione sezione] | Aggiungi un’intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungi un componente numero. |
| [!UICONTROL Data] | Aggiungi un componente data. |
| [!UICONTROL Elenco a discesa] | Aggiungi un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Campo nascosto] | Aggiungi un campo nascosto. Viene inviato come parametro POST al salvataggio della risorsa. |

#### Modifica di elementi modulo {#editing-form-items}

Per modificare le proprietà degli elementi del modulo, fare clic sul componente e modificare tutte o un sottoinsieme delle seguenti proprietà nella scheda **[!UICONTROL Impostazioni]**.

**[!UICONTROL Etichetta campo]**: nome della proprietà dei metadati visualizzata nella pagina delle proprietà della cartella.

**[!UICONTROL Mappa su proprietà]**: questa proprietà specifica il percorso relativo del nodo della cartella nell&#39;archivio di CRX in cui viene salvato. Inizia con &quot;**./**&quot;, che indica che il percorso si trova nel nodo della cartella.

Di seguito sono riportati i valori validi per questa proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore nel nodo di metadati della cartella come proprietà `dc:title`.

* `./jcr:created`: visualizza la proprietà JCR nel nodo della cartella. Se configuri queste proprietà in CRXDE, l’Adobe consiglia di contrassegnarle come Disattiva modifica, in quanto sono protette. In caso contrario, l&#39;errore &#39; `Asset(s) failed to modify`&#39; si verifica quando si salvano le proprietà della risorsa.

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, non includere uno spazio nel percorso della proprietà.

**[!UICONTROL Percorso JSON]**: utilizzalo per specificare il percorso del file JSON in cui specificare le coppie chiave-valore per le opzioni.

**[!UICONTROL Segnaposto]**: utilizzare questa proprietà per specificare il testo segnaposto relativo alla proprietà dei metadati.

**[!UICONTROL Opzioni]**: utilizzare questa proprietà per specificare le scelte in un elenco.

**[!UICONTROL Descrizione]**: utilizzare questa proprietà per aggiungere una breve descrizione del componente metadati.

**[!UICONTROL Classe]**: classe oggetto a cui è associata la proprietà.

### Elimina moduli schema metadati cartelle {#delete-folder-metadata-schema-forms}

Puoi eliminare i moduli schema metadati cartelle dalla pagina Forms dello schema metadati cartelle. Per eliminare un modulo, selezionalo e fai clic sull’opzione Elimina nella barra degli strumenti.

![elimina_modulo](assets/delete_form.png)

### Assegnare uno schema di metadati per le cartelle {#assign-a-folder-metadata-schema}

È possibile assegnare uno schema di metadati di cartella a una cartella dalla pagina Forms dello schema metadati cartelle o durante la creazione di una cartella.

Se si configura uno schema metadati per una cartella, il percorso del modulo schema viene memorizzato nella proprietà `folderMetadataSchema` del nodo della cartella in `./jcr:content`.

#### Assegnare a uno schema dalla pagina Schema metadati cartelle {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati cartelle]**.
1. Dalla pagina Forms schema metadati cartelle, seleziona il modulo schema da applicare a una cartella.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Applica a cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi fare clic su **[!UICONTROL Applica]**. Se nella cartella è già applicato uno schema metadati, un messaggio di avviso informa che stai per sovrascrivere lo schema metadati esistente. Fai clic su **[!UICONTROL Sovrascrivi]**.
1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.

   ![proprietà_cartella](assets/folder_properties.png)

   Per visualizzare i campi dei metadati della cartella, fare clic sulla scheda **[!UICONTROL Metadati cartella]**.

   ![proprietà_metadati_cartelle](assets/folder_metadata_properties.png)

#### Assegnare uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Puoi assegnare uno schema di metadati della cartella durante la creazione di una cartella. Se nel sistema è presente almeno uno schema di metadati di cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** verrà visualizzato un elenco aggiuntivo. Puoi selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcuno schema.

1. Nell&#39;interfaccia utente di [!DNL Experience Manager Assets], fare clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Specifica un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartelle, seleziona lo schema desiderato. Quindi fare clic su **[!UICONTROL Crea]**.

   ![seleziona_schema](assets/select_schema.png)

1. Apri le proprietà dei metadati per la cartella a cui hai applicato lo schema metadati.
1. Per visualizzare i campi dei metadati della cartella, fare clic sulla scheda **[!UICONTROL Metadati cartella]**.

### Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. Nella pagina delle [!UICONTROL proprietà] della cartella viene visualizzata la scheda **[!UICONTROL Metadati cartella]**. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immetti i valori dei metadati nei vari campi e fai clic su **[!UICONTROL Salva]** per memorizzare i valori. I valori specificati vengono memorizzati nel nodo della cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Suggerimenti e limitazioni {#best-practices-limitations}

* Per importare metadati su spazi dei nomi personalizzati, registra innanzitutto gli spazi dei nomi.
* Il selettore proprietà visualizza le proprietà utilizzate negli editor di schema e nei moduli di ricerca. Il selettore proprietà non seleziona le proprietà dei metadati da una risorsa.
* Potresti avere profili di metadati preesistenti da prima dell&#39;aggiornamento a [!DNL Experience Manager] 6.5. Dopo l&#39;aggiornamento, se si applica un profilo di questo tipo nella cartella [!UICONTROL Proprietà] della scheda [!UICONTROL Profili metadati], i campi del modulo metadati non vengono visualizzati. Tuttavia, se applichi un profilo di metadati appena creato, i campi del modulo vengono visualizzati ma non sono disponibili come previsto. Non si verifica alcuna perdita di funzionalità, ma se desideri visualizzare i campi modulo (non disponibili) modifica e salva i profili di metadati esistenti.

>[!MORELIKETHIS]
>
>* [Concetti e informazioni sui metadati](metadata-concepts.md).
>* [Modifica proprietà metadati di più raccolte](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importazione ed esportazione di metadati in Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html?lang=it).
>* [Profili per elaborare metadati, immagini e video](processing-profiles.md).
>* [Procedure consigliate per organizzare le risorse digitali in modo da utilizzare i profili di elaborazione](/help/assets/organize-assets.md).
>* [Write-back XMP](/help/assets/xmp-writeback.md).
