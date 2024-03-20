---
title: "[!DNL Adobe Camera Raw] supporto per l'elaborazione di risorse digitali"
description: Scopri come abilitare [!DNL Adobe Camera Raw] supporto in [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# Elabora immagini tramite [!DNL Adobe Camera Raw] {#camera-raw-support}

È possibile abilitare [!DNL Adobe Camera Raw] supporto per l’elaborazione di formati di file non elaborati, come CR2, NEF e RAF, e per il rendering delle immagini in formato JPEG. La funzionalità è supportata in [!DNL Adobe Experience Manager Assets] utilizzando [pacchetto Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponibile da Software Distribution.

>[!NOTE]
>
>Questa funzionalità supporta solo le rappresentazioni JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.

Per abilitare [!DNL Camera Raw] supporto in [!DNL Experience Manager Assets], effettua le seguenti operazioni:

1. Scarica il file [[!DNL Camera Raw] pacchetto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) da [!DNL Software Distribution].
1. Accesso `https://[aem_server]:[port]/workflow`. Apri **[!UICONTROL Aggiorna risorsa DAM]** flusso di lavoro.
1. Modifica il **[!UICONTROL Elabora miniature]** passaggio.
1. Fornisci la seguente configurazione in **[!UICONTROL Miniature]** scheda:

   * **[!UICONTROL Miniature]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignora tipi MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. In **[!UICONTROL Immagine abilitata per il web]** , nella scheda **[!UICONTROL Ignora elenco]** campo, specifica `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dal pannello laterale, aggiungi **[!UICONTROL Gestore Camera Raw/DNG]** passaggio sotto **[!UICONTROL Elabora miniature]** passaggio.
1. In **[!UICONTROL Gestore Camera Raw/DNG]** , aggiungi la seguente configurazione in **[!UICONTROL Argomenti]** scheda:

   * **[!UICONTROL Tipi MIME]**: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Assicurati che la configurazione precedente sia la stessa **[!UICONTROL Passaggio per risorsa di aggiornamento DAM di esempio con gestione DNG e Camera Raw]** configurazione.

Ora puoi importare i file Camera Raw in Assets. Dopo aver installato il pacchetto Camera Raw e configurato il flusso di lavoro richiesto, **[!UICONTROL Regolazione immagine]** nell&#39;elenco dei riquadri laterali.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opzioni nel riquadro laterale.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Utilizzare l&#39;opzione per apportare modifiche leggere alle immagini.*

Dopo aver salvato le modifiche in una [!DNL Camera Raw] immagine, una nuova rappresentazione `AdjustedPreview.jpg` viene generato per l&#39;immagine. Per altri tipi di immagini eccetto [!DNL Camera Raw], le modifiche vengono applicate a tutte le rappresentazioni.

## Best practice, problemi noti e limitazioni {#best-practices}

La funzionalità presenta le seguenti limitazioni:

* Questa funzionalità supporta solo le rappresentazioni JPEG. È supportato in Windows 64 Bit, Mac OS e RHEL 7.x.
* Il writeback dei metadati non è supportato per i formati RAW e DNG.
* Il [!DNL Camera Raw] la libreria ha limitazioni sul totale di pixel che può elaborare alla volta. Attualmente, può elaborare un massimo di 65000 pixel sul lato lungo di un file o 512 MP, indipendentemente dai criteri incontrati per primi.
