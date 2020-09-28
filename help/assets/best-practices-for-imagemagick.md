---
title: Installazione e configurazione di ImageMagick
description: Scopri il software ImageMagick, come installarlo, impostare il passaggio della riga di comando e utilizzarlo per modificare, comporre e generare miniature dalle immagini.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---


# Installazione e configurazione di ImageMagick per l’utilizzo [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick è un plug-in software per creare, modificare, comporre o convertire immagini bitmap. Può leggere e scrivere immagini in vari formati (oltre 200), tra cui PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF e SVG. ImageMagick consente di ridimensionare, riflettere, ruotare, distorcere, inclinare e trasformare le immagini. Con ImageMagick potete anche regolare i colori delle immagini, applicare vari effetti speciali o disegnare testo, linee, poligoni, ellissi e curve.

Utilizzare il gestore [!DNL Adobe Experience Manager] multimediale dalla riga di comando per elaborare le immagini tramite ImageMagick. Per utilizzare vari formati di file con ImageMagick, consulta Best practice [per i formati di file](/help/assets/assets-file-format-best-practices.md)Assets. Per informazioni su tutti i formati di file supportati, consulta Formati [supportati per le](/help/assets/assets-formats.md)risorse.

Per elaborare file di grandi dimensioni con ImageMagick, considerate requisiti di memoria superiori a quelli usuali, modifiche potenziali richieste ai criteri IM e l&#39;impatto complessivo sulle prestazioni. I requisiti di memoria dipendono da vari fattori come risoluzione, profondità di bit, profilo colore e formato file. Se intendete elaborare file di grandi dimensioni utilizzando ImageMagick, eseguite correttamente il benchmark del [!DNL Experience Manager] server. Alla fine vengono fornite alcune risorse utili.

>[!NOTE]
>
>Se utilizzi [!DNL Experience Manager] su [!DNL Adobe Managed Services] (AMS), contatta l&#39;Assistenza clienti  Adobe se intendi elaborare molti file PSD o PSB ad alta risoluzione. [!DNL Experience Manager] potrebbero non essere in grado di elaborare file PSB ad alta risoluzione con oltre 30000 x 23000 pixel.

## Installa ImageMagick {#installing-imagemagick}

Sono disponibili diverse versioni dei file di installazione ImageMagic per vari sistemi operativi. Utilizzate la versione appropriata per il sistema operativo in uso.

1. Scaricate i file [di installazione](https://www.imagemagick.org/script/download.php) ImageMagick appropriati per il sistema operativo in uso.
1. Per installare ImageMagick sul disco che ospita il [!DNL Experience Manager] server, avviate il file di installazione.

1. Impostate la variabile del percorso Ambiente sulla directory di installazione di ImageMagic.
1. Per verificare se l&#39;installazione è riuscita, eseguite il `identify -version` comando.

## Impostazione del passaggio della riga di comando {#set-up-the-command-line-process-step}

È possibile impostare il passaggio della riga di comando per il caso di utilizzo specifico. Effettuate le seguenti operazioni per generare un’immagine capovolta e miniature (140x100, 48x48, 319x319 e 1280x1280) ogni volta che aggiungete un file immagine JPEG `/content/dam` sul [!DNL Experience Manager] server:

1. Sul [!DNL Experience Manager] server, accedete alla console Flusso di lavoro (`https://[aem_server]:[port]/workflow`) e aprite il modello di flusso di lavoro Aggiorna risorsa **** DAM.
1. Dal modello di flusso di lavoro **[!UICONTROL DAM Update Asset]** (Aggiorna risorsa **[!UICONTROL DAM), aprite il passaggio delle miniature]** EPS (basato su ImageMagick).
1. Nella scheda **[!UICONTROL Argomenti]**, aggiungete `image/jpeg` all&#39;elenco **[!UICONTROL Tipi]** mime.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Nella casella **[!UICONTROL Comandi]** , immettere il comando seguente:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Selezionare i flag **[!UICONTROL Elimina rappresentazione]** generata e **[!UICONTROL Genera rappresentazione]** Web.

   ![select_flags](assets/select_flags.png)

1. Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, specificate i dettagli per la rappresentazione con dimensioni 1280x1280 pixel. Inoltre, specificate `image/jpeg` nella casella **[!UICONTROL Mimetype]** .

   ![web_enabled_image](assets/web_enabled_image.png)

1. Fate clic su **[!UICONTROL OK]** per salvare le modifiche.

   >[!NOTE]
   >
   >Il `convert` `convert` comando potrebbe non essere eseguito con alcune versioni di Windows (ad esempio Windows SE), in quanto è in conflitto con l&#39;utility nativa che fa parte dell&#39;installazione di Windows. In questo caso, indicare il percorso completo per l&#39;utilità ImageMagick. Ad esempio, specificate
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Aprite il passaggio Miniature **[!UICONTROL di]** processo e aggiungete il tipo MIME `image/jpeg` in **[!UICONTROL Skip Mime Types]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, aggiungere il tipo MIME `image/jpeg` sotto l&#39;elenco **** Salta. Fate clic su **[!UICONTROL OK]** per salvare le modifiche.

   ![web_enabled](assets/web_enabled.png)

1. Salvare il flusso di lavoro.

1. Per verificare la corretta elaborazione, caricate un’immagine JPG in [!DNL Assets]. Al termine dell&#39;elaborazione, verificate se un&#39;immagine capovolta e le rappresentazioni vengono generate o meno.

## Riduzione delle vulnerabilità di sicurezza {#mitigating-security-vulnerabilities}

L’utilizzo di ImageMagick per elaborare le immagini presenta diverse vulnerabilità di sicurezza. Ad esempio, l’elaborazione di immagini inviate dall’utente comporta il rischio di esecuzione di codice remoto (RCE).

Inoltre, diversi plug-in per l&#39;elaborazione delle immagini dipendono dalla libreria ImageMagick, tra cui, tra l&#39;altro, l&#39;immagine di PHP, il clip di immagine di Ruby e l&#39;immagine di nodejs.

Se si utilizza ImageMagick o una libreria interessata,  Adobe consiglia di attenuare le vulnerabilità note eseguendo almeno una delle seguenti operazioni (preferibilmente entrambe):

1. Verificate che tutti i file di immagine inizino con i [&quot;byte magici&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) previsti corrispondenti ai tipi di file di immagine supportati prima di inviarli a ImageMagick per l&#39;elaborazione.
1. Usate un file di criteri per disabilitare i codificatori ImageMagick vulnerabili. La politica globale per ImageMagick è disponibile all&#39;indirizzo `/etc/ImageMagick`.
