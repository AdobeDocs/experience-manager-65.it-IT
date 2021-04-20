---
title: Smart imaging
description: La tecnologia di imaging intelligente applica le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management
role: Business Practitioner, Administrator
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
translation-type: tm+mt
source-git-commit: 8d27457ad88cb84e670e78bab4c40da36fcfc629
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 2%

---


# Imaging avanzato {#smart-imaging}

## Cos’è l’imaging intelligente? {#what-is-smart-imaging}

La tecnologia Smart Imaging applica le funzionalità di Adobe Sensei AI e funziona con i &quot;predefiniti immagine&quot; esistenti per migliorare le prestazioni di distribuzione delle immagini ottimizzando automaticamente il formato, le dimensioni e la qualità delle immagini in base alle funzionalità del browser client.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata (Content Delivery Network) inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

L’imaging intelligente trae inoltre vantaggio dal miglioramento delle prestazioni dell’integrazione completa con il servizio CDN premium di Adobe. Questo servizio trova il percorso Internet ottimale tra server, reti e punti di peer. Trova un percorso che ha la latenza più bassa e la velocità di perdita più bassa del pacchetto invece di utilizzare il percorso predefinito su Internet.

Gli esempi di risorse immagine seguenti illustrano l’ottimizzazione Smart Imaging aggiunta:

| Immagine<br>(URL) | Miniatura  | Dimensione<br> (JPEG) | Dimensione (WebP)<br> (con Smart imaging) | Riduzione del % |
|---|---|---|---|---|
| [Immagine 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Immagine 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Immagine 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Immagine 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![immagine4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Media = 51% |

Simile a quanto sopra, Adobe ha anche eseguito un test con 7009 URL dai siti dei clienti live. Sono stati in grado di raggiungere una media del 38% in più di ottimizzazione delle dimensioni del file per JPEG. Per PNG con formato WebP, sono stati in grado di raggiungere una media di 31% ulteriore ottimizzazione delle dimensioni del file. Questo tipo di ottimizzazione è possibile grazie alla capacità di Smart imaging.

## Quali sono i vantaggi principali dell&#39;ultima generazione di Smart imaging? {#what-are-the-key-benefits-of-smart-imaging}

Poiché le immagini costituiscono la maggior parte del tempo di caricamento di una pagina, il miglioramento delle prestazioni può avere un impatto profondo su un&#39;azienda, come una conversione più elevata, il tempo trascorso sul sito e un tasso di mancato recapito del sito inferiore.

Miglioramenti all&#39;ultima versione di Smart imaging:

* È stata migliorata la classificazione SEO di Google per le pagine web che utilizzano le più recenti Smart imaging.
* Distribuisce immediatamente i contenuti ottimizzati (in fase di esecuzione).
* Utilizza la tecnologia Adobe Sensei per convertire in base alla qualità (qlt) specificata nella richiesta di immagine.
* L&#39;imaging avanzato può essere disattivato utilizzando il parametro URL &quot;bfc&quot;.
* TTL (Time To Live) indipendente. Precedentemente, per il funzionamento di Smart imaging era obbligatorio un TTL minimo di 12 ore.
* Precedentemente, sia le immagini originali che quelle derivate venivano memorizzate nella cache ed era un processo in due fasi per annullare la validità della cache. Nell’ultimo Smart imaging, solo i derivati vengono memorizzati nella cache, consentendo un processo di invalidazione della cache a un solo passaggio.
* I clienti che utilizzano intestazioni personalizzate nel loro set di regole beneficiano dell’ultima Smart imaging, in quanto queste intestazioni non sono bloccate, a differenza della versione precedente di Smart imaging. Ad esempio, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot; come suggerito in [Aggiunta di un valore di intestazione personalizzato alle risposte alle immagini|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Esistono costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. La funzione Smart imaging è inclusa nella licenza esistente di Dynamic Media Classic o Adobe Experience Manager - Dynamic Media (On-Prem, AMS e Adobe Experience Manager as a Cloud Service).

>[!NOTE]
>
>La funzione Smart imaging non è disponibile per i clienti ibridi di Dynamic Media.

## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Quando un&#39;immagine viene richiesta da un consumatore, Smart imaging controlla le caratteristiche dell&#39;utente e la conversione nel formato immagine appropriato in base al browser in uso. Queste conversioni di formato vengono effettuate in modo da non compromettere la fedeltà visiva. La funzione Smart imaging converte automaticamente le immagini in formati diversi in base alla funzionalità del browser nel modo seguente.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* Converti automaticamente in WebP per i seguenti browser:
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari (su iOS, macOS, iPadOS), supporto per la versione del browser e del sistema operativo WebP
   * Android™
   * Opera
* Supporto di browser legacy per i seguenti elementi:

   | Browser | Versione browser/sistema operativo | Formato |
   | --- | --- | --- |
   | Safari | Precedente a iOS/iPad 14.0 o macOS BigSur | JPEG2000 |
   | Bordo | Anteriore a 18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Per i browser che non supportano questi formati, viene distribuito il formato immagine richiesto originariamente.

Se la dimensione dell&#39;immagine originale è inferiore a quella prodotta da Smart imaging, l&#39;immagine originale viene servita.

## Quali formati immagine sono supportati? {#what-image-formats-are-supported}

I seguenti formati immagine sono supportati per Smart imaging:

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Come funziona l’imaging avanzato con i miei predefiniti immagine esistenti già in uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart imaging funziona con i &quot;predefiniti immagine&quot; esistenti ed osserva tutte le impostazioni dell&#39;immagine eccetto la qualità (`qlt`) e il formato (`fmt`) se il formato file richiesto è JPEG o PNG. Per la conversione del formato, l&#39;imaging intelligente mantiene la fedeltà visiva completa, come definita dalle impostazioni del predefinito per immagini, ma con dimensioni file inferiori. Se le dimensioni originali dell&#39;immagine sono inferiori a quelle prodotte da Smart imaging, l&#39;immagine originale viene servita.

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Devo modificare URL, predefiniti per immagini o distribuire un nuovo codice sul mio sito per Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

La funzione Smart Imaging funziona direttamente con gli URL delle immagini esistenti e i predefiniti per immagini se configuri Smart Imaging sul dominio personalizzato esistente. Inoltre, Smart imaging non richiede di aggiungere codice sul sito web per rilevare il browser di un utente. Viene gestito tutto automaticamente.

Se devi configurare un nuovo dominio personalizzato per l’utilizzo di Smart imaging, gli URL devono essere aggiornati per riflettere questo dominio personalizzato.

Per comprendere i prerequisiti per l’imaging intelligente, consulta [Posso utilizzare l’imaging avanzato?](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## L’imaging avanzato funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

Smart imaging funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Sono idoneo all’utilizzo di imaging intelligente? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare Smart imaging, l’account Dynamic Media Classic o Dynamic Media della tua azienda deve soddisfare i seguenti requisiti:

* Utilizza la rete CDN (Content Delivery Network) in bundle Adobe come parte della tua licenza.
* Utilizza un dominio dedicato (ad esempio, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ad esempio, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendali.

Tocca **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**. Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato]**. Se utilizzi un dominio generico, puoi richiedere il passaggio al dominio personalizzato come parte di questa transizione quando invii un ticket di assistenza tecnica.

Il tuo primo dominio personalizzato non comporta costi aggiuntivi con una licenza Dynamic Media.

## Qual è il processo per abilitare Smart imaging per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Avviate la richiesta di utilizzare l&#39;imaging intelligente; non è abilitato automaticamente.

1. [Utilizza l’Admin Console per creare un caso di supporto.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   1. Nome contatto principale, e-mail, telefono.
   1. Tutti i domini da abilitare per l’imaging intelligente (ovvero `images.company.com` o `mycompany.scene7.com`).

      Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendali.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato.]**
   1. Verifica di utilizzare la CDN tramite Adobe e di non gestirla con una relazione diretta.
   1. Verifica di utilizzare un dominio dedicato come `images.company.com` o `mycompany.scene7.com` e non un dominio generico, ad esempio `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account aziendali.

      Fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**.

      Cerca il campo con etichetta **[!UICONTROL Nome server pubblicato]**. Se utilizzi un dominio generico Dynamic Media Classic, puoi richiedere il passaggio al dominio personalizzato come parte di questa transizione.
   1. Indica se è anche necessario utilizzare l’imaging intelligente per utilizzare HTTP/2.

1. L’Assistenza clienti di Adobe ti aggiunge all’elenco di attesa del cliente Smart imaging in base all’ordine in cui sono state inviate le richieste.
1. Quando Adobe è pronto per gestire la richiesta, è necessario contattare il supporto per coordinare e impostare una data di destinazione.
1. **Facoltativo**: Facoltativamente, puoi testare l’imaging intelligente in Staging prima che Adobe introduca la nuova funzione in produzione.
1. Dopo il completamento, riceverai una notifica dall’Assistenza clienti.
1. Per ottimizzare le prestazioni dell’imaging avanzato, Adobe consiglia di impostare il valore TTL (Time To Live) a 24 ore o più. Il TTL definisce per quanto tempo le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzi Dynamic Media Classic, fai clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni pubblicazione > Image Server]**. Imposta il valore **[!UICONTROL Default Client Cache Time To Live]** su 24 o più a lungo.
   1. Se utilizzi Dynamic Media, segui [queste istruzioni](config-dynamic.md). Imposta il valore **[!UICONTROL Scadenza]** su 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con Smart imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti, in base all’Elenco di attesa.

>[!NOTE]
>
>Ci può essere un lungo tempo di lead perché l’abilitazione di Smart imaging comporta ad Adobe la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni dei clienti in un dato momento.

## Quali sono i rischi connessi al passaggio all’app per l’utilizzo di Smart imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Non vi è alcun rischio per una pagina web del cliente. Tuttavia, la transizione a Smart Imaging cancella la cache alla rete CDN perché implica il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media all’Experience Manager.

Durante la transizione iniziale, le immagini non memorizzate nella cache colpiscono direttamente i server di origine di Adobe fino a quando la cache non viene ricostruita nuovamente. Di conseguenza, Adobe pianifica di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili durante l’estrazione delle richieste dall’origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente nella rete CDN entro circa 1 - 2 giorni.

## Come posso verificare se l&#39;imaging intelligente funziona come previsto?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato l&#39;account con l&#39;imaging intelligente, carica un URL immagine Dynamic Media Classic o Adobe Experience Manager - Dynamic Media sul browser.
1. Apri il riquadro per sviluppatori di Chrome facendo clic su **[!UICONTROL Visualizza > Sviluppatore > Strumenti di sviluppo]** nel browser. Oppure, scegli uno strumento per sviluppatori di browser a tua scelta.

1. Assicurati che la cache sia disabilitata quando gli strumenti per sviluppatori sono aperti.

   * In Windows®, accedi alle impostazioni nel riquadro degli strumenti per sviluppatori, quindi seleziona la casella di controllo **[!UICONTROL Disattiva cache (mentre devtools è aperto)]**.
   * In macOS, nel riquadro dello sviluppatore, sotto la scheda **[!UICONTROL Rete]**, selezionare **[!UICONTROL disabilita cache]**.

1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra un&#39;immagine PNG convertita dinamicamente in WebP su Chrome.
1. Ripeti questo test su diversi browser e condizioni utente.

>[!NOTE]
>
>Non tutte le immagini vengono convertite. L’imaging intelligente decide se la conversione può migliorare le prestazioni. A volte, quando non si prevede alcun guadagno di prestazioni o il formato non è JPEG o PNG, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## È possibile disattivare l&#39;imaging intelligente per qualsiasi richiesta? {#turning-off-smart-imaging}

Sì. Per disattivare l’imaging avanzato, aggiungi il modificatore `bfc=off` all’URL.

## Quale &quot;tuning&quot; è disponibile? Esistono impostazioni o comportamenti che possono essere definiti? (#tuning-settings)

Attualmente, è possibile abilitare o disabilitare l&#39;imaging avanzato. Nessun&#39;altra sintonizzazione disponibile.

## Se Smart imaging gestisce le impostazioni di qualità, è necessario impostare valori minimi e massimi? Ad esempio, è possibile impostare &quot;non inferiore a 60&quot; e &quot;non superiore a 80 qualità&quot;? (#minimum-maximum)

L&#39;attuale Smart imaging non è in grado di effettuare il provisioning.

## A volte, un&#39;immagine JPEG viene restituita a Chrome invece di un&#39;immagine WebP. Perché? (#jpeg-webp)

L’imaging intelligente determina se la conversione è utile o meno. Restituisce la nuova immagine solo se la conversione si traduce in una dimensione file più piccola con qualità comparabile.
