---
title: Accessibilità in Dynamic Media
description: Informazioni sul supporto per l’accessibilità nei visualizzatori Dynamic Media e Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibilità
role: Business Practitioner, Administrator
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: a4e9a4003bf0ce686578d3f8b3fddc19bc49dfb4
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Accessibilità in [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] supporta il controllo da tastiera e le tecnologie per l’accessibilità, come gli assistenti vocali JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto per l’accessibilità da tastiera in [!DNL Dynamic Media]

Poiché [!DNL Dynamic Media] è un plug-in a [!DNL Adobe Experience Manager Assets], la maggior parte del comportamento del controllo da tastiera è lo stesso di in [!DNL Experience Manager Assets]. Ad esempio, il pulsante `Cancel` in [!DNL Dynamic Media] ha la stessa evidenziazione dello stato attivo di [!DNL Experience Manager Assets] e reagisce al tasto `Spacebar` come in [!DNL Experience Manager Assets]. Consulta [Scelte rapide da tastiera in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Le sequenze di tasti supportate dai singoli elementi dell’interfaccia utente in [!DNL Dynamic Media] sono nella maggior parte dei casi ovvie e facili da scoprire. Il controllo da tastiera in [!DNL Dynamic Media] riguarda i seguenti elementi:

* Possibilità di utilizzare i tasti `Tab` e `Shift+Tab` per spostarsi tra gli elementi interattivi della pagina.
L’utilizzo di `Tab` sposta lo stato attivo sull’elemento successivo dell’interfaccia utente nell’ordine di tabulazione; l&#39;utilizzo di `Shift+Tab` riporta lo stato attivo sull&#39;elemento dell&#39;interfaccia utente precedente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale dell&#39;elemento dell&#39;interfaccia utente sullo schermo e si sposta in ordine da sinistra a destra, quindi dall&#39;alto verso il basso. Inoltre, se un campo presenta un errore, è possibile premere `Tab` per spostarlo nello stato attivo.
* Possibilità di utilizzare il tasto `Spacebar` e `Enter` per attivare elementi standard dell’interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l’evidenziazione dello stato attivo da tastiera. L’elemento dell’interfaccia utente attivo riceve un’indicazione di messa a fuoco visiva sotto forma di bordo intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare alcuni tasti di scelta rapida personalizzati, ad esempio i tasti freccia, per interagire con elementi dell’interfaccia utente complessi per riposizionare i punti attivi.
* Nell’editor video interattivo, puoi utilizzare `Spacebar` per selezionare un’immagine e aggiungerla a un segmento. Inoltre, puoi utilizzare il tasto `Backspace` per eliminare l’elemento selezionato dalla scheda **[!UICONTROL Contenuto]** . Inoltre, premere `Tab` funziona come desiderato per navigare tra gli elementi interattivi della pagina.
* Nell’editor Ritaglio immagini/Ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Utilizzare i tasti freccia per ritagliare le dimensioni della cornice, riposizionare l&#39;immagine o entrambi.
   * Il primo `Tab` stop evidenzia l&#39;intero fotogramma dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare la cornice.
   * Le quattro fermate successive sono i quattro angoli del telaio. `Tab` Quando lo stato attivo è posto su un angolo del fotogramma, l&#39;angolo è evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo mirato.
Consulta [Modifica del ritaglio avanzato o campione avanzato di una singola immagine](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto della tecnologia di assistenza in [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] gli elementi dell’interfaccia utente funzionano con tecnologie per l’accessibilità, come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga sui punti di riferimento utilizzando le scelte rapide da tastiera `D` o le aree che utilizzano le scelte rapide da tastiera `R`. Inoltre, viene riportata l’intestazione durante la navigazione tramite la scelta rapida da tastiera dell’intestazione `H`.

## Supporto per l’accessibilità da tastiera nei visualizzatori [!DNL Dynamic Media] {#keyboard-accessibility-for-dm-viewers}

Tutti i componenti predefiniti per visualizzatori [!DNL Dynamic Media] supportano l’accessibilità da tastiera per i clienti.

Consulta [Accesso facilitato alla tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento per i visualizzatori di Dynamic Media.

## Supporto della tecnologia di assistenza nei visualizzatori [!DNL Dynamic Media] {#assistive-technology-support-for-dm-viewers}

Tutti i componenti per visualizzatori [!DNL Dynamic Media] supportano ruoli e attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie per l’accessibilità, come gli assistenti vocali.
Consulta l’ **Argomento della Guida relativo al supporto per la tecnologia di assistenza** in qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento per i visualizzatori di Dynamic Media. Ad esempio, per il visualizzatore video, consulta [Supporto per la tecnologia di assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) o [Supporto per la tecnologia di supporto](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

>[!MORELIKETHIS]
>
>* [Accessibilità delle soluzioni Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

