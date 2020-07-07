---
title: Aggiunta di funzioni di Dynamic Media Classic alla pagina
description: Scopri come aggiungere funzionalità e componenti Dynamic Media Classic alla pagina AEM.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 26%

---


# Aggiunta di funzioni di Dynamic Media Classic alla pagina {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) è una soluzione in hosting per la gestione, l&#39;ottimizzazione, la pubblicazione e la distribuzione di risorse multimediali per schermi e stampe Web, mobili, e-mail e connessi a Internet.

Potete visualizzare le risorse AEM pubblicate in Dynamic Media Classic in diversi visualizzatori:

* Zoom
* A comparsa
* Video
* Modello immagini
* Immagine

Potete pubblicare risorse digitali direttamente da AEM ad Dynamic Media Classic e pubblicare risorse digitali da Dynamic Media Classic ad AEM.

Questo documento descrive come pubblicare risorse digitali da AEM ad Dynamic Media Classic e viceversa. Sono inoltre descritti nel dettaglio i visualizzatori. Per informazioni sulla configurazione di AEM per Dynamic Media Classic, consultate [Integrazione di Dynamic Media Classic con AEM](/help/sites-administering/scene7.md).

Consulta anche [Aggiunta di mappe immagine](image-maps.md).

For more information on using video components with AEM, see [Video](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## Pubblicazione manuale in Dynamic Media Classic dalle risorse {#manually-publishing-to-scene-from-assets}

Potete pubblicare risorse digitali in Dynamic Media Classic come segue:

* [Nell’interfaccia utente classica dalla console Risorse](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Nell’interfaccia utente classica da una risorsa](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Nell’interfaccia utente classica dall’esterno della cartella Target di CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM viene pubblicato in Dynamic Media Classic in modo asincrono. After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Componenti Dynamic Media Classic {#scene-components}

In AEM sono disponibili i seguenti componenti Dynamic Media Classic:

* Zoom
* Zoom a comparsa
* Modello immagini
* Immagine
* Video

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. Le risorse non ancora pubblicate in Dynamic Media Classic vengono pubblicate in Dynamic Media Classic se si trovano in una cartella sincronizzata o su una pagina o con una configurazione cloud Dynamic Media Classic.

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Avviso sulla fine del ciclo di vita dei visualizzatori Flash {#flash-viewers-end-of-life-notice}

A partire dal 31 gennaio 2017, Adobe Dynamic Media Classic ha terminato il supporto per la piattaforma di visualizzatori Flash.

Per ulteriori informazioni su questa importante modifica, consulta le [domande frequenti sulla terminazione dei visualizzatori Flash](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

L’aggiunta di un componente Dynamic Media Classic (Scene7) a una pagina equivale all’aggiunta di un componente a qualsiasi pagina. I componenti di Dynamic Media Classic sono descritti dettagliatamente nelle sezioni seguenti.

**Aggiunta di un componente Dynamic Media Classic (Scene7) a una pagina**

1. In AEM, aprite la pagina in cui desiderate aggiungere il componente Dynamic Media Classic (Scene7).

1. Se non sono disponibili componenti Dynamic Media Classic, fate clic su **[!UICONTROL Modalità progettazione]** , toccate un componente con bordo blu, toccate l&#39;icona **[!UICONTROL Elemento padre]** e quindi l&#39;icona **[!UICONTROL Configurazione]** . In **[!UICONTROL Parsys (Design)]**, selezionate tutti i componenti Dynamic Media Classic per renderli disponibili e fate clic su **[!UICONTROL OK.]**

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Fate clic su **[!UICONTROL Modifica]** per tornare alla modalità **[!UICONTROL Modifica]** .

1. Trascinate un componente dal gruppo Dynamic Media Classic nella barra laterale sulla pagina nella posizione desiderata.

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. Se necessario, modifica il componente, quindi fai clic su **[!UICONTROL OK]** per salvare le modifiche.
1. Trascinate l’immagine o il video dal browser del contenuto al componente Dynamic Media Classic aggiunto alla pagina.

   >[!NOTE]
   >
   >Solo nell’interfaccia touch, è necessario trascinare l’immagine o il video sul componente Dynamic Media Classic inserito nella pagina. La selezione e la modifica del componente Dynamic Media Classic e la scelta della risorsa non sono supportate.

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

Una progettazione reattiva per le risorse significa che queste si adattano a seconda di dove vengono visualizzate. Grazie alla progettazione reattivo, le stesse risorse possono essere visualizzate in modo efficace su dispositivi diversi.

Vedere anche [Responsive Design for Web Pages](/help/sites-developing/responsive.md).

**Per aggiungere un&#39;esperienza di visualizzazione interattiva a un sito reattivo**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Se i componenti di Dynamic Media Classic non sono disponibili, accertatevi [di attivarli in modalità](/help/sites-authoring/default-components-designmode.md)Progettazione.

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. Selezionate il componente e toccate l’icona di configurazione.
1. Nella scheda Impostazioni **** Dynamic Media Classic, regolare i punti di interruzione.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Verifica che i visualizzatori si ridimensionino in modo reattivo e che tutte le interazioni siano ottimizzate per desktop, tablet e dispositivi mobili.

### Impostazioni comuni a tutti i componenti Dynamic Media Classic {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL Riferimento]** file - Individuare il file a cui si desidera fare riferimento. Il riferimento al file mostra l’URL della risorsa e non necessariamente l’URL completo di Dynamic Media Classic, inclusi i comandi e i parametri dell’URL. In questo campo non è possibile aggiungere parametri e comandi URL di Dynamic Media Classic. che devono essere aggiunti attraverso la funzionalità corrispondente nel componente.
* **[!UICONTROL Larghezza]** - Consente di impostare la larghezza.
* **[!UICONTROL Altezza]** - Consente di impostare l&#39;altezza.

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

La risorsa dispone di strumenti di zoom nella parte inferiore. Toccate **[!UICONTROL +]** per ingrandire. Toccate **[!UICONTROL per]** ridurre. Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. Toccate le frecce diagonali per visualizzarle a schermo intero. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### A comparsa {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. Tuttavia, tenete presente che esiste un limite alla configurazione reattiva del componente. When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### Immagine {#image}

Il componente **[!UICONTROL Immagine]** classica di Dynamic Media consente di aggiungere alle immagini funzionalità di Dynamic Media Classic, ad esempio modificatori Dynamic Media Classic, predefiniti per immagini o visualizzatori e nitidezza. Il componente **[!UICONTROL Immagine]** classica di Dynamic Media è simile ad altri componenti immagine in AEM con funzionalità Dynamic Media Classic speciale. In questo esempio, all’immagine è `&op_invert=1` applicato il modificatore URL Dynamic Media Classic.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Titolo, Testo]** Alt - Nella scheda **[!UICONTROL Avanzate]** , aggiungere un titolo all’immagine e testo alternativo per gli utenti che hanno disattivato la grafica.

**[!UICONTROL URL, Apri in]** - Puoi impostare una risorsa da cui aprire un collegamento. Imposta l’**[!UICONTROL URL]** e in **[!UICONTROL Apri in]** indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Predefinito]** visualizzatore - Selezionate un predefinito esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

**[!UICONTROL Configurazione]** Dynamic Media Classic - Selezionate la configurazione Dynamic Media Classic da usare per recuperare i predefiniti immagine attivi da SPS.

**[!UICONTROL Predefinito]** immagine - Selezionate un predefinito per immagini esistente dal menu a discesa. Se il predefinito per immagini che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per immagini](/help/assets/managing-image-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

**[!UICONTROL Formato]** di output - Selezionare il formato di output dell&#39;immagine, ad esempio jpeg. A seconda del formato di output selezionato, è possibile che siano disponibili ulteriori opzioni di configurazione. Consulta [Best practice sui predefiniti per immagini](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Nitidezza]** - Selezionate la modalità di nitidezza dell’immagine. La regolazione della nitidezza è descritta in dettaglio in [Best practice sui predefiniti per immagini](/help/assets/managing-image-presets.md#image-preset-options) e [Best practice sulla nitidezza](/help/assets/assets/s7_sharpening_images.pdf).

**[!UICONTROL Modificatori]** URL - Potete modificare gli effetti immagine fornendo ulteriori comandi immagine Dynamic Media Classic. Tali situazioni vengono descritte in [Predefiniti per immagini](/help/assets/managing-image-presets.md) e nella [Guida ai comandi](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Punti di interruzione]** - Se il sito Web è reattivo, è necessario regolare i punti di interruzione. I punti di interruzione devono essere separati da virgole ( , ).

### Modello immagini {#image-template}

[I modelli](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) immagine classici di Dynamic Media sono contenuti Photoshop a più livelli importati in Dynamic Media Classic, dove il contenuto e le proprietà erano parametrizzati per la variabilità. Il componente **[!UICONTROL Modello immagini]** consente di importare immagini e modificare il testo in modo dinamico in AEM. Inoltre, è possibile configurare il componente **[!UICONTROL Modello immagini]** in modo che utilizzi valori contestuali ClientContext, affinché ogni utente possa avere un’esperienza personalizzata dell’immagine.

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Riferimento file, Larghezza, Altezza]** - Consultate le impostazioni comuni a tutti i componenti di ScDynamic Media Classic7.

>[!NOTE]
>
>I comandi e i parametri URL di Dynamic Media Classic non possono essere aggiunti direttamente all’URL di riferimento del file. Possono essere definiti solo nell’interfaccia utente del componente del pannello **[!UICONTROL Parametri]**.

**[!UICONTROL Titolo, Testo]** Alt - Nella scheda Modello immagine di Dynamic Media Classic aggiungere un titolo all’immagine e al testo alternativo per gli utenti che hanno disattivato la grafica.

**[!UICONTROL URL, Apri in]** - Puoi impostare una risorsa da cui aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Pannello]** parametri - Quando importate un’immagine, i parametri vengono precompilati con le informazioni dell’immagine. Se non vi sono contenuti modificabili dinamicamente, questa finestra è vuota.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Modifica dinamica del testo {#changing-text-dynamically}

Per modificare il testo in modo dinamico, immetti un nuovo testo nei campi e fai clic su **[!UICONTROL OK.]** In questo esempio, il **[!UICONTROL Prezzo]** è ora di $50 e la spedizione è di 99 centesimi.

![chlimage_1-234](assets/chlimage_1-234.png)

Il testo nell’immagine cambia. You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Modifica del testo in base a un valore personalizzato ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK.]** In questo esempio, il nome cambia perché è collegato al nome formattato nel profilo.

![chlimage_1-236](assets/chlimage_1-236.png)

Il testo si aggiorna con il nome dell’utente attualmente connesso. Per ripristinare il testo al valore originale, fai clic su **[!UICONTROL Ripristina]** accanto al campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Come rendere il modello di immagine Dynamic Media Classic un collegamento {#making-the-scene-image-template-a-link}

1. Sulla pagina con il componente Dynamic Media Classic **[!UICONTROL Image Template]** , toccate **[!UICONTROL Modifica.]**
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. In the **[!UICONTROL Open in]** field, select whether you want the target to open (a new window or same window).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Toccate **[!UICONTROL OK.]**

### Componente video {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. Questo componente è un lettore video HTML5; è un singolo visualizzatore che può essere usato su più canali.

Può essere usato per set video adattivi, un singolo video MP4 o un singolo video F4V.

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. Inoltre, vedete [il componente Video di Dynamic Media Classic e il componente](s7-video.md)Video di base.

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitazioni note per il componente video {#known-limitations-for-the-video-component}

Adobe DAM e WCM mostrano se un video sorgente principale viene caricato. Non mostrano queste risorse proxy:

* Rappresentazioni codificate di Dynamic Media Classic
* Set video adattivi Dynamic Media Classic

Quando usate un set video adattivo con il componente video Dynamic Media Classic, dovete ridimensionare il componente per adattarlo alle dimensioni del video.

## Browser dei contenuti Dynamic Media Classic {#scene-content-browser}

Il browser Dynamic Media Classic consente di visualizzare i contenuti da Dynamic Media Classic direttamente in AEM. To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. La funzionalità è identica nelle due interfacce utente.

Se si dispone di più configurazioni, per impostazione predefinita AEM visualizza la [configurazione predefinita](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puoi selezionare diverse configurazioni direttamente nel browser del contenuto di Dynamic Media Classic nel menu a discesa.

>[!NOTE]
>
>* Le risorse che si trovano nella cartella ad hoc non verranno visualizzate nel browser del contenuto di Dynamic Media Classic.
>* Quando Anteprima [protetta è abilitata](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), le risorse pubblicate e non pubblicate in Dynamic Media Classic vengono visualizzate nel browser dei contenuti di Dynamic Media Classic.
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* Per i video, il browser del contenuto Dynamic Media Classic supporta:

   >
   >   
   * Set di video adattivo: contenitore di tutte le rappresentazioni video necessarie per consentirne la riproduzione su diversi tipi di schermi
   >   * Video MP4 singolo
   >   * Video F4V singolo


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

Potete accedere al browser del contenuto nell’interfaccia touch o classica. Al momento l’interfaccia touch presenta i seguenti limiti:

* Le risorse FXG e Flash di Dynamic Media Classic non sono supportate.

Sfogliate le risorse di Dynamic Media Classic selezionando **[!UICONTROL Dynamic Media Classic]** dal terzo menu a discesa. Dynamic Media Classic non viene visualizzato nell&#39;elenco se non è stata configurata l&#39;integrazione Dynamic Media Classic/AEM.

>[!NOTE]
>
>* Il browser dei contenuti di Dynamic Media Classic carica circa 100 risorse e le ordina per nome.
>* Se è impostato un server di anteprima protetto, il browser utilizzerà tale server di anteprima per eseguire il rendering delle miniature e delle risorse.

>



![chlimage_1-240](assets/chlimage_1-240.png)

Inoltre, potete sfogliare le informazioni sulla risoluzione, le dimensioni, i giorni successivi alla modifica e il nome del file passando il puntatore del mouse sulla risorsa nel browser.

![chlimage_1-241](assets/chlimage_1-241.png)

* Per i set video adattivi e i modelli, per le miniature non vengono generate informazioni sulle dimensioni.
* Per i set video adattivi, non viene generata alcuna risoluzione per le miniature.

### Ricerca di risorse Dynamic Media Classic con il browser dei contenuti {#searching-for-scene-assets-with-the-content-browser}

La ricerca di risorse Dynamic Media Classic è simile alla ricerca di risorse AEM, ma quando effettuate una ricerca viene visualizzata una visualizzazione remota delle risorse nel sistema Dynamic Media Classic, anziché importarle direttamente in AEM.

Per visualizzare e cercare le risorse è possibile utilizzare l’interfaccia touch o classica. A seconda dell’interfaccia, la modalità di ricerca è leggermente diversa.

Durante la ricerca in una qualsiasi delle interfacce utente, è possibile filtrare in base ai seguenti criteri (mostrati qui nell’interfaccia touch):

**[!UICONTROL Inserite le parole chiave]** : potete cercare le risorse per nome. Durante la ricerca, immetti le parole chiave con cui inizia il nome del file. Ad esempio, se digiti la parola “nuoto” verranno cercati i nomi dei file delle risorse che iniziano con queste lettere, in questo ordine. Toccate Invio dopo aver digitato il termine per trovare la risorsa.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Cartella/percorso]** - Il nome della cartella visualizzata si basa sulla configurazione selezionata. Per approfondire i livelli inferiori, toccate l’icona della cartella e selezionate una sottocartella, quindi toccate il segno di spunta per selezionarla.

Se si immette una parola chiave e si seleziona una cartella, AEM esegue la ricerca in tale cartella e in tutte le relative sottocartelle. Tuttavia, se non si immettono parole chiave durante la ricerca, la selezione della cartella mostrerà solo le risorse in quella cartella, senza includere le sottocartelle.

Per impostazione predefinita, AEM cerca nella cartella selezionata e in tutte le sue sottocartelle.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo di risorsa]** - Selezionate **[!UICONTROL Dynamic Media Classic]** per sfogliare il contenuto di Dynamic Media Classic. Questa opzione è disponibile solo se è stato configurato Dynamic Media Classic.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configurazione]** - Se hai più di una configurazione Dynamic Media Classic definita in [!UICONTROL Cloud Services], puoi selezionarla qui. Di conseguenza, la cartella cambierà in base alla configurazione scelta.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo]** di risorsa - Nel browser Dynamic Media Classic potete filtrare i risultati in modo da includere i seguenti elementi: immagini, modelli, video e set video adattivi. Se non si seleziona alcun tipo di risorsa, per impostazione predefinita AEM ricerca tutti i tipi di risorsa.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Nell’interfaccia classica, è anche possibile cercare **Flash** e **FXG**. Al momento questi non sono disponibili come filtro di ricerca nell’interfaccia touch.
   >
   >
* Durante la ricerca di video, si cerca una singola rappresentazione. I risultati restituiscono la rappresentazione originale (solo &amp;ast;.mp4) e la rappresentazione codificata.
>* Quando eseguite una ricerca in un set video adattivo, dovete cercare nella cartella e in tutte le sottocartelle, ma solo se avete aggiunto una parola chiave alla ricerca. Se non hai aggiunto una parola chiave, AEM non cerca nelle sottocartelle.

>



**[!UICONTROL Stato]** pubblicazione: potete filtrare le risorse in base allo stato di pubblicazione: **[!UICONTROL Non pubblicato]** o **[!UICONTROL Pubblicato.]** Se non selezionate Stato **** pubblicazione, AEM esegue per impostazione predefinita la ricerca in tutti gli stati di pubblicazione.

![chlimage_1-247](assets/chlimage_1-247.png)

