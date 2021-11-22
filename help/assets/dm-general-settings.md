---
title: Configurare le impostazioni generali di Dynamic Media
description: Scopri come gestire le impostazioni generali in Dynamic Media. Puoi impostare il nome del server di pubblicazione e il nome del server di origine qui e un’opzione di sovrascrittura delle immagini. Sono inoltre disponibili opzioni di caricamento predefinite per la maschera di contrasto delle immagini e opzioni di caricamento per l’elaborazione dei file PostScript, Adobe Photoshop, PDF e Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: f76f02f97de477af80666ea76a499578c36fb09e
workflow-type: tm+mt
source-wordcount: '2461'
ht-degree: 4%

---


# Configurare le impostazioni generali di Dynamic Media

Configurazione **[!UICONTROL Impostazioni generali di Dynamic Media]** è disponibile solo se:

* Stai eseguendo Dynamic Media in modalità Scene7. Vedi [Abilitare Dynamic Media in modalità Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Hai un *esistente* **[!UICONTROL Configurazione Dynamic Media]** in **[!UICONTROL Cloud Services]**) in Adobe Experience Manager 6.5 o versioni successive.
* Sei un amministratore di sistema di Experience Manager con privilegi di amministratore.

Dynamic Media General Settings è destinato all&#39;utilizzo da parte di sviluppatori e programmatori di siti web esperti. Adobe Dynamic Media consiglia agli utenti che modificano queste impostazioni di pubblicazione di avere familiarità con Dynamic Media su Adobe Experience Manager e la tecnologia di imaging di base.

Al momento della creazione dell’account, Adobe Dynamic Media fornisce automaticamente i server assegnati all’azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche del tuo account.

La pagina Configurazione pubblicazione di Dynamic Media stabilisce le impostazioni predefinite che determinano come le risorse vengono distribuite dai server Dynamic Media di Adobe ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Adobe Dynamic Media distribuisce una risorsa in base a un’impostazione predefinita configurata nella pagina Configurazione pubblicazione Dynamic Media.

Vedi anche [Facoltativo - Configurazione e configurazione di Dynamic Media - Impostazioni della modalità Scene7](/help/assets/option-b-config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) per ulteriori attività di configurazione facoltative.

>[!NOTE]
>
>Aggiornamento da Dynamic Media Classic a Dynamic Media su Adobe Experience Manager? La pagina Impostazioni generali e [Pubblica installazione](/help/assets/dm-publish-settings.md) In Dynamic Media vengono precompilati i valori presi dal tuo account Dynamic Media Classic . Le eccezioni sono tutti i valori elencati in **[!UICONTROL Opzioni di caricamento predefinite]** Area della pagina Impostazioni generali. Questi valori sono già in Experience Manager. Di conseguenza, eventuali modifiche apportate in **[!UICONTROL Opzioni di caricamento predefinite]**, in una qualsiasi delle cinque schede, tramite l’interfaccia utente di Experience Manager, si riflette in Dynamic Media, non in Dynamic Media Classic. Tutte le altre impostazioni e valori nella pagina Impostazioni generali e nella [Pubblica installazione](/help/assets/dm-publish-settings.md) vengono mantenute ad Experience Manager tra Dynamic Media Classic e Dynamic Media.

**Per configurare le impostazioni generali di Dynamic Media:**

1. In modalità Creazione Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Impostazioni generali di Dynamic Media]**.
1. Nella pagina Server , imposta la **[!UICONTROL Nome server pubblicato]** e **[!UICONTROL Nome server di origine]**, quindi utilizza le cinque schede per configurare le opzioni di caricamento predefinite per la modifica delle immagini e per i file Postscript, Photoshop, PDF e Illustrator.

   * [Server](#server-general-setting)
   * [Carica nell’applicazione](#upload-to-application)
   * [Modifica delle immagini](#image-editing-tab) scheda
   * [PostScript](#postscript-tab) scheda
   * [Photoshop](#photoshop-tab) scheda
   * [PDF](#pdf-tab) scheda
   * [Illustrator](#illustrator-tab) scheda

   ![Pagina Impostazioni generali di Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *pagina Impostazioni generali di Dynamic Media, con **[!UICONTROL Modifica delle immagini]**scheda selezionata.*<br><br>

1. Al termine, seleziona **[!UICONTROL Salva]**.

## Server {#server-general-setting}

Al momento della creazione dell’account, Adobe Dynamic Media fornisce automaticamente i server assegnati all’azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche del tuo account.

| Opzione | Descrizione |
| --- | --- |
| **[!UICONTROL Nome server pubblicato]** | Obbligatorio.<br>Il nome deve utilizzare `https://` nel percorso.<br>Questo server è il server CDN live (Content Deliver Network) utilizzato in tutte le chiamate URL generate dal sistema che sono specifiche per il tuo account. Non modificare il nome del server a meno che non venga richiesto da Adobe Technical Support. |
| **[!UICONTROL Nome server origine]** | Obbligatorio.<br>Questo server viene utilizzato solo per il test di controllo della qualità. Non modificare il nome del server a meno che non venga richiesto da Adobe Technical Support. |

## Carica nell’applicazione {#upload-to-application}

* **[!UICONTROL Sovrascrivi immagini]**

   Adobe Dynamic Media non consente a due file di avere lo stesso nome. L’ID Dynamic Media Adobe di ogni elemento (il nome dell’immagine meno l’estensione del nome del file) deve essere univoco. A causa di questa regola, **[!UICONTROL Carica nell’applicazione]** ha una sovrascrittura. L’effetto esatto di questa opzione dipende dall’opzione Sovrascrivi immagini selezionata. Queste opzioni specificano come vengono caricate le immagini sostitutive: se sostituiscono le immagini originali o diventano immagini duplicate. Le immagini duplicate vengono rinominate con un `-1`. Ad esempio: `chair.tif` viene rinominato `chair-1.tif`. Queste opzioni interessano le immagini caricate in una cartella diversa dall’originale o le immagini con un’estensione di nome file diversa dall’originale, ad esempio JPG, TIF o PNG.

   | Opzione Sovrascrivi immagini | Descrizione |
   | --- | --- |
   | **[!UICONTROL Sovrascrivi in cartella corrente, nome/estensione come risorsa base]** | Predefinito solo per i nuovi account Dynamic Media.<br>Questa opzione è la regola più rigida per la sostituzione. Richiede di caricare l&#39;immagine di sostituzione nella stessa cartella dell&#39;originale e che l&#39;immagine di sostituzione abbia la stessa estensione del nome file dell&#39;originale. Se tali requisiti non sono soddisfatti, viene creato un duplicato. |
   | **[!UICONTROL Sovrascrivi in cartella corrente, nome come risorsa base, ignora estensione]** | Richiede di caricare l&#39;immagine sostitutiva nella stessa cartella dell&#39;originale, tuttavia l&#39;estensione del nome file può essere diversa dall&#39;originale. Ad esempio, sedia.tif sostituisce sedia.jpg. |
   | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome/estensione come risorsa base]** | Richiede che l&#39;immagine sostitutiva abbia la stessa estensione del nome del file dell&#39;immagine originale (ad esempio, sedia.jpg deve sostituire sedia.jpg, non sedia.tif). Tuttavia, puoi caricare l’immagine di sostituzione in una cartella diversa dall’originale. L&#39;immagine aggiornata si trova nella nuova cartella; non è più possibile trovare il file nella posizione originale. |
   | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome come risorsa base, ignora estensione]** | Questa opzione è la regola di sostituzione più inclusiva. Puoi caricare un’immagine sostitutiva in una cartella diversa dall’originale, caricare un file con un’estensione diversa del nome del file e sostituire il file originale. Se il file originale si trova in una cartella diversa, l&#39;immagine sostitutiva si trova nella nuova cartella in cui è stata caricata. |

* **[!UICONTROL Mantieni ritaglio]**

   Controlla la conservazione di qualsiasi definizione di ritaglio manuale esistente.

   Vedi anche `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) e [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), entrambe nella Guida di riferimento visualizzatori di Dynamic Media.

## Opzioni di caricamento predefinite {#default-upload-options}

### Scheda Modifica immagine {#image-editing-tab}

Questo filtro consente di regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Consente di controllare l’intensità dell’effetto, il raggio dell’effetto (misurato in pixel) e una soglia di contrasto da ignorare.

L’effetto Maschera definizione dettagli utilizza le stesse opzioni del filtro Maschera definizione dettagli di Photoshop. Contrariamente a quanto suggerisce il nome, Maschera definizione dettagli è un filtro di nitidezza.

| Opzioni Maschera definizione dettagli | Descrizione |
| --- | --- |
| **[!UICONTROL Quantità]** | Obbligatorio.<br>Controlla la quantità di contrasto applicata ai pixel del bordo.<br>Pensatelo come l&#39;intensità dell&#39;effetto. La differenza principale tra i valori di quantità di Maschera definizione dettagli in Adobe Dynamic Media e i valori di quantità in Adobe Photoshop, è che Photoshop ha un intervallo di quantità compreso tra l’1% e il 500%. In Adobe Dynamic Media, invece, l’intervallo di valori è `0.0` a `5.0`. Un valore di 5.0 in Adobe Dynamic Media corrisponde approssimativamente al 500% in Photoshop; il valore 0,9 equivale al 90% e così via. |
| **[!UICONTROL Raggio]** | Obbligatorio.<br>Controlla il raggio dell&#39;effetto.<br>L&#39;intervallo di valori è `0` a `250`. L&#39;effetto viene eseguito su tutti i pixel di un&#39;immagine e si irradiano da tutti i pixel in tutte le direzioni. Il raggio viene misurato in pixel. Ad esempio, per ottenere un effetto di nitidezza simile per un&#39;immagine da 2000 x 2000 pixel e un&#39;immagine da 500 x 500 pixel, è necessario impostare un raggio di due pixel sull&#39;immagine da 2000 x 2000 pixel. Quindi imposta un valore di raggio di un pixel sull&#39;immagine da 500 x 500 pixel. Per un’immagine con più pixel viene utilizzato un valore più grande. |
| **[!UICONTROL Soglia]** | Obbligatorio.<br>La soglia è un intervallo di contrasto ignorato quando viene applicato il filtro Maschera definizione dettagli. Questo effetto è importante in modo che non venga introdotto alcun &quot;rumore&quot; a un&#39;immagine quando si utilizza questo filtro. L&#39;intervallo di valori è `0` - `255`, indica il numero di passaggi di luminosità in un&#39;immagine in scala di grigi. `0`=nero `128`=50% grigio e `255`=bianco.<br>Un valore soglia di `12` ignora le variazioni lievi è la luminosità del tono della pelle per evitare l’aggiunta di rumore, ma continua ad aggiungere contrasto ai bordi per le aree di contrasto, ad esempio dove le ciglia incontrano la pelle.<br>Se si dispone di una foto del volto di un utente, la Maschera definizione dettagli influisce sulle parti a contrasto dell’immagine. Ad esempio, dove ciglia e pelle si incontrano per creare un&#39;area ovvia di contrasto, e la pelle liscia stessa. Anche la pelle più liscia presenta sottili cambiamenti nei valori di luminosità. Se non utilizzi un valore di soglia, il filtro accentua queste sottili modifiche nei pixel dell’interfaccia. A sua volta, viene creato un effetto rumoroso e indesiderato mentre il contrasto sulle ciglia viene aumentato, aumentando la nitidezza.<br>Per evitare questo problema, viene introdotto un valore di soglia che indica al filtro di ignorare i pixel che non cambiano radicalmente il contrasto, come la pelle liscia.<br>Nell&#39;immagine della cerniera mostrata in precedenza, notate la texture accanto alle cerniere. Il rumore dell&#39;immagine è visibile perché i valori di soglia erano troppo bassi per eliminare il rumore. |
| **[!UICONTROL Monocromatico]** | Selezionare per applicare una maschera di contrasto alla luminosità dell&#39;immagine (intensità).<br>Deseleziona per applicare una maschera di contrasto a ciascun componente di colore separatamente. |

Vedi anche [Nitidezza delle immagini in Adobe Dynamic Media e su Image Server](/help/assets/assets/sharpening_images.pdf).

### Scheda PostScript {#postscript-tab}

È possibile rasterizzare i file Adobe PostScript®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

È possibile utilizzare i file Adobe PostScript® (EPS) in Adobe Dynamic Media. Adobe Dynamic Media offre comandi per configurare questi file durante il caricamento.

Quando carichi i file immagine PostScript (EPS), puoi formattarli in vari modi. È possibile rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore.

| Opzione PostScript | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire la grafica vettoriale nel file in formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini renderizzate]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |

### Scheda Photoshop {#photoshop-tab}

È possibile creare modelli da file Adobe® Photoshop®, mantenere i livelli, specificare il nome dei livelli, estrarre il testo e specificare il modo in cui le immagini vengono ancorate ai modelli.

| Opzione Photoshop | Descrizione |
| --- | --- |
| **[!UICONTROL Mantieni livelli]** | Racchiude gli eventuali livelli di PSD in singole risorse. I livelli delle risorse rimangono associati al PSD. Per visualizzarli, aprite il file PSD in Vista dettagli e selezionate il pannello dei livelli. Consulta Visualizzazione e modifica dei livelli in un file PSD. |
| **[!UICONTROL Crea modello]** | Crea un modello dai livelli nel file PSD. |
| **[!UICONTROL Estrai testo]** | Estrae il testo in modo che gli utenti possano cercare il testo in un visualizzatore. |
| **[!UICONTROL Estendi livelli a dimensione sfondo]** | Estende le dimensioni dei livelli immagine ritagliati alle dimensioni del livello di sfondo. |
| **[!UICONTROL Denominazione livelli]** | Estende le dimensioni dei livelli immagine ritagliati alle dimensioni del livello di sfondo.<br>・ **[!UICONTROL Nome livello]** - Assegna un nome alle immagini dopo i relativi nomi di livello nel file PSD. Ad esempio, un livello denominato Tag prezzo nel file PSD originale diventa un’immagine denominata Tag prezzo . Tuttavia, se i nomi dei livelli nel file PSD sono nomi di livello Photoshop predefiniti (Sfondo, Livello 1, Livello 2 e così via), le immagini vengono denominate in base ai numeri dei rispettivi livelli nel file PSD. <br>・ **[!UICONTROL Photoshop e numero di livello]** - Assegna un nome alle immagini dopo i relativi numeri di livello nel file PSD, ignorando i nomi dei livelli originali. Le immagini vengono denominate con il nome del file Photoshop e un numero di livello aggiunto. Ad esempio, il secondo livello di un file denominato `Spring Ad.psd` è denominato `Spring Ad_2` anche se aveva un nome non predefinito in Photoshop.<br>・ **[!UICONTROL Nome Photoshop e livello]** - Assegna un nome alle immagini dopo il file PSD seguito dal nome del livello o dal numero del livello. Il numero del livello viene utilizzato se i nomi dei livelli nel file PSD sono nomi di livello Photoshop predefiniti. Ad esempio, un livello denominato `Price Tag` in un file PSD denominato `SpringAd` è denominato `Spring Ad_Price Tag`. Viene chiamato un livello con il nome predefinito Livello 2 `Spring Ad_2`. |
| **[!UICONTROL Ancoraggio]** | Specifica il modo in cui le immagini vengono ancorate nei modelli generati dalla composizione a livelli prodotta dal file PSD. Per impostazione predefinita, l’ancoraggio è al centro. Un ancoraggio centrale consente alle immagini sostitutive di riempire al meglio lo stesso spazio, indipendentemente dalle proporzioni dell&#39;immagine sostitutiva. Le immagini con un aspetto diverso che sostituiscono questa immagine, quando fanno riferimento al modello e utilizzano la sostituzione di parametri, occupano effettivamente lo stesso spazio. Passa a un’impostazione diversa se l’applicazione richiede le immagini sostitutive per riempire lo spazio allocato nel modello. |

### Scheda PDF {#pdf-tab}

È possibile scegliere di rasterizzare i file, estrarre parole di ricerca e collegamenti, impostare la risoluzione e scegliere uno spazio colore.

| opzione PDF | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | ・ **[!UICONTROL Nessuno]** - Non viene eseguita alcuna elaborazione del PDF.<br>・ **[!UICONTROL Miniatura]** - Copia ogni pagina nel file PDF e la converte in un’immagine in miniatura.<br> ・ **[!UICONTROL Rasterizza]** - Esegue la rimozione delle pagine nel file PDF e converte la grafica vettoriale in immagini bitmap. Per creare un eCatalog, scegli questa opzione. |
| **[!UICONTROL Estrai]** | ・ **[!UICONTROL Nessuno]** - Nessun termine o collegamento di ricerca estratto da PDF.<br>・ **[!UICONTROL Parole di ricerca]** - Estrae le parole di ricerca dal file PDF in modo che la ricerca nel file possa essere eseguita per parola chiave in un visualizzatore di eCatalog.<br>・ **[!UICONTROL Collegamenti]** - Estrae i collegamenti dai file PDF e li converte in mappe immagine utilizzate in un visualizzatore di eCatalog.<br>・ **[!UICONTROL Ricerca di parole e collegamenti]** - Estrae sia le parole di ricerca che i collegamenti da utilizzare in un visualizzatore eCatalog. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file PDF. Il valore predefinito è 150. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file PDF.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |

### Scheda Illustrator {#illustrator-tab}

È possibile rasterizzare i file Adobe Illustrator®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

È possibile utilizzare file Adobe® Illustrator® (AI) in Adobe Dynamic Media. Adobe Dynamic Media offre comandi per configurare questi file durante il caricamento.

Quando carichi i file immagine di Illustrator (AI), puoi formattarli in vari modi. È possibile rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore. Le opzioni per la formattazione dei file PostScript e Illustrator sono disponibili nella schermata Carica in Opzioni PostScript e Opzioni Illustrator nella casella Opzioni processo di caricamento.


| Opzione Illustrator | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire la grafica vettoriale nel file in formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini renderizzate]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |
