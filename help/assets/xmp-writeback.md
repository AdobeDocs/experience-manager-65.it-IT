---
title: Write-back XMP alle rappresentazioni
description: Scopri in che modo la funzione di writeback dell’XMP propaga le modifiche ai metadati di una risorsa a tutte le sue rappresentazioni o a quelle specifiche.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 6%

---

# Write-back XMP alle rappresentazioni {#xmp-writeback-to-renditions}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Questo articolo |

Questa funzionalità di writeback XMP in [!DNL Adobe Experience Manager Assets] replica le modifiche ai metadati nelle rappresentazioni della risorsa originale. Quando modifichi i metadati di una risorsa dall’interno di Assets o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate nel nodo dei metadati nella gerarchia delle risorse.

La funzione di writeback dell’XMP consente di propagare le modifiche ai metadati a tutte le rappresentazioni specifiche della risorsa. La funzione riscrive solo le proprietà dei metadati che utilizzano spazi dei nomi registrati, ovvero una proprietà denominata `dc:title` viene scritto ma una proprietà denominata `mytitle` non lo è.

Considera uno scenario in cui modifichi il [!UICONTROL Titolo] proprietà della risorsa con titolo `Classic Leather` a `Nylon`.

![metadati](assets/metadata.png)

In questo caso, il [!DNL Experience Manager Assets] salva le modifiche al **[!UICONTROL Titolo]** proprietà in `dc:title` parametro per i metadati della risorsa memorizzati nella gerarchia della risorsa.

![metadati_memorizzati](assets/metadata_stored.png)

Tuttavia, [!DNL Experience Manager Assets] non propaga automaticamente le modifiche ai metadati nelle rappresentazioni di una risorsa. Consulta [come abilitare il writeback dell’XMP](#enable-xmp-writeback).

## Abilita writeback XMP {#enable-xmp-writeback}

Per consentire la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa durante il caricamento, modifica la **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Adobe CQ DAM Rendition Maker]** configurazione.
1. Seleziona la **[!UICONTROL Propagazione dell’XMP]** e quindi salvare le modifiche.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Abilitazione del writeback XMP per rappresentazioni specifiche {#enabling-xmp-writeback-for-specific-renditions}

Per consentire alla funzione Writeback dell&#39;XMP di propagare le modifiche ai metadati per selezionare le rappresentazioni, specifica queste rappresentazioni nel passaggio del flusso di lavoro Processo write-back dell&#39;XMP di [!UICONTROL WriteBack metadati DAM] flusso di lavoro. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per la funzione Writeback di XMP per la propagazione dei metadati alle miniature di rendering 140.100.png e 319.319.png, eseguire la procedura seguente.

1. Nell’interfaccia di Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli, apri **[!UICONTROL Writeback di metadati DAM]** modello di workflow.
1. Nella pagina delle proprietà **[!UICONTROL Writeback di metadati DAM]**, apri il passaggio **[!UICONTROL Processo write-back XMPs]**.
1. In [!UICONTROL Proprietà passaggio] , fare clic sul pulsante **[!UICONTROL Processo]** scheda.
1. In **Argomenti** box, aggiungi `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e fai clic su **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni piramidali di TIFF [!DNL Dynamic Media] con i nuovi attributi, aggiungi le **[!UICONTROL Risorse di immagine del processo di Dynamic Medie]** passa a [!UICONTROL Writeback di metadati DAM] flusso di lavoro.

   Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salva il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle rappresentazioni delle miniature.140.100.png e miniatura.319.319.png della risorsa e non delle altre.

>[!NOTE]
>
>Per i problemi di writeback dell&#39;XMP in Linux a 64 bit, vedere [Come abilitare il write-back dell&#39;XMP su RedHat Linux a 64 bit](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Per le piattaforme supportate, vedi [Prerequisiti per il write-back dei metadati XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtraggio dei metadati XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] supporta sia il filtro elenco Bloccati che elenco Consentiti di proprietà/nodi per i metadati XMP letti dai file binari delle risorse e memorizzati in JCR al momento dell’acquisizione delle risorse.

L’utilizzo di un elenco Bloccati per filtrare consente di importare tutte le proprietà dei metadati XMP, ad eccezione delle proprietà specificate per l’esclusione. Tuttavia, per i tipi di risorse come i file INDD che presentano grandi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se filtrando con un elenco Bloccati si consente di importare un numero elevato di risorse con numerosi metadati XMP, il [!DNL Experience Manager] La distribuzione può incontrare problemi di stabilità, ad esempio code di osservazione intasate.

Il filtraggio dei metadati XMP tramite elenco Consentiti risolve questo problema consentendo di definire le proprietà XMP da importare. In questo modo, qualsiasi altra o sconosciuta proprietà XMP vengono ignorate. Per compatibilità con le versioni precedenti, puoi aggiungere alcune di queste proprietà al filtro che utilizza un elenco Bloccati.

>[!NOTE]
>
>Il filtro funziona solo per le proprietà derivate da origini XMP nei dati binari delle risorse. Per le proprietà derivate da fonti non XMP, come i formati EXIF e IPTC, il filtro non funziona. Ad esempio, la data di creazione della risorsa viene memorizzata nella proprietà denominata `CreateDate` in EXIF TIFF. Questo valore viene memorizzato in un campo di metadati denominato Experience Manager `exif:DateTimeOriginal`. Poiché l’origine non è XMP, il filtro non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Adobe CQ DAM XmpFilter]** configurazione.
1. Per applicare il filtro tramite un elenco Consentiti, seleziona **[!UICONTROL Applica il Inserisco nell&#39;elenco Consentiti di alle proprietà XMP]** e specificare le proprietà da importare nel **[!UICONTROL Nomi XML consentiti per il filtro XMP]** casella.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Per filtrare le proprietà dell’XMP bloccate dopo aver applicato il filtro tramite elenco Consentiti, specifica quelle nella sezione **[!UICONTROL Nomi XML bloccati per filtro XMP]** casella.

   >[!NOTE]
   >
   >Il **[!UICONTROL Applica il Inserisco nell&#39;elenco Bloccati di alle proprietà XMP]** è selezionata per impostazione predefinita. In altre parole, il filtro con un elenco Bloccati è attivato per impostazione predefinita. Per disattivare tale filtro, annulla la selezione del **[!UICONTROL Applica il Inserisco nell&#39;elenco Bloccati di alle proprietà XMP]** opzione.

1. Salva le modifiche.
