---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Come aggiungere componenti Dynamic Media a una pagina in Adobe Experience Manager
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
role: Business Practitioner, Administrator
exl-id: 62d4a38c-2873-4560-8d58-ad172288764d
feature: Componenti,Pubblicazione
source-git-commit: 8199702fe778f11cc2a953979a4ccfdcef3f1154
workflow-type: tm+mt
source-wordcount: '3210'
ht-degree: 22%

---

# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi inserire direttamente nella pagina il componente **Dynamic Media**, **File multimediali interattivi**, **Elemento multimediale panoramico** o **File multimediali video 360**. Per aggiungere i componenti, entra in modalità Layout e abilita i componenti Dynamic Media. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Dynamic Media sono intelligenti: rilevano l’aggiunta di un’immagine o di un video, dunque le opzioni di configurazione disponibili cambiano di conseguenza.

Puoi aggiungere risorse Dynamic Media direttamente alla pagina se utilizzi Adobe Experience Manager come WCM. Se utilizzi una terza parte per WCM, puoi [collegare](/help/assets/linking-urls-to-yourwebapplication.md) o [incorporare](/help/assets/embed-code.md) le risorse. Per un sito web dinamico di terze parti, consulta la sezione [Distribuzione di immagini ottimizzate in un sito dinamico](/help/assets/responsive-site.md).

>[!NOTE]
>
>Accertati di pubblicare le risorse prima di aggiungerle alle pagine di Experience Manager. Consulta [Pubblicazione di risorse Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Aggiunta di un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

L’aggiunta a una pagina di un componente Media 3D, Dynamic Media, File multimediali interattivi, File multimediali panoramici, Video Ritaglio avanzato o File multimediali video 360 equivale all’aggiunta di un componente a qualsiasi pagina. I componenti Dynamic Media sono descritti nelle sezioni seguenti.

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il componente Dynamic Media.
1. Nel pannello a sinistra della pagina (se necessario, attiva la visualizzazione del pannello laterale), fai clic sull’icona **[!UICONTROL Componenti]** .
1. Nell&#39;elenco a discesa dell&#39;intestazione **[!UICONTROL Componenti]**, selezionare **[!UICONTROL Dynamic Media.]**

   Se non è disponibile alcun elenco di componenti Dynamic Media, è necessario abilitare i componenti Dynamic Media che si desidera utilizzare. Consulta [Abilitazione dei componenti Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](/help/assets/assets/6_5_360video_wcmcomponent.png)

1. Trascina un componente **[!UICONTROL Dynamic Media]** da utilizzare e rilascialo nella posizione desiderata sulla pagina.

1. Passa il puntatore del mouse direttamente sul componente. Quando un componente è circondato da una casella blu, tocca una volta per visualizzare la barra degli strumenti del componente. Tocca l’icona **[!UICONTROL Configurazione (chiave inglese)]** .

   ![6_5_360video_wcmcomponentconfigure](/help/assets/assets/6_5_360video_wcmcomponentconfigure.png)

1. A seconda del componente Dynamic Media rilasciato sulla pagina, viene visualizzata una finestra di dialogo di configurazione. [Imposta le ](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) opzioni del componente come necessario.

   L&#39;esempio seguente mostra la finestra di dialogo del componente Dynamic Media **[!UICONTROL Video 360 Media]** e le opzioni disponibili nell&#39;elenco a discesa Predefinito visualizzatore .

   ![Componente Video 360 Media](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Componente Dynamic Media Video 360 Media.

1. Al termine, nell’angolo superiore destro della finestra di dialogo, tocca il segno di spunta per salvare le modifiche.

### Abilitazione dei componenti Dynamic Media {#enabling-dynamic-media-components}

Se non è disponibile alcun componente Dynamic Media da aggiungere a una pagina, è probabile che sia necessario prima abilitare i componenti da utilizzare.

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il componente Dynamic Media.
1. Sul lato sinistro della barra degli strumenti vicino alla parte superiore della pagina, tocca l’icona Informazioni pagina , quindi tocca **[!UICONTROL Modifica modello]** dall’elenco a discesa.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. Sul lato destro della barra degli strumenti vicino alla parte superiore della pagina, dall’elenco a discesa tocca **[!UICONTROL Struttura.]**

   ![Criterio](/help/assets/assets-dm/structure-mode.png)

1. Nella parte inferiore della pagina, tocca **[!UICONTROL Contenitore di layout]** per aprire la relativa barra degli strumenti, quindi tocca l’icona Criterio .
1. Nella pagina **[!UICONTROL Contenitore di layout]**, sotto l’intestazione **[!UICONTROL Proprietà]** , accertati che sia selezionata la scheda **[!UICONTROL Componenti consentiti]** .

   ![Componenti consentiti](/help/assets/assets-dm/allowed-components.png)

1. Scorri fino a visualizzare **[!UICONTROL Dynamic Media.]**
1. Tocca l’icona > a sinistra di **[!UICONTROL Dynamic Media]** per espandere l’elenco, quindi seleziona i componenti Dynamic Media che desideri abilitare.

   ![Elenco dei componenti di Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Contenitore di layout]**, tocca l’icona Fine (segno di spunta).

1. Sul lato destro della barra degli strumenti vicino alla parte superiore della pagina, dall’elenco a discesa tocca **[!UICONTROL Contenuto iniziale]**, quindi [aggiungi un componente Dynamic Media a una pagina](#adding-a-dynamic-media-component-to-a-page) come di consueto.

## Localizzazione dei componenti Dynamic Media {#localizing-dynamic-media-components}

Puoi localizzare i componenti Dynamic Media in uno dei due modi seguenti:

* In una pagina web di Sites, apri **[!UICONTROL Proprietà]** e seleziona la scheda **[!UICONTROL Avanzate]**. Scegli la lingua desiderata per la localizzazione.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Dal selettore del sito, seleziona la pagina o il gruppo di pagine desiderato. Tocca **[!UICONTROL Proprietà]** e seleziona la scheda **[!UICONTROL Avanzate]** . Scegli la lingua desiderata per la localizzazione.

   >[!NOTE]
   >
   >Al momento non tutte le lingue disponibili nel menu **[!UICONTROL Lingua]** dispongono di token assegnati.

## Componente elementi multimediali dinamici {#dynamic-media-components}

I componenti Dynamic Media sono disponibili quando tocchi l&#39;icona **[!UICONTROL Componenti]** , quindi filtra su **[!UICONTROL Dynamic Media.]**

I componenti Dynamic Media disponibili includono:

* **[!UICONTROL Dynamic Media]**: da utilizzare per risorse quali immagini, video, eCatalog e set 360 gradi.
* **[!UICONTROL File multimediali interattivi]** : da utilizzare per qualsiasi risorsa interattiva, ad esempio video interattivi, immagini interattive o set carosello.
* **[!UICONTROL Supporti panoramici]** : da utilizzare per immagini panoramiche o per immagini VR panoramiche.
* **[!UICONTROL Video 360 Media]** : da utilizzare per 360 video e 360 video VR.

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita; devono essere resi disponibili tramite l’editor modelli prima di utilizzarli. [Una volta resi disponibili ](/help/sites-authoring/templates.md#editing-templates-template-authors)nell’editor modelli, puoi aggiungere i componenti alla pagina come faresti con qualsiasi altro componente di Experience Manager.

![6_5_dynamic_mediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente elementi multimediali dinamici {#dynamic-media-component}

Il componente Dynamic Media è intelligente. A seconda che si aggiunga un’immagine o un video, sono disponibili diverse opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina web ha i seguenti elementi:
>
>* istanze multiple del componente Dynamic Media in uso sulla stessa pagina.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito visualizzatore diverso a ciascun componente Dynamic Media in quella pagina non è supportata.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti di Dynamic Media che utilizzano risorse dello stesso tipo, all’interno della pagina.

Quando aggiungi il Componente elementi multimediali dinamici e le **[!UICONTROL Impostazioni elemento multimediale dinamico]** sono vuote o non è possibile aggiungere correttamente una risorsa, controlla quanto segue:

* È stato [abilitato Elemento multimediale dinamico](/help/assets/config-dynamic.md). Dynamic Media è disattivato per impostazione predefinita.
* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima di abilitare Dynamic Media non dispongono di un file TIFF piramidale.

#### Quando si lavora con le immagini {#when-working-with-images}

Il componente elementi multimediali dinamici consente di aggiungere immagini dinamiche, compresi set di immagini, set di rotazione e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere un’immagine reattiva, puoi impostare i punti di interruzione o applicare un predefinito per immagini reattive.

Modifica le seguenti impostazioni Dynamic Media toccando l&#39;icona **[!UICONTROL Modifica]** nel componente e quindi **[!UICONTROL Impostazioni Dynamic Media.]**

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza.]**

* **[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). Non puoi selezionare un predefinito visualizzatore se utilizzi un predefinito immagine e viceversa.

   Questa opzione è l’unica disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi. I predefiniti visualizzatore visualizzati sono intelligenti: vengono visualizzati solo i predefiniti visualizzatore pertinenti.

* **[!UICONTROL Modificatori visualizzatore]** : i modificatori visualizzatore assumono la forma di coppia nome=valore con un delimitatore &amp; e consentono di modificare i visualizzatori come descritto nella Guida di riferimento visualizzatori. Un esempio di modificatore visualizzatore è `posterimage=img.jpg&caption=text.vtt,1` che imposta un’immagine diversa per la miniatura del video e associa un file di sottotitoli/sottotitoli codificati al video.

* **[!UICONTROL Preimpostazione immagine]** : seleziona un predefinito immagine esistente dal menu a discesa. Se il predefinito immagine che cerchi non è visibile, devi renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non puoi selezionare un predefinito visualizzatore se utilizzi un predefinito immagine e viceversa.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Modificatori immagine]**  - È possibile applicare effetti immagine fornendo ulteriori comandi immagine. Questi effetti sono descritti in Predefiniti immagini e nella documentazione di riferimento Image Serving Command.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Punti di interruzione]** : se utilizzi questa risorsa su un sito reattivo, devi aggiungere i punti di interruzione immagine. I punti di interruzione dell’immagine sono separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Per modificare le seguenti Impostazioni avanzate, tocca **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Ottimizza per dispositivi]**  a risoluzione più elevata: seleziona (impostazione predefinita) la casella di controllo per consentire l’ottimizzazione DPR (Device Pixel Ratio).

   L&#39;opzione **[!UICONTROL Ottimizza per dispositivi a risoluzione più elevata]** viene visualizzata solo quando è vero quanto segue:
   * In Tipo predefinito, è selezionato **[!UICONTROL Predefinito immagine]** e **[!UICONTROL RESS_IP]** viene selezionato dall&#39;elenco a discesa **[!UICONTROL Predefinito immagine]**.

   ![impostazione del rapporto pixel del dispositivo per il predefinito immagine](/help/assets/assets-dm/dpr-ress-ip.png)

<!--   See also [About device pixel ratio optimization](/help/assets/imaging-faq.md#dpr).

  Note that any Adobe Experience Manager Dynamic Media Smart Imaging DPR values are ignored. -->

* **[!UICONTROL Titolo]**  - Consente di modificare il titolo dell’immagine.

* **[!UICONTROL Testo Alt]**  - Aggiungi un titolo all’immagine per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** : puoi impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** : immetti il valore in pixel se vuoi che l’immagine sia a dimensione fissa. Lasciando vuoto questo valore, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** : immetti il valore in pixel se vuoi che l’immagine sia di dimensioni fisse. Lasciando vuoto questo valore, la risorsa diventa adattiva.


#### Quando esegui operazioni con i Video {#when-working-with-video}

Utilizza il componente Dynamic Media per aggiungere video dinamici alle pagine web. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video per la riproduzione del video sulla pagina.

![chlimage_1-173](assets/chlimage_1-540.png)

Modifica le seguenti impostazioni Dynamic Media facendo clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se vuoi impostarne una dimensione fissa, impostala nel componente con la scheda **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nella scheda **[!UICONTROL Avanzate]** .

* **[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore video esistente dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

* **[!UICONTROL Modificatori visualizzatore]** : i modificatori visualizzatore assumono la forma di coppia nome=valore con un delimitatore &amp; e consentono di modificare i visualizzatori come descritto nella Guida di riferimento visualizzatori di Adobe. Un esempio di modificatore visualizzatore è `posterimage=img.jpg&caption=text.vtt,1`

   Con i modificatori visualizzatore, ad esempio, puoi effettuare le seguenti operazioni:

   * Associare un file di didascalia a un video: [didascalia][https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associare un file di navigazione a un video: [navigazione][https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Puoi modificare le seguenti Impostazioni avanzate facendo clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Titolo]**  - Modifica il titolo del video.

* **[!UICONTROL Larghezza]** : immetti il valore in pixel se vuoi che l’immagine sia a dimensione fissa. Lasciando vuoto questo valore, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** : immetti il valore in pixel se vuoi che l’immagine sia di dimensioni fisse. Lasciando vuoto questo valore, la risorsa diventa adattiva.

#### Quando si lavora con Smart Crop {#when-working-with-smart-crop}

Utilizza il componente Dynamic Media per aggiungere le risorse immagine ritaglio avanzato alle pagine web. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video per la riproduzione del video sulla pagina.

Vedere anche [Profili immagine](/help/assets/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

Modifica la seguente impostazione Dynamic Media facendo clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nella scheda **[!UICONTROL Avanzate]** del componente, alle voci **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza.]**

* **[!UICONTROL Modificatori immagine]**  - È possibile applicare effetti immagine fornendo ulteriori comandi immagine. Questi effetti sono descritti in Predefiniti immagini e nella documentazione di riferimento Image Serving Command.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

   Puoi modificare le seguenti Impostazioni avanzate facendo clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Abilita corrispondenza proporzioni]** : per consentire a Dynamic Media di scegliere un rendering di ritaglio avanzato con proporzioni che corrispondano al meglio alle proporzioni dell&#39;immagine originale, seleziona questa opzione.

* **[!UICONTROL Ottimizza per dispositivi]**  a risoluzione più elevata: seleziona (impostazione predefinita) la casella di controllo per consentire l’ottimizzazione DPR (Device Pixel Ratio).

   L&#39;opzione **[!UICONTROL Ottimizza per dispositivi a risoluzione più elevata]** viene visualizzata solo quando è vero quanto segue:

   * In Tipo predefinito, è selezionata l’opzione **[!UICONTROL Ritaglio avanzato]** .

   ![impostazione del rapporto pixel del dispositivo per il ritaglio avanzato](/help/assets/assets-dm/dpr-smartcrop.png)

<!--   See also [About device pixel ratio optimization](/help/assets/imaging-faq.md#dpr).

  Note that any Adobe Experience Manager Dynamic Media Smart Imaging DPR values are ignored. -->

* **[!UICONTROL Titolo]**  - Modifica il titolo dell’immagine Ritaglio avanzato.

* **[!UICONTROL Testo Alt]**  - Aggiungi un titolo all’immagine di ritaglio avanzato per gli utenti che hanno disattivato la grafica.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL URL, Apri in]** : puoi impostare una risorsa per aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

   Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

* **[!UICONTROL Larghezza]** : immetti il valore in pixel se vuoi che l’immagine sia a dimensione fissa. Lasciando vuoto questo valore, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** : immetti il valore in pixel se vuoi che l’immagine sia di dimensioni fisse. Lasciando vuoto questo valore, la risorsa diventa adattiva.

### Componente File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente File multimediali interattivi è intelligente. Sia che si aggiunga un&#39;immagine o un video, sono disponibili varie opzioni. Inoltre, il visualizzatore è reattivo: le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori HTML5.

>[!NOTE]
>
>Se la pagina web ha i seguenti elementi:
>
>* Nella stessa pagina vengono utilizzate più istanze del componente File multimediali interattivi.
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito visualizzatore diverso a ciascun componente File multimediali interattivi in quella pagina non è supportata.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti File multimediali interattivi che utilizzano risorse dello stesso tipo, all’interno della pagina.

![chlimage_1-174](assets/chlimage_1-541.png)

Per modificare le seguenti impostazioni **[!UICONTROL Generale]**, tocca **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

* **[!UICONTROL Titolo]**  - Modifica il titolo del video.

* **[!UICONTROL Larghezza]** : immetti il valore in pixel se vuoi che l’immagine sia a dimensione fissa. Lasciando vuoto questo valore, la risorsa diventa adattiva.

* **[!UICONTROL Altezza]** : immetti il valore in pixel se vuoi che l’immagine sia di dimensioni fisse. Lasciando vuoto questo valore, la risorsa diventa adattiva.

   È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

* **[!UICONTROL Mostra risorsa prodotto]** : per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

* **[!UICONTROL Mostra prezzo]**  prodotto: per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

* **[!UICONTROL Mostra modulo prodotto]** : per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.

### Componente elementi multimediali panoramici {#panoramic-media-component}

Il componente Elemento multimediale panoramico è per le risorse che sono immagini panoramiche sferiche. Tali immagini offrono un&#39;esperienza di visualizzazione a 360° di una stanza, proprietà, posizione o paesaggio. Affinché un&#39;immagine si qualifichi come panorama sferico, deve avere uno O entrambi i seguenti elementi:

* Rapporto di formato 2:1.
* Tag con le parole chiave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Consulta [Uso dei tag](/help/sites-authoring/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dettagli risorsa e al componente WCM per **[!UICONTROL elementi multimediali panoramici]**.

>[!NOTE]
>
>Se la pagina web ha i seguenti elementi:
>
>* Nella stessa pagina vengono utilizzate più istanze del componente **[!UICONTROL Elemento multimediale panoramico]** .
>* Ogni istanza utilizza lo stesso tipo di risorsa.

>
>
L’assegnazione di un predefinito visualizzatore diverso a ciascun componente **[!UICONTROL Elemento multimediale panoramico]** in quella pagina non è supportata.
>
>Tuttavia, puoi utilizzare lo stesso predefinito visualizzatore per tutti i componenti Elemento multimediale panoramico che utilizzano risorse dello stesso tipo, all’interno della pagina.

![panoramico-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Per modificare l’impostazione seguente, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** : seleziona un visualizzatore esistente dal menu a discesa Predefinito visualizzatore .

Se il predefinito per visualizzatori che stai cercando non è visibile, assicurati che sia pubblicato. Pubblica i predefiniti visualizzatore prima di utilizzarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

### Componente video 360 Media {#video-media-component}

Utilizza il componente **[!UICONTROL Video 360 Media]** per eseguire il rendering di video equirettangolari sulla pagina web per un&#39;esperienza di visualizzazione immersiva di una stanza, una proprietà, una posizione, un paesaggio o una procedura medica.

Durante la riproduzione su un display piatto, l&#39;utente ha il controllo dell&#39;angolo di visione; la riproduzione su dispositivi mobili utilizza solitamente i controlli giroscopici incorporati.

Il visualizzatore include il supporto nativo per la distribuzione di 360 risorse video. Per impostazione predefinita, non è necessaria alcuna configurazione aggiuntiva per la visualizzazione o la riproduzione. È possibile distribuire video 360 utilizzando estensioni video standard come .mp4, .mkv e .mov. Il codec più comune è H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Per modificare l’impostazione seguente, tocca **[!UICONTROL Configura]** nel componente.

* **[!UICONTROL Predefinito visualizzatore]** : seleziona un visualizzatore esistente dal menu a discesa Predefinito visualizzatore . Usa Video360VR per gli utenti finali che usano occhiali di realtà virtuale. Include controlli di base sulla riproduzione video e funzioni per social media. Utilizza Video360_social che include controlli di riproduzione video di base. Il rendering video viene eseguito in modalità stereo. Il controllo manuale del punto di vista è disattivato ma il controllo giroscopico è attivato. Non esistono funzioni per social media.

Se il predefinito per visualizzatori che stai cercando non è visibile, assicurati che sia pubblicato. Assicurati di pubblicare i predefiniti visualizzatore prima di utilizzarli. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

### Utilizzo di HTTP/2 per la distribuzione delle risorse Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui i browser e i server comunicano. Fornisce un trasferimento più rapido delle informazioni e riduce la quantità di potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media può ora avvenire tramite HTTP/2, garantendo tempi di risposta e caricamento migliori.

Per informazioni dettagliate su come iniziare a utilizzare HTTP/2 con il tuo account Dynamic Media, consulta [Distribuzione di contenuti HTTP2](/help/assets/http2.md) .

>[!MORELIKETHIS]
>
>* [Utilizzo del lettore video in Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [Utilizzo di video interattivi con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [Informazioni sul Visualizzatore risorse con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [Utilizzo di miniature video personalizzate con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Informazioni sulla gestione del colore con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [Utilizzo della nitidezza delle immagini con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

