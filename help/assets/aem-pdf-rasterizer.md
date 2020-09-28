---
title: Usare il rasterizzatore PDF per generare le rappresentazioni
description: Generate miniature e rappresentazioni di alta qualità utilizzando la libreria  Adobe PDF Rasterizer in [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---


# Usa PDF Rasterizer {#using-pdf-rasterizer}

Quando caricate file PDF o AI di grandi dimensioni e che richiedono molto contenuto, la conversione predefinita potrebbe non generare un output accurato. [!DNL Adobe Experience Manager Assets]  Adobe  libreria Rasterizer PDF può generare un output più affidabile e preciso rispetto all&#39;output di una libreria predefinita.  Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti scenari:

* File AI o PDF pesanti e ricchi di contenuti.
* File AI e file PDF con miniature non generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Le miniature e le anteprime generate con PDF Rasterizer sono di qualità migliore rispetto all’output out-of-the-box e, pertanto, offrono un’esperienza di visualizzazione coerente su tutti i dispositivi. La libreria  Adobe PDF Rasterizer non supporta la conversione dello spazio colore. Trasmette sempre in RGB indipendentemente dallo spazio colore del file sorgente.

1. Installate il pacchetto PDF Rasterizer nella [!DNL Adobe Experience Manager] distribuzione da Distribuzione [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)software.

   >[!NOTE]
   >
   >La libreria PDF Rasterizer è disponibile solo per Windows e Linux.

1. Accedete alla console del [!DNL Assets] flusso di lavoro in `https://[aem_server]:[port]/workflow`. Apri flusso di lavoro Aggiorna risorsa  DAM.

1. Per impedire la generazione di miniature e rappresentazioni Web per i file PDF e i file AI utilizzando i metodi predefiniti, procedere come segue:

   * Aprite il passaggio Miniature **[!UICONTROL di]** processo e aggiungete `application/pdf` o `application/postscript` nel campo **[!UICONTROL Skip Mime Types]** nella scheda **[!UICONTROL Miniature]** , a seconda delle necessità.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, aggiungete `application/pdf` o `application/postscript` in Elenco **** salti a seconda delle esigenze.

   ![Configurazione per saltare l&#39;elaborazione delle miniature per un formato immagine](assets/web_enabled_imageskiplist.png)

1. Aprite il passaggio **[!UICONTROL Rasterizza rappresentazione]** anteprima immagine PDF/AI e rimuovete il tipo MIME per il quale desiderate saltare la generazione di rappresentazioni immagine di anteprima predefinita. Ad esempio, rimuovere il tipo MIME `application/pdf`, `application/postscript`, o `application/illustrator` dall&#39;elenco Tipi **** MIME.

   ![process_topics](assets/process_arguments.png)

1. Trascinare il passaggio del gestore **[!UICONTROL Rasterizer]** PDF dal pannello laterale al passaggio Miniature **[!UICONTROL di]** processo.
1. Configurare gli argomenti seguenti per il passaggio del gestore **[!UICONTROL Rasterizer]** PDF:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Aggiungere le dimensioni delle miniature: 319:319, 140:100, 48:48. Se necessario, aggiungete una configurazione personalizzata per le miniature.

   Gli argomenti della riga di comando per il `PDFRasterizer` comando possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-p`: Numero pagina. Il valore predefinito è tutte le pagine. Per indicare tutte le pagine, utilizzate `*`.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione]** generata.

1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione]** Web.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specificate le impostazioni nella scheda Immagine **[!UICONTROL abilitata per il]** Web.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salvare il flusso di lavoro.

1. Per consentire a PDF Rasterizer di elaborare pagine PDF con librerie PDF, aprite il modello di risorse **[!UICONTROL secondarie del processo]** DAM dalla console [!UICONTROL Flusso] di lavoro.

1. Dal pannello laterale, trascinare il passaggio del Gestore di raster PDF sotto il passaggio **[!UICONTROL Crea rappresentazione]** immagine abilitata per il Web.

1. Configurare gli argomenti seguenti per il passaggio del gestore **[!UICONTROL Rasterizer]** PDF:

   * Tipi MIME: `application/pdf` o `application/postscript`

   * Comandi: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Aggiungete le dimensioni delle miniature: `319:319`, `140:100`, `48:48`. Aggiungi la configurazione personalizzata delle miniature, a seconda delle necessità.

   Gli argomenti della riga di comando per il `PDFRasterizer` comando possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-p`: Numero pagina. Il valore predefinito è tutte le pagine. `*` denota tutte le pagine.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione]** generata.
1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione]** Web.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specificate le impostazioni nella scheda Immagine **[!UICONTROL abilitata per il]** Web.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salvare il flusso di lavoro.
1. Caricate un PDF o un file AI in [!DNL Experience Manager Assets]. PDF Rasterizer genera le miniature e le rappresentazioni Web per il file.
