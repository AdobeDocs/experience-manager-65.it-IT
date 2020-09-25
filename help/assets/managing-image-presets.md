---
title: Gestione dei predefiniti per immagini per contenuti multimediali dinamici
description: Comprendere i predefiniti per immagini per contenuti multimediali dinamici e imparare a creare, modificare e gestire i predefiniti per immagini
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 10%

---


# Managing Dynamic Media image presets{#managing-image-presets}

I predefiniti per immagini consentono a  AEM Assets di distribuire dinamicamente immagini di diverse dimensioni, in diversi formati o con altre proprietà immagine generate in modo dinamico. Ciascun predefinito per immagini rappresenta una raccolta di comandi di ridimensionamento e formattazione per la visualizzazione delle immagini. Quando create un predefinito per immagini, scegliete una dimensione per la distribuzione delle immagini. Potete anche scegliere i comandi di formattazione in modo che l’aspetto dell’immagine venga ottimizzato quando l’immagine viene trasmessa per la visualizzazione.

Gli amministratori possono creare predefiniti per l’esportazione delle risorse. Quando esportate le immagini, gli utenti possono scegliere un predefinito, che consente di riformattare le immagini in base alle specifiche specificate dall’amministratore.

Potete anche creare dei predefiniti per immagini reattivi. Se applicate un predefinito immagine reattivo alle risorse, questo varia a seconda del dispositivo o della dimensione dello schermo su cui sono visualizzate. Potete configurare i predefiniti per immagini per l’utilizzo di CMYK nello spazio colore oltre che di RGB o Grigio.

Questa sezione descrive come creare, modificare e gestire in genere i predefiniti per immagini. Potete applicare un predefinito per immagini a un’immagine ogni volta che la visualizzate in anteprima. See [Applying Image Presets](/help/assets/image-presets.md).

>[!NOTE]
>
>La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Per ulteriori informazioni, consulta [Smart Imaging](/help/assets/imaging-faq.md) .

## Understanding Dynamic Media image presets {#understanding-image-presets}

Analogamente a una macro, un predefinito per immagini è un insieme predefinito di comandi di ridimensionamento e formattazione salvati con un nome. Per comprendere il funzionamento dei predefiniti per immagini, supponete che nel vostro sito Web ciascuna immagine di prodotto venga visualizzata in dimensioni diverse, in formati diversi e con tassi di compressione per la distribuzione desktop e mobile.

Potete creare due predefiniti per immagini: uno con 500 x 500 pixel per la versione desktop e 150 x 150 pixel per la versione mobile. Potete creare due predefiniti per immagini, uno `Enlarge` per visualizzare le immagini a 500x500 pixel e uno per visualizzare le immagini `Thumbnail` a 150x150 pixel. Per trasmettere le immagini a `Enlarge` e `Thumbnail` dimensione, AEM cerca la definizione del predefinito Ingrandimento immagine e Miniatura immagine. Quindi AEM genera in modo dinamico un’immagine secondo le specifiche di ridimensionamento e formattazione di ciascun predefinito per immagini.

Le immagini la cui dimensione viene ridotta quando vengono trasmesse in modo dinamico possono perdere nitidezza e dettaglio. Per questo motivo, ogni predefinito per immagini contiene controlli di formattazione per ottimizzare un’immagine quando questa viene trasmessa in una determinata dimensione. Questi controlli assicurano che le immagini siano nitide e chiare quando vengono trasmesse al sito Web o all’applicazione.

Gli amministratori possono creare dei predefiniti per immagini. Per creare un predefinito per immagini, potete partire da zero o iniziare da uno esistente e salvarlo con un nuovo nome.

## Managing Dynamic Media image presets {#managing-image-presets-1}

Per gestire i predefiniti per immagini in AEM, toccate o fate clic sul logo AEM per accedere alla console di navigazione globale, quindi toccate o fate clic sull’icona Strumenti e andate a **[!UICONTROL Risorse > Predefiniti immagine.]**

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Eventuali predefiniti per immagini creati sono disponibili anche come rappresentazioni dinamiche per l’anteprima o la distribuzione delle risorse.
>
>In *Contenuti multimediali dinamici - Modalità* Scene7, *non* è necessario pubblicare i predefiniti per immagini in quanto i predefiniti per immagini vengono pubblicati automaticamente.
>
>In *Dynamic Media - Modalità* ibrida, è necessario pubblicare manualmente i predefiniti per immagini.
>
>See [Publishing Image Presets.](#publishing-image-presets)

>[!NOTE]
>
>Il sistema mostra diverse rappresentazioni quando selezionate **[!UICONTROL Rappresentazioni]** nella visualizzazione Dettagli di una risorsa. Potete aumentare o diminuire il numero di predefiniti per immagini da visualizzare. See [Increasing the number of image presets that display](#increasing-or-decreasing-the-number-of-image-presets-that-display).

###  formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Se intendete supportare l’assimilazione di file AI, EPS e PDF in modo da poter generare rappresentazioni dinamiche di questi formati di file, prima di creare i predefiniti per immagini potrebbe essere utile consultare le seguenti informazioni.

 formato di file Adobe Illustrator è una variante di PDF. Le principali differenze, nel contesto di  AEM Assets, sono le seguenti:

*  documenti Adobe Illustrator sono composti da una singola pagina con più livelli. Ciascun livello viene estratto come risorsa secondaria PNG sotto la risorsa Illustrator  principale.
* I documenti PDF sono composti da una o più pagine. Ogni pagina viene estratta come una risorsa PDF a pagina singola sotto il documento PDF principale con più pagine.

Le risorse secondarie vengono create dal `Create Sub Asset process` componente all’interno del `DAM Update Asset` flusso di lavoro complessivo. Per visualizzare questo componente di processo nel flusso di lavoro, tocca **[!UICONTROL Strumenti > Flusso di lavoro > Modelli > DAM Update Asset (Aggiorna risorsa DAM) > Edit (Modifica).]**

Consultate anche [Visualizzazione delle pagine di un file](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file)con più pagine.

Potete visualizzare le risorse secondarie o le pagine quando aprite la risorsa, toccare il menu Contenuto e selezionare Risorse **[!UICONTROL secondarie]** o **[!UICONTROL Pagine.]** Le attività secondarie sono attività reali. In altre parole, le pagine PDF vengono estratte dal componente `Create Sub Asset` Workflow. Vengono quindi memorizzati come `page1.pdf`, `page2.pdf`e così via sotto la risorsa principale. Una volta memorizzati, il `DAM Update Asset` flusso di lavoro li elabora.

Per utilizzare gli elementi multimediali dinamici per visualizzare in anteprima e generare rappresentazioni dinamiche per i file AI, EPS o PDF, sono necessari i seguenti passaggi di elaborazione:

1. Nel `DAM Update Asset` flusso di lavoro, il componente `Rasterize PDF/AI Image Preview Rendition` Processo rasterizza la prima pagina della risorsa originale, utilizzando la risoluzione configurata, in una `cqdam.preview.png` rappresentazione.

1. La `cqdam.preview.png` rappresentazione viene quindi ottimizzata in un PTIFF dal componente `Dynamic Media Process Image Assets` di processo all’interno del flusso di lavoro.

>[!NOTE]
>
>In the [!UICONTROL DAM Update Asset] workflow, the **[!UICONTROL EPS thumbnails]** step generates thumbnails for EPS files.

#### Proprietà dei metadati delle risorse PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Proprietà metadata** | **Descrizione** |
|---|---|
| dam:Physicalwidthinpollici | Larghezza documento in pollici. |
| dam:Physicalheightinpollici | Altezza documento in pollici. |

Potete accedere alle opzioni dei componenti `Rasterize PDF/AI Image Preview Rendition` di processo tramite il `DAM Update Asset` flusso di lavoro.

Toccate Adobe Experience Manager in alto a sinistra, selezionate **[!UICONTROL Strumenti > Flusso di lavoro > Modelli.]** Nella pagina Modelli di workflow, seleziona **[!UICONTROL DAM Update Asset]**(Aggiorna risorsa DAM), quindi tocca **[!UICONTROL Edit (Modifica) sulla barra degli strumenti.]** Nella pagina del flusso di lavoro Aggiorna risorsa  DAM, toccate due volte il componente `Rasterize PDF/AI Image Preview Rendition` di processo per aprire la relativa finestra di dialogo Proprietà passaggio.

#### Rasterize PDF/AI Image Preview Rendition options {#rasterize-pdf-ai-image-preview-rendition-options}

![Argomenti per rasterizzare il flusso di lavoro PDF o AI](assets/rasterize_pdf_ai_image_preview.png)

Argomenti per rasterizzare il flusso di lavoro PDF o AI

<table>
 <tbody>
  <tr>
   <td><strong>Argomento processo</strong></td>
   <td><strong>Impostazione predefinita</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Tipi mime</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>Elenco di tipi di mime di documenti considerati come documenti PDF o  Illustrator.<br /> </td>
  </tr>
  <tr>
   <td>Larghezza max.</td>
   <td>2048</td>
   <td>Larghezza massima della rappresentazione di anteprima generata, in pixel.<br /> </td>
  </tr>
  <tr>
   <td>Altezza max.</td>
   <td>2048</td>
   <td>Altezza massima della rappresentazione di anteprima generata, in pixel.<br /> </td>
  </tr>
  <tr>
   <td>Risoluzione</td>
   <td>72</td>
   <td>Risoluzione per rasterizzare la prima pagina, in ppi (pixel per pollice).</td>
  </tr>
 </tbody>
</table>

Utilizzando gli argomenti di processo predefiniti, la prima pagina di un documento PDF/AI viene rasterizzata a 72 ppi e l&#39;immagine di anteprima generata viene ridimensionata a 2048 x 2048 pixel. Per una distribuzione tipica, potete aumentare la risoluzione fino a un minimo di 150 ppi o più. Ad esempio, un documento con dimensioni Lettera USA a 300 ppi richiede rispettivamente una larghezza e un&#39;altezza massime di 2550 x 3300 pixel.

Larghezza max e Altezza max limitano la risoluzione alla quale rasterizzare. Ad esempio, se i valori massimi sono invariati e Risoluzione è impostata su 300 ppi, un documento Lettera USA viene rasterizzato a 186 ppi. ovvero 1581 x 2046 pixel.

Il componente `Rasterize PDF/AI Image Preview Rendition` di processo ha un valore massimo definito per garantire che non vengano create immagini troppo grandi nella memoria. Tali immagini di grandi dimensioni possono sovraccaricare la memoria fornita alla JVM (Java Virtual Machine). È necessario prestare attenzione a fornire alla JVM memoria sufficiente per gestire il numero configurato di flussi di lavoro paralleli, ciascuno dei quali ha il potenziale per creare un&#39;immagine alle dimensioni massime configurate.

### Formato di file InDesign  (INDD) {#indesign-indd-file-format}

Se intendete supportare l’assimilazione di file INDD in modo da poter generare una rappresentazione dinamica di questo formato di file, prima di creare i predefiniti per immagini potrebbe essere utile consultare le seguenti informazioni.

Per  file InDesign, le risorse secondarie vengono estratte solo se il server Adobe InDesign  è integrato con AEM. Le risorse di riferimento sono collegate in base ai relativi metadati.  InDesign Server non è richiesto per il collegamento. Tuttavia, le risorse di riferimento devono essere presenti in AEM prima che i file di InDesign  vengano elaborati per creare i collegamenti tra i file InDesign  e le risorse di riferimento.

See [Integrating AEM Assets with InDesign Server](/help/assets/indesign.md).

Il componente Processo estrazione file multimediali nel `DAM Update Asset` flusso di lavoro esegue diversi script di estensione preconfigurati per elaborare  file InDesign.

![I percorsi ExtendScript  negli argomenti del processo di estrazione dei file multimediali](assets/6_5_mediaextractionprocess.png)

I percorsi ExtendScript  negli argomenti del componente Processo estrazione file multimediali nel flusso di lavoro [!UICONTROL DAM Update Asset] .

I seguenti script sono utilizzati dall&#39;integrazione di Dynamic Media:

<table>
 <tbody>
  <tr>
   <td><strong>Estendi nome script</strong></td>
   <td><strong>Predefiniti</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>Sì</td>
   <td>Genera una <code>thumbnail.jpg</code> rappresentazione a 300 ppi ottimizzata e trasformata in una rappresentazione PTIFF per componente di <code>Dynamic Media Process Image Assets</code> processo.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sì</td>
   <td>Genera una risorsa secondaria JPEG a 300 ppi per ogni pagina. La risorsa secondaria JPEG è una risorsa reale memorizzata nella risorsa InDesign . Inoltre, viene ottimizzata e trasformata in PTIFF in base al <code>DAM Update Asset</code> flusso di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>No</td>
   <td>Genera una risorsa secondaria PDF per ogni pagina. La risorsa secondaria PDF viene elaborata come descritto in precedenza. Poiché il PDF contiene una sola pagina, non vengono generate risorse secondarie.<br /> </td>
  </tr>
 </tbody>
</table>

## Configurazione delle dimensioni delle miniature delle immagini {#configuring-image-thumbnail-size}

Puoi configurare la dimensione delle miniature configurando tali impostazioni nel flusso di lavoro **[!UICONTROL DAM Update Asset]** . Nel flusso di lavoro, potete configurare la dimensione delle miniature delle risorse immagine in due passaggi. Sebbene per le risorse immagine dinamiche sia utilizzato uno (**[!UICONTROL Dynamic Media Process Image Assets]**) e l’altro (**[!UICONTROL Process Thumbnails]**) per la generazione di miniature statiche o quando tutti gli altri processi non generano le miniature, *entrambi* devono avere le stesse impostazioni.

Con il passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**, le miniature vengono generate da Image Server e questa configurazione è indipendente da quella applicata al passaggio **[!UICONTROL Elabora miniature]**. La generazione delle miniature tramite il passaggio **[!UICONTROL Elabora miniature]** rappresenta il modo più lento e laborioso di creare le miniature, in termini di utilizzo della memoria.

Il ridimensionamento delle miniature è definito nel seguente formato: **[!UICONTROL width:height:center]**, ad esempio *80:80:false*. Larghezza e altezza determinano le dimensioni in pixel della miniatura; il valore center è false o true e se è impostato su true, indica che l&#39;immagine in miniatura ha esattamente le dimensioni specificate nella configurazione. Se l’immagine ridimensionata è più piccola, viene centrata all’interno della miniatura.

>[!NOTE]
>
>* Le dimensioni delle miniature per i file EPS sono configurate nel passaggio **[!UICONTROL Miniature EPS]**, cui si accede selezionando la scheda **[!UICONTROL Argomenti]** della sezione Miniature.
   >
   >
* Le dimensioni delle miniature per i video sono configurate nel passaggio **[!UICONTROL Miniature FFmpeg]**, nella scheda **[!UICONTROL Processo]** di **[!UICONTROL Argomenti.]**

>



**Per configurare le dimensioni** delle miniature di immagine:

1. Toccate **[!UICONTROL Strumenti > Flusso di lavoro > Modelli > DAM Update Asset > Edit (Aggiorna risorsa DAM).]**
1. Toccate il passaggio **[!UICONTROL Risorse]** immagine di elaborazione file multimediali dinamici e toccate o fate clic sulla scheda **[!UICONTROL Miniature]** . Modifica le dimensioni delle miniature in base alle esigenze, quindi tocca **[!UICONTROL OK.]**

   ![6_5_dynamicmediaprocessimageassets-mininailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Tocca il passaggio **[!UICONTROL Elabora miniature]**, quindi tocca la scheda **[!UICONTROL Miniature]**. Modifica le dimensioni delle miniature in base alle esigenze, quindi tocca **[!UICONTROL OK.]**

   >[!NOTE]
   >
   >I valori nell’argomento miniature del passaggio **[!UICONTROL Elabora miniature]** devono corrispondere all’argomento miniature nel passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**.

1. Toccate **[!UICONTROL Salva]** per salvare le modifiche al flusso di lavoro.

### Aumento o riduzione del numero di predefiniti per immagini per file multimediali dinamici visualizzati {#increasing-or-decreasing-the-number-of-image-presets-that-display}

I predefiniti per immagini creati sono disponibili come rappresentazioni dinamiche per l’anteprima delle risorse. AEM mostra diverse rappresentazioni dinamiche quando visualizzate una risorsa da Visualizzazione **[!UICONTROL dettagli > Rappresentazioni.]** Potete aumentare o diminuire il limite di rappresentazioni visualizzate.

**Per aumentare o diminuire il numero di predefiniti per immagini per file multimediali dinamici visualizzati**:

1. Andate al CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Andate al nodo di elenco dei predefiniti per immagini in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Passa all’origine dati del predefinito per immagini in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Nella proprietà limit, modificare il numero in base al numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toccate **[!UICONTROL Salva tutto.]**

## Creazione di un predefinito per immagini per contenuti multimediali dinamici {#creating-image-presets}

La creazione di un predefinito per immagini per contenuti multimediali dinamici consente di applicare tali impostazioni a tutte le immagini al momento della visualizzazione in anteprima o della pubblicazione.

>[!NOTE]
>
>Se si utilizza Internet Explorer 9, la creazione di un predefinito non viene visualizzata nell&#39;elenco dei predefiniti subito dopo il salvataggio. Per risolvere questo problema, disattivate la cache per IE9.

Se intendete supportare l’assimilazione di file AI, PDF ed EPS in modo da poter generare una rappresentazione dinamica di questi formati di file, prima di creare i predefiniti per immagini potrebbe essere utile consultare le seguenti informazioni.
Consultate [formati](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)di file Adobe Illustrator (AI), Postscript (EPS) e PDF.

Se intendete supportare l’assimilazione di file INDD in modo da poter generare una rappresentazione dinamica di questo formato di file, prima di creare i predefiniti per immagini potrebbe essere utile consultare le seguenti informazioni.
Consultate [formato](#indesign-indd-file-format)di file InDesign (INDD).

>[!NOTE]
>
>Per creare i predefiniti per immagini per contenuti multimediali dinamici, è necessario disporre dei privilegi di amministratore in qualità di amministratore AEM o amministratore  Admin Console.

**Per creare un predefinito** per immagini per file multimediali dinamici:

1. In AEM, tap the AEM logo to access the global navigation console, then tap **[!UICONTROL Tools > Assets > Image Presets.]**
1. Fai clic su **[!UICONTROL Crea.]** Viene visualizzata la finestra **[!UICONTROL Modifica predefinito]** immagine.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Per rendere dinamico questo predefinito immagine, cancella i valori nei campi **[!UICONTROL larghezza]** e **[!UICONTROL altezza]**, lasciandoli vuoti.

1. Immetti i valori desiderati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, compreso un nome. Le opzioni sono descritte in [Opzioni predefinito immagine](#image-preset-options). I predefiniti vengono visualizzati nel riquadro a sinistra e possono essere usati all’istante con altre risorse.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Creating a responsive image preset {#creating-a-responsive-image-preset}

Per creare un predefinito per immagini reattivo, effettuate le operazioni descritte nella sezione [Creazione di predefiniti](#creating-image-presets)per immagini. Quando immettete l’altezza e la larghezza nella finestra **[!UICONTROL Modifica predefinito]** immagine, cancellate i valori e lasciateli vuoti.

Lasciandoli vuoti, AEM che questo predefinito per immagini è reattivo. Potete regolare gli altri valori in base alle necessità.



>[!NOTE]
>
>In order to see the **[!UICONTROL URL]** and **[!UICONTROL RESS]** buttons when applying an image preset to an asset, the asset must be published.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>In modalità Dynamic Media - Scene7, i predefiniti per immagini e le risorse di immagini vengono pubblicati automaticamente.
>
>In modalità Elemento multimediale dinamico - ibrido, è necessario pubblicare manualmente i predefiniti per immagini e le risorse immagine.

### Opzioni dei predefiniti per immagini {#image-preset-options}

Quando create o modificate i predefiniti per immagini, avete a disposizione le opzioni descritte in questa sezione. Inoltre,  Adobe consiglia di iniziare con le seguenti opzioni di &quot;best practice&quot;:

* **[!UICONTROL Formato]** scheda (**[!UICONTROL Base]**) - Seleziona **[!UICONTROL JPEG]** o un altro formato che rispetta i tuoi requisiti. Tutti i browser web supportano il formato immagine JPEG, in quanto offre un buon compromesso tra dimensioni ridotte dei file e qualità delle immagini. Tuttavia, le immagini in formato JPEG usano uno schema di compressione che causa la perdita di dati, con possibile introduzione di artefatti di immagine indesiderati, qualora l’impostazione di compressione sia troppo bassa. Per questo motivo, Adobe consiglia di impostare la qualità di compressione su 75. Questa impostazione offre un buon compromesso tra la qualità delle immagini e le dimensioni ridotte dei file.

* **[!UICONTROL Attiva nitidezza semplice]**: non selezionare **[!UICONTROL Attiva nitidezza semplice]** (il filtro di nitidezza offre un controllo inferiore rispetto alle impostazioni Maschera definizione dettagli).

* **[!UICONTROL Nitidezza: Modalità]** Di Ricampionamento - Seleziona **[!UICONTROL Bicubico.]**

#### Opzioni scheda Base {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Nome</strong></td>
   <td>Inserisci un nome descrittivo senza spazi vuoti. Includi nel nome le dimensioni immagine per aiutare gli utenti a identificare questo predefinito immagine.</td>
  </tr>
  <tr>
   <td><strong>Larghezza e Altezza</strong></td>
   <td>Specificate le dimensioni in pixel per la distribuzione dell’immagine. Larghezza e altezza devono essere maggiori di 0 pixel. Se uno dei due valori è 0, non viene creato alcun predefinito. Se entrambi i valori sono vuoti, viene creato un predefinito per immagini reattivo.</td>
  </tr>
  <tr>
   <td><strong>Formato</strong></td>
   <td><p>Scegliete un formato dal menu.</p> <p>L’opzione <strong>JPEG</strong> offre le seguenti opzioni aggiuntive:</p>
    <ul>
     <li><strong>Qualità</strong> - Controlla il livello di compressione JPEG. Questa impostazione influisce sia sulla dimensione del file che sulla qualità dell’immagine. La scala di qualità JPEG va da 1 a 100. La scala è visibile quando trascinate il cursore.</li>
     <li><strong>Attiva il downsampling della crominanza</strong> JPG - Poiché l'occhio è meno sensibile alle informazioni sui colori ad alta frequenza rispetto alla luminanza ad alta frequenza, le immagini JPEG dividono le informazioni sulle immagini in componenti luminanza e colore. Quando un’immagine JPEG viene compressa, il componente luminanza viene lasciato a risoluzione piena, mentre i componenti colore vengono sottoposti a downsampling calcolando la media di gruppi di pixel. Il downsampling riduce il volume dei dati di mezzo o di un terzo, senza quasi alcun impatto sulla qualità percepita. Il downsampling non è applicabile alle immagini in scala di grigio. Questa tecnica riduce la quantità di compressione utile per le immagini ad alto contrasto (ad esempio, per le immagini con testo sovrapposto).</li>
    </ul>
    <div>
      Se scegliete <strong>GIF</strong> o <strong>GIF con alfa</strong> , sono disponibili le seguenti opzioni aggiuntive di Quantizzazione <strong>colore</strong> GIF:
    </div>
    <ul>
     <li><strong>Tipo </strong>- Selezionate <strong>Adattato</strong> (impostazione predefinita), <strong>Web</strong>o <strong>Macintosh</strong>. If you select <strong>GIF with Alpha</strong>, the Macintosh option is not available.</li>
     <li><strong>Dithering</strong> - Seleziona <strong>Diffondi</strong> o <strong>Disattivato</strong>.</li>
     <li><strong>Numero di colori </strong>- Immettere un numero compreso tra 2 e 256.</li>
     <li><strong>Elenco</strong> colori - Immettere un elenco separato da virgole. Ad esempio, per bianco, grigio e nero immettete 000000,888888,ffffff.</li>
    </ul>
    <div>
      La scelta di <strong>PDF</strong>, <strong>TIFF</strong>o <strong>TIFF con alfa</strong> offre questa opzione aggiuntiva:
    </div>
    <ul>
     <li><strong>Compressione</strong> - Selezionare un algoritmo di compressione. Le opzioni di algoritmo per i PDF sono <strong>Nessuno</strong>, <strong>Zip</strong>e <strong>Jpeg</strong>; per TIFF sono <strong>None</strong>, <strong>LZW</strong>, <strong>Jpeg</strong>e <strong>Zip</strong>; e per TIFF con Alfa sono <strong>Nessuno</strong>, <strong>LZW</strong>e <strong>Zip</strong>.</li>
    </ul> <p>La scelta di <strong>PNG</strong>, <strong>PNG con Alfa,</strong> o <strong>EPS</strong> non offre opzioni aggiuntive.</p> </td>
  </tr>
  <tr>
   <td><strong>Nitidezza</strong></td>
   <td>Select the <strong>Enable Simple Sharpening</strong> option to apply a basic sharpening filter to the image after all scaling takes place. Sharpening can help compensate for blurriness that can result when you display an image at a different size. </td>
  </tr>
 </tbody>
</table>

#### Opzioni scheda Avanzate {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Spazio colore</strong></td>
   <td>Selezionate <strong>RGB,</strong> CMYK o <strong>Scala</strong> di grigio per lo spazio colore.</td>
  </tr>
  <tr>
   <td><strong>Profilo colore</strong></td>
   <td>Selezionate il profilo dello spazio colore di output in cui deve essere convertita la risorsa se è diversa dal profilo di lavoro.</td>
  </tr>
  <tr>
   <td><strong>Intento di rendering</strong></td>
   <td>Potete ignorare l'intento di rendering predefinito. Gli intenti di rendering determinano cosa accade ai colori che non possono essere riprodotti nel profilo colore di destinazione (fuori gamma). L'Intento di rendering viene ignorato se non è compatibile con il profilo ICC.
    <ul>
     <li>Selezionate <strong>Percettivo</strong> per comprimere la gamma totale da uno spazio colore a un altro spazio colore quando uno o più colori nell’immagine originale non rientrano nella gamma dello spazio colore di destinazione.</li>
     <li>Selezionate Colorimetrica <strong></strong> relativa quando un colore nello spazio colore corrente non è compreso nella gamma nello spazio colore di destinazione e desiderate mapparlo al colore più vicino possibile all’interno della gamma dello spazio colore di destinazione senza interferire con altri colori. </li>
     <li>Selezionate <strong>Saturazione</strong> per riprodurre la saturazione del colore dell’immagine originale durante la conversione nello spazio colore di destinazione. </li>
     <li>Selezionate Colorimetrica <strong></strong> assoluta per far corrispondere esattamente i colori senza alcuna regolazione per il punto bianco o il punto nero che altererebbe la luminosità dell’immagine.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensazione punto nero</strong></td>
   <td>Selezionate questa opzione se il profilo di output supporta questa funzione. La compensazione punto nero viene ignorata se non è compatibile con il profilo ICC specificato.</td>
  </tr>
  <tr>
   <td><strong>Dithering</strong></td>
   <td>Selezionate questa opzione per evitare o ridurre eventuali artefatti di bande colori. </td>
  </tr>
  <tr>
   <td><strong>Tipo nitidezza</strong></td>
   <td><p>Selezionate <strong>Nessuno</strong>, <strong>Nitidezza</strong>o Maschera di <strong>contrasto</strong>. </p>
    <ul>
     <li>Selezionate <strong>Nessuno</strong> per disattivare la nitidezza.</li>
     <li>Selezionate <strong>Nitidezza </strong>per applicare all’immagine un filtro di nitidezza di base dopo che è stato effettuato il ridimensionamento. La nitidezza può contribuire a compensare la sfocatura che può prodursi quando un’immagine viene visualizzata in dimensioni diverse. </li>
     <li>Select<strong> Unsharp mask</strong> to fine-tune a sharpening filter effect on the final downsampled image. Potete controllare l’intensità dell’effetto, il raggio (in pixel) e una soglia di contrasto che verrà ignorata. L’effetto utilizza le stesse opzioni del filtro “Maschera definizione dettagli” di Photoshop.</li>
    </ul> <p>In Maschera <strong>di contrasto</strong>sono disponibili le seguenti opzioni:</p>
    <ul>
     <li><strong>Fattore</strong> - Controlla la quantità di contrasto applicata ai pixel lungo i bordi. Il valore predefinito del numero reale è 1,0. Per le immagini ad alta risoluzione, è possibile aumentare la risoluzione fino a 5,0. Considerate l'importo come una misura dell'intensità del filtro.</li>
     <li><strong>Raggio</strong> - Determina il numero di pixel attorno ai pixel del bordo che influiscono sulla nitidezza. Per le immagini ad alta risoluzione, immettete un numero reale da 1 a 2. Un valore basso rende più nitidi solo i pixel del bordo; un valore elevato rende più nitida una banda più ampia di pixel. Il valore corretto dipende dalle dimensioni dell’immagine.</li>
     <li><strong>Soglia</strong> - Determina l'intervallo di contrasto da ignorare quando viene applicato il filtro maschera di contrasto. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel di un bordo e quindi resi più nitidi. Per evitare di introdurre disturbo, provate con valori interi compresi tra 2 e 20. </li>
     <li><strong>Applica a</strong> - Determina se applicare la non nitidezza a ogni colore o luminosità.</li>
    </ul>
    <div>
      La nitidezza è descritta in <a href="https://docs.adobe.com/content/help/en/dynamic-media-classic/using/assets/s7_sharpening_images.pdf">Immagini</a>di nitidezza.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modalità ricampionamento</strong></td>
   <td>Selezionate un’opzione <strong>Modalità</strong> di ricampionamento. Queste opzioni aumentano la nitidezza dell’immagine durante il downsampling:
    <ul>
     <li><strong>Bi-Lineare</strong> - Il metodo di ricampionamento più veloce. Sono visibili alcuni artefatti di alias.</li>
     <li><strong>Bicubico</strong> - Aumenta l'utilizzo della CPU, ma produce immagini più nitide con meno artefatti di alias.</li>
     <li><strong>Sharp2</strong> - È in grado di produrre risultati leggermente più nitidi rispetto a Bicubico, ma con un costo CPU ancora più elevato.</li>
     <li><strong>Bi-Sharp</strong> : seleziona il ricampionamento predefinito Photoshop per ridurre le dimensioni dell'immagine, che viene chiamato <strong>più nitido</strong> bicubico in  Adobe Photoshop.</li>
     <li><strong>Ogni colore</strong> e <strong>luminosità</strong> - ogni metodo può essere basato su colore o luminosità. Per impostazione predefinita, è selezionato <strong>Ciascun colore</strong> .</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Risoluzione di stampa</strong></td>
   <td>Selezionare una risoluzione per la stampa dell'immagine; Il valore predefinito è 72 pixel.</td>
  </tr>
  <tr>
   <td><strong>Modificatore immagine</strong></td>
   <td><p>Oltre alle comuni impostazioni delle immagini disponibili nell’interfaccia utente, Dynamic Media supporta numerose modifiche avanzate alle immagini che potete specificare nel campo <strong>Modificatori</strong> immagini. Questi parametri sono definiti nel riferimento <a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html">al comando</a>Image Server Protocol.</p> <p>Importante: Le seguenti funzionalità elencate nell'API non sono supportate:</p>
    <ul>
     <li>Comandi di base per la modellazione e il rendering del testo: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandi di localizzazione: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> non è disponibile per l'uso generale.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servizi per contenuti multimediali dinamici non core: SVG, Image Rendering e Web-stampa</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definizione delle opzioni dei predefiniti per immagini con i modificatori di immagini {#defining-image-preset-options-with-image-modifiers}

Oltre alle opzioni disponibili nelle schede Base e Avanzate, potete definire modificatori di immagini per fornire ulteriori opzioni per la definizione dei predefiniti per immagini. Il rendering delle immagini si basa sull’API di rendering delle immagini Scene7 e viene definito in dettaglio nella Guida di riferimento [del protocollo](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/c_http_protocol_reference.html)HTTP.

Di seguito sono riportati alcuni esempi di base delle operazioni che è possibile eseguire con i modificatori di immagini.

>[!NOTE]
>
>Alcuni modificatori di immagini [non possono essere utilizzati in AEM](#advanced-tab-options).

* [op_invert](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_invert.html) - Inverte ogni componente di colore per ottenere un effetto immagine negativo.

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_blur.html) - Applica un filtro di sfocatura all&#39;immagine.

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandi combinati - op_blur e op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_bright](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_op_brightness.html) - Diminuisce o aumenta la luminosità.

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-bright](assets/6_5_imagepreset-edit-brightness.png)

* [opaco](https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/http_ref/r_opac.html) - Regola l&#39;opacità dell&#39;immagine. Consente di ridurre l’opacità in primo piano.

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Modifica dei predefiniti per immagini {#modifying-image-presets}

1. In AEM, tap the AEM logo to access the global navigation console, then tap **[!UICONTROL Tools > Assets > Image Presets.]**

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Selezionate un predefinito e fate clic su **[!UICONTROL Modifica.]** Viene visualizzata la finestra **[!UICONTROL Modifica predefinito]** immagine.
1. Apportate le modifiche e fate clic su **[!UICONTROL Salva]** per salvare le modifiche oppure su **[!UICONTROL Annulla]** per annullare le modifiche.

## Publishing Dynamic Media image presets {#publishing-image-presets}

Se state eseguendo la modalità Elemento multimediale dinamico - Ibrido, dovete pubblicare manualmente i predefiniti per immagini.

(Se state eseguendo Dynamic Media - Modalità Scene7, i predefiniti per immagini vengono pubblicati automaticamente; non è necessario completare questi passaggi.)

**Per pubblicare i predefiniti per immagini in modalità** Elemento multimediale dinamico - Ibrido:

1. In AEM, toccate o fate clic sul logo AEM per accedere alla console di navigazione globale e toccate o fate clic sull’icona Strumenti, quindi individuate **[!UICONTROL Risorse > Predefiniti immagine.]**
1. Selezionate il predefinito per immagini o più predefiniti per immagini dall’elenco dei predefiniti per immagini e toccate o fate clic su **[!UICONTROL Pubblica.]**
1. Dopo la pubblicazione del predefinito per immagini, lo stato cambia da Non pubblicato a Pubblicato.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Deleting Dynamic Media image presets {#deleting-image-presets}

1. In AEM, toccate o fate clic sul logo AEM per accedere alla console di navigazione globale.
1. Toccate l’icona **[!UICONTROL Strumenti]** , quindi selezionate **[!UICONTROL Risorse > Predefiniti immagine.]**
1. Selezionate un predefinito, quindi fate clic su **[!UICONTROL Elimina]**. Elemento multimediale dinamico conferma l’eliminazione. Toccate **[!UICONTROL Elimina]** per eliminare o toccate **[!UICONTROL Annulla]** per interrompere.

