---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi aggiungere il componente Dynamic Media o File multimediali interattivi direttamente sulla pagina.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 52%

---

# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi aggiungere il componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL File multimediali interattivi]** direttamente sulla pagina. A tale scopo, accedi alla modalità [!UICONTROL Progettazione] e attiva i componenti Dynamic Media. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Dynamic Media e per contenuti multimediali interattivi sono intelligenti: sanno se aggiungi un’immagine o un video e le opzioni disponibili cambiano di conseguenza.

Se utilizzi AEM come WCM, puoi aggiungere direttamente alla pagina le risorse Dynamic Media.

>[!NOTE]
>
>Per i banner a carosello sono disponibili mappe immagine pronte all&#39;uso.

## Aggiunta di un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

Aggiungere un componente [!UICONTROL Dynamic Media] o [!UICONTROL File multimediali interattivi] a una pagina equivale ad aggiungere un componente a qualsiasi pagina. I componenti [!UICONTROL Dynamic Media] e [!UICONTROL File multimediali interattivi] sono descritti in dettaglio nelle sezioni seguenti.

Per aggiungere un componente/visualizzatore elementi multimediali dinamici a una pagina:

1. In AEM, apri la pagina in cui desideri aggiungere il Componente elementi multimediali dinamici.
1. Se non è disponibile alcun componente Dynamic Media, fai clic sul righello nella barra laterale [!UICONTROL Sidekick] per accedere alla modalità **[!UICONTROL Progettazione]**, fai clic su **[!UICONTROL Modifica]** parsys, quindi seleziona **[!UICONTROL Dynamic Media]** per rendere disponibili i componenti Dynamic Media.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Configurazione dei componenti in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

1. Torna alla modalità **[!UICONTROL Modifica]** facendo clic sull&#39;icona a forma di matita nella barra laterale [!UICONTROL a sinistra].
1. Trascina il componente **[!UICONTROL Dynamic Media]** o **[!UICONTROL File multimediali interattivi]** dal gruppo **[!UICONTROL Altro]** nella barra laterale sulla pagina nella posizione desiderata.
1. Fai clic su **[!UICONTROL Modifica]** per aprire il componente.
1. [](#dynamic-media-component)Se necessario, modifica il componente, quindi fai clic su **[!UICONTROL OK]** per salvare le modifiche.

## Componente elementi multimediali dinamici {#dynamic-media-components}

[!UICONTROL Dynamic ] Media e  [!UICONTROL Interactive ] Media sono disponibili in   Sidekickunder  **[!UICONTROL Dynamic Media]**. Puoi utilizzare un componente **[!UICONTROL File multimediali interattivi]** per tutte le risorse interattive, come per esempio video, immagini interattive o inserzioni carosello. Per tutti gli altri componenti Dynamic Media, utilizza il componente **[!UICONTROL Dynamic Media]** .

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati nella modalità di progettazione prima dell’uso. [Una volta resi disponibili in modalità Progettazione](/help/sites-authoring/default-components-designmode.md), potrai aggiungere i componenti sulla tua pagina con lo stesso procedimento da usare per qualsiasi altro componente AEM.

### Componente elementi multimediali dinamici {#dynamic-media-component}

Il componente Dynamic Media è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori basati su HTML5.

>[!NOTE]
>
>Quando aggiungi il componente [!UICONTROL Dynamic Media] e **[!UICONTROL Impostazioni Dynamic Media]** è vuoto o non puoi aggiungere correttamente una risorsa, controlla quanto segue:
>
>* È stato [abilitato Elemento multimediale dinamico](/help/assets/config-dynamic.md). Dynamic Media è disattivato per impostazione predefinita.
>* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell’abilitazione di Dynamic Media non dispongono di un file TIFF piramidale.

>



#### Quando si lavora con le immagini {#when-working-with-images}

Il componente [!UICONTROL Dynamic Media] consente di aggiungere immagini dinamiche, compresi set di immagini, set 360 gradi e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere un&#39;immagine reattiva è possibile impostare i punti di interruzione o applicare un predefinito immagine reattiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Per modificare le seguenti impostazioni di Dynamic Media, fai clic su **[!UICONTROL Modifica]** nel componente, quindi fai clic sulla scheda **[!UICONTROL Impostazioni Dynamic Media]** .

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se desideri impostarne una dimensione fissa, impostala nel componente nella scheda **[!UICONTROL Avanzate]** con le proprietà **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** .

**[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi. Anche i predefiniti visualizzatore visualizzati sono intelligenti: vengono visualizzati solo i predefiniti visualizzatore pertinenti.

**[!UICONTROL Preimpostazione immagine]** : seleziona un predefinito immagine esistente dal menu a discesa. Se il predefinito per immagini che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per immagini](/help/assets/managing-image-presets.md). Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Modificatori immagine]** : è possibile modificare gli effetti immagine fornendo ulteriori comandi immagine. Questi sono descritti in [Gestione dei predefiniti immagine](/help/assets/managing-viewer-presets.md) e nel riferimento [Comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Punti di interruzione]** : se utilizzi questa risorsa su un sito reattivo, devi aggiungere i punti di interruzione pagina. I punti di interruzione immagine devono essere separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

Puoi modificare le seguenti [!UICONTROL Impostazioni avanzate] facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]**  - Consente di modificare il titolo dell’immagine.

**[!UICONTROL Testo Alt]**  - Aggiungi un titolo all’immagine per gli utenti che hanno disattivato la grafica.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL URL, Apri in]** : puoi impostare una risorsa da per aprire un collegamento. Impostare l&#39; **[!UICONTROL URL]** e **[!UICONTROL Apri in]** per indicare se si desidera aprire nella stessa finestra o in una nuova finestra.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Larghezza e altezza]** : immetti il valore in pixel se vuoi che l’immagine sia di dimensioni fisse. Lasciando vuoti questi valori, la risorsa viene resa adattiva.

#### Quando si lavora con un video {#when-working-with-video}

Utilizza il componente [!UICONTROL Dynamic Media] per aggiungere video dinamici alle pagine web. Quando modifichi il componente puoi scegliere di usare un predefinito visualizzatore video predefinita per la riproduzione del video nella pagina.

![chlimage_1-74](assets/chlimage_1-74a.png)

Per modificare le seguenti [!UICONTROL Impostazioni Dynamic Media], fai clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se vuoi impostarne una dimensione fissa, impostala nel componente con la scheda **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nella scheda **[!UICONTROL Avanzate]** .

**[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore video esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

È possibile modificare le seguenti impostazioni [!UICONTROL Avanzate] facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]**  - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** : immetti il valore in pixel se vuoi che il video sia di dimensioni fisse. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

#### Modalità di distribuzione video sicura {#how-to-delivery-secure-video}

In AEM 6.2, quando installi [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480) è possibile controllare se un video viene distribuito tramite una connessione SSL sicura (HTTPS) o una connessione non sicura (HTTP). Per impostazione predefinita, il protocollo di distribuzione video viene ereditato automaticamente dal protocollo della pagina web in cui è stato incorporato. Se la pagina web viene caricata tramite HTTPS, anche il video viene trasmesso tramite HTTPS. Viceversa, se la pagina web è su HTTP, il video viene trasmesso tramite HTTP. Nella maggior parte dei casi, questo funzionamento predefinito è corretto e non è necessario apportare modifiche alla configurazione. Tuttavia, è possibile scavalcare questa impostazione predefinita aggiungendo `VideoPlayer.ssl=on` alla fine di un percorso URL o all&#39;elenco degli altri parametri di configurazione del visualizzatore da incorporare nello snippet di codice, per forzare la distribuzione video sicura.

Per ulteriori informazioni sulla distribuzione video sicura e su come usare l&#39;attributo di configurazione `VideoPlayer.ssl` nel vostro percorso URL, consultare [Distribuzione video sicura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) nella Guida di riferimento per i visualizzatori. Oltre al visualizzatore video, la distribuzione video sicura è disponibile per il visualizzatore di file multimediali diversi e per il visualizzatore di video interattivi.

### Componente File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

Il componente [!UICONTROL File multimediali interattivi] è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili diverse opzioni. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono visualizzatori basati su HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

È possibile modificare le seguenti impostazioni **[!UICONTROL Generali]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Predefinito visualizzatore]** : seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Consulta Gestione dei predefiniti per visualizzatori. 

**[!UICONTROL Titolo]**  - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** : immetti il valore in pixel se vuoi che il video sia di dimensioni fisse. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Mostra risorsa prodotto]** : per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

**[!UICONTROL Mostra prezzo]**  prodotto: per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

**[!UICONTROL Mostra modulo prodotto]** : per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.
