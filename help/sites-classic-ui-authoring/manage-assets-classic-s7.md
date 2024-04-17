---
title: Aggiungere funzioni di Dynamic Media Classic (Scene7) alla pagina
description: Adobe Dynamic Media Classic (Scene7) è una soluzione in hosting per la gestione, l'ottimizzazione, la pubblicazione e la distribuzione di risorse rich media per web, dispositivi mobili, e-mail, display e stampa connessi a Internet.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 1%

---

# Aggiungere funzioni di Dynamic Media Classic (Scene7) alla pagina{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) è una soluzione in hosting per la gestione, l&#39;ottimizzazione, la pubblicazione e la distribuzione di risorse rich media per web, dispositivi mobili, e-mail, display e stampa connessi a Internet.

Puoi visualizzare le risorse Experienci Manager pubblicate in Dynamic Media Classic (Scene7) in vari visualizzatori:

* Zoom
* A comparsa
* Video
* Modello immagini
* Immagine

Puoi pubblicare le risorse digitali direttamente da Experience Manager a Dynamic Media Classic (Scene7) e le risorse digitali da Dynamic Media Classic (Scene7) a Experience Manager.

Questo documento descrive come pubblicare risorse digitali da Experience Manager a Dynamic Media Classic (Scene7) e viceversa. Vengono descritti in dettaglio anche i visualizzatori. Per informazioni sulla configurazione di Experience Manager per Dynamic Media Classic (Scene7), consulta [Integrazione di Dynamic Media Classic (Scene7) con Experience Manager](/help/sites-administering/scene7.md).

Vedi anche [Aggiungi mappe immagine](/help/assets/image-maps.md).

Per ulteriori informazioni sull’utilizzo dei componenti video con Experience Manager, consulta:

* [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Se le risorse Dynamic Media Classic (Scene7) non vengono visualizzate correttamente, assicurati che Dynamic Medie sia [disabilitato](/help/assets/config-dynamic.md#disabling-dynamic-media) e quindi aggiorna la pagina.

## Pubblicazione manuale in Dynamic Media Classic (Scene7) da Assets {#manually-publishing-to-scene-from-assets}

Puoi pubblicare le risorse digitali su Dynamic Media Classic (Scene7) dalla console Assets nell’interfaccia utente classica o direttamente dalla risorsa.

>[!NOTE]
>
>Experience Manager pubblica in Dynamic Media Classic (Scene7) in modo asincrono. Dopo aver selezionato **[!UICONTROL Pubblica]**, la pubblicazione della risorsa in Dynamic Media Classic (Scene7) potrebbe richiedere alcuni secondi.
>

### Pubblicazione dalla console Assets {#publishing-from-the-assets-console}

Se le risorse si trovano in una cartella di destinazione di Dynamic Media Classic (Scene7), puoi pubblicarle in Dynamic Media Classic (Scene7) dalla console Assets.

1. Nell’interfaccia utente classica di Experience Manager, seleziona **[!UICONTROL Risorse digitali]** per accedere a digital asset manager.

1. Seleziona la risorsa o la cartella all’interno della cartella di destinazione da pubblicare su Dynamic Media Classic (Scene7), fai clic con il pulsante destro del mouse e seleziona (Copia negli Appunti) **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]**. In alternativa, è possibile selezionare **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]** dal **[!UICONTROL Strumenti]** menu.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Vai a Dynamic Media Classic (Scene7) e verifica che le risorse siano disponibili.

   >[!NOTE]
   >
   >Se le risorse non si trovano in una cartella sincronizzata di Dynamic Media Classic (Scene7), **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]** in entrambi i menu è visibile ma disabilitato.

### Pubblicare da una risorsa {#publishing-from-an-asset}

Puoi pubblicare manualmente una risorsa, purché si trovi all’interno della cartella sincronizzata di Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Se la risorsa non si trova nella cartella sincronizzata di Dynamic Media Classic (Scene7), il collegamento a **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]** non viene visualizzato.

Per pubblicare su Dynamic Media Classic (Scene7) direttamente da una risorsa digitale:

1. Ad Experience Manager, seleziona **[!UICONTROL Risorse digitali]** per accedere a digital asset manager.

1. Fai doppio clic per aprire una risorsa.

1. Nel riquadro dei dettagli della risorsa, seleziona **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. Il collegamento diventa **[!UICONTROL Pubblicazione...]** e poi **[!UICONTROL Pubblicato]**. Vai a Dynamic Media Classic (Scene7) e verifica che la risorsa sia disponibile.

   >[!NOTE]
   >
   >Se la risorsa non viene pubblicata correttamente in Dynamic Media Classic (Scene7), il collegamento diventa **[!UICONTROL Pubblicazione non riuscita]**. Se la risorsa è già stata pubblicata su Dynamic Media Classic (Scene7), il collegamento riporta **[!UICONTROL Pubblica di nuovo in Dynamic Media Classic (Scene7)]**. La ripubblicazione consente di modificare le risorse in Experience Manager e ripubblicarle.

### Pubblicare risorse dall’esterno della cartella di destinazione CQ {#publishing-assets-from-outside-the-cq-target-folder}

L’Adobe consiglia di pubblicare le risorse in Dynamic Media Classic (Scene7) solo dalle risorse presenti nella cartella di destinazione di Dynamic Media Classic (Scene7). Tuttavia, se devi caricare delle risorse da una cartella esterna a quella di destinazione, puoi comunque farlo caricandole in una cartella on-demand su Dynamic Media Classic (Scene7). Innanzitutto, configura la configurazione Cloud per la pagina in cui desideri visualizzare la risorsa. Quindi aggiungi un componente Dynamic Media Classic (Scene7) alla pagina e trascina e rilascia una risorsa sul componente. Dopo aver impostato le proprietà della pagina, viene visualizzata una **[!UICONTROL Pubblica su Dynamic Media Classic (Scene7)]** quando viene selezionato, questo collegamento attiva il caricamento in Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Le risorse presenti nella cartella on-demand non vengono visualizzate nel browser contenuti di Dynamic Media Classic (Scene7).

**Per pubblicare le risorse dall’esterno della cartella di destinazione CQ:**

1. Nell’Experience Manager dell’interfaccia classica, seleziona **[!UICONTROL Siti Web]** e accedi alla pagina web a cui desideri aggiungere una risorsa digitale non ancora pubblicata in Dynamic Media Classic (Scene7). (Si applicano le normali regole di ereditarietà delle pagine).

1. Nella barra laterale, seleziona la **[!UICONTROL Pagina]** e seleziona **[!UICONTROL Proprietà pagina]**.

1. Seleziona **[!UICONTROL Cloud Service]**.
1. Seleziona **[!UICONTROL Aggiungi servizi]**.
1. Seleziona **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. In **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]** , selezionare la configurazione desiderata e selezionare **[!UICONTROL OK]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Nella pagina web, aggiungi un componente Dynamic Media Classic (Scene7) alla posizione desiderata sulla pagina.
1. Dal Finder del contenuto, trascina una risorsa digitale sul componente. Viene visualizzato un collegamento a **[!UICONTROL Verifica stato pubblicazione Dynamic Media Classic (Scene7)]**.

   >[!NOTE]
   >
   >Se la risorsa digitale si trova nella cartella di destinazione CQ, nessun collegamento a **[!UICONTROL Verifica stato pubblicazione Dynamic Media Classic (Scene7)]** viene visualizzato. Le risorse vengono inserite nel componente.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Seleziona **[!UICONTROL Verifica stato pubblicazione Dynamic Media Classic (Scene7)]**. Se le risorse non sono pubblicate, Experience Manager le pubblica in Dynamic Media Classic (Scene7). Una volta caricata, la risorsa si trova nella cartella on-demand. Per impostazione predefinita, la cartella on-demand si trova nel **[!UICONTROL name_of_the_company/CQ5_adhoc]**. È possibile [se necessario, configura la cartella on-demand](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Se la risorsa non si trova in una cartella sincronizzata di Dynamic Media Classic (Scene7) e alla pagina corrente non è associata alcuna configurazione cloud di Dynamic Media Classic (Scene7), il caricamento non riesce.

## Componenti Dynamic Media Classic (Scene7) {#scene-components}

In Experience Manager sono disponibili i seguenti componenti di Dynamic Media Classic (Scene7):

* Zoom
* A comparsa (Zoom)
* Modello immagini
* Immagine
* Video

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati in modalità Progettazione prima di utilizzare.

Una volta resi disponibili in modalità Progettazione, puoi aggiungere i componenti alla pagina come qualsiasi altro componente di Experience Manager. Le risorse non ancora pubblicate in Dynamic Media Classic (Scene7) vengono pubblicate in Dynamic Media Classic (Scene7) se si trovano in una cartella sincronizzata o in una pagina o con una configurazione cloud di Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Se stai creando e sviluppando visualizzatori S7 personalizzati e utilizzi Content Finder, devi aggiungere esplicitamente il `allowfullscreen` parametro.

### Avviso sulla fine del ciclo di vita dei visualizzatori di Flash {#flash-viewers-end-of-life-notice}

A partire dal 31 gennaio 2017, Adobe Dynamic Media Classic (Scene7) ha ufficialmente terminato il supporto per la piattaforma di visualizzazione dei Flash.

### Aggiungere un componente Dynamic Media Classic (Scene7) a una pagina {#adding-a-scene-component-to-a-page}

L’aggiunta di un componente Dynamic Media Classic (Scene7) a una pagina equivale all’aggiunta di un componente a qualsiasi pagina. I componenti Dynamic Media Classic (Scene7) sono descritti in dettaglio nelle sezioni seguenti.

Per aggiungere un componente/visualizzatore Dynamic Media Classic (Scene7) a una pagina nell’interfaccia classica:

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il componente Dynamic Media Classic (Scene7).

1. Se non sono disponibili componenti di Dynamic Media Classic (Scene7), selezionare il righello nella barra laterale per immettere **Progettazione** modalità, seleziona **[!UICONTROL Modifica]** e selezionare tutte le opzioni **[!UICONTROL Dynamic Media Classic (Scene7)]** componenti per renderli disponibili.

1. Torna a **Modifica** selezionando la matita nella barra laterale.

1. Trascina un componente da **[!UICONTROL Dynamic Media Classic (Scene7)]** raggruppa nella barra laterale sulla pagina nella posizione desiderata.

1. Seleziona ***[!UICONTROL Modifica]** in modo da poter aprire il componente.

1. Modifica il componente secondo necessità e seleziona **[!UICONTROL OK]** per salvare le modifiche.

### Aggiungere esperienze di visualizzazione interattiva a un sito web dinamico {#adding-interactive-viewing-experiences-to-a-responsive-website}

La progettazione reattiva delle risorse comporta l’adattamento delle risorse in base alla posizione in cui vengono visualizzate. Con il design reattivo, le stesse risorse possono essere visualizzate in modo efficace su più dispositivi.

Per aggiungere un’esperienza di visualizzazione interattiva a un sito reattivo nell’interfaccia classica:

1. Accedi a Experience Manager e assicurati di disporre dei seguenti [Cloud Service Adobe Dynamic Media Classic (Scene7) configurati](/help/sites-administering/scene7.md#configuring-scene-integration) e che i componenti Dynamic Media Classic (Scene7) siano disponibili.

   >[!NOTE]
   >
   >Se i componenti WCM di Dynamic Media Classic (Scene7) non sono disponibili, assicurati di abilitarli tramite la modalità Progettazione.

1. In un sito web in cui sono abilitati i componenti Dynamic Media Classic (Scene7), trascina un’ **[!UICONTROL Immagine]** alla pagina.
1. Modifica il componente e regola i punti di interruzione nel **[!UICONTROL Impostazioni Dynamic Media Classic (Scene7)]** scheda.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Verifica che i visualizzatori siano ridimensionati in modo dinamico e che tutte le interazioni siano ottimizzate per desktop, tablet e dispositivi mobili.

### Impostazioni comuni a tutti i componenti Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Sebbene le opzioni di configurazione siano diverse, le seguenti sono comuni a tutti i componenti di Dynamic Media Classic (Scene7):

* **Riferimento file**: individua il file a cui desideri fare riferimento. Il riferimento file mostra l’URL della risorsa e non necessariamente l’URL completo di Dynamic Media Classic (Scene7), inclusi i comandi e i parametri dell’URL. Non è possibile aggiungere comandi e parametri URL di Dynamic Media Classic (Scene7) in questo campo. Devono invece essere aggiunte tramite la funzionalità corrispondente nel componente.
* **Larghezza** - Consente di impostare la larghezza.
* **Altezza** - Consente di impostare l&#39;altezza.

Per impostare queste opzioni di configurazione, apri (facendo doppio clic) un componente Dynamic Media Classic (Scene7), ad esempio, quando apri una **Zoom** componente:

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

Il componente Zoom di HTML5 mostra un’immagine più grande quando si preme il pulsante +.

La risorsa presenta strumenti di zoom in basso. Seleziona **[!UICONTROL +]** per ingrandire. Seleziona **[!UICONTROL -]** per ridurre. Selezione del **[!UICONTROL x]** oppure la freccia di ripristino riporta l&#39;immagine alle dimensioni originali con cui è stata importata. Seleziona le frecce diagonali per renderle a schermo intero. Seleziona **[!UICONTROL Modifica]** in modo da poter configurare il componente. Con questo componente, puoi configurare [impostazioni comuni a tutti i componenti di Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![Immagine dei fiori di tulipano nel componente Zoom di HTML5.](do-not-localize/chlimage_1-3.png)

### A comparsa {#flyout}

Nel componente a comparsa HTML5, la risorsa viene visualizzata come schermata divisa; a sinistra della risorsa viene visualizzata la dimensione specificata; a destra viene visualizzata la porzione di zoom. Seleziona **[!UICONTROL Modifica]** in modo da poter configurare il componente. Con questo componente, puoi configurare [impostazioni comuni a tutti i componenti di Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Se il componente a comparsa utilizza una dimensione personalizzata, questa viene utilizzata e la configurazione reattiva del componente viene disabilitata.
>
>Se il componente a comparsa utilizza le dimensioni predefinite, impostate nella vista Progettazione, vengono utilizzate le dimensioni predefinite. Il componente si estende per adattarsi alle dimensioni del layout di pagina con la configurazione reattiva del componente abilitata. Tieni presente, tuttavia, che la configurazione responsive del componente è limitata. Quando utilizzi il componente a comparsa con la configurazione reattiva, non utilizzarlo con l’estensione dell’intera pagina. In caso contrario, il riquadro a comparsa potrebbe estendersi oltre il bordo destro della pagina.

![chlimage_1-53](assets/chlimage_1-53.png)

### Immagine {#image}

Il componente Immagine Dynamic Media Classic (Scene7) consente di aggiungere la funzionalità Dynamic Media Classic (Scene7) alle immagini, ad esempio modificatori Dynamic Media Classic (Scene7), predefiniti per immagini o visualizzatori e nitidezza. Il componente immagine Dynamic Media Classic (Scene7) è simile ad altri componenti immagine in Experience Manager con speciali funzionalità Dynamic Media Classic (Scene7). In questo esempio, l’immagine ha il modificatore URL di Dynamic Media Classic (Scene7), `&op_invert=1` applicato.

![Immagine di una sfera all&#39;interno del componente immagine Dynamic Media Classic (Scene 7)](do-not-localize/chlimage_1-4.png)

**Titolo, Testo Alt** - Nella scheda Avanzate, aggiungi un titolo all&#39;immagine e testo alternativo per gli utenti che hanno la grafica disattivata.

**URL, Apri in** - È possibile impostare una risorsa da per aprire un collegamento. Imposta l’URL e in Apri in indicano se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-54](assets/chlimage_1-54.png)

**Predefinito visualizzatore** - Seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta Gestione dei predefiniti per i visualizzatori. Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

**Configurazione Dynamic Media Classic (Scene7)** - Selezionate la configurazione Dynamic Media Classic (Scene7) da utilizzare per recuperare i predefiniti immagine attivi dall&#39;SPS.

**Predefinito immagine** : seleziona un predefinito immagine esistente dal menu a discesa. Se il predefinito immagine che state cercando non è visibile, dovete renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

**Formato di output** : seleziona il formato di output dell’immagine, ad esempio jpeg. A seconda del formato di output selezionato, è possibile che siano disponibili opzioni di configurazione aggiuntive. Consulta le best practice per i predefiniti immagine.

**Nitidezza** - Selezionare la modalità di nitidezza dell&#39;immagine. La nitidezza è descritta in dettaglio nelle best practice per i predefiniti immagine e per la nitidezza.

**Modificatori URL** - È possibile modificare gli effetti immagine con comandi aggiuntivi per l&#39;immagine S7. Questi comandi sono descritti in Predefiniti immagine e nella Guida di riferimento dei comandi.

**Punti di interruzione** - Se il sito web è dinamico, è necessario regolare i punti di interruzione. I punti di interruzione devono essere separati da virgole (,).

### Modello immagini {#image-template}

I modelli di immagine Dynamic Media Classic (Scene7) sono contenuti Photoshop a più livelli importati in Dynamic Media Classic (Scene7), dove il contenuto e le proprietà sono stati parametrizzati per variabilità. Il **[!UICONTROL Modello immagine]** Questo componente consente di importare immagini e modificare dinamicamente il testo in Experience Manager. Inoltre, puoi configurare il **[!UICONTROL Modello immagine]** per utilizzare i valori provenienti dal contesto del client, in modo che ogni utente visualizzi l’immagine in modo personalizzato.

Seleziona **[!UICONTROL Modifica]** : per configurare il componente. Puoi configurare [impostazioni comuni a tutti i componenti di Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) e altre impostazioni descritte in questa sezione.

![chlimage_1-55](assets/chlimage_1-55.png)

**Riferimento file, larghezza, altezza** - Consulta [impostazioni comuni a tutti i componenti di Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>I comandi e i parametri URL di Dynamic Media Classic (Scene7) non possono essere aggiunti direttamente all’URL di riferimento del file. Possono essere definite solo nell’interfaccia utente dei componenti nel **[!UICONTROL Parametro]** pannello.

**Titolo, Testo Alt** - Nella scheda Modello immagine Dynamic Media Classic (Scene7), aggiungi un titolo all’immagine e un testo alternativo per gli utenti che hanno la grafica disattivata.

**URL, Apri in** - È possibile impostare una risorsa da per aprire un collegamento. Imposta l’URL e in Apri in indicano se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-56](assets/chlimage_1-56.png)

**Pannello Parametri** - Durante l&#39;importazione di un&#39;immagine, i parametri vengono precompilati con le informazioni dell&#39;immagine. Se non è possibile modificare dinamicamente alcun contenuto, la finestra è vuota.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Modifica dinamica del testo {#changing-text-dynamically}

Per modificare il testo in modo dinamico, immetti un nuovo testo nei campi e seleziona **[!UICONTROL OK]**. In questo esempio, la proprietà **Prezzo** ora è $50 e la spedizione è di 99 centesimi.

![chlimage_1-58](assets/chlimage_1-58.png)

Il testo nell&#39;immagine cambia. È possibile ripristinare il valore originale del testo selezionando **[!UICONTROL Reimposta]** accanto al campo.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Modificare il testo in modo che rifletta il valore di un contesto client {#changing-text-to-reflect-the-value-of-a-client-context-value}

Per collegare un campo a un valore di contesto client, selezionare **[!UICONTROL Seleziona]** per aprire il menu di scelta rapida client, selezionare il contesto client, quindi selezionare **[!UICONTROL OK]**. In questo esempio, il nome cambia in base al collegamento del Nome con il nome formattato nel profilo.

![chlimage_1-60](assets/chlimage_1-60.png)

Il testo riflette il nome dell’utente attualmente connesso. È possibile ripristinare il valore originale del testo selezionando **[!UICONTROL Reimposta]** accanto al campo.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Imposta il modello di immagine Dynamic Media Classic (Scene7) come collegamento {#making-the-scene-image-template-a-link}

Puoi impostare il componente del modello di immagine Dynamic Media Classic (Scene7) come collegamento cliccabile.

1. Nella pagina con il componente modello immagine Dynamic Media Classic (Scene7), seleziona **[!UICONTROL Modifica]**.
1. In **[!UICONTROL URL]** , immetti l&#39;URL a cui gli utenti accedono quando si fa clic sull&#39;immagine. In **[!UICONTROL Apri in]** , selezionare se si desidera aprire la destinazione (una nuova finestra o la stessa finestra).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Seleziona **[!UICONTROL OK]**.

### Componente video {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL Video]** Il componente (disponibile nella sezione Dynamic Media Classic (Scene7) della barra laterale) utilizza il rilevamento del dispositivo e della larghezza di banda per trasmettere il video corretto a ogni schermo. Questo componente è un lettore video HTML5; è un singolo visualizzatore che può essere utilizzato cross channel.

Può essere utilizzato per set video adattivi, un singolo video MP4 o un singolo video F4V.

Consulta [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) per ulteriori informazioni sul funzionamento dei video con l’integrazione Dynamic Media Classic (Scene7). Inoltre, scopri come [il **Video su Dynamic Media Classic (Scene7)** componente rispetto a foundation **video** componente](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitazioni note per il componente video {#known-limitations-for-the-video-component}

Adobe DAM e WCM mostrano se viene caricato un video sorgente principale. Non mostrano queste risorse proxy:

* Rappresentazioni con codifica Dynamic Media Classic (Scene7)
* Set video adattivi Dynamic Media Classic (Scene7)

Quando si utilizza un set video adattivo con il componente video Dynamic Media Classic (Scene7), il componente deve essere ridimensionato in base alle dimensioni del video.

## Browser di contenuti Dynamic Media Classic (Scene7) {#scene-content-browser}

Il browser del contenuto di Dynamic Media Classic (Scene7) consente di visualizzare il contenuto da Dynamic Media Classic (Scene7) direttamente in Experience Manager. Per accedere al browser del contenuto, in Content Finder, seleziona **Dynamic Media Classic (Scene7)** nell&#39;interfaccia touch o nella **S7** nell’interfaccia utente classica. La funzionalità è identica tra le due interfacce utente.

Se disponi di più configurazioni, per impostazione predefinita in Experience Manager viene visualizzato il [configurazione predefinita](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puoi selezionare diverse configurazioni direttamente nel browser del contenuto di Dynamic Media Classic (Scene7) nel menu a discesa.

>[!NOTE]
>
>* Le risorse nella cartella on-demand non vengono visualizzate nel browser del contenuto di Dynamic Media Classic (Scene7).
>* Quando [Anteprima protetta abilitata](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), le risorse pubblicate e non pubblicate su Dynamic Media Classic (Scene7) vengono visualizzate nel browser del contenuto di Dynamic Media Classic (Scene7).
>* Se non vede **[!UICONTROL Dynamic Media Classic (Scene7)]** o **[!UICONTROL S7]** come opzione nel browser del contenuto, è necessario [configurare Dynamic Media Classic (Scene7) per l’utilizzo con Experience Manager](/help/sites-administering/scene7.md).
>* Per i video, il browser dei contenuti di Dynamic Media Classic (Scene7) supporta:
>   * Set video adattivi: contenitore di tutte le rappresentazioni video necessarie per una riproduzione fluida su più schermi
>   * Video MP4 singolo
>   * Singolo video F4V

### Sfoglia contenuto {#browsing-content-in-the-classic-ui}

Sfogliare il contenuto in Dynamic Media Classic (Scene7) selezionando **[!UICONTROL S7]** scheda.

È possibile modificare la configurazione a cui si sta accedendo selezionando la configurazione. Le cartelle cambiano a seconda della configurazione selezionata.

![chlimage_1-64](assets/chlimage_1-64.png)

Come per il Finder dei contenuti di Assets, puoi cercare le risorse e filtrare i risultati. Tuttavia, a differenza del Finder risorse, quando si immette una parola chiave in **S7** , il nome del file **inizia con** la stringa immessa, anziché **contenente** la parola chiave nel nome del file.

Per impostazione predefinita, le risorse vengono visualizzate per nome file. Tuttavia, puoi anche filtrare i risultati per tipo di risorsa.

>[!NOTE]
>
>Per i video, il browser dei contenuti Dynamic Media Classic (Scene7) di WCM supporta:
>
>* Set video adattivi: contenitore di tutte le rappresentazioni video necessarie per una riproduzione fluida su più schermi
>* Video MP4 singolo
>* Singolo video F4V
>

### Cercare risorse Dynamic Media Classic (Scene7) con il browser del contenuto {#searching-for-scene-assets-with-the-content-browser}

La ricerca di risorse Dynamic Media Classic (Scene7) è simile alla ricerca di risorse Experience Manager. L’eccezione è che quando esegui una ricerca, visualizzi effettivamente una visualizzazione remota delle risorse nel sistema Dynamic Media Classic (Scene7), anziché importarle direttamente in Experience Manager.

Per visualizzare e cercare le risorse puoi utilizzare sia l’interfaccia classica che quella ottimizzata per il tocco. A seconda dell’interfaccia, la modalità di ricerca è leggermente diversa.

Quando esegui una ricerca in una delle due interfacce, puoi filtrare in base ai seguenti criteri (illustrati qui nell’interfaccia touch):

**Immettete le parole chiave** - È possibile cercare le risorse per nome. Durante la ricerca delle parole chiave, immetti il nome del file che inizia con. Ad esempio, digitando la parola &quot;nuotare&quot; si cercheranno i nomi dei file di risorse che iniziano con tali lettere in tale ordine. Assicurati di selezionare `Enter` dopo aver digitato il termine per trovare la risorsa.

![chlimage_1-65](assets/chlimage_1-65.png)

**Cartella/percorso** : il nome della cartella si basa sulla configurazione selezionata. È possibile eseguire il drill-down ai livelli inferiori selezionando l&#39;icona della cartella e una sottocartella, quindi selezionando il segno di spunta per selezionarla.

Se si immette una parola chiave e si seleziona una cartella, Experience Manager esegue la ricerca in tale cartella e nelle sottocartelle. Tuttavia, se non immetti alcuna parola chiave durante la ricerca, la selezione della cartella mostra solo le risorse presenti in quella cartella e non include alcuna sottocartella.

Per impostazione predefinita, in Experience Manager vengono cercate la cartella selezionata e tutte le sottocartelle.

![chlimage_1-66](assets/chlimage_1-66.png)

**Tipo di risorsa** - Selezionare Dynamic Media Classic (Scene7) per sfogliare il contenuto di Dynamic Media Classic (Scene7). Questa opzione è disponibile solo se è stato configurato Dynamic Media Classic (Scene7).

![chlimage_1-67](assets/chlimage_1-67.png)

**Configurazione** - Se nei Cloud Service sono definite più configurazioni di Dynamic Media Classic (Scene7), è possibile selezionarle qui. Di conseguenza, la cartella cambia in base alla configurazione scelta.

![chlimage_1-68](assets/chlimage_1-68.png)

**Tipo di risorsa** - Nel browser Dynamic Media Classic (Scene7) puoi filtrare i risultati in modo da includere uno dei seguenti elementi: immagini, modelli, video e set di video adattivi. Se non selezioni alcun tipo di risorsa, per impostazione predefinita Experience Manager esegue la ricerca in tutti i tipi di risorsa.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* Nell’interfaccia classica, puoi anche cercare **Flash** e **FXG**. Il filtro per questi due termini nell’interfaccia touch non è supportato.
>
>* Durante la ricerca di un video, viene eseguita la ricerca in un&#39;unica rappresentazione. I risultati restituiscono la rappresentazione originale (solo &#42;.mp4) e la rappresentazione codificata.
* Durante la ricerca in un set di video adattivi, esegui una ricerca nella cartella e in tutte le sottocartelle, ma solo se hai aggiunto una parola chiave alla ricerca. Se non è stata aggiunta alcuna parola chiave, la ricerca nelle sottocartelle non verrà eseguita in Experience Manager.
>

**Stato pubblicazione** - Puoi filtrare le risorse in base allo stato di pubblicazione: Non pubblicato o Pubblicato. Se non selezioni alcuno stato di pubblicazione, per impostazione predefinita Experience Manager esegue la ricerca in tutti gli stati di pubblicazione.

![chlimage_1-70](assets/chlimage_1-70.png)
