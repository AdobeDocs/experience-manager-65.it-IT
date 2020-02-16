---
title: Usare il rasterizzatore PDF per generare le rappresentazioni
description: Questo articolo descrive come generare miniature e rappresentazioni di alta qualità mediante la libreria Adobe PDF Rasterizer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Usa rasterizzatore PDF {#using-pdf-rasterizer}

A volte, quando carichi file PDF o AI di grandi dimensioni e che richiedono molto contenuto su Risorse Adobe Experience Manager (AEM), la libreria predefinita potrebbe non generare un output accurato. In tali casi, la libreria Rasterizer PDF di Adobe può generare un output più affidabile e preciso rispetto all&#39;output di una libreria predefinita.

Adobe consiglia di utilizzare la libreria PDF Rasterizer per le seguenti operazioni:

* File AI/PDF ricchi di contenuti
* File AI/PDF con miniature non generate
* File AI con colori Pantone Matching System (PMS)

Le miniature e le anteprime generate con PDF Rasterizer sono di qualità migliore rispetto all’output out-of-the-box e, pertanto, offrono un’esperienza di visualizzazione coerente su più dispositivi. La libreria Adobe PDF Rasterizer non supporta la conversione dello spazio colore. Trasmette sempre in RGB indipendentemente dallo spazio colore del file sorgente.

1. Installate il pacchetto PDF Rasterizer nell’istanza di AEM da [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >La libreria PDF Rasterizer è disponibile solo per Windows e Linux.

1. Accedi alla console del flusso di lavoro Risorse AEM in `https://[server]:[port]/workflow`.

   Aprite la pagina del flusso di lavoro Aggiorna risorsa DAM.

1. Per impedire la generazione di miniature e rappresentazioni Web per i file PDF e AI utilizzando i metodi predefiniti, procedere come segue:

   * Aprite il passaggio Miniature **[!UICONTROL di]** processo e aggiungete `application/pdf` o `application/postscript` nel campo **[!UICONTROL Skip Mime Types]** nella scheda **[!UICONTROL Miniature]** , a seconda delle necessità.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, aggiungete `application/pdf` o `application/postscript` in Elenco **** salti a seconda delle esigenze.
   ![Configurazione per saltare l&#39;elaborazione delle miniature per un formato immagine](assets/web_enabled_imageskiplist.png)

1. Aprite il passaggio **[!UICONTROL Rasterizza rappresentazione]** anteprima immagine PDF/AI e rimuovete il tipo MIME per il quale desiderate saltare la generazione di rappresentazioni immagine di anteprima predefinita. Ad esempio, rimuovere il tipo MIME `application/pdf`, `application/postscript`, o `application/illustrator` dall&#39;elenco Tipi **** MIME.

   ![process_topics](assets/process_arguments.png)

1. Trascinare il passaggio del gestore **[!UICONTROL Rasterizer]** PDF dal pannello laterale al passaggio Miniature **[!UICONTROL di]** processo.
1. Configurare gli argomenti seguenti per il passaggio del gestore **[!UICONTROL Rasterizer]** PDF:

   * Tipi MIME:    `application/pdf` o `application/postscript`

   * Comandi: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Aggiungi dimensioni miniatura: 319:319, 140:100, 48:48. Se necessario, aggiungete una configurazione personalizzata per le miniature.
   Gli argomenti della riga di comando per il `PDFRasterizer` comando possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-p`: Numero pagina. Il valore predefinito è tutte le pagine. &#39;*&#39; indica tutte le pagine.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione]** generata.
1. Per consentire a Rasterizza PDF di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione]** Web.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specificate le impostazioni nella scheda Immagine **[!UICONTROL abilitata per il]** Web.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salvare il flusso di lavoro.
1. Per abilitare PDF Rasterizer per l&#39;elaborazione di pagine PDF con librerie PDF, aprire il modello di risorse **[!UICONTROL secondarie del processo]** DAM dalla console Flusso di lavoro.
1. Dal pannello laterale, trascinare il passaggio del Gestore di raster PDF sotto il passaggio **[!UICONTROL Crea rappresentazione]** immagine abilitata per il Web.
1. Configurare gli argomenti seguenti per il passaggio del gestore **[!UICONTROL Rasterizer]** PDF:

   * Tipi MIME:    `application/pdf` o `application/postscript`

   * Comandi: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Aggiungi dimensioni miniatura: 319:319, 140:100, 48:48. Se necessario, aggiungete una configurazione personalizzata per le miniature.
   Gli argomenti della riga di comando per il comando PDFRasterizer possono includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Consente di creare immagini di qualità migliore. Tuttavia, se si inserisce questo parametro, il comando viene eseguito lentamente e le dimensioni delle immagini aumentano.

   * `-p`: Numero pagina. Il valore predefinito è tutte le pagine. `*` denota tutte le pagine.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questo viene convertito in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso del PDF di input. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione]** generata.
1. Per consentire a Rasterizza PDF di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione]** Web.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specificate le impostazioni nella scheda Immagine **[!UICONTROL abilitata per il]** Web.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salvare il flusso di lavoro.
1. Carica un file PDF o AI in Risorse AEM. PDF Rasterizer genera le miniature e le rappresentazioni Web per il file.
