---
title: Configurazione impostazioni generali di Dynamic Medie
description: Scopri come gestire le impostazioni generali in Dynamic Medie. Puoi impostare il nome del server di pubblicazione e il nome del server di origine qui, nonché un’opzione di sovrascrittura dell’immagine. Sono inoltre disponibili opzioni di caricamento predefinite per il mascheramento di contrasto delle immagini e opzioni di caricamento per l’elaborazione dei file PostScript, Adobe Photoshop, PDF e Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# Configurazione impostazioni generali di Dynamic Medie

La configurazione di **[!UICONTROL Impostazioni generali di Dynamic Medie]** è disponibile solo se:

* Dynamic Medie è in esecuzione in modalità Scene7. Vedere [Abilitare Dynamic Medie in modalità Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Hai *esistente* **[!UICONTROL Configurazione Dynamic Medie]** (in **[!UICONTROL Cloud Service]**) in Adobe Experience Manager 6.5.11 o versioni successive. Consulta [Creare una configurazione Dynamic Medie in Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Sei un amministratore di Experience Manager con privilegi di amministratore.

Le impostazioni generali di Dynamic Medie sono destinate all&#39;utilizzo da parte di sviluppatori e programmatori esperti di siti Web. Adobe Dynamic Medie consiglia agli utenti che modificano queste impostazioni di pubblicazione di avere familiarità con Dynamic Medie su Adobe Experience Manager e con la tecnologia di imaging di base.

Al momento della creazione dell’account, Adobe Dynamic Medie fornisce automaticamente i server assegnati alla tua azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche per il tuo account.

La pagina Configurazione di Dynamic Medie Publish stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono consegnate dai server Dynamic Medie Adobe ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Adobe Dynamic Medie distribuisce una risorsa in base a un’impostazione predefinita configurata nella pagina Dynamic Medie Publish Setup.

Vedi anche [Facoltativo - Installazione e configurazione di Dynamic Medie - Impostazioni modalità Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) per altre attività di configurazione facoltative.

>[!NOTE]
>
>Eseguire l&#39;aggiornamento da Dynamic Media Classic a Dynamic Medie su Adobe Experience Manager? La pagina Impostazioni generali e la pagina [Configurazione di Publish](/help/assets/dm-publish-settings.md) in Dynamic Medie sono precompilate con i valori presi dal tuo account Dynamic Media Classic. Le eccezioni sono tutti i valori elencati nell&#39;area **[!UICONTROL Opzioni di caricamento predefinite]** della pagina Impostazioni generali. Questi valori sono già in Experience Manager. Di conseguenza, qualsiasi modifica apportata in **[!UICONTROL Opzioni di caricamento predefinite]**, in una qualsiasi delle cinque schede, tramite l&#39;interfaccia utente di Experience Manager, si riflette in Dynamic Medie, non in Dynamic Media Classic. Tutte le altre impostazioni e i valori nella pagina Impostazioni generali e nella pagina [Configurazione di Publish](/help/assets/dm-publish-settings.md) sono mantenuti tra Dynamic Media Classic e Dynamic Medie in Experience Manager.

**Per configurare le impostazioni generali di Dynamic Medie:**

1. In modalità Autore Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Assets]** > **[!UICONTROL Impostazioni generali di Dynamic Medie]**.
1. Nella pagina Server, imposta **[!UICONTROL Nome server pubblicato]** e **[!UICONTROL Nome server di origine]**, quindi utilizza le cinque schede per configurare le opzioni di caricamento predefinite per la modifica delle immagini e per i file Postscript, Photoshop, PDF e Illustrator.

   * [Server](#server-general-setting)
   * [Carica nell’applicazione](#upload-to-application)
   * Scheda [Modifica immagine](#image-editing-tab)
   * Scheda [PostScript](#postscript-tab)
   * Scheda [Photoshop](#photoshop-tab)
   * Scheda [PDF](#pdf-tab)
   * Scheda [Illustrator](#illustrator-tab)

   ![Pagina Impostazioni generali di Dynamic Medie](/help/assets/assets-dm/dm-general-settings.png)
   *Pagina Impostazioni generali di Dynamic Medie, con la scheda **[!UICONTROL Modifica immagine]**&#x200B;selezionata.*<br><br>

1. Al termine, vicino all&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva]**.

## Server {#server-general-setting}

Al momento della creazione dell’account, Adobe Dynamic Medie fornisce automaticamente i server assegnati alla tua azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche per il tuo account.

| Opzione | Descrizione |
| --- | --- |
| **[!UICONTROL Nome server pubblicato]** | Obbligatorio.<br>Il nome deve utilizzare `https://` nel percorso.<br>Questo server è il server Live CDN (Content Deliver Network) utilizzato in tutte le chiamate URL generate dal sistema e specifiche per il tuo account. Non modificare il nome di questo server a meno che non sia stato richiesto dal supporto tecnico Adobe. |
| **[!UICONTROL Nome server di origine]** | Obbligatorio.<br>Questo server viene utilizzato solo per il test di controllo qualità. Non modificare il nome di questo server a meno che non sia richiesto dal supporto tecnico Adobe. |

## Carica nell’applicazione {#upload-to-application}

* **[!UICONTROL Sovrascrivi immagini]**

  Adobe Dynamic Medie non consente a due file di avere lo stesso nome. L’ID Dynamic Medie di Adobe di ogni elemento (il nome dell’immagine meno l’estensione del nome file) deve essere univoco. A causa di questa regola, **[!UICONTROL Il caricamento nell&#39;applicazione]** ha una sovrascrittura. L&#39;effetto esatto di questa opzione dipende dall&#39;opzione Sovrascrivi immagini selezionata. Queste opzioni specificano come vengono caricate le immagini sostitutive: se sostituiscono le immagini originali o se diventano immagini duplicate. Le immagini duplicate vengono rinominate con `-1`. Ad esempio, `chair.tif` è rinominato `chair-1.tif`. Queste opzioni hanno effetto sulle immagini caricate in una cartella diversa dall’originale o sulle immagini con un’estensione di nome file diversa dall’originale, come JPG, TIF o PNG.

  >[!NOTE]
  >
  >Per mantenere la coerenza con Experience Manager, selezionare l&#39;opzione Sovrascrivi immagini **[!UICONTROL Sovrascrivi nella cartella corrente, nome/estensione come base]**.

  | Opzione Sovrascrivi immagini | Descrizione |
  | --- | --- |
  | **[!UICONTROL Sovrascrivi nella cartella corrente, nome/estensione come base]** | *Predefinito* solo per i nuovi account Dynamic Medie.<br>Questa opzione è la regola più rigorosa per la sostituzione. È necessario caricare l&#39;immagine sostitutiva nella stessa cartella dell&#39;originale e che l&#39;immagine sostitutiva abbia la stessa estensione del nome file dell&#39;originale. Se questi requisiti non vengono soddisfatti, viene creato un duplicato.<br>*Per mantenere la coerenza con Experience Manager, selezionare questa opzione*. |
  | **[!UICONTROL Sovrascrivi nella cartella corrente, nome come risorsa base, senza estensione]** | Richiede di caricare l&#39;immagine sostitutiva nella stessa cartella dell&#39;originale, tuttavia l&#39;estensione del nome file può essere diversa dall&#39;originale. Ad esempio, chair.tif sostituisce chair.jpg. |
  | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome/estensione come risorsa base]** | Richiede che l&#39;immagine sostitutiva abbia la stessa estensione del nome file dell&#39;immagine originale (ad esempio, chair.jpg deve sostituire chair.jpg, non chair.tif). Tuttavia, è possibile caricare l&#39;immagine sostitutiva in una cartella diversa da quella originale. L&#39;immagine aggiornata si trova nella nuova cartella; il file non è più disponibile nella posizione originale. |
  | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome come risorsa base, senza estensione]** | Questa opzione è la regola di sostituzione più inclusiva. È possibile caricare un&#39;immagine sostitutiva in una cartella diversa da quella originale, caricare un file con un&#39;estensione diversa e sostituire il file originale. Se il file originale si trova in una cartella diversa, l&#39;immagine sostitutiva risiede nella nuova cartella in cui è stata caricata. |

* **[!UICONTROL Mantieni ritaglio]**

  Controlla la conservazione di qualsiasi definizione di ritaglio manuale esistente.

  Vedi anche `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) e [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), entrambi nella Guida di riferimento visualizzatori Dynamic Medie.

## Opzioni di caricamento predefinite {#default-upload-options}

### Scheda Editing immagini {#image-editing-tab}

Questo filtro consente di regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Consente di controllare l&#39;intensità dell&#39;effetto, il raggio dell&#39;effetto (misurato in pixel) e una soglia di contrasto che viene ignorata.

L&#39;effetto Maschera di contrasto utilizza le stesse opzioni del filtro Maschera di contrasto di Photoshop. Contrariamente a quanto suggerisce il nome, Maschera definizione dettagli è un filtro di nitidezza.

| Opzioni Maschera definizione dettagli | Descrizione |
| --- | --- |
| **[!UICONTROL Importo]** | Obbligatorio.<br>Controlla la quantità di contrasto applicata ai pixel del bordo.<br>Consideralo come l&#39;intensità dell&#39;effetto. La differenza principale tra i valori di quantità di Maschera di contrasto in Adobe Dynamic Medie e i valori di quantità in Adobe Photoshop è che Photoshop ha un intervallo di quantità compreso tra 1% e 500%. In Adobe Dynamic Medie, invece, l&#39;intervallo di valori è compreso tra `0.0` e `5.0`. Un valore di 5,0 in Adobe Dynamic Medie è l’equivalente approssimativo del 500% in Photoshop; un valore di 0,9 è l’equivalente del 90% e così via. |
| **[!UICONTROL Raggio]** | Obbligatorio.<br>Controlla il raggio dell&#39;effetto.<br>L&#39;intervallo di valori è compreso tra `0` e `250`. L&#39;effetto viene eseguito su tutti i pixel di un&#39;immagine e si irradia da tutti i pixel in tutte le direzioni. Il raggio è misurato in pixel. Ad esempio, per ottenere un effetto di nitidezza simile per un&#39;immagine da 2000 x 2000 pixel e per un&#39;immagine da 500 x 500 pixel, è necessario impostare un raggio di due pixel sull&#39;immagine da 2000 x 2000 pixel. Quindi impostate un valore di raggio di un pixel sull&#39;immagine da 500 x 500 pixel. Un valore più grande viene utilizzato per un&#39;immagine con più pixel. |
| **[!UICONTROL Soglia]** | Obbligatorio.<br>Soglia è un intervallo di contrasto che viene ignorato quando si applica il filtro Maschera di contrasto. Questo effetto è importante in modo che non venga introdotto alcun &quot;disturbo&quot; in un&#39;immagine quando si utilizza questo filtro. L&#39;intervallo di valori è compreso tra `0` e `255`, ovvero il numero di passaggi di luminosità in un&#39;immagine in scala di grigio. `0`=nero, `128`=grigio 50% e `255`=bianco.<br>Un valore di soglia di `12` ignora le variazioni lievi della luminosità della tonalità della pelle per evitare di aggiungere rumore, ma aggiunge comunque contrasto ai bordi delle aree in cui le ciglia incontrano la pelle.<br>Se hai una foto del volto di qualcuno, la Maschera definizione dettagli influisce sulle parti in contrasto dell&#39;immagine. Ad esempio, dove ciglia e pelle si incontrano per creare un’area di contrasto evidente e la pelle liscia stessa. Anche la pelle più liscia mostra lievi variazioni nei valori di luminosità. Se non utilizzi un valore di soglia, il filtro accentua queste sottili modifiche nei pixel della pelle. A sua volta, si crea un effetto rumoroso e indesiderato, mentre il contrasto sulle ciglia aumenta, aumentando la nitidezza.<br>Per evitare questo problema, viene introdotto un valore di soglia che indica al filtro di ignorare i pixel che non cambiano in modo significativo il contrasto, come lo skin uniforme.<br>Nell&#39;immagine della cerniera mostrata in precedenza, notare la trama accanto alle cerniere. Viene visualizzato disturbo dell&#39;immagine perché i valori di soglia erano troppo bassi per sopprimere il disturbo. |
| **[!UICONTROL Monocromatico]** | Selezionate questa opzione per applicare una maschera di contrasto alla luminosità (intensità) dell&#39;immagine.<br>Deselezionate questa opzione per applicare una maschera di contrasto a ogni componente di colore separatamente. |

Vedi anche [Immagini più nitide in Adobe Dynamic Medie e sul server immagini](/help/assets/assets/sharpening_images.pdf).

### Scheda PostScript {#postscript-tab}

Potete rasterizzare i file Adobe PostScript®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

Puoi utilizzare i file di Adobe PostScript® (EPS) in Adobe Dynamic Medie. Adobe Dynamic Medie offre comandi per la configurazione di questi file durante il caricamento.

Quando carichi i file immagine di PostScript (EPS), puoi formattarli in vari modi. Potete rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore.

| Opzione PostScript | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire gli elementi grafici vettoriali nel file nel formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini sottoposte a rendering]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina il numero di pixel visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | · **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>· **[!UICONTROL Forza come RGB]** - Converte in spazio colore RGB.<br>· **[!UICONTROL Forza come CMYK]** - Converte in spazio colore CMYK.<br>· **[!UICONTROL Forza come scala di grigio]** - Converte lo spazio colore in scala di grigio. |

### Scheda Photoshop {#photoshop-tab}

Potete creare modelli da file Adobe® Photoshop®, gestire i livelli, specificare il nome dei livelli, estrarre il testo e specificare come le immagini vengono ancorate ai modelli.

| Opzione Photoshop | Descrizione |
| --- | --- |
| **[!UICONTROL Gestisci livelli]** | Ripete i livelli nel PSD, se presenti, in singole risorse. I livelli di risorsa rimangono associati al PSD. Per visualizzarli, aprite il file PSD in Vista dettagli (Detail View) e selezionate il pannello dei livelli. Consultate Visualizzare e modificare i livelli in un file PSD. |
| **[!UICONTROL Crea modello]** | Crea un modello dai livelli nel file PSD. |
| **[!UICONTROL Estrai testo]** | Estrae il testo in modo che gli utenti possano cercare il testo in un visualizzatore. |
| **[!UICONTROL Estendi livelli alle dimensioni di sfondo]** | Estende le dimensioni dei livelli immagine strappati alle dimensioni del livello di sfondo. |
| **[!UICONTROL Denominazione livello]** | Estende le dimensioni dei livelli immagine strappati alle dimensioni del livello di sfondo.<br>· **[!UICONTROL Nome livello]** - Assegna alle immagini un nome dopo i relativi nomi di livello nel file PSD. Ad esempio, un livello denominato Tag prezzo nel file PSD originale diventa un&#39;immagine denominata Tag prezzo. Tuttavia, se i nomi dei livelli nel file PSD sono nomi di livello predefiniti di Photoshop (Sfondo, Livello 1, Livello 2 e così via), le immagini vengono denominate in base ai numeri dei livelli nel file PSD. <br>· **[!UICONTROL Photoshop e numero livello]** - Assegna alle immagini un nome dopo i numeri dei livelli nel file PSD, ignorando i nomi dei livelli originali. Le immagini sono denominate con il nome del file Photoshop e un numero di livello aggiunto. Il secondo livello di un file denominato `Spring Ad.psd`, ad esempio, è denominato `Spring Ad_2` anche se in Photoshop è presente un nome non predefinito.<br>· **[!UICONTROL Photoshop e nome livello]** - Denomina le immagini dopo il file PSD seguito dal nome o dal numero del livello. Il numero di livello viene utilizzato se i nomi di livello nel file PSD sono nomi di livello predefiniti di Photoshop. Ad esempio, un livello denominato `Price Tag` in un file PSD denominato `SpringAd` è denominato `Spring Ad_Price Tag`. Un livello con il nome predefinito Livello 2 è denominato `Spring Ad_2`. |
| **[!UICONTROL Ancoraggio]** | Specificate il modo in cui le immagini vengono ancorate nei modelli generati dalla composizione a livelli prodotta dal file PSD. Per impostazione predefinita, l&#39;ancoraggio è il centro. Un ancoraggio centrale consente alle immagini di sostituzione di occupare al meglio lo stesso spazio, indipendentemente dalle proporzioni dell&#39;immagine di sostituzione. Le immagini con un aspetto diverso che sostituiscono questa immagine, quando si fa riferimento al modello e si utilizza la sostituzione dei parametri, occupano di fatto lo stesso spazio. Impostate un&#39;impostazione diversa se l&#39;applicazione richiede le immagini sostitutive per riempire lo spazio allocato nel modello. |

### Scheda PDF {#pdf-tab}

Potete scegliere di rasterizzare i file, estrarre parole di ricerca e collegamenti, impostare la risoluzione e scegliere uno spazio colore.

| Opzione PDF | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | · **[!UICONTROL Nessuno]** - Non è stata eseguita alcuna elaborazione del PDF.<br>· **[!UICONTROL Miniatura]** - Ripete ogni pagina nel file PDF e la converte in un&#39;immagine di miniatura.<br> · **[!UICONTROL Rasterizza]** - Ripete le pagine nel file PDF e converte gli elementi grafici vettoriali in immagini bitmap. Per creare un eCatalog, scegliere questa opzione. |
| **[!UICONTROL Estrai]** | · **[!UICONTROL Nessuno]** - Nessuna parola o collegamento di ricerca estratto dal PDF.<br>· **[!UICONTROL Parole di ricerca]** - Estrae le parole di ricerca dal file PDF in modo che sia possibile eseguire ricerche per parola chiave in un visualizzatore eCatalog.<br>· **[!UICONTROL Collegamenti]** - Estrae i collegamenti dai file PDF e li converte in mappe immagine utilizzate in un visualizzatore eCatalog.<br>· **[!UICONTROL Parole e collegamenti di ricerca]** - Estrae sia le parole di ricerca che i collegamenti da utilizzare in un visualizzatore eCatalog. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina il numero di pixel visualizzati per pollice nel file PDF. Il valore predefinito è 150. |
| **[!UICONTROL Spazio colore]** | · **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file PDF.<br>· **[!UICONTROL Forza come RGB]** - Converte in spazio colore RGB.<br>· **[!UICONTROL Forza come CMYK]** - Converte in spazio colore CMYK.<br>· **[!UICONTROL Forza come scala di grigio]** - Converte lo spazio colore in scala di grigio. |

### Scheda Illustrator {#illustrator-tab}

Potete rasterizzare i file Adobe Illustrator®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

Puoi utilizzare i file Adobe® Illustrator® (AI) in Adobe Dynamic Medie. Adobe Dynamic Medie offre comandi per la configurazione di questi file durante il caricamento.

Quando carichi i file immagine di Illustrator (AI), puoi formattarli in vari modi. Potete rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore. Le opzioni per la formattazione dei file PostScript e Illustrator sono disponibili nella schermata Carica in Opzioni PostScript e Opzioni Illustrator nella casella Opzioni processo di caricamento.


| Opzione Illustrator | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire gli elementi grafici vettoriali nel file nel formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini sottoposte a rendering]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina il numero di pixel visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | · **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>· **[!UICONTROL Forza come RGB]** - Converte in spazio colore RGB.<br>· **[!UICONTROL Forza come CMYK]** - Converte in spazio colore CMYK.<br>· **[!UICONTROL Forza come scala di grigio]** - Converte lo spazio colore in scala di grigio. |
