---
title: Write-back XMP per le rappresentazioni
description: Scoprite in che modo la funzione di writeback XMP propaga le modifiche dei metadati per una risorsa a tutte le rappresentazioni o a specifiche della risorsa.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

Questa funzione di Write-back XMP in Risorse Adobe Experience Manager (AEM) replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa.

Quando modificate i metadati di una risorsa da Risorse AEM o durante il caricamento di tale risorsa, le modifiche vengono inizialmente memorizzate nel nodo della risorsa in Crx-De.

La funzione Write-back XMP propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui potete modificare la proprietà Titolo della risorsa `Classic Leather` a cui `Nylon`.

![metadati](assets/metadata.png)

In questo caso, Risorse AEM salva le modifiche alla proprietà **Titolo** nel `dc:title` parametro per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia, Risorse AEM non propaga automaticamente le modifiche ai metadati apportate alle rappresentazioni di una risorsa.

La funzione Write-back XMP consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

## Abilitazione della funzione di writeback XMP {#enabling-xmp-writeback}

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa al momento del caricamento, modificate la configurazione di **Adobe CQ DAM Rendition Maker** in Configuration Manager.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione di **Adobe CQ DAM Rendition Maker** .
1. Selezionate l&#39;opzione **Propaga XMP** , quindi salvate le modifiche.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Abilitazione della funzione di writeback XMP per rappresentazioni specifiche {#enabling-xmp-writeback-for-specific-renditions}

Per consentire alla funzione di WriteBack XMP di estendere le modifiche ai metadati per selezionare le rappresentazioni, specificate queste rappresentazioni nel passaggio del flusso di lavoro di WriteBack dei metadati XMP del flusso di lavoro di WriteBack dei metadati DAM. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per estendere i metadati alle miniature delle rappresentazioni 140.100.png e 319.319.png, effettuate le seguenti operazioni.

1. Toccate/fate clic sul logo AEM, quindi accedete a **Strumenti** > **Flusso** di lavoro > **Modelli**.
1. Dalla pagina Modelli, aprite il modello di flusso di lavoro **DAM Metadata Writeback** .
1. Nella pagina delle proprietà Write **dei metadati** DAM, aprite il passaggio **XMP Writeback Process** .
1. Nella finestra di dialogo Proprietà passaggio, toccate o fate clic sulla scheda **Processo** .
1. Nella casella **Argomenti** , aggiungete `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi toccate o fate clic su **OK**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni TIF piramidali per le immagini Dynamic Media con i nuovi attributi, aggiungi il passaggio **Dynamic Media Process Image Assets** al flusso di lavoro di Write-back dei metadati DAM.

   Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salvare il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle miniature delle rappresentazioni.140.100.png e thumbnail.319.319.png della risorsa, e non agli altri.

>[!NOTE]
>
>Per i problemi di reinserimento XMP in Linux a 64 bit, consultate [Come abilitare la riscrittura XMP su RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)a 64 bit.
>
>Per ulteriori informazioni sulle piattaforme supportate, consultate [Metadati XMP prerequisiti](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)per la riscrittura.

## Applicazione di filtri ai metadati XMP {#filtering-xmp-metadata}

AEM Assets supporta sia il filtro in blacklist che quello nella whitelist di proprietà/nodi per i metadati XMP letti dai binari delle risorse e memorizzati in JCR quando vengono assimilate le risorse.

Il filtro Blacklist consente di importare tutte le proprietà dei metadati XMP, ad eccezione delle proprietà specificate per l&#39;esclusione. Tuttavia, per i tipi di risorse come i file INDD con enormi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtraggio della blacklist consente di importare un gran numero di risorse con numerosi metadati XMP, l’istanza o il cluster AEM può incontrare problemi di stabilità, ad esempio code di osservazione bloccate.

Il filtro whitelist dei metadati XMP risolve questo problema consentendo di definire le proprietà XMP da importare. In questo modo, le altre proprietà XMP/sconosciute vengono ignorate. È possibile aggiungere alcune di queste proprietà al filtro blacklist per garantire la compatibilità con le versioni precedenti.

>[!NOTE]
>
>Il filtro funziona solo per le proprietà derivate da origini XMP nei file binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtro non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà denominata `CreateDate` in EXIF TIFF. AEM rileva questo valore nel campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtraggio non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione **Adobe CQ DAM XmpFilter** .
1. Per applicare il filtro della whitelist, selezionate **Applica whitelist alle proprietà** XMP e specificate le proprietà da importare nella casella Nomi XML **Whitelist per il filtro** XMP.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Per filtrare le proprietà XMP in blacklist dopo aver applicato il filtro della whitelist, specificatele nella casella Nomi XML **in blacklist per il filtro** XMP.

   >[!NOTE]
   >
   >L&#39;opzione **Applica lista nera alle proprietà** XMP è selezionata per impostazione predefinita. In altre parole, il filtro della blacklist è attivato per impostazione predefinita. Per disattivare il filtro della blacklist, deselezionate l&#39;opzione **Applica lista nera alle proprietà** XMP.

1. Salva le modifiche.
