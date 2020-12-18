---
title: Aggiunta di risorse Dynamic Media alle pagine
seo-title: Aggiunta di risorse Dynamic Media alle pagine
description: Per aggiungere la funzionalità multimediale dinamica alle risorse utilizzate sui siti web, è possibile aggiungere il Componente Elemento multimediale dinamico o File multimediali interattivi direttamente sulla pagina.
seo-description: Per aggiungere la funzionalità multimediale dinamica alle risorse utilizzate sui siti web, è possibile aggiungere il Componente Elemento multimediale dinamico o File multimediali interattivi direttamente sulla pagina.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 56%

---


# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti Web, potete aggiungere il componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Interactive Media]** direttamente sulla pagina. A tale scopo, è possibile accedere alla modalità [!UICONTROL Progettazione] e attivare i componenti per contenuti multimediali dinamici. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Elemento multimediale dinamico e File multimediali interattivi sono intelligenti: sanno se aggiungi un&#39;immagine o un video e le opzioni disponibili cambiano di conseguenza.

Se utilizzate AEM come WCM, potete aggiungere risorse multimediali dinamiche direttamente alla pagina.

>[!NOTE]
>
>Per i banner a carosello sono disponibili mappe immagine pronte all&#39;uso.

## Aggiunta di un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

L&#39;aggiunta del componente [!UICONTROL Dynamic Media] o [!UICONTROL Interactive Media] a una pagina equivale all&#39;aggiunta di un componente a qualsiasi pagina. I componenti [!UICONTROL Dynamic Media] e [!UICONTROL Interactive Media] sono descritti dettagliatamente nelle sezioni seguenti.

Per aggiungere un componente/visualizzatore elementi multimediali dinamici a una pagina:

1. In AEM, apri la pagina in cui desideri aggiungere il Componente elementi multimediali dinamici.
1. Se non è disponibile alcun componente Dynamic Media, fate clic sul righello nella barra laterale **[!UICONTROL Design]** per passare alla modalità &lt;a2/>Design&lt;a3/>, fate clic su **[!UICONTROL Edit]** parsys, quindi selezionate **[!UICONTROL Dynamic Media]** per rendere disponibili i componenti Dynamic Media.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Configurazione dei componenti in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

1. Tornate alla modalità **[!UICONTROL Modifica]** facendo clic sull&#39;icona matita nella barra laterale [!UICONTROL a3/>.]
1. Trascinate il componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL Interactive Media]** dal gruppo **[!UICONTROL Altro]** nella barra laterale sulla pagina nella posizione desiderata.
1. Fai clic su **[!UICONTROL Modifica]** per aprire il componente.
1. [](#dynamic-media-component)Se necessario, modifica il componente, quindi fai clic su **[!UICONTROL OK]** per salvare le modifiche.

## Componente elementi multimediali dinamici {#dynamic-media-components}

[!UICONTROL Dynamic ] Media e  [!UICONTROL Interactive ] Media sono disponibili in   Sidekickunder  **[!UICONTROL Dynamic Media.]** Puoi utilizzare un componente **[!UICONTROL File multimediali interattivi]** per tutte le risorse interattive, come per esempio video, immagini interattive o inserzioni carosello. Per tutti gli altri componenti dinamici, si consiglia di utilizzare il componente **[!UICONTROL elementi multimediali dinamici]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati nella modalità di progettazione prima dell’uso. [Una volta resi disponibili in modalità Progettazione](/help/sites-authoring/default-components-designmode.md), potrai aggiungere i componenti sulla tua pagina con lo stesso procedimento da usare per qualsiasi altro componente AEM.

### Componente elementi multimediali dinamici {#dynamic-media-component}

Il componente Dynamic Media è avanzato: a seconda se aggiungete un’immagine o un video, sono disponibili diverse opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori basati su HTML5.

>[!NOTE]
>
>Quando aggiungete il componente [!UICONTROL Dynamic Media] e **[!UICONTROL Dynamic Media Settings]** è vuoto oppure non potete aggiungere correttamente una risorsa, verificate quanto segue:
>
>* È stato [abilitato Elemento multimediale dinamico](/help/assets/config-dynamic.md). Dynamic Media è disattivato per impostazione predefinita.
>* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell&#39;attivazione dell’elemento multimediale dinamico non hanno un file TIFF piramidale.

>



#### Quando si lavora con le immagini {#when-working-with-images}

Il componente [!UICONTROL Dynamic Media] consente di aggiungere immagini dinamiche come set di immagini, set 360 gradi e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere un&#39;immagine reattiva è possibile impostare i punti di interruzione o applicare un predefinito immagine reattiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Per modificare le seguenti impostazioni Dynamic Media, fare clic su **[!UICONTROL Modifica]** nel componente, quindi fare clic sulla scheda **[!UICONTROL Dynamic Media Settings]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se si desidera impostare una dimensione fissa, impostare il componente nella scheda **[!UICONTROL Avanzate]** con le proprietà **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]**.

**[!UICONTROL Predefinito]**  visualizzatore - Selezionate un predefinito esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi. Anche i predefiniti per visualizzatori visualizzati sono intelligenti; vengono visualizzati solo i predefiniti per visualizzatori pertinenti.

**[!UICONTROL Predefinito]**  immagine - Selezionate un predefinito per immagini esistente dal menu a discesa. Se il predefinito per immagini che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per immagini](/help/assets/managing-image-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Modificatori]**  immagini - Per modificare gli effetti immagine, sono disponibili ulteriori comandi immagine. Sono descritte in [Gestione dei predefiniti per immagini](/help/assets/managing-viewer-presets.md) e [Riferimento comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Punti di interruzione]** : se utilizzi questa risorsa in un sito reattivo, devi aggiungere i punti di interruzione di pagina. I punti di interruzione immagine devono essere separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

È possibile modificare le seguenti [!UICONTROL Impostazioni avanzate] facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]**  - Consente di modificare il titolo dell’immagine.

**[!UICONTROL Testo]**  Alt: aggiungete un titolo all’immagine per gli utenti che hanno disattivato la grafica.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL URL, Apri in]**  - Puoi impostare una risorsa da cui aprire un collegamento. Impostare l&#39; **[!UICONTROL URL]** e **[!UICONTROL Apri in]** per indicare se si desidera aprirlo nella stessa finestra o in una nuova finestra.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Larghezza e altezza]**  - Immettete il valore in pixel se desiderate che l’immagine sia di dimensione fissa. Lasciando vuoti questi valori, la risorsa viene resa adattiva.

#### Durante l&#39;utilizzo di video {#when-working-with-video}

Utilizzate il componente [!UICONTROL Dynamic Media] per aggiungere video dinamici alle pagine Web. Quando modifichi il componente puoi scegliere di usare un predefinito visualizzatore video predefinita per la riproduzione del video nella pagina.

![chlimage_1-74](assets/chlimage_1-74a.png)

È possibile modificare le seguenti [!UICONTROL Impostazioni Dynamic Media] facendo clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se si desidera impostarne una dimensione fissa, impostarla nel componente con la scheda **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nella scheda **[!UICONTROL Avanzate]**.

**[!UICONTROL Predefinito]**  visualizzatore - Selezionate un predefinito per visualizzatori video esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

Per modificare le seguenti impostazioni [!UICONTROL Avanzate], fare clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]**  - Consente di cambiare il titolo del video.

**[!UICONTROL Larghezza e altezza]**  - Immettete il valore in pixel se desiderate che il video sia di dimensione fissa. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

#### Modalità di distribuzione video sicura {#how-to-delivery-secure-video}

In AEM 6.2, quando installi [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480) è possibile controllare se un video viene distribuito tramite una connessione SSL sicura (HTTPS) o una connessione non sicura (HTTP). Per impostazione predefinita, il protocollo di distribuzione video viene ereditato automaticamente dal protocollo della pagina web in cui è stato incorporato. Se la pagina web viene caricata tramite HTTPS, anche il video viene trasmesso tramite HTTPS. Viceversa, se la pagina web è su HTTP, il video viene trasmesso tramite HTTP. Nella maggior parte dei casi, questo funzionamento predefinito è corretto e non è necessario apportare modifiche alla configurazione. Tuttavia, è possibile scavalcare questa impostazione predefinita aggiungendo `VideoPlayer.ssl=on` alla fine di un percorso URL o all&#39;elenco degli altri parametri di configurazione del visualizzatore da incorporare nello snippet di codice, per forzare la distribuzione video sicura.

Per ulteriori informazioni sulla distribuzione video sicura e su come usare l&#39;attributo di configurazione `VideoPlayer.ssl` nel vostro percorso URL, consultare [Distribuzione video sicura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) nella Guida di riferimento per i visualizzatori. Oltre al visualizzatore per video, la distribuzione sicura dei video è disponibile per i visualizzatori per file multimediali diversi e per i visualizzatori per video interattivi.

### Componente File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente [!UICONTROL Supporto interattivo] è elegante. A seconda che sia stata aggiunta un&#39;immagine o un video, sono disponibili diverse opzioni. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori basati su HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

È possibile modificare le seguenti impostazioni **[!UICONTROL Generali]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Predefinito]**  visualizzatore - Selezionate un predefinito esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

**[!UICONTROL Titolo]**  - Consente di cambiare il titolo del video.

**[!UICONTROL Larghezza e altezza]**  - Immettete il valore in pixel se desiderate che il video sia di dimensione fissa. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Mostra risorsa]**  prodotto - Per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

**[!UICONTROL Mostra prezzo]**  prodotto - Per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

**[!UICONTROL Mostra modulo]**  prodotto - Per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.
