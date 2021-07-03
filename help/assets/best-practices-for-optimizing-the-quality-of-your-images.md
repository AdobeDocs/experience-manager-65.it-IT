---
title: Best practice per ottimizzare la qualità delle immagini
description: Scopri le best practice per ottimizzare la qualità delle immagini in Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Gestione risorse
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 6%

---

# Best practice per ottimizzare la qualità delle immagini {#best-practices-for-optimizing-the-quality-of-your-images}

L&#39;ottimizzazione della qualità delle immagini può richiedere molto tempo, in quanto molti fattori contribuiscono a rendere i risultati accettabili. Il risultato è in parte soggettivo perché gli individui percepiscono la qualità dell&#39;immagine in modo diverso. La sperimentazione strutturata è fondamentale.

Adobe Experience Manager include più di 100 comandi di distribuzione delle immagini Dynamic Media per ottimizzare e ottimizzare le immagini e i risultati di rendering. Le seguenti linee guida possono essere utili per semplificare il processo e ottenere rapidamente buoni risultati utilizzando alcuni comandi e best practice essenziali.

## Best practice per il formato immagine (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG o PNG sono le scelte migliori per offrire immagini di buona qualità e con dimensioni e peso gestibili.
* Se nell’URL non viene fornito alcun comando di formato, per impostazione predefinita la consegna delle immagini Dynamic Media è impostata su JPG.
* Il formato JPG si comprime con un rapporto di 10:1 e di solito genera file di dimensioni più ridotte. PNG si comprime con un rapporto di circa 2:1, tranne a volte, ad esempio quando le immagini contengono uno sfondo bianco. In genere, tuttavia, le dimensioni dei file PNG sono maggiori dei file JPG.
* Il formato JPG utilizza la compressione con perdita di dati, ovvero gli elementi dell&#39;immagine (pixel) vengono eliminati durante la compressione. Il PNG utilizza invece la compressione senza perdita di dati.
* JPG comprime spesso immagini fotografiche con una migliore fedeltà rispetto alle immagini sintetiche con bordi netti e contrasto.
* Se le immagini contengono trasparenza, utilizza PNG perché JPG non supporta la trasparenza.

Come best practice per il formato immagine, inizia con l’impostazione più comune `&fmt=JPG`.

## Best practice per le dimensioni delle immagini {#best-practices-for-image-size}

La riduzione dinamica delle dimensioni dell&#39;immagine è una delle attività più comuni. Si tratta di specificare le dimensioni e, facoltativamente, quale modalità di downsampling viene utilizzato per ridimensionare l&#39;immagine.

* Per il dimensionamento delle immagini, l&#39;approccio migliore e più semplice consiste nell&#39;utilizzare `&wid=<value>` e `&hei=<value>,`o semplicemente `&hei=<value>`. Questi parametri impostano automaticamente la larghezza dell&#39;immagine in base alle proporzioni.
* `&resMode=<value>`controlla l’algoritmo utilizzato per il downsampling. Inizia con `&resMode=sharp2`. Questo valore offre la migliore qualità delle immagini. Quando si utilizza il downsampling `value =bilin` è più veloce, spesso si genera l&#39;aliasing degli artefatti.

Come best practice per il dimensionamento delle immagini, utilizza `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Best practice per la nitidezza delle immagini {#best-practices-for-image-sharpening}

La nitidezza delle immagini è l’aspetto più complesso del controllo delle immagini sul sito web e in cui vengono commessi molti errori. Prenditi del tempo per saperne di più sul funzionamento di nitidezza e Maschera definizione dettagli in Experience Manager, facendo riferimento alle seguenti risorse utili:

White paper sulle best practice [Nitidezza delle immagini in Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf), applicabile anche all&#39;Experience Manager.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Ad Experience Manager, puoi rendere più nitide le immagini in fase di acquisizione, consegna o entrambe. Di solito, tuttavia, le immagini vengono rese più nitide utilizzando un solo metodo o l’altro, ma non entrambi. La nitidezza delle immagini sulla consegna, su un URL, in genere fornisce i risultati migliori.

Sono disponibili due metodi di nitidezza delle immagini:

* Nitidezza semplice ( `&op_sharpen`) : simile al filtro di nitidezza utilizzato in Photoshop, la nitidezza semplice applica una nitidezza di base alla visualizzazione finale dell’immagine dopo il ridimensionamento dinamico. Tuttavia, questo metodo non è configurabile dall&#39;utente. Si consiglia di non utilizzare &amp;op_sharpen se non richiesto.
* Maschera definizione dettagli ( `&op_USM`) - Il mascheramento definizione dettagli è un filtro di nitidezza standard del settore. La migliore pratica è quella di rendere più nitide le immagini con maschera di contrasto seguendo le linee guida riportate di seguito. La funzione Maschera definizione dettagli consente di controllare i tre parametri seguenti:

   * `&op_sharpen=`importo,raggio,soglia

      * **[!UICONTROL quantità]**  (0-5, forza dell&#39;effetto).
      * **[!UICONTROL raggio]**  (0-250, larghezza delle &quot;linee di nitidezza&quot; tracciate intorno all’oggetto affilato, misurata in pixel).

      Tieni presente che il raggio e la quantità dei parametri funzionano l’uno contro l’altro. La riduzione del raggio può essere compensata dall&#39;aumento della quantità. Il raggio consente un controllo più preciso, poiché un valore inferiore rende più nitidi solo i pixel del bordo, mentre un valore più alto rende più nitida una banda più ampia di pixel.

      * **[!UICONTROL soglia]**  (0-255, sensibilità dell&#39;effetto).

             Questo parametro determina la differenza tra i pixel da rendere più nitidi rispetto all’area circostante, prima che vengano considerati pixel del bordo e che il filtro li renda più nitidi. Il parametro **[!UICONTROL soglia]** consente di evitare l’eccessiva nitidezza delle aree con colori simili, ad esempio i toni della pelle. Ad esempio, con un valore di soglia pari a 12 vengono ignorate le variazioni lievi di luminosità nell’incarnato per evitare di aggiungere “disturbo”, mentre viene aumentato il contrasto lungo i bordi delle aree dove è più presente, ad esempio tra ciglia e pelle.
         
         Per ulteriori informazioni su come impostare questi tre parametri, incluse le best practice da utilizzare con il filtro, consulta le risorse seguenti:

         Experience Manager Argomento della Guida sulla nitidezza di un’immagine.

         White paper sulle best practice [Nitidezza delle immagini in Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager consente anche di controllare un quarto parametro: monocromatico (0,1). Questo parametro determina se la maschera di contrasto viene applicata separatamente a ciascun componente di colore utilizzando il valore 0 o alla luminosità/intensità dell&#39;immagine utilizzando il valore 1.


Come best practice, inizia con il parametro del raggio della maschera di contrasto. Le impostazioni del raggio che puoi iniziare sono le seguenti:

* **[!UICONTROL Sito web]**  - 0.2-0.3 pixel
* **[!UICONTROL Stampa fotografica (250-300 ppi)]**  - 0,3-0,5 pixel
* **[!UICONTROL Stampa offset (266-300 ppi)]**  - 0,7-1,0 pixel
* **[!UICONTROL Stampa su tela (150 ppi)]**  - 1,5-2,0 pixel

Aumentare gradualmente l&#39;importo da 1,75 a 4. Se la nitidezza non è ancora quella desiderata, aumenta il raggio di un punto decimale ed esegui di nuovo il valore da 1,75 a 4. Ripeti se necessario.

Lascia l’impostazione del parametro monocromatico su 0.

### Best practice per la compressione JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Questo parametro controlla la qualità di codifica JPG. un valore più elevato significa un&#39;immagine di qualità superiore ma di grandi dimensioni; in alternativa, un valore più basso indica un&#39;immagine di qualità inferiore ma una dimensione file inferiore. L&#39;intervallo per questo parametro è compreso tra 0 e 100.
* Per ottimizzare la qualità, non impostare il valore del parametro su 100. La differenza tra un&#39;impostazione di 90 o 95 e 100 è quasi impercettibile, ma 100 aumenta inutilmente la dimensione del file di immagine. Pertanto, per ottimizzare la qualità ma evitare che i file di immagine diventino troppo grandi, imposta il valore `qlt= value` su 90 o 95.
* Per ottimizzare le dimensioni di un file immagine di piccole dimensioni ma mantenere la qualità dell&#39;immagine a un livello accettabile, impostare `qlt= value` su 80. Valori inferiori a 70-75 determinano un significativo deterioramento della qualità delle immagini.
* Come best practice, per rimanere nel mezzo, imposta il `qlt= value` su 85 per rimanere nel mezzo.
* Utilizzo del flag chroma in `qlt=`

   * Il parametro `qlt=` dispone di una seconda impostazione che consente di attivare il sottocampionamento della cromaticità RGB utilizzando il valore `,1` o disattivandolo con il valore `,0`.
   * Per renderlo semplice, inizia con il downsampling della cromaticità RGB disattivato (`,0`). Questa impostazione di solito garantisce una migliore qualità delle immagini, specialmente per le immagini sintetiche con bordi netti e contrasto elevato.

Come best practice per la compressione JPG utilizza `&qlt=85,0`.

## Best practice per il ridimensionamento JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize è un parametro utile se vuoi garantire che un&#39;immagine non superi una certa dimensione per la distribuzione su dispositivi con memoria limitata.

* Questo parametro è impostato in kilobyte (`jpegSize=&lt;size_in_kilobytes&gt;`). Definisce le dimensioni massime consentite per la distribuzione delle immagini.
* `&jpegSize=` interagisce con il parametro di compressione JPG  `&qlt=`. Se la risposta JPG con il parametro di compressione JPG specificato (`&qlt=`) non supera il valore jpegSize, l&#39;immagine viene restituita con `&qlt=` come definito. In caso contrario, `&qlt=` viene gradualmente ridotto finché l&#39;immagine non rientra nelle dimensioni massime consentite, o finché il sistema non lo determina e restituisce un errore.

Come best practice, imposta `&jpegSize=` e aggiungi il parametro `&qlt=` se distribuisci immagini JPG a dispositivi con memoria limitata.

## Riepilogo delle best practice {#best-practices-summary}

Come best practice, per ottenere un&#39;elevata qualità delle immagini e dimensioni ridotte dei file, inizia con la seguente combinazione di parametri:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Questa combinazione di impostazioni produce risultati eccellenti nella maggior parte delle circostanze.

Se l&#39;immagine richiede un&#39;ulteriore ottimizzazione, regolate gradualmente i parametri di nitidezza (Mascheramento di contrasto) iniziando con un raggio impostato su 0.2 o 0.3. Quindi, incrementate gradualmente la quantità da 1.75 a un massimo di 4 (equivalente a 400% in Photoshop). Verificare che il risultato desiderato sia raggiunto.

Se i risultati della nitidezza non sono ancora soddisfacenti, aumenta il raggio in incrementi decimali. Per ogni incremento decimale, riavviare il valore a 1,75 e incrementarlo gradualmente a 4. Ripetere questo processo fino a ottenere il risultato desiderato. Anche se i valori di cui sopra sono un approccio convalidato dagli studi creativi, ricorda che puoi iniziare con altri valori e seguire altre strategie. Che i risultati siano soddisfacenti o meno è una questione soggettiva, quindi la sperimentazione strutturata è fondamentale.

Durante l’esperimento, i seguenti suggerimenti generali possono essere utili per ottimizzare ulteriormente il flusso di lavoro:

* Prova e verifica parametri diversi in tempo reale, direttamente su un URL.
* Come best practice, ricorda che puoi raggruppare i comandi di Dynamic Media Image Serving in un predefinito per immagini. Un predefinito per immagini è fondamentalmente macro di comando URL con nomi predefiniti personalizzati come `$thumb_low$` e `&product_high$`. Il nome predefinito personalizzato in un percorso URL chiama questi predefiniti. Tali funzionalità consentono di gestire i comandi e le impostazioni di qualità per diversi schemi di utilizzo delle immagini sul sito web e di ridurre la lunghezza complessiva degli URL.
* Experience Manager offre inoltre modalità più avanzate per ottimizzare la qualità delle immagini, ad esempio applicando la nitidezza delle immagini durante l’acquisizione. Per i casi d&#39;uso avanzati in cui sono disponibili opzioni per ottimizzare e ottimizzare i risultati di rendering, [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) può essere utile con informazioni personalizzate e best practice.
