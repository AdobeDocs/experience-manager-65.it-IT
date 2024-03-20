---
title: Usa rasterizzatore PDF per generare le rappresentazioni
description: Genera miniature e rappresentazioni di alta qualità utilizzando la libreria Rasterizer di Adobe PDF.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Usa rasterizzatore PDF {#using-pdf-rasterizer}

Quando si caricano file PDF o AI di grandi dimensioni e ad uso intensivo di contenuti in [!DNL Adobe Experience Manager Assets], la libreria predefinita potrebbe non generare un output accurato. La libreria PDF Rasterizer di Adobe può generare un output più affidabile e accurato rispetto all’output di una libreria predefinita. L’Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti scenari:

L’Adobe consiglia di utilizzare la libreria PDF Rasterizer per i seguenti elementi:

* File AI o PDF pesanti e ad alta intensità di contenuti.
* File AI e PDF con miniature non generate per impostazione predefinita.
* File AI con colori Pantone Matching System (PMS).

Le miniature e le anteprime generate con PDF Rasterizer offrono una qualità migliore rispetto all’output predefinito e forniscono pertanto un’esperienza di visualizzazione coerente sui dispositivi. La libreria di Adobe PDF Rasterizer non supporta alcuna conversione di spazio colore. Viene sempre inviato a RGB indipendentemente dallo spazio colore del file sorgente.

1. Installare il pacchetto PDF Rasterizer sul [!DNL Adobe Experience Manager] distribuzione da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip).

   >[!NOTE]
   >
   >La libreria PDF Rasterizer è disponibile solo per Windows e Linux®.

1. Accedere a [!DNL Assets] console del flusso di lavoro in `https://[aem_server]:[port]/workflow`. Apri [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro.

1. Per evitare che vengano generate le miniature e le rappresentazioni web per i file PDF e i file AI utilizzando i metodi predefiniti, effettua le seguenti operazioni:

   * Apri **[!UICONTROL Elabora miniature]** e aggiungi `application/pdf` o `application/postscript` nel **[!UICONTROL Ignora tipi MIME]** campo sotto **[!UICONTROL Miniature]** , a seconda delle necessità.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * In **[!UICONTROL Immagine abilitata per il web]** , aggiungi `application/pdf` o `application/postscript` in **[!UICONTROL Ignora elenco]** in base alle tue esigenze.

   ![Configurazione per ignorare l’elaborazione delle miniature per un formato immagine](assets/web_enabled_imageskiplist.png)

1. Apri **[!UICONTROL Rasterizza rappresentazione anteprima immagine PDF/AI]** e rimuovi il tipo MIME per il quale vuoi saltare la generazione predefinita di rappresentazioni dell’immagine di anteprima. Ad esempio, rimuovi il tipo MIME `application/pdf`, `application/postscript`, o `application/illustrator` dal **[!UICONTROL Tipi MIME]** elenco.

   ![process_arguments](assets/process_arguments.png)

1. Trascina **[!UICONTROL Gestore rasterizzatore PDF]** dal pannello laterale a sotto il **[!UICONTROL Elabora miniature]** passaggio.
1. Configura i seguenti argomenti per **[!UICONTROL Gestore rasterizzatore PDF]** passaggio:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungi dimensioni miniature: 319:319, 140:100, 48:48. Se necessario, aggiungi una configurazione di miniature personalizzata.

   Argomenti della riga di comando per `PDFRasterizer` Il comando può includere i seguenti elementi:

   * `-d`: flag per consentire un rendering fluido di testo, grafica vettoriale e immagini. Crea immagini di qualità superiore. Tuttavia, l&#39;inclusione di questo parametro determina un rallentamento dell&#39;esecuzione del comando e un aumento delle dimensioni delle immagini.

   * `-s`: dimensione immagine massima (altezza o larghezza). Viene convertito in DPI per ogni pagina. Se le pagine sono di dimensioni diverse, ogni pagina può potenzialmente ridimensionarsi in base a quantità diverse. L&#39;impostazione predefinita è la dimensione effettiva della pagina.

   * `-t`: tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: percorso di input PDF. È un parametro obbligatorio.

   * `-h`: Guida

1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione generata]**.
1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specificare le impostazioni in **[!UICONTROL Immagine abilitata per il web]** scheda.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salva il flusso di lavoro.
1. Per consentire a PDF Rasterizer di elaborare le pagine PDF con le librerie PDF, aprire **[!UICONTROL Elabora risorsa secondaria DAM]** modello da [!UICONTROL Flusso di lavoro] console.
1. Dal pannello laterale, trascina il passaggio Gestore rasterizzatore PDF sotto il **[!UICONTROL Crea rappresentazione immagini abilitate per il web]** passaggio.
1. Configura i seguenti argomenti per **[!UICONTROL Gestore rasterizzatore PDF]** passaggio:

   * Tipi MIME: `application/pdf` o `application/postscript`
   * Comandi: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Aggiungi dimensioni miniature: `319:319`, `140:100`, `48:48`. Aggiungi la configurazione di miniature personalizzata come richiesto.

   Argomenti della riga di comando per `PDFRasterizer` Il comando può includere i seguenti elementi:

   * `-d`: flag per consentire un rendering fluido di testo, grafica vettoriale e immagini. Crea immagini di qualità superiore. Tuttavia, l&#39;inclusione di questo parametro determina un rallentamento dell&#39;esecuzione del comando e un aumento delle dimensioni delle immagini.

   * `-s`: dimensione immagine massima (altezza o larghezza). Viene convertito in DPI per ogni pagina. Se le pagine sono di dimensioni diverse, ogni pagina può potenzialmente ridimensionarsi in base a quantità diverse. L&#39;impostazione predefinita è la dimensione effettiva della pagina.

   * `-t`: tipo di immagine di output. I tipi validi sono JPEG, PNG, GIF e BMP. Il valore predefinito è JPEG.

   * `-i`: percorso di input PDF. È un parametro obbligatorio.

   * `-h`: Guida

1. Per eliminare le rappresentazioni intermedie, selezionare **[!UICONTROL Elimina rappresentazione generata]**.
1. Per consentire a PDF Rasterizer di generare rappresentazioni Web, selezionare **[!UICONTROL Genera rappresentazione web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specificare le impostazioni in **[!UICONTROL Immagine abilitata per il web]** scheda.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salva il flusso di lavoro.
1. Carica un file PDF o AI in [!DNL Experience Manager Assets]. PDF Rasterizer genera le miniature e le rappresentazioni web del file.
