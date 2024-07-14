---
title: Anteprima delle risorse 3D
description: Scopri come visualizzare in anteprima le risorse 3D in Experience Manager.
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 9%

---

# Anteprima di risorse 3D in Adobe Experience Manager {#previewing-3d-assets-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

Experience Manager supporta il caricamento, la consegna e l’anteprima interattiva di risorse 3D come parte del processo di authoring.

Il visualizzatore 3D interattivo è disponibile dalla pagina dei dettagli della risorsa in Experience Manager. Il visualizzatore include, tra le altre, una raccolta di controlli interattivi della videocamera che consentono di eseguire zoom, rotazione e scorrimento della risorsa 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formati supportati per l’anteprima 3D in Experience Manager {#supported-3d-previewing-assets}

L&#39;anteprima 3D interattiva supporta i seguenti formati di file:

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary | |
| GLTF | Formato di trasmissione GL | model/gltf+json | Vedi **Nota** di seguito. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif | |
| STL | Stereolitografia | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | Supporto solo per l’acquisizione; anteprima non disponibile. |
| USDZ | Universal Scene Description Archivio zip | model/vnd.usdz+zip | Supporto solo per l’acquisizione; anteprima non disponibile. |

>[!NOTE]
>
>Se i materiali non vengono riprodotti nell&#39;anteprima di un modello gLTF, assicurarsi che siano denominati correttamente e in una cartella `textures` nella stessa cartella principale del modello, in modo simile a quanto segue:

    Risorsa (cartella)
    model.gltf
    model.bin
    textures (cartella)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considerazioni sulle prestazioni quando si visualizza l’anteprima delle risorse 3D in Experience Manager{#performance-3d-previewing-assets}

Il tempo necessario per aprire una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa dipende da diversi fattori, quali la larghezza di banda, la complessità delle immagini e le latenze per il server.

Inoltre, le funzionalità del computer client, ad esempio una workstation, un notebook o un dispositivo touch mobile, sono importanti quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l&#39;esperienza di visualizzazione 3D interattiva più fluida e più favorevole.

**Per visualizzare in anteprima le risorse 3D nell&#39;Experience Manager:**

1. Assicurati di aver caricato risorse 3D in Experience Manager.
Consulta [Formati supportati per anteprima 3D](#supported-3d-previewing-assets) e [Carica Assets](/help/assets/manage-assets.md#uploading-assets).
1. Dall&#39;Experience Manager, nella pagina **[!UICONTROL Navigazione]**, selezionare **[!UICONTROL Assets]** > **[!UICONTROL File]**.

   ![Pagina di navigazione](/help/assets/assets-dm/navigation-assets.png)

1. Dall&#39;elenco a discesa Visualizza posto nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Vista a schede]**, quindi individua la risorsa 3D da visualizzare in anteprima.

   ![Selezione scheda 3D](/help/assets/assets-dm/3d-card-select.png)
   _Nella vista a schede, seleziona la scheda della risorsa 3D da visualizzare in anteprima._

1. Seleziona la scheda della risorsa 3D.

   ![Anteprima 3D interattiva](/help/assets/assets-dm/3d-preview.png)
   _Anteprima interattiva di una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa._
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Ruota fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fare clic con il pulsante destro del mouse e trascinare. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Reinserire la fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Doppia selezione. |
   | **Reimposta** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |   |   |

1. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
