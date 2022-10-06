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

[!DNL Dynamic Media] supporta il controllo da tastiera e le tecnologie per l’accessibilità, come gli assistenti vocali JAWS e NVDA, nell’interfaccia utente di authoring.

## Supporto per l’accessibilità da tastiera in [!DNL Dynamic Media]

Perché [!DNL Dynamic Media] è un plug-in per [!DNL Adobe Experience Manager Assets], la maggior parte del comportamento del controllo da tastiera è uguale a in [!DNL Experience Manager Assets]. Ad esempio, il `Cancel` ingresso pulsante [!DNL Dynamic Media] presenta lo stesso focus evidenziato in [!DNL Experience Manager Assets]e reagisce alle `Spacebar` come in [!DNL Experience Manager Assets]. Vedi [Scelte rapide da tastiera in Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Tasti supportati da singoli elementi dell’interfaccia utente in [!DNL Dynamic Media] sono chiari e facili da scoprire. Controllo della tastiera in [!DNL Dynamic Media] è incentrato sui seguenti argomenti:

* Possibilità di utilizzo `Tab` e `Shift+Tab` tasti per spostarsi tra gli elementi interattivi sulla pagina.
Utilizzo `Tab` sposta lo stato attivo al successivo elemento dell’interfaccia utente nell’ordine di tabulazione; utilizzo `Shift+Tab` ripristina lo stato attivo dell’interfaccia utente precedente.
L&#39;attraversamento della messa a fuoco segue la posizione naturale dell&#39;elemento dell&#39;interfaccia utente sullo schermo e si sposta in ordine da sinistra a destra, quindi dall&#39;alto verso il basso. Inoltre, se un campo ha un errore, puoi premere `Tab` per spostare lo stato attivo su di esso.
* Possibilità di utilizzare `Spacebar` e `Enter` per attivare elementi standard dell’interfaccia utente, ad esempio pulsanti ed elenchi a discesa.
* Possibilità di visualizzare l’evidenziazione dello stato attivo da tastiera. L’elemento dell’interfaccia utente attivo riceve un’indicazione di messa a fuoco visiva sotto forma di bordo intorno all’elemento dell’interfaccia utente.
* Nell’editor dei punti attivi è possibile utilizzare alcuni tasti di scelta rapida personalizzati, ad esempio i tasti freccia, per interagire con elementi dell’interfaccia utente complessi per riposizionare i punti attivi.
* Nell’editor video interattivo, puoi utilizzare la funzione `Spacebar` per selezionare un’immagine e aggiungerla a un segmento. Inoltre, puoi utilizzare la `Backspace` per eliminare l’elemento selezionato dalla **[!UICONTROL Contenuto]** scheda . Anche, premendo `Tab` funziona nel modo desiderato per navigare tra gli elementi interattivi della pagina.
* Nell’editor Ritaglio immagini/Ritaglio avanzato, puoi effettuare le seguenti operazioni:
   * Utilizzare i tasti freccia per ritagliare le dimensioni della cornice, riposizionare l&#39;immagine o entrambi.
   * Il primo `Tab` stop evidenzia l&#39;intero fotogramma dell&#39;immagine. È quindi possibile utilizzare i tasti freccia sulla tastiera per riposizionare la cornice.
   * I prossimi quattro `Tab` le fermate sono i quattro angoli del telaio. Quando lo stato attivo è posto su un angolo del fotogramma, l&#39;angolo è evidenziato. Anche in questo caso, è possibile utilizzare i tasti freccia sulla tastiera per spostare l&#39;angolo mirato.
Vedi [Modificare il ritaglio avanzato o il campione avanzato di una singola immagine](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Supporto tecnologico per l&#39;assistenza in [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] gli elementi dell’interfaccia utente funzionano con tecnologie per l’accessibilità, come gli assistenti vocali. Ad esempio, riconosce i punti di riferimento in una pagina quando si naviga sui punti di riferimento utilizzando le scelte rapide da tastiera `D` o regioni che utilizzano scelte rapide da tastiera `R`. Analizza anche l’intestazione quando si naviga utilizzando le scelte rapide da tastiera dell’intestazione `H`.

## Supporto per l’accessibilità da tastiera in [!DNL Dynamic Media] visualizzatori {#keyboard-accessibility-for-dm-viewers}

Tutto pronto [!DNL Dynamic Media] i componenti visualizzatori supportano l’accessibilità da tastiera per i clienti.

Vedi [Accesso facilitato alla tastiera e navigazione](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) nella Guida di riferimento visualizzatori di Dynamic Media.

## Supporto tecnologico per l&#39;assistenza in [!DNL Dynamic Media] visualizzatori {#assistive-technology-support-for-dm-viewers}

Tutto [!DNL Dynamic Media] i componenti visualizzatore supportano ruoli e attributi ARIA (Accessible Rich Internet Applications) per migliorare l’integrazione con tecnologie per l’accessibilità, come gli assistenti vocali.
Consulta la sezione **Supporto tecnologico per assistenza** Argomento della Guida in linea in qualsiasi argomento relativo alla personalizzazione dei visualizzatori nella Guida di riferimento per i visualizzatori di Dynamic Media. Ad esempio, vedi [Supporto tecnologico per assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) per il visualizzatore video, oppure [Supporto tecnologico per assistenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) per il visualizzatore di immagini interattive.

## Supporto dei sottotitoli codificati in Dynamic Media {#closed-caption-support}

Dynamic Media supporta la distribuzione di video e set di video adattivi con sottotitoli codificati. Le didascalie devono essere visualizzate sopra il contenuto video.

Vedi [Video in Dynamic Media - Aggiungere sottotitoli o sottotitoli codificati al video](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Accessibilità delle soluzioni Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilità in [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

