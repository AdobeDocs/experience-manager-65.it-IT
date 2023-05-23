---
title: Accessibilità in Dynamic Media
description: Scopri il supporto per l’accessibilità nei visualizzatori Dynamic Media e Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# Accessibilità in [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] supporta il controllo da tastiera e tecnologie per l’accessibilità, come le utilità di lettura dello schermo JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto dell’accessibilità della tastiera in [!DNL Dynamic Media]

Perché [!DNL Dynamic Media] è un plug-in per [!DNL Adobe Experience Manager Assets], la maggior parte del comportamento di controllo della tastiera è uguale a quello [!DNL Experience Manager Assets]. Ad esempio, il `Cancel` pulsante in [!DNL Dynamic Media] ha la stessa evidenziazione di messa a fuoco di [!DNL Experience Manager Assets], e reagisce al `Spacebar` chiave come in [!DNL Experience Manager Assets]. Consulta [Tasti di scelta rapida in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Tasti supportati dai singoli elementi dell’interfaccia utente in [!DNL Dynamic Media] sono chiari e facili da scoprire. Controllo da tastiera in [!DNL Dynamic Media] riguarda i seguenti elementi:

* Capacità di utilizzare `Tab` e `Shift+Tab` tasti per spostarsi tra gli elementi interattivi della pagina.
Utilizzo di `Tab` sposta lo stato attivo dell&#39;input sull&#39;elemento dell&#39;interfaccia utente successivo nell&#39;ordine di tabulazione; utilizzando `Shift+Tab` riporta lo stato attivo sull’elemento dell’interfaccia utente precedente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale degli elementi dell&#39;interfaccia sullo schermo e si sposta da sinistra a destra e quindi dall&#39;alto al basso. Inoltre, se un campo presenta un errore, è possibile premere `Tab` per spostare lo stato attivo su di esso.
* Possibilità di utilizzare `Spacebar` e `Enter` per attivare gli elementi standard dell’interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l&#39;evidenziazione di tastiera sull&#39;elemento attivo. L’elemento dell’interfaccia utente che ha lo stato attivo sull’input riceve un’indicazione dello stato attivo visivo come bordo rappresentato intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare la pressione di alcuni tasti personalizzati, ad esempio i tasti di direzione, per interagire con elementi complessi dell’interfaccia utente e riposizionare i punti attivi.
* Nell’editor video interattivo puoi utilizzare `Spacebar` per selezionare un’immagine e aggiungerla a un segmento. Inoltre, è possibile utilizzare `Backspace` chiave per eliminare l’elemento selezionato da **[!UICONTROL Contenuto]** scheda. Inoltre, premendo `Tab` funziona come desiderato per navigare tra gli elementi interattivi sulla pagina.
* Nell’editor di ritaglio immagine/ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni del fotogramma, o riposizionare l&#39;immagine, o entrambi.
   * Il primo `Tab` stop evidenzia l&#39;intero frame dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le prossime quattro `Tab` Le fermate sono i quattro angoli del frame. Quando lo stato attivo viene posizionato su un angolo del fotogramma, l&#39;angolo viene evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Consulta [Modificare il ritaglio o il campione avanzato di una singola immagine](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto di tecnologie assistive in [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] Gli elementi dell’interfaccia utente funzionano con tecnologie per l’accessibilità, come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga tra i punti di riferimento utilizzando la scelta rapida da tastiera `D` o aree tramite scelta rapida da tastiera `R`. Vengono inoltre narrate le intestazioni durante la navigazione utilizzando la scelta rapida da tastiera per le intestazioni `H`.

## Supporto dell’accessibilità della tastiera in [!DNL Dynamic Media] visualizzatori {#keyboard-accessibility-for-dm-viewers}

Tutto pronto all’uso [!DNL Dynamic Media] i componenti visualizzatori supportano l’accessibilità da tastiera per i clienti.

Consulta [Accessibilità della tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento dei visualizzatori di Dynamic Media.

## Supporto di tecnologie assistive in [!DNL Dynamic Media] visualizzatori {#assistive-technology-support-for-dm-viewers}

Tutti [!DNL Dynamic Media] I componenti visualizzatore supportano i ruoli e gli attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie per l’accessibilità, come gli assistenti vocali.
Consulta la **Supporto di tecnologie assistive** Argomento della Guida in linea di qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento dei visualizzatori di Dynamic Media. Ad esempio, consulta [Supporto di tecnologie assistive](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore Video, oppure [Supporto di tecnologie assistive](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

## Supporto per sottotitoli codificati in Dynamic Media {#closed-caption-support}

Dynamic Media supporta la distribuzione di video e set di video adattivi con sottotitoli. I sottotitoli devono essere visualizzati sopra il contenuto video.

Consulta [Video in Dynamic Media: aggiungi sottotitoli o sottotitoli al video](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Accessibilità per soluzioni di Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

