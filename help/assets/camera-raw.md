---
title: Supporto di Camera Raw
description: Scopri come abilitare il supporto per Camera Raw in Risorse di Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Supporto per l&#39;elaborazione delle immagini con Camera Raw {#camera-raw-support}

Potete abilitare il supporto per Camera Raw per elaborare formati di file non elaborati, come CR2, NEF e RAF, ed eseguire il rendering delle immagini in formato JPEG. Questa funzionalità è supportata in Risorse Adobe Experience Manager mediante il pacchetto [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) Camera Raw disponibile tramite Package Share.

>[!NOTE]
>
>La funzionalità supporta solo le rappresentazioni JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.

Per abilitare il supporto per Camera Raw in Risorse Adobe Experience Manager, procedi come segue:

1. Scaricate il pacchetto [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) Camera Raw da Package Share.
1. Accesso `https://[aem_server]:[port]/workflow`. Aprite il flusso di lavoro Aggiorna risorsa **** DAM.
1. Aprite il passaggio Miniature **[!UICONTROL di]** processo.
1. Specificate la seguente configurazione nella scheda **[!UICONTROL Miniature]** :

   * **[!UICONTROL Miniature]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignora tipi MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`
   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, nel campo Elenco **** salti, specificare `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dal pannello laterale, aggiungete il passaggio **[!UICONTROL Camera Raw/DNG Handler]** sotto il passaggio di creazione **[!UICONTROL delle]** miniature.
1. Nel passaggio **[!UICONTROL Camera Raw/DNG Handler]** , aggiungi la seguente configurazione nella scheda **[!UICONTROL Argomenti]** :

   * **[!UICONTROL Tipi]** mime: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`
   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Assicurarsi che la configurazione di cui sopra sia la stessa del **[!UICONTROL campione DAM Update Asset With Camera RAW e della configurazione DNG Handling Step]** .

È ora possibile importare file da fotocamera in formato raw in Risorse AEM. Dopo aver installato il pacchetto Camera RAW e configurato il flusso di lavoro richiesto, nell’elenco dei riquadri laterali viene visualizzata l’opzione Regola **** immagine.

![chlimage_1-135](assets/chlimage_1-337.png)

*Figura: Opzioni nel riquadro laterale.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Utilizzate questa opzione per apportare modifiche leggere alle immagini.*

Dopo aver salvato le modifiche in un’immagine Camera Raw, `AdjustedPreview.jpg` viene generata una nuova rappresentazione per l’immagine. Per altri tipi di immagini eccetto Camera Raw, le modifiche si riflettono in tutte le rappresentazioni.

## Best practice, problemi noti e limitazioni {#best-practices}

La funzionalità presenta le seguenti limitazioni:

* La funzionalità supporta solo le rappresentazioni JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.
* Il writeback dei metadati non è supportato per i formati RAW e DNG.
* La libreria Camera Raw presenta dei limiti rispetto ai pixel totali che può elaborare alla volta. Al momento, può elaborare un massimo di 65000 pixel sul lato lungo di un file o 512 MP, indipendentemente dai criteri rilevati per primi.
