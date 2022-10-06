---
title: "[!DNL Adobe Camera Raw] supporto per l’elaborazione delle risorse digitali"
description: Scopri come abilitare [!DNL Adobe Camera Raw] supporto in [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Consente di elaborare le immagini utilizzando [!DNL Adobe Camera Raw] {#camera-raw-support}

È possibile abilitare [!DNL Adobe Camera Raw] supporto per l’elaborazione di formati di file non elaborati, come CR2, NEF e RAF, ed esecuzione del rendering delle immagini in formato JPEG. La funzionalità è supportata in [!DNL Adobe Experience Manager Assets] utilizzando [pacchetto Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponibile da Distribuzione di software.

>[!NOTE]
>
>La funzionalità supporta solo rappresentazioni di JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.

Per abilitare [!DNL Camera Raw] supporto in [!DNL Experience Manager Assets], segui questi passaggi:

1. Scarica la [[!DNL Camera Raw] pacchetto](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) da [!DNL Software Distribution].
1. Accesso `https://[aem_server]:[port]/workflow`. Apri **[!UICONTROL Risorsa di aggiornamento DAM]** workflow.
1. Modifica le **[!UICONTROL Miniature del processo]** passo.
1. Fornisci la seguente configurazione nel **[!UICONTROL Miniature]** scheda:

   * **[!UICONTROL Miniature]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignora tipi MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. In **[!UICONTROL Immagine abilitata per il web]** nella scheda **[!UICONTROL Ignora elenco]** campo , specifica `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dal pannello laterale, aggiungi la **[!UICONTROL Gestore Camera Raw/DNG]** sotto **[!UICONTROL Miniature del processo]** passo.
1. In **[!UICONTROL Gestore Camera Raw/DNG]** aggiungi la seguente configurazione nel **[!UICONTROL Argomenti]** scheda:

   * **[!UICONTROL Tipi di mime]**: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Fai clic su **[!UICONTROL Salva]**.

>[!NOTE]
>
>Assicurati che la configurazione di cui sopra sia la stessa del **[!UICONTROL Esempio di risorsa di aggiornamento DAM con passaggio di gestione Camera Raw e DNG]** configurazione.

È ora possibile importare file non elaborati della fotocamera in Assets. Dopo aver installato il pacchetto Camera Raw e configurato il flusso di lavoro richiesto, **[!UICONTROL Regolazione immagine]** nell’elenco dei riquadri laterali viene visualizzata l’opzione .

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opzioni nel riquadro laterale.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Utilizza l’opzione per apportare modifiche leggere alle immagini.*

Dopo aver salvato le modifiche in un [!DNL Camera Raw] immagine, una nuova rappresentazione `AdjustedPreview.jpg` viene generato per l’immagine. Per altri tipi di immagini eccetto [!DNL Camera Raw], le modifiche vengono applicate a tutte le rappresentazioni.

## Best practice, problemi noti e limitazioni {#best-practices}

La funzionalità presenta le seguenti limitazioni:

* La funzionalità supporta solo rappresentazioni di JPEG. È supportato su Windows a 64 bit, Mac OS e RHEL 7.x.
* Il write-back di metadati non è supportato per i formati RAW e DNG.
* La [!DNL Camera Raw] La libreria presenta limitazioni rispetto ai pixel totali che può elaborare alla volta. Attualmente, può elaborare un massimo di 65000 pixel sul lato lungo di un file o 512 MP qualunque sia il criterio che viene rilevato per primo.
