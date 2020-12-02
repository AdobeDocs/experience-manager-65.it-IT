---
title: Write-back XMP per le rappresentazioni
description: Scoprite in che modo la funzione di XMP writeback propaga le modifiche dei metadati di una risorsa a tutte le rappresentazioni o a specifiche della risorsa.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 5%

---


# Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

La funzione di XMP remix in [!DNL Adobe Experience Manager Assets] replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa. Quando modificate i metadati di una risorsa da [!DNL Experience Manager Assets] o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate nel nodo della risorsa in CRXDe. La funzione di XMP writeback propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui modificate la proprietà [!UICONTROL Title] della risorsa denominata `Classic Leather` in `Nylon`.

![metadati](assets/metadata.png)

In questo caso, la [!DNL Experience Manager Assets] salva le modifiche alla proprietà **[!UICONTROL Title]** nel parametro `dc:title` per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia, [!DNL Experience Manager Assets] non propaga automaticamente le modifiche apportate ai metadati alle rappresentazioni di una risorsa.

La funzione di XMP Write-back consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

## Abilitazione XMP writeback {#enabling-xmp-writeback}

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa durante il caricamento, modificate la configurazione di **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprire la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]**.
1. Selezionare l&#39;opzione **[!UICONTROL Propaga XMP]**, quindi salvare le modifiche.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Abilitazione XMP writeback per rappresentazioni specifiche {#enabling-xmp-writeback-for-specific-renditions}

Per consentire alla funzione di XMP WriteBack di diffondere le modifiche ai metadati per selezionare le rappresentazioni, specificate queste rappresentazioni nel passaggio del flusso di lavoro XMP WriteBack del flusso di lavoro [!UICONTROL DAM Metadata WriteBack]. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per estendere i metadati alle miniature delle rappresentazioni 140.100.png e 319.319.png, effettuate le seguenti operazioni.

1. Nell&#39;interfaccia del Experience Manager , passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli, aprire il modello di flusso di lavoro **[!UICONTROL Write-back metadati DAM]**.
1. Nella pagina delle proprietà **[!UICONTROL Writeback di metadati DAM]**, apri il passaggio **[!UICONTROL Processo write-back XMPs]**.
1. Nella finestra di dialogo [!UICONTROL Proprietà passaggio], fare clic sulla scheda **[!UICONTROL Processo]**.
1. Nella casella **Argomenti** aggiungere `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi fare clic su **OK**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni TIFF piramidali per le immagini [!DNL Dynamic Media] con i nuovi attributi, aggiungere il passaggio **[!UICONTROL Risorse immagine processo multimediale dinamico]** al flusso di lavoro [!UICONTROL Write-back di metadati DAM].

   Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salvare il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle miniature delle rappresentazioni.140.100.png e thumbnail.319.319.png della risorsa, e non agli altri.

>[!NOTE]
>
>Per XMP problemi di writeback in Linux a 64 bit, vedere [Come abilitare XMP riscrittura su RedHat Linux a 64 bit](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Per le piattaforme supportate, consultate [XMP prerequisiti per la riscrittura dei metadati](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrare XMP metadati {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] supporta sia  filtro elenco Bloccati che  elenco Consentiti di proprietà/nodi per XMP metadati letti dai file binari delle risorse e memorizzati in JCR quando vengono assimilate le risorse.

Il filtraggio mediante un elenco Bloccati  consente di importare tutte XMP proprietà di metadati, ad eccezione delle proprietà specificate per l’esclusione. Tuttavia, per i tipi di risorse come i file INDD con enormi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtraggio mediante un elenco Bloccati  consente l&#39;importazione di un gran numero di risorse con numerosi metadati XMP, la distribuzione [!DNL Experience Manager] può incontrare problemi di stabilità, ad esempio code di osservazione bloccate.

Il filtraggio XMP metadati tramite  elenco Consentiti risolve il problema consentendo di definire le proprietà XMP da importare. In questo modo, tutte le altre proprietà XMP o sconosciute vengono ignorate. Per compatibilità con versioni precedenti, potete aggiungere alcune di queste proprietà al filtro che utilizza un elenco Bloccati .

>[!NOTE]
>
>Il filtraggio funziona solo per le proprietà derivate XMP origini nei file binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtraggio non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà `CreateDate` in EXIF TIFF.  Experience Manager memorizza questo valore in un campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtraggio non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere a `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Per applicare un filtro tramite un elenco Consentiti , selezionare **[!UICONTROL Applica  Inserì nell&#39;elenco Consentiti a XMP proprietà]**, quindi specificare le proprietà da importare nella casella **[!UICONTROL Nomi XML consentiti per XMP filtro]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Per filtrare le proprietà bloccate XMP dopo aver applicato il filtro tramite  elenco Consentiti, specificate quelle nella casella **[!UICONTROL Nomi XML bloccati per XMP filtro]**.

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Applica  Inserii nell&#39;elenco Bloccati a proprietà XMP]** è selezionata per impostazione predefinita. In altre parole, per impostazione predefinita il filtraggio utilizzando un elenco Bloccati  è attivato. Per disattivare tale filtro, deselezionare l&#39;opzione **[!UICONTROL Applica  Inserii nell&#39;elenco Bloccati a proprietà XMP]**.

1. Salva le modifiche.
