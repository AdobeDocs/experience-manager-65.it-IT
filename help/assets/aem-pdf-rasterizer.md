---
title: Usare il rasterizzatore PDF per generare le rappresentazioni
description: Generazione di miniature e rappresentazioni di alta qualità tramite la libreria  Adobe PDF Rasterizer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b68311d593730d1c441b863967b15e6481758267
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---


# Usa Rasterizzatore PDF {#using-pdf-rasterizer}

Quando caricate in [!DNL Adobe Experience Manager Assets] file PDF o AI di grandi dimensioni che richiedono molto contenuto, la libreria predefinita potrebbe non generare un output accurato.  Adobe  libreria Rasterizer PDF può generare un output più affidabile e preciso rispetto all&#39;output di una libreria predefinita.  Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti scenari:

 Adobe consiglia di utilizzare la libreria PDF Rasterizer per le seguenti operazioni:

* File AI o PDF pesanti e ricchi di contenuti.
* File AI e file PDF con miniature non generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Le miniature e le anteprime generate con PDF Rasterizer sono di qualità migliore rispetto all’output out-of-the-box e, pertanto, offrono un’esperienza di visualizzazione coerente su tutti i dispositivi. La libreria  Adobe PDF Rasterizer non supporta la conversione dello spazio colore. Trasmette sempre in RGB indipendentemente dallo spazio colore del file sorgente.

1. Installate il pacchetto PDF Rasterizer nella distribuzione [!DNL Adobe Experience Manager] da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >La libreria PDF Rasterizer è disponibile solo per Windows e Linux.

1. Accedete alla console [!DNL Assets] del flusso di lavoro in `https://[aem_server]:[port]/workflow`. Aprire il flusso di lavoro [!UICONTROL DAM Update Asset].

1. Per impedire la generazione di miniature e rappresentazioni Web per i file PDF e i file AI utilizzando i metodi predefiniti, procedere come segue:

   * Aprite il passaggio **[!UICONTROL Miniature processo]** e aggiungete `application/pdf` o `application/postscript` nel campo **[!UICONTROL Skip Mime Types]** nella scheda **[!UICONTROL Miniature]**, a seconda delle necessità.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Nella scheda **[!UICONTROL Immagine abilitata per il Web]**, aggiungere `application/pdf` o `application/postscript` in **[!UICONTROL Skip List]** a seconda delle esigenze.

   ![Configurazione per saltare l&#39;elaborazione delle miniature per un formato immagine](assets/web_enabled_imageskiplist.png)

1. Aprite il passaggio **[!UICONTROL Rasterizza rendering anteprima immagine PDF/AI]** e rimuovete il tipo MIME per il quale desiderate saltare la generazione predefinita di rappresentazioni immagine di anteprima. Ad esempio, rimuovere il tipo MIME `application/pdf`, `application/postscript` o `application/illustrator` dall&#39;elenco **[!UICONTROL Tipi MIME]**.

   ![process_topics](assets/process_arguments.png)

1. Trascinare il passaggio **[!UICONTROL PDF Rasterizer Handler]** dal pannello laterale al punto **[!UICONTROL Miniature di processo]**.
1. Configurare gli argomenti seguenti per il passaggio **[!UICONTROL PDF Rasterizer Handler]**:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungere le dimensioni delle miniature: 319:319, 140:100, 48:48. Se necessario, aggiungete una configurazione personalizzata per le miniature.

   Gli argomenti della riga di comando per il comando `PDFRasterizer` possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazioni generate]**.
1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specificate le impostazioni nella scheda **[!UICONTROL Immagine abilitata per il Web]**.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salvare il flusso di lavoro.
1. Per abilitare PDF Rasterizer per l&#39;elaborazione di pagine PDF con librerie PDF, aprire il modello **[!UICONTROL DAM Process Subasset]** dalla console [!UICONTROL Workflow].
1. Dal pannello laterale, trascinare il passaggio del gestore di raster PDF sotto il passaggio **[!UICONTROL Crea rappresentazione immagine abilitata per il Web]**.
1. Configurare gli argomenti seguenti per il passaggio **[!UICONTROL PDF Rasterizer Handler]**:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungete le dimensioni delle miniature: `319:319`, `140:100`, `48:48`. Aggiungi la configurazione personalizzata delle miniature, a seconda delle necessità.

   Gli argomenti della riga di comando per il comando `PDFRasterizer` possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazioni generate]**.
1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specificate le impostazioni nella scheda **[!UICONTROL Immagine abilitata per il Web]**.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salvare il flusso di lavoro.
1. Caricate un file PDF o un file AI in [!DNL Experience Manager Assets]. PDF Rasterizer genera le miniature e le rappresentazioni Web per il file.
