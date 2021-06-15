---
title: Gestione dei predefiniti per immagini Dynamic Media
description: Comprendere i predefiniti immagine di Dynamic Media e imparare a creare, modificare e gestire i predefiniti immagine
uuid: 3e9a7af6-bf49-4cff-b516-0a3ee9765391
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cc1111c4-6e24-4570-9ac7-97c25cf24ede
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/image-presets
feature: Predefiniti immagini
role: Business Practitioner, Administrator
exl-id: 556b99fe-91c3-441f-ba81-22cb8c10ef7f
source-git-commit: 4ad5237939289b5411a988424b2a3ecad15ca029
workflow-type: tm+mt
source-wordcount: '3853'
ht-degree: 8%

---

# Gestione dei predefiniti immagine Dynamic Media{#managing-image-presets}

I predefiniti per immagini consentono ad Adobe Experience Manager Assets di distribuire dinamicamente immagini di dimensioni diverse, in formati diversi o con altre proprietà immagine generate in modo dinamico. Ogni predefinito per immagini rappresenta un insieme predefinito di comandi di ridimensionamento e formattazione per la visualizzazione delle immagini. Quando crei un predefinito per immagini, scegli una dimensione per la distribuzione delle immagini. È inoltre possibile scegliere i comandi di formattazione in modo che l&#39;aspetto dell&#39;immagine sia ottimizzato quando l&#39;immagine viene distribuita per la visualizzazione.

Gli amministratori possono creare predefiniti per l’esportazione delle risorse. Gli utenti possono scegliere un predefinito al momento dell’esportazione delle immagini, che riformatta anche le immagini in base alle specifiche specificate dall’amministratore.

Puoi anche creare predefiniti immagine reattivi. Se applichi un predefinito immagine reattiva alle risorse, questo cambia a seconda del dispositivo o delle dimensioni dello schermo su cui vengono visualizzate. È possibile configurare i predefiniti immagine per l’utilizzo di CMYK nello spazio colore, oltre a RGB o Grigio.

Questa sezione descrive come creare, modificare e gestire in genere i predefiniti per immagini. È possibile applicare un predefinito immagine a un&#39;immagine in qualsiasi momento in cui viene visualizzata in anteprima. Consulta [Applicazione dei predefiniti per immagini](/help/assets/image-presets.md).

>[!NOTE]
>
>La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Per ulteriori informazioni, consulta [Smart imaging](/help/assets/imaging-faq.md) .

## Informazioni sui predefiniti immagine Dynamic Media {#understanding-image-presets}

Come una macro, un predefinito per immagini è un insieme predefinito di comandi di ridimensionamento e formattazione salvati con un nome. Per comprendere il funzionamento dei predefiniti per immagini, supponiamo che il sito web richieda che ogni immagine del prodotto venga visualizzata in dimensioni diverse, in formati diversi e con tassi di compressione per la distribuzione desktop e mobile.

>[!NOTE]
>
>In modalità Dynamic Media - Scene7, i predefiniti immagine sono supportati solo per le risorse immagine.

Puoi creare due predefiniti immagine: uno con 500 x 500 pixel per la versione desktop e 150 x 150 pixel per la versione mobile. È possibile creare due predefiniti per immagini, uno denominato `Enlarge` per visualizzare le immagini a 500x500 pixel e uno chiamato `Thumbnail` per visualizzare le immagini a 150 x 150 pixel. Per fornire immagini con le dimensioni `Enlarge` e `Thumbnail`, Experience Manager cerca la definizione di Ingrandisci predefinito immagine e Predefinito immagine miniatura. Quindi, Experience Manager genera in modo dinamico un&#39;immagine con le specifiche di dimensione e formattazione di ciascun predefinito per immagini.

Le immagini a dimensioni ridotte quando vengono consegnate in modo dinamico possono perdere nitidezza e dettagli. Per questo motivo, ogni predefinito per immagini contiene controlli di formattazione per l’ottimizzazione di un’immagine quando viene distribuita con una particolare dimensione. Questi controlli assicurano che le immagini siano nitide e chiare quando vengono inviate al sito Web o all&#39;applicazione.

Gli amministratori possono creare i predefiniti per immagini. Per creare un predefinito per immagini, puoi iniziare da zero o da uno esistente e salvarlo con un nuovo nome.

## Gestione dei predefiniti immagine Dynamic Media {#managing-image-presets-1}

Per gestire i predefiniti immagine in Experience Manager, tocca o fai clic sul logo Experience Manager per accedere alla console di navigazione globale, quindi tocca o fai clic sull’icona Strumenti , infine passa a **[!UICONTROL Risorse > Predefiniti immagine]**.

![6_5_tools-assets-imagepresets](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Eventuali predefiniti immagine creati sono disponibili anche come rappresentazioni dinamiche quando visualizzi l’anteprima o la distribuzione delle risorse.
>
>In *Dynamic Media - Modalità Scene7*, *non* è necessario pubblicare i predefiniti per immagini quando i predefiniti per immagini vengono pubblicati automaticamente.
>
>In *Dynamic Media - Modalità ibrida*, è necessario pubblicare manualmente i predefiniti per immagini.
>
>Consulta [Pubblicazione di predefiniti immagine](#publishing-image-presets).

>[!NOTE]
>
>Il sistema mostra diverse rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** nella Vista dettagli di una risorsa. Puoi aumentare o diminuire il numero di predefiniti immagine da visualizzare. Consulta [Aumento del numero di predefiniti immagine da visualizzare](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF avanzati {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

>[!NOTE]
>
>Questo argomento è applicabile solo alla modalità ibrida di Dynamic Media.

Se desideri supportare l’acquisizione di file AI, EPS e PDF in modo da poter generare rappresentazioni dinamiche di questi formati di file, controlla le seguenti informazioni prima di creare i predefiniti per immagini.

Il formato di file Adobe Illustrator è una variante di PDF. Le principali differenze, nel contesto dell’attività di Experience Manager, sono le seguenti:

* I documenti Adobe Illustrator sono costituiti da una singola pagina con più livelli. Ogni livello viene estratto come risorsa secondaria PNG sotto la risorsa principale Illustrator.
* I documenti PDF sono costituiti da una o più pagine. Ogni pagina viene estratta come una risorsa PDF a pagina singola sotto il documento PDF principale con più pagine.

Le risorse secondarie vengono create dal componente `Create Sub Asset process` all’interno del flusso di lavoro complessivo `DAM Update Asset`. Per visualizzare questo componente del processo all&#39;interno del flusso di lavoro, tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Aggiorna risorsa DAM]** > **[!UICONTROL Modifica]**.

Vedere anche [Visualizzazione di pagine di un file multipagina](/help/assets/managing-linked-subassets.md#view-pages-of-a-multi-page-file).

Puoi visualizzare le risorse secondarie o le pagine quando apri la risorsa, toccare il menu Contenuto e selezionare **[!UICONTROL Risorse secondarie]** o **[!UICONTROL Pagine]**. Le risorse secondarie sono risorse reali. In altre parole, le pagine PDF sono estratte dal componente del flusso di lavoro `Create Sub Asset` . Vengono quindi memorizzati come `page1.pdf`, `page2.pdf` e così via, sotto la risorsa principale. Una volta memorizzati, il flusso di lavoro `DAM Update Asset` li elabora.

Per utilizzare Dynamic Media per visualizzare in anteprima e generare rappresentazioni dinamiche per file AI, EPS o PDF, sono necessari i seguenti passaggi di elaborazione:

1. Nel flusso di lavoro `DAM Update Asset`, il componente di processo `Rasterize PDF/AI Image Preview Rendition` rasterizza la prima pagina della risorsa originale, utilizzando la risoluzione configurata, in un rendering `cqdam.preview.png`.

1. Il rendering `cqdam.preview.png` viene quindi ottimizzato in un PTIFF dal componente di processo `Dynamic Media Process Image Assets` all’interno del flusso di lavoro.

>[!NOTE]
>
>Nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] , il passaggio **[!UICONTROL Miniature EPS]** genera le miniature per i file EPS.

#### Proprietà dei metadati delle risorse PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Proprietà metadati** | **Descrizione** |
|---|---|
| dam:Physicalwidthinpollici | Larghezza documento in pollici. |
| dam:Physicalheightinpollici | Altezza del documento in pollici. |

Puoi accedere alle opzioni dei componenti del processo `Rasterize PDF/AI Image Preview Rendition` tramite il flusso di lavoro `DAM Update Asset` .

Tocca Adobe Experience Manager in alto a sinistra, vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**. Nella pagina Modelli flusso di lavoro , seleziona **[!UICONTROL Risorsa di aggiornamento DAM]**, quindi sulla barra degli strumenti tocca **[!UICONTROL Modifica]**. Nella pagina del flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] , tocca due volte il componente di processo `Rasterize PDF/AI Image Preview Rendition` per aprire la relativa finestra di dialogo Proprietà passaggio .

#### Rasterizzare le opzioni di rendering anteprima immagine PDF/AI {#rasterize-pdf-ai-image-preview-rendition-options}

![Argomenti per rasterizzare il flusso di lavoro PDF o AI](assets/rasterize_pdf_ai_image_preview.png)

Argomenti per rasterizzare il flusso di lavoro PDF o AI

<table>
 <tbody>
  <tr>
   <td><strong>Argomento del processo</strong></td>
   <td><strong>Impostazione predefinita</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Tipi mime</td>
   <td><p>application/pdf</p> <p>application/postscript</p> <p>application/illustrator<br /> </p> </td>
   <td>Elenco dei tipi di mime dei documenti considerati documenti PDF o Illustrator.<br /> </td>
  </tr>
  <tr>
   <td>Larghezza max.</td>
   <td>2048</td>
   <td>Larghezza massima del rendering di anteprima generato, in pixel.<br /> </td>
  </tr>
  <tr>
   <td>Altezza max.</td>
   <td>2048</td>
   <td>Altezza massima in pixel del rendering di anteprima generato.<br /> </td>
  </tr>
  <tr>
   <td>Risoluzione</td>
   <td>72</td>
   <td>Risoluzione per rasterizzare la prima pagina, in ppi (pixel per pollice).</td>
  </tr>
 </tbody>
</table>

Utilizzando gli argomenti di processo predefiniti, la prima pagina di un documento PDF/AI viene rasterizzata a 72 ppi e l’immagine di anteprima generata è dimensionata a 2048 x 2048 pixel. Per una distribuzione tipica, è possibile aumentare la risoluzione fino a un minimo di 150 ppi o più. Ad esempio, un documento con dimensioni lettera USA a 300 ppi richiede rispettivamente una larghezza e un&#39;altezza massime di 2550 x 3300 pixel.

Larghezza massima e Altezza massima limitano la risoluzione a cui rasterizzare. Ad esempio, se i valori massimi sono invariati e la risoluzione è impostata su 300 ppi, un documento Lettera USA viene rasterizzato a 186 ppi. Cioè, il documento è di 1581 x 2046 pixel.

Il componente di processo `Rasterize PDF/AI Image Preview Rendition` ha un valore massimo definito per garantire che non crei immagini troppo grandi nella memoria. Immagini di grandi dimensioni possono sovraccaricare la memoria fornita alla JVM (Java™ Virtual Machine). È necessario prestare attenzione a fornire alla JVM memoria sufficiente per gestire il numero configurato di flussi di lavoro paralleli, ognuno dei quali ha il potenziale per creare un&#39;immagine alle dimensioni massime configurate.

### Formato di file InDesign (INDD) {#indesign-indd-file-format}

Se si desidera supportare l’acquisizione di file INDD in modo da poter generare il rendering dinamico di questo formato di file, prima di creare i predefiniti per immagini è possibile esaminare le seguenti informazioni.

Per i file InDesign, le risorse secondarie vengono estratte solo se Adobe InDesign Server è integrato con Experience Manager. Le risorse di riferimento sono collegate in base ai relativi metadati. InDesign Server non è necessario per il collegamento. Tuttavia, le risorse a cui si fa riferimento devono essere presenti in Experience Manager prima che i file InDesign vengano elaborati affinché i collegamenti possano essere creati tra i file InDesign e le risorse a cui si fa riferimento.

Consulta [Integrazione di risorse di Experience Manager con InDesign Server](/help/assets/indesign.md).

Il componente Processo di estrazione file multimediali nel flusso di lavoro `DAM Update Asset` esegue diversi script di estensione preconfigurati per elaborare i file InDesign.

![I percorsi ExtendScript negli argomenti del processo di estrazione di file multimediali](assets/6_5_mediaextractionprocess.png)

I percorsi ExtendScript negli argomenti del componente del processo di estrazione di file multimediali nel flusso di lavoro [!UICONTROL Aggiorna risorsa DAM] .

I seguenti script vengono utilizzati dall’integrazione Dynamic Media:

<table>
 <tbody>
  <tr>
   <td><strong>Nome ExtendScript</strong></td>
   <td><strong>Predefiniti</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>ThumbnailExport.jsx</td>
   <td>Sì</td>
   <td>Genera un rendering a 300 ppi <code>thumbnail.jpg</code> ottimizzato e trasformato in un rendering PTIFF dal componente di processo <code>Dynamic Media Process Image Assets</code>.<br /> </td>
  </tr>
  <tr>
   <td>JPEGPagesExport.jsx</td>
   <td>Sì</td>
   <td>Genera una risorsa secondaria JPEG da 300 ppi per ogni pagina. La risorsa secondaria JPEG è una risorsa reale memorizzata nella risorsa InDesign. Viene inoltre ottimizzato e trasformato in PTIFF dal flusso di lavoro <code>DAM Update Asset</code>.<br /> </td>
  </tr>
  <tr>
   <td>PDFPagesExport.jsx</td>
   <td>No</td>
   <td>Genera una risorsa secondaria PDF per ogni pagina. La risorsa secondaria PDF viene elaborata come descritto in precedenza. Poiché il PDF contiene una sola pagina, non vengono generate risorse secondarie.<br /> </td>
  </tr>
 </tbody>
</table>

## Configurazione della dimensione della miniatura dell’immagine {#configuring-image-thumbnail-size}

Puoi configurare le dimensioni delle miniature configurando tali impostazioni nel flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** . Nel flusso di lavoro sono disponibili due passaggi per configurare la dimensione delle miniature delle risorse immagine. Anche se una (**[!UICONTROL Risorse di immagine di processo Dynamic Media]**) viene utilizzata per le risorse di immagini dinamiche e l&#39;altra (**[!UICONTROL Miniature di processo]**) per la generazione di miniature statiche, o quando tutti gli altri processi non riescono a generare miniature, *entrambe* devono avere le stesse impostazioni.

Con il passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**, le miniature vengono generate da Image Server e questa configurazione è indipendente da quella applicata al passaggio **[!UICONTROL Elabora miniature]**. La generazione delle miniature tramite il passaggio **[!UICONTROL Elabora miniature]** rappresenta il modo più lento e laborioso di creare le miniature, in termini di utilizzo della memoria.

Il dimensionamento delle miniature è definito nel seguente formato: **[!UICONTROL width:height:center]**, ad esempio *80:80:false*. La larghezza e l’altezza determinano le dimensioni in pixel della miniatura. Il valore centrale è false o true e se è impostato su true, indica che l&#39;immagine in miniatura ha esattamente le dimensioni specificate nella configurazione. Se l&#39;immagine ridimensionata è più piccola, viene centrata all&#39;interno della miniatura.

>[!NOTE]
>
>* Le dimensioni delle miniature per i file EPS sono configurate nel passaggio **[!UICONTROL Miniature EPS]**, nella scheda **[!UICONTROL Argomenti]** sotto Miniature.
   >
   >
* Le dimensioni delle miniature per i video sono configurate nel passaggio **[!UICONTROL Miniature FFmpeg]** , nella scheda **[!UICONTROL Processo]** in **[!UICONTROL Argomenti]**.

>



**Per configurare le dimensioni delle miniature delle immagini:**

1. Tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]** > **[!UICONTROL Aggiorna risorsa DAM]** > **[!UICONTROL Modifica]**.
1. Tocca il passaggio **[!UICONTROL Risorse immagine di processo Dynamic Media]** e tocca o fai clic sulla scheda **[!UICONTROL Miniature]** . Modifica le dimensioni delle miniature in base alle esigenze, quindi tocca **[!UICONTROL OK]**.

   ![6_5_dinamicmediaprocesseassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Tocca il passaggio **[!UICONTROL Elabora miniature]**, quindi tocca la scheda **[!UICONTROL Miniature]**. Modifica le dimensioni delle miniature in base alle esigenze, quindi tocca **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >I valori nell’argomento miniature del passaggio **[!UICONTROL Elabora miniature]** devono corrispondere all’argomento miniature nel passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]**.

1. Tocca **[!UICONTROL Salva]** per salvare le modifiche al flusso di lavoro.

### Aumento o riduzione del numero di predefiniti immagine Dynamic Media visualizzati {#increasing-or-decreasing-the-number-of-image-presets-that-display}

I predefiniti immagine creati sono disponibili come rappresentazioni dinamiche quando visualizzi in anteprima le risorse. L&#39;Experience Manager mostra varie rappresentazioni dinamiche quando si visualizza una risorsa da **[!UICONTROL Vista dettagli > Rendering]**. Puoi aumentare o diminuire il limite di rappresentazioni visualizzate.

**Per aumentare o diminuire il numero di predefiniti immagine di Dynamic Media visualizzati:**

1. Passa a CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Passa al nodo di elenco dei predefiniti immagine in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![Increase_decreasethenumberofimagepresetsthatdisplay](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Nella proprietà **[!UICONTROL limit]**, modifica **[!UICONTROL Valore]**, che corrisponde a 15 per impostazione predefinita, inserendo un numero a piacere.
1. Passa alla sorgente dati del predefinito immagine in `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Nella proprietà limit , modifica il numero impostandolo sul numero desiderato, ad esempio `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Tocca **[!UICONTROL Salva tutto]**.

## Creazione di un predefinito immagine Dynamic Media {#creating-image-presets}

La creazione di un predefinito per immagini Dynamic Media consente di applicare tali impostazioni a tutte le immagini durante l’anteprima o la pubblicazione.

>[!NOTE]
>
>Se si utilizza Internet Explorer 9, la creazione di un predefinito non viene visualizzata nell’elenco dei predefiniti subito dopo il salvataggio. Per risolvere questo problema, disattiva la cache per IE9.

Se desideri supportare l’acquisizione di file AI, PDF ed EPS in modo da poter generare il rendering dinamico di questi formati di file, controlla le seguenti informazioni prima di creare i predefiniti per immagini.
Consulta [Formati di file Adobe Illustrator (AI), Postscript (EPS) e PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Se si desidera supportare l’acquisizione di file INDD in modo da poter generare il rendering dinamico di questo formato di file, prima di creare i predefiniti per immagini è possibile esaminare le seguenti informazioni.
Vedere [Formato del file InDesign (INDD)](#indesign-indd-file-format).

>[!NOTE]
>
>Per creare i predefiniti immagine di Dynamic Media, devi disporre dei privilegi di amministratore come amministratore di Experience Manager o amministratore di Admin Console.

**Per creare un predefinito immagine Dynamic Media:**

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale, quindi tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagini]**.
1. Fai clic su **[!UICONTROL Crea]**. Viene visualizzata la finestra **[!UICONTROL Modifica predefinito immagine]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Per rendere dinamico questo predefinito immagine, cancella i valori nei campi **[!UICONTROL larghezza]** e **[!UICONTROL altezza]**, lasciandoli vuoti.

1. Immetti i valori desiderati nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**, compreso un nome. Le opzioni sono descritte in [Opzioni predefinito immagine](#image-preset-options). I predefiniti vengono visualizzati nel riquadro a sinistra e possono essere usati all’istante con altre risorse.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Creazione di un predefinito per immagini reattive {#creating-a-responsive-image-preset}

Per creare un predefinito per immagini reattive, esegui i passaggi descritti in [Creazione di predefiniti immagine](#creating-image-presets). Quando immetti l&#39;altezza e la larghezza nella finestra **[!UICONTROL Modifica predefinito immagine]**, cancella i valori e lasciali vuoti.

Lasciandoli vuoti, indica ad Experience Manager che questo predefinito per immagini è reattivo. Se necessario, puoi regolare gli altri valori.



>[!NOTE]
>
>Per visualizzare i pulsanti **[!UICONTROL URL]** e **[!UICONTROL RESS]** quando applichi un predefinito immagine a una risorsa, la risorsa deve essere pubblicata.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>In modalità Dynamic Media - Scene7, i predefiniti immagine e le risorse immagine vengono pubblicati automaticamente.
>
>In Dynamic Media - Modalità ibrida, devi pubblicare manualmente i predefiniti immagine e le risorse immagine.

### Opzioni dei predefiniti per immagini {#image-preset-options}

Quando crei o modifichi i predefiniti immagine, hai le opzioni descritte in questa sezione. Inoltre, l’Adobe consiglia di iniziare con le seguenti opzioni di &quot;best practice&quot;:

* **[!UICONTROL Formato]** scheda (**[!UICONTROL Base]**) - Seleziona **[!UICONTROL JPEG]** o un altro formato che rispetta i tuoi requisiti. Tutti i browser web supportano il formato immagine JPEG, in quanto offre un buon compromesso tra dimensioni ridotte dei file e qualità delle immagini. Tuttavia, le immagini in formato JPEG usano uno schema di compressione che causa la perdita di dati, con possibile introduzione di artefatti di immagine indesiderati, qualora l’impostazione di compressione sia troppo bassa. Per questo motivo, Adobe consiglia di impostare la qualità di compressione su 75. Questa impostazione offre un buon compromesso tra la qualità delle immagini e le dimensioni ridotte dei file.

* **[!UICONTROL Attiva nitidezza semplice]**: non selezionare **[!UICONTROL Attiva nitidezza semplice]** (il filtro di nitidezza offre un controllo inferiore rispetto alle impostazioni Maschera definizione dettagli).

* **[!UICONTROL Nitidezza: Modalità]**  di ricampionamento - Seleziona  **[!UICONTROL Bi-Cubic]**.

#### Opzioni della scheda di base {#basic-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Nome</strong></td>
   <td>Inserisci un nome descrittivo senza spazi vuoti. Includi nel nome la specifica delle dimensioni dell’immagine in modo che gli utenti possano identificare questo predefinito per immagini.</td>
  </tr>
  <tr>
   <td><strong>Larghezza e Altezza</strong></td>
   <td>Immettere in pixel le dimensioni in cui l'immagine viene distribuita. Larghezza e altezza devono essere maggiori di 0 pixel. Se uno dei due valori è 0, non viene creato alcun predefinito. Se entrambi i valori sono vuoti, viene creato un predefinito per immagini reattive.</td>
  </tr>
  <tr>
   <td><strong>Formato</strong></td>
   <td><p>Scegli un formato dal menu.</p> <p>La scelta di <strong>JPEG</strong> offre le seguenti opzioni aggiuntive:</p>
    <ul>
     <li><strong>Qualità</strong>  - Controlla il livello di compressione JPEG. Questa impostazione influisce sia sulle dimensioni del file che sulla qualità dell'immagine. La scala di qualità JPEG è 1-100. La scala è visibile quando si trascina il cursore.</li>
     <li><strong>Attiva il downsampling della crominanza JPG</strong> : poiché l'occhio è meno sensibile alle informazioni sui colori ad alta frequenza rispetto alla luminanza ad alta frequenza, le immagini JPEG dividono le informazioni sulle immagini in componenti di luminanza e colore. Quando un'immagine JPEG viene compressa, il componente luminanza viene lasciato a risoluzione piena, mentre i componenti colore vengono sottoposti a sottocampionamento utilizzando una media di gruppi di pixel. Il sottocampionamento riduce il volume dei dati di mezzo o di un terzo, senza quasi alcun impatto sulla qualità percepita. Il campionamento non è applicabile alle immagini in scala di grigi. Questa tecnica riduce la quantità di compressione utile per le immagini con contrasto elevato (ad esempio, immagini con testo sovrapposto).</li>
    </ul>
    <div>
      Scelta
     <strong>GIF</strong> o
     <strong>Il GIF con alfa</strong> fornisce questi
     Opzioni <strong>Quantizzazione colore GIF</strong>:
    </div>
    <ul>
     <li><strong>Tipo  </strong>: seleziona  <strong>Adattivo</strong>  (opzione predefinita),  <strong>Web</strong> o  <strong>Macintosh</strong>. Se si seleziona <strong>GIF con Alpha</strong>, l'opzione Macintosh non è disponibile.</li>
     <li><strong>Dither</strong>  - Seleziona  <strong></strong> Diffusore o  <strong>Disattivato</strong>.</li>
     <li><strong>Numero di colori  </strong>- Immettere un numero da 2 a 256.</li>
     <li><strong>Elenco colori</strong>  - Inserisci un elenco separato da virgole. Ad esempio, per bianco, grigio e nero, immetti 00000,888888,ffff.</li>
    </ul>
    <div>
      Scelta
     <strong>PDF</strong>,
     <strong>TIFF</strong>, oppure
     <strong>TIFF con alfa</strong> fornisce questa opzione aggiuntiva:
    </div>
    <ul>
     <li><strong>Compressione</strong>  - Seleziona un algoritmo di compressione. Le opzioni dell'algoritmo per i PDF sono <strong>None</strong>, <strong>Zip</strong> e <strong>Jpeg</strong>; per TIFF le opzioni sono <strong>None</strong>, <strong>LZW</strong>, <strong>Jpeg</strong> e <strong>Zip</strong>; e per TIFF con Alpha sono <strong>Nessuno</strong>, <strong>LZW</strong> e <strong>Zip</strong>.</li>
    </ul> <p>La scelta di <strong>PNG</strong>, <strong>PNG con Alpha,</strong> o <strong>EPS</strong> non fornisce opzioni aggiuntive.</p> </td>
  </tr>
  <tr>
   <td><strong>Nitidezza</strong></td>
   <td>Selezionare l'opzione <strong>Abilita nitidezza semplice</strong> per applicare all'immagine un filtro di nitidezza di base dopo che è stata effettuata la modifica in scala. La nitidezza può contribuire a compensare la sfocatura che può verificarsi quando si visualizza un'immagine con dimensioni diverse. </td>
  </tr>
 </tbody>
</table>

#### Opzioni avanzate della scheda {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Campo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Spazio colore</strong></td>
   <td>Selezionare <strong>RGB, CMYK,</strong> o <strong>Scala di grigio</strong> per lo spazio colore.</td>
  </tr>
  <tr>
   <td><strong>Profilo colore</strong></td>
   <td>Seleziona il profilo dello spazio colore di output in cui deve essere convertita la risorsa se è diversa dal profilo di lavoro.</td>
  </tr>
  <tr>
   <td><strong>Intento di rendering</strong></td>
   <td>È possibile ignorare l'intento di rendering predefinito. Gli intenti di rendering determinano cosa succede ai colori che non possono essere riprodotti nel profilo del colore di destinazione (fuori gamma). L’Intento di rendering viene ignorato se non è compatibile con il profilo ICC.
    <ul>
     <li>Selezionare <strong>Perceptual</strong> per comprimere la gamma totale da uno spazio colore a un altro spazio colore quando uno o più colori nell'immagine originale non rientrano nella gamma dello spazio colore di destinazione.</li>
     <li>Selezionare <strong>Colorimetrico relativo</strong> quando un colore nello spazio colore corrente non rientra nell'intervallo di colori di destinazione. Inoltre, è possibile mapparlo al colore più vicino possibile all'interno della gamma dello spazio colore di destinazione senza influire su altri colori. </li>
     <li>Selezionare <strong>Saturazione</strong> per riprodurre la saturazione del colore dell'immagine originale durante la conversione nello spazio colore di destinazione. </li>
     <li>Selezionare <strong>Colorimetrico assoluto</strong> per abbinare esattamente i colori senza alcuna regolazione per il punto bianco o il punto nero che alteri la luminosità dell'immagine.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensazione punto nero</strong></td>
   <td>Seleziona questa opzione se il profilo di output supporta questa funzione. La compensazione blackpoint viene ignorata se non è compatibile con il profilo ICC specificato.</td>
  </tr>
  <tr>
   <td><strong>Dithering</strong></td>
   <td>Selezionare questa opzione per evitare o ridurre gli artefatti di striatura del colore. </td>
  </tr>
  <tr>
   <td><strong>Tipo di nitidezza</strong></td>
   <td><p>Selezionare <strong>Nessuno</strong>, <strong>Nitidezza</strong> o <strong>Maschera definizione dettagli</strong>. </p>
    <ul>
     <li>Selezionare <strong>Nessuno</strong> per disattivare la nitidezza.</li>
     <li>Selezionare <strong>Nitidezza</strong> se si desidera applicare all'immagine un filtro di nitidezza di base dopo che è stata effettuata la modifica in scala. La nitidezza può contribuire a compensare la sfocatura che può verificarsi quando si visualizza un'immagine con dimensioni diverse. </li>
     <li>Seleziona<strong> Maschera definizione dettagli</strong> per regolare con precisione un effetto filtro di nitidezza sull'immagine ricampionata verso il basso finale. Puoi controllare l’intensità dell’effetto, il raggio in pixel e una soglia di contrasto da ignorare. L’effetto utilizza le stesse opzioni del filtro “Maschera definizione dettagli” di Photoshop.</li>
    </ul> <p>In <strong>Maschera definizione dettagli</strong> sono disponibili le seguenti opzioni:</p>
    <ul>
     <li><strong>Importo</strong> : controlla la quantità di contrasto applicata ai pixel del bordo. Il valore predefinito del numero reale è 1,0. Per le immagini ad alta risoluzione, è possibile aumentarlo fino a 5,0. Considera il valore come una misura dell'intensità del filtro.</li>
     <li><strong>Raggio</strong> : determina il numero di pixel intorno ai pixel del bordo che influiscono sulla nitidezza. Per le immagini ad alta risoluzione, immetti un numero reale da 1 a 2. Un valore basso rende più nitidi solo i pixel del bordo; un valore elevato rende più nitida una banda più ampia di pixel. Il valore corretto dipende dalle dimensioni dell’immagine.</li>
     <li><strong>Soglia</strong> : determina l’intervallo di contrasto da ignorare quando viene applicato il filtro Maschera definizione dettagli. In altre parole, questa opzione determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e resi più nitidi. Per evitare di introdurre rumore, prova con valori interi compresi tra 2 e 20. </li>
     <li><strong>Applica a</strong> : determina se la non nitidezza viene applicata a ogni colore o luminosità.</li>
    </ul>
    <div>
      La nitidezza è descritta in
     <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/sharpening_images.pdf">Nitidezza immagini</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modalità ricampionamento</strong></td>
   <td>Selezionare un'opzione <strong>Modalità di ricampionamento</strong>. Queste opzioni consentono di aumentare la nitidezza dell’immagine durante il ricampionamento verso il basso:
    <ul>
     <li><strong>Bi-Lineare</strong>  - Il metodo di ricampionamento più veloce. Alcuni artefatti di aliasing sono evidenti.</li>
     <li><strong>Bi-Cubic</strong>  - Aumenta l'utilizzo della CPU ma produce immagini più nitide con artefatti di aliasing meno evidenti.</li>
     <li><strong>Sharp2</strong>  - Può produrre risultati leggermente più nitidi rispetto a Bi-Cubic, ma a un costo di CPU ancora più elevato.</li>
     <li><strong>Bi-Sharp</strong> : seleziona il ricampatore predefinito di Photoshop per ridurre le dimensioni dell'immagine, che si chiama Adobe Photoshop  <strong>bicubic </strong> sharperin.</li>
     <li><strong>Ogni </strong> colore e  <strong>luminosità</strong>  - ogni metodo può essere basato sul colore o sulla luminosità. Per impostazione predefinita, è selezionato <strong>Ogni colore</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Risoluzione di stampa</strong></td>
   <td>Selezionare una risoluzione per stampare l'immagine; Il valore predefinito è 72 pixel.</td>
  </tr>
  <tr>
   <td><strong>Modificatore immagine</strong></td>
   <td><p>Oltre alle comuni impostazioni immagine disponibili nell’interfaccia utente, Dynamic Media supporta numerose modifiche avanzate alle immagini che puoi specificare nel campo <strong>Modificatori immagine</strong> . Questi parametri sono definiti nel <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en#image-serving-api">riferimento al comando Image Server Protocol</a>.</p> <p>Importante: Le seguenti funzionalità elencate nell’API non sono supportate:</p>
    <ul>
     <li>Comandi di base per il modello e il rendering del testo: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandi di localizzazione: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> non è disponibile per l'utilizzo generale.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Servizi Dynamic Media non principali: SVG, Image Rendering e Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Definizione delle opzioni del predefinito immagine con i modificatori immagine {#defining-image-preset-options-with-image-modifiers}

Oltre alle opzioni disponibili nelle schede Base e Avanzate , è possibile definire modificatori di immagine per fornire ulteriori opzioni durante la definizione dei predefiniti per immagini. Il rendering delle immagini si basa sull&#39;API di rendering delle immagini definita in dettaglio in [Riferimento al protocollo HTTP](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html#image-serving-api).

Di seguito sono riportati alcuni esempi di base delle operazioni che puoi eseguire con i modificatori di immagini.

>[!NOTE]
>
>Alcuni modificatori di immagini [non possono essere utilizzati in Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html#image-serving-api)  - Inverte ogni componente del colore per ottenere un effetto immagine negativo.

   ```xml
   &op_invert=1
   ```

   ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html#image-serving-api)  - Applica un filtro di sfocatura all&#39;immagine.

   ```xml
   &op_blur=7
   ```

   ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandi combinati - op_blur e op-invert

   ```xml
   &op_invert=1&op_blur=7
   ```

   ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_bright](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html#image-serving-api)  - riduce o aumenta la luminosità.

   ```xml
   &op_brightness=58
   ```

   ![6_5_imagepreset-edit-luminosità](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html#image-serving-api)  - Regola l&#39;opacità dell&#39;immagine. Consente di ridurre l’opacità in primo piano.

   ```xml
   opac=29
   ```

   ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

## Modifica dei predefiniti per immagini {#modifying-image-presets}

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale, quindi tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagini]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Seleziona un predefinito e fai clic su **[!UICONTROL Modifica]**. Viene visualizzata la finestra **[!UICONTROL Modifica predefinito immagine]**.
1. Apporta le modifiche desiderate e fai clic su **[!UICONTROL Salva]** per salvarle oppure su **[!UICONTROL Annulla]** per annullare le modifiche.

## Pubblicazione dei predefiniti immagine Dynamic Media {#publishing-image-presets}

Se esegui Dynamic Media - Modalità ibrida, devi pubblicare manualmente i predefiniti per immagini.

(Se esegui la modalità Dynamic Media - Scene7, i predefiniti immagine vengono pubblicati automaticamente; non è necessario completare questi passaggi.)

**Per pubblicare i predefiniti immagine in Dynamic Media - Modalità ibrida:**

1. Ad Experience Manager, tocca o fai clic sul logo Experience Manager per accedere alla console di navigazione globale, quindi tocca o fai clic sull’icona Strumenti e passa a **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagini]**.
1. Seleziona il predefinito per immagini o più predefiniti immagine dall’elenco dei predefiniti per immagini e tocca o fai clic su **[!UICONTROL Pubblica]**.
1. Dopo la pubblicazione del predefinito immagine, lo stato cambia da non pubblicato a pubblicato.

   ![chlimage_1-81](assets/chlimage_1-505.png)

## Eliminazione dei predefiniti immagine Dynamic Media {#deleting-image-presets}

1. Ad Experience Manager, tocca o fai clic sul logo Experience Manager per accedere alla console di navigazione globale.
1. Tocca l’icona **[!UICONTROL Strumenti]**, quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Predefiniti immagini]**.
1. Seleziona un predefinito, quindi fai clic su **[!UICONTROL Elimina]**. Dynamic Media conferma che si desidera eliminarlo. Tocca **[!UICONTROL Elimina]** per eliminare o toccare **[!UICONTROL Annulla]** per interrompere l&#39;operazione.
