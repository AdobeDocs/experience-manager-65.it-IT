---
title: Immagini interattive
description: Scopri come utilizzare le immagini interattive in Dynamic Media
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: Immagini interattive
role: Business Practices, amministratore
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '4335'
ht-degree: 2%

---


# Immagini interattive{#interactive-images}

È possibile rendere le immagini statiche ricche di esperienze coinvolgenti per i clienti trascinando e rilasciando punti attivi &quot;shoppable&quot; su un&#39;immagine. Gli hotspot acquistabili combinano informazioni aggiuntive su un prodotto o servizio con una funzionalità diretta, punto vendita &quot;Aggiungi al carrello&quot; o &quot;Acquista&quot;. I clienti possono toccare o fare clic su questi hotspot ed essere collegati direttamente al prodotto o al servizio, aggiungerli a un carrello o essere collegati a una pagina web. Esperienze dirette come queste aumentano il coinvolgimento e la conversione dei clienti sul tuo sito web.

Di seguito è riportato un banner acquistabile con un pop-up Quickview. Un utente attiva la visualizzazione rapida toccando il cerchio o il &quot;punto attivo&quot; sul modello.

![chlimage_1-152](assets/chlimage_1-368.png)

Vedi le immagini interattive in azione nella pagina web precedente andando al seguente:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## Guarda come vengono creati i banner immagine interattivi {#watch-how-interactive-image-banners-are-created}

Guarda una procedura dettagliata di 10 minuti e 33 secondi sulla [creazione dei banner immagine interattivi](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Scoprirai anche come visualizzare in anteprima, modificare e distribuire banner immagine interattivi.

## Avvio rapido: Immagini interattive {#quick-start-interactive-images}

La seguente descrizione dettagliata del flusso di lavoro è stata progettata per aiutarti a iniziare rapidamente a usare le immagini interattive in AEM Assets.

Cerca l&#39;intestazione **Esempio** all&#39;interno di alcune delle attività di avvio rapido. Contiene una breve esercitazione basata sul seguente esempio di pagina web che non dispone ancora di Immagini interattive aggiunte:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

L’esercitazione illustra i passaggi necessari per integrare le immagini interattive nel sito web.

Passaggi per le immagini interattive:

1. **(Facoltativo) Identificazione delle variabili dei punti attivi** : se utilizzi AEM Assets e Dynamic Media come funzionalità autonoma, inizia identificando le variabili dinamiche utilizzate nell’implementazione di Quickview esistente, in modo da poter inserire i dati dei punti attivi durante la creazione dell’immagine interattiva. Consulta [(Facoltativo) Identificazione delle variabili dei punti attivi](#optional-identifying-hotspot-variables).
Tuttavia, se utilizzi AEM Sites, eCommerce AEM o entrambi, questo passaggio non è necessario.
Vedi [Concetti di eCommerce in AEM Assets](/help/sites-administering/concepts.md).

1. **(Facoltativo) Creazione di un predefinito**  visualizzatore di immagini interattive: personalizza l’immagine grafica utilizzata per rappresentare gli hotspot. La creazione di un proprio predefinito per visualizzatori di immagini interattive non è necessaria se invece desideri utilizzare il predefinito per visualizzatori di immagini interattive preimpostato `Shoppable_Banner`.
Consulta [(Facoltativo) Creazione di un predefinito visualizzatore di immagini interattive](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Caricamento di un banner immagine**  - Carica i banner immagine che desideri rendere interattivi.
Consulta [Caricamento di un banner immagine](#uploading-an-image-banner).

1. **Aggiunta di punti attivi a un banner immagine** : aggiungi uno o più punti attivi a un banner immagine e associali ciascuno di essi a un’azione come un collegamento ipertestuale, un Quickview o un frammento esperienza. Dopo aver aggiunto gli hotspot, finirai questa attività pubblicando l&#39;immagine interattiva.

   * Consulta [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).
   * Consulta [Anteprima delle immagini interattive](#optional-previewing-interactive-images) - Facoltativo. Se lo desideri, puoi visualizzare una rappresentazione del banner acquistabile e verificarne l’interattività.
   * Per informazioni dettagliate su come pubblicare le risorse immagine interattive, consulta [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md) .

1. **Aggiunta di un’immagine interattiva al sito web o al sito web in**
AEMIse utilizzi AEM Sites, eCommerce AEM o entrambi, puoi aggiungere l’immagine interattiva direttamente a una pagina web in AEM trascinando il componente File multimediali interattivi sulla pagina. Consulta [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)
Se utilizzi AEM Assets e Dynamic Media standalone, devi copiare il codice da incorporare sul tuo sito web e quindi integrarlo con la visualizzazione rapida esistente. Consulta [Integrazione di un’immagine interattiva con il sito web](#integrating-an-interactive-image-with-your-website).
Se utilizzi un WCM di terze parti (Web Content Manager), devi integrare il nuovo video interattivo con l’implementazione Quickview esistente utilizzata sul sito web. Consulta [Integrazione di un&#39;immagine interattiva con una visualizzazione rapida esistente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Facoltativo) Identificazione delle variabili dei punti attivi {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Questa attività è necessaria solo se sono soddisfatte le seguenti condizioni:
>
>* Per aggiungere interattività all’immagine, attiva le Quickview.
>* La tua implementazione di AEM *non* utilizza un framework di integrazione eCommerce per estrarre i dati dei prodotti in AEM da qualsiasi soluzione eCommerce come IBM Websphere Commerce, Elastic Path, hybris o Intershop. Vedi [Concetti di eCommerce in AEM Assets](/help/sites-administering/concepts.md).

>
>
Se l’implementazione di AEM utilizza eCommerce, puoi saltare questa attività e passare all’attività successiva.

Per iniziare, identifica le variabili dinamiche utilizzate dall&#39;implementazione di Quickview esistente in modo da poter inserire i dati dei punti attivi per creare l&#39;immagine interattiva.

Quando aggiungi punti attivi a un&#39;immagine del banner in AEM Assets, devi assegnare un SKU (Stock Keeping Unit; un identificatore univoco per ogni prodotto o servizio distinto offerto) e variabili aggiuntive facoltative per ogni punto attivo. Tali variabili dei punti attivi vengono utilizzate in seguito per far corrispondere gli hotspot con il contenuto di Quickview.

È importante identificare correttamente il numero e il tipo di variabili da associare ai dati dei punti attivi. Ogni punto attivo aggiunto a un&#39;immagine del banner deve contenere informazioni sufficienti per identificare in modo non ambiguo il prodotto nel sistema di back-end esistente.

Esistono diversi modi per identificare un set di variabili da utilizzare per i dati dei punti attivi.

A volte può essere sufficiente consultare gli specialisti IT responsabili dell&#39;implementazione di Quickview esistente, in quanto è probabile che sappiano quale sia il set minimo di dati necessari per identificare Quickview nel sistema. Tuttavia, nella maggior parte dei casi è anche possibile analizzare semplicemente il comportamento esistente del codice front-end.

La maggior parte delle implementazioni di Quickview utilizza il seguente paradigma:

* L’utente attiva un elemento dell’interfaccia utente sul sito web. Ad esempio, facendo clic su un pulsante &quot;Quickview&quot;.
* Il sito web invia una richiesta Ajax al backend per caricare i dati o il contenuto della visualizzazione rapida, se necessario.
* I dati Quickview vengono tradotti nel contenuto in preparazione al rendering sulla pagina web.
* Infine, il codice front-end esegue il rendering visivo di tali contenuti sullo schermo.

L’approccio consiste quindi nel visitare diverse aree del sito web esistente in cui è implementata la funzione Quickview , attivare la visualizzazione rapida e acquisire l’URL Ajax inviato dalla pagina web per caricare i dati o il contenuto della visualizzazione rapida.

Normalmente non è necessario utilizzare strumenti di debug specializzati. I browser web moderni dispongono di ispettori web che svolgono un lavoro adeguato. Di seguito sono riportati alcuni esempi di browser web che includono ispettori web:

* Per visualizzare tutte le richieste HTTP in uscita in Google Chrome, premere F12 per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.
Su un Mac, premere Comando+Opzione+I per aprire il pannello Strumenti per sviluppatori, quindi fare clic sulla scheda Rete.

* In Firefox, è possibile attivare il plug-in Firebug premendo F12 e utilizzando la relativa scheda Net, oppure è possibile utilizzare lo strumento integrato Inspector e la relativa scheda Rete.
Su un Mac, premere Comando+Opzione+I per aprire il pannello Strumenti di sviluppo, quindi fare clic sulla scheda Ispettore.

Quando il monitoraggio della rete è attivato nel browser, attiva la visualizzazione rapida nella pagina.

Ora trova l&#39;URL Ajax Quickview nel registro di rete e copia l&#39;URL registrato per analisi future. Nella maggior parte dei casi, quando si attiva la visualizzazione rapida sono presenti numerose richieste inviate al server. In genere, l’URL Ajax Quickview è uno dei primi dell’elenco. Dispone di una porzione o di un percorso complesso della stringa di query e il relativo tipo MIME di risposta è `text/html`, `text/xml` o `text/javascript`.

Durante questo processo è importante visitare diverse aree del sito web, con diverse categorie di prodotti e tipi. Il motivo è che gli URL Quickview possono avere parti comuni per una determinata categoria di siti web, ma possono essere modificati solo se visiti un’area diversa del sito web.

Nel caso più semplice, l’unica parte variabile nell’URL Quickview è lo SKU del prodotto. In questo caso, il valore SKU è l’unico elemento dati necessario per aggiungere punti attivi all’immagine del banner.

Tuttavia, in casi complessi, l’URL Quickview presenta diversi elementi in aggiunta all’SKU, come ID categoria, codice colore, codice dimensione e così via. In questi casi, ogni elemento è una variabile separata nella definizione dei dati del punto attivo nella funzione immagine interattiva acquistabile in AEM Assets.

Prendi in considerazione i seguenti esempi di URL di visualizzazione rapida e le relative variabili di punti attivi risultanti:

<table>
  <tbody>
  <tr>
    <td><p>SKU singolo, trovato nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>L’unica parte variabile nell’URL è il valore del parametro della stringa query productId= ed è chiaramente un valore SKU. Pertanto, i nostri hotspot necessitano solo di campi SKU compilati con valori come <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU singolo, trovato nel percorso URL.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variabile si trova nell’ultima parte del percorso e diventa il valore SKU degli hotspot: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID categoria nella stringa query.</p> </td>
    <td><p>Gli URL registrati di Quickview includono quanto segue:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>In questo caso, l’URL contiene due parti diverse. Lo SKU viene memorizzato nel parametro <code>prodId</code> e la categoria ID<code></code> nel parametro <code>category=</code>.</p> <p>Di conseguenza, le definizioni dei punti attivi sono coppie. In altre parole, un valore SKU e una variabile aggiuntiva denominata <code>categoryId</code>. Le coppie risultanti sono le seguenti:</p>
    <ul>
      <li><p>SKU è <strong><code>305466</code></strong> e <code>categoryId</code> è <code>1100004</code>.</p> </li>
      <li><p>SKU è <strong><code>310181</code></strong> e <code>categoryId</code> è <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU è <strong><code>308706</code></strong> e <code>categoryId</code> è <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Esempio**

Puoi applicare lo stesso approccio utilizzato nei tre esempi sopra alla pagina web demo:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

La pagina web demo ha diverse miniature di prodotto, ognuna con un pulsante Quickview con etichetta &quot;See More&quot; (Vedi altro). Con lo strumento di debug del browser Web ancora attivato, fai clic su ogni pulsante e osserva gli URL registrati di Quickview. Dopo aver attivato tutti e quattro i prodotti Quickview disponibili sulla pagina, si dispone del seguente elenco di richieste Quickview effettuate al backend:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Osservando queste chiamate al server, puoi vedere che le informazioni specifiche per il prodotto sono presenti solo nel percorso della richiesta. Noterai inoltre che la stringa di query non viene utilizzata e che sono presenti due tipi distinti di parti di dati:

* Il primo tipo è Uomo o Donna. Puoi chiamare questa &quot;categoria di prodotto&quot;.
* Il secondo tipo è il nome del prodotto, ad esempio CamoPullover. Si può presumere che questo sia il prodotto SKU.

Considerate queste informazioni, l&#39;intero URL della visualizzazione rapida ha il seguente pattern:

`/datafeed/$categoryId$-$SKU$.json`

In base a tale analisi, utilizzerai `categoryId` e `SKU` per gli hotspot.

Ora puoi caricare un banner immagine e aggiungervi hotspot utilizzando la funzione di immagine interattiva acquistabile in AEM Assets.

## (Facoltativo) Creazione di un predefinito visualizzatore di immagini interattive {#optional-creating-an-interactive-image-viewer-preset}

È possibile scegliere di utilizzare il predefinito visualizzatore di immagini interattive predefinito disponibile in AEM Assets, denominato `Shoppable_Banner` . Oppure puoi creare un predefinito visualizzatore personalizzato da usare con le immagini interattive.

Quando crei un predefinito visualizzatore di immagini interattive personalizzato, puoi determinare l’aspetto degli hotspot sul banner immagine. Come parte della creazione del predefinito visualizzatore, puoi scegliere di utilizzare un grafico per punti attivi da una raccolta di immagini predefinite.

Dopo aver salvato il predefinito visualizzatore, questo viene attivato automaticamente (attivato) nella pagina dell’elenco Predefiniti visualizzatore di AEM Assets. Questa funzionalità significa che è visibile nel componente File multimediali interattivi e ogni volta che visualizzi una risorsa. Tuttavia, per *fornire *un banner interattivo con questo predefinito visualizzatore, è necessario *pubblicare *anche il predefinito visualizzatore (questo vale per i predefiniti visualizzatore personalizzati o preconfigurati).

**Per creare un predefinito visualizzatore di immagini interattive**

1. Nella barra a sinistra, tocca **[!UICONTROL Strumenti > Risorse > Predefiniti visualizzatore.]**
1. Vicino all’angolo superiore destro della pagina, tocca **[!UICONTROL Crea.]**
1. Nella finestra di dialogo Nuovo predefinito visualizzatore , digita un nome per descrivere il predefinito visualizzatore banner interattivo.

   Titolo che verrà visualizzato nella pagina dell’elenco Predefiniti visualizzatore dopo il salvataggio.

1. Nel menu a discesa Tipo di contenuti multimediali avanzati, seleziona **[!UICONTROL Immagine interattiva.]**
1. Tocca **[!UICONTROL Crea.]**
1. Nella pagina Modifica predefinito visualizzatore, tocca la scheda **[!UICONTROL Aspetto]** .
1. Effettua una delle operazioni seguenti:

   * Per caricare un’immagine del tuo punto attivo da utilizzare sulle immagini, tocca l’icona Selettore risorse . Nella pagina Seleziona contenuto , individua l’immagine del punto attivo che desideri utilizzare, selezionala, quindi tocca l’icona con il segno di spunta nell’angolo in alto a destra.
   * Per selezionare un’immagine hotspot predefinita, tocca l’icona Raccolta punti attivi . Nella palette della galleria punto attivo, toccare l&#39;immagine del punto attivo che si desidera utilizzare.

1. Vicino all’angolo superiore destro della pagina, tocca **[!UICONTROL Salva.]**

   Assicurati di pubblicare il nuovo predefinito visualizzatore.

   Consulta [Pubblicazione dei predefiniti visualizzatore aggiunti](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

   Ora puoi caricare un banner immagine.

## Caricamento di un banner immagine {#uploading-an-image-banner}

Se hai già caricato le immagini da utilizzare, passa al passaggio successivo, [Aggiunta di punti attivi a un banner immagine](#adding-hotspots-to-an-image-banner).

**Per caricare un banner immagine**

1. Carica i banner immagine che desideri rendere interattivi.

   Consulta [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

   Ora puoi aggiungere punti attivi al banner immagine; consulta l’attività successiva di seguito.

## Aggiunta di hotspot a un banner immagine {#adding-hotspots-to-an-image-banner}

Puoi aggiungere punti attivi a un banner immagine utilizzando l’editor nella pagina Gestione dei punti attivi.

Quando aggiungi degli hotspot, puoi definirli come una visualizzazione a comparsa Quickview, come un collegamento ipertestuale o un frammento esperienza.

Consulta [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorpori il visualizzatore in un Frammento esperienza. Per ovviare a questo problema, puoi utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.

Le opzioni Annulla e Ripristina, situate nell’angolo superiore destro della pagina, sono supportate durante la sessione di creazione/modifica corrente.

Al termine della creazione dell’immagine interattiva, puoi utilizzare Anteprima per vedere come verrà visualizzata ai clienti l’immagine interattiva.

Consulta [(Facoltativo) Anteprima delle immagini interattive](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando aggiungi punti attivi a un&#39;immagine in un&#39;immagine interattiva o in un banner carosello, le informazioni relative al punto attivo vengono memorizzate nella stessa posizione di metadati, relativa alla posizione dell&#39;immagine, indipendentemente dal fatto che si tratti di un&#39;immagine interattiva o di un banner carosello. Questa funzionalità consente di riutilizzare facilmente la stessa immagine, insieme ai dati del relativo punto attivo definito, in entrambi i visualizzatori.
>
>Tenere tuttavia presente che i caroselli banner supportano mappe immagine su immagini che possono contenere anche punti attivi; un&#39;immagine interattiva non lo è. Tieni presente questo se desideri creare un’immagine interattiva o un banner carosello che utilizza la stessa immagine. È possibile creare immagini interattive e banner carosello utilizzando copie separate della stessa immagine.
>
>Vedere anche [Banner carosello](/help/assets/carousel-banners.md).

>[!NOTE]
>
>Se modifichi immagini interattive con punti attivi e ritagli l’immagine, questi vengono rimossi.

**Per aggiungere punti attivi a un banner immagine**

1. Nella vista Risorse, individua il banner immagine che desideri rendere interattivo.
1. Effettua una delle operazioni seguenti:

   * Passa il puntatore sull&#39;immagine, quindi tocca **[!UICONTROL Seleziona]** (icona a forma di segno di spunta). Sulla barra degli strumenti, tocca **[!UICONTROL Modifica.]**

   * Passa il puntatore sull&#39;immagine, quindi tocca **[!UICONTROL Altre azioni]** (icona a tre punti) **[!UICONTROL > Modifica.]**

   * Toccare l’immagine per aprirla nella pagina Vista dettagli. Sulla barra degli strumenti, tocca **[!UICONTROL Modifica.]**

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Aggiungi punto attivo]** (icona a forma di dito che tocca) per aprire la pagina Gestione punti attivi.
1. Vicino all&#39;angolo superiore sinistro della pagina, tocca **[!UICONTROL Punto attivo.]**

1. Nell&#39;angolo in alto a sinistra della pagina Gestione punti attivi, tocca **[!UICONTROL Punto attivo.]**
1.  Sull’immagine, tocca la posizione in cui vuoi visualizzare il punto attivo. Se necessario, trascina il punto attivo per regolarne la posizione.
1. Aggiungi gli hotspot aggiuntivi necessari ripetendo i passaggi a e b.
1. (Facoltativo) Per eliminare un punto attivo, selezionalo sull&#39;immagine, quindi tocca **[!UICONTROL Elimina]** (icona del cestino per gli oggetti inattivi) sotto l&#39;intestazione **[!UICONTROL Punti attivi]** .

1. Nel campo di testo Nome, digitare il nome del punto attivo. Questo nome viene visualizzato anche nell’elenco a discesa Punto attivo selezionato .
1. Effettua una delle operazioni seguenti:

   * Tocca **[!UICONTROL Quickview.]**

      * Se sei un cliente AEM Sites o eCommerce, tocca o fai clic sull’icona Selettore prodotto (lente di ingrandimento) per aprire la pagina Seleziona prodotto . Tocca o fai clic sul prodotto che desideri utilizzare, quindi tocca **Seleziona **nell’angolo in alto a destra della pagina per tornare alla pagina Gestione punti attivi.
      * Se sei *non* un cliente AEM Sites o eCommerce

         * Consultare [Identificazione di variabili di punti attivi](#optional-identifying-hotspot-variables); dovrai definire queste variabili.
         * Quindi, inserisci manualmente il valore SKU. Nel campo di testo Valore SKU digitare la SKU (Stock Keeping Unit) del prodotto, che è un identificatore univoco per ogni prodotto o servizio distinto offerto. Il valore SKU inserito popola automaticamente la parte variabile del modello Quickview in modo che il sistema sappia associare il punto attivo toccato a una particolare visualizzazione rapida SKU.
         * (Facoltativo) Se nella visualizzazione rapida sono presenti altre variabili che è necessario utilizzare per identificare ulteriormente un prodotto, tocca **[!UICONTROL Aggiungi variabile generica.]** Nel campo di testo, specifica una variabile aggiuntiva. Ad esempio, `category=Mens` è una variabile aggiunta.
   * Toccare **[!UICONTROL Collegamento ipertestuale.]**

      * Se sei un cliente AEM Sites, tocca o fai clic sull’icona Selettore sito (cartella) per passare a un URL. Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine AEM Sites.
      * Se si è un cliente autonomo, nel campo di testo HREF specificare il percorso completo dell&#39;URL di una pagina Web collegata.

   Assicurati di specificare se aprire il collegamento in una nuova scheda del browser (impostazione predefinita consigliata) o nella stessa scheda.

   Per ulteriori informazioni, consulta [Utilizzo dei selettori](/help/assets/working-with-selectors.md) .

   * Tocca **[!UICONTROL Frammento esperienza.]**

      * Se sei un cliente AEM Sites, tocca o fai clic sull’icona Ricerca (lente di ingrandimento) per aprire la pagina Frammento esperienza . Tocca o fai clic sul frammento esperienza da utilizzare, quindi tocca Seleziona nell’angolo in alto a destra della pagina per tornare alla pagina Gestione punti attivi.
Consulta [Frammenti esperienza](/help/sites-authoring/experience-fragments.md).

      * Specifica la larghezza e l’altezza del frammento esperienza così come apparirà sul banner.

         >[!NOTE]
         >
         >Gli strumenti di condivisione social media in Immagine interattiva non sono supportati quando incorpori il visualizzatore in un Frammento esperienza. Per ovviare a questo problema, puoi utilizzare o creare predefiniti visualizzatore privi di strumenti per la condivisione dei social media. Questi predefiniti per visualizzatori consentono di incorporarli correttamente nei Frammenti esperienza.



1. Tocca **[!UICONTROL Salva]** per salvare il lavoro e tornare alla pagina Sfoglia.
1. Pubblica l’immagine interattiva. La pubblicazione consente di distribuire il banner tramite il cloud e genera anche codice di incorporamento se è necessario eseguire l’integrazione con un sito web di terze parti.

   Consulta [Pubblicazione di risorse](/help/assets/manage-assets.md#publishing-assets).

   Dopo aver aggiunto gli hotspot e pubblicato l&#39;immagine interattiva, ora puoi aggiungerla al tuo sito web esistente.

   Consulta [Integrazione di un’immagine interattiva con il sito web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >Se modifichi immagini interattive con punti attivi e ritagli l’immagine, i punti attivi vengono eliminati.

### (Facoltativo) Anteprima delle immagini interattive {#optional-previewing-interactive-images}

È possibile utilizzare Anteprima per vedere come si presenterà l’immagine interattiva ai clienti e per testare gli hotspot dell’immagine in modo che si comportino come previsto.

Una volta ottenuta l’immagine interattiva, puoi pubblicarla.
Consulta [Incorporamento del visualizzatore di video o immagini in una pagina Web](/help/assets/embed-code.md).
Consulta [Collegamento di URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md). Il metodo di collegamento basato su URL non è possibile se il contenuto interattivo include collegamenti con URL relativi, in particolare con le pagine AEM Sites.
Consulta [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

**Per visualizzare in anteprima le immagini interattive**

1. Nella vista Risorse, individua un’immagine interattiva esistente creata e tocca per aprirla in Anteprima.
1. Nell’elenco a discesa Contenuto, nell’angolo in alto a sinistra della pagina Anteprima, tocca **[!UICONTROL Visualizzatori.]**
1. Nell’elenco Visualizzatori, tocca **[!UICONTROL Shoppable_Banner]** o il nome del predefinito visualizzatore di immagini interattivo creato.
1. Tocca i punti attivi sull’immagine per testare le azioni associate.

## Pubblicazione delle risorse di immagini interattive {#publishing-interactive-image-assets}

Per informazioni dettagliate su come pubblicare le risorse immagine interattive, consulta [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md) .

## Integrazione di un’immagine interattiva con il sito web {#integrating-an-interactive-image-with-your-website}

Dopo aver caricato un&#39;immagine del banner, aggiunto degli hotspot all&#39;immagine e pubblicato l&#39;immagine interattiva, ora puoi aggiungerla alla pagina del tuo sito web.

Se sei un cliente di AEM Sites, puoi aggiungere l’immagine interattiva trascinando il componente File multimediali interattivi sulla pagina. Consulta [Aggiunta di risorse Dynamic Media alle pagine.](/help/assets/adding-dynamic-media-assets-to-pages.md)

Se sei un cliente AEM Assets autonomo, puoi aggiungere manualmente l’immagine interattiva al tuo sito web come descritto in questa sezione.

1. Copia il codice di incorporamento dell’immagine interattiva pubblicata.
Consulta [Incorporamento del visualizzatore di video o immagini in una pagina Web](/help/assets/embed-code.md).

1. Aggiungi il codice di incorporamento copiato nella posizione desiderata all’interno della pagina web.
Il codice di incorporamento copiato è impostato per un ambiente reattivo e dovrebbe quindi adattarsi automaticamente all’area assegnata.

**Esempio**

Utilizzo del sito web demo come esempio:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

L&#39;immagine dei tre uomini è un tag statico `IMG` :

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

L&#39;integrazione è semplice come rimuovere il tag `IMG` e sostituirlo con il codice di incorporamento copiato da AEM Assets. Puoi vedere il risultato nel seguente URL che mostra l&#39;immagine interattiva acquistabile sulla pagina con tre punti attivi di cerchio:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>A questo punto, gli hotspot sull&#39;immagine interattiva acquistabile del sito web demo sono solo a scopo di visualizzazione; non sono ancora integrati con le Quickview esistenti.

Per applicare un &quot;ritaglio&quot; a un’immagine interattiva acquistabile per un ambiente dinamico, puoi includere l’attributo di configurazione dell’immagine interattiva `ZoomView.iscommand` nel percorso, dove `ZoomView` è il componente da chiamare e `iscommand` è il comando di servizio dell’immagine &quot;ritaglia&quot; applicato.

Vedere l&#39;attributo di configurazione [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) .

Consultare [crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) Image serving command.

È ora possibile integrare l’immagine interattiva con una Quickview esistente sul sito web.

## Integrazione di un&#39;immagine interattiva con una visualizzazione rapida esistente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>Questa attività si applica solo se sei un cliente AEM Assets autonomo.

L’ultimo passaggio di questo processo consiste nell’integrazione dell’immagine interattiva con un’implementazione Quickview esistente sul sito web. Non esiste una soluzione all’integrazione che funzioni per tutti i casi. Ogni implementazione di Quickview è unica ed è necessario un approccio specifico che molto probabilmente coinvolge l&#39;assistenza di una persona IT front-end.

L&#39;implementazione di Quickview esistente rappresenta normalmente una catena di azioni correlate che avvengono sulla pagina web nel seguente ordine:

1. Un utente attiva un elemento nell’interfaccia utente del sito web.
1. Il codice front-end ottiene un URL Quickview basato sull’elemento dell’interfaccia utente attivato nel passaggio 1.
1. Il codice front-end invia una richiesta Ajax utilizzando l’URL ottenuto al passaggio 2.
1. La logica di back-end restituisce i dati o il contenuto Quickview corrispondenti al codice front-end.
1. Il codice front-end carica i dati o il contenuto di Quickview.
1. Facoltativamente, il codice front-end converte i dati Quickview caricati in una rappresentazione HTML.
1. Il codice front-end visualizza una finestra di dialogo o un pannello modale ed esegue il rendering del contenuto HTML sullo schermo per l’utente finale.

Queste chiamate potrebbero non rappresentare chiamate API pubbliche indipendenti che possono essere richiamate dalla logica della pagina web da un passaggio arbitrario. Si tratta invece di una chiamata concatenata in cui ogni passaggio successivo viene nascosto nell’ultima fase (callback) del passaggio precedente.

Allo stesso tempo, quando l&#39;immagine interattiva acquistabile sostituisce il passaggio 1 e in parte il passaggio 2, quando un utente fa clic su un punto attivo all&#39;interno dell&#39;immagine acquistabile, l&#39;interazione dell&#39;utente viene gestita dal visualizzatore. Il visualizzatore restituisce un evento alla pagina web che contiene tutti i dati del punto attivo precedentemente aggiunti ad AEM Assets.

In un tale gestore di eventi, il codice front-end effettua le seguenti operazioni:

* Ascolta un evento emesso dall&#39;immagine interattiva acquistabile.
* Crea un URL di visualizzazione rapida basato sui dati del punto attivo.
* Attiva il processo di caricamento della visualizzazione rapida dal back-end e di rendering sullo schermo per la visualizzazione.

Il codice di incorporamento restituito da AEM Assets dispone già di un gestore eventi ready-to-use che viene commentato, come mostrato nel seguente frammento di codice evidenziato:

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

Pertanto, è solo necessario rimuovere il commento dal codice e sostituire il corpo del gestore fittizio con il codice specifico per la pagina web specifica.

Il processo di costruzione dell’URL di visualizzazione rapida è sostanzialmente opposto al processo utilizzato per identificare le variabili dei punti attivi trattate in precedenza.

Consulta [Identificazione delle variabili dei punti attivi](#optional-identifying-hotspot-variables).

Utilizzando i nostri precedenti esempi di URL di visualizzazione rapida, puoi vedere negli esempi seguenti come viene costruito l’URL di visualizzazione rapida in ogni caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU singolo, trovato nella stringa query</p> </td>
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
   <td><p>SKU e ID categoria nella stringa query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

L&#39;ultimo passaggio per attivare l&#39;URL Quickview e attivare il pannello Quickview richiede molto probabilmente l&#39;assistenza di un esperto IT front-end del reparto IT. Hanno la conoscenza di sapere come attivare con precisione l&#39;implementazione di Quickview dal passaggio appropriato, avendo un URL di Quickview pronto all&#39;uso.

Puoi vedere come questi passaggi vengono applicati al sito web demo per integrare completamente un’immagine interattiva acquistabile con il codice Quickview. In precedenza, la struttura dell’URL di visualizzazione rapida era identificata come segue:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Per ricostruire questo URL all&#39;interno del gestore `quickViewActivate`, è possibile utilizzare i campi `categoryId` e `SKU` disponibili nell&#39;oggetto `inData` passato al gestore dal codice del visualizzatore:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

Il sito Web demo sta attivando la finestra di dialogo Quickview utilizzando una semplice chiamata di funzione `loadQuickView()`. Questa funzione accetta un solo argomento, ovvero l’URL dei dati Quickview. Come tale, l&#39;ultimo passaggio necessario per integrare l&#39;immagine interattiva acquistabile è quello di aggiungere la seguente riga di codice al gestore `quickViewActivate`:

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

Il sito web demo finale con l&#39;immagine interattiva completamente integrata si presenta così:

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate {#using-quickviews-to-create-custom-pop-ups}

Consulta [Utilizzo di Quickview per creare pop-up personalizzati](/help/assets/custom-pop-ups.md).
