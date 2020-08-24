---
title: Come modificare o aggiungere i metadati
description: Scoprite i metadati delle risorse [!DNL Adobe Experience Manager Assets] in vari modi per modificarli.
contentOwner: AG
translation-type: tm+mt
source-git-commit: fc14ccc834c9a41b67eb8cf17dd8b34f5dff2406
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# Come modificare o aggiungere i metadati {#how-to-edit-or-add-metadata}

I metadati sono informazioni aggiuntive sulla risorsa ricercabile. Viene estratto automaticamente quando caricate un’immagine. Potete modificare i metadati esistenti o aggiungere nuove proprietà di metadati al campo esistente, ad esempio quando un campo di metadati è vuoto.

Le organizzazioni hanno bisogno di vocabolari di metadati controllati e affidabili. Pertanto [!DNL Experience Manager Assets] non è possibile aggiungere su richiesta nuove proprietà di metadati. Gli sviluppatori e non gli autori possono aggiungere nuovi campi di metadati per le risorse. Consultate [Creare le proprietà dei metadati per le risorse](meta-edit.md#editing-metadata-schema).

## Modificare i metadati di una risorsa {#editing-metadata-for-an-asset}

Per modificare i metadati, effettuate le seguenti operazioni:

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

## Modifica schema metadati {#editing-metadata-schema}

Per informazioni dettagliate, vedere [Modificare i moduli](metadata-schemas.md#edit-metadata-schema-forms)degli schemi di metadati.

## Registra uno spazio nomi personalizzato all&#39;interno di [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Potete aggiungere spazi dei nomi personalizzati all&#39;interno [!DNL Experience Manager]. Allo stesso modo in cui esistono spazi dei nomi predefiniti come `cq`, `jcr`e `sling`, potete avere uno spazio dei nomi per i metadati dell&#39;archivio e l&#39;elaborazione XML.

1. Accedere alla pagina di amministrazione del tipo di nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Per accedere alla pagina di amministrazione dello spazio dei nomi, fare clic su **[!UICONTROL Spazi dei nomi]** nella parte superiore della pagina.
1. Per aggiungere uno spazio nomi, fate clic su **[!UICONTROL Nuovo]** nella parte inferiore della pagina.
1. Specificate uno spazio nomi personalizzato nella convenzione spazio nomi XML. Specificate l’ID sotto forma di URI e il prefisso associato per l’ID. Fai clic su **[!UICONTROL Salva]**.

## Suggerimenti e limitazioni {#best-practices-limitations}

* Gli aggiornamenti dei metadati tramite l&#39;interfaccia touch modificano le proprietà dei metadati nello `dc` spazio dei nomi. Eventuali aggiornamenti effettuati tramite l’API HTTP modificano le proprietà dei metadati nello `jcr` spazio nomi. Scoprite [come aggiornare i metadati mediante l&#39;API](/help/assets/mac-api-assets.md#update-asset-metadata)HTTP.

>[!MORELIKETHIS]
>
>* [Informazioni sui metadati e le relative esigenze in Risorse](metadata.md)
>* [Metadati XMP](xmp.md)
>* [Riferimento schemi metadati](meta-ref.md)

