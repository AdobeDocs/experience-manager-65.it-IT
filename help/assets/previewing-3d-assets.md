---
title: Anteprima delle risorse 3D
description: Scopri come visualizzare in anteprima le risorse 3D
contentOwner: Rick Brough
docset: aem65
feature: Risorse 3D
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 10%

---

# Anteprima di risorse 3D in Adobe Experience Manager {#previewing-3d-assets-aem}

Experience Manager supporta il caricamento, la distribuzione e l’anteprima interattiva di risorse 3D come parte del processo di authoring.

Il visualizzatore 3D interattivo è disponibile nella pagina dei dettagli della risorsa in Experience Manager. Il visualizzatore include, tra le altre, una raccolta di controlli interattivi della videocamera che consentono di eseguire zoom, rotazione e scorrimento della risorsa 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formati supportati per l’anteprima 3D in Experience Manager {#supported-3d-previewing-assets}

L&#39;anteprima 3D interattiva supporta i seguenti formati di file:

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario |  |
| GLTF | Formato di trasmissione GL | model/gltf+json | Vedi **Nota** di seguito. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Sostegno solo all&#39;acquisizione; anteprima non disponibile. |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | Sostegno solo all&#39;acquisizione; anteprima non disponibile. |

>[!NOTE]
>
>Se il rendering dei materiali non viene eseguito in anteprima di un modello gLTF, accertarsi che il nome sia corretto e che si trovi in una cartella `textures` nella stessa cartella principale del modello, in modo simile al seguente:

    Risorsa (cartella)
    model.
    gltfmodel.
    bintextures (cartella)
    material_0_baseColor.
    jpegmaterial_0_Normal.jpeg

## Considerazioni sulle prestazioni quando si visualizzano in anteprima le risorse 3D in Experience Manager{#performance-3d-previewing-assets}

Il tempo necessario per aprire una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa dipende da diversi fattori, come la larghezza di banda, la complessità delle immagini e le latenze al server.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo touch mobile, sono importanti anche quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

**Per visualizzare in anteprima le risorse 3D, ad Experience Manager:**

1. Assicurati di aver caricato risorse 3D in Experience Manager.
Consulta [Formati supportati per l&#39;anteprima 3D](#supported-3d-previewing-assets) e [Carica risorse](/help/assets/manage-assets.md#uploading-assets).
1. Ad Experience Manager, nella pagina **[!UICONTROL Navigazione]**, seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.

   ![Pagina di navigazione](/help/assets/assets-dm/navigation-assets.png)

1. Dall’elenco a discesa Visualizza posto nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Vista a schede]**, quindi individua la risorsa 3D da visualizzare in anteprima.

   ![Selezione scheda 3D](/help/assets/assets-dm/3d-card-select.png)
   _In Vista a schede, selezionate la scheda della risorsa 3D da visualizzare in anteprima._

1. Seleziona la scheda della risorsa 3D.

   ![Anteprima 3D interattiva](/help/assets/assets-dm/3d-preview.png)
   _Anteprima interattiva di una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa._
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione touch screen |
   | --- | --- | --- | --- |
   | **Girare la fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Clic a sinistra + trascinamento. | Premere un dito singolo + trascinare. |
   | **Panning della fotocamera** | Consente di scorrere la visualizzazione a sinistra, a destra, in alto o in basso. | Fai clic con il pulsante destro del mouse e trascina. | Premere due dita + trascinare. |
   | **Zoom della fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Ruota di scorrimento. | Pizzico a due dita. |
   | **Ricollegare la fotocamera** | Rientra la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic. | Tocca due volte. |
   | **Ripristina** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole. |  |  |
   | **Modalità a tutto schermo** | Per passare alla modalità a tutto schermo, seleziona l’icona a schermo intero nell’angolo inferiore destro della pagina. |  |  |

1. Al termine, vicino all’angolo superiore destro della pagina, seleziona **[!UICONTROL Chiudi]**.
