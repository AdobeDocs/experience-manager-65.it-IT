---
title: Accessibilità in elementi multimediali dinamici
description: Informazioni sull’accessibilità nei visualizzatori per contenuti multimediali dinamici e per contenuti multimediali dinamici
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 696aaa54007e4a78fe6b07d8ba65660595286dca
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Accessibilità in [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] supporta le tecnologie di controllo della tastiera e di assistenza, come gli assistenti vocali JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto per l&#39;accessibilità da tastiera in [!DNL Dynamic Media]

Poiché [!DNL Dynamic Media] è un plug-in per [!DNL Adobe Experience Manager Assets], la maggior parte del comportamento dei controlli da tastiera è esattamente uguale a quello di [!DNL Experience Manager Assets]. Ad esempio, il `Cancel` pulsante in [!DNL Dynamic Media] ha la stessa evidenziazione dello stato attivo [!DNL Experience Manager Assets]e reagisce alla `Spacebar` chiave come in [!DNL Experience Manager Assets]. Consultate Scelte rapide da [tastiera in Risorse](/help/assets/accessibility.md#keyboard-shortcuts).

Nella maggior parte dei casi, i tasti supportati dai singoli elementi dell&#39;interfaccia utente [!DNL Dynamic Media] sono evidenti e facili da scoprire. Il controllo della tastiera in [!DNL Dynamic Media] è circa quanto segue:

* Possibilità di utilizzare `Tab` e `Shift+Tab` tasti per spostarsi tra gli elementi interattivi sulla pagina.
L&#39;utilizzo di `Tab` rende più attivo il successivo elemento dell&#39;interfaccia utente nell&#39;ordine di tabulazione; l&#39;utilizzo `Shift+Tab` ripristina l&#39;input dell&#39;elemento dell&#39;interfaccia utente precedente.
La barra laterale di messa a fuoco segue la posizione naturale dell&#39;elemento dell&#39;interfaccia utente sullo schermo e si sposta in ordine da sinistra a destra, quindi dall&#39;alto verso il basso. Inoltre, se un campo ha un errore, è possibile premere `Tab` per attivarlo.
* Possibilità di utilizzare il tasto `Spacebar` e `Enter` per attivare gli elementi standard dell&#39;interfaccia utente, ad esempio pulsanti, elenchi a discesa e così via.
* Possibilità di visualizzare l&#39;evidenziazione dello stato attivo. L&#39;elemento dell&#39;interfaccia utente attivo può ricevere un&#39;indicazione visiva come bordo intorno all&#39;elemento dell&#39;interfaccia utente.
* Nell&#39;editor dei punti di attivazione è possibile utilizzare alcuni tasti di scelta rapida personalizzati, ad esempio i tasti freccia, per interagire con elementi dell&#39;interfaccia utente complessi per riposizionare i punti di attivazione.
* Nell’editor video interattivo, potete usare l’icona `Spacebar` per selezionare un’immagine e aggiungerla a un segmento. Inoltre, potete utilizzare la `Backspace` chiave per eliminare l&#39;elemento selezionato dalla scheda **[!UICONTROL Contenuto]** . Inoltre, premendo `Tab` le funzioni desiderate per spostarsi tra gli elementi interattivi sulla pagina.
* Nell’editor Ritaglio immagine/Ritaglio avanzato, potete effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni della cornice, riposizionare l’immagine o entrambi.
   * La prima `Tab` interruzione evidenzia l’intera cornice dell’immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le quattro `Tab` fermate successive sono i quattro angoli del telaio. Quando lo stato attivo è posizionato su un angolo cornice, l&#39;angolo è evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Consultate [Modifica del ritaglio avanzato o del campione avanzato di una singola immagine](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto per la tecnologia di assistenza in [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] gli elementi dell&#39;interfaccia utente funzionano con tecnologie di assistenza come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si spostano i punti di riferimento tramite scelte rapide da tastiera `D` o aree geografiche utilizzando le scelte rapide da tastiera `R`. Inoltre, l&#39;intestazione viene riportata quando si naviga utilizzando la scelta rapida da tastiera del titolo `H`.

## Supporto per l&#39;accessibilità da tastiera nei [!DNL Dynamic Media] visualizzatori {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti [!DNL Dynamic Media] per visualizzatori integrati supportano l’accessibilità da tastiera per i clienti.

Consultate Accessibilità [della tastiera e navigazione](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento dei visualizzatori per contenuti multimediali dinamici.

## Supporto della tecnologia di assistenza nei [!DNL Dynamic Media] visualizzatori {#assistive-technology-support-for-dm-viewers}

Tutti i componenti [!DNL Dynamic Media] del visualizzatore supportano ruoli e attributi ARIA (Accessible Rich Internet Applications) per migliorare l&#39;integrazione con tecnologie di supporto come gli assistenti vocali.
Consultate l’argomento della guida del supporto **per la tecnologia di** assistenza in qualsiasi argomento del visualizzatore personalizzato nella guida di riferimento dei visualizzatori per contenuti multimediali dinamici. Ad esempio, consultate Supporto per la tecnologia [di assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore video o Supporto per la tecnologia di [assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

>[!MORELIKETHIS]
>
>* [Accessibilità per soluzioni  Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

