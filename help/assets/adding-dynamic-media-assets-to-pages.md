---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Come aggiungere componenti per contenuti multimediali dinamici a una pagina in AEM
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '3092'
ht-degree: 33%

---


# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi inserire direttamente nella pagina il componente **Dynamic Media**, **File multimediali interattivi**, **Elemento multimediale panoramico** o **File multimediali video 360**. A tale scopo, entra in modalità Layout e attiva i componenti Dynamic Media. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Dynamic Media sono intelligenti: rilevano l’aggiunta di un’immagine o di un video, dunque le opzioni di configurazione disponibili cambiano di conseguenza.

Se utilizzi AEM come WCM, puoi aggiungere direttamente alla pagina le risorse Dynamic Media. Se ti avvali di una terza parte per WCM, puoi [collegare](/help/assets/linking-urls-to-yourwebapplication.md) o [incorporare](/help/assets/embed-code.md) le risorse. Per un sito web dinamico di terze parti, consulta la sezione [Distribuzione di immagini ottimizzate in un sito dinamico](/help/assets/responsive-site.md).

>[!NOTE]
>
>È necessario pubblicare le risorse prima di aggiungerle alle pagine in AEM. See [Publishing Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md).

## Adding a Dynamic Media component to a page {#adding-a-dynamic-media-component-to-a-page}

L’aggiunta di un componente File multimediali 3D, Contenuti multimediali dinamici, Contenuti multimediali interattivi, Contenuti multimediali panoramici, Video SmartCrop o Video 360 a una pagina equivale all’aggiunta di un componente a qualsiasi pagina. I componenti per contenuti multimediali dinamici sono descritti nelle sezioni seguenti.

1. In AEM, apri la pagina in cui desideri aggiungere il Componente elementi multimediali dinamici.
1. Nel pannello a sinistra della pagina (potrebbe essere necessario attivare o disattivare la visualizzazione del pannello laterale), fate clic sull’icona **[!UICONTROL Componenti]** .
1. Nell’intestazione **[!UICONTROL Componenti]** , selezionate Contenuti multimediali **[!UICONTROL dinamici dall’elenco a discesa.]**

   Se non è disponibile alcun elenco di componenti per contenuti multimediali dinamici, è probabile che sia necessario attivarli. See [Enabling Dynamic Media components](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](/help/assets/assets/6_5_360video_wcmcomponent.png)

1. Trascinate un componente **[!UICONTROL Contenuti multimediali]** dinamici da usare e rilasciatelo nella posizione desiderata sulla pagina.

1. Passate il puntatore del mouse direttamente sul componente. Quando il componente è circondato da una casella blu, toccate una volta per visualizzare la barra degli strumenti del componente. Toccate l&#39;icona **[!UICONTROL Configurazione (chiave inglese)]** .

   ![6_5_360video_wcmcomponentconfigure](/help/assets/assets/6_5_360video_wcmcomponentconfigure.png)

1. A seconda del componente Contenuti multimediali dinamici rilasciato sulla pagina, si apre una finestra di dialogo di configurazione. [Impostate le opzioni](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) del componente come necessario.

   L’esempio seguente mostra la finestra di dialogo del componente **[!UICONTROL Video 360 per contenuti multimediali]** dinamici e le opzioni disponibili nell’elenco a discesa Predefinito visualizzatore.

   ![Video 360 Media component](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Componente Video multimediale dinamico 360.

1. Al termine, nell’angolo superiore destro della finestra di dialogo toccate il segno di spunta per salvare le modifiche.

### Abilitazione di componenti per contenuti multimediali dinamici {#enabling-dynamic-media-components}

Se non è disponibile alcun componente per contenuti multimediali dinamici da aggiungere a una pagina, è probabile che sia necessario prima abilitare i componenti che si desidera utilizzare.

1. In AEM, apri la pagina in cui desideri aggiungere il Componente elementi multimediali dinamici.
1. Sul lato sinistro della barra degli strumenti accanto alla parte superiore della pagina, toccate l’icona Informazioni pagina, quindi toccate **[!UICONTROL Modifica modello]** dall’elenco a discesa.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. Sul lato destro della barra degli strumenti accanto alla parte superiore della pagina, toccate **[!UICONTROL Struttura dall’elenco a discesa.]**

   ![Criterio](/help/assets/assets-dm/structure-mode.png)

1. Nella parte inferiore della pagina, toccate Contenitore **[!UICONTROL di]** layout per aprire la relativa barra degli strumenti, quindi toccate l&#39;icona Criterio.
1. Nella pagina Contenitore **[!UICONTROL di]** layout, sotto l&#39;intestazione **[!UICONTROL Proprietà]** , assicurarsi che la scheda Componenti **** consentiti sia selezionata.

   ![Componenti consentiti](/help/assets/assets-dm/allowed-components.png)

1. Scorrete fino a visualizzare gli elementi multimediali **[!UICONTROL dinamici.]**
1. Toccate l’icona > a sinistra di **[!UICONTROL Contenuti multimediali]** dinamici per espandere l’elenco, quindi selezionate i componenti Contenuti multimediali dinamici da attivare.

   ![Elenco dei componenti per elementi per elementi per elementi per elementi per contenuti multimediali dinamici](/help/assets/assets-dm/dm-components-select.png)

1. Nell&#39;angolo superiore destro della pagina Contenitore **[!UICONTROL di]** layout, toccate l&#39;icona Fine (segno di spunta).

1. Sul lato destro della barra degli strumenti accanto alla parte superiore della pagina, toccate Contenuto **** iniziale dall’elenco a discesa, quindi [aggiungete un componente Contenuti multimediali dinamici alla pagina](#adding-a-dynamic-media-component-to-a-page) come al solito.

## Localizzazione dei componenti per contenuti multimediali dinamici {#localizing-dynamic-media-components}

Potete localizzare i componenti per contenuti multimediali dinamici in uno dei due modi seguenti:

* In una pagina web di Sites, apri **[!UICONTROL Proprietà]** e seleziona la scheda **[!UICONTROL Avanzate]**. Scegli la lingua desiderata per la localizzazione.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Dal selettore del sito, selezionate la pagina o il gruppo di pagine desiderato. Toccate **[!UICONTROL Proprietà]** e selezionate la scheda **[!UICONTROL Avanzate]** . Scegli la lingua desiderata per la localizzazione.

   >[!NOTE]
   >
   >Al momento non tutte le lingue disponibili nel menu **[!UICONTROL Lingua]** dispongono di token.

## Componente elementi multimediali dinamici {#dynamic-media-components}

I componenti per contenuti multimediali dinamici sono disponibili quando toccate l’icona **[!UICONTROL Componenti]** e quindi applicate un filtro agli elementi multimediali **[!UICONTROL dinamici.]**

I componenti per contenuti multimediali dinamici disponibili sono i seguenti:

* **[!UICONTROL Dynamic Media]**: da utilizzare per risorse quali immagini, video, eCatalog e set 360 gradi.
* **[!UICONTROL Contenuti multimediali]** interattivi - Utilizzate per qualsiasi risorsa interattiva, ad esempio video interattivi, immagini interattive o set di caroselli.
* **[!UICONTROL Supporti]** panoramici - Utilizzati per immagini panoramiche o risorse di immagini VR panoramiche.
* **[!UICONTROL Video 360 Media]** - Utilizzate per risorse video 360 e 360 VR.

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere resi disponibili dall’editor modelli prima di utilizzarli. [Una volta resi disponibili](/help/sites-authoring/templates.md#editing-templates-template-authors)nell’editor modelli, potete aggiungere i componenti alla pagina come qualsiasi altro componente AEM.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente elementi multimediali dinamici {#dynamic-media-component}

Il componente Contenuti multimediali dinamici è elegante. A seconda se aggiungete un’immagine o un video, avete a disposizione diverse opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Più istanze del componente Contenuti multimediali dinamici in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito per visualizzatori diverso a ciascun componente per contenuti multimediali dinamici nella pagina non è supportata.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti per contenuti multimediali dinamici che utilizzano risorse dello stesso tipo, all’interno della pagina.

Quando aggiungi il Componente elementi multimediali dinamici e le **[!UICONTROL Impostazioni elemento multimediale dinamico]** sono vuote o non è possibile aggiungere correttamente una risorsa, controlla quanto segue:

* È stato [abilitato Elemento multimediale dinamico](/help/assets/config-dynamic.md). Dynamic Media è disattivato per impostazione predefinita.
* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell&#39;attivazione dell’elemento multimediale dinamico non hanno un file TIFF piramidale.

#### Quando si lavora con le immagini {#when-working-with-images}

Il componente elementi multimediali dinamici consente di aggiungere immagini dinamiche, compresi set di immagini, set di rotazione e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere un&#39;immagine reattiva è possibile impostare i punti di interruzione o applicare un predefinito immagine reattiva.

You *must* edit the following Dynamic Media Settings by tapping the **[!UICONTROL Edit]** icon in the component and then **[!UICONTROL Dynamic Media Settings.]**

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza.]**

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un predefinito esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi. Anche i predefiniti per visualizzatori sono avanzati: vengono visualizzati solo i predefiniti per visualizzatori pertinenti.

* **[!UICONTROL Modificatori]** visualizzatore - I modificatori visualizzatore assumono la forma di coppia nome=valore con un carattere di delimitazione &amp; e consentono di modificare i visualizzatori come indicato nella guida di riferimento dei visualizzatori. Un esempio di modificatore del visualizzatore è `posterimage=img.jpg&caption=text.vtt,1` che imposta un’immagine diversa per la miniatura del video e associa un file di sottotitoli/sottotitoli codificati al video.

* **[!UICONTROL Predefinito]** immagine - Selezionate un predefinito per immagini esistente dal menu a discesa. Se il predefinito per immagini che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Modificatori]** immagini - Potete applicare effetti immagine fornendo ulteriori comandi immagine. Questi sono descritti nei predefiniti per immagini e nel riferimento al comando Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Punti di interruzione]**: se utilizzi questa risorsa in un sito reattivo, devi aggiungere i punti di interruzione immagine. I punti di interruzione immagine devono essere separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   You can edit the following Advanced Settings by tapping **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Titolo]**(Title) - Consente di modificare il titolo dell&#39;immagine.

* **[!UICONTROL Testo]** Alt (Alt Text) - Aggiungete un titolo all&#39;immagine per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]**(Open in) - Potete impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]**(Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]**(Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.


#### Quando esegui operazioni con i Video {#when-working-with-video}

Usate il componente Contenuti multimediali dinamici per aggiungere video dinamici alle pagine Web. Quando modifichi il componente puoi scegliere di usare un predefinito visualizzatore video predefinita per la riproduzione del video nella pagina.

![chlimage_1-173](assets/chlimage_1-540.png)

You must edit the following Dynamic Media Settings by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. If you want to make it a fixed size, set it in the component with the **[!UICONTROL Width]** and **[!UICONTROL Height]** in the **[!UICONTROL Advanced]** tab.

* **[!UICONTROL Predefinito]** visualizzatore: selezionate un predefinito per visualizzatori video esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Modificatori]** visualizzatore - I modificatori visualizzatore assumono la forma di coppia nome=valore con un carattere di delimitazione &amp; e consentono di modificare i visualizzatori come indicato nella guida di riferimento dei visualizzatori di Adobi . Un esempio di modificatore visualizzatore è `posterimage=img.jpg&caption=text.vtt,1`

   I modificatori del visualizzatore consentono, ad esempio, di effettuare le seguenti operazioni:

   * Associare un file di sottotitoli a un video: [caption][https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associare un file di navigazione a un video: [navigation][https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   You can edit the following Advanced Settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Titolo]**(Title) - Consente di modificare il titolo del video.

* **[!UICONTROL Larghezza]**(Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]**(Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

#### Quando si lavora con Smart Crop {#when-working-with-smart-crop}

Usate il componente Contenuti multimediali dinamici per aggiungere le risorse di immagine Ritaglio avanzato alle pagine Web. Quando modifichi il componente puoi scegliere di usare un predefinito visualizzatore video predefinita per la riproduzione del video nella pagina.

Consultate anche Profili [immagine](/help/assets/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

You must edit the following Dynamic Media Setting by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza.]**

* **[!UICONTROL Modificatori]** immagini - Potete applicare effetti immagine fornendo ulteriori comandi immagine. Questi sono descritti nei predefiniti per immagini e nel riferimento al comando Image Server.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   You can edit the following Advanced Settings by clicking **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Titolo]**(Title) - Consente di modificare il titolo dell&#39;immagine SmartCrop.

* **[!UICONTROL Testo]** Alt (Alt Text) - Aggiungete un titolo all&#39;immagine di ritaglio avanzato per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]**(Open in) - Potete impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]**(Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]**(Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

### Componente File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente Contenuti multimediali interattivi è avanzato. A seconda se aggiungete un’immagine o un video, avete a disposizione diverse opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Più istanze del componente Supporto interattivo in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
Tenete presente che l’assegnazione di un predefinito per visualizzatori diverso a ciascun componente per contenuti multimediali interattivi in quella pagina non è supportata.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti per contenuti multimediali interattivi che utilizzano risorse dello stesso tipo, all’interno della pagina.

![chlimage_1-174](assets/chlimage_1-541.png)

You can edit the following **[!UICONTROL General]** settings by tapping **[!UICONTROL Edit]** in the component.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un predefinito esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Titolo]**(Title) - Consente di modificare il titolo del video.

* **[!UICONTROL Larghezza]**(Width) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]**(Height) - Immettete il valore in pixel se desiderate che l&#39;immagine sia di dimensione fissa. Se questo valore viene lasciato vuoto, la risorsa diventa adattiva.

   È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Mostra risorsa]** prodotto: per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

* **[!UICONTROL Mostra prezzo]** prodotto: per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

* **[!UICONTROL Mostra modulo]** prodotto - Per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.

### Componente multimediale panoramica {#panoramic-media-component}

Il componente Contenuti multimediali panoramici è destinato alle risorse che sono immagini panoramiche sferiche. Tali immagini forniscono un&#39;esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio. Affinché un’immagine possa essere definita come panorama sferico, deve avere una O entrambe le caratteristiche seguenti:

* Proporzioni di 2:1.
* Tag con le parole chiave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Consultate [Utilizzo dei tag](/help/sites-authoring/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dettagli risorsa e al componente WCM per **[!UICONTROL elementi multimediali panoramici]**.

>[!NOTE]
>
>Se la pagina Web ha i seguenti elementi:
>
>* Nella stessa pagina vengono utilizzate più istanze del componente **[!UICONTROL Panoramic Media]** .
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
Non è supportata l’assegnazione di un predefinito visualizzatore diverso a ciascun componente **[!UICONTROL Elemento multimediale panoramico]** di quella pagina.
>
>Tuttavia, potete usare lo stesso predefinito per visualizzatori per tutti i componenti per file multimediali panoramici che utilizzano risorse dello stesso tipo, all’interno della pagina.

![panoramica-media-predefinito per visualizzatori](assets/panoramic-media-viewer-preset.png)

Per modificare la seguente impostazione, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un visualizzatore esistente dal menu a discesa Predefinito visualizzatore.

Se il predefinito per visualizzatori ricercato non è visibile, accertatevi che sia pubblicato. Per poter usare i predefiniti per visualizzatori, dovete pubblicarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

### Video 360 Media Component {#video-media-component}

Usate il componente **[!UICONTROL Video 360 Media]** per riprodurre video equirettangolari sulla pagina Web per un’esperienza di visualizzazione coinvolgente di una stanza, una proprietà, un luogo, un paesaggio o una procedura medica.

Durante la riproduzione su un display piatto, l&#39;utente ha il controllo dell&#39;angolo di visione; la riproduzione su dispositivi mobili solitamente utilizza i controlli giroscopici incorporati.

Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. Potete distribuire video a 360 gradi utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Per modificare la seguente impostazione, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito]** visualizzatore - Selezionate un visualizzatore esistente dal menu a discesa Predefinito visualizzatore. Utilizzate Video360VR per gli utenti finali che utilizzano occhiali di realtà virtuale. Include controlli di riproduzione video di base e funzioni per social media. Utilizzate Video360_social che include controlli di riproduzione video di base. Il rendering video viene eseguito in modalità stereo. Il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato. Non esistono funzioni per social media.

Se il predefinito per visualizzatori ricercato non è visibile, accertatevi che sia pubblicato. Per poter usare i predefiniti per visualizzatori, dovete pubblicarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

### Utilizzo di HTTP/2 per la distribuzione di risorse multimediali dinamiche {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 è il nuovo protocollo Web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, migliorando la risposta e i tempi di caricamento.

Per informazioni dettagliate sull’utilizzo di HTTP/2 con l’account per contenuti multimediali dinamici, consultate Consegna di contenuti [](/help/assets/http2.md) HTTP2.

>[!MORELIKETHIS]
>
>* [Utilizzo del lettore video in AEM file multimediali dinamici](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-player-feature-video-use.html)
>* [Utilizzo di video interattivi con AEM file multimediali dinamici](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-interactive-video-feature-video-use.html)
>* [Il visualizzatore delle risorse con AEM elementi multimediali dinamici](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-viewer-feature-video-understand.html)
>* [Utilizzo della miniatura video personalizzata con AEM elemento multimediale dinamico](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Gestione del colore con AEM elementi multimediali dinamici](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-color-management-technical-video-setup.html)
>* [Utilizzo della nitidezza delle immagini con AEM elementi multimediali dinamici](https://helpx.adobe.com/experience-manager/kt/assets/using/dynamic-media-image-sharpening-feature-video-use.html)

