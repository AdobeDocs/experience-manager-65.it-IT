---
title: Anteprima delle risorse 3D
description: Scopri come visualizzare in anteprima le risorse 3D
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 16%

---


# Anteprima delle risorse 3D in AEM{#previewing-3d-assets-aem}

Adobe Experience Manager supporta il caricamento, la distribuzione e l’anteprima interattiva di risorse 3D come parte del processo di authoring.

Il visualizzatore 3D interattivo è disponibile dalla pagina dei dettagli delle risorse in AEM. Il visualizzatore include, tra le altre, una raccolta di controlli interattivi della videocamera che consentono di eseguire zoom, rotazione e scorrimento della risorsa 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formati supportati per l&#39;anteprima 3D in AEM {#supported-3d-previewing-assets}

L&#39;anteprima 3D interattiva supporta i seguenti formati di file:

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf binario |  |
| GLTF | Formato di trasmissione GL | model/gltf+json | Vedi **Nota** di seguito. |
| OBJ | File oggetto 3D WaveFront | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Sostegno solo all&#39;acquisizione; anteprima non disponibile. |
| USDZ | Universal Scene Descrizione Archivio ZIP | model/vnd.usdz+zip | Sostegno solo all&#39;acquisizione; anteprima non disponibile. |

**Nota**: Se il rendering dei materiali non viene eseguito in anteprima di un modello gLTF, assicurarsi che siano denominati correttamente e che si trovino in una  `textures` cartella nella stessa cartella principale del modello, in modo simile al seguente:

    Risorsa (cartella)
    model.
    gltfmodel.
    bintextures (cartella)
    material_0_baseColor.
    jpegmaterial_0_Normal.jpeg

## Considerazioni sulle prestazioni durante l&#39;anteprima delle risorse 3D in AEM{#performance-3d-previewing-assets}

Il tempo necessario per aprire una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa dipende da diversi fattori, come la larghezza di banda, la complessità delle immagini e le latenze al server.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo touch mobile, sono importanti anche quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

**Per visualizzare in anteprima le risorse 3D in AEM**

1. Assicurati di aver caricato le risorse 3D in AEM.
Consulta [Formati supportati per l&#39;anteprima 3D](#supported-3d-previewing-assets) e [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).
1. Da AEM, nella pagina **[!UICONTROL Navigazione]**, tocca **[!UICONTROL Risorse > File.]**

   ![Pagina di navigazione](/help/assets/assets-dm/navigation-assets.png)

1. Dall’elenco a discesa Visualizza posto nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Vista a schede]**, quindi individua la risorsa 3D da visualizzare in anteprima.

   ![Selezione scheda 3D](/help/assets/assets-dm/3d-card-select.png)
   _Nella Vista a schede, tocca la scheda della risorsa 3D da visualizzare in anteprima._

1. Tocca la scheda della risorsa 3D per aprirla nella pagina di visualizzazione dei dettagli della risorsa.

   ![Anteprima 3D interattiva](/help/assets/assets-dm/3d-preview.png)
   _Anteprima interattiva di una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa._
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:
   * **Girare la fotocamera** - Rotazione la visualizzazione intorno alla scena e agli oggetti 3D.
      * _Mouse_: Clic a sinistra + trascinamento.
      * _Schermata_ touch: Premere un dito singolo + trascinare.
   * **Panning della videocamera**: effettua il panning della vista a sinistra, a destra, su o giù.
      * _Mouse_: Fai clic con il pulsante destro del mouse e trascina.
      * _Schermata_ touch: Premere due dita + trascinare.
   * **Zoom della fotocamera** (Zoom della fotocamera) - Consente di ingrandire e ridurre le aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Schermata_ touch: Pizzico a due dita.
   * **Ricentrate la fotocamera** (Recenter your camera) - Riposizionate la fotocamera in un punto della scena 3D.
      * _Mouse_: Fare doppio clic.
      * _Schermata_ touch: Tocca due volte.
   * **Ripristina** - Nell’angolo in basso a destra della pagina, tocca l’icona Ripristina per ripristinare il punto di destinazione della visualizzazione al centro della risorsa 3D. Inoltre, la funzione Reset sposta la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità** a schermo intero - Per passare alla modalità a tutto schermo, tocca l’icona a schermo intero nell’angolo in basso a destra della pagina.

1. Al termine, vicino all’angolo superiore destro della pagina, tocca **[!UICONTROL Chiudi.]**
