---
title: Schema metadati per cartelle
description: Scopri come creare uno schema di metadati per le cartelle di risorse in  Adobe Experience Manager Risorse
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 6%

---


# Schema metadati per cartelle {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] consente di creare schemi di metadati per le cartelle delle risorse, che definiscono il layout e i metadati visualizzati nelle pagine di proprietà delle cartelle.

## Aggiunta di uno schema di metadati di una cartella {#add-a-folder-metadata-schema-form}

Usate l’editor Forms Schema metadati cartella per creare e modificare gli schemi di metadati per le cartelle.

1. Nell’ [!DNL Experience Manager] interfaccia, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di metadati **[!UICONTROL della cartella]**.
1. Nella pagina Forms [!UICONTROL Schema metadati] cartella, fate clic su **[!UICONTROL Crea]**.
1. Specify a name for the form, and click **[!UICONTROL Create]**. Il nuovo modulo schema è elencato nella pagina Forms  schema.

## Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

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

### Componenti per la creazione di moduli {#components-to-build-forms}

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

### Modifica degli elementi del modulo {#editing-form-items}

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

## Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

È possibile eliminare i moduli dello schema di metadati della cartella dalla pagina Forms Schema metadati cartella. Per eliminare un modulo, selezionarlo e fare clic sull&#39;opzione Elimina dalla barra degli strumenti.

![delete_form](assets/delete_form.png)

## Assegnazione di uno schema di metadati di una cartella {#assign-a-folder-metadata-schema}

Potete assegnare uno schema di metadati a una cartella dalla pagina Forms Schema metadati cartella o durante la creazione di una cartella.

Se si configura uno schema di metadati per una cartella, il percorso del modulo dello schema viene memorizzato nella `folderMetadataSchema` proprietà del nodo della cartella in .*/jcr:content*.

### Assegnazione a uno schema dalla pagina Schema metadati cartella {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Nell’ [!DNL Experience Manager] interfaccia, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > Schemi di metadati **[!UICONTROL della cartella]**.
1. Nella pagina Forms Schema metadati cartella, selezionate il modulo dello schema da applicare a una cartella.
1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Applica alle cartelle]**.

1. Selezionare la cartella in cui applicare lo schema, quindi fare clic su **[!UICONTROL Applica]**. Se uno schema di metadati è già applicato alla cartella, un messaggio di avviso informa che lo schema di metadati esistente sta per essere sovrascritto. Fate clic su **[!UICONTROL Sovrascrivi]**.
1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### Assegnazione di uno schema durante la creazione di una cartella {#assign-a-schema-when-creating-a-folder}

Quando create una cartella, potete assegnare uno schema di metadati a una cartella. Se nel sistema è presente almeno uno schema di metadati della cartella, nella finestra di dialogo **[!UICONTROL Crea cartella]** viene visualizzato un elenco aggiuntivo. È possibile selezionare lo schema desiderato. Per impostazione predefinita, non è selezionato alcun schema.

1. Dall’interfaccia [!DNL Experience Manager Assets] utente, fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Specificate un titolo e un nome per la cartella.
1. Dall’elenco Schema metadati cartella, selezionate lo schema desiderato. Quindi fate clic su **[!UICONTROL Crea]**.

   ![select_schema](assets/select_schema.png)

1. Aprite le proprietà dei metadati per la cartella a cui avete applicato lo schema di metadati.
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

## Utilizzare lo schema di metadati della cartella {#use-the-folder-metadata-schema}

Apri le proprietà di una cartella configurata con uno schema di metadati della cartella. A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. Seleziona questa scheda per visualizzare il modulo schema metadati della cartella.

Immettete i valori dei metadati nei vari campi e fate clic su **[!UICONTROL Salva]** per memorizzarli. I valori specificati vengono memorizzati nel nodo cartella nell&#39;archivio CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)
