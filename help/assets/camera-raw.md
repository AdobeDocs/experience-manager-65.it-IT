---
title: Supporto di [!DNL Adobe Camera Raw] per l'elaborazione di risorse digitali
description: Scopri come abilitare il supporto per [!DNL Adobe Camera Raw] in [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%
---
# Elabora immagini con [!DNL Adobe Camera Raw] {#camera-raw-support}

È possibile abilitare il supporto di [!DNL Adobe Camera Raw] per elaborare i formati di file non elaborati, ad esempio CR2, NEF e RAF, ed eseguire il rendering delle immagini in formato JPEG. La funzionalità è supportata in [!DNL Adobe Experience Manager Assets] utilizzando il [pacchetto Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponibile in Software Distribution.

>[!NOTE]
>
>Questa funzionalità supporta solo le rappresentazioni di JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.

Per abilitare il supporto di [!DNL Camera Raw] in [!DNL Experience Manager Assets], eseguire la procedura seguente:

1. Scarica il [[!DNL Camera Raw] pacchetto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) da [!DNL Software Distribution].
1. Accedi a `https://[aem_server]:[port]/workflow`. Apri il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Modifica il passaggio **[!UICONTROL Elabora miniature]**.
1. Fornisci la seguente configurazione nella scheda **[!UICONTROL Miniature]**:

   * **[!UICONTROL Miniature]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignora tipi MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Nella scheda **[!UICONTROL Immagine abilitata per il Web]**, nel campo **[!UICONTROL Elenco di salto]**, specificare `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dal pannello laterale, aggiungi il passaggio **[!UICONTROL Gestore Camera Raw/DNG]** sotto il passaggio **[!UICONTROL Elabora miniature]**.
1. Nel passaggio **[!UICONTROL Gestore Camera Raw/DNG]**, aggiungi la seguente configurazione nella scheda **[!UICONTROL Argomenti]**:

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
>Assicurati che la configurazione precedente sia la stessa della configurazione del **[!UICONTROL Esempio di risorsa di aggiornamento DAM con Camera Raw e del passaggio di gestione DNG]**.

Ora è possibile importare i file Camera Raw in Assets. Dopo aver installato il pacchetto Camera Raw e configurato il flusso di lavoro richiesto, nell&#39;elenco dei riquadri laterali viene visualizzata l&#39;opzione **[!UICONTROL Regola immagine]**.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: opzioni nel riquadro laterale.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: utilizzare l&#39;opzione per apportare modifiche leggere alle immagini.*

Dopo aver salvato le modifiche in un&#39;immagine [!DNL Camera Raw], viene generata una nuova rappresentazione `AdjustedPreview.jpg` per l&#39;immagine. Per gli altri tipi di immagine ad eccezione di [!DNL Camera Raw], le modifiche vengono applicate a tutte le rappresentazioni.

## Best practice, problemi noti e limitazioni {#best-practices}

La funzionalità presenta le seguenti limitazioni:

* Questa funzionalità supporta solo le rappresentazioni di JPEG. È supportato in Windows 64 Bit, Mac OS e RHEL 7.x.
* Il writeback dei metadati non è supportato per i formati RAW e DNG.
* La libreria [!DNL Camera Raw] presenta limitazioni sul totale di pixel che può elaborare alla volta. Attualmente, può elaborare un massimo di 65000 pixel sul lato lungo di un file o 512 MP, indipendentemente dai criteri incontrati per primi.
