---
title: Installare e configurare ImageMagick
description: Scopri il software ImageMagick, come installarlo, configurare il passaggio del processo della riga di comando e utilizzarlo per modificare, comporre e generare miniature dalle immagini.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Installare e configurare ImageMagick per l&#39;utilizzo con [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick è un plug-in software per creare, modificare, comporre o convertire immagini bitmap. È in grado di leggere e scrivere immagini in vari formati (oltre 200) tra cui PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF e SVG. Utilizzare ImageMagick per ridimensionare, capovolgere, specchiare, ruotare, distorcere, tranciare e trasformare le immagini. È inoltre possibile regolare i colori delle immagini, applicare vari effetti speciali o disegnare testo, linee, poligoni, ellissi e curve utilizzando ImageMagick.

Utilizza il [!DNL Adobe Experience Manager] gestore multimediale dalla riga di comando per elaborare le immagini tramite ImageMagick. Per utilizzare vari formati di file con ImageMagick, vedere [Best practice per i formati dei file di Assets](/help/assets/assets-file-format-best-practices.md). Per informazioni su tutti i formati di file supportati, consulta [Formati di risorse supportati](/help/assets/assets-formats.md).

Per elaborare file di grandi dimensioni utilizzando ImageMagick, considera requisiti di memoria superiori al solito, potenziali modifiche necessarie ai criteri IM e l’impatto complessivo sulle prestazioni. I requisiti di memoria dipendono da vari fattori come la risoluzione, la profondità di bit, il profilo colore e il formato del file. Se intendi elaborare file molto grandi utilizzando ImageMagick, effettua correttamente il benchmark del [!DNL Experience Manager] server. Alla fine vengono fornite alcune risorse utili.

>[!NOTE]
>
>Se sta usando [!DNL Experience Manager] il [!DNL Adobe Managed Services] (AMS), contatta l’Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB ad alta risoluzione. [!DNL Experience Manager] potrebbe non elaborare file PSB ad alta risoluzione con una risoluzione superiore a 30000 x 23000 pixel.

## Installare ImageMagick {#installing-imagemagick}

Sono disponibili più versioni dei file di installazione di ImageMagic per vari sistemi operativi. Utilizzare la versione appropriata per il sistema operativo in uso.

1. Scarica il file appropriato [File di installazione di ImageMagick](https://www.imagemagick.org/script/download.php) per il sistema operativo.
1. Per installare ImageMagick sul disco che ospita [!DNL Experience Manager] server, avviare il file di installazione.

1. Impostare la variabile di ambiente del percorso sulla directory di installazione di ImageMagic.
1. Per verificare se l&#39;installazione è stata completata correttamente, eseguire la `identify -version` comando.

## Impostare il passaggio del processo della riga di comando {#set-up-the-command-line-process-step}

È possibile impostare il passaggio della riga di comando per il caso d’uso specifico. Eseguire la procedura seguente per generare un&#39;immagine capovolta e miniature (140x100, 48x48, 319x319 e 1280x1280) ogni volta che si aggiunge un file di immagine JPEG a `/content/dam` il [!DNL Experience Manager] server:

1. Il giorno [!DNL Experience Manager] , passare alla console Flusso di lavoro (`https://[aem_server]:[port]/workflow`) e aprire la **[!UICONTROL Aggiorna risorsa DAM]** modello di workflow.
1. Dalla sezione **[!UICONTROL Aggiorna risorsa DAM]** modello di flusso di lavoro, aprire **[!UICONTROL Miniature di EPS (con tecnologia ImageMagick)]** passaggio.
1. In **[!UICONTROL Scheda Argomenti]**, aggiungi `image/jpeg` al **[!UICONTROL Tipi MIME]** elenco.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. In **[!UICONTROL Comandi]** immetti il comando seguente:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Seleziona la **[!UICONTROL Elimina rappresentazione generata]** e **[!UICONTROL Genera rappresentazione web]** contrassegni.

   ![select_flags](assets/select_flags.png)

1. In **[!UICONTROL Immagine abilitata per il web]** , specifica i dettagli della rappresentazione con dimensioni di 1280x1280 pixel. Inoltre, specifica `image/jpeg` nel **[!UICONTROL Mimetype]** casella.

   ![immagine_abilitata_per_web](assets/web_enabled_image.png)

1. Clic **[!UICONTROL OK]** per salvare le modifiche.

   >[!NOTE]
   >
   >Il `convert` potrebbe non essere eseguito con alcune versioni di Windows (ad esempio, Windows SE), perché è in conflitto con il `convert` che fa parte dell&#39;installazione di Windows. In questo caso, indicare il percorso completo dell&#39;utility ImageMagick. Ad esempio, specifica:
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Apri **[!UICONTROL Elabora miniature]** e aggiungi il tipo MIME `image/jpeg` in **[!UICONTROL Ignora tipi MIME]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. In **[!UICONTROL Immagine abilitata per il web]** , aggiungi il tipo MIME `image/jpeg` sotto **[!UICONTROL Ignora elenco]**. Clic **[!UICONTROL OK]** per salvare le modifiche.

   ![web_enabled](assets/web_enabled.png)

1. Salva il flusso di lavoro.

1. Per verificare la corretta elaborazione, carica un’immagine JPG in [!DNL Assets]. Al termine dell’elaborazione, verifica se vengono generate o meno un’immagine capovolta e le rappresentazioni.

## Mitigazione delle vulnerabilità di sicurezza {#mitigating-security-vulnerabilities}

Esistono diverse vulnerabilità di sicurezza associate all’utilizzo di ImageMagick per elaborare le immagini. Ad esempio, l’elaborazione delle immagini inviate dall’utente comporta il rischio di esecuzione di codice remoto (RCE).

Inoltre, vari plug-in di elaborazione delle immagini dipendono dalla libreria ImageMagick, tra cui, ma non solo, imagemagick di PHP, ruby&#39;s magick e paperclip e imagemagick di nodejs.

Se utilizzi ImageMagick o una libreria interessata, Adobe consiglia di attenuare le vulnerabilità note eseguendo almeno una delle seguenti attività (ma preferibilmente entrambe):

1. Verificare che tutti i file di immagine inizino con il [&quot;byte magici&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) corrispondenti ai tipi di file immagine supportati prima di inviarli a ImageMagick per l&#39;elaborazione.
1. Utilizza un file di criteri per disabilitare i codificatori ImageMagick vulnerabili. Il criterio globale per ImageMagick si trova all&#39;indirizzo `/etc/ImageMagick`.
