---
title: Libreria trascodifica immagini
description: Scopri come configurare e utilizzare Adobe Imaging Transcoding Library, una soluzione di elaborazione delle immagini in grado di eseguire funzioni di gestione delle immagini di base, tra cui codifica, transcodifica, ricampionamento e ridimensionamento delle immagini.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
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

* **Ridimensiona con l&#39;aumento delle dimensioni o della risoluzione del file**: il ridimensionamento si ottiene principalmente grazie alla brevettata capacità della Libreria di trascodifica delle immagini di ridimensionare i file durante la decodifica. Questa capacità assicura che l’utilizzo della memoria di runtime sia sempre ottimale e non sia una funzione quadratica di aumento delle dimensioni del file o della risoluzione dei megapixel. La libreria di trascodifica di immagini può elaborare file di grandi dimensioni e ad alta risoluzione (contenenti megapixel più elevati). Strumenti di terze parti, come ImageMagick, non è in grado di gestire file di grandi dimensioni e arresti anomali durante l’elaborazione di tali file.
* **Algoritmi di compressione e ridimensionamento della qualità Photoshop**: in termini di qualità del downsampling (uniformità, nitidezza e automaticità bicubica) e della compressione, la conformità agli standard di settore. Imaging Transcoding Library valuta ulteriormente il fattore di qualità dell&#39;immagine di input e utilizza in modo intelligente tabelle e impostazioni di qualità ottimali per l&#39;immagine di output. Questa capacità produce file di dimensioni ottimali senza compromettere la qualità visiva.
* **Alta velocità:** Il tempo di risposta è inferiore e il throughput è notevolmente superiore rispetto a ImageMagick. Pertanto, la libreria di transcodifica delle immagini dovrebbe ridurre il tempo di attesa per gli utenti e i costi di hosting.
* **Scalabilità migliore con carico simultaneo:** La libreria di trascodifica delle immagini funziona in modo ottimale in condizioni di carico simultanee. Fornisce un throughput elevato con prestazioni ottimali della CPU, utilizzo della memoria e tempi di risposta ridotti, che contribuiscono a ridurre i costi di hosting.

## Piattaforme supportate {#supported-platforms}

La libreria di trascodifica delle immagini è disponibile solo per le distribuzioni RHEL 7 e CentOS 7.

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

Puoi configurare le seguenti opzioni per `-resize` parametro:

* `X`: funziona in modo simile a [!DNL Experience Manager]. Ad esempio -resize 319.
* `WxH`: le proporzioni non vengono mantenute, ad esempio `-resize 319x319`.
* `Wx`: corregge la larghezza e calcola l’altezza mantenendo le proporzioni. Esempio `-resize 319x`.
* `xH`: corregge l’altezza e calcola la larghezza mantenendo le proporzioni. Esempio `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configura libreria di trascodifica immagini {#configuring-imaging-transcoding-library}

Per configurare l’elaborazione ITL, crea un file di configurazione e aggiorna il flusso di lavoro per eseguirlo.

### Crea un file di configurazione per il bundle estratto {#create-conf-file}

Per configurare la libreria, crea un file CONF per indicare le librerie seguendo la procedura riportata di seguito. Sono necessarie autorizzazioni di amministratore o radice.

1. Scarica il file [Pacchetto libreria di trascodifica immagini da Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e installarlo utilizzando Gestione pacchetti. Il pacchetto è compatibile con [!DNL Experience Manager] 6.5

1. Per conoscere un ID bundle per `com.day.cq.dam.cq-dam-switchengine`, accedi alla console web e fai clic su **[!UICONTROL OSGi]** > **[!UICONTROL Bundle]**. In alternativa, per aprire la console dei bundle, accedi a `https://[aem_server:[port]/system/console/bundles/` URL. Individua `com.day.cq.dam.cq-dam-switchengine` e il relativo ID.

1. Assicurati di estrarre tutte le librerie richieste, controllando la cartella con il comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, in cui il nome della cartella viene creato utilizzando l’ID del bundle. Ad esempio, il comando è `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se l’id bundle è `588`.

1. Crea `SWitchEngineLibs.conf` file da collegare alla libreria.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Aggiungi `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` percorso del file conf tramite `cat SWitchEngineLibs.conf` comando.

1. Esegui `ldconfig` per creare i collegamenti e la cache necessari.

1. Nell’account utilizzato per avviare [!DNL Experience Manager], modifica `.bash_profile` file. Aggiungi `LD_LIBRARY_PATH` aggiungendo i seguenti elementi.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Per assicurarsi che il valore del percorso sia impostato su `.`, utilizza `echo $LD_LIBRARY_PATH` comando. L’output deve essere `.`. Se il valore non è impostato `.`, riavviare la sessione.

### Configura [!UICONTROL Aggiorna risorsa DAM] workflow {#configure-dam-asset-update-workflow}

Aggiornare il [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro per utilizzare la libreria per l’elaborazione delle immagini.

1. In entrata [!DNL Experience Manager] interfaccia utente, selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Dalla sezione **[!UICONTROL Modelli flusso di lavoro]** , apri la pagina **[!UICONTROL Aggiorna risorsa DAM]** modello di flusso di lavoro in modalità di modifica.

1. Apri **[!UICONTROL Elabora miniature]** passaggio del processo di workflow. In **[!UICONTROL Miniature]** , aggiungere i tipi MIME per i quali si desidera saltare il processo di generazione delle miniature predefinito nella scheda **[!UICONTROL Ignora tipi MIME]** elenco.
Se ad esempio si desidera creare miniature per un&#39;immagine TIFF utilizzando la libreria di trascodifica immagini, specificare `image/tiff` nel **[!UICONTROL Ignora tipi MIME]** campo.

1. In **[!UICONTROL Immagine abilitata per il web]** , aggiungi i tipi MIME per i quali vuoi saltare il processo predefinito di generazione della rappresentazione web in **[!UICONTROL Ignora elenco]**. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/tiff` all&#39;elenco di salto.

1. Apri **[!UICONTROL Miniature di EPS (con tecnologia ImageMagick)]** passaggio, passa alla **[!UICONTROL Argomenti]** scheda. In **[!UICONTROL Tipi MIME]** , aggiungi i tipi MIME che desideri elaborare con Imaging Transcoding Library. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/jpeg` al **[!UICONTROL Tipi MIME]** elenco.

1. Rimuovere i comandi predefiniti eventualmente esistenti.

1. Attiva/disattiva pannello laterale e dall’elenco dei passaggi aggiungi **[!UICONTROL Gestore SWitchEngine]**.

1. Aggiungere comandi al [!UICONTROL Gestore SwitchEngine] in base ai requisiti personalizzati. Regolare i parametri dei comandi specificati in base alle proprie esigenze. Se ad esempio si desidera mantenere il profilo colore dell&#39;immagine JPEG, aggiungere i seguenti comandi al **[!UICONTROL Comandi]** elenco:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (Facoltativo) Genera miniature da una rappresentazione intermedia utilizzando un singolo comando. La rappresentazione intermedia funge da origine per generare rappresentazioni statiche e web. Questo metodo è più veloce del metodo precedente. Tuttavia, con questo metodo non è possibile applicare parametri personalizzati alle miniature.

   ![chlimage](assets/chlimage_1-200.png)

1. Per generare le rappresentazioni web, configura i parametri in **[!UICONTROL Immagine abilitata per il web]** scheda.

1. Sincronizza il file aggiornato [!UICONTROL Aggiorna risorsa DAM] modello di workflow. Salva il flusso di lavoro.

Verifica la configurazione, carica un’immagine TIFF e monitora il file error.log. Noterai `INFO` messaggi con menzioni di `SwitchEngineHandlingProcess execute: executing command line`. I registri menzionano le rappresentazioni generate. Al termine del flusso di lavoro, puoi visualizzare le nuove rappresentazioni in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Articolo sui tipi MIME supportati](assets-formats.md#supported-image-transcoding-library)

