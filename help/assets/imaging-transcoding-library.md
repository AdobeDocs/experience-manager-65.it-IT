---
title: Libreria di transcodifica delle immagini
description: Scopri come configurare e utilizzare la Libreria di transcodifica delle immagini di Adobe, una soluzione di elaborazione delle immagini in grado di eseguire le funzioni di base per la gestione delle immagini, tra cui codifica, transcodifica, ricampionamento delle immagini e ridimensionamento delle immagini.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Libreria di transcodifica delle immagini {#imaging-transcoding-library}

La libreria di transcodifica delle immagini di Adobe è una soluzione di elaborazione delle immagini proprietaria in grado di eseguire funzioni di base per la gestione delle immagini, tra cui:

* Codifica
* Transcodifica (conversione dei formati supportati)
* Ricampionamento delle immagini, utilizzando gli algoritmi PS e Intel IPP
* Conservazione della profondità dei bit e del profilo del colore
* Compressione della qualità JPEG
* Ridimensionamento dell&#39;immagine

La libreria di transcodifica delle immagini fornisce supporto CMYK e supporto alfa completo, ad eccezione di CMYK -Alpha.

Oltre a supportare un’ampia gamma di formati e profili di file, la libreria di transcodifica delle immagini presenta vantaggi significativi rispetto ad altre soluzioni di terze parti in termini di prestazioni, scalabilità e qualità. Di seguito sono riportati alcuni dei vantaggi principali dell’utilizzo della libreria di transcodifica delle immagini:

* **Scala con dimensioni o risoluzione dei file crescenti**: La scalabilità è ottenuta principalmente dalla capacità brevettata della libreria di transcodifica delle immagini di ridimensionare durante la decodifica dei file. Questa capacità assicura che l&#39;utilizzo della memoria di runtime sia sempre ottimale e non è una funzione quadratica di aumentare le dimensioni dei file o la risoluzione megapixel. La libreria di transcodifica delle immagini può elaborare file più grandi e ad alta risoluzione (contenenti megapixel più alti). Gli strumenti di terze parti, come ImageMagick, non sono in grado di gestire file di grandi dimensioni e arresti anomali durante l’elaborazione di tali file.
* **Algoritmi di compressione e ridimensionamento della qualità Photoshop**: Coerenza con lo standard industriale in termini di qualità del campionamento a discesa (morbido, nitido e automatico bicubico) e di qualità della compressione. La libreria di transcodifica delle immagini valuta ulteriormente il fattore di qualità dell&#39;immagine di input e utilizza in modo intelligente tabelle ottimali e impostazioni di qualità per l&#39;immagine di output. Questa capacità produce file di dimensioni ottimali senza compromettere la qualità visiva.
* **Velocità effettiva elevata:** Il tempo di risposta è inferiore e il throughput è costantemente superiore a ImageMagick. Pertanto, la libreria di transcodifica delle immagini dovrebbe ridurre il tempo di attesa per gli utenti e il costo dell’hosting.
* **Scala migliore con carico simultaneo:** La libreria di transcodifica delle immagini funziona in modo ottimale in condizioni di caricamento simultanee. Offre un throughput elevato con prestazioni ottimali della CPU, utilizzo della memoria e tempi di risposta ridotti, il che contribuisce a ridurre i costi di hosting.

## Piattaforme supportate {#supported-platforms}

La libreria di transcodifica delle immagini è disponibile solo per le distribuzioni RHEL 7 e CentOS 7.

>[!NOTE]
>
>Il sistema operativo Mac e altre distribuzioni *nix (ad esempio Debian e Ubuntu) non sono supportate.

## Utilizzo {#usage}

Gli argomenti della riga di comando per la libreria di transcodifica delle immagini possono includere quanto segue:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Puoi configurare le seguenti opzioni per la `-resize` parametro:

* `X`: Lavori simili a [!DNL Experience Manager]. Ad esempio -resize 319.
* `WxH`: Il rapporto di formato non viene mantenuto, ad esempio `-resize 319x319`.
* `Wx`: Corregge la larghezza e calcola l&#39;altezza mantenendo le proporzioni. Esempio `-resize 319x`.
* `xH`: Corregge l&#39;altezza e calcola la larghezza mantenendo le proporzioni. Esempio `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurare la libreria di transcodifica delle immagini {#configuring-imaging-transcoding-library}

Per configurare l’elaborazione ITL, crea un file di configurazione e aggiorna il flusso di lavoro per eseguirlo.

### Crea un file di configurazione per il bundle estratto {#create-conf-file}

Per configurare la libreria, crea un file CONF per indicare le librerie utilizzando i seguenti passaggi. Sono necessarie autorizzazioni di livello amministratore o radice.

1. Scarica la [Pacchetto libreria di transcodifica delle immagini da Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e installalo utilizzando Gestione pacchetti. Il pacchetto è compatibile con [!DNL Experience Manager] 6.5.

1. Per conoscere un ID bundle di `com.day.cq.dam.cq-dam-switchengine`, accedi alla console Web e fai clic su **[!UICONTROL OSGi]** > **[!UICONTROL Bundle]**. In alternativa, per aprire la console dei bundle, accedi a `https://[aem_server:[port]/system/console/bundles/` URL. Individua `com.day.cq.dam.cq-dam-switchengine` e il relativo ID.

1. Assicurati che tutte le librerie richieste siano estratte, controllando la cartella utilizzando il comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, in cui il nome della cartella viene costruito utilizzando il bundle ID. Ad esempio, il comando è `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` se l&#39;id del bundle è `588`.

1. Crea `SWitchEngineLibs.conf` file da collegare alla libreria.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Aggiungi `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` percorso del file conf utilizzando `cat SWitchEngineLibs.conf` comando.

1. Esegui `ldconfig` per creare i collegamenti e la cache necessari.

1. Nell’account utilizzato per iniziare [!DNL Experience Manager], modifica `.bash_profile` file. Aggiungi `LD_LIBRARY_PATH` aggiungendo quanto segue:

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Per garantire che il valore del percorso sia impostato su `.`, utilizza `echo $LD_LIBRARY_PATH` comando. L&#39;uscita dovrebbe essere `.`. Se il valore non è impostato su `.`, riavvia la sessione.

### Configura [!UICONTROL Risorsa di aggiornamento DAM] workflow {#configure-dam-asset-update-workflow}

Aggiorna [!UICONTROL Risorsa di aggiornamento DAM] per utilizzare la libreria per l’elaborazione delle immagini.

1. In [!DNL Experience Manager] interfaccia utente, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Da **[!UICONTROL Modelli di flusso di lavoro]** aprire **[!UICONTROL Risorsa di aggiornamento DAM]** modello di flusso di lavoro in modalità di modifica.

1. Apri **[!UICONTROL Miniature del processo]** passaggio del processo del flusso di lavoro. In **[!UICONTROL Miniature]** aggiungi i tipi MIME per i quali desideri saltare il processo predefinito di generazione delle miniature nel **[!UICONTROL Ignora tipi mime]** elenco.
Ad esempio, se desideri creare miniature per un’immagine di TIFF utilizzando la libreria di transcodifica delle immagini, specifica `image/tiff` in **[!UICONTROL Ignora tipi mime]** campo .

1. In **[!UICONTROL Immagine abilitata per il web]** aggiungi i tipi MIME per i quali desideri saltare il processo predefinito di generazione del rendering web in **[!UICONTROL Ignora elenco]**. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/tiff` all&#39;elenco saltato.

1. Apri **[!UICONTROL Miniature EPS (con tecnologia ImageMagick)]** passaggio , passa alla **[!UICONTROL Argomenti]** scheda . In **[!UICONTROL Tipi di mime]** aggiungi i tipi MIME che desideri elaborare nella libreria di transcodifica delle immagini. Ad esempio, se hai saltato il tipo MIME `image/tiff` nel passaggio precedente, aggiungi `image/jpeg` al **[!UICONTROL Tipi di mime]** elenco.

1. Se esistono, rimuovere i comandi predefiniti.

1. Attiva/disattiva il pannello laterale e dall’elenco dei passaggi aggiunti **[!UICONTROL Gestore SWitchEngine]**.

1. Aggiungi comandi al [!UICONTROL Gestore SwitchEngine] in base ai requisiti personalizzati. Regola i parametri dei comandi specificati per soddisfare le tue esigenze. Ad esempio, se desideri mantenere il profilo colore dell’immagine JPEG, aggiungi i seguenti comandi al **[!UICONTROL Comandi]** elenco:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![calcagno](assets/chlimage_1-199.png)

1. (Facoltativo) Genera miniature da una rappresentazione intermedia utilizzando un singolo comando. Il rendering intermedio funge da origine per generare rappresentazioni statiche e web. Questo metodo è più veloce del metodo precedente. Tuttavia, non è possibile applicare parametri personalizzati alle miniature utilizzando questo metodo.

   ![calcagno](assets/chlimage_1-200.png)

1. Per generare rappresentazioni web, configura i parametri nel **[!UICONTROL Immagine abilitata per il web]** scheda .

1. Sincronizza gli aggiornamenti [!UICONTROL Risorsa di aggiornamento DAM] modello di flusso di lavoro. Salva il flusso di lavoro.

Verifica la configurazione, carica un’immagine TIFF e monitora il file error.log. Lo noterete `INFO` messaggi con menzioni di `SwitchEngineHandlingProcess execute: executing command line`. I registri menzionano le rappresentazioni generate. Al termine del flusso di lavoro, puoi visualizzare le nuove rappresentazioni in [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Articolo sui tipi MIME supportati](assets-formats.md#supported-image-transcoding-library)

