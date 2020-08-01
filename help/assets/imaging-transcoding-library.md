---
title: Imaging Transcoding Library
description: Scoprite come configurare e utilizzare  libreria  transcodifica immagini, una soluzione per l’elaborazione delle immagini in grado di eseguire le funzioni di base per la gestione delle immagini, tra cui codifica, transcodifica, ricampionamento delle immagini e ridimensionamento delle immagini.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---


# Imaging Transcoding Library {#imaging-transcoding-library}

 Adobe  Libreria per la transcodifica delle immagini è una soluzione proprietaria per l&#39;elaborazione delle immagini che può eseguire le funzioni di base per la gestione delle immagini, tra cui:

* Codifica
* Transcodifica (conversione di formati supportati)
* Ricampionamento delle immagini, utilizzando gli algoritmi PS e Intel IPP
* Profondità di bit e conservazione del profilo colore
* Compressione della qualità JPEG
* Ridimensionamento delle immagini

La libreria di transcodifica delle immagini fornisce supporto CMYK e supporto alfa completo, ad eccezione di CMYK -Alpha.

Oltre a supportare un&#39;ampia gamma di formati di file e profili, la libreria Imaging Transcoding offre notevoli vantaggi rispetto ad altre soluzioni di terze parti in termini di prestazioni, scalabilità e qualità. Di seguito sono riportati alcuni dei vantaggi principali dell’utilizzo della libreria di transcodifica delle immagini:

* **Scala con dimensioni file o risoluzione** crescenti: Il ridimensionamento viene ottenuto principalmente dalla capacità brevettata della libreria Imaging Transcoding Library di ridimensionare i file durante la decodifica. Questa capacità assicura che l&#39;utilizzo della memoria di runtime sia sempre ottimale e non sia una funzione quadratica di dimensioni file crescenti o megapixel di risoluzione. La libreria di transcodifica immagini può elaborare file di dimensioni maggiori e ad alta risoluzione (contenenti file megapixel superiori). Strumenti di terze parti, come ImageMagick, non sono in grado di gestire file di grandi dimensioni e arresti anomali durante l’elaborazione di tali file.
* **algoritmi** di compressione e ridimensionamento della qualità Photoshop: Coerenza con gli standard di settore in termini di qualità del campionamento in discesa (uniforme, nitido e automatico bicubico) e di qualità della compressione. Imaging Transcoding Library (Libreria transcodifica immagini) valuta ulteriormente il fattore di qualità dell&#39;immagine di input e utilizza in modo intelligente tabelle ottimali e impostazioni di qualità per l&#39;immagine di output. Questa capacità produce file di dimensioni ottimali senza compromettere la qualità visiva.
* **Alta velocità:** Il tempo di risposta è inferiore e il throughput è sempre superiore a ImageMagick. Pertanto, la libreria di transcodifica immagini dovrebbe ridurre il tempo di attesa per gli utenti e il costo di hosting.
* **Scalabilità migliore con carico simultaneo:** La libreria di transcodifica delle immagini funziona in modo ottimale in condizioni di carico simultaneo. Offre un throughput elevato con prestazioni CPU ottimali, utilizzo della memoria e tempi di risposta ridotti, riducendo così i costi di hosting.

## Supported platforms {#supported-platforms}

La libreria di transcodifica immagini è disponibile solo per le distribuzioni RHEL 7 e CentOS 7.

>[!NOTE]
>
>Mac OS e altre distribuzioni *nix (ad esempio, Debian e Ubuntu) non sono supportate.

## Utilizzo {#usage}

Gli argomenti della riga di comando per Imaging Transcoding Library possono includere quanto segue:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Potete configurare le seguenti opzioni per il `-resize` parametro:

* `X`: Funzionamento simile a [!DNL Experience Manager]. Ad esempio -resize 319.
* `WxH`: Le proporzioni non vengono mantenute, ad esempio `-resize 319x319`.
* `Wx`: Corregge la larghezza e calcola l’altezza mantenendo le proporzioni. Esempio `-resize 319x`.
* `xH`: Corregge l’altezza e calcola la larghezza mantenendo le proporzioni. Esempio `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configura libreria transcodifica immagini {#configuring-imaging-transcoding-library}

Per configurare l’elaborazione ITL, create un file di configurazione e aggiornate il flusso di lavoro per eseguirlo.

### Creare un file di configurazione per il bundle estratto {#create-conf-file}

Per configurare la libreria, create un file CONF per indicare le librerie utilizzando la procedura seguente. Sono necessarie autorizzazioni di livello amministratore o principale.

1. Scaricate il pacchetto [Imaging Transcoding Library (Libreria transcodifica immagini) da Software Distribution (Distribuzione](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) software) e installatelo utilizzando Package Manager (Gestione pacchetti). Il pacchetto è compatibile con [!DNL Experience Manager] 6.5.

1. Per conoscere un ID bundle per `com.day.cq.dam.cq-dam-switchengine`, accedete alla console Web e fate clic su **[!UICONTROL OSGi]** > **[!UICONTROL Bundle]**. In alternativa, per aprire la console dei bundle, accedete all’ `https://[aem_server:[port]/system/console/bundles/` URL. Individua `com.day.cq.dam.cq-dam-switchengine` il bundle e il relativo ID.

1. Verificate che tutte le librerie necessarie siano estratte, controllando la cartella utilizzando il comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, dove il nome della cartella è costruito utilizzando il bundle ID. Ad esempio, il comando è `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se il bundle id è `588`.

1. Creare un `SWitchEngineLibs.conf` file da collegare alla libreria.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Aggiungere `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` il percorso al file conf utilizzando `cat SWitchEngineLibs.conf` il comando.

1. Esegui `ldconfig` comando per creare i collegamenti e la cache necessari.

1. Nell&#39;account utilizzato per avviare [!DNL Experience Manager], modificare `.bash_profile` il file. Aggiungete `LD_LIBRARY_PATH` i seguenti elementi.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Per assicurarsi che il valore del percorso sia impostato su `.`, utilizzare `echo $LD_LIBRARY_PATH` command. L&#39;output dovrebbe essere solo `.`. Se il valore non è impostato su `.`, riavviare la sessione.

### Configurare il flusso di lavoro Aggiorna risorsa  DAM {#configure-dam-asset-update-workflow}

Aggiornate il flusso di lavoro [!UICONTROL DAM Update Asset] per utilizzare la libreria per elaborare le immagini.

1. Nell&#39;interfaccia [!DNL Experience Manager] utente, selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Dalla pagina Modelli **[!UICONTROL di]** flusso di lavoro, aprite il modello di flusso di lavoro Aggiorna risorsa **** DAM in modalità di modifica.

1. Aprite il passaggio del flusso di lavoro Miniature **** processo. Nella scheda **[!UICONTROL Miniature]** , aggiungere i tipi MIME per i quali si desidera saltare il processo di generazione delle miniature predefinito nell&#39;elenco **[!UICONTROL Skip Mime Types]** .
Ad esempio, se desiderate creare le miniature per un’immagine TIFF utilizzando la libreria di transcodifica delle immagini, specificate `image/tiff` nel campo **[!UICONTROL Skip Mime Types]** .

1. Nella scheda Immagine **[!UICONTROL abilitata per il]** Web, aggiungere i tipi MIME per i quali si desidera ignorare il processo di generazione della rappresentazione Web predefinito in **[!UICONTROL Elenco]** disalta. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/tiff` all&#39;elenco di salto.

1. Aprite il passaggio Miniature **[!UICONTROL EPS (con ImageMagick)]** , quindi passate alla scheda **[!UICONTROL Argomenti]** . Nell&#39;elenco Tipi **** mime, aggiungete i tipi MIME che desiderate elaborare nella libreria Transcodifica immagini. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/jpeg` all&#39;elenco **[!UICONTROL Tipi]** mime.

1. Rimuovete gli eventuali comandi predefiniti.

1. Attiva/disattiva il pannello laterale e dall’elenco di passaggi aggiungi il gestore **** SWitchEngine.

1. Aggiungere comandi al gestore  SwitchEngine in base ai requisiti personalizzati. Ottimizzate i parametri dei comandi specificati per soddisfare le vostre esigenze. Ad esempio, per mantenere il profilo colore dell’immagine JPEG, aggiungere i seguenti comandi all’elenco **[!UICONTROL Comandi]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![calce](assets/chlimage_1-199.png)

1. (Facoltativo) Generare miniature da una rappresentazione intermedia utilizzando un singolo comando. La rappresentazione intermedia funge da origine per generare rappresentazioni statiche e Web. Questo metodo è più veloce rispetto al metodo precedente. Tuttavia, questo metodo non consente di applicare parametri personalizzati alle miniature.

   ![calce](assets/chlimage_1-200.png)

1. Per generare le rappresentazioni Web, configurate i parametri nella scheda Immagine **[!UICONTROL abilitata per il]** Web.

1. Sincronizza il modello di flusso di lavoro aggiornato di [!UICONTROL DAM Update Asset] . Salvare il flusso di lavoro.

Verificare la configurazione, caricare un&#39;immagine TIFF e monitorare il file error.log. Noterete `INFO` messaggi con menzioni di `SwitchEngineHandlingProcess execute: executing command line`. Nei registri vengono indicati i rendering generati. Al termine del flusso di lavoro, potete visualizzare le nuove rappresentazioni in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Articolo sui tipi MIME supportati](assets-formats.md#supported-image-transcoding-library)

