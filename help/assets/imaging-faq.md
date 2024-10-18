---
title: Imaging avanzato
description: La tecnologia Smart Imaging applica le esclusive caratteristiche di visualizzazione di ogni utente per fornire le immagini giuste ottimizzate automaticamente per la propria esperienza, con conseguente miglioramento delle prestazioni e del coinvolgimento.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7fb3ec9654b56605321f0d12a4c1e23d2e18dab9
workflow-type: tm+mt
source-wordcount: '3322'
ht-degree: 0%

---

# Imaging avanzato {#smart-imaging}

La tecnologia Smart Imaging applica le esclusive caratteristiche di visualizzazione di ogni utente per fornire le immagini giuste ottimizzate automaticamente per la propria esperienza, con conseguente miglioramento delle prestazioni e del coinvolgimento.

## Informazioni sulla tecnologia Smart Imaging {#what-is-smart-imaging}

La tecnologia di imaging intelligente applica le funzionalità di intelligenza artificiale di Adobe Sensei e funziona con i &quot;predefiniti immagine&quot; esistenti. Funziona per migliorare le prestazioni di consegna delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

E ora, ottieni un punteggio Google Core Web Vital migliore per LCP (Largest Contentful Paint) con Smart Imaging migliorato, che ora viene fornito con supporto sia AVIF che WebP.

>[!IMPORTANT]
>
>La tecnologia Smart Imaging richiede l’utilizzo della rete CDN (Content Delivery Network) predefinita in bundle con Adobe Experience Manager - Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

>[!TIP]
>
>Prova e scopri i vantaggi dei modificatori di immagini Dynamic Medie e dell&#39;imaging avanzato con Dynamic Medie [_Snapshot_](https://snapshot.scene7.com/).
>
>Snapshot è uno strumento di dimostrazione visiva, progettato per illustrare la potenza di Dynamic Medie per la distribuzione di immagini ottimizzate e dinamiche. Sperimenta immagini di test o URL Dynamic Medie per osservare visivamente l’output di vari modificatori di immagini Dynamic Medie e ottimizzazioni Smart Imaging per i seguenti elementi:
>
>* Dimensione del file (con consegna WebP e AVIF)
>* Larghezza di banda di rete
>* DPR (Device Pixel Ratio, rapporto pixel dispositivo)
>
>Per scoprire quanto è facile utilizzare Snapshot, riprodurre il [video di formazione Snapshot](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minuti e 17 secondi).

La tecnologia Smart Imaging ottimizza ulteriormente le prestazioni grazie alla piena integrazione con il migliore servizio CDN (Content Delivery Network) Adobe. Questo servizio individua il percorso Internet ottimale tra server, reti e punti di peering. Trova una route con latenza e velocità di perdita dei pacchetti più basse anziché utilizzare la route predefinita su Internet.

I seguenti esempi di risorse di immagini illustrano l’ottimizzazione Smart Imaging aggiunta:

| Immagine (URL) | Miniatura  | Dimensione (JPEG) | Dimensioni (WebP) con Smart Imaging | Formato (AVIF) con Smart Imaging | Riduzione % con WebP | % di riduzione con AVIF |
|---|---|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90,2 KB | 26,89% | 37,79% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01% | 72,57% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87,1 KB | 14,47% | 60,58% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25% | 51,85% |

Analogamente a quanto sopra, Adobe ha anche eseguito un test con un set di campioni più grande. Il formato AVIF forniva una riduzione delle dimensioni del 20% in più rispetto a WebP, che forniva una riduzione del 27% rispetto a JPEG. Tutto alla stessa qualità visiva. In totale, AVIF fornisce una riduzione media delle dimensioni fino al 41% rispetto a JPEG.

Confrontando WebP e AVIF con PNG, si può notare una riduzione delle dimensioni dell&#39;84% con WebP e dell&#39;87% con AVIF. Inoltre, poiché sia il formato WebP che AVIF supportano la trasparenza e le animazioni di più immagini, si tratta di una valida sostituzione per i file PNG e GIF trasparenti.

Vedi anche [Ottimizzazione immagine con formati immagine di nuova generazione (WebP e AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Vantaggi della tecnologia Smart Imaging {#what-are-the-key-benefits-of-smart-imaging}

La tecnologia Smart Imaging ottimizza automaticamente la consegna delle immagini ottimizzando le dimensioni del file in base al browser, alla visualizzazione del dispositivo e alle condizioni di rete dell&#39;utente. Questo approccio garantisce tempi di caricamento più rapidi e una migliore esperienza di visualizzazione in ambienti diversi. Poiché le immagini rappresentano la maggior parte del tempo di caricamento di una pagina, qualsiasi miglioramento delle prestazioni può avere un impatto profondo sui KPI aziendali, ad esempio quanto segue:

* Tassi di conversione più elevati.
* Tempo trascorso su un sito.
* Riduci le percentuali di mancato recapito del sito.

I vantaggi più recenti della tecnologia Smart Imaging includono:

* Supporta il formato AVIF di nuova generazione.
* PNG in WebP e AVIF ora supporta la conversione con perdita di dati. Poiché PNG è un formato senza perdita di dati, le versioni precedenti di WebP e AVIF distribuite non avevano perdite.
* Conversione formato browser (`bfc`)
* Proporzioni pixel dispositivo (`dpr`)
* Larghezza di banda di rete (`network`)

### Informazioni sulla conversione formato browser (bfc) {#bfc}

Attivando la conversione del formato del browser aggiungendo `bfc=on` all&#39;URL dell&#39;immagine, JPEG e PNG vengono automaticamente convertiti in file AVIF con perdita di dati, WebP con perdita di dati, JPEGXR con perdita di dati, JPEG2000 con perdita di dati per browser diversi. Per i browser che non supportano tali formati, la tecnologia Smart Imaging continua a essere utilizzata come JPEG o PNG. Smart Imaging ricalcola la qualità del nuovo formato insieme alla modifica del formato.

Per disattivare Smart Imaging, aggiungi `bfc=off` all&#39;URL dell&#39;immagine.

Vedere anche [bfc](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc) nell&#39;API di server e rendering immagini Dynamic Medie.

### Informazioni sull&#39;ottimizzazione del rapporto pixel del dispositivo (dpr) {#dpr}

DPR (Device Pixel Ratio), noto anche come CSS Pixel Ratio (Rapporto pixel CSS), rappresenta la relazione tra i pixel fisici di un dispositivo e i pixel logici. Con l&#39;aumento dei display retina, la risoluzione dei pixel dei dispositivi mobili moderni è in rapido aumento.

Attivando l&#39;ottimizzazione del rapporto pixel del dispositivo, l&#39;immagine viene riprodotta alla risoluzione nativa dello schermo, rendendola più nitida.

Attualmente, la densità di pixel della visualizzazione proviene dai valori di intestazione della rete CDN di Akamai.

| Valori consentiti nell’URL di un’immagine | Descrizione |
|---|---|
| `dpr=off` | Disattiva l’ottimizzazione DPR a livello di singolo URL immagine. |
| `dpr=on,dprValue` | Sostituisci il valore DPR rilevato da Smart Imaging con un valore personalizzato (rilevato da qualsiasi logica lato client o in altro modo). Il valore consentito per `dprValue` è un numero qualsiasi maggiore di 0. |

>[!NOTE]
>
>* È possibile utilizzare `dpr=on,dprValue` anche se l&#39;impostazione DPR a livello aziendale è disattivata.
>* A causa dell&#39;ottimizzazione DPR, quando l&#39;immagine risultante è maggiore dell&#39;impostazione MaxPix Dynamic Medie, la larghezza MaxPix viene sempre riconosciuta mantenendo le proporzioni dell&#39;immagine.

| Dimensione immagine richiesta | Valore rapporto pixel dispositivo (dpr) | Dimensioni immagine consegnata |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Vedi anche [Quando lavori con le immagini](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Quando lavori con Ritaglio avanzato](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Informazioni sull&#39;ottimizzazione della larghezza di banda di rete {#network}

L&#39;attivazione della larghezza di banda consente di regolare automaticamente la qualità dell&#39;immagine trasmessa in base all&#39;effettiva larghezza di banda della rete. In caso di larghezza di banda insufficiente, l&#39;ottimizzazione DPR (Device Pixel Ratio) viene automaticamente disattivata, anche se è già attiva.

La tua azienda può disabilitare l&#39;ottimizzazione della larghezza di banda di rete per singole immagini aggiungendo `network=off` all&#39;URL dell&#39;immagine.

| Valore consentito nell’URL di un’immagine | Descrizione |
|---|---|
| `network=off` | Disattiva l&#39;ottimizzazione della rete a livello di singolo URL immagine. |

I valori di DPR e larghezza di banda di rete si basano sui valori lato client rilevati per la rete CDN in bundle. Questi valori a volte sono imprecisi. Ad esempio, iPhone5 con DPR=2 e iPhone12 con `dpr=3`, entrambi mostrano `dpr=2`. Tuttavia, per i dispositivi ad alta risoluzione, l&#39;invio di `dpr=2` è migliore rispetto all&#39;invio di `dpr=1`. Il modo migliore per superare questa imprecisione, tuttavia, è utilizzare il DPR lato client per fornire valori accurati al 100%. E funziona per qualsiasi dispositivo, sia esso Apple o qualsiasi altro dispositivo che è stato lanciato. Vedi [Utilizzare Smart Imaging con le proporzioni pixel del dispositivo lato client](/help/assets/client-side-dpr.md).

### Vantaggi chiave aggiuntivi della tecnologia Smart Imaging

* È stata migliorata la classificazione SEO di Google per le pagine web che utilizzano l’imaging avanzato più recente.
* Distribuisce immediatamente il contenuto ottimizzato (in fase di runtime).
* Utilizza la tecnologia Adobe Sensei per la conversione in base alla qualità (`qlt`) specificata nella richiesta di immagine.
* TTL (Time To Live) indipendente. In precedenza, era obbligatorio un TTL minimo di 12 ore affinché l’imaging intelligente potesse funzionare.
* In precedenza, le immagini originali e derivate venivano memorizzate nella cache ed era un processo in due fasi per invalidare la cache. Nell’ultima versione di Smart Imaging, vengono memorizzate nella cache solo le derivate, consentendo un processo di invalidamento della cache in un unico passaggio.
* I clienti che utilizzano intestazioni personalizzate nei propri set di regole beneficiano della tecnologia Smart Imaging più recente, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart Imaging. &quot;Timing Allow Origin&quot; e &quot;X-Robot&quot;, ad esempio, come suggerito in [Aggiungere un valore di intestazione personalizzato alle risposte dell&#39;immagine|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Domande frequenti

+++Esistono costi di licenza associati all&#39;imaging avanzato?

No. Smart Imaging è incluso nella licenza esistente. Questa regola è valida per Dynamic Media Classic o Experience Manager - Dynamic Medie (on-prem, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>Smart Imaging non è disponibile per i clienti Dynamic Medie - Hybrid.

+++

+++Come funziona l&#39;imaging avanzato?

Quando un consumatore richiede un’immagine, la tecnologia Smart Imaging ne analizza le caratteristiche e la converte nel formato appropriato in base al browser. Queste conversioni di formato vengono eseguite in modo da non compromettere la fedeltà visiva. La tecnologia Smart Imaging converte automaticamente le immagini in diversi formati in base alla funzionalità del browser, nel modo seguente.

* Converti automaticamente in AVIF se il browser supporta il formato
* Converti automaticamente in WebP se la conversione AVIF non è stata utile o se il browser non supporta AVIF
* Converti automaticamente in JPEG2000 se Safari non supporta WebP
* Converti automaticamente in JPEGXR per IE 9+ o se Edge non supporta WebP

  | Formato immagine | Browser supportati |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGX | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* Per i browser che non supportano questi formati, viene fornito il formato immagine richiesto originariamente.

Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart Imaging, viene distribuita l&#39;immagine originale.

+++

+++Quali formati di immagine sono supportati?

Per la creazione di immagini avanzate sono supportati i seguenti formati di immagine:

* JPEG
* PNG

La funzione Smart Imaging ricalcola la qualità dei formati di file immagine JPEG durante la conversione in un nuovo formato.

Per i formati di file di immagine che supportano la trasparenza come PNG, puoi configurare Smart Imaging per fornire file AVIF e WebP con perdita di dati. Per la conversione di formato con perdita di dati, Smart Imaging utilizza la qualità indicata nell’URL dell’immagine oppure la qualità configurata nell’account aziendale di Dynamic Medie.

+++

+++Come funziona la tecnologia Smart Imaging con i predefiniti immagine esistenti già in uso?

Smart Imaging si integra perfettamente con i predefiniti immagine esistenti, rispettando tutte le impostazioni immagine.

Le uniche regolazioni riguardano il formato dell&#39;immagine, la qualità o entrambi. Durante la conversione del formato, la tecnologia Smart Imaging mantiene la fedeltà visiva totale in base alle impostazioni predefinite, ma offre un file di dimensioni inferiori. È sufficiente abilitarlo aggiungendo `bfc=on`, o `dpr=on,dprValue`, o `network=on`, oppure tutte e tre le impostazioni dei parametri agli URL o ai predefiniti esistenti.

Supponiamo ad esempio che un predefinito immagine specifichi un formato JPEG di 500 × 500 pixel, con `quality=85` e `unsharp mask=0.1,1,5`. Smart Imaging rileva se l’utente si trova su un browser Chrome. Quindi converte l&#39;immagine in WebP con le stesse dimensioni (500 × 500) e una maschera di contrasto corrispondente alle impostazioni del JPEG. Vengono quindi confrontate le dimensioni dei file delle versioni WebP e JPEG e viene distribuita all&#39;utente la versione più piccola.

+++

<!--

### Do I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? 

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++Smart Imaging funziona con HTTPS? E HTTP/2?

La tecnologia Smart Imaging funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

+++

+++Posso utilizzare l’imaging avanzato?

Smart Imaging è disponibile immediatamente per tutti i clienti. Per iniziare a usufruire dei vantaggi, aggiungi `bfc=on`, `dpr=on,dprValue` o `network=on` oppure tutte e tre le impostazioni dei parametri agli URL o ai predefiniti esistenti.

Per utilizzare Smart Imaging, l’account Dynamic Media Classic o Dynamic Medie dell’azienda su Experience Manager deve includere nell’ambito della licenza la rete CDN (Content Delivery Network) inclusa nell’Adobe.

+++

+++Qual è il processo per abilitare Smart Imaging per un account?

Per iniziare a utilizzare Smart Imaging, aggiungi `bfc=on`, o `dpr=on,dprValue`, o `network=on`, oppure tutte e tre le impostazioni dei parametri agli URL o ai predefiniti esistenti. Se preferisci non apportare queste modifiche manualmente, puoi abilitare Smart Imaging per impostazione predefinita creando un caso di supporto.

Quando crei il caso di supporto, specifica le funzioni di Smart Imaging da attivare sul tuo account:

* Conversione formato browser (WebP o AVIF)
* Ottimizzazione della larghezza di banda di rete

>[!NOTE]
>
>DPR richiede modifiche lato client per determinare il `dprValue` corretto. Pertanto, l&#39;Adobe consiglia di abilitare DPR tramite gli URL aggiungendo `dpr=on,dprValue`.

**Per creare un caso di supporto per abilitare Smart Imaging sul tuo account:**

1. [Utilizzare l&#39;Admin Console per avviare la creazione di un nuovo caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * **Dettagli contatto principale:**

      * Immetti nome, e-mail e numero di telefono.

   * **Funzionalità Smart Imaging da abilitare:**

      * Elencare le funzionalità desiderate per l&#39;account:

         * Conversione formato browser: WebP o AVIF
         * Ottimizzazione della larghezza di banda di rete
         * DPR: DPR richiede adeguamenti lato client per determinare il `dprValue` corretto. Pertanto, l&#39;Adobe consiglia di abilitare DPR tramite gli URL aggiungendo `dpr=on,dprValue`.

   * **Dominio per Smart Imaging:**

      * Elenca tutti i domini rilevanti, ad esempio *`company.com`* o *`mycompany.scene7.com`*
      * Smart Imaging supporta domini sia generici che personalizzati.
      * Per identificare i domini, apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started) e accedi al tuo account aziendale.

         1. Passa a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**.
         1. Cerca il campo **[!UICONTROL Nome server pubblicato]** per confermare il dominio.
         1. Verifica di utilizzare la rete CDN di Adobe anziché una rete gestita da un altro provider.

   * **Indicare il supporto HTTP/2:**

      * Specifica se è necessario Smart Imaging per funzionare su HTTP/2.

1. L’Assistenza clienti Adobe abilita le funzioni di Smart Imaging richieste per impostazione predefinita, eliminando la necessità di aggiungere manualmente i parametri agli URL.
1. L’Adobe consiglia di impostare il valore TTL (Time To Live) su almeno 24 ore per massimizzare le prestazioni tramite la memorizzazione in cache.
Per regolare il valore TTL:

   1. **Per Dynamic Media Classic:**
      1. Passa a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Installazione di Publish]** > **[!UICONTROL Server immagini]**.
      1. Imposta il valore **[!UICONTROL Durata predefinita cache client]** su 24 ore o più.
   1. **Per Dynamic Medie su Adobe Experience Manager:**
      1. Segui [queste istruzioni](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab).
      1. Imposta il valore **[!UICONTROL Scadenza]** per 24 ore o più.

+++

+++Quando è possibile prevedere che un account sia abilitato con Smart Imaging?

L’Assistenza clienti elabora le richieste nell’ordine in cui vengono ricevute, seguendo la Lista d’attesa.

>[!NOTE]
>
>Il lead time può essere lungo perché l’abilitazione di Smart Imaging richiede la cancellazione della cache da parte di un Adobe. Pertanto, è possibile gestire solo poche transizioni cliente in un dato momento.

+++

+++Quali rischi comporta il passaggio all&#39;uso di Smart Imaging?

Non esiste alcun rischio per una pagina web del cliente. Tuttavia, la transizione a Smart Imaging elimina la cache CDN. Questa operazione comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Medie su Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate in cache hanno colpito direttamente i server di origine di Adobe fino a quando la cache non viene nuovamente generata. Adobe prevede quindi di gestire alcune transizioni cliente alla volta in modo da mantenere prestazioni accettabili durante il richiamo delle richieste dall’origine. Per la maggior parte dei clienti, la cache è completamente integrata di nuovo nella rete CDN entro circa 1-2 giorni.

+++

+++Come posso verificare se Smart Imaging funziona come previsto?

1. Dopo aver configurato l’account con Smart Imaging, carica un URL immagine Dynamic Media Classic o Adobe Experience Manager - Dynamic Medie nel browser.
1. Apri il riquadro per sviluppatori di Chrome andando in **[!UICONTROL Visualizza]** > **[!UICONTROL Sviluppatore]** > **[!UICONTROL Strumenti per sviluppatori]** nel browser. In alternativa, scegli uno degli strumenti di sviluppo del browser desiderato.

1. Assicurati che la cache sia disabilitata quando gli strumenti di sviluppo sono aperti.

   * In Windows®, passare alle impostazioni nel riquadro Strumenti sviluppatore, quindi selezionare la casella di controllo **[!UICONTROL Disattiva cache (mentre devtools è aperto)]**.
   * In macOS, nel riquadro Sviluppatore, nella scheda **[!UICONTROL Rete]**, selezionare **[!UICONTROL Disabilita cache]**.

1. Osserva che il Tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un’immagine PNG convertita dinamicamente in WebP su Chrome. Se nel dominio è abilitato AVIF, è anche possibile prevedere di visualizzare AVIF nel Tipo di contenuto.
1. Ripeti questo test su diversi browser e condizioni utente.

>[!NOTE]
>
>Non tutte le immagini vengono convertite. L&#39;imaging intelligente decide se la conversione può migliorare le prestazioni. Talvolta, se non è previsto alcun miglioramento delle prestazioni o se il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![immagine2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

+++

+++Come posso conoscere il miglioramento delle prestazioni? Esiste un modo per conoscere i vantaggi della tecnologia Smart Imaging?

L’intestazione Smart Imaging determina i vantaggi della tecnologia Smart Imaging. Quando Smart Imaging è abilitato, dopo aver richiesto un&#39;immagine, sotto l&#39;intestazione **[!UICONTROL Intestazioni di risposta]** puoi visualizzare `-X-Adobe-Smart-Imaging` come mostrato nell&#39;esempio seguente:

![Intestazione Smart Imaging](/help/assets/assets-dm/smart-imaging-header2.png)

Questa intestazione indica quanto segue:

* Smart Imaging funziona per l’azienda.
* Un valore positivo indica che la conversione è riuscita. In questo caso, viene restituita una nuova immagine WebP.
* Un valore negativo indica che la conversione non ha esito positivo. In tal caso, viene restituita l’immagine richiesta originale (JPEG per impostazione predefinita, se non specificata).
* Un valore positivo mostra la differenza in byte tra l’immagine richiesta e la nuova immagine. Nell&#39;esempio precedente, i byte salvati sono `75048` o circa 75 KB per un&#39;immagine.
* Un valore negativo indica che l’immagine richiesta è più piccola della nuova immagine. Viene visualizzata la differenza di dimensione negativa, ma l’immagine trasmessa è solo l’immagine originale richiesta.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 con WebP consegnato**
>
>Se il valore di `X-Adobe-Smart-Imaging` è -1 e WebP è ancora in fase di distribuzione, Smart Imaging è attivo. Tuttavia, i vantaggi in termini di dimensioni non sono stati calcolati a causa di una cache obsoleta. Per risolvere il problema, è possibile utilizzare `cache=update` (una sola volta) nell&#39;URL dell&#39;immagine.
>Esempio di utilizzo del modificatore:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Per invalidare l’intera cache, è necessario creare un caso di supporto.

+++

+++Come posso disabilitare l’ottimizzazione AVIF in Smart Imaging?

Se si desidera tornare al WebP in servizio per impostazione predefinita, creare un caso di supporto per lo stesso. Come sempre, è possibile disattivare Smart Imaging aggiungendo il parametro `bfc=off` all&#39;URL dell&#39;immagine. Tuttavia, non è possibile selezionare WebP o AVIF nel modificatore URL per Smart Imaging. Questa funzionalità viene mantenuta a livello di account aziendale.

+++

+++È possibile disattivare Smart Imaging per qualsiasi richiesta?

Sì. È possibile disattivare Smart Imaging aggiungendo uno dei seguenti modificatori:

* `bfc=off` per disattivare la conversione del formato browser. Vedere anche [Conversione formato browser](#bfc).
* `dpr=off` per disattivare le proporzioni pixel del dispositivo. Vedere anche [Rapporto pixel dispositivo](#dpr).
* `network=off` per disattivare la larghezza di banda di rete. Vedere anche [Larghezza di banda](#network).

+++

+++Quale &quot;messa a punto&quot; è disponibile? È possibile definire impostazioni o comportamenti?

Smart Imaging dispone di tre opzioni che è possibile abilitare o disabilitare.

* [Conversione formato browser](#bfc)
* [Proporzioni pixel dispositivo](#dpr)
* [Larghezza di banda di rete](#network)

+++

+++Ho un URL con fmt=tif nel browser Web Chrome. Tuttavia, la richiesta non riesce e viene restituito un errore ImageServer. Perché?

Questo errore non si verifica se Smart Imaging non è abilitato sul tuo account. Smart Imaging funziona solo con i formati JPEG o PNG.

Per evitare questo errore, puoi effettuare le seguenti operazioni:

* Specificare JPEG o PNG oppure
* Non utilizzare il modificatore `fmt`, oppure
* Utilizza un formato preferito dal browser e definito da Smart Imaging. È ad esempio possibile utilizzare WebP per il browser Web Chrome.

+++

+++Desidero scaricare un’immagine TIFF dall’URL di un’immagine. Come lo faccio?

Aggiungi `fmt=tif` e `bfc=off` al percorso URL dell&#39;immagine.

+++

+++Smart Imaging gestisce solo il formato dell&#39;immagine o gestisce anche le impostazioni di qualità dell&#39;immagine per ottenere risultati ottimali?

La tecnologia Smart Imaging utilizza sia il formato che la qualità. Gli altri parametri rimangono invariati, se richiesto nell’URL dell’immagine.

+++

+++Se Smart Imaging gestisce le impostazioni di qualità, è possibile impostare valori minimi e massimi? In altre parole, una qualità non inferiore a 60 e non superiore a 80?

Attualmente non esiste un provisioning di questo tipo.

+++

+++Smart Imaging regola automaticamente l&#39;impostazione di qualità percentuale dell&#39;output o è un&#39;impostazione che viene regolata manualmente e si applica a tutte le immagini? Entro quale intervallo?

La tecnologia Smart Imaging regola automaticamente la percentuale di qualità. Questa qualità è determinata utilizzando un algoritmo di machine learning sviluppato da Adobe. Questa percentuale non è specifica per l&#39;intervallo.

+++

+++Con Smart Imaging, quali comandi Image Server sono supportati o ignorati?

Gli unici comandi ignorati sono `fmt` e `qlt`. Sono supportati tutti i comandi rimanenti.

+++

+++Solo le immagini JPEG vengono sostituite da Smart Imaging? Cosa succede se si richiede un WebP, un PNG o altro?

Questa funzionalità funziona solo per JPEG e PNG.

+++

+++Perché a volte un&#39;immagine JPEG viene restituita a Chrome invece che a WebP?

La tecnologia Smart Imaging determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione è utile.

+++

+++Perché la funzionalità Device Pixel Ratio (dpr) non funziona come previsto con le immagini composite?

Se un&#39;immagine composita coinvolge troppi livelli, la funzionalità dpr potrebbe essere interessata durante l&#39;utilizzo di un modificatore di posizione. Questo problema è noto e dovrebbe essere risolto nelle versioni future di Smart Imaging. Se altre funzionalità di Smart Imaging non funzionano come previsto, puoi creare un caso di supporto per segnalare il problema.

+++

+++Perché Smart Imaging PNG viene ancora convertito in WebP/AVIF senza perdita di dati?

Poiché il PNG è un formato senza perdita di dati, le versioni precedenti di WebP e AVIF consegnate non presentavano perdita di dati, con il risultato di dimensioni superiori al previsto. La tecnologia Smart Imaging ora supporta la conversione con perdita di dati. Per risolvere il problema, è possibile utilizzare il modificatore `cache=update` (una sola volta) in una richiesta di immagine. Esempio di utilizzo del modificatore:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Per invalidare l’intera cache, devi creare un caso di supporto che richieda tale impegno.

+++

+++Come posso continuare a utilizzare il PNG per una conversione senza perdite in Smart Imaging?

La tecnologia Smart Imaging ora supporta la conversione con perdita di dati in base al livello di qualità. Puoi continuare a utilizzare la conversione senza perdita impostando la qualità su 100, tramite le impostazioni della tua società o aggiungendo `qlt=100` al percorso URL dell&#39;immagine.

+++

