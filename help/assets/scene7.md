---
title: Aggiungere funzioni di Dynamic Media Classic alle pagine
description: Come aggiungere funzioni e componenti di Dynamic Media Classic a una pagina in Adobe Experience Manager.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 1%

---

# Aggiungere funzioni di Dynamic Media Classic alle pagine {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) è una soluzione in hosting per la gestione, l&#39;ottimizzazione, la pubblicazione e la distribuzione di risorse rich media per web, dispositivi mobili, e-mail, display e stampa connessi a Internet.

Puoi visualizzare le risorse di Experience Manager pubblicate in Dynamic Media Classic in vari visualizzatori:

* Zoom
* A comparsa
* Video
* Modello immagini
* Immagine

Puoi pubblicare le risorse digitali direttamente da Experience Manager a Dynamic Media Classic, e le risorse digitali da Dynamic Media Classic a Experience Manager.

Questo documento descrive come pubblicare le risorse digitali da Experience Manager a Dynamic Media Classic e viceversa. Vengono descritti in dettaglio anche i visualizzatori. Per informazioni sulla configurazione di Experience Manager per Dynamic Media Classic, consulta [Integrare Dynamic Media Classic con Experience Manager](/help/sites-administering/scene7.md).

Vedi anche [Aggiungi mappe immagine](image-maps.md).

Per ulteriori informazioni sull’utilizzo dei componenti video con Experience Manager, consulta [Video](video.md).

>[!NOTE]
>
>Se le risorse Dynamic Media Classic non vengono visualizzate correttamente, assicurati che Dynamic Medie sia [disabilitato](config-dynamic.md#disabling-dynamic-media) e quindi aggiorna la pagina.

## Pubblicazione manuale in Dynamic Media Classic dalle risorse {#manually-publishing-to-scene-from-assets}

Puoi pubblicare le risorse digitali in Dynamic Media Classic nel modo seguente:

* [Nell’interfaccia utente classica dalla console Assets](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Nell’interfaccia utente classica da una risorsa](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Nell’interfaccia utente classica dall’esterno della cartella di CQ Target](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager pubblica in Dynamic Media Classic in modo asincrono. Dopo aver selezionato **[!UICONTROL Pubblica]**, la pubblicazione della risorsa in Dynamic Media Classic richiede diversi secondi.
>

## Componenti Dynamic Media Classic {#scene-components}

In Experience Manager sono disponibili i seguenti componenti di Dynamic Media Classic:

* Zoom
* A comparsa (Zoom)
* Modello immagini
* Immagine
* Video

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati in **[!UICONTROL Progettazione]** prima di utilizzare.

Dopo che sono stati resi disponibili in **[!UICONTROL Progettazione]** in modalità, puoi aggiungere i componenti alla pagina come qualsiasi altro componente di Experience Manager. Le risorse non ancora pubblicate in Dynamic Media Classic vengono pubblicate in Dynamic Media Classic se si trovano in una cartella sincronizzata o in una pagina o con una configurazione cloud di Dynamic Media Classic.

>[!NOTE]
>
>Se crei e sviluppi visualizzatori personalizzati e utilizzi Content Finder, devi aggiungere esplicitamente il `allowfullscreen` parametro.

### Avviso sulla fine del ciclo di vita dei visualizzatori Flash {#flash-viewers-end-of-life-notice}

A partire dal 31 gennaio 2017, Adobe Dynamic Media Classic ha terminato il supporto per la piattaforma di visualizzazione dei Flash.

### Aggiungere un componente Dynamic Media Classic (Scene7) a una pagina {#adding-a-scene-component-to-a-page}

L’aggiunta di un componente Dynamic Media Classic (Scene7) a una pagina equivale all’aggiunta di un componente a qualsiasi pagina. I componenti Dynamic Media Classic sono descritti in dettaglio nelle sezioni seguenti.

**Per aggiungere un componente Dynamic Media Classic (Scene7) a una pagina:**

1. Ad Experience Manager, apri la pagina in cui desideri aggiungere il **[!UICONTROL Dynamic Media Classic (Scene7)]** componente.

1. Se non è disponibile alcun componente di Dynamic Media Classic, seleziona **[!UICONTROL Progettazione]** , seleziona un componente con un bordo blu, seleziona la **[!UICONTROL Elemento padre]** e quindi l&#39; **[!UICONTROL Configurazione]** icona. In entrata **[!UICONTROL Parsys (Progettazione)]**, seleziona tutti i componenti Dynamic Media Classic per renderli disponibili e seleziona **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Seleziona **[!UICONTROL Modifica]** in modo da poter tornare a **[!UICONTROL Modifica]** modalità.

1. Trascina un componente dal gruppo Dynamic Media Classic nella barra laterale e rilascialo sulla pagina nella posizione desiderata.

1. Seleziona la **[!UICONTROL Configurazione]** in modo da poter aprire il componente.

1. Modifica il componente secondo necessità e seleziona **[!UICONTROL OK]** per salvare le modifiche.
1. Trascina l’immagine o il video dal browser dei contenuti al componente Dynamic Media Classic aggiunto alla pagina.

   >[!NOTE]
   >
   >Solo nell’interfaccia touch, devi trascinare e rilasciare l’immagine o il video sul componente Dynamic Media Classic inserito nella pagina. Non sono supportate la selezione e la modifica del componente Dynamic Media Classic e la scelta della risorsa.

### Aggiungere un’esperienza di visualizzazione interattiva a un sito reattivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

Il design reattivo delle risorse si adatta a seconda della posizione in cui vengono visualizzate. Con il design reattivo, le stesse risorse possono essere visualizzate in modo efficace su più dispositivi.

Vedi anche [Progettazione reattiva per le pagine web](/help/sites-developing/responsive.md).

**Per aggiungere un’esperienza di visualizzazione interattiva a un sito reattivo:**

1. Accedi a Experience Manager e assicurati di disporre dei seguenti [Cloud Service Adobe Dynamic Media Classic configurati](/help/sites-administering/scene7.md#configuring-scene-integration) e che i componenti Dynamic Media Classic siano disponibili.

   >[!NOTE]
   >
   >Se i componenti Dynamic Media Classic non sono disponibili, assicurati [per attivarli in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

1. In un sito Web con **[!UICONTROL Dynamic Media Classic]** componenti abilitati, trascina un’ **[!UICONTROL Immagine]** alla pagina.
1. Seleziona il componente e fai clic sull’icona di configurazione.
1. In **[!UICONTROL Impostazioni Dynamic Media Classic]** , regolare i punti di interruzione.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Verifica che i visualizzatori siano ridimensionati in modo dinamico e che tutte le interazioni siano ottimizzate per desktop, tablet e dispositivi mobili.

### Impostazioni comuni a tutti i componenti Dynamic Media Classic {#settings-common-to-all-scene-components}

Anche se le opzioni di configurazione variano, le seguenti sono comuni a tutti [!UICONTROL Dynamic Media Classic] componenti:

* **[!UICONTROL Riferimento file]** : individua il file a cui desideri fare riferimento. Il riferimento file mostra l’URL della risorsa e non necessariamente l’URL completo di Dynamic Media Classic, inclusi i comandi e i parametri dell’URL. Non è possibile aggiungere comandi e parametri URL di Dynamic Media Classic in questo campo. Puoi invece aggiungerli attraverso la funzionalità corrispondente nel componente.
* **[!UICONTROL Larghezza]** - Consente di impostare la larghezza.
* **[!UICONTROL Altezza]** - Consente di impostare l&#39;altezza.

Per impostare queste opzioni di configurazione, apri (facendo doppio clic) un componente Dynamic Media Classic, ad esempio, quando apri un **[!UICONTROL Zoom]** componente:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

Il componente Zoom di HTML5 mostra un&#39;immagine più grande quando si preme il tasto **[!UICONTROL +]** pulsante.

La risorsa presenta strumenti di zoom in basso. Seleziona **[!UICONTROL +]** per ingrandire, selezionare **[!UICONTROL -]** se vuoi ridurre. Toccando la **[!UICONTROL x]** oppure la freccia di ripristino riporta l&#39;immagine alle dimensioni originali in cui è stata importata. Seleziona le frecce diagonali per renderle a schermo intero. Seleziona **[!UICONTROL Modifica]** in modo da poter configurare il componente. Con questo componente, puoi configurare [impostazioni comuni a tutti [!UICONTROL Dynamic Media Classic] componenti](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### A comparsa {#flyout}

Nel HTML 5 **[!UICONTROL A comparsa]** componente, la risorsa viene visualizzata come schermata divisa; lascia la risorsa nelle dimensioni specificate; a destra viene visualizzata la porzione di zoom. Seleziona **[!UICONTROL Modifica]** in modo da poter configurare il componente. Con questo componente, puoi configurare [impostazioni comuni a tutti i componenti di Dynamic Media Classic](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Se il **[!UICONTROL A comparsa]** il componente utilizza una dimensione personalizzata, quindi viene utilizzata tale dimensione personalizzata e la configurazione reattiva del componente è disabilitata.
>
>Se il **[!UICONTROL A comparsa]** il componente utilizza le dimensioni predefinite, impostate in **[!UICONTROL Visualizzazione Progettazione]**, quindi vengono utilizzate le dimensioni predefinite e il componente si estende per adattarsi alle dimensioni del layout di pagina con la configurazione reattiva del componente abilitata. La configurazione reattiva del componente è limitata. Quando si utilizza **[!UICONTROL A comparsa]** con la configurazione reattiva, non utilizzarlo con l’estensione dell’intera pagina. In caso contrario, **[!UICONTROL A comparsa]** si estende oltre il bordo destro della pagina.

![chlimage_1-228](assets/chlimage_1-228.png)

### Immagine {#image}

Dynamic Media Classic **[!UICONTROL Immagine]** Questo componente consente di aggiungere funzionalità Dynamic Media Classic alle immagini, ad esempio modificatori Dynamic Media Classic, predefiniti per immagini o visualizzatori e nitidezza. Dynamic Media Classic **[!UICONTROL Immagine]** è simile ad altri componenti immagine in Experience Manager con speciali funzionalità Dynamic Media Classic. In questo esempio, l’immagine ha il modificatore URL di Dynamic Media Classic, `&op_invert=1` applicato.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Titolo, Testo Alt]** - Nella **[!UICONTROL Avanzate]** , aggiungi un titolo all&#39;immagine e testo alternativo per gli utenti che hanno la grafica disattivata.

**[!UICONTROL URL, Apri in]** - È possibile impostare una risorsa da per aprire un collegamento. Imposta il **[!UICONTROL URL]** e in **[!UICONTROL Apri in]** indicare se si desidera aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Predefinito visualizzatore]** - Seleziona un predefinito visualizzatore esistente dal menu a discesa. Se il predefinito visualizzatore che stai cercando non è visibile, devi renderlo visibile. Consulta [Gestisci predefiniti visualizzatore](/help/assets/managing-viewer-presets.md). Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

**[!UICONTROL Configurazione Dynamic Media Classic]** - Selezionate la configurazione Dynamic Media Classic da utilizzare per recuperare i predefiniti immagine attivi da SPS.

**[!UICONTROL Predefinito immagine]** : seleziona un predefinito immagine esistente dal menu a discesa. Se il predefinito immagine che state cercando non è visibile, dovete renderlo visibile. Consulta [Gestione predefiniti immagine](/help/assets/managing-image-presets.md). Non è possibile selezionare un predefinito visualizzatore se si utilizza un predefinito immagine e viceversa.

**[!UICONTROL Formato di output]** : seleziona il formato di output dell’immagine, ad esempio jpeg. A seconda del formato di output selezionato, sono disponibili opzioni di configurazione aggiuntive. Consulta [Best practice per il predefinito immagine](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Nitidezza]** - Selezionare la modalità di nitidezza dell&#39;immagine. L&#39;nitidezza viene spiegata in dettaglio in [Best practice per il predefinito immagine](/help/assets/managing-image-presets.md#image-preset-options) e [Best practice per la nitidezza](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL Modificatori URL]** - È possibile modificare gli effetti immagine con comandi immagine Dynamic Media Classic aggiuntivi. Questi comandi sono descritti in [Predefiniti immagine](/help/assets/managing-image-presets.md) e [Riferimento comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Punti di interruzione]** - Se il sito web è dinamico, è necessario regolare i punti di interruzione. I punti di interruzione devono essere separati da virgole ( , ).

### Modello immagini {#image-template}

[Modelli immagine Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) sono contenuti Photoshop a più livelli importati in Dynamic Media Classic, dove contenuto e proprietà sono stati parametrizzati per la variabilità. Il **[!UICONTROL Modello immagine]** Questo componente consente di importare immagini e modificare dinamicamente il testo in Experience Manager. Inoltre, puoi configurare il **[!UICONTROL Modello immagine]** per utilizzare i valori provenienti dal contesto del client, in modo che ogni utente visualizzi l’immagine in modo personalizzato.

Seleziona **[!UICONTROL Modifica]** se desideri configurare il componente. Puoi configurare [impostazioni comuni a tutti i componenti di Dynamic Media Classic](#settings-common-to-all-scene-components) e altre impostazioni descritte in questa sezione.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Riferimento file, larghezza, altezza]** - Consulta le impostazioni comuni a tutti i componenti di ScDynamic Media Classicene7.

>[!NOTE]
>
>I comandi e i parametri URL di Dynamic Media Classic non possono essere aggiunti direttamente all’URL di riferimento del file. Possono essere definite solo nell’interfaccia utente dei componenti nel **[!UICONTROL Parametro]** pannello.

**[!UICONTROL Titolo, Testo Alt]** - Nella scheda Modello di immagine Dynamic Media Classic, aggiungi un titolo all&#39;immagine e testo alternativo per gli utenti che hanno la grafica disattivata.

**[!UICONTROL URL, Apri in]** - È possibile impostare una risorsa da per aprire un collegamento. Imposta l’URL e in Apri in indicano se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Pannello Parametri]** - Durante l&#39;importazione di un&#39;immagine, i parametri vengono precompilati con le informazioni dell&#39;immagine. Se non è possibile modificare dinamicamente alcun contenuto, la finestra è vuota.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Modificare il testo in modo dinamico {#changing-text-dynamically}

Per modificare il testo in modo dinamico, immetti un nuovo testo nei campi e seleziona **[!UICONTROL OK]**. In questo esempio, la proprietà **[!UICONTROL Prezzo]** ora è $50 e la spedizione è di 99 centesimi.

![chlimage_1-234](assets/chlimage_1-234.png)

Il testo nell&#39;immagine cambia. Per ripristinare il testo al valore originale, tocca **[!UICONTROL Reimposta]** accanto al campo.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Modificare il testo in modo che rifletta il valore di un contesto client {#changing-text-to-reflect-the-value-of-a-client-context-value}

Per collegare un campo a un valore di contesto client, selezionare **[!UICONTROL Seleziona]** per aprire il menu di scelta rapida client, selezionare il contesto client, quindi selezionare **[!UICONTROL OK]**. In questo esempio, il nome cambia in base al collegamento del Nome con il nome formattato nel profilo.

![chlimage_1-236](assets/chlimage_1-236.png)

Il testo riflette il nome dell’utente attualmente connesso. È possibile ripristinare il valore originale del testo facendo clic su **[!UICONTROL Reimposta]** accanto al campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Imposta il modello di immagine Dynamic Media Classic come collegamento {#making-the-scene-image-template-a-link}

1. Sulla pagina con Dynamic Media Classic **[!UICONTROL Modello immagini]** componente, seleziona **[!UICONTROL Modifica]**.
1. In **[!UICONTROL URL]** , immetti l&#39;URL a cui gli utenti accedono quando l&#39;immagine viene toccata. In **[!UICONTROL Apri in]** , selezionare se si desidera aprire la destinazione (una nuova finestra o la stessa finestra).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Seleziona **[!UICONTROL OK]**.

### Componente video {#video-component}

Dynamic Media Classic **[!UICONTROL Video]** Il componente (disponibile nella sezione Dynamic Media Classic della barra laterale) utilizza il rilevamento del dispositivo e della larghezza di banda per trasmettere il video corretto a ogni schermo. Questo componente è un lettore video HTML5; è un singolo visualizzatore che può essere utilizzato cross channel.

Può essere utilizzato per set video adattivi, un singolo video MP4 o un singolo video F4V.

Consulta [Video](s7-video.md) per ulteriori informazioni sul funzionamento dei video con l’integrazione Dynamic Media Classic. Inoltre, vedi [Componente video Dynamic Media Classic e Componente video di base](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitazioni note del componente video {#known-limitations-for-the-video-component}

Adobe DAM e WCM mostrano se viene caricato un video sorgente principale. Non mostrano queste risorse proxy:

* Rappresentazioni con codifica Dynamic Media Classic
* Set video adattivi Dynamic Media Classic

Quando utilizzi un set di video adattivi con il componente video Dynamic Media Classic, devi ridimensionare il componente in base alle dimensioni del video.

## Browser contenuti Dynamic Media Classic {#scene-content-browser}

Il browser del contenuto di Dynamic Media Classic consente di visualizzare il contenuto da Dynamic Media Classic direttamente in Experience Manager. Per accedere al browser del contenuto, in **[!UICONTROL Content Finder]**, seleziona **[!UICONTROL Dynamic Media Classic]** nell&#39;interfaccia touch o nella **[!UICONTROL S7]** nell’interfaccia utente classica. La funzionalità è identica tra le due interfacce utente.

Se disponi di più configurazioni, per impostazione predefinita in Experience Manager viene visualizzato il [configurazione predefinita](/help/sites-administering/scene7.md#configuring-a-default-configuration). Puoi selezionare diverse configurazioni direttamente nel browser del contenuto di Dynamic Media Classic nel menu a discesa.

>[!NOTE]
>
>* Le risorse nella cartella on-demand non vengono visualizzate nel browser del contenuto di Dynamic Media Classic.
>* Quando [Anteprima protetta abilitata](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)Le risorse pubblicate e non pubblicate su Dynamic Media Classic vengono visualizzate nel browser del contenuto di Dynamic Media Classic.
>* Se non vede **[!UICONTROL Dynamic Media Classic]** o **[!UICONTROL S7]** come opzione nel browser del contenuto, è necessario [configurare Dynamic Media Classic per l’utilizzo con Experience Manager](/help/sites-administering/scene7.md).
>* Per i video, il browser dei contenuti di Dynamic Media Classic supporta:
>
>   * Set video adattivi: contenitore di tutte le rappresentazioni video necessarie per una riproduzione fluida su più schermi
>   * Video MP4 singolo
>   * Singolo video F4V

### Sfogliare i contenuti nell’interfaccia touch {#browsing-content-in-the-touch-optimized-ui}

Puoi accedere al browser dei contenuti dall’interfaccia utente classica o ottimizzata per il tocco. Attualmente, il touch-optimized presenta i seguenti limiti:

* Le risorse FXG e Flash di Dynamic Media Classic non sono supportate.

Sfogliare le risorse Dynamic Media Classic selezionando **[!UICONTROL Dynamic Media Classic]** dal terzo menu a discesa. Dynamic Media Classic non viene visualizzato nell’elenco se non è stata configurata l’integrazione Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* Il browser del contenuto di Dynamic Media Classic carica circa 100 risorse e le ordina per nome.
>* Se hai impostato un server di anteprima protetto, il browser lo utilizza per eseguire il rendering di miniature e risorse.
>

![chlimage_1-240](assets/chlimage_1-240.png)

Inoltre, puoi sfogliare le informazioni sulla risoluzione, le dimensioni, i giorni trascorsi dalla modifica e il nome del file passando il puntatore del mouse sulla risorsa nel browser.

![chlimage_1-241](assets/chlimage_1-241.png)

* Per i set e i modelli video adattivi, non vengono generate informazioni sulle dimensioni delle miniature.
* Per i set video adattivi, non viene generata alcuna risoluzione per le miniature.

### Cercare risorse Dynamic Media Classic con il browser del contenuto {#searching-for-scene-assets-with-the-content-browser}

La ricerca delle risorse in Dynamic Media Classic è simile alla ricerca delle risorse in Experience Manager Assets. Tuttavia, quando esegui una ricerca, visualizzi effettivamente una visualizzazione remota delle risorse nel sistema Dynamic Media Classic, anziché importarle direttamente in Experience Manager.

Per visualizzare e cercare le risorse puoi utilizzare sia l’interfaccia classica che quella ottimizzata per il tocco. A seconda dell’interfaccia, la modalità di ricerca è leggermente diversa.

Quando esegui una ricerca in una delle due interfacce, puoi filtrare in base ai seguenti criteri (illustrati qui nell’interfaccia touch):

**[!UICONTROL Immettete le parole chiave]** - È possibile cercare le risorse per nome. Durante la ricerca, le parole chiave immesse sono quelle iniziali del nome del file. Ad esempio, digitando la parola &quot;nuotare&quot; si cercheranno i nomi dei file di risorse che iniziano con tali lettere in tale ordine. Assicurati di premere Invio dopo aver digitato il termine per trovare la risorsa.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Cartella/percorso]** : il nome della cartella visualizzata dipende dalla configurazione selezionata. Per eseguire il drill-down ai livelli inferiori, tocca l’icona della cartella e seleziona una sottocartella, quindi tocca il segno di spunta per selezionarla.

Se si immette una parola chiave e si seleziona una cartella, Experience Manager esegue la ricerca in tale cartella e nelle sottocartelle. Tuttavia, se non immetti alcuna parola chiave durante la ricerca, la selezione della cartella mostra solo le risorse presenti in quella cartella e non include alcuna sottocartella.

Per impostazione predefinita, in Experience Manager vengono cercate la cartella selezionata e tutte le sottocartelle.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo di risorsa]** - Seleziona **[!UICONTROL Dynamic Media Classic]** per sfogliare il contenuto di Dynamic Media Classic. Questa opzione è disponibile solo se Dynamic Media Classic è stato configurato.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configurazione]** - Se sono definite più configurazioni Dynamic Media Classic [!UICONTROL Cloud Service], è possibile selezionarlo qui. Di conseguenza, la cartella cambia in base alla configurazione scelta.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo di risorsa]** - Nel browser Dynamic Media Classic puoi filtrare i risultati in modo da includere uno dei seguenti elementi: immagini, modelli, video e set di video adattivi. Se non selezioni alcun tipo di risorsa, ad Experience Manager, per impostazione predefinita, cerca tutti i tipi di risorsa.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Nell’interfaccia classica, puoi anche cercare **Flash** e **FXG**. Il filtro per questi tipi nell’interfaccia touch non è supportato.
>
>* Durante la ricerca di un video, viene eseguita la ricerca in un&#39;unica rappresentazione. I risultati restituiscono la rappresentazione originale (solo &amp;ast;.mp4) e la rappresentazione codificata.
>* Durante la ricerca in un set di video adattivi, la ricerca viene eseguita nella cartella e in tutte le sottocartelle, ma solo se alla ricerca è stata aggiunta una parola chiave. Se non è stata aggiunta alcuna parola chiave, la ricerca nelle sottocartelle non verrà eseguita in Experience Manager.
>

**[!UICONTROL Stato pubblicazione]** - Puoi filtrare le risorse in base allo stato di pubblicazione: **[!UICONTROL Non pubblicato]** o **[!UICONTROL Pubblicato]**. Se non si seleziona alcuna **[!UICONTROL Stato pubblicazione]**, Experience Manager per impostazione predefinita cerca tutti gli stati di pubblicazione.

![chlimage_1-247](assets/chlimage_1-247.png)
