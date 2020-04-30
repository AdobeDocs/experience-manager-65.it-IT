---
title: Come modificare o aggiungere i metadati
description: Scopri i metadati delle risorse in [!DNL Risorse Adobe Experience Manager] e vari modi per modificare i metadati delle risorse.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Come modificare o aggiungere i metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. Viene estratto automaticamente quando caricate un’immagine. Potete modificare i metadati esistenti o aggiungere nuove proprietà di metadati ai campi esistenti (ad esempio, quando un campo di metadati è vuoto).

Poiché le organizzazioni necessitano di vocabolari di metadati controllati e affidabili, [!DNL Experience Manager Assets] non consentono l&#39;aggiunta ad hoc di nuove proprietà di metadati. Sebbene gli autori non possano aggiungere nuovi campi di metadati per le risorse, gli sviluppatori possono farlo. Consultate [Creare nuove proprietà di metadati per le risorse](meta-edit.md#editing-metadata-schema).

## Modificare i metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati:

1. Effettua una delle operazioni seguenti:

   * Dall’ [!DNL Assets] interfaccia, selezionate la risorsa e fate clic su **[!UICONTROL Visualizza proprietà]** nella barra degli strumenti.
   * Dalla miniatura della risorsa, selezionate l’azione rapida **[!UICONTROL Visualizza proprietà]** .
   * Dalla pagina della risorsa, fate clic su **[!UICONTROL Visualizza proprietà]** ![chlimage_1-168](assets/chlimage_1-168.png) nella barra degli strumenti.
   Nella pagina della risorsa vengono visualizzati tutti i metadati della risorsa. I metadati vengono estratti quando la risorsa viene caricata (assimilata) in Experience Manager.

   ![selezionate Proprietà risorsa per visualizzare i metadati](assets/asset-metadata.png)

   *Figura: Modificate o aggiungete i metadati nella pagina Proprietà risorsa.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >Se un campo di testo è vuoto, non esiste alcun set di metadati. Potete immettere un valore nel campo e salvarlo per aggiungere la proprietà dei metadati.

Qualsiasi modifica ai metadati di una risorsa viene riscritta nel binario originale come parte dei dati XMP. Questa operazione viene eseguita tramite il flusso di lavoro di riscrittura dei metadati di Experience Manager. Le modifiche apportate alle proprietà esistenti (ad esempio `dc:title`) vengono sovrascritte e le proprietà create di recente (comprese le proprietà personalizzate come `cq:tags`) vengono aggiunte insieme allo schema.

La funzione di riscrittura XMP è supportata e abilitata per le piattaforme e i formati di file descritti nei requisiti [tecnici.](/help/sites-deploying/technical-requirements.md)

## Modifica schema metadati {#editing-metadata-schema}

Per informazioni dettagliate su come modificare lo schema di metadati, vedere [Modificare i moduli](metadata-schemas.md#edit-metadata-schema-forms)dello schema di metadati.

## Registrazione di uno spazio dei nomi personalizzato in Experience Manager {#registering-a-custom-namespace-within-aem}

Puoi aggiungere spazi dei nomi personalizzati in Experience Manager. Così come esistono spazi dei nomi predefiniti come cq, jcr e sling, potete avere uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione xml.

1. Vai alla pagina di amministrazione del tipo di nodo `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Fate clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina. La pagina di amministrazione dello spazio dei nomi viene visualizzata in una finestra.

1. Per aggiungere uno spazio nomi, fate clic su **[!UICONTROL Nuovo]** in basso.
1. Specificate uno spazio dei nomi personalizzato nella convenzione dello spazio dei nomi XML (specificate l’ID nel modulo di un URI e un prefisso associato per l’ID), quindi fate clic su **[!UICONTROL Salva]**.
