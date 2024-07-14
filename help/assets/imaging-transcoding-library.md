---
title: Libreria trascodifica immagini
description: Scopri come configurare e utilizzare Adobe Imaging Transcoding Library, una soluzione di elaborazione delle immagini in grado di eseguire funzioni di gestione delle immagini di base, tra cui codifica, transcodifica, ricampionamento e ridimensionamento delle immagini.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Libreria trascodifica immagini {#imaging-transcoding-library}

Adobe Imaging Transcoding Library è una soluzione di elaborazione delle immagini proprietaria in grado di eseguire funzioni di gestione delle immagini di base, tra cui:

* Codifica
* Transcodifica (conversione dei formati supportati)
* Ricampionamento delle immagini mediante algoritmi IPP PS e Intel
* Profondità di bit e conservazione del profilo colore
* Compressione di qualità JPEG
* Ridimensionamento immagine

La libreria di trascodifica delle immagini fornisce il supporto CMYK e il supporto alfa completo, ad eccezione di CMYK -Alpha.

Oltre a supportare una vasta gamma di formati e profili di file, Imaging Transcoding Library offre vantaggi significativi rispetto ad altre soluzioni di terze parti in termini di prestazioni, scalabilità e qualità. Di seguito sono riportati alcuni dei principali vantaggi dell’utilizzo della libreria di trascodifica di immagini:

* **Scalabilità con aumento delle dimensioni o della risoluzione dei file**: il ridimensionamento viene ottenuto principalmente grazie alla possibilità brevettata di ridimensionare la libreria di trascodifica di immagini durante la decodifica dei file. Questa capacità assicura che l’utilizzo della memoria di runtime sia sempre ottimale e non sia una funzione quadratica di aumento delle dimensioni del file o della risoluzione dei megapixel. La libreria di trascodifica di immagini può elaborare file di grandi dimensioni e ad alta risoluzione (contenenti megapixel più elevati). Strumenti di terze parti, come ImageMagick, non è in grado di gestire file di grandi dimensioni e arresti anomali durante l’elaborazione di tali file.
* **Algoritmi di compressione e ridimensionamento di qualità Photoshop**: coerenza con gli standard di settore in termini di qualità del downsampling (uniforme, nitida e automatica bicubica) e della qualità della compressione. Imaging Transcoding Library valuta ulteriormente il fattore di qualità dell&#39;immagine di input e utilizza in modo intelligente tabelle e impostazioni di qualità ottimali per l&#39;immagine di output. Questa capacità produce file di dimensioni ottimali senza compromettere la qualità visiva.
* **Throughput elevato:** Il tempo di risposta è inferiore e il throughput è notevolmente superiore rispetto a ImageMagick. Pertanto, la libreria di transcodifica delle immagini dovrebbe ridurre il tempo di attesa per gli utenti e i costi di hosting.
* **Scalabilità migliore con carico simultaneo:** La libreria di trascodifica di immagini funziona in modo ottimale in condizioni di carico simultanee. Fornisce un throughput elevato con prestazioni ottimali della CPU, utilizzo della memoria e tempi di risposta ridotti, che contribuiscono a ridurre i costi di hosting.

## Piattaforme supportate {#supported-platforms}

La libreria di trascodifica delle immagini è disponibile solo per le distribuzioni RHEL 7 e CentOS 7.

>[!NOTE]
>
>Mac OS e altre distribuzioni *nix (ad esempio, Debian e Ubuntu) non sono supportate.

## Utilizzo {#usage}

Gli argomenti della riga di comando per Imaging Transcoding Library possono includere quanto segue:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

È possibile configurare le opzioni seguenti per il parametro `-resize`:

* `X`: funziona in modo simile a [!DNL Experience Manager]. Ad esempio, -resize 319.
* `WxH`: le proporzioni non vengono mantenute, ad esempio `-resize 319x319`.
* `Wx`: corregge la larghezza e calcola l&#39;altezza mantenendo le proporzioni. Esempio: `-resize 319x`.
* `xH`: corregge l&#39;altezza e calcola la larghezza mantenendo le proporzioni. Esempio: `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configura libreria di trascodifica immagini {#configuring-imaging-transcoding-library}

Per configurare l’elaborazione ITL, crea un file di configurazione e aggiorna il flusso di lavoro per eseguirlo.

### Crea un file di configurazione per il bundle estratto {#create-conf-file}

Per configurare la libreria, crea un file CONF per indicare le librerie seguendo la procedura riportata di seguito. Sono necessarie autorizzazioni di amministratore o radice.

1. Scarica il pacchetto [Libreria trascodifica immagini da Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e installalo tramite Gestione pacchetti. Il pacchetto è compatibile con [!DNL Experience Manager] 6.5.

1. Per conoscere un ID bundle per `com.day.cq.dam.cq-dam-switchengine`, accedi alla console Web e fai clic su **[!UICONTROL OSGi]** > **[!UICONTROL Bundle]**. In alternativa, per aprire la console dei bundle, accedere all&#39;URL `https://[aem_server:[port]/system/console/bundles/`. Individua il bundle `com.day.cq.dam.cq-dam-switchengine` e il relativo ID.

1. Assicurarsi che tutte le librerie richieste siano estratte, controllando la cartella con il comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, dove il nome della cartella viene costruito utilizzando l&#39;ID bundle. Ad esempio, il comando è `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se l&#39;ID bundle è `588`.

1. Crea il file `SWitchEngineLibs.conf` da collegare alla libreria.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Aggiungi il percorso `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` al file conf utilizzando il comando `cat SWitchEngineLibs.conf`.

1. Eseguire il comando `ldconfig` per creare i collegamenti e la cache necessari.

1. Nell&#39;account utilizzato per avviare [!DNL Experience Manager], modificare il file `.bash_profile`. Aggiungere `LD_LIBRARY_PATH` aggiungendo gli elementi seguenti.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Per assicurarsi che il valore del percorso sia impostato su `.`, utilizzare il comando `echo $LD_LIBRARY_PATH`. L&#39;output deve essere solo `.`. Se il valore non è impostato su `.`, riavviare la sessione.

### Configura il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] {#configure-dam-asset-update-workflow}

Aggiorna il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] per utilizzare la libreria per l&#39;elaborazione delle immagini.

1. Nell&#39;interfaccia utente di [!DNL Experience Manager], selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Dalla pagina **[!UICONTROL Modelli flusso di lavoro]**, apri il modello di flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** in modalità di modifica.

1. Apri il passaggio del processo del flusso di lavoro **[!UICONTROL Elabora miniature]**. Nella scheda **[!UICONTROL Miniature]**, aggiungi i tipi MIME per i quali vuoi saltare il processo di generazione miniature predefinito nell&#39;elenco **[!UICONTROL Ignora tipi MIME]**.
Se ad esempio si desidera creare miniature per un&#39;immagine TIFF utilizzando la libreria di trascodifica immagini, specificare `image/tiff` nel campo **[!UICONTROL Ignora tipi MIME]**.

1. Nella scheda **[!UICONTROL Immagine abilitata per il Web]**, aggiungi i tipi MIME per i quali vuoi saltare il processo predefinito di generazione della rappresentazione Web in **[!UICONTROL Elenco di salto]**. Ad esempio, se nel passaggio precedente hai saltato il tipo MIME `image/tiff`, aggiungi `image/tiff` all&#39;elenco di salto.

1. Apri il passaggio **[!UICONTROL Miniature EPS (basate su ImageMagick)]**, passa alla scheda **[!UICONTROL Argomenti]**. Nell&#39;elenco **[!UICONTROL Tipi MIME]** aggiungere i tipi MIME che si desidera elaborare con la Libreria trascodifica immagini. Ad esempio, se nel passaggio precedente hai ignorato il tipo MIME `image/tiff`, aggiungi `image/jpeg` all&#39;elenco **[!UICONTROL Tipi MIME]**.

1. Rimuovere i comandi predefiniti eventualmente esistenti.

1. Attiva/disattiva pannello laterale e dall&#39;elenco di passaggi aggiungi **[!UICONTROL Gestore SWitchEngine]**.

1. Aggiungi comandi al gestore [!UICONTROL SwitchEngine] in base ai requisiti personalizzati. Regolare i parametri dei comandi specificati in base alle proprie esigenze. Se ad esempio si desidera mantenere il profilo colore dell&#39;immagine JPEG, aggiungere i seguenti comandi all&#39;elenco **[!UICONTROL Comandi]**:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (Facoltativo) Genera miniature da una rappresentazione intermedia utilizzando un singolo comando. La rappresentazione intermedia funge da origine per generare rappresentazioni statiche e web. Questo metodo è più veloce del metodo precedente. Tuttavia, con questo metodo non è possibile applicare parametri personalizzati alle miniature.

   ![chlimage](assets/chlimage_1-200.png)

1. Per generare le rappresentazioni Web, configurare i parametri nella scheda **[!UICONTROL Immagine abilitata per il Web]**.

1. Sincronizza il modello di flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] aggiornato. Salva il flusso di lavoro.

Per verificare la configurazione, carica un’immagine TIFF e monitora il file error.log. Noterai `INFO` messaggi con menzioni di `SwitchEngineHandlingProcess execute: executing command line`. I registri menzionano le rappresentazioni generate. Al termine del flusso di lavoro, sarà possibile visualizzare le nuove copie trasformate in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Articolo sui tipi MIME supportati](assets-formats.md#supported-image-transcoding-library)
