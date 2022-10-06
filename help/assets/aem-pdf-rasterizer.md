---
title: Utilizza PDF rasterizer per generare rappresentazioni
description: Genera miniature e rappresentazioni di alta qualità utilizzando la libreria Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Usa PDF Rasterizer {#using-pdf-rasterizer}

Quando si caricano file PDF o AI di grandi dimensioni e ad alta intensità di contenuto in [!DNL Adobe Experience Manager Assets], la libreria predefinita potrebbe non generare un output accurato. La libreria PDF Rasterizer di Adobe può generare un output più affidabile e preciso rispetto all&#39;output di una libreria predefinita. Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti scenari:

Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti elementi:

* File AI o file PDF pesanti e ad alta intensità di contenuto.
* File AI e file PDF con miniature non generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Le miniature e le anteprime generate con PDF Rasterizer offrono una qualità migliore rispetto all’output preconfigurato e forniscono quindi un’esperienza di visualizzazione coerente su tutti i dispositivi. La libreria Adobe PDF Rasterizer non supporta la conversione dello spazio colore. Emette sempre in RGB indipendentemente dallo spazio colore del file di origine.

1. Installa il pacchetto PDF Rasterizer sul tuo [!DNL Adobe Experience Manager] distribuzione da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >La libreria PDF Rasterizer è disponibile solo per Windows e Linux.

1. Accedere al [!DNL Assets] console del flusso di lavoro in `https://[aem_server]:[port]/workflow`. Apri [!UICONTROL Risorsa di aggiornamento DAM] workflow.

1. Per impedire la generazione di miniature e rappresentazioni web per i file PDF e AI utilizzando i metodi predefiniti, procedi come segue:

   * Apri **[!UICONTROL Miniature del processo]** e aggiungi `application/pdf` o `application/postscript` in **[!UICONTROL Ignora tipi mime]** campo **[!UICONTROL Miniature]** se necessario.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * In **[!UICONTROL Immagine abilitata per il web]** scheda aggiungi `application/pdf` o `application/postscript` sotto **[!UICONTROL Ignora elenco]** a seconda delle tue esigenze.

   ![Configurazione per saltare l&#39;elaborazione delle miniature per un formato immagine](assets/web_enabled_imageskiplist.png)

1. Apri **[!UICONTROL Rasterizza rappresentazione anteprima immagine PDF/AI]** e rimuovi il tipo MIME per il quale vuoi saltare la generazione predefinita di rappresentazioni di immagini di anteprima. Ad esempio, rimuovi il tipo MIME `application/pdf`, `application/postscript`oppure `application/illustrator` dal **[!UICONTROL Tipi MIME]** elenco.

   ![process_objects](assets/process_arguments.png)

1. Trascina **[!UICONTROL Gestore Rasterizer PDF]** dal pannello laterale al di sotto del **[!UICONTROL Miniature del processo]** passo.
1. Configura i seguenti argomenti per **[!UICONTROL Gestore Rasterizer PDF]** passo:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungi le dimensioni delle miniature: 319:319, 140:100, 48:48. Aggiungi la configurazione personalizzata delle miniature, se necessario.

   Argomenti della riga di comando per `PDFRasterizer` può includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Crea immagini di qualità migliore. Tuttavia, l&#39;inclusione di questo parametro causa l&#39;esecuzione lenta del comando e l&#39;aumento delle dimensioni delle immagini.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questa viene convertita in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso di input PDF. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare i rendering intermedi, seleziona **[!UICONTROL Elimina rappresentazione generata]**.
1. Per consentire ad PDF Rasterizer di generare rappresentazioni web, seleziona **[!UICONTROL Genera rappresentazione web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specifica le impostazioni nella **[!UICONTROL Immagine abilitata per il web]** scheda .

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salva il flusso di lavoro.
1. Per abilitare PDF Rasterizer all’elaborazione delle pagine PDF con le librerie di PDF, apri le **[!UICONTROL Subasset del processo DAM]** dal modello [!UICONTROL Flusso di lavoro] console.
1. Dal pannello laterale, trascina il passaggio PDF Rasterizer Handler sotto la **[!UICONTROL Crea rappresentazione immagine abilitata per il web]** passo.
1. Configura i seguenti argomenti per **[!UICONTROL Gestore Rasterizer PDF]** passo:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungi dimensioni miniature: `319:319`, `140:100`, `48:48`. Aggiungi la configurazione personalizzata delle miniature in base alle esigenze.

   Argomenti della riga di comando per `PDFRasterizer` può includere quanto segue:

   * `-d`: Contrassegno per consentire il rendering uniforme di testo, immagini vettoriali e immagini. Crea immagini di qualità migliore. Tuttavia, l&#39;inclusione di questo parametro causa l&#39;esecuzione lenta del comando e l&#39;aumento delle dimensioni delle immagini.

   * `-s`: Dimensione massima dell’immagine (altezza o larghezza). Questa viene convertita in DPI per ogni pagina. Se le pagine hanno dimensioni diverse, ogni pagina può essere ridimensionata in base a quantità diverse. Il valore predefinito è la dimensione effettiva della pagina.

   * `-t`: Tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: Percorso di input PDF. È un parametro obbligatorio.

   * `-h`: Aiuto


1. Per eliminare i rendering intermedi, seleziona **[!UICONTROL Elimina rappresentazione generata]**.
1. Per consentire ad PDF Rasterizer di generare rappresentazioni web, seleziona **[!UICONTROL Genera rappresentazione web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specifica le impostazioni nella **[!UICONTROL Immagine abilitata per il web]** scheda .

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salva il flusso di lavoro.
1. Caricare un file PDF o un file AI in [!DNL Experience Manager Assets]. PDF Rasterizer genera le miniature e le rappresentazioni web del file.
