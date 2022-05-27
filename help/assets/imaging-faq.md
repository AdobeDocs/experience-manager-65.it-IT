---
title: Imaging avanzato
description: La funzione Smart imaging applica le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, garantendo prestazioni e coinvolgimento migliori.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 9b02a5363d32771cd9c039f97044e8a1d72fe286
workflow-type: tm+mt
source-wordcount: '3518'
ht-degree: 1%

---

# Imaging avanzato {#smart-imaging}

## Cos’è l’imaging intelligente? {#what-is-smart-imaging}

La tecnologia Smart Imaging applica le funzionalità di Adobe Sensei AI e funziona con i &quot;predefiniti immagine&quot; esistenti. Funziona per migliorare le prestazioni di distribuzione delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

E ora, ottenere un punteggio migliore Google Core Web Vital per LCP (Paint più grande contentful) con Smart imaging migliorato che ora viene fornito con supporto sia AVIF che WebP.

>[!IMPORTANT]
>
>L’imaging avanzato richiede l’utilizzo della rete CDN preconfigurata (Content Delivery Network) fornita in bundle con Adobe Experience Manager - Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

La funzione Smart imaging sfrutta l’aumento delle prestazioni in aggiunta, grazie all’integrazione completa con il servizio premium CDN (Content Delivery Network) di Adobe. Questo servizio trova il percorso Internet ottimale tra server, reti e punti di peer. Trova un percorso che ha la latenza più bassa e la velocità di perdita più bassa del pacchetto invece di utilizzare il percorso predefinito su Internet.

Gli esempi di risorse immagine seguenti illustrano l’ottimizzazione Smart Imaging aggiunta:

| Immagine (URL) | Miniatura  | Dimensioni (JPEG) | Dimensioni (WebP) con Smart imaging | Dimensioni (AVIF) con Smart imaging | Riduzione del % con WebP | Riduzione del % con AVIF |
|---|---|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26,89% | 37,79% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01% | 72,57% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14,47% | 60,58% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25% | 51,85% |

Simile a quanto sopra, l’Adobe ha anche eseguito un test con un set di campioni più grande. Il formato AVIF ha fornito una riduzione del 20% in più rispetto a WebP, che ha fornito una riduzione del 27% rispetto a JPEG. Tutte con la stessa qualità visiva. In totale, l&#39;AVIF fornisce una riduzione media delle dimensioni fino al 41% rispetto alla JPEG.

Confronta WebP e AVIF con PNG, si può vedere una riduzione delle dimensioni dell&#39;84% con WebP e 87% con AVIF. Inoltre, poiché sia i formati WebP che AVIF supportano la trasparenza e più animazioni delle immagini, è una buona sostituzione per i file PNG e GIF trasparenti.

Vedi anche [Ottimizzazione delle immagini con formati di immagine di nuova generazione (WebP e AVIF)](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Quali sono i vantaggi principali dell&#39;ultima generazione di Smart imaging? {#what-are-the-key-benefits-of-smart-imaging}

La funzione Smart imaging migliora le prestazioni di distribuzione delle immagini ottimizzando automaticamente le dimensioni dei file immagine in base al browser utilizzato, alle condizioni di visualizzazione e di rete del dispositivo. Poiché le immagini costituiscono la maggior parte del tempo di caricamento di una pagina, qualsiasi miglioramento delle prestazioni può avere un impatto profondo sui KPI aziendali, come tassi di conversione più elevati, tempo trascorso su un sito e tassi di mancato recapito del sito più bassi.

Gli ultimi vantaggi principali dell&#39;ultima generazione di Smart imaging includono:

* Ora supporta il formato AVIF di nuova generazione.
* Da PNG a WebP e AVIF ora supporta la conversione con perdita di dati. Poiché PNG è un formato senza perdita di dati, il WebP e l&#39;AVIF precedenti che vengono consegnati erano senza perdita di dati.
* Conversione del formato del browser (`bfc`)
* Rapporto pixel dispositivo (`dpr`)
* Larghezza di banda della rete (`network`)

### Informazioni sulla conversione del formato browser (bfc) {#bfc}

Attivare la conversione del formato del browser aggiungendo `bfc=on` all&#39;URL dell&#39;immagine converte automaticamente JPEG e PNG in AVIF con perdita, WebP con perdita, JPEGXR con perdita, JPEG2000 con perdita per diversi browser. Per i browser che non supportano tali formati, Smart imaging continua a servire JPEG o PNG. Insieme al formato, la qualità del nuovo formato viene ricalcolata da Smart imaging.

L&#39;aggiunta di Smart imaging può anche essere disattivata `bfc=off` all’URL dell’immagine.

Vedi anche [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) nell’API di Dynamic Media Image Server e Rendering .

### Ottimizzazione del rapporto pixel del dispositivo (dpr) {#dpr}

Rapporto pixel del dispositivo (DPR) - noto anche come rapporto pixel CSS - è la relazione tra i pixel fisici di un dispositivo e i pixel logici. Soprattutto con l&#39;avvento degli schermi Retina, la risoluzione dei pixel dei moderni dispositivi mobili sta crescendo a un ritmo veloce.

Attivando l&#39;ottimizzazione del rapporto pixel del dispositivo, l&#39;immagine viene riprodotta alla risoluzione nativa dello schermo, rendendo più nitida l&#39;immagine.

Attualmente, la densità di pixel del display proviene dai valori di intestazione CDN di Akamai.

| Valori consentiti nell’URL di un’immagine | Descrizione |
|---|---|
| `dpr=off` | Disattiva l’ottimizzazione DPR a livello di singolo URL immagine. |
| `dpr=on,dprValue` | Sostituisci il valore DPR rilevato da Smart Imaging con un valore personalizzato (rilevato da qualsiasi logica lato client o con altri metodi). Valore consentito per `dprValue` è un numero qualsiasi maggiore di 0. |

>[!NOTE]
>
>* È possibile utilizzare `dpr=on,dprValue` anche se l’impostazione DPR a livello aziendale è disattivata.
>* Grazie all’ottimizzazione DPR, quando l’immagine risultante è maggiore dell’impostazione MaxPix Dynamic Media, la larghezza MaxPix viene sempre riconosciuta mantenendo le proporzioni dell’immagine.


| Dimensioni immagine richieste | Valore DPR (Device Pixel Ratio) | Dimensione dell&#39;immagine |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Vedi anche [Quando si lavora con le immagini](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Quando si lavora con Smart Crop](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Informazioni sull’ottimizzazione della larghezza di banda di rete {#network}

L&#39;attivazione della larghezza di banda della rete regola automaticamente la qualità dell&#39;immagine fornita in base all&#39;effettiva larghezza di banda della rete. Per una larghezza di banda di rete ridotta, l&#39;ottimizzazione DPR (Device Pixel Ratio) viene automaticamente disattivata, anche se è già attiva.

Se lo desideri, la tua azienda può rinunciare all&#39;ottimizzazione della larghezza di banda di rete a livello delle singole immagini aggiungendo `network=off` all’URL dell’immagine.

| Valore consentito nell’URL di un’immagine | Descrizione |
|---|---|
| `network=off` | Disattiva l&#39;ottimizzazione della rete a livello di singolo URL immagine. |

I valori DPR e della larghezza di banda di rete si basano sui valori rilevati lato client della rete CDN inclusa nel pacchetto. Questi valori a volte sono imprecisi. Ad esempio, iPhone5 con DPR=2 e iPhone12 con `dpr=3`, entrambi `dpr=2`. Still, per dispositivi ad alta risoluzione, invio `dpr=2` è migliore dell’invio `dpr=1`. Il modo migliore per superare questa imprecisione, tuttavia, è utilizzare il DPR lato client per fornire valori precisi al 100%. Funziona per qualsiasi dispositivo, sia che si tratti di Apple o di qualsiasi altro dispositivo avviato. Vedi [Utilizzare l’imaging intelligente con il rapporto pixel del dispositivo lato client](/help/assets/client-side-dpr.md).

### Ulteriori vantaggi chiave dell&#39;imaging intelligente

* È stata migliorata la classificazione SEO di Google per le pagine web che utilizzano l’immagine avanzata più recente.
* Distribuisce immediatamente il contenuto ottimizzato (in fase di runtime).
* Utilizza la tecnologia Adobe Sensei per convertire in base alla qualità (`qlt`) specificata nella richiesta di immagine.
* TTL (Time To Live) indipendente. Precedentemente, per il funzionamento di Smart imaging era obbligatorio un TTL minimo di 12 ore.
* Precedentemente, sia le immagini originali che quelle derivate venivano memorizzate nella cache ed era un processo in due fasi per annullare la validità della cache. Nell’ultimo Smart imaging, solo i derivati vengono memorizzati nella cache, consentendo un processo di invalidazione della cache a un solo passaggio.
* I clienti che utilizzano intestazioni personalizzate nel loro set di regole beneficiano dell’ultima Smart imaging, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart imaging. Ad esempio, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot; come suggerito in [Aggiungi un valore di intestazione personalizzato alle risposte alle immagini|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Sono presenti costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. Smart imaging è incluso nella licenza esistente. Questa regola è valida per Dynamic Media Classic o Experience Manager - Dynamic Media (On-Prem, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>La funzione Smart imaging non è disponibile per i clienti ibridi di Dynamic Media.

## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Quando un&#39;immagine viene richiesta da un consumatore, Smart imaging controlla le caratteristiche dell&#39;utente e la conversione nel formato immagine appropriato in base al browser in uso. Queste conversioni di formato vengono effettuate in modo da non compromettere la fedeltà visiva. La funzione Smart imaging converte automaticamente le immagini in formati diversi in base alla funzionalità del browser nel modo seguente.

* Converti automaticamente in AVIF se il browser supporta il formato
* Converti automaticamente in WebP se la conversione AVIF non è vantaggiosa o il browser non supporta AVIF
* Converti automaticamente in JPEG2000 se Safari non supporta WebP
* Converti automaticamente in JPEGXR per IE 9+ o se Edge non supporta WebP\
   | Formato immagine | Browser supportati | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* Per i browser che non supportano questi formati, viene distribuito il formato immagine richiesto originariamente.

Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart imaging, l&#39;immagine originale viene servita.

## Quali formati immagine sono supportati? {#what-image-formats-are-supported}

I seguenti formati immagine sono supportati per Smart imaging:

* JPEG
* PNG

Per il formato di file immagine di JPEG, la qualità del nuovo formato viene ricalcolata mediante Smart imaging.

Per i formati di file immagine che supportano la trasparenza come PNG, è possibile configurare Smart imaging per fornire AVIF e WebP con perdita di dati. Per la conversione del formato con perdita di dati, Smart imaging utilizza la qualità indicata nell’URL dell’immagine o la qualità configurata nell’account aziendale Dynamic Media.

## Come funziona l’imaging avanzato con i miei predefiniti immagine esistenti già in uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart imaging funziona con i predefiniti per immagini esistenti ed osserva tutte le impostazioni delle immagini. Ciò che cambia è il formato dell&#39;immagine, l&#39;impostazione della qualità, o entrambi. Per la conversione del formato, l&#39;imaging intelligente mantiene la fedeltà visiva completa, come definita dalle impostazioni del predefinito per immagini, ma con dimensioni file inferiori.

Ad esempio, supponiamo che un predefinito per immagini sia definito con formato JPEG, dimensioni 500 x 500, qualità=85 e maschera di contrasto=0.1,1,5. Quando Smart imaging rileva che un utente si trova su un browser Chrome, l&#39;immagine viene convertita in formato WebP, con dimensioni 500 x 500 e maschera di contrasto=0.1,1,5 a una qualità WebP che corrisponde a una qualità JPEG di 85 il più vicino possibile. L&#39;impronta di tale conversione WebP viene confrontata con il JPEG e viene restituito il minore dei due.

## Devo modificare URL, predefiniti per immagini o distribuire un nuovo codice sul mio sito per Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

No. La funzione Smart imaging funziona perfettamente con gli URL delle immagini esistenti e con i predefiniti per immagini. Inoltre, Smart imaging non richiede di aggiungere codice al sito web per rilevare il browser di un utente. Tutte queste funzionalità vengono gestite automaticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## L’imaging avanzato funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart imaging funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Posso utilizzare le Smart imaging? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare Smart imaging, l’account Dynamic Media Classic o Dynamic Media della tua azienda deve soddisfare i seguenti requisiti:

* Utilizza la rete CDN (Content Delivery Network) in bundle Adobe come parte della tua licenza.
* Utilizza un dominio dedicato (ad esempio, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com`oppure `s7d13.scene7.com`).

Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**. Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**. Se al momento utilizzi un dominio generico, puoi richiedere di passare al dominio personalizzato. Esegui questa richiesta di transizione quando invii un caso di assistenza.

Il tuo primo dominio personalizzato non comporta costi aggiuntivi con una licenza Dynamic Media.

## Qual è il processo per abilitare Smart imaging per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Avviare una richiesta per utilizzare Smart imaging; non è abilitato automaticamente.

Crea un caso di assistenza come descritto di seguito. Nel tuo caso di assistenza, assicurati di indicare quali delle seguenti funzionalità di Smart imaging (una o più) vuoi abilitare sul tuo account:

* WebP
* AVIF
* Ottimizzazione di DPR e larghezza di banda di rete
* PNG a AVIF con perdita o webP con perdita

Se l&#39;opzione Smart imaging è già abilitata con WebP ma desideri utilizzare altre funzionalità come indicato in precedenza, devi creare un caso di supporto.

**Per creare un caso di supporto per abilitare Smart imaging sul tuo account:**

1. [Utilizza l’Admin Console per avviare la creazione di un nuovo caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Nome contatto principale, e-mail, telefono.

   * Elenca le funzionalità di Smart imaging seguenti (una o più) che desideri abilitare sul tuo account:
      * WebP
      * AVIF
      * Ottimizzazione di DPR e larghezza di banda di rete
      * PNG a AVIF con perdita o webP con perdita
   * Tutti i domini da abilitare per l’imaging intelligente (ovvero, `images.company.com` o `mycompany.scene7.com`).

      Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**.

   * Verifica di utilizzare la CDN tramite Adobe e di non gestirla con una relazione diretta.

   * Verifica di utilizzare un dominio dedicato come `images.company.com` o `mycompany.scene7.com`e non un dominio generico come `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i tuoi domini, apri le [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendale.

      Vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

      Cerca il campo contrassegnato **[!UICONTROL Nome server pubblicato]**. Se utilizzi un dominio Dynamic Media Classic generico, puoi richiedere il passaggio al dominio personalizzato come parte di questa transizione.

   * Indica se desideri che funzioni su HTTP/2.


1. L’Assistenza clienti di Adobe ti aggiunge all’Elenco di attesa clienti di Smart imaging in base all’ordine in cui vengono inviate le richieste.
1. Quando Adobe è pronto per gestire la richiesta, l&#39;Assistenza clienti ti contatta per coordinare e impostare una data di destinazione.
1. **Facoltativo**: Facoltativamente, puoi testare l’imaging avanzato nell’ambiente di staging prima che Adobe introduca la nuova funzione in produzione.
1. Dopo il completamento dell’attività, riceverai una notifica dall’Assistenza clienti.
1. Per ottimizzare le prestazioni dell’imaging avanzato, Adobe consiglia di impostare il valore TTL (Time To Live) a 24 ore o più. Il TTL definisce per quanto tempo le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzi Dynamic Media Classic, vai a **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Pubblica installazione]** > **[!UICONTROL Server immagini]**. Imposta la **[!UICONTROL Durata predefinita cache client]** a 24 o più.
   1. Se utilizzi Dynamic Media, segui [queste istruzioni](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). Imposta la **[!UICONTROL Scadenza]** 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con Smart imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti, in base all’Elenco di attesa.

>[!NOTE]
>
>Ci può essere un lungo tempo di lead perché l’abilitazione di Smart imaging comporta ad Adobe la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni dei clienti in un dato momento.

## Quali sono i rischi connessi al passaggio all’app per l’utilizzo di Smart imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Non vi è alcun rischio per una pagina web del cliente. Tuttavia, la transizione a Smart imaging cancella la cache CDN. Questa operazione comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media all’Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate nella cache colpiscono direttamente i server di origine di Adobe fino a quando la cache non viene ricostruita nuovamente. Di conseguenza, Adobe prevede di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili durante l’estrazione delle richieste dall’origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente nella rete CDN entro circa 1 - 2 giorni.

## Come posso verificare se l’imaging intelligente funziona come previsto?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato il tuo account con Smart imaging, carica un URL immagine Dynamic Media Classic o Adobe Experience Manager - Dynamic Media sul browser.
1. Apri il riquadro per sviluppatori di Chrome andando in **[!UICONTROL Visualizza]** > **[!UICONTROL Sviluppatore]** > **[!UICONTROL Strumenti per gli sviluppatori]** nel browser. Oppure, scegli uno strumento per sviluppatori di browser a tua scelta.

1. Assicurati che la cache sia disabilitata quando gli strumenti per sviluppatori sono aperti.

   * In Windows®, passare alle impostazioni nel riquadro degli strumenti per sviluppatori, quindi selezionare **[!UICONTROL Disattiva la cache (mentre devtools è aperto)]** casella di controllo.
   * In macOS, nel riquadro dello sviluppatore, sotto la sezione **[!UICONTROL Rete]** scheda , seleziona **[!UICONTROL disattiva cache]**.

1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un&#39;immagine PNG convertita dinamicamente in WebP su Chrome. Se il dominio ha abilitato AVIF, puoi anche aspettarti di visualizzare AVIF in Content Type (Tipo di contenuto).
1. Ripeti questo test su diversi browser e condizioni utente.

>[!NOTE]
>
>Non tutte le immagini vengono convertite. L’imaging intelligente decide se la conversione può migliorare le prestazioni. A volte, quando non si prevede alcun guadagno di prestazioni o il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## Come faccio a conoscere l&#39;aumento delle prestazioni? Esiste un modo per conoscere i vantaggi dell&#39;imaging intelligente? {#benefits}

L’intestazione Smart imaging determina i vantaggi dell’imaging intelligente. Quando l&#39;immagine avanzata è abilitata, dopo aver richiesto un&#39;immagine, sotto la sezione **[!UICONTROL Intestazioni di risposta]** intestazione, potete vedere `-X-Adobe-Smart-Imaging` come mostrato nell&#39;esempio evidenziato seguente:

![Intestazione di imaging intelligente](/help/assets/assets-dm/smart-imaging-header2.png)

Questa intestazione indica quanto segue:

* Smart imaging sta lavorando per l&#39;azienda.
* Un valore positivo significa che la conversione ha esito positivo. In questo caso, viene restituita una nuova immagine WebP.
* Un valore negativo significa che la conversione non ha esito positivo. In tal caso, viene restituita l’immagine richiesta originale (se non è specificato, per impostazione predefinita viene restituito JPEG).
* Un valore positivo mostra la differenza in byte tra l&#39;immagine richiesta e la nuova immagine. Nell&#39;esempio precedente, i byte salvati vengono `75048` o circa 75 KB per un&#39;immagine.
* Un valore negativo significa che l&#39;immagine richiesta è più piccola della nuova immagine. Viene visualizzata la differenza di dimensione negativa, ma l&#39;immagine servita è solo l&#39;immagine richiesta originale.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 con WebP in fase di distribuzione**
>
>Se il valore di `X-Adobe-Smart-Imaging` è -1 e WebP è ancora in fase di distribuzione, significa che Smart Imaging funziona ma i vantaggi di dimensione non sono stati calcolati a causa della vecchia cache. È possibile utilizzare `cache=update` (solo una volta) nell&#39;URL dell&#39;immagine per risolvere questo problema.
>Esempio di utilizzo del modificatore:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Per annullare la validità dell’intera cache, devi creare un caso di supporto.

## Come posso disabilitare l&#39;ottimizzazione AVIF in Smart imaging?{#disable-avif}

Se si desidera tornare al servizio WebP per impostazione predefinita, creare un caso di supporto per lo stesso. Come al solito, è possibile disattivare l’imaging avanzato aggiungendo il parametro `bfc=off` all’URL dell’immagine. Tuttavia, non è possibile selezionare WebP o AVIF nel modificatore URL per Smart imaging. Questa funzionalità viene mantenuta a livello di account aziendale.

## È possibile disattivare l&#39;imaging intelligente per qualsiasi richiesta?{#turning-off-smart-imaging}

Sì. Per disattivare l’imaging avanzato, aggiungi uno dei seguenti modificatori:

* `bfc=off` per disattivare la conversione del formato del browser. Vedi anche [Conversione del formato del browser](#bfc).
* `dpr=off` per disattivare il rapporto pixel del dispositivo. Vedi anche [Rapporto pixel dispositivo](#dpr).
* `network=off` per disattivare la larghezza di banda della rete. Vedi anche [Larghezza di banda della rete](#network).

## Quale &quot;tuning&quot; è disponibile? Esistono impostazioni o comportamenti che possono essere definiti? {#tuning-settings}

L&#39;imaging avanzato dispone di tre opzioni che è possibile abilitare o disabilitare.

* [Conversione del formato del browser](#bfc)
* [Rapporto pixel dispositivo](#dpr)
* [Larghezza di banda della rete](#network)

## Ho un URL con fmt=tif sul browser Web Chrome. Ma la mia richiesta non riesce con un errore ImageServer. Perché? {#fmt-tif}

Questo errore non si verifica se Smart imaging non è abilitato sul tuo account. La funzione Smart imaging funziona solo con i formati JPEG o PNG.

Per evitare questo errore, puoi effettuare le seguenti operazioni:

* Specificare JPEG o PNG, oppure
* Non utilizzare il `fmt` modificatore, oppure
* Utilizza un formato preferito dal browser definito da Smart imaging. Ad esempio, è possibile utilizzare WebP per il browser Web Chrome.

## Voglio scaricare un&#39;immagine di TIFF dall&#39;URL di un&#39;immagine. Come lo faccio? {#download-tif}

Aggiungi `fmt=tif` e `bfc=off` al percorso URL dell’immagine.

## La funzione Smart imaging gestisce solo il formato immagine o gestisce le impostazioni di qualità delle immagini per ottenere risultati ottimali?

La funzione Smart imaging utilizza sia il formato che la qualità. Il resto dei parametri rimane lo stesso, se richiesto nell’URL dell’immagine.

## Se Smart imaging gestisce le impostazioni di qualità, posso impostare valori minimi e massimi? In altre parole, una qualità non inferiore a 60 e non superiore a 80? {#quality-setting}

Attualmente non esiste un provisioning di questo tipo.

## La funzione Smart imaging regola automaticamente l&#39;impostazione di output della percentuale di qualità o si tratta di un&#39;impostazione regolata manualmente e applicata a tutte le immagini? Entro quale intervallo? {#percent-quality}

L&#39;imaging intelligente regola automaticamente la percentuale di qualità. Questa percentuale di qualità è determinata utilizzando un algoritmo di apprendimento automatico sviluppato per Adobe. Questa percentuale non è specifica dell&#39;intervallo.

## Con Smart imaging, quali comandi di gestione delle immagini sono supportati o ignorati? {#support-ignore}

Gli unici comandi ignorati sono `fmt` e `qlt`. Tutti i comandi rimanenti sono supportati.

## Solo le immagini JPEG sono sostituite da Smart imaging? Cosa succede se richiedo un WebP, un PNG o qualcos&#39;altro? {#replace-request}

Questa funzionalità funziona solo per JPEG e PNG.

## Perché a volte un&#39;immagine di JPEG viene restituita a Chrome invece che a WebP? {#jpeg-returned}

L’imaging intelligente determina se la conversione è utile o meno. Restituisce la nuova immagine solo della conversione è utile.

## Perché la funzionalità Device Pixel Ratio (dpr) non funziona come previsto con le immagini composite? {#composite-images}

Se un&#39;immagine composita coinvolge troppi livelli, la funzionalità dpr potrebbe essere interessata quando si utilizza un modificatore di posizione. Questo problema è noto e verrà risolto nelle future versioni di Smart imaging. Se altre funzionalità di Smart imaging non funzionano come previsto, puoi creare un caso di supporto per segnalare il problema.

## Perché lo Smart imaging PNG si converte ancora in webP/AVIF senza perdite? {#convert-to-lossless}

Poiché PNG è un formato senza perdita di dati, il WebP e l&#39;AVIF precedenti che vengono consegnati erano senza perdita di risultato è di dimensioni più elevate del previsto. La funzione Smart imaging ora supporta la conversione con perdita di dati. È possibile utilizzare il modificatore `cache=update` (solo una volta) in una richiesta di immagine per risolvere questo problema. Esempio di utilizzo del modificatore:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Per annullare la validità dell’intera cache, devi creare un caso di supporto che richieda tale sforzo.

## Come posso continuare a utilizzare il PNG per la conversione senza perdita di dati in Smart imaging? {#continue-using}

La funzione Smart imaging ora supporta la conversione con perdita di dati in base al livello di qualità. Per continuare a utilizzare la conversione senza perdita di dati, puoi utilizzare una qualità 100 impostata sia tramite l’impostazione della tua azienda sia tramite l’URL dell’immagine utilizzando `qlt=100` nel percorso.