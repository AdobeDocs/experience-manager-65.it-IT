---
title: Write-back XMP per le rappresentazioni
description: Scopri in che modo la funzione di XMP write-back propaga le modifiche ai metadati di una risorsa a tutte le rappresentazioni o a specifiche della risorsa.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cf86d0c38e326766b35318e78a94a3f32e166e01
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 5%

---


# Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

La funzione di XMP write-back in [!DNL Adobe Experience Manager Assets] replica le modifiche ai metadati delle risorse alle rappresentazioni della risorsa. Quando modifichi i metadati di una risorsa da [!DNL Experience Manager Assets] o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate nel nodo della risorsa in CRXDe. La funzione di XMP write-back propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considera uno scenario in cui modifichi la proprietà [!UICONTROL Title] della risorsa denominata `Classic Leather` in `Nylon`.

![Metadati](assets/metadata.png)

In questo caso, il [!DNL Experience Manager Assets] salva le modifiche alla proprietà **[!UICONTROL Title]** nel parametro `dc:title` per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_memorizzati](assets/metadata_stored.png)

Tuttavia, [!DNL Experience Manager Assets] non propaga automaticamente eventuali modifiche ai metadati delle rappresentazioni di una risorsa.

La funzione Writeback di XMP consente di propagare le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche nei file binari per le rappresentazioni.

## Abilitazione XMP writeback {#enabling-xmp-writeback}

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa durante il caricamento, modifica la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selezionare l&#39;opzione **[!UICONTROL Propaga XMP]**, quindi salvare le modifiche.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Abilitazione XMP ripristino per rappresentazioni specifiche {#enabling-xmp-writeback-for-specific-renditions}

Per consentire alla funzione XMP Writeback di propagare le modifiche ai metadati per selezionare le rappresentazioni, specifica queste rappresentazioni al passaggio del flusso di lavoro XMP Writeback Process del flusso di lavoro [!UICONTROL DAM Metadata WriteBack]. Per impostazione predefinita, questo passaggio è configurato con il rendering originale.

Per la funzione Writeback di XMP per la propagazione dei metadati alle miniature di rendering 140.100.png e 319.319.png, esegui questi passaggi.

1. Nell’interfaccia di Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli , apri il modello di flusso di lavoro **[!UICONTROL Writeback di metadati DAM]** .
1. Nella pagina delle proprietà **[!UICONTROL Writeback di metadati DAM]**, apri il passaggio **[!UICONTROL Processo write-back XMPs]**.
1. Nella finestra di dialogo [!UICONTROL Proprietà passaggio], fare clic sulla scheda **[!UICONTROL Processo]**.
1. Nella casella **Argomenti**, aggiungere `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi fare clic su **OK**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni TIFF piramidali per le immagini [!DNL Dynamic Media] con i nuovi attributi, aggiungi il passaggio **[!UICONTROL Dynamic Media Process Image Assets]** al flusso di lavoro [!UICONTROL DAM Metadata Writeback] .

   Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salva il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle rappresentazioni miniature.140.100.png e thumbnail.319.319.png della risorsa e non alle altre.

>[!NOTE]
>
>Per XMP problemi di write-back in Linux a 64 bit, vedere [Come abilitare XMP write-back su RedHat Linux a 64 bit](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Per le piattaforme supportate, consulta [XMP prerequisiti per la scrittura di metadati](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtro dei metadati XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] supporta sia l’elenco bloccato che l’elenco consentito di filtri di proprietà/nodi per XMP metadati letti dai binari delle risorse e memorizzati in JCR quando le risorse vengono acquisite.

Il filtro tramite un elenco bloccato consente di importare tutte le proprietà dei metadati XMP eccetto le proprietà specificate per l’esclusione. Tuttavia, per i tipi di risorse come i file INDD con grandi quantità di metadati XMP (ad esempio 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtro applicato a un elenco bloccato consente l’importazione di un gran numero di risorse con numerosi metadati XMP, la distribuzione [!DNL Experience Manager] può incontrare problemi di stabilità, ad esempio code di osservazione intasate.

Il filtro dei metadati XMP tramite l’elenco consentiti risolve questo problema consentendo di definire le proprietà XMP da importare. In questo modo, qualsiasi altra proprietà XMP o sconosciuta viene ignorata. Per la compatibilità con le versioni precedenti, puoi aggiungere alcune di queste proprietà al filtro che utilizza un elenco bloccato.

>[!NOTE]
>
>Il filtraggio funziona solo per le proprietà derivate XMP origini nei binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtro non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà `CreateDate` in EXIF TIFF. Experience Manager memorizza questo valore in un campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtro non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. Per applicare un filtro tramite un elenco consentito, selezionare **[!UICONTROL Applica elenco consentiti a XMP proprietà]** e specificare le proprietà da importare nella casella **[!UICONTROL Nomi XML consentiti per XMP filtro]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Per filtrare le proprietà bloccate XMP dopo aver applicato il filtro tramite l&#39;elenco Consentiti, specificare quelle nella casella **[!UICONTROL Nomi XML bloccati per XMP filtro]**.

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Applica elenco Bloccati a XMP proprietà]** è selezionata per impostazione predefinita. In altre parole, il filtraggio utilizzando un elenco bloccato è abilitato per impostazione predefinita. Per disattivare questo filtro, annulla la selezione dell&#39;opzione **[!UICONTROL Applica elenco Bloccati a XMP proprietà]** .

1. Salva le modifiche.
