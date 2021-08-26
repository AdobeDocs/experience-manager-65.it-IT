---
title: '[!DNL Adobe Camera Raw] supporto per l’elaborazione delle risorse digitali'
description: Scopri come abilitare il supporto [!DNL Adobe Camera Raw] in [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: 73e53f516d8e10b548f913db079c7e9812deb907
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 3%

---

# Elabora immagini utilizzando [!DNL Adobe Camera Raw] {#camera-raw-support}

È possibile abilitare il supporto [!DNL Adobe Camera Raw] per elaborare formati di file non elaborati, come CR2, NEF e RAF, ed eseguire il rendering delle immagini in formato JPEG. La funzionalità è supportata in [!DNL Adobe Experience Manager Assets] utilizzando il [pacchetto Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponibile da Distribuzione software.

>[!NOTE]
>
>La funzionalità supporta solo le rappresentazioni JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.

Per abilitare il supporto [!DNL Camera Raw] in [!DNL Experience Manager Assets], procedi come segue:

1. Scarica il [pacchetto Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) da [!DNL Software Distribution].
1. Accesso `https://[aem_server]:[port]/workflow`. Apri il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** .
1. Modifica il passaggio **[!UICONTROL Elabora miniature]** .
1. Fornisci la seguente configurazione nella scheda **[!UICONTROL Miniature]** :

   * **[!UICONTROL Miniature]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignora tipi MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Nella scheda **[!UICONTROL Immagine abilitata per il Web]**, nel campo **[!UICONTROL Ignora elenco]** , specifica `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dal pannello laterale, aggiungi il passaggio **[!UICONTROL Camera Raw/DNG Handler]** sotto il passaggio **[!UICONTROL Elabora miniature]** .
1. Nel passaggio **[!UICONTROL Camera Raw/DNG Handler]** , aggiungi la seguente configurazione nella scheda **[!UICONTROL Argomenti]** :

   * **[!UICONTROL Tipi]** MIME:  `image/dng` e  `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Assicurati che la configurazione di cui sopra sia la stessa della configurazione **[!UICONTROL Sample DAM Update Asset With Camera Raw and DNG Handling Step]** .

È ora possibile importare file non elaborati della fotocamera in Assets. Dopo aver installato il pacchetto Camera Raw e configurato il flusso di lavoro richiesto, l&#39;opzione **[!UICONTROL Regolazione immagine]** viene visualizzata nell&#39;elenco dei riquadri laterali.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opzioni nel riquadro laterale.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Utilizza l’opzione per apportare modifiche leggere alle immagini.*

Dopo aver salvato le modifiche a un&#39;immagine [!DNL Camera Raw], viene generato un nuovo rendering `AdjustedPreview.jpg` per l&#39;immagine. Per gli altri tipi di immagini eccetto [!DNL Camera Raw], le modifiche si riflettono in tutte le rappresentazioni.

## Best practice, problemi noti e limitazioni {#best-practices}

La funzionalità presenta le seguenti limitazioni:

* La funzionalità supporta solo le rappresentazioni JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.
* Il write-back di metadati non è supportato per i formati RAW e DNG.
* La libreria [!DNL Camera Raw] presenta limitazioni rispetto ai pixel totali che può elaborare alla volta. Attualmente, può elaborare un massimo di 65000 pixel sul lato lungo di un file o 512 MP qualunque sia il criterio che viene rilevato per primo.
