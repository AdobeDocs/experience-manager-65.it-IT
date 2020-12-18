---
title: Immagini interattive
description: Scoprite come lavorare con le immagini interattive in Dynamic Media
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '4330'
ht-degree: 2%

---


# Immagini interattive{#interactive-images}

Potete rendere le immagini statiche ricche di immagini e creare esperienze coinvolgenti per i clienti trascinando e rilasciando punti di attivazione &quot;shoppable&quot; su un’immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o un servizio con una funzionalità &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot; diretta, punto vendita. I clienti possono toccare o fare clic su questi punti di attivazione ed essere collegati direttamente al prodotto o al servizio, aggiungerli a un carrello o essere collegati a una pagina Web. Esperienze dirette come queste aumentano il coinvolgimento e la conversione dei clienti sul sito Web.

Di seguito è riportato un banner acquistabile con una finestra a comparsa Quickview. Un utente attiva la visualizzazione rapida toccando il cerchio o il punto di attivazione del modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Per vedere le immagini interattive in azione sulla pagina Web precedente, effettuate le seguenti operazioni:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## Scoprite come creare i banner immagine interattivi {#watch-how-interactive-image-banners-are-created}

Guardate la procedura dettagliata di 10 minuti e 33 secondi su [come vengono creati i banner immagine interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Inoltre verrà illustrato come visualizzare in anteprima, modificare e distribuire i banner immagine interattivi.

## Avvio rapido: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata creata per consentirvi di imparare a usare rapidamente le immagini interattive in  AEM Assets.

Cercare l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di Avvio rapido. Contiene una breve esercitazione basata sul seguente esempio di pagina Web in cui non sono ancora state aggiunte immagini interattive:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

Questa esercitazione illustra i passaggi necessari per integrare le immagini interattive nel sito Web.

Passaggi Immagini interattive:

1. **(Facoltativo) Identificazione delle variabili**  dei punti di attivazione: se utilizzate  standalone AEM Assets e Dynamic Media, iniziate identificando le variabili dinamiche utilizzate nell’implementazione esistente di Quickview in modo da poter inserire i dati dei punti di attivazione al momento della creazione dell’immagine interattiva. Vedere [(facoltativo) Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables).
Tuttavia, se utilizzi  AEM Sites, AEM eCommerce o entrambi, questo passaggio non è necessario.
Vedere [Concetti di eCommerce in  AEM Assets](/help/sites-administering/concepts.md).

1. **(Facoltativo) Creazione di un predefinito**  per visualizzatori di immagini interattive - Personalizzare l’immagine grafica utilizzata per rappresentare i punti attivi. La creazione di un predefinito per visualizzatori di immagini interattive non è necessaria se intendete utilizzare il predefinito per visualizzatori di immagini interattive preimpostato denominato `Shoppable_Banner`.
Consultate [(facoltativo) Creazione di un predefinito per visualizzatori immagini interattivi](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Caricamento di un banner**  immagine - Caricamento dei banner immagine da rendere interattivi.
Consultate [Caricamento di un banner immagine](#uploading-an-image-banner).

1. **Aggiunta di punti attivi a un banner**  di immagini: aggiunta di uno o più punti attivi a un banner di immagini e associazione di ciascuno ad un&#39;azione come un collegamento ipertestuale, una visualizzazione rapida o un frammento esperienza. Dopo aver aggiunto i punti di attivazione, questa attività verrà completata pubblicando l&#39;immagine interattiva.

   * Consultate [Aggiunta di punti di attivazione a un banner di immagine](#adding-hotspots-to-an-image-banner).
   * Consultate [Anteprima delle immagini interattive](#optional-previewing-interactive-images) - Facoltativo. Se necessario, potete visualizzare una rappresentazione del banner acquistabile e verificarne l’interattività.
   * Consultate [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

1. **Aggiunta di un’immagine interattiva al sito Web o al sito Web in**
AEMIse utilizzate  AEM Sites, AEM eCommerce, o entrambi, potete aggiungere l’immagine interattiva direttamente a una pagina Web in AEM trascinando il componente Supporto interattivo sulla pagina. Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)
Se utilizzate  standalone AEM Assets e Dynamic Media, dovete copiare il codice da incorporare sul vostro sito Web e quindi integrarlo con la visualizzazione rapida esistente. Consultate [Integrazione di un&#39;immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).
Se utilizzate un WCM di terze parti (Web Content Manager), dovete integrare il nuovo video interattivo con l’implementazione esistente di Quickview utilizzata sul vostro sito Web. Consultate [Integrazione di un&#39;immagine interattiva con una visualizzazione rapida esistente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Facoltativo) Identificazione delle variabili dei punti di attivazione {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività all’immagine, attivate l’opzione Visualizzazioni rapide.
>* L&#39;implementazione di AEM non utilizza *un* framework di integrazione eCommerce per estrarre i dati di prodotto in AEM da qualsiasi soluzione di eCommerce come IBM Webferfera Commerce, Elastic Path, hybris o Intershop. Vedere [Concetti di eCommerce in  AEM Assets](/help/sites-administering/concepts.md).

>
>
Se l&#39;implementazione di AEM utilizza eCommerce, puoi saltare questa attività e passare all&#39;attività successiva.

Per iniziare, identificate le variabili dinamiche utilizzate dall’implementazione esistente di Quickview in modo da poter inserire i dati dei punti di attivazione per creare l’immagine interattiva.

Quando aggiungete punti di attivazione a un&#39;immagine del banner in  AEM Assets, dovete assegnare un SKU (Stock Keeping Unit); un identificatore univoco per ciascun prodotto o servizio distinto offerto) e variabili aggiuntive facoltative per ciascun punto di attivazione. Tali variabili per i punti di attivazione vengono successivamente utilizzate per far corrispondere i punti di attivazione con il contenuto della visualizzazione rapida.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti di attivazione. Ogni punto di attivazione aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo univoco il prodotto nel sistema di back-end esistente.

Esistono diversi modi per identificare un insieme di variabili da utilizzare per i dati dei punti di attivazione.

A volte può essere sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview, in quanto è probabile che sappiano quale sia il set minimo di dati necessario per identificare Quickview nel sistema. Tuttavia, nella maggior parte dei casi è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, facendo clic su un pulsante &quot;Quickview&quot;.
* Il sito Web invia una richiesta Ajax al back-end per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati della visualizzazione rapida vengono convertiti nel contenuto in preparazione del rendering sulla pagina Web.
* Infine, il codice front-end esegue visivamente il rendering di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito Web esistente in cui è implementata la funzione Quickview, attivare la visualizzazione rapida e acquisire l’URL Ajax inviato dalla pagina Web per caricare i dati o il contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser Web moderni dispongono di ispettori Web che eseguono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser Web che includono ispettori Web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzare la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Ispettore e la relativa scheda Rete.
In Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attivare la visualizzazione rapida sulla pagina.

Ora trova l’URL Ajax di Quickview nel registro di rete e copia l’URL registrato per l’analisi futura. Nella maggior parte dei casi, quando si attiva la visualizzazione rapida, vengono inviate al server numerose richieste. In genere, l’URL Ajax della visualizzazione rapida è uno dei primi nell’elenco. Dispone di una porzione o di un percorso di una stringa di query complessa e il tipo MIME della risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo è importante visitare diverse aree del sito Web, con diverse categorie e tipi di prodotti. Il motivo è che gli URL di visualizzazione rapida possono avere parti comuni per una determinata categoria di sito Web, ma possono essere modificati solo se visitate un’area diversa del sito Web.

Nel caso più semplice, l’unica parte variabile dell’URL di visualizzazione rapida è lo SKU del prodotto. In questo caso, il valore SKU è l’unico dato necessario per aggiungere aree sensibili all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta elementi diversi oltre allo SKU, come ID categoria, codice colore, codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto di attivazione nella funzione di immagine interattiva acquistabile in  AEM Assets.

Considerate i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti di attivazione:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa di query.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile dell’URL è il valore del parametro della stringa di query productId= ed è chiaramente un valore SKU. Pertanto, i nostri punti di attivazione richiedono solo campi SKU compilati con valori quali <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso dell’URL.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU dei punti di attivazione: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa di query.</p> </td>
    <td><p>Gli URL della visualizzazione rapida registrati includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU è memorizzato nel parametro <code>prodId</code> e la categoria ID<code></code> è memorizzata nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni dei punti di attivazione sono coppie. ovvero un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Potete applicare lo stesso approccio utilizzato nei tre esempi riportati sopra alla pagina Web della demo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

La pagina Web della demo contiene diverse miniature di prodotto, ognuna delle quali presenta un pulsante di visualizzazione rapida con l&#39;etichetta &quot;Ulteriori informazioni&quot;. Con lo strumento di debug del browser Web ancora attivato, fate clic su ciascun pulsante e prendete nota degli URL di visualizzazione rapida registrati. Dopo aver attivato tutte e quattro le quickview del prodotto disponibili sulla pagina, è disponibile il seguente elenco di richieste Quickview effettuate sul back-end:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Osservando queste chiamate al server, le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Si noti inoltre che la stringa di query non viene utilizzata e che sono coinvolti due tipi distinti di dati:

* Il primo tipo è Uomo o Donna. Puoi chiamare questa &quot;categoria di prodotti&quot;.
* Il secondo tipo è il nome del prodotto, ad esempio CamoPullover. Potete presumere che questo sia lo SKU del prodotto.

Considerate queste informazioni, l’intero URL di Quickview presenta il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, per i punti di attivazione si utilizzerebbero `categoryId` e `SKU`.

È ora possibile caricare un banner immagine e aggiungervi degli hotspot tramite la funzione per immagini interattive acquistabile in  AEM Assets.

## (Facoltativo) Creazione di un predefinito per visualizzatori immagini interattivi {#optional-creating-an-interactive-image-viewer-preset}

Potete scegliere di utilizzare il predefinito per visualizzatori di immagini interattive predefinito, denominato `Shoppable_Banner` fornito con  AEM Assets. Oppure potete creare un predefinito per visualizzatori personalizzato da usare con immagini interattive.

Quando create un predefinito per visualizzatori di immagini interattive personalizzato, potete determinare l’aspetto dei punti attivi nel banner immagine. Come parte della creazione del predefinito per visualizzatori, potete scegliere di usare un elemento grafico per punti di attivazione da una raccolta di immagini predefinite.

Dopo aver salvato il predefinito per visualizzatori, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefiniti visualizzatore  AEM Assets. Questa funzionalità significa che è visibile nel componente Contenuti multimediali interattivi e ogni volta che visualizzate una risorsa. Tuttavia, per *fornire *un banner interattivo con questo predefinito per visualizzatori, dovete anche *pubblicare *il predefinito per visualizzatori (vale per i predefiniti per visualizzatori personalizzati o forniti con Scene7).

**Per creare un predefinito per visualizzatori immagini interattivi**

1. Nella barra a sinistra, toccate **[!UICONTROL Strumenti > Risorse > Predefiniti visualizzatore.]**
1. Vicino all&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Crea.]**
1. Nella finestra di dialogo Nuovo predefinito per visualizzatori, digitate un nome per descrivere il predefinito per visualizzatori per banner interattivi.

   Titolo che verrà visualizzato nella pagina dell’elenco Predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva.]**
1. Toccare **[!UICONTROL Crea.]**
1. Nella pagina Modifica predefinito per visualizzatori, toccate la scheda **[!UICONTROL Aspetto]**.
1. Effettua una delle operazioni seguenti:

   * Per caricare un’immagine del punto di attivazione che desiderate usare sulle immagini, toccate l’icona del selettore delle risorse. Nella pagina Seleziona contenuto, individuate l’immagine del punto di attivazione da usare, selezionatela, quindi toccate l’icona con il segno di spunta nell’angolo superiore destro.
   * Per selezionare un&#39;immagine per un punto di attivazione predefinito, toccate l&#39;icona Galleria punti di attivazione. Nella palette della galleria del punto di attivazione, toccate l’immagine del punto di attivazione che desiderate usare.

1. Nell&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Salva.]**

   Accertatevi di pubblicare il nuovo predefinito per visualizzatori.

   Consultate [Pubblicazione dei predefiniti per visualizzatori aggiunti](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   È ora possibile caricare un banner immagine.

## Caricamento di un banner immagine {#uploading-an-image-banner}

Se avete già caricato le immagini che desiderate usare, passate al passaggio successivo, [Aggiunta di punti di attivazione a un banner di immagine](#adding-hotspots-to-an-image-banner).

**Per caricare un banner immagine**

1. Caricate i banner immagine da rendere interattivi.

   Consultate [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

   È ora possibile aggiungere punti di attivazione al banner immagine; consulta l’attività successiva di seguito.

## Aggiunta di punti attivi a un banner di immagine {#adding-hotspots-to-an-image-banner}

Potete aggiungere punti attivi a un banner di immagini utilizzando l&#39;editor nella pagina Gestione dei punti attivi.

Quando aggiungete degli hotspot, potete definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Vedere [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.

Le opzioni Annulla e Ripristina, accanto all’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell’immagine interattiva, potete usare Anteprima per vedere in che modo l’immagine interattiva verrà visualizzata ai clienti.

Consultate [(facoltativo) Anteprima delle immagini interattive](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando aggiungete punti di attivazione a un’immagine in un’immagine interattiva o in un banner carosello, le informazioni relative ai punti di attivazione vengono memorizzate nella stessa posizione di metadati, relativa alla posizione dell’immagine, indipendentemente dal fatto che si tratti di un’immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati dei punti di attivazione definiti, in entrambi i visualizzatori.
>
>Tenete presente, tuttavia, che i banner carosello supportano le mappe immagine sulle immagini che possono anche contenere punti di attivazione; un’immagine interattiva non lo è. Tenete presente questo aspetto se intendete creare un&#39;immagine interattiva o un banner carosello che utilizza la stessa immagine. È possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
>
>Vedere anche [Carosello Banner](/help/assets/carousel-banners.md).

>[!NOTE]
>
>Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono rimossi.

**Per aggiungere punti attivi a un banner di immagine**

1. Nella vista Risorse, individuate il banner immagine da rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Passate il puntatore del mouse sull&#39;immagine, quindi toccate **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, toccare **[!UICONTROL Modifica.]**

   * Passa il puntatore del mouse sull&#39;immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica.]**

   * Toccate l’immagine per aprirla nella pagina Visualizzazione dettagli. Sulla barra degli strumenti, toccare **[!UICONTROL Modifica.]**

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Aggiungi punto attivo]** (icona a forma di dito che tocca) per aprire la pagina Gestione punti attivi.
1. Vicino all&#39;angolo superiore sinistro della pagina, toccare **[!UICONTROL Punto attivo.]**

1. Vicino all&#39;angolo superiore sinistro della pagina Gestione punti attivi, toccare **[!UICONTROL Punto attivo.]**
1.  Sull’immagine, tocca la posizione in cui vuoi visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione.
1. Se necessario, potete aggiungere altri punti di attivazione ripetendo i passaggi a e b.
1. (Facoltativo) Per eliminare un punto di attivazione, selezionatelo sull&#39;immagine, quindi toccate **[!UICONTROL Elimina]** (icona cestino) sotto l&#39;intestazione **[!UICONTROL Punti attivi]**.

1. Nel campo di testo Nome, digitate il nome del punto di attivazione. Questo nome viene visualizzato anche nell&#39;elenco a discesa Area sensibile selezionata.
1. Effettua una delle operazioni seguenti:

   * Toccate **[!UICONTROL Quickview.]**

      * Se siete un cliente  AEM Sites o eCommerce, toccate o fate clic sull&#39;icona del selettore prodotto (lente di ingrandimento) per aprire la pagina Selezione prodotto. Toccate o fate clic sul prodotto che desiderate utilizzare, quindi toccate **Select ** nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dei punti attivi.
      * Se si è *not* un cliente AEM Sites o eCommerce 

         * Vedere [Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables); sarà necessario definire queste variabili.
         * Quindi, immettete manualmente il valore SKU. Nel campo di testo Valore SKU, digitare lo SKU del prodotto (Stock Keeping Unit), che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU immesso popola automaticamente la porzione variabile del modello Quickview, in modo che il sistema sia in grado di associare il punto attivo toccato a una particolare visualizzazione Quickview dello SKU.
         * (Facoltativo) Se all&#39;interno della visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, toccare **[!UICONTROL Aggiungi variabile generica.]** Nel campo di testo, specificate una variabile aggiuntiva. Ad esempio, `category=Mens` è una variabile aggiunta.
   * Toccare **[!UICONTROL Collegamento ipertestuale.]**

      * Se siete clienti AEM Sites , toccate o fate clic sull&#39;icona Selettore sito (cartella) per passare a un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.
      * Se siete clienti indipendenti, nel campo HREF specificate il percorso completo dell’URL di una pagina Web collegata.

   Accertatevi di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, vedere [Utilizzo dei selettori](/help/assets/working-with-selectors.md).

   * Toccate **[!UICONTROL Frammento esperienza.]**

      * Se siete un cliente AEM Sites , toccate o fate clic sull’icona di ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza. Toccate o fate clic sul frammento esperienza che desiderate utilizzare, quindi toccate Seleziona nell&#39;angolo superiore destro della pagina per tornare alla pagina di gestione dell&#39;area sensibile.
Vedere [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

      * Specificate la larghezza e l&#39;altezza del frammento esperienza così come apparirà sul banner.

         >[!NOTE]
         >
         >Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorporate il visualizzatore in un frammento esperienza. Per ovviare a questo problema, potete usare o creare predefiniti per visualizzatori privi di strumenti per la condivisione social media. Tali predefiniti per visualizzatori consentono di incorporarli correttamente nei frammenti esperienza.



1. Toccate **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblicate l’immagine interattiva. La pubblicazione consente la distribuzione del banner tramite cloud e la generazione del codice da incorporare se è necessario effettuare l’integrazione con un sito Web di terze parti.

   Consultate [Pubblicazione di risorse](/help/assets/manage-assets.md#publishing-assets).

   Dopo aver aggiunto degli hotspot e pubblicato l’immagine interattiva, potete ora aggiungerla al sito Web esistente.

   Consultate [Integrazione di un&#39;immagine interattiva con il sito Web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Se modificate immagini interattive con punti attivi e ritagliate l’immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima delle immagini interattive {#optional-previewing-interactive-images}

Potete usare Anteprima per vedere l’aspetto dell’immagine interattiva per i clienti e per verificare i punti di attivazione dell’immagine in modo che si comportino come previsto.

Una volta ottenuta l’immagine interattiva, potete pubblicarla.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/embed-code.md).
Consultate [Collegamento di URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo contiene collegamenti con URL relativi, in particolare con collegamenti alle pagine  AEM Sites.
Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

**Per visualizzare in anteprima le immagini interattive**

1. Nella vista Risorse, individuate un’immagine interattiva esistente creata e toccate per aprirla in Anteprima.
1. Vicino all&#39;angolo superiore sinistro della pagina Anteprima, nell&#39;elenco a discesa Contenuto, toccate **[!UICONTROL Visualizzatori.]**
1. Nell’elenco Visualizzatori, toccate **[!UICONTROL Shoppable_Banner]** o il nome del predefinito per visualizzatori di immagini interattivo creato.
1. Toccate i punti di attivazione sull&#39;immagine per verificare le azioni associate.

## Pubblicazione di risorse di immagine interattive {#publishing-interactive-image-assets}

Consultate [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md) per informazioni dettagliate sulla pubblicazione di risorse di immagini interattive.

## Integrazione di un&#39;immagine interattiva con il sito Web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, aggiunto dei punti di attivazione all&#39;immagine e pubblicato l&#39;immagine interattiva, potete ora aggiungerla alla pagina del sito Web.

Se siete un cliente AEM Sites , potete aggiungere l’immagine interattiva trascinando il componente Supporto interattivo sulla pagina. Consultate [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Se siete clienti indipendenti  AEM Assets, potete aggiungere manualmente l’immagine interattiva al sito Web come descritto in questa sezione.

1. Copiate il codice da incorporare dell’immagine interattiva pubblicata.
Consultate [Incorporamento del visualizzatore video o di immagini in una pagina Web](/help/assets/embed-code.md).

1. Aggiungete il codice da incorporare copiato nella posizione desiderata all’interno della pagina Web.
Il codice da incorporare copiato è impostato per un ambiente reattivo e dovrebbe quindi adattarsi automaticamente all&#39;area assegnata.

**Esempio**

Esempio di utilizzo del sito Web demo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

L&#39;immagine dei tre uomini è un tag statico `IMG`:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L&#39;integrazione è semplice come rimuovere il tag `IMG` e sostituirlo con il codice da incorporare copiato da  AEM Assets. Potete visualizzare il risultato nel seguente URL che mostra l’immagine interattiva acquistabile sulla pagina con tre punti di attivazione cerchio:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>A questo punto, i punti di attivazione sull&#39;immagine interattiva acquistabile del sito Web demo sono solo a scopo di visualizzazione; non sono ancora integrati con le viste Quickview esistenti.

Per applicare un &quot;ritaglio&quot; a un&#39;immagine interattiva acquistabile per un ambiente reattivo, potete includere l&#39;attributo di configurazione immagine interattiva `ZoomView.iscommand` nel percorso, dove `ZoomView` è il componente da chiamare e `iscommand` è il comando di trasmissione delle immagini &quot;ritagliato&quot; applicato.

Vedere [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) attributo di configurazione.

Vedere [ritaglio](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) comando di gestione delle immagini.

È ora possibile integrare l’immagine interattiva con una visualizzazione rapida esistente sul sito Web.

## Integrazione di un&#39;immagine interattiva con una visualizzazione rapida esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Questa attività si applica solo se siete clienti  AEM Assets indipendenti.

L’ultimo passaggio di questo processo consiste nell’integrare l’immagine interattiva con un’implementazione esistente di Quickview sul sito Web. Non esiste una soluzione all&#39;integrazione che funzioni per tutti i casi. Ogni implementazione di Quickview è univoca ed è necessario un approccio specifico che molto probabilmente coinvolga l&#39;assistenza di una persona IT front-end.

L’implementazione esistente di Quickview rappresenta in genere una catena di azioni correlate che si verificano sulla pagina Web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito Web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al punto 2.
1. La logica di back-end restituisce i dati o il contenuto della visualizzazione rapida corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto della visualizzazione rapida.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l&#39;utente finale.

Queste chiamate potrebbero non rappresentare chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina Web da un passaggio arbitrario. Si tratta, invece, di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Contemporaneamente alla sostituzione dell’immagine interattiva acquistabile con il passaggio 1 e in parte il passaggio 2, quando un utente fa clic su un punto di attivazione all’interno dell’immagine acquistabile, tale interazione viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina Web che contiene tutti i dati del punto attivo precedentemente aggiunti a  AEM Assets.

In un tale gestore di eventi, il codice front-end esegue le seguenti operazioni:

* Ascolta un evento emesso dall&#39;immagine interattiva acquistabile.
* Crea un URL di visualizzazione rapida basato sui dati del punto di attivazione.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering della visualizzazione sullo schermo.

Il codice da incorporare restituito da  AEM Assets dispone già di un gestore eventi ready-to-use impostato come commento, come illustrato nel frammento di codice evidenziato seguente:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo fittizio del gestore con il codice specifico per la pagina Web specifica.

Il processo di creazione dell’URL di visualizzazione rapida è sostanzialmente opposto a quello utilizzato per identificare le variabili dei punti di attivazione trattate in precedenza.

Vedere [Identificazione delle variabili dei punti di attivazione](#optional-identifying-hotspot-variables).

Utilizzando i nostri precedenti esempi di URL di Quickview, potete vedere negli esempi seguenti in che modo l’URL di Quickview è costruito in ogni caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU singolo, trovato nella stringa di query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU singolo, trovato nel percorso URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID categoria nella stringa di query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

L’ultimo passaggio per attivare l’URL di visualizzazione rapida e attivare il pannello di visualizzazione rapida richiede probabilmente l’assistenza di un esperto IT front-end del reparto IT. Essi hanno la capacità di sapere come attivare con precisione l’implementazione della visualizzazione rapida dal passaggio corretto, avendo un URL Quickview pronto all’uso.

Potete vedere come questi passaggi vengono applicati al sito Web dimostrativo per integrare completamente un’immagine interattiva acquistabile con il codice Quickview. In precedenza, la struttura dell’URL di Quickview era identificata come segue:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire questo URL all&#39;interno del gestore `quickViewActivate`, è possibile utilizzare i campi `categoryId` e `SKU` disponibili nell&#39;oggetto `inData` passato al gestore dal codice del visualizzatore:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web dimostrativo sta attivando la finestra di dialogo Quickview utilizzando una semplice chiamata di funzione `loadQuickView()`. Questa funzione richiede un solo argomento, ovvero l&#39;URL dei dati di Quickview. Come tale, l&#39;ultimo passaggio necessario per integrare l&#39;immagine interattiva acquistabile è quello di aggiungere la seguente riga di codice al gestore `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

Di seguito è riportato il codice sorgente completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

Il sito Web dimostrativo finale con l&#39;immagine interattiva completamente integrata si presenta come segue:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

Vedere [Uso delle visualizzazioni rapide per creare pop-up personalizzati](/help/assets/custom-pop-ups.md).
