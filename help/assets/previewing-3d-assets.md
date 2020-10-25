---
title: Anteprima delle risorse 3D
description: Scopri come visualizzare in anteprima le risorse 3D
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 15%

---


# Anteprima delle risorse 3D in AEM{#previewing-3d-assets-aem}

Adobe Experience Manager supporta il caricamento, la distribuzione e l’anteprima interattiva di risorse 3D come parte del processo di authoring.

Il visualizzatore 3D interattivo è disponibile dalla pagina dei dettagli delle risorse in AEM. Il visualizzatore include, tra le altre, una raccolta di controlli interattivi della videocamera che consentono di eseguire zoom, rotazione e scorrimento della risorsa 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formati supportati per l&#39;anteprima 3D in AEM {#supported-3d-previewing-assets}

L&#39;anteprima 3D interattiva supporta i seguenti formati di file:

| Estensione dei file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binario | model/gltf-binary |  |
| GLTF | Formato di trasmissione GL | model/gltf+json | Vedi **Nota** di seguito. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| DN |  Adobe Dimension | model/x-adobe-dn | Sostegno solo all&#39;ingestione; Anteprima non disponibile. |
| USDZ | Archivio ZIP con descrizione universale di Scene7 | model/vnd.usdz+zip | Sostegno solo all&#39;ingestione; Anteprima non disponibile. |

**Nota**: Se il rendering dei materiali non viene eseguito in anteprima di un modello gLTF, accertatevi che siano denominati correttamente e che si trovino in una `textures` cartella nella stessa cartella principale del modello, in modo simile al seguente:

    Risorsa (cartella)
    model.
    gltfmodel.
    bintextures (cartella)
    Material_0_baseColor.
    jpegMaterial_0_normal.jpeg

## Considerazioni sulle prestazioni per l’anteprima delle risorse 3D in AEM{#performance-3d-previewing-assets}

Il tempo necessario per aprire una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa dipende da diversi fattori quali larghezza di banda, complessità dell’immagine e latenze verso il server.

Inoltre, le funzionalità del computer client, come una workstation, un notebook o un dispositivo touch mobile, sono importanti anche quando si modifica la telecamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l’esperienza di visualizzazione 3D interattiva più fluida e favorevole.

**Per visualizzare in anteprima le risorse 3D in AEM**

1. Assicurati di aver caricato le risorse 3D in AEM.
Consultate Formati [supportati per l’anteprima](#supported-3d-previewing-assets) 3D e per il [caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).
1. Da AEM, nella pagina di **[!UICONTROL navigazione]** toccate **[!UICONTROL Risorse > File.]**

   ![Pagina di navigazione](/help/assets/assets-dm/navigation-assets.png)

1. Dall’elenco a discesa Visualizza posto nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Vista a schede]**, quindi individua la risorsa 3D da visualizzare in anteprima.

   ![Selezione scheda 3D](/help/assets/assets-dm/3d-card-select.png)
   _Nella vista a schede, toccate la scheda della risorsa 3D da visualizzare in anteprima._

1. Toccate la scheda della risorsa 3D per aprirla nella pagina di visualizzazione dei dettagli della risorsa.

   ![Anteprima 3D interattiva](/help/assets/assets-dm/3d-preview.png)
   _Anteprima interattiva di una risorsa 3D nella pagina di visualizzazione dei dettagli della risorsa._
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettuate una delle seguenti operazioni:
   * **Ruotare la fotocamera**: orbita la vista intorno alla scena e agli oggetti 3D.
      * _Mouse_: Fare clic con il pulsante sinistro del mouse e trascinare.
      * _Touch screen_: Premere un dito singolo e trascinare.
   * **Scorrimento della videocamera**: consente di scorrere la vista verso sinistra, destra, verso l’alto o verso il basso.
      * _Mouse_: Fare clic con il pulsante destro del mouse e trascinare.
      * _Touch screen_: Premere due dita e trascinare.
   * **Zoom della fotocamera**- Zoom della fotocamera per spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D.
      * _Mouse_: Ruota di scorrimento.
      * _Touch screen_: Pizzicotto a due dita.
   * **Rientra la fotocamera**: consente di rientrare la fotocamera in un punto della scena 3D.
      * _Mouse_: Fate doppio clic.
      * _Touch screen_: Doppio tocco.
   * **Ripristina**(Reset) - Nell’angolo inferiore destro della pagina, toccate l’icona Ripristina per ripristinare il punto di destinazione della vista al centro della risorsa 3D. La funzione Reset (Reimposta) consente di spostare la telecamera più vicino o più lontano per mostrare la risorsa nella sua interezza e a una dimensione di visualizzazione ragionevole.
   * **Modalità** Schermo intero: per passare alla modalità Schermo intero, nell&#39;angolo inferiore destro della pagina toccate l&#39;icona Schermo intero.

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close.]**
