---
title: Aggiunta di risorse Dynamic Media alle pagine
description: Per aggiungere la funzionalità Dynamic Medie alle risorse utilizzate sui siti web, puoi aggiungere il componente Dynamic Medie o File multimediali interattivi direttamente sulla pagina.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 2%

---

# Aggiunta di risorse Dynamic Media alle pagine{#adding-dynamic-media-assets-to-pages}

Per aggiungere la funzionalità Dynamic Medie alle risorse utilizzate sui siti web, puoi aggiungere **[!UICONTROL Dynamic Medie]** o **[!UICONTROL File multimediali interattivi]** direttamente sulla pagina. Invio **[!UICONTROL Progettazione]** e abilitando i componenti Dynamic Medie. Quindi, potrai aggiungere questi componenti alla pagina e fornire così risorse al componente. I componenti Dynamic Medie e gli elementi multimediali interattivi sono intelligenti: rilevano l’aggiunta di un’immagine o di un video e le opzioni disponibili cambiano di conseguenza.

Se utilizzi Adobe Experience Manager come WCM, puoi aggiungere direttamente alla pagina le risorse Dynamic Medie.

>[!NOTE]
>
>Per i banner a carosello sono disponibili mappe immagine pronte all’uso.

## Aggiungere un componente Dynamic Medie a una pagina {#adding-a-dynamic-media-component-to-a-page}

Aggiunta di [!UICONTROL Dynamic Medie] o [!UICONTROL File multimediali interattivi] per aggiungere un componente a una pagina si intende come aggiungere un componente a una pagina. Il [!UICONTROL Dynamic Medie] e [!UICONTROL File multimediali interattivi] I componenti sono descritti in dettaglio nelle sezioni seguenti.

Per aggiungere un componente/visualizzatore Dynamic Medie a una pagina:

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il componente Dynamic Medie.
1. Se non è disponibile alcun componente di Dynamic Medie, selezionare il righello nella [!UICONTROL Sidekick] per inserire **[!UICONTROL Progettazione]** modalità.
1. Seleziona **[!UICONTROL Modifica]** parsys.
1. Seleziona **[!UICONTROL Dynamic Medie]** in modo da poter rendere disponibili i componenti Dynamic Medie.

   >[!NOTE]
   >
   >Consulta [Configurazione dei componenti in modalità progettazione](/help/sites-authoring/default-components-designmode.md) per ulteriori informazioni.

1. Torna a **[!UICONTROL Modifica]** facendo clic sull’icona della matita nella [!UICONTROL Sidekick].
1. Trascina **[!UICONTROL Dynamic Medie]** o **[!UICONTROL File multimediali interattivi]** componente da **[!UICONTROL Altro]** raggruppa nella barra laterale sulla pagina nella posizione desiderata.
1. Seleziona **[!UICONTROL Modifica]** in questo modo il componente si apre.
1. [Modificare il componente](#dynamic-media-component) secondo necessità.
1. Seleziona **[!UICONTROL OK]** le modifiche vengono salvate.

## Componenti Dynamic Medie {#dynamic-media-components}

[!UICONTROL Dynamic Medie] e [!UICONTROL File multimediali interattivi] sono disponibili in [!UICONTROL Sidekick] in **[!UICONTROL Dynamic Medie]**. Utilizzi il **[!UICONTROL File multimediali interattivi]** componente per qualsiasi risorsa interattiva come video interattivo, immagini interattive o set carosello. Per tutti gli altri componenti di Dynamic Medie, utilizza **[!UICONTROL Dynamic Medie]** componente.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati in modalità Progettazione prima di utilizzare. [Dopo che sono stati resi disponibili in modalità Progettazione](/help/sites-authoring/default-components-designmode.md), puoi aggiungere i componenti alla pagina come faresti con qualsiasi altro componente di Experience Manager.

### Componente Dynamic Medie {#dynamic-media-component}

Il componente Dynamic Medie è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Il componente supporta predefiniti per immagini, visualizzatori basati su immagini come set di immagini, set 360 gradi, set di file multimediali diversi e video. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono basati su HTML5.

>[!NOTE]
>
>Quando si aggiunge [!UICONTROL Dynamic Medie] componente, e **[!UICONTROL Impostazioni Dynamic Medie]** è vuoto oppure non è possibile aggiungere correttamente una risorsa, verifica quanto segue:
>
>* Hai [Dynamic Medie abilitato](/help/assets/config-dynamic.md). Dynamic Medie è disabilitato per impostazione predefinita.
>* L&#39;immagine ha un file tiff piramidale. Le immagini importate prima dell&#39;attivazione di Dynamic Medie non dispongono di un file tiff piramidale.
>

#### Utilizzo delle immagini {#when-working-with-images}

Il [!UICONTROL Dynamic Medie] Questo componente consente di aggiungere immagini dinamiche, inclusi set di immagini, set 360 gradi e set di file multimediali diversi. È possibile ingrandire, ridurre e, se applicabile, ruotare un&#39;immagine all&#39;interno di un set 360 gradi o selezionare un&#39;immagine da un altro tipo di set.

Puoi anche configurare il predefinito visualizzatore, il predefinito immagine o il formato immagine direttamente nel componente. Per rendere reattiva un’immagine, puoi impostare i punti di interruzione o applicare un predefinito per immagine reattiva.

![chlimage_1-72](assets/chlimage_1-72a.png)

Puoi modificare le seguenti impostazioni di Dynamic Medie facendo clic su **[!UICONTROL Modifica]** nel componente, quindi facendo clic su **[!UICONTROL Impostazioni Dynamic Medie]** scheda.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Per impostazione predefinita, il componente immagine Dynamic Media è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nel componente in **[!UICONTROL Avanzate]** scheda con **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** proprietà.

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per i visualizzatori](/help/assets/managing-viewer-presets.md). Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

Questa opzione è disponibile solo se vengono visualizzati set di immagini, set 360 gradi o set di file multimediali diversi. I predefiniti visualizzatore visualizzati sono intelligenti. In altre parole, vengono visualizzati solo i predefiniti visualizzatore rilevanti.

**[!UICONTROL Predefinito immagine]** : seleziona un predefinito immagine esistente dal menu a discesa. Se il predefinito immagine che state cercando non è visibile, dovete renderlo visibile. Consulta [Gestione dei predefiniti per le immagini](/help/assets/managing-image-presets.md). Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

Questa opzione non è disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi.

**[!UICONTROL Modificatori immagine]** - È possibile modificare gli effetti immagine mediante comandi immagine aggiuntivi. Questi comandi sono descritti in [Gestione dei predefiniti per le immagini](/help/assets/managing-viewer-presets.md) e [Riferimento comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Questa opzione non è disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi.

**[!UICONTROL Punti di interruzione]** - Se utilizzi questa risorsa su un sito reattivo, devi aggiungere i punti di interruzione di pagina. I punti di interruzione delle immagini sono separati da virgole (,). Questa opzione funziona quando in un predefinito immagine non è definita alcuna altezza o larghezza.

Questa opzione non è disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi.

È possibile modificare quanto segue [!UICONTROL Impostazioni avanzate] facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]** - Modifica il titolo dell&#39;immagine.

**[!UICONTROL Testo alternativo]** : aggiungi un titolo all&#39;immagine per gli utenti che hanno la grafica disattivata.

Questa opzione non è disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi.

**[!UICONTROL URL, Apri in]** - È possibile impostare una risorsa da per aprire un collegamento. Imposta il **[!UICONTROL URL]** e **[!UICONTROL Apri in]** per indicare se si desidera aprirlo nella stessa finestra o in una nuova finestra.

Questa opzione non è disponibile se visualizzi set di immagini, set 360 gradi o set di file multimediali diversi.

**[!UICONTROL Larghezza e altezza]** - Immettete il valore in pixel se desiderate che l&#39;immagine abbia una dimensione fissa. Se si omettono questi valori, la risorsa diventa adattiva.

#### Quando si lavora con il video {#when-working-with-video}

Utilizza il **[!UICONTROL Dynamic Medie]** per aggiungere video dinamici alle pagine web. Quando modifichi il componente, puoi scegliere di utilizzare un predefinito visualizzatore video predefinito per riprodurre il video sulla pagina.

![chlimage_1-74](assets/chlimage_1-74a.png)

È possibile modificare quanto segue [!UICONTROL Impostazioni Dynamic Medie] facendo clic su **[!UICONTROL Modifica]** nel componente.

>[!NOTE]
>
>Per impostazione predefinita, il componente video Dynamic Medie è adattivo. Se vuoi impostarne una dimensione fissa, lo puoi fare nel componente con **[!UICONTROL Larghezza]** e **[!UICONTROL Altezza]** nel **[!UICONTROL Avanzate]** scheda.

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore video esistente dal menu a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestione dei predefiniti per i visualizzatori](/help/assets/managing-viewer-presets.md).

È possibile modificare quanto segue [!UICONTROL Avanzate] impostazioni facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Titolo]** - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** - Immetti il valore in pixel se vuoi che il video abbia una dimensione fissa. Se si omettono questi valori, la variabile diventa adattiva.

#### Distribuire video sicuri {#how-to-delivery-secure-video}

All&#39;Experience Manager 6.2, quando si installa [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), è possibile controllare se un video viene distribuito tramite una connessione SSL protetta (HTTPS) o una connessione non sicura (HTTP). Per impostazione predefinita, il protocollo di consegna video viene ereditato automaticamente dal protocollo della pagina web in cui è incorporato. Se la pagina web viene caricata su HTTPS, anche il video viene distribuito su HTTPS. Al contrario, se la pagina web è su HTTP, il video viene distribuito su HTTP. In genere, questo comportamento predefinito va bene e non è necessario apportare modifiche alla configurazione. Tuttavia, puoi ignorare questo comportamento predefinito. Aggiungi `VideoPlayer.ssl=on` alla fine di un percorso URL o all’elenco di altri parametri di configurazione del visualizzatore in uno snippet di codice da incorporare. Entrambe le azioni impongono la distribuzione sicura dei video.

Per ulteriori informazioni sulla distribuzione sicura dei video e sull’utilizzo di `VideoPlayer.ssl` dell&#39;attributo di configurazione nel percorso URL, vedi [Consegna video sicura](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) nella Guida di riferimento dei visualizzatori. Oltre al visualizzatore video, per il visualizzatore di file multimediali diversi e per il visualizzatore di video interattivi è disponibile una distribuzione video protetta.

### Componente per contenuti multimediali interattivi {#interactive-media-component}

Il componente Contenuti multimediali interattivi è destinato alle risorse che presentano interattività, come punti attivi o mappe immagine. Se hai un&#39;immagine interattiva, un video interattivo o un banner a carosello, utilizza **[!UICONTROL File multimediali interattivi]** componente.

Il [!UICONTROL File multimediali interattivi] Il componente è intelligente: a seconda che si aggiunga un’immagine o un video, sono disponibili varie opzioni. Inoltre, il visualizzatore è reattivo. In altre parole, le dimensioni dello schermo cambiano automaticamente in base alle dimensioni dello schermo. Tutti i visualizzatori sono basati su HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

È possibile modificare quanto segue **[!UICONTROL Generale]** impostazioni facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. I predefiniti visualizzatore devono essere pubblicati prima di poter essere utilizzati. Consulta [Gestione predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

**[!UICONTROL Titolo]** - Modifica il titolo del video.

**[!UICONTROL Larghezza e altezza]** - Immetti il valore in pixel se vuoi che il video abbia una dimensione fissa. Se si omettono questi valori, la variabile diventa adattiva.

È possibile modificare quanto segue **[!UICONTROL Aggiungi al carrello]** impostazioni facendo clic su **[!UICONTROL Modifica]** nel componente.

**[!UICONTROL Mostra risorsa prodotto]** - Per impostazione predefinita, questo valore è selezionato. La risorsa prodotto mostra un’immagine del prodotto come definito nel modulo Commerce. Per non visualizzare la risorsa del prodotto, deseleziona questa opzione.

**[!UICONTROL Mostra prezzo prodotto]** - Per impostazione predefinita, questo valore è selezionato. Nel campo Prezzo prodotto viene visualizzato il prezzo dell’articolo definito nel modulo Commerce. Deselezionare il segno di spunta per non visualizzare il prezzo del prodotto.

**[!UICONTROL Mostra modulo prodotto]** - Per impostazione predefinita, questo valore non è selezionato. Il Modulo prodotto include qualsiasi variante di prodotto, ad esempio dimensioni e colore. Deseleziona il segno di spunta per non mostrare le varianti prodotto.
