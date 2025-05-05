---
title: Accessibilità in Dynamic Media
description: Scopri il supporto per l’accessibilità nei visualizzatori Dynamic Medie e Dynamic Medie.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
source-git-commit: ed7183efa57db6d97941e3acc99d126c2fc0f6c5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Accessibilità in [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] supporta il controllo da tastiera e le tecnologie per l&#39;accessibilità, ad esempio le utilità di lettura dello schermo JAWS e NVDA, nell&#39;interfaccia utente di creazione.

## Supporto per l&#39;accessibilità della tastiera in [!DNL Dynamic Media]

Poiché [!DNL Dynamic Media] è un plug-in di [!DNL Adobe Experience Manager Assets], la maggior parte del comportamento del controllo da tastiera è uguale a quello di [!DNL Experience Manager Assets]. Ad esempio, il pulsante `Cancel` in [!DNL Dynamic Media] ha la stessa evidenziazione di attivazione di [!DNL Experience Manager Assets] e reagisce alla chiave `Spacebar` come in [!DNL Experience Manager Assets]. Consulta [Scelte rapide da tastiera in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Le sequenze di tasti supportate dai singoli elementi dell&#39;interfaccia utente in [!DNL Dynamic Media] sono chiare e facili da individuare. Il controllo da tastiera in [!DNL Dynamic Media] riguarda:

* Possibilità di utilizzare le pressioni dei tasti `Tab` e `Shift+Tab` per spostarsi tra gli elementi interattivi della pagina.
L&#39;utilizzo di `Tab` fa avanzare lo stato attivo dell&#39;input all&#39;elemento successivo dell&#39;interfaccia utente nell&#39;ordine di tabulazione; l&#39;utilizzo di `Shift+Tab` riporta lo stato attivo dell&#39;input all&#39;elemento precedente dell&#39;interfaccia utente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale degli elementi dell&#39;interfaccia sullo schermo e si sposta da sinistra a destra e quindi dall&#39;alto al basso. Inoltre, se un campo presenta un errore, è possibile premere `Tab` per spostare lo stato attivo su di esso.
* Possibilità di utilizzare i tasti `Spacebar` e `Enter` per attivare gli elementi standard dell&#39;interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l&#39;evidenziazione di tastiera sull&#39;elemento attivo. L’elemento dell’interfaccia utente che ha lo stato attivo sull’input riceve un’indicazione dello stato attivo visivo come bordo rappresentato intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare la pressione di alcuni tasti personalizzati, ad esempio i tasti di direzione, per interagire con elementi complessi dell’interfaccia utente e riposizionare i punti attivi.
* Nell&#39;editor video interattivo è possibile utilizzare `Spacebar` per selezionare un&#39;immagine e aggiungerla a un segmento. È inoltre possibile utilizzare la chiave `Backspace` per eliminare l&#39;elemento selezionato dalla scheda **[!UICONTROL Contenuto]**. Inoltre, premendo `Tab` è possibile spostarsi tra gli elementi interattivi della pagina.
* Nell’editor di ritaglio immagine/ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Usate i tasti freccia per ritagliare le dimensioni del fotogramma, o riposizionare l&#39;immagine, o entrambi.
   * La prima interruzione di `Tab` evidenzia l&#39;intero frame dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare il fotogramma.
   * Le prossime quattro `Tab` interruzioni sono i quattro angoli del frame. Quando lo stato attivo viene posizionato su un angolo del fotogramma, l&#39;angolo viene evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo attivo.
Vedi [Modifica il ritaglio avanzato o il campione avanzato di una singola immagine](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto per la tecnologia di supporto in [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

Gli elementi dell&#39;interfaccia utente [!DNL Dynamic Media] funzionano con tecnologie per l&#39;accessibilità, ad esempio utilità per la lettura dello schermo. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga tra i punti di riferimento utilizzando la scelta rapida da tastiera `D` o le aree utilizzando la scelta rapida da tastiera `R`. Inoltre, legge l&#39;intestazione quando si naviga utilizzando la scelta rapida da tastiera per l&#39;intestazione `H`.

## Supporto dell&#39;accessibilità della tastiera in [!DNL Dynamic Media] visualizzatori {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti predefiniti dei visualizzatori [!DNL Dynamic Media] supportano l&#39;accessibilità da tastiera per i clienti.

Consulta [Accesso facilitato alla tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=it) nella Guida di riferimento dei visualizzatori di Dynamic Medie.

## Supporto per la tecnologia di supporto in [!DNL Dynamic Media] visualizzatori {#assistive-technology-support-for-dm-viewers}

Tutti i componenti visualizzatore [!DNL Dynamic Media] supportano i ruoli e gli attributi ARIA (Accessible Rich Internet Applications) per migliorare l&#39;integrazione con tecnologie per l&#39;accessibilità, come gli assistenti vocali.
Vedere l&#39;argomento della Guida relativo al supporto tecnico **Assistive Technology** in qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento dei visualizzatori di Dynamic Medie. Ad esempio, consulta [Supporto per la tecnologia per l&#39;accesso facilitato](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html?lang=it) per il visualizzatore di video o [Supporto per la tecnologia per l&#39;accesso facilitato](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=it#viewers-for-aem-assets-only) per il visualizzatore di immagini interattivo.

## Supporto per sottotitoli codificati in Dynamic Medie {#closed-caption-support}

Dynamic Medie supporta la distribuzione di video e set di video adattivi con sottotitoli. I sottotitoli devono essere visualizzati sopra il contenuto video.

Vedi [Video in Dynamic Medie - Aggiungi sottotitoli al video](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Accessibilità per le soluzioni Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
