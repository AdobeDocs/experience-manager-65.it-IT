---
title: Write-back XMP per le rappresentazioni
description: Scoprite in che modo la funzione di XMP writeback propaga le modifiche dei metadati di una risorsa a tutte le rappresentazioni o a specifiche della risorsa.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 5%

---


# Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

La funzione di XMP writeback [!DNL Adobe Experience Manager Assets] replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa. Quando modificate i metadati di una risorsa dall’interno [!DNL Experience Manager Assets] o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate all’interno del nodo della risorsa in CRXDe. La funzione di XMP writeback propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui modificate la proprietà [!UICONTROL Titolo] della risorsa `Classic Leather` con titolo `Nylon`.

![metadati](assets/metadata.png)

In questo caso, [!DNL Experience Manager Assets] salva le modifiche alla proprietà **[!UICONTROL Titolo]** nel `dc:title` parametro per i metadati della risorsa memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia, [!DNL Experience Manager Assets] non propaga automaticamente le modifiche apportate ai metadati alle rappresentazioni di una risorsa.

La funzione di XMP Write-back consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

## Abilitazione XMP writeback {#enabling-xmp-writeback}

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa al momento del caricamento, modificate la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selezionare l&#39;opzione **[!UICONTROL Propaga XMP[!UICONTROL **, quindi salvare le modifiche.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Abilitazione XMP writeback per rappresentazioni specifiche {#enabling-xmp-writeback-for-specific-renditions}

Per consentire alla funzione di XMP WriteBack di diffondere le modifiche ai metadati per selezionare le rappresentazioni, specificate queste rappresentazioni nel passaggio del flusso di lavoro XMP Writeback Process del flusso di lavoro di WriteBack [!UICONTROL dei metadati] DAM. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per estendere i metadati alle miniature delle rappresentazioni 140.100.png e 319.319.png, effettuate le seguenti operazioni.

1. Nell&#39;interfaccia del Experience Manager , passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli, aprite il modello di flusso di lavoro **[!UICONTROL DAM Metadata Writeback]** .
1. Nella pagina delle proprietà **[!UICONTROL Writeback di metadati DAM]**, apri il passaggio **[!UICONTROL Processo write-back XMPs]**.
1. In the [!UICONTROL Step Properties] dialog box, click the **[!UICONTROL Process]** tab.
1. Nella casella **Argomenti** , aggiungere `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi fare clic su **OK**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. To regenerate the pyramid TIFF renditions for [!DNL Dynamic Media] images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the [!UICONTROL DAM Metadata Writeback] workflow.

   Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salvare il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle miniature delle rappresentazioni.140.100.png e thumbnail.319.319.png della risorsa, e non agli altri.

>[!NOTE]
>
>Per XMP problemi di writeback in Linux a 64 bit, vedere [Come abilitare XMP riscrittura su RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)a 64 bit.
>
>Per le piattaforme supportate, consultate [XMP prerequisiti](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)per la scrittura di metadati.

## Filtrare XMP metadati {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] supporta sia  filtro elenco Bloccati che  elenco Consentiti di proprietà/nodi per XMP metadati letti dai file binari delle risorse e memorizzati in JCR quando vengono assimilate le risorse.

Il filtraggio mediante un elenco Bloccati  consente di importare tutte XMP proprietà di metadati, ad eccezione delle proprietà specificate per l’esclusione. Tuttavia, per i tipi di risorse come i file INDD con enormi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtraggio mediante un elenco Bloccati  consente l’importazione di un gran numero di risorse con numerosi metadati XMP, la [!DNL Experience Manager] distribuzione può incontrare problemi di stabilità, ad esempio code di osservazione bloccate.

Il filtraggio XMP metadati tramite  elenco Consentiti risolve il problema consentendo di definire le proprietà XMP da importare. In questo modo, tutte le altre proprietà XMP o sconosciute vengono ignorate. Per compatibilità con versioni precedenti, potete aggiungere alcune di queste proprietà al filtro che utilizza un elenco Bloccati .

>[!NOTE]
>
>Il filtraggio funziona solo per le proprietà derivate XMP origini nei file binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtraggio non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà denominata `CreateDate` in EXIF TIFF.  Experience Manager memorizza questo valore in un campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtraggio non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Allowlist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Allowed XML Names for XMP filtering]** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Per filtrare XMP proprietà bloccate dopo aver applicato il filtro tramite  elenco Consentiti, specificate quelle nella casella Nomi XML **[!UICONTROL bloccati per XMP filtro]** .

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Applica  Inserii nell&#39;elenco Bloccati a XMP proprietà]** è selezionata per impostazione predefinita. In altre parole, per impostazione predefinita il filtraggio utilizzando un elenco Bloccati  è attivato. Per disattivare tale filtro, deselezionate l&#39;opzione **[!UICONTROL Applica  Inserii nell&#39;elenco Bloccati a XMP proprietà]** .

1. Salva le modifiche.
