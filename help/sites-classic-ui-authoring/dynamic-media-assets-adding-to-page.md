---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi aggiungere il componente Dynamic Media o File multimediali interattivi direttamente sulla pagina.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 32%

---

# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Media alle risorse utilizzate sui siti web, puoi aggiungere la **[!UICONTROL Dynamic Media]** o **[!UICONTROL File multimediali interattivi]** direttamente sulla pagina. Invio **[!UICONTROL Progettazione]** e abilitare i componenti Dynamic Media. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Dynamic Media e per contenuti multimediali interattivi sono intelligenti: sanno se aggiungi un’immagine o un video e le opzioni disponibili cambiano di conseguenza.

Puoi aggiungere risorse Dynamic Media direttamente alla pagina se utilizzi Adobe Experience Manager come WCM.

>[!NOTE]
>
>Per i banner a carosello sono disponibili mappe immagine pronte all&#39;uso.

## Aggiungere un componente Dynamic Media a una pagina {#adding-a-dynamic-media-component-to-a-page}

Aggiunta di [!UICONTROL Dynamic Media] o [!UICONTROL File multimediali interattivi] equivale ad aggiungere un componente a una pagina. La [!UICONTROL Dynamic Media] e [!UICONTROL File multimediali interattivi] I componenti sono descritti in dettaglio nelle sezioni seguenti.

Per aggiungere un componente/visualizzatore elementi multimediali dinamici a una pagina:

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il componente Dynamic Media.
1. Se non è disponibile alcun componente Dynamic Media, seleziona il righello nel [!UICONTROL Barra laterale] per immettere **[!UICONTROL Progettazione]** modalità.
1. Seleziona **[!UICONTROL Modifica]** parsys.
1. Seleziona **[!UICONTROL Dynamic Media]** in modo da rendere disponibili i componenti Dynamic Media.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Configurazione dei componenti in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

1. Torna a **[!UICONTROL Modifica]** facendo clic sull’icona a forma di matita [!UICONTROL Barra laterale].
1. Trascina **[!UICONTROL Dynamic Media]** o **[!UICONTROL File multimediali interattivi]** dal **[!UICONTROL Altro]** nella barra laterale sulla pagina nella posizione desiderata.
1. Seleziona **[!UICONTROL Modifica]** si apre il componente.
1. [Modificare il componente](#dynamic-media-component) se necessario.
1. Seleziona **[!UICONTROL OK]** in modo da salvare le modifiche.

## Componente elementi multimediali dinamici {#dynamic-media-components}

[!UICONTROL Dynamic Media] e [!UICONTROL File multimediali interattivi] sono disponibili in [!UICONTROL Barra laterale] sotto **[!UICONTROL Dynamic Media]**. Puoi utilizzare un componente **[!UICONTROL File multimediali interattivi]** per tutte le risorse interattive, come per esempio video, immagini interattive o inserzioni carosello. Per tutti gli altri componenti di Dynamic Media, utilizza la variabile **[!UICONTROL Dynamic Media]** componente.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati in modalità Progettazione prima dell’utilizzo. [Una volta resi disponibili in modalità Progettazione](/help/sites-authoring/default-components-designmode.md), puoi aggiungere i componenti alla pagina come qualsiasi altro componente di Experience Manager.

### Componente elementi multimediali dinamici {#dynamic-media-component}

Il componente Dynamic Media è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Il componente supporta i predefiniti per immagini e i visualizzatori basati su immagini, come set di immagini, set di rotazione, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono basati su HTML5.

>[!NOTE]
>
>Quando aggiungi la [!UICONTROL Dynamic Media] e **[!UICONTROL Impostazioni Dynamic Media]** è vuoto oppure non è possibile aggiungere correttamente una risorsa, controlla quanto segue:
>
>* È stato [abilitato Elemento multimediale dinamico](/help/assets/config-dynamic.md). Dynamic Media è disattivato per impostazione predefinita.
>* L&#39;immagine è in formato TIFF piramidale. Le immagini importate prima dell’abilitazione di Dynamic Media non dispongono di un file TIFF piramidale.
>


#### Quando si lavora con le immagini {#when-working-with-images}

La [!UICONTROL Dynamic Media] consente di aggiungere immagini dinamiche, compresi set di immagini, set 360 gradi e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi, o selezionare un&#39;immagine da un altro tipo di set.

È possibile anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere un’immagine reattiva, puoi impostare i punti di interruzione o applicare un predefinito per immagini reattive.

![chlimage_1-72](assets/chlimage_1-72a.png)

Per modificare le seguenti impostazioni di Dynamic Media, fai clic su **[!UICONTROL Modifica]** nel componente , quindi fai clic su **[!UICONTROL Impostazioni Dynamic Media]** scheda .

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, impostala nel componente nel **[!UICONTROL Avanzate]** con la scheda **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** proprietà.

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito per visualizzatori esistente dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). Non puoi selezionare un predefinito visualizzatore se utilizzi un predefinito immagine e viceversa.

Questa opzione è disponibile solo se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi. I predefiniti visualizzatore visualizzati sono intelligenti. In altre parole, vengono visualizzati solo i predefiniti visualizzatore pertinenti.

**[!UICONTROL Predefinito immagine]** - Seleziona un predefinito per immagini dal menu a discesa. Se il predefinito immagine che cerchi non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per immagini](/help/assets/managing-image-presets.md). Non puoi selezionare un predefinito visualizzatore se utilizzi un predefinito immagine e viceversa.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Modificatori immagine]** - È possibile modificare gli effetti immagine fornendo ulteriori comandi immagine. Questi comandi sono descritti in [Gestione dei predefiniti per immagini](/help/assets/managing-viewer-presets.md) e [Riferimento comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Punti di interruzione]** - Se utilizzi questa risorsa su un sito reattivo, devi aggiungere i punti di interruzione pagina. I punti di interruzione dell’immagine sono separati da virgole (,). Questa opzione funziona quando non è stata definita alcuna altezza o larghezza in un predefinito immagine.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

È possibile modificare quanto segue [!UICONTROL Impostazioni avanzate] facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]** - Modificare il titolo dell&#39;immagine.

**[!UICONTROL Testo Alt]** - Aggiungi un titolo all’immagine per gli utenti che hanno disattivato la grafica.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL URL, Apri in]** - Puoi impostare una risorsa da per aprire un collegamento. Imposta la **[!UICONTROL URL]** e **[!UICONTROL Apri in]** per indicare se si desidera aprire nella stessa finestra o in una nuova finestra.

Questa è l&#39;unica opzione disponibile se stai visualizzando set di immagini, set di rotazione o set di file multimediali diversi.

**[!UICONTROL Larghezza e altezza]** - Immetti il valore in pixel se vuoi che l&#39;immagine sia di dimensioni fisse. Lasciando vuoti questi valori, la risorsa viene resa adattiva.

#### Quando si lavora con i video {#when-working-with-video}

Utilizza la **[!UICONTROL Dynamic Media]** per aggiungere video dinamici alle pagine web. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video per la riproduzione del video sulla pagina.

![chlimage_1-74](assets/chlimage_1-74a.png)

È possibile modificare quanto segue [!UICONTROL Impostazioni Dynamic Media] facendo clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video elementi multimediali dinamici è adattivo. Se vuoi impostarne una dimensione fissa, impostala nel componente con la **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** in **[!UICONTROL Avanzate]** scheda .

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito per visualizzatori video dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md). 

È possibile modificare quanto segue [!UICONTROL Avanzate] impostazioni facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]** - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** - Immetti il valore in pixel se vuoi che il video sia di dimensioni fisse. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

#### Fornire video sicuri {#how-to-delivery-secure-video}

In Experience Manager 6.2, quando installi [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), puoi controllare se un video viene distribuito tramite una connessione SSL protetta (HTTPS) o una connessione non sicura (HTTP). Per impostazione predefinita, il protocollo di distribuzione video viene ereditato automaticamente dal protocollo della pagina web in cui è stato incorporato. Se la pagina web viene caricata tramite HTTPS, anche il video viene trasmesso tramite HTTPS. Al contrario, se la pagina web è su HTTP, il video viene distribuito via HTTP. Di solito, questo comportamento predefinito va bene e non è necessario apportare modifiche alla configurazione. Tuttavia, puoi ignorare questo comportamento predefinito. Aggiungi `VideoPlayer.ssl=on` alla fine di un percorso URL o all’elenco di altri parametri di configurazione del visualizzatore in uno snippet di codice da incorporare. Entrambe le azioni forzano la distribuzione sicura dei video.

Per ulteriori informazioni sulla distribuzione video sicura e su come usare l&#39;attributo di configurazione `VideoPlayer.ssl` nel vostro percorso URL, consultare [Distribuzione video sicura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) nella Guida di riferimento per i visualizzatori. Oltre al visualizzatore video, la distribuzione video sicura è disponibile per il visualizzatore di file multimediali diversi e per il visualizzatore di video interattivi.

### Componente File multimediali interattivi {#interactive-media-component}

Il Componente File multimediali interattivi è adatto per le risorse che dispongono di interattività, come punti attivi o mappe immagine. Se disponi di un&#39;immagine, un video interattivo o un banner carosello, utilizza il componente **[!UICONTROL File multimediali interattivi]**.

La [!UICONTROL File multimediali interattivi] componente è intelligente : a seconda che aggiunga un’immagine o un video, avrai a disposizione diverse opzioni. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono basati su HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

È possibile modificare le seguenti impostazioni **[!UICONTROL Generali]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito per visualizzatori esistente dal menu a discesa. Se il predefinito per visualizzatori che stai cercando non è visibile, devi renderlo visibile. I predefiniti per visualizzatori devono essere pubblicati prima di poter essere utilizzati. Vedi [Gestire i predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

**[!UICONTROL Titolo]** - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** - Immetti il valore in pixel se vuoi che il video sia di dimensioni fisse. Se questi valori vengono lasciati vuoti, la risorsa sarà adattiva.

È possibile modificare le seguenti impostazioni **[!UICONTROL Aggiungi al carrello]**, facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Mostra risorsa prodotto]** - Per impostazione predefinita, questo valore è selezionato. La risorsa di prodotto mostra un&#39;immagine del prodotto in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare la risorsa di prodotto.

**[!UICONTROL Mostra prezzo prodotto]** - Per impostazione predefinita, questo valore è selezionato. Prezzo del prodotto mostra il prezzo dell&#39;elemento in base a quanto definito nel modulo Commerce. Rimuovi il segno di spunta per non visualizzare il prezzo del prodotto.

**[!UICONTROL Mostra modulo di prodotto]** - Per impostazione predefinita, questo valore non è selezionato. Il Modulo del prodotto include tutte le varianti del prodotto, come la dimensione e il colore. Rimuovi il segno di spunta per non visualizzare le varianti prodotto.
