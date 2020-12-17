---
title: Aggiunta di funzionalità di Scene7 alla pagina
seo-title: Aggiunta di funzionalità di Scene7 alla pagina
description: 'Adobe Scene7 è una soluzione in hosting per la gestione, l’ottimizzazione, la modifica e la distribuzione di risorse multimediali sul vari canali: web, dispositivi mobili, e-mail, schermi collegati a Internet e stampa.'
seo-description: 'Adobe Scene7 è una soluzione in hosting per la gestione, l’ottimizzazione, la modifica e la distribuzione di risorse multimediali sul vari canali: web, dispositivi mobili, e-mail, schermi collegati a Internet e stampa.'
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
translation-type: tm+mt
source-git-commit: 863c3292d272ba4c80a80645262919e55870a437
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 61%

---


# Aggiunta di funzionalità di Scene7 alla pagina{#adding-scene-features-to-your-page}

[Adobe Scene7](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) è una soluzione in hosting per la gestione, l’ottimizzazione, la modifica e la distribuzione di risorse multimediali sul vari canali: web, dispositivi mobili, e-mail, schermi collegati a Internet e stampa.

Potete visualizzare  risorse di Experience Manager pubblicate in Scene7 in diversi visualizzatori:

* Zoom
* A comparsa
* Video
* Modello immagini
* Immagine

Potete pubblicare le risorse digitali direttamente da  Experience Manager ad Scene7 e pubblicare le risorse digitali da Scene7 a  Experience Manager.

Questo documento descrive come pubblicare risorse digitali da  Experience Manager ad Scene7 e viceversa. Sono inoltre descritti nel dettaglio i visualizzatori. Per informazioni sulla configurazione  Experience Manager per Scene7, vedere [Integrazione di Scene7 con  Experience Manager](/help/sites-administering/scene7.md).

Consulta anche [Aggiunta di mappe immagine](/help/assets/image-maps.md).

Per ulteriori informazioni sull’uso dei componenti video con  Experience Manager, consultate i seguenti riferimenti:

* [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Se le risorse Scene7 non vengono visualizzate correttamente, accertatevi che il supporto dinamico sia [disabilitato](/help/assets/config-dynamic.md#disabling-dynamic-media), quindi aggiornate la pagina.

## Pubblicazione manuale in Scene7 da Assets {#manually-publishing-to-scene-from-assets}

Si possono pubblicare le risorse digitali in Scene7 dalla console Assets nell’interfaccia classica, o direttamente dalla singola risorsa.

>[!NOTE]
>
> Experience Manager viene pubblicato in Scene7 in modo asincrono. Dopo aver cliccato su **Pubblica**, la pubblicazione della risorsa in Scene7 potrebbe richiedere alcuni secondi.


### Pubblicazione dalla console Assets {#publishing-from-the-assets-console}

Per pubblicare in Scene7 dalla console Assets se le risorse si trovano in una cartella di destinazione di Scene7:

1. Nell&#39;interfaccia classica  Experience Manager, fai clic su **Risorse digitali** per accedere al gestore risorse digitali.

1. Seleziona la risorsa (o le risorse) o la cartella all’interno della cartella di destinazione da pubblicare in Scene7, quindi fai clic con il pulsante destro del mouse e scegli **Pubblica in Scene7**. In alternativa, è possibile selezionare **Pubblica su Scene7** dal menu **Strumenti**.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Apri Scene7 e conferma che le risorse sono disponibili.

   >[!NOTE]
   >
   >Se le risorse non si trovano in una cartella sincronizzata di Scene7, l’opzione **Pubblica in Scene7** in entrambi i menu è visibile ma disabilitata.

### Pubblicazione da una risorsa {#publishing-from-an-asset}

È possibile pubblicare manualmente una risorsa purché si trovi all’interno della cartella sincronizzata di Scene7.

>[!NOTE]
>
>Se la risorsa non si trova nella cartella sincronizzata Scene7, il collegamento a **Pubblica su Scene7** non verrà visualizzato.

Per pubblicare in Scene7 direttamente da una risorsa digitale:

1. In  Experience Manager, fai clic su **Risorse digitali** per accedere al gestore risorse digitali.

1. Fai doppio clic per aprire una risorsa.

1. Nel riquadro dei dettagli delle risorse, seleziona **Pubblica in Scene7**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. Il collegamento diventa **Pubblicazione...** e quindi **Pubblicato**. Apri Scene7 e verifica che la risorsa sia disponibile.

   >[!NOTE]
   >
   >Se la risorsa non viene pubblicato correttamente in Scene7, il collegamento diventa **Pubblicazione non riuscita**. Se la risorsa è già stato pubblicata in Scene7, il collegamento reca la dicitura **Ripubblica in Scene7**. La ripubblicazione consente di apportare modifiche a una risorsa in  Experience Manager e di ripubblicarla.

### Pubblicazione di risorse dall’esterno della cartella di destinazione di CQ {#publishing-assets-from-outside-the-cq-target-folder}

Adobe consiglia di pubblicare le risorse in Scene7 solo a partire da quelle presenti nella cartella di destinazione di Scene7. Tuttavia, se dovete caricare le risorse da una cartella all’esterno della cartella di destinazione, potete comunque caricarle in una cartella **ad-hoc** su Scene7.

Per fare ciò, configura prima la configurazione Cloud per la pagina in cui apparirà la risorsa. Quindi, aggiungi un componente di Scene7 alla pagina e rilascia una risorsa sul componente. Dopo aver impostato le proprietà della pagina, viene visualizzato un collegamento **Pubblica su Scene7** che, quando selezionato, attiva il caricamento in Scene7.

>[!NOTE]
>
>Le risorse che si trovano nella cartella ad-hoc non vengono visualizzate nel browser dei contenuti di Scene7.

Per pubblicare le risorse che risiedono al di fuori della cartella di destinazione di CQ:

1. In  Experience Manager nell&#39;interfaccia classica, fate clic su **Siti Web** e individuate la pagina Web in cui desiderate aggiungere una risorsa digitale a cui non è ancora pubblicata in Scene7. (Si applicano le normali regole di ereditarietà delle pagine.)

1. Nella barra laterale, fai clic sull’icona **Pagina** e su **Proprietà pagina**.

1. Fai clic su **Servizi cloud**, quindi su **Aggiungi servizi** e seleziona **Scene7**.
1. Nell&#39;elenco a discesa **Adobe Scene7**, selezionare la configurazione desiderata e fare clic su **OK**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Nella pagina web, aggiungi un componente Scene7 alla posizione desiderata nella pagina.
1. Dal Content Finder, trascina una risorsa digitale sul componente. Viene visualizzato un collegamento a **Controlla stato pubblicazione Scene7**.

   >[!NOTE]
   >
   >Se la risorsa digitale si trova nella cartella di destinazione CQ, non viene visualizzato alcun collegamento a **Controlla stato pubblicazione Scene7**. Le risorse sono semplicemente inserite nel componente.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Fai clic su **Verifica lo stato di pubblicazione in Scene7**. Se le risorse non vengono pubblicate,  Experience Manager pubblica la risorsa in Scene7. Dopo il caricamento, la risorsa si trova nella cartella ad-hoc. Per impostazione predefinita, la cartella ad-hoc si trova in **nome_azienda/CQ5_adhoc**. Se necessario, [è possibile configurarla](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Se la risorsa non si trova in una cartella sincronizzata di Scene7 e non vi è alcuna configurazione cloud di Scene7 associata alla pagina corrente, il caricamento non andrà a buon fine.

## Componenti di Scene7  {#scene-components}

I seguenti componenti Scene7 sono disponibili in  Experience Manager:

* Zoom
* Zoom a comparsa
* Modello immagini
* Immagine
* Video

>[!NOTE]
>
>Questi componenti non sono disponibili per impostazione predefinita e devono essere selezionati nella modalità di progettazione prima dell’uso.

Una volta resi disponibili in modalità Progettazione, potete aggiungere i componenti alla pagina come qualsiasi altro componente di Experience Manager . Le risorse non ancora pubblicate in Scene7 vengono pubblicate se si trovano in una cartella sincronizzata, o su una pagina, o con una configurazione cloud di Scene7.

>[!NOTE]
>
>Se state creando e sviluppando visualizzatori S7 personalizzati e utilizzate Content Finder, dovete aggiungere esplicitamente il parametro **Allowfullscreen**.

### Avviso sulla fine del ciclo di vita dei visualizzatori Flash {#flash-viewers-end-of-life-notice}

A partire dal 31 gennaio 2017, in Adobe Scene7 verrà ufficialmente terminato il supporto per la piattaforma di visualizzazione Flash.

Per ulteriori informazioni su questa importante modifica, consulta le [domande frequenti sulla terminazione dei visualizzatori Flash](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Aggiunta di un componente Scene7 a una pagina  {#adding-a-scene-component-to-a-page}

Aggiungere un componente di Scene7 a una pagina è come aggiungere un componente a qualsiasi pagina. I componenti di Scene7 sono descritti in dettaglio nelle sezioni seguenti.

Per aggiungere un componente o visualizzatore di Scene7 a una pagina nell’interfaccia classica:

1. In  Experience Manager, aprite la pagina in cui desiderate aggiungere il componente Scene7.

1. Se non sono disponibili componenti di Scene7, fai clic sul righello nella barra laterale per accedere alla modalità **Progettazione**, fai clic su parsys **Modifica** e seleziona tutti i componenti di **Scene7** per renderli disponibili.

1. Tornate alla modalità **Modifica** facendo clic sulla matita nella barra laterale.

1. Trascina un componente dal gruppo **Scene7** nella barra laterale sulla pagina nella posizione desiderata.

1. Fai clic su **Modifica** per aprire il componente.

1. Se necessario, modifica il componente, quindi fai clic su **OK** per salvare le modifiche.

### Aggiunta di esperienze di visualizzazione interattive a un sito web reattivo  {#adding-interactive-viewing-experiences-to-a-responsive-website}

Una progettazione reattiva per le risorse significa che queste si adattano a seconda di dove vengono visualizzate. Grazie alla progettazione reattivo, le stesse risorse possono essere visualizzate in modo efficace su dispositivi diversi.

Per aggiungere un’esperienza di visualizzazione interattiva a un sito reattivo nell’interfaccia classica:

1. Accedete  Experience Manager e accertatevi di avere [configurato  Adobe Scene7 Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) e che i componenti Scene7 siano disponibili.

   >[!NOTE]
   >
   >Se i componenti Scene7 WCM non sono disponibili, accertatevi di attivarli in modalità Progettazione.

1. In un sito web con i componenti Scene7 abilitati, trascina un visualizzatore **Immagine** sulla pagina.
1. Modifica il componente e regola i punti di interruzione nella scheda **Impostazioni di Scene7**.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Verifica che i visualizzatori si ridimensionino in modo reattivo e che tutte le interazioni siano ottimizzate per desktop, tablet e dispositivi mobili.

### Impostazioni comuni a tutti i componenti di Scene7  {#settings-common-to-all-scene-components}

Anche se le opzioni di configurazione variano, le seguenti sono comuni a tutti i componenti di Scene7:

* **File di riferimento**: consente di individuare un file a cui fare riferimento. File di riferimento mostra l’URL della risorsa e non necessariamente l’URL completo di Scene7, inclusi i comandi e i parametri dell’URL. In questo campo non è possibile aggiungere comandi e parametri URL di Scene7, che devono essere aggiunti attraverso la funzionalità corrispondente nel componente.
* **Larghezza**: consente di impostare la larghezza.
* **Altezza**: consente di impostare l’altezza.

Per impostare queste opzioni di configurazione, apri (fai doppio clic) su un componente di Scene7, ad esempio per aprire un componente **Zoom**:

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

Il componente Zoom HTML5 visualizza un’immagine più grande quando si preme il pulsante +.

La risorsa dispone di strumenti di zoom nella parte inferiore. Fai clic su **+** per ingrandire. Fai clic su **-** per ridurre. Facendo clic sulla **x** o sulla freccia di ripristino dello zoom, l&#39;immagine viene riportata alle dimensioni originali con cui è stata importata. Fai clic sulle frecce diagonali per renderla a schermo intero. Fai clic su **Modifica** per configurare il componente. Con questo componente potete configurare le [impostazioni comuni a tutti i componenti Scene7](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-3.png)

### A comparsa {#flyout}

Nel componente A comparsa HTML5, la risorsa viene visualizzata come schermo diviso; a sinistra la risorsa nelle dimensioni specificate; a destra viene visualizzata la porzione di zoom. Fai clic su **Modifica** per configurare il componente. Con questo componente potete configurare le [impostazioni comuni a tutti i componenti Scene7](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Se il componente A comparsa utilizza una dimensione personalizzata, viene utilizzata tale dimensione e la configurazione reattiva del componente viene disabilitata.
>
>Se il componente a comparsa utilizza le dimensioni predefinite, come impostato nella vista Progettazione, viene utilizzata la dimensione predefinita e il componente si estende per adattarsi alle dimensioni del layout di pagina con l&#39;impostazione reattiva del componente abilitata. Tuttavia, tenete presente che esiste un limite alla configurazione reattiva del componente. Quando si utilizza il componente A comparsa con un’impostazione reattiva, non utilizzarlo con dilatazione sull’intera pagina. In caso contrario, il riquadro a comparsa potrebbe estendersi oltre il bordo destro della pagina.

![chlimage_1-53](assets/chlimage_1-53.png)

### Immagine {#image}

Il componente Immagine di Scene7 consente di aggiungere funzionalità di Scene7 alle immagini, ad esempio modificatori, impostazioni predefinite dell’immagine o del visualizzatore di Scene7 e nitidezza. Il componente immagine Scene7 è simile ad altri componenti immagine nel Experience Manager  con funzionalità Scene7 speciali. In questo esempio, all&#39;immagine è applicato il modificatore URL Scene7, **&amp;op_invert=1**.

![](do-not-localize/chlimage_1-4.png)

**Titolo,** Testo AltNella scheda Avanzate, aggiungere un titolo all’immagine e testo alternativo per gli utenti che hanno disattivato la grafica.

**URL, Apri** inPotete impostare una risorsa da cui aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-54](assets/chlimage_1-54.png)

**Visualizzatore** predefinito: selezionate un predefinito per visualizzatori esistente dal menu a discesa. Se il predefinito per visualizzatori che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta Gestione dei predefiniti per visualizzatori. Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

**Scene7** Configuration: selezionate la configurazione Scene7 da usare per recuperare i predefiniti per immagini attivi da SPS.

**Predefinito immagineSelezionate un predefinito per immagini esistente dal menu a discesa.** Se il predefinito per immagini che cerchi non è visibile, potrebbe essere necessario renderlo visibile. Consulta Gestione dei predefiniti per immagini. Non è possibile selezionare un predefinito per visualizzatori se si utilizza un predefinito per immagini, e viceversa.

**Output** Format: consente di selezionare il formato di output dell&#39;immagine, ad esempio jpeg. A seconda del formato di output selezionato, è possibile che siano disponibili ulteriori opzioni di configurazione. Consulta Best practice sui predefiniti per immagini.

**** NitidezzaSelezionate la modalità di nitidezza dell’immagine. La regolazione della nitidezza è descritta in dettaglio in Best practice sui predefiniti per immagini e Best practice sulla nitidezza.

**URL** ModificatoriPotete modificare gli effetti immagine fornendo ulteriori comandi immagine S7. Tali situazioni vengono descritte in Predefiniti per immagini e nella Guida ai comandi.

**Punti di** interruzione: se il sito Web è reattivo, è necessario regolare i punti di interruzione. I punti di interruzione devono essere separati da virgole (,).

### Modello immagini {#image-template}

I [Modelli immagini di Scene7](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) sono contenuti Photoshop a più livelli importati in Scene7, dove il contenuto e le proprietà sono stati parametrizzati per la variabilità. Il componente **Modello immagine** consente di importare immagini e modificare il testo in modo dinamico  Experience Manager. Inoltre, è possibile configurare il componente **Modello immagini** in modo che utilizzi valori contestuali ClientContext, affinché ogni utente possa avere un’esperienza personalizzata dell’immagine.

Fai clic su **Modifica** per configurare il componente. È possibile configurare le impostazioni [comuni a tutti i componenti Scene7](/help/sites-administering/scene7.md#settingscommontoallscene7components), nonché altre impostazioni descritte in questa sezione.

![chlimage_1-55](assets/chlimage_1-55.png)

**Riferimento file, Larghezza,** AltezzaVedere le impostazioni comuni a tutti i componenti Scene7.

>[!NOTE]
>
>I comandi e i parametri URL di Scene7 non possono essere aggiunti direttamente all’URL di File di riferimento. Possono essere definiti solo nell’interfaccia utente del componente del pannello **Parametri**.

**Titolo,** Testo AltNella scheda Modello immagine di Scene7, aggiungere un titolo all’immagine e al testo alternativo per gli utenti che hanno disattivato la grafica.

**URL, Apri** inPotete impostare una risorsa da cui aprire un collegamento. Imposta l’URL e in Apri in indica se desideri aprirlo nella stessa finestra o in una nuova finestra.

![chlimage_1-56](assets/chlimage_1-56.png)

**Pannello** Parametri: quando importate un’immagine, i parametri vengono precompilati con le informazioni dell’immagine. Se non vi sono contenuti modificabili dinamicamente, questa finestra è vuota.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Modifica dinamica del testo {#changing-text-dynamically}

Per modificare il testo in modo dinamico, immetti un nuovo testo nei campi e fai clic su **OK**. In questo esempio, il **Prezzo** è ora di $50 e la spedizione è di 99 centesimi.

![chlimage_1-58](assets/chlimage_1-58.png)

Il testo nell’immagine cambia. Per ripristinare il testo al valore originale, fai clic su **Ripristina** accanto al campo.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Modifica del testo in base a un valore personalizzato ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

Per collegare un campo a un valore di contesto client, fare clic su **Seleziona** per aprire il menu di scelta rapida del client, selezionare il contesto client e fare clic su **OK**. In questo esempio, il nome cambia perché è collegato al nome formattato nel profilo.

![chlimage_1-60](assets/chlimage_1-60.png)

Il testo si aggiorna con il nome dell’utente attualmente connesso. Per ripristinare il testo al valore originale, fai clic su **Ripristina** accanto al campo.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Creazione di un collegamento dal modello immagini di Scene7 {#making-the-scene-image-template-a-link}

Per fare in modo che il componente Modello immagini di Scene7 diventi un collegamento cliccabile:

1. Nella pagina contenente il componente Modello immagini di Scene7, fai clic su **Modifica**.
1. Nel campo **URL**, immetti l’URL a cui gli utenti verranno indirizzati quando fanno clic sull’immagine. Nel campo **Apri in**, selezionare se si desidera aprire la destinazione (una nuova finestra o una stessa finestra).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Fai clic su **OK**.

### Componente video  {#video-component}

Il componente Scene7 **Video** (disponibile dalla sezione Scene7 della barra laterale) utilizza il rilevamento del dispositivo e della larghezza di banda per trasmettere il video corretto a ogni schermo. Questo componente è un lettore video HTML5; è un singolo visualizzatore che può essere usato su più canali.

Può essere usato per set video adattivi, un singolo video MP4 o un singolo video F4V.

Per ulteriori informazioni sul funzionamento dei video con l’integrazione Scene7, consulta [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md). Inoltre, vedere come [il componente **Scene7 video** viene confrontato con il componente **video** di base](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitazioni note per il componente video {#known-limitations-for-the-video-component}

 Adobe DAM e WCM mostra se viene caricato un video sorgente principale. Non mostrano queste risorse proxy:

* Rappresentazioni codificate di Scene7
* Set di video adattivo di Scene7

Quando si utilizza un set di video adattivo con il componente video di Scene7, il componente dovrà essere ridimensionato per adattarsi alle dimensioni del video.

## Browser dei contenuti di Scene7 {#scene-content-browser}

Il browser dei contenuti Scene7 consente di visualizzare il contenuto di Scene7 direttamente  . Per accedere al browser dei contenuti, in Content Finder, selezionate **Scene7** nell&#39;interfaccia utente ottimizzata per il tocco o l&#39;icona **S7** nell&#39;interfaccia utente classica. La funzionalità è identica nelle due interfacce utente.

Se si dispone di più configurazioni,  Experience Manager per impostazione predefinita visualizza la [configurazione predefinita](/help/sites-administering/scene7.md#configuring-a-default-configuration). È possibile selezionare diverse configurazioni direttamente nel browser dei contenuti di Scene7 nel menu a discesa.

>[!NOTE]
>
>* Le risorse presenti nella cartella ad-hoc non verranno visualizzate nel browser dei contenuti di Scene7.
>* Quando l’[anteprima sicura è abilitata](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), nel browser dei contenuti di Scene7 vengono visualizzate le risorse pubblicate e non pubblicate in Scene7.
>* Se non visualizzate l&#39;icona **Scene7** o **S7** come opzione nel browser del contenuto, è necessario [configurare Scene7 in modo che funzioni con  Experience Manager](/help/sites-administering/scene7.md).
>* Per i video, il browser dei contenuti di Scene7 supporta:
   >   * Set di video adattivo: contenitore di tutte le rappresentazioni video necessarie per consentirne la riproduzione su diversi tipi di schermi
   >   * Video MP4 singolo
   >   * Video F4V singolo


### Esplorazione dei contenuti {#browsing-content-in-the-classic-ui}

Navigazione dei contenuti di Scene7 dalla scheda **S7**.

È possibile modificare la configurazione a cui si accede selezionando la configurazione. Le cartelle cambiano a seconda della configurazione selezionata.

![chlimage_1-64](assets/chlimage_1-64.png)

Come per il Content Finder di Assets, è possibile cercare le risorse e filtrare i risultati. Tuttavia, a differenza del finder di Assets, quando si immette una parola chiave nella scheda **S7**, il nome del file **inizia con** la stringa immessa, anziché **contenere** la parola chiave nel nome del file.

Per impostazione predefinita, le risorse vengono visualizzate per nome di file. È anche possibile filtrare i risultati per tipo di risorsa.

>[!NOTE]
>
>Per i video, il browser di contenuti di Scene7 di WCM supporta:
>
>* Set di video adattivo: contenitore di tutte le rappresentazioni video necessarie per consentirne la riproduzione su diversi tipi di schermi
>* Video MP4 singolo
>* Video F4V singolo

>



### Ricerca delle risorse di Scene7 con il browser dei contenuti {#searching-for-scene-assets-with-the-content-browser}

La ricerca di risorse Scene7 è simile alla ricerca  risorse di Experience Manager, ma quando effettuate una ricerca viene visualizzata una visualizzazione remota delle risorse nel sistema Scene7, anziché importarle direttamente in  Experience Manager.

Per visualizzare e cercare le risorse è possibile utilizzare l’interfaccia touch o classica. A seconda dell’interfaccia, la modalità di ricerca è leggermente diversa.

Durante la ricerca in una qualsiasi delle interfacce utente, è possibile filtrare in base ai seguenti criteri (mostrati qui nell’interfaccia touch):

**Inserite** le parole chiave: potete cercare le risorse per nome. Durante la ricerca, immetti le parole chiave con cui inizia il nome del file. Ad esempio, se digiti la parola “nuoto” verranno cercati i nomi dei file delle risorse che iniziano con queste lettere, in questo ordine. Assicurati di fare clic su Invia dopo aver digitato il termine per trovare la risorsa.

![chlimage_1-65](assets/chlimage_1-65.png)

**Cartella/** percorsoIl nome della cartella visualizzata si basa sulla configurazione selezionata. Per passare alle cartelle di livello inferiore, fai clic sull’icona della cartella e seleziona una sottocartella, quindi fai clic sul segno di spunta per selezionarla.

Se immettete una parola chiave e selezionate una cartella,  Experience Manager cerca tale cartella e tutte le sottocartelle. Tuttavia, se non si immettono parole chiave durante la ricerca, la selezione della cartella mostrerà solo le risorse in quella cartella, senza includere le sottocartelle.

Per impostazione predefinita,  Experience Manager esegue la ricerca nella cartella selezionata e in tutte le sottocartelle.

![chlimage_1-66](assets/chlimage_1-66.png)

**Tipo di** risorsa: selezionate Scene7 per sfogliare il contenuto Scene7. Questa opzione è disponibile solo se Scene7 è stato configurato.

![chlimage_1-67](assets/chlimage_1-67.png)

**** Configurazione: se hai più di una configurazione Scene7 definita in Cloud Services, puoi selezionarla qui. Di conseguenza, la cartella cambierà in base alla configurazione scelta.

![chlimage_1-68](assets/chlimage_1-68.png)

**Tipo** di risorsaNel browser Scene7 potete filtrare i risultati in modo da includere i seguenti elementi: immagini, modelli, video e set video adattivi. Se non selezionate alcun tipo di risorsa, per impostazione predefinita  Experience Manager esegue la ricerca in tutti i tipi di risorsa.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* Nell’interfaccia classica, è anche possibile cercare **Flash** e **FXG**. Al momento questi non sono disponibili come filtro di ricerca nell’interfaccia touch.
   >
   >
* Durante la ricerca di video, si cerca una singola rappresentazione. I risultati restituiscono la rappresentazione originale (solo *.mp4) e quella codificata.
* Quando eseguite una ricerca in un set video adattivo, state cercando la cartella e tutte le sottocartelle, ma solo se avete aggiunto una parola chiave alla ricerca. Se non avete aggiunto una parola chiave,  Experience Manager non esegue la ricerca nelle sottocartelle.



**Pubblica** statoPotete filtrare le risorse in base allo stato di pubblicazione: Non pubblicato o pubblicato. Se non selezionate Stato pubblicazione,  Experience Manager per impostazione predefinita esegue la ricerca in tutti gli stati di pubblicazione.

![chlimage_1-70](assets/chlimage_1-70.png)
